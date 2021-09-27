title: 在 OpenShift 上免费搭建 Ghost 博客的过程
date: 2015-08-09 20:49:11
tags:
- Blog
- Ghost
categories:
- 博客
---

{% asset_img ghost.png %}

### Ghost 简介
>Ghost 是一个基于 Node.js 的开源博客平台，由前 WordPress UI 部门主管 John O’Nolan 和 WordPress 开发人员 Hannah Wolfe 创立，目的是为了给用户提供一种更加纯粹的内容写作发布平台。

Ghost 简单轻量部署快，后台使用具备预览功能的 Markdown 编辑器进行写作，这些就是我选择它的原因。（下面提及的 Bug 还没修复，所以现在改用 Hexo 了 —— [Ghost 博客一览请点击](http://ghost.demojameson.com)

<!--more-->

### 搭建过程

主要参考了[《使用 Nitrous.IO+OpenShift 免费搭建 Ghost 博客》](http://hjc.im/free-ghost-blog-openshift-guide/)这篇文章，下面就将搭建的过程简单的记录一下，说说遇到的坑以及解决方法。


1. 注册 [OpenShift](https://www.openshift.com/)使用其提供的免费服务搭建 Ghost Blog。

2. 注册 [nitrous.io](https://www.nitrous.io/)，该服务提供了一个在线的 Linux 开发环境，稍后需要使用这个环境安装 Ghost 和配置。注册后创建 Node.js IDE 时需要通过手机短信进行验证，经测试中国移动的号码无法使用免费的方案，遂借用 [Heywire](http://www.heywire.com/) 这个手机应用（获得虚拟的美国号码，免费接收短信）完成了验证。

3. 使用 [nitrous.io](https://www.nitrous.io/) 的 Node.js IDE 环境搭建 Ghost Blog：
  * 安装 rhc 工具（OpenShift 的客户端工具）：`sudo gem install rhc`
  * 初始化 rhc 工具：`rhc setup`（按照提示输入用户名密码）
  * 安装 Ghost Blog：`rhc app create ghost nodejs-0.10 mysql-5.1 --env NODE_ENV=production --from-code https://github.com/openshift-quickstart/openshift-ghost-quickstart.git`（该语句中的 ghost 以及下文 rhc 命令中的 ghost 同为 OpenShift 中的应用名，可自行更改为其它内容）

4. 这时已经可以通过`http://ghost-用户名.rhcloud.com`连接访问 Ghost Blog 了，但是由于众所周知的原因 OpenShift 很可能被墙了，这时候就得通过自定义域名来绕过围墙：
  * 在 OpenShift 中自定义域名：`rhc alias add ghost [你自己的域名]`
  * 在 DNS 服务商处，将对应域名的 CNAME 记录指向 `ghost-用户名.rhcloud.com`
  * 在 nitrous 中打开 `ghost/config.js` 文件，将 `'http://'+process.env.OPENSHIFT_APP_DNS` 替换为 `'http://[你的域名]'`

5. 使用 CDN 加速访问（非必须）：
  * 不知为何无法使用 [Incapsula](https://www.incapsula.com/) 服务，获取不到我的 IP，所以选择了 [Cloudflare](https://www.cloudflare.com/)。
  * 经测试国内访问[Cloudflare](https://www.cloudflare.com/)速度也不够快，考虑备案然后使用国内的 CDN 服务。
6. 也是因为众所周知的原因，需要替换 Google Font 使用 360 CDN 提供的字体库，打开 `ghost/content/themes/[主题]/default.hbs` 文件，搜索`fonts.googleapis.com`全部替换为`fonts.useso.com`

7. 参考[《解决 Ghost 中 gravatar 被墙不能显示的问题》](http://www.kisshc.com/ghost-gravatar/)，数据库相关信息可在 OpenShift 中找到：

        mysql -u [数据库用户名] -p -D [数据库名称]
        Enter password:[数据库密码]
        select image from users where email = "your email address";
        update users set image = "//去掉www的Gravatar地址" where email = "your email address";

8. 主题安装：

        cd ~/ghost/content/themes/
        git clone [git地址]
可能需要为 git 设置默认的用户名以及邮箱，下载完主题后需删除目录下的 .git 目录以及 .gitignore，以免稍后无法应用更新。

9. 添加~~[多说](http://duoshuo.com/)~~（试用多说过程中弹出了广告）[Disqus](https://disqus.com)评论区以及 [Swiftype](https://swiftype.com/) 站内搜索的代码可以放置在后台`Setting -> Code Injection`中，不必修改主题。以下是我修改过的多说脚本（请将 short_name 改为自己的）：
```javascript
<!-- 多说公共JS代码 start (一个网页只需插入一次) -->
<script type="text/javascript">
    var s = document.createElement("section");
    s.className = "post-comments";
    s.innerHTML = '<div class="ds-thread" data-thread-key="' + location.pathname.replace(/\//g,"") + '" data-title="'+ document.title +'" data-url="' + location.href.replace(/^https/, "http") + '"></div>';
    document.querySelector(".post-container").parentNode.appendChild(s);
    var duoshuoQuery = {short_name:"xxxxxxxxx"};
    (function() {
        var ds = document.createElement('script');
        ds.type = 'text/javascript';ds.async = true;
        ds.src = (document.location.protocol == 'https:' ? 'https:' : 'http:') + '//static.duoshuo.com/embed.js';
        ds.charset = 'UTF-8';
        (document.getElementsByTagName('head')[0]
         || document.getElementsByTagName('body')[0]).appendChild(ds);
    })();
</script>
<!-- 多说公共JS代码 end -->
```

10. 更新应用，在 nirtous 中做的所有更改均需通过 git 同步到 OpenShift 中，使用以下命令即可：
```
    cd ~/ghost
    git add .
    git commit -m "[随便输入什么内容]"
    git push
```
    等待更新成功提示出现：`remote: Deployment completed with status: success`

11. 开始写作，通过网址`http://[你的域名]/ghost`初始化博客，设置管理员账号密码，然后进入后台写作以及配置

### 未解之谜
* 尝试配置[七牛云存储](https://github.com/Minwe/qn-store)后无法启动 Ghost -_-
* 尝试在  cloudflare 中使用 page rule 功能使 `demojameson.com` 跳转到 `www.demojameson.com` ~~失败，转而使用 [wwwizer](http://wwwizer.com/naked-domain-redirect) 实现该功能~~，两个域名均需在 cloudflare 中添加 CNAME 记录，在 OpenShift 中添加 Alias
* 有序列表中插入代码块会扰乱顺序，使用8 个空格的缩进又不能指定代码高亮，心好累……原来是个已知 [Bug](https://github.com/TryGhost/Ghost/issues/5632)
{% asset_img ghost-markdown-bug.png %}

### 参考资料
1. [使用 Nitrous.IO+OpenShift 免费搭建 Ghost 博客](http://hjc.im/free-ghost-blog-openshift-guide/)
1. [简单实现 Ghost 独立博客的 QQ 空间、新浪微博和人人网分享按钮](http://hjc.im/ghost-share-qzone-weibo-renren/)
2. [解决 Ghost 中 gravatar 被墙不能显示的问题](http://www.kisshc.com/ghost-gravatar/)
3. [绑定 GoDaddy 域名到 OpenShift 应用](http://www.cnblogs.com/russellluo/p/3363209.html)
4. [用 Prism 给 Ghost 添加代码高亮](http://www.denpe.com/prism-ghost-code-highlight/)
5. [Ghost 博客平台：安装多说, Disqus](http://www.applecho.com/ghost-duoshuo-disqus/)
6. [使用 Swiftype 完成 Ghost 搜索功能](http://blog.erguotou.me/ghost-swiftype-guide/)
