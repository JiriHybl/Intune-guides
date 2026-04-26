# Intune Guides

Step-by-step guides for admins and users to configure and use Microsoft Intune across different enrollment scenarios.

---

## 📋 Guides Overview

### 🔒 MAM – Mobile Application Management (Without Enrollment)

Manage company apps on personal devices **without enrolling the device** into Intune.

| File | Audience | Description |
|------|----------|-------------|
| [MAM admin.md](MAM%20admin.md) | Admin | Configure MAM policies in Intune: deploy apps (Outlook, Teams, OneDrive, Authenticator), set up App Protection Policies, App Configuration Policies, and assign them to users. |
| [MAM user.md](MAM%20user.md) | End User | Install Company Portal, sign in with a work account, install apps, and enable contact sync on a personal device — without device enrollment. |

---

### 🤖 Android Work Profile (WP)

Separate work and personal data on Android devices using an **Android Enterprise Work Profile**.

| File | Audience | Description |
|------|----------|-------------|
| [WP admin](WP%20admin) | Admin | Enable Android Enterprise, configure Work Profile enrollment, approve apps via Managed Google Play, deploy App Protection Policies, App Configuration Policies, and compliance policies. |
| [WP user](WP%20user) | End User | Enroll an Android device, set up the Work Profile, install apps, allow contacts permission, and understand how work contacts appear for caller ID and search while keeping personal data separate. |

---

### 🍎 iOS Device Enrollment (Company Portal)

Fully enroll **iPhone / iPad** devices into Intune via Company Portal (BYOD).

| File | Audience | Description |
|------|----------|-------------|
| [iOS device enrollment admin](iOS%20device%20enrollment%20admin) | Admin | Configure iOS enrollment prerequisites, deploy and assign required apps, set up App Protection Policies, App Configuration Policies, and compliance policies. |
| [iOS device enrollment user](iOS%20device%20enrollment%20user) | End User | Install Company Portal, enroll the device, install a management profile, and complete app setup. Covers how work contacts sync to the device. |

---

## 📌 Quick Reference

| Scenario | Device Enrollment | Platform | Contact Sync Behavior |
|----------|-------------------|----------|-----------------------|
| MAM | ❌ No | iOS & Android | iOS: copied to device · Android: device-dependent |
| Work Profile | ✅ Yes (Work Profile) | Android | Contacts stay in Work Profile; available for caller ID |
| iOS Enrollment | ✅ Yes (MDM) | iOS | Contacts copied to device; accessible by all apps |

---

## 🤝 Contributing

This project welcomes contributions and suggestions. Please read [CONTRIBUTING.md](CONTRIBUTING.md) before submitting a pull request.

Most contributions require you to agree to a **Contributor License Agreement (CLA)** declaring that you have the right to, and actually do, grant us the rights to use your contribution. For details, visit [https://cla.opensource.microsoft.com](https://cla.opensource.microsoft.com).

---

## 📜 Code of Conduct

This project has adopted the [Microsoft Open Source Code of Conduct](https://opensource.microsoft.com/codeofconduct/). See [CODE_OF_CONDUCT.md](CODE_OF_CONDUCT.md) for details or contact [opencode@microsoft.com](mailto:opencode@microsoft.com) with any questions.

---

## ⚖️ License

This project is licensed under the MIT License — see the [LICENSE](LICENSE) file for details.

---

## 🔒 Security

Please do **not** report security vulnerabilities through public GitHub issues. See [SECURITY.md](SECURITY.md) for instructions on responsible disclosure.
