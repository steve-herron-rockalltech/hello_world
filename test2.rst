.. _environment-prerequisites:

Environment prerequisites
*************************

.. note::

   COLLATE has proven to operate successfully using the minimum specifications mentioned here. However, dependent on the volumes of data, and numbers of users to be considered, it may be necessary to scale the infrastructure vertically (additional resources) and/or horizontally (additional servers operating in a cluster).
   
Heading 1 text
**************

Normal text.

.. rubric:: Legal Notice

Normal text.

Heading 2 text
##############

Normal text.

Heading 3 text
==============

Normal text.

Heading 4 text
--------------

Normal text.

Heading 5 text
~~~~~~~~~~~~~~

Normal text.
   
Database server specifications
===============================

The COLLATE web application requires an Oracle database to persist data. Details of the environments certified and supported are as follows:

.. list-table:: 
   :widths: 15 30
   :header-rows: 1

   * - Component
     - Version
   * - Database
     - Oracle Database 11g Release 2 (11.2.0.2.0) Enterprise Edition
   * - CPU
     - Intel Xeon (quad core)
   * - Memory
     - 8GB
   * - Disk
     - 25GB

Web Browser specifications
============================

.. list-table::
   :widths: 30 30 30
   :header-rows: 1

   * - Component
     - Version
     - Support
   * - Browser
     - Internet Explorer 8
     - Partial
   * - Browser
     - Internet Explorer 11
     - Full

Application server specifications
==================================

The COLLATE web application runs within a Java application server. Details of the environments certified and supported are outlined in the following three tables:

Apache Tomcat
-------------

.. list-table::
   :widths: 15 30
   :header-rows: 1

   * - Component
     - Version
   * - Application Server
     - Tomcat 7.0.68
   * - Java JVM
     - Oracle Java SE Runtime Environment (1.7.0_71)
   * - OS
     - Red Hat Enterprise Linux (RHEL) 6.5 
   * - CPU
     - Intel Xeon (quad core)
   * - Memory
     - 8GB
   * - Disk
     - 25GB

     
Oracle WebLogic
----------------

.. list-table::
   :widths: 15 30
   :header-rows: 1

   * - Component
     - Version
   * - Application Server
     - WebLogic Server 12.1.3.0.0
   * - Java JVM
     - Oracle Java SE Runtime Environment (1.7.0_71)
   * - OS
     - Red Hat Enterprise Linux (RHEL) 6.5      
   * - CPU
     - Intel Xeon (quad core)
   * - Memory
     - 8GB
   * - Disk
     - 25GB  
 
IBM WebSphere
----------------

.. list-table::
   :widths: 15 30
   :header-rows: 1

   * - Component
     - Version
   * - Application Server
     - IBM WebSphere 8.5.5.5
   * - Java JVM
     - IBM Java 7.1 (SDK 1.7.1_64)
   * - OS
     - Windows Server 2008 R2 Standard Service Pack 1 64-bit 
   * - CPU
     - Intel Xeon (quad core)
   * - Memory
     - 8GB
   * - Disk
     - 25GB
     
.. note::
   It is recommended that SSL is implemented; several security features of COLLATE rely on SSL being present.

Utility server specifications
==============================

Details of the environments certified and supported are as follows:

.. list-table::
   :widths: 15 30
   :header-rows: 1

   * - Component
     - Version
   * - Java JVM
     - Oracle Java SE Runtime Environment (1.7.0_71)
   * - OS
     - Windows Server 2008 R2 Standard Service Pack 1 64-bit  
   * - OS
     - Red Hat Enterprise Linux 6.5
   * - JDBC Driver
     - Oracle JDBC driver version ojdbc7-12.1.0.1
   * - CPU
     - Intel Xeon (quad core)
   * - Memory
     - 8GB
   * - Disk
     - 25GB
     
Unified Search server specifications
======================================

Details of the environments certified and supported are as follows:

.. list-table::
   :widths: 15 30
   :header-rows: 1

   * - Component
     - Version
   * - `Elasticsearch <https://www.elastic.co/products/elasticsearch>`_   
     - 1.5.2
   * - Java JVM
     - Oracle Java SE Runtime Environment (1.7.0_71)
   * - OS
     - Windows Server 2008 R2 Standard Service Pack 1 64-bit  
   * - OS
     - Red Hat Enterprise Linux 6.5
   * - CPU
     - Intel Xeon (quad core)
   * - Memory
     - 8GB
   * - Disk
     - 25GB
     

     

