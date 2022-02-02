#1. Crontab

Edit the crontab file

```sudo crontab -e```

Add to the end of file

@reboot python3 /home/pi/app.py  > /home/pi/app.log 2>&1


#2. Service

Open a sample unit file using the command as shown below:

sudo nano /lib/systemd/system/sample.service > /home/pi/service.log 2>&1
Add in the following text :

```
 [Unit]
 Description=My Sample Service
 After=multi-user.target

 [Service]
 Type=idle
 ExecStart=/usr/bin/python /home/pi/sample.py

 [Install]
 WantedBy=multi-user.target
```
You should save and exit the nano editor.

Configure systemd Run a Program On Your Raspberry Pi At Startup

This defines a new service called “Sample Service” and we are requesting that it is launched once the multi-user environment is available. The “ExecStart” parameter is used to specify the command we want to run. The “Type” is set to “idle” to ensure that the ExecStart command is run only when everything else has loaded. Note that the paths are absolute and define the complete location of Python as well as the location of our Python script.

In order to store the script’s text output in a log file you can change the ExecStart line to:

ExecStart=/usr/bin/python /home/pi/sample.py > /home/pi/sample.log 2>&1
The permission on the unit file needs to be set to 644 :

```sudo chmod 644 /lib/systemd/system/sample.service```
