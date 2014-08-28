# 这货是机械外挂！在它面前，好吧，我们都停下来了。
作者：Valentin Heun 编者&译者：Kalimov
标签（空格分隔）： Arduino 外挂 电路
---
不得不说一句，作者没有过多说明其中原理，只是给了个电路图、程序代码，还有……就是当时的心情。
"After a few addicted minutes, I thought why not making an Arduino playing Timberman for me."
“在沉迷了几分钟后，我想，何不做一个Arduino帮我玩《疯狂伐木工》呢？”
这个想法，对于手机游戏控来说注定要被鄙视。那种“根本停不下来”类型的游戏，给他这种想法污染过后，让疯狂在被窝打了一晚上飞机（别想歪了）的手机游戏控情何以堪啊？（其实编者本身也有这种想法，让高分榜上的高手一夜回到解放前。）
Valentin Heun瞄准了这个游戏的一个特点——树枝出现非左即右，只要时机合适就切换位置。他用一个光敏元件紧贴屏幕，只要有树枝划过就输入控制信号。而代替手指触摸平板电脑或手机用的电容屏的角色，就靠机械臂，哦不，电子工程的人咋能用机械这么粗鲁的词呢？就用电子控制开关来代劳了。通过电磁继电器接通开关改变电容屏接触点上电容值的变化，模拟人手触碰的效果，这就是为啥所有电阻都选1千欧的原因了——人体的电阻大概在1千欧左右。
看过下面的演示视频，奉劝各位手机游戏控，别鄙视作者，比起用八门神器，这有创意多了。（你觉得八门神器能修改这不能暂停的游戏？嘿嘿。）

用Arduino玩《疯狂伐木工》
>[原文链接](https://github.com/vheun/ArduinoPlaysTimberman)
>[原文链接](http://vimeo.com/101663279)
以下介绍一个程序，用Arduino玩手机游戏《疯狂伐木工》，最高得分记录：2417。
演示视频： https://vimeo.com/101663279
使用元件：
•	已连接上TIP120三极管（可用许多常见NPN三极管代替TIP120型号）的JZC-11F电磁继电器两个，分别连接到引脚4和8。
•	OP580DA光敏NPN三极管连接到A0。
•	开关连接到引脚7。
•	所有电阻都是1千欧。
安装：
将光敏三极管放在屏幕背景树木的右上方，第三级树枝正好会经过的地方。
电路设计外观（一切以实物为准）：
![](http://doask.qiniudn.com/ArduinoPlaysTimberman.png) 
程序代码：
/*
	 Arduino Plays Timberman
	
	 A simple programm for Arduino that plays Timberman.
	
	Circuit:
	 * JZC-11F RELAYS attached to TIP120 attached to pins 4 and 8
	 * OP580DA PHOTODARLINGTON NPN attached to A0
	 * BUTTON attached to pin 7
	
	 created July 23th 1014
	 by Valentin Heun
	 */
	
	
	int left = 4; int right = 8;
	int button = 7; int timing = 23;
	int Buffer[] = {0, 0, 0, 0, 0};
	int startstate = 0;
	
	void setup() {
	  pinMode(left, OUTPUT); pinMode(right, OUTPUT);
	  pinMode(button, INPUT); digitalWrite(button, HIGH);
	}
	
	void loop() {
	  //realise the axe
	  digitalWrite(left, LOW);  digitalWrite(right, LOW);
	
	  // update the buffer
	  if (startstate > 0) {
	    for (int i = 3; i > 0; i--) {
	      Buffer[i] = Buffer[i - 1];
	    }
	
	    // read a couple of frames and determan if a branch had crossed the sensor
	    Buffer[0] = 0;
	    for (int i = 0; i <= timing; i++) {
	      delay(4);
	      //delayMicroseconds(200);
	      
	      int analog = analogRead(A0);
	      if ((analog > startstate + 5) || (analog < startstate - 5)) {
	        Buffer[0]  = 1;
	      }
	    }
	  }
	
	  // set start value for the sensor
	  if (digitalRead(button) == HIGH) {
	    if (startstate == 0) {
	      startstate = analogRead(A0);
	    }
	
	    // timberman cutts around the right side of the branches.
	    int theswitch = Buffer[1];
	    if (Buffer[2] == 1 && Buffer[1] == 0) {
	      theswitch = 1;
	    }
	
	    // make the actuall cut
	    if (theswitch == 0) {
	      digitalWrite(left, HIGH);
	    }
	    else {
	      digitalWrite(right, HIGH);
	    }
	    delay(38);
	     
	  }
	  else {
	    // if switched off, set everything back to zero
	    startstate = 0;
	    for (int i = 0; i <= 4; i++) {
	      Buffer[i] = 0;
	    }
	  }
	}

