[TOC]

# Installation

## Windows Installation
It is not necessary to install oxD in Windows, it can be downloaded and run. The oxD server is available for download from [maven repository](http://ox.gluu.org/maven/org/xdi/oxd-server/1.0.6-master-SNAPSHOT/oxd-server-1.0.6-master-SNAPSHOT-distribution.zip).

1. Download [oxd-server-1.0.6-master-SNAPSHOT-distribution.zip](http://ox.gluu.org/maven/org/xdi/oxd-server/1.0.6-master-SNAPSHOT/oxd-server-1.0.6-master-SNAPSHOT-distribution.zip)
2. Unzip the file in `oxd-server` folder. The folder name is for reference only; any other name will work as well.
3. Run `oxd-server/bin/oxd-start.bat`

## Unix Installation
It is not necessary to install oxD in Unix, it can be downloaded and run. The oxD server is available for download from [maven repository](http://ox.gluu.org/maven/org/xdi/oxd-server/1.0.6-master-SNAPSHOT/oxd-server-1.0.6-master-SNAPSHOT-distribution.zip).

1. Download [oxd-server-1.0.6-master-SNAPSHOT-distribution.zip](http://ox.gluu.org/maven/org/xdi/oxd-server/1.0.6-master-SNAPSHOT/oxd-server-1.0.6-master-SNAPSHOT-distribution.zip)
2. Unzip the file in `oxd-server` folder. The folder name is for reference only; any other name will work as well.
3. Run `oxd-server/bin/oxd-start.sh`

# Configuration
oxD configuration file is located in the `conf/configuration.json` file. 

![image](http://ox.gluu.org/lib/exe/fetch.php?media=oxd:oxd-dist.png)

The contents of the configuration file is as follows:

```
configuration.json
{
    "port":8099,
    "localhost_only":true,
    "time_out_in_seconds":0,
    "register_client_app_type":"web",
    "register_client_response_types":"code id_token token",
    "use_client_authentication_for_pat":true,
    "trust_all_certs":true,
    "trust_store_path":"",
    "license_server_endpoint":"",
    "license_id":"",
    "license_check_period_in_hours": 24,
    "public_key":"",
    "public_password":"",
    "license_password":""
}
```

* port - oxD socket port
* localhost_only - flag to restrict communication
* time_out_in_seconds - time out for oxd socket in seconds
* register_client_app_type - dynamic client registration application type
* register_client_response_types - dynamic client registration response types
