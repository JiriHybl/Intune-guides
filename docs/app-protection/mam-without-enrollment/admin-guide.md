# Intune MAM Configuration Guide (Admin – MAM without Enrollment)

> This is recommended guidance for a limited pilot of MAM without enrollment on
> iOS/iPadOS and Android. It is not a complete production deployment guide.

## Objective

Configure Microsoft Intune Mobile Application Management (MAM) for:
- Microsoft Outlook
- Microsoft Teams
- Microsoft OneDrive

without requiring device enrollment. Windows MAM is outside the scope of this
pilot guide.

Pilot users need an appropriate Intune license, an organizational account, and
must be targeted by the relevant app protection, app configuration, and (where
used) Conditional Access policies.

---

## 1. Deploy Applications

### Step 1 – Add apps

Go to:
Apps → All apps → Add

Add the protected apps needed for the pilot:
- Microsoft Outlook
- Microsoft Teams
- Microsoft OneDrive

Add Microsoft Authenticator when it is needed as the iOS/iPadOS broker for
applicable Entra authentication and Conditional Access scenarios.

### Step 2 – Assign apps

For apps distributed through Intune to unenrolled pilot users:
- Assignment: **Available with or without enrollment**
- Target: The pilot user group

Users manually install assigned apps from Company Portal or install supported
apps from the public App Store or Google Play. Apps are not silently installed
on unenrolled devices.

---

## 2. Broker and app installation requirements

- **Android:** Company Portal is required on the device for App Protection
  Policy delivery.
- **iOS/iPadOS:** Microsoft Authenticator is the broker for applicable Entra
  authentication and Conditional Access scenarios. Company Portal is not
  universally required.
- On either platform, protected apps may be installed from Company Portal or
  the public app store, depending on the pilot design.

---

## 3. Configure Company Portal (MAM Experience)

Go to:
Tenant admin → Customization

Create the pilot customization:
- Device enrollment = Unavailable

This hides the enrollment option for the pilot flow; it does not enroll the
device.

---

## 4. Configure App Protection Policy (APP)

Go to:
Apps → App protection policies → Create

Platform:
- iOS/iPadOS
- Android

Target the pilot group and the protected apps being tested (for example,
Outlook, Teams, and OneDrive).

### Data protection

- Receive data from other apps = All apps
- Send org data to other apps = Policy managed apps
- Save copies of org data = Block
- Restrict cut, copy, paste = Policy managed apps

### Access requirements

- Require PIN = Yes
- Biometric = Allow

### Data sharing (optional)

To test Outlook contacts synchronization, set:
- Sync policy managed app data with native apps or add-ins = Allow

Keep this disabled unless exporting work contacts to the native contacts store
is intentional for the pilot.

---

## 5. Configure App Configuration Policy (Outlook)

Go to:
Apps → App configuration policies → Add → Managed apps

Target Microsoft Outlook and the pilot group. For the contacts test, configure:
- Save Contacts = Yes

The APP setting and the Outlook configuration setting must both allow contact
synchronization. The user must also grant Contacts permission on the device.

---

## 6. Configure Conditional Access

Create a pilot-only policy with:
- Users: Include only the pilot group
- Exclude an emergency-access account and appropriate administrators
- Platforms: iOS/iPadOS and Android
- Target resources: Exchange Online is sufficient for an Outlook-focused pilot
- Grant: **Require app protection policy**
- Mode: Start in **Report-only**

Validate sign-in and policy behavior before changing the policy to **On**.
If Teams or OneDrive are being tested, explicitly expand the targeted resources
to cover those services; targeting Exchange Online alone does not cover them.

Do not use the retired/legacy **Require approved client app** control for new
guidance.

---

## 7. Contacts Sync – Technical Requirement

Contact synchronization is optional. Enabling it intentionally exports
supported work contacts from Outlook to the device's native contacts store.

Configure all three:
1. APP: Sync policy managed app data with native apps = Allow
2. Outlook app configuration: Save Contacts = Yes
3. User permission: The user allows Contacts access on the device

Contacts synchronized directly from Outlook can be removed by an Intune MAM
selective wipe. However, copies that the native contacts service synchronizes
to another external service or destination may not be removable by Intune.

---

## 8. Pilot validation

1. Sign in to each protected app and confirm access.
2. Verify that the APP controls, such as the PIN and data-transfer restrictions,
   are applied.
3. If contacts synchronization is enabled, test Outlook contacts and confirm
   the expected native contacts behavior.
4. Submit an Intune app selective wipe for a pilot user. Have the user open the
   app if necessary for the wipe to process.
5. Confirm company data is removed while personal device data remains.

---

## Final State

- No device enrollment is required.
- Pilot users install apps manually.
- Data is protected inside supported apps by MAM policies.
- Any contacts synchronization is an intentional, separately validated export.
