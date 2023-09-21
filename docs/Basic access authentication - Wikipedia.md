---
type: note
tags:
  - literature
  - zettelkasten
page-title: Basic access authentication - Wikipedia
url: https://en.wikipedia.org/wiki/Basic_access_authentication
date: 2023-05-16 19:46:14
share: "true"
---

> In the context of an [HTTP](https://en.wikipedia.org/wiki/HTTP "HTTP") transaction, **basic access authentication** is a method for an [HTTP user agent](https://en.wikipedia.org/wiki/User_agent "User agent") (e.g. a [web browser](https://en.wikipedia.org/wiki/Web_browser "Web browser")) to provide a [user name](https://en.wikipedia.org/wiki/User_name "User name") and [password](https://en.wikipedia.org/wiki/Password "Password") when making a request. In basic HTTP authentication, a request contains a header field in the form of `Authorization: Basic <credentials>`, where credentials is the [Base64](https://en.wikipedia.org/wiki/Base64 "Base64") encoding of ID and password joined by a single colon `:`.
## 2023-05-16 19:50:52

> The BA mechanism does not provide [confidentiality](https://en.wikipedia.org/wiki/Information_security#Confidentiality "Information security") protection for the transmitted credentials. They are merely encoded with [Base64](https://en.wikipedia.org/wiki/Base64 "Base64") in transit and not [encrypted](https://en.wikipedia.org/wiki/Encryption "Encryption") or [hashed](https://en.wikipedia.org/wiki/Cryptographic_hash "Cryptographic hash") in any way. Therefore, basic authentication is typically used in conjunction with [HTTPS](https://en.wikipedia.org/wiki/HTTPS "HTTPS") to provide confidentiality.
## 2023-05-16 19:53:27

> Because the BA field has to be sent in the header of each HTTP request, the web browser needs to [cache](https://en.wikipedia.org/wiki/Cache_(computing) "Cache (computing)") credentials for a reasonable period of time to avoid constantly prompting the user for their username and password. Caching policy differs between browsers.
