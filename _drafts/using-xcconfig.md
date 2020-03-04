---
title: Configure XCode project signing with xcconfig
categories: 
  - mobile
tags:
  - ios
  - development
---

### Version
:information-source: The projects are built with XCode 11.3 on MacOS Mojave

XCode build configuration files, known as _xcconfig_, is a plaintext file that defines or overrides the configuration of a project or target. Xcconfig enables scripts to update an XCode project's configuration and makes it easier to share configurations across projects.
  
This article describes configuring an XCode project's code signing settings with xcconfig. We also cover how to build a project with xcconfig from the command line.

## Code Signing Parameters 
XCode code signing requires the following build settings:
* Team Identifier
* Provisioning profile UUID
* Development certificate SHA-1 hash

For provisioning profile and development certificate, you may use their names. However if there are multiple profiles and certificates on your machine, it is easy to get confused on which one to use. I would recommend that you use UUID and hash for provisioning profile and certificate respectively.

### Finding the values for the code signing parameters
To install and run an application on a device during development, you will need a development provisioning profile. It is assumed that you have the provisioning profile installed on your development machine. The provisioning profiles are kept in the path shown:

```
~/Library/MobileDevice/Provisioning\ Profiles
```

If you have multiple provisioning profiles, you need to look at each one to find the right development profile. You can use a text editor to view each file or an easier way is to use the __Quick Look__ from Finder's context menu. Right-click on the mobileprovision file and choose Quick Look. Take note of the highlighted values.

![Signing parameters](/assets/images/xcconfig/find-signing-parameters.png) 

## Setting up XCode project for xcconfig use

To use xcconfig for signing, you must perform four main tasks:
1. Disable automatic signing.
2. Create your xcconfig files.
3. Set your build configuration to use the xcconfig.
4. Update your signing settings to use the build settings from the xcconfig.

The XCode project __XCConfig Signing__ illustrates the steps to setup an XCode project with xcconfig.

### Disable automatic signing
Open your XCode project, highlight __XCConfig Signing__ in the Project navigator, then select the __XCConfig Signing__ target. Select __Signing & Capabilities__, then uncheck the __Automatically manage signing__ checkbox. 

![Disable autosigning](/assets/images/xcconfig/disable-autosigning.png) 

### Create xcconfig files

A personal preference is to create a folder to organize the xcconfig files. Highlight __XCConfig Signing__ in the Project navigator, right-click then choose __New Group__. Name the group __BuildConfiguration__.

With BuildConfiguration highlighted, create a __New File__, choose __Configuration Settings File__ from the template dialog window. Name the file __Sign-Debug__. This build configuration will hold the signing parameters for the Debug scheme.

Create another file named __Debug.xcconfig__ to hold the Debug scheme configuration.

You may do all of this on a single build configuration file, however separating gives you the option of not checking in Sign-Debug.xcconfig to your source code repository. It is good practice particularly if you upload the project to a public Github repository.

Next, edit __Sign-Debug.xcconfig__ with the following XCode Build Settings:
* __DEVELOPMENT_TEAM__: The team identifier.
* __CODE_SIGN_IDENTITY__: The development certificate SHA-1 hash.
* __PROVISIONING_PROFILE_IDENTIFIER__: The provisioning profile UUID.

You can refer to Apples' [Build settings reference](https://help.apple.com/xcode/mac/11.4/#/itcaec37c2a6) for details on each setting.

![Sign Debug](/assets/images/xcconfig/sign-debug.png) 

Finally, edit __Debug.xcconfig__ to include the signing configuration. This xcconfig feature allows configuration reuse. In actual projects, Debug.xcconfig can be used for other Debug scheme build settings.

![Debug](/assets/images/xcconfig/debug.png)

You are now ready to set your build configuration.

## Set XCode Configurations
By setting the Configurations to an xcconfig, XCode applies the build settings to the project.
The way to set the configuration is the same for Debug and Release so only Debug will be shown here.

Highlight __XCConfig Signing__ in the Project navigator, then select the __XCConfig Signing__ project. Under __Configurations__, expand __Debug__ and from the __XConfig Signing__ target choose __Debug__.

![Set Debug](/assets/images/xcconfig/set-debug.png)

The Debug configuration is set as shown.

![Debug Set](/assets/images/xcconfig/debug-config-set.png)

With the configuration set to use the build settings from the xcconfig, you can now update the signing settings.

## Update Signing Settings


