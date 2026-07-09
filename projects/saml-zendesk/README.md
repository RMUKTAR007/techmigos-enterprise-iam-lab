# 🔐 Okta + Zendesk SAML 2.0 Integration

## 📌 Project Overview

This project demonstrates how to integrate **Okta (Identity Provider)** with **Zendesk (Service Provider)** using **SAML 2.0 Single Sign-On (SSO)**.

The goal was to centralize authentication, enable secure SSO for Zendesk team members, and gain hands-on experience with enterprise IAM concepts.

---

# Architecture

```text
                    +----------------------+
                    |        Okta          |
                    |  Identity Provider   |
                    +----------+-----------+
                               |
                       SAML 2.0 Assertion
                               |
                               ▼
                    +----------------------+
                    |      Zendesk         |
                    |  Service Provider    |
                    +----------+-----------+
                               |
                               ▼
                      Authenticated User
```

---

# Technologies

- Okta Identity Engine
- Zendesk
- SAML 2.0
- Identity Federation
- Single Sign-On (SSO)

---

# Step 1 - Added Zendesk Application in Okta

Added the Zendesk application from the Okta Integration Network.

📷 **Screenshot**

> 

<img width="703" height="816" alt="image" src="https://github.com/user-attachments/assets/53dfc239-00d5-43ee-8bd3-4ac545f5ba4d" />
<img width="752" height="689" alt="image" src="https://github.com/user-attachments/assets/66f21e76-1340-4900-a90b-422b9f8678c4" />




---

# Step 2 - Configure General Settings

Configured the Zendesk subdomain and application settings.

📷 **Screenshot**

<img width="1913" height="983" alt="image" src="https://github.com/user-attachments/assets/27b1a8e4-de26-4c6e-93aa-8d54f1c60bf3" />

> <img width="732" height="784" alt="image" src="https://github.com/user-attachments/assets/844f5243-e88d-43b5-8099-6a2d412a51ce" />
<img width="717" height="746" alt="image" src="https://github.com/user-attachments/assets/a6810421-3d30-4894-89bb-d228c82a08ad" />



---

# Step 3 - Configure SAML Settings in Okta

Generated:

- SAML SSO URL
- Certificate Fingerprint
- Remote Logout URL

📷 **Screenshot**

> <img width="571" height="748" alt="image" src="https://github.com/user-attachments/assets/7971074f-1c33-41e6-a34b-64392a7dbc93" />
 
<img width="1025" height="601" alt="image" src="https://github.com/user-attachments/assets/24700d50-3794-4e8c-a0cd-d25955e0fb21" />





---

# Step 4 - Create SAML Configuration in Zendesk

Configured:

- Configuration Name
- SAML SSO URL
- SHA256 Certificate Fingerprint
- Remote Logout URL

📷 **Screenshot**

> Insert image here

```
images/04-zendesk-saml-configuration.png
```

---

# Step 5 - Enable Team Member Authentication

Enabled:

- Zendesk Authentication (Backup)
- Okta Single Sign-On

Redirected users to authenticate through Okta.

📷 **Screenshot**


<img width="861" height="133" alt="image" src="https://github.com/user-attachments/assets/07f847ab-37d2-4060-9e76-1dd1c57e3380" />


# Authentication Flow

## IdP-Initiated

```text
User
   │
   ▼
Okta Dashboard
   │
Launch Zendesk
   │
   ▼
Zendesk
```

---

## SP-Initiated

```text
User
   │
   ▼
Zendesk Login Page
   │
Redirect to Okta
   │
Authenticate
   │
   ▼
Zendesk
```

---

# IAM Concepts Learned

## Identity Provider (IdP)

Okta authenticates users and issues SAML assertions.

---

## Service Provider (SP)

Zendesk trusts Okta and grants access after validating the SAML assertion.

---

## ACS URL

The endpoint where Zendesk receives the SAML assertion.

---

## Certificate Fingerprint

Used by Zendesk to verify that the SAML assertion was signed by Okta.

---

## Remote Logout

Logs users out of both Zendesk and Okta.

---

# Challenges Encountered

- Understanding the difference between the Signing Certificate and the SHA256 Certificate Fingerprint.
- Matching the correct SAML values between Okta and Zendesk.
- Activating SAML through Team Member Authentication after creating the configuration.

---

# Skills Demonstrated

- Identity and Access Management (IAM)
- Okta Administration
- Zendesk Administration
- SAML 2.0
- Single Sign-On (SSO)
- Identity Federation
- Authentication Policies
- Certificate-Based Trust
- Enterprise Application Integration

---

# Outcome

Successfully configured and activated a working SAML 2.0 Single Sign-On integration between Okta and Zendesk.

The integration enables Zendesk team members to authenticate through Okta while keeping Zendesk authentication available as a backup during testing.
