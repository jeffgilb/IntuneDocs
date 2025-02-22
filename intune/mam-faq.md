---
# required metadata

title: Frequently asked questions about MAM and app protection
description: This article provides answers to some frequently asked questions on Intune mobile application management (MAM) and Intune app protection.
keywords:
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 06/04/2019
ms.topic: conceptual
ms.service: microsoft-intune
ms.localizationpriority: high
ms.technology:
ms.assetid: 149def73-9d08-494b-97b7-4ba1572f0623

# optional metadata
  
#audience:
#ms.devlang:
ms.reviewer: erikre
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection: M365-identity-device-management
---

# Frequently asked questions about MAM and app protection

This article provides answers to some frequently asked questions on Intune mobile application management (MAM) and Intune app protection.

## MAM Basics

**What is MAM?**<br></br>
[Intune mobile application management](/intune/app-lifecycle) refers to the suite of Intune management features that lets you publish, push, configure, secure, monitor, and update mobile apps for your users.

**What are the benefits of MAM app protection?**<br></br>
MAM protects an organization's data within an application. With MAM without enrollment (MAM-WE), a work or school-related app that contains sensitive data can be managed on almost any device, including personal devices in bring-your-own-device (BYOD) scenarios. Many productivity apps, such as the Microsoft Office apps, can be managed by Intune MAM. See the official list of [Intune-managed apps](https://www.microsoft.com/cloud-platform/microsoft-intune-apps) available for public use.

**What device configurations does MAM support?**<br></br>
Intune MAM supports two configurations:
- **Intune MDM + MAM**: IT administrators can only manage apps using MAM and app protection policies on devices that are enrolled with Intune mobile device management (MDM). To manage apps using MDM + MAM, customers should use the Intune console in the Azure portal at https://portal.azure.com.

- **MAM without device enrollment**: MAM without device enrollment, or MAM-WE, allows IT administrators to manage apps using MAM and app protection policies on devices not enrolled with Intune MDM. This means apps can be managed by Intune on devices enrolled with third-party EMM providers. To manage apps using MAM-WE, customers should use the Intune console in the Azure portal at https://portal.azure.com. Also, apps can be managed by Intune on devices enrolled with third-party Enterprise Mobility Management (EMM) providers or not enrolled with an MDM at all.


## App protection policies

**What are app protection policies?**<br></br>
App protection policies are rules that ensure an organization's data remains safe or contained in a managed app. A policy can be a rule that is enforced when the user attempts to access or move "corporate" data, or a set of actions that are prohibited or monitored when the user is inside the app.

**What are examples of app protection policies?**<br></br>
See the [Android app protection policy settings](app-protection-policy-settings-android.md) and [iOS app protection policy settings](app-protection-policy-settings-ios.md) for detailed information on each app protection policy setting.

**Is it possible to have both MDM and MAM policies applied to the same user at the same time, for different devices? For example, if a user could be able to access their work resources from their own MAM-enabled machine, but also come to work and use an Intune MDM-managed device. Are there any caveats to this idea?**<br></br>
If you apply a MAM policy to the user without setting the device state, the user will get the MAM policy on both the BYOD device and the Intune-managed device. You can also apply a MAM policy based on the managed state. So when you create an app protection policy, next to Target to all app types, you'd select No. Then do any of the following:
- Apply a less strict MAM policy to Intune managed devices, and apply a more restrictive MAM policy to non MDM-enrolled devices.
- Apply a MAM policy to unenrolled devices only.

For more information, see [How to monitor app protection policies](app-protection-policies-monitor.md).

## Apps you can manage with app protection policies

**Which apps can be managed by app protection policies?**<br></br>
Any app that has been integrated with the [Intune App SDK](/intune/app-sdk) or wrapped by the [Intune App Wrapping Tool](/intune/apps-prepare-mobile-application-management) can be managed using Intune app protection policies. See the official list of [Intune-managed apps](https://www.microsoft.com/cloud-platform/microsoft-intune-apps) available for public use.

**What are the baseline requirements to use app protection policies on an Intune-managed app?**

- The end user must have an Azure Active Directory (AAD) account. See [Add users and give administrative permission to Intune](/intune/users-permissions-add) to learn how to create Intune users in Azure Active Directory.

- The end user must have a license for Microsoft Intune assigned to their Azure Active Directory account. See [Manage Intune licenses](/intune/licenses-assign) to learn how to assign Intune licenses to end users.

- The end user must belong to a security group that is targeted by an app protection policy. The same app protection policy must target the specific app being used. App protection policies can be created and deployed in the Intune console in the [Azure portal](https://portal.azure.com). Security groups can currently be created in the [Microsoft 365 admin center](https://admin.microsoft.com).

- The end user must sign into the app using their AAD account.

**What if I want to enable an app with Intune App Protection but it is not using a supported app development platform?** 

The Intune SDK development team actively tests and maintains support for apps built with the native Android, iOS (Obj-C, Swift), Xamarin, Xamarin.Forms, and Cordova platforms. While some customers have had success with Intune SDK integration with other platforms such as React Native and NativeScript, we do not provide explicit guidance or plugins for app developers using anything other than our supported platforms.

**Does the Intune APP SDK support Microsoft Authentication Library (MSAL), or social accounts?**<br></br>
The Intune APP SDK uses some advanced ADAL capabilities for both the 1st party and the 3rd party versions of the SDK. As such, MSAL does not work well with many of our core scenarios such as authentication into the Intune App Protection service and conditional launch. Given that the overall guidance from Microsoft's Identity team is to switch to MSAL for all of the Microsoft Office apps, the Intune SDK will eventually need to support it, but there are no plans today.

**What are the additional requirements to use the [Outlook mobile app](https://products.office.com/outlook)?**

- The end user must have the Outlook mobile app installed to their device.

- The end user must have an [Office 365 Exchange Online](https://products.office.com/exchange/exchange-online) mailbox and license linked to their Azure Active Directory account.

  >[!NOTE]
  > The Outlook mobile app currently only supports Intune App Protection for Microsoft Exchange Online and [Exchange Server with hybrid modern authentication](https://technet.microsoft.com/library/mt846639(v=exchg.160).aspx) and does not support Exchange in Office 365 Dedicated.

**What are the additional requirements to use the [Word, Excel, and PowerPoint](https://products.office.com/business/office) apps?**

- The end user must have a license for [Office 365 Business or Enterprise](https://products.office.com/business/compare-more-office-365-for-business-plans) linked to their Azure Active Directory account. The subscription must include the Office apps on mobile devices and can include a cloud storage account with [OneDrive for Business](https://onedrive.live.com/about/business/). Office 365 licenses can be assigned in the [Microsoft 365 admin center](https://admin.microsoft.com) following these [instructions](https://support.office.com/article/Assign-or-remove-licenses-for-Office-365-for-business-997596b5-4173-4627-b915-36abac6786dc).

- The end user must have a managed location configured using the granular save as functionality under the "Prevent Save As" application protection policy setting. For example, if the managed location is OneDrive, the [OneDrive](https://onedrive.live.com/about/) app should be configured in the end user's Word, Excel, or PowerPoint app.

- If the managed location is OneDrive, the app must be targeted by the app protection policy deployed to the end user.

  >[!NOTE]
  > The Office mobile apps currently only support SharePoint Online and not SharePoint on-premises.

**Why is a managed location (i.e. OneDrive) needed for Office?**<br></br>
Intune marks all data in the app as either "corporate" or "personal." Data is considered "corporate" when it originates from a business location. For the Office apps, Intune considers the following as business locations: email (Exchange) or cloud storage (OneDrive app with a OneDrive for Business account).

**What are the additional requirements to use Skype for Business?**<br></br>
See [Skype for Business](https://products.office.com/skype-for-business/it-pros) license requirements. For Skype for Business (SfB) hybrid and on-prem configurations, see [Hybrid Modern Auth for SfB and Exchange goes GA](https://techcommunity.microsoft.com/t5/Skype-for-Business-Blog/Hybrid-Modern-Auth-for-SfB-and-Exchange-goes-GA/ba-p/134756) and [Modern Auth for SfB OnPrem with AAD](https://techcommunity.microsoft.com/t5/Skype-for-Business-Blog/Modern-Auth-for-SfB-OnPrem-with-AAD/ba-p/180910), respectively.

## App protection features

**What is multi-identity support?**<br></br>
Multi-identity support is the ability for the Intune App SDK to only apply app protection policies to the work or school account signed into the app. If a personal account is signed into the app, the data is untouched.

**What is the purpose of multi-identity support?**<br></br>
Multi-identity support allows apps with both "corporate" and consumer audiences (i.e. the Office apps) to be released publicly with Intune app protection capabilities for the "corporate" accounts.

**What about Outlook and multi-identity?**<br></br>
Because Outlook has a combined email view of both personal and "corporate" emails, the Outlook app prompts for the Intune PIN on launch.

**What is the Intune app PIN?**<br></br>
The Personal Identification Number (PIN) is a passcode used to verify that the correct user is accessing the organization's data in an application.

- **When is the user prompted to enter their PIN?**<br></br> Intune prompts for the user's app PIN when the user is about to access "corporate" data. In multi-identity apps such as Word/Excel/PowerPoint, the user is prompted for their PIN when they try to open a "corporate" document or file. In single-identity apps, such as line-of-business apps managed using the Intune App Wrapping Tool, the PIN is prompted at launch, because the Intune App SDK knows the user's experience in the app is always "corporate."

- **How often will the user be prompted for the Intune PIN?**<br></br> The IT admin can define the Intune app protection policy setting 'Recheck the access requirements after (minutes)' in the Intune admin console. This setting specifies the amount of time before the access requirements are checked on the device, and the application PIN screen is shown again. However, important details about PIN that affect how often the user will be prompted are: 

    - **The PIN is shared among apps of the same publisher to improve usability:** On iOS, one app PIN is shared amongst all apps **of the same app publisher**. On Android, one app PIN is shared amongst all apps.
    - **The 'Recheck the access requirements after (minutes)' behavior  after a device reboot:** A "PIN timer" tracks the number of minutes of inactivity that determine when to show the Intune app PIN next. On iOS, the PIN timer is unaffected by device reboot. Thus, device restart has no effect on the number of minutes the user has been inactive from an iOS app with Intune PIN policy. On Android, the PIN timer is reset on device reboot. As such, Android apps with Intune PIN policy will likely prompt for an app PIN regardless of the 'Recheck the access requirements after (minutes)' setting value **after a device reboot**.  
    - **The rolling nature of the timer associated with the PIN:** Once a PIN is entered to access an app (app A), and the app leaves the foreground (main input focus) on the device, the PIN timer gets reset for that PIN. Any app (app B) that shares this PIN will not prompt the user for PIN entry because the timer has reset. The prompt will show up again once the 'Recheck the access requirements after (minutes)' value is met again.

For iOS devices, even if the PIN is shared between apps from different publishers, the prompt will show up again when the **Recheck the access requirements after (minutes)** value is met again for the app that is not the main input focus. So, for example, a user has app _A_ from publisher _X_ and app _B_ from publisher _Y_, and those two apps share the same PIN. The user is focused on app _A_ (foreground), and app _B_ is minimized. After the **Recheck the access requirements after (minutes)** value is met and the user switches to app _B_, the PIN would be required.

  >[!NOTE] 
  > In order to verify the user's access requirements more often (i.e. PIN prompt), especially for a frequently used app, it is recommended to reduce the value of the 'Recheck the access requirements after (minutes)' setting. 
      
- **How does the Intune PIN work with built-in app PINs for Outlook and OneDrive?**<br></br>
The Intune PIN works based on an inactivity-based timer (aka the value of 'Recheck the access requirements after (minutes)'). As such, Intune PIN prompts show up independently from the built-in app PIN prompts for Outlook and OneDrive which often are tied to app launch by default. If the user receives both PIN prompts at the same time, the expected behavior should be that the Intune PIN takes precedence. 

- **Is the PIN secure?**<br></br> The PIN serves to allow only the correct user to access their organization's data in the app. Therefore, an end user must sign in with their work or school account before they can set or reset their Intune app PIN. This authentication is handled by Azure Active Directory via secure token exchange and is not transparent to the Intune App SDK. From a security perspective, the best way to protect work or school data is to encrypt it. Encryption is not related to the app PIN but is its own app protection policy.

- **How does Intune protect the PIN against brute force attacks?**<br></br> As part of the app PIN policy, the IT administrator can set the maximum number of times a user can try to authenticate their PIN before locking the app. After the number of attempts has been met, the Intune App SDK can wipe the "corporate" data in the app.
  
- **Why do I have to set a PIN twice on apps from same publisher?**<br></br> MAM (on iOS) currently allows application-level PIN with alphanumeric and special characters (called 'passcode') which requires the participation of applications (i.e. WXP, Outlook, Managed Browser, Yammer) to integrate the Intune APP SDK for iOS. Without this, the passcode settings are not properly enforced for the targeted applications. This was a feature released in the Intune SDK for iOS v. 7.1.12. <br><br> In order to support this feature and ensure backward compatibility with previous versions of the Intune SDK for iOS, all PINs (either numeric or passcode) in 7.1.12+ are handled separately from the numeric PIN in previous versions of the SDK. Therefore, if a device has applications with Intune SDK for iOS versions before 7.1.12 AND after 7.1.12 from the same publisher, they will have to set up two PINs. <br><br> That being said, the two PINs (for each app) are not related in any way i.e. they must adhere to the app protection policy that’s applied to the app. As such, *only* if apps A and B have the same policies applied (with respect to PIN), user may setup the same PIN twice. <br><br> This behavior is specific to the PIN on iOS applications that are enabled with Intune Mobile App Management. Over time, as applications adopt later versions of the Intune SDK for iOS, having to set a PIN twice on apps from the same publisher becomes less of an issue. Please see the note below for an example.

  >[!NOTE]
  > For example, if app A is built with a version prior to 7.1.12 and app B is built with a version greater than or equal to 7.1.12 from the same publisher, the end user will need to set up PINs separately for A and B if both are installed on an iOS device. <br><br> If an app C that has SDK version 7.1.9 is installed on the device, it will share the same PIN as app A. <br><br> An app D built with 7.1.14 will share the same PIN as app B. <br><br> If only apps A and C are installed on a device, then one PIN will need to be set. The same applies to if only apps B and D are installed on a device.

**What about encryption?**<br></br>
IT administrators can deploy an app protection policy that requires app data to be encrypted. As part of the policy, the IT administrator can also specify when the content is encrypted.

- **How does Intune encrypt data?**<br></br> See the [Android app protection policy settings](app-protection-policy-settings-android.md) and [iOS app protection policy settings](app-protection-policy-settings-ios.md) for detailed information on the encryption app protection policy setting.

- **What gets encrypted?**<br></br> Only data marked as "corporate" is encrypted according to the IT administrator's app protection policy. Data is considered "corporate" when it originates from a business location. For the Office apps, Intune considers the following as business locations: email (Exchange) or cloud storage (OneDrive app with a OneDrive for Business account). For line-of-business apps managed by the Intune App Wrapping Tool, all app data is considered "corporate."

**How does Intune remotely wipe data?**<br></br>
Intune can wipe app data in three different ways: full device wipe, selective wipe for MDM, and MAM selective wipe. For more information about remote wipe for MDM, see [Remove devices by using wipe or retire](devices-wipe.md). For more information about selective wipe using MAM, see [the Retire action](devices-wipe.md#retire) and [How to wipe only corporate data from apps](apps-selective-wipe.md).

- **What is wipe?**<br></br> [Wipe](devices-wipe.md) removes all user data and settings from **the device** by restoring the device to its factory default settings. The device is removed from Intune.
  >[!NOTE]
  > Wipe can only be achieved on devices enrolled with Intune mobile device management (MDM).

- **What is selective wipe for MDM?**<br></br> See [Remove devices - retire](devices-wipe.md#retire) to read about removing company data.

- **What is selective wipe for MAM?**<br></br> Selective wipe for MAM simply removes company app data from an app. The request is initiated using the Intune Azure portal. To learn how to initiate a wipe request, see [How to wipe only corporate data from apps](apps-selective-wipe.md).

- **How quickly does selective wipe for MAM happen?**<br></br> If the user is using the app when selective wipe is initiated, the Intune App SDK checks every 30 minutes for a selective wipe request from the Intune MAM service. It also checks for selective wipe when the user launches the app for the first time and signs in with their work or school account.

**Why don't On-Premises (on-prem) services work with Intune protected apps?**<br></br>
Intune app protection depends on the identity of the user to be consistent between the application and the Intune App SDK. The only way to guarantee that is through modern authentication. There are scenarios in which apps may work with an on-prem configuration, but they are neither consistent nor guaranteed.

**Is there a secure way to open web links from managed apps?**<br></br>
Yes! The IT administrator can deploy and set app protection policy for the [Intune Managed Browser app](app-configuration-managed-browser.md), a web browser developed by Microsoft Intune that can be managed easily with Intune. The IT administrator can require all web links in Intune-managed apps to be opened using the Managed Browser app.



## App experience on Android

**Why is the Company Portal app needed for Intune app protection to work on Android devices?**<br></br>
Much of app protection functionality is built into the Company Portal app. Device enrollment is _not required_ even though the Company Portal app is always required. For MAM-WE, the end user just needs to have the Company Portal app installed on the device.

**How do multiple Intune app protection access settings that are configured to the same set of apps and users work on Android?**<br></br>
Intune app protection policies for access will be applied in a specific order on end user devices as they try to access a targeted app from their corporate account. In general, a block would take precedence, then a dismissible warning. For example, if applicable to the specific user/app, a minimum Android patch version setting that warns a user to take a patch upgrade will be applied after the minimum Android patch version setting that blocks the user from access. So, in the scenario where the IT admin configures the min Android patch version to 2018-03-01 and the min Android patch version (Warning only) to 2018-02-01, while the device trying to access the app was on a patch version 2018-01-01, the end user would be blocked based on the more restrictive setting for min Android patch version that results in blocked access. 

When dealing with different types of settings, an app version requirement would take precedence, followed by Android operating system version requirement and Android patch version requirement. Then, any warnings for all types of settings in the same order are checked.

**Intune App Protection Policies provide the capability for admins to require end user devices to pass Google's SafetyNet Attestation for Android devices. How often is a new SafetyNet Attestation result sent to the service?** <br><br> A new Google Play service determination will be reported to the IT admin at an interval determined by the Intune service. How often the service call is made is throttled due to load, thus this value is maintained internally and is not configurable. Any IT admin configured action for the Google SafetyNet Attestation setting will be taken based on the last reported result to the Intune service at the time of conditional launch. If there is no data, access will be allowed depending on no other conditional launch checks failing, and Google Play Service "roundtrip" for determining attestation results will begin in the backend and prompt the user asynchronously if the device has failed. If there is stale data, access will be blocked or allowed depending on the last reported result, and similarly, a Google Play Service "roundtrip" for determining attestation results will begin and prompt the user asynchronously if the device has failed.

**Intune App Protection Policies provide the capability for admins to require end user devices to send signals via Google's Verify Apps API for Android devices. How can an end user turn on the app scan so that they are not blocked from access due to this?**<br><br> The instructions on how to do this vary slightly by device. The general process involves going to the Google Play Store, then clicking on **My apps & games**, clicking on the result of the last app scan which will take you into the Play Protect menu. Ensure the toggle for **Scan device for security threats** is switched to on.

**What does Google's SafetyNet Attestation API actually check on Android devices? What is the difference between the configurable values of 'Check basic integrity' and 'Check basic integrity & certified devices'?** <br><br>
Intune leverages Google Play Protect SafetyNet APIs to add to our existing root detection checks for unenrolled devices. Google has developed and maintained this API set for Android apps to adopt if they do not want their apps to run on rooted devices. The Android Pay app has incorporated this, for example. While Google does not share publicly the entirety of the root detection checks that occur, we expect these APIs to detect users who have rooted their devices. These users can then be blocked from accessing, or their corporate accounts wiped from their policy enabled apps. 'Check basic integrity' tells you about the general integrity of the device. Rooted devices, emulators, virtual devices, and devices with signs of tampering fail basic integrity. 'Check basic integrity & certified devices' tells you about the compatibility of the device with Google's services. Only unmodified devices that have been certified by Google can pass this check. Devices that will fail include the following:
* Devices that fail basic integrity
* Devices with an unlocked bootloader
* Devices with a custom system image/ROM
* Devices for which the manufacturer didn’t apply for, or pass, Google certification 
* Devices with a system image built directly from the Android Open Source Program source files
* Devices with a beta/developer preview system image

See [Google's documentation on the SafetyNet Attestation](https://developer.android.com/training/safetynet/attestation) for technical details.

**There are two similiar checks in the Conditional Launch section when creating an Intune App Protection Policy for Android devices. Should I be requiring the 'SafetyNet device attestation' setting or the 'jailbroken/rooted devices' setting?** <br><br>
Google Play Protect's SafetyNet API checks require the end user being online, atleast for the duration of the time when the "roundtrip" for determining attestation results executes. If end user is offline, IT admin can still expect a result to be enforced from the 'jailbroken/rooted devices' setting. That being said, if the end user has been offline too long, the 'Offline grace period' value comes into play, and all access to work or school data is blocked once that timer value is reached, until network access is available. Turning on both settings allows for a layered approach to keeping end user devices healthy which is important when end users access work or school data on mobile. 

**The app protection policy settings that leverage Google Play Protect APIs require Google Play Services to function. What if Google Play Services are not allowed in the location where the end user may be?**<br><br>
Both the 'SafetyNet device attestation', and 'Threat scan on apps' settings require Google determined version of Google Play Services to function correctly. Since these are settings that fall in the area of security, the end user will be blocked if they have been targeted with these settings and are not meeting the appropriate version of Google Play Services or have no access to Google Play Services. 

## App experience on iOS
**What happens if I add or remove a fingerprint or face to my device?**<br></br>
Intune app protection policies allow control over app access to only the Intune licensed user. One of the ways to control access to the app is to require either Apple's Touch ID or Face ID on supported devices. Intune implements a behavior where if there is any change to the device's biometric database, Intune prompts the user for a PIN when the next inactivity timeout value is met. Changes to biometric data include the addition or removal of a fingerprint, or face. If the Intune user does not have a PIN set, they are led to set up an Intune PIN.
 
The intent of this is to continue keeping your organization's data within the app secure and protected at the app level. This feature is only available for iOS, and requires the participation of applications that integrate the Intune APP SDK for iOS, version 9.0.1 or later. Integration of the SDK is necessary so that the behavior can be enforced on the targeted applications. This integration happens on a rolling basis and is dependent on the specific application teams. Some apps that participate include WXP, Outlook, Managed Browser, and Yammer. 
  
**I am able to use the iOS share extension to open work or school data in unmanaged apps, even with the data transfer policy set to "managed apps only" or "no apps." Doesn't this leak data?**<br></br>
Intune app protection policy cannot control the iOS share extension without managing the device. Therefore, Intune _**encrypts "corporate" data before it is shared outside the app**_. You can validate this by attempting to open the "corporate" file outside of the managed app. The file should be encrypted and unable to be opened outside the managed app.

**How do multiple Intune app protection access settings that are configured to the same set of apps and users work on iOS?**<br></br>
Intune app protection policies for access will be applied in a specific order on end user devices as they try to access a targeted app from their corporate account. In general, a wipe would take precedence, followed by a block, then a dismissible warning. For example, if applicable to the specific user/app, a minimum iOS operating system setting that warns a user to update their iOS version will be applied after the minimum iOS operating system setting that blocks the user from access. So, in the scenario where the IT admin configures the min iOS operating system to 11.0.0.0 and the min iOS operating system (Warning only) to 11.1.0.0, while the device trying to access the app was on iOS 10, the end user would be blocked based on the more restrictive setting for min iOS operating system version that results in blocked access.

When dealing with different types of settings, an Intune App SDK version requirement would take precedence, then an app version requirement, followed by the iOS operating system version requirement. Then, any warnings for all types of settings in the same order are checked. We recommend the Intune App SDK version requirement be configured only upon guidance from the Intune product team for essential blocking scenarios.


## See also
- [Implement your Intune plan](planning-guide-onboarding.md)
- [Intune testing and validation](planning-guide-test-validation.md)
- [Android mobile app management policy settings in Microsoft Intune](app-protection-policy-settings-android.md)
- [iOS mobile app management policy settings](app-protection-policy-settings-ios.md)
- [App protection policies policy refresh](app-protection-policy-delivery.md)
- [Validate your app protection policies](app-protection-policy-delivery.md)
- [Add app configuration policies for managed apps without device enrollment](app-configuration-policies-managed-app.md)
- [How to get support for Microsoft Intune](get-support.md)
