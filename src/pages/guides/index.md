---
title: Authentication
description: This is the authentication guide for Adobe Firefly API
contributors:
  - https://github.com/fly0102030405
  - https://github.com/BaskarMitrah
---

import "../../styles/main.css";

# Authentication

Server-to-server authentication credentials lets your application’s server generate access tokens and make API calls on behalf of your application. This is sometimes referred to as “two-legged OAuth”.

For your application to generate an access token, an end-user does not need to sign in or provide consent to your application. Instead, your application can use its credentials (client id and secrets) to authenticate itself and generate access tokens. Your application can then use the generated access token to call Adobe APIs and services on its behalf.

## Access tokens

Each access token is valid for 24 hours. To adhere with OAuth best practices, you should generate a new token every 23 hours. Generating access tokens can be accomplished programmatically by sending a `POST` request to the following endpoint:

```bash
curl -X POST 'https://ims-na1.adobelogin.com/ims/token/v3' \
-H 'Content-Type: application/x-www-form-urlencoded' \
-d 'grant_type=client_credentials&client_id={client_id}&client_secret={client_secret}&scope=openid,AdobeID,firefly_enterprise'
```

The required parameters are:

* `client_id`: Client ID
* `client_secret`: Client secret
* `scope`: `openid`, `AdobeID`, `firefly_enterprise`

Automate your token generation by calling the IMS endpoint above using standard OAuth2 libraries. Using industry-standard libraries is the quickest and most secure way of integrating with OAuth. We recommend developers diligently pick the OAuth 2.0 library that works best for their application. Your teams' projects are likely leveraging OAuth libraries already to connect with other APIs. Use these libraries to automatically generate tokens when they expire.

The token endpoint also returns an expiry date and the token itself (when decoded) contains the expiry time.
