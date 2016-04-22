[TOC]

# Installation
This page documents the building, installation of the oxD server.

## Build oxD Server
oxD server can be built using Maven.

oxD code is available in  [Github](https://github.com/GluuFederation/oxd). Maven is used to build the code from github. Download the oxD code from github in any method that is suitable. The code can be downloaded directly from [this link](https://github.com/GluuFederation/oxd/archive/master.zip). The following command can be run inside the oxd folder and it will build oxD Server. Please read the [Maven Guide](http://maven.apache.org/download.cgi) to download and install Maven if necessary.

`# mvn clean package`


## Windows Installation
It is not necessary to install oxD in Windows, it can be downloaded and run. The oxD server is available for download from [maven repository](http://ox.gluu.org/maven/org/xdi/oxd-server).

1. Download oxd Server according to you CE installation (for CE 2.4.3 please download oxd 2.4.3)[oxd-server-2.4.3-Final.zip](http://ox.gluu.org/maven/org/xdi/oxd-server/2.4.3.Final/oxd-server-2.4.3.Final-distribution.zip)
2. Unzip the file in `oxd-server` folder. The folder name is for reference only; any other name will work as well.
3. Run `oxd-server/bin/oxd-start.bat`

## Unix Installation
It is not necessary to install oxD in Unix, it can be downloaded and run. The oxD server is available for download from [maven repository](http://ox.gluu.org/maven/org/xdi/oxd-server/).

1. Download xd Server according to you CE installation (for CE 2.4.3 please download oxd 2.4.3)[oxd-server-2.4.3-Final-distribution.zip](http://ox.gluu.org/maven/org/xdi/oxd-server/2.4.3.Final/oxd-server-2.4.3.Final-distribution.zip)
2. Unzip the file in `oxd-server` folder. The folder name is for reference only; any other name will work as well.
3. Run `oxd-server/bin/oxd-start.sh`

# Configuration
oxD configuration file is located in the `conf/oxd-conf.json` file.

![image](http://ox.gluu.org/lib/exe/fetch.php?media=oxd:oxd-dist.png)

**Please define op_host which should point to valid CE installation.** Sample: "op_host":"https://ce-dev.gluu.org".

The contents of the configuration file is as follows:

```
oxd-conf.json
{
    "port":8099,
    "localhost_only":true,
    "time_out_in_seconds":0,
    "jetty_port":8098,
    "start_jetty":false,
    "use_client_authentication_for_pat":true,
    "trust_all_certs":true,
    "trust_store_path":"",
    "license_server_endpoint":"",
    "license_id":"",
    "license_check_period_in_hours": 24,
    "public_key":"",
    "public_password":"",
    "license_password":"",
    "op_host":""
}
```

* port - oxD socket port
* localhost_only - flag to restrict communication
* time_out_in_seconds - time out for oxd socket in seconds
* register_client_app_type - dynamic client registration application type
* register_client_response_types - dynamic client registration response types

