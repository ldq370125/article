# Ѱ�ȷ���

>[ԭ������] (http://www.instructables.com/id/Heat-Seeking-Desk-Fan-using-Arduino/?ALLSTEPS) 
����:ePums ����:AD��ldq370125��
��ǩ���ո�ָ����� Arduino ����

---

![](http://huohua.qiniudn.com/HeatSeekingFan1.jpg)

##1. ���
���Ǹ����ѧ����������
��hot�ޱȵ�����Ҳֻ��ס���ᡣ����
ס���ᵹ����ν������
�ؼ�������ȵ�����������˯����ʺһ��������
��Ϊľ�пյ�������
Ϊľ�пյ�������
ľ�пյ�������
�пյ�������
�յ�������
��������
������
����
��

���ϴ����Ⱥ����׾ͻᵼ�µڶ�������ĳ�����ֱ�����ʮ����ʹ������Ϊ���Ȳ������ܵġ�����
����һ����һ�����ܴ����Ⱦ����ҵ�target��
������������һ���Ƚϼ����ŵġ�Ѱ�ȷ��ȡ����������ȵ�ʱ����ܴ����磬����ʱ��Ͳ��ٴ��磡
    
##2. �嵥
###2.1 ����
- ��������� MLX90614 X1
- �ŷ���� X1
- Arduino UNO X1
- 12V DC ���Է��� X1
- 12V��Դ������ X1
- ���۽� X1
- 6x8" ���ð� X1
- ��������

###2.2 ����
- ������
- ���۽�ǹ

##3. ��װ
### 3.1 �¶ȴ���������
������Ҫ����һС�����ð壬���Է����¶ȴ�����������������ǡ�����������������ð������۽�ճ����һ�����ð�ߴ�Ĵ�С���Ը�����ķ��ȴ�С�����ᣬ������ͼƬ���Բο���
��������ǵ�����ʮ����Ҫ�������б����±���ʾ��
|�¶ȴ�����|Arduino UNO|
| :-----: | :-----:|
|SDA(DATA)|A4 analog|
|SCL(CLOCK)|A5 analog| 
|VCC|3.3V|
|GND|GND| 

![](http://huohua.qiniudn.com/HeatSeekingFan2.jpg)

![](http://huohua.qiniudn.com/HeatSeekingFan7.jpg)


### 3.2 �ŷ��������

�����ŷ�����Ĺ�������̫������������Ҫ������ŷ������5V��Դ�������б����±���ʾ��

|�ŷ����|Arduino UNO|����5V��Դ|
| :-----: | :-----:| :-----:|
|��ɫ������|Pin 9|/|
|VCC|/|5V|
|GND|/|GND|

![](http://huohua.qiniudn.com/HeatSeekingFan3.jpg)

### 3.3 ��������

һ����Է��ȵĵ�ѹ���Ƚϴ���12V����Ƚϳ������������������Ҫһ��12V��Դ���������硣
���Ƚ���һ��С���غ󣬸�12V��Դ������������

![](http://huohua.qiniudn.com/HeatSeekingFan4.jpg)


### 3.4 ����
���Ƚ����к�������ǵ����ð������۽�ճ���ڷ��ȵĳ����һ�������ת���ϣ������Ϳ��Ա������ð嵲ס��ĳ�·��
Ȼ�����ŷ�����ϰ�װһ�������������ȹ̶��ڵ����ϡ�

![](http://huohua.qiniudn.com/HeatSeekingFan5.jpg)

�ŷ������Ҫ�̶���һ������ĵ��������Ա����ȶ��������ʹ���ݶ����߼򵥵�Ľ������й̶���

![](http://huohua.qiniudn.com/HeatSeekingFan8.jpg)


##5 �������

��������Ҫ����������Arduino UNO��ȡ���⴫�������¶ȡ�
�����沽��������

- ���롰i2cmaster���⣺
   ����[����](http://huohua.qiniudn.com/i2cmaster.zip)���ء�i2cmaster.zip���ļ�����ѹ����/{arduino root}/hardware/libraries�����i2cmaster.h and twimaster.c�ļ�
- �޸Ĳ�����
  ��twimaster.c�ļ�������ʼ�Ĵ����޸ĳ����²�����


```python
#ifndef F_CPU
#define F_CPU 16000000UL
#endif

/* I2C clock in Hz */
#define SCL_CLOCK 50000L
```
  
- ��������ܹ���Serial monitor�п����¶ȵĴ��룬��Ϊ���Դ��룺

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
  
- ����ʹ����Ѱ�ȵ����մ���������ʾ��

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
  
## 6 �ɹ�չʾ
���Ѱ�ȷ��ȵ�ת���Ƕ�Ϊ120�㣬����������ģ������Լ��Ķ�����Ĵ��룬������Ϳ��԰����Լ�����Ը��������̨��Ѱ�ȷ��ȡ�����

![](http://huohua.qiniudn.com/HeatSeekingFan1.jpg)

![](http://huohua.qiniudn.com/HeatSeekingFan6.jpg)









