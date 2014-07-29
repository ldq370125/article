# 用ardunio 制作无刷万向节“我是大标题”
>[原文链接](http://www.instructables.com/id/Brushless-Gimbal-with-Arduino/?ALLSTEPS) 作者:Jonah Grubb 翻译:石头

“翻译文章一定要注明原文链接，作者，及翻译者。”

**tag: arduino 无刷**

##1.简介

用Arduino只玩玩LED是不是已经玩腻了呢？

是不是看过别人各种各样的机器人，自己也很心动呢？

既然Arduino这个平台强大到无所不能，我们何不做一个自己的小机器人呢？

下面就跟着我的节奏一起“摇摆摇摆”吧！啊。。。不对，跟着我们的BoB机器人一起摇摆摇摆吧！

![](http://doask.qiniudn.com/openbook9-brushless1.jpg)
>这是图片介绍

![](http://doask.qiniudn.com/openbook9-brushless2.jpg)
>这是图片介绍

![](http://doask.qiniudn.com/openbook9-brushless3.jpg)
>这是图片介绍


##2.清单
###2.1.材料

+ Arduino套件（如果能用更小一点的开发板会更好） X1

+ 模拟舵机X4

+ 电池组

+ 3D打印部件

+ 超声波传感器 X1

###2.2.工具

+ 螺丝刀

+ 锉刀

##3.组装
###3.1.组装1

视频
<iframe height=498 width=510 src="http://player.youku.com/embed/XNzM0MDk5ODQw" frameborder=0 allowfullscreen></iframe>

###3.2.组装2

代码段

```c++
#include

Servo servo;

void setup()
{
  servo.attach(9);  // attaches the servo to digital pin 9
}


void loop()
{
    myservo.write(90);  //tells the servo to go to the center position
}


```

##4.软件

**我是加粗**如文中出现“注意:某某”时，则需对**注意**进行加粗处理

*我是倾斜*

***我是加粗倾斜***

##5.成果


| 0:0 | 1:0 |
| -- | -- |
| 0:2 | 1:2 |
|wre|sdf|
>我是表格

##6.评论

    我是引用，引用某人的说话，或对图片或表格做注释，则使用此种功能

```
或如此使用
这样也可以
```

编辑软件建议使cmd，https://www.zybuluo.com/mdeditor
