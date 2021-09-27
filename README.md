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

## BUILDING a CLOUD SERVER(GOOGLE CLOUD:
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

  ```ssh -i ~/.ssh/id_rsa amitesh@34.125.15.44```
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

  ## MQTT Broker Installation and Configuration):
  
  1.Installing MQTT broker on the cloud server

ssh to your cloud server and run the following command to install mosquitto mqtt broker

```sudo apt-get install mosquitto```

```sudo apt-get install mosquitto-clients```

```sudo pip3 install paho-mqtt```
Then start mosquitto service

```sudo systemctl start mosquitto```
```sudo systemctl enable mosquitto```

Test if mosquitto broker is working
run the following command to subscribe

```mosquitto_sub -h localhost -t test```

Then open another terminal to the cloud server and run the following command to publish
```mosquitto_pub -h localhost -t test -m "hello world"```

You should be seeing "hello world" displayed in the first terminal where you ran the
subscriber command
If so, mosquitto broker is ready to go

2.Allow port 1883 on the firewall of your cloud server so that packet to moquitto broker will be
allowed

Go to https://console.cloud.google.com/compute

Click on the menu (three lines at the top lest).
Then select VPC Network -> Firewall
Go to Networking -> VPC Network -> Firewall
Then click on 'Create Newfirewall rule' tab at the top
In the form that opens, give any name for this rule
For target, select 'Specified service account'
For source IP range, enter 0.0.0.0/0
For Protocol ports, Check 'Specified protocols and ports'
Then check 'tcp'. Then enter ports a 1883
Leave everything else as default
Then press 'Create'
That will allow incoming tcp ports 1883

3.Now setting user name and password for mosquitto mqtt broker

Run the following command on the server to set username and password for mosquitto.

```sudo mosquitto_passwd -c /etc/mosquitto/passwd <user name>```

```sudo mosquitto_passwd -c /etc/mosquitto/passwd amitesh```

This creates a file /etc/mosquitto/passwd

Now, create a file default.conf in /etc/mosquitto/conf.d

```cd /etc/mosquitto/conf.d```

```sudo vi default.conf```

Then add the following lines and save

allow_anonymous false

password_file /etc/mosquitto/passwd
Now, restart mosquitto

```sudo systemctl restart mosquitto```
  
*********************************************************************************************************************************************************************************  
### FILE PERMISSION:
  
Before you run the program check if the file has execute permissions by running
the following command, if your are using MacBook or any Linux machines.
  
```ls -l <file name>```
  
###For examples,
  
```ls -l mqtt_publish-1.py```
  
-rwxr-xr-x@ 1 viswa staff 545 2 Feb 16:51 mqtt_publish-1.py
  
The first few characters in that output shows permissions for user, group and others.
An x indicates execute permission. If execute permission does not exit for the user,
change permission using the following command before executing the programming
  
```chmod 755 <file name>```
  
For example:
  
```chmod 755 mqtt_publish-1.py```
  

*********************************************************************************************************************************************************************************

## Domain Name Registration:
  
We need a domain name
  
go to [https://godaddy.com](url) and register a domain

If it is just for this course, register a name
  
Once registered, go to manage DNS of your domain. There, you will see a
few rows of entry already.

In the row of A type record, press edit and change ;Parked' to the ip address of your cloud
server. In my case, the ip address of my cloud server was 34.125.15.44 So, I changeed 'parked' to
this ip address  
  
When everything is done, you will be able to ping your cloud server as
try the following command from your computer
  
```ping <your domain name>```
  
  Example:
  
```ping amiteshkr.xyz```
  
  *********************************************************************************************************************************************************************************
  
### Uploading Files on Cloud Server:

1.first goto file location in PowerShell

2.Sftp login to your virtual machine:
  
```sftp -i ~/.ssh/course_rsa amitesh@34.125.15.44```

3.Use command:

```put <file name> ```///to upload single file of that location
  
```put * ```///to upload all files of that location
  
  *********************************************************************************************************************************************************************************
