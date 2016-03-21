# Welcome to the oxD Documentation

# Goal

The design goal for oxD is to make it easier for developers to writeOpenID Connect and (eventually) UMA applications.

# Introduction
![image](https://raw.githubusercontent.com/GluuFederation/gluu-wordpress-oxd-login-plugin/master/plugin.jpg)

Gluu oxD is the new addition to the Gluu family which is set of software that helps to easily work with:

  - OpenID Connect as Relying Party
  - UMA - as Resource Server (for easy resource protection) or Relying Party (to request resources protected by UMA Resource Server)

Under oxD we understand:

- [oxD Server](./oxdserver/index.md)
- [oxD plugins](./plugin/index.md) (which are actually clients of oxD Server, for example `mod_ox` Apache plugins which helps to protect Apache resources with OpenID Connect & UMA Authorization server (oxAuth). It is a standalone application bound within `localhost` using only sockets to communicate with the plugins and servers.

![oxd_overview](https://raw.githubusercontent.com/GluuFederation/docs-oxd/master/sources/img/oxd_overview.png)


# Documentation

- [oxD Server](./oxdserver/index.md)
    - [Installation](./oxdserver/install/index.md)
    - [Run](./oxdserver/run/index.md)
    - [Troubleshooting](./oxdserver/troubleshooting/index.md)
- [Plugins](./plugin/index.md)
    - [Python](./plugin/python/index.md)
    - [PHP products](./plugin/php/index.md)
        - [Php Library](./plugin/php/library/index.md)
        - [Wordpress plugin](./plugin/php/cms/wordpress/index.md)
        - [Magento extension](./plugin/php/cms/magento/index.md)
        - [Drupal module](./plugin/php/cms/drupal/index.md)
        - [SugarCRM module](./plugin/php/crm/sugarcrm/index.md)
        - [SuiteCRM module](./plugin/php/crm/suitecrm/index.md)
