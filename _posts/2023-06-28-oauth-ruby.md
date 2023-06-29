---
title: OAuth
author: gcalvoCR
date: 2023-06-28 12:00:00 -0600
categories: [concepts, oauth, ruby]
tags: [concepts, oauth, ruby] # tag names should always be lowercase
---

# Oauth

OAuth (Open Authorization) is an open and standard authorization protocol that allows users to grant third-party access to their online resources without sharing their login credentials. It was designed to enable users to authorize access to their accounts on different services without revealing their usernames and passwords to those services.

## Use case flow

![Use case flow 2](/assets/img/oauth2-caseflow.png)

Terms

- **Resource Server** – The server hosting the protected resource.

- **Resource Owner** – An entity capable of granting access to a protected resource.

- **Client** – An application making protected resource requests on behalf of the resource owner. It can be a server-based, mobile or a desktop application.

- **Authorization Server** – The server issuing access tokens to the clients after successfully authenticating the resource owner and obtaining authorization.
