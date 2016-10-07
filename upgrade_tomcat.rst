.. _upgrade-tomcat:

Upgrading COLLATE using Tomcat
==============================

Before upgrading the web application, COLLATE’s Oracle database must be upgraded, and COLLATE artifacts must be updated. 
For more information, see :ref:`upgrade-the-database` and :ref:`update-artifacts`.

This section describes the process of upgrading a deployment of the COLLATE web application using Apache Tomcat. 
After reading this document, you will know the steps involved in updating artifacts, installing the latest .war file, and creating/uploading an application context (.xml) file.

.. tip::
   For the version of Apache Tomcat supported, see :ref:`environment-prerequisites`. 


Installing the latest COLLATE .war file on your Tomcat application server
--------------------------------------------------------------------------

.. note::
   At this point, Tomcat should not be running (the first step of uninstalling the COLLATE .war file was to shut down Tomcat).

#. Move the latest COLLATE .war file to the *webapps* folder of your Apache Tomcat installation.

#. Start Tomcat using the *tomcat\_home/bin/startup.bat* or *tomcat\_home/bin/startup.sh* command.

Confirming deployment
---------------------

To check that you have successfully installed the web application, navigate to your Tomcat web server address. If the deployment has been successful, COLLATE is live.

Troubleshooting
---------------


Validating the database version on start-up
-------------------------------------------

If, following an upgrade in a Tomcat or WebSphere environment, the COLLATE login screen does not display at start-up, check product.log. If there is an issue with your database version not being compatible with the newly deployed .war file, a message similar to that below displays.

.. code:: 

    SEVERE: Exception sending context initialized event to listener instance of class org.springframework.web.context.ContextLoaderListener
    org.springframework.beans.factory.BeanCreationException: Error creating bean with name 'flywayDBValidator' defined in class path resource [appContext.xml]: Invocation of init method failed; nested exception is org.flywaydb.core.api.FlywayException: Validate failed. Detected resolved migration not applied to database...
    .....
    Caused by: org.flywaydb.core.api.FlywayException: Validate failed. Detected resolved migration not applied to database...
    ...

To validate the database version, do the following:
    
#. Ensure the COLLATE database is up-to-date.

#. Stop the COLLATE .war file.

#. Start the COLLATE .war file again.


