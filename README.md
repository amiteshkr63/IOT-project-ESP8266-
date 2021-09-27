# OBJECTIVE:
## Develop a complete IOT system we can activate parts of an IOT device from remote browsers as well as voice prompt through Google Home on your smartphone.

***********************************************************************************************************************************************************************************
### Development of IOT system
#### Steps Involved:
##### 1)Hardware design and Cabling sensors
##### 2)Firmware Programming(Arduino IDE)
##### 3)Cloud Server Building and Configuration
##### 4)MQTT installation cofiguration Publish/Subscribe Programming
##### 5)Domain name registration
##### 6)Django web server for IOT installation Configuration programming
##### 7)SSL Certificate Data encryption for IOT
##### 8)Google Home Linking Action Fullfilment endpoint programming
***********************************************************************************************************************************************************************************
### Hardware needed:
##### 1)ESP8266/NodeMCU
##### 2)Relay module
##### 3)Temperature sensor
##### 4)Motion Sensor
##### 5)Buzzer
##### 6)RGB Led
##### 7)Solid state Relay
***********************************************************************************************************************************************************************************
#### PIN Connections:
  D0:  Relay, When 0 is applied, relay is activated
  
  D2:  P0, solid state switch
  
  D3:  LED_RED
  
  D4:  LED_GREEN
  
  D5:  LED_BLUE
  
  D6:  I/O   ; Will connect motion sensor to this
  
  D7:  I/O   ; will connect DHT11 temp/humidity sensor to this
  
  D8:  Buzzer 

![Screenshot (1679)](https://user-images.githubusercontent.com/88953654/134885998-6c5e7e4d-4b61-4493-872f-82511caa7a83.png)

In ARDUINO IDE, Make these following changes:
1) Open arduino IDE

2) Go to File -> preferences 
On that page, add the following in the Additional Boards Manager URL
http://arduino.esp8266.com/stable/package_esp8266com_index.json

3) Click on Tools -> Boards -> Boards Manager
Search for ESP8266
And, Install esp8266 by ESP8266 Community

4) Now, select the board
Click on Tools -> Board -> ESP8266 boards -> NodeMCU 1.0 (ESP-12E Module)

5) Click Tools -> Upload speed -> 115200

6) Connect your board to a USB port of your computer.
Then power ON the board
Then click on Tools -> Port -> Select the appropriate serial port

7) Open Serial Monitor of the Arduino by clicking the button on the right top
corner of the arduino IDE window. Then, check is baud rate at the bottom tabs.
By default, it may be 9600. Change it to 115200

8) Install DHT sensor library by Adrafruit
click on sketch -> include library -> Manage Library.
Then, Type DHT11 in the right field
That will show this library along with a few others.
Click on Install

