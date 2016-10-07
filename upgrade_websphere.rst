.. _upgrade-websphere:

Upgrading COLLATE using WebSphere
=================================

Before upgrading the web application, COLLATE’s Oracle database must be upgraded, and COLLATE artifacts must be updated. 
For more information, see :ref:`upgrade-the-database` and :ref:`update-artifacts`.

This section describes the process of upgrading a deployment of the COLLATE web application using using WebSphere. 
After reading this document, you will know the steps involved in updating artifacts and installing the latest .war file.

.. tip::
   For the version of WebSphere supported, see :ref:`environment-prerequisites`. 

Before installing the web application, COLLATE’s Oracle database must be . For more information, 
see .

Installing the latest COLLATE .war file on your WebSphere application server
------------------------------------------------------------------------------
 
 
Clearing cache
~~~~~~~~~~~~~~~~

.. important::
   Before installing the latest .war file, stop the application server, clear the cache, then start the application server again. 
   This prevents licensing and caching issues occuring during deployment of the new .war file. 
   
#. Log on to the application server.

#. Click **Start**, select **Administrative Tools**, and click **Services**.

#. Right-click the **IBM WebSphere Application Server {version}** service and select **Stop**.

#. Navigate to where the cache files are located, for example *C:/Windows/Temp*.

#. Delete the files to clear the cache.

#. Delete the existing COLLATE .war deployment folder from *C:/IBM/WebSphere/AppServer/profiles/<server node name>/config/cells/<node cell name>/applications*.
   For example, *C:\\IBM\\WebSphere\\AppServer\\profiles\\AppSrv01\\config\\cells\\EVESPHERENode01Cell\\applications*.
   
#. Return to the **Services** window, right-click the **IBM WebSphere Application Server {version}** 
   service and select **Start**.

.. note::
   If the licensing issue persists, after performing the steps above, reboot the application server machine to ensure the cache 
   is cleared. 

Installing the .war file on WebSphere
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

After clearing the cache, and starting the application server again, you can install the latest .war file.

#. Log in to your WebSphere Application Server administration console.

#. On the side bar, click **Applications** > **Application Types** > **WebSphere enterprise applications**.

#. Click **Install**.

   .. image:: /deployment_and_configuration/images/websphere_install_war_file.png

#. Click a **Browse…** button to select the .war file you want to upload
   and click **Next**.

   .. image:: /deployment_and_configuration/images/websphere_browse_to_war_file.png

#. Select the radio button for the **Fast Path** option and click **Next**.

   .. image:: /deployment_and_configuration/images/websphere_select_fast_path.png

   -  Step 1 - on the **Select installation options** screen, select the
      check box for **Precompile JavaServer Pages files**, complete the
      **Application name** field, and click **Next**.

   -  Step 2 - on the **Map modules to servers** screen, select the
      checkbox for **Rockall Technologies - Collate** and click
      **Next**.

   -  Step 3 - on the **Map resource references to resources** screen,
      click the **Browse…** button for the **Rockall Technologies -
      Collate** module. Select the data source you would like to connect
      to, then click **Apply**. Ensure the checkbox beside **Rockall
      Technologies - Collate** is selected, then click **Next**.

   -  Step 4 - on the **Map virtual hosts for Web modules** screen,
      select the checkbox for **Rockall Technologies - Collate** and
      click **Next**.

   -  Step 5 - on the **Map context roots for web modules** screen,
      click in the **Context root** field and enter the text you want to
      display in the URL and click **Next**. For example, enter
      */COLLATE*.

   -  Step 6 - At the **Summary** screen, read/confirm all details
      entered. Then click **Previous** to edit the settings configured
      in steps 1 to 5, or click **Finish** to return to the **Enterprise
      Applications** screen.

#. Click the **Save** link to save changes to the master configuration.

.. note::
   If any issue relating to licensing issue remains, reboot the application server machine to ensure the cache is cleared. 
   
Setting properties for class loading
------------------------------------

#. On the **Enterprise Applications** screen, click name of your application.

   .. image:: /deployment_and_configuration/images/websphere_select_web_application.png

#. In the **Details Properties** section of the **Configuration** tab, click **Class loading and update detection**.

   .. image:: /deployment_and_configuration/images/websphere_select_class_loading.png

#. In the **Class loader order** section, select the radio button for **Classes loaded with local class loader first (parent last)**.

#. In the **WAR class loader policy** section, select the radio button for **Single class loader for application**.

#. Click **OK**.

#. Click the **Save** link to save changes to the master configuration.
 

Purging previous data source connections
----------------------------------------

.. note::
   To avoid *StaleConnection* errors, when starting the application, ensure you do the following before confirming deployment:  

#. On the side tab, click **JDBC** and select **Data sources**.

   .. image:: /deployment_and_configuration/images/websphere_purge_connection_01.png   

#. On the **Data sources** screen, select the checkbox representing the data source requiring an edit to settings, and click **Manage state…​**.

   .. image:: /deployment_and_configuration/images/websphere_purge_connection_02.png


#. On the **JCA lifecycle management** screen, select the checkbox for the data source connection to be purged.

#. Click **Purge**.

   A message displays indicating that the purge operation was successful.

   .. image:: /deployment_and_configuration/images/websphere_purge_connection_03.png

Confirming deployment
---------------------

To check that you have successfully installed the web application, do the following:

#. On the side bar, click **Applications** > **Application Types** > **WebSphere enterprise applications**.

#. Select the checkbox beside your deployment and click **Start**.

#. Access your deployment with your respective web server name and port numbers.

     

Troubleshooting
---------------

Validating the database version on start-up
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

If, following an upgrade in a Tomcat or WebSphere environment, the COLLATE login screen does not display at start-up, check product.log. If there is an issue with your database version not being compatible with the newly deployed .war file, 
a message similar to that below displays.

.. code:: 

    SEVERE: Exception sending context initialized event to listener instance of class org.springframework.web.context.ContextLoaderListener
    org.springframework.beans.factory.BeanCreationException: Error creating bean with name 'flywayDBValidator' defined in class path resource [appContext.xml]: Invocation of init method failed; nested exception is org.flywaydb.core.api.FlywayException: Validate failed. Detected resolved migration not applied to database...
    .....
    Caused by: org.flywaydb.core.api.FlywayException: Validate failed. Detected resolved migration not applied to database...
    ...

To resolve the validate failed issue, do the following:

#. Ensure the COLLATE database is up-to-date.

#. Stop the COLLATE .war file.

#. Start the COLLATE .war file again.


