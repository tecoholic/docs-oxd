# Goal

- It is super simple to protect web site by OpenID Connect or UMA (using specific library, e.g. python/php/java)
- Implementation of new library/plugin (on any language) is simple (convenient for Gluu library support)

oxD Server is designed to work as standalone application (without Web Application Container, e.g. tomcat). It communicates with plugin(s) via socket. oxD is restricted to `localhost` by default.

# Web site protection with oxD

Web site communicates with oxD Server via library/plugin (python/php/java). Library provides all convenient methods to web site code which in background call oxD Server. Concrete library depends on programming language used by a web site. Here for simplicity we use Python as sample.

![oxd_overview](https://raw.githubusercontent.com/GluuFederation/docs-oxd/master/sources/img/oxd-rp.png)

First of all web site must register itself with oxD Server via registration command (using python/php library). With registration it gets oxd_id from oxD Server. oxd_id must be passed to all commands.

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