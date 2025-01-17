---
# required metadata

title: Android Enterprise compliance settings in Microsoft Intune - Azure | Microsoft Docs
description: See a list of all the settings you can use when setting compliance for your Android Enterprise devices in Microsoft Intune. Set password rules, choose a minimum or maximum operating system version, restrict specific apps, prevent reusing password, and more.
keywords:
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 04/15/2019
ms.topic: reference
ms.service: microsoft-intune
ms.localizationpriority: medium
ms.technology:
ms.assetid: 9da89713-6306-4468-b211-57cfb4b51cc6

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: joglocke
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection: M365-identity-device-management
---

# Android Enterprise settings to mark devices as compliant or not compliant using Intune

[!INCLUDE [azure_portal](./includes/azure_portal.md)]

This article lists and describes the different compliance settings you can configure on Android Enterprise devices in Intune. As part of your mobile device management (MDM) solution, use these settings to mark rooted (jailbroken) devices as not compliant, set an allowed threat level, enable Google Play Protect, and more.

This feature applies to:

- Android Enterprise

As an Intune administrator, use these compliance settings to help protect your organizational resources. To learn more about compliance policies, and what they do, see [get started with device compliance](device-compliance-get-started.md).

> [!IMPORTANT]
> Compliance policies also apply Android Enterprise dedicated devices. If a compliance policy is assigned to a dedicated device, the device may show as **Not compliant**. Conditional Access and enforcing compliance isn't available on dedicated devices. Be sure to complete any tasks or actions to get dedicated devices compliant with your assigned policies.

## Before you begin

[Create a compliance policy](create-compliance-policy.md#create-the-policy). For **Platform**, select **Android Enterprise**.

## Device owner

### Device properties

- **Minimum OS version**: When a device doesn't meet the minimum OS version requirement, it's reported as non-compliant. A link with information on how to upgrade is shown. The end user can upgrade their device, and then access organization resources.
- **Maximum OS version**: When a device is using an OS version later than the version in the rule, access to organization resources is blocked. The user is asked to contact their IT administrator. Until a rule is changed to allow the OS version, this device can't access organization resources.

### System security

- **Require a password to unlock mobile devices**: **Require** users to enter a password before they can access their device. When you choose **Not configured** (default), this setting isn't evaluated for compliance or non-compliance.

  This setting is applied at the device level. If you only need to require a password at the work profile level, then use a configuration policy. See [Android Enterprise device configuration settings](device-restrictions-android-for-work.md).

  - **Required password type**: Choose if a password should include only numeric characters, or a mix of numerals and other characters. Your options:
    - **Device default**
    - **Password required, no restrictions**
    - **Weak biometric**: [Strong vs. weak biometrics](https://android-developers.googleblog.com/2018/06/better-biometrics-in-android-p.html) (opens Android's web site)
    - **Numeric**: Password must only be numbers, such as `123456789`. Enter the **minimum password length** a user must enter, between 4 and 16 characters.
    - **Numeric complex**: Repeated or consecutive numbers, such as "1111" or "1234", aren't allowed. Enter the **minimum password length** a user must enter, between 4 and 16 characters.
    - **Alphabetic**: Letters in the alphabet are required. Numbers and symbols aren't required. Enter the **minimum password length** a user must enter, between 4 and 16 characters.
    - **Alphanumeric**: Includes uppercase letters, lowercase letters, and numeric characters. Enter the **minimum password length** a user must enter, between 4 and 16 characters.
    - **Alphanumeric with symbols**: Includes uppercase letters, lowercase letters, numeric characters, punctuation marks, and symbols. Also enter:

      - **Minimum password length**: Enter the minimum length the password must have, between 4 and 16 characters.
      - **Number of characters required**: Enter the number of characters the password must have, between 0 and 16 characters.
      - **Number of lowercase characters required**: Enter the number of lowercase characters the password must have, between 0 and 16 characters.
      - **Number of uppercase characters required**: Enter the number of uppercase characters the password must have, between 0 and 16 characters.
      - **Number of non-letter characters required**: Enter the number of non-letters (anything other than letters in the alphabet) the password must have, between 0 and 16 characters.
      - **Number of numeric characters required**: Enter the number of numeric characters (`1`, `2`, `3`, and so on) the password must have, between 0 and 16 characters.
      - **Number of symbol characters required**: Enter the number of symbol characters (`&`, `#`, `%`, and so on) the password must have, between 0 and 16 characters.

- **Maximum minutes of inactivity before password is required**: Enter the idle time before the user must reenter their password. When you choose **Not configured** (default), this setting isn't evaluated for compliance or non-compliance.
- **Number of days until password expires**: Enter the number of days, between 1-365, until the device password must be changed. For example, to change the password after 60 days, enter `60`. When the password expires, users are prompted to create a new password.
- **Number of passwords required before user can reuse a password**: Enter the number of recent passwords that can't be reused, between 1-24. Use this setting to restrict the user from creating previously used passwords.

- **Encryption of data storage on device**: Choose **Require** to encrypt data storage on your devices. When you choose **Not configured** (default), this setting isn't evaluated for compliance or non-compliance.

  You don't have to configure this setting because Android Enterprise devices enforce encryption.

Select **OK** > **Create** to save your changes.

## Work profile

### Device health

- **Rooted devices**: Choose **Block** to mark rooted (jailbroken) devices as not compliant. When you choose **Not configured** (default), this setting isn't evaluated for compliance or non-compliance.
- **Require the device to be at or under the Device Threat Level**: Use this setting to take the risk assessment from the Lookout Mobile Endpoint Security solution as a condition for compliance. When you choose **Not configured** (default), this setting isn't evaluated for compliance or non-compliance. To use this setting, choose the allowed threat level:
  - **Secured**: This option is the most secure, and means that the device can't have any threats. If the device is detected with any level of threats, it's evaluated as noncompliant.
  - **Low**: The device is evaluated as compliant if only low-level threats are present. Anything higher puts the device in a noncompliant status.
  - **Medium**: The device is evaluated as compliant if the threats that are present on the device are low or medium level. If the device is detected to have high-level threats, it's determined to be noncompliant.
  - **High**: This option is the least secure, as it allows all threat levels. It may be useful if you're using this solution only for reporting purposes.

#### Google Play Protect

- **Google Play Services is configured**: **Require** that the Google Play services app is installed and enabled. Google Play services allows security updates, and is a base-level dependency for many security features on certified-Google devices. When you choose **Not configured** (default), this setting isn't evaluated for compliance or non-compliance.
- **Up-to-date security provider**: **Require** that an up-to-date security provider can protect a device from known vulnerabilities. When you choose **Not configured** (default), this setting isn't evaluated for compliance or non-compliance.
- **SafetyNet device attestation**: Enter the level of [SafetyNet attestation](https://developer.android.com/training/safetynet/attestation.html) that must be met. Your options:
  - **Not configured** (default): Setting isn't evaluated for compliance or non-compliance.
  - **Check basic integrity**
  - **Check basic integrity & certified devices**

> [!NOTE]
> On Android Enterprise devices, **Threat scan on apps** is a device configuration policy. Using a configuration policy, administrators can enable the setting on a device. See [Android Enterprise device restriction settings](device-restrictions-android-for-work.md).

### Device properties

- **Minimum OS version**: When a device doesn't meet the minimum OS version requirement, it's reported as non-compliant. A link with information on how to upgrade is shown. The end user can upgrade their device, and then access organization resources.
- **Maximum OS version**: When a device is using an OS version later than the version in the rule, access to organization resources is blocked. The user is asked to contact their IT administrator. Until a rule is changed to allow the OS version, this device can't access organization resources.

### System security

- **Require a password to unlock mobile devices**: **Require** users to enter a password before they can access their device. When you choose **Not configured** (default), this setting isn't evaluated for compliance or non-compliance. This setting is applied at the device level. If you only need to require a password at the work profile level, then use a configuration policy. See [Android Enterprise device configuration settings](device-restrictions-android-for-work.md).
- **Required password type**: Choose if a password should include only numeric characters, or a mix of numerals and other characters. Your options:
  - **Device Default**
  - **Low security biometric**
  - **At least numeric** (default): Enter the **minimum password length** a user must enter, between 4 and 16 characters.
  - **Numeric complex**: Enter the **minimum password length** a user must enter, between 4 and 16 characters.
  - **At least alphabetic**: Enter the **minimum password length** a user must enter, between 4 and 16 characters.
  - **At least alphanumeric**: Enter the **minimum password length** a user must enter, between 4 and 16 characters.
  - **At least alphanumeric with symbols**: Enter the **minimum password length** a user must enter, between 4 and 16 characters.

- **Maximum minutes of inactivity before password is required**: Enter the idle time before the user must reenter their password. When you choose **Not configured** (default), this setting isn't evaluated for compliance or non-compliance.
- **Number of days until password expires**: Select the number of days before the password expires, and the end user must create a new password.
- **Number of previous passwords to prevent reuse**: Enter the number of recent passwords that can't be reused. Use this setting to restrict the user from creating previously used passwords.

#### Encryption

- **Encryption of data storage on device**: Choose **Require** to encrypt data storage on your devices. When you choose **Not configured** (default), this setting isn't evaluated for compliance or non-compliance. 

  You don't have to configure this setting because Android Enterprise devices enforce encryption.

#### Device Security

- **Block apps from unknown sources**: Choose to **block** devices with **Security** > **Unknown Sources** enabled sources (supported on Android 4.0 – Android 7.x; not supported by Android 8.0 and later). When you choose **Not configured** (default), this setting isn't evaluated for compliance or non-compliance.

  To side-load apps, unknown sources must be allowed. If you're not side-loading Android apps, then set this feature to **Block** to enable this compliance policy.

  > [!IMPORTANT]
  > Side-loading applications require that the **Block apps from unknown sources** setting is enabled. Enforce this compliance policy only if you're not side-loading Android apps on devices.

  You don't have to configure this setting as Android Enterprise devices always restrict installation from unknown sources.

- **Company portal app runtime integrity**: Choose **Require** to confirm the Company Portal app meets all the following requirements:

  - Has the default runtime environment installed
  - Is properly signed
  - Isn't in debug-mode
  - Is installed from a known source

  When you choose **Not configured** (default), this setting isn't evaluated for compliance or non-compliance.

- **Block USB debugging on device**: Choose **Block** to prevent devices from using the USB debugging feature. When you choose **Not configured** (default), this setting isn't evaluated for compliance or non-compliance.

  You don't have to configure this setting because USB debugging is already disabled on Android Enterprise devices.

- **Minimum security patch level**: Select the oldest security patch level a device can have. Devices that aren't at least at this patch level are noncompliant. The date must be entered in the *YYYY-MM-DD* format.

Select **OK** > **Create** to save your changes.

## Next steps

- [Add actions for noncompliant devices](actions-for-noncompliance.md) and [use scope tags to filter policies](scope-tags.md).
- [Monitor your compliance policies](compliance-policy-monitor.md).
- See the [compliance policy settings for Android](compliance-policy-create-android.md) devices.
