# Intune Configuration Guide – Android Work Profile (Admin)

## Objective
Configure Android Enterprise Work Profile with Microsoft Intune to:

- Separate work and personal data
- Deploy Outlook, Teams, OneDrive, Authenticator
- Enable contact sync from Outlook to device
- Protect data using App Protection Policies

---

## 1. Enable Android Enterprise

Navigate to:
Devices → Android → Android enrollment

Configure:
- Android Enterprise
- Connect Managed Google Play
- Complete onboarding

---

## 2. Configure Work Profile Enrollment

Navigate to:
Devices → Android → Android enrollment

Select:
- Personally owned devices with work profile

Configuration:
- Allow enrollment

---

## 3. Approve Applications (Managed Google Play)

Navigate to:
Apps → Android → Managed Google Play

Approve:
- Microsoft Outlook
- Microsoft Teams
- Microsoft OneDrive
- Microsoft Authenticator
- Company Portal

Sync apps to Intune

---

## 4. Deploy Applications

Navigate to:
Apps → All apps

### Assignments

#### Required apps
- Company Portal → Required
- Microsoft Authenticator → Required

#### User-installed apps
- Outlook → Available
- Teams → Available
- OneDrive → Available

Target:
- User group

---

## 5. Configure App Protection Policy (APP)

Navigate to:
Apps → App protection policies → Create

Platform:
- Android

Target:
- Core Microsoft Apps

---

### Recommended settings

#### Data protection
- Receive data from other apps → All apps
- Send org data to other apps → Policy managed apps
- Restrict cut, copy, paste → Policy managed apps
- Save copies of org data → Block

#### Access
- Require PIN → Yes
- Biometrics → Allow

---

### Data sharing (IMPORTANT FOR CONTACTS)

Set:
- Sync policy managed app data with native apps or add-ins → Allow

This enables Outlook to export contacts outside the app.

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

## 8. Contacts Sync – Technical Requirements

To enable contact synchronization:

### Required configuration

1. App Protection Policy:
   - Sync policy managed app data with native apps → Allow

2. Outlook App Configuration:
   - Save Contacts → Yes

3. Device permission:
   - User must allow Contacts access

---

### Result

- Outlook exports contacts into Android Work Profile contacts provider
- Contacts remain within work profile boundary

---

## 9. Final Architecture

- Device enrolled (Work Profile)
- Apps installed into Work Profile
- Outlook data protected via APP
- Contacts available for caller ID and search (via OS integration)
