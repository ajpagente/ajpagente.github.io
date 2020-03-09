---
title: Configure XCode Project Signing with xcconfig
categories: 
  - mobile
tags:
  - ios
  - development
---

__Version:__ The project is built with XCode 11.3 on MacOS Mojave

XCode build configuration files, known as _xcconfig_, is a plaintext file that defines or overrides the configuration of a project or target. Xcconfig enables scripts to update an XCode project's configuration and makes it easier to share configurations across projects.
  
This article describes configuring an XCode project's code signing settings with xcconfig.

## Code Signing Parameters 
XCode code signing requires the following build settings:
* Team Identifier
* Provisioning profile UUID
* Development certificate SHA-1 hash

If you only have one copy of a provisioning profile and development certificate on your development machine, you may use the profile and certificate name. However if there are multiple profiles and certificates, it is easy to get confused on which one to use. To mimimize mistakes and to be explicit, it is better to use UUID and hash for provisioning profile and certificate respectively.

### Finding the Code Signing Parameter Values 
To install and run an application on a device during development, you will need a development provisioning profile. It is assumed that you have the provisioning profile installed on your development machine. The provisioning profiles are kept in the path shown:

```
~/Library/MobileDevice/Provisioning\ Profiles
```

If you have multiple provisioning profiles, you need to look at each one to find the right development profile. You can use a text editor to view each file or an easier way is to use the __Quick Look__ from Finder's context menu. Right-click on the mobileprovision file and choose __Quick Look__. Take note of the highlighted values.

![Signing parameters](/assets/images/xcconfig/find-signing-parameters.png) 

## Setup an XCode Project to Use xcconfig

To use xcconfig for signing, you must perform four main tasks:
1. Disable automatic signing.
2. Create your xcconfig files.
3. Set your build configuration to use the xcconfig.
4. Update your signing settings to use the build settings from the xcconfig.

We use the XCode project named __XCConfig Signing__ to show the setup steps.

### Disable Automatic Signing
Open your XCode project, highlight __XCConfig Signing__ in the Project navigator, then select the __XCConfig Signing__ target. Choose the __Signing & Capabilities__ tab, then uncheck the __Automatically manage signing__ checkbox. 

![Disable autosigning](/assets/images/xcconfig/disable-autosigning.png) 

### Create xcconfig Files

A personal preference is to create a folder to organize the xcconfig files. Highlight __XCConfig Signing__ in the Project navigator, right-click then choose __New Group__. Name the group __BuildConfiguration__.

With __BuildConfiguration__ highlighted, create a __New File__, choose __Configuration Settings File__ from the template dialog window. Name the file __Sign-Debug__. This build configuration will hold the signing parameters for the Debug scheme.

Create another file named __Debug.xcconfig__ to hold the Debug scheme configuration.

You may do all of this on a single build configuration file, however separating gives you the option of not checking in Sign-Debug.xcconfig to your source code repository. It is good practice particularly if you upload the project to a public Github repository.

Next, edit __Sign-Debug.xcconfig__ with the following XCode Build Settings:
* __DEVELOPMENT_TEAM__: The team identifier.
* __CODE_SIGN_IDENTITY__: The development certificate SHA-1 hash.
* __PROVISIONING_PROFILE_SPECIFIER__: The provisioning profile UUID.

You can refer to Apples' [Build settings reference](https://help.apple.com/xcode/mac/11.4/#/itcaec37c2a6) for details on each setting.

![Sign Debug](/assets/images/xcconfig/sign-debug.png) 

Finally, edit __Debug.xcconfig__ to include the signing configuration. This xcconfig feature allows configuration reuse.

![Debug](/assets/images/xcconfig/debug.png)

You are now ready to set your build configuration.

## Set XCode Configurations
By setting the Configurations to an xcconfig, XCode applies the build settings to the project.
The way to set the configuration is the same for Debug and Release so only Debug will be shown here.

Highlight __XCConfig Signing__ in the Project navigator, then select the __XCConfig Signing__ target. Under __Configurations__, expand __Debug__ and from the __XConfig Signing__ target choose __Debug__.

![Set Debug](/assets/images/xcconfig/set-debug.png)

The Debug configuration is set as shown.

![Debug Set](/assets/images/xcconfig/debug-config-set.png)

With the configuration set to use the build settings from the xcconfig, you can now update the signing settings.

## Update Signing Settings

Highlight __XCConfig Signing__ in the Project navigator, then select the __XCConfig Signing__ project. Choose the __Build Settings__ tab, type __signing__ in the search field to filter the signing settings.

The __Signing__ settings you have to update are:
* __Code Signing Identity__: Set to the development certificate SHA-1 hash. There are cases such as this sample project where the code signing identify value is not automatically reflected in the field. If you have the same experience then the value has to be set as described in this section.
* __Development Team__: Set to the team identifier.
* __Provisioning Profile__: Set to the the provisioning profile UDID.

![Signing Settings](/assets/images/xcconfig/signing-settings.png)

To set the fields, expand the field settings and choose __Other...__

![Dropdown](/assets/images/xcconfig/setting-dropdown.png)

Type __$(inherited)__ in the text field and press __return__. 

![Inherited](/assets/images/xcconfig/inherited.png)

Do the same for the rest of the fields. Once done, the Debug signing settings is as shown.

![Done](/assets/images/xcconfig/setting-done.png)

## Verify the Settings

To verify your signing settings, attach a device to your development Mac, choose the device as the build target in XCode, and press ⌘+B to build. A successful build confirms that the signing settings are right.


That's it! You have configured your XCode project to use xcconfig. You can now run your app on a device. Happy developing!!!


