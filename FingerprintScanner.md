# 给你的房子DIY一个指纹门禁开关

>[原文链接](http://www.instructables.com/id/DIY-Fingerprint-Scanning-Garage-Door-Opener/) 作者:nodcah  翻译:showerwu

标签（空格分隔）： 门禁 指纹扫描 3D打印

---

![](http://huohua.qiniudn.com/FingerPrint01.jpg)

##1.简介

对于一个出门经常忘带钥匙而被不幸锁在门外的人来说，等待着家人帮忙开锁或者请开锁匠暴力开锁简直就是一场噩梦，简直是“劳民伤财”。为了这个解决这个问题，本项目使用一个超赞的[fingerprint scanner](https://www.sparkfun.com/products/11836)来制作一个可以安装在门上的指纹门禁开关。这样不喜欢带钥匙的小伙伴就不用困扰于被不幸锁在门外所带来的不安了，用指纹识别技术你就可以轻松的出入自如。当然，我们的这个项目不仅仅用于门禁，还有很多有趣有用的场景等着你去挖掘。

##2.清单

![](http://huohua.qiniudn.com/FingerPrint03.jpg)

![](http://huohua.qiniudn.com/FingerPrint04.jpg)

###2.1材料

|元件|	供应商|
|--|--|
|Fingerprint scanner指纹扫描模块 |[Sparkfun](https://www.sparkfun.com/products/11836) |
|JST connector for Fingerprint scanner|[Sparkfun](https://www.sparkfun.com/products/10359) |
|串口LCD显示套件(w/ATmega328)	|[Sparkfun](https://www.sparkfun.com/products/10097) |
|ATtiny85芯片|	[Sparkfun](https://www.sparkfun.com/products/9378)|
|PNP三级管|	[Sparkfun](https://www.sparkfun.com/products/522)，[Radioshark](http://www.radioshack.com/product/index.jsp?productId=2062609)|
|蜂鸣器|[Sparkfun](https://www.sparkfun.com/products/7950)，[Radioshark](http://www.radioshack.com/product/index.jsp?productId=2062402)|
|功放线|[Radioshark](http://www.radioshack.com/product/index.jsp?productId=2036278&retainProdsInSession=1&znt_campaign=Category_CMS&znt_source=CAT&znt_medium=RSCOM&znt_content=CT2032227)|
|3D打印外壳|参考步骤3.8中提供的3D建模文件|
|铜带|[Amazon](http://www.amazon.com/gp/product/B0086769IQ/ref=oh_details_o01_s00_i00?ie=UTF8&psc=1)|
|5v稳压器|[Sparkfun](https://www.sparkfun.com/products/107)|
|9v电池|[Sparkfun](https://www.sparkfun.com/products/10218)|
|9v电池连接器|[Sparkfun](https://www.sparkfun.com/products/91)|
|SPDT limit switch限位开关|[Sparkfun](https://www.sparkfun.com/products/98)|



###2.2工具:

- 电烙铁
- 电线若干
- 跳线若干
- 剥线钳
- 钻子、螺丝刀、螺丝
- 电路母板
- 测试用的LED若干
- [5V FTDI board](https://www.sparkfun.com/products/9716)
- 热胶枪
- 3D打印机
- 可选工具：IC holder (8 pin for ATtiny and 28 pin for ATmega)
- 可选工具：Arduino board/10uF capacitor (参考步骤3.4的细节)

##3.组装


###3.1 电路原理图

![](http://huohua.qiniudn.com/FingerPrint10.jpg)

根据上面的电路原理图搭建电路。整个电路主要是由串口LCD显示模块、ATtiny85芯片、指纹识别模块、蜂鸣器和限位开关等几个电子部件组成。其中串口显示模块用来显示交互信息，指纹识别模块用来进行指纹识别，蜂鸣器用来发出操作提示音，限位开关用来控制电源的供给（系统不工作室可节省电池电量）

**串口LCD模块的引脚说明**
|引脚号|接驳说明|
|--|--|
|D10|指纹识别模块2号引脚 (through voltage divider)|
|D11|FPS pin 1 (黑线)|
|D12|ATtiny85芯片|
|D13|蜂鸣器|

**ATiny85芯片引脚说明**
|引脚号|接驳说明|
|--|--|
|Pin5（代码中编号0）|由ATmega（LCD）芯片输入|
|Pin3（代码中编号4）|三极管/黄色LED|
|Pin7（代码中编号2）|LED指示灯|

###3.2 焊接LCD显示模块

![](http://huohua.qiniudn.com/FingerPrint11.jpg)

关于如何进行焊接，Sparkfun上有[手把手教你如何进行电路焊接](https://www.sparkfun.com/tutorials/289)的教程

###3.3 焊接电路板

![](http://huohua.qiniudn.com/FingerPrint16.jpg)

按照上面示意图所示在电路母板上焊接各个模块。电路板如何布局可以自行掌握，但是需要注意应尽量让指纹识别模块的线朝向一个方向，这样才保证线路不会折断。

当所有模块焊接完毕后，用热胶枪将电路板正反两面的焊点进行固定和绝缘。
###3.4 给ATmega328芯片编写LCD的控制程序
