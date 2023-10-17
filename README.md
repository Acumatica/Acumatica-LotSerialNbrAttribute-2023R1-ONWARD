[![Project Status](http://opensource.box.com/badges/active.svg)](http://opensource.box.com/badges)

Adding Attribute Support to Lot/Serial Number
==================================
Acumatica ERP lets you define attributes for flexible, meaningful classification of an Entity (Lead, Stock/Non-Stock Items Etc.) as required for your company's specific needs. An attribute is a property that enables you to specify additional information for Entity in the system. 

This extension allows to add attribute support to Lot/Serial Number so that each Lot/Serial Number's unique characteristic (Example – color variation, stone pattern etc. in case of Granite Slab) can be tracked. With this extension, you can:

* View Lot/Serial numbers in listing Screen (IN2025LS)
* Define numeric type (Integer and Decimal) of controls for Attributes (CS205000)
* Define attributes to be tracked for each Lot/Serial class
* Assign attribute values, Manufacturing Lot/Serial number while receiving items via Allocations dialog in Inventory Receipt (IN301000), Purchase Receipt (PO302000) and Move (AM302000) Screens
* Assign attribute values and image for individual Lot/Serial Number (IN202501) 
* Assign description, detailed description, Sales Price, MSRP and E-Commerce settings at individual Lot/Serial Number (IN202501); values will be defaulted from Stock Item during receiving process
* Bulk assignment of attribute values via Import Scenario
* Access custom Web Services Endpoint (eCommerceLotSerial) exposing Lot/Serial Screen (IN202501)
* Search and allocate Lot/Serial Number by attribute value/s in Sales Order (SO301000) and Material (AM300000) Screens

### Prerequisites
* Acumatica 2023 R1 (23.104.0030 or higher) [2023 R1 Deployment Package](https://github.com/Acumatica/Acumatica-LotSerialNbrAttribute-2023R1-ONWARD/tree/2023R1)
* Acumatica 2023 R2 (23.200.0136 or higher) [2023 R2 Deployment Package](https://github.com/Acumatica/Acumatica-LotSerialNbrAttribute-2023R1-ONWARD/tree/2023R2)

Quick Start
-----------

### Installation

##### Install customization deployment package
1. Download **PXLotSertialNbrAttributeExtPkg.zip** from respective branch.
2. In your Acumatica ERP instance, navigate to System -> Customization -> Customization Projects (SM204505), import PXLotSertialNbrAttributeExtPkg.zip as a customization project
3. Publish customization project.

### Migrating from https://github.com/Acumatica/Acumatica-LotSerialNbrAttribute solution:
You need to execute below SQL Script. We recommend you to verify solution in Sandbox environment prior using in production environment. 
 
   	UPDATE CSAttributeGroup 
   	SET EntityType = 'PX.LotSerialNbrAttribute.Ext.INItemLotSerialInfo' 
   	WHERE EntityType = 'PX.LotSertialNbrAttribute.Ext.UsrInventoryLotSerialContainer' 
   	GO 
   	UPDATE INItemLotSerial 
   	SET NoteID = UsrInventoryLotSerialContainer.NoteId 
   	FROM INItemLotSerial 
	  	INNER JOIN UsrInventoryLotSerialContainer 
	  	ON  UsrInventoryLotSerialContainer.CompanyID = INItemLotSerial.CompanyID 
	  	AND UsrInventoryLotSerialContainer.InventoryID = INItemLotSerial.InventoryID 
	  	AND UsrInventoryLotSerialContainer.LotSerialNbr = INItemLotSerial.LotSerialNbr 
   
### Usage

1. Go to Attributes Screen (CS205000) and create new attributes if you need to. You can create attribute/s with numeric control types (Integer and Decimal) as well.

   <img src="/_ReadMeImages/Image0-CS205000.png" width=60% height=60%>

2. Navigate to Lot/Serial classes Screen (IN207000) and select the class for which you need to specify list of Attributes.

   <img src="/_ReadMeImages/Image1-IN207000.PNG" width=70% height=70%>

3. Navigate to Stock Item Screen (IN202500) and create a new Stock Item having Lot/Serial class created in Step # 2.
4. Create Purchase Order (PO301000) for Stock Item created in Step # 3. And move forward with creating Purchase Receipt (PO302000) for this Purchase Order.
5. Click on Allocations button, you should be able to see Attributes specified in Step # 2 and can specify value for them. Also, you can specify value for Mfg Lot/Serial as well.
6. **Apply Attribute from First** button copies attribute values specified for very first Lot/Serial Number and applies to rest of the Lot/Serial Number displayed in the dialog. One can specify value for each individual Lot/Serial Number as well.

   <img src="/_ReadMeImages/Image2-PO302000.PNG">
   
8. Attribute value can be assigned similarly for Lot/Serial Number while receiving inventory using Receipt (IN301000) and Move (AM302000) Screens as well via Allocations dialog.
9. **Lot/Serial** screen (IN202501) can be used to assign Attribute values, image, description, detailed description, Sales Price, MSRP and E-Commerce settings at individual Lot/Serial Number (IN202501); values are defaulted from Stock Item (IN202500) during receiving process

    <img src="/_ReadMeImages/Image3-IN202501-1.PNG">

10. **Lot/Serial** screen (IN202501) can be used to view information like Warehouse, Location, Created With, Assigned To, Cost, Price Sold For and history.

    <img src="/_ReadMeImages/Image3-IN202501-2.PNG">

11. Attribute values can be imported via **Import Lot/Serial Attributes** custom import scenario available via customization package.

    <img src="/_ReadMeImages/Image4-SM206025.PNG">
    
    <img src="/_ReadMeImages/Image5-SM206036.PNG">

12. Lot/Serial Screen (IN202501) is available for REST API via custom Web Services Endpoint (eCommerceLotSerial)

13. **Add Item Lot/Serial** option can be utilized to search Lot/Serial Number by attribute value and allocate in Sales Order (SO301000) and Material (AM300000) Screens. Columns for Attribute/s will be dynamically added.
    
    <img src="/_ReadMeImages/Image5-SO301000-1.PNG">
    
    <img src="/_ReadMeImages/Image5-SO301000-2.PNG">

Known Issues
------------
1. Attributes having numeric control type (Integer or Decimal) are not supported as User defined fields (UDF) at present

Source Code
------------
Contact Acumatica customization team for additional feature to be developed by community members for consideration to be part of general availability of this customization via submitting a [New Customization Request Case](https://portal.acumatica.com/Main?ScreenId=SP203006).

For customer specific additional feature; a second level of customization must be created on top of this customization by referencing extension library. 

Support and Maintenance
------------
Acumatica will provide upgraded package within 90 days of each major release. If you require package to be upgraded prior to this release schedule then annual customization maintenance plan is required.

Assistance with setup, training, troubleshooting issues with this customization requires annual customization maintenance plan. Contact Acumatica customization team by submitting a [New Customization Request Case](https://portal.acumatica.com/Main?ScreenId=SP203006).

Additional Feature Request
------------
Please submit a [New Customization Request Case](https://portal.acumatica.com/Main?ScreenId=SP203006) to determine effort and cost.

## Copyright and License

Copyright © `2023` `Acumatica`

This component is licensed under the GPL-3.0 License, a copy of which is available online [here](LICENSE)
