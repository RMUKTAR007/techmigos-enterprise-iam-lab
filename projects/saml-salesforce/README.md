# Salesforce SAML 2.0 SSO Integration

## Project Overview

This project demonstrates how to configure Single Sign-On (SSO) between Okta and Salesforce using the SAML 2.0 protocol.

The objective was to allow users to authenticate through Okta and securely access Salesforce without entering their Salesforce credentials.

---

## Environment

| Component | Value |
|----------|---------|
| Identity Provider | Okta |
| Service Provider | Salesforce Developer Edition |
| Protocol | SAML 2.0 |
| Authentication | IdP-Initiated SSO |
| User Assignment | Okta Group |

---

## Skills Demonstrated

- Configure a Custom SAML Application in Okta
- Configure Salesforce as a SAML Service Provider
- Exchange SAML metadata
- Configure Assertion Consumer Service (ACS) URL
- Configure Entity ID (Audience URI)
- Configure NameID format
- Assign users and groups
- Test IdP-Initiated SSO
- Troubleshoot common SAML errors

---

## Configuration Steps

### 1. Created Salesforce Developer Org

- Created a Salesforce Developer account
- Enabled Single Sign-On settings
- Enabled SAML authentication

---

### 2. Created a Custom SAML Application in Okta

Configured:

- Single Sign-On URL (ACS URL)
- Audience URI (Entity ID)
- NameID Format
- Application Username

---

### 3. Configured Salesforce

Configured:

- Login URL
- Entity ID
- Identity Provider Certificate
- Identity Provider Login URL

---

### 4. Assigned Users

Assigned the Salesforce application to an Okta group.

Verified that assigned users could see the Salesforce application on the Okta dashboard.

---

### 5. Tested Single Sign-On

Verified successful login flow:

User → Okta Dashboard → Salesforce

No Salesforce password was required after successful authentication through Okta.

---

## Challenges Encountered

### Federation ID confusion

Initially experienced login failures because the Federation ID and NameID configuration did not match.

Resolved by ensuring Salesforce expected the same identifier sent by Okta.

---

### Username Mapping

Verified that the Salesforce username matched the value sent within the SAML assertion.

---

### Certificate Validation

Imported the Okta signing certificate into Salesforce to establish trust.

---

### Login Testing

Repeated multiple login tests until the SAML assertion was successfully accepted by Salesforce.

---

## Security Concepts Learned

- Identity Provider (IdP)
- Service Provider (SP)
- SAML Assertion
- Assertion Consumer Service (ACS)
- Entity ID
- Audience Restriction
- NameID
- X.509 Signing Certificate
- Digital Signature
- Single Sign-On (SSO)

---

## Screenshots

### Okta SAML Application
<img width="791" height="820" alt="image" src="https://github.com/user-attachments/assets/e970ab6d-4fe8-4051-bfc7-34aeb7f42387" />


---

### Salesforce Single Sign-On Configuration

<img width="878" height="792" alt="image" src="https://github.com/user-attachments/assets/1b26a349-967d-45fc-822d-e3d0d0cb097f" />

<img width="824" height="820" alt="image" src="https://github.com/user-attachments/assets/75895539-db1f-4ebd-96e5-fe74b91a49b6" />

<img width="1069" height="822" alt="image" src="https://github.com/user-attachments/assets/06d10cad-0541-4a3e-af8a-d32314be43e9" />


---

### Application Assignments

<img width="1134" height="643" alt="image" src="https://github.com/user-attachments/assets/541d8cc0-e271-47f4-b9a8-6327efaa49ad" />


---

### Successful Salesforce Login

<img width="1911" height="911" alt="image" src="https://github.com/user-attachments/assets/dd5472ce-e6fa-4f0b-b2fc-1938128e5929" />
<img width="1145" height="711" alt="image" src="https://github.com/user-attachments/assets/2e1aabd1-c897-4c56-8a40-86be29d2c214" />



---

### SAML Settings

<img width="1695" height="524" alt="image" src="https://github.com/user-attachments/assets/33e0dfa1-4b15-4101-b68a-89cebde91c80" />


---

## Outcome

Successfully integrated Salesforce with Okta using SAML 2.0 authentication.

Users authenticated through Okta and gained seamless access to Salesforce using Single Sign-On without entering Salesforce credentials.

This project provided practical experience configuring enterprise SAML integrations, exchanging trust metadata, assigning users through Okta, and troubleshooting common federation issues.
