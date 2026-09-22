# Configure Windows Update Maintenance Windows in Microsoft Intune

**Audience:** Administrator  
**Platform:** Windows  
**Intune workload:** Devices  
**Last reviewed:** 2026-09-23  
**Status:** Validated

---

## Overview

Use Windows Update maintenance windows in Microsoft Intune to define when selected Windows Update actions, such as **installation** and **restart**, are allowed to start.

Maintenance windows are useful for kiosks, manufacturing devices, medical devices, and other endpoints where update activity must occur during a controlled servicing period.

If Windows Autopatch is already configured, keep the existing Autopatch configuration and add the maintenance-window policy separately.

## Prerequisites

- Microsoft Intune enrolled device.
- Windows 11, version 24H2 or later.
- Current Windows updates installed.
- Windows Update managed through Intune.
- A Microsoft Entra device group containing the devices that should use the maintenance window.
- Intune administrator permissions to create and assign device configuration profiles.

## Administrator steps

### 1. Create the policy

1. Open the **Microsoft Intune admin center**.
2. Go to **Devices > Manage devices > Configuration > Create > New policy**.
3. Configure:
   - **Platform:** Windows 10 and later
   - **Profile type:** Settings catalog
4. Select **Create**.

### 2. Add the maintenance-window settings

1. Give the policy a descriptive name, such as:

   ```text
   Windows Update - Maintenance Window
   ```

2. Under **Configuration settings**, select **Add settings**.
3. Search for:

   ```text
   Maintenance Window
   ```

4. Under **Windows Update**, add these settings:
   - **Maintenance Window Enabled**
   - **Maintenance Window Start Date Time**
   - **Maintenance Window Duration**
   - **Maintenance Window Recurrence Type**
   - **Maintenance Window Governed Actions**

### 3. Enable the maintenance window

Configure **Maintenance Window Enabled** as:

```text
Enabled
```

### 4. Configure the start time

Configure **Maintenance Window Start Date Time** using ISO 8601 format.

Example:

```text
2026-09-26T22:00:00.000Z
```

The `Z` suffix represents UTC. Take the required local maintenance time into account when setting the value.

### 5. Configure the duration

Configure **Maintenance Window Duration** in minutes.

For example, for a five-hour maintenance period:

```text
300
```

Example:

```text
Start:     22:00
Duration:  300 minutes

22:00 -------------------- 03:00
       Maintenance Window
```

### 6. Configure recurrence

Configure **Maintenance Window Recurrence Type**.

| Value | Recurrence |
|------:|------------|
| `1` | One time |
| `2` | Daily |
| `3` | Weekly |
| `4` | Monthly |

For example, use the following value for a daily maintenance window:

```text
2
```

### 7. Choose which update actions the window controls

Configure **Maintenance Window Governed Actions**.

| Value | Action |
|------:|--------|
| `1` | Install updates |
| `2` | Restart device |
| `3` | Install updates and restart |

To have both installation and update-triggered restart controlled by the maintenance window, configure:

```text
3
```

### 8. Assign and create the policy

1. Select **Next** and open **Assignments**.
2. Under **Included groups**, add the Microsoft Entra device group containing the devices that should use the maintenance window.
3. Select **Next > Review + create > Create**.

The maintenance-window policy is now deployed separately from any existing Windows Autopatch configuration.

## End-user steps

No end-user action is required. The policy applies through Intune after assignment and device check-in.

## Example configuration

A simple nightly servicing configuration could look like this:

```text
Maintenance Window Enabled
    Enabled

Maintenance Window Start Date Time
    2026-09-26T22:00:00.000Z

Maintenance Window Duration
    360

Maintenance Window Recurrence Type
    2

Maintenance Window Governed Actions
    3
```

Result:

```text
22:00                                      04:00
  |==========================================|
             MAINTENANCE WINDOW

              Install updates
                    +
              Restart device
```

## Validation

- [ ] The settings catalog profile reports as successfully deployed.
- [ ] The target Windows device receives the maintenance-window configuration.
- [ ] Windows Update installation and restart actions occur only within the configured maintenance window.
- [ ] Existing Windows Autopatch behavior remains in place if Autopatch is used.

## Troubleshooting

| Symptom | Likely cause | Resolution |
|---|---|---|
| Policy does not apply | Device is not in the assigned Microsoft Entra group | Confirm group membership and wait for Intune assignment evaluation. |
| Maintenance window uses the wrong local time | Start time was configured in UTC without local-time conversion | Convert the intended local time to UTC and update **Maintenance Window Start Date Time**. |
| Updates install but restart outside the window | Governed actions only control installation | Set **Maintenance Window Governed Actions** to `3` to control both installation and restart. |
| Device does not recognize the setting | Windows version is below the supported minimum | Upgrade the device to Windows 11, version 24H2 or later. |

## Rollback

1. In the Intune admin center, open the maintenance-window settings catalog profile.
2. Remove or exclude the assignment.
3. Confirm the device receives the updated policy.
4. Delete the profile if the maintenance window is no longer needed.
5. Restore the prior Windows Update or Windows Autopatch configuration if necessary.

## References

- [Microsoft Learn: Windows update management overview](https://learn.microsoft.com/en-us/intune/device-updates/windows/)
- [Intune maintenance window configuration example](https://anavem.com/tutorials/intune-configure-maintenance-windows)
