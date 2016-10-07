.. _upgrade-unified-search:

Upgrading the Unified Search service (search server)
***********************************************************

.. important::
   The COLLATE_HOME environment variable must be set on the search server. For information see :ref:`set-COLLATE_HOME`.  

After confirming that the COLLATE_HOME environment variable has been set on the search server, and before deploying the latest .war file, update artifacts for the COLLATE web application.


Updating artifacts (search server)
=========================================

The following artifacts are required for upgrading the Unified Search service.

*license.zip*
   Contains the license file for COLLATE. 
      
*server-config.properties*
   The configuration file which defines details of schema, configSetId, directory locations of license.zip and validation.zip, and other configuration settings.
   
*validation.zip*
   Contains drools rules required for validating COLLATE. 
   

For a summary of changes to all artifacts since the previous release of COLLATE, see :ref:`appendix-B`.

.. _update-license-validation-files-search-server:

Updating license and validation files (search server)
------------------------------------------------------------

Between releases of COLLATE, changes have been made to licensing and validation files. For information on updating your license file and validation files on the search server, see similar steps laid out in :ref:`update-license-validation-files`.

.. _update-server-config-properties-search-server:

Updating your copy of *server-config.properties* (search server)
-----------------------------------------------------------------------

Between releases of COLLATE, changes have been made to *server-config.properties*. For details of edits required for *server-config.properties* on the search server, see similar steps laid out in :ref:`update-server-config-properties`.

.. _set-security-policy-content-search-server:


Re-indexing the Unified Search service
=======================================

The Unified Search service index is queried by COLLATE’s Unified Search functionality. 
After upgrading COLLATE, re-index the Unifield Search Service. To re-index the Unified Search service, do the following:

#. After updating the artifacts for the search server, stop the COLLATE Application server.

#. Remove the previous COLLATE index by doing one of the following:

   *  For a Windows environment, start Powershell from the **Run**
      command, and run the following command:

      .. code:: 
         
         $webclient = New-Object system.net.webclient
         $result=$webclient.UploadString("http://<Elastic search ip/hostname>:<port>/collate","DELETE","0")

   *  For a UNIX/LINUX environment, run the following command:

      .. code:: 
      
         curl -XDELETE 'http://<Elastic search ip/hostname>:<port>/collate'

#. Re-index the Unified Search service :sup:`[forinfo]`.

#. Install the .war file updated in step 4 :sup:`[forinfo]`.


.. rubric:: Increasing memory allocated to the Elasticsearch server

Rockall Technologies recommends that the server on which the Unified Search service is installed must have least 4GB of RAM allocated to it. To allocate RAM, do the following:

#. Stop the Elasticsearch server.

#. Set the environment variables to 4GB each.

   ::

       ES_MIN_MEM=4g
       ES_MAX_MEM=4g

#. Start the Elasticsearch server.



