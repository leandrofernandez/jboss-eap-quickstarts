mail: E-Mail Example using CDI (Contexts and Dependency Injection) and JSF (JavaServer Faces)
================================================================================================
Author: Joel Tosi  
Level: Beginner  
Technologies: JavaMail, JSF, CDI  
Summary: Demonstrates the use of JavaMail  
Target Product: EAP  
Product Versions: EAP 6.1, EAP 6.2  
Source: <https://github.com/jboss-developer/jboss-eap-quickstarts/>  

What is it?
-----------

This example demonstrates sending email with the use of *CDI 1.0* and *JSF 2.0* in Red Hat JBoss Enterprise Application Platform.

The example uses the default Mail provider that comes out of the box with JBoss EAP. It uses your local mail relay and the default SMTP port of 25.

The configuration of the mail provider is found in the `EAP_HOME/standalone/configuration/standalone.xml` if you are running a standalone server or in the `EAP_HOME/domain/configuration/domain.xml` file if you are running in a managed domain. An example of the mail subsystem XML configuration is provided below:

    <subsystem xmlns="urn:jboss:domain:mail:1.0">
        <mail-session jndi-name="java:jboss/mail/Default" >
            <smtp-server address="localhost" port="25"/>
        </mail-session>
        <mail-session jndi-name="java:/MyOtherMail">
            <smtp-server address="localhost" port="9999">
                <login name="nobody" password="pass"/>
            </smtp-server>
            <pop3-server address="example.com" port="1234"/>
            <imap-server address="example.com" port="432">
                <login name="nobody" password="pass"/>
            </imap-server>
        </mail-session>
    </subsystem>

The example is a web application that takes `To`, `From`, `Subject`, and `Message Body` input and sends mail to that address. The front end is a JSF page with a simple POJO backing, leveraging CDI for resource injection.

System requirements
-------------------

The application this project produces is designed to be run on Red Hat JBoss Enterprise Application Platform 6.1 or later. 

All you need to build this project is Java 6.0 (Java SDK 1.6) or later, Maven 3.0 or later.

 
Configure Maven
---------------

If you have not yet done so, you must [Configure Maven](https://github.com/jboss-developer/jboss-developer-shared-resources/blob/master/guides/CONFIGURE_MAVEN.md#configure-maven-to-build-and-deploy-the-quickstarts) before testing the quickstarts.


Start the JBoss EAP Server
-------------------------

1. Open a command prompt and navigate to the root of the JBoss EAP directory.
2. The following shows the command line to start the server:

        For Linux:   EAP_HOME/bin/standalone.sh
        For Windows: EAP_HOME\bin\standalone.bat

 
Build and Deploy the Quickstart
-------------------------

_NOTE: The following build command assumes you have configured your Maven user settings. If you have not, you must include Maven setting arguments on the command line. See [Build and Deploy the Quickstarts](../README.md#build-and-deploy-the-quickstarts) for complete instructions and additional options._

1. Make sure you have started the JBoss EAP server as described above.
2. Open a command prompt and navigate to the root directory of this quickstart.
3. Type this command to build and deploy the archive:

        mvn clean install jboss-as:deploy

4. This will deploy `target/jboss-mail.war` to the running instance of the server.


Access the application 
---------------------

The application will be running at the following URL: <http://localhost:8080/jboss-mail>. 


Undeploy the Archive
--------------------

1. Make sure you have started the JBoss EAP server as described above.
2. Open a command prompt and navigate to the root directory of this quickstart.
3. When you are finished testing, type this command to undeploy the archive:

        mvn jboss-as:undeploy


Run the Quickstart in JBoss Developer Studio or Eclipse
-------------------------------------
You can also start the server and deploy the quickstarts from Eclipse using JBoss tools. For more information, see [Use JBoss Developer Studio or Eclipse to Run the Quickstarts](https://github.com/jboss-developer/jboss-developer-shared-resources/blob/master/guides/USE_JDBS.md#use-jboss-developer-studio-or-eclipse-to-run-the-quickstarts) 


Debug the Application
------------------------------------

If you want to debug the source code or look at the Javadocs of any library in the project, run either of the following commands to pull them into your local repository. The IDE should then detect them.

        mvn dependency:sources
        mvn dependency:resolve -Dclassifier=javadoc
