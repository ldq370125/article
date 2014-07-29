# 寻热风扇

>[原文链接] (http://www.instructables.com/id/Heat-Seeking-Desk-Fan-using-Arduino/?ALLSTEPS)  作者:ePums 翻译:AD（ldq370125）

标签（空格分隔）： Arduino 风扇

---

![](http://huohua.qiniudn.com/HeatSeekingFan1.jpg)

##1. 简介
我是个苦逼学生党。。。
巨hot无比的夏天也只能住宿舍。。。
住宿舍倒无所谓。。。
关键是这鬼热的天气，晚上睡觉会屎一样。。。
因为木有空调。。。
为木有空调。。。
木有空调。。。
有空调。。。
空调。。。
调。。。
。。。
。。
。

晚上吹电扇很容易就会导致第二天身体某个部分被吹得十分疼痛，是因为风扇不是智能的。。。
这样一来，一个智能吹风扇就是我的target！
下面我们来做一个比较简单入门的“寻热风扇”，让你在热的时候就能吹吹风，凉的时候就不再吹风！
    
##2. 清单
###2.1 材料
- 红外测温仪 MLX90614 X1
- 伺服电机 X1
- Arduino UNO X1
- 12V DC 电脑风扇 X1
- 12V电源适配器 X1
- 热熔胶 X1
- 6x8" 万用板 X1
- 导线若干

###2.2 工具
- 电烙铁
- 热熔胶枪

##3. 组装
### 3.1 温度传感器连线
我们需要切下一小块万用板，用以放置温度传感器，即红外测温仪。将红外测温仪与万用板用热熔胶粘合在一起。万用板尺寸的大小可以根据你的风扇大小来定夺，下文有图片可以参考。
红外测温仪的连线十分重要。连线列表如下表所示：
|温度传感器|Arduino UNO|
| :-----: | :-----:|
|SDA(DATA)|A4 analog|
|SCL(CLOCK)|A5 analog| 
|VCC|3.3V|
|GND|GND| 

![](http://huohua.qiniudn.com/HeatSeekingFan2.jpg)

![](http://huohua.qiniudn.com/HeatSeekingFan7.jpg)


### 3.2 伺服电机连线

由于伺服电机的工作电流太大，所以我们需要额外给伺服电机供5V电源。连线列表如下表所示：

|伺服电机|Arduino UNO|额外5V电源|
| :-----: | :-----:| :-----:|
|橙色数据线|Pin 9|/|
|VCC|/|5V|
|GND|/|GND|

![](http://huohua.qiniudn.com/HeatSeekingFan3.jpg)

### 3.3 风扇连线

一般电脑风扇的电压都比较大，以12V供电比较常见，所以这儿我们需要一个12V电源适配器供电。
风扇接入一个小开关后，跟12V电源适配器相连。

![](http://huohua.qiniudn.com/HeatSeekingFan4.jpg)


### 3.4 合体
首先将带有红外测温仪的万用板用热熔胶粘合在风扇的出风口一侧的中心转轴上，这样就可以避免万用板挡住风的出路。
然后在伺服电机上安装一个底座，将风扇固定于底座上。

![](http://huohua.qiniudn.com/HeatSeekingFan5.jpg)

伺服电机需要固定在一个更大的底座上用以保持稳定。你可以使用螺钉或者简单点的胶带进行固定。

![](http://huohua.qiniudn.com/HeatSeekingFan8.jpg)


##5 代码测试

我们首先要做的是利用Arduino UNO获取红外传感器的温度。
按下面步骤来做：

- 导入“i2cmaster”库：
   到此[链接](http://huohua.qiniudn.com/i2cmaster.zip)下载“i2cmaster.zip”文件，解压后，在/{arduino root}/hardware/libraries下添加i2cmaster.h and twimaster.c文件
- 修改参数：
  打开twimaster.c文件，将开始的代码修改成如下参数：


```python
#ifndef F_CPU
#define F_CPU 16000000UL
#endif

/* I2C clock in Hz */
#define SCL_CLOCK 50000L
```
  
- 下面代码能够在Serial monitor中看到温度的代码，作为测试代码：

```python
#include 

void setup()
{
Serial.begin(9600);
i2c_init(); //Initialise the i2c bus
PORTC = (1 << PORTC4) | (1 << PORTC5);//enable pullups
}

void loop()
{
int dev = 0x5A<<1;
int data_low = 0;
int data_high = 0;
int pec = 0;
i2c_start_wait(dev+I2C_WRITE);
i2c_write(0x07);


i2c_rep_start(dev+I2C_READ);
data_low = i2c_readAck(); //Read 1 byte and then send ack
data_high = i2c_readAck(); //Read 1 byte and then send ack
pec = i2c_readNak();
i2c_stop();

//This converts high and low bytes together and processes temperature, MSB is a error bit and is ignored for temps
double tempFactor = 0.02; // 0.02 degrees per LSB
double tempData = 0x0000;
int frac;

// This masks off the error bit of the high byte, then moves it left 8 bits and adds the low byte.
tempData = (double)(((data_high & 0x007F) << 8) + data_low);
tempData = (tempData * tempFactor)-0.01;
tempData = tempData - 273.15;
Serial.print((int)tempData); //Print temp in degrees C to serial
Serial.print(".");
tempData=tempData-(int)tempData;
frac=tempData*100;
Serial.println(frac);
delay(500); 
}

```
  
- 可以使风扇寻热的最终代码如下所示：

```python
//**TrackFan**//
//Code and concept by ePums
//tempRead code by Dave Eaton and SensorJunkie

#include <Servo.h>
#include <i2cmaster.h>

Servo mrservo;

int j = 0;
int pos;
int posVals[]= {
  0, 10, 20, 30, 40, 50, 60, 70, 80, 90, 100, 110, 120
};
double tempVals[12];
int hotPos;

void tempRead(){

  //Define function for reading the temperature from the IR Sensor.
  int dev = 0x5A<<1;
  int data_low = 0;
  int data_high = 0;
  int pec = 0;
  i2c_start_wait(dev+I2C_WRITE);
  i2c_write(0x07);


  i2c_rep_start(dev+I2C_READ);
  data_low = i2c_readAck(); //Read 1 byte and then send ack
  data_high = i2c_readAck(); //Read 1 byte and then send ack
  pec = i2c_readNak();
  i2c_stop();

  //This converts high and low bytes together and processes temperature, MSB is a error bit and is ignored for temps
  double tempFactor = 0.02; // 0.02 degrees per LSB
  double tempData = 0x0000;
  int frac;

  // This masks off the error bit of the high byte, then moves it left 8 bits and adds the low byte.
  tempData = (double)(((data_high & 0x007F) << 8) + data_low);
  tempData = (tempData * tempFactor)-0.01;
  tempData = tempData - 273.15;

  tempVals[j] = tempData;
  j+=1;
}


void servoSweep(){
  Serial.println("servoSweep initialize!");
  j = 0;
  pos = 0;
  //reset pos and temp indices
  delay(500);
  Serial.println("Positions:");
  //return servo to initial position
  for (pos = 0; pos < 130; pos +=10)
  {
    mrservo.write(pos);
    //move servo 10 degrees
    delay(200);
    //allow sensor to settle
    tempRead();
    Serial.println(pos);
    //read and store temp data
    delay(300);
  }
}

void findHot(){
  Serial.println ("findHot started!");
  //find highest temperature, move servo to corresponding position
  int i = 0;
  //local search index
  int q = 0;
  double hotTemp = tempVals[0];
  //the position data associated with the highest temperature in a given sweep
  for (i=0; i < 13; i+=1) {
    if (tempVals[i] >= hotTemp) {
      hotTemp =tempVals[i];
      Serial.print("#" + String(i) + " hot Temp: ");
      Serial.println(hotTemp);
      delay(50);
      q = i;
      //retrieve index for highest temp value in tempVals array
    }
  }
  hotPos = posVals[q];
  Serial.println("hotPos: ");
  Serial.print(hotPos);

  //retrieve the corresponding pos value from posVals index
  if (mrservo.attached()) {
    Serial.println("this is reading output right now");
  }
  delay(1000);
  mrservo.detach();
  mrservo.attach(3);
  mrservo.write(hotPos);
  delay(1000);
  //move the servo
  Serial.println("Returning to hotPos");
 
  
  /////////**DELAY BETWEEN SCANS**//////////////// 
  delay(10000);

  i=0;
}


void setup(){
  Serial.begin(9600);
  i2c_init();
  PORTC = (1 << PORTC4) | (1 << PORTC5);
}

void loop(){
  mrservo.attach(3);
  delay(1000);
  mrservo.write(0);
  i2c_init();
  servoSweep();
  Serial.println("Temperatures!");
  for (int n=0; n < 13; n += 1) {
    Serial.println(tempVals[n]);
    delay(50);
  }
  findHot();

  mrservo.detach();
  delay(2000);
}

```
  
## 6 成果展示
这个寻热风扇的转动角度为120°，如果你有信心，可以自己改动上面的代码，这样你就可以按照自己的意愿来控制这台“寻热风扇”啦！

![](http://huohua.qiniudn.com/HeatSeekingFan1.jpg)

![](http://huohua.qiniudn.com/HeatSeekingFan6.jpg)









