Wordpress SSO plugin 
=========================
![image](https://raw.githubusercontent.com/GluuFederation/gluu-wordpress-oxd-login-plugin/master/plugin.jpg)

WP-GlUU-SSO plugin gives access for login to your wordpress site, with the help of GLUU server.

There are already 2 versions of WP-GlUU-SSO (2.4.2 and 2.4.3) plugins, each in its turn is working with oXD and GLUU servers.
For example if you are using wp-gluu-sso-2.4.2 plugin, you need to connect with oXD-server-2.4.2.

Now I want to explain in details how to use plugin step by step. 

Plugin will not be working if your host does not have https://. 

# Step 1. Install Gluu-server 

(version 2.4.2 or 2.4.3)

If you want to use external gluu server, You can not do this step.   

[Gluu-server installation gide](https://www.gluu.org/docs/deployment/).

# Step 2. Download oXD-server 

(version 2.4.2 or 2.4.3)

[Download oXD-server-2.4.2.Final](https://ox.gluu.org/maven/org/xdi/oxd-server/2.4.2.Final/oxd-server-2.4.2.Final-distribution.zip).

or

[Download oXD-server-2.4.3.DEMO](https://ox.gluu.org/maven/org/xdi/oxd-server/2.4.3-SNAPSHOT/oxd-server-2.4.3-SNAPSHOT-distribution.zip).

# Step 3. Unzip and run oXD-server
 
### Unzip your oXD-server. 
### Open the command line and navigate to the extracted folder in the conf directory.
### Open oxd-conf.json file.  
### If your server is using 8099 port, please change "port" number to free port, which is not using.
### Set parameter "op_host":"Your gluu-server-url (internal or external)"
### Open the command line and navigate to the extracted folder in the bin directory.
### For Linux environment, run sh oxd-start.sh&. 
### For Windows environment, run oxd-start.bat.
### After the server starts, go to Step 4.

# Step 4. Download wp-sso-plugin
 
(version 2.4.2 or 2.4.3)

[Download WP-sso-2.4.2 plugin](https://ox.gluu.org/maven/org/xdi/oxd-server/2.4.2.Final/oxd-server-2.4.2.Final-distribution.zip).

or

[Download WP-sso-2.4.3 plugin](https://ox.gluu.org/maven/org/xdi/oxd-server/2.4.3-SNAPSHOT/oxd-server-2.4.3-SNAPSHOT-distribution.zip).

For example if you are using gluu-server-2.4.2 it is necessary to use oXD-server-2.4.2 and wp-sso-plugin-2.4.2.

# Step 5. Open Wordpress site plugin page
 
Go to https://{site-base-url}/wp-admin/plugin-install.php?tab=upload

# Step 6. Upload plugin
 
Upload plugin and click install now button.

# Step 7. Activate plugin
 
### Go to https://{site-base-url}/wp-admin/plugins.php
### Find Gluu SSO {version} plugin and click activate button.

# Step 8. Plugin configuration
 
Now in your admin menu panel you can see Gluu SSO {version menu} tab, click on it.

# Step 9. General

![General](https://github.com/GluuFederation/gluu-wordpress-sso-login-plugin/blob/master/wp-sso-2.4.2/docu/1.png) 

### Membership: must be checked.
### New User Default Role: please choose user role. 
### Admin Email: please add your or admin email address for registrating site in Gluu server.
### Oxd port: choose that port which is using oxd-server (see in oxd-server/conf/oxd-conf.json file).

