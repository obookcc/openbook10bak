# 看啥写啥--眼睛作家2.0
作者：thesystemis 译者：Kalimov
标签（空格分隔）： Arduino 残障 开源
---

>[原文链接](http://www.instructables.com/id/The-EyeWriter-20/?ALLSTEPS)
![](http://doask.qiniudn.com/EyeWriter1.jpg)
![](http://doask.qiniudn.com/EyeWriter2.jpg)
![](http://doask.qiniudn.com/EyeWriter3.jpg)
![](http://doask.qiniudn.com/EyeWriter4.jpg)
![](http://doask.qiniudn.com/EyeWriter5.jpg)
![](http://doask.qiniudn.com/EyeWriter6.jpg) 

眼睛作家是一台低成本视线跟踪装置，配备有特制软件，方便那些因肌肉萎缩、偏瘫、硬化症而瘫痪的随笔作家和艺术家用他

们的眼睛来创作。

下面展示的原型设计，以一副眼镜为基本设备，方便“眼睛创作者”工作：
>[视频](The Eyewriter)

从第一个视频展示开始，我们一直深入发掘和改进装置，最终我们有个新版本问世--“眼睛作家2.0”。新版本改善了输入准

确度，即使用户头部轻微移动也能使用。旧版本眼睛作家是为瘫痪作家而设计的，是要戴在完全无法运动的头部上使用的。

2.0版本设计上使用一个摄像头和LED系统，将其远离头部放置，于是头部轻微移动的用户也能使用了，例如多发性硬化症患者

、戴眼镜的人等等。

眼睛作家既廉价又完全开源。现时，零件成本大约200美金，而传统商用视线跟踪系统则需9000至20000美金。便宜订单是巨大

吸引力，也是为了那些需要视线跟踪器的人所考虑的。

这个秋季，我们展出和公测了眼睛作家2.0。我们甚至将其与一个机械臂连接，用来画出人们用眼睛视线创作的艺术作品。详

情见以下链接：

http://www.switched.com/2010/12/13/eyewriter-teams-up-with-robotagger-to-print-kids-ocular-artwork/print/
EyeWriter Teams Up With Robotagger to Print Kids' Ocular Artwork


## 装有机械臂的眼睛作家团队打印出孩子用视线做的艺术品
作者：Matthew Zuras 译者：Kalimov
---
>[原文链接](http://www.switched.com/2010/12/13/eyewriter-teams-up-with-robotagger-to-print-kids-ocular-

artwork/print/)
![](http://doask.qiniudn.com/EyeWriter7.jpg) 

最初眼睛作家是为了Tony Quan，一名2003年不幸确诊为渐冻人的随笔艺术家所设计的。将摄像头对准用户眼珠子，仪器就能

跟踪用户眼睛动向，从而使他得以绘画。在儿童电影节当中，一些小幸运儿有幸获得试用眼睛作家的机会。用眼睛作家指挥的

机械臂将孩子的创作用它那橘黄臂膀变成了现实。
>[视频](Eyewriter 2)



# (2.0版本在设计过程中，在Ito Takayuki、Kyle McDonald、Golan Levin和Parsons大学“眼睛作家“协作小组的学生帮助

和录入下得以完成。同时也鸣谢卡内基梅隆大学创意调查工作室为开发研究设立一个部门。)
---
# 步骤1：总览
---
简单来说，我们就做了几件事。首先，我们将发光LED放在屏幕边缘和中央。接着，我们拆开利用PS3的摄像头，用以获得垂直

同步信号（产生于拍摄每帧图像时），使红外传感器探测到。第三步是编程步骤，建立Arduino和电路，控制闪光信号。最后

，我们为这个系统做个底层，初步测试软件。

以技术角度来看，2.0版本系统以3个红外发光器对每帧进行闪频观测。在偶数帧时，瞳孔出现发光，那是因为红外光正从你的

眼中反射回来，就像常见那种照相机红眼现象那样。在奇数帧时，你的瞳孔则是黯淡的。两者的差别使我们实时区别追踪瞳孔

轨迹成为可能。进一步说，探测到由红外发光造成的反光，加上瞳孔中的信息，用反光/瞳孔位置映射算法方程的最少正方形

吻合解进行屏幕位置校正。

# 步骤2：零件清单
---

在动工之前，我们需要合理数目的零件制作这个设备。看看图片，先对我们做的东西有个概念，而详细零件清单在PDF档案里

已有列明。

![部件图](http://doask.qiniudn.com/EyeWriter8.jpg) 

>[下载详细零件清单](http://eyewriter.org/docs/PartsList_EyeWriter2.pdf)

# 步骤3：软件——开放式框架与眼睛作家
---
![](http://doask.qiniudn.com/EyeWriter9.jpg)  
![](http://doask.qiniudn.com/EyeWriter10.jpg) 

眼睛作家2.0由数个程序片断组装及运行。在这个步骤中，我们讲述如何下载安装集成开发环境、程序开放式框架及眼睛作家

程序本身。

一、集成开发环境（IDE）

•	集成开发环境（IDE）是为软件开发程序员准备的综合性开发工具软件。
•	如有需要，下面链接用以下载安装一个IDE来运行开放式程序框架。
>[http://www.openframeworks.cc/setup](http://www.openframeworks.cc/setup)

二、开放式程序框架
•	开放式程序框架以C++库文件设计，以简单直观的实验框架为创造过程提供帮助。
•	如有需要，可于下面链接下载开放式程序框架。
>[http://www.openframeworks.cc/download](http://www.openframeworks.cc/download)

三、眼睛作家的GitHub
•	GitHub是一个基于网页界面的分布式版本控制系统，用户们在这个平台上分享交换程序代码。
•	Visit the EyeWriter source page on GitHub.
>[http://github.com/eyewriter/eyewriter/tree/remoteEyetracker]

(http://github.com/eyewriter/eyewriter/tree/remoteEyetracker)
•	眼睛作家的源代码在以下GitHub页面内。
>[http://github.com/eyewriter/eyewriter/tree/remoteEyetracker]

(http://github.com/eyewriter/eyewriter/tree/remoteEyetracker)
•	在右上角菜单中下载代码。
•	选择ZIP格式。
•	完成下载后，解压缩文件，将“eyewriter-xxxxxx”文件夹移动到开放式框架的“apps”文件夹中。
•	打开“apps/eyewriter-xxxxxxx/eyeWriterTracker/RemoteEyeTracker.xcodeproj”文件，测试所有安装程序工作无

恙。
•	试运行源代码，跟踪调试窗口应该出现在演示视频模式中。

# 步骤4：软件——摄像头和Arduino
---
我们需要为硬件安装多两个驱动。摄像头驱动建立起PS3摄像头和电脑之间的交互，Arduino软件则提供软件和硬件之间的接口

。

安装PS摄像头驱动

Mac系统下：
•	Macam是Mac OS X的USB摄像头驱动程序，数以百计的USB摄像头通过它能被Mac OS X的视频捕捉程序所识别。我们用

的是PS3摄像头，那么驱动程序就是为了让电脑识别它所要安装的。
 
•	从SourceForge链接下载摄像头驱动程序：
>[http://sourceforge.net/projects/webcam-osx/files/cvs-build/2009-09-25/macam-cvs-build-2009-09-

25.zip/download](http://sourceforge.net/projects/webcam-osx/files/cvs-build/2009-09-25/macam-cvs-build-2009-

09-25.zip/download)
 
•	下载完成后，解压缩档案，将macam.component放入硬盘里 /Library/Quicktime/文件夹中。
 
PC版本的：
•	下载并安装CL-Eye-Driver:
>[http://codelaboratories.com/downloads/](http://codelaboratories.com/downloads/)

Arduino
•	Arduino是嵌入式计算机系统的设计开发工具，有开源单片机控制硬件、集成了输入输出和基本程序语言所组成。
 
•	从[http://arduino.cc/en/Main/Software](http://arduino.cc/en/Main/Software)下载安装Arduino软件。
 
•	不熟悉Arduino环境的话，[http://arduino.cc/en/Guide/HomePage](http://arduino.cc/en/Guide/HomePage)内可

以参考入门解说。

# 步骤5：载入Arduino程序框架
---
在这里，你需要载入Arduino程序框架，以便PS摄像头工作。

一、Arduino程序框架（仅限PS摄像头使用）
•	在Arduino IDE软件内载入Arduino眼睛作家程序框架“apps/eyewriter-

xxxxxxx/eyeWriterTracker/StrobeEye/StrobeEye.pde”，使眼睛作家软件能识别硬件。

•	当Arduino板连接上时，将程序框架上载到板内。如果你不熟悉这一步，请参阅

[http://arduino.cc/en/Guide/HomePage](http://arduino.cc/en/Guide/HomePage)内的入门解说。

# 步骤6：硬件：电源适配器
---
 
电源适配器
在这里，你需要切下一段电源适配器的导线，用以驱动面包板电路。
•	剪下7.5伏电源适配器的接口。
![](http://doask.qiniudn.com/EyeWriter11.jpg)

•	用电压计从裸露导线中确定正负极。

•	用一段剥好的红线和黑线，将红线焊上适配器的正极导线，黑线焊上负极导线。

•	先单独捆扎裸露导线，确保正负极分开不会短路，然后再将它们扎在一块，确保没有导线裸露。

# 步骤7：硬件：红外LED
---

红外LED
•	收集8个红外发光二极管（IR LED）和一片圆形的印刷电路板（PCB）。
 
•	在PCB上做一个LED阵列，你需要确定每个LED的正负极引脚。一般来说，长脚阳（正），短脚阴（负）。另外，在镜

头发光阴极那边往往有个扁平斑点。
为方便区分，不妨在导线节点上标注正负极。
![](http://doask.qiniudn.com/EyeWriter12.jpg)

•	串联4个LED为一组，下一组也是4个，互相并联。将LED的引脚剪短柄焊接在一起。
![](http://doask.qiniudn.com/EyeWriter13.jpg)
![](http://doask.qiniudn.com/EyeWriter14.jpg)

•	将LED引脚焊接在一起组成电路后，将大约2英尺（约60厘米）的红绿通信导线分别焊到LED电路的正负两端。
![](http://doask.qiniudn.com/EyeWriter15.jpg)

•	测试LED的PCB电路板，建立下图所示电路。仔细观察红外LED是否发出黯淡的红光。
![](http://doask.qiniudn.com/EyeWriter16.jpg)

•	确认红外LED工作无误后，用热熔胶固定电路板背后的所有节点。

•	重复以上1~5步，做多一些LED PCB电路板。

•	用一块较大的圆形PCB，小心在中间钻一个洞，如下图所示。
![](http://doask.qiniudn.com/EyeWriter18.jpg)

•	在PCB的外缘，建立一个4个LED串联一组共4个互相并联电路。LED的放置位置需使PS摄像头正好吻合，而摄像头不会

阻挡住LED。
![](http://doask.qiniudn.com/EyeWriter19.jpg)

•	在焊接好LED引脚组成电路和4对正负极电源导线后，将4组LED并联排列。
![](http://doask.qiniudn.com/EyeWriter20.jpg)

•	焊接约2英尺（约６０厘米）红绿通信导线至LED电路的正负极端点。

•	建立如下的电路来测试较大的LED PCB板，看看红外LED是否发出黯淡红光。
![](http://doask.qiniudn.com/EyeWriter21.jpg)

•	确认红外LED工作无误后，用热熔胶固定电路板背后的所有节点。
![](http://doask.qiniudn.com/EyeWriter17.jpg)

# 步骤８：拆解PS摄像头——前期准备
---
![](http://doask.qiniudn.com/EyeWriter22.jpg)

在这里我们讲解如何取出PS摄像头。对于替换摄像镜头、加装红外滤镜和连接垂直同步信号来说这步是必须的。
•	拿出PS摄像头。温馨提示：私拆不保，责任自负。

•	撬开四颗盒子底部的螺帽。
![](http://doask.qiniudn.com/EyeWriter23.jpg)

•	扭下四颗螺帽下的螺丝。别丢掉，稍后你要用回它们。
![](http://doask.qiniudn.com/EyeWriter24.jpg)

•	拿掉四颗螺丝后，继续撬开后半部分盒子，建议使用一字螺丝刀和锤子，或一把尖嘴钳。使用巧劲，别坏了里面的东

西或伤着自己。
![](http://doask.qiniudn.com/EyeWriter25.jpg)
![](http://doask.qiniudn.com/EyeWriter26.jpg)

•	拉出导线，将塑料座边上的两颗底部螺丝扭下来，保留它们备用。
![](http://doask.qiniudn.com/EyeWriter27.jpg)

•	拿掉垂直的部分。
![](http://doask.qiniudn.com/EyeWriter28.jpg)

•	扭下电路板周围的五颗螺丝（两颗在边上，三颗在上面），同样保留它们备用。
![](http://doask.qiniudn.com/EyeWriter29.jpg)

•	拿掉五颗螺丝后，从盒子前面拿起电路板。
![](http://doask.qiniudn.com/EyeWriter30.jpg)
![](http://doask.qiniudn.com/EyeWriter31.jpg)

•	有四个麦克风穿过电路板顶部。直接使用剪子剪掉它们，我们用不着它们。
![](http://doask.qiniudn.com/EyeWriter32.jpg)

•	PS摄像电路板准备完毕，随时可接线。下一步是将它连接垂直同步信号和接地点。

# 步骤9：拆解PS摄像头--垂直同步信号
---

在这里我们介绍如何截取摄像头的垂直同步信号。垂直同步信号是由摄像头刷新率所产生的电子信号。获取摄像头的垂直同步

信号至关重要，只有通过它我们才能将摄像头刷新率和红外LED信号相吻合。

•	标出PS摄像电路板的接地点。有些型号的PS摄像头在镜头底座（左下图）附近有5个节点，而另一些则只有4个（右下

图）。倘若你的型号有5个节点，那接地点就是最接近镜头底座的那个。如果你的型号有4个节点的画，接地点还是在最接近镜

头底座那里，不过那个节点宽度相当于其他的两倍。
![](http://doask.qiniudn.com/EyeWriter33.jpg)

•	剪下约两英尺（约60厘米）四色通讯导线，将红绿色导线和黑白色导线分开。
![](http://doask.qiniudn.com/EyeWriter34.jpg)
 
•	在距离一端约两英寸（约5厘米）分开红线和绿线。剥开一小片绿线末端的绝缘层，用于焊接PS摄像头接地端。
 
•	将PS摄像电路板和绿线别在一个支架上，准备焊接一端绿线到接地点。用一片厚纸张或卡纸夹在曲别针上，避免划伤

电路板。
![](http://doask.qiniudn.com/EyeWriter35.jpg)
 
•	将绿线和PS摄像头接地点焊接起来。
 
•	标定电路板上的垂直同步信号源，在下图圆圈内所示。注意：近期型号的PS摄像头（由电路板的金色外缘可以得知）

中，信号源在PCB板的前方，R19电阻的上方。而更近期更新一些的型号也投入市场，在下图介绍如何在上面找到信号源。
![](http://doask.qiniudn.com/EyeWriter36.jpg)
![](http://doask.qiniudn.com/EyeWriter37.jpg)
![](http://doask.qiniudn.com/EyeWriter59.jpg)
![](http://doask.qiniudn.com/EyeWriter60.jpg)

•	用一把锋利小刀，小心用刀尖架在信号源上，轻轻刮开绝缘涂层，使金属触点裸露出来。
![](http://doask.qiniudn.com/EyeWriter38.jpg)
 
•	红线用于连接裸露的信号源，但导线太粗，无法在这么小区域内焊接平整，于是我们需要一条标号30导线作为中介。

将两条标号30导线末端剥线。
 
•	截短红线，将标号30导线一端与红线焊接起来。
![](http://doask.qiniudn.com/EyeWriter39.jpg)
 
•	在焊接标号30导线到信号源之前，需要测试一下所有连接是否准确无误。组装如下图所示电路，当标号30导线接触信

号源时，面包板上的LED应会快速闪烁。
![](http://doask.qiniudn.com/EyeWriter40.jpg)
 
•	用0.022英寸（0.56毫米）细的焊锡，小心翼翼将标号30导线焊上裸露的信号源。面包板上闪烁的LED能确认是否操作

成功。

# 步骤10：拆解PS摄像头——完成
---

这里介绍如何将摄像头重组一体。
•	松开固定镜头的两颗螺丝，小心操作，垂直同步信号传输节点是很脆弱的。拆开镜头，放好螺丝。
![](http://doask.qiniudn.com/EyeWriter41.jpg)

•	量度新装镜头架的正方形开口大小。用滤纸裁减一个刚好大小的正方形，将其放入开口处。
![](http://doask.qiniudn.com/EyeWriter42.jpg)
![](http://doask.qiniudn.com/EyeWriter43.jpg)

•	滤纸到位后，螺接新的镜头架。也许需要出一些力，镜头架对于电路板来说稍大，导致其中一个螺丝将成角度钻入。
![](http://doask.qiniudn.com/EyeWriter44.jpg)

•	将新的镜头旋进电路板新镜头架上。
![](http://doask.qiniudn.com/EyeWriter45.jpg)

•	灌热熔胶固定保护垂直同步信号连接。
![](http://doask.qiniudn.com/EyeWriter46.jpg)

# 步骤11：
--- 

在这里我们告诉大家如何在面包板上组装电路，而这是让Arduino融入眼睛作家的最初过程。
•	用下面链接的电路图组装电路。
![](http://doask.qiniudn.com/EyeWriter47.jpg)

•	组装好全部电路后，眼睛作家的代码已预备妥当，等待摄像机实时输入。要从演示视频模式切换回实时图像模式，打

开“apps/eyewriter-xxxxxxx/eyeWriterTracker/bin/data/Settings/inputSettings.xml”，将mode tag选项从1改为0。

•	打开“apps/eyewriter-xxxxxxx/eyeWriterTracker/RemoteEyeTracker.xcodeprof”文件，运行源代码，跟踪调试画

面应该显示PS的摄像头拍摄的画面。

# 步骤12：做个木底座
---

在这里我们讲一讲如何做个木制手提底座。做这个蛮有意思的，它使得整个系统有一个稳定结构摆放在上面，便于测试校准及

提供眼睛作家工作环境。
![](http://doask.qiniudn.com/EyeWriter48.jpg)

下面列出制作底座所需材料和零件：
•	2根5/16英寸直径木棒，约20英寸长。（A）

•	2根5/16英寸直径木棒，约1.5英寸长。（D）

•	一个20 x 4 x 0.5英寸的木块（B）

•	3个3 x 1.75 x 1.75英寸的木块（C）

•	钻头的直径和木棒直径一样。

如图所示，用一块C零件调整另外两块C零件，夹紧它们，在距离它们边缘0.75英寸处钻穿它们。
![](http://doask.qiniudn.com/EyeWriter49.jpg)

•	第二步：
将两块零件C洞对洞排整齐，将它们放置到零件B的边上，排齐夹住（如图所示）并钻它们至零件B大约1.5英寸深。
将短木棒穿过每个零件C和零件B的钻孔放进去。
![](http://doask.qiniudn.com/EyeWriter50.jpg)

•	第三步
钻一个适合三脚架快装板螺丝直径的孔。
![](http://doask.qiniudn.com/EyeWriter51.jpg)

•	第四步：
将底座（B）和边缘部件（C）组装，插入并通过钻孔排齐木棒（A），使它们和底座长度平齐。
![](http://doask.qiniudn.com/EyeWriter52.jpg)

# 步骤13：使用眼睛作家软件——安装与跟踪屏幕
---

在这里我们介绍眼睛作家这款软件，让你能安装使用。
•	通过电脑视角（CV）面板右面第一排的屏幕对焦选项将摄像头对焦。旋转摄像头镜头直到图像变得锐利清晰，接着跳

出屏幕对焦选项，返回跟踪屏幕。
![](http://doask.qiniudn.com/EyeWriter53.jpg)

•	在面板右面第一排选择载入视频设定。
![](http://doask.qiniudn.com/EyeWriter54.jpg)

PS3摄像头：
理想状态下，你希望图像是清晰、平衡，噪点最少的，就如同下图所示。在摄像头选项表单下，通过滑动图像增益和快门选项

，直到图像达至理想。

•	在压缩选项表单下，就有类似以下情况。倘若你的电脑性能较好，那就选择每秒30帧（FPS）。如果电脑速度较慢，

那就设为每秒15帧吧。

# 步骤14：用眼睛作家进行屏幕定位
---

在这步中完成屏幕校正。
•	按下空格键出现指引提示，在按下空格键开始。当红点出现时，盯着看吧。
![](http://doask.qiniudn.com/EyeWriter55.jpg)

•	在校正后，蓝线显示所有校正误差范围。当出现长条蓝线时，按下空格键重设校正步骤。

# 步骤15：用眼睛作家玩抓人游戏
---

•	盯着“抓我吧”方块，方块的颜色将转为绿色。
![](http://doask.qiniudn.com/EyeWriter56.jpg)

•	当方块完全绿色时，意味着捕捉到了，接着它会出现在别的地方。不断抓取方块，这用来测试校正视线追踪功能。

# 步骤16：使用眼睛作家软件——画图
---
画字母

•	绘图模式开始时默认暂停。在绘图前，你可以选择显示背景网格与否。当然，背景网格可在任何暂停时选择切换。

•	盯着暂停按钮，切换为录制模式来进行绘图。盯着按钮，它将转为绿色，便切换到录制模式。

•	它用向量点计算法绘图，以盯住画布区域某个点约一秒钟建立标点的方式完成。绿色视线追踪圆圈是需要停留一段时

间确定一个标点的。

•	当增加标点时，标点之间将以线条连接。 用这些线条，你可以创作不同的图形或画字母。要想新开一个线条端点，

只需盯住“下一笔”这个按钮。

•	保留当前图形或字母，并移往下一个，盯住“下一个字母”按钮。先前你所画的字母会在屏幕顶部出现，新的画布已

为下一个字母准备好。

•	当你完成绘制图形和字母后，盯住“下个模式”进入放置模式。

放置模式
•	默认上，你画的字母处于全选状态，等待安置。若想选择单个字母，只需盯着“选择字母”按钮。

•	若想让你选择的图像顺时针或逆时针旋转则选择“旋转”按钮。

•	要上下左右移动你选的图像，选择“平移”按钮。

•	要想放大缩小则按下“变焦”，你选择的图像会因此改变尺寸。

•	按钮“自动放置”是将你的字母按照你画的次序并排放置。

•	完成放置图像和字母后，再次盯着“下个模式”进入效果渲染模式。

# 步骤17：用眼睛作家打字
---
 
•	你想按哪个键，就盯着哪个键。当你盯着的时候，按键的颜色变为绿色然后闪为蓝色。
![](http://doask.qiniudn.com/EyeWriter57.jpg)

•	字母键闪为蓝色后，就等于被按下了。在屏幕上方，你能看到你打了什么字。


•	按下屏幕左下方的SPEAK键将说出你打的词汇。切换语音朗读开关在屏幕的中间偏右，在你输入词汇并按下空格键后

将自动阅读。


•	注意屏幕右下方的大写开关。在输入数字及特殊字符，例如“!@#$%”等需要手动切换。

# 步骤18：用眼睛作家玩打乒乓游戏
---

•	阻挡小球通过屏幕下方你的球拍光标。

•	球拍会滑向你目光移动到的X坐标。因此当你盯住移动小球时，球拍也随之横向移动。
![](http://doask.qiniudn.com/EyeWriter58.jpg)

