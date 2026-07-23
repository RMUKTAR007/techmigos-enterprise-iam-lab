# 🔐 Salesforce SAML 2.0 SSO Integration

This project sets up Single Sign-On between Okta and Salesforce using SAML 2.0 — the goal being that users log in once through Okta and land in Salesforce without ever typing a Salesforce password.

## Environment

| Component | Value |
|-----------|-------|
| Identity Provider | Okta |
| Service Provider | Salesforce Developer Edition |
| Protocol | SAML 2.0 |
| Authentication | IdP-Initiated SSO |
| User Assignment | Okta Group |

## What I did

### 1. Set up the Salesforce side first

Created a Salesforce Developer org and enabled Single Sign-On settings along with SAML authentication, since Salesforce needs to be ready to accept SAML assertions before Okta can be pointed at it.

### 2. Built a custom SAML app in Okta

Configured the core SAML fields: the Single Sign-On URL (ACS URL), Audience URI (Entity ID), NameID format, and the application username format Okta would send over.

### 3. Fed that config back into Salesforce

Took the values Okta generated and configured them on the Salesforce side — Login URL, Entity ID, Identity Provider Certificate, and Identity Provider Login URL. This is really the "handshake" step: both sides need to agree on the same identifiers or the trust relationship never establishes.

### 4. Assigned users

Assigned the Salesforce app to an Okta group and confirmed assigned users could see it show up on their Okta dashboard.

![Application Assignment](./screenshots/app-assignment.png)

### 5. Tested the login flow

Ran through the full flow: user logs into Okta → clicks Salesforce tile → lands in Salesforce, fully authenticated, no Salesforce password prompt.

![Successful Salesforce Login](./screenshots/successful-login-1.png)
![Successful Salesforce Login Confirmation](./screenshots/successful-login-2.png)

## Where it actually broke (and how I fixed it)

This integration didn't work on the first try, which honestly taught me more than if it had.

**Federation ID mismatch** — my first few login attempts failed outright. Turned out the Federation ID Salesforce expected didn't match the NameID Okta was actually sending in the assertion. Once I aligned both sides to use the same identifier, logins started going through.

**Username mapping** — related issue: I had to double-check that the Salesforce username field matched exactly what was coming through in the SAML assertion, since a mismatch there silently breaks the login even if the certificate and URLs are all correct.

**Certificate trust** — had to import Okta's signing certificate into Salesforce manually so Salesforce would actually trust assertions coming from Okta rather than rejecting them outright.

It took a handful of repeated login attempts, tweaking one variable at a time, before the assertion was fully accepted — which is probably closer to how this goes in a real environment than a one-shot clean setup would be.

## Screenshots

![Okta SAML Application](./screenshots/okta-saml-app.png)
*Custom SAML application configured in Okta*

![Salesforce SSO Configuration](./screenshots/salesforce-sso-config-1.png)
![Salesforce SSO Configuration](./screenshots/salesforce-sso-config-2.png)
![Salesforce SSO Configuration](./screenshots/salesforce-sso-config-3.png)
*Salesforce Single Sign-On settings*

![SAML Settings](./screenshots/saml-settings-1.png)
![SAML Settings](./screenshots/saml-settings-2.png)
![SAML Settings](./screenshots/saml-settings-3.png)
![SAML Settings](./screenshots/saml-settings-4.png)
*Detailed SAML configuration values*

## Concepts covered

Identity Provider (IdP), Service Provider (SP), SAML assertion, Assertion Consumer Service (ACS), Entity ID, Audience Restriction, NameID, X.509 signing certificates, digital signatures, and Single Sign-On.

## Skills demonstrated

Configuring a custom SAML app in Okta, configuring a service provider (Salesforce) to trust that app, exchanging SAML metadata between IdP and SP, assigning users/groups to the app, and troubleshooting real federation errors rather than just following a clean happy-path tutorial.

## Outcome

Salesforce and Okta are now fully federated over SAML 2.0 — users authenticate once through Okta and get into Salesforce with zero additional credentials. The debugging process (Federation ID mismatch, username mapping, certificate trust) ended up being the most valuable part of this project, since that's the stuff that actually goes wrong in production SAML setups, not just the initial configuration screens.
