# Introduction
![image](https://raw.githubusercontent.com/GluuFederation/gluu-wordpress-oxd-login-plugin/master/plugin.jpg)

Gluu oxD is the new addition to the Gluu family which acts as a mediator between `mod_ox` Apache plugins and OpenID Connect & UMA Authorization server (oxAuth). It is a standalone application bound within `localhost` using only sockets to communicate with the plugins and servers. The application is developed in `java` to use its rich libraries.

![oxd_overview](https://raw.githubusercontent.com/GluuFederation/docs-oxd/master/sources/img/oxd_overview.png)

# Design

The disign goal for oxD is simplicity and with that goal the use of (python/php) libraries by the website is kept simple.