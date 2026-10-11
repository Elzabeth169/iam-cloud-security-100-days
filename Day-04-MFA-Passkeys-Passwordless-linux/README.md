# Day 4 — MFA, Passkeys & Passwordless Authentication

## Objective

Understand how modern authentication strengthens security beyond traditional passwords.

## Topics Covered

- Multi-Factor Authentication (MFA)
- Authentication factors
- 2FA vs MFA
- Passwordless authentication
- Passkeys
- Public-key cryptography
- Passkey registration and authentication
- Phishing resistance
- Biometrics vs passkeys
- Passwordless authentication in enterprise IAM

---

## 1. Multi-Factor Authentication (MFA)

MFA requires two or more different authentication factors.

### Three Authentication Factors

1. **Something you know**
   - Password
   - PIN

2. **Something you have**
   - Phone
   - Authenticator app
   - Security key
   - OTP token

3. **Something you are**
   - Fingerprint
   - Face recognition
   - Iris scan

Example:

```text
Username + Password
        ↓
Authenticator App Approval
        ↓
Authenticated

Password = Something you know
Authenticator/device = Something you have

2. MFA vs 2FA
2FA requires exactly two authentication factors.
MFA requires two or more authentication factors.
Therefore:
2FA ⊂ MFA

Every 2FA implementation is MFA, but MFA can use more than two factors.


3. Passwordless Authentication
Passwordless authentication allows a user to authenticate without using a traditional password.
Examples include:
- Passkeys
- Security keys
- Device-based credentials
- Biometrics used to unlock an authentication credential
Basic flow:
User
 ↓
Device / Authenticator
 ↓
Cryptographic Authentication
 ↓
Identity Provider
 ↓
Authenticated

Passwordless authentication removes the traditional password from the authentication process.


4. Passkeys
A passkey is a passwordless credential based on public-key cryptography.
During registration, the authenticator generates:
Private Key → Protected on the device/authenticator
Public Key  → Registered with the service

The private key is used to create cryptographic signatures.
The public key is used by the service to verify those signatures.


5. Passkey Registration
User
 ↓
Create Passkey
 ↓
Authenticator
 ↓
Generates Key Pair
 ├── Private Key → Protected locally
 └── Public Key → Registered with service

The private key is not sent to the website.


6. Passkey Authentication
During login:
User
 ↓
"Sign in with passkey"
 ↓
Service generates challenge
 ↓
Authenticator receives challenge
 ↓
User verification
(Fingerprint / Face / PIN)
 ↓
Private key signs challenge
 ↓
Cryptographic signature
 ↓
Service verifies signature
using public key
 ↓
Authentication successful

Challenge-Response Concept
Challenge + Private Key
        ↓
Cryptographic Signature
        ↓
Server verifies using Public Key

7. Where Is the Private Key?
The private key is protected by the user's authenticator, such as the device's secure environment or a hardware security key.
The private key is designed not to be exposed to the website or transmitted to the server during normal authentication.
The service stores the public key.


8. Why Passkeys Are Phishing-Resistant
Traditional password authentication:
User
 ↓
Enters Password
 ↓
Phishing Website
 ↓
Attacker obtains Password

Passkeys work differently.
They are associated with the legitimate website's origin.
Legitimate Website
 ↓
Correct Origin
 ↓
Passkey Authentication

A phishing website has a different origin and cannot simply collect the user's passkey like a password.
Therefore, passkeys provide strong resistance against traditional credential-phishing attacks.


9. Biometrics vs Passkeys
Biometrics and passkeys are not the same thing.
A fingerprint or face scan can be used to verify the user locally and unlock/authorize use of a passkey.
Conceptually:
Passkey
   ↓
Cryptographic Credential
   ↓
Private Key
   ↓
Protected by Authenticator
   ↓
Fingerprint / PIN
   ↓
Unlocks or authorizes use

The biometric is the user-verification mechanism.
The passkey is the cryptographic credential.


10. MFA vs Passwordless
Method	        Password Required?	    Example
Password	    Yes	                    Username + Password
Password + OTP	Yes	                    Password + Authenticator OTP
Authenticator   Approval	            Usually	Push notification
Security Key	No/Can be passwordless	Hardware security key
Passkey	        No	                    Device-based passkey


Passwordless authentication does not simply mean replacing a password with a fingerprint.


11. Authentication vs Authorization
Successful authentication does not automatically give access to every resource.
User
 ↓
Authentication
 ↓
Identity Confirmed
 ↓
Authorization
 ↓
Permission Check
 ↓
ALLOW / DENY

Example:
Authentication → SUCCESS
Authorization  → DENIED

A user can successfully authenticate using a passkey but still receive Access Denied or 403 Forbidden if their permissions do not allow the requested action.


12. Why Passwordless Authentication Matters in Enterprise IAM
Passwords can be:
- Phished
- Stolen
- Reused
- Leaked
- Brute-forced
Passwordless authentication can provide:
- Stronger authentication
- Phishing resistance
- Reduced credential theft
- Better user experience
- Reduced password-reset overhead
- Better alignment with Zero Trust security
For enterprise IAM, passwordless authentication helps organizations reduce their dependence on passwords while strengthening identity security.

Key Takeaways
- MFA uses multiple authentication factors.
- 2FA is a type of MFA using exactly two factors.
- Passwordless authentication removes the need for traditional passwords.
- Passkeys use public-key cryptography.
- The private key remains protected by the authenticator.
- The public key is registered with the service.
- Passkeys use challenge-response authentication.
- Passkeys are strongly resistant to phishing because authentication is tied to the legitimate origin.
- Biometrics can unlock or authorize use of a passkey but are not the passkey itself.
- Authentication confirms identity; authorization determines access.
