# 便携式太阳能USB充电器

标签：太阳能 USB充电器

--- 
>[原文链接](http://www.instructables.com/id/Portable-Solar-USB-Charger/?ALLSTEPS) 作者: jenfoxbot   翻译:BigBear

![](http://doask.qiniudn.com/Portable%20Solar%20USB%20Charger_1.jpg)

便携式USB充电器对于户外探险，旅游和节日庆祝活动来说是非常有用的。在便携式USB充电器上添加一个太阳能电池板可以让你的移动电源在户外拥有无穷的电力来源。这个DIY仅仅花费20美刀就能够轻松完成。

##步骤一：材料

![](http://doask.qiniudn.com/Portable%20Solar%20USB%20Charger_2.jpg)

* 太阳能电池板（输出最小功率4W，当然如果银子足够建议选择更高功率的太阳能电池板）
* [1N914二极管](http://www.browndoggadgets.com/products/1n914-diode)
* （也可以用类似系列的二极管替代）
  二极管具有单向导电性，其在电路中的作用是确保电流的方向为从太阳能电池板到电池，从而保护电路的安全。如果你选择其他类型的二极管，请确保二极管的额定电流和电源与太阳能电池板的电流和电压参数匹配。
* [ USB车载充电器](http://www.browndoggadgets.com/products/1n914-diode)
* 9V可充电电池
  如果你想给苹果的设备充电，那么你需要2节9V可充电电池。
USB车载充电器从车内电源得到的电压时直流12V，但是实际上USB车载充电器可接受的输入电压范围为6VDC到14.5VDC。使用一个9V电池可以最容易从太阳能电池板得到充足的电压并给USB电路输出5V直流电压。
* [9V电池夹]
* 工具箱（例如保鲜盒、薄荷糖盒子或者点心盒子等）
万事俱备，只欠开工！


##步骤二：工具
![](http://doask.qiniudn.com/Portable%20Solar%20USB%20Charger_3.jpg)

*  剥线钳
也可以用剪刀替代，用剪刀割开电线的一圈，用手指剥掉绝缘层即可。
*  电工胶布
*  环氧树脂胶水或者其他类似的粘合剂（例如大猩猩胶水gorilla glue）
*  电烙铁
也可以将线头缠起来，用环氧树脂胶水固定。
*  万用表
万用表可以用来测试电路的连接正确与否。

##步骤三：USB接口介绍
![](http://doask.qiniudn.com/Portable%20Solar%20USB%20Charger_4.jpg)

正如图片所示，USB充电器有4针。所有USB充电器都由Vcc引脚输出直流5V电压。USB充电器的输出[电流](http://en.wikipedia.org/wiki/Electric_current)与USB充电器的型号有关。主要有3种主要类型的充电器：标准接口（500mA），快速充电接口（1500mA）和专用充电接口（900mA）。
苹果的USB充电器有些特别，数据引脚的电压是2.7V直流。所以如果你制作完毕你的便携式USB充电器并且你想给你的iPhone或者ipod充电，你需要提升你的电压。可以通过更高电压的电池或者用两节9V电池[串联](http://en.wikipedia.org/wiki/Series_and_parallel_circuits)完成。

##步骤四：开始动手！第一部分
![](http://doask.qiniudn.com/Portable%20Solar%20USB%20Charger_5.jpg)
注：如果你用胶水粘结的方法去连接电线，在你测试过所有电路正确之后再用胶水粘结，环氧树脂胶水是永久的密封，一旦密封后就不容易恢复了。
1.剥掉太阳能电池板末端电线的绝缘皮（使之漏出一定长度的导体）
太阳能电池板导线没有标正负或者没有电烙铁怎么办，这里有一个简单的方法，将太阳能电池板导线用电工胶带粘在背面，用万用表量一下正负或者连接在汽车USB充电器上使充电[LED](http://en.wikipedia.org/wiki/Light-emitting_diode)灯亮。用胶水固定，风干搞定。

2.把二极管和太阳能电池板正极相连，最好用电烙铁焊接好。
如果没哟电烙铁，将线头缠好，用环氧树脂固定。
重要提示：而接管有银色环的一端要和电池相连，如上图所示。
##步骤五：开始动手！第二部分
![](http://doask.qiniudn.com/Portable%20Solar%20USB%20Charger_7.jpg)

3.连接二极管的正极（红色）到电池夹正极，太阳能电池板负极（黑色）到电池夹负极。电路一断设计成可随意移动的，相当于一个简易开关。
4.一般USB车载充电器的前端金属部分是正极，侧边是负极和地。也可以通过以下的方法来测试USB车载充电器的负极或地。

*  打开车载充电器，查看正负极金属片与那个线相连接。
*  使用太阳能电池板驱动充电器。连接电池或者太阳能电池板的正极到充电器前端金属片，用电池或者太阳能电池板的负极触碰侧边的金属片，如果连接的金属片是负极，那么充电器的充电led灯会亮起。

##步骤六：开始动手！第三部分
![](http://doask.qiniudn.com/Portable%20Solar%20USB%20Charger_9.jpg)
5.连接电池和太阳能电池板的负极和USB车载充电器的负极，电池和太阳能电池板的正极和USB车载充电器的正极。根据你拥有的工具的不同可以用不同的方式实现，最简单的方法是用小鳄鱼嘴夹子（当调试完毕后用环氧树脂胶水固定好）。
6.测试。连接一个USB设备（例如树莓派控制板），如果该USB设备正常工作，那么可以用环氧树脂将必要部分固定好。

##步骤七：享受时刻
![](http://doask.qiniudn.com/Portable%20Solar%20USB%20Charger_11.jpg)

如果你制作好了你的第一版作品，那么尽可能的去完善它吧！
课外补充小知识：
我用的太阳能电池板是1W，6V的，从[RadioShack](http://www.ebay.com/itm/New-Radioshack-1W-6V-Solar-panel-2770049-/191113892817?nma=true&si=1Z9cA9bqVrQMbVBcok1GVJq2SqY%253D&orig_cvip=true&rt=nc&_trksid=p2047675.l2557)灯上购买的,输出166mA电流。为了避免电池的过度充电，当充电完成时断开电路的连接。如果你的太阳能电池板功率大于6W，那么添加一个[充电控制](http://en.wikipedia.org/wiki/Charge_controller)器是很有必要的。[这里](https://www.google.com/?gws_rd=ssl#tbs=p_ord:p&tbm=shop&q=solar+charge+controller)列出了不同型号充电控制器，你可以根据你的需要选择。
太阳能电池板的能量转换效率较低，大概只有12%~15%。最近的科研正在不断提高太阳能的能量转换效率，德国的一个实验室已经创造了44.7%的太阳能转换效率记录。
在2012年，每瓦特太阳能能量的转换成本在$1~$2之间，最低的在$0.7每瓦特。虽然这不包括其他的硬件成本（例如电池，变压器等等），随着成本的降低，太阳能已经越来越有可能替代传统的化石燃料了！






