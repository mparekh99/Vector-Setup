# Vector-Setup Guide (Windows)

## 1. WirePod Set Up
- Go here and download this: https://github.com/kercre123/WirePod/releases/tag/v1.2.13

![downloadpic](https://github.com/user-attachments/assets/59bebef5-eb0c-46d4-95c8-2f9085f5b81d)


Run the exectubale and say yes to everything and once installed you'll see this. Select the red highlighted box from pic below.

![Screenshot 2025-04-26 205620](https://github.com/user-attachments/assets/5170316f-62ac-4381-beb5-fc4862a0bfc8)


![Screenshot 2025-04-26 205739](https://github.com/user-attachments/assets/e69427b7-8936-4c75-a112-6f330931c9b8)

--No need to change anything just click submit. 

The place your Anki Vector on its charger and hold its power button (on the top back part of the robot) down for **15 seconds** to put it into recovery mode. 
To know it worked after the 15 seconds the light will show 1 white bar and when 2 blue bars as it powers back on. 

Wait for the robot to turn back on with a screen showing: Vector (Its name)
and under in bigger text anki.com/v.

After putting it into recovery mode go to this link:  https://wpsetup.keriganc.com/html/main.html.

(READ BEFORE GOING TO LINK so you don't make a mistake)

It should queue you do connect via bluetooth, connect to the wifi, then will start doing a cloud update. 

Wait for Vector to fully finish updating and it will turn off and turn back on again. 

Then double click on the power button while(vector is still on charger) which cause it change screens to Vector name and a key, then pull the Vector's lift up and then down changes to another screen showing serial number, OS, SSID, and IP, and a cursor next to exit with rest below. 

Then pick up the vector, move the treads on the wheels to move the cursor down to reset. Then lift the lift up and down to select reset. Once reset is selected it will queuue you with a screen sayying "CLEAR USER DATA?"

Wheere you'll repeat the same process and select CONFIRM. Cauing the vector to reboot. 

Once rebooted, follow the instructions in https://wpsetup.keriganc.com/html/main.html , which will just as you to connect the vector via bluetooth and authenticate. Once authenticated, select save settings and your vector will be set up with your wire pod once you get this: ![image](https://github.com/user-attachments/assets/644eb705-e8a2-40ac-839a-3757ea3fcd3a)

Go to your WirePod Web Interface and reload to confirm it has populated with your setup vector. 



This is a more detailed guide if you still have questions or are stuck:

[Wirepod Installation Guide](https://github.com/kercre123/wire-pod/wiki/Installation)

---

## 2. Environment Set Up

Use virtual Environment becuase using a Vm or WSL will signifantly increase runtime. 

1) Make Sure You Have Compatible Python Version: (Python 3.6.1 - 3.12):
   If you dont have python installed yet, download and install it from the Python.org. Make sure to tick the “Add Python 3.X to PATH” checkbox on the Setup screen.

To check python verion: python -V or py -V or python3 -V


Commands:
(Depending on which has the version of python you want between (python, py, python3)

python -m venv .venv

Creates your empty virtual environment

To activate it: 

..\venv\Scripts\activate


To ensure it's empty do pip freeze: to show there are no packages installed. 

Then run:

py -m pip install -U pip
py -m pip install --upgrade setuptools


If your using Python3.11 or above, create a file at \.venv\Lib\site-packages\pip\ and call it pip.conf:
Put this inside pip.conf:
[global]
break-system-packages = true



THen FOr the big pip installs:
pip install wirepod_vector_sdk
pip install "wirepod_vector_sdk[3dviewer]"


Run this to see if anki_vector is installed:
python -m anki_vector.configure









---

## 3. SDK Setup

Follow the step-by-step guide to configure your **Wirepod** setup using the **Python SDK**.

[Wirepod Python SDK Setup Guide](https://github.com/kercre123/wirepod-vector-python-sdk?tab=readme-ov-file)


## FAQ 

I keep getting this error message when configuring SDK: 
"Dowloading Vector certificate from wire-pod... ERROR
b'cert does not exist\n"


After connecting Vector to Wirepod via: (https://wpsetup.keriganc.com/html/main.html) and moving onto configuring your Vector with the Wirepod SDK with the command:
python -m anki_vector.configure and getting the output above.

** Make sure **NO other-wirepod instances** are running on the same network. If this is the case, locate the wirepod (Most likely in your C:\Users\NAME\AppData\Roaming\wire-pod\" folder if your using Windows) and navigate to the "certs" folder.

![image](https://github.com/user-attachments/assets/82c636b0-28ea-495a-a17d-7c15bdc53866)

Then open in a text editor "server_config.json" where you need to change {"jdocs":"escapepod.local:443","tms":"escapepod.local:443","chipper":"escapepod.local:443","check":"escapepod.local/ok","logfiles":"s3://anki-device-logs-prod/victor","appkey":"XX"} 
to something like: {"jdocs":"wirepod-NAME.local:443", "tms":"wirepod-mihir.local:443", "chipper":"wirepod-mihir.local:443", "check":"wirepod-mihir.local/ok", "logfiles":"s3://anki-device-logs-prod/victor", "appkey":"XX"}







