.. _update-artifacts:   
   
Updating artifacts (application server)
==============================================

Before upgrading the web application, you must update artifacts previously configured. The following artifacts are required for upgrading COLLATE 16.4 to COLLATE 16.5:

*license.zip*
   Contains the license file for COLLATE. 
      
*server-config.properties*
   The configuration file which defines details of schema, configSetId, directory locations of license.zip and validation.zip, and other configuration settings.

*validation.zip*
   Contains drools rules required for validating COLLATE. 
 
.. note::
   The current COLLATE .war file (containing resources that together constitute the COLLATE web application) is also shipped with the artifacts described above. For information on reinstalling the .war file, see :ref:`upgrade-tomcat`, :ref:`upgrade-weblogic`, or :ref:`deploy-using-WebSphere`. 


.. _update-server-config-properties:   
   
Updating your copy of *server-config.properties* (application server)
----------------------------------------------------------------------------

The latest version of *server-config.properties* includes a number of updates.
You must update your copy of *server-config.properties* to replicate this latest version.

#. Open your copy of *server-config.properties* on the application server.

#. Open *server-config.properties* (from the folder it was copied to) and complete the edits detailed below.

   .. code-block:: properties
      :linenos:
      :emphasize-lines: 32, 33
   
      schema={application_user_schema_name} 
      bankCode=N
      authenticateUsingDirectory=false
      ldapUseSearchAccount=false
      ldapProviderUrl=ldap://100.1.1.5:389/
      ldapUseSsl=false
      ldapSearchAccountDN=LDAPTEST@Rockall.dub
      ldapSearchAccountPW=password
      ldapSearchContext=DC=Rockall,DC=dub
      ldapUniqueSearchAttribute=sAMAccountName
      createUserBasedOnSSO=false
      licenseFile=.../collate_home/licence/licence.stoc 
      configSetId={BKAndBank} 
      useIBMSecurityLogout=false
      contextMenuEnabled=true
      validationRulesFolder=.../collate_home/validation
      httpHeaderUsername=SM_UNIVERSALID
      ssoActive=false
      preValidationActive=false
      log4jFileLocation=.../collate_home/config/log4j.xml
      # document and template locations
      fileOutputType=PDF 
      fileOutputDirectory=.../collate_home/uploaded-files/files
      templateDirectory=.../collate_home/doc-generation/templates
      documentReportDirectory=.../collate_home/doc-generation/documents
      elasticsearchHostname=100.1.1.210 
      elasticsearchClustername=RockallElastic
      migrateDatabaseOnStartUp=false
      logoutURLRedirect=https://www.google.ie
      securityPolicyFileName=rockall-policy-strict.xml
      baseCurrency=EUR
      collateralValuationTemplateName=Valuation_doc_clt.docx
      marketValuationTemplateName=Valuation_doc_mkt.docx
      
          
   .. note:: 
       
      Line 32: Check that the value set for the **collateralValuationTemplateName** variable matches the template to be used for reporting on collateral valuations. The default template defined here is one of the templates extracted from *static-doc-templates.zip*. For more information, see :ref:`copy-valuation-templates-for-upgrade`.
      
      Line 33: Check that the value set for the **marketValuationTemplateName** variable matches the template to be used for reporting on market valuations. The default template defined here is one of the templates extracted from *static-doc-templates.zip*. For more information, see :ref:`copy-valuation-templates-for-upgrade`.

#. Save changes and close your *server-config.properties* file.

.. tip::
   If you have followed recommendations associated with the previous COLLATE deployment(s), your copy of *server-config.properties* 
   is stored in *…​collate_home/config*. For an illustration of directories/folders suggested for configuration files, 
   and other artifacts, see :ref:`suggested-file-locations`.  

.. _copy-valuation-templates-for-upgrade:

Copying valuation templates (application server)
-------------------------------------------------
   
Extract *valuation_doc_clt.docx* and *valuation_doc_mkt.docx* from *static-doc-templates.zip* to a directory/folder on the application server. 
Rockall Tecknologies recommends extracting these templates to *…​collate_home/doc-generation/templates* on the application server. 
For an illustration of suggested file locations, see :ref:`suggested-file-locations`.

.. note::
   Ensure these templates are stored in the same location as defined for the *templateDirectory* variable in *server-config.properties* 
   (see :ref:`server-config-properties`).
   
   
.. _update-license-validation-files: 

Updating license and validation files (application server)
------------------------------------------------------------

Between releases of COLLATE, changes have been made to licensing and validation files. So that licensing and validation is up-to-date for your latest deployment of COLLATE, do the following: 

#. Extract *license.stoc* from *license.zip* to a directory/folder on the application server.

   .. tip::
      If you have followed recommendations associated with the previous COLLATE deployment(s), your license file is stored in  *…​collate_home/license*. For an illustration of suggested file locations, see :ref:`suggested-file-locations`.

#. Extract the artifacts from *validation.zip*.

   #. Replace all of your core validation files with the core files shipped with the latest release of COLLATE.
   #. Review all of your customised validation files, and update the .drl file(s) as required.
   
   .. tip::
      To help identify updates required, see the changes summarized in :ref:`appendix-C`.
      
   .. tip::
      If you have followed recommendations associated with the previous COLLATE deployment(s), your validation files are stored in sub-directories/sub-folders of *…​collate_home/validation*. For an illustration of suggested file locations, see :ref:`suggested-file-locations`.
   
