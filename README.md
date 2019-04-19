BACKGROUND
--------------------


CMS-DH is an old generic application created for resale, probably by
Dahua or one of it's divisions. It is used to control Digimerge security cameras.
Now Flir owns Digimerge and everybody wants to forget this software exists. 
In reality it doesn't matter and I don't really care. There are configuration 
entries to change the name of the application in toolbar menu's, so that should 
give you an idea of how generic it was meant to be.

If you lose access to CMS-DH it can be extremely difficult to connect to the DVR
and make changes to it. The documentation for Digimerge hardware is practically 
non-existent, and the company itself doesn't exist anymore (now absorbed into Flir 
Security, who don't even have a TLS cert on their security-centric website). The 
lack of information presents a problem that is compounded by the fact that there
seem to be different versions of documentation out there for the Digimerge equipment 
and not many of them seem to have accurate or useful information.

Luckily, the hardware uses CMS-DH to make configuration changes from a computer. 
CMS-DH is what I like to call "third world software" meaning that it was written 
without any consideration for security, nobody wants to own support for it, 
and it hangs all it's secrets out there in the open.

GAINING ACCESS
--------------------


This hack was tested to work with.....

App Version: 1.8.8.24

Service Version: 1.8.8.10

Codec Version: 3.0.2.3

Download Dll Version: 3.0.0.1


.....Although I'm not sure of a way to find this info until you log in at least once.

CMS-DH stores configuration data in C:\Users\USERNAME\Documents\CMS-DH. The  ".ems" 
files in this folder contain the configurationd data for CMS-DH and can be opened in 
Notepad or any other text editor.

In order for the hack to work, you must have a copy of CMS-DH installed and configured
with devices and an admin connection to a DVR. This hack will only give you access to
CMS-DH. If CMS-DH is connected to devices (using the device password) you will have access
those devices once you gain access to CMS-DH. If CMS-DH is not connected to any devices
this won't get you anywhere. This hack is only valuable on a pre-configured CMS-DH that
you do not have credentials for.

To gain access to CMS-DH without valid login credentials you must open "registry.ems"
with a text editor and locating the "PASSWORD=" line. 

The "PASSWORD=" line contains the user password in hashed form. If you look a little
further down you'll see another line that starts with "LOGINAC=" followed by a plain text
username. 

Start by backing up "Registry.ems" and then wipe out the hashed password string from the 
"PASSWORD=" line. So "PASSWORD=54883fsdf83nn2nb4" would become simply "PASSWORD=".
Save the file and launch CMS-DH. It will start the application and bypass the login 
screen. 

STEALING CREDENTIALS
--------------------


We know that an attacker can wipe out the cached password from CMS-DH and that it will completely skip
the login screen. An attacker can leverage this to gain access to DVR's we don't have authorization 
to by obtaining a copy of someone else's CMS-DH config directory. Because all the config data for 
devices are stored in the CMS-DH config directory, a successful attacker would have everything they 
need to log into gain unauthorized access to a local security system. 

Possible attack vectors for stealing the directory include.....

1. Phishing the user and convincing them to send you CMS-DH "log files."
2. Misconfigured Windows Share.
3. Boot to USB and copy/paste unencrypted HDD contents.
4. Make the user run a script which dumps the contents of the CMS-DH directory somewhere.
5. Gain access to the machine (physical or remote) and exfiltrate the files to a CNC server.
6. The files are small enough to exfiltrate through a DNS TXT query.
