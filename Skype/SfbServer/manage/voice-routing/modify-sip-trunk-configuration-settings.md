---
title: "Skype for Business ServerModify SIP trunk configuration settings"
ms.reviewer: 
ms.author: v-cichur
author: cichur
manager: serdars
audience: ITPro
ms.topic: article
ms.prod: skype-for-business-itpro
f1.keywords:
- NOCSH
ms.localizationpriority: medium
description: "SIP trunk configuration settings define the relationship and capabilities between a Mediation Server and the public switched telephone network gateway, an IP-public branch exchange (PBX), or a Session Border Controller (SBC) at the service provider. "
---

# Skype for Business ServerModify SIP trunk configuration settings

SIP trunk configuration settings define the relationship and capabilities between a Mediation Server and the public switched telephone network (PSTN) gateway, an IP-public branch exchange (PBX), or a Session Border Controller (SBC) at the service provider. These settings do such things as specify:

- Whether media bypass should be enabled on the trunks.
- The conditions under which real-time transport control protocol (RTCP) packets are sent.
- Whether or not secure real-time protocol (SRTP) encryption is required on each trunk.

When you install Skype for Business Server, a global collection of SIP trunk configuration settings is created for you. In addition, administrators can create custom setting collections at the site scope or at the service scope (for the PSTN gateway service, only). Any of these collections can later be modified using either the Skype for Business Server Control Panel or Windows PowerShell.

When modifying SIP trunk configuration settings using the Skype for Business Server Server Control Panel, the following options are available to you:

|UI Setting |PowerShell Parameter |Description |
|--|--|--|
|Name|Identity|Unique identifier for the collection. This property is read-only; you cannot change the Identity of a collection of trunk configuration settings.|
|Description|Description|Provides a way for administrators to store addition information about the settings (for example, the purpose of the trunk configuration).|
|Maximum early dialogs supported|MaxEarlyDialogs|The maximum number of forked responses a PSTN gateway, IP-PBX, or SBC at the service provider can receive to an Invite that it sent to the Mediation Server.|
|Encryption support level|SRTPMode|Indicates the level of support for protecting media traffic between the Mediation Server and the PSTN Gateway, IP-PBX, or SBC at the service provider. For media bypass cases, this value must be compatible with the EncryptionLevel setting in the media configuration. Media configuration is set by using the New-CsMediaConfiguration and Set-CsMediaConfiguration cmdlets.<br/>Allowed values are:<br/><br/>**Required**: SRTP encryption must be used.<br/>**Optional**: SRTP will be used if the gateway supports it.<br/>**Not Supported**: SRTP encryption is not supported and therefore will not be used.<br/><br/>SRTPMode is used only if the gateway is configured to use Transport Layer Security (TLS). If the gateway is configured with Transmission Control Protocol (TCP) as the transport, SRTPMode is internally set to Not Supported.|
|Refer support|Enable3pccRefer<br/>EnableReferSupport|If set to **Enable sending refer to the gateway**, indicates that the trunk supports receiving Refer requests from the Mediation Server.<br/>If set to **Enable refer using third-party call control**, indicates that the 3pcc protocol can be used to allow transferred calls to bypass the hosted site. 3pcc is also known as "third party control," and occurs when a third-party is used to connect a pair of callers (for example, an operator placing a call from person A to person B).|
|Enable media bypass|EnableBypass|Indicates whether media bypass is enabled for this trunk. Media bypass can only be enabled if **Centralized media processing** is also enabled.|
|Centralized media processing|ConcentratedTopology|Indicates whether there is a well-known media termination point. (An example of a well-known media termination point would be a PSTN gateway where the media termination has the same IP as the signaling termination.)|
|Enable RTP latching|EnableRTPLatching|Indicates whether or not the SIP trunks support RTP latching. RTP latching is a technology that enables RTP/RTCP connectivity through a NAT (network address translator) device or firewall.|
|Enable forward call history|ForwardCallHistory|Indicates whether call history information will be forwarded through the trunk.|
|Enable forward P-Asserted-Identity data|ForwardPAI|Indicates whether the P-Asserted-Identity (PAI) header will be forwarded along with the call. The PAI header provides a way to verify the identity of the caller.|
|Enable outbound routing failover timer|EnableFastFailoverTimer|Indicates whether outbound calls that are not answered by the gateway within 10 seconds will be routed to the next available trunk; if there are no additional trunks then the call will automatically be dropped. In an organization with slow networks and gateway responses, that could potentially result in calls being dropped unnecessarily.|
|Associated PSTN usages|PSTNUsages|Collection of PSTN usages assigned to the trunk.|
|Translated number to test|N/A|Phone number that can be used to do an ad hoc test of the trunk configuration settings.|
|Associated translation rules|OutboundTranslationRulesList|Collection of phone number translation rules that apply to calls handled by Outbound Routing (calls routed to PBX or PSTN destinations).|
|Called number translation rules|OutboundCallingNumberTranslationRulesList|Collection of outbound calling number translation rules assigned to the trunk.|
|Phone number to test|N/A|Phone number that can be used to do an ad hoc test of the translation rules.|
|Calling number|N/A|Indicates that the phone number to test is the phone number of the caller.|
|Called number|N/A|Indicates that the phone number to test is the phone number of the person being called.|
|||

> [!Note]
> The Skype for Business Server CsTrunkConfiguration cmdlets support additional properties not shown in the Skype for Business Server Control Panel. For more information, see the help topic for the [Set-CsTrunkConfiguration](/powershell/module/skype/Set-CsTrunkConfiguration) cmdlet. 

**To modify SIP trunk configuration settings by using the Skype for Business Server Control Panel**

1. In the Skype for Business Server Control Panel, click **Voice Routing**, and then click **Trunk Configuration**.
2. On the **Trunk Configuration** tab, double-click the trunk configuration settings to be modified. Note that you can only edit one collection of settings at a time. If you would like to make the same changes on multiple collections, use Windows PowerShell instead.
3. In the **Edit Trunk Configuration** dialog box, make the appropriate selections and then click **OK**.
4. The State property for the collection will be updated to Uncommitted. To commit the changes, and to delete the collection, click **Commit**, and then click **Commit All**.
5. In the **Uncommitted Voice Configuration Setting**s dialog box, click **OK**.
6. In the **Skype for Business Server Control Panel** dialog box, click **OK**.
