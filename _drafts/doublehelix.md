---
title: "Jailbreak iOS 10.3.3 with doubleH3lix"
categories: 
  - mobile
tags:
  - ios
  - jailbreak
  - mobile pentest
---

# Introduction
This document describes how to jailbreak iOS 10.3.3 with doubleH3lix 

doubleH3lix is a jailbreak for 64-bit 10.x devices. It is composed of an ipa which you install on a target device and run the app.

## Environment
* macOS Catalina version 10.15.1

## Prerequisites
* Download Cydia Impactor from [here](https://yalujailbreak.net/download-cydia-impactor/). Install by double-clicking on the downloaded dmg file.

![Impactor version](/assets/images/impactor-version.PNG)

* Download the doubleH3lix ipa [here](https://doubleh3lix.tihmstar.net)

* Create an app-specific password to be used with Impactor.
  * Go to Apple ID [signin page](https://appleid.apple.com/#!&page=signin)
You will be asked to enter your Apple ID, password, and one-time password.i

  ![login](/assets/images/appleid-login.PNG) 

  * On successful login, scroll to the Security section and click on "Generate password...". Follow the prompt to generate an app-specific password. The password can be reused for future resigning hence keep it somewhere safe.

  ![app-specific pw](/assets/images/app-specific-pw.PNG)

## Installation
* Attach your target device to your machine
* Launch Cydia Impactor. Your device will show up in the top field of Impactor.
  ![Impactor](/assets/images/impactor-phone.PNG)
* Drag the doubleH3lix ipa to the Impactor dialog. It will start the resigning process. You will be prompted for your Apple ID.

  ![Impactor](/assets/images/impactor-appleid.PNG)

  You will then be prompted for a password. Enter the app-specific password.

  ![Impactor](/assets/images/impactor-pw.PNG)

  Signing proceeds and doubleH3lix will be installed on your device.

  ![doubleH3lix](/assets/images/doublehelix-phone.png)

### Troubleshooting
1. Signing fails and the dialog below pops-up. This is an issue with using temporary app IDs which according to someone in [Reddit](https://www.reddit.com/r/jailbreak/comments/dslnaw/help_help_with_cydia_impactor/) requires Impactor to be updated. There is no fix as of the time this article is written. The solution is to use an Apple ID with a paid developer account.

    ![trouble 1](/assets/images/impactor-error-provision.PNG)

2. An error dialog may pop-up as shown below. You can ignore this error as this does not prevent installation.

    ![trouble 2](/assets/images/impactor-error-plist.PNG)

## Jailbreak
1. Make sure your device is connected to the internet
2. Go to Settings > General > Profile & Device Management. Tap the Apple ID and trust  
3. Launch doubleH3lix
4. Tap Kickstart
    ![launch](/assets/images/doublehelix-launch.PNG)
5. The device will be jailbroken after it reboots. Repeat steps 3 and 4 if you shutdown or reboot your device.

