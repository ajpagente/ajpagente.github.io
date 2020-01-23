---
title: "Jailbreak iOS 10.x with doubleH3lix"
categories: 
  - mobile
tags:
  - ios
  - jailbreak
  - mobile pentest
---

# Introduction
This document describes how to jailbreak iOS 10.x with doubleH3lix 

doubleH3lix is a jailbreak for 64-bit 10.x devices with A7-A9 processors (devices with headphone jacks). It is composed of an ipa which you install on a target device and run the app to jailbreak.

## Environment
* macOS Catalina version 10.15.1

## Prerequisites
* Download Cydia Impactor from [here](https://yalujailbreak.net/download-cydia-impactor/). Install by double-clicking on the downloaded dmg file.

![Impactor version](/assets/images/impactor-version.png)

* Download the doubleH3lix ipa [here](https://doubleh3lix.tihmstar.net)

* Create an app-specific password to be used with Impactor.
  * Go to Apple ID [signin page](https://appleid.apple.com/#!&page=signin)
You will be asked to enter your Apple ID, password, and one-time password.i

  ![login](/assets/images/appleid-login.png) 

  * On successful login, scroll to the Security section and click on "Generate password...". Follow the prompt to generate an app-specific password. The password can be reused for future resigning hence keep it somewhere safe.

  ![app-specific pw](/assets/images/app-specific-pw.png)

## Installation
* Attach your target device to your machine
* Launch Cydia Impactor. Your device will show up in the top field of Impactor.
  ![Impactor](/assets/images/impactor-phone.png)
* Drag the doubleH3lix ipa to the Impactor dialog. The signing process starts and you will be prompted for your Apple ID.

  ![Impactor](/assets/images/impactor-appleid.png)

  Next, you will then be prompted for a password. Enter the app-specific password.

  ![Impactor](/assets/images/impactor-pw.png)

  Signing proceeds and doubleH3lix will be installed on your device.

  ![doubleH3lix](/assets/images/doublehelix-phone.png)

### Troubleshooting
1. Signing fails and the dialog below pops-up. This is an issue when using an Apple ID which is not registered to an Apple Developer account. According to a post on [Reddit](https://www.reddit.com/r/jailbreak/comments/dslnaw/help_help_with_cydia_impactor/) this requires Impactor to be updated. There is no fix as of the time this article is written. The solution is to use an Apple ID registered with a paid Apple Developer account.

    ![trouble 1](/assets/images/impactor-error-provision.png)

2. An error dialog may pop-up as shown below. You can ignore this error as this does not prevent installation.

    ![trouble 2](/assets/images/impactor-error-plist.png)

## Jailbreak
Perform the following steps after successfully installing doubleH3lix.
 
1. Make sure your device is connected to the internet
2. Go to **Settings > General > Profile & Device Management**. Locate the certificate for the doubleH3lix app and tap the Trust option.  
3. Launch doubleH3lix
4. Tap Kickstart
    ![launch](/assets/images/doublehelix-launch.png)
5. The device will be jailbroken after it reboots. Repeat steps 3 and 4 if you shutdown or reboot your device.

