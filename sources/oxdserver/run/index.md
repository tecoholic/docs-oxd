[TOC]

# Running oxD Server 
##Manually
These instructions are running the oxD Server manually.

1. Download [oxD distrubution](http://ox.gluu.org/maven/org/xdi/oxd-server/1.0.6-master-SNAPSHOT/oxd-server-1.0.6-master-SNAPSHOT-distribution.zip) and **unzip** it.

2. Download the [resteasy jar](http://ox.gluu.org/maven/org/jboss/resteasy/resteasy-jaxrs/2.3.4.Final/resteasy-jaxrs-2.3.4.Final.jar) and [castle jar](http://ox.gluu.org/maven/org/bouncycastle/bcprov-jdk16/1.46/bcprov-jdk16-1.46.jar).

3. Run `java -cp bcprov-jdk16-1.46.jar;resteasy-jaxrs-2.3.4.Final.jar;oxd-server-1.3-SNAPSHOT-jar-with-dependencies.jar org.xdi.oxd.server.ServerLauncher`

The following screen is similar to what you will see if the oxD server start successfully.
![image](http://ox.gluu.org/lib/exe/fetch.php?media=oxd:oxd_started.png)

### Manually with Advanced Configuration
The custom configurations can be loaded using the `oxd.server.config` system property. This property is used to point to the custom configuration `json` file while running the oxD server. The example shoes the location of the custom configurtion to be `C:\tmp\oxd.json`

1. Download [oxD distrubution](http://ox.gluu.org/maven/org/xdi/oxd-server/1.0.6-master-SNAPSHOT/oxd-server-1.0.6-master-SNAPSHOT-distribution.zip) and **unzip** it.

2. Download the [resteasy jar](http://ox.gluu.org/maven/org/jboss/resteasy/resteasy-jaxrs/2.3.4.Final/resteasy-jaxrs-2.3.4.Final.jar) and [castle jar](http://ox.gluu.org/maven/org/bouncycastle/bcprov-jdk16/1.46/bcprov-jdk16-1.46.jar).

3. Run `ava -cp resteasy-jaxrs-2.3.4.Final.jar;oxd-server-1.0-SNAPSHOT-jar-with-dependencies.jar org.xdi.oxd.server.ServerLauncher -Doxd.server.config=C:\tmp\oxd.json -Dlog4j.configuration=C:\tmp\test\log4j.xml`

# Logs
Logs are written into the working directoy in oxD Server by default. Custom log locations can be provided with the `log4j.xml` file. The file is loaded using the `log4j.configuration` system property. The following is an example for running the oxD server with `log4j` with the file located in `C:\tmp\test\log4j.xml`.

`# java -cp resteasy-jaxrs-2.3.4.Final.jar;oxd-server-1.0-SNAPSHOT-jar-with-dependencies.jar org.xdi.oxd.server.ServerLauncher -Doxd.server.config=C:\tmp\oxd.json -Dlog4j.configuration=C:\tmp\test\log4j.xml`

The following is an example of `log4j.xml` file:

```
<?xml version="1.0" encoding="UTF-8"?><!DOCTYPE log4j:configuration SYSTEM "log4j.dtd">
 
<log4j:configuration xmlns:log4j="http://jakarta.apache.org/log4j/" debug="false">
 
    <appender name="CONSOLE" class="org.apache.log4j.ConsoleAppender">
        <layout class="org.apache.log4j.PatternLayout">
            <!-- The default pattern: Date Priority [Category] Message\n -->
            <param name="ConversionPattern" value="%d %-5p [%c] %m%n"/>
        </layout>
    </appender>
 
    <appender name="FILE" class="org.apache.log4j.DailyRollingFileAppender">
        <param name="File" value="C:\\tmp\\test\\oxd-server.log"/>
        <param name="DatePattern" value="'.'yyyy-MM-dd"/>
        <param name="BufferSize" value="1000"/>
        <layout class="org.apache.log4j.PatternLayout">
            <!-- The default pattern: Date Priority [Category] Message\n -->
            <param name="ConversionPattern" value="%d %-5p [%c] %m%n"/>
        </layout>
    </appender>
 
    <category name="org.xdi">
        <priority value="TRACE"/>
    </category>
 
    <root>
        <priority value="INFO"/>
        <appender-ref ref="FILE"/>
        <appender-ref ref="CONSOLE"/>
    </root>
 
</log4j:configuration>
```
