

## 描述

> The authorization code grant is used when an application exchanges an authorization code for an access token. After the user returns to the application via the redirect URL, the application will get the authorization code from the URL and use it to request an access token. This request will be made to the token endpoint.


[[@OAuthGrantTypes]]
> ## Authorization Code Grant Type

> The authorization code grant type is the most commonly used grant type. This grant type is for server-side apps.

> ### Authorization Code Grant Type Roles

> The Authorization Code grant type uses the following roles:

> -   **Resource Owner**: A person or system capable of granting access to a protected resource.
> -   **Application**: A client that makes protected requests using the authorization of the resource owner.
> -   **Authorization Server**: The Single Sign‑On server that issues access tokens to client apps after successfully authenticating the resource owner.
> -   **Resource Server**: The server that hosts protected resources and accepts and responds to protected resource requests using access tokens. Apps access the server through APIs.

> ### Authorization Code Grant Type Flow

> The following diagram shows the flow for the Authorization Code grant type:
[![Diagram of the authorization code grant type flow described in detail in the list below.](https://docs.vmware.com/en/Single-Sign-On-for-VMware-Tanzu-Application-Service/1.14/sso/Images/images-oauth_auth_code.png)](https://docs.vmware.com/en/Single-Sign-On-for-VMware-Tanzu-Application-Service/1.14/sso/Images/images-oauth_auth_code.png)

> The flow of the Authorization Code grant type is:

> 1.  **Access Application**: The user accesses the app and triggers authentication and authorization.
> 2.  **Authentication and Request Authorization**: The app redirects the user to the authorization server where it prompts the user for their username and password. The first time the user goes through this flow for the app, the user sees an approval page. On this page, the user can choose permissions to authorize the app to access resources on their behalf.
> 3.  **Authentication and Grant Authorization**: The authorization server receives the authentication and authorization grant.
> 4.  **Send Authorization Code**: After the user authorizes the app, the authorization server sends an authorization code to the app using a redirect.
> 5.  **Request Code Exchange for Token**: The app uses the authorization code to request an access token from the authorization server. This gives the app access to the approved permissions.
> 6.  **Issue Access Token**: The authorization server validates the authorization code and issues an access token.
> 7.  **Request Resource w/ Access Token**: The app attempts to access the resource from the resource server by presenting the access token.
> 8.  **Return Resource**: If the access token is valid, the resource server returns the resources that the user authorized the app to receive.


authorization code grant type 
implicit grant type 
password grant type 
client credential grant type
authentication code => 索要token



## 複習
#🧠 Question :: ->->-> ``
<!--SR:!2023-03-20,3,250-->

---
Status: 
Tags:
Links:
References:
[[@OAuthGrantTypes]]




