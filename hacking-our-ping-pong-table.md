# 球拍上的极客--自动计分乒乓球桌
作者：Si Digital 译者：Kalimov
关键字（空格分隔）：DIY 乒乓球 比赛
---
>[原文链接]( http://sidigital.co/blog/lab-notes-hacking-our-ping-pong-table)
几个月前，我们买了一张新乒乓球桌，并迷上了它。从第一天起，我们的球技突飞猛进，只是有一样却毫无长进--计分能力。程序猿们手眼协调能力在身体巅峰时并不是最好的，再加上处于竞技游戏，再聊会天，没过多久就连基本数学计数也忘得九霄云外了（译者画外音：别看我，我也忘了几比几了……）。
我们承认，在这行中拥有一张乒乓球桌是蛮老套的。网上某机构曾下决心做一台数字积分板跟进比赛，甚至搭配更多功能，有不少很棒的实例例如Campaign Monitor's那种也做出来了。它们都不错，只是都有同样问题，你还得在每一局比赛手动计分。
In true Si digital fashion we decided to take this to the next level and automate everything…
以真正硅基数码为潮流目标的我们决定将此更上一层楼，所以所有东西自动化……

## 全面自动化
我们在球拍里埋入微小的射频标识（即电子标签）。在这套系统下，玩家们只需走向球桌，他们的脸便出现在大屏幕上，新的一局就准备好了。
<embed src="http://player.youku.com/player.php/sid/XNzc5MjQzNTQ4/v.swf" allowFullScreen="true" quality="high" width="480" height="400" align="middle" allowScriptAccess="always" type="application/x-shockwave-flash"></embed>
在得到一分后，我们只需用手指碰碰球桌下，屏幕就会自动更新实时比分。
<embed src="http://player.youku.com/player.php/sid/XNzc5MjQ0NTM2/v.swf" allowFullScreen="true" quality="high" width="480" height="400" align="middle" allowScriptAccess="always" type="application/x-shockwave-flash"></embed>
在玩家加分和启动系统时会播放提示音，而这提示音也预防了作弊--你休想在对手转身不注意时使出无影手按加分按钮！
当有玩家到达最终21分而又领先对手2分时，系统自动结束游戏，发送祝贺信息，计算新排名，然后跳转回排名榜画面。比起11分制，我们还是玩21分制比赛，因为以我们现在的渣球技，比赛会太早结束！
<embed src="http://player.youku.com/player.php/sid/XNzc5MjQ1Njky/v.swf" allowFullScreen="true" quality="high" width="480" height="400" align="middle" allowScriptAccess="always" type="application/x-shockwave-flash"></embed>
## 技术细节
这个项目分为三个关键要素，令软硬件协调，共建乒乓球赛良好风尚。（有那么大的帽子扣上吗？）
1.计分
为便于计分，我们在球桌每边安置了个电容触感开关，玩家轻轻触碰便可计分。它们连接到Spark Core微控制器，而这又连上了WiFi，在分数增加时将触碰事件发送到Spark云空间。这个系统装在球桌下，由一枚2500毫安时电池驱动，大概能维持一个星期运作。我们加装了个小型独立电源，在玩的同时既能充电又能计分，就不存在电池没电这么扫兴的事了！当然，我们也设计了在电量低的时候将警报发送到分数板上，那样就不会有意外中盘比赛了！（画外音：由于计分系统故障，本次比赛宣布取消，已投注的观众可取回自己的投注……两程序猿，卒。）
![]( http://doask.qiniudn.com/Pingpong1.jpg)
2.自动识别选手
每个选手拿的球拍都是唯一的。我们在球拍底部钻有小孔，埋入一些很小的12毫米玻璃电子标识。
![]( http://doask.qiniudn.com/Pingpong2.jpg)
![]( http://doask.qiniudn.com/Pingpong3.jpg)
而在球桌上我们用Arduino Pro Mini为核心做了个读取电子标签设备，用CC3000连上WiFi，配上个小型ID-12LA电子标签识别器。我们将其装入个小盒子，贴上少量LED作为扫描提示。这些程序源代码在文章的底部可以找到。
![]( http://doask.qiniudn.com/Pingpong4.jpg)
![]( http://doask.qiniudn.com/Pingpong5.jpg)
![]( http://doask.qiniudn.com/Pingpong6.jpg)

3.实时计分板
Nide.js和Socket.io是用来确保在我们玩的时候，屏幕上实时更新分数。有明确的事件触发时，提示音就会播出。
<embed src="http://player.youku.com/player.php/sid/XNzc5MjUyOTA0/v.swf" allowFullScreen="true" quality="high" width="480" height="400" align="middle" allowScriptAccess="always" type="application/x-shockwave-flash"></embed>
最初我们发现破解提示音挺麻烦的。移动浏览器受限于用户输入才能触发提示音，意味着用户必须在进入应用时触发某种输入条件（例如触屏）才能启用声音。经过些粗略尝试破解后（直接录入音源），我们选中了一段声音片段，最后将其质量提高和稳定化。经过采样匹配算法和发音模块处理，我们很快完成输出声音片段的流程。我们用脚本howler.js处理音频输出。
我们在Github的报告里，从服务器程序到硬件统统开源了。
想加入我们下个创作计划吗？我们正寻求一名UI/网页设计师和一名前端开发工程师。

# 译者站着说话不腰疼点评
这解决了平常打球赖皮的问题。一般我们上个球馆，或在自家后院打打，怎么也用不上裁判观战。即使双方球风良好，也免不了忘记计分，或者出点小错什么的。
甲：听说老王昨晚拿着一盒烤鸭上你家去了。（乒）
乙：我昨晚在家呐，没人来。（乓）
甲：是嘛。可能是你隔壁吧，当时看走眼了。（啪，没接到球）
乙：几比几了？
甲：啊？！
又或者会出现一时脑误，失球变得分的计分法。总之不一而足。这些该多扫兴啊！
不过，能理解原理却做不出来的译者，倒是有条思路贡献出来，让爱好者参详改进。
干嘛要手动按钮计分？如果再自动化呢？流程如下：
1.	双方上台，识别身份。（这步和原作一样）
2.	发球，球碰到甲的球拍，球拍感受到压力，发出时间信号。
3.	球落到乙方区域桌面，弹跳一下，乙方区域振动传感器触发（和甲方区域传感器相比信号大小就能知道落点区域），乙方桌面发出时间信号，等待乙球拍接球。
4.	如果乙球拍错失球超过一秒钟，判定乙失分。（乒乓球应该接球反应时间不超过一秒吧）
5.	乙接球成功，返回第二步流程，只是甲乙身份对调。
6.	如果一方接发球过大力，导致出界，只要对方区域传感器没有信号输出，都判定发球者失误。
7.	球网上也要假装传感器，判断是否触网。
