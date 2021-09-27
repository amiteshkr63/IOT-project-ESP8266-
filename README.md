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

## BUILDING a CLOUD SERVER(GOOGLE CLOUD):
goto:
[https://console.cloud.google.com/compute](url)
There, create a project, if you do not have one already. Give the project any name or, leave it
as default My Project
Then, create an instance by clicking 'Create an Instance'
In the form that opens up,
>> In the Firewall section, check both 'Allow HTTP traffic' and 'Allow HTTPS traffic'
>> Leave everything else as default
>> Then press 'Create' button
This may take a few minutes. If everything is successfull,
it will show a page with the name of the instance.
It will also show its external ip address.

Logging in to the cloud server:
Create a rsa key pair to ssh to this server as per the steps below:
If you are using a macbook, or any unix OS, open a terminal and run the following command:
(If you are using Windows, you can open powershell and run this command.
(Or, you can use putty)
ssh-keygen -t rsa -C <user name>
--- where <user name> may be replaced with your user name
for example,
```ssh-keygen -t rsa -C amitesh```
When it prompts for file name to store the keys, you can either use the default,
or use any other file name.
Once completed, this command will generate two files.
They are private and public keys.
These files are saved at the location you entered in when it prompted.
Next, you need to enter the contents of the public key to metadata
of the cloud server as follows:
On the browser, go to .https://console.cloud.google.com/compute
Then, click on metadata
> Click on SSH Keys
> Then click on Add SSH keys
Note: If you have earlier added ssh keys to this server,
> There click on Edit
> Then click on +
> Then, paste the contents of the .pub file here
> Then press Save
Now, you can ssh to your cloud instance with the following command
from a terminal of your computer as follows:
(Microsoft Windows users can do this in a powershell, or use Putty)
  
```ssh -i <absolute path of private key file name> <user name>@<external ip address of cloud server>```
Example:

  ```ssh -i ~/.ssh/id_rsa amitesh@35.232.76.4```
where id_rsa is the name of the default private key.
Use the correct file path and file name of your private key as per what you have
chosen when running ssh-keygen command above
Hereafter, to login to the cloud server, use the above command
1.login to the cloud server and set root password

  ```sudo passwd```

2.Update server

  ```sudo apt-get update```

  ```sudo apt-get upgrade```

3.check python on your cloud server:

  ```which python3```

  ```python3 --version```

4.run the following command to install pip3:

  ```sudo apt install python3-pip```

  ```which pip3```

  ```pip3 --version```
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
