# 🏢 Okta Organization Setup

## Overview

This project documents the initial setup and configuration of the **TechMigos Enterprise** Okta Identity Engine (OIE) tenant.

The objective was to create a clean enterprise IAM environment that would later support user lifecycle management, authentication policies, SAML integrations, and identity governance.

---

## Objectives

- Create an Okta Identity Engine organization
- Configure the administrator account
- Customize the organization branding
- Explore the Okta Admin Console
- Design a realistic group structure for access governance
- Prepare the tenant for enterprise IAM deployments

---

## Environment

| Component | Value |
|-----------|-------|
| Platform | Okta Identity Engine |
| Organization | TechMigos Enterprise |
| Environment | Developer Tenant |
| Administrator | Super Admin |

---

## Step 1 — Creating the Organization

The project began by creating a new Okta Identity Engine tenant.

Tasks completed:
- Registered a new Okta developer organization
- Verified the administrator email
- Activated the tenant
- Signed in to the Okta Admin Console

📷 Screenshot
_Added image here_
<img width="1341" height="778" alt="image" src="https://github.com/user-attachments/assets/1b6ed98b-94f1-4323-b663-6524a164f32f" />


---

## Step 2 — First Login

After activating the organization, I logged into the Admin Console for the first time to get oriented before making any configuration changes.

📷 Screenshot
_Added image here_
<img width="1540" height="885" alt="image" src="https://github.com/user-attachments/assets/8a3844c8-bfd2-4c2f-9acc-32e0403f70c5" />


---

## Step 3 — Enterprise Branding

To simulate a real-world organization, I customized the tenant branding.

Changes included:
- Organization Name
- Company Logo
- Dashboard Branding

The organization was branded as **TechMigos Enterprise**.

📷 Screenshot
_Added image here_
<img width="1298" height="879" alt="image" src="https://github.com/user-attachments/assets/7f2a2c52-ecba-46ab-909f-53fe56754e6b" />


---

## Step 4 — Uploading the Company Logo

A custom company logo was designed and uploaded to represent the TechMigos Enterprise environment. This gives the tenant a professional appearance similar to a production deployment.

📷 Screenshot
_Added image here_

<img width="621" height="654" alt="image" src="https://github.com/user-attachments/assets/bef0292f-aa16-4e13-84c3-38c087a25b08" />

<img width="619" height="680" alt="image" src="https://github.com/user-attachments/assets/96ec52cf-e0b8-4bec-9a4d-d8647471f171" />
<img width="602" height="637" alt="image" src="https://github.com/user-attachments/assets/b8479f50-e7d3-461e-8a5e-0a372479e768" />




---

## Step 5 — Exploring the Admin Console

With branding in place, I reviewed each major administrative section to understand what it governs before touching configuration elsewhere in the lab:

- **Dashboard** — org health, active users, system status at a glance
- **Directory** — People, Groups, Devices, Profile Editor, Directory Integrations, Profile Sources
- **Applications** — where SSO integrations (Salesforce, Zendesk, Slack) would later be configured
- **Security** — authentication policies, MFA enrollment, network zones
- **Workflow** — automation and lifecycle event triggers
- **Reports** — usage and access reporting
- **System Log** — audit trail for every identity event in the org

📷 Screenshot
_Added image here_

<img width="733" height="519" alt="image" src="https://github.com/user-attachments/assets/ec7b4eab-4bf9-496c-acf8-fa215eb99ed6" />


---

## Step 6 — Designing the Group Structure

To simulate real enterprise access governance, I built a group structure spanning department, function, and administrative tiers rather than relying on a single flat group list.

**Groups created:**
- **Department-based:** TechMigos Finance Group, TechMigos Marketing Group, TechMigos HR Group, TechMigos IT Group
- **Function-based:** TechMigos Help Support, TechMigos Cloud Professionals, TechMigos CyberOps
- **Administrative tiers:** TechMigos Administrators, TechMigos Okta Admins, Okta Administrators
- **Location-based:** New York Office
- **Default:** Everyone (all org users)

📷 Screenshot
_Added image here_
<img width="917" height="790" alt="image" src="https://github.com/user-attachments/assets/c0106f71-37cf-4e30-bc18-717719dbbaf0" />


---

## Design Decisions

**Why three separate admin groups instead of one?**

Rather than granting broad admin access through a single group, I split administrative access into three tiers:
- **Okta Administrators** — the built-in, Okta-managed group reserved for top-level org administrators
- **TechMigos Okta Admins** — day-to-day Okta configuration access (apps, policies, groups)
- **TechMigos Administrators** — broader organizational admin role, separate from Okta-specific permissions

This reflects a real-world **separation of duties** principle: not everyone who needs administrative visibility should have the same level of platform access. It reduces blast radius if any single account is compromised and creates a clearer audit trail of who can do what.

**Why separate department, function, and location groups?**

Department groups (Finance, HR, Marketing, IT) map naturally to org structure, but function-based groups (Help Support, CyberOps, Cloud Professionals) capture cross-department roles that don't fit a department model — someone on the Help Support team might sit in any department. Keeping these as separate group types makes downstream SAML/attribute-based access rules far easier to write than trying to force everything into one hierarchy.

---

## Skills Demonstrated

- Okta Identity Engine (OIE) tenant deployment
- Enterprise organization branding
- Admin Console navigation and structure
- Group design for department, function, and administrative access
- Separation-of-duties principles applied to admin roles
- Identity infrastructure planning

---

## What I'd Do Differently at Enterprise Scale

- Use **group rules** (dynamic, attribute-based membership) instead of manually assigning users to groups, so group membership updates automatically as HR attributes change
- Integrate with a real HR system (e.g., Workday) as the source of truth rather than manually created test users
- Apply **naming conventions and group descriptions as a governance standard** from day one, rather than cleaning them up after the fact
- Document a formal **RBAC matrix** mapping each group to the specific permissions/applications it grants, before creating any groups

---

## Outcome

The TechMigos Enterprise Okta tenant was successfully deployed, branded, and structured with a realistic group hierarchy. This organization now serves as the foundation for every other project in this repository:

- User Lifecycle Management
- Profile Editor & Attribute Mapping
- SAML Single Sign-On (Salesforce, Zendesk)
- Security Policies
- MFA and Network Zones
- Authentication Policies

Setting up an Okta organization is the first step in building an enterprise IAM environment — the decisions made here about branding, admin separation, and group design directly shape how every downstream policy and integration gets applied.
