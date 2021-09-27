title: Genymotion 安装记 —— 曾经最快的 Android 模拟器
date: 2015-12-15 17:42:03
updated: 2015-12-16 15:33:05
tags:
- 安卓
- Android
- bug
- genymotion
categories:
- 编程
---
{% asset_img genymotion-cover.png %}
<br>
> Genymotion —— 曾经最快的 Android 模拟器，简单，实用，高效。
>
> Android Studio 2.0 之后版本自带的模拟器已经够用了，前提是你用的 Intel CPU

<!--more-->

### 下载
[注册](https://www.genymotion.com)之后才能之后才能[下载](https://www.genymotion.com/#!/download)，根据是否集成 VirtualBox 有两种版本可供选择。

### 安装
- 一路 Next 即可。如果是集成了 VirtualBox 的版本，安装过程中会弹出 VirtualBox 的安装界面
- 推荐在 IDE 里安装相应的 Genymotion 插件以便直接打开模拟器，具体安装说明请看[下载页面](https://www.genymotion.com/#!/download)

### 使用
运行 Genymotion 后先登陆，然后添加下载需要使用的镜像，接着点击 Start 运行模拟器就 OK 了。OK 个大头鬼，接着我就遇到了点问题：
1. 运行后弹错误提示 balabala 的，然后我打开 VirtualBox 查看详细信息，具体错误信息没有记录下来。Google 一发后没有找到解决方案，我就将 VirtualBox 从 5.0.4 升级到 5.0.10。
2. 可惜还是不能运行，不过错误信息变成了 `Unable to load R3 module`，从网络中找到了[解决方案](http://tieba.baidu.com/p/3369724797)，大意是因为破解了 uxtheme.dll 文件所以出错了云云，借用工具将其还原即可
3. 今天开机又出现刚一开始的错误了：
    ```
       The virtual machine 'Custom Phone - 4.1.1 - API 16 - 768x1280' has terminated unexpectedly during startup with exit code -1073741819 (0xc0000005).
       
       返回代码:    E_FAIL (0x80004005)
       组件:        MachineWrap
       界面:        IMachine {f30138d4-e5ea-4b3a-8858-a059de4c93fd}
    ```
    经过搜索发现是 Mactype 的锅，也就表明一开始升级 VirtualBox 并不能解决问题，正确的姿势应该是将 VirtualBox 的相关进程从 Mactype 中排除，将以下内容添加到配置文件中：
    ```
    [UnloadDll]
    VBoxSVC.exe
    VirtualBox.exe
    ```

### 更新记录
* 2015 年 12 月 15 日 - 发布
* 2015 年 12 月 16 日 - 添加 Mactype 导致的错误描述以及解决方案
* 2017 年 03 月 26 日 - 不推荐 Genymotion，建议使用新版 Android Studio 自带的模拟器