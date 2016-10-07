.. _upgrade-web-application:

Upgrading the COLLATE web application (application server)
*****************************************************************

Having updated artifacts on your application server (see :ref:`update-artifacts`), you can deploy the COLLATE web application.

.. important::
   The COLLATE_HOME environment variable must be set on the application server. For information, see :ref:`set-COLLATE_HOME`.  

After confirming that the COLLATE_HOME environment variable has been set on the application server, you can perform the upgrade. To successfully upgrade the COLLATE web application, you must install the new .war file on your application server and perform product configuration (see :ref:`appendix-D`).

.. toctree::
   :maxdepth: 2
   
   upgrade_tomcat.rst
   upgrade_weblogic.rst
   upgrade_websphere.rst
