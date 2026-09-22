# Ubuntu Intune Enrollment with Microsoft Entra and SSO

**Audience:** End user, administrator  
**Platform:** Ubuntu Desktop  
**Intune workload:** Devices  
**Last reviewed:** 2026-09-22  
**Status:** Validated

---

## Overview

This guide enrolls an Ubuntu Desktop device into Microsoft Intune using a Microsoft Entra work or school account, then validates SSO-oriented access with Microsoft Edge.

On Linux, enrollment is performed through the Microsoft Intune app. It is not the same as the Windows OOBE Microsoft Entra join flow.

## Scope

- Platform: Ubuntu Desktop 26.04 LTS
- Environment: Physical or Hyper-V x86/x64 device
- Management: Microsoft Intune
- Identity: Microsoft Entra ID
- Browser for SSO testing: Microsoft Edge

## Prerequisites

- Ubuntu Desktop 24.04 LTS or 26.04 LTS with the GNOME desktop environment.
- A Microsoft Entra work or school account.
- Intune licensing for the enrolling user.
- Permission for the user to enroll Linux devices.
- Internet access to Microsoft package repositories and Intune services.
- Microsoft Intune compliance policies assigned to the user or device group, if compliance is being tested.

## 1. Prepare Ubuntu

Open Terminal in Ubuntu and update the system:

```bash
sudo apt update
sudo apt upgrade -y
```

Confirm you are using the normal Ubuntu GNOME desktop session, not WSL or a server-only shell.

## 2. Install the Microsoft Intune app

Microsoft recommends using the Linux Intune installer from the official shell samples repository.

Run:

```bash
sudo apt install -y curl ca-certificates
mkdir -p ~/Downloads/intune-installer
cd ~/Downloads/intune-installer
curl -L -o installer.sh https://raw.githubusercontent.com/microsoft/shell-intune-samples/master/Linux/Intune%20Installer/installer.sh
chmod +x installer.sh
./installer.sh
```

The installer sets up the Microsoft Intune app and required dependencies, including Microsoft Edge.

If the raw installer URL changes, use the Microsoft redirect:

```text
https://go.microsoft.com/fwlink/?linkid=2358529
```

## 3. Enroll the Ubuntu device

Launch the Microsoft Intune app:

```bash
intune-portal
```

Or open **Microsoft Intune** from the Ubuntu app launcher.

Then complete enrollment:

1. Sign in with your Microsoft Entra work or school account.
2. Complete MFA if prompted.
3. Accept the device registration and enrollment prompts.
4. Wait for the compliance evaluation to complete.
5. Keep the Intune app open until the device shows as registered or enrolled.

## 4. Verify in Microsoft Intune

In the Microsoft Intune admin center, verify the device appears:

```text
Devices > Linux > Linux devices
```

Check that the Ubuntu device is listed and has a compliance status.

## 5. Verify in Microsoft Entra

In the Microsoft Entra admin center, verify the device appears:

```text
Identity > Devices > All devices
```

The device should be associated with the signed-in user.

## 6. Configure and test SSO behavior

Open Microsoft Edge:

```bash
microsoft-edge
```

Then:

1. Sign in to Edge with the same Microsoft Entra work or school account.
2. Go to:

   ```text
   https://myapps.microsoft.com
   ```

3. Open a Microsoft 365 app or another Entra-integrated app.
4. Confirm the session does not repeatedly prompt for credentials after the device is enrolled and compliant.

For best results, use Microsoft Edge when testing Conditional Access and SSO behavior on Linux.

## 7. Recommended Intune lab checks

Confirm these items in the Intune admin center:

| Area | Check |
|---|---|
| Enrollment | The user is licensed for Intune and allowed to enroll Linux devices. |
| Compliance policy | A Linux compliance policy is assigned to the user or device group. |
| Conditional Access | If testing compliance, use a test policy that requires a compliant device for a test cloud app. |
| Device platform | Ubuntu Desktop 24.04 LTS or 26.04 LTS is used. |
| Browser | Microsoft Edge is installed and signed in with the same Entra account. |

## 8. Useful commands

Check whether Intune packages are installed:

```bash
apt list --installed | grep intune
```

Start the Intune app:

```bash
intune-portal
```

Refresh compliance:

1. Open the Microsoft Intune app.
2. Sign in if prompted.
3. Open the device details or compliance issues page.
4. Select **Refresh**.

## 9. Reset enrollment if needed

To remove the Intune app and local registration data:

```bash
sudo apt remove intune-portal
sudo apt purge intune-portal
```

After purging, reinstall the Intune app and enroll again if needed.

## 10. Recommended lab flow

1. Update Ubuntu.
2. Install the Microsoft Intune app.
3. Enroll with the Microsoft Entra test user.
4. Verify the device in Intune.
5. Verify the device in Microsoft Entra.
6. Sign in to Microsoft Edge with the same account.
7. Test access to `https://myapps.microsoft.com`.
8. Test Conditional Access with a policy that requires a compliant device.

## Troubleshooting

| Symptom | Likely cause | Resolution |
|---|---|---|
| Device does not appear in Intune | Enrollment did not complete or the user is not licensed | Reopen the Intune app, sign in, and confirm the user has an Intune license. |
| Device appears but remains noncompliant | Compliance policy requirements are not met | Open the Intune app compliance page, review the failing setting, remediate it, and select **Refresh**. |
| SSO prompts repeatedly | Edge is not signed in or device compliance has not updated | Sign in to Edge with the same account and wait for Intune compliance to refresh. |

## References

- [Get the Microsoft Intune app for Linux](https://learn.microsoft.com/en-us/intune/user-help/company-portal/intune-app-linux)
- [Linux device compliance settings in Microsoft Intune](https://learn.microsoft.com/en-us/intune/device-security/compliance/ref-linux-settings)
- [Microsoft shell Intune samples - Linux Intune Installer](https://github.com/microsoft/shell-intune-samples/tree/master/Linux/Intune%20Installer)
