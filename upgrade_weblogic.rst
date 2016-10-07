.. _upgrade-weblogic:

Upgrading COLLATE using WebLogic
================================

Before upgrading the web application, COLLATE’s Oracle database must be upgraded, and COLLATE artifacts must be updated. 
For more information, see :ref:`upgrade-the-database` and :ref:`update-artifacts`.

This section describes the process of upgrading a deployment of the COLLATE web application using 
WebLogic Server Administration Console. After reading this document, you will know the steps involved in updating artifacts 
and installing the latest .war file.

.. tip::
   For the version of WebLogic supported, see :ref:`environment-prerequisites`. 


Deploying COLLATE in Production mode
------------------------------------

When performing either a greenfield or an upgrade deployment of COLLATE, in a WebLogic environment, 
ensure that WebLogic is set to operate in *Production mode*, even if the deployment is just to test the COLLATE application.


Setting WebLogic to operate in Production mode
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

To set the Weblogic application server to operate in production mode, run one of the following commands:

.. rubric:: Command for LINUX environments

.. code:: 

    nohup $DOMAIN_HOME/startWebLogic.sh production &

.. rubric:: Command for Windows environments

.. code:: 

    start %DOMAIN_HOME%\startWebLogic.cmd production


Installing the latest COLLATE .war file on your WebLogic application server
----------------------------------------------------------------------------

#. On the side tab, click **Deployments**.

#. Click **Take Lock and Edit** (in the **Change Center** section).

#. Click **Install**.

   .. image:: /deployment_and_configuration/images/weblogic_installing_war_file.png

#. On the **Locate deployment to install and prepare for deployment** screen, complete the **Path** field by clicking 
   **upload your file(s)** to browse for the .war file to be uploaded.
   
   (Use the **Deployment Archive:** section of **Upload a deployment to the Administration server Archive:**.)

#. Select the radio button representing the required .war file and click **Next**.

#. On the **Choose targeting style** screen, ensure the install as an application radio button is selected and 
   click **Next**.

#. On the **Select deployment targets** screen, select the checkbox for **Adminserver**.

#. On the **Optional Settings** screen, review the default settings and click **Next**.

#. Review the **Summary** screen and click **Finish** if no changes are required.

#. When the .war file has been successfully deployed, click **Activate Changes** (in the **Change Center** section) to 
   save all changes.
   
   At this point, WebLogic displays a value of *Prepared* in the **State** column and a value of *OK* in 
   the **Health** column.

#. Select the COLLATE application and click **Start** and select
   **Servicing all requests**.

#. Click **Yes** to confirm start.

   At this point, WebLogic displays a value of *Active* in the **State** column and a value of *OK* in the **Health** column.

#. Stop the Weblogic application server via command line by logging onto the application server and running one 
   of the following commands:

   .. code:: 

       cd $DOMAIN_HOME/bin
       nohup sh stopWebLogic.sh &

   or

   .. code:: 

       cd %DOMAIN_HOME%\bin
       stopWebLogic.cmd

#. Restart the Weblogic application server via command line by logging onto the application server and running one 
   of the following commands:

   .. code:: 

       nohup $DOMAIN_HOME/startWebLogic.sh production &

   or

   .. code:: 

       start %DOMAIN_HOME%\startWebLogic.cmd production

Confirming deployment
---------------------

To check that you have successfully installed the web application, go to the URL defined for the COLLATE web application.

