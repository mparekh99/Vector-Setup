# Vector-Setup Guide (Windows)

## Table of Contents

1. [WirePod Setup](#1-wirepod-setup)  
   - Installation and initial setup of WirePod software.

2. [Environment & SDK Setup](#2-environment--sdk-setup)  
   - Installing Python, setting up a virtual environment, and SDK installation.


3. [FAQ](#faq)  
   - Common issues and troubleshooting steps.

SDK DOCS -->  (https://keriganc.com/sdkdocs/index.html)

---

## 1. WirePod Setup 

- Download the WirePod installer:  
  👉 [WirePod v1.2.13](https://github.com/kercre123/WirePod/releases/tag/v1.2.13)

![Download Screenshot](https://github.com/user-attachments/assets/59bebef5-eb0c-46d4-95c8-2f9085f5b81d)

- Run the executable. Accept all prompts during installation.
- Once installed, open WirePod and click the red-highlighted box as shown below:

![WirePod UI 1](https://github.com/user-attachments/assets/5170316f-62ac-4381-beb5-fc4862a0bfc8)  
![WirePod UI 2](https://github.com/user-attachments/assets/e69427b7-8936-4c75-a112-6f330931c9b8)

> No changes needed — just click **Submit**.

### Put Vector in Recovery Mode
1. Place Vector on its charger.
2. Hold the **rear power button** for **15 seconds**.
3. The light will show 1 white bar, then 2 blue bars as it reboots.
4. Wait until Vector displays its name and **anki.com/v** on screen.

### Begin Setup
Go to: [https://wpsetup.keriganc.com/html/main.html](https://wpsetup.keriganc.com/html/main.html)

Follow the steps:
- Connect via Bluetooth.
- Connect to Wi-Fi.
- Wait for the cloud update to complete (Vector will reboot).

### Factory Reset
1. While Vector is still on the charger, **double-tap the power button**.
2. Lift the arm **up and down** to view serial number and IP screen.
3. Pick up Vector and use the treads to move the cursor to **Reset**.
4. Lift arm **up and down** again to select **Reset**.
5. Confirm the **"CLEAR USER DATA?"** prompt using the same method.

### Finalize Setup
- After reboot, go back to [https://wpsetup.keriganc.com/html/main.html](https://wpsetup.keriganc.com/html/main.html).
- Reconnect via Bluetooth and **Authenticate**.
- Click **Save Settings**.

You should now see this confirmation:

![Confirmation Screenshot](https://github.com/user-attachments/assets/644eb705-e8a2-40ac-839a-3757ea3fcd3a)

Open your WirePod Web Interface and confirm your Vector appears there.

📘 More help: [WirePod Installation Guide](https://github.com/kercre123/wire-pod/wiki/Installation)

---

## 2. Environment & SDK Setup

> ⚠️ Avoid WSL or VMs — they significantly slow down runtime. Use a native Python virtual environment instead.

### Install Python (v3.6.1 – 3.12)
- Download from: [python.org](https://www.python.org/)
- During installation, check the box: **"Add Python to PATH"**

To verify version:
```bash
python -V
# or
py -V
# or
python3 -V
```

### Create and Activate Virtual Environment
```bash
python -m venv .venv
.\.venv\Scripts\activate
```
### Confirm it's empty:
```bash
pip freeze
```
### Update pip and setuptools:
```bash
py -m pip install -U pip
py -m pip install --upgrade setuptools
```
### If using Python 3.11+
Create a file:
```bash
.venv\Lib\site-packages\pip\pip.conf
```
Add the following:
```bash
[global]
break-system-packages = true
```
### Install SDK Packages
```bash
pip install wirepod_vector_sdk
pip install "wirepod_vector_sdk[3dviewer]"
```

### Verify anki_vector installed
```bash
python -c "import anki_vector as _; print(_.__path__)"
```

### Configure SDK 
```bash
python -m anki_vector.configure
```


## FAQ

### ❗ Issue: Vector SDK configuration fails with certificate error

You may encounter this message when running the SDK configuration command:

```bash
python -m anki_vector.configure
```

Resulting in:
```bash
Downloading Vector certificate from wire-pod... ERROR
b'cert does not exist\n'
```

### ✅ Cause:
This error typically happens when **multiple WirePod instances** are running on the same network, or your local WirePod hostname is **incorrectly configured**.

---

### 🔧 Solution:
If you see the error, follow these steps to resolve it:

1. **Uninstall WirePod**:  
   Make sure to check **yes** to all questions it asks during the uninstallation process.

2. **Reinstall WirePod**:  
   Download and reinstall it again.

3. **Open the Web Setup Link**:  
   Once downloaded, open the browser link. Click **Submit** as before, and navigate to the **Config Folder**.  
   ![Config Folder Screenshot](https://github.com/user-attachments/assets/9965b009-fc46-43e2-8c0c-92ac9a5ea60d)  
   *(Follow Fixing WirePod Instructions)*

4. **Repeat WirePod Setup & Run Configure Command Again**.


### Fixing Wirepod Instructions

#### 1. Locate your WirePod certs directory:
```bash
C:\Users\YOUR_NAME\AppData\Roaming\wire-pod\certs\
```


### 2. Open `server_config.json` in a text editor

You'll likely see something like this:

```json
{
  "jdocs": "escapepod.local:443",
  "tms": "escapepod.local:443",
  "chipper": "escapepod.local:443",
  "check": "escapepod.local/ok",
  "logfiles": "s3://anki-device-logs-prod/victor",
  "appkey": "XX"
}
```
### 3. Change `escapepod.local` to match your actual WirePod hostname

For example, if your hostname is `wirepod-user.local`, update the config to:

```json
{
  "jdocs": "wirepod-user.local:443",
  "tms": "wirepod-user.local:443",
  "chipper": "wirepod-user.local:443",
  "check": "wirepod-user.local/ok",
  "logfiles": "s3://anki-device-logs-prod/victor",
  "appkey": "XX"
}
```









