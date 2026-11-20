# Migrating from Enterprise SSO to Platform SSO on macOS (Test Guide)

**Audience:** Administrator  
**Platform:** macOS  
**Intune workload:** Devices  
**Last reviewed:** 2026-11-20  
**Status:** Draft

---

## Overview

Use this guide to validate migration from a standalone **Enterprise SSO App Extension** profile to **Platform SSO (PSSO)** on a single test Mac and test user.

Platform SSO includes SSO App Extension capabilities. For testing, keep the existing Enterprise SSO profile in place until Platform SSO is configured, registered, and validated.

## Prerequisites

- The Mac is enrolled in Microsoft Intune.
- The user has a Microsoft Entra ID account.
- Company Portal for macOS is installed and up to date.
- The Mac runs a supported macOS version.
- The existing Enterprise SSO configuration is working.
- You have a test user and test Mac for migration validation.
- Relevant Conditional Access policies are identified for post-migration testing.

Company Portal provides the Microsoft Enterprise SSO plug-in used by Platform SSO.

## Administrator steps

### 1. Review the existing Enterprise SSO configuration

In the Intune admin center, locate the current macOS profile that configures the **Single Sign-On App Extension**.

Record:

- Assignments
- SSO extension settings
- Application configuration
- Allow lists or exclusions
- Custom configuration values

Do not modify or remove this profile yet.

### 2. Choose the Platform SSO authentication method

Select the method you want to test:

| Method | Typical use case |
|---|---|
| Secure Enclave | Passwordless, hardware-bound authentication |
| Password | Entra password-based authentication and local password integration |
| Smart Card | Certificate or smart-card based authentication |

For a new deployment, **Secure Enclave** is usually the preferred test path unless password-based sign-in is required.

### 3. Verify Company Portal on the test Mac

Confirm:

- Company Portal opens successfully
- The device appears correctly in Intune
- The user can sign in to Company Portal
- The device receives Intune configuration profiles

### 4. Create the Platform SSO policy

1. In the Intune admin center, go to **Devices > macOS > Configuration**.
2. Select **Create > New policy**.
3. Configure:
   - **Platform:** macOS
   - **Profile type:** Settings catalog
4. Name the profile, for example:

   ```text
   macOS - Platform SSO - Test
   ```

5. Add settings under **Authentication / Extensible Single Sign On (SSO)**.
6. Configure Platform SSO with the authentication method selected in step 2.
7. Save the policy.

### 5. Assign the Platform SSO policy to the test scope

- Assign only to the test Mac and test user.
- Keep the existing Enterprise SSO profile assigned during testing.

### 6. Synchronize and confirm policy delivery

1. Trigger Intune sync on the Mac (or wait for regular MDM check-in).
2. In Intune, confirm the Platform SSO profile reports as delivered.

Policy delivery alone does not complete Platform SSO registration.

### 7. Register Platform SSO on the Mac

On the test Mac, complete the Platform SSO registration prompt/notification.

High-level flow:

```text
Intune policy -> Platform SSO available -> User registration -> Entra authentication -> Platform SSO registered
```

During registration, the Mac establishes Entra device identity used by the Microsoft Enterprise SSO plug-in.

### 8. Verify Platform SSO status

On supported macOS versions, run:

```bash
app-sso platform -s
```

Confirm the expected registration state and no registration errors.

### 9. Test macOS authentication experience

Validate Platform SSO behavior for:

- Lock/unlock
- Sign-out/sign-in
- Restart and sign-in
- Touch ID (if applicable)
- Chosen authentication method behavior
- Password behavior (if using password authentication)

### 10. Test application and browser SSO

Test representative apps and browsers without re-entering Entra credentials unnecessarily, such as:

- Outlook
- Teams
- Word/Excel
- Company Portal
- Safari
- Supported third-party browsers
- Business apps using Entra authentication

### 11. Test Conditional Access

Validate access to apps protected by Conditional Access and confirm expected outcomes for:

- Compliant device checks
- Managed device checks
- MFA
- Authentication strength
- Device-based access decisions

### 12. Remove the old Enterprise SSO profile assignment

After Platform SSO and app/browser SSO are validated:

1. Unassign the old standalone Enterprise SSO App Extension profile from the test scope.
2. Synchronize the Mac again.

### 13. Perform final validation after removal

Re-test and confirm:

- Platform SSO remains registered
- macOS sign-in works
- Lock/unlock works
- Microsoft 365 app SSO works
- Browser SSO works
- Business app SSO works
- Conditional Access still works
- Restart scenario still works

This confirms authentication is provided by Platform SSO, not the legacy standalone Enterprise SSO profile.

## Validation

- [ ] Platform SSO policy is delivered to the test Mac.
- [ ] Platform SSO registration completes successfully.
- [ ] `app-sso platform -s` reports expected state without errors.
- [ ] macOS sign-in and unlock experience works as expected.
- [ ] Application and browser SSO work without unexpected prompts.
- [ ] Conditional Access behavior remains correct.
- [ ] Legacy standalone Enterprise SSO profile is removed from test scope.
- [ ] Post-removal validation passes after restart.

## Cleanup

1. Remove or exclude test assignments from the Platform SSO policy if the test is complete.
2. Remove any temporary test groups used for this scenario.
3. Keep production assignments unchanged until test results are approved.

## Expected end state

```text
Mac enrolled in Intune
        ↓
Company Portal
        ↓
Microsoft Enterprise SSO plug-in
        ↓
Platform SSO + SSO App Extension
        ↓
Microsoft Entra ID
        ↓
Applications + browsers + macOS authentication
```

The old standalone Enterprise SSO profile is no longer required once Platform SSO migration is validated.

## References

- [Configure Platform SSO for macOS in Intune (Microsoft Learn)](https://learn.microsoft.com/en-us/intune/device-configuration/settings-catalog/configure-platform-sso-macos)
- [Configure Enterprise SSO plug-in on macOS (Microsoft Learn)](https://learn.microsoft.com/en-us/intune/device-configuration/templates/configure-enterprise-sso-plugin-macos)
