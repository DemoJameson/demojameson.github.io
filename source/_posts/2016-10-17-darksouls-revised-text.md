title: 黑暗之魂受死版繁体中文文本校正补丁
tags:
  - darksouls
  - 黑暗之魂
  - 受苦
  - 传火
  - MOD
categories:
  - 游戏
author: DemoJameson
date: 2016-10-17 15:12:00
updated: 2016-10-17 15:12:03
---
{% asset_img darksouls_dlc_pk.jpeg %}
# 简介

首先黑魂标点符号参差不齐显示效果比较糟心，然后又到处加多余的逗号句号，于是我就做了这个补丁解决这些问题。

<!--more-->

# 具体改动

| **改动的内容**          | **改动后**                                  |
| ------------------ | ---------------------------------------- |
| 省略号……              | 缩小为…                                     |
| 会话中的逗号句号           | 半角空格                                     |
| 其它文本行末的逗号句号        | 删除（包含另外两个版本，一个是不做处理，一个是全部文本中的逗号句号都替换成空格） |
| 各种斜杠╱／/            | 统一用 /                                    |
| 各种加号＋+             | 统一用 +                                    |
| 全角ＨＰ               | 半角 HP                                    |
| 希芙                 | 希夫                                       |
| PRESS START BUTTON | 按下 START 鍵                               |
| NEW GAME           | 開始遊戲                                     |
| LOAD GAME          | 繼續遊戲                                     |
| 篝火传送地点底部几个地名前的空格   | 删除                                       |
| 出血、中毒等提示最前面的感叹号    | 删除                                       |

# 预览

| **改动前**                                  | **改动后**                                  |
| ---------------------------------------- | ---------------------------------------- |
| {% asset_img before1.png %} | {% asset_img after1.png %} |
| {% asset_img before2.jpeg %} | {% asset_img after2.jpeg %} |
| {% asset_img before3.png %} | {% asset_img after3.png %} |

# 下载

包含三个版本，分别为是否删除行末逗号句号和替换全文逗号句号为空格，请根据自己的喜好使用。建议和[黑暗之魂繁体中文文字高清 MOD](/2016/10/17/darksouls-hd-text/) 搭配，效果更佳。

链接: https://pan.baidu.com/s/1DBGeBBiJX3eh1kgVfd55Wg 提取码: cvvu

# 使用说明

1. 打开游戏 exe 文件所在目录，备份 dvdbnd3.bdt 和 dvdbnd3.bhd5 文件，以备出现问题还原
2. 选择自己喜欢的修改版本覆盖源文件
3. 打开游戏受苦

# 如何自己制作补丁

## 工具

- [Alexandria](https://github.com/Burton-Radons/Alexandria?utm_source=cowlevel) 用来查看黑魂的资源文件（非必须）
- [BND File Rebuilder](http://wulf2k.ca/consoles/PS3/DeS/DeS-BNDBuild-2016-04-16-01.rar?utm_source=cowlevel) 用来解包打包黑魂的资源文件
- [darksouls2_texttool](http://zenhax.com/viewtopic.php?f=12&t=1933&utm_source=cowlevel#p11229) 用来将包含文本内容的 fmg 文件与 txt 文件互转

## 步骤

1. 用 BND File Rebuilder 解包 dvdbnd3.bhd5 文件得到 dvdbnd3.bhd5.extract 目录
2. 进入 dvdbnd3.bhd5.extract\msg\TCHINESE 目录，继续用 BND File Rebuilder 解包 item.msgbnd.dcx 和 menu.msgbnd.dcx 得到 item.msgbnd 和 menu.msgbnd
3. 还是用 BND File Rebuilder 解包 item.msgbnd 和 menu.msgbnd 得到 item.msgbnd.extract 和 menu.msgbnd.extract 目录
4. 运行 darksouls2_export.exe 工具，选择 dvdbnd3.bhd5.extract\msg\TCHINESE 目录得到 TCHINESE.txt 文件
5. 修改 TCHINESE.txt 文件，注意中文得用繁体而且不能增删行数
6. 运行 darksouls2_import.exe 先选择 TCHINESE.txt 文件，接着选择 dvdbnd3.bhd5.extract\msg\TCHINESE 用于将修改的文本打包回去
7. 反过来来操作 1、2、3 步，使用 BND File Rebuilder 按照顺序分别选择 item.msgbnd、menu.msgbnd、item.msgbnd.dcx、menu.msgbnd.dcx、dvdbnd3.bhd5 进行打包
8. 完成