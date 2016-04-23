# Goal

- It is super simple to protect web site by OpenID Connect or UMA (using specific library, e.g. python/php/java)
- Implementation of new library/plugin (on any language) is simple (convenient for Gluu library support)

oxD Server is designed to work as standalone application (without Web Application Container, e.g. tomcat). It communicates via socket. oxD is restricted to `localhost` by default.

# Web site protection with oxD

Web site communicates with oxD Server via library (python/php/java). Library provides all convenient methods to web site code which in background call oxD Server. Concrete library depends on programming language used by a web site. Here for simplicity we use Java as sample.

![oxd_overview](https://raw.githubusercontent.com/GluuFederation/docs-oxd/master/sources/img/Overview.png)

First of all web site must register itself with oxD Server via registration command (using java/python/php library). With registration it gets oxd_id from oxD Server. oxd_id must be passed to all commands.

Web site configuration:
```
   oxd_address : localhost:8090
   oxd_id : 6F9619FF-8B86-D011-B42D-00CF4FC964FF
```
oxd_id (6F9619FF-8B86-D011-B42D-00CF4FC964FF) - GUID for web site. It can be any GUID that does not exist yet on oxD Server.

# Library/Plugin (Python/PHP/Java)

Library must support following commands:

## Register site

During registration operation oxd dynamically register client for web site and keeps it in configuration.

All parameters in register_site operation are optional except `authorization_redirect_uri`! All fallback values are taken from oxd-default-site-config.json

For latest and most up to date parameters of command please check latest successful [jenkins build](https://ox.gluu.org/jenkins/job/oxd)

Request:

```json
{
    "command":"register_site",
    "params": {
        "authorization_redirect_uri": "https://client.example.org/cb",<- REQUIRED public address of the site
        "logout_redirect_uri": "https://client.example.org/cb",    <- OPTIONAL public address of the site
        "application_type":"web",                                  <- OPTIONAL, default web (can be "native")
        "redirect_uris": ["https://client.example.org/cb"],        <- OPTIONAL
        "acr_values":[""],                                         <- OPTIONAL
        "client_jwks_uri":"",                                      <- OPTIONAL
        "client_token_endpoint_auth_method":"",                    <- OPTIONAL
        "client_request_uris":[],                                  <- OPTIONAL
        "contacts":["yuriy@gluu.org"]                              <- OPTIONAL
    }
}
```

Response:

```json
{
    "status":"ok",
    "data":{
        "oxd_id":"6F9619FF-8B86-D011-B42D-00CF4FC964FF"
    }
}
```

## Update site registration

For latest and most up to date parameters of command please check latest successful [jenkins build](https://ox.gluu.org/jenkins/job/oxd)

Request:

```json
{
    "command":"update_site_registration",
    "params": {
        "oxd_id":"6F9619FF-8B86-D011-B42D-00CF4FC964FF",
        "authorization_redirect_uri": "https://client.example.org/cb",<- REQUIRED public address of the site
        "post_logout_redirect_uri": "https://client.example.org/cb",  <- OPTIONAL public address of the site
        "client_logout_uris":["https://client.example.org/logout"],<-OPTIONAL
        "application_type":"web",                                  <- OPTIONAL, default web (can be "native")
        "grant_types":[],                                          <- OPTIONAL
        "redirect_uris": ["https://client.example.org/cb"],        <- OPTIONAL
        "acr_values":[""],                                         <- OPTIONAL
        "client_jwks_uri":"",                                      <- OPTIONAL
        "client_token_endpoint_auth_method":"",                    <- OPTIONAL
        "client_request_uris":[],                                  <- OPTIONAL
        "contacts":["yuriy@gluu.org"]                              <- OPTIONAL
    }
}
```

Response:

```json
{
    "status":"ok"
}
```


## Get authorization url

Note: authorization_code grant type

For latest and most up to date parameters of command please check latest successful [jenkins build](https://ox.gluu.org/jenkins/job/oxd)

Request:

```json
{
    "command":"get_authorization_url",
    "params": {
        "oxd_id":"6F9619FF-8B86-D011-B42D-00CF4FC964FF"
        "acr_values":["basic", "duo"]                         <- optional, may be skipped (default: basic)
    }
}
```

Response:

```json
{
    "status":"ok",
    "data":{
        "authorization_url":"  https://server.example.com/authorize?response_type=id_token%20token
    &client_id=s6BhdRkqt3
    &redirect_uri=https%3A%2F%2Fclient.example.org%2Fcb
    &scope=openid%20profile
    &state=af0ifjsldkj
    &nonce=n-0S6_WzA2Mj"
    }
}
```

## Get Tokens (ID & Access) by Code

Note: Library (php/python/java/node) must provide utility methods for web site to parse response from OP and send parsed code and state parameters to oxd:

For latest and most up to date parameters of command please check latest successful [jenkins build](https://ox.gluu.org/jenkins/job/oxd)

```
HTTP/1.1 302 Found
Location: https://client.example.org/cb?code=SplxlOBeZQQYbYS6WxSbIA&state=af0ifjsldkj&scopes=openid%20profile
```

Request:

```json
{
    "command":"get_tokens_by_code",
    "params": {
        "oxd_id":"6F9619FF-8B86-D011-B42D-00CF4FC964FF",
        "code":"I6IjIifX0",                <- Required, code from OP redirect url (see example above)
        "state":"af0ifjsldkj",             <- Optional can be skipped
        "scopes":["openid", "profile"]     <- Required, scopes from OP redirect url (see example above)
    }
}
```

Or otherwise if library does not provide parsing, call oxd server in following way:

Request:

```
{
    "command":"get_tokens_by_code",
    "params": {
        "oxd_id":"6F9619FF-8B86-D011-B42D-00CF4FC964FF",
        "location":"https://client.example.org/cb?code=SplxlOBeZQQYbYS6WxSbIA&state=af0ifjsldkj&scopes=openid%20profile"
    }
}
```

Response:

```
{
    "status":"ok",
    "data":{
        "access_token":"SlAV32hkKG",
        "expires_in":3600,
        "refresh_token":"aaAV32hkKG1"
        "id_token":"eyJ0 ... NiJ9.eyJ1c ... I6IjIifX0.DeWt4Qu ... ZXso",
        "id_token_claims": {
             "iss": "https://server.example.com",
             "sub": "24400320",
             "aud": "s6BhdRkqt3",
             "nonce": "n-0S6_WzA2Mj",
             "exp": 1311281970,
             "iat": 1311280970,
             "at_hash": "MTIzNDU2Nzg5MDEyMzQ1Ng"
        }
    }
}
```

## Get User Info

For latest and most up to date parameters of command please check latest successful [jenkins build](https://ox.gluu.org/jenkins/job/oxd)

Request:

```json
{
    "command":"get_user_info",
    "params": {
        "oxd_id":"6F9619FF-8B86-D011-B42D-00CF4FC964FF",
        "access_token":"SlAV32hkKG"
    }
}
```

Response:

```json
{
    "status":"ok",
    "data":{
        "claims":{
            "sub": ["248289761001"],
            "name": ["Jane Doe"],
            "given_name": ["Jane"],
            "family_name": ["Doe"],
            "preferred_username": ["j.doe"],
            "email": ["janedoe@example.com"],
            "picture": ["http://example.com/janedoe/me.jpg"]
        }
    }
}
```

## Log out

For latest and most up to date parameters of command please check latest successful [jenkins build](https://ox.gluu.org/jenkins/job/oxd)

Request:

```json
{
    "command":"logout",
    "params": {
        "oxd_id":"6F9619FF-8B86-D011-B42D-00CF4FC964FF",
        "id_token":"eyJ0 ... NiJ9.eyJ1c ... I6IjIifX0.DeWt4Qu ... ZXso" <-- OPTIONAL (oxd server will use last used ID Token)
        "post_logout_redirect_uri":"<post logout redirect uri here>",   <-- OPTIONAL
        "http_based_logout":false     <- true if front-channed http based logout should be used
    }
}
```

Response:

```json
{
    "status":"ok",
    "data":{
        "html":"<html of http based logout>"  <-- OPTIONAL, returned only if http_based_logout=true
    }
}
```