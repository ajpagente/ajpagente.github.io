---
title: "Generate an ipa from the command-line"
categories: 
  - mobile
tags:
  - ios
  - development
---

The article [Configuring XCode Project Signing with xcconfig]({% link _posts/2020-03-09-using-xcconfig.md %}) describes setting up an XCode project for manual signing with xcconfig. This article uses the same project and describes how to generate an ipa from the command-line.

Before you jump to the command-line, make sure that the Xcode project __Archive__ setting is configured correctly.

## Verify archive setting
The XCode project's __Debug__ configuration is set to use xcconfig. By default, XCode sets the scheme's __Archive__ phase to the __Release__ configuration. To modify the __Archive__ phase setting, edit the __XCConfig Signing__ scheme and choose __Archive__.

![Before scheme update](/assets/images/xcconfig/scheme-archive-config.png)
 
 Update the __Build Configuration__ to __Debug__ from the dropdown then click __Close__ to close the dialog. The __XCConfig Signing__ scheme is now set to the __Debug__ configuration for archiving. 

![Scheme updated](/assets/images/xcconfig/scheme-archive-config-updated.png)

Launch __Terminal__ and navigate to the folder where your __xcodeproj__ file is located.

## Generate an ipa
__xcodebuild__ is a command-line tool that allows you to perform various operations on your Xcode projects and workspaces from the command line. To generate an ipa, execute the __archive__ and __export__ operations in sequence.

### 1. Archive app

To archive the app, run the following command from the Terminal.
```
xcodebuild -project <your-project-name>.xcodeproj -scheme <scheme name> -archivePath <path/to/your/app>.xcarchive archive
```

The command applied to the project is as shown.
```
xcodebuild -project XCConfig\ Signing.xcodeproj -scheme "XCConfig Signing" -archivePath out/myapp.xcarchive archive
```

__myapp.xcarchive__ is generated in the __out__ folder.

![xcarchive-out](/assets/images/xcconfig/xcarchive-out.png)

### 2. Export archive to ipa 

To export the archive to an ipa, run the following command from the Terminal.
```
xcodebuild -exportArchive -archivePath <path/to/your/app>.xcarchive -exportPath <path/to/ipa/output/folder> -exportOptionsPlist <path/to/ExportOptions>.plist
```

The __exportOptionsPlist__ is a plist file that configures archive exporting. You can download the __export-options.plist__ template and modify it with your profile and certificate settings.

<script src="https://gist.github.com/ajpagente/e3715e019a800365db91c627476eff22.js"></script>

The command applied to the project is as shown.
```
xcodebuild -exportArchive -archivePath out/myapp.xcarchive -exportPath out -exportOptionsPlist export.plist
```

__XCConfig Signing.ipa__, DistributionSummary.plist, ExportOptions.plist, and Packaging.log are generated in the __out__ folder.

![ipa-out](/assets/images/xcconfig/ipa-out.png)

Voila! You are now able to take a manually-signed XCode project using xcconfig and  generate an ipa from the command-line. Happy developing!!