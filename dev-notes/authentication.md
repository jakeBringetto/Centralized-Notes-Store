---
description: frontend + backend authentication tutorial
---

# Authentication

### Overview

[https://zivukushingai.medium.com/everything-you-need-to-know-about-frontend-and-backend-authentication-ultimate-guide-7142a752249c](https://zivukushingai.medium.com/everything-you-need-to-know-about-frontend-and-backend-authentication-ultimate-guide-7142a752249c)

* Identification: verifying a person's identity
* Techniques:
  * ID card
  * Username + password
  * Mobile OTP
  * Biometrics
* Authorization: process of granting users or services the right to access certain resources or perform certain actions
* Authorization mechanisms:
  * Sessions
  * Cookies
  * Authorization tokens
* Authentication: process of verifying the identity of an entity and confirming the authenticity of the rights claimed by that entity
* Access control: process of defining a list of permissible operations and determining whether an operation is allowed or prohibited

<figure><img src="../.gitbook/assets/image (1).png" alt=""><figcaption></figcaption></figure>

### Frontend authentication methods

* HTTP Basic Auth
  * Allows the client to authenticate using username and password in HHTP request to the server, which does identity verification
  * Cons: insecure, unable to actively log out
* Session Cookie Authentication
