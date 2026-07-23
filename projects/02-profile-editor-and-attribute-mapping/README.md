# 📝 Profile Editor & Attribute Mapping

## Overview

This project demonstrates how Okta's **Profile Editor** and **Attribute Mapping** are used to manage user attributes and synchronize identity information between Okta and connected applications.

It builds directly on the [Okta Organization Setup](../01-okta-organization-setup) project, using that tenant as the foundation for attribute governance.

---

## Project Goal

Configure and validate attribute mappings to ensure accurate identity data is shared across enterprise applications while maintaining a single source of truth.

---

## Environment

| Component | Value |
|-----------|-------|
| Platform | Okta Identity Engine |
| Organization | TechMigos Enterprise |
| Source Profile | Okta User Profile |
| Connected Apps | Salesforce.com, Zendesk |

---

## Step 1 — Reviewing the Okta User Profile

Before making changes, I reviewed the default Okta User Profile to understand which attributes exist out of the box (name, email, login, etc.) and which would need to be added for enterprise use cases.

[<img width="915" height="734" alt="image" src="https://github.com/user-attachments/assets/feb18a13-1c1b-4c1b-935b-7f295561fb32" />
]

---

## Step 2 — Exploring the Profile Editor

I opened the Profile Editor under Directory to see how Okta separates the **Okta User Profile** (source of truth) from **Application User Profiles** (per-app attribute sets).

[<img width="773" height="792" alt="image" src="https://github.com/user-attachments/assets/188faa07-d28c-450d-9ac0-a2d8ec310566" />
]

---

## Step 3 — Creating Custom Attributes

Standard attributes don't cover every enterprise need, so I added custom attributes to the Okta User Profile to support downstream use cases.

[<img width="805" height="556" alt="image" src="https://github.com/user-attachments/assets/4adc2169-c323-4229-822b-3d2d21f360a2" />
]

---

## Step 4 — Mapping Okta Attributes to Applications

I configured bidirectional attribute mappings for both Salesforce and Zendesk, defining how identity data flows in each direction.

### Okta → Salesforce (Outbound)

| Okta Attribute | Salesforce Attribute | Mapping Type |
|----------------|----------------------|--------------|
| `user.firstName` | `firstName` | Push (always applied) |
| `user.lastName` | `lastName` | Push (always applied) |
| `user.email` | `email` | Push (always applied) |

[<img width="731" height="494" alt="image" src="https://github.com/user-attachments/assets/5696ee7e-ccab-4717-869f-0968629bdbcc" />
]

### Salesforce → Okta (Inbound)

| Salesforce Attribute | Okta Attribute | Mapping Type |
|----------------------|-----------------|--------------|
| `appuser.firstName` | `firstName` | Apply on user creation only |
| `appuser.lastName` | `lastName` | Apply on user creation only |
| `appuser.email` | `email` | Apply on user creation only |

[<img width="703" height="552" alt="image" src="https://github.com/user-attachments/assets/36ed1c08-1535-4dc6-a111-7676b6163f2e" />
]

### Zendesk → Okta (Inbound)

| Zendesk Attribute | Okta Attribute | Mapping Type |
|--------------------|-----------------|--------------|
| `appuser.userName` | `login` | Uses default Okta username setting |
| `appuser.firstName` | `firstName` | Apply on user creation only |
| `appuser.lastName` | `lastName` | Apply on user creation only |
| `appuser.email` | `email` | Apply on user creation only |

[PASTE IMAGE HERE]

### Okta → Zendesk (Outbound)

| Okta Attribute | Zendesk Attribute | Mapping Type |
|-----------------|---------------------|--------------|
| `user.firstName` | `firstName` | Apply on user creation only |
| `user.lastName` | `lastName` | Apply on user creation only |
| — | `userName` | Set by Zendesk |

[PASTE IMAGE HERE]

**Note on Mapping Types:**
Okta distinguishes between two mapping behaviors:
- **Push (green arrow)** — the attribute is continuously synced; any change in the source updates the target every time
- **Apply on creation (yellow key)** — the attribute is only set once, when the user account is first created, and won't overwrite existing values afterward

I used push mappings for Okta → Salesforce to keep Salesforce continuously current with Okta as the source of truth, while inbound mappings from both apps use creation-only behavior to avoid Okta's profile being overwritten by app-side edits after the initial sync.

---

## Step 5 — Validating Inbound and Outbound Mappings

I tested the configured mappings to confirm attribute values flowed correctly in both directions, checking for:
- Correct data type matching
- No attribute value loss during transformation
- Consistent formatting across applications

[PASTE IMAGE HERE]

---

## Step 6 — Testing Profile Synchronization

To confirm the mappings worked end-to-end, I updated a user's attribute in Okta and verified the change synchronized correctly to the connected application's profile.

[PASTE IMAGE HERE]

---

## Design Decisions

**Why maintain Okta as the single source of truth?**

Rather than letting each application manage its own copy of user attributes independently, all identity data flows from the Okta User Profile outward. This avoids the classic enterprise problem of conflicting user data across systems — if HR data changes, it updates once in Okta and propagates everywhere, instead of requiring manual updates in every connected app.

**Why use push mappings outbound but creation-only mappings inbound?**

Push mappings to Salesforce keep the app continuously in sync with Okta as changes happen. Inbound mappings from Salesforce and Zendesk are set to apply only on user creation, so that app-side edits after initial provisioning don't unintentionally overwrite the Okta profile — preserving Okta's role as the authoritative source.

**Why use Okta Expression Language (OEL) instead of direct 1:1 mapping in some cases?**

Some attributes needed transformation rather than a straight copy — for example, combining first and last name into a display name, or formatting a field differently for a specific app's requirements. OEL let me handle these transformations at the mapping layer rather than storing duplicate or reformatted data in the base profile.

---

## Concepts Covered

- Universal Directory
- Okta User Profile
- Application User Profile
- Custom Attributes
- Attribute Mapping (push vs. apply-on-creation)
- Profile Editor
- Source of Truth
- Data Transformation
- Okta Expression Language (OEL)

---

## Skills Demonstrated

- Universal Directory Administration
- Profile Editor Configuration
- Bidirectional Attribute Mapping
- Identity Synchronization
- Okta Expression Language (OEL)
- Enterprise Identity Management

---

## What I'd Do Differently at Enterprise Scale

- Document a formal **attribute dictionary** before creating custom attributes, so naming stays consistent as more applications are added
- Use **group-based attribute push policies** rather than mapping every attribute to every app by default
- Build automated validation tests for mapping changes, rather than manually checking each sync
- Standardize on push vs. creation-only mapping rules across all apps from the start, documented as a policy rather than decided per-integration

---

## Outcome

Successfully configured and validated bidirectional profile attribute mappings within Okta Identity Engine for both Salesforce and Zendesk, ensuring consistent identity data across connected applications while following enterprise IAM best practices.

This attribute foundation now supports every downstream application integration in this repository, including SAML federation to Salesforce and Zendesk.
