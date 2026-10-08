# MAM Quick Start Guide (End User – Pilot)

> This is recommended guidance for a limited pilot of MAM without enrollment on
> iOS/iPadOS and Android. It is not a complete production deployment guide.

## Objective

Access company email, Teams, and files on a personal device without enrolling
it. Windows MAM is outside the scope of this pilot guide.

Your organization must assign you the relevant apps and policies, and you need
an appropriate Intune license.

---

## 1. Install the required broker

- **Android:** Install Company Portal from Google Play. It is required for App
  Protection Policy delivery.
- **iOS/iPadOS:** Install Microsoft Authenticator when your organization
  requires it as the broker for Entra authentication or Conditional Access.
  Company Portal is not universally required on iOS/iPadOS.

---

## 2. Sign in

Open the required broker or Company Portal and sign in with your work account.
Follow any Entra registration, PIN, or permission prompts.

---

## 3. Install protected apps

Install the apps assigned for the pilot manually from Company Portal or from
the public App Store or Google Play:
- Microsoft Outlook
- Microsoft Teams
- Microsoft OneDrive

The apps are not silently installed on an unenrolled device. Microsoft
Authenticator is a broker, not a replacement for the protected apps.

---

## 4. Open a protected app

Open the app, sign in with your work account, and follow the prompts. You may
be asked to set an app PIN, enable biometrics, or allow permissions. These
prompts and the available apps depend on the pilot policies.

---

## 5. Optional Outlook contacts synchronization

Only test this if your organization enabled it for the pilot:

1. Allow Contacts permission when prompted.
2. In Outlook settings, enable **Save Contacts** if instructed.

This intentionally copies supported work contacts to the device's native
contacts store. Contacts synchronized directly from Outlook can be removed by
an Intune MAM selective wipe, but copies synchronized onward by the native
contacts service may not be removable by Intune.

---

## 6. Pilot validation

1. Sign in to the protected apps and confirm that company data is available.
2. Confirm that the app PIN and other protection controls are applied.
3. If contacts synchronization is enabled, test Outlook contacts only.
4. During the pilot, an administrator may request an Intune app selective wipe.
   Open the app if asked; it may need to be open for the wipe to process.
5. Confirm that company data is removed while personal device data remains.

---

## 7. Start working

You can now use the protected apps assigned for the pilot. Your device is not
enrolled; only company data inside supported apps is managed and protected.
