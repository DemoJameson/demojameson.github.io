title: 搭建使用 Hexo 的些许经验
date: 2015-11-26 04:43:47
updated: 2015-11-29 13:55:52
tags:
- Blog
- Hexo
categories:
- 博客
---

{% asset_img hexo-logo.png %}

</br>

Hexo 的搭建的确挺方便的，然而使用过程中却是遇到了不少问题，这里就权当记录了。

<!--more-->

### 解决 GitHub Pages 的 302 转向问题
之前使用的是根域名 `demojameson.com`，设置 Swiftype 后发现一直无法抓取到内容。添加 sitemap.xml 添加 robot.txt 等办法通通无效后，[几经搜索才发现是 302 问题](http://theo.im/blog/2014/05/14/resolve-302-redirection-on-github-pages/)。所以还是老老实实按照 [GitHub 的建议使用二级域名了](https://help.github.com/articles/about-custom-domains-for-github-pages-sites/#subdomains)。

### 文章中的 title 注意转义
写 [[译] 为什么 Kotlin 是我下一门要使用的语言](/2015/11/08/why-kotlin/)这篇文章时发现 title 添加 [] 符号后就无法 Generate 了。因为开头这部分被称为 [Front-matter](https://hexo.io/zh-cn/docs/front-matter.html)，使用 YAML 格式记录文章的数据，某些符号需要转义时使用单引号框住即可正常工作。

### 同时兼顾本地编辑时图片的预览以及网页的正常显示
Markdown 中引用网络上绝对地址的图片即可，可[使用七牛云存储当图床](http://yotuku.cn/)。

不过最终我还是选择了直接将文章中的图片上传到 GitHub 中（本地编辑无法预览图片），如果文章中图片使用的是相对路径需要[进行一些变动](https://hexo.io/docs/asset-folders.html)

### 百度无法抓取 GitHub Pages 内容的问题
GitHub 禁止了百度的爬虫，[解决方法挺多](http://jerryzou.com/posts/feasibility-of-allowing-baiduSpider-for-Github-Pages/)，一箭双雕的方案是同时部署到 GitHub 以及 GitCafe，[通过 DNSPod 将国内线路解析到 GitCafe](http://godera.org/2015/03/16/Mac%E4%B8%8B%E7%A8%8B%E5%BA%8F%E5%91%98%E5%8D%9A%E5%AE%A2%E4%B9%8BHexo-GitHub-Pages-GitCafe-Pages-DNSPod/)。然并卵，百度可以抓取到 sitemap，抓取诊断也没有问题，但是索引量依旧是零，哈哈哈哈~

```
# _config.yml 文件同时部署到 GitHub 与 GitCafe 的配置
deploy:
  type: git
  message: [message]
  repo:
    github: <repository url>,[branch]
    gitcafe: <repository url>,[branch]
```

### 从根域名自动跳转到 www 子域名
GitHub 会帮你自动跳转，但是 GitCafe 需要自己到域名解析服务商设置，可用 DNSPod 的显性转发功能（域名托管 30 天后才可使用该功能）

### 插件推荐
* [hexo-browsersync](https://github.com/hexojs/hexo-browsersync) 本地调试时修改文章后可在浏览器马上看到效果
* [hexo-deployer-git](https://github.com/hexojs/hexo-deployer-git) 配置好后可以很方便的更新文章到 GitHub Pages
* [hexo-generator-sitemap](https://github.com/hexojs/hexo-generator-sitemap) 在网站根目录生成 sitemap.xml 方便搜索引擎抓取

### 更新历史
* 2015 年 11 月 26 日 - 初稿
* 2015 年 11 月 28 日 - 添加百度无法抓取 GitHub Pages 内容的问题、从根域名自动跳转到 www 子域名
* 2015 年 11 月 29 日 - 百度索引量依旧是零
