# playdeck

<!-- TOC -->

- [playdeck](#playdeck)
- [Introduction](#introduction)
  - [Purpose](#purpose)
  - [Audience](#audience)
- [System Overview](#system-overview)
  - [Benefits and Values](#benefits-and-values)
- [User Personas](#user-personas)
  - [RACI Matrix](#raci-matrix)
- [Requirements](#requirements)
  - [Mac](#mac)
- [Installation and Configuration](#installation-and-configuration)
  - [Setting up the Stream Deck for the first time](#setting-up-the-stream-deck-for-the-first-time)
- [Deployment](#deployment)
  - [Deploy a script to Automator](#deploy-a-script-to-automator)
- [Troubleshooting and FAQs](#troubleshooting-and-faqs)
  - [Creating a symbolic link /usr/local/bin/python](#creating-a-symbolic-link-usrlocalbinpython)

<!-- /TOC -->

---
# 1. Introduction
## 1.1. Purpose

This document describes the Stream Deck automation and manual services that is provided for DevSecOps, Developers and Mac Users.

## 1.2. Audience

The audience for this document includes:

* Mac User who will install and configure Stream Deck on their workstation, and to automate day-to-day tasks with a key press.

* Developer who will implement, build, test all automation scripts.

* DevSecOps who will deploy each script to Automator, and to publish the Automator application for the Users.

---
# 2. System Overview
## 2.1. Benefits and Values

---
# 3. User Personas
## 3.1 RACI Matrix

|            Category            |                     Activity                     | Mac User | Developer | DevSecOps |
|:------------------------------:|:------------------------------------------------:|:--------:|:---------:|:---------:|
| Installation and Configuration |  Setting up the Stream Deck for the first time   |   R,A    |           |           |
| Installation and Configuration |       Set up an application on Stream Deck       |   R,A    |           |           |
|           Deployment           |           Deploy a script to Automator           |    I     |     C     |    R,A    |
|    Troubleshooting and FAQs    | Creating a symbolic link `/usr/local/bin/python` |    I     |     C     |    R,A    |


---
# 4. Requirements
## 4.1 Mac

* `python`
* **Automator**

---
# 5. Installation and Configuration
## 5.1. Setting up the Stream Deck for the first time

This runbook should be performed by the User.

1. Open your web browser and navigate to `https://www.elgato.com/us/en/s/downloads` > click **Download** to download the Stream Deck installer.

2. Run the Stream Deck installer and follow the on-screen instructions.

## 5.2. Set up an application on Stream Deck

This runbook should be performed by the User.

1. Open **Stream Deck** on your workstation > click **Configure Stream Deck**.

2. In the right-hand panel > Find the plugin **System** > Drag and drop the **Open** command to an available slot.

3. Configure the command as follows:
  - For **Title**, enter your application title.
  - For **App/File**, click on the File icon > Choose your application, e.g. `~/playdeck/automation/QuickDaily.app`.
  - For **Icon**, click on the drop-down arrow > Select **Set from File** > Choose your icon, e.g. `~/playdeck/img/chrome.png`.

---
# 6. Deployment
## 6.1. Deploy a script to Automator

This runbook should be performed by the DevSecOps.

1. Open **Automator** on your workstation > Choose **Application** as the type of document.

2. Under Actions > drag and drop the **Run Shell Script** into the blank canvas.

3. In the Run Shell Script dialog window:
  - For **Shell**, choose your shell interpreter, e.g. `/usr/local/bin/python`.
  - Copy and paste your script into the text box.

Example script:

```py
import subprocess

if __name__ == "__main__":
  chrome = ['/usr/bin/open','-b','com.google.Chrome']
  urls = [
    'https://github.com',
    'https://netflix.com'
  ]

  lstCmd = []
  for c in chrome:
    lstCmd.append(c)
  for u in urls:
    lstCmd.append(u)
  print(" ".join(map(str,lstCmd)))
  subprocess.Popen(lstCmd)
```

4. Name your application, e.g. `QuickDaily`

5. Click File > **Save**.

6. Click **Run** to test the script.

7. Click File > **Move To**, and select the folder to save your Automator application, e.g. `~/playdeck/automator`.

---
# 7. Troubleshooting and FAQs
## 7.1. Creating a symbolic link `/usr/local/bin/python`

This runbook should be performed by the DevSecOps.

The Run Shell Script within the Automator software cannot be configured to use a custom shell path. We use a workaround by creating a symbolic link that points to any pre-defined shell path, e.g. `/usr/local/bin/python`.

1. Open a shell terminal, and type the following command:

```sh
sudo ln -s /opt/homebrew/bin/python3 /usr/local/bin/python
```

2. The target link `/usr/local/bin/python` should now exists, and points to our custom shell path `/opt/homebrew/bin/python3`.