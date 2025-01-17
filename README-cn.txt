LAV Filters - 基于ffmpeg的DirectShow分割器和解码器

LAV Filters 是一组基于libavformat和libavcodec库的DirectShow筛选器

从ffmpeg项目，这将允许您发挥几乎任何格式的DirectShow播放器。

过滤器仍在开发中，因此不是每个功能都完成，或者支持的每种格式。

安装
=============================
- 解压
- 注册 (install_*.bat files)
	注册需要管理员权限和提升的shell（“以管理员身份运行”）

如何使用
=============================
默认情况下，拆分器将注册所有已删除的媒体格式

测试发现至少部分有效。
目前包括（但不限于）
	MKV/WebM, AVI, MP4/MOV, TS/M2TS/MPG, FLV, OGG, BluRay (.bdmv and .mpls)

然而，其他一些分裂注册在一个“坏”的方式，并迫使所有球员

使用它们。哈利媒体分裂者就是其中之一，并给予优先权

对于lavfslitter，您必须卸载Haali或重命名其.ax文件

至少是暂时的。

音频和视频解码器将注册具有较高的优点，这应使

默认情况下，它是首选解码器。大多数玩家提供了一种选择首选的方法

然而，解码器。

自动流选择
=============================
LAV Splitter提供了在打开文件时预选流的不同方法。

视频流的选择是不可配置的，LAV分配器将非常简单

挑一个质量最好的。

音频流选择提供了一些灵活性，特别是您可以配置首选语言。

语言配置很简单。只需输入3个字母的语言代码列表（ISO 639-2），

用逗号或空格分隔。
例如: "我给予和平". 这将尝试选择与这些语言之一匹配的流，

按照你指定的顺序。首先，检查是否有英语曲目，如果没有，

上德语课，然后上法语课。

如果多个音轨匹配一种语言，则根据音质进行选择。这里的主要属性

是通道数，之后是使用的编解码器。PCM和无损编解码器具有更高的优先级

比有损编解码器。

字幕选择提供了最大的灵活性。

有4种不同的字幕选择模式。

"没有字幕"
此模式很简单，默认情况下字幕将关闭。

"只有强制字幕"
此模式仅预选带有“强制”标志的字幕。当然，它也会遵循语言偏好。

"默认"
默认模式将选择与语言首选项匹配的字幕。如果没有匹配，或者未配置

语言，不会激活字幕。此外，将始终使用标有“default”或“强制”的字幕。

"高级"
高级模式允许您使用特殊语法编写自己的规则组合。它还允许选择字幕

基于文件的音频语言。

基本语法很简单，它总是需要一对音频和字幕语言，用冒号分隔，例如：“eng:ger"

在本例中，如果找到英语音频，LAV Splitter将选择德语字幕。

高级模式不支持语言代码，而是支持两种特殊情况：“*”和“off”。

当您为语言代码指定“*”时，它将匹配所有内容。例如“*：eng”将激活英文字幕，独立

有声语言。反之亦然：“eng:*”将在音频为英语时激活任何字幕。

“off”标志仅对字幕语言有效，它指示LAV Splitter关闭字幕。

所以”eng:off“表示当音频为英语时，字幕将被禁用。

除了上述语法之外，还支持两个标志来增强字幕选择。

具体来说，LAV Splitter理解标志“d”表示默认字幕，标志“f”表示强制字幕，

标志“h”表示听力受损，标志“n”表示正常流（非默认、强制或受损）。

此外，可以用前导“！”来否定标志在整个旗子阻挡之前-“！“h”变为“dfn”等。

标志附加到字幕语言中，由管道符号（“|”）分隔。示例：“*：*| f”

此标记指定在任何音频语言上，您需要标记为强制的任何字幕。

高级规则可以通过附加字幕、用逗号或空格分隔，组合成一个完整的字幕选择逻辑。

规则将始终从左到右解析，第一个匹配优先。

考虑以下规则集:
"eng:eng|f eng:ger|f eng:off *:eng *:ger"
此规则的含义如下:
如果音频为英语，则加载英语或德语强制字幕曲目，否则关闭字幕。

如果音频不是英语，请加载英语或德语字幕。

BluRay 支持
=============================
要播放BluRay，只需打开BluRay光盘上bdmv文件夹中的index.bdmv文件。

LAV分配器将自动检测光盘上最长的音轨（通常是主电影），

开始玩吧。
或者，也可以打开播放列表文件（*.mpls，位于BDMV/playlist）和LAV Splitter

然后播放特定的标题。

在将来的版本中，您也可以从播放器中选择标题。

编译
=============================
使用VS2019（包括项目文件）编译非常简单。

旧版本的visualstudio不受官方支持，但仍然可以工作。

但是，它确实要求您构建自己的ffmpeg和libbluray。

您需要将完整的ffmpeg包放置在一个名为“ffmpeg”的目录中

主源目录（该文件所在的目录）。有脚本要

构建适当的ffmpeg。

我建议使用ffmpeg的fork，因为它包含了用于

媒体兼容性:
https://git.1f0.de/gitweb?p=ffmpeg.git;a=summary

libbluray是用MSVC项目文件编译的，但是

需要libbluray的版本。与ffmpeg类似，只需放置完整的树

在主目录的“libbluray”目录中。

你可以在这里得到修改过的版本:
https://git.1f0.de/gitweb?p=libbluray.git;a=summary

反馈
=============================
GitHub Project: https://github.com/Nevcairiel/LAVFilters
Doom9: https://forum.doom9.org/showthread.php?t=156191

下载
=============================
https://github.com/Nevcairiel/LAVFilters/releases