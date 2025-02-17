---
title: The authentication guide
description: This is the authentication guide for Adobe Firefly's ADLS API.
contributors:
  - https://github.com/fly0102030405
  - https://github.com/BaskarMitrah
---

import "../../styles/main.css";

# Authentication

Server-to-server authentication credentials let your application's server generate access tokens and make API calls on behalf of your application. This is sometimes referred to as [two-legged OAuth](https://www.ibm.com/docs/en/datapower-gateway/10.5.x?topic=flows-two-legged-oauth-flow).

## Access tokens

Each access token is valid for 24 hours. To adhere to OAuth best practices, you should generate a new token every 23 hours.

Access tokens can be generated programmatically by sending a `POST` request to the following endpoint:

// verify scopes
```bash
curl -X POST 'https://ims-na1.adobelogin.com/ims/token/v3' \
-H 'Content-Type: application/x-www-form-urlencoded' \
-d 'grant_type=client_credentials&client_id={client_id}&client_secret={client_secret}&scope=openid,AdobeID,firefly_enterprise'
```

The required parameters are:

* `client_id`: The client ID.
* `client_secret`: The client secret.
* `scope`: The scopes are `openid`, `AdobeID`, `firefly_enterprise`.

The token endpoint also returns an expiry date and the token itself (when decoded) contains the expiry time.

### Automate tokens

Automate your token generation by calling the IMS endpoint using standard OAuth2 libraries. Using industry-standard libraries is the quickest and most secure way of integrating with OAuth.

We recommend that developers be diligent when picking the OAuth 2.0 library that works best for their application. Your teams' projects are likely leveraging OAuth libraries already to connect with other APIs. Use these libraries to automatically generate tokens when they expire.
