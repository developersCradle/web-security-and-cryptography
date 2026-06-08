# Section 04: OAuth for Server-Side Applications.

OAuth for Server-Side Applications. 

# What I Learned.

# Introduction.

# Registering an Application.

> [!NOTE]
> Application registration = creating a trusted client in the Authorization Server and obtaining a **Client ID** (and sometimes a **Client Secret**).

- When we register the OAuth with given **Authorization Server**!

- What you provide during registration typically:
    - Application name.
    - Redirect URI(s).
        - Example of redirect URI `https://myapp.example.com/callback`.
    - Application type (web, mobile, SPA, etc.).
    - Contact information (optional).

- Without **registration**, the Authorization Server would not know:
    - Which app is requesting access.
    - Which redirect URIs are allowed.
    - Whether the app is public or confidential.
- Hacker can't start OAuth flow and redirect to attackers website!
    - Redirect hack!

<div align="center">
    <img src="We_Might_Get_Back.PNG" alt="The Nuts and Bolts of OAuth 2.0." width="500"/>
</div>

1. Once registered with the **Authorization Server**, we might get `client_id` and `client_secret`. We might get:
    ````Xml
    Client ID: abc123
    Client Secret: xyz789
    ````
    - The `Client ID` identifies your application. 
        - **Public information**, can be in **source code**!
    - The `Client Secret` is like a password for confidential clients (e.g., backend web apps). Public clients such as mobile apps and SPAs typically do not use a client secret and instead use PKCE.
        - **Depends, can add**:
            - Confidential clients (server-side apps).
                - Backend web applications.
                - Server-to-server services.
            - You **can store** the **client secret** on the **server** because users cannot access it.
        - **Depends, cannot add**:
            - Public clients (mobile apps, SPAs, desktop apps).
             - **Do not store** a **client secret** in these apps.
                - JavaScript bundles
                - Mobile app binaries
                - Desktop app executables
            - Can eventually be extracted by users.

# Authorization Code Flow for Web Applications.

<div align="center">
    <img src="Summary_Of_The_Flow_Authorization_For_Web_Applications.PNG" alt="The Nuts and Bolts of OAuth 2.0." width="500"/>
</div>

1. User needs to access App.
    - Browser never receives tokens directly, this should be done in app backend server.
2. App needs token from OAuth server.
3. To make API requests.

<div align="center">
    <img src="Flow_01.PNG" alt="The Nuts and Bolts of OAuth 2.0." width="500"/>
</div>

1. User clicking login button!
    - Before redirecting
        - App create **new secret** and **hashes it**!


````
Browser → Authorization Server (login)
Authorization Server → Browser (authorization code)
Backend → Authorization Server (token exchange)
Backend ← Access Token + ID Token
````