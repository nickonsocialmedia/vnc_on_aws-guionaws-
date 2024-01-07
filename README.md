# vnc_on_aws-guionaws-
This is how to use a gui interface on aws. there is lots to go over for further modifications but for not should hold true. this is a secure tunnel to vnc.

# I WILL FURTHER EDIT THIS IN THE FUTURE.

# Getting Started:

Set up an Ubuntu server on free tear, free-tier only allows for one cpu so not much but still enough for what were doing. make security keys i named mine AWSKEYS and made them .pem edit security groups and ass security group all utf source 0.0.0.0 and add all tcp source 0.0.0.0 26GB of Storage. go to your instance an take note of your ip address you'll need it.


open desktop terminal:

chmod 400 /YOUR/AWS/KEYS.pem

ssh sign in ass root: 

ssh -i /home/x1/AWSKEYS.pem ubuntu@ ip address (may or may not need sudo)

adduser: 
sudo adduser lucky

sudo usermod -aG sudo lucky

firewall settings for secure tunnel:
sudo ufw app list

Output
Available applications:
  OpenSSH


sudo ufw allow OpenSSH

sudo ufw enable

sudo ufw status


To                         Action      From
--                         ------      ----
OpenSSH                    ALLOW       Anywhere                  
OpenSSH (v6)               ALLOW       Anywhere (v6)


addkeytolucky:
sudo rsync --archive --chown=lucky:lucky ~/.ssh /home/lucky


!!!! this is really important !!!!

open another terminal window and ssh into lucky

sudo ssh -i /home/x1/AWSKEYS.pem lucky@youripaddress

sudo apt update

sudo apt install xfce4 xfce4-goodies

sudo apt install tightvncserver

vncserver

Output:
You will require a password to access your desktops.

Password:
Verify: ENTER PASSWORD only ( 8 char len )


Output:
Would you like to enter a view-only password (y/n)? n
xauth:  file /home/sammy/.Xauthority does not exist

New 'X' desktop is your_hostname:1

Creating default startup script /home/sammy/.vnc/xstartup
Starting applications specified in /home/sammy/.vnc/xstartup
Log file is /home/sammy/.vnc/your_hostname:1.log



if you want to change this password use: vncpasswd

next:
vncserver -kill :1

Output
Killing Xtightvnc process ID 17648



mv ~/.vnc/xstartup ~/.vnc/xstartup.bak

nano ~/.vnc/xstartup


add these lines:

#!/bin/bash
xrdb $HOME/.Xresources
startxfce4 &



chmod +x ~/.vnc/xstartup


verry import you run:

vncserver -localhost


Output:
New 'X' desktop is your_hostname:1

Starting applications specified in /home/sammy/.vnc/xstartup
Log file is /home/sammy/.vnc/your_hostname:1.log


exit server with exit


if you have a password use this might need to modify  :
sudo ssh -L 59000:localhost:5901 -C -N -l lucky server_ip 

if you have keypair use this: 
sudo ssh -i /home/x1/AWSKEYS.pem -L 59000:localhost:5901 -C -N -l lucky 18.224.31.126

( if you dont have realvnc or other vnc viewer available do that first )

! the tunnel after the second time you connect wont output anything !


if you had issues with the password!!

!!! last ditch efforts !!!

try editing:

sudo nano /etc/ssh/sshd_config

find:
#PasswordAuthentication no

change to:
PasswordAuthentication yes 

??? might help ????



🔥🔥🔥🔥🔥🔥🔥🔥🔥🔥🔥🔥🔥🔥🔥🔥🔥🔥🔥🔥🔥🔥🔥🔥🔥🔥🔥
install a vnc viewer i am using free trial sign up from real vnc
for ubuntu. sign up run through an install process.
🔥🔥🔥🔥🔥🔥🔥🔥🔥🔥🔥🔥🔥🔥🔥🔥🔥🔥🔥🔥🔥🔥🔥🔥🔥🔥🔥

have to sign in in the app. 

go to file > new connection:


set local host to :   localhost:59000

name it something ( what ever you want )

and your done have to sign in with the vnc password you made and if 
you for got it just use  vncpasswd like i showed earlier.

and you'll be logged in. 


( should do this before you establish a secure tunnel. ) 



🔥🔥🔥🔥🔥🔥🔥🔥🔥🔥🔥🔥🔥🔥🔥🔥🔥🔥🔥🔥🔥🔥🔥🔥🔥🔥🔥
now cool thing is i can install a web browser!!!!!

🔥🔥🔥🔥🔥🔥🔥🔥🔥🔥🔥🔥🔥🔥🔥🔥🔥🔥🔥🔥🔥🔥🔥🔥🔥🔥🔥

open terminal in xfce:

download chrome using this command: 

wget https://dl.google.com/linux/direct/google-chrome-stable_current_amd64.deb


execute the downloaded installer: 

sudo apt install ./google-chrome-stable_current_amd64.deb


launch the browser: 

google-chrome



!!!! works as is with tunnel no nonsense !!!!!!!


i havent tried this yet but apparently you can make a desktop icon:

https://superuser.com/questions/1503529/failed-to-execute-default-web-browser-input-output-error


*********************** quote **********************


Later, I decided to make the default browser icon to launch google chrome, so I followed Grant 
Curell's answer, basically:

    run xfce4-settings-manager
    find "Preferred Applications"
    under "Web Browser", click "Other..."
    type in /usr/bin/google-chrome


****************************************************





