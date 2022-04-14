# Policy 1 

This policy demonstrates how to:

1. Get the system app ID for both [OpenID Connect](https://github.com/yoelhor/public/blob/main/policy1/AppAccessControl_Common.xml#L78) and [SAML](https://github.com/yoelhor/public/blob/main/policy1/AppAccessControl_Common.xml#L91) protocols
2. Map the [system app Id to the app name](https://github.com/yoelhor/public/blob/main/policy1/AppAccessControl_Common.xml#L104)
3. [Concatenate the user’s role](https://github.com/yoelhor/public/blob/main/policy1/AppAccessControl_Common.xml#L131)

To be done:

1. Check if the full app name is in the app list
1. Block the user (if required)

## Note

- Since this policy does not have a real sign, it simulates getting the [user type manually](https://github.com/yoelhor/public/blob/main/policy1/AppAccessControl_Common.xml#L118) which returns the type of the user.
- You need to call the REST API to get the app roles
- Then, check if the user role we created (based on the app name and user type) exists in the apps. For example, you can use the [StringContains](https://docs.microsoft.com/en-us/azure/active-directory-b2c/string-transformations#stringcontains), or [StringCollectionContains](https://docs.microsoft.com/en-us/azure/active-directory-b2c/stringcollection-transformations#stringcollectioncontains) claims transformations.
- If user doesn't have the role, block the user, using a self-asserted technical profile (without the continue button)

## Live demo

- [App 1 (jwt.ms)](https://irisflower.b2clogin.com/irisflower.onmicrosoft.com/B2C_1A_AppAccessControl_OIDC/oauth2/v2.0/authorize?client_id=63ba0d17-c4ba-47fd-89e9-31b3c2734339&nonce=defaultNonce&redirect_uri=https%3A%2F%2Fjwt.ms&scope=openid&response_type=id_token&prompt=login&disable_cache=true)
- [App 2 (jwt.io)](https://irisflower.b2clogin.com/irisflower.onmicrosoft.com/B2C_1A_APPACCESSCONTROL_OIDC/oauth2/v2.0/authorize?client_id=567c4bf3-fdca-404c-8cbe-11f2036aa50a&nonce=defaultNonce&redirect_uri=https%3A%2F%2Fjwt.io&scope=openid&response_type=id_token&prompt=login)
- [App that dosn't have the mapping](https://irisflower.b2clogin.com/irisflower.onmicrosoft.com/oauth2/v2.0/authorize?p=B2C_1A_APPACCESSCONTROL_OIDC&client_id=1301223c-b6f9-4471-8bfc-52f9469c9aad&nonce=defaultNonce&redirect_uri=https%3A%2F%2Fjwt.ms&scope=openid&response_type=id_token&prompt=login). This flow returns an error message since the appName claim is empty. We need to think how to fix it. Maybe having a default value.
- For SAML app, use the [SAML test application](https://samltestapp2.azurewebsites.net/SP) to test this policy. In the SAML test app provide the following information:

    - **Tenant Name**: `irisflower`
    - **B2C Policy**: `B2C_1A_AppAccessControl_SAML`
    - **Issuer**: `https://irisflower.onmicrosoft.com/saml-app1`
