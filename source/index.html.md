---
title: API Reference

language_tabs:
  - shell


toc_footers:
  - <a href='https://github.com/tripit/slate'>Documentation Powered by Slate</a>

includes:
  - users
  - sessions
  - donations
  - donors
  - drivers
  - errors

search: true
---

# Introduction
The Hacksmiths Food Drivr API is fairly easy to use.  When in doubt, follow REST principles.

Most requests require specific headers.  Make sure to include the Content-Type header and the Authorization header for any request.  The only exception to this is when you are creating a User or a Session, in which case you will not yet have an Auth token.

### REST & HTTP Methods
With this API, there are 4 main HTTP methods you will use.
* GET
Get will get you data, either in the form of an array or a singular JSON object.

* POST
POST is used to create resources, i.e. Users, Sessions, Donations, et. al.
* PATCH
PATCH is used to update one or more parameters of a JSON object.  As long as you use the right parameter names, this should be easy.
* DELETE
DELETE is really only used in the context of deleting a Session.  To sign a user out and change their auth token, you will send a DELETE request, for example.

### Headers
To the right, you will see an example of your typical headers.

```shell
  "Content-Type: application/json"  
  "Authorization: your_authorization_token"
```
