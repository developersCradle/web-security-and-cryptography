# Section 01: Introduction.

Introduction.

# What I Learned.

# Intro to this Course.

<div align="center">
    <img src="Introduction.PNG" alt="The Nuts and Bolts of OAuth 2.0." width="600"/>
</div>

1. The instructor!

<div align="center">
    <img src="Oauth_Is_Collection_Of_Multiple_Specs.PNG" alt="The Nuts and Bolts of OAuth 2.0." width="600"/>
</div>

1. **OAuth** is collection of multiple specs!

<div align="center">
    <img src="Two_Perspective.PNG" alt="The Nuts and Bolts of OAuth 2.0." width="600"/>
</div>

1. This course will have two perspectives:
    - Applications.
        - OAuth.
    - APIs.
        - OAuth.

<div align="center">
    <img src="Two_Perspective.PNG" alt="The Nuts and Bolts of OAuth 2.0." width="600"/>
</div>

1. Multiple ways to deal with OAuth.
    - Server-Side.
    - Mobile/Native.
    - SPA's.

# A Brief History of OAuth.

- Before **OAuth** there was **basic authentication**!

- **Old way** of asking permission!

<div align="center">
    <img src="Old_Way_Of_Asking_Credentials.PNG" alt="The Nuts and Bolts of OAuth 2.0." width="600"/>
</div>

1. If one would see following today, would you want to give application your password?
    - **3rd party** was give password to authenticate!
        - Lot of companies implemented their own way to authenticate!
            - They all had different names for things!

- OAuth 1.0 was some troubles with mobile apps.

- Some example using OAuth in **Smart TV**!

<div align="center">
    <img src="Oauth_In_Smart_Tvs.PNG" alt="The Nuts and Bolts of OAuth 2.0." width="600"/>
</div>

# How OAuth Improves Application Security.

<div align="center">
    <img src="Basic_Authentiac.PNG" alt="The Nuts and Bolts of OAuth 2.0." width="600"/>
</div>

1. Normally the authentication was handled as following!
    - Saved in session cookie!

- This will brake down, when there is need for multiple apps:
    - Single sign on.
    - Mobile app.

- We would need to **save password** in **multiple apps**!

<div align="center">
    <img src="Security_From_Perspective_Of_An.PNG" alt="The Nuts and Bolts of OAuth 2.0." width="600"/>
</div>

1. Aspects that User cares about:
2. Aspects that API cares about:


# OAuth vs OpenID Connect.

- **OAuth**:
    - Was designed to access to API.
        - No need to identify who is accessing.

- **OpenID**:

<div align="center">
    <img src="Illustration_Of_The_Open_ID.PNG" alt="The Nuts and Bolts of OAuth 2.0." width="600"/>
</div>

1. We can think of **Oauth** like the key card for the hotel room! Door does not **need** to know who opener is!
    - **Front desk**, checks your ID!
        - **Front desk** is behaving like **authentication** server!
        - **Card** is behaving like **access token**!
            - **Key card** will have what it **can open** and **how long its working**!
        - **Door** is behaving like **resource server**!

<div align="center">
    <img src="OpenID_Is_Implemented_Into_OAuth.PNG" alt="The Nuts and Bolts of OAuth 2.0." width="600"/>
</div>

1. **OpenID** is extension for the **OAuth** that provides **user information**!
    - Since names etc ...
    - **OAuth** uses **Access tokens**!
    - **OpenID** uses **ID tokens**!
        - This tells about the users!

<div align="center">
    <img src="Seperation_Of_Responsibilities.PNG" alt="The Nuts and Bolts of OAuth 2.0." width="600"/>
</div>

# Quiz 01: The Basics.