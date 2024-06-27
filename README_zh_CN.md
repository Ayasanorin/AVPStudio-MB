# AVPStudio
杜比影院动态视听走廊显示内容制作工具。

## 简介
部分杜比影院在影厅入口处建设有动态视听走廊系统。该系统使用由科视数字系统公司（Christie Digital）研发的科视Christie® 潘多拉魔盒®系列媒体和显示控制系统，使用多个超短焦投影仪投影多个相邻画面并进行几何校正与边缘融合，实现在白墙上呈现出一个颇具沉浸感的长画面，以在观众进入影厅前营造观影氛围。

制作适配于科视Christie® 潘多拉魔盒®系统的内容需要使用由科视数字系统公司研发的专业内容创建软件及相关工具。遗憾的是，这些工具售价昂贵且授权门槛较高，不适合于观影活动等DIY目的应用。然而，杜比影院所使用的潘多拉魔盒®软件已经预设好了一种画面分离模板，我们只需参照该模板就可以选择制作一种特殊排列规格的视频并将其添加至潘多拉魔盒®时间线，即可产生近似于杜比官方内容的沉浸式显示效果。

AVPStudio是一个编码工具。它可以将任意视频按照该预设的分离模板重新排列并编码为潘多拉魔盒®系统所支持的格式，从而实现自制动态视听走廊的播放内容，在观影活动等需要投影自制内容的情况下应用。

## 使用说明
**注意：本程序仅适用于Dolby AVP V2。其它类型配置未经测试。AVPStudio不保证对其它类型配置的可用性。**

### 我不熟悉程序设计。如何下载并运行软件？
请访问[此地址](https://github.com/izwb003/AVPStudio/releases/latest)以下载最新版本的可执行程序，将其安装到您的电脑中。

### 素材准备
杜比影院动态视听走廊具有三种不同的规格。三种规格的具体参数如下：

| 规格   | 尺寸        | 分辨率        | 音频轨道         |
| ------ | ----------- | ------------- | ---------------- |
| Small  | 5.5m x 2.1m | 2830W x 1080H | 7.1 PCM Surround |
| Medium | 9m x 2.1m   | 4633W x 1080H | 7.1 PCM Surround |
| Large  | 12m x 2.1m  | 6167W x 1080H | 7.1 PCM Surround |

有关目标影院的具体规格，可向影院工作人员咨询。若对方无法透露准确信息，可自行对实际投影区域进行测量。

> 提示：
> 您可以通过查阅杜比官方发送至影院的音视频文件来了解具体规格。对于V2配置，文件命名规则如下：
> V2_Name_audio_all.wav
> V2_Name_video_Xm.mxl
> X即指代当前配置视听走廊宽度尺寸。

AVPStudio亦提供一个参考表格给出部分已知影城的配置规格。

确认规格后，请以目标规格的分辨率制作内容视频。务必留意：

- 根据默认配置，视频将自动循环播放。故请考虑好首尾衔接。
- 影片长度不可过长。
- 请制作常见的普通规格SDR视频，并控制码率在合理范围内。建议考虑使用CBR。不要尝试制作高规格内容，可能会面临不兼容问题。
- 音频声道最高为7.1声道。5.1或立体声也会受到支持。
- 尽可能调低音频音量。否则会影响影厅内观影体验。
- 规范一般要求视频宽度或高度为偶数。故此您剪辑的视频可能是偶数分辨率（4632x1080或6166x1080），这是正常现象，可以被AVPStudio正确处理。

### 转换操作
- 启动AVPStudio，选择您的目标影院的走廊尺寸，单击“创建内容”。
- 拖放您制作好的目标规格的分辨率视频到程序窗口中，或单击“浏览”选择视频文件。
- 播放并预览画面效果，在右侧“输出设置”中确认必要的设置。
- 单击“导出放映内容”，等待程序运行完成。
- 联系影院技术人员，将生成的```.mxl```视频文件及```.wav```音频文件拷贝进影院潘多拉魔盒®系统，并按与添加杜比官方内容相同的方法将内容拖入时间线。

### 我的内容未播放完毕即自动跳转回到了开头播放，怎么办？
请仔细观察潘多拉魔盒®系统的时间线，留意图中所框出的两个“cue”标记：

![](images/pandorasbox_timeline_mark_hint.jpg)

您的视频将从“![](images/pandorasbox_start_mark.png)”标记开始播放，播放至“![](images/pandorasbox_cue_mark.png)”即自动返回“![](images/pandorasbox_start_mark.png)”标记处循环播放。您可以按住并拖动“![](images/pandorasbox_cue_mark.png)”标记来调整它的位置。如图所示：

![](images/pandorasbox_drag_cue.jpg)

这样，通过将“![](images/pandorasbox_cue_mark.png)”拉至更远的位置（甚至视频末尾），即可让循环（cue）持续时间更长以避免中途返回开头。

## 附加工具

### AVPStudio ImageOrganizer
用于将图片构建为符合杜比影院动态视听走廊分离画面的图片工具。

若您的放映内容仅为单张静态图片，该工具可以省去制作视频的工作。

### AVPStudio WAVGenerator
用于生成音频WAV的工具。

可搭配ImageOrganizer用于为图片放映内容添加背景音乐，亦可用于及时调整WAV音频的音量大小。

### AVPStudio MXLPlayer
MXL播放器。

可播放转换完成的（或者官方的）mxl文件预览实际放映效果，亦可将mxl文件转换为H264 MP4视频。

## 技术信息

### 原理说明
有关实现的具体原理及画面结构，请参阅[此专栏](https://www.bilibili.com/read/cv27334455/)。

### 构建说明
截至目前，软件仅在Windows环境下调试并测试通过，尚未针对Linux及macOS环境进行配置与调试。

CMake脚本已被调整为默认从互联网下载预构建ffmpeg。请确保构建时互联网连接畅通。您也可以参阅CMakeLists.txt自行配置外部库。

构建需要完整的Qt6环境。项目必须使用以下Qt库：Qt6Core, Qt6Widgets, Qt6Multimedia, Qt6MultimediaWidgets, Qt6Network。

## 致谢与声明
AVPStudio的诞生离不开[@筱理_Rize](https://space.bilibili.com/3848521/)先生的探索结果。本软件的所有实现原理均由@筱理_Rize先生经沟通及自行测试与活动经验得出。

AVPStudio需要致谢[@冷小鸢aque](https://space.bilibili.com/27063907/)和[@讓晚風温暖各位的心](https://space.bilibili.com/122957742/)在实践中得出的测试结论。

更多致谢信息，请参阅软件的[“关于”](res/texts/aboutinfo_zh_CN.md)页面。

杜比®、杜比影院®、Dolby®、Dolby Cinema®是杜比实验室国际有限公司的注册商标。

Christie®、Christie Pandoras Box®是科视数字系统有限公司的商标。

所有其它商标皆为各自所有者的财产。

AVPStudio与杜比实验室、科视数字系统有限公司无关。AVPStudio的输出不能代表上述企业的产品质量。AVPStudio仅被设计用于UGC内容创作目的，而不可被用于专业内容发行工作。针对专业内容发行需求，请与杜比实验室或科视数字系统有限公司联系。

根据《GNU通用公共许可协议》第十一、十二条，本程序为免费授权，故在适用法律范围内不提供品质担保。除非另作书面声明，版权持有人及其他程序提供者“概”不提供任何显式或隐式的品质担保，品质担保所指包括而不仅限于有经济价值和适合特定用途的保证。全部风险，如程序的质量和性能问题，皆由你承担。若程序出现缺陷，你将承担所有必要的修复和更正服务的费用。除非适用法律或书面协议要求，任何版权持有人或本程序按本协议可能存在的第三方修改和再发布者，都不对你的损失负有责任，包括由于使用或者不能使用本程序造成的任何一般的、特殊的、偶发的或重大的损失（包括而不仅限于数据丢失、数据失真、你或第三方的后续损失、其他程序无法与本程序协同运作），即使那些人声称会对此负责。

## 第三方软件与开放源代码许可

AVPStudio基于Qt许可证使用Qt6技术。

AVPStudio基于LGPLv2.1及GPLv2使用来自[FFmpeg](https://ffmpeg.org/)的软件。

AVPStudio MXLPlayer基于zlib license使用来自[SDL](https://www.libsdl.org/)的软件。

AVPStudio是在[GNU GPLv2](https://www.gnu.org/licenses/old-licenses/gpl-2.0.html#SEC1)下开放源代码的软件。