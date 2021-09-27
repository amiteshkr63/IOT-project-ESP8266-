# OBJECTIVE:
## Develop a complete IOT system we can activate parts of an IOT device from remote browsers as well as voice prompt through Google Home on your smartphone.

#### This projects of following Sections:

- BUILDING a CLOUD SERVER(GOOGLE CLOUD): https://github.com/amiteshkr63/IOT-project-ESP8266-#building-a-cloud-servergoogle-cloud

- MQTT Broker Installation and Configuration: https://github.com/amiteshkr63/IOT-project-ESP8266-/blob/main/README.md#mqtt-broker-installation-and-configuration
 
- FILE PERMISSION: https://github.com/amiteshkr63/IOT-project-ESP8266-/blob/main/README.md#file-permission
 
- Uploading Files on Cloud Server: https://github.com/amiteshkr63/IOT-project-ESP8266-/blob/main/README.md#uploading-files-on-cloud-server
 
- Domain Name Registration: https://github.com/amiteshkr63/IOT-project-ESP8266-/blob/main/README.md#domain-name-registration
 
- Django web server - Installation: https://github.com/amiteshkr63/IOT-project-ESP8266-/blob/main/README.md#django-web-server---installation
 
- Configure apache2 to server Django: https://github.com/amiteshkr63/IOT-project-ESP8266-/blob/main/README.md#configure-apache2-to-server-django
 
- SSL certificates Installation: https://github.com/amiteshkr63/IOT-project-ESP8266-/blob/main/README.md#ssl-certificates-installation

- Configuring MQTT broker with SSL encryption:
[https://github.com/amiteshkr63/IOT-project-ESP8266-/blob/main/README.md#configuring-mqtt-broker-with-ssl-encryption](url)

- Modify firmware of the device to use ssl certificate:
*********************************************************************************************************************************************************************************
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
*********************************************************************************************************************************************************************************
### Hardware needed:
##### 1)ESP8266/NodeMCU
##### 2)Relay module
##### 3)Temperature sensor
##### 4)Motion Sensor
##### 5)Buzzer
##### 6)RGB Led
##### 7)Solid state Relay
*********************************************************************************************************************************************************************************
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

## In ARDUINO IDE, Make these following changes:
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

*********************************************************************************************************************************************************************************
Why Cloud Server needed?
-Because all IOT devices are connected via CLOUD to INTERNET.
-Also communicates with all human interfaces such as Human Interfaces and browsers on 
CLIENT computers and so on.

*********************************************************************************************************************************************************************************
Building CLOUD SERVER:
Needs:
-Static IP address with Configurable Firewaall
-e.g-Amazon web service,Google cloud,Digital ocean, Microsoft Azure
(mostly free for 1 year..i.e in this google cloud is for 90 days)
-If you want to login from other system apart from your comuter system, Add the PUBLIC KEY for
that particular system into METADATA of Cloud server

*********************************************************************************************************************************************************************************

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

## MQTT Broker Installation and Configuration:

*********************************************************************************************************************************************************************************

MQTT(Message Queuing Telemetry Transport)
(Specicially Developed For IOT Devices)
-Lightweight Messaging Protocol for in cases where clients need small code footprint
-Uses TLS(Transport layer Security) encryption with user name, password and password protected 
connections
-Optional certifications requires clients to provide a certificate file that matches with the server
-Clients unawre of each other IP address
-Uses Publsh/subscribe model to communicate
-MQTT broker is Center of Communication.
-Each client can Publish and/or Subscribe a message with a topic with the broker. The Broker passes
the message to all clients who subscribed to that topic.
-PORT-1883 is the secure listener port for the broker.

*********************************************************************************************************************************************************************************

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

### Uploading Files on Cloud Server:

1.first goto file location in PowerShell

2.Sftp login to your virtual machine:
  
```sftp -i ~/.ssh/course_rsa amitesh@34.125.15.44```

3.Use command:

```put <file name> ```///to upload single file of that location
  
```put * ```///to upload all files of that location
  
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

## Django web server - Installation:

  1)install apache2 and mod-wsgi
Open a terminal to your cloud server and run the following command

```sudo apt-get install apache2 apache2-utils ssl-cert libapache2-mod-wsgi-py3```

2) Create virtual environment:

Run the following commands to install virtual environmemt

```pip3 install virtualenv```

```pip3 install virtualenvwrapper```

then edit the file ~/.bashrc and add the following:

```
export WORKON_HOME=~/.virtualenvs
export MY_PROJECT=~/my_proj
export VIRTUALENVWRAPPER_WORKON_CD=1
export VIRTUALENVWRAPPER_PYTHON=/usr/bin/python3
export VIRTUALENVWRAPPER_VIRTUALENV=/home/amitesh/.local/bin/virtualenv
source /home/amitesh/.local/bin/virtualenvwrapper.sh
```

Then, run the following command:

```source ~/.bashrc```

Then create a virtual environment by running the following command.
Here, django is the name of the virtual environment

```mkvirtualenv django```

then activate the virtual environment by running the following command

```workon django```

We are in virtual environment now

install paho-mqtt in the django virtual environment by running the following command

```pip install paho-mqtt```


install django by running the following command

```pip install django```

Create a django project by running the following command

django-admin.py startproject my_proj

edit the file settings.py

```cd ~/my_proj/my_proj```

```vi settings.py```

import os

And, modify the ALLOWED_HOSTS line as shown below:
Note: iotcourse.xyz is my domain name. You may replace it with your domain name
35.223.145.82 is my server's ip address. You may replace it with your server's ip address

```
ALLOWED_HOSTS = ["127.0.0.1", "34.125.15.44", 'amiteshkr.xyz', 'http://amiteshkr.xyz',
'https://amiteshkr.xyz', 'www.amiteshkr.xyz', 'https://amiteshkr.xyz', 'https://www.amiteshkr.xyz',]
```

And, add the following just after STATIC_URL at the bottom

STATIC_ROOT = os.path.join(BASE_DIR, 'static/')

Then save the settings.py

now, migrate by running the following commands

```cd ~/my_proj```

```python manage.py makemigrations```

```python manage.py migrate```

Create superuser by running the following command

```python manage.py createsuperuser```

collect static files by running the following command

```python manage.py collectstatic```

run the following command and see if you see any errors

```python manage.py runserver 0:8000```

If everything is correct, this will not show any errors.

  *********************************************************************************************************************************************************************************

## Configure apache2 to server Django:
  
 #### Configure apache2 to run on port 80
  
 edit the file /etc/apache2/sites-available

```cd /etc/apache2/sites-available```

```sudo vi 000-default.conf```

And, add the following lines just before the last line <VirtualHost>

PS. After copying, Make sure to replace /home/raman with your home directory

also, while copying from this file, make sure to keep the format. Also make sure that
there are no extra unwanted characters.
That can happen if you are copying from thios pdf file.

```
WSGIDaemonProcess my_proj python-path=/home/raman/my_proj:/home/amitesh/.virtualenvs/django/lib/python3.7/site-packages
WSGIProcessGroup my_proj
WSGIScriptAlias / /home/amitesh/my_proj/my_proj/wsgi.py
```

Then, within the <VitualHost>, add the following lines

```
Alias /static /home/amitesh/my_proj/static
<Directory /home/amitesh/my_proj/static>
Require all granted
</Directory>
<Directory /home/amitesh/my_proj/my_proj>
<Files wsgi.py>
Require all granted
</Files>
</Directory>
```

Note: I have attached a file 000-default.conf in the resources of this lesson.

When you modify this file, make sure that what you get is similar to what I have attached,
except the home directory. The attached files have my home directory. You may have to
replace them with yours when you are comparing or copying
Now, change file permissions of a few files so that apache can use them.
Run the following commands

```cd ~```

```chmod 664 ~/my_proj/db.sqlite3```

```chmod 775 ~/my_proj```

```sudo chown :www-data ~/my_proj/db.sqlite3```

```sudo chown :www-data ~/my_proj```

Now, check if config is correct by running the following command

```sudo apache2ctl configtest```

It should say:

Syntax OK

Now, start apache2 by running the following command

```sudo systemctl start apache2```

Now start a django app by running the following command

workon django```

```cd ~/my_proj```

```python manage.py startapp myapp```

edit the file settings.py and add the following lines within the INSTALLED_APPS

```
'myapp.apps.MyappConfig',
```

edit the file my_proj/my_proj/urls.py and add the following:

```
from django.contrib import admin
from django.urls import path, include
from myapp import views
urlpatterns = [
path('admin/', admin.site.urls),
path('myapp/', include('myapp.urls')),
path('', views.index, name='index'),
]
```

Now, cd to ~/my_proj/myapp and create a file views.py
Add the following lines in views.py.

```from django.shortcuts import render```

```from django.http import HttpResponse```

Create your views here.

```
def index(request):
message = “Hello ! Welcome to this course”
context = {
'message': message,
}
return render(request, 'myapp/display_a_message.html', context)
```

Next, edit or create a file urls.py 

```
from django.urls import path
from . import views
app_name = 'myapp'
urlpatterns = [
path('', views.index, name='index'),
path('index/', views.index, name='index'),
]
```

then in this myapp folder, create a directory by running the following commands

```cd ~/my_proj/myapp```

```mkdir templates```

```cd templates```

```mkdir myapp```

```cd myapp```

To this folder, copy the following files:

```
base_form.html
display_a_message.html
```

Note: If done correctly, the above two files are in location:

```~/my_proj/myapp/templates/myapp/```

Then restart apache2 by running the following command

```sudo systemctl restart apache2```

Then on a browser of your computer enter the domain name of your cloud server in the
address bar and press enter.
Example:
```http://amiteshkr.xyz```

If you have completed all the steps correctly, You should be seeing a page with title: My
Course
  
*********************************************************************************************************************************************************************************
  
  
## SSL certificates Installation:

We need to make https access instead of http. This is required for security.

Google Home actions also need https access and not http.

Installing letsencrypt certificate. On a terminal of the cloud server, run the following
command:

```sudo apt install python3-certbot-apache```

Edit the file /etc/apache2/sites-enabled/000-default.conf

```sudo vi /etc/apache2/sites-enabled/000-default.conf```


This file is a copy from my server and, therefore, it has my home directory.
To use this file or to compare it with yours, you need to replace my home directory with
yours.
After modifying and saving the above file, test the configuration by running the following
command

```sudo apachectl configtest```

It should say syntax ok

Then restart apache2 by running the following command

```sudo systemctl restart apache2```

Now, install letsencrypt certificate by running the following command

```sudo certbot --apache```




When all options are selected, it will complete installation of the certificate with a long
message starting with 'Congratulations ...'
If you get any errors, it may be because of any errors in configuration. Fix it and reinstall the
certificate.
The certificates and private and public keys are sored at the following location:

```
/etc/letsencrypt/live/<domain name>/cert.pem
/etc/letsencrypt/live/<domain name>/chain.pem
/etc/letsencrypt/live/<domain name>/privkey.pem
```

Now, restart apache2 by running the following command

```sudo systemctl restart apache2```

Open a browser and enter the urls https://<your domain name>

Check if it displays your page as before

Setting autorenewal of certificate

Now, for regular renewal of the certificate, run the following commands:

```
sudo systemctl start certbot.timer
sudo systemctl enable certbot.timer
sudo systemctl status certbot.timer
```

Now, edit settings.py of the django (in the directory my_proj/my_proj)

```cd /my_proj/my_proj```

```vi settings.py```

Add the following lines at the end

```
secure proxy SSL header and secure cookies
SECURE_PROXY_SSL_HEADER = ('HTTP_X_FORWARDED_PROTO', 'https')
SESSION_COOKIE_SECURE = True
CSRF_COOKIE_SECURE = True
session expire at browser close
SESSION_EXPIRE_AT_BROWSER_CLOSE = False
wsgi scheme
os.environ['wsgi.url_scheme'] = 'https'
```

Now, edit the file wsgi.py in the same directory and add the following lines at the end

```os.environ['HTTPS'] = "on"```

Then, restart apache2 by running the following command

```sudo systemctl restart apache2```

Now, on a browser enter the url as follows:

```https://<your domain name>```

That should work
You will also notice that even if you enter http://<your domain name>, it re-directs to

```https://<your domain name>```

If all steps are successful, you have installed SSL certificate on your cloud server.

 *********************************************************************************************************************************************************************************
 
 ## Configuring MQTT broker with SSL encryption:

edit the file /etc/mosquitto/conf.d/default.conf and add the following:
This will make sure that it uses letsencrypt certificate and uses encryption on connections on
```port 8883```

```
listener 1883 localhost
listener 8883
certfile /etc/letsencrypt/live/amiteshkr.xyz/cert.pem
cafile /etc/letsencrypt/live/amiteshkr.xyz/chain.pem
keyfile /etc/letsencrypt/live/amiteshkr.xyz/privkey.pem
```

since mosquito is using ```8883``` port for external communications, we need to change
the firewall rules of the cloude server

```Allow port 8883 on firewall```, And, ```remove port 1883 from allowed ports```

To do that...

Go to https://console.cloud.google.com/compute

Click on the menu (three lines at the top lest).

Then select ```VPC Network -> Firewall```

Go to ```Networking -> VPC Network -> Firewall```

Then click on the name of the firewall where you have allowed port 1883

Then click on Edit tab

Then scroll down where you will see 1883 under Protocols and ports.

There, change ```1883``` to ```8883```

Then press ```Save```

The firewall will now allow ```tcp port 8883``` to cloud server

Then restart mosquitto by running the following command

```sudo systemctl restart mosquitto```

## Modify firmware of the device to use ssl certificate:
 
Change the line ```WiFiClient wifiClient``` to ```WiFiClientSecure wifiClient```
Then, open a terminal to the cloud server and print out the cert.pem

```sudo cat /etc/letsencrypt/live/amiteshkr.xyz/cert.pem```

Copy that text to the arduino sketch as (example):

Here it is for my server:
```
const char caCert[] PROGMEM = R"EOF(
< Paste that cerificate text here including
-----BEGIN CERTIFICATE-----
<text from cert.pem>
-----END CERTIFICATE-----
)EOF";
```

Next, you need to find the ```fingerprint(SHA-1)``` of this certificate. This is needed in firmware.


```
const uint8_t mqttCertFingerprint[] =
{YOUR SHA-1 fingerprint};```

Then, copy this to arduino sketch. Paste this just after the previous pasted line
in the arduino sketch.

Then, add the following line next to it

```X509List caCertX509(caCert);```

Then, in the next to next line, ```change the mqtt broker's port to 8883```

Then, within the in the setup() function of the sketch, add the following lines
 after WiFi is connected:
 ```
wifiClient.setTrustAnchors(&caCertX509);
wifiClient.setFingerprint(mqttCertFingerprint);
```
Then compile and load the sketch.
 It should compile and load without errors.

Open the serial monitor of the arduino sketch. If successful, you should be seeing a message
Connected Successfully to MQTT Broker !
 
