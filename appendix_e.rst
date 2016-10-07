.. _appendix-E:

Appendix E - Web service changes associated with upgrading COLLATE 16.4 to COLLATE 16.5
##########################################################################################

Changes have been made since the release of COLLATE 16.4 which affect post-upgrade configuration required. Web services affected as a result of continued development, are outlined below; code required for configuration is displayed thereafter.

Web services updated
*********************

Updates have been made to web services since the the release of COLLATE 16.4. These updates are summarized below:

*AddressCreate*
   The following optional fields have been added to request and response messages: *adminAreaL1*, *adminAreaL2*, *adminAreaL3*, *adminAreaL4*, *adminAreaL5*, *locality*, *subLocalityL1*, *subLocalityL2*, *subLocalityL3*, *subLocalityL4*, *subLocalityL5*, *subLocalityL6*, *thoroughfareNumber*, *thoroughfareName*, *premise*, *subPremiseL1*, *subPremiseL2*, *subPremiseL3*, *postBox*, *longitude*, and *latitude*.
   
*AddressRead*
   The following optional fields have been added to response messages: *adminAreaL1*, *adminAreaL2*, *adminAreaL3*, *adminAreaL4*, *adminAreaL5*, *locality*, *subLocalityL1*, *subLocalityL2*, *subLocalityL3*, *subLocalityL4*, *subLocalityL5*, *subLocalityL6*, *thoroughfareNumber*, *thoroughfareName*, *premise*, *subPremiseL1*, *subPremiseL2*, *subPremiseL3*, *postBox*, *longitude*, and *latitude*.

*ValuationCreate*
   The following mandadory fields have been added to response messages: *id*, *tcn* and *stale* (if the valuation is stale).
   
*ValuationRead*
   The following mandadory fields have been added to response messages: *id*, *tcn* and *stale* (if the valuation is stale).

New web services 
******************************

New web services have been shipped since the release of COLLATE 16.4. The names of the new web services are list below, along with supporting action required to consume the new web services.

*InvalidateValuation*
   Use the *invalidateValuationOperation* operation to update a valuation status to invalid (using *valuationId* and *tcn*). To consume this web service, run the command documented for the *InvalidateValuation* web service in :ref:`enabling-users-to-run-valuations-web-services`.
   
*StaleValuation*
   Use the *staleValuationOperation* operation to update an valuation to **stale** using *valuationId* and *tcn*.  To consume this web service, run the command documented for the *StaleValuation* web service in :ref:`enabling-users-to-run-valuations-web-services`.

.. note::

   Where **<role code>** is used, insert the role for which permission is being granted.  
 
Valuations web services
===========================

.. _enabling-users-to-run-valuations-web-services:
 
Granting permission to a role
------------------------------

So that one or more roles have access to the *InvalidateValuation* web service, run the following command (for each role that requires it):


.. code-block:: sql
   :linenos:
   
   PKG_RCK_BUILD_UTILS.add_permission_to_role('InvalidateValuation', <role_code>);
  
So that one or more roles have access to the *StaleValuation* web service, run the following command (for each role that requires it):


.. code-block:: sql
   :linenos:
     
   PKG_RCK_BUILD_UTILS.add_permission_to_role('StaleValuation', <role_code>);




   



   
   

