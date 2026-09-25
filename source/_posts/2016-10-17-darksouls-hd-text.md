title: 黑暗之魂受死版繁体中文文字高清 MOD
date: 2016-10-17 14:42:03
updated: 2016-10-17 14:42:03
tags:
- darksouls
- 黑暗之魂
- 受苦
- 传火
- MOD
categories:
- 游戏
---
{% asset_img darksouls_firelink_shrine.jpeg %}
# 简介

最近在 [@莫伊图拉](https://cowlevel.net/people/moyitula)‍ 的安利下开始了魂一的受苦之旅并借助 [DSfix](https://github.com/PeterTh/dsfix?utm_source=cowlevel) 打上了一系列的 MOD，其中有个很受欢迎的[界面文字与会话对白高清 MOD](http://www.nexusmods.com/darksouls/mods/21/?&utm_source=cowlevel) 能够很好的提升玩家的游戏体验，不过该 MOD 对繁体中文的支持不太好，只有界面文字得到了调整并且许多文字有污点（位图字体没对准所致）。在打完小隆德四天王后我的忍耐达到了极限（你这不怎么看道具说明和对白的人有什么要忍耐的←_←），遂对位图字体进行重绘做出了此 MOD。

<!--more-->

# 预览

## 界面文字对比
|            | **改动前**                                  | **改动后**                                  |
| ---------- | ---------------------------------------- | ---------------------------------------- |
| **界面文字对比** | {% asset_img interface_text_before.png %} | {% asset_img interface_text_after.png %} |
| **会话文字对比** | {% asset_img subtitle_before.png %} | {% asset_img subtitle_after.png %} |

# 下载

包含 [GitHub 新版 DSfix](https://steamcommunity.com/app/211420/discussions/0/392184522702551585?utm_source=cowlevel)（增加预加载纹理材质文件的功能以及修复自动备份功能）和 MOD 本体
链接: https://pan.baidu.com/s/1DBGeBBiJX3eh1kgVfd55Wg 提取码: cvvu

# 使用说明

1. 解压所有文件到 DARKSOULS.exe 所在的目录

2. 打开 DSfix.ini 并将以下两个参数修改为你游戏中的分辨率

   ```
   renderWidth  3840
   renderHeight 2160
   ```

3.  打开游戏进入设置界面关闭抗锯齿，不然加载存档时游戏会报错

4. 开始受苦

根据我制作 MOD 时的瞌睡程度有可能出现错字、污点、缺字等等问题，反馈时麻烦告知是界面字体还是会话字体并且出现在何处，感谢配合。

# 制作历程

首先 DSfix 提供了导出纹理材质文件的功能，从中找出需要修改的位图字体文件。字体文件分成界面字体和会话字体两类，这两类字体我在重绘时分别选择了新细明体和标楷体两种与原来十分相似的字体，并且将界面字体中出现的日文异体字替换成正常的字形（如原字体中的**道**字走之底是两点，因为日文与繁体中文使用的是同一套字体），而会话字体我在参照原字体进行描边处理后发现在游戏中缩放后会有白色的斑点，所以最终我取消了描边。

找到字体文件后下一步就是将图片中的文本提取出来，借助[在线 OCR 服务](http://www.onlineocr.net/?utm_source=cowlevel)或者 [OCR 软件](http://www.abbyy.cn/finereader/?utm_source=cowlevel)还有直接从 [Unicode 编码表](http://unicode-table.com/cn?utm_source=cowlevel)中复制等手段可以完成该工作。

最后则是用 Photoshop 将原字体图片放大 4 倍，然后把准备好的文本铺上去调整每个文字的位置使其和原图一致，大功告成！（总共三十几张图，很惭愧，就做了一点微小的工作）

# MOD 与插件推荐

下面是我在用的一些 MOD 和插件，个人感觉可以提高游戏体验并且不会造成游戏卡顿，请根据个人喜好下载安装：

- [游戏场景高清材质包](http://www.nexusmods.com/darksouls/mods/446/?&utm_source=cowlevel)
- [SweetFX HDR](http://www.nexusmods.com/darksouls/mods/289/?&utm_source=cowlevel) 游戏画面效果增强插件，与上一个 MOD 是同一个作者建议配套使用，我比较喜欢其中的 Natural and Soft 风格效果。游戏中可按 **Scroll Lock **键开启 / 关闭效果
- [魂三界面 MOD](http://www.nexusmods.com/darksouls/mods/1107/?&utm_source=cowlevel)，使用中文语言进行游戏的话需要将 40fbc4ad.dds 文件改名为 8fdc74b1.dds 不然手柄按钮高清图将不起作用
- [联机增强插件](http://www.nexusmods.com/darksouls/mods/1047/?&utm_source=cowlevel) 提高连接上其他玩家的几率与个数，并且可以方便与特定玩家联机（后者我还没尝试过）
- [开始界面的 Logo 动画](http://www.nexusmods.com/darksouls/mods/585/?&utm_source=cowlevel)，篝火加配乐十分融洽
- 取用网上的 GIF 动画制作了 [Artorias](http://steamcommunity.com/sharedfiles/filedetails/?id=356583468&utm_source=cowlevel) 和 [Nito](http://steamcommunity.com/sharedfiles/filedetails/?id=217494524&utm_source=cowlevel) 的 Loding 动画以及原动画去污点版（与字体 MOD 同一下载地址）
- 自制的[繁体中文文本校正补丁](/2016/10/17/darksouls-revised-text/)，调整了标点符号和修复一些明显的错误