## 描述


> ### Implicit Flow

> The following diagram shows the flow for the Implict grant type:

[![Diagram of the Implicit grant type flow described in detail in the list below.](https://docs.vmware.com/en/Single-Sign-On-for-VMware-Tanzu-Application-Service/1.14/sso/Images/images-oauth_implicit.png)](https://docs.vmware.com/en/Single-Sign-On-for-VMware-Tanzu-Application-Service/1.14/sso/Images/images-oauth_implicit.png)

> The flow of the Implicit grant type is:
> 
> 1.  **Access Application**: The user accesses the app and triggers authentication and authorization.
> 2.  **Authentication and Request Authorization**: The app prompts the user for their username and password. The first time the user goes through this flow for the app, the user sees an approval page. On this page, the user can choose permissions to authorize the app to access resources on their behalf.
> 3.  **Authentication and Grant Authorization**: The authorization server receives the authentication and authorization grant.
> 4.  **Issue Access Token**: The authorization server validates the authorization code and returns an access token with the redirect URL.
> 5.  **Request Resource w/ Access Token in**: The app attempts to access the resource from the resource server by presenting the access token in the URL.
> 6.  **Return Resource**: If the access token is valid, the resource server returns the resources that the user authorized the app to receive.


## 複習


---
Status: #🌱 
Tags:
[[OAuth]]
Links:
References:
