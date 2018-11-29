# Wildfly + Elastic APM POC
This repository contains a simple copy&paste fork of the Wildfly 9.0.2.FINAL HelloWorld Quickstart example
with the addition of Elastic APM. It exists to easily reproduce an incompatibility bug between Wildfly,
Elastic APM java agent, and the APM agent API.

To reproduce the bug, deploy into Wildfly 9.0.2.FINAL or newer with elastic agent configuration added
to standalone.conf (replace wfly and agent paths):
```
#Add Elastic APM agent
#JBOSS_MODULES_SYSTEM_PKGS="co.elastic.apm"
JAVA_OPTS="$JAVA_OPTS -javaagent:<wfly_home>/bin/elastic-apm-agent-1.1.0.jar"
JAVA_OPTS="$JAVA_OPTS -Delastic.apm.service_name=apm-poc"
JAVA_OPTS="$JAVA_OPTS -Delastic.apm.server_url=http://localhost:8200"
JAVA_OPTS="$JAVA_OPTS -Delastic.apm.application_packages=org.jboss.as.quickstarts.helloworld"
JAVA_OPTS="$JAVA_OPTS -Delastic.apm.log_level=DEBUG"
JAVA_OPTS="$JAVA_OPTS -Delastic.apm.enable_log_correlation=true"
JAVA_OPTS="$JAVA_OPTS -Delastic.apm.log_file=<wfly_home>/standalone/log/apm.log"
```
Run with JDK8.

Original Wildfly-Quickstart readme follows:

---
---
---
---
helloworld: Helloworld Example
===============================
Author: Pete Muir  
Level: Beginner  
Technologies: CDI, Servlet  
Summary: Basic example that can be used to verify that the server is configured and running correctly  
Target Project: WildFly
Source: <https://github.com/wildfly/quickstart/>  

What is it?
-----------

This example demonstrates the use of *CDI 1.1* and *Servlet 3.1* in *JBoss WildFly*.

There is a tutorial for this quickstart in the [Getting Started Developing Applications Guide](https://github.com/wildfly/quickstart/guide/HelloworldQuickstart).

System requirements
-------------------

All you need to build this project is Java 7.0 (Java SDK 1.7) or better, Maven 3.1 or better.

The application this project produces is designed to be run on JBoss WildFly.

 
Configure Maven
---------------

If you have not yet done so, you must [Configure Maven](../README.md#mavenconfiguration) before testing the quickstarts.


Start JBoss WildFly with the Web Profile
-------------------------

1. Open a command line and navigate to the root of the JBoss server directory.
2. The following shows the command line to start the server with the web profile:

        For Linux:   JBOSS_HOME/bin/standalone.sh
        For Windows: JBOSS_HOME\bin\standalone.bat

 
Build and Deploy the Quickstart
-------------------------

_NOTE: The following build command assumes you have configured your Maven user settings. If you have not, you must include Maven setting arguments on the command line. See [Build and Deploy the Quickstarts](../README.md#buildanddeploy) for complete instructions and additional options._

1. Make sure you have started the JBoss Server as described above.
2. Open a command line and navigate to the root directory of this quickstart.
3. Type this command to build and deploy the archive:

        mvn clean package wildfly:deploy

4. This will deploy `target/wildfly-helloworld.war` to the running instance of the server.


Access the application 
---------------------

The application will be running at the following URL: <http://localhost:8080/wildfly-helloworld>.


Undeploy the Archive
--------------------

1. Make sure you have started the JBoss Server as described above.
2. Open a command line and navigate to the root directory of this quickstart.
3. When you are finished testing, type this command to undeploy the archive:

        mvn wildfly:undeploy


Run the Quickstart in JBoss Developer Studio or Eclipse
-------------------------------------
You can also start the server and deploy the quickstarts from Eclipse using JBoss tools. For more information, see [Use JBoss Developer Studio or Eclipse to Run the Quickstarts](../README.md#useeclipse) 


Debug the Application
------------------------------------

If you want to debug the source code or look at the Javadocs of any library in the project, run either of the following commands to pull them into your local repository. The IDE should then detect them.

        mvn dependency:sources
        mvn dependency:resolve -Dclassifier=javadoc
