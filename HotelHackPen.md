# 如何将人畜无害的白板笔变成“黑店神棍”
原帖作者：Gabrielle Taylor 翻译：Kalimov
标签（空格分隔）： Arduino 白板笔 破解
---
>[原文链接](http://null-byte.wonderhowto.com/how-to/turn-innocent-dry-erase-marker-into-hotel-hacking-machine-0139534/)
几个月前在黑帽安全技术大会上，黑客科迪•布罗修斯给了酒店业一个好大的惊喜——笑不出来的——他展示了如何破解全球数以百万计酒店用的Onity安全锁。
他的破解过程之所以使人印象深刻，只有四个字——简单、经济。一个不贵的Arduino微控制器读取了门锁内存里的钥匙信息。
 
![](http://doask.qiniudn.com/turn-innocent-dry-erase-marker-into-hotel-hacking-machine1.jpg)
Onity在他们的技术支持页面（在撤版之后，重新登载在布罗修斯的博客上。译者按：不过现在也倒了，原因不明。）回应，他们将为客户提供两条解决之道。一是加多一个机械外壳作为应急手段，然后通过固件升级来彻底解决问题。不过，按布罗修斯的说法，Onity打算让客户承担部分改装经费，对大多数酒店来说，除了贵还是贵。
这意味着即使门锁最终升级成功，在大批酒店装备起它仍需时间。而这段时间内，数以百万计的客房仍处于坐以待毙状态。当然也有“好消息”，有人刚刚优化了“布氏开锁大法”。
那个技术小组在Trustwave的SpiderLabs实验室实现了这个改进方案，成功使之放进一支白板笔。他们将所有源代码和步骤公布，你也能做一根出来。

![](http://doask.qiniudn.com/turn-innocent-dry-erase-marker-into-hotel-hacking-machine2.jpg)

一块Arduino板、直流电源槽和一个5.6千欧电阻为材料，他们做了一个对Onity卡式电子锁基本适用的万能钥匙。他们用一个16兆赫的晶振作为时序，一枚A23 12伏电池驱动整个电路。

![](http://doask.qiniudn.com/turn-innocent-dry-erase-marker-into-hotel-hacking-machine3.jpg)
![](http://doask.qiniudn.com/turn-innocent-dry-erase-marker-into-hotel-hacking-machine4.jpg)

  
在他们的博客(http://blog.spiderlabs.com/2012/10/pentesting-hotels-with-pens.html)里，你能找到电路图的更多细节，以下的片段演示了这玩艺如何运作。

客官，看完这篇之后，住宿吗？

>[摘录自SpiderLabs的博客](http://blog.spiderlabs.com/2012/10/pentesting-hotels-with-pens.html)
詹士邦白板笔——酒店渗透入侵笔
---
你也许看过科迪•布罗修斯用一块Arduino如何破解Onity酒店房门锁的演讲和演示，真乃007詹士邦也。若能将其缩小，变成一支白板笔或钢笔大小岂不更好？作为一名Trustwave SpiderLabs实验室的安全测试员，我随便就能拿到不同的笔，蓝的、红的、绿的，当然也有最常见最呆板的黑笔。大多数的笔书写畅顺，有时我不禁在想，为虾米老板给我钱去试笔呢？跑题了。最初的想法是把所有零部件塞进一支钢笔里，很快我们发现这显然不可能。于是我们就挑选了白板笔。
我不详细说明破解流程和原理的技术细节了，柯迪在他的个人网站http://demoseen.com/bhpaper.html已经说得很详细了。如果你对破解技术本身有任何疑问或想知道任何细节，最好去问他，谁叫他是始作俑者呢？我嘛，不过把这玩意儿做小罢了。:)
既然我们目的明确，那就准备器材吧。你需要下列东西来制作和测试这一套装置：
•1块Arduino板（几乎任何型号都行，科迪用了一块Arduino Mega 128）
•1个直流电源插槽，5毫米外径，2.1毫米内径。
•1个5.6千欧电阻
•1个Onity门锁
我手上已有了一个门锁，是从eBay买的吗？我不记得了。下一步我们准备块Arduino，这也不是什么难事，每个黑客乃至于他们的奶奶都该有超过50片在手头上。我前几年在国防部的“世界首席黑客大赛”上赢取的那片现在拿来用了。电源槽和转接器这些我身边都有。
用以上的零件我做了个Arduino电路，载入科迪在http://demoseen.com/bhpaper.html公布的Arduino程序框架。测试表明，它运行起来就像插上电源线那样容易，我们只需等等锁上的绿灯亮起就完事了。既然这玩意儿能使，那我就开始做个适合白板笔大小的原型机出来。
我从这儿的黑客空间寻求我朋友乔什•克鲁格和乔丹•本克关于电路图方面的帮助。我们知道电路需要晶振来有效计时，使程序代码工作，从而开启门锁。同时，Arduino需要3到5伏电压，而连在一根线上的数码3引脚则需要3.3伏电压工作。将电路体积缩小并不太难，痛苦的是以手上有限的工具完成它。在设计上几经周折，我们当晚决定用以下部件来完成它。
•1个ATMega328单片机模块（已预装程序框架）
•1个5.6千欧电阻
•1个30欧电阻
•1个16兆赫晶振
•3.3伏稳压管
•1个A23 12伏电池
•1个迷你单掷开关（常闭）
•1条直流电源插线，外径5毫米，内径2.1毫米。
•1块实验板，1.75乘1.5英寸大小。
照着下图接线，你该可以做一个自己的酒店客房开门笔。
![](http://doask.qiniudn.com/turn-innocent-dry-erase-marker-into-hotel-hacking-machine5.jpg)
 
Your finished product should look something like this.
成品看起来该像下图那样。
![](http://doask.qiniudn.com/turn-innocent-dry-erase-marker-into-hotel-hacking-machine2.jpg)
![](http://doask.qiniudn.com/turn-innocent-dry-erase-marker-into-hotel-hacking-machine3.jpg)
![](http://doask.qiniudn.com/turn-innocent-dry-erase-marker-into-hotel-hacking-machine4.jpg)

放上大家都喜闻乐见的演示视频，主演：白板笔、我的酒店客房锁。
