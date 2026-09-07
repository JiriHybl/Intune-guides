# Intune MAM Configuration Guide (Admin – MAM without Enrollment)

## Objective
Configure Microsoft Intune Mobile Application Management (MAM) for iOS and Android devices using:
- Microsoft Outlook
- Microsoft Teams
- Microsoft OneDrive
- Microsoft Authenticator

without requiring device enrollment.

---

## 1. Deploy Applications

### Step 1 – Add apps
Go to:
Apps → All apps → Add

Add:
- Microsoft Outlook
- Microsoft Teams
- Microsoft OneDrive
- Microsoft Authenticator

### Step 2 – Assign apps
For each app:
- Assignment: Available for enrolled devices
- Target: All Users

NOTE: Apps can still be used without enrollment when accessed via Company Portal + MAM.

---

## 2. Deploy Company Portal (Required Entry Point)

Users must install:
- Company Portal (iOS App Store / Google Play)

Purpose:
- Authentication broker
- App discovery and installation

---

## 3. Configure Company Portal (MAM Experience)

Go to:
Tenant admin → Customization

Create policy for MAM users:
- Device enrollment = Unavailable

Result:
- Enrollment option hidden
- Users stay in MAM-only flow

---

## 4. Configure App Protection Policy (APP)

Go to:
Apps → App protection policies → Create

Platform:
- iOS/iPadOS
- Android

Target apps:
- Core Microsoft Apps (or explicitly Outlook, Teams, OneDrive)

### Data protection
- Receive data from other apps = All apps
- Send org data to other apps = Policy managed apps
- Save copies of org data = Block
- Restrict cut, copy, paste = Policy managed apps

### Access requirements
- Require PIN = Yes
- Biometric = Allow

### Data sharing (IMPORTANT)
To allow Outlook contacts to sync to native apps:

Set:
- Sync policy managed app data with native apps or add-ins = Allow

NOTE:
This enables apps to export data to native OS (contacts/calendar if supported).

---

## 5. Configure App Configuration Policy (Outlook)

Go to:
Apps → App configuration policies → Add → Managed apps

Target: Microsoft Outlook

Settings:
- Focused Inbox = Off
- External Recipients MailTip = On
- Block External Images = On
- Save Contacts = Yes

IMPORTANT:
Both settings are required for contacts sync:
- APP → allows native app sync
- Outlook config → Save Contacts = Yes

---

## 6. Configure Conditional Access

Create policy:
- Target: Exchange Online
- Grant: Require app protection policy

Result:
- Only protected apps can access data

---

## 7. Contacts Sync – Technical Requirement

To sync contacts to native apps you MUST configure:

1. App Protection Policy:
   Sync policy managed app data with native apps = Allow

2. Outlook App Configuration:
   Save Contacts = Yes

3. User permission:
   User must allow Contacts access on device

Result:
- Outlook exports contacts to native Contacts app

WARNING:
- iOS → contacts copied to device (full exposure)
- Android → depends on device/profile behavior

---

## Final State

- No device enrollment required
- Apps installed via Company Portal
- Outlook contacts can sync to native contacts
- Data protected via MAM policies
