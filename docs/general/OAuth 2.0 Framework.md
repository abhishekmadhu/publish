---
share: "true"
---

#programming 
# OAuth 2.0 Framework

Framework for [[OAuth 2|OAuth 2]]
Web RFC: [https://datatracker.ietf.org/doc/html/rfc6749](https://datatracker.ietf.org/doc/html/rfc6749)

# Table of Contents
```toc
```

# Introduction

There are many weaknesses if a resource owner shares their password to provide access to a third party. OAuth decouples authentication from authorization, by relying on a third party to grant an access token. Doing this reduces your attack surface since your client secret is not required to access certain resources.

In OAuth 2.0, an `access token` is used to grant access to a specific scope and limited time of access.

OAuth 2.0 is not backward compatible with 1.0

# Roles

```
OAuth defines four roles:

   resource owner
      An entity capable of granting access to a protected resource.
      When the resource owner is a person, it is referred to as an
      end-user (or simply, "user").

   resource server
      The server hosting the protected resources, capable of accepting
      and responding to protected resource requests using access tokens.

   client
      An application making protected resource requests on behalf of the
      resource owner and with its authorization.  The term "client" does
      not imply any particular implementation characteristics (e.g.,
      whether the application executes on a server, a desktop, or other
      devices).

   authorization server
      The server issuing access tokens to the client after successfully
      authenticating the resource owner and obtaining authorization.
```

The authorization server may be the same server as the resource server or a separate entity. A single authorization server may issue access tokens accepted by multiple resource servers.

# Protocol Flow

```
     +--------+                               +---------------+
     |        |--(A)- Authorization Request ->|   Resource    |
     |        |                               |     Owner     |
     |        |<-(B)-- Authorization Grant ---|               |
     |        |          (four options)       +---------------+
     |        |
     |        |                               +---------------+
     |        |--(C)-- Authorization Grant -->| Authorization |
     | Client |                               |     Server    |
     |        |<-(D)----- Access Token -------|               |
     |        |                               +---------------+
     |        |
     |        |                               +---------------+
     |        |--(E)----- Access Token ------>|    Resource   |
     |        |                               |     Server    |
     |        |<-(F)--- Protected Resource ---|               |
     +--------+                               +---------------+
```

## (A) Authorization Request

## (B) Authorization Granted by Resource Owner

## (C) Request Access token using Authorization Grant

## (D) Access token provided by Authorization Server

## (E) Request protected resource using Access Token

## (F) Get protected resource

# Authorization Grant

It is a separate set of credentials that have their own lifetime and scope to access the protected resources of the resource owner. Think of it as a new password (not really, but we will get to that) that the resource owner can create, limit what can be accessed with this password, and share it with a third party.

There are four different types for authorization grant:

- Authorization code
- Implicit Grant
- Resource Owner Password Credentials
- Client Credentials

## Authorization Code

```python
Client ----(req)----> Authorisation Server ----(req)----> Resource Owner
Client <---(res)----- Authorisation Server <---(res)----- Resource Owner

```

1. The user (resource-owner) visits the client
2. The client redirects the user to the auth server
3. The Auth server asks the user for their credentials
4. The Auth server validates that the credentials are accurate
5. The Auth server generates an authorization code
6. The Auth server redirects the user to the client with the authorization code

Since the resource owner never shares the credentials with the third party, it does not have access to it. Instead it now uses the authorization code to get the `access token` to act on behalf of the user under the limited scope for the limited time.

### Security Benefits of Authorization Code

1. Resource-owner’s user-agent and network is bypassed, which provides a lot of security from MITM attacks, bad extensions, network logging and snooping

### PKCE - Proof Key for Code Exchange

This is an extension to Authorization Code Flow that prevents CSRF and Authorization code injection attacks.

## Implicit Grant

Simplified authorization code flow optimized for JS (and other scripting) clients.

Instead of the `authorization code`, a direct `access token` is issued to the client.

### Benefits

Since it reduced the number of round trips to the servers, it enhances performance.

### Drawbacks

This is not recommended anymore because of the following security issues

- [https://datatracker.ietf.org/doc/html/rfc6749#section-10.16](https://datatracker.ietf.org/doc/html/rfc6749#section-10.16)
- [https://datatracker.ietf.org/doc/html/rfc6749#section-10.3](https://datatracker.ietf.org/doc/html/rfc6749#section-10.3)

## Resource Owner Password Credentials

Needs real username-password from the resource owner.

This is used to get a `access token` and a `refresh token`

The username-password does not need to be stored anymore. The client can use the access token to get all data in scope. The access token generally lives long (24 hours for example), and can be refreshed using the refresh token when it expires.

This must be used only when no other authentication method is available.

## Client Credentials

- Used typically when the client is also the resource owner
- or is requesting access to previously configured resources (requires pre-configuration with the authorization server if needs access to user’s resources)

# Access Token

Access tokens are credentials used to access protected resources. It is generally a string representing an authorization issues to a client.
This is used in order to allow a wide range of grant types, but also allow the resource server to only understand the `access token`. This way the users can use multiple grant types but the resource server needs to process only the access token.

Based on the security requirements of the resource server, access tokens can have different cryptographic properties (length, format, use, content).

## Refresh Token

```
  +--------+                                           +---------------+
  |        |--(A)------- Authorization Grant --------->|               |
  |        |                                           |               |
  |        |<-(B)----------- Access Token -------------|               |
  |        |               & Refresh Token             |               |
  |        |                                           |               |
  |        |                            +----------+   |               |
  |        |--(C)---- Access Token ---->|          |   |               |
  |        |                            |          |   |               |
  |        |<-(D)- Protected Resource --| Resource |   | Authorization |
  | Client |                            |  Server  |   |     Server    |
  |        |--(E)---- Access Token ---->|          |   |               |
  |        |                            |          |   |               |
  |        |<-(F)- Invalid Token Error -|          |   |               |
  |        |                            +----------+   |               |
  |        |                                           |               |
  |        |--(G)----------- Refresh Token ----------->|               |
  |        |                                           |               |
  |        |<-(H)----------- Access Token -------------|               |
  +--------+           & Optional Refresh Token        +---------------+

```
