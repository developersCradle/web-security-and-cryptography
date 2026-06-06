# Section 09 - Introduction to OpenID Connect.

Introduction to OpenID Connect.

# What I Learned.

# What is an ID Token.

- **ID tokens** are **JWT tokens**.

<div align="center">
    <img src="ID_Token_Jwt.PNG" alt="The Nuts and Bolts of OAuth 2.0." width="500"/>
</div>

1.  There is the **header**, **payload** and **signature** part!
    - These **base64** coded headers!

- Once we are running the brought the **base64** decoder!

<div align="center">
    <img src="Decoded_Id_Token.PNG" alt="The Nuts and Bolts of OAuth 2.0." width="500"/>
</div>


1. This is abut the token!
````Json
{
  "kid": "gaNTVZLLCZI1NyzlfB4AED-yXy15dlvC5vIfgiknJ620",
  "alg": "RS256"
}
````
2. This is about the **payload**.
    - `iss` about the issuer if the token!
    - `aud` Identify the user of the token!
    - `iat` is Unix **timestamp** when it was issued!
    - `exp` is Unix **timestamp** when it will be expired!
    - `sub` The unique identifier for the user ({USER_ID}).
````Json
{
  "sub": "{USER_ID}",
  "email": "user@example.com",
  "iss": "https://authorization-server.com/oauth2/ausd1nry9hBoyvKrY0h7",
  "aud": "{CLIENT_ID}",
  "iat": 1524237221,
  "exp": 1524240821,
  "nonce": "{NONCE}",
  "auth_time": 1524606562
}
````
3. The signature is the security guard of the **JSON Web Token** (**JWT**). Its entire job is to ensure that the token hasn't been **tampered** with while traveling across the internet.
````Json
signature
````

# How ID Tokens are Different from Access Tokens.

<div align="center">
    <img src="Token_Are_The_Same.PNG" alt="The Nuts and Bolts of OAuth 2.0." width="500"/>
</div>

1. Often time the `access token` and `ID token` is the same, the token looks the same!
    - They are not the **same thing**!

- **Access token** to used to make **API calls**! Getting the key from **Auhtorzation Server**!

<div align="center">
    <img src="Access_Token_Flow.gif" alt="The Nuts and Bolts of OAuth 2.0." width="500"/>
</div>

- **ID token** to! Getting the key from **Auhtorzation Server**!

<div align="center">
    <img src="Authorization_Token_Flow.gif" alt="The Nuts and Bolts of OAuth 2.0." width="500"/>
</div>

1.  Application gets the **ID token** and unpack it
    - Validate the **claim**!
    - Validate the **signature**!




# Obtaining an ID Token.

# Hybrid OpenID Connect Flows.

# Validating and Using an ID Token.

# Assignment 06: Getting the User's Name and Email Address using OpenID Connect.