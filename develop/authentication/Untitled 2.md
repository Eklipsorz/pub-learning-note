## 描述

> What Is an ID Token?

> An ID token is an artifact that proves that the user has been authenticated. It was introduced by OpenID Connect (OIDC), an open standard for authentication used by many identity providers such as Google, Facebook, and, of course, Auth0. Check out this document for more details on OpenID Connect. Let's take a quick look at the problem OIDC wants to resolve.


ID token 是一個用來證明使用者是受過認證

![](https://images.ctfassets.net/23aumh6u8s0i/4x34jgYBU7vjBYLumNr9Sg/57e0b420de0d27568981af4aef0ab27f/id-token-scenario.png)
> Here, a user with their browser authenticates against an OpenID provider and gets access to a web application.


> The result of that authentication process based on OpenID Connect is the ID token, which is passed to the application as proof that the user has been authenticated.

> This provides a very basic idea of what an ID token is: proof of the user's authentication. Let’s see some other details.

> An ID token is **encoded as a JSON Web Token** (JWT), a standard format that allows your application to easily inspect its content, and make sure it comes from the expected issuer and that no one else changed it

> To put it simply, an example of ID token looks like this:

```
eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJodHRwOi8vbXktZG9tYWluLmF1dGgwLmNvbSIsInN1YiI6ImF1dGgwfDEyMzQ1NiIsImF1ZCI6IjEyMzRhYmNkZWYiLCJleHAiOjEzMTEyODE5NzAsImlhdCI6MTMxMTI4MDk3MCwibmFtZSI6IkphbmUgRG9lIiwiZ2l2ZW5fbmFtZSI6IkphbmUiLCJmYW1pbHlfbmFtZSI6IkRvZSJ9.bql-jxlG9B_bielkqOnjTY9Di9FillFb6IMQINXoYsw
```

> Of course, this isn't readable to the human eye, so you have to decode it to see what content the JWT holds. By the way, the ID token is not encrypted but just Base 64 encoded. You can use one of the many available libraries to decode it, or you can examine it yourself with the jwt.io debugger.


> Without going deeper into the details, the relevant information carried by the ID token above looks like the following:

```json
{ 
  "iss": "http://my-domain.auth0.com", 
  "sub": "auth0|123456", 
  "aud": "1234abcdef", 
  "exp": 1311281970, 
  "iat": 1311280970, 
  "name": "Jane Doe", 
  "given_name": "Jane", 
  "family_name": "Doe"
}
```

> These JSON properties are called **claims**, and they are **declarations about the user** and the token itself. The claims about the user define the user’s identity


aud => token的接收者，會用特定獨特識別字來表示特定使用方，


> One important claim is the `aud` claim. This claim defines the **audience** of the token, i.e., the web application that is meant to be **the final recipient of the token**. In the case of the ID token, its value is the client ID of the application that should consume the token.

https://auth0.com/blog/id-token-access-token-what-is-the-difference/




## 複習


---
Status: #🌱 
Tags:
[[Authentication]]
Links:
[[authentication 是指特定事物被驗證是對、正確、合法事物之過程；authorization 是指授與權力給特定事物去做特定事情之過程]]
References: