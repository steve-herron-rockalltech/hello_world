.. _uninstall-war-file:

Uninstalling your COLLATE .war file
====================================

Before updating artifacts, uninstall the current .war file.

Uninstalling your COLLATE .war file on a Tomcat application server
------------------------------------------------------------------

Before :ref:`update-artifacts`, uninstall the COLLATE .war file currently uploaded by moving it to a backup directory/folder.

#. Stop Tomcat, using the *tomcat_home/bin/shutdown.bat* or *tomcat_home/bin/shutdown.sh* command.

#. Create a backup directory/folder in the *webapps* directory/folder of your Apache Tomcat installation.

#. Move the COLLATE .war file, and COLLATE folder, from the *webapps* directory/folder, to the new backup directory/folder.

Uninstalling your COLLATE .war file on a WebLogic application server
---------------------------------------------------------------------

Before :ref:`update-artifacts`, use a **Delete** button in the WebLogic Server UI to uninstall the COLLATE .war file currently uploaded.

#. Log in to your WebLogic Server administrative console.

#. On the side tab, click **Deployments**.

#. Select the checkbox for the COLLATE .war file.

#. Click **Stop** and select **Force Stop Now**.

   .. image:: /deployment_and_configuration/images/weblogic_upgrade_stop_15_5_war_file.png

#. Click **Yes** to confirm the stopping of the application.
   After stopping the application, WebLogic displays a value of *Prepared* in the **State** column.

#. Select the checkbox for your current .war file again and click
   **Delete**.

#. Click **Lock and Edit**.

#. Click **Delete** to uninstall the .war file

#. Click **Yes** to confirm the uninstall.

#. To save all changes, click **Activate Changes** (in the **Change Center** section).



Uninstalling your COLLATE .war file  on a WebSphere application server
-----------------------------------------------------------------------

Before :ref:`update-artifacts`, stop the application and then uninstall the COLLATE .war file currently uploaded.

#. Select the checkbox beside the COLLATE .war file.

#. Click **Stop**.
   When the application has stopped, a red cross displays in the *Application Status* column (see image below).

   .. image:: /deployment_and_configuration/images/websphere_upgrade_stop_application_message.png

#. Select the checkbox beside the COLLATE .war file.

#. Click **Uninstall**, and then click **OK**.
   When the .war file has been uninstalled, a message similar to the following displays:

   .. image:: /deployment_and_configuration/images/ websphere_upgrade_uninstall_message.png


#. Click the **Save** link save changes to the master configuration.