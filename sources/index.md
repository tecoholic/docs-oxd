# Welcome to the oxD Documentation

# Introduction
![image](https://raw.githubusercontent.com/GluuFederation/gluu-wordpress-oxd-login-plugin/master/plugin.jpg)

Gluu oxD is the new addition to the Gluu family which is set of software that helps to easily work with:

  - OpenID Connect as Relying Party
  - UMA - as Resource Server (for easy resource protection) or Relying Party


Mainly under oxD we understand:

- oxD Server
- oxD plugins (which are actually clients of oxD Server, for example `mod_ox` Apache plugins which helps to protect Apache resources with OpenID Connect & UMA Authorization server (oxAuth). It is a standalone application bound within `localhost` using only sockets to communicate with the plugins and servers.

![oxd_overview](https://raw.githubusercontent.com/GluuFederation/docs-oxd/master/sources/img/oxd_overview.png)

# Goal

The design goal for oxD is simplicity and with that goal the use of (python/php) libraries by the website is kept simple.


# Documentation

- [Introduction](./intro/index.md)
	  - [Plugins](./plugin/index.md)

