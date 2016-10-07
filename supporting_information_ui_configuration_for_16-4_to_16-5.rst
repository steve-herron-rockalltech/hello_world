UI configuration associated with upgrading COLLATE 16.4 to COLLATE 16.5 
###########################################################################

.. note:: 
   The code documented in this section is required by customers consuming COLLATE via the UI.

Changes have been made since the release of COLLATE 16.4 which affect post-upgrade configuration required. Entities/screens affected, as a result of continued development, are outlined below; code required for configuration is displayed thereafter.

Address 
   An **Add Address Wizard** is now available when recording address details for legal entities and facilities. For details of the code required to make screen elements visible in the UI, and for details of permissions associated with the address wizard functionality, see :ref:`configure-address-wizard-functionality`.

Tasks
   A **Saved Filters** field, and **Clear Filters** / **Save Filter** buttons have been added to the **Global Tasks** dashboard (on the **Tasks** tab); these features now make it possible to create task filters for use in task searches. Task graph functionality has been enhanced in that different task statuses are represented by different colors. For details of the code required to make screen elements visible in the UI, and for details of permissions associated with task functionality, see :ref:`configure-tasks-functionality`.

Valuations
   Valuations functionality has been enhanced in that it is now possible to mark the status of a valuation as being **invalid**, on the **Valuations** tab. On this tab, it is also now possible to mark a valuation as being **stale**. On the **Valuations** tab for a ``Portfolio``, a **download** link is available (after generating a valuation with log). This new link allows users to download a MARKET valuation report and COLLATERAL valuation report outlining the variables in these calculations. For details of permissions associated with valuations functionality, see :ref:`configure-valuations-functionality`.
   
.. note::
   Where the **VISIBLE_STATE** value is used in a package, ensure you include the following statement:  

.. code:: sql

   declare
   VISIBLE_STATE VARCHAR2(10) DEFAULT 'VISIBLE';

.. note::
   Where the **EDIT_DISABLED_STATE** value is used in a package, ensure you include the following statement:  

.. code:: sql

   declare
   EDIT_DISABLED_STATE VARCHAR2(10) DEFAULT 'EDITDSBD';

.. note::
   Where **<role code>** is used, insert a role for which permission is being granted, for example <FULL_ROLE>. 

.. _configure-address-wizard-functionality:

Configuring the Add Address Wizard  
************************************

Granting permissions to one or more roles
==========================================

So that one or more roles have access to address wizard functionality, run the following commands (for each role that  requires the functionality):

.. code-block:: sql
   :linenos:
   
   PKG_RCK_BUILD_UTILS.add_permission_to_role('exposureAddressCancel', <role_code>);
   PKG_RCK_BUILD_UTILS.add_permission_to_role('exposureAddressStep1Show', <role_code>);
   PKG_RCK_BUILD_UTILS.add_permission_to_role('exposureAddressStep1Next', <role_code>);
   PKG_RCK_BUILD_UTILS.add_permission_to_role('exposureAddressStep2Show', <role_code>);
   PKG_RCK_BUILD_UTILS.add_permission_to_role('exposureAddressStep2Generate', <role_code>);
   PKG_RCK_BUILD_UTILS.add_permission_to_role('exposureAddressStep2Finish', <role_code>);
   PKG_RCK_BUILD_UTILS.add_permission_to_role('legalEntityAddressCancel', <role_code>);
   PKG_RCK_BUILD_UTILS.add_permission_to_role('legalEntityAddressStep1Show', <role_code>);
   PKG_RCK_BUILD_UTILS.add_permission_to_role('legalEntityAddressStep1Next', <role_code>);
   PKG_RCK_BUILD_UTILS.add_permission_to_role('legalEntityAddressStep2Show', <role_code>);
   PKG_RCK_BUILD_UTILS.add_permission_to_role('legalEntityAddressStep2Generate', <role_code>);
   PKG_RCK_BUILD_UTILS.add_permission_to_role('legalEntityAddressStep2Finish', <role_code>);

Configuring screen elements 
============================

So that the **Country** dropdown displays on step 1 of the wizard (the **Choose Country** screen), run the following commands:

.. code-block:: sql
   :linenos:   
   
   PKG_RCK_BUILD_UTILS.add_product_conf (2, 'address.cou3chrCd', 'LegalEntityAddressStep1', VISIBLE_STATE);
   PKG_RCK_BUILD_UTILS.add_product_conf (2, 'address.cou3chrCd', 'ExposureAddressStep1', VISIBLE_STATE);

So that the new **Latitude** and **Longitude** fields display on step 2 of the wizard (the **Create Address** screen), run the following commands:

.. code-block:: sql
   :linenos:
   
   PKG_RCK_BUILD_UTILS.add_product_conf (2, 'address.latitude', 'Address', VISIBLE_STATE);
   PKG_RCK_BUILD_UTILS.add_product_conf (2, 'address.longitude', 'Address', VISIBLE_STATE);
 
So that other (country-specific) fields display on step 2 of the wizard (the **Create Address** screen), run the following commands:

.. code-block:: sql
   :linenos:
   
   PKG_RCK_BUILD_UTILS.add_product_conf (2, 'address.adminAreaL1', 'Address', VISIBLE_STATE);
   PKG_RCK_BUILD_UTILS.add_product_conf (2, 'address.adminAreaL2', 'Address', VISIBLE_STATE);
   PKG_RCK_BUILD_UTILS.add_product_conf (2, 'address.adminAreaL3', 'Address', VISIBLE_STATE);
   PKG_RCK_BUILD_UTILS.add_product_conf (2, 'address.adminAreaL4', 'Address', VISIBLE_STATE);
   PKG_RCK_BUILD_UTILS.add_product_conf (2, 'address.adminAreaL5', 'Address', VISIBLE_STATE);
   PKG_RCK_BUILD_UTILS.add_product_conf (2, 'address.locality', 'Address', VISIBLE_STATE);
   PKG_RCK_BUILD_UTILS.add_product_conf (2, 'address.subLocalityL1', 'Address', VISIBLE_STATE);
   PKG_RCK_BUILD_UTILS.add_product_conf (2, 'address.subLocalityL2', 'Address', VISIBLE_STATE);
   PKG_RCK_BUILD_UTILS.add_product_conf (2, 'address.subLocalityL3', 'Address', VISIBLE_STATE);
   PKG_RCK_BUILD_UTILS.add_product_conf (2, 'address.subLocalityL4', 'Address', VISIBLE_STATE);
   PKG_RCK_BUILD_UTILS.add_product_conf (2, 'address.subLocalityL5', 'Address', VISIBLE_STATE);
   PKG_RCK_BUILD_UTILS.add_product_conf (2, 'address.subLocalityL6', 'Address', VISIBLE_STATE);
   PKG_RCK_BUILD_UTILS.add_product_conf (2, 'address.thoroughfareNumber', 'Address', VISIBLE_STATE);
   PKG_RCK_BUILD_UTILS.add_product_conf (2, 'address.thoroughfareName', 'Address', VISIBLE_STATE);
   PKG_RCK_BUILD_UTILS.add_product_conf (2, 'address.premise', 'Address', VISIBLE_STATE);
   PKG_RCK_BUILD_UTILS.add_product_conf (2, 'address.subPremiseL1', 'Address', VISIBLE_STATE);
   PKG_RCK_BUILD_UTILS.add_product_conf (2, 'address.subPremiseL2', 'Address', VISIBLE_STATE);
   PKG_RCK_BUILD_UTILS.add_product_conf (2, 'address.subPremiseL3', 'Address', VISIBLE_STATE);
   PKG_RCK_BUILD_UTILS.add_product_conf (2, 'address.postBox', 'Address', VISIBLE_STATE);
   
.. note:: 
   To use these country-specific fields, you must configure them by updating the *ADDRESS_COUNTRY_FIELD*. For more information, see :ref:`configure-country-specific-address-fields`.
   
So that the **Formatted Address Template** field displays on the **Country** maintenance screen, run the following command:

.. code-block:: sql
   :linenos:
   
   PKG_RCK_BUILD_UTILS.add_product_conf (2, 'country.formattedAddrTemplate', 'Country', VISIBLE_STATE);
   
.. _configure-tasks-functionality:

Configuring tasks
********************

Granting permissions to one or more roles
==========================================

So that one or more roles have access to task status color functionality, run the following command (for each role that requires it):

.. code-block:: sql
      
   PKG_RCK_BUILD_UTILS.add_permission_to_role('taskStatusesMap', <role code>);

.. note::

   FULL roles and INQUIRY roles, must have access to the 'taskStatusesMap' action.
   
So that one or more roles have access to creating/deleting task filters, run the following command (for each role that requires it): 

.. code-block:: sql
   :linenos:
   
   PKG_RCK_BUILD_UTILS.add_permission_to_role('addTaskFilter', <role_code>);
   PKG_RCK_BUILD_UTILS.add_permission_to_role('taskFilterList', <role_code>);
   PKG_RCK_BUILD_UTILS.add_permission_to_role('deleteTaskFilter', <role_code>);
   
.. _configure-valuations-functionality:   
  
Configuring valuations 
***********************

Granting permissions to one or more roles
==========================================

So that one or more roles have access to changing the status of valuations, run the following command (for each role that requires it):

.. code-block:: sql
      
   PKG_RCK_BUILD_UTILS.add_permission_to_role('invalidateValuationAction', <role_code>);
   
.. note::
   The *LK_VALUATION_STATUS* table has been added to the COLLATE database to record the status of valuations.
   
So that one or more roles are able to set valuations to **stale**, run the following command (for each role that requires it):

.. code-block:: sql
      
   PKG_RCK_BUILD_UTILS.add_permission_to_role('staleValuationAction', <role_code>);  

So that one or more roles have access to the **download** link, run the following command (for each role that requires it):

.. code-block:: sql
      
   PKG_RCK_BUILD_UTILS.add_permission_to_role('valuationReportDownload', <role_code>);   

.. note::
   For further configuration required, see updates required for *server-config.properties* in .
