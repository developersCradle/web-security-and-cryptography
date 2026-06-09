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
    - Before redirecting.
        - It goes to **App** create **new secret** and **hashes it** for this particular flow!

<div align="center">
    <img src="PKCE_Code_Verifier.PNG" alt="The Nuts and Bolts of OAuth 2.0." width="500"/>
</div>

1. **PKCE** generates **Code Verifier**!

<div align="center">
    <img src="PKCE_Code_Challenge.PNG" alt="The Nuts and Bolts of OAuth 2.0." width="500"/>
</div>

1. **PKCE** generates **Code Challenge**!  

<div align="center">
    <img src="Flow_02.PNG" alt="The Nuts and Bolts of OAuth 2.0." width="500"/>
</div>

1. **App** generates the **hash** and returns it to the browser!
2. **User browser** carrying that **hash** to the **OAuth server**
    - This is **used** in **front channel**!
        - This is the reason why we are using the **hash**, when sending request thought the **User browser**! We are not sending the secret itself!

<div align="center">
    <img src="Flow_03.PNG" alt="The Nuts and Bolts of OAuth 2.0." width="500"/>
</div>

1. User is asked to log in in **OAuth server**! After the user logs in, the **Authorization Server** redirects back with an **authorization code**.

<div align="center">
    <img src="Flow_04.PNG" alt="The Nuts and Bolts of OAuth 2.0." width="500"/>
</div>

1. **OAuth** returns the **temporary code** that can be used to get a token!

<div align="center">
    <img src="Flow_05.PNG" alt="The Nuts and Bolts of OAuth 2.0." width="500"/>
</div>

1. Now we can get request for **access token** from the **App server side**. This includes:
    ````Json
    POST /token
    Content-Type: application/x-www-form-urlencoded

    grant_type=authorization_code
    code=AUTH_CODE
    redirect_uri=https://app.com/callback
    client_id=CLIENT_ID
    client_secret=CLIENT_SECRET
    ````
    - If using **PKCE**, you also send code_verifier instead of relying on a client secret.
    - The OAuth server will reply with the **tokens**!
    ````Json
    {
    "access_token": "ACCESS_TOKEN",
    "refresh_token": "REFRESH_TOKEN",
    "expires_in": 3600
    }
    ````

- **PKCE** is recommended to use!

<div align="center">
    <img src="Authorization_Code_Injection.PNG" alt="The Nuts and Bolts of OAuth 2.0." width="500"/>
</div>

1. **PKCE** should be used, to prevent this!

<div align="center">
    <img src="PKCE_Codes.PNG" alt="The Nuts and Bolts of OAuth 2.0." width="500"/>
</div>

1. **Code Verifier** (Secret) random string!
2. **Cade Challenge** (Publish Hash) `base64url(sha256(code_verifier))`!

- Now we are ready to **send user** to OAuth server!

<div align="center">
    <img src="Authorization_URL.PNG" alt="The Nuts and Bolts of OAuth 2.0." width="500"/>
</div>

1. Find **authorization endpoint** from:
    - Document! 
    - OAuth metadata URL to find it!
        - Use OpenID Connect **Discovery** (recommended)!
2. Rest **Query String**:
    - `response_type=code` - Request an **authorization code**! We want **authorization code**!
    - `client_id` - Identifies the application! Add your apps **client_id**!
    - `redirect_uri` - Where to send the user back! This has to match, ones which you registered the app!
    - `scope` - Permissions being requested!
    - `state` - **CSRF** protection! **PKCE** provides this protection also! 
    - `code_challenge` - **PKCE** challenge (if using **PKCE**)!
    - `code_challenge_method=S256` - **PKCE** hashing method!
    - todo fix this
    ````JSON
    GET /authorize?
    response_type=code
    client_id=CLIENT_ID
    redirect_uri=https://app.example.com/callback
    scope=openid profile email
    state=random123
    ````

<div align="center">
    <img src="OAuth_Login_Screen.PNG" alt="The Nuts and Bolts of OAuth 2.0." width="500"/>
</div>


<div align="center">
    <img src="Authorization_Code_Flow.PNG" alt="The Nuts and Bolts of OAuth 2.0." width="500"/>
</div>