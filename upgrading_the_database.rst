.. _upgrade-the-database:

Upgrading the COLLATE database on the database server
*****************************************************

About the COLLATE database
==========================

Rockall Technologies recommends using a dual schema setup for COLLATE deployment. Using this approach, the two schemas are:

*  Owner schema

*  Application user schema

The owner schema owns the COLLATE database objects and the COLLATE data. This schema must always be locked, 
except when a deployment is taking place.

The application user schema does not own any data or database objects. This schema has the following privileges:

*  *Read* access for tables and views in the owner schema

*  *Execute* access privileges for code in the owner schema

The COLLATE application user uses the application user schema to read COLLATE data and execute COLLATE database code. 
The application user schema is always unlocked. Both schemas are installed on an Oracle relational database. 
The Oracle database can run on Windows and/or supported versions of UNIX/Linux.

.. rubric:: Pre-installation notes

*  Standard provisioning procedures should be followed according to your IT guidelines. 
   COLLATE has no specific requirements in relation to partitioning.

*  The schemas to be used must be allocated at least 2GB for tablespace.

*  TEMP and UNDO tables must have similar tablespace provision.

.. important::
   Before running the scripts required to upgrade the database, Rockall Technologies recommends that you perform a 
   full database backup. If an error occurs during the upgrade process, a full database backup is required for restoring your database.  

The script parameters used during an upgrade are described here:

[application\_user\_schema]
   The database user to which COLLATE connects.
[application\_user\_schema\_password] 
   Password for the schema application user.
[owner\_schema] 
   The schema to which the database will be installed.
[owner\_schema\_password] 
   Password for the schema owner.
[owner\_schema\_role] 
   The role to be created for the owner schema and granted to the application user. 

Unlocking the owner schema and granting privileges
==================================================


Before attempting to upgrade database components, unlock the owner schema and grant privileges.

#. Connect to the Oracle server as Oracle.

   .. code:: sql
   
      sqlplus [sys]/[oracle]@database host name as sysdba

#. Unlock the owner schema.

   .. code:: sql
      
      ALTER USER [owner_schema] ACCOUNT UNLOCK;

#. Grant DBA privileges.

   .. code:: sql
   
      GRANT DBA TO [owner_schema];

#. Exit.

   .. code:: sql
   
      EXIT;

Performing customer-specific, pre-installation cleanup
======================================================

To address potential conflict of metadata codes (delivered in the latest COLLATE release), run the following command (from *db-pre-installer-config*).

#. Connect to the Oracle server as [OWNER\_SCHEMA].

   .. code:: sql
   
      sqlplus [OWNER_SCHEMA]/[OWNER_SCHEMA PASSWORD]@database host name

#. Once connected, run the following query.

   .. code:: sql
   
      @install.sql

#. Exit.

   .. code:: sql
   
      EXIT;

Upgrading the database
======================

As part of a COLLATE release, Rockall Technologies ships *db-installer.zip*. *db-installer.zip* contains the database scripts required to create the database objects and populate preset metadata. Use these scripts to upgrade the database from a previous version. For details of all artifacts shipped, see :ref:`appendix-B`.

.. important::
   JRE must be present on the same system where you are running data migration scripts, and JRE\_HOME must be set. 
   Also, when transferring files (for example, with FTP), and extracting the contents of .zip files, always do so while connected 
   to the database server as the Oracle user. 

.. tip::
   Open a command line tool to execute scripts extracted from .zip files. 

Extracting installation files and setting database details
----------------------------------------------------------

#. While connected to the database server as the Oracle user, copy *db-installer.zip* to a directory/folder on the database server.

#. Extract all files.

   The contents of *db-installer.zip* extract as shown below.

   .. image:: /deployment_and_configuration/images/dbinstaller_contents.png

#. Open *conf/db.conf* to set the following database details:

   #. Set the jdbc url to be used to connect to the database - flyway.url=jdbc:oracle:thin:@//localhost:1521/stoc - replacing **localhost:1521** with your database server host name or IP address, and replace **stoc** with your SID.

   #. Set the user to be used to connect to the database - flyway.user=<SCHEMA USERNAME> - replacing **<SCHEMA USERNAME>** with the name of your owner schema.

   #. Set the user password to be used to connect to the database - flyway.password=<SCHEMA PASSWORD> - replacing **<SCHEMA PASSWORD>** with your owner schema password.

#. Close *conf/db.conf* and save changes.

Running installation scripts to upgrade the database
--------------------------------------------------------

.. note::
   Before running the database (db) scripts, ensure that both database and flyway scripts have adequate execute permissions assigned. 

To upgrade database components, do the following:


#. To confirm what’s going to be updated, run one of the following commands:

   *  *db-status.bat* (for a Windows environment).
   *  *db-status.sh* (for a Linux environment).
   
   After running one of the above commands, an overview of items installed, and items pending installation, is displayed (see example below).

   .. image:: /deployment_and_configuration/images/dbstatus_before_16-3_to_16-4_upgrade.png

#. To run all required installation scripts, run one of the following commands:

   *  *db-install.bat* (for a Windows environment).
   *  *db-install.sh* (for a Linux environment).

#. When prompted **"Are you sure you want to run this database install [y/n] (default - n)?:"**, 
   enter **y** to continue with the installation, or enter **n** to cancel.

   .. important::
      Flyway will report whether any database object includes errors/is in an error state. If an error is reported, restore the database from backup, and contact Rockall Technologies for support. 

#. To see an overview of successfully installed components, run one of the following commands:

*  Run *db-status.bat* (for a Windows environment).
*  Run *db-status.sh* (for a Linux environment).

   .. image:: /deployment_and_configuration/images/dbstatus_success_16_3_to_16_4.png

.. note::
   Flyway software is shipped with the COLLATE release. For details of the associated license, see https://github.com/flyway/flyway/blob/master/LICENSE.  

Installing customer-specific, post-installation configuration data
==================================================================

To install customer-specific configuration data, do the following:

#. Connect to the Oracle server as the owner schema.

   .. code:: sql
   
      sqlplus [owner_schema]/[owner_schema_password]@database host name

#. Create context.

   .. code:: sql
   
      @schema_utilities/create_context.sql [application_user_schema];

#. Exit.

   .. code:: sql
   
      EXIT;

#. Navigate to *db-post-installer-config*.

#. Connect to the Oracle server as the owner schema.

#. Once connected, run the following command to install the configuration data required.

   .. code:: sql
   
      @install.sql

#. Exit.

   .. code:: sql
   
      EXIT;

Amending privileges
===================

After installing database components and sample data, amend DBA privileges.

#. Connect to the Oracle server as Oracle.

   .. code:: sql
   
      sqlplus [sys]/[oracle]@database host name as sysdba

#. Amend privileges.

   .. code:: sql
   
      REVOKE DBA FROM [owner_schema];
      GRANT CREATE SESSION, CONNECT, RESOURCE, UNLIMITED TABLESPACE TO [owner_schema];

#. Exit.

   .. code:: sql
      
      EXIT;

Granting privileges
===================

#. Connect to the Oracle server as the schema owner and grant privileges to the owner schema role.

   .. code:: sql
      
      3sqlplus [owner schema]/[owner schema password]@database host name
      @schema_utilities/apply_grant.sql [owner user schema role]

#. Exit.

   .. code:: sql
   
      EXIT;

Creating synonyms for the application user schema and locking the owner schema
==============================================================================

#. Connect to the Oracle server as the application user schema and create synonyms for the application user schema.

   .. code:: sql
   
      sqlplus [application_user_schema]/[application user schema password]@database host name
      @schema_utilities/create_synonym.sql [owner_schema]

#. Exit.

   .. code:: sql
   
      EXIT;

#. Connect to the Oracle server as the Oracle user and lock the owner schema.

   .. code:: sql
      
      sqlplus [sys]/[oracle]@database host name as sysdba
      ALTER USER [owner_schema] ACCOUNT LOCK;
      
#. Exit.

   .. code:: sql
   
      EXIT;

.. tip::
   For information on changes to the database model, since the previous release of COLLATE, see :ref:`appendix-A`. 

