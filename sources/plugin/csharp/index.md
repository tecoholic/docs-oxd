## oxD-CSharp
 
CSharp Client Library for the [Gluu oxD](https://www.gluu.org/docs-oxd/2.4.4/) 

oxdCsharp is a thin wrapper around the [communication protocol](https://www.gluu.org/docs-oxd/oxdserver/) of 
oxD server. This can be used to access the OpenID connect Authorization end points of 
the Gluu Server via the oxD RP. This library provides the function calls required by a website 
to access user information from a OpenID Connect Provider (OP) by using the OxD as the Relying Party (RP).

## Installation

Note : Gluu server and oxD-server needs to be installed in the hosting server to use oxD-node library with your application.

* To download and install Gluu server [click me](http://www.gluu.org/docs/).
* To download and install oxD server [click me](http://ox.gluu.org/doku.php?id=oxd:rp).
* For oxD server configuration [click me](http://ox.gluu.org/doku.php?id=oxd:home&s[]=mvn).

## How to use

* oxd-csharp is oxD Server client implemented in C# language which acts according to [Protocol](https://www.gluu.org/docs-oxd/2.4.4/oxdserver/).
* All test classes using [CommonClasses](https://github.com/GluuFederation/oxd-csharp/tree/master/TCP/CommonClasses) and [ResponseClasses](https://github.com/GluuFederation/oxd-csharp/tree/master/TCP/ResponseClasses).		

## Register Site

		public RegisterSiteResponse RegisterSite(string host, int port, string redirectUrl)
        {
            try
            {
                CommandClient client = new CommandClient(host, port);
                RegisterSiteParams param = new RegisterSiteParams();
                param.SetAuthorizationRedirectUri(redirectUrl);
                param.SetPostLogoutRedirectUri(redirectUrl);
                param.SetClientLogoutUri(Lists.newArrayList(new string[] { "" }));

                Command cmd = new Command(CommandType.register_site);
                cmd.setParamsObject(param);

                string commandresponse = client.send(cmd);
                RegisterSiteResponse response = new RegisterSiteResponse(JsonConvert.DeserializeObject<dynamic>(commandresponse).data);
                Assert.IsNotNull(response);
                Assert.IsTrue(!String.IsNullOrEmpty(response.getOxdId()));
                StoredValues._oxd_id = response.getOxdId();
                return response;
            }
            catch (Exception ex)
            {
                Console.WriteLine(ex.Message);
                Logger.Debug(ex.Message);
                return null;
            }
        }
		

* Parameters necessary for to request register_site protocol
	* op_host
	* port
	* redirectUrl	

* Response 
	* oxd-id (Type: String)	
	
## Update Site Registeration

		public UpdateSiteResponse UpdateSiteRegisteration(string host, int port)
        {
            try
            {
                CommandClient client = new CommandClient(host, port);
                UpdateSiteParams param = new UpdateSiteParams();
                param.SetOxdId(StoredValues._oxd_id);
                param.SetAuthorizationRedirectUri("http://www.test.com/wp-login.php");
                param.SetPostLogoutRedirectUri("http://www.test.com/wp-login.php?action=logout&_wpnonce=a3c70643e9");
                param.SetApplicationType("web");
                param.SetRedirectUris(Lists.newArrayList(new string[] { "http://www.test.com/wp-login.php" }));
                param.SetAcrValues(new List<string>());
                param.SetClientJwksUri("");
                param.SetContacts(Lists.newArrayList(new string[] { "test@gmail.com" }));
                param.SetGrantType(Lists.newArrayList(new string[] { "authorization_code" }));
                param.SetClientTokenEndpointAuthMethod("");
                param.SetClientLogoutUri(Lists.newArrayList(new string[] { "http://www.test.com/wp-login.php?action=logout&_wpnonce=a3c70643e9" }));

                Command cmd = new Command(CommandType.update_site_registration);
                cmd.setParamsObject(param);

                string commandresponse = client.send(cmd);
                UpdateSiteResponse response = new UpdateSiteResponse(JsonConvert.DeserializeObject<dynamic>(commandresponse).data);
                Assert.IsNotNull(response);
                Assert.IsTrue(!String.IsNullOrEmpty(response.getOxdId()));
                return response;
            }
            catch (Exception ex)
            {
                Console.WriteLine(ex.Message);
                Logger.Debug(ex.Message);
                return null;
            }
        }	
		
update_site_registration class using [TCP.CommonClasses](https://github.com/GluuFederation/oxd-csharp/tree/master/TCP/CommonClasses) and [TCP.ResponseClasses](https://github.com/GluuFederation/oxd-csharp/tree/master/TCP/ResponseClasses).		

* Parameters necessary for to request update_site_registration protocol
	* op_host
	* port 	

* Response 
	* oxd-id (Type: String)
	 	
