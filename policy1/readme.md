# Policy 1 

This policy demonstrates how to:

1. Get the system app ID for both [OpenID Connect](https://github.com/yoelhor/public/blob/main/policy1/AppAccessControl_Common.xml#L78) and [SAML](https://github.com/yoelhor/public/blob/main/policy1/AppAccessControl_Common.xml#L91) protocols
2. Map the [system app Id to the app name](https://github.com/yoelhor/public/blob/main/policy1/AppAccessControl_Common.xml#L104)
3. [Concatenate the user’s role](https://github.com/yoelhor/public/blob/main/policy1/AppAccessControl_Common.xml#L131)

To be done:

1. Check if the full app name is in the app list
1. Block the user (if required)

Note:

- Since this policy does not have a real sign, it simulates getting the [user type manually](https://github.com/yoelhor/public/blob/main/policy1/AppAccessControl_Common.xml#L118) which returns the type of the user.
- You need to call the REST API to get the app roles
- Then, check if the user role we created (based on the app name and user type) exists in the apps. For example, you can use the [StringContains](https://docs.microsoft.com/en-us/azure/active-directory-b2c/string-transformations#stringcontains), or [StringCollectionContains](https://docs.microsoft.com/en-us/azure/active-directory-b2c/stringcollection-transformations#stringcollectioncontains) claims transformations.
- If user doesn't have the role, block the user, using a self-asserted technical profile (without the continue button)

