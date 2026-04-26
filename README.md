# Intune Guides

Step-by-step guides for admins and users to configure and use Microsoft Intune across different enrollment scenarios.

---

## 📋 Guides Overview

### 🔒 MAM – Mobile Application Management (Without Enrollment)

Manage company apps on personal devices **without enrolling the device** into Intune.

| File | Audience | Description |
|------|----------|-------------|
| [MAM admin.md](MAM%20admin.md) | Admin | Configure MAM policies in Intune: deploy apps (Outlook, Teams, OneDrive, Authenticator), set up App Protection Policies, App Configuration Policies, and Conditional Access. Includes contact sync configuration. |
| [MAM user.md](MAM%20user.md) | End User | Install Company Portal, sign in with a work account, install apps, and enable contact sync on a personal device — without device enrollment. |

---

### 🤖 Android Work Profile (WP)

Separate work and personal data on Android devices using an **Android Enterprise Work Profile**.

| File | Audience | Description |
|------|----------|-------------|
| [WP admin](WP%20admin) | Admin | Enable Android Enterprise, configure Work Profile enrollment, approve apps via Managed Google Play, deploy App Protection Policies, App Configuration Policies, and Conditional Access. Includes contact sync setup. |
| [WP user](WP%20user) | End User | Enroll an Android device, set up the Work Profile, install apps, allow contacts permission, and understand how work contacts appear for caller ID and search while staying within the Work Profile boundary. |

---

### 🍎 iOS Device Enrollment (Company Portal)

Fully enroll **iPhone / iPad** devices into Intune via Company Portal (BYOD).

| File | Audience | Description |
|------|----------|-------------|
| [iOS device enrollment admin](iOS%20device%20enrollment%20admin) | Admin | Configure iOS enrollment prerequisites, deploy and assign required apps, set up App Protection Policies, App Configuration Policies for Outlook, and Conditional Access. Includes contact sync behavior notes. |
| [iOS device enrollment user](iOS%20device%20enrollment%20user) | End User | Install Company Portal, enroll the device, install a management profile, and complete app setup. Covers how work contacts are synced to the device and what that means for privacy. |

---

## 📌 Quick Reference

| Scenario | Device Enrollment | Platform | Contact Sync Behavior |
|----------|-------------------|----------|-----------------------|
| MAM | ❌ No | iOS & Android | iOS: copied to device · Android: device-dependent |
| Work Profile | ✅ Yes (Work Profile) | Android | Contacts stay in Work Profile; available for caller ID |
| iOS Enrollment | ✅ Yes (MDM) | iOS | Contacts copied to device; accessible by all apps |
