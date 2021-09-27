title: 游戏《死亡细胞 Dead Cells》道具敌人关卡速查表
tags: [dead cells, javascript]
categories: 游戏
author: DemoJameson
date: 2017-05-21 01:03:00 
updated:  2017-12-25 23:39:00 
---

{% asset_img cover.jpg %}

给《[死亡细胞](http://store.steampowered.com/app/588650/Dead_Cells/)》这个游戏做了个速查表页面，数据来自游戏内解包的文件，[点击直达](http://www.demojameson.com/deadcells/dead-cells-data.html?lang=zh)（需要等待一会加载数据）。

<!--more-->

# 简介

>欢迎来到《[死亡细胞](http://store.steampowered.com/app/588650/Dead_Cells/)》，这是一款将 Roguelite 与银河战士恶魔城类特点融为一炉的 2D 平台动作游戏。游戏中并无检查点，玩家将体验魂味战斗，一路挑战诸多守卫，在杀戮与死亡的反复轮回中探索一座房间不断变化的巨大城堡。

游戏在 5 月 10 日发售后立马获得了好评如潮的评价。虽然目前还是[抢先体验](http://store.steampowered.com/earlyaccessfaq/?snr=1_5_9_)状态，但已经有了较为不错的官方中文支持，因为有谜之声和 indienova 的协助汉化。游戏凭借精美的像素风，畅快的打击感，多样的武器和技能再加上 Roguelike 元素，让人百玩不厌。

# 速查表

在花了几天通关（目前只有 11 个不同关卡，两个 BOSS）和收集所有道具后，我尝试挖掘更多的信息，通过 [QuickBMS](https://forum.xentax.com/viewtopic.php?f=10&t=16244) 将游戏里的 res.pak 文件解包得到了一些有趣的东西。其中包括描述道具敌人关卡的数据，相关的图标，以及不同语言的文本。于是我将其整理了一下，写了个简单的网页来展示这些信息，充当游戏的速查表。可以了解到游戏道具的掉落率，从何处掉落，关卡的难度级别，掉落物品级别等内容。

# 相关工具
1. [res.pak 文件解包工具](https://forum.xentax.com/viewtopic.php?f=10&t=16244)
2. [语言文件格式 mo 转换为 po](http://tools.konstruktors.com/)
3. [data.crd 数据预览工具](http://castledb.org/)，使用前需先将 data.crd 文件中的 `"typeStr": "17"` 批量替换为 `"typeStr": "8"`


# 更新

* 2017年6月3日——更新到游戏版本 ([e2c7b364](https://steamcommunity.com/app/588650/discussions/4/2741975115066406458/#c1291817837623809239))~~，但是解包的资源中没有未编译的文本文件了，所以以后新增的内容只能显示原文法文~~
* 2017年6月4日——增加 Loading 界面；裁剪压缩数据文件提高加载速度（3MB 变 100KB）
* 2017年6月5日——找到获取文本的方法了，未翻译内容显示英文；添加词缀/附魔列表；添加搜索高亮关键字功能
* 2017年6月7日——更新到 [2017-06-05B (e118994b)](http://steamcommunity.com/app/588650/discussions/4/2741975115066406458/#c1291817837635692966) 版本
* 2017年12月25日——更新到 [2017-12-22 (4a8c1404c)](steam://openurl_external/http://store.steampowered.com/news/externalpost/steam_community_announcements/2284879949510879205) 版本，添加开发过程中使用的相关工具说明