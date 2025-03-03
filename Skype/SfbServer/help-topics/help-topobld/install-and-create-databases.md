---
title: "Install and Create Databases"
ms.reviewer: 
ms.author: v-cichur
author: cichur
manager: serdars
ms.date: 11/17/2018
audience: ITPro
ms.topic: article
f1.keywords:
- CSH
ms.custom:
- ms.lync.tb.InstallDatabaseCreateDatabasePage
ms.prod: skype-for-business-itpro
ms.localizationpriority: medium
ms.assetid: 515754ad-1344-42dc-8219-ee973de2e4c4
description: "You select the databases that you want to create for your deployment. By default, the database will be created on the defined SQL Server in the defined site, and will automatically deploy and configure the database files based on the SQL Server you are placing the databases on."
---

# Install and Create Databases

You select the databases that you want to create for your deployment. By default, the database will be created on the defined SQL Server in the defined site, and will automatically deploy and configure the database files based on the SQL Server you are placing the databases on.

 **Select the databases you want to create**: Select the checkbox of any databases that you intend to deploy and configure. Select the check box of any or all databases that you will deploy.

> [!CAUTION]
> The SQL Server must already have been configured for the instance (if any) and firewall ports must be opened to accommodate the instance that you are deploying the databases to. For details, see [Configure SQL Server for Lync Server 2013 Preview](/previous-versions/office/lync-server-2013/lync-server-2013-configure-sql-server-for-lync-server)

 **Advanced**: Click on the SQL Server and click the **Advanced** button to choose options for the database file locations on your SQL Server. For details on advanced database file placement, see [Database Installation Using Lync Server Management Shell](/previous-versions/office/lync-server-2013/lync-server-2013-database-installation-using-lync-server-management-shell)

 **Back**: Clicking this button returns you to the previous screen (may not always be available, based on how you arrived at this dialog).

 **Next**: Clicking this button commits your selection on the current dialog and takes you to the next dialog for configuring additional information

 **Cancel**: Clicking this button will quit the configuration and discard your changes. Some, but not all configuration screens will prompt you if you want to quit and discard your changes. Selecting **Yes** will close the current configuration and close the current configuration and return you to Topology Builder. Selecting **No** will return you to the current configuration dialog and allow you to continue the configuration.

 **Help**: Clicking the **Help** button displays this help information associated with the current configuration dialog.