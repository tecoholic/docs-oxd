# Goal

- It is super simple to protect web site by OpenID Connect or UMA (using specific library, e.g. python/php/java)
- Implementation of new library (on any language) is simple (convenient for Gluu library support)

oxD Server is designed to work as standalone application (without Web Application Container, e.g. tomcat). It communicates with plugin(s) via socket. oxD is restricted to `localhost` by default.

# Web site protection with oxD

Web site communicates with oxD Server via library (python/php/java). Library provides all convenient methods to web site code which in background call oxD Server. Concrete library depends on programming language used by a web site. Here for simplicity we use Python as sample.

First of all web site must register itself with oxD Server via registration command (using python/php library). With registration it gets oxd_id from oxD Server. oxd_id must be passed to all commands.

Web site configuration:
```
   oxd_address : localhost:8090
   oxd_id : 6F9619FF-8B86-D011-B42D-00CF4FC964FF
```
oxd_id (6F9619FF-8B86-D011-B42D-00CF4FC964FF) - GUID for web site. It can be any GUID that does not exist yet on oxD Server.