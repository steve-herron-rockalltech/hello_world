.. _upgrade-bulk-import:

Upgrading COLLATE Bulk Import (utility server)
*****************************************************

.. important::
   The COLLATE_HOME environment variable must be set on the utility server. For information see 
   :ref:`set-COLLATE_HOME`. 

After confirming that the COLLATE_HOME environment variable has been set on your utility server, update artifacts for the COLLATE Bulk Import application as described here.

Updating artifacts (utility server)
======================================

The following artifacts are required for upgrading COLLATE Bulk Import.

*collate-bulk-import.zip*
   Contains *collate-bulk-import-{version}.jar* (required for upgrading the COLLATE Bulk Import application).

*license.zip*
   Contains the license file for COLLATE. 
     
*server-config.properties*
   The configuration file which defines details of schema, configSetId, directory locations of license.zip and validation.zip, and other configuration settings.
   
*validation.zip*
   Contains drools rules required for validating COLLATE.

For a summary of changes to all artifacts since the previous release of COLLATE, see :ref:`appendix-B`.

.. _update-and-run-bulk-import-jar:

Updating and running *collate-bulk-import-{version}.jar*
--------------------------------------------------------

To upgrade your deployment of COLLATE Bulk Import, update your copy of *collate-bulk-import-{version}.jar*.


#. Extract *collate-bulk-import-{version}.jar* (from *collate-bulk-import.zip*). 

   Rockall Tecknologies recommends extracting *indexer-config.properties* to the *config* directory/folder on the utility server.
   For an illustration of suggested file locations, see :ref:`suggested-file-locations`.

#. Run *collate-cli{version}.jar* (from the location it was extracted to).


.. _update-license-validation-files-utility-server:

Updating license and validation files (utility server)
------------------------------------------------------------

Between releases of COLLATE, changes have been made to licensing and validation files. For information on updating your license file and validation files on the search server, see similar steps laid out in :ref:`update-license-validation-files`.


.. _update-server-config-properties-utility-server:

Updating your copy of *server-config.properties* (utility server)
------------------------------------------------------------------------

Between releases of COLLATE, changes have been made to *server-config.properties*. For details of edits required for *server-config.properties* on the utility server, see similar steps laid out in :ref:`update-server-config-properties`.

