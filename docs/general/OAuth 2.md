---
share: "true"
---

# OAuth 2

Website: [https://oauth.net/2/](https://oauth.net/2/)

[[OAuth 2.0 Framework](https://tools.ietf.org/html/rfc6749)](OAuth%202%200%20587e717d80f145009484a01e19db769c/OAuth%202%200%20Framework%20ccd68836589c4275ac243945819340ea.md)

[[Client Registration|Client Registration]]

There are many weaknesses if a resource owner shares their password to provide access to a third party. OAuth decouples authentication from authorization, by relying on a third party to grant an access token. Doing this reduces your attack surface since your client secret is not required to access certain resources.

In OAuth 2.0, an `access token` is used to grant access to a specific scope and limited time of access.

Access tokens are credentials used to access protected resources. It is generally a string representing an authorization issues to a client.
This is used in order to allow a wide range of grant types, but also allow the resource server to only understand the `access token`. This way the users can use multiple grant types but the resource server needs to process only the access token.
