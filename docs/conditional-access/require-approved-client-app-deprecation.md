# Require Approved Client App — Deprecation & Migration Guide

**Audience:** Administrator
**Platform:** iOS & Android
**Intune workload:** Conditional Access
**Last reviewed:** See file history
**Status:** Deprecation notice

---

## Migration: "Require approved client app" → "Require app protection policy"

### Background

The retirement date has been extended from the originally announced March 2026 to **June 30, 2026**. After that date, Microsoft will stop enforcing the "Require approved client app" grant control — it will be as if the grant isn't selected at all.

The "Require app protection policy" control has all the same capabilities, plus it verifies the corresponding Intune policy, is applied before a user is granted access, and has improved security features such as verifying that an application policy is actually applied.

---

### Step 1 — Inventory your existing CA policies

Before touching anything, export and document the current state.

- In **Entra admin center → Conditional Access → Policies**, filter for policies that use the **"Require approved client app"** grant (alone or combined).
- Note for each policy: scope (users/groups), target resources (specific apps vs. All cloud apps), platform conditions, and whether it uses "require one of" or "require all".
- Export the full CA policy set via **Graph API or the Entra portal JSON export** for rollback reference.

> **Watch out:** Policies that use *only* "Require approved client app" are the critical ones — those will silently stop working after June 30. Policies already combining both grants are safer but should still be cleaned up.

---

### Step 2 — Audit your App Protection Policies (APP) in Intune

Not all applications that are supported as approved applications support app protection policies. For a list of common client apps, see the App protection policy requirement documentation. If your application isn't listed, contact the application developer.

- Verify you have APPs deployed for **iOS/iPadOS** and **Android** covering all apps targeted by your CA policies (Outlook, Teams, OneDrive, Edge, etc.).
- Confirm the apps are assigned to the same user groups that are in scope of the CA policies.
- Note that Kaizala, Skype for Business, and Visio don't support the "Require app protection policy" grant — if you require these apps to work, you have a specific exception problem to solve.

---

### Step 3 — Verify broker app prerequisites

To apply the "Require app protection policy" grant control, the device must be registered in Microsoft Entra ID, which requires using a broker app. The broker app can be Microsoft Authenticator for iOS, or either Microsoft Authenticator or Microsoft Company Portal for Android devices.

- Confirm Authenticator / Company Portal is deployed (or available) to your user population — especially relevant for unmanaged/BYOD devices.
- For managed devices, push the broker app via Intune if not already present.

---

### Step 4 — Switch existing policies to the dual-grant (transitional)

For existing CA policies, go to **Entra ID → Conditional Access → Policies**, select a policy that uses the approved client app grant, go to **Access controls → Grant**, select both "Require approved client app" **and** "Require app protection policy", and set the combination to **"Require one of the selected controls"**. Repeat for all affected policies.

This is the **safe transitional step** — "Require one of" means either condition satisfies the policy, so apps not yet covered by APP won't immediately break.

> Do this in **Report-only mode first** (see Step 5) before enabling.

---

### Step 5 — Validate using Report-only mode and Sign-in logs

- Before enforcing, set the updated policies to **Report-only**.
- Monitor **Entra ID → Sign-in logs** and **CA Insights workbook** for failures — look for sign-ins that would be blocked by the new grant.
- Pay particular attention to: unmanaged devices, legacy apps, third-party apps, and any app not in your APP scope.
- Validate across iOS and Android, both enrolled and unenrolled devices.

---

### Step 6 — Enable the updated policies

Once sign-in log analysis shows no unexpected failures:

- Switch policies from Report-only to **On** one by one (or in a pilot group first).
- Monitor for user-reported issues in the first 24–48h per policy activation.

---

### Step 7 — Final cleanup: move to "Require app protection policy" only

For any new CA policy, only apply the "Require app protection policy" grant. After June 30, 2026, the "Require approved client app" grant will stop being enforced.

Once you're confident everything is covered by APP:
- Edit existing policies to **remove** "Require approved client app" — leave only "Require app protection policy".
- This is also a good time to consolidate any overlapping policies.

---

### Key risks and considerations

| Risk | Mitigation |
|---|---|
| App not in APP scope when CA enforces | Complete Step 2 thoroughly before Step 4 |
| BYOD users without broker app | Communicate/deploy Authenticator before enforcement |
| Visio / Skype for Business / Kaizala | Exclude these apps from APP-only policy or create a separate exception policy |
| Silent failure after June 30 if not migrated | Calendar reminder before June 30; policy review in Step 1 |
| WebViews outside Edge | WebViews hosted outside of Microsoft Edge don't satisfy the approved client app policy — test any internal app that loads SharePoint or other M365 in a webview |

---

**Supporting official docs**

| Topic | Link |
|---|---|
| Grant controls reference (approved app + APP explained) | [concept-conditional-access-grant](https://learn.microsoft.com/en-us/entra/identity/conditional-access/concept-conditional-access-grant) |
| App protection policy requirement (supported app list) | [same page, #require-app-protection-policy anchor](https://learn.microsoft.com/en-us/entra/identity/conditional-access/concept-conditional-access-grant#require-app-protection-policy) |
| Create app protection policies in Intune | [app-protection-policies](https://learn.microsoft.com/en-us/intune/intune-service/apps/app-protection-policies) |
| APP overview (what it does, platforms) | [app-protection-policy](https://learn.microsoft.com/en-us/mem/intune/apps/app-protection-policy) |
| Report-only mode for CA validation | [concept-conditional-access-report-only](https://learn.microsoft.com/en-us/entra/identity/conditional-access/concept-conditional-access-report-only) |
| Require approved app or APP — full policy walkthrough | [policy-all-users-approved-app-or-app-protection](https://learn.microsoft.com/en-us/entra/identity/conditional-access/policy-all-users-approved-app-or-app-protection) |
