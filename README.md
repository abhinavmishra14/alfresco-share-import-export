# Alfresco-Share Import Export AddOn (AIO Project - SDK 4.1) 
 
"Import/Export ACP Tool" for Alfresco Share
================================

This extension allows you to **import** and **export** ACP files from Share UI (you can also import (and extract) ZIP files).  

Building the module
-------------------
Check out the project if you have not already done so 

        git clone https://github.com/abhinavmishra14/alfresco-share-import-export.git
        
Switch to SDK 4.1 branch: 
          
        git fetch && git checkout sdk4.1 

Run with `./run.sh build_start` or `./run.bat build_start` and verify that it

 * Runs Alfresco Content Service (ACS)
 * Runs Alfresco Share
 * Runs Alfresco Search Service (ASS)
 * Runs PostgreSQL database
 * Deploys the JAR assembled modules
 
All the services of the project are now run as docker containers. The run script offers the next tasks:

 * `build_start`. Build the whole project, recreate the ACS and Share docker images, start the dockerised environment composed by ACS, Share, ASS and 
 PostgreSQL and tail the logs of all the containers.
 * `build_start_it_supported`. Build the whole project including dependencies required for IT execution, recreate the ACS and Share docker images, start the 
 dockerised environment composed by ACS, Share, ASS and PostgreSQL and tail the logs of all the containers.
 * `start`. Start the dockerised environment without building the project and tail the logs of all the containers.
 * `stop`. Stop the dockerised environment.
 * `purge`. Stop the dockerised container and delete all the persistent data (docker volumes).
 * `tail`. Tail the logs of all the containers.
 * `reload_share`. Build the Share module, recreate the Share docker image and restart the Share container.
 * `reload_acs`. Build the ACS module, recreate the ACS docker image and restart the ACS container.
 * `build_test`. Build the whole project, recreate the ACS and Share docker images, start the dockerised environment, execute the integration tests from the
 `integration-tests` module and stop the environment.
 * `test`. Execute the integration tests (the environment must be already started).


Installing the module
---------------------

####Installing Alfresco Platform module:

1- Navigate to parent pom.xml
2- Execute maven command: `mvn clean install`
3- You can find the 'alfresco-share-import-export-platform' jar file at this path: /alfresco-share-import-export/alfresco-share-import-export-platform-docker/target/extensions/alfresco-share-import-export-platform-1.0-SNAPSHOT.jar
4- Stop the alfresco container 
     
    e.g.: docker-compose -f ./docker-compose.yml kill alfresco-share-import-export-acs
          docker-compose -f ./docker-compose.yml rm -f alfresco-share-import-export-acs
   
5- Copy the jar file to $TOMCAT_DIR/webapps/alfresco/WEB-INF/lib/

    Get container name or short container id:
     - `docker ps`
    Get full container id:
	 - `docker inspect -f '{{.Id}}' CONTAINER_ID`
	 Copy file:
	 - `docker cp localFile FULLCONTAINER_ID:pathOnContainer`
	
	 Example:
	 - `docker cp ./alfresco-share-import-export/alfresco-share-import-export-platform-docker/target/extensions/alfresco-share-import-export-platform-1.0-SNAPSHOT.jar ac23e51fd0b5c4cc11a12133ceea16d603e7f105d8d39873c75d7cfdd5942e40:/usr/local/tomcat/webapps/alfresco/WEB-INF/lib/`

6- Start the alfresco container
   
    e.g.: docker-compose -f ./docker-compose.yml up --build -d alfresco-share-import-export-acs
    
####Installing Share module:

1- Navigate to parent pom.xml
2- Execute maven command: `mvn clean install`
3- You can find the 'alfresco-share-import-export-share' jar file at this path: /alfresco-share-import-export/alfresco-share-import-export-share-docker/target/extensions/alfresco-share-import-export-share-1.0-SNAPSHOT.jar
4- Stop the share container 
      
    e.g.: docker-compose -f ./docker-compose.yml kill alfresco-share-import-export-share
          docker-compose -f ./docker-compose.yml rm -f alfresco-share-import-export-share
   
5- Copy the jar file to $TOMCAT_DIR/webapps/alfresco/WEB-INF/lib/

	 Get container name or short container id:
     - `docker ps`
    Get full container id:
	 - `docker inspect -f '{{.Id}}' CONTAINER_ID`
	 Copy file:
	 - `docker cp localFile FULLCONTAINER_ID:pathOnContainer`
	
	 Example:
	 - `docker cp ./alfresco-share-import-export/alfresco-share-import-export-share-docker/target/extensions/alfresco-share-import-export-share-1.0-SNAPSHOT.jar bc23e51frfr5c4cc11a12133ceea16d603e7f105d8d39873c75d7cfdd5942456:/usr/local/tomcat/webapps/share/WEB-INF/lib/`

6- Start the share container
   
    e.g.: docker-compose -f ./docker-compose.yml up --build -d alfresco-share-import-export-share

Using the module
---------------------
Go to the Share Admin console.  
Export tool (ACP only): `http://server:port/share/page/console/admin-console/export`  
Import tool (ACP and ZIP files): `http://server:port/share/page/console/admin-console/import`  


LICENSE
---------------------
This extension is licensed under `GNU Library or "Lesser" General Public License (LGPL)`.  
Created by: [Julien BERTHOUX] (https://github.com/jberthoux) and [Bertrand FOREST] (https://github.com/bforest)  


Our company
---------------------
[Atol Conseils et Développements] (http://www.atolcd.com) is Alfresco [Gold Partner] (http://www.alfresco.com/partners/atol)  
Follow us on twitter [ @atolcd] (https://twitter.com/atolcd)  