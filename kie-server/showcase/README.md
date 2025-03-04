Drools KIE Server showcase Docker image
=======================================

Drools KIE Server showcase [Docker](http://docker.io/) image.

More information of KIE Server available at [JBoss documentation](http://docs.jboss.org/drools/release/7.52.0.Final/drools-docs/html_single/#_ch.kie.server).

Table of contents
------------------

* Introduction
* Usage
* Users and roles
* Logging
* Extending this image
* Experimenting
* Notes
* Release notes

Introduction
------------

The image contains: 
              
* JBoss Wildfly 19.1.0.Final
* JBoss Drools KIE Server 7.52.0.Final

This is a **ready to run Docker image for Drools KIE Server**. Just run it and try the Drools runtime execution server!                   

Usage
-----

The JBoss KIE Execution server is intended to be used as a standalone runtime execution environment managed by a KIE Drools Workbench or a jBPM Workbench application that acts as a controller.             

Once having a KIE Drools Workbench or a jBPM Workbench application container running, you can run several execution server instances linked with your workbench by running:                                 
    
    # NOTE: Consider 'drools-wb' as the name of your Drools workbench running container.     
    docker run -p 8180:8080 -d --name kie-server --link drools-wb:kie-wb jboss/kie-server-showcase:latest

Note: Port `8080` is bind to port `8180` on the docker host considering that `drools-wb` container is already using it.         
 
As in the above example, the use of the link alias `kie-wb` produces:               
  
* Use of your `drools-wb` container as the controller for the execution server.                     
* The repository in the Maven settings, for consuming your artifacts from the `drools-wb` container, is automatically set.                    

So at the point the execution server container is up and running, this server instance will be automatically detected and available in your Drools/jBPM Workbench application, so you can deploy and run your application rules, etc into it.                 

For more information, please read the documentation at [Installing the KIE Server](http://docs.jboss.org/drools/release/7.52.0.Final/drools-docs/html_single/#_installing_the_kie_server).

Once container and web applications started, the application is available at:              

    http://localhost:8180/kie-server

The **REST API service** is located at:               

    http://localhost:8180/kie-server/services/rest/server/

Users and roles
----------------

This image provides a default user `kieserver` using password `kieserver1!` and with the role `kie-server`.                      

Logging
-------

You can see all logs generated by the `standalone` binary running:

    docker logs [-f] <container_id>
    
You can attach the container by running:

    docker attach <container_id>

The Drools KIE Server web application logs can be found inside the container at path:

    /opt/jboss/wildfly/standalone/log/server.log

    Example:
    sudo nsenter -t $(docker inspect --format '{{ .State.Pid }}' $(docker ps -lq)) -m -u -i -n -p -w
    -bash-4.2# tail -f /opt/jboss/wildfly/standalone/log/server.log


Experimenting
-------------

To spin up a shell in one of the containers try:

    docker run -t -i -p 8080:8080 jboss/kie-server-showcase:latest /bin/bash

You can then noodle around the container and run stuff & look at files etc.

Notes
-----

* The context path for Drools KIE Server application services is `kie-server`
* Drools KIE Server version is `7.52.0.Final`
* In order to perform container linking with a jBPM / Drools Workbench image, the link alias must be `kie-wb`       
* No support for clustering                
* This image is not intended to be run on cloud environments such as RedHat OpenShift or Amazon EC2, as it does not meet all the requirements.                      
* Please give us your feedback or report a issue at [Drools Setup](https://groups.google.com/forum/#!forum/drools-setup) or [Drools Usage](https://groups.google.com/forum/#!forum/drools-usage) Google groups.              

Release notes
-------------

**7.52.0.Final**

* See release notes for [KIE-server](https://docs.jboss.org/drools/release/7.52.0.Final/drools-docs/html_single/index.html#_ch.kie.server)
