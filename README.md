# Intune Guides

Step-by-step guides for admins and users to configure and use Microsoft Intune across different enrollment scenarios.

---

## 📍 Start here

Guides live under [`docs/`](docs/), organized by Intune workload and scenario:

- **[`app-protection/`](docs/app-protection/)** — MAM / App Protection Policy guides (managing apps without device enrollment).
- **[`device-enrollment/`](docs/device-enrollment/)** — Android and iOS/iPadOS device enrollment scenarios.
- **[`conditional-access/`](docs/conditional-access/)** — Conditional Access guidance and deprecation notes.
- **[`printing/`](docs/printing/)** — Universal Print deployment guidance.

Each scenario folder contains an admin-focused guide and/or a user-focused guide. New guides should follow the same layout — see [`templates/guide-template.md`](templates/guide-template.md) for the starting point.

---

## 📋 Guides Overview

### 🔒 App Protection – MAM (Without Enrollment)

Manage company apps on personal devices **without enrolling the device** into Intune.

| Guide | Audience | Platform | Description |
|------|----------|----------|-------------|
| [Admin guide](docs/app-protection/mam-without-enrollment/admin-guide.md) | Admin | iOS & Android | Configure MAM policies in Intune: deploy apps (Outlook, Teams, OneDrive, Authenticator), set up App Protection Policies, App Configuration Policies, and assign them to users. |
| [User guide](docs/app-protection/mam-without-enrollment/user-guide.md) | End User | iOS & Android | Install Company Portal, sign in with a work account, install apps, and enable contact sync on a personal device — without device enrollment. |

---

### 🤖 Device Enrollment – Android Work Profile

Separate work and personal data on Android devices using an **Android Enterprise Work Profile**.

| Guide | Audience | Platform | Description |
|------|----------|----------|-------------|
| [Admin guide](docs/device-enrollment/android-work-profile/admin-guide.md) | Admin | Android | Enable Android Enterprise, configure Work Profile enrollment, approve apps via Managed Google Play, deploy App Protection Policies, App Configuration Policies, and compliance policies. |
| [User guide](docs/device-enrollment/android-work-profile/user-guide.md) | End User | Android | Enroll an Android device, set up the Work Profile, install apps, allow contacts permission, and understand how work contacts appear for caller ID and search while keeping work and personal data separate. |

---

### 🍎 Device Enrollment – iOS/iPadOS (Company Portal)

Fully enroll **iPhone / iPad** devices into Intune via Company Portal (BYOD).

| Guide | Audience | Platform | Description |
|------|----------|----------|-------------|
| [Admin guide](docs/device-enrollment/ios-ipados-company-portal/admin-guide.md) | Admin | iOS/iPadOS | Configure iOS enrollment prerequisites, deploy and assign required apps, set up App Protection Policies, App Configuration Policies, and compliance policies. |
| [User guide](docs/device-enrollment/ios-ipados-company-portal/user-guide.md) | End User | iOS/iPadOS | Install Company Portal, enroll the device, install a management profile, and complete app setup. Covers how work contacts sync to the device. |

---

### 🖨️ Printing – Universal Print

| Guide | Audience | Platform | Description |
|------|----------|----------|-------------|
| [Deployment plan](docs/printing/universal-print/deployment-plan.md) | Admin | Cross-platform | Plan and deploy Universal Print, including licensing, printer registration, sharing, and policy configuration. |

---

### 🚦 Conditional Access

| Guide | Audience | Platform | Description |
|------|----------|----------|-------------|
| [Require approved client app – deprecation](docs/conditional-access/require-approved-client-app-deprecation.md) | Admin | iOS & Android | Understand the deprecation of the "Require approved client app" Conditional Access grant control and how to migrate to app protection–based policies. |

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

Most contributions require you to agree to a **Contributor License Agreement (CLA)** declaring that you have the right to, and actually do, grant us the rights to use your contribution. For details, visit https://cla.opensource.microsoft.com.

---

## 📜 Code of Conduct

This project has adopted the [Microsoft Open Source Code of Conduct](https://opensource.microsoft.com/codeofconduct/). See [CODE_OF_CONDUCT.md](CODE_OF_CONDUCT.md) for details or contact [opencode@microsoft.com](mailto:opencode@microsoft.com) with any questions.

---

## ⚖️ License

This project is licensed under the MIT License — see the [LICENSE](LICENSE) file for details.

---

## 🔒 Security

Please do **not** report security vulnerabilities through public GitHub issues. See [SECURITY.md](SECURITY.md) for instructions on responsible disclosure.
