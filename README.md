# 上古卷轴5 Skyrim SE / AE Mod 安装教程 2026 基础篇

> 由 B 站预览稿《上古卷轴5 mod安装教程 指南 2024 (基础篇)》整理更新为 2026 年 GitHub 版。  
> 核对时间：2026-05-25。Bethesda、SKSE、Nexus 页面都可能继续变化，实际安装前请再看一次对应下载页的版本说明。

## 2026 快速结论

2026 年新入坑，最省心的路线是：Steam 正版英文版 Skyrim Special Edition / Anniversary Edition + Mod Organizer 2 + SKSE AE 当前版 + 只安装支持你游戏运行时版本的 Mod。

| 路线 | 游戏运行时 | SKSE | 适合谁 |
| --- | --- | --- | --- |
| Steam AE / SE 当前版 | `1.6.1170` | [SKSE 2.2.6 AE build](https://skse.silverlock.org/) | 2026 年新装推荐 |
| GOG AE 当前版 | `1.6.1179` | [SKSE 2.2.6 GOG build](https://skse.silverlock.org/) | GOG 用户 |
| 旧 SE 版 | `1.5.97` | [SKSE 2.0.20 SE build](https://skse.silverlock.org/) | 只为兼容老整合、老 DLL Mod |

如果 Bethesda 又更新了游戏：先不要急着更新，等 [SKSE](https://skse.silverlock.org/)、[Address Library](https://www.nexusmods.com/skyrimspecialedition/mods/32444) 和关键 DLL Mod 适配后再动。已经被更新导致旧 Mod 失效时，可以参考原来的 [降级教程](https://www.bilibili.com/read/cv28351442)。

## 基础条件

1. 一台 Windows 个人电脑。
2. 能正常访问 Steam、Nexus Mods、GitHub、YouTube 等网站的网络环境。
3. 基本的电脑文件管理能力，以及足够的耐心。
4. 建议把游戏和 Mod 工具装在非系统保护目录，例如 `D:\SteamLibrary`、`D:\MO2\SkyrimSE`。

下面默认基于 Steam 版 Skyrim Special Edition / Anniversary Edition。

## 安装前准备

1. 在 Steam 下载 Skyrim Special Edition，语言建议选英文。
2. 第一次启动游戏到主菜单，让游戏生成配置文件。
3. 查看 `SkyrimSE.exe` 属性里的产品版本，确认是 `1.6.1170`、`1.6.1179`、`1.5.97` 还是其他版本。
4. Steam 游戏更新建议改成“启动时更新”，并用 MO2 通过 SKSE 启动游戏，减少被突然更新的概率。
5. 注册并登录 [Nexus Mods](https://www.nexusmods.com/)。现在很多模组不登录看不到文件。

## 核心工具

- [SKSE](https://skse.silverlock.org/)：脚本扩展框架。必须和游戏运行时版本对应。
- [Mod Organizer 2](https://github.com/ModOrganizer2/modorganizer/releases)：Mod 管理器。当前稳定版仍可使用 [v2.5.2](https://github.com/ModOrganizer2/modorganizer/releases/tag/v2.5.2)。
- [LOOT](https://loot.github.io/)：排序工具，适合基础排序和检查缺失 Master。
- [SSEEdit / xEdit](https://github.com/TES5Edit/TES5Edit/releases)：进阶清理、冲突检查工具。
- [ENBSeries Skyrim SE](http://enbdev.com/download_mod_tesskyrimse.html)：画面增强底层文件，需要时再装。

SKSE 安装要点：下载与你游戏版本对应的包，把 `skse64_loader.exe` 和相关 DLL 放到游戏根目录；`Data\Scripts` 可以打包成一个 MO2 Mod 管理。之后通过 MO2 运行 `skse64_loader.exe`。

ENB 安装要点：下载 Skyrim SE 版 ENBSeries，从 `WrapperVersion` 里把 `d3d11.dll` 和 `d3dcompiler_46e.dll` 放到 `Skyrim Special Edition` 根目录，再安装具体 ENB 预设。

## 必装或常用前置 Mod

版本敏感的 DLL 前置，一定要在 Files 页看清楚 `AE 1.6.1170`、`GOG 1.6.1179`、`SE 1.5.97` 或 `NG` 支持说明。

- [SkyUI](https://www.nexusmods.com/skyrimspecialedition/mods/12604)：经典 UI 和 MCM 基础。
- [SkyUI 中文](https://www.nexusmods.com/skyrimspecialedition/mods/45137)：SkyUI 汉化。
- [USSEP 非官方补丁](https://www.nexusmods.com/skyrimspecialedition/mods/266)：大型基础修复。
- [USSEP 汉化](https://www.nexusmods.com/skyrimspecialedition/mods/73303)：非官方补丁汉化。
- [非官方中文翻译](https://www.nexusmods.com/skyrimspecialedition/mods/10845)：中文基础翻译。
- [Address Library for SKSE Plugins](https://www.nexusmods.com/skyrimspecialedition/mods/32444)：大量 DLL Mod 的必备前置。
- [OPparco Mfg Command](https://www.nexusmods.com/skyrimspecialedition/mods/12919)：表情控制相关前置。
- [PapyrusUtil SE](https://www.nexusmods.com/skyrimspecialedition/mods/13048)：脚本功能前置。
- [JContainers SE](https://www.nexusmods.com/skyrimspecialedition/mods/16495)：数据结构前置。
- [ConsoleUtilSSE](https://www.nexusmods.com/skyrimspecialedition/mods/24858)：控制台功能前置。
- [Fuz Ro D-oh](https://www.nexusmods.com/skyrimspecialedition/mods/15109)：无语音对白口型/字幕相关前置。
- [SSE Engine Fixes](https://www.nexusmods.com/skyrimspecialedition/mods/17230)：引擎修复。Part 2 需要放进游戏根目录。
- [Papyrus Tweaks NG](https://www.nexusmods.com/skyrimspecialedition/mods/77779)：脚本性能调整。
- [UIExtensions](https://www.nexusmods.com/skyrimspecialedition/mods/17561)：UI 前置。
- [Better Dialogue Controls](https://www.nexusmods.com/skyrimspecialedition/mods/1429)：对话操作优化。
- [Better MessageBox Controls](https://www.nexusmods.com/skyrimspecialedition/mods/1428)：消息框操作优化。
- [XPMSSE](https://www.nexusmods.com/skyrimspecialedition/mods/1988)：骨骼前置。
- [CBBE](https://www.nexusmods.com/skyrimspecialedition/mods/198)：女性身形基础。
- [CBBE 3BA](https://www.nexusmods.com/skyrimspecialedition/mods/30174)：3BA 身形。
- [CBPC](https://www.nexusmods.com/skyrimspecialedition/mods/21224)：物理前置。
- [Faster HDT-SMP](https://www.nexusmods.com/skyrimspecialedition/mods/57339)：HDT-SMP 物理。
- [powerofthree's Tweaks](https://www.nexusmods.com/skyrimspecialedition/mods/51073)：常见 DLL 前置。
- [powerofthree's Papyrus Extender](https://www.nexusmods.com/skyrimspecialedition/mods/22854)：脚本扩展前置。
- [MCM Helper](https://www.nexusmods.com/skyrimspecialedition/mods/53000)：MCM 菜单前置。
- [ENB Helper SE](https://www.nexusmods.com/skyrimspecialedition/mods/23174)：ENB 天气/室内外识别前置。

## 功能类 Mod

- [RaceMenu](https://www.nexusmods.com/skyrimspecialedition/mods/19080)：捏脸插件。游戏中按 `~` 打开控制台，输入 `showracemenu`。
- [Alternate Start](https://www.nexusmods.com/skyrimspecialedition/mods/272)：开局不用坐马车。
- [Achievements Mods Enabler](https://www.nexusmods.com/skyrimspecialedition/mods/245)：启用 Mod 后仍可解锁成就。
- [Stay At The System Page](https://www.nexusmods.com/skyrimspecialedition/mods/67883)：按 ESC 停留在系统选项。
- [BodySlide and Outfit Studio](https://www.nexusmods.com/skyrimspecialedition/mods/201)：身形和服装刷形工具。
- [Nemesis Unlimited Behavior Engine](https://www.nexusmods.com/skyrimspecialedition/mods/60033)：经典动作行为生成器。
- [Pandora Behaviour Engine Plus](https://github.com/Monitor221hz/Pandora-Behaviour-Engine-Plus/releases)：2026 年更推荐优先尝试的行为生成器，当前可见版本为 `v4.3.1-beta`。
- [True Directional Movement](https://www.nexusmods.com/skyrimspecialedition/mods/51614)：360 度移动和现代化第三人称控制。
- [AddItemMenu](https://www.nexusmods.com/skyrimspecialedition/mods/17563)：物品获取器，可获取 ESP 内物品。新版本环境下如果有问题，优先看评论区和替代品。
- [Wheeler](https://www.nexusmods.com/skyrimspecialedition/mods/97345)：天际快速行动轮。

## 人物美化

人物美化很吃个人审美，建议先搭好稳定前置，再慢慢加。不要一口气装几十个 NPC 美化和身形替换。

- Cherry 高模预设参考：[arca.live / tullius](https://arca.live/b/tullius/68838837)。
- 韩网资源区：[Tullius Channel](https://arca.live/b/tullius)。
- 成人向和身形资源常见于 [LoversLab](https://www.loverslab.com/)。
- 英文讨论和排错可看 [Reddit / r/skyrimmods](https://www.reddit.com/r/skyrimmods/)。
- 儿童美化示例：[Woo Children Overhaul SSE](https://schaken-mods.com/files/file/1031-woo-children-overhaul-sse/)。

## 环境美化

2026 年仍然可以用 NAT.ENB 系路线。ENB 没有绝对完美的预设，不同时间、地点、天气表现都不同，最好自己试。

- [NAT.ENB / Natural and Atmospheric Tamriel](https://www.nexusmods.com/skyrimspecialedition/mods/27141)：天气基础。
- [Cabbage ENB for NAT](https://www.nexusmods.com/skyrimspecialedition/mods/103042)：白菜预设。
- [Rudy ENB for NAT](https://www.nexusmods.com/skyrimspecialedition/mods/91675)：Rudy NAT 预设。
- [PI-CHO ENB](https://www.nexusmods.com/skyrimspecialedition/mods/35082)：PI-CHO 预设。
- [Skyrim 202X Downscale](https://www.nexusmods.com/skyrimspecialedition/mods/68307)：优化后的 2020 材质，2K 比较适合大多数机器。
- [Folkvangr - Grass and Landscape Overhaul](https://www.nexusmods.com/skyrimspecialedition/mods/44899)：草地景观大修。
- [Fabled Forests](https://www.nexusmods.com/skyrimspecialedition/mods/94462)：森林/树木。
- [Archwood - Falkreath Tree Overhaul](https://www.nexusmods.com/skyrimspecialedition/mods/104698)：显卡压力较高，谨慎安装。
- [Static Mesh Improvement Mod](https://www.nexusmods.com/skyrimspecialedition/mods/659)：静态网格改进，强烈推荐。
- [Splashes of Storms](https://www.nexusmods.com/skyrimspecialedition/mods/72115)：雨水落地反弹效果。

## 动作、服装和任务地图

动作方面，老路线是 Nemesis，新路线可以先试 Pandora。部分动作作者会在 YouTube 视频说明里列出 10 到 20 个前置，必须按说明装。

- 免费阎魔刀动作示例：[YouTube 视频](https://youtu.be/gI9bOHkuIiA)。
- 服装搜索可看 [ModBooru Skyrim SE](https://modbooru.com/mods?query=skyrim_se)。
- 也可以在 [X / Twitter](https://x.com/search?q=skyrim%20se%20mod&src=typed_query) 搜作者发布页。
- Vicn 三部曲作者页：[Nexus 用户页](https://www.nexusmods.com/skyrimspecialedition/users/3863233)。
- [GomaPeroLand SE](https://www.loverslab.com/files/file/5173-gomaperoland-se/)：经典泳池拍照地图。
- 黑魂地图作者参考：[RudolphSergey](https://twitter.com/RudolphSergey)。
- [Chanterelle / 鸡油菌](https://www.nexusmods.com/skyrimspecialedition/mods/32603)：一个值得探索的野蛮世界。

## 其他工具和进阶参考

- [韩网 Nemesis 修复参考](https://arca.live/b/breaking/89606806)：解决部分非英文用户报错。
- [xTranslator](https://www.nexusmods.com/skyrimspecialedition/mods/134)：翻译工具，常逛 Nexus 的话很有用，可以在新版本上套用旧翻译。
- [ReSaver](https://www.nexusmods.com/skyrimspecialedition/mods/5031)：存档清理工具。
- [OStim Standalone 安装指南](https://www.nexusmods.com/skyrimspecialedition/articles/5654)：进阶成人向框架参考。
- [Nolvus Mod List](https://www.nolvus.net/modlist)：可参考它的 Mod 列表和分类方式。
- [我的 Mod 列表](https://loadorderlibrary.com/lists/yisal-mod-list)：原稿附带列表。

## 推荐安装顺序

1. 游戏本体英文版，启动一次到主菜单。
2. MO2，创建 Skyrim SE 实例，建议 Portable。
3. SKSE，确认 MO2 能通过 `skse64_loader.exe` 进游戏。
4. SkyUI、Address Library、USSEP、中文翻译等基础前置。
5. DLL 前置和引擎修复，例如 SSE Engine Fixes、PapyrusUtil、JContainers。
6. 身形、骨骼、物理，例如 XPMSSE、CBBE、3BA、CBPC、Faster HDT-SMP。
7. UI、功能、动作、人物、环境、服装、任务地图。
8. 每装一批就进游戏测试一次，不要等 300 个 Mod 全装完才排错。

## 排错原则

- 游戏闪退时，先确认 SKSE、Address Library、SSE Engine Fixes、DLL Mod 是否匹配当前运行时。
- MO2 左侧负责文件覆盖顺序，右侧负责 ESP / ESL / ESM 加载顺序，两边都要看。
- 有 FOMOD 安装界面的 Mod，不要一路默认下一步，必须按自己的版本选。
- 看到 `AE`、`SE`、`1.5.97`、`1.6.640`、`1.6.1130`、`1.6.1170`、`NG` 时，不要猜，打开说明看清楚。
- 先少装、勤测试、保留存档备份。新手最大的敌人不是某一个 Mod，而是一次性装太多导致不知道谁坏了。

## 转载说明

本文从原 B 站预览稿整理为 2026 GitHub 版。原稿末尾写有“本文禁止转载或摘编”，因此默认仅作为作者本人整理发布用途；如非作者本人，请先取得授权。
