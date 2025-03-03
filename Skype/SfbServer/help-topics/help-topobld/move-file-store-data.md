---
title: "Move File Store Data to a New File Store in Skype for Business Server 2015"
ms.reviewer: 
ms.author: v-cichur
author: cichur
manager: serdars
ms.date: 8/30/2016
audience: ITPro
ms.topic: article
ms.prod: skype-for-business-itpro
f1.keywords:
- NOCSH
ms.localizationpriority: medium
ms.assetid: 8d1d5819-add2-4f5d-a436-74c00a281df0
description: "If you need to remove the file server that is currently acting as the file store for your Skype for Business Server 2015 deployment, or if you need to make other changes that would make the current file store unavailable, you first need to create a new share. Then you need to perform the following steps:"
---

# Move File Store Data to a New File Store in Skype for Business Server 2015

If you need to remove the file server that is currently acting as the file store for your Skype for Business Server 2015 deployment, or if you need to make other changes that would make the current file store unavailable, you first need to create a new share. Then you need to perform the following steps:

1. Shut down the Skype for Business Server 2015 services that use the file store that you plan to remove.

2. Define the file store in Topology Builder and publish the changes to make the new file store available to your deployment.

3. Move the data to the new file store.

4. Restart the servers or services.

5. Optionally, remove the old file share and file folder.

### To move file store data from one file store to a new file store

1. Log on to a computer as a member of the RTCUniversersalServerAdmins or CsServerAdministrator group where the Skype for Business Server 2015, Administrative Tools are installed.

2. Open a browser window, and then enter the Admin URL to open the Skype for Business Server Control Panel.

3. In the left navigation bar, click **Topology**, and then click **Status**.

4. For each Director pool, Director, Standard Edition server, and Front End pool that uses the file store that you plan to remove, select the server or pool, click **Action**, and then click **Stop all services**.

5. Log on to the computer where Topology Builder is installed as a member of the Domain Admins group and the RTCUniversalServerAdmins group.

6. Start Topology Builder: Click **Start**, click **All Programs**, click **Skype for Business Server 2015**, and then click **Skype for Business Server 2015Topology Builder**.

7. Select a server or pool that uses the file store, and do the following:

8. Right-click the server or pool, and then click **Edit Properties**.

9. In **Edit properties**, under **Associations**, under **File store**, click **New**.

10. In **Define New File Store**, under **File server FQDN**, type the fully qualified domain name (FQDN) of the file server. Under **File share**, type the folder name for the new file share, and then click **OK**.

     > [!IMPORTANT]
     > This step defines a new file store for use in Topology Builder. You define it only once, not for each server. Before you publish the topology, you must create the defined file share on the defined file server. For details, see [Define the File Store for the Front End](/previous-versions/office/communications/gg133895(v=ocs.14)).

11. For each server or pool that uses the file store, do the following:

12. Right-click the server or pool, and then click **Edit properties**.

13. In **Edit Properties**, under **Associations**, in **File store**, select the new file share, and then click **OK**.

14. Publish the topology, check replication status, and then run the Skype for Business Server Deployment Wizard as needed. For details, see [Common Procedures for Removing Lync Servers and Components](/previous-versions/office/skype-server-2010/gg195688(v=ocs.14)).

15. Start a command prompt: Click **Start**, click **Run**, and then type cmd.exe.

16. At the command line, type the following:

    ```console
    Robocopy \\<OldFileServer>\<OldShare> \\<NewFileServer>\<NewShare> /S /R:10 /W:10 /XF Meeting.Active /MT /LOG:<directory path\logname>
    ```

    > [!TIP]
    > The /S switch copies over files, directories and subdirectories. The /XF switch skips any files that are named Meeting.Active. Current versions of the robocopy.exe with the /MT switch greatly increase copy speed by using multiple threads. For the /LOG switch, use a directory path and log file name in the form of C:\Logfiles\log.txt. This switch creates a log file of operations at the named location.

17. When the data copy is complete, in Lync Server Control Panel, click **Topology**, and then click **Status**.

18. For each server or pool where you stopped services, select the server or pool, click **Action**, and then click **Start all services**.

19. Remove the old file store from the topology and then publish the topology. For details, see [Remove a file store](/previous-versions/office/skype-server-2010/gg195635(v=ocs.14)).

20. (Optional) Log on to the computer that contains the file store that you just removed as a member of the local Administrators group or the Domain Admins group, and then remove the old file share and directory.

## See also

[Reassign a Server to a Different File Store](/previous-versions/office/skype-server-2010/gg195633(v=ocs.14))

[Remove a file store](/previous-versions/office/skype-server-2010/gg195635(v=ocs.14))