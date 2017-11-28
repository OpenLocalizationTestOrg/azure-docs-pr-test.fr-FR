---
title: "aaaAzure haute disponibilité de Machines virtuelles pour SAP NetWeaver | Documents Microsoft"
description: "Guide de haute disponibilité pour SAP NetWeaver sur machines virtuelles Azure"
services: virtual-machines-windows,virtual-network,storage
documentationcenter: saponazure
author: goraco
manager: timlt
editor: 
tags: azure-resource-manager
keywords: 
ms.assetid: 5e514964-c907-4324-b659-16dd825f6f87
ms.service: virtual-machines-windows
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 12/07/2016
ms.author: goraco
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 927409830065573248a43427eb382448ca07b6e4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="high-availability-for-sap-netweaver-on-azure-vms"></a><span data-ttu-id="e0e69-103">Haute disponibilité pour SAP NetWeaver sur des machines virtuelles Azure</span><span class="sxs-lookup"><span data-stu-id="e0e69-103">High availability for SAP NetWeaver on Azure VMs</span></span>

[767598]:https://launchpad.support.sap.com/#/notes/767598
[773830]:https://launchpad.support.sap.com/#/notes/773830
[826037]:https://launchpad.support.sap.com/#/notes/826037
[965908]:https://launchpad.support.sap.com/#/notes/965908
[1031096]:https://launchpad.support.sap.com/#/notes/1031096
[1139904]:https://launchpad.support.sap.com/#/notes/1139904
[1173395]:https://launchpad.support.sap.com/#/notes/1173395
[1245200]:https://launchpad.support.sap.com/#/notes/1245200
[1409604]:https://launchpad.support.sap.com/#/notes/1409604
[1558958]:https://launchpad.support.sap.com/#/notes/1558958
[1585981]:https://launchpad.support.sap.com/#/notes/1585981
[1588316]:https://launchpad.support.sap.com/#/notes/1588316
[1590719]:https://launchpad.support.sap.com/#/notes/1590719
[1597355]:https://launchpad.support.sap.com/#/notes/1597355
[1605680]:https://launchpad.support.sap.com/#/notes/1605680
[1619720]:https://launchpad.support.sap.com/#/notes/1619720
[1619726]:https://launchpad.support.sap.com/#/notes/1619726
[1619967]:https://launchpad.support.sap.com/#/notes/1619967
[1750510]:https://launchpad.support.sap.com/#/notes/1750510
[1752266]:https://launchpad.support.sap.com/#/notes/1752266
[1757924]:https://launchpad.support.sap.com/#/notes/1757924
[1757928]:https://launchpad.support.sap.com/#/notes/1757928
[1758182]:https://launchpad.support.sap.com/#/notes/1758182
[1758496]:https://launchpad.support.sap.com/#/notes/1758496
[1772688]:https://launchpad.support.sap.com/#/notes/1772688
[1814258]:https://launchpad.support.sap.com/#/notes/1814258
[1882376]:https://launchpad.support.sap.com/#/notes/1882376
[1909114]:https://launchpad.support.sap.com/#/notes/1909114
[1922555]:https://launchpad.support.sap.com/#/notes/1922555
[1928533]:https://launchpad.support.sap.com/#/notes/1928533
[1941500]:https://launchpad.support.sap.com/#/notes/1941500
[1956005]:https://launchpad.support.sap.com/#/notes/1956005
[1973241]:https://launchpad.support.sap.com/#/notes/1973241
[1984787]:https://launchpad.support.sap.com/#/notes/1984787
[1999351]:https://launchpad.support.sap.com/#/notes/1999351
[2002167]:https://launchpad.support.sap.com/#/notes/2002167
[2015553]:https://launchpad.support.sap.com/#/notes/2015553
[2039619]:https://launchpad.support.sap.com/#/notes/2039619
[2121797]:https://launchpad.support.sap.com/#/notes/2121797
[2134316]:https://launchpad.support.sap.com/#/notes/2134316
[2178632]:https://launchpad.support.sap.com/#/notes/2178632
[2191498]:https://launchpad.support.sap.com/#/notes/2191498
[2233094]:https://launchpad.support.sap.com/#/notes/2233094
[2243692]:https://launchpad.support.sap.com/#/notes/2243692

[sap-installation-guides]:http://service.sap.com/instguides

[azure-cli]:../../../cli-install-nodejs.md
[azure-portal]:https://portal.azure.com
[azure-ps]:https://docs.microsoft.com/powershell/azureps-cmdlets-docs
[azure-quickstart-templates-github]:https://github.com/Azure/azure-quickstart-templates
[azure-script-ps]:https://go.microsoft.com/fwlink/p/?LinkID=395017
[azure-subscription-service-limits]:../../../azure-subscription-service-limits.md
[azure-subscription-service-limits-subscription]:../../../azure-subscription-service-limits.md

[dbms-guide]:../../virtual-machines-windows-sap-dbms-guide.md
[dbms-guide-2.1]:../../virtual-machines-windows-sap-dbms-guide.md#c7abf1f0-c927-4a7c-9c1d-c7b5b3b7212f
[dbms-guide-2.2]:../../virtual-machines-windows-sap-dbms-guide.md#c8e566f9-21b7-4457-9f7f-126036971a91
[dbms-guide-2.3]:../../virtual-machines-windows-sap-dbms-guide.md#10b041ef-c177-498a-93ed-44b3441ab152
[dbms-guide-2]:../../virtual-machines-windows-sap-dbms-guide.md#65fa79d6-a85f-47ee-890b-22e794f51a64
[dbms-guide-3]:../../virtual-machines-windows-sap-dbms-guide.md#871dfc27-e509-4222-9370-ab1de77021c3
[dbms-guide-5.5.1]:../../virtual-machines-windows-sap-dbms-guide.md#0fef0e79-d3fe-4ae2-85af-73666a6f7268
[dbms-guide-5.5.2]:../../virtual-machines-windows-sap-dbms-guide.md#f9071eff-9d72-4f47-9da4-1852d782087b
[dbms-guide-5.6]:../../virtual-machines-windows-sap-dbms-guide.md#1b353e38-21b3-4310-aeb6-a77e7c8e81c8
[dbms-guide-5.8]:../../virtual-machines-windows-sap-dbms-guide.md#9053f720-6f3b-4483-904d-15dc54141e30
[dbms-guide-5]:../../virtual-machines-windows-sap-dbms-guide.md#3264829e-075e-4d25-966e-a49dad878737
[dbms-guide-8.4.1]:../../virtual-machines-windows-sap-dbms-guide.md#b48cfe3b-48e9-4f5b-a783-1d29155bd573
[dbms-guide-8.4.2]:../../virtual-machines-windows-sap-dbms-guide.md#23c78d3b-ca5a-4e72-8a24-645d141a3f5d
[dbms-guide-8.4.3]:../../virtual-machines-windows-sap-dbms-guide.md#77cd2fbb-307e-4cbf-a65f-745553f72d2c
[dbms-guide-8.4.4]:../../virtual-machines-windows-sap-dbms-guide.md#f77c1436-9ad8-44fb-a331-8671342de818
[dbms-guide-900-sap-cache-server-on-premises]:../../virtual-machines-windows-sap-dbms-guide.md#642f746c-e4d4-489d-bf63-73e80177a0a8

[dbms-guide-figure-100]:media/virtual-machines-shared-sap-dbms-guide/100_storage_account_types.png
[dbms-guide-figure-200]:media/virtual-machines-shared-sap-dbms-guide/200-ha-set-for-dbms-ha.png
[dbms-guide-figure-300]:media/virtual-machines-shared-sap-dbms-guide/300-reference-config-iaas.png
[dbms-guide-figure-400]:media/virtual-machines-shared-sap-dbms-guide/400-sql-2012-backup-to-blob-storage.png
[dbms-guide-figure-500]:media/virtual-machines-shared-sap-dbms-guide/500-sql-2012-backup-to-blob-storage-different-containers.png
[dbms-guide-figure-600]:media/virtual-machines-shared-sap-dbms-guide/600-iaas-maxdb.png
[dbms-guide-figure-700]:media/virtual-machines-shared-sap-dbms-guide/700-livecach-prod.png
[dbms-guide-figure-800]:media/virtual-machines-shared-sap-dbms-guide/800-azure-vm-sap-content-server.png
[dbms-guide-figure-900]:media/virtual-machines-shared-sap-dbms-guide/900-sap-cache-server-on-premises.png

[deployment-guide]:../../virtual-machines-windows-sap-deployment-guide.md
[deployment-guide-2.2]:../../virtual-machines-windows-sap-deployment-guide.md#42ee2bdb-1efc-4ec7-ab31-fe4c22769b94
[deployment-guide-3.1.2]:../../virtual-machines-windows-sap-deployment-guide.md#3688666f-281f-425b-a312-a77e7db2dfab
[deployment-guide-3.2]:../../virtual-machines-windows-sap-deployment-guide.md#db477013-9060-4602-9ad4-b0316f8bb281
[deployment-guide-3.3]:../../virtual-machines-windows-sap-deployment-guide.md#54a1fc6d-24fd-4feb-9c57-ac588a55dff2
[deployment-guide-3.4]:../../virtual-machines-windows-sap-deployment-guide.md#a9a60133-a763-4de8-8986-ac0fa33aa8c1
[deployment-guide-3]:../../virtual-machines-windows-sap-deployment-guide.md#b3253ee3-d63b-4d74-a49b-185e76c4088e
[deployment-guide-4.1]:../../virtual-machines-windows-sap-deployment-guide.md#604bcec2-8b6e-48d2-a944-61b0f5dee2f7
[deployment-guide-4.2]:../../virtual-machines-windows-sap-deployment-guide.md#7ccf6c3e-97ae-4a7a-9c75-e82c37beb18e
[deployment-guide-4.3]:../../virtual-machines-windows-sap-deployment-guide.md#31d9ecd6-b136-4c73-b61e-da4a29bbc9cc
[deployment-guide-4.4.2]:../../virtual-machines-windows-sap-deployment-guide.md#6889ff12-eaaf-4f3c-97e1-7c9edc7f7542
[deployment-guide-4.4]:../../virtual-machines-windows-sap-deployment-guide.md#c7cbb0dc-52a4-49db-8e03-83e7edc2927d
[deployment-guide-4.5.1]:../../virtual-machines-windows-sap-deployment-guide.md#987cf279-d713-4b4c-8143-6b11589bb9d4
[deployment-guide-4.5.2]:../../virtual-machines-windows-sap-deployment-guide.md#408f3779-f422-4413-82f8-c57a23b4fc2f
[deployment-guide-4.5]:../../virtual-machines-windows-sap-deployment-guide.md#d98edcd3-f2a1-49f7-b26a-07448ceb60ca
[deployment-guide-5.1]:../../virtual-machines-windows-sap-deployment-guide.md#bb61ce92-8c5c-461f-8c53-39f5e5ed91f2
[deployment-guide-5.2]:../../virtual-machines-windows-sap-deployment-guide.md#e2d592ff-b4ea-4a53-a91a-e5521edb6cd1
[deployment-guide-5.3]:../../virtual-machines-windows-sap-deployment-guide.md#fe25a7da-4e4e-4388-8907-8abc2d33cfd8

[deployment-guide-configure-monitoring-scenario-1]:../../virtual-machines-windows-sap-deployment-guide.md#ec323ac3-1de9-4c3a-b770-4ff701def65b
[deployment-guide-configure-proxy]:../../virtual-machines-windows-sap-deployment-guide.md#baccae00-6f79-4307-ade4-40292ce4e02d
[deployment-guide-figure-100]:media/virtual-machines-shared-sap-deployment-guide/100-deploy-vm-image.png
[deployment-guide-figure-1000]:media/virtual-machines-shared-sap-deployment-guide/1000-service-properties.png
[deployment-guide-figure-11]:../../virtual-machines-windows-sap-deployment-guide.md#figure-11
[deployment-guide-figure-1100]:media/virtual-machines-shared-sap-deployment-guide/1100-azperflib.png
[deployment-guide-figure-1200]:media/virtual-machines-shared-sap-deployment-guide/1200-cmd-test-login.png
[deployment-guide-figure-1300]:media/virtual-machines-shared-sap-deployment-guide/1300-cmd-test-executed.png
[deployment-guide-figure-14]:../../virtual-machines-windows-sap-deployment-guide.md#figure-14
[deployment-guide-figure-1400]:media/virtual-machines-shared-sap-deployment-guide/1400-azperflib-error-servicenotstarted.png
[deployment-guide-figure-300]:media/virtual-machines-shared-sap-deployment-guide/300-deploy-private-image.png
[deployment-guide-figure-400]:media/virtual-machines-shared-sap-deployment-guide/400-deploy-using-disk.png
[deployment-guide-figure-5]:../../virtual-machines-windows-sap-deployment-guide.md#figure-5
[deployment-guide-figure-50]:media/virtual-machines-shared-sap-deployment-guide/50-forced-tunneling-suse.png
[deployment-guide-figure-500]:media/virtual-machines-shared-sap-deployment-guide/500-install-powershell.png
[deployment-guide-figure-6]:../../virtual-machines-windows-sap-deployment-guide.md#figure-6
[deployment-guide-figure-600]:media/virtual-machines-shared-sap-deployment-guide/600-powershell-version.png
[deployment-guide-figure-7]:../../virtual-machines-windows-sap-deployment-guide.md#figure-7
[deployment-guide-figure-700]:media/virtual-machines-shared-sap-deployment-guide/700-install-powershell-installed.png
[deployment-guide-figure-760]:media/virtual-machines-shared-sap-deployment-guide/760-azure-cli-version.png
[deployment-guide-figure-900]:media/virtual-machines-shared-sap-deployment-guide/900-cmd-update-executed.png
[deployment-guide-figure-azure-cli-installed]:../../virtual-machines-windows-sap-deployment-guide.md#402488e5-f9bb-4b29-8063-1c5f52a892d0
[deployment-guide-figure-azure-cli-version]:../../virtual-machines-windows-sap-deployment-guide.md#0ad010e6-f9b5-4c21-9c09-bb2e5efb3fda
[deployment-guide-install-vm-agent-windows]:../../virtual-machines-windows-sap-deployment-guide.md#b2db5c9a-a076-42c6-9835-16945868e866
[deployment-guide-troubleshooting-chapter]:../../virtual-machines-windows-sap-deployment-guide.md#564adb4f-5c95-4041-9616-6635e83a810b

[deploy-template-cli]:../../../resource-group-template-deploy.md#deploy-with-azure-cli-for-mac-linux-and-windows
[deploy-template-portal]:../../../resource-group-template-deploy.md#deploy-with-the-preview-portal
[deploy-template-powershell]:../../../resource-group-template-deploy.md#deploy-with-powershell

[dr-guide-classic]:http://go.microsoft.com/fwlink/?LinkID=521971

[getting-started]:../../virtual-machines-windows-sap-get-started.md
[getting-started-dbms]:../../virtual-machines-windows-sap-get-started.md#1343ffe1-8021-4ce6-a08d-3a1553a4db82
[getting-started-deployment]:../../virtual-machines-windows-sap-get-started.md#6aadadd2-76b5-46d8-8713-e8d63630e955
[getting-started-planning]:../../virtual-machines-windows-sap-get-started.md#3da0389e-708b-4e82-b2a2-e92f132df89c

[getting-started-windows-classic]:../../virtual-machines-windows-classic-sap-get-started.md
[getting-started-windows-classic-dbms]:../../virtual-machines-windows-classic-sap-get-started.md#c5b77a14-f6b4-44e9-acab-4d28ff72a930
[getting-started-windows-classic-deployment]:../../virtual-machines-windows-classic-sap-get-started.md#f84ea6ce-bbb4-41f7-9965-34d31b0098ea
[getting-started-windows-classic-dr]:../../virtual-machines-windows-classic-sap-get-started.md#cff10b4a-01a5-4dc3-94b6-afb8e55757d3
[getting-started-windows-classic-ha-sios]:../../virtual-machines-windows-classic-sap-get-started.md#4bb7512c-0fa0-4227-9853-4004281b1037
[getting-started-windows-classic-planning]:../../virtual-machines-windows-classic-sap-get-started.md#f2a5e9d8-49e4-419e-9900-af783173481c

[ha-guide-classic]:http://go.microsoft.com/fwlink/?LinkId=613056

[ha-guide]:high-availability-guide.md

[install-extension-cli]:virtual-machines-linux-enable-aem.md

[Logo_Linux]:media/virtual-machines-shared-sap-shared/Linux.png
[Logo_Windows]:media/virtual-machines-shared-sap-shared/Windows.png

[msdn-set-azurermvmaemextension]:https://msdn.microsoft.com/library/azure/mt670598.aspx

[planning-guide]:planning-guide.md
[planning-guide-1.2]:planning-guide.md#e55d1e22-c2c8-460b-9897-64622a34fdff
[planning-guide-11]:planning-guide.md#7cf991a1-badd-40a9-944e-7baae842a058
[planning-guide-11.4.1]:planning-guide.md#5d9d36f9-9058-435d-8367-5ad05f00de77
[planning-guide-11.5]:planning-guide.md#4e165b58-74ca-474f-a7f4-5e695a93204f
[planning-guide-2.1]:planning-guide.md#1625df66-4cc6-4d60-9202-de8a0b77f803
[planning-guide-2.2]:planning-guide.md#f5b3b18c-302c-4bd8-9ab2-c388f1ab3d10
[planning-guide-3.1]:planning-guide.md#be80d1b9-a463-4845-bd35-f4cebdb5424a
[planning-guide-3.2.1]:planning-guide.md#df49dc09-141b-4f34-a4a2-990913b30358
[planning-guide-3.2.2]:planning-guide.md#fc1ac8b2-e54a-487c-8581-d3cc6625e560
[planning-guide-3.2.3]:planning-guide.md#18810088-f9be-4c97-958a-27996255c665
[planning-guide-3.2]:planning-guide.md#8d8ad4b8-6093-4b91-ac36-ea56d80dbf77
[planning-guide-3.3.2]:planning-guide.md#ff5ad0f9-f7f4-4022-9102-af07aef3bc92
[planning-guide-5.1.1]:planning-guide.md#4d175f1b-7353-4137-9d2f-817683c26e53
[planning-guide-5.1.2]:planning-guide.md#e18f7839-c0e2-4385-b1e6-4538453a285c
[planning-guide-5.2.1]:planning-guide.md#1b287330-944b-495d-9ea7-94b83aff73ef
[planning-guide-5.2.2]:planning-guide.md#57f32b1c-0cba-4e57-ab6e-c39fe22b6ec3
[planning-guide-5.2]:planning-guide.md#6ffb9f41-a292-40bf-9e70-8204448559e7
[planning-guide-5.3.1]:planning-guide.md#6e835de8-40b1-4b71-9f18-d45b20959b79
[planning-guide-5.3.2]:planning-guide.md#a43e40e6-1acc-4633-9816-8f095d5a7b6a
[planning-guide-5.4.2]:planning-guide.md#9789b076-2011-4afa-b2fe-b07a8aba58a1
[planning-guide-5.5.1]:planning-guide.md#4efec401-91e0-40c0-8e64-f2dceadff646
[planning-guide-5.5.3]:planning-guide.md#17e0d543-7e8c-4160-a7da-dd7117a1ad9d
[planning-guide-7.1]:planning-guide.md#3e9c3690-da67-421a-bc3f-12c520d99a30
[planning-guide-7]:planning-guide.md#96a77628-a05e-475d-9df3-fb82217e8f14
[planning-guide-9.1]:planning-guide.md#6f0a47f3-a289-4090-a053-2521618a28c3
[planning-guide-azure-premium-storage]:planning-guide.md#ff5ad0f9-f7f4-4022-9102-af07aef3bc92

[planning-guide-figure-100]:media/virtual-machines-shared-sap-planning-guide/100-single-vm-in-azure.png
[planning-guide-figure-1300]:media/virtual-machines-shared-sap-planning-guide/1300-ref-config-iaas-for-sap.png
[planning-guide-figure-1400]:media/virtual-machines-shared-sap-planning-guide/1400-attach-detach-disks.png
[planning-guide-figure-1600]:media/virtual-machines-shared-sap-planning-guide/1600-firewall-port-rule.png
[planning-guide-figure-1700]:media/virtual-machines-shared-sap-planning-guide/1700-single-vm-demo.png
[planning-guide-figure-1900]:media/virtual-machines-shared-sap-planning-guide/1900-vm-set-vnet.png
[planning-guide-figure-200]:media/virtual-machines-shared-sap-planning-guide/200-multiple-vms-in-azure.png
[planning-guide-figure-2100]:media/virtual-machines-shared-sap-planning-guide/2100-s2s.png
[planning-guide-figure-2200]:media/virtual-machines-shared-sap-planning-guide/2200-network-printing.png
[planning-guide-figure-2300]:media/virtual-machines-shared-sap-planning-guide/2300-sapgui-stms.png
[planning-guide-figure-2400]:media/virtual-machines-shared-sap-planning-guide/2400-vm-extension-overview.png
[planning-guide-figure-2500]:media/virtual-machines-shared-sap-planning-guide/2500-vm-extension-details.png
[planning-guide-figure-2600]:media/virtual-machines-shared-sap-planning-guide/2600-sap-router-connection.png
[planning-guide-figure-2700]:media/virtual-machines-shared-sap-planning-guide/2700-exposed-sap-portal.png
[planning-guide-figure-2800]:media/virtual-machines-shared-sap-planning-guide/2800-endpoint-config.png
[planning-guide-figure-2900]:media/virtual-machines-shared-sap-planning-guide/2900-azure-ha-sap-ha.png
[planning-guide-figure-300]:media/virtual-machines-shared-sap-planning-guide/300-vpn-s2s.png
[planning-guide-figure-3000]:media/virtual-machines-shared-sap-planning-guide/3000-sap-ha-on-azure.png
[planning-guide-figure-3200]:media/virtual-machines-shared-sap-planning-guide/3200-sap-ha-with-sql.png
[planning-guide-figure-400]:media/virtual-machines-shared-sap-planning-guide/400-vm-services.png
[planning-guide-figure-600]:media/virtual-machines-shared-sap-planning-guide/600-s2s-details.png
[planning-guide-figure-700]:media/virtual-machines-shared-sap-planning-guide/700-decision-tree-deploy-to-azure.png
[planning-guide-figure-800]:media/virtual-machines-shared-sap-planning-guide/800-portal-vm-overview.png
[planning-guide-microsoft-azure-networking]:planning-guide.md#61678387-8868-435d-9f8c-450b2424f5bd
[planning-guide-storage-microsoft-azure-storage-and-data-disks]:planning-guide.md#a72afa26-4bf4-4a25-8cf7-855d6032157f

[sap-ha-guide]:high-availability-guide.md
[sap-ha-guide-1]:high-availability-guide.md#217c5479-5595-4cd8-870d-15ab00d4f84c
[sap-ha-guide-2]:high-availability-guide.md#42b8f600-7ba3-4606-b8a5-53c4f026da08
[sap-ha-guide-3]:high-availability-guide.md#42156640c6-01cf-45a9-b225-4baa678b24f1
[sap-ha-guide-3.1]:high-availability-guide.md#f76af273-1993-4d83-b12d-65deeae23686
[sap-ha-guide-3.2]:high-availability-guide.md#3e85fbe0-84b1-4892-87af-d9b65ff91860
[sap-ha-guide-4]:high-availability-guide.md#8ecf3ba0-67c0-4495-9c14-feec1a2255b7
[sap-ha-guide-4.1]:high-availability-guide.md#1a3c5408-b168-46d6-99f5-4219ad1b1ff2
[sap-ha-guide-5]:high-availability-guide.md#fdfee875-6e66-483a-a343-14bbaee33275
[sap-ha-guide-5.1]:high-availability-guide.md#be21cf3e-fb01-402b-9955-54fbecf66592
[sap-ha-guide-5.2]:high-availability-guide.md#ff7a9a06-2bc5-4b20-860a-46cdb44669cd
[sap-ha-guide-6]:high-availability-guide.md#2ddba413-a7f5-4e4e-9a51-87908879c10a
[sap-ha-guide-6.1]:high-availability-guide.md#1a464091-922b-48d7-9d08-7cecf757f341
[sap-ha-guide-6.2]:high-availability-guide.md#44641e18-a94e-431f-95ff-303ab65e0bcb
[sap-ha-guide-7]:high-availability-guide.md#2e3fec50-241e-441b-8708-0b1864f66dfa
[sap-ha-guide-7.1]:high-availability-guide.md#93faa747-907e-440a-b00a-1ae0a89b1c0e
[sap-ha-guide-7.2]:high-availability-guide.md#f559c285-ee68-4eec-add1-f60fe7b978db
[sap-ha-guide-7.2.1]:high-availability-guide.md#b5b1fd0b-1db4-4d49-9162-de07a0132a51
[sap-ha-guide-7.3]:high-availability-guide.md#ddd878a0-9c2f-4b8e-8968-26ce60be1027
[sap-ha-guide-7.4]:high-availability-guide.md#045252ed-0277-4fc8-8f46-c5a29694a816
[sap-ha-guide-8]:high-availability-guide.md#78092dbe-165b-454c-92f5-4972bdbef9bf
[sap-ha-guide-8.1]:high-availability-guide.md#c87a8d3f-b1dc-4d2f-b23c-da4b72977489
[sap-ha-guide-8.2]:high-availability-guide.md#7fe9af0e-3cce-495b-a5ec-dcb4d8e0a310
[sap-ha-guide-8.3]:high-availability-guide.md#47d5300a-a830-41d4-83dd-1a0d1ffdbe6a
[sap-ha-guide-8.4]:high-availability-guide.md#b22d7b3b-4343-40ff-a319-097e13f62f9e
[sap-ha-guide-8.5]:high-availability-guide.md#9fbd43c0-5850-4965-9726-2a921d85d73f
[sap-ha-guide-8.6]:high-availability-guide.md#84c019fe-8c58-4dac-9e54-173efd4b2c30
[sap-ha-guide-8.7]:high-availability-guide.md#7a8f3e9b-0624-4051-9e41-b73fff816a9e
[sap-ha-guide-8.8]:high-availability-guide.md#f19bd997-154d-4583-a46e-7f5a69d0153c
[sap-ha-guide-8.9]:high-availability-guide.md#fe0bd8b5-2b43-45e3-8295-80bee5415716
[sap-ha-guide-8.10]:high-availability-guide.md#e69e9a34-4601-47a3-a41c-d2e11c626c0c
[sap-ha-guide-8.11]:high-availability-guide.md#661035b2-4d0f-4d31-86f8-dc0a50d78158
[sap-ha-guide-8.12]:high-availability-guide.md#0d67f090-7928-43e0-8772-5ccbf8f59aab
[sap-ha-guide-8.12.1]:high-availability-guide.md#5eecb071-c703-4ccc-ba6d-fe9c6ded9d79
[sap-ha-guide-8.12.2]:high-availability-guide.md#e49a4529-50c9-4dcf-bde7-15a0c21d21ca
[sap-ha-guide-8.12.2.1]:high-availability-guide.md#06260b30-d697-4c4d-b1c9-d22c0bd64855
[sap-ha-guide-8.12.2.2]:high-availability-guide.md#4c08c387-78a0-46b1-9d27-b497b08cac3d
[sap-ha-guide-8.12.3]:high-availability-guide.md#5c8e5482-841e-45e1-a89d-a05c0907c868
[sap-ha-guide-8.12.3.1]:high-availability-guide.md#1c2788c3-3648-4e82-9e0d-e058e475e2a3
[sap-ha-guide-8.12.3.2]:high-availability-guide.md#dd41d5a2-8083-415b-9878-839652812102
[sap-ha-guide-8.12.3.3]:high-availability-guide.md#d9c1fc8e-8710-4dff-bec2-1f535db7b006
[sap-ha-guide-9]:high-availability-guide.md#a06f0b49-8a7a-42bf-8b0d-c12026c5746b
[sap-ha-guide-9.1]:high-availability-guide.md#31c6bd4f-51df-4057-9fdf-3fcbc619c170
[sap-ha-guide-9.1.1]:high-availability-guide.md#a97ad604-9094-44fe-a364-f89cb39bf097
[sap-ha-guide-9.1.2]:high-availability-guide.md#eb5af918-b42f-4803-bb50-eff41f84b0b0
[sap-ha-guide-9.1.3]:high-availability-guide.md#e4caaab2-e90f-4f2c-bc84-2cd2e12a9556
[sap-ha-guide-9.1.4]:high-availability-guide.md#10822f4f-32e7-4871-b63a-9b86c76ce761
[sap-ha-guide-9.1.5]:high-availability-guide.md#4498c707-86c0-4cde-9c69-058a7ab8c3ac
[sap-ha-guide-9.2]:high-availability-guide.md#85d78414-b21d-4097-92b6-34d8bcb724b7
[sap-ha-guide-9.3]:high-availability-guide.md#8a276e16-f507-4071-b829-cdc0a4d36748
[sap-ha-guide-9.4]:high-availability-guide.md#094bc895-31d4-4471-91cc-1513b64e406a
[sap-ha-guide-9.5]:high-availability-guide.md#2477e58f-c5a7-4a5d-9ae3-7b91022cafb5
[sap-ha-guide-9.6]:high-availability-guide.md#0ba4a6c1-cc37-4bcf-a8dc-025de4263772
[sap-ha-guide-10]:high-availability-guide.md#18aa2b9d-92d2-4c0e-8ddd-5acaabda99e9
[sap-ha-guide-10.1]:high-availability-guide.md#65fdef0f-9f94-41f9-b314-ea45bbfea445
[sap-ha-guide-10.2]:high-availability-guide.md#5e959fa9-8fcd-49e5-a12c-37f6ba07b916
[sap-ha-guide-10.3]:high-availability-guide.md#755a6b93-0099-4533-9f6d-5c9a613878b5

[sap-ha-multi-sid-guide]:high-availability-multi-sid.md (SAP multi-SID high-availability configuration)


[sap-ha-guide-figure-1000]:media/virtual-machines-shared-sap-high-availability-guide/1000-wsfc-for-sap-ascs-on-azure.png
[sap-ha-guide-figure-1001]:media/virtual-machines-shared-sap-high-availability-guide/1001-wsfc-on-azure-ilb.png
[sap-ha-guide-figure-1002]:media/virtual-machines-shared-sap-high-availability-guide/1002-wsfc-sios-on-azure-ilb.png
[sap-ha-guide-figure-2000]:media/virtual-machines-shared-sap-high-availability-guide/2000-wsfc-sap-as-ha-on-azure.png
[sap-ha-guide-figure-2001]:media/virtual-machines-shared-sap-high-availability-guide/2001-wsfc-sap-ascs-ha-on-azure.png
[sap-ha-guide-figure-2003]:media/virtual-machines-shared-sap-high-availability-guide/2003-wsfc-sap-dbms-ha-on-azure.png
[sap-ha-guide-figure-2004]:media/virtual-machines-shared-sap-high-availability-guide/2004-wsfc-sap-ha-e2e-archit-template1-on-azure.png
[sap-ha-guide-figure-2005]:media/virtual-machines-shared-sap-high-availability-guide/2005-wsfc-sap-ha-e2e-arch-template2-on-azure.png

[sap-ha-guide-figure-3000]:media/virtual-machines-shared-sap-high-availability-guide/3000-template-parameters-sap-ha-arm-on-azure.png
[sap-ha-guide-figure-3001]:media/virtual-machines-shared-sap-high-availability-guide/3001-configuring-dns-servers-for-Azure-vnet.png
[sap-ha-guide-figure-3002]:media/virtual-machines-shared-sap-high-availability-guide/3002-configuring-static-IP-address-for-network-card-of-each-vm.png
[sap-ha-guide-figure-3003]:media/virtual-machines-shared-sap-high-availability-guide/3003-setup-static-ip-address-ilb-for-ascs-instance.png
[sap-ha-guide-figure-3004]:media/virtual-machines-shared-sap-high-availability-guide/3004-default-ascs-scs-ilb-balancing-rules-for-azure-ilb.png
[sap-ha-guide-figure-3005]:media/virtual-machines-shared-sap-high-availability-guide/3005-changing-ascs-scs-default-ilb-rules-for-azure-ilb.png
[sap-ha-guide-figure-3006]:media/virtual-machines-shared-sap-high-availability-guide/3006-adding-vm-to-domain.png
[sap-ha-guide-figure-3007]:media/virtual-machines-shared-sap-high-availability-guide/3007-config-wsfc-1.png
[sap-ha-guide-figure-3008]:media/virtual-machines-shared-sap-high-availability-guide/3008-config-wsfc-2.png
[sap-ha-guide-figure-3009]:media/virtual-machines-shared-sap-high-availability-guide/3009-config-wsfc-3.png
[sap-ha-guide-figure-3010]:media/virtual-machines-shared-sap-high-availability-guide/3010-config-wsfc-4.png
[sap-ha-guide-figure-3011]:media/virtual-machines-shared-sap-high-availability-guide/3011-config-wsfc-5.png
[sap-ha-guide-figure-3012]:media/virtual-machines-shared-sap-high-availability-guide/3012-config-wsfc-6.png
[sap-ha-guide-figure-3013]:media/virtual-machines-shared-sap-high-availability-guide/3013-config-wsfc-7.png
[sap-ha-guide-figure-3014]:media/virtual-machines-shared-sap-high-availability-guide/3014-config-wsfc-8.png
[sap-ha-guide-figure-3015]:media/virtual-machines-shared-sap-high-availability-guide/3015-config-wsfc-9.png
[sap-ha-guide-figure-3016]:media/virtual-machines-shared-sap-high-availability-guide/3016-config-wsfc-10.png
[sap-ha-guide-figure-3017]:media/virtual-machines-shared-sap-high-availability-guide/3017-config-wsfc-11.png
[sap-ha-guide-figure-3018]:media/virtual-machines-shared-sap-high-availability-guide/3018-config-wsfc-12.png
[sap-ha-guide-figure-3019]:media/virtual-machines-shared-sap-high-availability-guide/3019-assign-permissions-on-share-for-cluster-name-object.png
[sap-ha-guide-figure-3020]:media/virtual-machines-shared-sap-high-availability-guide/3020-change-object-type-include-computer-objects.png
[sap-ha-guide-figure-3021]:media/virtual-machines-shared-sap-high-availability-guide/3021-check-box-for-computer-objects.png
[sap-ha-guide-figure-3022]:media/virtual-machines-shared-sap-high-availability-guide/3022-set-security-attributes-for-cluster-name-object-on-file-share-quorum.png
[sap-ha-guide-figure-3023]:media/virtual-machines-shared-sap-high-availability-guide/3023-call-configure-cluster-quorum-setting-wizard.png
[sap-ha-guide-figure-3024]:media/virtual-machines-shared-sap-high-availability-guide/3024-selection-screen-different-quorum-configurations.png
[sap-ha-guide-figure-3025]:media/virtual-machines-shared-sap-high-availability-guide/3025-selection-screen-file-share-witness.png
[sap-ha-guide-figure-3026]:media/virtual-machines-shared-sap-high-availability-guide/3026-define-file-share-location-for-witness-share.png
[sap-ha-guide-figure-3027]:media/virtual-machines-shared-sap-high-availability-guide/3027-successful-reconfiguration-cluster-file-share-witness.png
[sap-ha-guide-figure-3028]:media/virtual-machines-shared-sap-high-availability-guide/3028-install-dot-net-framework-35.png
[sap-ha-guide-figure-3029]:media/virtual-machines-shared-sap-high-availability-guide/3029-install-dot-net-framework-35-progress.png
[sap-ha-guide-figure-3030]:media/virtual-machines-shared-sap-high-availability-guide/3030-sios-installer.png
[sap-ha-guide-figure-3031]:media/virtual-machines-shared-sap-high-availability-guide/3031-first-screen-sios-data-keeper-installation.png
[sap-ha-guide-figure-3032]:media/virtual-machines-shared-sap-high-availability-guide/3032-data-keeper-informs-service-be-disabled.png
[sap-ha-guide-figure-3033]:media/virtual-machines-shared-sap-high-availability-guide/3033-user-selection-sios-data-keeper.png
[sap-ha-guide-figure-3034]:media/virtual-machines-shared-sap-high-availability-guide/3034-domain-user-sios-data-keeper.png
[sap-ha-guide-figure-3035]:media/virtual-machines-shared-sap-high-availability-guide/3035-provide-sios-data-keeper-license.png
[sap-ha-guide-figure-3036]:media/virtual-machines-shared-sap-high-availability-guide/3036-data-keeper-management-config-tool.png
[sap-ha-guide-figure-3037]:media/virtual-machines-shared-sap-high-availability-guide/3037-tcp-ip-address-first-node-data-keeper.png
[sap-ha-guide-figure-3038]:media/virtual-machines-shared-sap-high-availability-guide/3038-create-replication-sios-job.png
[sap-ha-guide-figure-3039]:media/virtual-machines-shared-sap-high-availability-guide/3039-define-sios-replication-job-name.png
[sap-ha-guide-figure-3040]:media/virtual-machines-shared-sap-high-availability-guide/3040-define-sios-source-node.png
[sap-ha-guide-figure-3041]:media/virtual-machines-shared-sap-high-availability-guide/3041-define-sios-target-node.png
[sap-ha-guide-figure-3042]:media/virtual-machines-shared-sap-high-availability-guide/3042-define-sios-synchronous-replication.png
[sap-ha-guide-figure-3043]:media/virtual-machines-shared-sap-high-availability-guide/3043-enable-sios-replicated-volume-as-cluster-volume.png
[sap-ha-guide-figure-3044]:media/virtual-machines-shared-sap-high-availability-guide/3044-data-keeper-synchronous-mirroring-for-SAP-gui.png
[sap-ha-guide-figure-3045]:media/virtual-machines-shared-sap-high-availability-guide/3045-replicated-disk-by-data-keeper-in-wsfc.png
[sap-ha-guide-figure-3046]:media/virtual-machines-shared-sap-high-availability-guide/3046-dns-entry-sap-ascs-virtual-name-ip.png
[sap-ha-guide-figure-3047]:media/virtual-machines-shared-sap-high-availability-guide/3047-dns-manager.png
[sap-ha-guide-figure-3048]:media/virtual-machines-shared-sap-high-availability-guide/3048-default-cluster-probe-port.png
[sap-ha-guide-figure-3049]:media/virtual-machines-shared-sap-high-availability-guide/3049-cluster-probe-port-after.png
[sap-ha-guide-figure-3050]:media/virtual-machines-shared-sap-high-availability-guide/3050-service-type-ers-delayed-automatic.png
[sap-ha-guide-figure-5000]:media/virtual-machines-shared-sap-high-availability-guide/5000-wsfc-sap-sid-node-a.png
[sap-ha-guide-figure-5001]:media/virtual-machines-shared-sap-high-availability-guide/5001-sios-replicating-local-volume.png
[sap-ha-guide-figure-5002]:media/virtual-machines-shared-sap-high-availability-guide/5002-wsfc-sap-sid-node-b.png
[sap-ha-guide-figure-5003]:media/virtual-machines-shared-sap-high-availability-guide/5003-sios-replicating-local-volume-b-to-a.png

[sap-ha-guide-figure-6003]:media/virtual-machines-shared-sap-high-availability-guide/6003-sap-multi-sid-full-landscape.png

[powershell-install-configure]:https://docs.microsoft.com/powershell/azure/install-azurerm-ps
[resource-group-authoring-templates]:../../../resource-group-authoring-templates.md
[resource-group-overview]:../../../../../azure-resource-manager/resource-group-overview.md
[resource-groups-networking]:../../../virtual-network/resource-groups-networking.md
[sap-pam]:https://support.sap.com/pam (SAP Product Availability Matrix)
[sap-templates-2-tier-marketplace-image]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-2-tier-marketplace-image%2Fazuredeploy.json
[sap-templates-2-tier-os-disk]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-2-tier-user-disk%2Fazuredeploy.json
[sap-templates-2-tier-user-image]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-2-tier-user-image%2Fazuredeploy.json
[sap-templates-3-tier-marketplace-image]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image%2Fazuredeploy.json
[sap-templates-3-tier-user-image]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-user-image%2Fazuredeploy.json
[sap-templates-3-tier-multisid-xscs-marketplace-image]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image-multi-sid-xscs%2Fazuredeploy.json
[sap-templates-3-tier-multisid-db-marketplace-image]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image-multi-sid-db%2Fazuredeploy.json
[sap-templates-3-tier-multisid-apps-marketplace-image]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image-multi-sid-apps%2Fazuredeploy.json
[storage-azure-cli]:../../../storage/common/storage-azure-cli.md
[storage-azure-cli-copy-blobs]:../../../storage/common/storage-azure-cli.md#copy-blobs
[storage-introduction]:../../../storage/common/storage-introduction.md
[storage-powershell-guide-full-copy-vhd]:../../../storage/common/storage-powershell-guide-full.md#how-to-copy-blobs-from-one-storage-container-to-another
[storage-premium-storage-preview-portal]:../../../storage/common/storage-premium-storage.md
[storage-redundancy]:../../../storage/common/storage-redundancy.md
[storage-scalability-targets]:../../../storage/common/storage-scalability-targets.md
[storage-use-azcopy]:../../../storage/common/storage-use-azcopy.md
[template-201-vm-from-specialized-vhd]:https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-from-specialized-vhd
[templates-101-simple-windows-vm]:https://github.com/Azure/azure-quickstart-templates/tree/master/101-simple-windows-vm
[templates-101-vm-from-user-image]:https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-from-user-image
[virtual-machines-linux-attach-disk-portal]:../../linux/attach-disk-portal.md
[virtual-machines-windows-attach-disk-portal]:../../virtual-machines-windows-attach-disk-portal.md
[virtual-machines-azure-resource-manager-architecture]:../../../azure-resource-manager/resource-group-overview.md
[virtual-machines-azure-resource-manager-architecture-benefits-arm]:../../../azure-resource-manager/resource-group-overview.md#the-benefits-of-using-resource-manager
[virtual-machines-azurerm-versus-azuresm]:virtual-machines-windows-compare-deployment-models.md
[virtual-machines-windows-classic-configure-oracle-data-guard]:../../virtual-machines-windows-classic-configure-oracle-data-guard.md
[virtual-machines-linux-cli-deploy-templates]:../../linux/cli-deploy-templates.md
[virtual-machines-deploy-rmtemplates-powershell]:../../virtual-machines-windows-ps-manage.md
[virtual-machines-linux-agent-user-guide]:../../linux/agent-user-guide.md
[virtual-machines-linux-agent-user-guide-command-line-options]:../../linux/agent-user-guide.md#command-line-options
[virtual-machines-linux-capture-image]:../../linux/capture-image.md
[virtual-machines-linux-capture-image-capture]:../../linux/capture-image.md#capture-the-vm
[virtual-machines-windows-capture-image]:../../virtual-machines-windows-capture-image.md
[virtual-machines-windows-capture-image-capture]:../../virtual-machines-windows-capture-image.md#capture-the-vm
[virtual-machines-linux-configure-lvm]:../../linux/configure-lvm.md
[virtual-machines-linux-configure-raid]:../../linux/configure-raid.md
[virtual-machines-linux-classic-create-upload-vhd-step-1]:../../virtual-machines-linux-classic-create-upload-vhd.md#step-1-prepare-the-image-to-be-uploaded
[virtual-machines-linux-create-upload-vhd-suse]:../../linux/suse-create-upload-vhd.md
[virtual-machines-linux-redhat-create-upload-vhd]:../../linux/redhat-create-upload-vhd.md
[virtual-machines-linux-how-to-attach-disk]:../../linux/add-disk.md
[virtual-machines-linux-how-to-attach-disk-how-to-initialize-a-new-data-disk-in-linux]:../../linux/add-disk.md#connect-to-the-linux-vm-to-mount-the-new-disk
[virtual-machines-linux-tutorial]:../../linux/quick-create-cli.md
[virtual-machines-linux-update-agent]:../../linux/update-agent.md
[virtual-machines-manage-availability]:../../virtual-machines-windows-manage-availability.md
[virtual-machines-ps-create-preconfigure-windows-resource-manager-vms]:../../virtual-machines-windows-ps-create.md
[virtual-machines-sizes]:../../virtual-machines-windows-sizes.md
[virtual-machines-windows-portal-sql-alwayson-availability-groups-manual]:../../windows/sql/virtual-machines-windows-portal-sql-alwayson-availability-groups-manual.md
[virtual-machines-windows-portal-sql-alwayson-int-listener]:../../windows/sql/virtual-machines-windows-portal-sql-alwayson-int-listener.md
[virtual-machines-upload-image-windows-resource-manager]:../../virtual-machines-windows-upload-image.md
[virtual-machines-windows-tutorial]:../../virtual-machines-windows-hero-tutorial.md
[virtual-machines-workload-template-sql-alwayson]:https://azure.microsoft.com/documentation/templates/sql-server-2014-alwayson-dsc/
[virtual-network-deploy-multinic-arm-cli]:../../../virtual-network/virtual-network-deploy-multinic-arm-cli.md
[virtual-network-deploy-multinic-arm-ps]:../../../virtual-network/virtual-network-deploy-multinic-arm-ps.md
[virtual-network-deploy-multinic-arm-template]:../../../virtual-network/virtual-network-deploy-multinic-arm-template.md
[virtual-networks-configure-vnet-to-vnet-connection]:../../../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md
[virtual-networks-create-vnet-arm-pportal]:../../../virtual-network/virtual-networks-create-vnet-arm-pportal.md
[virtual-networks-manage-dns-in-vnet]:../../../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md
[virtual-networks-multiple-nics]:../../../virtual-network/virtual-networks-multiple-nics.md
[virtual-networks-nsg]:../../../virtual-network/virtual-networks-nsg.md
[virtual-networks-reserved-private-ip]:../../../virtual-network/virtual-networks-static-private-ip-arm-ps.md
[virtual-networks-static-private-ip-arm-pportal]:../../../virtual-network/virtual-networks-static-private-ip-arm-pportal.md
[virtual-networks-udr-overview]:../../../virtual-network/virtual-networks-udr-overview.md
[vpn-gateway-about-vpn-devices]:../../../vpn-gateway/vpn-gateway-about-vpn-devices.md
[vpn-gateway-create-site-to-site-rm-powershell]:../../../vpn-gateway/vpn-gateway-create-site-to-site-rm-powershell.md
[vpn-gateway-cross-premises-options]:../../../vpn-gateway/vpn-gateway-plan-design.md
[vpn-gateway-site-to-site-create]:../../../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md
[vpn-gateway-vpn-faq]:../../../vpn-gateway/vpn-gateway-vpn-faq.md
[xplat-cli]:../../../cli-install-nodejs.md
[xplat-cli-azure-resource-manager]:../../../xplat-cli-azure-resource-manager.md


<span data-ttu-id="e0e69-109">Machines virtuelles Azure est la solution hello pour les organisations qui ont besoin de calcul, stockage et ressources réseau, dans le temps minimal et sans par de longs cycles.</span><span class="sxs-lookup"><span data-stu-id="e0e69-109">Azure Virtual Machines is hello solution for organizations that need compute, storage, and network resources, in minimal time, and without lengthy procurement cycles.</span></span> <span data-ttu-id="e0e69-110">Vous pouvez utiliser les applications classiques de Machines virtuelles Azure toodeploy comme basés sur SAP NetWeaver ABAP, Java et une pile ABAP + Java.</span><span class="sxs-lookup"><span data-stu-id="e0e69-110">You can use Azure Virtual Machines toodeploy classic applications like SAP NetWeaver-based ABAP, Java, and an ABAP+Java stack.</span></span> <span data-ttu-id="e0e69-111">Élargissez la fiabilité et la disponibilité sans ressources locales supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="e0e69-111">Extend reliability and availability without additional on-premises resources.</span></span> <span data-ttu-id="e0e69-112">Comme le service Machines virtuelles Azure prend en charge la connectivité intersite, vous pouvez intégrer les machines virtuelles Azure dans les domaines locaux, les clouds privés et le paysage SAP de votre organisation.</span><span class="sxs-lookup"><span data-stu-id="e0e69-112">Azure Virtual Machines supports cross-premises connectivity, so you can integrate Azure Virtual Machines into your organization's on-premises domains, private clouds, and SAP system landscape.</span></span>

<span data-ttu-id="e0e69-113">Dans cet article, nous aborderons les étapes de hello que vous pouvez bénéficier toodeploy systèmes SAP à haute disponibilité dans Azure à l’aide du modèle de déploiement du Gestionnaire de ressources Azure hello.</span><span class="sxs-lookup"><span data-stu-id="e0e69-113">In this article, we cover hello steps that you can take toodeploy high-availability SAP systems in Azure by using hello Azure Resource Manager deployment model.</span></span> <span data-ttu-id="e0e69-114">Nous vous guidons à travers les tâches principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="e0e69-114">We walk you through these major tasks:</span></span>

* <span data-ttu-id="e0e69-115">Trouver des guides d’installation et les Notes SAP droite, répertoriés dans hello de hello [ressources] [ sap-ha-guide-2] section.</span><span class="sxs-lookup"><span data-stu-id="e0e69-115">Find hello right SAP Notes and installation guides, listed in hello [Resources][sap-ha-guide-2] section.</span></span> <span data-ttu-id="e0e69-116">Cet article complète la documentation d’installation SAP et les Notes SAP, qui sont des ressources principales hello qui peuvent vous aider à installer et déployer des logiciels SAP sur des plateformes spécifiques.</span><span class="sxs-lookup"><span data-stu-id="e0e69-116">This article complements SAP installation documentation and SAP Notes, which are hello primary resources that can help you install and deploy SAP software on specific platforms.</span></span>
* <span data-ttu-id="e0e69-117">Découvrez les différences de hello entre le modèle de déploiement du Gestionnaire de ressources Azure hello et le modèle de déploiement classique Azure hello.</span><span class="sxs-lookup"><span data-stu-id="e0e69-117">Learn hello differences between hello Azure Resource Manager deployment model and hello Azure classic deployment model.</span></span>
* <span data-ttu-id="e0e69-118">En savoir plus sur les modes de quorum le Clustering de basculement Windows Server, afin de pouvoir modèle hello qui convient à votre déploiement Azure.</span><span class="sxs-lookup"><span data-stu-id="e0e69-118">Learn about Windows Server Failover Clustering quorum modes, so you can select hello model that is right for your Azure deployment.</span></span>
* <span data-ttu-id="e0e69-119">Découvrir le stockage partagé en cluster de basculement Windows Server dans les services Azure.</span><span class="sxs-lookup"><span data-stu-id="e0e69-119">Learn about Windows Server Failover Clustering shared storage in Azure services.</span></span>
* <span data-ttu-id="e0e69-120">Découvrez comment toohelp protègent les composants de l’unique point de défaillance comme Advanced Business Application Programming (ABAP) SAP Central Services (ASC) / SAP Central Services (SCS) et les systèmes de gestion de base de données (SGBD) et des composants redondants, tels que SAP Serveur d’applications dans Azure.</span><span class="sxs-lookup"><span data-stu-id="e0e69-120">Learn how toohelp protect single-point-of-failure components like Advanced Business Application Programming (ABAP) SAP Central Services (ASCS)/SAP Central Services (SCS) and database management systems (DBMS), and redundant components like SAP Application Server, in Azure.</span></span>
* <span data-ttu-id="e0e69-121">Suivre un exemple pas à pas d’installation et de configuration d’un système SAP à haute disponibilité dans un cluster de clustering de basculement Windows Server dans Azure en utilisant Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="e0e69-121">Follow a step-by-step example of an installation and configuration of a high-availability SAP system in a Windows Server Failover Clustering cluster in Azure by using Azure Resource Manager.</span></span>
* <span data-ttu-id="e0e69-122">Obtenir des informations sur les étapes supplémentaires requises toouse est Clustering de basculement Windows Server dans Azure, mais qui ne sont pas nécessaires dans un déploiement sur site.</span><span class="sxs-lookup"><span data-stu-id="e0e69-122">Learn about additional steps required toouse Windows Server Failover Clustering in Azure, but which are not needed in an on-premises deployment.</span></span>

<span data-ttu-id="e0e69-123">déploiement de toosimplify et de configuration, dans cet article, nous utilisons hello des modèles de gestionnaire de ressources haute disponibilité SAP à trois niveaux.</span><span class="sxs-lookup"><span data-stu-id="e0e69-123">toosimplify deployment and configuration, in this article, we use hello SAP three-tier high-availability Resource Manager templates.</span></span> <span data-ttu-id="e0e69-124">modèles de Hello automatisent le déploiement de hello toute infrastructure dont vous avez besoin pour un système SAP à haute disponibilité.</span><span class="sxs-lookup"><span data-stu-id="e0e69-124">hello templates automate deployment of hello entire infrastructure that you need for a high-availability SAP system.</span></span> <span data-ttu-id="e0e69-125">infrastructure de Hello prend également en charge le dimensionnement de SAP Application performances Standard (SAP) de votre système SAP.</span><span class="sxs-lookup"><span data-stu-id="e0e69-125">hello infrastructure also supports SAP Application Performance Standard (SAPS) sizing of your SAP system.</span></span>

## <span data-ttu-id="e0e69-126"><a name="217c5479-5595-4cd8-870d-15ab00d4f84c"></a> Conditions préalables</span><span class="sxs-lookup"><span data-stu-id="e0e69-126"><a name="217c5479-5595-4cd8-870d-15ab00d4f84c"></a> Prerequisites</span></span>
<span data-ttu-id="e0e69-127">Avant de commencer, assurez-vous que conditions préalables hello qui sont décrites dans les sections suivantes de hello.</span><span class="sxs-lookup"><span data-stu-id="e0e69-127">Before you start, make sure that you meet hello prerequisites that are described in hello following sections.</span></span> <span data-ttu-id="e0e69-128">En outre, être toocheck que toutes les ressources répertoriées dans hello [ressources] [ sap-ha-guide-2] section.</span><span class="sxs-lookup"><span data-stu-id="e0e69-128">Also, be sure toocheck all resources listed in hello [Resources][sap-ha-guide-2] section.</span></span>

<span data-ttu-id="e0e69-129">Dans cet article, nous utilisons des modèles Azure Resource Manager pour [SAP NetWeaver à trois niveaux](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-marketplace-image/).</span><span class="sxs-lookup"><span data-stu-id="e0e69-129">In this article, we use Azure Resource Manager templates for [three-tier SAP NetWeaver](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-marketplace-image/).</span></span> <span data-ttu-id="e0e69-130">Pour une vue d’ensemble utile des modèles Azure Resource Manager SAP, consultez [cet article](https://blogs.msdn.microsoft.com/saponsqlserver/2016/05/16/azure-quickstart-templates-for-sap/).</span><span class="sxs-lookup"><span data-stu-id="e0e69-130">For a helpful overview of templates, see [SAP Azure Resource Manager templates](https://blogs.msdn.microsoft.com/saponsqlserver/2016/05/16/azure-quickstart-templates-for-sap/).</span></span>

## <span data-ttu-id="e0e69-131"><a name="42b8f600-7ba3-4606-b8a5-53c4f026da08"></a> Ressources</span><span class="sxs-lookup"><span data-stu-id="e0e69-131"><a name="42b8f600-7ba3-4606-b8a5-53c4f026da08"></a> Resources</span></span>
<span data-ttu-id="e0e69-132">Ces articles couvrent les déploiements SAP dans Azure :</span><span class="sxs-lookup"><span data-stu-id="e0e69-132">These articles cover SAP deployments in Azure:</span></span>

* <span data-ttu-id="e0e69-133">[Planification et implémentation de machines virtuelles Azure pour SAP NetWeaver][planning-guide]</span><span class="sxs-lookup"><span data-stu-id="e0e69-133">[Azure Virtual Machines planning and implementation for SAP NetWeaver][planning-guide]</span></span>
* <span data-ttu-id="e0e69-134">[Déploiement de machines virtuelles Azure pour SAP NetWeaver][deployment-guide]</span><span class="sxs-lookup"><span data-stu-id="e0e69-134">[Azure Virtual Machines deployment for SAP NetWeaver][deployment-guide]</span></span>
* <span data-ttu-id="e0e69-135">[Déploiement SGBD de machines virtuelles Azure pour SAP NetWeaver][dbms-guide]</span><span class="sxs-lookup"><span data-stu-id="e0e69-135">[Azure Virtual Machines DBMS deployment for SAP NetWeaver][dbms-guide]</span></span>
* <span data-ttu-id="e0e69-136">[Haute disponibilité des machines virtuelles Azure pour SAP NetWeaver (ce guide)][sap-ha-guide]</span><span class="sxs-lookup"><span data-stu-id="e0e69-136">[Azure Virtual Machines high availability for SAP NetWeaver (this guide)][sap-ha-guide]</span></span>

> [!NOTE]
> <span data-ttu-id="e0e69-137">Chaque fois que possible, nous vous offrons une toohello lien référence guide d’installation SAP (voir hello [guides d’installation SAP][sap-installation-guides]).</span><span class="sxs-lookup"><span data-stu-id="e0e69-137">Whenever possible, we give you a link toohello referring SAP installation guide (see hello [SAP installation guides][sap-installation-guides]).</span></span> <span data-ttu-id="e0e69-138">Pour les conditions préalables et les informations sur les processus d’installation de hello, elle une installation de SAP NetWeaver conseillé tooread hello Guide avec soin.</span><span class="sxs-lookup"><span data-stu-id="e0e69-138">For prerequisites and information about hello installation process, it's a good idea tooread hello SAP NetWeaver installation guides carefully.</span></span> <span data-ttu-id="e0e69-139">Cet article traite uniquement des tâches spécifiques pour les systèmes basés sur SAP NetWeaver que vous pouvez utiliser avec le service Machines virtuelles Azure.</span><span class="sxs-lookup"><span data-stu-id="e0e69-139">This article covers only specific tasks for SAP NetWeaver-based systems that you can use with Azure Virtual Machines.</span></span>
>
>

<span data-ttu-id="e0e69-140">Ces Notes SAP sont rubrique toohello connexes de SAP dans Azure :</span><span class="sxs-lookup"><span data-stu-id="e0e69-140">These SAP Notes are related toohello topic of SAP in Azure:</span></span>

| <span data-ttu-id="e0e69-141">Numéro de la note</span><span class="sxs-lookup"><span data-stu-id="e0e69-141">Note number</span></span> | <span data-ttu-id="e0e69-142">Intitulé</span><span class="sxs-lookup"><span data-stu-id="e0e69-142">Title</span></span> |
| --- | --- |
| <span data-ttu-id="e0e69-143">[1928533]</span><span class="sxs-lookup"><span data-stu-id="e0e69-143">[1928533]</span></span> |<span data-ttu-id="e0e69-144">Applications SAP sur Azure : dimensionnement et produits pris en charge</span><span class="sxs-lookup"><span data-stu-id="e0e69-144">SAP Applications on Azure: Supported Products and Sizing</span></span> |
| <span data-ttu-id="e0e69-145">[2015553]</span><span class="sxs-lookup"><span data-stu-id="e0e69-145">[2015553]</span></span> |<span data-ttu-id="e0e69-146">SAP sur Microsoft Azure : configuration requise</span><span class="sxs-lookup"><span data-stu-id="e0e69-146">SAP on Microsoft Azure: Support Prerequisites</span></span> |
| <span data-ttu-id="e0e69-147">[1999351]</span><span class="sxs-lookup"><span data-stu-id="e0e69-147">[1999351]</span></span> |<span data-ttu-id="e0e69-148">Surveillance Azure améliorée pour SAP</span><span class="sxs-lookup"><span data-stu-id="e0e69-148">Enhanced Azure Monitoring for SAP</span></span> |
| <span data-ttu-id="e0e69-149">[2178632]</span><span class="sxs-lookup"><span data-stu-id="e0e69-149">[2178632]</span></span> |<span data-ttu-id="e0e69-150">Métriques de surveillance clés pour SAP sur Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="e0e69-150">Key Monitoring Metrics for SAP on Microsoft Azure</span></span> |
| <span data-ttu-id="e0e69-151">[1999351]</span><span class="sxs-lookup"><span data-stu-id="e0e69-151">[1999351]</span></span> |<span data-ttu-id="e0e69-152">Virtualisation sur Windows : surveillance améliorée</span><span class="sxs-lookup"><span data-stu-id="e0e69-152">Virtualization on Windows: Enhanced Monitoring</span></span> |
| <span data-ttu-id="e0e69-153">[2243692]</span><span class="sxs-lookup"><span data-stu-id="e0e69-153">[2243692]</span></span> |<span data-ttu-id="e0e69-154">Utilisation du stockage SSD Azure Premium pour l’instance de SGBD SAP</span><span class="sxs-lookup"><span data-stu-id="e0e69-154">Use of Azure Premium SSD Storage for SAP DBMS Instance</span></span> |

<span data-ttu-id="e0e69-155">En savoir plus sur hello [limitations des abonnements Azure][azure-subscription-service-limits-subscription], y compris les limitations générales par défaut et limitations maximales.</span><span class="sxs-lookup"><span data-stu-id="e0e69-155">Learn more about hello [limitations of Azure subscriptions][azure-subscription-service-limits-subscription], including general default limitations and maximum limitations.</span></span>

## <span data-ttu-id="e0e69-156"><a name="42156640c6-01cf-45a9-b225-4baa678b24f1"></a>Haute disponibilité SAP avec Azure Resource Manager et le modèle de déploiement classique Azure hello</span><span class="sxs-lookup"><span data-stu-id="e0e69-156"><a name="42156640c6-01cf-45a9-b225-4baa678b24f1"></a>High-availability SAP with Azure Resource Manager vs. hello Azure classic deployment model</span></span>
<span data-ttu-id="e0e69-157">Hello Azure Resource Manager et les modèles de déploiement classique Azure sont différentes dans hello suivant de zones :</span><span class="sxs-lookup"><span data-stu-id="e0e69-157">hello Azure Resource Manager and Azure classic deployment models are different in hello following areas:</span></span>

- <span data-ttu-id="e0e69-158">Groupes de ressources</span><span class="sxs-lookup"><span data-stu-id="e0e69-158">Resource groups</span></span>
- <span data-ttu-id="e0e69-159">Azure interne charger la dépendance d’équilibrage sur le groupe de ressources Azure hello</span><span class="sxs-lookup"><span data-stu-id="e0e69-159">Azure internal load balancer dependency on hello Azure resource group</span></span>
- <span data-ttu-id="e0e69-160">Prise en charge des scénarios SAP multi-SID</span><span class="sxs-lookup"><span data-stu-id="e0e69-160">Support for SAP multi-SID scenarios</span></span>

### <span data-ttu-id="e0e69-161"><a name="f76af273-1993-4d83-b12d-65deeae23686"></a> Groupes de ressources</span><span class="sxs-lookup"><span data-stu-id="e0e69-161"><a name="f76af273-1993-4d83-b12d-65deeae23686"></a> Resource groups</span></span>
<span data-ttu-id="e0e69-162">Dans le Gestionnaire de ressources Azure, vous pouvez utiliser toomanage de groupes de ressources toutes les ressources de l’application hello dans votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="e0e69-162">In Azure Resource Manager, you can use resource groups toomanage all hello application resources in your Azure subscription.</span></span> <span data-ttu-id="e0e69-163">Une approche intégrée, dans un groupe de ressources, toutes les ressources ont hello même cycle de vie.</span><span class="sxs-lookup"><span data-stu-id="e0e69-163">An integrated approach, in a resource group, all resources have hello same life cycle.</span></span> <span data-ttu-id="e0e69-164">Par exemple, toutes les ressources sont créées à hello même temps et ils sont supprimés à hello même temps.</span><span class="sxs-lookup"><span data-stu-id="e0e69-164">For example, all resources are created at hello same time and they are deleted at hello same time.</span></span> <span data-ttu-id="e0e69-165">En savoir plus sur les [groupes de ressources](../../../azure-resource-manager/resource-group-overview.md#resource-groups).</span><span class="sxs-lookup"><span data-stu-id="e0e69-165">Learn more about [resource groups](../../../azure-resource-manager/resource-group-overview.md#resource-groups).</span></span>

### <span data-ttu-id="e0e69-166"><a name="3e85fbe0-84b1-4892-87af-d9b65ff91860"></a>Azure interne charger la dépendance d’équilibrage sur le groupe de ressources Azure hello</span><span class="sxs-lookup"><span data-stu-id="e0e69-166"><a name="3e85fbe0-84b1-4892-87af-d9b65ff91860"></a> Azure internal load balancer dependency on hello Azure resource group</span></span>

<span data-ttu-id="e0e69-167">Dans le modèle de déploiement classique Azure hello, il existe une dépendance entre l’équilibreur de charge interne Azure hello (service d’équilibrage de charge Azure) et le groupe de service cloud hello.</span><span class="sxs-lookup"><span data-stu-id="e0e69-167">In hello Azure classic deployment model, there is a dependency between hello Azure internal load balancer (Azure Load Balancer service) and hello cloud service group.</span></span> <span data-ttu-id="e0e69-168">Chaque équilibreur de charge interne a besoin d’un groupe de services cloud.</span><span class="sxs-lookup"><span data-stu-id="e0e69-168">Every internal load balancer needs one cloud service group.</span></span>

<span data-ttu-id="e0e69-169">Dans le Gestionnaire de ressources Azure, vous n’avez pas besoin une toouse de groupe de ressources Azure équilibrage de charge Azure.</span><span class="sxs-lookup"><span data-stu-id="e0e69-169">In Azure Resource Manager, you don't need an Azure resource group toouse Azure Load Balancer.</span></span> <span data-ttu-id="e0e69-170">environnement de Hello est plus simple et flexible.</span><span class="sxs-lookup"><span data-stu-id="e0e69-170">hello environment is simpler and more flexible.</span></span>

### <a name="support-for-sap-multi-sid-scenarios"></a><span data-ttu-id="e0e69-171">Prise en charge des scénarios SAP multi-SID</span><span class="sxs-lookup"><span data-stu-id="e0e69-171">Support for SAP multi-SID scenarios</span></span>

<span data-ttu-id="e0e69-172">Dans Azure Resource Manager, vous pouvez installer plusieurs instances d’identificateur système SAP (SID) ASCS/SCS dans un cluster.</span><span class="sxs-lookup"><span data-stu-id="e0e69-172">In Azure Resource Manager, you can install multiple SAP system identifier (SID) ASCS/SCS instances in one cluster.</span></span> <span data-ttu-id="e0e69-173">Il est possible d’utiliser des instances multi-SID en raison de la prise en charge de plusieurs adresses IP pour chaque équilibreur de charge interne Azure.</span><span class="sxs-lookup"><span data-stu-id="e0e69-173">Multi-SID instances are possible because of support for multiple IP addresses for each Azure internal load balancer.</span></span>

<span data-ttu-id="e0e69-174">toouse hello du modèle de déploiement classique Azure, suivez les procédures hello décrites dans [SAP NetWeaver dans Azure : les instances de Clustering ASCS/SCS SAP à l’aide de Clustering de basculement Windows Server dans Azure avec SIOS DataKeeper](http://go.microsoft.com/fwlink/?LinkId=613056).</span><span class="sxs-lookup"><span data-stu-id="e0e69-174">toouse hello Azure classic deployment model, follow hello procedures described in [SAP NetWeaver in Azure: Clustering SAP ASCS/SCS instances by using Windows Server Failover Clustering in Azure with SIOS DataKeeper](http://go.microsoft.com/fwlink/?LinkId=613056).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e0e69-175">Nous vous recommandons fortement d’utiliser le modèle de déploiement du Gestionnaire de ressources Azure hello pour les installations SAP.</span><span class="sxs-lookup"><span data-stu-id="e0e69-175">We strongly recommend that you use hello Azure Resource Manager deployment model for your SAP installations.</span></span> <span data-ttu-id="e0e69-176">Il offre de nombreux avantages qui ne sont pas disponibles dans le modèle de déploiement classique hello.</span><span class="sxs-lookup"><span data-stu-id="e0e69-176">It offers many benefits that are not available in hello classic deployment model.</span></span> <span data-ttu-id="e0e69-177">En savoir plus sur les [modèles de déploiement][virtual-machines-azure-resource-manager-architecture-benefits-arm] Azure.</span><span class="sxs-lookup"><span data-stu-id="e0e69-177">Learn more about Azure [deployment models][virtual-machines-azure-resource-manager-architecture-benefits-arm].</span></span>   
>
>

## <span data-ttu-id="e0e69-178"><a name="8ecf3ba0-67c0-4495-9c14-feec1a2255b7"></a> Clustering de basculement Windows Server</span><span class="sxs-lookup"><span data-stu-id="e0e69-178"><a name="8ecf3ba0-67c0-4495-9c14-feec1a2255b7"></a> Windows Server Failover Clustering</span></span>
<span data-ttu-id="e0e69-179">Le Clustering de basculement Windows Server est foundation hello d’une installation SAP ASCS/SCS de haute disponibilité et un SGBD dans Windows.</span><span class="sxs-lookup"><span data-stu-id="e0e69-179">Windows Server Failover Clustering is hello foundation of a high-availability SAP ASCS/SCS installation and DBMS in Windows.</span></span>

<span data-ttu-id="e0e69-180">Un cluster de basculement est un groupe de 1 + n serveurs indépendants (nœuds) qui fonctionnent ensemble de disponibilité de hello tooincrease des applications et services.</span><span class="sxs-lookup"><span data-stu-id="e0e69-180">A failover cluster is a group of 1+n independent servers (nodes) that work together tooincrease hello availability of applications and services.</span></span> <span data-ttu-id="e0e69-181">En cas de défaillance d’un nœud, le Clustering de basculement Windows Server calcule nombre hello d’échecs qui peuvent se produire lors de la gestion d’état de fonctionnement normal de cluster tooprovide applications et services.</span><span class="sxs-lookup"><span data-stu-id="e0e69-181">If a node failure occurs, Windows Server Failover Clustering calculates hello number of failures that can occur while maintaining a healthy cluster tooprovide applications and services.</span></span> <span data-ttu-id="e0e69-182">Vous pouvez choisir de quorum différents modes tooachieve le clustering de basculement.</span><span class="sxs-lookup"><span data-stu-id="e0e69-182">You can choose from different quorum modes tooachieve failover clustering.</span></span>

### <span data-ttu-id="e0e69-183"><a name="1a3c5408-b168-46d6-99f5-4219ad1b1ff2"></a> Modes de quorum</span><span class="sxs-lookup"><span data-stu-id="e0e69-183"><a name="1a3c5408-b168-46d6-99f5-4219ad1b1ff2"></a> Quorum modes</span></span>
<span data-ttu-id="e0e69-184">Lorsque vous utilisez le clustering de basculement Windows Server, vous pouvez choisir parmi quatre modes de quorum :</span><span class="sxs-lookup"><span data-stu-id="e0e69-184">You can choose from four quorum modes when you use Windows Server Failover Clustering:</span></span>

* <span data-ttu-id="e0e69-185">**Nœud majoritaire** :</span><span class="sxs-lookup"><span data-stu-id="e0e69-185">**Node Majority**.</span></span> <span data-ttu-id="e0e69-186">Chaque nœud du cluster de hello peut voter.</span><span class="sxs-lookup"><span data-stu-id="e0e69-186">Each node of hello cluster can vote.</span></span> <span data-ttu-id="e0e69-187">Bonjour cluster ne fonctionne uniquement avec la majorité des votes, autrement dit, avec plus de la moitié des votes de hello.</span><span class="sxs-lookup"><span data-stu-id="e0e69-187">hello cluster functions only with a majority of votes, that is, with more than half hello votes.</span></span> <span data-ttu-id="e0e69-188">Nous recommandons cette option pour les clusters qui présentent un nombre impair de nœuds.</span><span class="sxs-lookup"><span data-stu-id="e0e69-188">We recommend this option for clusters that have an uneven number of nodes.</span></span> <span data-ttu-id="e0e69-189">Par exemple, trois nœuds dans un cluster à sept nœuds peuvent échouer et images fixes de cluster hello atteigne une majorité et continue toorun.</span><span class="sxs-lookup"><span data-stu-id="e0e69-189">For example, three nodes in a seven-node cluster can fail, and hello cluster stills achieves a majority and continues toorun.</span></span>  
* <span data-ttu-id="e0e69-190">**Nœud et disque majoritaires** :</span><span class="sxs-lookup"><span data-stu-id="e0e69-190">**Node and Disk Majority**.</span></span> <span data-ttu-id="e0e69-191">Chaque nœud et un disque désigné (un témoin de disque) dans le stockage de cluster hello peuvent voter lorsqu’ils sont disponibles et en communication.</span><span class="sxs-lookup"><span data-stu-id="e0e69-191">Each node and a designated disk (a disk witness) in hello cluster storage can vote when they are available and in communication.</span></span> <span data-ttu-id="e0e69-192">Hello cluster ne fonctionne seulement avec une majorité de hello de votes, autrement dit, avec plus de la moitié des votes de hello.</span><span class="sxs-lookup"><span data-stu-id="e0e69-192">hello cluster functions only with a majority of hello votes, that is, with more than half hello votes.</span></span> <span data-ttu-id="e0e69-193">Ce mode est pertinent dans un environnement de cluster comprenant un nombre pair de nœuds.</span><span class="sxs-lookup"><span data-stu-id="e0e69-193">This mode makes sense in a cluster environment with an even number of nodes.</span></span> <span data-ttu-id="e0e69-194">Si les nœuds de moitié hello et de disque de hello sont en ligne, le cluster de hello reste dans un état sain.</span><span class="sxs-lookup"><span data-stu-id="e0e69-194">If half hello nodes and hello disk are online, hello cluster remains in a healthy state.</span></span>
* <span data-ttu-id="e0e69-195">**Nœud et partage de fichiers majoritaires** :</span><span class="sxs-lookup"><span data-stu-id="e0e69-195">**Node and File Share Majority**.</span></span> <span data-ttu-id="e0e69-196">Chaque nœud et partage de fichiers désigné (un témoin de partage de fichiers) qui hello administrateur crée peut voter, que les nœuds hello et partage de fichiers soient disponibles et en communication.</span><span class="sxs-lookup"><span data-stu-id="e0e69-196">Each node plus a designated file share (a file share witness) that hello administrator creates can vote, regardless of whether hello nodes and file share are available and in communication.</span></span> <span data-ttu-id="e0e69-197">Hello cluster ne fonctionne seulement avec une majorité de hello de votes, autrement dit, avec plus de la moitié des votes de hello.</span><span class="sxs-lookup"><span data-stu-id="e0e69-197">hello cluster functions only with a majority of hello votes, that is, with more than half hello votes.</span></span> <span data-ttu-id="e0e69-198">Ce mode est pertinent dans un environnement de cluster comprenant un nombre pair de nœuds.</span><span class="sxs-lookup"><span data-stu-id="e0e69-198">This mode makes sense in a cluster environment with an even number of nodes.</span></span> <span data-ttu-id="e0e69-199">Il est similaire toohello nœud et le mode disque majoritaires, mais il utilise un partage de fichiers témoin au lieu d’un disque témoin.</span><span class="sxs-lookup"><span data-stu-id="e0e69-199">It's similar toohello Node and Disk Majority mode, but it uses a witness file share instead of a witness disk.</span></span> <span data-ttu-id="e0e69-200">Ce mode est tooimplement facile, mais si un partage de fichiers de hello lui-même n’est pas hautement disponible, il peut devenir un point de défaillance unique.</span><span class="sxs-lookup"><span data-stu-id="e0e69-200">This mode is easy tooimplement, but if hello file share itself is not highly available, it might become a single point of failure.</span></span>
* <span data-ttu-id="e0e69-201">**Pas de majorité : disque uniquement** :</span><span class="sxs-lookup"><span data-stu-id="e0e69-201">**No Majority: Disk Only**.</span></span> <span data-ttu-id="e0e69-202">cluster de Hello possède un quorum si un nœud est disponible et en communication avec un disque spécifique du stockage de cluster hello.</span><span class="sxs-lookup"><span data-stu-id="e0e69-202">hello cluster has a quorum if one node is available and in communication with a specific disk in hello cluster storage.</span></span> <span data-ttu-id="e0e69-203">Seuls les nœuds hello qui se trouvent également dans la communication avec ce disque peuvent être ajouté hello cluster.</span><span class="sxs-lookup"><span data-stu-id="e0e69-203">Only hello nodes that also are in communication with that disk can join hello cluster.</span></span> <span data-ttu-id="e0e69-204">Nous vous déconseillons d’utiliser ce mode.</span><span class="sxs-lookup"><span data-stu-id="e0e69-204">We recommend that you do not use this mode.</span></span>
 

## <span data-ttu-id="e0e69-205"><a name="fdfee875-6e66-483a-a343-14bbaee33275"></a> Clustering de basculement Windows Server local</span><span class="sxs-lookup"><span data-stu-id="e0e69-205"><a name="fdfee875-6e66-483a-a343-14bbaee33275"></a> Windows Server Failover Clustering on-premises</span></span>
<span data-ttu-id="e0e69-206">La figure 1 illustre un cluster de deux nœuds.</span><span class="sxs-lookup"><span data-stu-id="e0e69-206">Figure 1 shows a cluster of two nodes.</span></span> <span data-ttu-id="e0e69-207">Si hello Échec de la connexion réseau entre les nœuds de hello et les deux nœuds restent des et en cours d’exécution, un quorum disque ou partage de fichiers détermine quel nœud continuera de cluster tooprovide hello applications et services.</span><span class="sxs-lookup"><span data-stu-id="e0e69-207">If hello network connection between hello nodes fails and both nodes stay up and running, a quorum disk or file share determines which node will continue tooprovide hello cluster's applications and services.</span></span> <span data-ttu-id="e0e69-208">nœud Hello qui possède le disque quorum accès toohello ou partager des fichiers est le nœud hello qui permet aux services de continuer.</span><span class="sxs-lookup"><span data-stu-id="e0e69-208">hello node that has access toohello quorum disk or file share is hello node that ensures that services continue.</span></span>

<span data-ttu-id="e0e69-209">Étant donné que cet exemple utilise un cluster à deux nœuds, nous utilisons hello nœud et le mode de quorum de partage de fichiers majoritaires.</span><span class="sxs-lookup"><span data-stu-id="e0e69-209">Because this example uses a two-node cluster, we use hello Node and File Share Majority quorum mode.</span></span> <span data-ttu-id="e0e69-210">Hello nœud et disque majoritaires également est une option valide.</span><span class="sxs-lookup"><span data-stu-id="e0e69-210">hello Node and Disk Majority also is a valid option.</span></span> <span data-ttu-id="e0e69-211">Dans un environnement de production, nous vous recommandons d’utiliser un disque quorum.</span><span class="sxs-lookup"><span data-stu-id="e0e69-211">In a production environment, we recommend that you use a quorum disk.</span></span> <span data-ttu-id="e0e69-212">Vous pouvez utiliser le réseau et stockage toomake de technologie système hautement disponibles.</span><span class="sxs-lookup"><span data-stu-id="e0e69-212">You can use network and storage system technology toomake it highly available.</span></span>

![Figure 1 : Exemple de configuration de clustering de basculement Windows Server pour SAP ASCS/SCS dans Azure][sap-ha-guide-figure-1000]

<span data-ttu-id="e0e69-214">_**Figure 1 :** Exemple de configuration de clustering de basculement Windows Server pour SAP ASCS/SCS dans Azure_</span><span class="sxs-lookup"><span data-stu-id="e0e69-214">_**Figure 1:** Example of a Windows Server Failover Clustering configuration for SAP ASCS/SCS in Azure_</span></span>

### <span data-ttu-id="e0e69-215"><a name="be21cf3e-fb01-402b-9955-54fbecf66592"></a> Stockage partagé</span><span class="sxs-lookup"><span data-stu-id="e0e69-215"><a name="be21cf3e-fb01-402b-9955-54fbecf66592"></a> Shared storage</span></span>
<span data-ttu-id="e0e69-216">La figure 1 illustre également un cluster de stockage partagé à deux nœuds.</span><span class="sxs-lookup"><span data-stu-id="e0e69-216">Figure 1 also shows a two-node shared storage cluster.</span></span> <span data-ttu-id="e0e69-217">Dans un cluster de stockage partagé local, tous les nœuds de cluster de hello détectent le stockage partagé.</span><span class="sxs-lookup"><span data-stu-id="e0e69-217">In an on-premises shared storage cluster, all nodes in hello cluster detect shared storage.</span></span> <span data-ttu-id="e0e69-218">Un mécanisme de verrouillage protège les données de hello contre d’éventuels dommages.</span><span class="sxs-lookup"><span data-stu-id="e0e69-218">A locking mechanism protects hello data from corruption.</span></span> <span data-ttu-id="e0e69-219">Tous les nœuds peuvent détecter si un autre nœud échoue.</span><span class="sxs-lookup"><span data-stu-id="e0e69-219">All nodes can detect if another node fails.</span></span> <span data-ttu-id="e0e69-220">Si un nœud échoue, nœud restant de hello prend possession des ressources de stockage hello et garantit la disponibilité de hello des services.</span><span class="sxs-lookup"><span data-stu-id="e0e69-220">If one node fails, hello remaining node takes ownership of hello storage resources and ensures hello availability of services.</span></span>

> [!NOTE]
> <span data-ttu-id="e0e69-221">Avec certaines applications de SGBD, telles que SQL Server, vous n’avez pas besoin de disques partagés pour atteindre une haute disponibilité.</span><span class="sxs-lookup"><span data-stu-id="e0e69-221">You don't need shared disks for high availability with some DBMS applications, like with SQL Server.</span></span> <span data-ttu-id="e0e69-222">SQL Server Always On réplique les fichiers de données et les journaux du SGBD à partir du disque local de hello de disque local de la toohello de nœud d’un cluster d’un autre nœud de cluster.</span><span class="sxs-lookup"><span data-stu-id="e0e69-222">SQL Server Always On replicates DBMS data and log files from hello local disk of one cluster node toohello local disk of another cluster node.</span></span> <span data-ttu-id="e0e69-223">Dans ce cas, configuration du cluster Windows hello n’a pas besoin d’un disque partagé.</span><span class="sxs-lookup"><span data-stu-id="e0e69-223">In that case, hello Windows cluster configuration doesn't need a shared disk.</span></span>
>
>

### <span data-ttu-id="e0e69-224"><a name="ff7a9a06-2bc5-4b20-860a-46cdb44669cd"></a> Mise en réseau et résolution de noms</span><span class="sxs-lookup"><span data-stu-id="e0e69-224"><a name="ff7a9a06-2bc5-4b20-860a-46cdb44669cd"></a> Networking and name resolution</span></span>
<span data-ttu-id="e0e69-225">Les ordinateurs clients d’accéder cluster de hello sur une adresse IP virtuelle et un nom d’hôte virtuel que hello fournit du serveur DNS.</span><span class="sxs-lookup"><span data-stu-id="e0e69-225">Client computers reach hello cluster over a virtual IP address and a virtual host name that hello DNS server provides.</span></span> <span data-ttu-id="e0e69-226">Hello nœuds sur site et le serveur DNS de hello peut gérer plusieurs adresses IP.</span><span class="sxs-lookup"><span data-stu-id="e0e69-226">hello on-premises nodes and hello DNS server can handle multiple IP addresses.</span></span>

<span data-ttu-id="e0e69-227">Dans une installation type, vous utilisez deux ou plusieurs connexions réseau :</span><span class="sxs-lookup"><span data-stu-id="e0e69-227">In a typical setup, you use two or more network connections:</span></span>

* <span data-ttu-id="e0e69-228">Un stockage de toohello connexion dédiée</span><span class="sxs-lookup"><span data-stu-id="e0e69-228">A dedicated connection toohello storage</span></span>
* <span data-ttu-id="e0e69-229">Une connexion de réseau interne de cluster pour la vérification des pulsations hello</span><span class="sxs-lookup"><span data-stu-id="e0e69-229">A cluster-internal network connection for hello heartbeat</span></span>
* <span data-ttu-id="e0e69-230">Un réseau public que les clients utilisent tooconnect toohello cluster</span><span class="sxs-lookup"><span data-stu-id="e0e69-230">A public network that clients use tooconnect toohello cluster</span></span>

## <span data-ttu-id="e0e69-231"><a name="2ddba413-a7f5-4e4e-9a51-87908879c10a"></a> Clustering de basculement Windows Server dans Azure</span><span class="sxs-lookup"><span data-stu-id="e0e69-231"><a name="2ddba413-a7f5-4e4e-9a51-87908879c10a"></a> Windows Server Failover Clustering in Azure</span></span>
<span data-ttu-id="e0e69-232">Comparé les déploiements de cloud privé ou complète toobare, les Machines virtuelles Azure nécessite tooconfigure des étapes supplémentaires Clustering de basculement Windows Server.</span><span class="sxs-lookup"><span data-stu-id="e0e69-232">Compared toobare metal or private cloud deployments, Azure Virtual Machines requires additional steps tooconfigure Windows Server Failover Clustering.</span></span> <span data-ttu-id="e0e69-233">Lorsque vous créez un disque de cluster partagé, vous devez tooset plusieurs adresses IP et l’hôte virtuel des noms d’instance de SAP ASCS/SCS hello.</span><span class="sxs-lookup"><span data-stu-id="e0e69-233">When you build a shared cluster disk, you need tooset several IP addresses and virtual host names for hello SAP ASCS/SCS instance.</span></span>

<span data-ttu-id="e0e69-234">Dans cet article, nous présentent les concepts clés et hello toobuild requis d’étapes supplémentaires un cluster de haute disponibilité des services centrale SAP dans Azure.</span><span class="sxs-lookup"><span data-stu-id="e0e69-234">In this article, we discuss key concepts and hello additional steps required toobuild an SAP high-availability central services cluster in Azure.</span></span> <span data-ttu-id="e0e69-235">Nous vous indiquons comment tooset des hello un outil tiers SIOS DataKeeper, et comment tooconfigure hello Azure interne l’équilibrage de charge.</span><span class="sxs-lookup"><span data-stu-id="e0e69-235">We show you how tooset up hello third-party tool SIOS DataKeeper, and how tooconfigure hello Azure internal load balancer.</span></span> <span data-ttu-id="e0e69-236">Vous pouvez utiliser ces outils de toocreate un cluster de basculement Windows avec un témoin de partage de fichiers dans Azure.</span><span class="sxs-lookup"><span data-stu-id="e0e69-236">You can use these tools toocreate a Windows failover cluster with a file share witness in Azure.</span></span>

![Figure 2 : Configuration du clustering de basculement Windows Server dans Azure sans disque partagé][sap-ha-guide-figure-1001]

<span data-ttu-id="e0e69-238">_**Figure 2 :** Configuration du clustering de basculement Windows Server dans Azure sans disque partagé_</span><span class="sxs-lookup"><span data-stu-id="e0e69-238">_**Figure 2:** Windows Server Failover Clustering configuration in Azure without a shared disk_</span></span>

### <span data-ttu-id="e0e69-239"><a name="1a464091-922b-48d7-9d08-7cecf757f341"></a> Disque partagé dans Azure avec SIOS DataKeeper</span><span class="sxs-lookup"><span data-stu-id="e0e69-239"><a name="1a464091-922b-48d7-9d08-7cecf757f341"></a> Shared disk in Azure with SIOS DataKeeper</span></span>
<span data-ttu-id="e0e69-240">Vous avez besoin d’un stockage partagé en cluster pour bénéficier d’une instance SAP ASCS/SCS à haute disponibilité.</span><span class="sxs-lookup"><span data-stu-id="e0e69-240">You need cluster shared storage for a high-availability SAP ASCS/SCS instance.</span></span> <span data-ttu-id="e0e69-241">Comme de septembre 2016, Azure n’offre pas un stockage partagé que vous pouvez utiliser toocreate un cluster de stockage partagé.</span><span class="sxs-lookup"><span data-stu-id="e0e69-241">As of September 2016, Azure doesn't offer shared storage that you can use toocreate a shared storage cluster.</span></span> <span data-ttu-id="e0e69-242">Vous pouvez utiliser un logiciel tiers SIOS DataKeeper Cluster Edition toocreate un stockage en miroir qui simule le stockage partagé de cluster.</span><span class="sxs-lookup"><span data-stu-id="e0e69-242">You can use third-party software SIOS DataKeeper Cluster Edition toocreate a mirrored storage that simulates cluster shared storage.</span></span> <span data-ttu-id="e0e69-243">Hello solution SIOS assure une réplication synchrone des données en temps réel.</span><span class="sxs-lookup"><span data-stu-id="e0e69-243">hello SIOS solution provides real-time synchronous data replication.</span></span> <span data-ttu-id="e0e69-244">Voici comment créer une ressource de disque partagé pour un cluster :</span><span class="sxs-lookup"><span data-stu-id="e0e69-244">This is how you can create a shared disk resource for a cluster:</span></span>

1. <span data-ttu-id="e0e69-245">Attacher un tooeach supplémentaires Azure disque dur virtuel (VHD) de hello machines () dans une configuration de cluster Windows.</span><span class="sxs-lookup"><span data-stu-id="e0e69-245">Attach an additional Azure virtual hard disk (VHD) tooeach of hello virtual machines (VMs) in a Windows cluster configuration.</span></span>
2. <span data-ttu-id="e0e69-246">Exécutez SIOS DataKeeper Cluster Edition sur les deux nœuds de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="e0e69-246">Run SIOS DataKeeper Cluster Edition on both virtual machine nodes.</span></span>
3. <span data-ttu-id="e0e69-247">Configurer le Cluster SIOS DataKeeper Edition afin qu’elle reflète le contenu du volume de disque dur virtuel attaché supplémentaire hello de hello source toohello supplémentaires disque dur virtuel attaché volume de machine virtuelle de la machine virtuelle cible hello hello.</span><span class="sxs-lookup"><span data-stu-id="e0e69-247">Configure SIOS DataKeeper Cluster Edition so that it mirrors hello content of hello additional VHD attached volume from hello source virtual machine toohello additional VHD attached volume of hello target virtual machine.</span></span> <span data-ttu-id="e0e69-248">SIOS DataKeeper résume les volumes locaux hello source et cible et les présente ensuite tooWindows Clustering de basculement de serveur en tant qu’un disque partagé.</span><span class="sxs-lookup"><span data-stu-id="e0e69-248">SIOS DataKeeper abstracts hello source and target local volumes, and then presents them tooWindows Server Failover Clustering as one shared disk.</span></span>

<span data-ttu-id="e0e69-249">Vous trouverez plus d’informations sur SIOS DataKeeper [ici](http://us.sios.com/products/datakeeper-cluster/).</span><span class="sxs-lookup"><span data-stu-id="e0e69-249">Get more information about [SIOS DataKeeper](http://us.sios.com/products/datakeeper-cluster/).</span></span>

![Figure 3 : Configuration du clustering de basculement Windows Server dans Azure à l’aide de SIOS DataKeeper][sap-ha-guide-figure-1002]

<span data-ttu-id="e0e69-251">_**Figure 3 :** Configuration du clustering de basculement Windows Server dans Azure à l’aide de SIOS DataKeeper_</span><span class="sxs-lookup"><span data-stu-id="e0e69-251">_**Figure 3:** Windows Server Failover Clustering configuration in Azure with SIOS DataKeeper_</span></span>

> [!NOTE]
> <span data-ttu-id="e0e69-252">Avec certains SGBD, tels que SQL Server, vous n’avez pas besoin de disques partagés pour atteindre une haute disponibilité.</span><span class="sxs-lookup"><span data-stu-id="e0e69-252">You don't need shared disks for high availability with some DBMS products, like SQL Server.</span></span> <span data-ttu-id="e0e69-253">SQL Server Always On réplique les fichiers de données et les journaux du SGBD à partir du disque local de hello de disque local de la toohello de nœud d’un cluster d’un autre nœud de cluster.</span><span class="sxs-lookup"><span data-stu-id="e0e69-253">SQL Server Always On replicates DBMS data and log files from hello local disk of one cluster node toohello local disk of another cluster node.</span></span> <span data-ttu-id="e0e69-254">Dans ce cas, configuration du cluster Windows hello n’a pas besoin d’un disque partagé.</span><span class="sxs-lookup"><span data-stu-id="e0e69-254">In this case, hello Windows cluster configuration doesn't need a shared disk.</span></span>
>
>

### <span data-ttu-id="e0e69-255"><a name="44641e18-a94e-431f-95ff-303ab65e0bcb"></a> Résolution de noms dans Azure</span><span class="sxs-lookup"><span data-stu-id="e0e69-255"><a name="44641e18-a94e-431f-95ff-303ab65e0bcb"></a> Name resolution in Azure</span></span>
<span data-ttu-id="e0e69-256">plateforme de cloud computing Azure Hello n’offre pas hello option tooconfigure adresses IP virtuelles, telles que les adresses IP flottantes.</span><span class="sxs-lookup"><span data-stu-id="e0e69-256">hello Azure cloud platform doesn't offer hello option tooconfigure virtual IP addresses, such as floating IP addresses.</span></span> <span data-ttu-id="e0e69-257">Vous avez besoin d’un tooset autre solution d’une virtuel tooreach hello cluster ressource d’adresse IP dans le cloud de hello.</span><span class="sxs-lookup"><span data-stu-id="e0e69-257">You need an alternative solution tooset up a virtual IP address tooreach hello cluster resource in hello cloud.</span></span>
<span data-ttu-id="e0e69-258">Azure a un équilibreur de charge interne Bonjour service d’équilibrage de charge Azure.</span><span class="sxs-lookup"><span data-stu-id="e0e69-258">Azure has an internal load balancer in hello Azure Load Balancer service.</span></span> <span data-ttu-id="e0e69-259">Avec équilibrage de charge interne hello, les clients atteindre cluster de hello sur l’adresse IP virtuelle du cluster hello.</span><span class="sxs-lookup"><span data-stu-id="e0e69-259">With hello internal load balancer, clients reach hello cluster over hello cluster virtual IP address.</span></span>
<span data-ttu-id="e0e69-260">Vous avez besoin d’équilibreur de charge interne toodeploy hello dans le groupe de ressources hello qui contient les nœuds de cluster hello.</span><span class="sxs-lookup"><span data-stu-id="e0e69-260">You need toodeploy hello internal load balancer in hello resource group that contains hello cluster nodes.</span></span> <span data-ttu-id="e0e69-261">Ensuite, configurez tous les ports nécessaires, règles de transfert avec une sonde hello ports d’équilibrage de charge interne hello.</span><span class="sxs-lookup"><span data-stu-id="e0e69-261">Then, configure all necessary port forwarding rules with hello probe ports of hello internal load balancer.</span></span>
<span data-ttu-id="e0e69-262">les clients de Hello peuvent se connecter via un nom d’hôte virtuel hello.</span><span class="sxs-lookup"><span data-stu-id="e0e69-262">hello clients can connect via hello virtual host name.</span></span> <span data-ttu-id="e0e69-263">serveur DNS de Hello résout l’adresse IP du cluster hello et port d’handles équilibrage de charge interne hello toohello le nœud actif du cluster de hello de transfert.</span><span class="sxs-lookup"><span data-stu-id="e0e69-263">hello DNS server resolves hello cluster IP address, and hello internal load balancer handles port forwarding toohello active node of hello cluster.</span></span>

## <span data-ttu-id="e0e69-264"><a name="2e3fec50-241e-441b-8708-0b1864f66dfa"></a> Haute disponibilité pour SAP NetWeaver dans Azure IaaS (Infrastructure as a Service)</span><span class="sxs-lookup"><span data-stu-id="e0e69-264"><a name="2e3fec50-241e-441b-8708-0b1864f66dfa"></a> SAP NetWeaver high availability in Azure Infrastructure-as-a-Service (IaaS)</span></span>
<span data-ttu-id="e0e69-265">tooachieve SAP haute disponibilité des applications, par exemple pour les composants logiciels SAP, vous devez hello tooprotect suivant des composants :</span><span class="sxs-lookup"><span data-stu-id="e0e69-265">tooachieve SAP application high availability, such as for SAP software components, you need tooprotect hello following components:</span></span>

* <span data-ttu-id="e0e69-266">Instance de serveur d’applications SAP</span><span class="sxs-lookup"><span data-stu-id="e0e69-266">SAP Application Server instance</span></span>
* <span data-ttu-id="e0e69-267">Instance SAP ASCS/SCS</span><span class="sxs-lookup"><span data-stu-id="e0e69-267">SAP ASCS/SCS instance</span></span>
* <span data-ttu-id="e0e69-268">Serveur SGBD</span><span class="sxs-lookup"><span data-stu-id="e0e69-268">DBMS server</span></span>

<span data-ttu-id="e0e69-269">Pour plus d’informations sur la protection des composants SAP dans des scénarios de haute disponibilité, consultez [Planification et implémentation de machines virtuelles Azure pour SAP NetWeaver](planning-guide.md).</span><span class="sxs-lookup"><span data-stu-id="e0e69-269">For more information about protecting SAP components in high-availability scenarios, see [Azure Virtual Machines planning and implementation for SAP NetWeaver](planning-guide.md).</span></span>

### <span data-ttu-id="e0e69-270"><a name="93faa747-907e-440a-b00a-1ae0a89b1c0e"></a> Serveur d’applications SAP à haute disponibilité</span><span class="sxs-lookup"><span data-stu-id="e0e69-270"><a name="93faa747-907e-440a-b00a-1ae0a89b1c0e"></a> High-availability SAP Application Server</span></span>
<span data-ttu-id="e0e69-271">Vous ne devez généralement une solution de haute disponibilité spécifique pour les instances de serveur d’applications SAP et de la boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="e0e69-271">You usually don't need a specific high-availability solution for hello SAP Application Server and dialog instances.</span></span> <span data-ttu-id="e0e69-272">La haute disponibilité s’obtient par redondance, et vous configurez plusieurs instances de dialogue sur différentes instances de machines virtuelles Azure.</span><span class="sxs-lookup"><span data-stu-id="e0e69-272">You achieve high availability by redundancy, and you'll configure multiple dialog instances in different instances of Azure Virtual Machines.</span></span> <span data-ttu-id="e0e69-273">Vous devez avoir au moins deux instances d’applications SAP installées dans deux instances de machines virtuelles Azure.</span><span class="sxs-lookup"><span data-stu-id="e0e69-273">You should have at least two SAP application instances installed in two instances of Azure Virtual Machines.</span></span>

![Figure 4 : Serveur d’applications SAP à haute disponibilité][sap-ha-guide-figure-2000]

<span data-ttu-id="e0e69-275">_**Figure 4 :** Serveur d’applications SAP à haute disponibilité_</span><span class="sxs-lookup"><span data-stu-id="e0e69-275">_**Figure 4:** High-availability SAP Application Server_</span></span>

<span data-ttu-id="e0e69-276">Vous devez placer tous les ordinateurs virtuels que les instances de serveur d’applications SAP d’hôte hello même groupe à haute disponibilité Azure.</span><span class="sxs-lookup"><span data-stu-id="e0e69-276">You must place all virtual machines that host SAP Application Server instances in hello same Azure availability set.</span></span> <span data-ttu-id="e0e69-277">Un groupe à haute disponibilité Azure garantit que :</span><span class="sxs-lookup"><span data-stu-id="e0e69-277">An Azure availability set ensures that:</span></span>

* <span data-ttu-id="e0e69-278">Tous les ordinateurs virtuels font partie de hello même domaine de mise à niveau.</span><span class="sxs-lookup"><span data-stu-id="e0e69-278">All virtual machines are part of hello same upgrade domain.</span></span> <span data-ttu-id="e0e69-279">Un domaine de mise à niveau, par exemple, permet de s’assurer que les ordinateurs virtuels de hello ne sont pas mis à jour à hello même temps pendant le temps mort de maintenance planifiée.</span><span class="sxs-lookup"><span data-stu-id="e0e69-279">An upgrade domain, for example, makes sure that hello virtual machines aren't updated at hello same time during planned maintenance downtime.</span></span>
* <span data-ttu-id="e0e69-280">Tous les ordinateurs virtuels font partie de hello même domaine par défaut.</span><span class="sxs-lookup"><span data-stu-id="e0e69-280">All virtual machines are part of hello same fault domain.</span></span> <span data-ttu-id="e0e69-281">Un domaine d’erreur, par exemple, permet de s’assurer que les ordinateurs virtuels sont déployés afin qu’aucun point de défaillance unique n’affecte la disponibilité de hello de tous les ordinateurs virtuels.</span><span class="sxs-lookup"><span data-stu-id="e0e69-281">A fault domain, for example, makes sure that virtual machines are deployed so that no single point of failure affects hello availability of all virtual machines.</span></span>

<span data-ttu-id="e0e69-282">En savoir plus sur la façon trop[gérer la disponibilité hello des machines virtuelles][virtual-machines-manage-availability].</span><span class="sxs-lookup"><span data-stu-id="e0e69-282">Learn more about how too[manage hello availability of virtual machines][virtual-machines-manage-availability].</span></span>

<span data-ttu-id="e0e69-283">Hello compte de stockage Azure est un point de défaillance unique potentiel, il est important toohave au moins deux comptes de stockage Azure, dans laquelle au moins deux ordinateurs virtuels sont distribuées.</span><span class="sxs-lookup"><span data-stu-id="e0e69-283">Because hello Azure storage account is a potential single point of failure, it's important toohave at least two Azure storage accounts, in which at least two virtual machines are distributed.</span></span> <span data-ttu-id="e0e69-284">Dans une configuration idéale, disques hello de chaque ordinateur virtuel qui exécute une instance de la boîte de dialogue SAP sont déployées dans un autre compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="e0e69-284">In an ideal setup, hello disks of each virtual machine that is running an SAP dialog instance would be deployed in a different storage account.</span></span>

### <span data-ttu-id="e0e69-285"><a name="f559c285-ee68-4eec-add1-f60fe7b978db"></a> Instance SAP ASCS/SCS à haute disponibilité</span><span class="sxs-lookup"><span data-stu-id="e0e69-285"><a name="f559c285-ee68-4eec-add1-f60fe7b978db"></a> High-availability SAP ASCS/SCS instance</span></span>
<span data-ttu-id="e0e69-286">La figure 5 est un exemple d’instance SAP ASCS/SCS à haute disponibilité.</span><span class="sxs-lookup"><span data-stu-id="e0e69-286">Figure 5 is an example of a high-availability SAP ASCS/SCS instance.</span></span>

![Figure 5 : Instance SAP ASCS/SCS à haute disponibilité][sap-ha-guide-figure-2001]

<span data-ttu-id="e0e69-288">_**Figure 5 :** Instance SAP ASCS/SCS à haute disponibilité_</span><span class="sxs-lookup"><span data-stu-id="e0e69-288">_**Figure 5:** High-availability SAP ASCS/SCS instance_</span></span>

#### <span data-ttu-id="e0e69-289"><a name="b5b1fd0b-1db4-4d49-9162-de07a0132a51"></a> Haute disponibilité de l’instance SAP ASCS/SCS avec le clustering de basculement Windows Server dans Azure</span><span class="sxs-lookup"><span data-stu-id="e0e69-289"><a name="b5b1fd0b-1db4-4d49-9162-de07a0132a51"></a> SAP ASCS/SCS instance high availability with Windows Server Failover Clustering in Azure</span></span>
<span data-ttu-id="e0e69-290">Comparé les déploiements de cloud privé ou complète toobare, les Machines virtuelles Azure nécessite tooconfigure des étapes supplémentaires Clustering de basculement Windows Server.</span><span class="sxs-lookup"><span data-stu-id="e0e69-290">Compared toobare metal or private cloud deployments, Azure Virtual Machines requires additional steps tooconfigure Windows Server Failover Clustering.</span></span> <span data-ttu-id="e0e69-291">toobuild un cluster de basculement Windows, vous devez un disque de cluster partagé, plusieurs adresses IP, plusieurs noms d’hôte virtuel et un équilibrage de charge interne Azure pour le clustering d’une instance SAP ASCS/SCS.</span><span class="sxs-lookup"><span data-stu-id="e0e69-291">toobuild a Windows failover cluster, you need a shared cluster disk, several IP addresses, several virtual host names, and an Azure internal load balancer for clustering an SAP ASCS/SCS instance.</span></span> <span data-ttu-id="e0e69-292">Nous aborderons cela plus en détail plus loin dans l’article de hello.</span><span class="sxs-lookup"><span data-stu-id="e0e69-292">We discuss this in more detail later in hello article.</span></span>

![Figure 6 : Configuration du clustering de basculement Windows Server pour une instance SAP ASCS/SCS dans Azure à l’aide de SIOS DataKeeper][sap-ha-guide-figure-1002]

<span data-ttu-id="e0e69-294">_**Figure 6 :** Configuration du clustering de basculement Windows Server pour une instance SAP ASCS/SCS dans Azure à l’aide de SIOS DataKeeper_</span><span class="sxs-lookup"><span data-stu-id="e0e69-294">_**Figure 6:** Windows Server Failover Clustering for an SAP ASCS/SCS configuration in Azure with SIOS DataKeeper_</span></span>

### <span data-ttu-id="e0e69-295"><a name="ddd878a0-9c2f-4b8e-8968-26ce60be1027"></a> Instance SGBD à haute disponibilité</span><span class="sxs-lookup"><span data-stu-id="e0e69-295"><a name="ddd878a0-9c2f-4b8e-8968-26ce60be1027"></a>High-availability DBMS instance</span></span>
<span data-ttu-id="e0e69-296">Hello SGBD est également un point de contact unique dans un système SAP.</span><span class="sxs-lookup"><span data-stu-id="e0e69-296">hello DBMS also is a single point of contact in an SAP system.</span></span> <span data-ttu-id="e0e69-297">Vous devez tooprotect à l’aide d’une solution de haute disponibilité.</span><span class="sxs-lookup"><span data-stu-id="e0e69-297">You need tooprotect it by using a high-availability solution.</span></span> <span data-ttu-id="e0e69-298">La figure 7 illustre une solution de haute disponibilité SQL Server Always On dans Azure, avec le Clustering de basculement Windows Server et hello Azure interne l’équilibrage de charge.</span><span class="sxs-lookup"><span data-stu-id="e0e69-298">Figure 7 shows a SQL Server Always On high-availability solution in Azure, with Windows Server Failover Clustering and hello Azure internal load balancer.</span></span> <span data-ttu-id="e0e69-299">SQL Server Always On réplique les fichiers journaux et les données du SGBD à l’aide de sa propre réplication de SGBD.</span><span class="sxs-lookup"><span data-stu-id="e0e69-299">SQL Server Always On replicates DBMS data and log files by using its own DBMS replication.</span></span> <span data-ttu-id="e0e69-300">Dans ce cas, vous ne devez disques de cluster partagés, qui simplifie la configuration entière de hello.</span><span class="sxs-lookup"><span data-stu-id="e0e69-300">In this case, you don't need cluster shared disks, which simplifies hello entire setup.</span></span>

![Figure 7 : Exemple de SGBD SAP à haute disponibilité avec SQL Server Always On][sap-ha-guide-figure-2003]

<span data-ttu-id="e0e69-302">_**Figure 7 :** Exemple de SGBD SAP à haute disponibilité avec SQL Server Always On_</span><span class="sxs-lookup"><span data-stu-id="e0e69-302">_**Figure 7:** Example of a high-availability SAP DBMS, with SQL Server Always On_</span></span>

<span data-ttu-id="e0e69-303">Pour plus d’informations sur les clusters SQL Server dans Azure à l’aide du modèle de déploiement du Gestionnaire de ressources Azure hello, voir les articles suivants :</span><span class="sxs-lookup"><span data-stu-id="e0e69-303">For more information about clustering SQL Server in Azure by using hello Azure Resource Manager deployment model, see these articles:</span></span>

* <span data-ttu-id="e0e69-304">[Configurer un groupe de disponibilité Always On dans des machines virtuelles manuellement à l’aide du modèle Resource Manager][virtual-machines-windows-portal-sql-alwayson-availability-groups-manual]</span><span class="sxs-lookup"><span data-stu-id="e0e69-304">[Configure Always On availability group in Azure Virtual Machines manually by using Resource Manager][virtual-machines-windows-portal-sql-alwayson-availability-groups-manual]</span></span>
* <span data-ttu-id="e0e69-305">[Configurer un équilibreur de charge interne Azure pour un groupe de disponibilité AlwaysOn dans Azure][virtual-machines-windows-portal-sql-alwayson-int-listener]</span><span class="sxs-lookup"><span data-stu-id="e0e69-305">[Configure an Azure internal load balancer for an Always On availability group in Azure][virtual-machines-windows-portal-sql-alwayson-int-listener]</span></span>

## <span data-ttu-id="e0e69-306"><a name="045252ed-0277-4fc8-8f46-c5a29694a816"></a> Scénarios de déploiement à haute disponibilité de bout en bout</span><span class="sxs-lookup"><span data-stu-id="e0e69-306"><a name="045252ed-0277-4fc8-8f46-c5a29694a816"></a> End-to-end high-availability deployment scenarios</span></span>

### <a name="deployment-scenario-using-architectural-template-1"></a><span data-ttu-id="e0e69-307">Scénario de déploiement à l’aide du modèle architectural n°1</span><span class="sxs-lookup"><span data-stu-id="e0e69-307">Deployment scenario using Architectural Template 1</span></span>

<span data-ttu-id="e0e69-308">La figure 8 illustre une architecture SAP NetWeaver à haute disponibilité dans Azure pour **un** système SAP.</span><span class="sxs-lookup"><span data-stu-id="e0e69-308">Figure 8 shows an example of an SAP NetWeaver high-availability architecture in Azure for **one** SAP system.</span></span> <span data-ttu-id="e0e69-309">Ce scénario est défini comme suit :</span><span class="sxs-lookup"><span data-stu-id="e0e69-309">This scenario is set up as follows:</span></span>

- <span data-ttu-id="e0e69-310">Un cluster dédié est utilisé pour l’instance de SAP ASCS/SCS hello.</span><span class="sxs-lookup"><span data-stu-id="e0e69-310">One dedicated cluster is used for hello SAP ASCS/SCS instance.</span></span>
- <span data-ttu-id="e0e69-311">Un cluster dédié est utilisé pour l’instance de SGBD hello.</span><span class="sxs-lookup"><span data-stu-id="e0e69-311">One dedicated cluster is used for hello DBMS instance.</span></span>
- <span data-ttu-id="e0e69-312">Des instances de serveurs d’applications SAP sont déployées dans des machines virtuelles dédiées.</span><span class="sxs-lookup"><span data-stu-id="e0e69-312">SAP Application Server instances are deployed in their own dedicated VMs.</span></span>

![Figure 8 : Modèle d’architecture SAP à haute disponibilité n°1, avec un cluster dédié à ASCS/SCS et SGBD][sap-ha-guide-figure-2004]

<span data-ttu-id="e0e69-314">_**Figure 8 :** Modèle d’architecture SAP à haute disponibilité n°1, avec des clusters dédiés à ASCS/SCS et SGBD_</span><span class="sxs-lookup"><span data-stu-id="e0e69-314">_**Figure 8:** SAP high-availability Architectural Template 1, dedicated clusters for ASCS/SCS and DBMS_</span></span>

### <a name="deployment-scenario-using-architectural-template-2"></a><span data-ttu-id="e0e69-315">Scénario de déploiement à l’aide du modèle architectural n°2</span><span class="sxs-lookup"><span data-stu-id="e0e69-315">Deployment scenario using Architectural Template 2</span></span>

<span data-ttu-id="e0e69-316">La figure 9 illustre une architecture SAP NetWeaver à haute disponibilité dans Azure pour **un** système SAP.</span><span class="sxs-lookup"><span data-stu-id="e0e69-316">Figure 9 shows an example of an SAP NetWeaver high-availability architecture in Azure for **one** SAP system.</span></span> <span data-ttu-id="e0e69-317">Ce scénario est défini comme suit :</span><span class="sxs-lookup"><span data-stu-id="e0e69-317">This scenario is set up as follows:</span></span>

- <span data-ttu-id="e0e69-318">Un cluster dédié est utilisé pour **les deux** hello SAP ASCS/SCS d’instance et hello SGBD.</span><span class="sxs-lookup"><span data-stu-id="e0e69-318">One dedicated cluster is used for **both** hello SAP ASCS/SCS instance and hello DBMS.</span></span>
- <span data-ttu-id="e0e69-319">Des instances de serveurs d’applications SAP sont déployées dans leurs propres machines virtuelles dédiées.</span><span class="sxs-lookup"><span data-stu-id="e0e69-319">SAP Application Server instances are deployed in own dedicated VMs.</span></span>

![Figure 9 : Modèle d’architecture SAP à haute disponibilité n°2, avec un cluster dédié à l’instance ASCS/SCS et un cluster dédié à SGBD][sap-ha-guide-figure-2005]

<span data-ttu-id="e0e69-321">_**Figure 9 :** Modèle d’architecture SAP à haute disponibilité n°2, avec un cluster dédié à l’instance ASCS/SCS et un cluster dédié à SGBD_</span><span class="sxs-lookup"><span data-stu-id="e0e69-321">_**Figure 9:** SAP high-availability Architectural Template 2, with a dedicated cluster for ASCS/SCS and a dedicated cluster for DBMS_</span></span>

### <a name="deployment-scenario-using-architectural-template-3"></a><span data-ttu-id="e0e69-322">Scénario de déploiement à l’aide du modèle architectural n°3</span><span class="sxs-lookup"><span data-stu-id="e0e69-322">Deployment scenario using Architectural Template 3</span></span>

<span data-ttu-id="e0e69-323">La figure 10 montre une architecture SAP NetWeaver à haute disponibilité dans Azure pour **deux** systèmes SAP, avec &lt;SID1&gt; et &lt;SID2&gt;.</span><span class="sxs-lookup"><span data-stu-id="e0e69-323">Figure 10 shows an example of an SAP NetWeaver high-availability architecture in Azure for **two** SAP systems, with &lt;SID1&gt; and &lt;SID2&gt;.</span></span> <span data-ttu-id="e0e69-324">Ce scénario est défini comme suit :</span><span class="sxs-lookup"><span data-stu-id="e0e69-324">This scenario is set up as follows:</span></span>

- <span data-ttu-id="e0e69-325">Un cluster dédié est utilisé pour **les deux** instance de hello SAP ASCS/SCS SID1 *et* l’instance hello SAP ASCS/SCS SID2 (un cluster).</span><span class="sxs-lookup"><span data-stu-id="e0e69-325">One dedicated cluster is used for **both** hello SAP ASCS/SCS SID1 instance *and* hello SAP ASCS/SCS SID2 instance (one cluster).</span></span>
- <span data-ttu-id="e0e69-326">Un cluster dédié est utilisé pour SGBD SID1, et un autre cluster dédié est utilisé pour SGBD SID2 (deux clusters).</span><span class="sxs-lookup"><span data-stu-id="e0e69-326">One dedicated cluster is used for DBMS SID1, and another dedicated cluster is used for DBMS SID2 (two clusters).</span></span>
- <span data-ttu-id="e0e69-327">Instances de serveur d’applications SAP pourquoi le système SAP SID1 ont leurs propres ordinateurs virtuels dédiés.</span><span class="sxs-lookup"><span data-stu-id="e0e69-327">SAP Application Server instances for hello SAP system SID1 have their own dedicated VMs.</span></span>
- <span data-ttu-id="e0e69-328">Instances de serveur d’applications SAP pourquoi le système SAP SID2 ont leurs propres ordinateurs virtuels dédiés.</span><span class="sxs-lookup"><span data-stu-id="e0e69-328">SAP Application Server instances for hello SAP system SID2 have their own dedicated VMs.</span></span>

![Figure 10 : Modèle d’architecture SAP à haute disponibilité n°3, avec un cluster dédié aux différentes instances ASCS/SCS][sap-ha-guide-figure-6003]

<span data-ttu-id="e0e69-330">_**Figure 10 :** Modèle d’architecture SAP à haute disponibilité n°3, avec un cluster dédié aux différentes instances ASCS/SCS_</span><span class="sxs-lookup"><span data-stu-id="e0e69-330">_**Figure 10:** SAP high-availability Architectural Template 3, with a dedicated cluster for different ASCS/SCS instances_</span></span>

## <span data-ttu-id="e0e69-331"><a name="78092dbe-165b-454c-92f5-4972bdbef9bf"></a>Préparer l’infrastructure de hello</span><span class="sxs-lookup"><span data-stu-id="e0e69-331"><a name="78092dbe-165b-454c-92f5-4972bdbef9bf"></a> Prepare hello infrastructure</span></span>

### <a name="prepare-hello-infrastructure-for-architectural-template-1"></a><span data-ttu-id="e0e69-332">Préparer l’infrastructure de hello pour architecture modèle 1</span><span class="sxs-lookup"><span data-stu-id="e0e69-332">Prepare hello infrastructure for Architectural Template 1</span></span>
<span data-ttu-id="e0e69-333">Les modèles Azure Resource Manager pour SAP simplifient le déploiement des ressources requises.</span><span class="sxs-lookup"><span data-stu-id="e0e69-333">Azure Resource Manager templates for SAP help simplify deployment of required resources.</span></span>

<span data-ttu-id="e0e69-334">modèles à trois niveaux de Hello dans Azure Resource Manager prennent également en charge des scénarios de haute disponibilité, comme dans l’architecture 1 de modèle, qui a deux clusters.</span><span class="sxs-lookup"><span data-stu-id="e0e69-334">hello three-tier templates in Azure Resource Manager also support high-availability scenarios, such as in Architectural Template 1, which has two clusters.</span></span> <span data-ttu-id="e0e69-335">Chaque cluster constitue un point de défaillance pour l’instance SAP ASCS/SCS et l’instance SGBD.</span><span class="sxs-lookup"><span data-stu-id="e0e69-335">Each cluster is an SAP single point of failure for SAP ASCS/SCS and DBMS.</span></span>

<span data-ttu-id="e0e69-336">Voici où obtenir des modèles Azure Resource Manager pour le scénario d’exemple hello que nous décrivons dans cet article :</span><span class="sxs-lookup"><span data-stu-id="e0e69-336">Here's where you can get Azure Resource Manager templates for hello example scenario we describe in this article:</span></span>

* [<span data-ttu-id="e0e69-337">Image Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="e0e69-337">Azure Marketplace image</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-marketplace-image)  
* [<span data-ttu-id="e0e69-338">Image personnalisée</span><span class="sxs-lookup"><span data-stu-id="e0e69-338">Custom image</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-user-image)

<span data-ttu-id="e0e69-339">infrastructure de hello tooprepare pour architecture modèle 1 :</span><span class="sxs-lookup"><span data-stu-id="e0e69-339">tooprepare hello infrastructure for Architectural Template 1:</span></span>

- <span data-ttu-id="e0e69-340">Bonjour portail Azure, sur hello **paramètres** panneau, Bonjour **SYSTEMAVAILABILITY** boîte, sélectionnez **HA**.</span><span class="sxs-lookup"><span data-stu-id="e0e69-340">In hello Azure portal, on hello **Parameters** blade, in hello **SYSTEMAVAILABILITY** box, select **HA**.</span></span>

  ![Figure 11 : Définir les paramètres Azure Resource Manager de haute disponibilité SAP][sap-ha-guide-figure-3000]

<span data-ttu-id="e0e69-342">_**Figure 11 :** Définir les paramètres Azure Resource Manager de haute disponibilité SAP_</span><span class="sxs-lookup"><span data-stu-id="e0e69-342">_**Figure 11:** Set SAP high-availability Azure Resource Manager parameters_</span></span>


  <span data-ttu-id="e0e69-343">créent des modèles de Hello :</span><span class="sxs-lookup"><span data-stu-id="e0e69-343">hello templates create:</span></span>

  * <span data-ttu-id="e0e69-344">**Des machines virtuelles** :</span><span class="sxs-lookup"><span data-stu-id="e0e69-344">**Virtual machines**:</span></span>
    * <span data-ttu-id="e0e69-345">Des machines virtuelles de serveur d’applications SAP : <*SIDSystèmeSAP*>-di-<*Numéro*></span><span class="sxs-lookup"><span data-stu-id="e0e69-345">SAP Application Server virtual machines: <*SAPSystemSID*>-di-<*Number*></span></span>
    * <span data-ttu-id="e0e69-346">Des machines virtuelles de cluster ASCS/SCS : <*SIDSystèmeSAP*>-ascs-<*Numéro*></span><span class="sxs-lookup"><span data-stu-id="e0e69-346">ASCS/SCS cluster virtual machines: <*SAPSystemSID*>-ascs-<*Number*></span></span>
    * <span data-ttu-id="e0e69-347">Cluster SGBD : <*SIDSystèmeSAP*>-db-<*Numéro*></span><span class="sxs-lookup"><span data-stu-id="e0e69-347">DBMS cluster: <*SAPSystemSID*>-db-<*Number*></span></span>

  * <span data-ttu-id="e0e69-348">**Des cartes réseau pour toutes les machines virtuelles, avec une adresse IP associée** :</span><span class="sxs-lookup"><span data-stu-id="e0e69-348">**Network cards for all virtual machines, with associated IP addresses**:</span></span>
    * <span data-ttu-id="e0e69-349"><*SIDSystèmeSAP*&gt;-nic-di-&lt;*Numéro*></span><span class="sxs-lookup"><span data-stu-id="e0e69-349"><*SAPSystemSID*>-nic-di-<*Number*></span></span>
    * <span data-ttu-id="e0e69-350"><*SIDSystèmeSAP*&gt;-nic-ascs-&lt;*Numéro*></span><span class="sxs-lookup"><span data-stu-id="e0e69-350"><*SAPSystemSID*>-nic-ascs-<*Number*></span></span>
    * <span data-ttu-id="e0e69-351"><*SIDSystèmeSAP*&gt;-nic-db-&lt;*Numéro*></span><span class="sxs-lookup"><span data-stu-id="e0e69-351"><*SAPSystemSID*>-nic-db-<*Number*></span></span>

  * <span data-ttu-id="e0e69-352">**Des comptes de stockage Azure**</span><span class="sxs-lookup"><span data-stu-id="e0e69-352">**Azure storage accounts**</span></span>

  * <span data-ttu-id="e0e69-353">**Des groupes de disponibilité** pour :</span><span class="sxs-lookup"><span data-stu-id="e0e69-353">**Availability groups** for:</span></span>
    * <span data-ttu-id="e0e69-354">Les machines virtuelles de serveur d’applications SAP : <*SIDSystèmeSAP*>-avset-di</span><span class="sxs-lookup"><span data-stu-id="e0e69-354">SAP Application Server virtual machines: <*SAPSystemSID*>-avset-di</span></span>
    * <span data-ttu-id="e0e69-355">Les machines virtuelles de cluster SAP ASCS/SCS : <*SIDSystèmeSAP*>-avset-ascs</span><span class="sxs-lookup"><span data-stu-id="e0e69-355">SAP ASCS/SCS cluster virtual machines: <*SAPSystemSID*>-avset-ascs</span></span>
    * <span data-ttu-id="e0e69-356">Les machines virtuelles de cluster SGBD : <*SIDSystèmeSAP*>-avset-db</span><span class="sxs-lookup"><span data-stu-id="e0e69-356">DBMS cluster virtual machines: <*SAPSystemSID*>-avset-db</span></span>

  * <span data-ttu-id="e0e69-357">**Un équilibrage de charge interne Azure** :</span><span class="sxs-lookup"><span data-stu-id="e0e69-357">**Azure internal load balancer**:</span></span>
    * <span data-ttu-id="e0e69-358">Avec tous les ports pour l’instance ASCS/SCS hello et l’adresse IP <*SAPSystemSID*> - lb - ASC</span><span class="sxs-lookup"><span data-stu-id="e0e69-358">With all ports for hello ASCS/SCS instance and IP address <*SAPSystemSID*>-lb-ascs</span></span>
    * <span data-ttu-id="e0e69-359">Avec tous les ports pour hello système SGBD de SQL Server et l’adresse IP <*SAPSystemSID*> - lb - db</span><span class="sxs-lookup"><span data-stu-id="e0e69-359">With all ports for hello SQL Server DBMS and IP address <*SAPSystemSID*>-lb-db</span></span>

  * <span data-ttu-id="e0e69-360">**Un groupe de sécurité réseau** : &lt;*SIDSystèmeSAP*&gt;-nsg-ascs-0</span><span class="sxs-lookup"><span data-stu-id="e0e69-360">**Network security group**: <*SAPSystemSID*>-nsg-ascs-0</span></span>  
    * <span data-ttu-id="e0e69-361">Avec un toohello de port de protocole RDP (Remote Desktop) externe ouvrir <*SAPSystemSID*> - ASC - 0 virtual machine</span><span class="sxs-lookup"><span data-stu-id="e0e69-361">With an open external Remote Desktop Protocol (RDP) port toohello <*SAPSystemSID*>-ascs-0 virtual machine</span></span>

> [!NOTE]
> <span data-ttu-id="e0e69-362">Toutes les adresses IP des cartes réseau de hello et équilibreurs de charge interne Azure sont **dynamique** par défaut.</span><span class="sxs-lookup"><span data-stu-id="e0e69-362">All IP addresses of hello network cards and Azure internal load balancers are **dynamic** by default.</span></span> <span data-ttu-id="e0e69-363">Modifiez-les trop**statique** des adresses IP.</span><span class="sxs-lookup"><span data-stu-id="e0e69-363">Change them too**static** IP addresses.</span></span> <span data-ttu-id="e0e69-364">Nous allons décrire comment toodo cela plus loin dans l’article de hello.</span><span class="sxs-lookup"><span data-stu-id="e0e69-364">We describe how toodo this later in hello article.</span></span>
>
>

### <span data-ttu-id="e0e69-365"><a name="c87a8d3f-b1dc-4d2f-b23c-da4b72977489"></a>Déployer des ordinateurs virtuels avec toouse (entre sites) de connectivité de réseau d’entreprise en production</span><span class="sxs-lookup"><span data-stu-id="e0e69-365"><a name="c87a8d3f-b1dc-4d2f-b23c-da4b72977489"></a> Deploy virtual machines with corporate network connectivity (cross-premises) toouse in production</span></span>
<span data-ttu-id="e0e69-366">Pour les systèmes SAP de production, déployez les machines virtuelles Azure avec une [connectivité de réseau d’entreprise (intersite)][planning-guide-2.2] à l’aide d’un VPN de site à site Azure ou d’Azure ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="e0e69-366">For production SAP systems, deploy Azure virtual machines with [corporate network connectivity (cross-premises)][planning-guide-2.2] by using Azure Site-to-Site VPN or Azure ExpressRoute.</span></span>

> [!NOTE]
> <span data-ttu-id="e0e69-367">Vous pouvez utiliser votre instance de réseau virtuel Azure.</span><span class="sxs-lookup"><span data-stu-id="e0e69-367">You can use your Azure Virtual Network instance.</span></span> <span data-ttu-id="e0e69-368">sous-réseau et réseau virtuel de hello ont déjà été créés et préparés.</span><span class="sxs-lookup"><span data-stu-id="e0e69-368">hello virtual network and subnet have already been created and prepared.</span></span>
>
>

1.  <span data-ttu-id="e0e69-369">Bonjour portail Azure, sur hello **paramètres** panneau, Bonjour **NEWOREXISTINGSUBNET** boîte, sélectionnez **existant**.</span><span class="sxs-lookup"><span data-stu-id="e0e69-369">In hello Azure portal, on hello **Parameters** blade, in hello **NEWOREXISTINGSUBNET** box, select **existing**.</span></span>
2.  <span data-ttu-id="e0e69-370">Bonjour **IDSOUSRÉSEAU** zone, ajouter hello de chaîne complet de votre réseau Azure préparée IDSousRéseau où vous prévoyez toodeploy vos machines virtuelles Azure.</span><span class="sxs-lookup"><span data-stu-id="e0e69-370">In hello **SUBNETID** box, add hello full string of your prepared Azure network SubnetID where you plan toodeploy your Azure virtual machines.</span></span>
3.  <span data-ttu-id="e0e69-371">tooget une liste de tous les sous-réseaux du réseau Azure, exécutez la commande PowerShell :</span><span class="sxs-lookup"><span data-stu-id="e0e69-371">tooget a list of all Azure network subnets, run this PowerShell command:</span></span>

  ```PowerShell
  (Get-AzureRmVirtualNetwork -Name <azureVnetName>  -ResourceGroupName <ResourceGroupOfVNET>).Subnets
  ```

  <span data-ttu-id="e0e69-372">Hello **ID** champ affiche hello **IDSOUSRÉSEAU**.</span><span class="sxs-lookup"><span data-stu-id="e0e69-372">hello **ID** field shows hello **SUBNETID**.</span></span>
4. <span data-ttu-id="e0e69-373">tooget une liste de tous les **IDSOUSRÉSEAU** valeurs, exécutez la commande PowerShell :</span><span class="sxs-lookup"><span data-stu-id="e0e69-373">tooget a list of all **SUBNETID** values, run this PowerShell command:</span></span>

  ```PowerShell
  (Get-AzureRmVirtualNetwork -Name <azureVnetName>  -ResourceGroupName <ResourceGroupOfVNET>).Subnets.Id
  ```

  <span data-ttu-id="e0e69-374">Hello **IDSOUSRÉSEAU** ressemble à ceci :</span><span class="sxs-lookup"><span data-stu-id="e0e69-374">hello **SUBNETID** looks like this:</span></span>

  ```
  /subscriptions/<SubscriptionId>/resourceGroups/<VPNName>/providers/Microsoft.Network/virtualNetworks/azureVnet/subnets/<SubnetName>
  ```

### <span data-ttu-id="e0e69-375"><a name="7fe9af0e-3cce-495b-a5ec-dcb4d8e0a310"></a> Déployer des instances SAP dans le cloud uniquement à des fins de test et de démonstration</span><span class="sxs-lookup"><span data-stu-id="e0e69-375"><a name="7fe9af0e-3cce-495b-a5ec-dcb4d8e0a310"></a> Deploy cloud-only SAP instances for test and demo</span></span>
<span data-ttu-id="e0e69-376">Vous pouvez déployer votre système SAP à haute disponibilité dans un modèle de déploiement cloud uniquement.</span><span class="sxs-lookup"><span data-stu-id="e0e69-376">You can deploy your high-availability SAP system in a cloud-only deployment model.</span></span> <span data-ttu-id="e0e69-377">Ce type de déploiement est surtout utile pour les démonstrations et les tests.</span><span class="sxs-lookup"><span data-stu-id="e0e69-377">This kind of deployment primarily is useful for demo and test use cases.</span></span> <span data-ttu-id="e0e69-378">Il ne convient pas à une utilisation en production.</span><span class="sxs-lookup"><span data-stu-id="e0e69-378">It's not suited for production use cases.</span></span>

- <span data-ttu-id="e0e69-379">Bonjour portail Azure, sur hello **paramètres** panneau, Bonjour **NEWOREXISTINGSUBNET** boîte, sélectionnez **nouveau**.</span><span class="sxs-lookup"><span data-stu-id="e0e69-379">In hello Azure portal, on hello **Parameters** blade, in hello **NEWOREXISTINGSUBNET** box, select **new**.</span></span> <span data-ttu-id="e0e69-380">Laissez hello **IDSOUSRÉSEAU** champ vide.</span><span class="sxs-lookup"><span data-stu-id="e0e69-380">Leave hello **SUBNETID** field empty.</span></span>

  <span data-ttu-id="e0e69-381">Hello crée automatiquement le Gestionnaire des ressources SAP Azure hello sous-réseau et réseau virtuel Azure.</span><span class="sxs-lookup"><span data-stu-id="e0e69-381">hello SAP Azure Resource Manager template automatically creates hello Azure virtual network and subnet.</span></span>

> [!NOTE]
> <span data-ttu-id="e0e69-382">Vous devez également toodeploy au moins l’un dédié machine virtuelle pour Active Directory et DNS dans hello la même instance de réseau virtuel Azure.</span><span class="sxs-lookup"><span data-stu-id="e0e69-382">You also need toodeploy at least one dedicated virtual machine for Active Directory and DNS in hello same Azure Virtual Network instance.</span></span> <span data-ttu-id="e0e69-383">modèle de Hello ne crée pas ces ordinateurs virtuels.</span><span class="sxs-lookup"><span data-stu-id="e0e69-383">hello template doesn't create these virtual machines.</span></span>
>
>


### <a name="prepare-hello-infrastructure-for-architectural-template-2"></a><span data-ttu-id="e0e69-384">Préparer infrastructure de hello pour architecture modèle 2</span><span class="sxs-lookup"><span data-stu-id="e0e69-384">Prepare hello infrastructure for Architectural Template 2</span></span>

<span data-ttu-id="e0e69-385">Vous pouvez utiliser ce modèle de gestionnaire de ressources Azure pour SAP toohelp simplifier le déploiement des ressources de l’infrastructure requise pour 2 modèle Architectural de SAP.</span><span class="sxs-lookup"><span data-stu-id="e0e69-385">You can use this Azure Resource Manager template for SAP toohelp simplify deployment of required infrastructure resources for SAP Architectural Template 2.</span></span>

<span data-ttu-id="e0e69-386">Voici où vous pouvez obtenir des modèles Azure Resource Manager pour ce scénario de déploiement :</span><span class="sxs-lookup"><span data-stu-id="e0e69-386">Here's where you can get Azure Resource Manager templates for this deployment scenario:</span></span>

* [<span data-ttu-id="e0e69-387">Image Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="e0e69-387">Azure Marketplace image</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-marketplace-image-converged)  
* [<span data-ttu-id="e0e69-388">Image personnalisée</span><span class="sxs-lookup"><span data-stu-id="e0e69-388">Custom image</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-user-image-converged)


### <a name="prepare-hello-infrastructure-for-architectural-template-3"></a><span data-ttu-id="e0e69-389">Préparer infrastructure de hello pour les modèles architecturaux de 3</span><span class="sxs-lookup"><span data-stu-id="e0e69-389">Prepare hello infrastructure for Architectural Template 3</span></span>

<span data-ttu-id="e0e69-390">Vous pouvez préparer l’infrastructure de hello et configurer SAP pour **multi-SID**.</span><span class="sxs-lookup"><span data-stu-id="e0e69-390">You can prepare hello infrastructure and configure SAP for **multi-SID**.</span></span> <span data-ttu-id="e0e69-391">Par exemple, vous pouvez ajouter une instance SAP ASCS/SCS supplémentaire à une configuration de cluster *existante*.</span><span class="sxs-lookup"><span data-stu-id="e0e69-391">For example, you can add an additional SAP ASCS/SCS instance into an *existing* cluster configuration.</span></span> <span data-ttu-id="e0e69-392">Pour plus d’informations, consultez [configurer une instance SAP ASCS/SCS supplémentaire dans un toocreate de configuration de cluster existant une configuration de multi-SID SAP dans Azure Resource Manager][sap-ha-multi-sid-guide].</span><span class="sxs-lookup"><span data-stu-id="e0e69-392">For more information, see [Configure an additional SAP ASCS/SCS instance into an existing cluster configuration toocreate an SAP multi-SID configuration in Azure Resource Manager][sap-ha-multi-sid-guide].</span></span>

<span data-ttu-id="e0e69-393">Si vous voulez toocreate un nouveau cluster multi-SID, vous pouvez utiliser hello multi-SID [modèles de démarrage rapide sur GitHub](https://github.com/Azure/azure-quickstart-templates).</span><span class="sxs-lookup"><span data-stu-id="e0e69-393">If you want toocreate a new multi-SID cluster, you can use hello multi-SID [quickstart templates on GitHub](https://github.com/Azure/azure-quickstart-templates).</span></span>
<span data-ttu-id="e0e69-394">toocreate un nouveau cluster multi-SID, vous devez hello toodeploy suivant trois modèles :</span><span class="sxs-lookup"><span data-stu-id="e0e69-394">toocreate a new multi-SID cluster, you need toodeploy hello following three templates:</span></span>

* [<span data-ttu-id="e0e69-395">Modèle ASCS/SCS</span><span class="sxs-lookup"><span data-stu-id="e0e69-395">ASCS/SCS template</span></span>](#ASCS-SCS-template)
* [<span data-ttu-id="e0e69-396">Modèle de base de données</span><span class="sxs-lookup"><span data-stu-id="e0e69-396">Database template</span></span>](#database-template)
* [<span data-ttu-id="e0e69-397">Modèle de serveurs d’applications</span><span class="sxs-lookup"><span data-stu-id="e0e69-397">Application servers template</span></span>](#application-servers-template)

<span data-ttu-id="e0e69-398">Hello sections suivantes incluent des informations supplémentaires sur les modèles hello et paramètres hello tooprovide dans les modèles de hello.</span><span class="sxs-lookup"><span data-stu-id="e0e69-398">hello following sections have more details about hello templates and hello parameters you need tooprovide in hello templates.</span></span>

#### <span data-ttu-id="e0e69-399"><a name="ASCS-SCS-template"></a> Modèle ASCS/SCS</span><span class="sxs-lookup"><span data-stu-id="e0e69-399"><a name="ASCS-SCS-template"></a> ASCS/SCS template</span></span>

<span data-ttu-id="e0e69-400">modèle ASCS/SCS Hello déploie les deux ordinateurs virtuels que vous pouvez utiliser toocreate un cluster de basculement Windows Server qui héberge plusieurs instances ASCS/SCS.</span><span class="sxs-lookup"><span data-stu-id="e0e69-400">hello ASCS/SCS template deploys two virtual machines that you can use toocreate a Windows Server failover cluster that hosts multiple ASCS/SCS instances.</span></span>

<span data-ttu-id="e0e69-401">tooset modèle hello ASCS/SCS multi-SID, Bonjour [modèle de multi-SID ASCS/SCS][sap-templates-3-tier-multisid-xscs-marketplace-image], entrez des valeurs pour hello paramètres suivants :</span><span class="sxs-lookup"><span data-stu-id="e0e69-401">tooset up hello ASCS/SCS multi-SID template, in hello [ASCS/SCS multi-SID template][sap-templates-3-tier-multisid-xscs-marketplace-image], enter values for hello following parameters:</span></span>

  - <span data-ttu-id="e0e69-402">**Préfixe de ressource**.</span><span class="sxs-lookup"><span data-stu-id="e0e69-402">**Resource Prefix**.</span></span>  <span data-ttu-id="e0e69-403">Définir le préfixe de ressource hello, qui est utilisé tooprefix toutes les ressources qui sont créés au cours du déploiement de hello.</span><span class="sxs-lookup"><span data-stu-id="e0e69-403">Set hello resource prefix, which is used tooprefix all resources that are created during hello deployment.</span></span> <span data-ttu-id="e0e69-404">Étant donné que les ressources hello ne font pas partie d’un même système SAP tooonly, préfixe hello de ressource de hello n’est pas hello SID d’un système SAP.</span><span class="sxs-lookup"><span data-stu-id="e0e69-404">Because hello resources do not belong tooonly one SAP system, hello prefix of hello resource is not hello SID of one SAP system.</span></span>  <span data-ttu-id="e0e69-405">préfixe de Hello doit être comprise entre **trois à six caractères**.</span><span class="sxs-lookup"><span data-stu-id="e0e69-405">hello prefix must be between **three and six characters**.</span></span>
  - <span data-ttu-id="e0e69-406">**Type de pile**.</span><span class="sxs-lookup"><span data-stu-id="e0e69-406">**Stack Type**.</span></span> <span data-ttu-id="e0e69-407">Sélectionnez le type de pile hello Hello système SAP.</span><span class="sxs-lookup"><span data-stu-id="e0e69-407">Select hello stack type of hello SAP system.</span></span> <span data-ttu-id="e0e69-408">Selon le type de pile hello, équilibrage de charge Azure a un (ABAP ou Java uniquement) ou deux (ABAP + Java) des adresses IP privées par le système SAP.</span><span class="sxs-lookup"><span data-stu-id="e0e69-408">Depending on hello stack type, Azure Load Balancer has one (ABAP or Java only) or two (ABAP+Java) private IP addresses per SAP system.</span></span>
  -  <span data-ttu-id="e0e69-409">**Type de système d’exploitation**.</span><span class="sxs-lookup"><span data-stu-id="e0e69-409">**OS Type**.</span></span> <span data-ttu-id="e0e69-410">Sélectionnez le système d’exploitation de hello d’ordinateurs virtuels hello.</span><span class="sxs-lookup"><span data-stu-id="e0e69-410">Select hello operating system of hello virtual machines.</span></span>
  -  <span data-ttu-id="e0e69-411">**Nombre de systèmes SAP**.</span><span class="sxs-lookup"><span data-stu-id="e0e69-411">**SAP System Count**.</span></span> <span data-ttu-id="e0e69-412">Sélectionnez le nombre de hello de systèmes SAP, vous souhaitez tooinstall dans ce cluster.</span><span class="sxs-lookup"><span data-stu-id="e0e69-412">Select hello number of SAP systems you want tooinstall in this cluster.</span></span>
  -  <span data-ttu-id="e0e69-413">**Disponibilité du système**.</span><span class="sxs-lookup"><span data-stu-id="e0e69-413">**System Availability**.</span></span> <span data-ttu-id="e0e69-414">Sélectionnez la haute disponibilité **(HA)**.</span><span class="sxs-lookup"><span data-stu-id="e0e69-414">Select **HA**.</span></span>
  -  <span data-ttu-id="e0e69-415">**Nom d’utilisateur et mot de passe d’administrateur**.</span><span class="sxs-lookup"><span data-stu-id="e0e69-415">**Admin Username and Admin Password**.</span></span> <span data-ttu-id="e0e69-416">Créer un utilisateur qui peut être utilisé toosign dans toohello machine.</span><span class="sxs-lookup"><span data-stu-id="e0e69-416">Create a new user that can be used toosign in toohello machine.</span></span>
  -  <span data-ttu-id="e0e69-417">**Sous-réseau nouveau ou existant**.</span><span class="sxs-lookup"><span data-stu-id="e0e69-417">**New Or Existing Subnet**.</span></span> <span data-ttu-id="e0e69-418">Déterminez s’il faut créer un réseau virtuel et un sous-réseau, ou utiliser un sous-réseau existant.</span><span class="sxs-lookup"><span data-stu-id="e0e69-418">Set whether a new virtual network and subnet should be created, or an existing subnet should be used.</span></span> <span data-ttu-id="e0e69-419">Si vous disposez déjà d’un réseau virtuel qui est le réseau local de tooyour connecté, sélectionnez **existant**.</span><span class="sxs-lookup"><span data-stu-id="e0e69-419">If you already have a virtual network that is connected tooyour on-premises network, select **existing**.</span></span>
  -  <span data-ttu-id="e0e69-420">**ID du sous-réseau**. ID de hello l’ensemble d’ordinateurs virtuels hello sous-réseau toowhich hello doit être connecté.</span><span class="sxs-lookup"><span data-stu-id="e0e69-420">**Subnet Id**. Set hello ID of hello subnet toowhich hello virtual machines should be connected.</span></span> <span data-ttu-id="e0e69-421">Sélectionnez sous-réseau hello de votre réseau privé virtuel (VPN) ou de réseau local de tooyour ExpressRoute réseau virtuel tooconnect hello de machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="e0e69-421">Select hello subnet of your virtual private network (VPN) or ExpressRoute virtual network tooconnect hello virtual machine tooyour on-premises network.</span></span> <span data-ttu-id="e0e69-422">ID de Hello ressemble généralement à ceci :</span><span class="sxs-lookup"><span data-stu-id="e0e69-422">hello ID usually looks like this:</span></span>

   <span data-ttu-id="e0e69-423">/subscriptions/<*subscription id*>/resourceGroups/<*resource group name*>/providers/Microsoft.Network/virtualNetworks/<*virtual network name*>/subnets/<*subnet name*></span><span class="sxs-lookup"><span data-stu-id="e0e69-423">/subscriptions/<*subscription id*>/resourceGroups/<*resource group name*>/providers/Microsoft.Network/virtualNetworks/<*virtual network name*>/subnets/<*subnet name*></span></span>

<span data-ttu-id="e0e69-424">modèle de Hello déploie une seule instance d’équilibrage de charge Azure, qui prend en charge plusieurs systèmes SAP.</span><span class="sxs-lookup"><span data-stu-id="e0e69-424">hello template deploys one Azure Load Balancer instance, which supports multiple SAP systems.</span></span>

- <span data-ttu-id="e0e69-425">Hello ASC sont configurées pour le numéro d’instance de 00, 10, 20...</span><span class="sxs-lookup"><span data-stu-id="e0e69-425">hello ASCS instances are configured for instance number 00, 10, 20...</span></span>
- <span data-ttu-id="e0e69-426">Hello SCS sont configurées pour le numéro d’instance 01, 11, 21...</span><span class="sxs-lookup"><span data-stu-id="e0e69-426">hello SCS instances are configured for instance number 01, 11, 21...</span></span>
- <span data-ttu-id="e0e69-427">Hello ASC Enqueue réplication serveur ERS (Linux uniquement) sont configurées pour le numéro d’instance 02, 12, 22...</span><span class="sxs-lookup"><span data-stu-id="e0e69-427">hello ASCS Enqueue Replication Server (ERS) (Linux only) instances are configured for instance number 02, 12, 22...</span></span>
- <span data-ttu-id="e0e69-428">Hello SCS ERS (Linux uniquement) sont configurées pour le numéro d’instance 03, 13, 23...</span><span class="sxs-lookup"><span data-stu-id="e0e69-428">hello SCS ERS (Linux only) instances are configured for instance number 03, 13, 23...</span></span>

<span data-ttu-id="e0e69-429">équilibrage de charge Hello contient 1 (2 pour Linux) VIP(s), 1 VIP x ASCS/SCS et adresse IP virtuelle de 1 x pour ERS (Linux uniquement).</span><span class="sxs-lookup"><span data-stu-id="e0e69-429">hello load balancer contains 1 (2 for Linux) VIP(s), 1x VIP for ASCS/SCS and 1x VIP for ERS (Linux only).</span></span>

<span data-ttu-id="e0e69-430">Hello liste suivante contient des règles (où x est le nombre de hello de hello système SAP, par exemple, 1, 2, 3, etc.) d’équilibrage de charge de toutes les :</span><span class="sxs-lookup"><span data-stu-id="e0e69-430">hello following list contains all load balancing rules (where x is hello number of hello SAP system, for example, 1, 2, 3...):</span></span>
- <span data-ttu-id="e0e69-431">Ports spécifiques de Windows pour chaque système SAP 445, 5985</span><span class="sxs-lookup"><span data-stu-id="e0e69-431">Windows-specific ports for every SAP system: 445, 5985</span></span>
- <span data-ttu-id="e0e69-432">Ports ASCS (numéro d’instance x0) : 32x0, 36x0, 39x0, 81x0, 5x013, 5x014, 5x016</span><span class="sxs-lookup"><span data-stu-id="e0e69-432">ASCS ports (instance number x0): 32x0, 36x0, 39x0, 81x0, 5x013, 5x014, 5x016</span></span>
- <span data-ttu-id="e0e69-433">Ports SCS (numéro d’instance x1) : 32x1, 33x1, 39x1, 81x1, 5x113, 5x114, 5x116</span><span class="sxs-lookup"><span data-stu-id="e0e69-433">SCS ports (instance number x1): 32x1, 33x1, 39x1, 81x1, 5x113, 5x114, 5x116</span></span>
- <span data-ttu-id="e0e69-434">Ports ASCS ERS sous Linux (numéro d’instance x2) : 33x2, 5x213, 5x214, 5x216</span><span class="sxs-lookup"><span data-stu-id="e0e69-434">ASCS ERS ports on Linux (instance number x2): 33x2, 5x213, 5x214, 5x216</span></span>
- <span data-ttu-id="e0e69-435">Ports SCS ERS sous Linux (numéro d’instance x3) : 33x3, 5x313, 5x314, 5x316</span><span class="sxs-lookup"><span data-stu-id="e0e69-435">SCS ERS ports on Linux (instance number x3): 33x3, 5x313, 5x314, 5x316</span></span>

<span data-ttu-id="e0e69-436">équilibrage de charge Hello est hello toouse configuré suivant des ports de sonde (où x est le nombre de hello de hello système SAP, par exemple, 1, 2, 3...) :</span><span class="sxs-lookup"><span data-stu-id="e0e69-436">hello load balancer is configured toouse hello following probe ports (where x is hello number of hello SAP system, for example, 1, 2, 3...):</span></span>
- <span data-ttu-id="e0e69-437">Port de sondage d’équilibrage de charge interne ASCS/SCS : 620x0</span><span class="sxs-lookup"><span data-stu-id="e0e69-437">ASCS/SCS internal load balancer probe port: 620x0</span></span>
- <span data-ttu-id="e0e69-438">Port de sondage d’équilibrage de charge interne ERS (Linux uniquement) : 621x2</span><span class="sxs-lookup"><span data-stu-id="e0e69-438">ERS internal load balancer probe port (Linux only): 621x2</span></span>

#### <span data-ttu-id="e0e69-439"><a name="database-template"></a> Modèle de base de données</span><span class="sxs-lookup"><span data-stu-id="e0e69-439"><a name="database-template"></a> Database template</span></span>

<span data-ttu-id="e0e69-440">modèle de base de données Hello déploie une ou deux machines virtuelles que vous pouvez utiliser tooinstall hello le système de gestion de base de données relationnelle (SGBDR) pour un système SAP.</span><span class="sxs-lookup"><span data-stu-id="e0e69-440">hello database template deploys one or two virtual machines that you can use tooinstall hello relational database management system (RDBMS) for one SAP system.</span></span> <span data-ttu-id="e0e69-441">Par exemple, si vous déployez un modèle ASCS/SCS pour les cinq systèmes SAP, vous devez toodeploy ce modèle cinq fois.</span><span class="sxs-lookup"><span data-stu-id="e0e69-441">For example, if you deploy an ASCS/SCS template for five SAP systems, you need toodeploy this template five times.</span></span>

<span data-ttu-id="e0e69-442">tooset modèle de multi-SID de base de données hello, Bonjour [modèle de base de données multi-SID][sap-templates-3-tier-multisid-db-marketplace-image], entrez des valeurs pour hello paramètres suivants :</span><span class="sxs-lookup"><span data-stu-id="e0e69-442">tooset up hello database multi-SID template, in hello [database multi-SID template][sap-templates-3-tier-multisid-db-marketplace-image], enter values for hello following parameters:</span></span>

  -  <span data-ttu-id="e0e69-443">**ID du système SAP**. Entrez l’ID du système SAP hello Hello système SAP tooinstall.</span><span class="sxs-lookup"><span data-stu-id="e0e69-443">**Sap System Id**. Enter hello SAP system ID of hello SAP system you want tooinstall.</span></span> <span data-ttu-id="e0e69-444">Hello ID sera utilisé en tant que préfixe pour les ressources hello qui sont déployés.</span><span class="sxs-lookup"><span data-stu-id="e0e69-444">hello ID will be used as a prefix for hello resources that are deployed.</span></span>
  -  <span data-ttu-id="e0e69-445">**Type de système d’exploitation**.</span><span class="sxs-lookup"><span data-stu-id="e0e69-445">**Os Type**.</span></span> <span data-ttu-id="e0e69-446">Sélectionnez le système d’exploitation de hello d’ordinateurs virtuels hello.</span><span class="sxs-lookup"><span data-stu-id="e0e69-446">Select hello operating system of hello virtual machines.</span></span>
  -  <span data-ttu-id="e0e69-447">**Type de base de données**.</span><span class="sxs-lookup"><span data-stu-id="e0e69-447">**Dbtype**.</span></span> <span data-ttu-id="e0e69-448">Sélectionnez le type de hello de base de données hello souhaité tooinstall sur le cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="e0e69-448">Select hello type of hello database you want tooinstall on hello cluster.</span></span> <span data-ttu-id="e0e69-449">Sélectionnez **SQL** si vous souhaitez tooinstall Microsoft SQL Server.</span><span class="sxs-lookup"><span data-stu-id="e0e69-449">Select **SQL** if you want tooinstall Microsoft SQL Server.</span></span> <span data-ttu-id="e0e69-450">Sélectionnez **HANA** si vous envisagez de tooinstall SAP HANA sur des machines virtuelles de hello.</span><span class="sxs-lookup"><span data-stu-id="e0e69-450">Select **HANA** if you plan tooinstall SAP HANA on hello virtual machines.</span></span> <span data-ttu-id="e0e69-451">Assurez-vous que tooselect hello type de système d’exploitation correct : sélectionnez **Windows** pour SQL, sélectionnez une distribution Linux pour HANA.</span><span class="sxs-lookup"><span data-stu-id="e0e69-451">Make sure tooselect hello correct operating system type: select **Windows** for SQL, and select a Linux distribution for HANA.</span></span> <span data-ttu-id="e0e69-452">Hello équilibrage de charge Azure qui est connecté toohello ordinateurs virtuels doivent être configurés type de base de données toosupport hello sélectionné :</span><span class="sxs-lookup"><span data-stu-id="e0e69-452">hello Azure Load Balancer that is connected toohello virtual machines will be configured toosupport hello selected database type:</span></span>
    * <span data-ttu-id="e0e69-453">**SQL**.</span><span class="sxs-lookup"><span data-stu-id="e0e69-453">**SQL**.</span></span> <span data-ttu-id="e0e69-454">équilibrage de charge Hello est le port 1433 équilibrer la charge.</span><span class="sxs-lookup"><span data-stu-id="e0e69-454">hello load balancer will load-balance port 1433.</span></span> <span data-ttu-id="e0e69-455">Assurez-vous que toouse ce port pour votre installation de SQL Server Always On.</span><span class="sxs-lookup"><span data-stu-id="e0e69-455">Make sure toouse this port for your SQL Server Always On setup.</span></span>
    * <span data-ttu-id="e0e69-456">**HANA**.</span><span class="sxs-lookup"><span data-stu-id="e0e69-456">**HANA**.</span></span> <span data-ttu-id="e0e69-457">équilibrage de charge Hello sera équilibrer la charge de ports 35015 et 35017.</span><span class="sxs-lookup"><span data-stu-id="e0e69-457">hello load balancer will load-balance ports 35015 and 35017.</span></span> <span data-ttu-id="e0e69-458">Assurez-vous que tooinstall SAP HANA avec numéro d’instance **50**.</span><span class="sxs-lookup"><span data-stu-id="e0e69-458">Make sure tooinstall SAP HANA with instance number **50**.</span></span>
    <span data-ttu-id="e0e69-459">équilibrage de charge Hello utilisera le port de la sonde 62550.</span><span class="sxs-lookup"><span data-stu-id="e0e69-459">hello load balancer will use probe port 62550.</span></span>
  -  <span data-ttu-id="e0e69-460">**Taille du système SAP**.</span><span class="sxs-lookup"><span data-stu-id="e0e69-460">**Sap System Size**.</span></span> <span data-ttu-id="e0e69-461">Nombre de hello ensemble du système de nouveau hello SAP fournit.</span><span class="sxs-lookup"><span data-stu-id="e0e69-461">Set hello number of SAPS hello new system will provide.</span></span> <span data-ttu-id="e0e69-462">Si vous n’êtes pas sûr du système de hello SAP combien nécessitera, demandez à votre partenaire technologique SAP ou un intégrateur de système.</span><span class="sxs-lookup"><span data-stu-id="e0e69-462">If you are not sure how many SAPS hello system will require, ask your SAP Technology Partner or System Integrator.</span></span>
  -  <span data-ttu-id="e0e69-463">**Disponibilité du système**.</span><span class="sxs-lookup"><span data-stu-id="e0e69-463">**System Availability**.</span></span> <span data-ttu-id="e0e69-464">Sélectionnez la haute disponibilité **(HA)**.</span><span class="sxs-lookup"><span data-stu-id="e0e69-464">Select **HA**.</span></span>
  -  <span data-ttu-id="e0e69-465">**Nom d’utilisateur et mot de passe d’administrateur**.</span><span class="sxs-lookup"><span data-stu-id="e0e69-465">**Admin Username and Admin Password**.</span></span> <span data-ttu-id="e0e69-466">Créer un utilisateur qui peut être utilisé toosign dans toohello machine.</span><span class="sxs-lookup"><span data-stu-id="e0e69-466">Create a new user that can be used toosign in toohello machine.</span></span>
  -  <span data-ttu-id="e0e69-467">**ID du sous-réseau**. Entrez hello les ID de sous-réseau hello que vous avez utilisé lors du déploiement hello du modèle ASCS/SCS hello ou hello de sous-réseau hello qui a été créé dans le cadre de hello déploiement de modèle ASCS/SCS.</span><span class="sxs-lookup"><span data-stu-id="e0e69-467">**Subnet Id**. Enter hello ID of hello subnet that you used during hello deployment of hello ASCS/SCS template, or hello ID of hello subnet that was created as part of hello ASCS/SCS template deployment.</span></span>

#### <span data-ttu-id="e0e69-468"><a name="application-servers-template"></a> Modèle de serveurs d’applications</span><span class="sxs-lookup"><span data-stu-id="e0e69-468"><a name="application-servers-template"></a> Application servers template</span></span>

<span data-ttu-id="e0e69-469">modèle de serveurs d’application Hello déploie deux ou plusieurs ordinateurs virtuels qui peut être utilisés en tant qu’instances de serveur d’applications SAP pour un système SAP.</span><span class="sxs-lookup"><span data-stu-id="e0e69-469">hello application servers template deploys two or more virtual machines that can be used as SAP Application Server instances for one SAP system.</span></span> <span data-ttu-id="e0e69-470">Par exemple, si vous déployez un modèle ASCS/SCS pour les cinq systèmes SAP, vous devez toodeploy ce modèle cinq fois.</span><span class="sxs-lookup"><span data-stu-id="e0e69-470">For example, if you deploy an ASCS/SCS template for five SAP systems, you need toodeploy this template five times.</span></span>

<span data-ttu-id="e0e69-471">tooset des hello serveurs multi-SID modèle d’application Bonjour [ce modèle d’application serveurs multi-SID][sap-templates-3-tier-multisid-apps-marketplace-image], entrez des valeurs pour hello paramètres suivants :</span><span class="sxs-lookup"><span data-stu-id="e0e69-471">tooset up hello application servers multi-SID template, in hello [application servers multi-SID template][sap-templates-3-tier-multisid-apps-marketplace-image], enter values for hello following parameters:</span></span>

  -  <span data-ttu-id="e0e69-472">**ID du système SAP**. Entrez l’ID du système SAP hello Hello système SAP tooinstall.</span><span class="sxs-lookup"><span data-stu-id="e0e69-472">**Sap System Id**. Enter hello SAP system ID of hello SAP system you want tooinstall.</span></span> <span data-ttu-id="e0e69-473">Hello ID sera utilisé en tant que préfixe pour les ressources hello qui sont déployés.</span><span class="sxs-lookup"><span data-stu-id="e0e69-473">hello ID will be used as a prefix for hello resources that are deployed.</span></span>
  -  <span data-ttu-id="e0e69-474">**Type de système d’exploitation**.</span><span class="sxs-lookup"><span data-stu-id="e0e69-474">**Os Type**.</span></span> <span data-ttu-id="e0e69-475">Sélectionnez le système d’exploitation de hello d’ordinateurs virtuels hello.</span><span class="sxs-lookup"><span data-stu-id="e0e69-475">Select hello operating system of hello virtual machines.</span></span>
  -  <span data-ttu-id="e0e69-476">**Taille du système SAP**.</span><span class="sxs-lookup"><span data-stu-id="e0e69-476">**Sap System Size**.</span></span> <span data-ttu-id="e0e69-477">nombre de Hello du nouveau système SAP hello fournissent.</span><span class="sxs-lookup"><span data-stu-id="e0e69-477">hello number of SAPS hello new system will provide.</span></span> <span data-ttu-id="e0e69-478">Si vous n’êtes pas sûr du système de hello SAP combien nécessitera, demandez à votre partenaire technologique SAP ou un intégrateur de système.</span><span class="sxs-lookup"><span data-stu-id="e0e69-478">If you are not sure how many SAPS hello system will require, ask your SAP Technology Partner or System Integrator.</span></span>
  -  <span data-ttu-id="e0e69-479">**Disponibilité du système**.</span><span class="sxs-lookup"><span data-stu-id="e0e69-479">**System Availability**.</span></span> <span data-ttu-id="e0e69-480">Sélectionnez la haute disponibilité **(HA)**.</span><span class="sxs-lookup"><span data-stu-id="e0e69-480">Select **HA**.</span></span>
  -  <span data-ttu-id="e0e69-481">**Nom d’utilisateur et mot de passe d’administrateur**.</span><span class="sxs-lookup"><span data-stu-id="e0e69-481">**Admin Username and Admin Password**.</span></span> <span data-ttu-id="e0e69-482">Créer un utilisateur qui peut être utilisé toosign dans toohello machine.</span><span class="sxs-lookup"><span data-stu-id="e0e69-482">Create a new user that can be used toosign in toohello machine.</span></span>
  -  <span data-ttu-id="e0e69-483">**ID du sous-réseau**. Entrez hello les ID de sous-réseau hello que vous avez utilisé lors du déploiement hello du modèle ASCS/SCS hello ou hello de sous-réseau hello qui a été créé dans le cadre de hello déploiement de modèle ASCS/SCS.</span><span class="sxs-lookup"><span data-stu-id="e0e69-483">**Subnet Id**. Enter hello ID of hello subnet that you used during hello deployment of hello ASCS/SCS template, or hello ID of hello subnet that was created as part of hello ASCS/SCS template deployment.</span></span>


### <span data-ttu-id="e0e69-484"><a name="47d5300a-a830-41d4-83dd-1a0d1ffdbe6a"></a> Réseau virtuel Azure</span><span class="sxs-lookup"><span data-stu-id="e0e69-484"><a name="47d5300a-a830-41d4-83dd-1a0d1ffdbe6a"></a> Azure virtual network</span></span>
<span data-ttu-id="e0e69-485">Dans notre exemple, espace d’adressage hello Hello réseau virtuel Azure est 10.0.0.0/16.</span><span class="sxs-lookup"><span data-stu-id="e0e69-485">In our example, hello address space of hello Azure virtual network is 10.0.0.0/16.</span></span> <span data-ttu-id="e0e69-486">Il existe un sous-réseau appelé **Subnet** (Sous-réseau), avec la plage d’adresses 10.0.0.0/24.</span><span class="sxs-lookup"><span data-stu-id="e0e69-486">There is one subnet called **Subnet**, with an address range of 10.0.0.0/24.</span></span> <span data-ttu-id="e0e69-487">L’ensemble des machines virtuelles et des équilibrages de charge internes sont déployés au sein de ce réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="e0e69-487">All virtual machines and internal load balancers are deployed in this virtual network.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e0e69-488">N’apportez aucune modification des paramètres de réseau toohello à l’intérieur du système d’exploitation de hello invité.</span><span class="sxs-lookup"><span data-stu-id="e0e69-488">Don't make any changes toohello network settings inside hello guest operating system.</span></span> <span data-ttu-id="e0e69-489">(adresses IP, serveurs DNS, sous-réseau, etc.).</span><span class="sxs-lookup"><span data-stu-id="e0e69-489">This includes IP addresses, DNS servers, and subnet.</span></span> <span data-ttu-id="e0e69-490">Configurez tous vos paramètres réseau dans Azure.</span><span class="sxs-lookup"><span data-stu-id="e0e69-490">Configure all your network settings in Azure.</span></span> <span data-ttu-id="e0e69-491">Hello service de Configuration protocole DHCP (Dynamic Host) propage vos paramètres.</span><span class="sxs-lookup"><span data-stu-id="e0e69-491">hello Dynamic Host Configuration Protocol (DHCP) service propagates your settings.</span></span>
>
>

### <span data-ttu-id="e0e69-492"><a name="b22d7b3b-4343-40ff-a319-097e13f62f9e"></a>Adresses IP DNS</span><span class="sxs-lookup"><span data-stu-id="e0e69-492"><a name="b22d7b3b-4343-40ff-a319-097e13f62f9e"></a> DNS IP addresses</span></span>

<span data-ttu-id="e0e69-493">tooset hello nécessaire que des adresses IP DNS, hello comme suit.</span><span class="sxs-lookup"><span data-stu-id="e0e69-493">tooset hello required DNS IP addresses, do hello following steps.</span></span>

1.  <span data-ttu-id="e0e69-494">Bonjour portail Azure, sur hello **serveurs DNS** panneau, assurez-vous que votre réseau virtuel **serveurs DNS** option a la valeur trop**personnalisé DNS**.</span><span class="sxs-lookup"><span data-stu-id="e0e69-494">In hello Azure portal, on hello **DNS servers** blade, make sure that your virtual network **DNS servers** option is set too**Custom DNS**.</span></span>
2.  <span data-ttu-id="e0e69-495">Sélectionnez vos paramètres en fonction de type hello du réseau que vous avez.</span><span class="sxs-lookup"><span data-stu-id="e0e69-495">Select your settings based on hello type of network you have.</span></span> <span data-ttu-id="e0e69-496">Pour plus d’informations, consultez hello suivant des ressources :</span><span class="sxs-lookup"><span data-stu-id="e0e69-496">For more information, see hello following resources:</span></span>
    * <span data-ttu-id="e0e69-497">[Connectivité de réseau d’entreprise (intersite)][planning-guide-2.2]: ajouter hello des adresses IP des serveurs DNS de local hello.</span><span class="sxs-lookup"><span data-stu-id="e0e69-497">[Corporate network connectivity (cross-premises)][planning-guide-2.2]: Add hello IP addresses of hello on-premises DNS servers.</span></span>  
    <span data-ttu-id="e0e69-498">Vous pouvez étendre locale DNS serveurs toohello machines virtuelles qui s’exécutent dans Azure.</span><span class="sxs-lookup"><span data-stu-id="e0e69-498">You can extend on-premises DNS servers toohello virtual machines that are running in Azure.</span></span> <span data-ttu-id="e0e69-499">Dans ce scénario, vous pouvez ajouter des adresses IP de hello Hello Azure des machines virtuelles sur lequel vous exécutez le service DNS hello.</span><span class="sxs-lookup"><span data-stu-id="e0e69-499">In that scenario, you can add hello IP addresses of hello Azure virtual machines on which you run hello DNS service.</span></span>
    * <span data-ttu-id="e0e69-500">[Déploiement de cloud uniquement][planning-guide-2.1]: déployer un ordinateur virtuel supplémentaire dans hello même instance de réseau virtuel qui sert à un serveur DNS.</span><span class="sxs-lookup"><span data-stu-id="e0e69-500">[Cloud-only deployment][planning-guide-2.1]: Deploy an additional virtual machine in hello same Virtual Network instance that serves as a DNS server.</span></span> <span data-ttu-id="e0e69-501">Ajouter des adresses IP hello Hello Azure des machines virtuelles que vous avez configuré le service DNS toorun.</span><span class="sxs-lookup"><span data-stu-id="e0e69-501">Add hello IP addresses of hello Azure virtual machines that you've set up toorun DNS service.</span></span>

    ![Figure 12 : Configurer les serveurs DNS du réseau virtuel Azure][sap-ha-guide-figure-3001]

    <span data-ttu-id="e0e69-503">_**Figure 12 :** Configurer les serveurs DNS du réseau virtuel Azure_</span><span class="sxs-lookup"><span data-stu-id="e0e69-503">_**Figure 12:** Configure DNS servers for Azure Virtual Network_</span></span>

  > [!NOTE]
  > <span data-ttu-id="e0e69-504">Si vous modifiez les adresses IP de hello des serveurs DNS de hello, vous devez toorestart hello machines virtuelles tooapply hello de modification et de propager les nouveaux serveurs DNS de hello.</span><span class="sxs-lookup"><span data-stu-id="e0e69-504">If you change hello IP addresses of hello DNS servers, you need toorestart hello Azure virtual machines tooapply hello change and propagate hello new DNS servers.</span></span>
  >
  >

<span data-ttu-id="e0e69-505">Dans notre exemple, hello service DNS est installé et configuré sur ces ordinateurs virtuels de Windows :</span><span class="sxs-lookup"><span data-stu-id="e0e69-505">In our example, hello DNS service is installed and configured on these Windows virtual machines:</span></span>

| <span data-ttu-id="e0e69-506">Rôle de la machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="e0e69-506">Virtual machine role</span></span> | <span data-ttu-id="e0e69-507">Nom d’hôte de la machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="e0e69-507">Virtual machine host name</span></span> | <span data-ttu-id="e0e69-508">Nom de la carte réseau</span><span class="sxs-lookup"><span data-stu-id="e0e69-508">Network card name</span></span> | <span data-ttu-id="e0e69-509">Adresse IP statique</span><span class="sxs-lookup"><span data-stu-id="e0e69-509">Static IP address</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="e0e69-510">Premier serveur DNS</span><span class="sxs-lookup"><span data-stu-id="e0e69-510">First DNS server</span></span> |<span data-ttu-id="e0e69-511">domcontr-0</span><span class="sxs-lookup"><span data-stu-id="e0e69-511">domcontr-0</span></span> |<span data-ttu-id="e0e69-512">pr1-nic-domcontr-0</span><span class="sxs-lookup"><span data-stu-id="e0e69-512">pr1-nic-domcontr-0</span></span> |<span data-ttu-id="e0e69-513">10.0.0.10</span><span class="sxs-lookup"><span data-stu-id="e0e69-513">10.0.0.10</span></span> |
| <span data-ttu-id="e0e69-514">Deuxième serveur DNS</span><span class="sxs-lookup"><span data-stu-id="e0e69-514">Second DNS server</span></span> |<span data-ttu-id="e0e69-515">domcontr-1</span><span class="sxs-lookup"><span data-stu-id="e0e69-515">domcontr-1</span></span> |<span data-ttu-id="e0e69-516">pr1-nic-domcontr-1</span><span class="sxs-lookup"><span data-stu-id="e0e69-516">pr1-nic-domcontr-1</span></span> |<span data-ttu-id="e0e69-517">10.0.0.11</span><span class="sxs-lookup"><span data-stu-id="e0e69-517">10.0.0.11</span></span> |

### <span data-ttu-id="e0e69-518"><a name="9fbd43c0-5850-4965-9726-2a921d85d73f"></a>Les noms d’hôte et des adresses IP statiques pour l’instance en cluster de SAP ASCS/SCS hello et l’instance en cluster du SGBD</span><span class="sxs-lookup"><span data-stu-id="e0e69-518"><a name="9fbd43c0-5850-4965-9726-2a921d85d73f"></a> Host names and static IP addresses for hello SAP ASCS/SCS clustered instance and DBMS clustered instance</span></span>

<span data-ttu-id="e0e69-519">Pour un déploiement local, vous avez besoin des noms d’hôtes et adresses IP réservés suivants :</span><span class="sxs-lookup"><span data-stu-id="e0e69-519">For on-premises deployment, you need these reserved host names and IP addresses:</span></span>

| <span data-ttu-id="e0e69-520">Rôle du nom d’hôte virtuel</span><span class="sxs-lookup"><span data-stu-id="e0e69-520">Virtual host name role</span></span> | <span data-ttu-id="e0e69-521">Nom d’hôte virtuel</span><span class="sxs-lookup"><span data-stu-id="e0e69-521">Virtual host name</span></span> | <span data-ttu-id="e0e69-522">Adresse IP statique virtuelle</span><span class="sxs-lookup"><span data-stu-id="e0e69-522">Virtual static IP address</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e0e69-523">Nom d’hôte virtuel du premier cluster SAP ASCS/SCS (pour la gestion du cluster)</span><span class="sxs-lookup"><span data-stu-id="e0e69-523">SAP ASCS/SCS first cluster virtual host name (for cluster management)</span></span> |<span data-ttu-id="e0e69-524">pr1-ascs-vir</span><span class="sxs-lookup"><span data-stu-id="e0e69-524">pr1-ascs-vir</span></span> |<span data-ttu-id="e0e69-525">10.0.0.42</span><span class="sxs-lookup"><span data-stu-id="e0e69-525">10.0.0.42</span></span> |
| <span data-ttu-id="e0e69-526">Nom d’hôte virtuel de l’instance SAP ASCS/SCS</span><span class="sxs-lookup"><span data-stu-id="e0e69-526">SAP ASCS/SCS instance virtual host name</span></span> |<span data-ttu-id="e0e69-527">pr1-ascs-sap</span><span class="sxs-lookup"><span data-stu-id="e0e69-527">pr1-ascs-sap</span></span> |<span data-ttu-id="e0e69-528">10.0.0.43</span><span class="sxs-lookup"><span data-stu-id="e0e69-528">10.0.0.43</span></span> |
| <span data-ttu-id="e0e69-529">Nom d’hôte virtuel du deuxième cluster SAP SGBD (gestion du cluster)</span><span class="sxs-lookup"><span data-stu-id="e0e69-529">SAP DBMS second cluster virtual host name (cluster management)</span></span> |<span data-ttu-id="e0e69-530">pr1-dbms-vir</span><span class="sxs-lookup"><span data-stu-id="e0e69-530">pr1-dbms-vir</span></span> |<span data-ttu-id="e0e69-531">10.0.0.32</span><span class="sxs-lookup"><span data-stu-id="e0e69-531">10.0.0.32</span></span> |

<span data-ttu-id="e0e69-532">Lorsque vous créez le cluster de hello, les noms d’hôte virtuel hello créer **pr1-ASC-vir** et **pr1-SGBD-vir** et hello associés à des adresses IP qui gèrent le cluster hello lui-même.</span><span class="sxs-lookup"><span data-stu-id="e0e69-532">When you create hello cluster, create hello virtual host names **pr1-ascs-vir** and **pr1-dbms-vir** and hello associated IP addresses that manage hello cluster itself.</span></span> <span data-ttu-id="e0e69-533">Pour plus d’informations sur la façon toodo, consultez [collecter les nœuds de cluster dans une configuration de cluster][sap-ha-guide-8.12.1].</span><span class="sxs-lookup"><span data-stu-id="e0e69-533">For information about how toodo this, see [Collect cluster nodes in a cluster configuration][sap-ha-guide-8.12.1].</span></span>

<span data-ttu-id="e0e69-534">Vous pouvez créer manuellement hello autres deux noms d’hôte virtuel, **pr1 ASC sap** et **pr1 SGBD sap**, et hello associés à des adresses IP sur le serveur DNS de hello.</span><span class="sxs-lookup"><span data-stu-id="e0e69-534">You can manually create hello other two virtual host names, **pr1-ascs-sap** and **pr1-dbms-sap**, and hello associated IP addresses, on hello DNS server.</span></span> <span data-ttu-id="e0e69-535">Hello instance SAP ASCS/SCS en cluster et instance de SGBD hello en cluster utilisent ces ressources.</span><span class="sxs-lookup"><span data-stu-id="e0e69-535">hello clustered SAP ASCS/SCS instance and hello clustered DBMS instance use these resources.</span></span> <span data-ttu-id="e0e69-536">Pour plus d’informations sur la façon toodo, consultez [créer un nom d’hôte virtuel pour une instance SAP ASCS/SCS cluster][sap-ha-guide-9.1.1].</span><span class="sxs-lookup"><span data-stu-id="e0e69-536">For information about how toodo this, see [Create a virtual host name for a clustered SAP ASCS/SCS instance][sap-ha-guide-9.1.1].</span></span>

### <span data-ttu-id="e0e69-537"><a name="84c019fe-8c58-4dac-9e54-173efd4b2c30"></a>Définir les adresses IP statiques pour les ordinateurs virtuels SAP hello</span><span class="sxs-lookup"><span data-stu-id="e0e69-537"><a name="84c019fe-8c58-4dac-9e54-173efd4b2c30"></a> Set static IP addresses for hello SAP virtual machines</span></span>
<span data-ttu-id="e0e69-538">Après avoir déployé toouse de machines virtuelles hello dans votre cluster, vous devez tooset des adresses IP statiques pour tous les ordinateurs virtuels.</span><span class="sxs-lookup"><span data-stu-id="e0e69-538">After you deploy hello virtual machines toouse in your cluster, you need tooset static IP addresses for all virtual machines.</span></span> <span data-ttu-id="e0e69-539">Cela dans la configuration de réseau virtuel Azure hello et pas dans le système de d’exploitation invité hello.</span><span class="sxs-lookup"><span data-stu-id="e0e69-539">Do this in hello Azure Virtual Network configuration, and not in hello guest operating system.</span></span>

1.  <span data-ttu-id="e0e69-540">Bonjour portail Azure, sélectionnez **groupe de ressources** > **carte réseau** > **paramètres** > **adresse IP** .</span><span class="sxs-lookup"><span data-stu-id="e0e69-540">In hello Azure portal, select **Resource Group** > **Network Card** > **Settings** > **IP Address**.</span></span>
2.  <span data-ttu-id="e0e69-541">Sur hello **des adresses IP** panneau, sous **affectation**, sélectionnez **statique**.</span><span class="sxs-lookup"><span data-stu-id="e0e69-541">On hello **IP addresses** blade, under **Assignment**, select **Static**.</span></span> <span data-ttu-id="e0e69-542">Bonjour **adresse IP** , entrez l’adresse IP de hello que vous souhaitez toouse.</span><span class="sxs-lookup"><span data-stu-id="e0e69-542">In hello **IP address** box, enter hello IP address that you want toouse.</span></span>

  > [!NOTE]
  > <span data-ttu-id="e0e69-543">Si vous changez d’adresse IP de hello hello de carte de réseau, vous devez toorestart hello machines virtuelles tooapply hello de modification.</span><span class="sxs-lookup"><span data-stu-id="e0e69-543">If you change hello IP address of hello network card, you need toorestart hello Azure virtual machines tooapply hello change.</span></span>  
  >
  >

  ![Figure 13 : Définir des adresses IP statiques pour la carte réseau de hello de chaque ordinateur virtuel][sap-ha-guide-figure-3002]

  <span data-ttu-id="e0e69-545">_**Figure 13 :** définir les adresses IP statiques pour la carte réseau de hello de chaque ordinateur virtuel_</span><span class="sxs-lookup"><span data-stu-id="e0e69-545">_**Figure 13:** Set static IP addresses for hello network card of each virtual machine_</span></span>

  <span data-ttu-id="e0e69-546">Répétez cette étape pour toutes les interfaces réseau, autrement dit, pour tous les ordinateurs virtuels, y compris les ordinateurs virtuels que vous souhaitez toouse pour votre service Active Directory/DNS.</span><span class="sxs-lookup"><span data-stu-id="e0e69-546">Repeat this step for all network interfaces, that is, for all virtual machines, including virtual machines that you want toouse for your Active Directory/DNS service.</span></span>

<span data-ttu-id="e0e69-547">Dans notre exemple, nous avons les machines virtuelles et les adresses IP statiques suivantes :</span><span class="sxs-lookup"><span data-stu-id="e0e69-547">In our example, we have these virtual machines and static IP addresses:</span></span>

| <span data-ttu-id="e0e69-548">Rôle de la machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="e0e69-548">Virtual machine role</span></span> | <span data-ttu-id="e0e69-549">Nom d’hôte de la machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="e0e69-549">Virtual machine host name</span></span> | <span data-ttu-id="e0e69-550">Nom de la carte réseau</span><span class="sxs-lookup"><span data-stu-id="e0e69-550">Network card name</span></span> | <span data-ttu-id="e0e69-551">Adresse IP statique</span><span class="sxs-lookup"><span data-stu-id="e0e69-551">Static IP address</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="e0e69-552">Première instance du serveur d’applications SAP</span><span class="sxs-lookup"><span data-stu-id="e0e69-552">First SAP Application Server instance</span></span> |<span data-ttu-id="e0e69-553">pr1-di-0</span><span class="sxs-lookup"><span data-stu-id="e0e69-553">pr1-di-0</span></span> |<span data-ttu-id="e0e69-554">pr1-nic-di-0</span><span class="sxs-lookup"><span data-stu-id="e0e69-554">pr1-nic-di-0</span></span> |<span data-ttu-id="e0e69-555">10.0.0.50</span><span class="sxs-lookup"><span data-stu-id="e0e69-555">10.0.0.50</span></span> |
| <span data-ttu-id="e0e69-556">Deuxième instance du serveur d’applications SAP</span><span class="sxs-lookup"><span data-stu-id="e0e69-556">Second SAP Application Server instance</span></span> |<span data-ttu-id="e0e69-557">pr1-di-1</span><span class="sxs-lookup"><span data-stu-id="e0e69-557">pr1-di-1</span></span> |<span data-ttu-id="e0e69-558">pr1-nic-di-1</span><span class="sxs-lookup"><span data-stu-id="e0e69-558">pr1-nic-di-1</span></span> |<span data-ttu-id="e0e69-559">10.0.0.51</span><span class="sxs-lookup"><span data-stu-id="e0e69-559">10.0.0.51</span></span> |
| <span data-ttu-id="e0e69-560">...</span><span class="sxs-lookup"><span data-stu-id="e0e69-560">...</span></span> |<span data-ttu-id="e0e69-561">...</span><span class="sxs-lookup"><span data-stu-id="e0e69-561">...</span></span> |<span data-ttu-id="e0e69-562">...</span><span class="sxs-lookup"><span data-stu-id="e0e69-562">...</span></span> |<span data-ttu-id="e0e69-563">...</span><span class="sxs-lookup"><span data-stu-id="e0e69-563">...</span></span> |
| <span data-ttu-id="e0e69-564">Dernière instance du serveur d’applications SAP serveur d’applications SAP</span><span class="sxs-lookup"><span data-stu-id="e0e69-564">Last SAP Application Server instance</span></span> |<span data-ttu-id="e0e69-565">pr1-di-5</span><span class="sxs-lookup"><span data-stu-id="e0e69-565">pr1-di-5</span></span> |<span data-ttu-id="e0e69-566">pr1-nic-di-5</span><span class="sxs-lookup"><span data-stu-id="e0e69-566">pr1-nic-di-5</span></span> |<span data-ttu-id="e0e69-567">10.0.0.55</span><span class="sxs-lookup"><span data-stu-id="e0e69-567">10.0.0.55</span></span> |
| <span data-ttu-id="e0e69-568">Premier nœud de cluster pour l’instance ASCS/SCS</span><span class="sxs-lookup"><span data-stu-id="e0e69-568">First cluster node for ASCS/SCS instance</span></span> |<span data-ttu-id="e0e69-569">pr1-ascs-0</span><span class="sxs-lookup"><span data-stu-id="e0e69-569">pr1-ascs-0</span></span> |<span data-ttu-id="e0e69-570">pr1-nic-ascs-0</span><span class="sxs-lookup"><span data-stu-id="e0e69-570">pr1-nic-ascs-0</span></span> |<span data-ttu-id="e0e69-571">10.0.0.40</span><span class="sxs-lookup"><span data-stu-id="e0e69-571">10.0.0.40</span></span> |
| <span data-ttu-id="e0e69-572">Deuxième nœud de cluster pour l’instance ASCS/SCS</span><span class="sxs-lookup"><span data-stu-id="e0e69-572">Second cluster node for ASCS/SCS instance</span></span> |<span data-ttu-id="e0e69-573">pr1-ascs-1</span><span class="sxs-lookup"><span data-stu-id="e0e69-573">pr1-ascs-1</span></span> |<span data-ttu-id="e0e69-574">pr1-nic-ascs-1</span><span class="sxs-lookup"><span data-stu-id="e0e69-574">pr1-nic-ascs-1</span></span> |<span data-ttu-id="e0e69-575">10.0.0.41</span><span class="sxs-lookup"><span data-stu-id="e0e69-575">10.0.0.41</span></span> |
| <span data-ttu-id="e0e69-576">Premier nœud de cluster pour l’instance SGBD</span><span class="sxs-lookup"><span data-stu-id="e0e69-576">First cluster node for DBMS instance</span></span> |<span data-ttu-id="e0e69-577">pr1-db-0</span><span class="sxs-lookup"><span data-stu-id="e0e69-577">pr1-db-0</span></span> |<span data-ttu-id="e0e69-578">pr1-nic-db-0</span><span class="sxs-lookup"><span data-stu-id="e0e69-578">pr1-nic-db-0</span></span> |<span data-ttu-id="e0e69-579">10.0.0.30</span><span class="sxs-lookup"><span data-stu-id="e0e69-579">10.0.0.30</span></span> |
| <span data-ttu-id="e0e69-580">Deuxième nœud de cluster pour l’instance SGBD</span><span class="sxs-lookup"><span data-stu-id="e0e69-580">Second cluster node for DBMS instance</span></span> |<span data-ttu-id="e0e69-581">pr1-db-1</span><span class="sxs-lookup"><span data-stu-id="e0e69-581">pr1-db-1</span></span> |<span data-ttu-id="e0e69-582">pr1-nic-db-1</span><span class="sxs-lookup"><span data-stu-id="e0e69-582">pr1-nic-db-1</span></span> |<span data-ttu-id="e0e69-583">10.0.0.31</span><span class="sxs-lookup"><span data-stu-id="e0e69-583">10.0.0.31</span></span> |

### <span data-ttu-id="e0e69-584"><a name="7a8f3e9b-0624-4051-9e41-b73fff816a9e"></a>Définissez une adresse IP statique pour l’équilibrage de charge interne Azure hello</span><span class="sxs-lookup"><span data-stu-id="e0e69-584"><a name="7a8f3e9b-0624-4051-9e41-b73fff816a9e"></a> Set a static IP address for hello Azure internal load balancer</span></span>

<span data-ttu-id="e0e69-585">modèle de SAP Azure Resource Manager Hello crée un équilibreur de charge interne Azure qui est utilisé pour l’instance SAP ASCS/SCS hello et clusters de SGBD hello.</span><span class="sxs-lookup"><span data-stu-id="e0e69-585">hello SAP Azure Resource Manager template creates an Azure internal load balancer that is used for hello SAP ASCS/SCS instance cluster and hello DBMS cluster.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e0e69-586">Hello adresse IP du nom d’hôte virtuel hello Hello SAP ASCS/SCS est hello même en tant qu’adresse IP de hello Hello équilibreur de charge interne SAP ASCS/SCS : **pr1-lb-ASC**.</span><span class="sxs-lookup"><span data-stu-id="e0e69-586">hello IP address of hello virtual host name of hello SAP ASCS/SCS is hello same as hello IP address of hello SAP ASCS/SCS internal load balancer: **pr1-lb-ascs**.</span></span>
> <span data-ttu-id="e0e69-587">Hello adresse IP du nom virtuel de hello Hello SGBD est hello même en tant qu’adresse IP de hello Hello équilibreur de charge interne SGBD : **pr1-lb-SGBD**.</span><span class="sxs-lookup"><span data-stu-id="e0e69-587">hello IP address of hello virtual name of hello DBMS is hello same as hello IP address of hello DBMS internal load balancer: **pr1-lb-dbms**.</span></span>
>
>

<span data-ttu-id="e0e69-588">équilibrage de charge tooset une adresse IP statique pour hello Azure interne :</span><span class="sxs-lookup"><span data-stu-id="e0e69-588">tooset a static IP address for hello Azure internal load balancer:</span></span>

1.  <span data-ttu-id="e0e69-589">Hello déploiement initial définit adresse IP d’équilibrage de charge interne hello trop**dynamique**.</span><span class="sxs-lookup"><span data-stu-id="e0e69-589">hello initial deployment sets hello internal load balancer IP address too**Dynamic**.</span></span> <span data-ttu-id="e0e69-590">Bonjour portail Azure, sur hello **des adresses IP** panneau, sous **affectation**, sélectionnez **statique**.</span><span class="sxs-lookup"><span data-stu-id="e0e69-590">In hello Azure portal, on hello **IP addresses** blade, under **Assignment**, select **Static**.</span></span>
2.  <span data-ttu-id="e0e69-591">Définir l’adresse IP de hello d’équilibreur de charge interne hello **pr1-lb-ASC** adresse toohello de nom d’hôte virtuel hello d’instance de SAP ASCS/SCS hello.</span><span class="sxs-lookup"><span data-stu-id="e0e69-591">Set hello IP address of hello internal load balancer **pr1-lb-ascs** toohello IP address of hello virtual host name of hello SAP ASCS/SCS instance.</span></span>
3.  <span data-ttu-id="e0e69-592">Définir l’adresse IP de hello d’équilibreur de charge interne hello **pr1-lb-SGBD** adresse toohello de nom d’hôte virtuel hello d’instance de SGBD hello.</span><span class="sxs-lookup"><span data-stu-id="e0e69-592">Set hello IP address of hello internal load balancer **pr1-lb-dbms** toohello IP address of hello virtual host name of hello DBMS instance.</span></span>

  ![La figure 14 : Définir des adresses IP statiques pour l’équilibrage de charge interne hello pour l’instance de SAP ASCS/SCS hello][sap-ha-guide-figure-3003]

  <span data-ttu-id="e0e69-594">_**La figure 14 :** définir des adresses IP statiques pour l’équilibrage de charge interne hello pour l’instance de SAP ASCS/SCS hello_</span><span class="sxs-lookup"><span data-stu-id="e0e69-594">_**Figure 14:** Set static IP addresses for hello internal load balancer for hello SAP ASCS/SCS instance_</span></span>

<span data-ttu-id="e0e69-595">Dans notre exemple, nous avons deux équilibrages de charge internes Azure qui présentent les adresses IP statiques suivantes :</span><span class="sxs-lookup"><span data-stu-id="e0e69-595">In our example, we have two Azure internal load balancers that have these static IP addresses:</span></span>

| <span data-ttu-id="e0e69-596">Rôle de l’équilibrage de charge interne Azure</span><span class="sxs-lookup"><span data-stu-id="e0e69-596">Azure internal load balancer role</span></span> | <span data-ttu-id="e0e69-597">Nom de l’équilibrage de charge interne Azure</span><span class="sxs-lookup"><span data-stu-id="e0e69-597">Azure internal load balancer name</span></span> | <span data-ttu-id="e0e69-598">Adresse IP statique</span><span class="sxs-lookup"><span data-stu-id="e0e69-598">Static IP address</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e0e69-599">Équilibrage de charge interne de l’instance SAP ASCS/SCS</span><span class="sxs-lookup"><span data-stu-id="e0e69-599">SAP ASCS/SCS instance internal load balancer</span></span> |<span data-ttu-id="e0e69-600">pr1-lb-ascs</span><span class="sxs-lookup"><span data-stu-id="e0e69-600">pr1-lb-ascs</span></span> |<span data-ttu-id="e0e69-601">10.0.0.43</span><span class="sxs-lookup"><span data-stu-id="e0e69-601">10.0.0.43</span></span> |
| <span data-ttu-id="e0e69-602">Équilibrage de charge interne du SGBD SAP</span><span class="sxs-lookup"><span data-stu-id="e0e69-602">SAP DBMS internal load balancer</span></span> |<span data-ttu-id="e0e69-603">pr1-lb-dbms</span><span class="sxs-lookup"><span data-stu-id="e0e69-603">pr1-lb-dbms</span></span> |<span data-ttu-id="e0e69-604">10.0.0.33</span><span class="sxs-lookup"><span data-stu-id="e0e69-604">10.0.0.33</span></span> |


### <span data-ttu-id="e0e69-605"><a name="f19bd997-154d-4583-a46e-7f5a69d0153c"></a>Par défaut pour l’équilibrage de charge interne Azure hello les règles d’équilibrage de charge ASCS/SCS</span><span class="sxs-lookup"><span data-stu-id="e0e69-605"><a name="f19bd997-154d-4583-a46e-7f5a69d0153c"></a> Default ASCS/SCS load balancing rules for hello Azure internal load balancer</span></span>

<span data-ttu-id="e0e69-606">modèle de SAP Azure Resource Manager Hello crée des ports hello que vous avez besoin :</span><span class="sxs-lookup"><span data-stu-id="e0e69-606">hello SAP Azure Resource Manager template creates hello ports you need:</span></span>
* <span data-ttu-id="e0e69-607">Une instance ABAP ASCS, avec le numéro d’instance par défaut hello **00**</span><span class="sxs-lookup"><span data-stu-id="e0e69-607">An ABAP ASCS instance, with hello default instance number **00**</span></span>
* <span data-ttu-id="e0e69-608">Une instance Java SCS, avec le numéro d’instance par défaut hello **01**</span><span class="sxs-lookup"><span data-stu-id="e0e69-608">A Java SCS instance, with hello default instance number **01**</span></span>

<span data-ttu-id="e0e69-609">Lorsque vous installez votre instance SAP ASCS/SCS, vous devez utiliser le numéro d’instance par défaut hello **00** votre ABAP ASCS instance et hello par défaut instance numéro **01** pour votre instance Java SCS.</span><span class="sxs-lookup"><span data-stu-id="e0e69-609">When you install your SAP ASCS/SCS instance, you must use hello default instance number **00** for your ABAP ASCS instance and hello default instance number **01** for your Java SCS instance.</span></span>

<span data-ttu-id="e0e69-610">Ensuite, créez des points de terminaison pour les ports de SAP NetWeaver hello d’équilibrage de charge d’interne requise.</span><span class="sxs-lookup"><span data-stu-id="e0e69-610">Next, create required internal load balancing endpoints for hello SAP NetWeaver ports.</span></span>

<span data-ttu-id="e0e69-611">toocreate requis de points de terminaison de l’équilibrage de charge interne, créez tout d’abord, ces points de terminaison pour les ports de SAP NetWeaver ABAP ASC hello d’équilibrage de charge :</span><span class="sxs-lookup"><span data-stu-id="e0e69-611">toocreate required internal load balancing endpoints, first, create these load balancing endpoints for hello SAP NetWeaver ABAP ASCS ports:</span></span>

| <span data-ttu-id="e0e69-612">Service/nom de la règle d’équilibrage de charge</span><span class="sxs-lookup"><span data-stu-id="e0e69-612">Service/load balancing rule name</span></span> | <span data-ttu-id="e0e69-613">Numéros de ports par défaut</span><span class="sxs-lookup"><span data-stu-id="e0e69-613">Default port numbers</span></span> | <span data-ttu-id="e0e69-614">Ports concrets pour (instance ASCS avec numéro d’instance 00) (ERS avec 10)</span><span class="sxs-lookup"><span data-stu-id="e0e69-614">Concrete ports for (ASCS instance with instance number 00) (ERS with 10)</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e0e69-615">Serveur de file d’attente / *lbrule3200*</span><span class="sxs-lookup"><span data-stu-id="e0e69-615">Enqueue Server / *lbrule3200*</span></span> |<span data-ttu-id="e0e69-616">32<*NuméroInstance*></span><span class="sxs-lookup"><span data-stu-id="e0e69-616">32<*InstanceNumber*></span></span> |<span data-ttu-id="e0e69-617">3200</span><span class="sxs-lookup"><span data-stu-id="e0e69-617">3200</span></span> |
| <span data-ttu-id="e0e69-618">Serveur de messages ABAP / *lbrule3600*</span><span class="sxs-lookup"><span data-stu-id="e0e69-618">ABAP Message Server / *lbrule3600*</span></span> |<span data-ttu-id="e0e69-619">36<*NuméroInstance*></span><span class="sxs-lookup"><span data-stu-id="e0e69-619">36<*InstanceNumber*></span></span> |<span data-ttu-id="e0e69-620">3600</span><span class="sxs-lookup"><span data-stu-id="e0e69-620">3600</span></span> |
| <span data-ttu-id="e0e69-621">Message ABAP interne / *lbrule3900*</span><span class="sxs-lookup"><span data-stu-id="e0e69-621">Internal ABAP Message / *lbrule3900*</span></span> |<span data-ttu-id="e0e69-622">39<*NuméroInstance*></span><span class="sxs-lookup"><span data-stu-id="e0e69-622">39<*InstanceNumber*></span></span> |<span data-ttu-id="e0e69-623">3900</span><span class="sxs-lookup"><span data-stu-id="e0e69-623">3900</span></span> |
| <span data-ttu-id="e0e69-624">Serveur de messages HTTP / *Lbrule8100*</span><span class="sxs-lookup"><span data-stu-id="e0e69-624">Message Server HTTP / *Lbrule8100*</span></span> |<span data-ttu-id="e0e69-625">81<*NuméroInstance*></span><span class="sxs-lookup"><span data-stu-id="e0e69-625">81<*InstanceNumber*></span></span> |<span data-ttu-id="e0e69-626">8100</span><span class="sxs-lookup"><span data-stu-id="e0e69-626">8100</span></span> |
| <span data-ttu-id="e0e69-627">Service de démarrage SAP ASCS HTTP / *Lbrule50013*</span><span class="sxs-lookup"><span data-stu-id="e0e69-627">SAP Start Service ASCS HTTP / *Lbrule50013*</span></span> |<span data-ttu-id="e0e69-628">5<*NuméroInstance*>13</span><span class="sxs-lookup"><span data-stu-id="e0e69-628">5<*InstanceNumber*>13</span></span> |<span data-ttu-id="e0e69-629">50013</span><span class="sxs-lookup"><span data-stu-id="e0e69-629">50013</span></span> |
| <span data-ttu-id="e0e69-630">Service de démarrage SAP ASCS HTTPS / *Lbrule50014*</span><span class="sxs-lookup"><span data-stu-id="e0e69-630">SAP Start Service ASCS HTTPS / *Lbrule50014*</span></span> |<span data-ttu-id="e0e69-631">5<*NuméroInstance*>14</span><span class="sxs-lookup"><span data-stu-id="e0e69-631">5<*InstanceNumber*>14</span></span> |<span data-ttu-id="e0e69-632">50014</span><span class="sxs-lookup"><span data-stu-id="e0e69-632">50014</span></span> |
| <span data-ttu-id="e0e69-633">Réplication de la file d’attente / *Lbrule50016*</span><span class="sxs-lookup"><span data-stu-id="e0e69-633">Enqueue Replication / *Lbrule50016*</span></span> |<span data-ttu-id="e0e69-634">5<*NuméroInstance*>16</span><span class="sxs-lookup"><span data-stu-id="e0e69-634">5<*InstanceNumber*>16</span></span> |<span data-ttu-id="e0e69-635">50016</span><span class="sxs-lookup"><span data-stu-id="e0e69-635">50016</span></span> |
| <span data-ttu-id="e0e69-636">Service de démarrage SAP ERS HTTP / *Lbrule51013*</span><span class="sxs-lookup"><span data-stu-id="e0e69-636">SAP Start Service ERS HTTP *Lbrule51013*</span></span> |<span data-ttu-id="e0e69-637">5<*NuméroInstance*>13</span><span class="sxs-lookup"><span data-stu-id="e0e69-637">5<*InstanceNumber*>13</span></span> |<span data-ttu-id="e0e69-638">51013</span><span class="sxs-lookup"><span data-stu-id="e0e69-638">51013</span></span> |
| <span data-ttu-id="e0e69-639">Service de démarrage SAP ERS HTTP / *Lbrule51014*</span><span class="sxs-lookup"><span data-stu-id="e0e69-639">SAP Start Service ERS HTTP *Lbrule51014*</span></span> |<span data-ttu-id="e0e69-640">5<*NuméroInstance*>14</span><span class="sxs-lookup"><span data-stu-id="e0e69-640">5<*InstanceNumber*>14</span></span> |<span data-ttu-id="e0e69-641">51014</span><span class="sxs-lookup"><span data-stu-id="e0e69-641">51014</span></span> |
| <span data-ttu-id="e0e69-642">WinRM *Lbrule5985*</span><span class="sxs-lookup"><span data-stu-id="e0e69-642">Win RM *Lbrule5985*</span></span> | |<span data-ttu-id="e0e69-643">5985</span><span class="sxs-lookup"><span data-stu-id="e0e69-643">5985</span></span> |
| <span data-ttu-id="e0e69-644">Partage de fichiers *Lbrule445*</span><span class="sxs-lookup"><span data-stu-id="e0e69-644">File Share *Lbrule445*</span></span> | |<span data-ttu-id="e0e69-645">445</span><span class="sxs-lookup"><span data-stu-id="e0e69-645">445</span></span> |

<span data-ttu-id="e0e69-646">_**Tableau 1 :** numéros d’instances de SAP NetWeaver ABAP ASC hello de Port_</span><span class="sxs-lookup"><span data-stu-id="e0e69-646">_**Table 1:** Port numbers of hello SAP NetWeaver ABAP ASCS instances_</span></span>

<span data-ttu-id="e0e69-647">Ensuite, créez ces points de terminaison pour les ports de SAP NetWeaver Java SCS hello d’équilibrage de charge :</span><span class="sxs-lookup"><span data-stu-id="e0e69-647">Then, create these load balancing endpoints for hello SAP NetWeaver Java SCS ports:</span></span>

| <span data-ttu-id="e0e69-648">Service/nom de la règle d’équilibrage de charge</span><span class="sxs-lookup"><span data-stu-id="e0e69-648">Service/load balancing rule name</span></span> | <span data-ttu-id="e0e69-649">Numéros de ports par défaut</span><span class="sxs-lookup"><span data-stu-id="e0e69-649">Default port numbers</span></span> | <span data-ttu-id="e0e69-650">Ports concrets pour (instance SCS avec numéro d’instance 01) (ERS avec 11)</span><span class="sxs-lookup"><span data-stu-id="e0e69-650">Concrete ports for (SCS instance with instance number 01) (ERS with 11)</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e0e69-651">Serveur de file d’attente / *lbrule3201*</span><span class="sxs-lookup"><span data-stu-id="e0e69-651">Enqueue Server / *lbrule3201*</span></span> |<span data-ttu-id="e0e69-652">32<*NuméroInstance*></span><span class="sxs-lookup"><span data-stu-id="e0e69-652">32<*InstanceNumber*></span></span> |<span data-ttu-id="e0e69-653">3201</span><span class="sxs-lookup"><span data-stu-id="e0e69-653">3201</span></span> |
| <span data-ttu-id="e0e69-654">Serveur de passerelle / *lbrule3301*</span><span class="sxs-lookup"><span data-stu-id="e0e69-654">Gateway Server / *lbrule3301*</span></span> |<span data-ttu-id="e0e69-655">33<*NuméroInstance*></span><span class="sxs-lookup"><span data-stu-id="e0e69-655">33<*InstanceNumber*></span></span> |<span data-ttu-id="e0e69-656">3301</span><span class="sxs-lookup"><span data-stu-id="e0e69-656">3301</span></span> |
| <span data-ttu-id="e0e69-657">Serveur de messages Java / *lbrule3900*</span><span class="sxs-lookup"><span data-stu-id="e0e69-657">Java Message Server / *lbrule3900*</span></span> |<span data-ttu-id="e0e69-658">39<*NuméroInstance*></span><span class="sxs-lookup"><span data-stu-id="e0e69-658">39<*InstanceNumber*></span></span> |<span data-ttu-id="e0e69-659">3901</span><span class="sxs-lookup"><span data-stu-id="e0e69-659">3901</span></span> |
| <span data-ttu-id="e0e69-660">Serveur de messages HTTP / *Lbrule8101*</span><span class="sxs-lookup"><span data-stu-id="e0e69-660">Message Server HTTP / *Lbrule8101*</span></span> |<span data-ttu-id="e0e69-661">81<*NuméroInstance*></span><span class="sxs-lookup"><span data-stu-id="e0e69-661">81<*InstanceNumber*></span></span> |<span data-ttu-id="e0e69-662">8101</span><span class="sxs-lookup"><span data-stu-id="e0e69-662">8101</span></span> |
| <span data-ttu-id="e0e69-663">Service de démarrage SAP SCS HTTP / *Lbrule50113*</span><span class="sxs-lookup"><span data-stu-id="e0e69-663">SAP Start Service SCS HTTP / *Lbrule50113*</span></span> |<span data-ttu-id="e0e69-664">5<*NuméroInstance*>13</span><span class="sxs-lookup"><span data-stu-id="e0e69-664">5<*InstanceNumber*>13</span></span> |<span data-ttu-id="e0e69-665">50113</span><span class="sxs-lookup"><span data-stu-id="e0e69-665">50113</span></span> |
| <span data-ttu-id="e0e69-666">Service de démarrage SAP SCS HTTPS / *Lbrule50114*</span><span class="sxs-lookup"><span data-stu-id="e0e69-666">SAP Start Service SCS HTTPS / *Lbrule50114*</span></span> |<span data-ttu-id="e0e69-667">5<*NuméroInstance*>14</span><span class="sxs-lookup"><span data-stu-id="e0e69-667">5<*InstanceNumber*>14</span></span> |<span data-ttu-id="e0e69-668">50114</span><span class="sxs-lookup"><span data-stu-id="e0e69-668">50114</span></span> |
| <span data-ttu-id="e0e69-669">Réplication de la file d’attente / *Lbrule50116*</span><span class="sxs-lookup"><span data-stu-id="e0e69-669">Enqueue Replication / *Lbrule50116*</span></span> |<span data-ttu-id="e0e69-670">5<*NuméroInstance*>16</span><span class="sxs-lookup"><span data-stu-id="e0e69-670">5<*InstanceNumber*>16</span></span> |<span data-ttu-id="e0e69-671">50116</span><span class="sxs-lookup"><span data-stu-id="e0e69-671">50116</span></span> |
| <span data-ttu-id="e0e69-672">Service de démarrage SAP ERS HTTP / *Lbrule51113*</span><span class="sxs-lookup"><span data-stu-id="e0e69-672">SAP Start Service ERS HTTP *Lbrule51113*</span></span> |<span data-ttu-id="e0e69-673">5<*NuméroInstance*>13</span><span class="sxs-lookup"><span data-stu-id="e0e69-673">5<*InstanceNumber*>13</span></span> |<span data-ttu-id="e0e69-674">51113</span><span class="sxs-lookup"><span data-stu-id="e0e69-674">51113</span></span> |
| <span data-ttu-id="e0e69-675">Service de démarrage SAP ERS HTTP / *Lbrule51114*</span><span class="sxs-lookup"><span data-stu-id="e0e69-675">SAP Start Service ERS HTTP *Lbrule51114*</span></span> |<span data-ttu-id="e0e69-676">5<*NuméroInstance*>14</span><span class="sxs-lookup"><span data-stu-id="e0e69-676">5<*InstanceNumber*>14</span></span> |<span data-ttu-id="e0e69-677">51114</span><span class="sxs-lookup"><span data-stu-id="e0e69-677">51114</span></span> |
| <span data-ttu-id="e0e69-678">WinRM *Lbrule5985*</span><span class="sxs-lookup"><span data-stu-id="e0e69-678">Win RM *Lbrule5985*</span></span> | |<span data-ttu-id="e0e69-679">5985</span><span class="sxs-lookup"><span data-stu-id="e0e69-679">5985</span></span> |
| <span data-ttu-id="e0e69-680">Partage de fichiers *Lbrule445*</span><span class="sxs-lookup"><span data-stu-id="e0e69-680">File Share *Lbrule445*</span></span> | |<span data-ttu-id="e0e69-681">445</span><span class="sxs-lookup"><span data-stu-id="e0e69-681">445</span></span> |

<span data-ttu-id="e0e69-682">_**Tableau 2 :** numéros d’instances de SAP NetWeaver Java SCS hello de Port_</span><span class="sxs-lookup"><span data-stu-id="e0e69-682">_**Table 2:** Port numbers of hello SAP NetWeaver Java SCS instances_</span></span>

![Figure 15 : Par défaut ASCS/SCS équilibrage de la charge des règles pour l’équilibrage de charge interne Azure hello][sap-ha-guide-figure-3004]

<span data-ttu-id="e0e69-684">_**Figure 15 :** règles pour l’équilibrage de charge interne Azure hello équilibrage de la valeur par défaut ASCS/SCS_</span><span class="sxs-lookup"><span data-stu-id="e0e69-684">_**Figure 15:** Default ASCS/SCS load balancing rules for hello Azure internal load balancer_</span></span>

<span data-ttu-id="e0e69-685">Définir l’adresse IP de hello d’équilibrage de charge hello **pr1-lb-SGBD** adresse toohello de nom d’hôte virtuel hello d’instance de SGBD hello.</span><span class="sxs-lookup"><span data-stu-id="e0e69-685">Set hello IP address of hello load balancer **pr1-lb-dbms** toohello IP address of hello virtual host name of hello DBMS instance.</span></span>

### <span data-ttu-id="e0e69-686"><a name="fe0bd8b5-2b43-45e3-8295-80bee5415716"></a>Modifier les règles pour l’équilibrage de charge interne Azure hello d’équilibrage de charge de valeur par défaut ASCS/SCS de hello</span><span class="sxs-lookup"><span data-stu-id="e0e69-686"><a name="fe0bd8b5-2b43-45e3-8295-80bee5415716"></a> Change hello ASCS/SCS default load balancing rules for hello Azure internal load balancer</span></span>

<span data-ttu-id="e0e69-687">Si vous souhaitez toouse différents nombres pour hello ASCS SAP ou des instances SCS, vous devez modifier les noms de hello et les valeurs de leurs ports des valeurs par défaut.</span><span class="sxs-lookup"><span data-stu-id="e0e69-687">If you want toouse different numbers for hello SAP ASCS or SCS instances, you must change hello names and values of their ports from default values.</span></span>

1.  <span data-ttu-id="e0e69-688">Bonjour portail Azure, sélectionnez  **<* SID*> - lb - ASC charge équilibrage ** > **règles d’équilibrage de charge**.</span><span class="sxs-lookup"><span data-stu-id="e0e69-688">In hello Azure portal, select **<*SID*>-lb-ascs load balancer** > **Load Balancing Rules**.</span></span>
2.  <span data-ttu-id="e0e69-689">Pour les règles qui appartiennent toohello ASCS SAP ou instance SCS d’équilibrage de charge tous les, modifiez ces valeurs :</span><span class="sxs-lookup"><span data-stu-id="e0e69-689">For all load balancing rules that belong toohello SAP ASCS or SCS instance, change these values:</span></span>

  * <span data-ttu-id="e0e69-690">Nom</span><span class="sxs-lookup"><span data-stu-id="e0e69-690">Name</span></span>
  * <span data-ttu-id="e0e69-691">Port</span><span class="sxs-lookup"><span data-stu-id="e0e69-691">Port</span></span>
  * <span data-ttu-id="e0e69-692">Port principal</span><span class="sxs-lookup"><span data-stu-id="e0e69-692">Back-end port</span></span>

  <span data-ttu-id="e0e69-693">Par exemple, si vous souhaitez que le numéro d’instance ASC toochange hello par défaut à partir de 00 too31, vous devez les modifications de hello toomake pour tous les ports répertoriés dans le tableau 1.</span><span class="sxs-lookup"><span data-stu-id="e0e69-693">For example, if you want toochange hello default ASCS instance number from 00 too31, you need toomake hello changes for all ports listed in Table 1.</span></span>

  <span data-ttu-id="e0e69-694">Voici un exemple de mise à jour pour le port *lbrule3200*.</span><span class="sxs-lookup"><span data-stu-id="e0e69-694">Here's an example of an update for port *lbrule3200*.</span></span>

  ![Figure 16 : Modifier des règles pour l’équilibrage de charge interne Azure hello d’équilibrage de charge de valeur par défaut ASCS/SCS de hello][sap-ha-guide-figure-3005]

  <span data-ttu-id="e0e69-696">_**Figure 16 :** modification hello ASCS/SCS par défaut l’équilibrage de charge des règles pour l’équilibrage de charge interne Azure hello_</span><span class="sxs-lookup"><span data-stu-id="e0e69-696">_**Figure 16:** Change hello ASCS/SCS default load balancing rules for hello Azure internal load balancer_</span></span>

### <span data-ttu-id="e0e69-697"><a name="e69e9a34-4601-47a3-a41c-d2e11c626c0c"></a>Ajouter le domaine toohello de machines virtuelles Windows</span><span class="sxs-lookup"><span data-stu-id="e0e69-697"><a name="e69e9a34-4601-47a3-a41c-d2e11c626c0c"></a> Add Windows virtual machines toohello domain</span></span>

<span data-ttu-id="e0e69-698">Une fois que vous affectez un statique IP adresse toohello les ordinateurs virtuels, ajoutez le domaine de toohello de machines virtuelles de hello.</span><span class="sxs-lookup"><span data-stu-id="e0e69-698">After you assign a static IP address toohello virtual machines, add hello virtual machines toohello domain.</span></span>

![Figure 17 : Ajouter un domaine tooa de machine virtuelle][sap-ha-guide-figure-3006]

<span data-ttu-id="e0e69-700">_**Figure 17 :** ajouter un domaine tooa de machine virtuelle_</span><span class="sxs-lookup"><span data-stu-id="e0e69-700">_**Figure 17:** Add a virtual machine tooa domain_</span></span>

### <span data-ttu-id="e0e69-701"><a name="661035b2-4d0f-4d31-86f8-dc0a50d78158"></a>Ajouter des entrées de Registre sur les deux nœuds de cluster de l’instance de SAP ASCS/SCS hello</span><span class="sxs-lookup"><span data-stu-id="e0e69-701"><a name="661035b2-4d0f-4d31-86f8-dc0a50d78158"></a> Add registry entries on both cluster nodes of hello SAP ASCS/SCS instance</span></span>

<span data-ttu-id="e0e69-702">L’équilibrage de charge Azure a un équilibreur de charge interne que les connexions se ferme quand les connexions hello sont inactives pendant un laps de temps (délai d’inactivité).</span><span class="sxs-lookup"><span data-stu-id="e0e69-702">Azure Load Balancer has an internal load balancer that closes connections when hello connections are idle for a set period of time (an idle timeout).</span></span> <span data-ttu-id="e0e69-703">Le processus de travail SAP dans la boîte de dialogue instances connexions ouvertes toohello SAP enqueue traiter dès que hello première file d’attente/de retrait demande toobe besoins envoyé.</span><span class="sxs-lookup"><span data-stu-id="e0e69-703">SAP work processes in dialog instances open connections toohello SAP enqueue process as soon as hello first enqueue/dequeue request needs toobe sent.</span></span> <span data-ttu-id="e0e69-704">Ces connexions sont généralement établies jusqu'à ce que le processus de travail hello ou hello du processus de file d’attente.</span><span class="sxs-lookup"><span data-stu-id="e0e69-704">These connections usually remain established until hello work process or hello enqueue process restarts.</span></span> <span data-ttu-id="e0e69-705">Toutefois, si la connexion de hello est inactive pendant un laps de temps défini, hello connexions hello de charge interne Azure équilibrage se ferme.</span><span class="sxs-lookup"><span data-stu-id="e0e69-705">However, if hello connection is idle for a set period of time, hello Azure internal load balancer closes hello connections.</span></span> <span data-ttu-id="e0e69-706">Cela n’est pas un problème car hello processus de travail SAP rétablit le processus de file d’attente toohello hello connexion si elle n’existe plus.</span><span class="sxs-lookup"><span data-stu-id="e0e69-706">This isn't a problem because hello SAP work process reestablishes hello connection toohello enqueue process if it no longer exists.</span></span> <span data-ttu-id="e0e69-707">Ces activités sont documentées dans les traces de développeur hello processus SAP, mais ils créent une grande quantité de contenu supplémentaire dans les traces.</span><span class="sxs-lookup"><span data-stu-id="e0e69-707">These activities are documented in hello developer traces of SAP processes, but they create a large amount of extra content in those traces.</span></span> <span data-ttu-id="e0e69-708">Il s’agit d’un Bonjour de toochange conseillé TCP/IP `KeepAliveTime` et `KeepAliveInterval` sur les deux nœuds de cluster.</span><span class="sxs-lookup"><span data-stu-id="e0e69-708">It's a good idea toochange hello TCP/IP `KeepAliveTime` and `KeepAliveInterval` on both cluster nodes.</span></span> <span data-ttu-id="e0e69-709">Combiner ces modifications dans les paramètres TCP/IP hello avec des paramètres de profil SAP, décrites plus loin dans l’article de hello.</span><span class="sxs-lookup"><span data-stu-id="e0e69-709">Combine these changes in hello TCP/IP parameters with SAP profile parameters, described later in hello article.</span></span>

<span data-ttu-id="e0e69-710">tooadd les entrées de Registre sur les deux nœuds de cluster d’instance SAP ASCS/SCS hello, ajoutent d’abord ces entrées de Registre Windows sur les deux nœuds de cluster Windows pour SAP ASCS/SCS :</span><span class="sxs-lookup"><span data-stu-id="e0e69-710">tooadd registry entries on both cluster nodes of hello SAP ASCS/SCS instance, first, add these Windows registry entries on both Windows cluster nodes for SAP ASCS/SCS:</span></span>

| <span data-ttu-id="e0e69-711">Chemin</span><span class="sxs-lookup"><span data-stu-id="e0e69-711">Path</span></span> | <span data-ttu-id="e0e69-712">HKLM\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters</span><span class="sxs-lookup"><span data-stu-id="e0e69-712">HKLM\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters</span></span> |
| --- | --- |
| <span data-ttu-id="e0e69-713">Nom de la variable</span><span class="sxs-lookup"><span data-stu-id="e0e69-713">Variable name</span></span> |`KeepAliveTime` |
| <span data-ttu-id="e0e69-714">Type de variable</span><span class="sxs-lookup"><span data-stu-id="e0e69-714">Variable type</span></span> |<span data-ttu-id="e0e69-715">REG_DWORD (décimal)</span><span class="sxs-lookup"><span data-stu-id="e0e69-715">REG_DWORD (Decimal)</span></span> |
| <span data-ttu-id="e0e69-716">Valeur</span><span class="sxs-lookup"><span data-stu-id="e0e69-716">Value</span></span> |<span data-ttu-id="e0e69-717">120 000</span><span class="sxs-lookup"><span data-stu-id="e0e69-717">120000</span></span> |
| <span data-ttu-id="e0e69-718">Lien toodocumentation</span><span class="sxs-lookup"><span data-stu-id="e0e69-718">Link toodocumentation</span></span> |[<span data-ttu-id="e0e69-719">https://technet.microsoft.com/en-us/library/cc957549.aspx</span><span class="sxs-lookup"><span data-stu-id="e0e69-719">https://technet.microsoft.com/en-us/library/cc957549.aspx</span></span>](https://technet.microsoft.com/en-us/library/cc957549.aspx) |

<span data-ttu-id="e0e69-720">_**Tableau 3 :** modification hello premier TCP/IP paramètre_</span><span class="sxs-lookup"><span data-stu-id="e0e69-720">_**Table 3:** Change hello first TCP/IP parameter_</span></span>

<span data-ttu-id="e0e69-721">Puis, ajoutez ces entrées de registre Windows aux deux nœuds de cluster Windows pour l’instance SAP ASCS/SCS :</span><span class="sxs-lookup"><span data-stu-id="e0e69-721">Then, add this Windows registry entries on both Windows cluster nodes for SAP ASCS/SCS:</span></span>

| <span data-ttu-id="e0e69-722">Chemin</span><span class="sxs-lookup"><span data-stu-id="e0e69-722">Path</span></span> | <span data-ttu-id="e0e69-723">HKLM\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters</span><span class="sxs-lookup"><span data-stu-id="e0e69-723">HKLM\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters</span></span> |
| --- | --- |
| <span data-ttu-id="e0e69-724">Nom de la variable</span><span class="sxs-lookup"><span data-stu-id="e0e69-724">Variable name</span></span> |`KeepAliveInterval` |
| <span data-ttu-id="e0e69-725">Type de variable</span><span class="sxs-lookup"><span data-stu-id="e0e69-725">Variable type</span></span> |<span data-ttu-id="e0e69-726">REG_DWORD (décimal)</span><span class="sxs-lookup"><span data-stu-id="e0e69-726">REG_DWORD (Decimal)</span></span> |
| <span data-ttu-id="e0e69-727">Valeur</span><span class="sxs-lookup"><span data-stu-id="e0e69-727">Value</span></span> |<span data-ttu-id="e0e69-728">120 000</span><span class="sxs-lookup"><span data-stu-id="e0e69-728">120000</span></span> |
| <span data-ttu-id="e0e69-729">Lien toodocumentation</span><span class="sxs-lookup"><span data-stu-id="e0e69-729">Link toodocumentation</span></span> |[<span data-ttu-id="e0e69-730">https://technet.microsoft.com/en-us/library/cc957548.aspx</span><span class="sxs-lookup"><span data-stu-id="e0e69-730">https://technet.microsoft.com/en-us/library/cc957548.aspx</span></span>](https://technet.microsoft.com/en-us/library/cc957548.aspx) |

<span data-ttu-id="e0e69-731">_**Tableau 4 :** modification hello deuxième TCP/IP paramètre_</span><span class="sxs-lookup"><span data-stu-id="e0e69-731">_**Table 4:** Change hello second TCP/IP parameter_</span></span>

<span data-ttu-id="e0e69-732">**modifications de hello tooapply, redémarrez les deux nœuds de cluster**.</span><span class="sxs-lookup"><span data-stu-id="e0e69-732">**tooapply hello changes, restart both cluster nodes**.</span></span>

### <span data-ttu-id="e0e69-733"><a name="0d67f090-7928-43e0-8772-5ccbf8f59aab"></a> Configurer un cluster de clustering de basculement Windows Server pour une instance SAP ASCS/SCS</span><span class="sxs-lookup"><span data-stu-id="e0e69-733"><a name="0d67f090-7928-43e0-8772-5ccbf8f59aab"></a> Set up a Windows Server Failover Clustering cluster for an SAP ASCS/SCS instance</span></span>

<span data-ttu-id="e0e69-734">La configuration d’un cluster de basculement Windows Server pour une instance SAP ASCS/SCS implique les tâches suivantes :</span><span class="sxs-lookup"><span data-stu-id="e0e69-734">Setting up a Windows Server Failover Clustering cluster for an SAP ASCS/SCS instance involves these tasks:</span></span>

- <span data-ttu-id="e0e69-735">Collecte des nœuds de cluster hello dans une configuration de cluster</span><span class="sxs-lookup"><span data-stu-id="e0e69-735">Collecting hello cluster nodes in a cluster configuration</span></span>
- <span data-ttu-id="e0e69-736">Configurer un témoin de partage de fichiers de cluster</span><span class="sxs-lookup"><span data-stu-id="e0e69-736">Configuring a cluster file share witness</span></span>

#### <span data-ttu-id="e0e69-737"><a name="5eecb071-c703-4ccc-ba6d-fe9c6ded9d79"></a>Collecter les nœuds de cluster hello dans une configuration de cluster</span><span class="sxs-lookup"><span data-stu-id="e0e69-737"><a name="5eecb071-c703-4ccc-ba6d-fe9c6ded9d79"></a> Collect hello cluster nodes in a cluster configuration</span></span>

1.  <span data-ttu-id="e0e69-738">Dans Ajouter un rôle de hello Assistant et de fonctionnalités, ajouter tooboth les nœuds de cluster de clustering de basculement.</span><span class="sxs-lookup"><span data-stu-id="e0e69-738">In hello Add Role and Features Wizard, add failover clustering tooboth cluster nodes.</span></span>
2.  <span data-ttu-id="e0e69-739">Configurer le cluster de basculement hello à l’aide du Gestionnaire du Cluster de basculement.</span><span class="sxs-lookup"><span data-stu-id="e0e69-739">Set up hello failover cluster by using Failover Cluster Manager.</span></span> <span data-ttu-id="e0e69-740">Dans le Gestionnaire de Cluster de basculement, sélectionnez **création d’un Cluster**, puis ajoutez uniquement hello nom de cluster première hello, nœud A. N’ajoutez pas de nœud de deuxième hello vous allez ajouter le nœud de deuxième hello dans une étape ultérieure.</span><span class="sxs-lookup"><span data-stu-id="e0e69-740">In Failover Cluster Manager, select **Create Cluster**, and then add only hello name of hello first cluster, node A. Do not add hello second node yet; you'll add hello second node in a later step.</span></span>

  ![La figure 18 : Ajouter hello nom du serveur ou ordinateur virtuel du premier nœud de cluster hello][sap-ha-guide-figure-3007]

  <span data-ttu-id="e0e69-742">_**La figure 18 :** ajouter hello machine virtuelle nom du serveur ou du premier nœud de cluster hello_</span><span class="sxs-lookup"><span data-stu-id="e0e69-742">_**Figure 18:** Add hello server or virtual machine name of hello first cluster node_</span></span>

3.  <span data-ttu-id="e0e69-743">Entrez le nom hello réseau (nom d’hôte virtuel) du cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="e0e69-743">Enter hello network name (virtual host name) of hello cluster.</span></span>

  ![Figure 19 : Entrez le nom du cluster hello][sap-ha-guide-figure-3008]

  <span data-ttu-id="e0e69-745">_**Figure 19 :** Entrez le nom de cluster hello_</span><span class="sxs-lookup"><span data-stu-id="e0e69-745">_**Figure 19:** Enter hello cluster name_</span></span>

4.  <span data-ttu-id="e0e69-746">Une fois que vous avez créé le cluster de hello, exécutez un test de validation de cluster.</span><span class="sxs-lookup"><span data-stu-id="e0e69-746">After you've created hello cluster, run a cluster validation test.</span></span>

  ![Figure 20 : Exécuter la vérification de validation de cluster de hello][sap-ha-guide-figure-3009]

  <span data-ttu-id="e0e69-748">_**Figure 20 :** exécuter le contrôle de validation de cluster hello_</span><span class="sxs-lookup"><span data-stu-id="e0e69-748">_**Figure 20:** Run hello cluster validation check_</span></span>

  <span data-ttu-id="e0e69-749">Vous pouvez ignorer les avertissements relatifs à des disques à ce stade dans le processus de hello.</span><span class="sxs-lookup"><span data-stu-id="e0e69-749">You can ignore any warnings about disks at this point in hello process.</span></span> <span data-ttu-id="e0e69-750">Vous allez ajouter qu'un témoin de partage de fichiers et de hello SIOS des disques partagés plus tard.</span><span class="sxs-lookup"><span data-stu-id="e0e69-750">You'll add a file share witness and hello SIOS shared disks later.</span></span> <span data-ttu-id="e0e69-751">À ce stade, vous n’avez pas besoin tooworry sur ayant un quorum.</span><span class="sxs-lookup"><span data-stu-id="e0e69-751">At this stage, you don't need tooworry about having a quorum.</span></span>

  ![Figure 21 : Aucun disque quorum trouvé][sap-ha-guide-figure-3010]

  <span data-ttu-id="e0e69-753">_**Figure 21 :** Aucun disque quorum trouvé_</span><span class="sxs-lookup"><span data-stu-id="e0e69-753">_**Figure 21:** No quorum disk is found_</span></span>

  ![Figure 22 : La ressource principale du cluster a besoin d’une nouvelle adresse IP][sap-ha-guide-figure-3011]

  <span data-ttu-id="e0e69-755">_**Figure 22 :** La ressource principale du cluster a besoin d’une nouvelle adresse IP_</span><span class="sxs-lookup"><span data-stu-id="e0e69-755">_**Figure 22:** Core cluster resource needs a new IP address_</span></span>

5.  <span data-ttu-id="e0e69-756">Modifier l’adresse IP de hello hello principaux du service de cluster.</span><span class="sxs-lookup"><span data-stu-id="e0e69-756">Change hello IP address of hello core cluster service.</span></span> <span data-ttu-id="e0e69-757">Hello ne peut pas le démarrage du cluster jusqu'à ce que vous modifiez l’adresse IP de hello hello principaux du service de cluster, car les points de l’adresse hello du serveur de hello tooone de nœuds de machine virtuelle hello.</span><span class="sxs-lookup"><span data-stu-id="e0e69-757">hello cluster can't start until you change hello IP address of hello core cluster service, because hello IP address of hello server points tooone of hello virtual machine nodes.</span></span> <span data-ttu-id="e0e69-758">Cela sur hello **propriétés** page de ressource d’IP du service cluster hello core.</span><span class="sxs-lookup"><span data-stu-id="e0e69-758">Do this on hello **Properties** page of hello core cluster service's IP resource.</span></span>

  <span data-ttu-id="e0e69-759">Par exemple, nous devons tooassign une adresse IP (dans notre exemple, **10.0.0.42**) pour le nom d’hôte virtuel de cluster de hello **pr1-ASC-vir**.</span><span class="sxs-lookup"><span data-stu-id="e0e69-759">For example, we need tooassign an IP address (in our example, **10.0.0.42**) for hello cluster virtual host name **pr1-ascs-vir**.</span></span>

  ![Figure 23 : Modifier dans la boîte de dialogue de propriétés hello, adresse IP de hello][sap-ha-guide-figure-3012]

  <span data-ttu-id="e0e69-761">_**La figure 23 :** Bonjour **propriétés** boîte de dialogue, de modifier l’adresse IP hello_</span><span class="sxs-lookup"><span data-stu-id="e0e69-761">_**Figure 23:** In hello **Properties** dialog box, change hello IP address_</span></span>

  ![Figure 24 : Affecter des adresses IP hello qui est réservée pour le cluster de hello][sap-ha-guide-figure-3013]

  <span data-ttu-id="e0e69-763">_**Figure 24 :** affecter l’adresse IP hello qui est réservée pour le cluster de hello_</span><span class="sxs-lookup"><span data-stu-id="e0e69-763">_**Figure 24:** Assign hello IP address that is reserved for hello cluster_</span></span>

6.  <span data-ttu-id="e0e69-764">Mettez le nom d’hôte virtuel cluster hello en ligne.</span><span class="sxs-lookup"><span data-stu-id="e0e69-764">Bring hello cluster virtual host name online.</span></span>

  ![Figure 25 : Le service principal de Cluster est activé et en cours d’exécution et avec hello Corrigez l’adresse IP][sap-ha-guide-figure-3014]

  <span data-ttu-id="e0e69-766">_**Figure 25 :** service principal de Cluster est activé et en cours d’exécution et avec hello Corrigez l’adresse IP_</span><span class="sxs-lookup"><span data-stu-id="e0e69-766">_**Figure 25:** Cluster core service is up and running, and with hello correct IP address_</span></span>

7.  <span data-ttu-id="e0e69-767">Ajouter le second nœud de cluster hello.</span><span class="sxs-lookup"><span data-stu-id="e0e69-767">Add hello second cluster node.</span></span>

  <span data-ttu-id="e0e69-768">Maintenant que le service de cluster hello principal est en cours d’exécution, vous pouvez ajouter le second nœud de cluster hello.</span><span class="sxs-lookup"><span data-stu-id="e0e69-768">Now that hello core cluster service is up and running, you can add hello second cluster node.</span></span>

  ![Figure 26 : Ajouter le second nœud de cluster hello][sap-ha-guide-figure-3015]

  <span data-ttu-id="e0e69-770">_**Figure 26 :** ajouter hello second nœud de cluster_</span><span class="sxs-lookup"><span data-stu-id="e0e69-770">_**Figure 26:** Add hello second cluster node_</span></span>

8.  <span data-ttu-id="e0e69-771">Entrez un nom pour le second hôte de nœud de cluster hello.</span><span class="sxs-lookup"><span data-stu-id="e0e69-771">Enter a name for hello second cluster node host.</span></span>

  ![Figure 27 : Entrez le nom d’hôte de nœud de hello deuxième cluster][sap-ha-guide-figure-3016]

  <span data-ttu-id="e0e69-773">_**Figure 27 :** nom d’entrée hello deuxième cluster nœud hôte_</span><span class="sxs-lookup"><span data-stu-id="e0e69-773">_**Figure 27:** Enter hello second cluster node host name_</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="e0e69-774">Veillez à ce que hello **ajouter tous les totalité du stockage du cluster toohello** case à cocher est **pas** sélectionné.</span><span class="sxs-lookup"><span data-stu-id="e0e69-774">Be sure that hello **Add all eligible storage toohello cluster** check box is **NOT** selected.</span></span>  
  >
  >

  ![Figure 28 : Ne sélectionnez pas la case à cocher hello][sap-ha-guide-figure-3017]

  <span data-ttu-id="e0e69-776">_**Figure 28 :** faire **pas** sélectionnez hello case à cocher_</span><span class="sxs-lookup"><span data-stu-id="e0e69-776">_**Figure 28:** Do **not** select hello check box_</span></span>

  <span data-ttu-id="e0e69-777">Vous pouvez ignorer les avertissements concernant le quorum et les disques.</span><span class="sxs-lookup"><span data-stu-id="e0e69-777">You can ignore warnings about quorum and disks.</span></span> <span data-ttu-id="e0e69-778">Vous devez définir hello quorum et partage hello disque ultérieurement, comme décrit dans [installation SIOS DataKeeper Cluster Edition pour le partage de disque du cluster de SAP ASCS/SCS][sap-ha-guide-8.12.3].</span><span class="sxs-lookup"><span data-stu-id="e0e69-778">You'll set hello quorum and share hello disk later, as described in [Installing SIOS DataKeeper Cluster Edition for SAP ASCS/SCS cluster share disk][sap-ha-guide-8.12.3].</span></span>

  ![Figure 29 : Ignorer les avertissements sur le quorum de disque hello][sap-ha-guide-figure-3018]

  <span data-ttu-id="e0e69-780">_**Figure 29 :** ignorer les avertissements sur le quorum de disque hello_</span><span class="sxs-lookup"><span data-stu-id="e0e69-780">_**Figure 29:** Ignore warnings about hello disk quorum_</span></span>


#### <span data-ttu-id="e0e69-781"><a name="e49a4529-50c9-4dcf-bde7-15a0c21d21ca"></a> Configurer un témoin de partage de fichiers de cluster</span><span class="sxs-lookup"><span data-stu-id="e0e69-781"><a name="e49a4529-50c9-4dcf-bde7-15a0c21d21ca"></a> Configure a cluster file share witness</span></span>

<span data-ttu-id="e0e69-782">La configuration d’un témoin de partage de fichiers de cluster implique les tâches suivantes :</span><span class="sxs-lookup"><span data-stu-id="e0e69-782">Configuring a cluster file share witness involves these tasks:</span></span>

- <span data-ttu-id="e0e69-783">Création d'un partage de fichiers</span><span class="sxs-lookup"><span data-stu-id="e0e69-783">Creating a file share</span></span>
- <span data-ttu-id="e0e69-784">Configuration de quorum de témoin de partage de fichiers hello Gestionnaire du Cluster de basculement</span><span class="sxs-lookup"><span data-stu-id="e0e69-784">Setting hello file share witness quorum in Failover Cluster Manager</span></span>

##### <span data-ttu-id="e0e69-785"><a name="06260b30-d697-4c4d-b1c9-d22c0bd64855"></a> Créer un partage de fichiers</span><span class="sxs-lookup"><span data-stu-id="e0e69-785"><a name="06260b30-d697-4c4d-b1c9-d22c0bd64855"></a> Create a file share</span></span>

1.  <span data-ttu-id="e0e69-786">Sélectionnez un témoin de partage de fichiers plutôt qu’un disque quorum.</span><span class="sxs-lookup"><span data-stu-id="e0e69-786">Select a file share witness instead of a quorum disk.</span></span> <span data-ttu-id="e0e69-787">SIOS DataKeeper prend en charge cette option.</span><span class="sxs-lookup"><span data-stu-id="e0e69-787">SIOS DataKeeper supports this option.</span></span>

  <span data-ttu-id="e0e69-788">Dans les exemples hello dans cet article, le témoin de partage de fichiers hello est sur le serveur DNS d’Active Directory/hello qui s’exécute dans Azure.</span><span class="sxs-lookup"><span data-stu-id="e0e69-788">In hello examples in this article, hello file share witness is on hello Active Directory/DNS server that is running in Azure.</span></span> <span data-ttu-id="e0e69-789">Hello témoin de partage de fichiers est appelée **domcontr-0**.</span><span class="sxs-lookup"><span data-stu-id="e0e69-789">hello file share witness is called **domcontr-0**.</span></span> <span data-ttu-id="e0e69-790">Il serez que vous avez configuré un tooAzure de la connexion VPN (via un VPN de Site à Site ou ExpressRoute Azure), témoin de partage de votre Active Directory/DNS service est sur site et n’est pas un fichier de toorun approprié.</span><span class="sxs-lookup"><span data-stu-id="e0e69-790">Because you would have configured a VPN connection tooAzure (via Site-to-Site VPN or Azure ExpressRoute), your Active Directory/DNS service is on-premises and isn't suitable toorun a file share witness.</span></span>

  > [!NOTE]
  > <span data-ttu-id="e0e69-791">Si votre service Active Directory/DNS s’exécute uniquement sur site, ne configurez pas votre témoin de partage de fichiers sur système d’exploitation Active Directory/DNS Windows hello locale est en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="e0e69-791">If your Active Directory/DNS service runs only on-premises, don't configure your file share witness on hello Active Directory/DNS Windows operating system that is running on-premises.</span></span> <span data-ttu-id="e0e69-792">La latence du réseau entre les nœuds de cluster exécutés dans Azure et le service Active Directory/DNS local peut être trop importante et entraîner des problèmes de connectivité.</span><span class="sxs-lookup"><span data-stu-id="e0e69-792">Network latency between cluster nodes running in Azure and Active Directory/DNS on-premises might be too large and cause connectivity issues.</span></span> <span data-ttu-id="e0e69-793">Être vraiment tooconfigure hello partage témoin de fichiers sur une machine virtuelle Azure qui exécute le nœud de cluster toohello fermer.</span><span class="sxs-lookup"><span data-stu-id="e0e69-793">Be sure tooconfigure hello file share witness on an Azure virtual machine that is running close toohello cluster node.</span></span>  
  >
  >

  <span data-ttu-id="e0e69-794">lecteur de quorum Hello doit au moins 1 024 Mo d’espace libre.</span><span class="sxs-lookup"><span data-stu-id="e0e69-794">hello quorum drive needs at least 1,024 MB of free space.</span></span> <span data-ttu-id="e0e69-795">Nous vous recommandons de 2 048 Mo d’espace libre pour le lecteur quorum hello.</span><span class="sxs-lookup"><span data-stu-id="e0e69-795">We recommend 2,048 MB of free space for hello quorum drive.</span></span>

2.  <span data-ttu-id="e0e69-796">Ajoutez l’objet nom de cluster hello.</span><span class="sxs-lookup"><span data-stu-id="e0e69-796">Add hello cluster name object.</span></span>

  ![La figure 30 : Affecter des autorisations de hello sur Partage hello pour l’objet nom de cluster hello][sap-ha-guide-figure-3019]

  <span data-ttu-id="e0e69-798">_**La figure 30 :** affecter des autorisations hello sur Partage hello pour l’objet nom de cluster hello_</span><span class="sxs-lookup"><span data-stu-id="e0e69-798">_**Figure 30:** Assign hello permissions on hello share for hello cluster name object_</span></span>

  <span data-ttu-id="e0e69-799">Assurez-vous que les autorisations hello incluent des données toochange de l’autorité hello dans un partage de hello pour l’objet nom de cluster hello (dans notre exemple, **pr1-ASC-vir$**).</span><span class="sxs-lookup"><span data-stu-id="e0e69-799">Be sure that hello permissions include hello authority toochange data in hello share for hello cluster name object (in our example, **pr1-ascs-vir$**).</span></span>

3.  <span data-ttu-id="e0e69-800">tooadd hello cluster nom objet toohello liste, sélectionnez **ajouter**.</span><span class="sxs-lookup"><span data-stu-id="e0e69-800">tooadd hello cluster name object toohello list, select **Add**.</span></span> <span data-ttu-id="e0e69-801">Modifiez toocheck de filtre hello pour les objets ordinateur dans toothose Ajout indiqué dans la Figure 31.</span><span class="sxs-lookup"><span data-stu-id="e0e69-801">Change hello filter toocheck for computer objects, in addition toothose shown in Figure 31.</span></span>

  ![Figure 31 : Modifier les ordinateurs tooinclude hello les Types d’objets][sap-ha-guide-figure-3020]

  <span data-ttu-id="e0e69-803">_**Figure 31 :** modifier hello Types d’objet tooinclude ordinateurs_</span><span class="sxs-lookup"><span data-stu-id="e0e69-803">_**Figure 31:** Change hello Object Types tooinclude computers_</span></span>

  ![Figure 32 : Sélectionnez la case à cocher ordinateurs hello][sap-ha-guide-figure-3021]

  <span data-ttu-id="e0e69-805">_**La figure 32 :** hello sélectionnez **ordinateurs** case à cocher_</span><span class="sxs-lookup"><span data-stu-id="e0e69-805">_**Figure 32:** Select hello **Computers** check box_</span></span>

4.  <span data-ttu-id="e0e69-806">Entrez l’objet nom de cluster hello comme indiqué dans la Figure 31.</span><span class="sxs-lookup"><span data-stu-id="e0e69-806">Enter hello cluster name object as shown in Figure 31.</span></span> <span data-ttu-id="e0e69-807">Car hello enregistrement a déjà été créé, vous pouvez modifier les autorisations de hello, comme indiqué dans la Figure 30.</span><span class="sxs-lookup"><span data-stu-id="e0e69-807">Because hello record has already been created, you can change hello permissions, as shown in Figure 30.</span></span>

5.  <span data-ttu-id="e0e69-808">Sélectionnez hello **sécurité** onglet de partage de hello et définissez les autorisations pour l’objet nom de cluster hello plus détaillée.</span><span class="sxs-lookup"><span data-stu-id="e0e69-808">Select hello **Security** tab of hello share, and then set more detailed permissions for hello cluster name object.</span></span>

  ![Figure 33 : Définir les attributs de sécurité hello pour l’objet nom de cluster hello sur le quorum du partage de fichier hello][sap-ha-guide-figure-3022]

  <span data-ttu-id="e0e69-810">_**Figure 33 :** définir les attributs de sécurité hello pour l’objet nom de cluster hello sur le quorum du partage de fichier hello_</span><span class="sxs-lookup"><span data-stu-id="e0e69-810">_**Figure 33:** Set hello security attributes for hello cluster name object on hello file share quorum_</span></span>

##### <span data-ttu-id="e0e69-811"><a name="4c08c387-78a0-46b1-9d27-b497b08cac3d"></a>Quorum témoin de partage de fichiers hello ensemble gestionnaire du Cluster de basculement</span><span class="sxs-lookup"><span data-stu-id="e0e69-811"><a name="4c08c387-78a0-46b1-9d27-b497b08cac3d"></a> Set hello file share witness quorum in Failover Cluster Manager</span></span>

1.  <span data-ttu-id="e0e69-812">Ouvrez hello Assistant Configuration de Quorum du paramètre.</span><span class="sxs-lookup"><span data-stu-id="e0e69-812">Open hello Configure Quorum Setting Wizard.</span></span>

  ![Figure 34 : Démarrer l’Assistant Configuration du paramètre de Quorum du Cluster de hello][sap-ha-guide-figure-3023]

  <span data-ttu-id="e0e69-814">_**Figure 34 :** Start hello Assistant Configuration des paramètres du Quorum de Cluster_</span><span class="sxs-lookup"><span data-stu-id="e0e69-814">_**Figure 34:** Start hello Configure Cluster Quorum Setting Wizard_</span></span>

2.  <span data-ttu-id="e0e69-815">Sur hello **sélectionner la Configuration de Quorum** , sélectionnez **sélectionner le témoin de quorum hello**.</span><span class="sxs-lookup"><span data-stu-id="e0e69-815">On hello **Select Quorum Configuration** page, select **Select hello quorum witness**.</span></span>

  ![Figure 35 : Configurations de quorum sélectionnables][sap-ha-guide-figure-3024]

  <span data-ttu-id="e0e69-817">_**Figure 35 :** Configurations de quorum sélectionnables_</span><span class="sxs-lookup"><span data-stu-id="e0e69-817">_**Figure 35:** Quorum configurations you can choose from_</span></span>

3.  <span data-ttu-id="e0e69-818">Sur hello **sélectionner le témoin de Quorum** , sélectionnez **configurer un témoin de partage de fichiers**.</span><span class="sxs-lookup"><span data-stu-id="e0e69-818">On hello **Select Quorum Witness** page, select **Configure a file share witness**.</span></span>

  ![Figure 36 : Témoin de partage de fichier hello Select][sap-ha-guide-figure-3025]

  <span data-ttu-id="e0e69-820">_**Figure 36 :** sélectionnez hello témoin de partage de fichiers_</span><span class="sxs-lookup"><span data-stu-id="e0e69-820">_**Figure 36:** Select hello file share witness_</span></span>

4.  <span data-ttu-id="e0e69-821">Entrez le partage de fichiers toohello hello UNC chemin (dans notre exemple, \\domcontr-0\FSW).</span><span class="sxs-lookup"><span data-stu-id="e0e69-821">Enter hello UNC path toohello file share (in our example, \\domcontr-0\FSW).</span></span> <span data-ttu-id="e0e69-822">toosee une liste de modifications hello possibles, sélectionnez **suivant**.</span><span class="sxs-lookup"><span data-stu-id="e0e69-822">toosee a list of hello changes you can make, select **Next**.</span></span>

  ![Figure 37 : Définir l’emplacement du partage de fichier pour partage de témoin hello hello][sap-ha-guide-figure-3026]

  <span data-ttu-id="e0e69-824">_**Figure 37 :** définir l’emplacement du partage de fichier pour partage de témoin hello hello_</span><span class="sxs-lookup"><span data-stu-id="e0e69-824">_**Figure 37:** Define hello file share location for hello witness share_</span></span>

5.  <span data-ttu-id="e0e69-825">Sélectionnez hello modifications souhaitées, puis sélectionnez **suivant**.</span><span class="sxs-lookup"><span data-stu-id="e0e69-825">Select hello changes you want, and then select **Next**.</span></span> <span data-ttu-id="e0e69-826">Vous devez toosuccessfully reconfigurer la configuration du cluster hello comme indiqué dans la Figure 38.</span><span class="sxs-lookup"><span data-stu-id="e0e69-826">You need toosuccessfully reconfigure hello cluster configuration as shown in Figure 38.</span></span>  

  ![Figure 38 : Confirmation que vous avez reconfiguré le cluster de hello][sap-ha-guide-figure-3027]

  <span data-ttu-id="e0e69-828">_**Figure 38 :** Confirmation que vous avez reconfiguré le cluster de hello_</span><span class="sxs-lookup"><span data-stu-id="e0e69-828">_**Figure 38:** Confirmation that you've reconfigured hello cluster_</span></span>

<span data-ttu-id="e0e69-829">Après avoir installé hello Cluster de basculement Windows avec succès, les modifications doivent toobe apportée toosome seuils tooadapt basculement détection tooconditions dans Azure.</span><span class="sxs-lookup"><span data-stu-id="e0e69-829">After installing hello Windows Failover Cluster successfully, changes need toobe made toosome thresholds tooadapt failover detection tooconditions in Azure.</span></span> <span data-ttu-id="e0e69-830">Hello toobe paramètres modifié sont documentées dans ce billet de blog : https://blogs.msdn.microsoft.com/clustering/2012/11/21/tuning-failover-cluster-network-thresholds/.</span><span class="sxs-lookup"><span data-stu-id="e0e69-830">hello parameters toobe changed are documented in this blog: https://blogs.msdn.microsoft.com/clustering/2012/11/21/tuning-failover-cluster-network-thresholds/ .</span></span> <span data-ttu-id="e0e69-831">En supposant que vos deux machines virtuelles qui générer hello Configuration en Cluster Windows pour ASCS/SCS sont dans hello même sous-réseau, hello paramètres suivants doivent toobe modifié toothese valeurs :</span><span class="sxs-lookup"><span data-stu-id="e0e69-831">Assuming that your two VMs that build hello Windows Cluster Configuration for ASCS/SCS are in hello same SubNet, hello following parameters need toobe changed toothese values:</span></span>
- <span data-ttu-id="e0e69-832">SameSubNetDelay = 2</span><span class="sxs-lookup"><span data-stu-id="e0e69-832">SameSubNetDelay = 2</span></span>
- <span data-ttu-id="e0e69-833">SameSubNetThreshold = 15</span><span class="sxs-lookup"><span data-stu-id="e0e69-833">SameSubNetThreshold = 15</span></span>

<span data-ttu-id="e0e69-834">Ces paramètres ont été testés avec les clients et fournis un bon compromis toobe suffisamment résilient hello un côté.</span><span class="sxs-lookup"><span data-stu-id="e0e69-834">These settings were tested with customers and provided a good compromise toobe resilient enough on hello one side.</span></span> <span data-ttu-id="e0e69-835">Sur hello contre ces paramètres ont été fournissant rapide suffisamment basculement dans les conditions d’erreur réelle en cas d’échec de nœud/machine virtuelle ou de logiciels SAP.</span><span class="sxs-lookup"><span data-stu-id="e0e69-835">On hello other hand those settings were providing fast enough failover in real error conditions on SAP software or node/VM failure.</span></span> 

### <span data-ttu-id="e0e69-836"><a name="5c8e5482-841e-45e1-a89d-a05c0907c868"></a>Installer SIOS DataKeeper Cluster Edition pour le disque de partage de cluster hello SAP ASCS/SCS</span><span class="sxs-lookup"><span data-stu-id="e0e69-836"><a name="5c8e5482-841e-45e1-a89d-a05c0907c868"></a> Install SIOS DataKeeper Cluster Edition for hello SAP ASCS/SCS cluster share disk</span></span>

<span data-ttu-id="e0e69-837">Vous disposez maintenant d’une configuration fonctionnelle de clustering de basculement Windows Server dans Azure.</span><span class="sxs-lookup"><span data-stu-id="e0e69-837">You now have a working Windows Server Failover Clustering configuration in Azure.</span></span> <span data-ttu-id="e0e69-838">Mais, tooinstall une instance SAP ASCS/SCS, vous avez besoin d’une ressource de disque partagé.</span><span class="sxs-lookup"><span data-stu-id="e0e69-838">But, tooinstall an SAP ASCS/SCS instance, you need a shared disk resource.</span></span> <span data-ttu-id="e0e69-839">Impossible de créer des ressources de disque hello partagé que nécessaires dans Azure.</span><span class="sxs-lookup"><span data-stu-id="e0e69-839">You cannot create hello shared disk resources you need in Azure.</span></span> <span data-ttu-id="e0e69-840">SIOS DataKeeper Cluster Edition est une solution de tiers que vous pouvez utiliser les ressources de disque toocreate partagé.</span><span class="sxs-lookup"><span data-stu-id="e0e69-840">SIOS DataKeeper Cluster Edition is a third-party solution you can use toocreate shared disk resources.</span></span>

<span data-ttu-id="e0e69-841">Installation de l’édition de Cluster SIOS DataKeeper pour hello SAP ASCS/SCS disque de cluster partage implique les tâches :</span><span class="sxs-lookup"><span data-stu-id="e0e69-841">Installing SIOS DataKeeper Cluster Edition for hello SAP ASCS/SCS cluster share disk involves these tasks:</span></span>

- <span data-ttu-id="e0e69-842">Ajout de hello .NET Framework 3.5</span><span class="sxs-lookup"><span data-stu-id="e0e69-842">Adding hello .NET Framework 3.5</span></span>
- <span data-ttu-id="e0e69-843">Installation de SIOS DataKeeper</span><span class="sxs-lookup"><span data-stu-id="e0e69-843">Installing SIOS DataKeeper</span></span>
- <span data-ttu-id="e0e69-844">Configuration de SIOS DataKeeper</span><span class="sxs-lookup"><span data-stu-id="e0e69-844">Setting up SIOS DataKeeper</span></span>

#### <span data-ttu-id="e0e69-845"><a name="1c2788c3-3648-4e82-9e0d-e058e475e2a3"></a>Ajouter hello .NET Framework 3.5</span><span class="sxs-lookup"><span data-stu-id="e0e69-845"><a name="1c2788c3-3648-4e82-9e0d-e058e475e2a3"></a> Add hello .NET Framework 3.5</span></span>
<span data-ttu-id="e0e69-846">Hello Microsoft .NET Framework 3.5 n’est pas automatiquement activé ou installé sur Windows Server 2012 R2.</span><span class="sxs-lookup"><span data-stu-id="e0e69-846">hello Microsoft .NET Framework 3.5 isn't automatically activated or installed on Windows Server 2012 R2.</span></span> <span data-ttu-id="e0e69-847">SIOS DataKeeper nécessitant toobe de .NET Framework hello sur tous les nœuds que vous installez DataKeeper sur, vous devez installer hello .NET Framework 3.5 sur hello systèmes d’exploitation de tous les ordinateurs virtuels dans un cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="e0e69-847">Because SIOS DataKeeper requires hello .NET Framework toobe on all nodes that you install DataKeeper on, you must install hello .NET Framework 3.5 on hello guest operating system of all virtual machines in hello cluster.</span></span>

<span data-ttu-id="e0e69-848">Il existe deux hello de tooadd méthodes .NET Framework 3.5 :</span><span class="sxs-lookup"><span data-stu-id="e0e69-848">There are two ways tooadd hello .NET Framework 3.5:</span></span>

- <span data-ttu-id="e0e69-849">Utiliser hello ajouter Assistant de rôles et fonctionnalités dans Windows, comme indiqué dans la Figure 39.</span><span class="sxs-lookup"><span data-stu-id="e0e69-849">Use hello Add Roles and Features Wizard in Windows as shown in Figure 39.</span></span>

  ![Figure 39 : Installer hello .NET Framework 3.5 à l’aide de hello Ajout de rôles et fonctionnalités Assistant][sap-ha-guide-figure-3028]

  <span data-ttu-id="e0e69-851">_**Figure 39 :** hello installer .NET Framework 3.5 à l’aide de hello Ajout de rôles et fonctionnalités Assistant_</span><span class="sxs-lookup"><span data-stu-id="e0e69-851">_**Figure 39:** Install hello .NET Framework 3.5 by using hello Add Roles and Features Wizard_</span></span>

  ![Figure 40 : Progression de l’Installation de la barre lorsque vous installez hello .NET Framework 3.5 à l’aide de hello Ajout de rôles et fonctionnalités Assistant][sap-ha-guide-figure-3029]

  <span data-ttu-id="e0e69-853">_**Figure 40 :** progression de l’Installation de la barre lorsque vous installez hello .NET Framework 3.5 à l’aide de hello Ajout de rôles et fonctionnalités Assistant_</span><span class="sxs-lookup"><span data-stu-id="e0e69-853">_**Figure 40:** Installation progress bar when you install hello .NET Framework 3.5 by using hello Add Roles and Features Wizard_</span></span>

- <span data-ttu-id="e0e69-854">À présent utiliser dism.exe d’outil de ligne de commande hello.</span><span class="sxs-lookup"><span data-stu-id="e0e69-854">Use hello command-line tool dism.exe.</span></span> <span data-ttu-id="e0e69-855">Pour ce type d’installation, vous avez besoin d’un répertoire SxS tooaccess hello hello support d’installation Windows.</span><span class="sxs-lookup"><span data-stu-id="e0e69-855">For this type of installation, you need tooaccess hello SxS directory on hello Windows installation media.</span></span> <span data-ttu-id="e0e69-856">Dans une invite de commandes avec élévation de privilèges, tapez :</span><span class="sxs-lookup"><span data-stu-id="e0e69-856">At an elevated command prompt, type:</span></span>

  ```
  Dism /online /enable-feature /featurename:NetFx3 /All /Source:installation_media_drive:\sources\sxs /LimitAccess
  ```

#### <span data-ttu-id="e0e69-857"><a name="dd41d5a2-8083-415b-9878-839652812102"></a> Installer SIOS DataKeeper</span><span class="sxs-lookup"><span data-stu-id="e0e69-857"><a name="dd41d5a2-8083-415b-9878-839652812102"></a> Install SIOS DataKeeper</span></span>

<span data-ttu-id="e0e69-858">Installez SIOS DataKeeper Cluster Edition sur chaque nœud de cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="e0e69-858">Install SIOS DataKeeper Cluster Edition on each node in hello cluster.</span></span> <span data-ttu-id="e0e69-859">un stockage partagé virtuel toocreate avec SIOS DataKeeper, créer un miroir synchronisé et simuler ensuite le stockage partagé de cluster.</span><span class="sxs-lookup"><span data-stu-id="e0e69-859">toocreate virtual shared storage with SIOS DataKeeper, create a synced mirror and then simulate cluster shared storage.</span></span>

<span data-ttu-id="e0e69-860">Avant d’installer des logiciels SIOS hello, créez l’utilisateur de domaine hello **DataKeeperSvc**.</span><span class="sxs-lookup"><span data-stu-id="e0e69-860">Before you install hello SIOS software, create hello domain user **DataKeeperSvc**.</span></span>

> [!NOTE]
> <span data-ttu-id="e0e69-861">Ajouter hello **DataKeeperSvc** utilisateur toohello **administrateur Local** groupe sur les deux nœuds de cluster.</span><span class="sxs-lookup"><span data-stu-id="e0e69-861">Add hello **DataKeeperSvc** user toohello **Local Administrator** group on both cluster nodes.</span></span>
>
>

<span data-ttu-id="e0e69-862">tooinstall SIOS DataKeeper :</span><span class="sxs-lookup"><span data-stu-id="e0e69-862">tooinstall SIOS DataKeeper:</span></span>

1.  <span data-ttu-id="e0e69-863">Installer le logiciel SIOS hello sur les deux nœuds de cluster.</span><span class="sxs-lookup"><span data-stu-id="e0e69-863">Install hello SIOS software on both cluster nodes.</span></span>

  ![Programme d’installation de SIOS][sap-ha-guide-figure-3030]

  ![Figure 41 : Première page de hello SIOS DataKeeper installation][sap-ha-guide-figure-3031]

  <span data-ttu-id="e0e69-866">_**Figure 41 :** première page de hello SIOS DataKeeper installation_</span><span class="sxs-lookup"><span data-stu-id="e0e69-866">_**Figure 41:** First page of hello SIOS DataKeeper installation_</span></span>

2.  <span data-ttu-id="e0e69-867">Dans la boîte de dialogue hello indiqué dans la Figure 42, sélectionnez **Oui**.</span><span class="sxs-lookup"><span data-stu-id="e0e69-867">In hello dialog box shown in Figure 42, select **Yes**.</span></span>

  ![Figure 42 : DataKeeper vous indique qu’un service va être désactivé][sap-ha-guide-figure-3032]

  <span data-ttu-id="e0e69-869">_**Figure 42 :** DataKeeper vous indique qu’un service va être désactivé_</span><span class="sxs-lookup"><span data-stu-id="e0e69-869">_**Figure 42:** DataKeeper informs you that a service will be disabled_</span></span>

3.  <span data-ttu-id="e0e69-870">Dans la boîte de dialogue hello illustré à la Figure 43, nous vous recommandons de sélectionner **compte de domaine ou serveur**.</span><span class="sxs-lookup"><span data-stu-id="e0e69-870">In hello dialog box shown in Figure 43, we recommend that you select **Domain or Server account**.</span></span>

  ![Figure 43 : Sélection de l’utilisateur de SIOS DataKeeper][sap-ha-guide-figure-3033]

  <span data-ttu-id="e0e69-872">_**Figure 43:** Sélection de l’utilisateur de SIOS DataKeeper_</span><span class="sxs-lookup"><span data-stu-id="e0e69-872">_**Figure 43:** User selection for SIOS DataKeeper_</span></span>

4.  <span data-ttu-id="e0e69-873">Entrez le nom d’utilisateur domaine hello et des mots de passe que vous avez créé pour SIOS DataKeeper.</span><span class="sxs-lookup"><span data-stu-id="e0e69-873">Enter hello domain account user name and passwords that you created for SIOS DataKeeper.</span></span>

  ![Figure 44 : Entrez les nom d’utilisateur de domaine de hello et un mot de passe pour hello SIOS DataKeeper installation][sap-ha-guide-figure-3034]

  <span data-ttu-id="e0e69-875">_**Figure 44 :** Entrez le nom d’utilisateur de domaine de hello et un mot de passe pour hello SIOS DataKeeper installation_</span><span class="sxs-lookup"><span data-stu-id="e0e69-875">_**Figure 44:** Enter hello domain user name and password for hello SIOS DataKeeper installation_</span></span>

5.  <span data-ttu-id="e0e69-876">Installez la clé de licence hello pour votre instance de SIOS DataKeeper, comme indiqué dans la Figure 45.</span><span class="sxs-lookup"><span data-stu-id="e0e69-876">Install hello license key for your SIOS DataKeeper instance as shown in Figure 45.</span></span>

  ![Figure 45 : Entrer votre clé licence SIOS DataKeeper][sap-ha-guide-figure-3035]

  <span data-ttu-id="e0e69-878">_**Figure 45 :** Entrer votre clé de licence SIOS DataKeeper_</span><span class="sxs-lookup"><span data-stu-id="e0e69-878">_**Figure 45:** Enter your SIOS DataKeeper license key_</span></span>

6.  <span data-ttu-id="e0e69-879">Lorsque vous y êtes invité, redémarrez hello virtual machine.</span><span class="sxs-lookup"><span data-stu-id="e0e69-879">When prompted, restart hello virtual machine.</span></span>

#### <span data-ttu-id="e0e69-880"><a name="d9c1fc8e-8710-4dff-bec2-1f535db7b006"></a> Configurer SIOS DataKeeper</span><span class="sxs-lookup"><span data-stu-id="e0e69-880"><a name="d9c1fc8e-8710-4dff-bec2-1f535db7b006"></a> Set up SIOS DataKeeper</span></span>

<span data-ttu-id="e0e69-881">Après avoir installé SIOS DataKeeper sur les deux nœuds, vous avez besoin de configuration de hello toostart.</span><span class="sxs-lookup"><span data-stu-id="e0e69-881">After you install SIOS DataKeeper on both nodes, you need toostart hello configuration.</span></span> <span data-ttu-id="e0e69-882">Hello configuration de hello vise toohave la réplication synchrone des données entre hello tooeach de disques durs virtuels attachés supplémentaire d’ordinateurs virtuels hello.</span><span class="sxs-lookup"><span data-stu-id="e0e69-882">hello goal of hello configuration is toohave synchronous data replication between hello additional VHDs attached tooeach of hello virtual machines.</span></span>

1.  <span data-ttu-id="e0e69-883">Démarrer hello DataKeeper Management et l’outil de Configuration, puis sélectionnez **connexion serveur**.</span><span class="sxs-lookup"><span data-stu-id="e0e69-883">Start hello DataKeeper Management and Configuration tool, and then select **Connect Server**.</span></span> <span data-ttu-id="e0e69-884">(Cette option est entourée en rouge dans la figure 46.)</span><span class="sxs-lookup"><span data-stu-id="e0e69-884">(In Figure 46, this option is circled in red.)</span></span>

  ![Figure 46 : Outil de configuration et de gestion de SIOS DataKeeper][sap-ha-guide-figure-3036]

  <span data-ttu-id="e0e69-886">_**Figure 46 :** Outil de configuration et de gestion de SIOS DataKeeper_</span><span class="sxs-lookup"><span data-stu-id="e0e69-886">_**Figure 46:** SIOS DataKeeper Management and Configuration tool_</span></span>

2.  <span data-ttu-id="e0e69-887">Entrez hello nom ou adresse TCP/IP de hello premier nœud hello outil et de gestion Configuration doit se connecter à, puis, dans un deuxième temps, le nœud de deuxième hello.</span><span class="sxs-lookup"><span data-stu-id="e0e69-887">Enter hello name or TCP/IP address of hello first node hello Management and Configuration tool should connect to, and, in a second step, hello second node.</span></span>

  ![Figure 47 : Insérer le nom hello ou une adresse TCP/IP de hello premier nœud hello outil et de gestion Configuration doit se connecter à et dans un deuxième temps, le nœud de deuxième hello][sap-ha-guide-figure-3037]

  <span data-ttu-id="e0e69-889">_**Figure 47 :** insérer le nom hello ou une adresse TCP/IP de hello premier nœud hello outil et de gestion Configuration doit se connecter à et dans un deuxième temps, le nœud de deuxième hello_</span><span class="sxs-lookup"><span data-stu-id="e0e69-889">_**Figure 47:** Insert hello name or TCP/IP address of hello first node hello Management and Configuration tool should connect to, and in a second step, hello second node_</span></span>

3.  <span data-ttu-id="e0e69-890">Créer un travail de réplication hello entre deux nœuds de hello.</span><span class="sxs-lookup"><span data-stu-id="e0e69-890">Create hello replication job between hello two nodes.</span></span>

  ![Figure 48 : Créer un travail de réplication][sap-ha-guide-figure-3038]

  <span data-ttu-id="e0e69-892">_**Figure 48 :** Créer un travail de réplication_</span><span class="sxs-lookup"><span data-stu-id="e0e69-892">_**Figure 48:** Create a replication job_</span></span>

  <span data-ttu-id="e0e69-893">Un Assistant vous guide tout au long des processus de hello de création d’un travail de réplication.</span><span class="sxs-lookup"><span data-stu-id="e0e69-893">A wizard guides you through hello process of creating a replication job.</span></span>
4.  <span data-ttu-id="e0e69-894">Définissez hello nom et adresse TCP/IP, volume de disque du nœud de source de hello.</span><span class="sxs-lookup"><span data-stu-id="e0e69-894">Define hello name, TCP/IP address, and disk volume of hello source node.</span></span>

  ![Figure 49 : Définissez le nom de hello du travail de réplication hello][sap-ha-guide-figure-3039]

  <span data-ttu-id="e0e69-896">_**Figure 49 :** nom hello de définir de tâche de réplication hello_</span><span class="sxs-lookup"><span data-stu-id="e0e69-896">_**Figure 49:** Define hello name of hello replication job_</span></span>

  ![Figure 50 : Définir les données de base hello pour nœud hello, qui doit être de nœud de source hello actuel][sap-ha-guide-figure-3040]

  <span data-ttu-id="e0e69-898">_**Figure 50 :** définissent les données de base hello pour nœud hello, qui doit être de nœud de source hello actuel_</span><span class="sxs-lookup"><span data-stu-id="e0e69-898">_**Figure 50:** Define hello base data for hello node, which should be hello current source node_</span></span>

5.  <span data-ttu-id="e0e69-899">Définissez hello nom et adresse TCP/IP, volume de disque du nœud cible de hello.</span><span class="sxs-lookup"><span data-stu-id="e0e69-899">Define hello name, TCP/IP address, and disk volume of hello target node.</span></span>

  ![Figure 51 : Définir les données de base hello pour nœud hello, qui doit être nœud cible en cours de hello][sap-ha-guide-figure-3041]

  <span data-ttu-id="e0e69-901">_**Figure 51 :** définissent les données de base hello pour nœud hello, qui doit être nœud cible en cours de hello_</span><span class="sxs-lookup"><span data-stu-id="e0e69-901">_**Figure 51:** Define hello base data for hello node, which should be hello current target node_</span></span>

6.  <span data-ttu-id="e0e69-902">Définir les algorithmes de compression hello.</span><span class="sxs-lookup"><span data-stu-id="e0e69-902">Define hello compression algorithms.</span></span> <span data-ttu-id="e0e69-903">Dans notre exemple, nous vous recommandons de compresser les flux de réplication hello.</span><span class="sxs-lookup"><span data-stu-id="e0e69-903">In our example, we recommend that you compress hello replication stream.</span></span> <span data-ttu-id="e0e69-904">En particulier dans les situations de resynchronisation, la compression du flux de réplication hello hello réduit considérablement les temps de resynchronisation.</span><span class="sxs-lookup"><span data-stu-id="e0e69-904">Especially in resynchronization situations, hello compression of hello replication stream dramatically reduces resynchronization time.</span></span> <span data-ttu-id="e0e69-905">Notez que la compression utilise des ressources de processeur et de RAM hello d’un ordinateur virtuel.</span><span class="sxs-lookup"><span data-stu-id="e0e69-905">Note that compression uses hello CPU and RAM resources of a virtual machine.</span></span> <span data-ttu-id="e0e69-906">Comme le taux de compression hello augmente, donc hello que le volume de ressources du processeur utilisées.</span><span class="sxs-lookup"><span data-stu-id="e0e69-906">As hello compression rate increases, so does hello volume of CPU resources used.</span></span> <span data-ttu-id="e0e69-907">Vous pouvez également ajuster ce paramètre ultérieurement.</span><span class="sxs-lookup"><span data-stu-id="e0e69-907">You also can adjust this setting later.</span></span>

7.  <span data-ttu-id="e0e69-908">Un autre paramètre, vous devez toocheck sera si hello réplication synchrone ou asynchrone.</span><span class="sxs-lookup"><span data-stu-id="e0e69-908">Another setting you need toocheck is whether hello replication occurs asynchronously or synchronously.</span></span> <span data-ttu-id="e0e69-909">*Lorsque vous protégez des configurations SAP ASCS/SCS, vous devez utiliser la réplication synchrone*.</span><span class="sxs-lookup"><span data-stu-id="e0e69-909">*When you protect SAP ASCS/SCS configurations, you must use synchronous replication*.</span></span>  

  ![Figure 52 : Définir les détails de la réplication][sap-ha-guide-figure-3042]

  <span data-ttu-id="e0e69-911">_**Figure 52 :** Définir les détails de la réplication_</span><span class="sxs-lookup"><span data-stu-id="e0e69-911">_**Figure 52:** Define replication details_</span></span>

8.  <span data-ttu-id="e0e69-912">Définir si le volume hello répliquée par le travail de réplication hello doit être représenté tooa configuration de cluster Clustering de basculement Windows Server comme un disque partagé.</span><span class="sxs-lookup"><span data-stu-id="e0e69-912">Define whether hello volume that is replicated by hello replication job should be represented tooa Windows Server Failover Clustering cluster configuration as a shared disk.</span></span> <span data-ttu-id="e0e69-913">Pour une configuration SAP ASCS/SCS hello, sélectionnez **Oui** afin que Windows hello cluster voit hello volume répliqué comme un disque partagé qu’il peut utiliser comme un volume de cluster.</span><span class="sxs-lookup"><span data-stu-id="e0e69-913">For hello SAP ASCS/SCS configuration, select **Yes** so that hello Windows cluster sees hello replicated volume as a shared disk that it can use as a cluster volume.</span></span>

  ![Figure 53 : Sélectionnez Oui tooset hello répliquées volume comme volume de cluster][sap-ha-guide-figure-3043]

  <span data-ttu-id="e0e69-915">_**Figure 53 :** sélectionnez **Oui** tooset hello répliquées que le volume d’un cluster_</span><span class="sxs-lookup"><span data-stu-id="e0e69-915">_**Figure 53:** Select **Yes** tooset hello replicated volume as a cluster volume_</span></span>

  <span data-ttu-id="e0e69-916">Après la création de volume de hello, outil de Configuration et la gestion de DataKeeper hello illustre que cette tâche de réplication hello est active.</span><span class="sxs-lookup"><span data-stu-id="e0e69-916">After hello volume is created, hello DataKeeper Management and Configuration tool shows that hello replication job is active.</span></span>

  ![Figure 54 : DataKeeper mise en miroir synchrone de hello SAP ASCS/SCS partage de disque est actif][sap-ha-guide-figure-3044]

  <span data-ttu-id="e0e69-918">_**Figure 54 :** la mise en miroir synchrone de DataKeeper pour hello SAP ASCS/SCS de partage de disque est actif_</span><span class="sxs-lookup"><span data-stu-id="e0e69-918">_**Figure 54:** DataKeeper synchronous mirroring for hello SAP ASCS/SCS share disk is active_</span></span>

  <span data-ttu-id="e0e69-919">Gestionnaire du Cluster de basculement affiche maintenant disque hello en tant que DataKeeper disque, comme indiqué dans la Figure 55.</span><span class="sxs-lookup"><span data-stu-id="e0e69-919">Failover Cluster Manager now shows hello disk as a DataKeeper disk, as shown in Figure 55.</span></span>

  ![Figure 55 : Le Gestionnaire du Cluster de basculement présente disque hello DataKeeper de réplication][sap-ha-guide-figure-3045]

  <span data-ttu-id="e0e69-921">_**Figure 55 :** Gestionnaire du Cluster de basculement affiche les disques hello que DataKeeper répliquée_</span><span class="sxs-lookup"><span data-stu-id="e0e69-921">_**Figure 55:** Failover Cluster Manager shows hello disk that DataKeeper replicated_</span></span>

## <span data-ttu-id="e0e69-922"><a name="a06f0b49-8a7a-42bf-8b0d-c12026c5746b"></a>Installer le système SAP NetWeaver de hello</span><span class="sxs-lookup"><span data-stu-id="e0e69-922"><a name="a06f0b49-8a7a-42bf-8b0d-c12026c5746b"></a> Install hello SAP NetWeaver system</span></span>

<span data-ttu-id="e0e69-923">Nous ne décrivons le programme d’installation de hello SGBD, car les configurations varient en fonction de hello système SGBD que vous utilisez.</span><span class="sxs-lookup"><span data-stu-id="e0e69-923">We won’t describe hello DBMS setup because setups vary depending on hello DBMS system you use.</span></span> <span data-ttu-id="e0e69-924">Toutefois, nous supposons que haute disponibilité avec hello SGBD tenant avec fonctionnalités hello prennent en charge de différents fournisseurs de SGBD hello pour Azure.</span><span class="sxs-lookup"><span data-stu-id="e0e69-924">However, we assume that high-availability concerns with hello DBMS are addressed with hello functionalities hello different DBMS vendors support for Azure.</span></span> <span data-ttu-id="e0e69-925">par exemple Always On ou la mise en miroir de base de données pour SQL Server, et Oracle Data Guard pour bases de données Oracle.</span><span class="sxs-lookup"><span data-stu-id="e0e69-925">For example, Always On or database mirroring for SQL Server, and Oracle Data Guard for Oracle databases.</span></span> <span data-ttu-id="e0e69-926">Dans le scénario de hello que nous utilisons dans cet article, nous n’avez pas ajouté plus protection toohello SGBD.</span><span class="sxs-lookup"><span data-stu-id="e0e69-926">In hello scenario we use in this article, we didn't add more protection toohello DBMS.</span></span>

<span data-ttu-id="e0e69-927">Il n’existe pas de considérations particulières lorsque différents services de SGBD interagissent avec ce type de configuration SAP ASCS/SCS en cluster dans Azure.</span><span class="sxs-lookup"><span data-stu-id="e0e69-927">There are no special considerations when different DBMS services interact with this kind of clustered SAP ASCS/SCS configuration in Azure.</span></span>

> [!NOTE]
> <span data-ttu-id="e0e69-928">procédures d’installation Hello des systèmes de ABAP SAP NetWeaver, les systèmes de Java et les systèmes ABAP + Java sont presque identiques.</span><span class="sxs-lookup"><span data-stu-id="e0e69-928">hello installation procedures of SAP NetWeaver ABAP systems, Java systems, and ABAP+Java systems are almost identical.</span></span> <span data-ttu-id="e0e69-929">différence la plus significative Hello est qu’une seule instance ASC sur un système SAP ABAP.</span><span class="sxs-lookup"><span data-stu-id="e0e69-929">hello most significant difference is that an SAP ABAP system has one ASCS instance.</span></span> <span data-ttu-id="e0e69-930">Hello système Java de SAP a une seule instance SCS.</span><span class="sxs-lookup"><span data-stu-id="e0e69-930">hello SAP Java system has one SCS instance.</span></span> <span data-ttu-id="e0e69-931">Hello système SAP ABAP + Java a une seule instance ASC et une seule instance SCS en cours d’exécution hello même groupe de clusters de basculement de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="e0e69-931">hello SAP ABAP+Java system has one ASCS instance and one SCS instance running in hello same Microsoft failover cluster group.</span></span> <span data-ttu-id="e0e69-932">Toute différence d’installation pour chaque pile d’installation de SAP NetWeaver est mentionnée explicitement.</span><span class="sxs-lookup"><span data-stu-id="e0e69-932">Any installation differences for each SAP NetWeaver installation stack are explicitly mentioned.</span></span> <span data-ttu-id="e0e69-933">Vous pouvez supposer que toutes les autres parties sont hello identiques.</span><span class="sxs-lookup"><span data-stu-id="e0e69-933">You can assume that all other parts are hello same.</span></span>  
>
>

### <span data-ttu-id="e0e69-934"><a name="31c6bd4f-51df-4057-9fdf-3fcbc619c170"></a> Installer SAP avec une instance ASCS/SCS à haute disponibilité</span><span class="sxs-lookup"><span data-stu-id="e0e69-934"><a name="31c6bd4f-51df-4057-9fdf-3fcbc619c170"></a> Install SAP with a high-availability ASCS/SCS instance</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e0e69-935">Veillez pas les tooplace du fichier de votre page sur DataKeeper des volumes en miroir.</span><span class="sxs-lookup"><span data-stu-id="e0e69-935">Be sure not tooplace your page file on DataKeeper mirrored volumes.</span></span> <span data-ttu-id="e0e69-936">DataKeeper ne prend pas en charge les volumes mis en miroir.</span><span class="sxs-lookup"><span data-stu-id="e0e69-936">DataKeeper does not support mirrored volumes.</span></span> <span data-ttu-id="e0e69-937">Vous pouvez laisser votre fichier d’échange sur le lecteur temporaire hello D d’une machine virtuelle Azure, qui est la valeur par défaut hello.</span><span class="sxs-lookup"><span data-stu-id="e0e69-937">You can leave your page file on hello temporary drive D of an Azure virtual machine, which is hello default.</span></span> <span data-ttu-id="e0e69-938">S’il n’y ne figure pas déjà, déplacez la page fichier toodrive D hello Windows de votre machine virtuelle Azure.</span><span class="sxs-lookup"><span data-stu-id="e0e69-938">If it's not already there, move hello Windows page file toodrive D of your Azure virtual machine.</span></span>
>
>

<span data-ttu-id="e0e69-939">L’installation de SAP avec une instance ASCS/SCS à haute disponibilité implique les tâches suivantes :</span><span class="sxs-lookup"><span data-stu-id="e0e69-939">Installing SAP with a high-availability ASCS/SCS instance involves these tasks:</span></span>

- <span data-ttu-id="e0e69-940">Création d’un nom d’hôte virtuel d’instance de SAP ASCS/SCS hello en cluster</span><span class="sxs-lookup"><span data-stu-id="e0e69-940">Creating a virtual host name for hello clustered SAP ASCS/SCS instance</span></span>
- <span data-ttu-id="e0e69-941">Lors de l’installation hello SAP premier nœud de cluster</span><span class="sxs-lookup"><span data-stu-id="e0e69-941">Installing hello SAP first cluster node</span></span>
- <span data-ttu-id="e0e69-942">Modifier le profil SAP hello de l’instance ASCS/SCS hello</span><span class="sxs-lookup"><span data-stu-id="e0e69-942">Modifying hello SAP profile of hello ASCS/SCS instance</span></span>
- <span data-ttu-id="e0e69-943">Ajout d'un port de sondage</span><span class="sxs-lookup"><span data-stu-id="e0e69-943">Adding a probe port</span></span>
- <span data-ttu-id="e0e69-944">Ouverture du port de sondage du pare-feu Windows hello</span><span class="sxs-lookup"><span data-stu-id="e0e69-944">Opening hello Windows firewall probe port</span></span>

#### <span data-ttu-id="e0e69-945"><a name="a97ad604-9094-44fe-a364-f89cb39bf097"></a>Créer un nom d’hôte virtuel d’instance de SAP ASCS/SCS hello en cluster</span><span class="sxs-lookup"><span data-stu-id="e0e69-945"><a name="a97ad604-9094-44fe-a364-f89cb39bf097"></a> Create a virtual host name for hello clustered SAP ASCS/SCS instance</span></span>

1.  <span data-ttu-id="e0e69-946">Dans le Gestionnaire DNS Windows hello, créez une entrée DNS pour le nom d’hôte virtuel hello de l’instance ASCS/SCS hello.</span><span class="sxs-lookup"><span data-stu-id="e0e69-946">In hello Windows DNS manager, create a DNS entry for hello virtual host name of hello ASCS/SCS instance.</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="e0e69-947">Hello adresse IP que vous attribuez le nom d’hôte virtuel toohello Hello ASCS/SCS instance doit être hello même en tant qu’adresse IP de hello que vous avez affecté tooAzure équilibrage de charge (**<*SID*> - lb - ASC **).</span><span class="sxs-lookup"><span data-stu-id="e0e69-947">hello IP address that you assign toohello virtual host name of hello ASCS/SCS instance must be hello same as hello IP address that you assigned tooAzure Load Balancer (**<*SID*>-lb-ascs**).</span></span>  
  >
  >

  <span data-ttu-id="e0e69-948">Hello d’adresse IP du nom d’hôte hello virtuel SAP ASCS/SCS (**pr1 ASC sap**) est identique à hello en tant qu’adresse IP de hello d’équilibrage de charge Azure (**pr1-lb-ASC**).</span><span class="sxs-lookup"><span data-stu-id="e0e69-948">hello IP address of hello virtual SAP ASCS/SCS host name (**pr1-ascs-sap**) is hello same as hello IP address of Azure Load Balancer (**pr1-lb-ascs**).</span></span>

  ![Figure 56 : Définir l’entrée DNS de hello pour le nom virtuel du cluster SAP ASCS/SCS hello et adresse TCP/IP][sap-ha-guide-figure-3046]

  <span data-ttu-id="e0e69-950">_**Figure 56 :** définir l’entrée DNS de hello pour le nom virtuel du cluster SAP ASCS/SCS hello et adresse TCP/IP_</span><span class="sxs-lookup"><span data-stu-id="e0e69-950">_**Figure 56:** Define hello DNS entry for hello SAP ASCS/SCS cluster virtual name and TCP/IP address_</span></span>

2.  <span data-ttu-id="e0e69-951">toodefine hello IP adresse affectée toohello nom d’hôte virtuel, sélectionnez **Gestionnaire DNS** > **domaine**.</span><span class="sxs-lookup"><span data-stu-id="e0e69-951">toodefine hello IP address assigned toohello virtual host name, select **DNS Manager** > **Domain**.</span></span>

  ![Figure 57 : Nouveau nom virtuel et nouvelle adresse TCP/IP de la configuration du cluster SAP ASCS/SCS][sap-ha-guide-figure-3047]

  <span data-ttu-id="e0e69-953">_**Figure 57 :** Nouveau nom virtuel et nouvelle adresse TCP/IP de la configuration du cluster SAP ASCS/SCS_</span><span class="sxs-lookup"><span data-stu-id="e0e69-953">_**Figure 57:** New virtual name and TCP/IP address for SAP ASCS/SCS cluster configuration_</span></span>

#### <span data-ttu-id="e0e69-954"><a name="eb5af918-b42f-4803-bb50-eff41f84b0b0"></a>Installer hello SAP premier nœud de cluster</span><span class="sxs-lookup"><span data-stu-id="e0e69-954"><a name="eb5af918-b42f-4803-bb50-eff41f84b0b0"></a> Install hello SAP first cluster node</span></span>

1.  <span data-ttu-id="e0e69-955">Exécuter l’option de nœud de cluster première hello sur le nœud de cluster A. Par exemple, sur hello **pr1-ascs-0** hôte.</span><span class="sxs-lookup"><span data-stu-id="e0e69-955">Execute hello first cluster node option on cluster node A. For example, on hello **pr1-ascs-0** host.</span></span>
2.  <span data-ttu-id="e0e69-956">les ports par défaut tookeep hello pour hello Azure interne l’équilibrage de charge, sélectionnez :</span><span class="sxs-lookup"><span data-stu-id="e0e69-956">tookeep hello default ports for hello Azure internal load balancer, select:</span></span>

  * <span data-ttu-id="e0e69-957">**Système ABAP** : numéro d’instance **ASCS****00**</span><span class="sxs-lookup"><span data-stu-id="e0e69-957">**ABAP system**: **ASCS** instance number **00**</span></span>
  * <span data-ttu-id="e0e69-958">**Système Java** : numéro d’instance **SCS****01**</span><span class="sxs-lookup"><span data-stu-id="e0e69-958">**Java system**: **SCS** instance number **01**</span></span>
  * <span data-ttu-id="e0e69-959">**Système ABAP+Java** : numéro d’instance **ASCS****00** et numéro d’instance **SCS****01**</span><span class="sxs-lookup"><span data-stu-id="e0e69-959">**ABAP+Java system**: **ASCS** instance number **00** and **SCS** instance number **01**</span></span>

  <span data-ttu-id="e0e69-960">chiffres de toouse instance autre que 00 pour hello ABAP ASCS, instance et 01 pour l’instance de Java SCS hello, vous devez commencer toochange hello de charge interne Azure par défaut d’équilibrage de règles, décrites dans [charge par défaut de modification hello ASCS/SCS règles pour l’équilibrage de charge interne Azure hello d’équilibrage][sap-ha-guide-8.9].</span><span class="sxs-lookup"><span data-stu-id="e0e69-960">toouse instance numbers other than 00 for hello ABAP ASCS instance and 01 for hello Java SCS instance, first you need toochange hello Azure internal load balancer default load balancing rules, described in [Change hello ASCS/SCS default load balancing rules for hello Azure internal load balancer][sap-ha-guide-8.9].</span></span>

<span data-ttu-id="e0e69-961">Hello suivants certaines tâches ne sont pas décrits dans la documentation d’installation SAP standard hello.</span><span class="sxs-lookup"><span data-stu-id="e0e69-961">hello next few tasks aren't described in hello standard SAP installation documentation.</span></span>

> [!NOTE]
> <span data-ttu-id="e0e69-962">Hello documentation d’installation SAP décrit comment tooinstall hello premier nœud de cluster ASCS/SCS.</span><span class="sxs-lookup"><span data-stu-id="e0e69-962">hello SAP installation documentation describes how tooinstall hello first ASCS/SCS cluster node.</span></span>
>
>

#### <span data-ttu-id="e0e69-963"><a name="e4caaab2-e90f-4f2c-bc84-2cd2e12a9556"></a>Modifier hello profil de SAP de l’instance ASCS/SCS hello</span><span class="sxs-lookup"><span data-stu-id="e0e69-963"><a name="e4caaab2-e90f-4f2c-bc84-2cd2e12a9556"></a> Modify hello SAP profile of hello ASCS/SCS instance</span></span>

<span data-ttu-id="e0e69-964">Vous devez tooadd un nouveau paramètre de profil.</span><span class="sxs-lookup"><span data-stu-id="e0e69-964">You need tooadd a new profile parameter.</span></span> <span data-ttu-id="e0e69-965">paramètre de profil Hello empêche des connexions entre les processus de travail SAP et le serveur de file d’attente hello de fermer lorsqu’elles sont inactives pendant trop longtemps.</span><span class="sxs-lookup"><span data-stu-id="e0e69-965">hello profile parameter prevents connections between SAP work processes and hello enqueue server from closing when they are idle for too long.</span></span> <span data-ttu-id="e0e69-966">Nous l’avons mentionné problème du scénario hello dans [ajouter des entrées de Registre sur les deux nœuds de cluster de l’instance de SAP ASCS/SCS hello][sap-ha-guide-8.11].</span><span class="sxs-lookup"><span data-stu-id="e0e69-966">We mentioned hello problem scenario in [Add registry entries on both cluster nodes of hello SAP ASCS/SCS instance][sap-ha-guide-8.11].</span></span> <span data-ttu-id="e0e69-967">Dans cette section, nous avons introduit également deux paramètres de connexion de TCP/IP base modifications toosome.</span><span class="sxs-lookup"><span data-stu-id="e0e69-967">In that section, we also introduced two changes toosome basic TCP/IP connection parameters.</span></span> <span data-ttu-id="e0e69-968">Dans un deuxième temps, vous devez tooset hello enqueue server toosend un `keep_alive` signal afin que les connexions hello n’atteint le seuil d’inactivité de l’équilibrage de charge interne Azure hello.</span><span class="sxs-lookup"><span data-stu-id="e0e69-968">In a second step, you need tooset hello enqueue server toosend a `keep_alive` signal so that hello connections don't hit hello Azure internal load balancer's idle threshold.</span></span>

<span data-ttu-id="e0e69-969">hello toomodify profil SAP d’instance ASCS/SCS hello :</span><span class="sxs-lookup"><span data-stu-id="e0e69-969">toomodify hello SAP profile of hello ASCS/SCS instance:</span></span>

1.  <span data-ttu-id="e0e69-970">Ajoutez cette toohello de paramètre de profil profil d’instance SAP ASCS/SCS :</span><span class="sxs-lookup"><span data-stu-id="e0e69-970">Add this profile parameter toohello SAP ASCS/SCS instance profile:</span></span>

  ```
  enque/encni/set_so_keepalive = true
  ```
  <span data-ttu-id="e0e69-971">Dans notre exemple, le chemin d’accès de hello est :</span><span class="sxs-lookup"><span data-stu-id="e0e69-971">In our example, hello path is:</span></span>

  `<ShareDisk>:\usr\sap\PR1\SYS\profile\PR1_ASCS00_pr1-ascs-sap`

  <span data-ttu-id="e0e69-972">Par exemple, profil d’instance SAP SCS toohello et chemin d’accès correspondant :</span><span class="sxs-lookup"><span data-stu-id="e0e69-972">For example, toohello SAP SCS instance profile and corresponding path:</span></span>

  `<ShareDisk>:\usr\sap\PR1\SYS\profile\PR1_SCS01_pr1-ascs-sap`

2.  <span data-ttu-id="e0e69-973">modifications de hello tooapply, redémarrez l’instance de ASCS SAP /SCS de hello.</span><span class="sxs-lookup"><span data-stu-id="e0e69-973">tooapply hello changes, restart hello SAP ASCS /SCS instance.</span></span>

#### <span data-ttu-id="e0e69-974"><a name="10822f4f-32e7-4871-b63a-9b86c76ce761"></a> Ajouter un port de sondage</span><span class="sxs-lookup"><span data-stu-id="e0e69-974"><a name="10822f4f-32e7-4871-b63a-9b86c76ce761"></a> Add a probe port</span></span>

<span data-ttu-id="e0e69-975">Utilisez le travail de configuration de l’équilibrage de charge interne hello sonde fonctionnalité toomake hello ensemble du cluster avec équilibrage de charge Azure.</span><span class="sxs-lookup"><span data-stu-id="e0e69-975">Use hello internal load balancer's probe functionality toomake hello entire cluster configuration work with Azure Load Balancer.</span></span> <span data-ttu-id="e0e69-976">équilibrage de charge interne Azure Hello distribue généralement hello entrants la charge de travail entre les participants machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="e0e69-976">hello Azure internal load balancer usually distributes hello incoming workload equally between participating virtual machines.</span></span> <span data-ttu-id="e0e69-977">Toutefois, cela ne fonctionne pas dans certaines configurations de cluster, car une seule instance est active.</span><span class="sxs-lookup"><span data-stu-id="e0e69-977">However, this won't work in some cluster configurations because only one instance is active.</span></span> <span data-ttu-id="e0e69-978">Bonjour autre instance est passive et ne peut pas accepter des charges de travail hello.</span><span class="sxs-lookup"><span data-stu-id="e0e69-978">hello other instance is passive and can’t accept any of hello workload.</span></span> <span data-ttu-id="e0e69-979">Une fonctionnalité de sonde est utile lors de la lui affecte équilibreur de charge interne Azure hello tooan uniquement les instances actives de travail.</span><span class="sxs-lookup"><span data-stu-id="e0e69-979">A probe functionality helps when hello Azure internal load balancer assigns work only tooan active instance.</span></span> <span data-ttu-id="e0e69-980">Avec la fonctionnalité de sonde hello, l’équilibreur de charge interne hello peut détecter les instances sont actifs et puis ciblent uniquement les instance hello avec une charge de travail hello.</span><span class="sxs-lookup"><span data-stu-id="e0e69-980">With hello probe functionality, hello internal load balancer can detect which instances are active, and then target only hello instance with hello workload.</span></span>

<span data-ttu-id="e0e69-981">tooadd un port de la sonde :</span><span class="sxs-lookup"><span data-stu-id="e0e69-981">tooadd a probe port:</span></span>

1.  <span data-ttu-id="e0e69-982">Vérifiez hello actuel **ProbePort** définition en exécutant hello suivant de commande PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e0e69-982">Check hello current **ProbePort** setting by running hello following PowerShell command.</span></span> <span data-ttu-id="e0e69-983">Exécuter à partir de dans une des machines virtuelles de hello dans la configuration de cluster hello.</span><span class="sxs-lookup"><span data-stu-id="e0e69-983">Execute it from within one of hello virtual machines in hello cluster configuration.</span></span>

  ```PowerShell
  $SAPSID = "PR1"     # SAP <SID>

  $SAPNetworkIPClusterName = "SAP $SAPSID IP"
  Get-ClusterResource $SAPNetworkIPClusterName | Get-ClusterParameter
  ```

2.  <span data-ttu-id="e0e69-984">Définissez un port de sondage.</span><span class="sxs-lookup"><span data-stu-id="e0e69-984">Define a probe port.</span></span> <span data-ttu-id="e0e69-985">numéro de port de sonde Hello par défaut est **0**.</span><span class="sxs-lookup"><span data-stu-id="e0e69-985">hello default probe port number is **0**.</span></span> <span data-ttu-id="e0e69-986">Dans notre exemple, nous utilisons le port de sondage **62000**.</span><span class="sxs-lookup"><span data-stu-id="e0e69-986">In our example, we use probe port **62000**.</span></span>

  ![Figure 58 : port de la sonde hello cluster configuration par défaut est 0][sap-ha-guide-figure-3048]

  <span data-ttu-id="e0e69-988">_**Figure 58 :** port de la sonde du cluster configuration de hello par défaut est 0_</span><span class="sxs-lookup"><span data-stu-id="e0e69-988">_**Figure 58:** hello default cluster configuration probe port is 0_</span></span>

  <span data-ttu-id="e0e69-989">numéro de port Hello est défini dans les modèles SAP Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="e0e69-989">hello port number is defined in SAP Azure Resource Manager templates.</span></span> <span data-ttu-id="e0e69-990">Vous pouvez affecter le numéro de port hello dans PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e0e69-990">You can assign hello port number in PowerShell.</span></span>

  <span data-ttu-id="e0e69-991">tooset une nouvelle valeur de ProbePort pour hello  **SAP <*SID*> IP ** ressource de cluster, exécutez hello suite du script PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e0e69-991">tooset a new ProbePort value for hello **SAP <*SID*> IP** cluster resource, run hello following PowerShell script.</span></span> <span data-ttu-id="e0e69-992">Mettre à jour les variables PowerShell hello pour votre environnement.</span><span class="sxs-lookup"><span data-stu-id="e0e69-992">Update hello PowerShell variables for your environment.</span></span> <span data-ttu-id="e0e69-993">Après l’exécution du script de hello, vous serez invité à toorestart hello SAP groupe tooactivate hello les modifications de cluster.</span><span class="sxs-lookup"><span data-stu-id="e0e69-993">After hello script runs, you'll be prompted toorestart hello SAP cluster group tooactivate hello changes.</span></span>

  ```PowerShell
  $SAPSID = "PR1"      # SAP <SID>
  $ProbePort = 62000   # ProbePort of hello Azure Internal Load Balancer

  Clear-Host
  $SAPClusterRoleName = "SAP $SAPSID"
  $SAPIPresourceName = "SAP $SAPSID IP"
  $SAPIPResourceClusterParameters =  Get-ClusterResource $SAPIPresourceName | Get-ClusterParameter
  $IPAddress = ($SAPIPResourceClusterParameters | Where-Object {$_.Name -eq "Address" }).Value
  $NetworkName = ($SAPIPResourceClusterParameters | Where-Object {$_.Name -eq "Network" }).Value
  $SubnetMask = ($SAPIPResourceClusterParameters | Where-Object {$_.Name -eq "SubnetMask" }).Value
  $OverrideAddressMatch = ($SAPIPResourceClusterParameters | Where-Object {$_.Name -eq "OverrideAddressMatch" }).Value
  $EnableDhcp = ($SAPIPResourceClusterParameters | Where-Object {$_.Name -eq "EnableDhcp" }).Value
  $OldProbePort = ($SAPIPResourceClusterParameters | Where-Object {$_.Name -eq "ProbePort" }).Value

  $var = Get-ClusterResource | Where-Object {  $_.name -eq $SAPIPresourceName  }

  Write-Host "Current configuration parameters for SAP IP cluster resource '$SAPIPresourceName' are:" -ForegroundColor Cyan
  Get-ClusterResource -Name $SAPIPresourceName | Get-ClusterParameter

  Write-Host
  Write-Host "Current probe port property of hello SAP cluster resource '$SAPIPresourceName' is '$OldProbePort'." -ForegroundColor Cyan
  Write-Host
  Write-Host "Setting hello new probe port property of hello SAP cluster resource '$SAPIPresourceName' too'$ProbePort' ..." -ForegroundColor Cyan
  Write-Host

  $var | Set-ClusterParameter -Multiple @{"Address"=$IPAddress;"ProbePort"=$ProbePort;"Subnetmask"=$SubnetMask;"Network"=$NetworkName;"OverrideAddressMatch"=$OverrideAddressMatch;"EnableDhcp"=$EnableDhcp}

  Write-Host

  $ActivateChanges = Read-Host "Do you want tootake restart SAP cluster role '$SAPClusterRoleName', tooactivate hello changes (yes/no)?"

  if($ActivateChanges -eq "yes"){
  Write-Host
  Write-Host "Activating changes..." -ForegroundColor Cyan

  Write-Host
  write-host "Taking SAP cluster IP resource '$SAPIPresourceName' offline ..." -ForegroundColor Cyan
  Stop-ClusterResource -Name $SAPIPresourceName
  sleep 5

  Write-Host "Starting SAP cluster role '$SAPClusterRoleName' ..." -ForegroundColor Cyan
  Start-ClusterGroup -Name $SAPClusterRoleName

  Write-Host "New ProbePort parameter is active." -ForegroundColor Green
  Write-Host

  Write-Host "New configuration parameters for SAP IP cluster resource '$SAPIPresourceName':" -ForegroundColor Cyan
  Write-Host
  Get-ClusterResource -Name $SAPIPresourceName | Get-ClusterParameter
  }else
  {
  Write-Host "Changes are not activated."
  }
  ```

  <span data-ttu-id="e0e69-994">Après avoir mis hello  **SAP <*SID*> ** rôle en ligne du cluster, vérifiez que **ProbePort** a la valeur toohello nouvelle valeur.</span><span class="sxs-lookup"><span data-stu-id="e0e69-994">After you bring hello **SAP <*SID*>** cluster role online, verify that **ProbePort** is set toohello new value.</span></span>

  ```PowerShell
  $SAPSID = "PR1"     # SAP <SID>

  $SAPNetworkIPClusterName = "SAP $SAPSID IP"
  Get-ClusterResource $SAPNetworkIPClusterName | Get-ClusterParameter

  ```

  ![Figure 59 : Port de la sonde hello cluster après avoir défini la nouvelle valeur de hello][sap-ha-guide-figure-3049]

  <span data-ttu-id="e0e69-996">_**Figure 59 :** sonde de port de cluster hello après avoir défini la nouvelle valeur de hello_</span><span class="sxs-lookup"><span data-stu-id="e0e69-996">_**Figure 59:** Probe hello cluster port after you set hello new value_</span></span>

#### <span data-ttu-id="e0e69-997"><a name="4498c707-86c0-4cde-9c69-058a7ab8c3ac"></a>Ouvrez le port de sondage du pare-feu Windows hello</span><span class="sxs-lookup"><span data-stu-id="e0e69-997"><a name="4498c707-86c0-4cde-9c69-058a7ab8c3ac"></a> Open hello Windows firewall probe port</span></span>

<span data-ttu-id="e0e69-998">Vous devez tooopen un port de sondage du pare-feu Windows sur les deux nœuds de cluster.</span><span class="sxs-lookup"><span data-stu-id="e0e69-998">You need tooopen a Windows firewall probe port on both cluster nodes.</span></span> <span data-ttu-id="e0e69-999">Utilisez hello suivant script tooopen un port de sondage du pare-feu Windows.</span><span class="sxs-lookup"><span data-stu-id="e0e69-999">Use hello following script tooopen a Windows firewall probe port.</span></span> <span data-ttu-id="e0e69-1000">Mettre à jour les variables PowerShell hello pour votre environnement.</span><span class="sxs-lookup"><span data-stu-id="e0e69-1000">Update hello PowerShell variables for your environment.</span></span>

  ```PowerShell
  $ProbePort = 62000   # ProbePort of hello Azure Internal Load Balancer

  New-NetFirewallRule -Name AzureProbePort -DisplayName "Rule for Azure Probe Port" -Direction Inbound -Action Allow -Protocol TCP -LocalPort $ProbePort
  ```

<span data-ttu-id="e0e69-1001">Hello **ProbePort** est défini trop**62000**.</span><span class="sxs-lookup"><span data-stu-id="e0e69-1001">hello **ProbePort** is set too**62000**.</span></span> <span data-ttu-id="e0e69-1002">Maintenant vous pourrez accéder au partage de fichiers hello  **\\\ascsha-clsap\sapmnt** d’autres hôtes, notamment du **ascsha-DBA**.</span><span class="sxs-lookup"><span data-stu-id="e0e69-1002">Now you can access hello file share **\\\ascsha-clsap\sapmnt** from other hosts, such as from **ascsha-dbas**.</span></span>

### <span data-ttu-id="e0e69-1003"><a name="85d78414-b21d-4097-92b6-34d8bcb724b7"></a>Installer l’instance de base de données hello</span><span class="sxs-lookup"><span data-stu-id="e0e69-1003"><a name="85d78414-b21d-4097-92b6-34d8bcb724b7"></a> Install hello database instance</span></span>

<span data-ttu-id="e0e69-1004">base de données tooinstall hello d’une instance, suivez hello est décrite dans la documentation d’installation SAP de hello.</span><span class="sxs-lookup"><span data-stu-id="e0e69-1004">tooinstall hello database instance, follow hello process described in hello SAP installation documentation.</span></span>

### <span data-ttu-id="e0e69-1005"><a name="8a276e16-f507-4071-b829-cdc0a4d36748"></a>Installer le second nœud de cluster hello</span><span class="sxs-lookup"><span data-stu-id="e0e69-1005"><a name="8a276e16-f507-4071-b829-cdc0a4d36748"></a> Install hello second cluster node</span></span>

<span data-ttu-id="e0e69-1006">tooinstall hello deuxième cluster, suivez les étapes hello Bonjour guide d’installation SAP.</span><span class="sxs-lookup"><span data-stu-id="e0e69-1006">tooinstall hello second cluster, follow hello steps in hello SAP installation guide.</span></span>

### <span data-ttu-id="e0e69-1007"><a name="094bc895-31d4-4471-91cc-1513b64e406a"></a>Modifier le type de démarrage hello d’instance de service SAP ERS Windows hello</span><span class="sxs-lookup"><span data-stu-id="e0e69-1007"><a name="094bc895-31d4-4471-91cc-1513b64e406a"></a> Change hello start type of hello SAP ERS Windows service instance</span></span>

<span data-ttu-id="e0e69-1008">Modifier le type de démarrage de hello Hello service SAP ERS Windows trop**automatique (début différé)** sur les deux nœuds de cluster.</span><span class="sxs-lookup"><span data-stu-id="e0e69-1008">Change hello start type of hello SAP ERS Windows service too**Automatic (Delayed Start)** on both cluster nodes.</span></span>

![Figure 60 : Modifier le type de service hello pour hello SAP ERS instance toodelayed automatique][sap-ha-guide-figure-3050]

<span data-ttu-id="e0e69-1010">_**Figure 60 :** modifier le type de service hello pour hello SAP ERS instance toodelayed automatique_</span><span class="sxs-lookup"><span data-stu-id="e0e69-1010">_**Figure 60:** Change hello service type for hello SAP ERS instance toodelayed automatic_</span></span>

### <span data-ttu-id="e0e69-1011"><a name="2477e58f-c5a7-4a5d-9ae3-7b91022cafb5"></a>Installer hello principal serveur d’applications SAP</span><span class="sxs-lookup"><span data-stu-id="e0e69-1011"><a name="2477e58f-c5a7-4a5d-9ae3-7b91022cafb5"></a> Install hello SAP Primary Application Server</span></span>

<span data-ttu-id="e0e69-1012">Installer l’instance de serveur d’Application principal (PAS) hello <*SID*> - di - 0 sur l’ordinateur virtuel hello que vous avez désigné toohost hello PAS.</span><span class="sxs-lookup"><span data-stu-id="e0e69-1012">Install hello Primary Application Server (PAS) instance <*SID*>-di-0 on hello virtual machine that you've designated toohost hello PAS.</span></span> <span data-ttu-id="e0e69-1013">Il n’existe aucune dépendance sur des paramètres spécifiques à Azure ou DataKeeper.</span><span class="sxs-lookup"><span data-stu-id="e0e69-1013">There are no dependencies on Azure or DataKeeper-specific settings.</span></span>

### <span data-ttu-id="e0e69-1014"><a name="0ba4a6c1-cc37-4bcf-a8dc-025de4263772"></a>Installer hello serveur d’applications SAP supplémentaires</span><span class="sxs-lookup"><span data-stu-id="e0e69-1014"><a name="0ba4a6c1-cc37-4bcf-a8dc-025de4263772"></a> Install hello SAP Additional Application Server</span></span>

<span data-ttu-id="e0e69-1015">Installez une SAP supplémentaires Application serveur (agents) sur tous les ordinateurs virtuels de hello que vous avez désigné toohost une instance de serveur d’applications SAP.</span><span class="sxs-lookup"><span data-stu-id="e0e69-1015">Install an SAP Additional Application Server (AAS) on all hello virtual machines that you've designated toohost an SAP Application Server instance.</span></span> <span data-ttu-id="e0e69-1016">Par exemple, sur <*SID*> - di - 1 trop <*SID*> - di -&lt;n&gt;.</span><span class="sxs-lookup"><span data-stu-id="e0e69-1016">For example, on <*SID*>-di-1 too<*SID*>-di-&lt;n&gt;.</span></span>

> [!NOTE]
> <span data-ttu-id="e0e69-1017">Cela termine installation hello d’un système SAP NetWeaver de haute disponibilité.</span><span class="sxs-lookup"><span data-stu-id="e0e69-1017">This finishes hello installation of a high-availability SAP NetWeaver system.</span></span> <span data-ttu-id="e0e69-1018">Procédez maintenant à un test de basculement.</span><span class="sxs-lookup"><span data-stu-id="e0e69-1018">Next, proceed with failover testing.</span></span>
>


## <span data-ttu-id="e0e69-1019"><a name="18aa2b9d-92d2-4c0e-8ddd-5acaabda99e9"></a>Tester une instance SAP ASCS/SCS hello ou la réplication SIOS</span><span class="sxs-lookup"><span data-stu-id="e0e69-1019"><a name="18aa2b9d-92d2-4c0e-8ddd-5acaabda99e9"></a> Test hello SAP ASCS/SCS instance failover and SIOS replication</span></span>
<span data-ttu-id="e0e69-1020">Il est facile tootest et surveiller une instance SAP ASCS/SCS ou réplication de disque SIOS en utilisant le Gestionnaire du Cluster de basculement et l’outil de Configuration et la gestion de DataKeeper de SIOS hello.</span><span class="sxs-lookup"><span data-stu-id="e0e69-1020">It's easy tootest and monitor an SAP ASCS/SCS instance failover and SIOS disk replication by using Failover Cluster Manager and hello SIOS DataKeeper Management and Configuration tool.</span></span>

### <span data-ttu-id="e0e69-1021"><a name="65fdef0f-9f94-41f9-b314-ea45bbfea445"></a> L’instance SAP ASCS/SCS s’exécute sur le nœud de cluster A</span><span class="sxs-lookup"><span data-stu-id="e0e69-1021"><a name="65fdef0f-9f94-41f9-b314-ea45bbfea445"></a> SAP ASCS/SCS instance is running on cluster node A</span></span>

<span data-ttu-id="e0e69-1022">Hello **SAP PR1** groupe du cluster est en cours d’exécution sur le nœud de cluster A. Par exemple, sur **pr1-ascs-0**.</span><span class="sxs-lookup"><span data-stu-id="e0e69-1022">hello **SAP PR1** cluster group is running on cluster node A. For example, on **pr1-ascs-0**.</span></span> <span data-ttu-id="e0e69-1023">Affecter le lecteur de disque hello partagé S, qui fait partie de hello **SAP PR1** groupe du cluster, et l’instance ASCS/SCS hello utilise, toocluster nœud A.</span><span class="sxs-lookup"><span data-stu-id="e0e69-1023">Assign hello shared disk drive S, which is part of hello **SAP PR1** cluster group, and which hello ASCS/SCS instance uses, toocluster node A.</span></span>

![Figure 61 : Gestionnaire du Cluster de basculement : groupe de clusters SAP < SID > hello est en cours d’exécution sur le nœud de cluster A][sap-ha-guide-figure-5000]

<span data-ttu-id="e0e69-1025">_**Figure 61 :** Gestionnaire du Cluster de basculement : hello SAP <*SID*> groupe de cluster est en cours d’exécution sur le nœud de cluster A_</span><span class="sxs-lookup"><span data-stu-id="e0e69-1025">_**Figure 61:** Failover Cluster Manager: hello SAP <*SID*> cluster group is running on cluster node A_</span></span>

<span data-ttu-id="e0e69-1026">Dans hello SIOS DataKeeper gestion et l’outil de Configuration, vous pouvez voir ce disque partagé hello les données sont répliquées de façon synchrone à partir du lecteur de volume hello source S sur le nœud de cluster toohello lecteur cible de volume S sur le nœud de cluster B. Par exemple, elle est répliquée à partir de **pr1-ascs-0 [10.0.0.40]** trop**pr1-ascs-1 [de 10.0.0.41]**.</span><span class="sxs-lookup"><span data-stu-id="e0e69-1026">In hello SIOS DataKeeper Management and Configuration tool, you can see that hello shared disk data is synchronously replicated from hello source volume drive S on cluster node A toohello target volume drive S on cluster node B. For example, it's replicated from **pr1-ascs-0 [10.0.0.40]** too**pr1-ascs-1 [10.0.0.41]**.</span></span>

![Figure 62 : Dans SIOS DataKeeper, répliquer volume local de hello à partir du nœud de cluster nœud toocluster B][sap-ha-guide-figure-5001]

<span data-ttu-id="e0e69-1028">_**Figure 62 :** dans SIOS DataKeeper, répliquer le volume local de hello à partir du nœud de cluster nœud toocluster B_</span><span class="sxs-lookup"><span data-stu-id="e0e69-1028">_**Figure 62:** In SIOS DataKeeper, replicate hello local volume from cluster node A toocluster node B_</span></span>

### <span data-ttu-id="e0e69-1029"><a name="5e959fa9-8fcd-49e5-a12c-37f6ba07b916"></a>Basculement de nœud A toonode B</span><span class="sxs-lookup"><span data-stu-id="e0e69-1029"><a name="5e959fa9-8fcd-49e5-a12c-37f6ba07b916"></a> Failover from node A toonode B</span></span>

1.  <span data-ttu-id="e0e69-1030">Choisissez une de ces options tooinitiate un basculement de hello SAP <*SID*> groupe de clusters à partir du cluster A toocluster nœud b :</span><span class="sxs-lookup"><span data-stu-id="e0e69-1030">Choose one of these options tooinitiate a failover of hello SAP <*SID*> cluster group from cluster node A toocluster node B:</span></span>
  - <span data-ttu-id="e0e69-1031">Utiliser le Gestionnaire du cluster de basculement</span><span class="sxs-lookup"><span data-stu-id="e0e69-1031">Use Failover Cluster Manager</span></span>  
  - <span data-ttu-id="e0e69-1032">Utiliser l’applet de commande PowerShell de cluster de basculement</span><span class="sxs-lookup"><span data-stu-id="e0e69-1032">Use Failover Cluster PowerShell</span></span>

  ```PowerShell
  $SAPSID = "PR1"     # SAP <SID>

  $SAPClusterGroup = "SAP $SAPSID"
  Move-ClusterGroup -Name $SAPClusterGroup

  ```
2.  <span data-ttu-id="e0e69-1033">Redémarrez le nœud de cluster A hello Windows système d’exploitation invité (cette commande lance un basculement automatique de hello SAP <*SID*> groupe de clusters à partir du nœud A toonode B).</span><span class="sxs-lookup"><span data-stu-id="e0e69-1033">Restart cluster node A within hello Windows guest operating system (this initiates an automatic failover of hello SAP <*SID*> cluster group from node A toonode B).</span></span>  
3.  <span data-ttu-id="e0e69-1034">Redémarrage d’un nœud de cluster à partir de hello portail Azure (cette commande lance un basculement automatique de hello SAP <*SID*> groupe de clusters à partir du nœud A toonode B).</span><span class="sxs-lookup"><span data-stu-id="e0e69-1034">Restart cluster node A from hello Azure portal (this initiates an automatic failover of hello SAP <*SID*> cluster group from node A toonode B).</span></span>  
4.  <span data-ttu-id="e0e69-1035">Redémarrage d’un nœud de cluster à l’aide de Azure PowerShell (cette commande lance un basculement automatique de hello SAP <*SID*> groupe de clusters à partir du nœud A toonode B).</span><span class="sxs-lookup"><span data-stu-id="e0e69-1035">Restart cluster node A by using Azure PowerShell (this initiates an automatic failover of hello SAP <*SID*> cluster group from node A toonode B).</span></span>

  <span data-ttu-id="e0e69-1036">Après le basculement, hello SAP <*SID*> groupe de cluster est en cours d’exécution sur le nœud de cluster B. Par exemple, il est en cours d’exécution **pr1-ascs-1**.</span><span class="sxs-lookup"><span data-stu-id="e0e69-1036">After failover, hello SAP <*SID*> cluster group is running on cluster node B. For example, it's running on **pr1-ascs-1**.</span></span>

  ![Figure 63 : Dans le Gestionnaire de Cluster de basculement, groupe de clusters SAP < SID > hello est en cours d’exécution sur le nœud de cluster B][sap-ha-guide-figure-5002]

  <span data-ttu-id="e0e69-1038">_**Figure 63**: basculement Gestionnaire du Cluster de hello SAP <*SID*> groupe de cluster est en cours d’exécution sur le nœud de cluster B_</span><span class="sxs-lookup"><span data-stu-id="e0e69-1038">_**Figure 63**: In Failover Cluster Manager, hello SAP <*SID*> cluster group is running on cluster node B_</span></span>

  <span data-ttu-id="e0e69-1039">Hello disque partagé est maintenant monté sur un cluster de nœud B. SIOS DataKeeper réplique des données à partir du lecteur de volume source S sur le cluster le nœud B tootarget volume lecteur S sur le nœud de cluster A. Par exemple, il se réplique à partir de **pr1-ascs-1 [de 10.0.0.41]** trop**pr1-ascs-0 [10.0.0.40]**.</span><span class="sxs-lookup"><span data-stu-id="e0e69-1039">hello shared disk is now mounted on cluster node B. SIOS DataKeeper is replicating data from source volume drive S on cluster node B tootarget volume drive S on cluster node A. For example, it's replicating from **pr1-ascs-1 [10.0.0.41]** too**pr1-ascs-0 [10.0.0.40]**.</span></span>

  ![Figure 64 : SIOS DataKeeper réplique le volume de local hello de cluster B toocluster nœud A][sap-ha-guide-figure-5003]

  <span data-ttu-id="e0e69-1041">_**Figure 64 :** SIOS DataKeeper réplique le volume de local hello du nœud de toocluster B de nœud de cluster A_</span><span class="sxs-lookup"><span data-stu-id="e0e69-1041">_**Figure 64:** SIOS DataKeeper replicates hello local volume from cluster node B toocluster node A_</span></span>
