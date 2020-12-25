# WordPress Proxy Auth Plugin
## Introduction
The WordPress Proxy Auth plugin helps developers/DevOps/admins easily implement authentication and authorization for WordPress by using the HTTP header fields provided by a reverse proxy.

This could be employed to achieve SSO (OAUTH/OIDC and SAML) to a Cloud Identity Provider (e.g., Azure Active Directory, Okta, Auth0) by using an Identity-Aware Proxy, e.g., [Datawiza Access Broker](https://www.datawiza.com/access-broker) and [Google IAP](https://cloud.google.com/iap).

Note that the plugin requires a reverse proxy sitting in front of the WordPress site. The reverse proxy performs authentication, and passes the user name and role to the plugin via HTTP headers.

## How it works

* The plugin retrieves the user id (email) from the HTTP header and then checks if such a user exists. If not, the plugin creates a new user by using this email and signs him/her in.
* The plugin retrieves the user role from the HTTP header and sets it as the user\'s role in WordPress.
* The HTTP headers for user id and role are HTTP_X_USER and HTTP_ROLE, respectively.

**!!! NOTES !!!**

* **MAKE SURE that clients cannot bypass the reverse proxy. This is to prevent people from sending forged malicious requests with arbitrary headers directly to WordPress.**
* **MAKE SURE that the reverse proxy in front of the WordPress site erases the headers passing user id and role: HTTP_X_USER and HTTP_ROLE. This prevents malicious clients from sending forged malicious requests by setting the headers with arbitrary value (e.g., setting HTTP_ROLE to Administrator), which would compromise the security.**

