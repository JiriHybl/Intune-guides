# Use Android AMAPI Policy Schema in an Intune Scenario

**Audience:** Administrator  
**Platform:** Android  
**Intune workload:** Devices  
**Last reviewed:** 2026-11-24  
**Status:** Draft

---

## Overview

This scenario adds a reusable Android Enterprise baseline based on the Android Management API (AMAPI) policy schema and keeps the schema snapshot in this repository for versioned review.

Use this when you want an Intune-friendly policy baseline that maps to AMAPI concepts (apps, kiosk behavior, update controls, connectivity, and restrictions) and a source-controlled schema reference.

## Artifacts in this scenario

- Schema snapshot: [`amapi-reference.md`](./amapi-reference.md)
- Scenario guide: this file (`admin-guide.md`)

## Prerequisites

- Intune tenant with Android Enterprise connected to Managed Google Play.
- One or more test devices enrolled as Android Enterprise (for example, Work Profile, Dedicated, or Fully Managed).
- Intune role permissions to create and assign Android configuration and app policies.
- A pilot Microsoft Entra group for staged rollout.

## Administrator steps

### 1. Review the schema snapshot

1. Open [`amapi-reference.md`](./amapi-reference.md).
2. Start with **Resource: Policy** and identify fields relevant to your scenario:
   - `applications`
   - `kioskCustomization`
   - `systemUpdate` / `unifiedUpdatePolicy`
   - `statusReportingSettings`
   - `advancedSecurityOverrides`

### 2. Build a baseline policy payload

Use the schema field names as your design source, then map them to your Intune profiles.

Example baseline payload (AMAPI-style structure):

```json
{
  "name": "Policy baseline - frontline Android",
  "applications": [
    {
      "packageName": "com.microsoft.launcher.enterprise",
      "installType": "FORCE_INSTALLED"
    },
    {
      "packageName": "com.microsoft.office.outlook",
      "installType": "AVAILABLE"
    }
  ],
  "statusReportingSettings": {
    "applicationReportsEnabled": true,
    "deviceSettingsEnabled": true
  },
  "systemUpdate": {
    "type": "AUTOMATIC"
  },
  "advancedSecurityOverrides": {
    "untrustedAppsPolicy": "DISALLOW_INSTALL"
  }
}
```

### 3. Implement equivalent controls in Intune

1. In the Intune admin center, go to **Devices > Manage devices > Configuration** and create Android Enterprise profiles for the required controls.
2. Go to **Apps > Android > Managed Google Play** and approve all required packages from your baseline.
3. Assign required applications and configuration profiles to the pilot group.

### 4. Validate on pilot devices

1. Confirm required apps install with expected install behavior.
2. Confirm targeted restrictions and update behavior are applied.
3. Confirm reporting and compliance signals arrive in Intune.

### 5. Promote to production

1. Keep the same policy model and expand assignments ring-by-ring.
2. Update this scenario and the schema snapshot when AMAPI adds fields that affect your baseline.

## Validation

- [ ] Schema snapshot is present in the repository and reviewable in pull requests.
- [ ] Intune policies reflect the selected AMAPI fields for the scenario.
- [ ] Pilot devices receive expected app, restriction, and update behavior.
- [ ] Reporting and compliance data is visible for pilot devices.

## Troubleshooting

| Symptom | Likely cause | Resolution |
|---|---|---|
| A field in the baseline has no visible effect in Intune | Feature exists in AMAPI but not exposed in the selected Intune profile type | Implement the nearest supported Intune control and note the gap in this scenario guide. |
| Required app does not install | App not approved in Managed Google Play or assignment mismatch | Approve app in Managed Google Play, sync, and verify group targeting. |
| Update behavior differs from expectation | Conflicting update settings across multiple profiles | Consolidate update settings and revalidate precedence. |

## Rollback

1. Remove or exclude production assignments for the new baseline controls.
2. Keep pilot assignment only until behavior is confirmed.
3. Reapply the previous known-good Android profiles if needed.

## References

- [Google Android Management API: enterprises.policies](https://developers.google.com/android/management/reference/rest/v1/enterprises.policies)
- [Microsoft Learn: Enroll Android Enterprise devices in Intune](https://learn.microsoft.com/en-us/intune/intune-service/enrollment/android-enroll)
- [Microsoft Learn: Android Enterprise device restriction settings in Intune](https://learn.microsoft.com/en-us/intune/intune-service/configuration/device-restrictions-android-enterprise)
