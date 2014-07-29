# CoolDrink--炫酷酒杯座

>[原文链接] (http://makezine.com/projects/vampire-flashlight/)  作者:Sean Michael Ragan 翻译:AD（ldq370125）

标签（空格分隔）： 酒杯座 LED 

---

![] (http://huohua.qiniudn.com/CoolDrink01.jpg)

## 1 简介

还在使用淘宝上买的硅胶杯垫么？
还在使用商店里买的普通杯座么？
有没有觉得它们都已经弱爆了啊！
PARTY上没有什么值得炫酷吊炸天的奇思妙玩？
BAR里面没有值得让顾客眼前一亮的新鲜玩意？

这儿给你一个超级炫酷，但制作十分简单的东东——炫酷酒杯座！

## 2 清单
### 2.1 材料
- 绿色LED X2
- 红色LED X2
- 黄色LED X2
- 13×24×1/8" 透明压克力透明亚克力板 X1
- 比较器IC X1
- 与非门IC X1
- 压敏电阻 X1
- 面包板 X1
- 1K电阻 X2
- 680K电阻 X3
- 56K电阻 X1
- 6.8K电阻 X1
- 9V电池 X1
- 9V电池连接线 X1
- 橡皮筋 X2

### 2.2 工具
- 电烙铁
- 钢丝钳
- 剥线钳
- 尖嘴钳
- 激光切割机（没有的话可以外出加工）

## 3 组装
### 3.1 电路
![] (http://huohua.qiniudn.com/CoolDrink03.jpg)

关于电路的原理可以不用了解的过于详细，不过这儿给大家列出这个电路的逻辑列表，以供参考：

| 压力        | 比较器1输出（红LED）   |  与非门输出（黄色） |  比较器2输出（绿LED） |
| --------   | :-----:  | :----:  | :----:  |
|低|低|高|高| 
|中|高|低|高| 
|高|高|高|低| 

### 3.2 利用亚克力板制作基底

首先，使用透明的亚克力板设计基底，是为了光线能够透出来，使效果更加炫丽。
这个基底完全可以凭自己的喜好进行自由发挥，这儿将给出我的设计方案，如下图所示。

![] (http://huohua.qiniudn.com/CoolDrink05.jpg)

![] (http://huohua.qiniudn.com/CoolDrink06.jpg)

![] (http://huohua.qiniudn.com/CoolDrink07.jpg)

我做了12片的部件，其中有：1个大底，6片舱体，1片大圆（用以放置LED），1片可以透出LED并托住压敏电阻的盖板A，1片可以透出LED并露出压敏电阻的盖板B，2片大圆。具体安装方式可以参考下文成品。

### 3.3 电路组装
- 将9V电源线焊接在面包板上。

![] (http://huohua.qiniudn.com/CoolDrink08.jpg)

- 将比较器IC与与非门IC插入面包板

![] (http://huohua.qiniudn.com/CoolDrink09.jpg)

- 将电阻连入

![] (http://huohua.qiniudn.com/CoolDrink10.jpg)

- 补充相应的连线

![] (http://huohua.qiniudn.com/CoolDrink11.jpg)

- 将所有的LED交叉着插入盖板A，最好用胶水适当粘合一下，以防脱落。将针脚弯向中心位置。

![] (http://huohua.qiniudn.com/CoolDrink12.jpg)

- 把相同颜色的LED并联在一起后串联一个680kΩ电阻，另一侧则连接到相应的比较器IC或者与非门IC上。

![] (http://huohua.qiniudn.com/CoolDrink13.jpg)

- 连入压敏电阻。

![] (http://huohua.qiniudn.com/CoolDrink14.jpg)

- 将亚力克板的大底、舱体等与面包板电路组合起来，并用橡皮筋固定住。

![] (http://huohua.qiniudn.com/CoolDrink15.jpg)

- 9V电池的放置方式

![] (http://huohua.qiniudn.com/CoolDrink16.jpg)

## 4 成果

有了这么一个炫酷的酒杯底座，那么在聚会时，你将会是最闪耀的那一位！

![] (http://huohua.qiniudn.com/CoolDrink25.jpg)





