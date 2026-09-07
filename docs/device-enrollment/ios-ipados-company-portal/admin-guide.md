# Intune Configuration Guide – iOS Device Enrollment (Company Portal)

## Objective

Configure iOS devices using Microsoft Intune with device enrollment via Company Portal to:

- Deploy Outlook, Teams, OneDrive, Authenticator as required apps
- Enable Outlook contact synchronization
- Secure corporate data using App Protection Policies
- Manage devices via MDM

---

## 1. Prerequisites

- Apple MDM Push Certificate configured in Intune
- iOS/iPadOS enrollment enabled
- Microsoft Intune license assigned to users

---

## 2. Configure iOS Enrollment

Navigate to:
Devices → iOS/iPadOS → Enrollment

Ensure:
- Device enrollment is enabled
- Enrollment type: Company Portal (BYOD)

---

## 3. Deploy Required Applications

Navigate to:
Apps → All apps → Add

### Add apps (iOS App Store):

- Microsoft Outlook  
- Microsoft Teams  
- Microsoft OneDrive  
- Microsoft Authenticator  
- Company Portal  

---

## 4. Assign Applications

For each application configure:

### Required apps (MANDATORY)

Assign:
- Microsoft Outlook → Required
- Microsoft Teams → Required
- Microsoft OneDrive → Required
- Microsoft Authenticator → Required
- Company Portal → Required

Target:
- User group

---

## 5. Configure App Protection Policy (APP)

Navigate to:
Apps → App protection policies → Create

Platform:
- iOS/iPadOS

Target:
- Core Microsoft Apps

---

### Data protection

- Receive data from other apps → All apps  
- Send org data to other apps → Policy managed apps  
- Save copies of org data → Block  
- Backup org data to iCloud → Block  
- Restrict cut, copy, paste → Policy managed apps  

---

### Access requirements

- Require PIN → Yes  
- Biometric → Allow  

---

### Data sharing (required for contacts sync)

Set:
- Sync policy managed app data with native apps or add-ins → Allow  

---

## 6. Configure App Configuration Policy (Outlook)

Navigate to:
Apps → App configuration policies → Add → Managed apps

Target:
- Microsoft Outlook

---

### Settings

- Focused Inbox → Off  
- External Recipients MailTip → On  
- Block External Images → On  
- Save Contacts → Yes  

---

## 7. Configure Conditional Access

Create policy:

- Target:
  Exchange Online  

- Grant:
  Require app protection policy  

---

## 8. Contacts Sync – Technical Behavior

### Required configuration

1. App Protection Policy:
   Sync policy managed app data with native apps = Allow  

2. Outlook App Configuration:
   Save Contacts = Yes  

3. User permission:
   User must allow Contacts access  

---

### iOS behavior (IMPORTANT)

- Contacts are physically copied into the iOS Contacts database  
- Contacts become available to ALL apps on the device  
- Data is no longer protected by Intune once exported  

---

## 9. Final State

- Device is enrolled via Company Portal  
- All required apps are automatically installed  
- Outlook data is protected inside the app  
- Contacts may be synced to device (based on policy)  
