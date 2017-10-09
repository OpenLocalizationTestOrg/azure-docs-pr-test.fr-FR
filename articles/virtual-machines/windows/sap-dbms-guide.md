---
title: "aaaSAP NetWeaver sur machines virtuelles Azure – Guide de déploiement de système SGBD | Documents Microsoft"
description: "SAP NetWeaver sur machines virtuelles Azure – Guide de déploiement SGBD"
services: virtual-machines-windows,virtual-network,storage
documentationcenter: 
author: MSSedusch
manager: timlt
editor: 
tags: azure-resource-manager
keywords: 
ms.assetid: e0e05b5e-47aa-4c1e-bf83-0d62ee8f614e
ms.service: virtual-machines-windows
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 11/08/2016
ms.author: sedusch
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: a56b8f6b3b26fa10e01a25a251a3e4a7bfc77e2b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="sap-netweaver-on-azure-windows-virtual-machines-vms--dbms-deployment-guide"></a>SAP NetWeaver sur machines virtuelles Azure Windows – Guide de déploiement SGBD
[767598 ]:https://launchpad.support.sap.com/#/notes/767598
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

[azure-cli]:../../cli-install-nodejs.md
[azure-portal]:https://portal.azure.com
[azure-ps]:/powershell/azureps-cmdlets-docs
[azure-quickstart-templates-github]:https://github.com/Azure/azure-quickstart-templates
[azure-script-ps]:https://go.microsoft.com/fwlink/p/?LinkID=395017
[azure-subscription-service-limits]:../../azure-subscription-service-limits.md
[azure-subscription-service-limits-subscription]:../../azure-subscription-service-limits.md#subscription-limits

[dbms-guide]:sap-dbms-guide.md 
[dbms-guide-2.1]:#c7abf1f0-c927-4a7c-9c1d-c7b5b3b7212f 
[dbms-guide-2.2]:#c8e566f9-21b7-4457-9f7f-126036971a91 
[dbms-guide-2.3]:#10b041ef-c177-498a-93ed-44b3441ab152 
[dbms-guide-2]:#65fa79d6-a85f-47ee-890b-22e794f51a64 
[dbms-guide-3]:#871dfc27-e509-4222-9370-ab1de77021c3 
[dbms-guide-5.5.1]:#0fef0e79-d3fe-4ae2-85af-73666a6f7268 
[dbms-guide-5.5.2]:#f9071eff-9d72-4f47-9da4-1852d782087b 
[dbms-guide-5.6]:#1b353e38-21b3-4310-aeb6-a77e7c8e81c8 
[dbms-guide-5.8]:#9053f720-6f3b-4483-904d-15dc54141e30 
[dbms-guide-5]:#3264829e-075e-4d25-966e-a49dad878737 
[dbms-guide-8.4.1]:#b48cfe3b-48e9-4f5b-a783-1d29155bd573 
[dbms-guide-8.4.2]:#23c78d3b-ca5a-4e72-8a24-645d141a3f5d 
[dbms-guide-8.4.3]:#77cd2fbb-307e-4cbf-a65f-745553f72d2c 
[dbms-guide-8.4.4]:#f77c1436-9ad8-44fb-a331-8671342de818 
[dbms-guide-900-sap-cache-server-on-premises]:#642f746c-e4d4-489d-bf63-73e80177a0a8

[dbms-guide-figure-100]:./media/virtual-machines-shared-sap-dbms-guide/100_storage_account_types.png
[dbms-guide-figure-200]:./media/virtual-machines-shared-sap-dbms-guide/200-ha-set-for-dbms-ha.png
[dbms-guide-figure-300]:./media/virtual-machines-shared-sap-dbms-guide/300-reference-config-iaas.png
[dbms-guide-figure-400]:./media/virtual-machines-shared-sap-dbms-guide/400-sql-2012-backup-to-blob-storage.png
[dbms-guide-figure-500]:./media/virtual-machines-shared-sap-dbms-guide/500-sql-2012-backup-to-blob-storage-different-containers.png
[dbms-guide-figure-600]:./media/virtual-machines-shared-sap-dbms-guide/600-iaas-maxdb.png
[dbms-guide-figure-700]:./media/virtual-machines-shared-sap-dbms-guide/700-livecach-prod.png
[dbms-guide-figure-800]:./media/virtual-machines-shared-sap-dbms-guide/800-azure-vm-sap-content-server.png
[dbms-guide-figure-900]:./media/virtual-machines-shared-sap-dbms-guide/900-sap-cache-server-on-premises.png

[deployment-guide]:sap-deployment-guide.md 
[deployment-guide-2.2]:sap-deployment-guide.md#42ee2bdb-1efc-4ec7-ab31-fe4c22769b94 
[deployment-guide-3.1.2]:sap-deployment-guide.md#3688666f-281f-425b-a312-a77e7db2dfab 
[deployment-guide-3.2]:sap-deployment-guide.md#db477013-9060-4602-9ad4-b0316f8bb281 
[deployment-guide-3.3]:sap-deployment-guide.md#54a1fc6d-24fd-4feb-9c57-ac588a55dff2 
[deployment-guide-3.4]:sap-deployment-guide.md#a9a60133-a763-4de8-8986-ac0fa33aa8c1
[deployment-guide-3]:sap-deployment-guide.md#b3253ee3-d63b-4d74-a49b-185e76c4088e 
[deployment-guide-4.1]:sap-deployment-guide.md#604bcec2-8b6e-48d2-a944-61b0f5dee2f7 
[deployment-guide-4.2]:sap-deployment-guide.md#7ccf6c3e-97ae-4a7a-9c75-e82c37beb18e
[deployment-guide-4.3]:sap-deployment-guide.md#31d9ecd6-b136-4c73-b61e-da4a29bbc9cc 
[deployment-guide-4.4.2]:sap-deployment-guide.md#6889ff12-eaaf-4f3c-97e1-7c9edc7f7542 
[deployment-guide-4.4]:sap-deployment-guide.md#c7cbb0dc-52a4-49db-8e03-83e7edc2927d 
[deployment-guide-4.5.1]:sap-deployment-guide.md#987cf279-d713-4b4c-8143-6b11589bb9d4 
[deployment-guide-4.5.2]:sap-deployment-guide.md#408f3779-f422-4413-82f8-c57a23b4fc2f 
[deployment-guide-4.5]:sap-deployment-guide.md#d98edcd3-f2a1-49f7-b26a-07448ceb60ca 
[deployment-guide-5.1]:sap-deployment-guide.md#bb61ce92-8c5c-461f-8c53-39f5e5ed91f2 
[deployment-guide-5.2]:sap-deployment-guide.md#e2d592ff-b4ea-4a53-a91a-e5521edb6cd1 
[deployment-guide-5.3]:sap-deployment-guide.md#fe25a7da-4e4e-4388-8907-8abc2d33cfd8 

[deployment-guide-configure-monitoring-scenario-1]:sap-deployment-guide.md#ec323ac3-1de9-4c3a-b770-4ff701def65b 
[deployment-guide-configure-proxy]:sap-deployment-guide.md#baccae00-6f79-4307-ade4-40292ce4e02d 
[deployment-guide-figure-100]:./media/virtual-machines-shared-sap-deployment-guide/100-deploy-vm-image.png
[deployment-guide-figure-1000]:./media/virtual-machines-shared-sap-deployment-guide/1000-service-properties.png
[deployment-guide-figure-11]:sap-deployment-guide.md#figure-11
[deployment-guide-figure-1100]:./media/virtual-machines-shared-sap-deployment-guide/1100-azperflib.png
[deployment-guide-figure-1200]:./media/virtual-machines-shared-sap-deployment-guide/1200-cmd-test-login.png
[deployment-guide-figure-1300]:./media/virtual-machines-shared-sap-deployment-guide/1300-cmd-test-executed.png
[deployment-guide-figure-14]:sap-deployment-guide.md#figure-14
[deployment-guide-figure-1400]:./media/virtual-machines-shared-sap-deployment-guide/1400-azperflib-error-servicenotstarted.png
[deployment-guide-figure-300]:./media/virtual-machines-shared-sap-deployment-guide/300-deploy-private-image.png
[deployment-guide-figure-400]:./media/virtual-machines-shared-sap-deployment-guide/400-deploy-using-disk.png
[deployment-guide-figure-5]:sap-deployment-guide.md#figure-5
[deployment-guide-figure-50]:./media/virtual-machines-shared-sap-deployment-guide/50-forced-tunneling-suse.png
[deployment-guide-figure-500]:./media/virtual-machines-shared-sap-deployment-guide/500-install-powershell.png
[deployment-guide-figure-6]:sap-deployment-guide.md#figure-6
[deployment-guide-figure-600]:./media/virtual-machines-shared-sap-deployment-guide/600-powershell-version.png
[deployment-guide-figure-7]:sap-deployment-guide.md#figure-7
[deployment-guide-figure-700]:./media/virtual-machines-shared-sap-deployment-guide/700-install-powershell-installed.png
[deployment-guide-figure-760]:./media/virtual-machines-shared-sap-deployment-guide/760-azure-cli-version.png
[deployment-guide-figure-900]:./media/virtual-machines-shared-sap-deployment-guide/900-cmd-update-executed.png
[deployment-guide-figure-azure-cli-installed]:sap-deployment-guide.md#402488e5-f9bb-4b29-8063-1c5f52a892d0
[deployment-guide-figure-azure-cli-version]:sap-deployment-guide.md#0ad010e6-f9b5-4c21-9c09-bb2e5efb3fda
[deployment-guide-install-vm-agent-windows]:sap-deployment-guide.md#b2db5c9a-a076-42c6-9835-16945868e866
[deployment-guide-troubleshooting-chapter]:sap-deployment-guide.md#564adb4f-5c95-4041-9616-6635e83a810b 

[deploy-template-cli]:../../resource-group-template-deploy-cli.md
[deploy-template-portal]:../../resource-group-template-deploy-portal.md
[deploy-template-powershell]:../../resource-group-template-deploy.md

[dr-guide-classic]:http://go.microsoft.com/fwlink/?LinkID=521971

[getting-started]:sap-get-started.md
[getting-started-dbms]:sap-get-started.md#1343ffe1-8021-4ce6-a08d-3a1553a4db82
[getting-started-deployment]:sap-get-started.md#6aadadd2-76b5-46d8-8713-e8d63630e955
[getting-started-planning]:sap-get-started.md#3da0389e-708b-4e82-b2a2-e92f132df89c

[getting-started-windows-classic]:../virtual-machines-windows-classic-sap-get-started.md
[getting-started-windows-classic-dbms]:../virtual-machines-windows-classic-sap-get-started.md#c5b77a14-f6b4-44e9-acab-4d28ff72a930
[getting-started-windows-classic-deployment]:../virtual-machines-windows-classic-sap-get-started.md#f84ea6ce-bbb4-41f7-9965-34d31b0098ea
[getting-started-windows-classic-dr]:../virtual-machines-windows-classic-sap-get-started.md#cff10b4a-01a5-4dc3-94b6-afb8e55757d3
[getting-started-windows-classic-ha-sios]:../virtual-machines-windows-classic-sap-get-started.md#4bb7512c-0fa0-4227-9853-4004281b1037
[getting-started-windows-classic-planning]:../virtual-machines-windows-classic-sap-get-started.md#f2a5e9d8-49e4-419e-9900-af783173481c

[ha-guide-classic]:http://go.microsoft.com/fwlink/?LinkId=613056

[ha-guide]:sap-high-availability-guide.md

[install-extension-cli]:virtual-machines-linux-enable-aem.md

[Logo_Linux]:./media/virtual-machines-shared-sap-shared/Linux.png
[Logo_Windows]:./media/virtual-machines-shared-sap-shared/Windows.png

[msdn-set-azurermvmaemextension]:https://msdn.microsoft.com/library/azure/mt670598.aspx

[planning-guide]:sap-planning-guide.md  
[planning-guide-1.2]:sap-planning-guide.md#e55d1e22-c2c8-460b-9897-64622a34fdff 
[planning-guide-11]:sap-planning-guide.md#7cf991a1-badd-40a9-944e-7baae842a058 
[planning-guide-11.4.1]:sap-planning-guide.md#5d9d36f9-9058-435d-8367-5ad05f00de77 
[planning-guide-11.5]:sap-planning-guide.md#4e165b58-74ca-474f-a7f4-5e695a93204f 
[planning-guide-2.1]:sap-planning-guide.md#1625df66-4cc6-4d60-9202-de8a0b77f803 
[planning-guide-2.2]:sap-planning-guide.md#f5b3b18c-302c-4bd8-9ab2-c388f1ab3d10
[planning-guide-3.1]:sap-planning-guide.md#be80d1b9-a463-4845-bd35-f4cebdb5424a 
[planning-guide-3.2.1]:sap-planning-guide.md#df49dc09-141b-4f34-a4a2-990913b30358 
[planning-guide-3.2.2]:sap-planning-guide.md#fc1ac8b2-e54a-487c-8581-d3cc6625e560 
[planning-guide-3.2.3]:sap-planning-guide.md#18810088-f9be-4c97-958a-27996255c665 
[planning-guide-3.2]:sap-planning-guide.md#8d8ad4b8-6093-4b91-ac36-ea56d80dbf77 
[planning-guide-3.3.2]:sap-planning-guide.md#ff5ad0f9-f7f4-4022-9102-af07aef3bc92 
[planning-guide-5.1.1]:sap-planning-guide.md#4d175f1b-7353-4137-9d2f-817683c26e53 
[planning-guide-5.1.2]:sap-planning-guide.md#e18f7839-c0e2-4385-b1e6-4538453a285c 
[planning-guide-5.2.1]:sap-planning-guide.md#1b287330-944b-495d-9ea7-94b83aff73ef 
[planning-guide-5.2.2]:sap-planning-guide.md#57f32b1c-0cba-4e57-ab6e-c39fe22b6ec3 
[planning-guide-5.2]:sap-planning-guide.md#6ffb9f41-a292-40bf-9e70-8204448559e7 
[planning-guide-5.3.1]:sap-planning-guide.md#6e835de8-40b1-4b71-9f18-d45b20959b79 
[planning-guide-5.3.2]:sap-planning-guide.md#a43e40e6-1acc-4633-9816-8f095d5a7b6a 
[planning-guide-5.4.2]:sap-planning-guide.md#9789b076-2011-4afa-b2fe-b07a8aba58a1 
[planning-guide-5.5.1]:sap-planning-guide.md#4efec401-91e0-40c0-8e64-f2dceadff646 
[planning-guide-5.5.3]:sap-planning-guide.md#17e0d543-7e8c-4160-a7da-dd7117a1ad9d 
[planning-guide-7.1]:sap-planning-guide.md#3e9c3690-da67-421a-bc3f-12c520d99a30 
[planning-guide-7]:sap-planning-guide.md#96a77628-a05e-475d-9df3-fb82217e8f14 
[planning-guide-9.1]:sap-planning-guide.md#6f0a47f3-a289-4090-a053-2521618a28c3 
[planning-guide-azure-premium-storage]:sap-planning-guide.md#ff5ad0f9-f7f4-4022-9102-af07aef3bc92 

[planning-guide-figure-100]:./media/virtual-machines-shared-sap-planning-guide/100-single-vm-in-azure.png
[planning-guide-figure-1300]:./media/virtual-machines-shared-sap-planning-guide/1300-ref-config-iaas-for-sap.png
[planning-guide-figure-1400]:./media/virtual-machines-shared-sap-planning-guide/1400-attach-detach-disks.png
[planning-guide-figure-1600]:./media/virtual-machines-shared-sap-planning-guide/1600-firewall-port-rule.png
[planning-guide-figure-1700]:./media/virtual-machines-shared-sap-planning-guide/1700-single-vm-demo.png
[planning-guide-figure-1900]:./media/virtual-machines-shared-sap-planning-guide/1900-vm-set-vnet.png
[planning-guide-figure-200]:./media/virtual-machines-shared-sap-planning-guide/200-multiple-vms-in-azure.png
[planning-guide-figure-2100]:./media/virtual-machines-shared-sap-planning-guide/2100-s2s.png
[planning-guide-figure-2200]:./media/virtual-machines-shared-sap-planning-guide/2200-network-printing.png
[planning-guide-figure-2300]:./media/virtual-machines-shared-sap-planning-guide/2300-sapgui-stms.png
[planning-guide-figure-2400]:./media/virtual-machines-shared-sap-planning-guide/2400-vm-extension-overview.png
[planning-guide-figure-2500]:./media/virtual-machines-shared-sap-planning-guide/2500-vm-extension-details.png
[planning-guide-figure-2600]:./media/virtual-machines-shared-sap-planning-guide/2600-sap-router-connection.png
[planning-guide-figure-2700]:./media/virtual-machines-shared-sap-planning-guide/2700-exposed-sap-portal.png
[planning-guide-figure-2800]:./media/virtual-machines-shared-sap-planning-guide/2800-endpoint-config.png
[planning-guide-figure-2900]:./media/virtual-machines-shared-sap-planning-guide/2900-azure-ha-sap-ha.png
[planning-guide-figure-300]:./media/virtual-machines-shared-sap-planning-guide/300-vpn-s2s.png
[planning-guide-figure-3000]:./media/virtual-machines-shared-sap-planning-guide/3000-sap-ha-on-azure.png
[planning-guide-figure-3200]:./media/virtual-machines-shared-sap-planning-guide/3200-sap-ha-with-sql.png
[planning-guide-figure-400]:./media/virtual-machines-shared-sap-planning-guide/400-vm-services.png
[planning-guide-figure-600]:./media/virtual-machines-shared-sap-planning-guide/600-s2s-details.png
[planning-guide-figure-700]:./media/virtual-machines-shared-sap-planning-guide/700-decision-tree-deploy-to-azure.png
[planning-guide-figure-800]:./media/virtual-machines-shared-sap-planning-guide/800-portal-vm-overview.png
[planning-guide-microsoft-azure-networking]:sap-planning-guide.md#61678387-8868-435d-9f8c-450b2424f5bd 
[planning-guide-storage-microsoft-azure-storage-and-data-disks]:sap-planning-guide.md#a72afa26-4bf4-4a25-8cf7-855d6032157f 

[powershell-install-configure]:/powershell/azureps-cmdlets-docs
[resource-group-authoring-templates]:../../resource-group-authoring-templates.md
[resource-group-overview]:../../azure-resource-manager/resource-group-overview.md
[resource-groups-networking]:../../virtual-network/resource-groups-networking.md
[sap-pam]:https://support.sap.com/pam 
[sap-templates-2-tier-marketplace-image]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-2-tier-marketplace-image%2Fazuredeploy.json
[sap-templates-2-tier-os-disk]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-2-tier-user-disk%2Fazuredeploy.json
[sap-templates-2-tier-user-image]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-2-tier-user-image%2Fazuredeploy.json
[sap-templates-3-tier-marketplace-image]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image%2Fazuredeploy.json
[sap-templates-3-tier-user-image]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-user-image%2Fazuredeploy.json
[storage-azure-cli]:../../storage/storage-azure-cli.md
[storage-azure-cli-copy-blobs]:../../storage/storage-azure-cli.md#copy-blobs
[storage-introduction]:../../storage/storage-introduction.md
[storage-powershell-guide-full-copy-vhd]:../../storage/storage-powershell-guide-full.md#how-to-copy-blobs-from-one-storage-container-to-another
[storage-premium-storage-preview-portal]:../../storage/storage-premium-storage.md
[storage-redundancy]:../../storage/storage-redundancy.md
[storage-scalability-targets]:../../storage/storage-scalability-targets.md
[storage-use-azcopy]:../../storage/storage-use-azcopy.md
[template-201-vm-from-specialized-vhd]:https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-from-specialized-vhd
[templates-101-simple-windows-vm]:https://github.com/Azure/azure-quickstart-templates/tree/master/101-simple-windows-vm
[templates-101-vm-from-user-image]:https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-from-user-image
[virtual-machines-linux-attach-disk-portal]:../linux/attach-disk-portal.md
[virtual-machines-azure-resource-manager-architecture]:../../resource-manager-deployment-model.md
[virtual-machines-azurerm-versus-azuresm]:../../resource-manager-deployment-model.md
[virtual-machines-windows-classic-configure-oracle-data-guard]:../virtual-machines-windows-classic-configure-oracle-data-guard.md
[virtual-machines-linux-cli-deploy-templates]:../linux/cli-deploy-templates.md (Deploy and manage virtual machines by using Azure Resource Manager templates and hello Azure CLI)
[virtual-machines-deploy-rmtemplates-powershell]:../virtual-machines-windows-ps-manage.md (Manage virtual machines using Azure Resource Manager and PowerShell)
[virtual-machines-linux-agent-user-guide]:../linux/agent-user-guide.md
[virtual-machines-linux-agent-user-guide-command-line-options]:../linux/agent-user-guide.md#command-line-options
[virtual-machines-linux-capture-image]:../linux/capture-image.md
[virtual-machines-linux-capture-image-resource-manager]:../linux/capture-image.md
[virtual-machines-linux-capture-image-resource-manager-capture]:../linux/capture-image.md#step-2-capture-the-vm
[virtual-machines-linux-configure-lvm]:../linux/configure-lvm.md
[virtual-machines-linux-configure-raid]:../linux/configure-raid.md
[virtual-machines-linux-classic-create-upload-vhd-step-1]:../virtual-machines-linux-classic-create-upload-vhd.md#step-1-prepare-the-image-to-be-uploaded
[virtual-machines-linux-create-upload-vhd-suse]:../linux/suse-create-upload-vhd.md
[virtual-machines-linux-redhat-create-upload-vhd]:../linux/redhat-create-upload-vhd.md
[virtual-machines-linux-how-to-attach-disk]:../linux/add-disk.md
[virtual-machines-linux-how-to-attach-disk-how-to-initialize-a-new-data-disk-in-linux]:../linux/add-disk.md#connect-to-the-linux-vm-to-mount-the-new-disk
[virtual-machines-linux-tutorial]:../linux/quick-create-cli.md
[virtual-machines-linux-update-agent]:../linux/update-agent.md
[virtual-machines-manage-availability]:../virtual-machines-windows-manage-availability.md
[virtual-machines-ps-create-preconfigure-windows-resource-manager-vms]:../virtual-machines-windows-ps-create.md
[virtual-machines-sizes]:sizes.md
[virtual-machines-windows-classic-ps-sql-alwayson-availability-groups]:classic/ps-sql-alwayson-availability-groups.md
[virtual-machines-windows-classic-ps-sql-int-listener]:classic/ps-sql-int-listener.md
[virtual-machines-sql-server-high-availability-and-disaster-recovery-solutions]:./sql/virtual-machines-windows-sql-high-availability-dr.md
[virtual-machines-sql-server-infrastructure-services]:./sql/virtual-machines-windows-sql-server-iaas-overview.md
[virtual-machines-sql-server-performance-best-practices]:./sql/virtual-machines-windows-sql-performance.md
[virtual-machines-upload-image-windows-resource-manager]:upload-image.md
[virtual-machines-windows-tutorial]:../virtual-machines-windows-hero-tutorial.md
[virtual-machines-workload-template-sql-alwayson]:https://azure.microsoft.com/documentation/templates/sql-server-2014-alwayson-dsc/
[virtual-network-deploy-multinic-arm-cli]:../../virtual-network/virtual-network-deploy-multinic-arm-cli.md
[virtual-network-deploy-multinic-arm-ps]:../../virtual-network/virtual-network-deploy-multinic-arm-ps.md
[virtual-network-deploy-multinic-arm-template]:../../virtual-network/virtual-network-deploy-multinic-arm-template.md
[virtual-networks-configure-vnet-to-vnet-connection]:../../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md
[virtual-networks-create-vnet-arm-pportal]:../../virtual-network/virtual-networks-create-vnet-arm-pportal.md
[virtual-networks-manage-dns-in-vnet]:../../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md
[virtual-networks-multiple-nics]:../../virtual-network/virtual-networks-multiple-nics.md
[virtual-networks-nsg]:../../virtual-network/virtual-networks-nsg.md
[virtual-networks-reserved-private-ip]:../../virtual-network/virtual-networks-static-private-ip-arm-ps.md
[virtual-networks-static-private-ip-arm-pportal]:../../virtual-network/virtual-networks-static-private-ip-arm-pportal.md
[virtual-networks-udr-overview]:../../virtual-network/virtual-networks-udr-overview.md
[vpn-gateway-about-vpn-devices]:../../vpn-gateway/vpn-gateway-about-vpn-devices.md
[vpn-gateway-create-site-to-site-rm-powershell]:../../vpn-gateway/vpn-gateway-create-site-to-site-rm-powershell.md
[vpn-gateway-cross-premises-options]:../../vpn-gateway/vpn-gateway-plan-design.md
[vpn-gateway-site-to-site-create]:../../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md
[vpn-gateway-vpn-faq]:../../vpn-gateway/vpn-gateway-vpn-faq.md
[xplat-cli]:../../cli-install-nodejs.md
[xplat-cli-azure-resource-manager]:../../xplat-cli-azure-resource-manager.md

Ce guide fait partie de la documentation hello sur l’implémentation et de déploiement de logiciels SAP hello sur Microsoft Azure. Avant de lire ce guide, lisez hello [Guide de planification et implémentation][planning-guide]. Ce document décrit le déploiement hello de différents systèmes de gestion de base de données relationnelle (SGBDR) et les produits connexes en association avec SAP sur Microsoft Azure des Machines virtuelles (VM) à l’aide de hello Infrastructure Azure comme des fonctionnalités de Service (IaaS).

Hello papier complète hello Documentation d’Installation SAP et les Notes SAP, qui représentent les ressources principales de hello pour les installations et les déploiements de logiciels SAP sur obtiennent des plateformes

## <a name="general-considerations"></a>Considérations d’ordre général
Ce chapitre présente les considérations générales concernant l’exécution de systèmes SGBD relationnelle SAP sur les machines virtuelles Azure. Il y a peu de références toospecific SGBD utilisés dans ce chapitre. À la place des systèmes SGBD hello spécifiques sont décrits dans ce document, après ce chapitre.

### <a name="definitions-upfront"></a>Préambule : définitions
Dans l’ensemble de documents de hello, nous allons utiliser hello dispositions suivantes :

* IaaS : Infrastructure as a Service.
* PaaS : Platform as a Service.
* SaaS : Software as a Service.
* Composant SAP : application SAP individuelle telle que ECC, BW, Solution Manager ou EP.  Les composants SAP peuvent être basés sur des technologies ABAP ou Java traditionnelles ou une application non basée sur NetWeaver telle que Business Objects.
* Environnement SAP : un ou plusieurs composants SAP regroupement logiquement tooperform une fonction d’entreprise telles que le développement, Choisissons, formation, récupération d’urgence ou de Production.
* Paysage SAP : Cela fait référence à toohello des ressources SAP ensemble dans un client paysage informatique. Hello paysage SAP comprend tous les environnements de production et de non-production.
* Système SAP : hello une combinaison de couche SGBD et de, par exemple un système de développement ERP SAP, système de test SAP BW, système de production CRM SAP, etc. la couche application. Dans Azure les déploiements, qu'il n’est pas pris en charge toodivide ces deux couches entre locaux et Azure. Cela signifie qu’un système SAP doit être déployé en local ou dans Azure. Toutefois, vous pouvez déployer hello différents systèmes d’un paysage SAP dans Azure ou localement. Par exemple, vous pourriez déployer des systèmes de développement et de test de CRM SAP dans Azure hello mais hello production CRM SAP/système sur site.
* Déploiement de cloud uniquement : un déploiement où hello abonnement Azure n’est pas connecté via un site à site ou ExpressRoute connexion toohello localement l’infrastructure du réseau. Dans la documentation Azure courante, ces types de déploiements sont également décrits comme des déploiements « cloud uniquement ». Ordinateurs virtuels déployés avec cette méthode sont accessibles via Internet de hello et points de terminaison Internet publics affectés toohello machines virtuelles Azure. Hello locale Active Directory (AD) et DNS n’est pas étendu tooAzure dans ces types de déploiement. Par conséquent, les machines virtuelles de hello ne font pas partie de hello locale Active Directory. Remarque : dans ce document, les déploiements cloud uniquement sont définis comme des paysages SAP complets exécutés uniquement dans Azure, sans extension du répertoire Active Directory ou de la résolution de noms des sites au cloud public. Les configurations uniquement dans le cloud ne sont pas pris en charge pour les systèmes SAP de production ou les configurations où SAP STMS ou autres ressources sur site doivent toobe utilisé entre les systèmes SAP hébergés sur Azure et aux ressources locales.
* Intersite : Décrit un scénario dans lequel les machines virtuelles sont déployée tooan abonnement Azure qui utilise le site à site, plusieurs site ou ExpressRoute la connectivité entre les centres de local hello et Azure. Dans la documentation Azure courante, ces types de déploiements sont également décrits comme des scénarios intersites. Hello connexion de hello fait tooextend domaines locaux, locale Active Directory et DNS sur site dans Azure. Hello local paysage est étendue toohello ressources Azure de l’abonnement de hello. Avoir cette extension, hello machines virtuelles peut être la partie du domaine local de hello. Les utilisateurs du domaine local de hello peuvent accéder aux serveurs de hello et exécuter des services sur ces machines virtuelles (comme les services SGBD). La communication et la résolution de noms entre les machines virtuelles déployées en local et les machines virtuelles déployées dans Azure est possible. Nous pensons que ce scénario le plus courant toobe hello pour le déploiement des ressources SAP sur Azure. Pour plus d’informations, consultez [cet][vpn-gateway-cross-premises-options] article et [celui-ci][vpn-gateway-site-to-site-create].

> [!NOTE]
> Les déploiements intersites de systèmes SAP dans lesquels des machines virtuelles Azure exécutant des systèmes SAP font partie d’un domaine local sont pris en charge pour les systèmes SAP de production. Les configurations entre différents locaux sont prises en charge pour le déploiement d’éléments ou de l’intégralité des paysages SAP dans Azure. Même en cours d’exécution paysage SAP complète de hello dans Azure requiert ayant ces machines virtuelles faisant partie d’un domaine local et des annonces. Dans les versions précédentes de la documentation de hello, nous avons parlé des scénarios hybrides, où le terme hello « Hybride » associé à des faits hello qu’il existe une connectivité intersite entre locaux et Azure. Dans ce cas « Hybride » également signifie que les machines virtuelles de hello dans Azure font partie de hello locale Active Directory.
>
>

Certaines documentations Microsoft décrivent les scénarios intersites de façon légèrement différente, en particulier pour les configurations haute disponibilité SGBD. Bonjour documents relatifs au cas de hello SAP, scénario de hello intersite simplement résume toohaving un site à site ou privé (ExpressRoute) connectivité et toohello fait que le paysage SAP de hello est distribué entre locaux et Azure.

### <a name="resources"></a>Ressources
Hello guides suivants sont disponibles pour la rubrique hello des déploiements SAP sur Azure :

* [SAP NetWeaver sur machines virtuelles Azure – Guide de planification et d’implémentation][planning-guide]
* [SAP NetWeaver sur machines virtuelles Azure – Guide de déploiement][deployment-guide]
* [SAP NetWeaver sur machines virtuelles Azure – Guide de déploiement SGBD (ce document)][dbms-guide]
* [SAP NetWeaver sur machines virtuelles Azure – Guide de déploiement haute disponibilité][ha-guide]

Hello suit les Notes SAP est rubrique toohello connexes de SAP sur Azure :

| Numéro de la note | Intitulé |
| --- | --- |
| [1928533] |Applications SAP sur Azure : produits et types de machines virtuelles pris en charge |
| [2015553] |SAP sur Microsoft Azure : configuration requise |
| [1999351] |Résolution des problèmes de surveillance Azure améliorée pour SAP |
| [2178632] |Métriques de surveillance clés pour SAP sur Microsoft Azure |
| [1409604] |Virtualisation sur Windows : surveillance améliorée |
| [2191498] |SAP sur Linux avec Azure : surveillance améliorée |
| [2039619] |Applications SAP sur Microsoft Azure à l’aide hello de base de données Oracle : prise en charge des produits et des Versions |
| [2233094] |DB6 : Exécution d’applications SAP sur Azure à l’aide d’IBM DB2 pour Linux, UNIX et Windows - Informations supplémentaires |
| [2243692] |Linux sur Microsoft Azure Virtual Machines (IaaS) : problèmes de licence SAP |
| [1984787] |SUSE LINUX Enterprise Server 12 : Notes d’installation |
| [2002167] |Red Hat Enterprise Linux 7.x : Installation et mise à niveau |

Lisez aussi hello [SCN Wiki](https://wiki.scn.sap.com/wiki/display/HOME/SAPonLinuxNotes) qui contient toutes les Notes SAP pour Linux.

Vous devez posséder une connaissance de travail sur hello Architecture Microsoft Azure et comment les Machines virtuelles Microsoft Azure sont déployé et géré. Pour plus d’informations, consultez la page <https://azure.microsoft.com/documentation/>

> [!NOTE]
> Nous sommes **pas** traitant la plateforme Microsoft Azure comme un offres de Service (PaaS) de hello plateforme Microsoft Azure. Ce document est sur l’exécution d’un système de gestion de base de données (SGBD) dans Microsoft Azure Virtual Machines (IaaS) tout comme vous exécuteriez hello SGBD dans votre environnement local. Les capacités et fonctionnalités de base de données de ces deux services sont très différentes et ne doivent pas être confondues. Voir aussi : <https://azure.microsoft.com/services/sql-database/>
>
>

Étant donné que nous traiterons IaaS, en général hello Windows, Linux et SGBD l’installation et la configuration sont essentiellement hello identique à n’importe quel ordinateur virtuel ou récupération complète vous devez installer localement. Cependant, les décisions en matière d’implémentation de la gestion de l’architecture et des systèmes diffèrent sur certains points. Hello ce document vise tooexplain hello architecturaux et système de gestion des différences spécifiques que vous devez être préparé pour lors de l’utilisation d’IaaS.

En général, hello des zones globales ce livre blanc décrira les différences sont :

* Planification hello VM/VHD mise en forme de tooensure de systèmes SAP ont la disposition du fichier de données approprié hello et pouvez obtenir suffisamment d’IOPS pour votre charge de travail.
* Considérations relatives à la mise en réseau lors de l’utilisation de l’IaaS.
* Toouse de fonctionnalités de base de données spécifique dans la disposition de base de données de commande toooptimize hello.
* Considérations relatives à la sauvegarde et à la restauration de l’IaaS.
* Utilisation de différents types d’images pour le déploiement.
* Haute disponibilité dans Azure IaaS.

## <a name="65fa79d6-a85f-47ee-890b-22e794f51a64"></a>Structure d’un déploiement SGBDR
Dans l’ordre, suivez ce chapitre, il est nécessaire toounderstand qui est présenté dans [cela] [ deployment-guide-3] chapitre Hello [Guide de déploiement][deployment-guide]. Connaissance hello différents pour les séries de machines virtuelles et leurs différences et les différences entre Azure Standard et Premium Storage doivent être compris et connus avant de lire ce chapitre.

Jusqu'à mars 2015, disques durs virtuels de Azure qui contient un système d’exploitation ont été limités too127 go. Cette limitation a été levée en mars 2015 (pour plus d’informations, voir <https://azure.microsoft.com/blog/2015/03/25/azure-vm-os-drive-limit-octupled/>). À partir de là, sur les disques durs virtuels contenant système d’exploitation de hello peut avoir hello même taille comme n’importe quel autre disque dur virtuel. Toutefois, nous préférons toujours une structure de déploiement où hello système d’exploitation, SGBD et les binaires SAP finale sont distincts des fichiers de base de données hello de. Par conséquent, nous pensons que les systèmes SAP dans Azure Virtual Machines en cours d’exécution aura hello base virtuelle (ou VHD) installé avec le système d’exploitation de hello, base de données Gestion exécutables du système et les exécutables SAP. Hello données SGBD et les fichiers journaux seront stockées dans le stockage Azure (Standard ou Premium Storage) dans des fichiers VHD séparés et attachés en tant qu’image de système d’exploitation Azure d’origine disques logiques toohello machine virtuelle.

Dépendent de l’exploitant il Azure Standard ou Premium Storage (par exemple, en utilisant hello série DS ou machines virtuelles de série GS) sont les autres quotas dans Azure qui sont expliqués [ici][virtual-machines-sizes]. Lorsque vous planifiez vos disques durs virtuels de Azure, vous devez toofind hello meilleur compromis entre les quotas de hello pour les éléments suivants de hello :

* nombre de Hello des fichiers de données.
* nombre de Hello de disques durs virtuels qui contiennent les fichiers hello.
* quotas d’IOPS Hello d’un VHD.
* débit de données Hello par disque dur virtuel.
* nombre de Hello de VHD supplémentaires possibles par taille de machine virtuelle.
* Hello globale du débit de stockage une machine virtuelle peut fournir.

Azure applique un quota d’E/S par seconde par lecteur de disque dur virtuel. Ces quotas sont différents pour les disques durs virtuels selon qu’ils sont hébergés sur le stockage Azure Standard ou Premium Storage. Les latences d’e/s sera également très différentes entre deux types de stockage hello avec le stockage Premium remise facteurs meilleurs temps de latence d’e/s. Chacun des types de machine virtuelle hello ont un nombre limité de disques durs virtuels que vous êtes en mesure de tooattach. Une autre restriction concerne le fait que seuls certains types de machines virtuelles peuvent tirer parti d’Azure Premium Storage. Cela signifie que la décision de hello pour un certain type de machine virtuelle ne peut pas uniquement déterminée par les hello du processeur et les besoins en mémoire, mais aussi par hello IOPS, exigences de débit de latence et de disque qui généralement à l’échelle avec un nombre de hello de disques durs virtuels ou hello du type de disque de stockage Premium. En particulier avec un stockage Premium taille hello d’un disque dur virtuel peut également être dicté par hello IOPS et débit nécessitant toobe atteint par chaque disque dur virtuel.

faits Hello hello globale taux d’IOPS, nombre de hello de disques durs virtuels montés, et hello taille de machine virtuelle sont liés entre eux, de hello peut entraîner une configuration Azure de toobe d’un système SAP différent de celui de son déploiement sur site. limites d’IOPS Hello par LUN sont généralement configurables dans des déploiements sur site. Alors qu’avec le stockage Azure ces limites sont fixes ou comme type de disque hello en fonction de stockage Premium. Par conséquent, avec des déploiements sur site, nous voyons les configurations de client de serveurs de base de données qui sont à l’aide de nombreux volumes pour les exécutables spéciaux tels que SAP et hello SGBD ou des volumes spéciaux pour les bases de données temporaires ou des espaces de table. Lorsqu’un système local est déplacé tooAzure il peut entraîner des déchets tooa de la bande passante des IOPS potentielle gaspiller un disque dur virtuel pour les fichiers exécutables ou des bases de données qui n’effectuent pas de tout ou pas un grand nombre d’IOPS. Par conséquent, dans des machines virtuelles Azure nous recommandons qu’exécutables SGBD et SAP de hello installée sur le disque du système d’exploitation de hello si possible.

Hello placement des fichiers de base de données hello et de fichiers journaux et de type hello de stockage Azure utilisé, doivent être définis par les e/s, la latence et les exigences de débit. Dans l’ordre toohave suffisamment IOPS pour le journal des transactions hello, vous pouvez être forcé tooleverage plusieurs disques durs virtuels pour le journal des transactions hello de fichier ou utilisent un plus grand disque de stockage Premium. Dans ce cas un est conseillé de créer un logiciel RAID (par exemple, Pool de stockage Windows pour Windows ou MDADM et Gestionnaire de volume logique (Gestionnaire de Volume logique) pour Linux) avec hello disques durs virtuels qui contiendra le journal des transactions hello.

- - -
> ![Windows][Logo_Windows] Windows
>
> Lecteur D:\ dans une machine virtuelle Azure est un lecteur non persistant qui est soutenu par certains disques locaux sur le nœud de calcul Azure hello. Comme il est non persistant, cela signifie que n’importe quel contenu toohello modifications hello lecteur D:\ est perdu lors du redémarrage de machine virtuelle de hello. Par modifications, nous entendons les fichiers enregistrés, les répertoires créés, les applications installées, etc.
>
> ![Linux][Logo_Linux] Linux
>
> Les machines virtuelles Azure Linux monter automatiquement un lecteur sur/mnt/Resource qui est un lecteur non persistant soutenu par les disques locaux sur le nœud de calcul Azure hello. Car il est non persistant, cela signifie que n’importe quel toocontent modifications apportées dans/mnt/Resource est perdue lors du redémarrage de hello machine virtuelle. Par modifications, nous entendons les fichiers enregistrés, les répertoires créés, les applications installées, etc.
>
>

- - -
Dépend de hello séries de machines virtuelles Azure, disques locaux hello hello calcul nœud afficher des performances différentes qui peuvent être classés comme :

* A0-A7 : performances très limitées. Non utilisables pour autre chose que le fichier d’échange Windows.
* A8-A11 : très bonnes caractéristiques de performances, avec quelque 10 000 E/S par seconde et un débit supérieur à 1 Go/s.
* Série D : très bonnes caractéristiques de performances, avec quelque 10 000 E/S par seconde et un débit supérieur à 1 Go/s.
* Série DS : très bonnes caractéristiques de performances, avec quelque 10 000 E/S par seconde et un débit supérieur à 1 Go/s.
* Série G : très bonnes caractéristiques de performances, avec quelque 10 000 E/S par seconde et un débit supérieur à 1 Go/s.
* Série GS : très bonnes caractéristiques de performances, avec quelque 10 000 E/S par seconde et un débit supérieur à 1 Go/s.

Les instructions ci-dessus appliquez des types de machine virtuelle toohello certifiées avec SAP. Hello séries de machines virtuelles avec une excellente IOPS et le débit qualifier pour tirer parti de certaines fonctionnalités SGBD, telles que tempdb ou espace de table temporaire.

### <a name="c7abf1f0-c927-4a7c-9c1d-c7b5b3b7212f"></a>Mise en cache pour les machines virtuelles et les disques durs virtuels
Lorsque nous créons ces disques/VHD via le portail de hello ou lorsque nous monter téléchargé tooVMs de disques durs virtuels, nous pouvons choisir si le trafic de hello d’e/s entre hello machine virtuelle et les disques durs virtuels situés dans le stockage Azure sont mis en cache. Azure Standard et Premium Storage font appel à deux technologies différentes pour ce type de mise en cache. Dans les deux cas hello du cache lui-même serait disque reposer sur hello utilisés par les lecteurs mêmes hello disque temporaire (D:\ sur Windows) ou/mnt/Resource sur Linux Hello machine virtuelle.

Pour le stockage Azure Standard les types hello cache possibles sont :

* Aucune mise en cache
* Mise en cache en lecture
* Mise en cache en lecture et en écriture

Commande tooget cohérentes et déterministes les performances, vous devez définir hello mise en cache sur le stockage Azure Standard pour tous les VHD contenant **SGBD liées des fichiers de données, les fichiers journaux et too'NONE d’espace de table'**. Hello mise en cache de hello machine virtuelle peut rester avec la valeur par défaut hello.

Pour le stockage Azure Premium hello options de mise en cache suivantes existe :

* Aucune mise en cache
* Mise en cache en lecture

Il est recommandé pour le stockage Azure Premium tooleverage **cache de lecture pour les fichiers de données** de la base de données SAP hello et choisissez **aucune mise en cache pour un ou plusieurs vhd de fichiers journaux de hello**.

### <a name="c8e566f9-21b7-4457-9f7f-126036971a91"></a>RAID logiciel
Comme déjà indiqué ci-dessus, vous devrez nombre de hello toobalance d’IOPS nécessaire pour les fichiers de base de données hello nombre hello de disques durs virtuels que vous pouvez configurer et hello IOPS maximales qu’une machine virtuelle Azure fournit par disque dur virtuel ou stockage Premium disque type. Moyen le plus simple toodeal avec hello IOPS charge sur les disques durs virtuels est toobuild un RAID logiciels sur hello différents disques durs virtuels. Puis, placez un nombre de fichiers de données de hello SGBD SAP sur hello que LUN coupées les volumes RAID logiciels hello. Dépend des exigences hello souhaité tooconsider hello d’utilisation du stockage Premium ainsi depuis deux Hello trois différents disques de stockage Premium fournissent des quota d’IOPS plus élevée que les disques durs virtuels basés sur le stockage Standard. En outre hello significatif mieux la latence d’e/s fournis par le stockage Azure Premium.

Journal des transactions toohello systèmes SGBD hello va de même. Avec un grand nombre d'entre eux ajouter simplement plus de fichiers Tlog ne change rien depuis SGBD hello écrire dans un des fichiers de hello à la fois uniquement. Si le taux d’IOPS plus élevés sont nécessaires à une norme unique en fonction de stockage disque dur virtuel peut fournir, vous pouvez distribuer sur plusieurs disques durs virtuels de stockage Standard, ou vous pouvez utiliser un type de disque de stockage Premium supérieure qui dépasse le taux d’IOPS plus élevés fournit également des facteurs une latence plus faible pour l’écriture de hello I / Système d’exploitation dans le journal des transactions hello.

Les situations rencontrées dans les déploiements Azure qui justifient l’utilisation d’un RAID logiciel sont les suivantes :

* Le journal des transactions et le journal de rétablissement nécessitent plus d’E/S par seconde que ce qu’un disque dur virtuel Azure unique peut offrir. Comme indiqué ci-dessus, vous pouvez résoudre ce problème en créant un LUN sur plusieurs disques durs virtuels à l’aide d’un RAID logiciel.
* E/s la charge de travail une distribution inégale sur hello différents fichiers de données de base de données SAP hello. Dans ce cas un peut rencontrer un fichier de données atteint le quota de hello plutôt souvent. Alors que les autres fichiers de données ne reçoivent pas même fermer toohello quota d’IOPS d’un disque dur virtuel unique. Dans ce type hello cas solution la plus simple est toobuild un numéro d’unité logique sur plusieurs disques durs virtuels à l’aide d’un logiciel RAID.
* Vous ne savez pas quel hello exacte d’e/s charge de travail par fichier de données est et uniquement à peu près savoir ce que hello globale charge de travail des IOPS hello SGBD est. Toodo plus simple est toobuild un numéro d’unité logique avec hello aide d’un logiciel RAID. somme de Hello des quotas de plusieurs disques durs virtuels derrière ce numéro d’unité logique doit satisfaire puis hello connu IOPS taux.

- - -
> ![Windows][Logo_Windows] Windows
>
> L’utilisation de Windows Server 2012 ou d’espaces de stockage ultérieurs est préférable, car l’entrelacement est plus efficace que dans les versions antérieures de Windows. Sachez que vous devrez peut-être toocreate hello Pools de stockage Windows et les espaces de stockage par les commandes PowerShell lors de l’utilisation de Windows Server 2012 en tant que système d’exploitation. commandes de PowerShell Hello se trouve ici <https://technet.microsoft.com/library/jj851254.aspx>
>
> ![Linux][Logo_Linux] Linux
>
> MDADM et Gestionnaire de volume logique (Gestionnaire de volumes logiques) sont pris en charge toobuild un logiciel RAID sur Linux. Pour plus d’informations, lisez hello suivant des articles :
>
> * [Configuration d’un RAID logiciel sur Linux][virtual-machines-linux-configure-raid] (pour MDADM)
> * [Configurer LVM sur une machine virtuelle Linux dans Azure][virtual-machines-linux-configure-lvm]
>
>

- - -
Considérations pour exploiter série de machines virtuelles qui sont en mesure de toowork avec le stockage Azure Premium généralement sont :

* Demandes de latences d’e/s Fermez toowhat SAN/NAS périphériques livrer.
* Exigence d’une latence d’E/S plusieurs fois inférieure à celle offerte par le stockage Azure Standard.
* Nombre d’E/S par seconde par machine virtuelle plus élevé que ce que permettent d’atteindre plusieurs disques durs virtuels Standard avec un certain type de machine virtuelle.

Depuis hello Azure stockage sous-jacent réplique chaque nœuds de stockage de disque dur virtuel tooat moins de trois, simple RAID 0 agrégation par bandes peut être utilisée. Il n’existe aucun tooimplement besoin RAID5 ou RAID1.

### <a name="10b041ef-c177-498a-93ed-44b3441ab152"></a>Microsoft Azure Storage
Microsoft Azure Storage stockera hello machine virtuelle de base (avec le système d’exploitation) et les nœuds de stockage séparés tooat au moins 3 disques durs virtuels ou des objets BLOB. Lors de la création d’un compte de stockage, plusieurs options de protection sont proposées :

![Géoréplication activée pour le compte Azure Storage][dbms-guide-figure-100]

Réplication locale Azure Storage (localement redondant) fournit les niveaux de protection contre la perte de données en raison de l’échec de tooinfrastructure que quelques clients peuvent se permettre de toodeploy. Comme indiqué ci-dessus 4 différentes options sont un cinquième étant une variante de l’un des hello tout d’abord trois. En les examinant de plus près, nous pouvons distinguer :

* **Stockage localement redondant Premium (LRS)**: Azure Premium Storage offre une prise en charge très performante et à faible latence des disques pour les machines virtuelles exécutant des charges de travail qui utilisent beaucoup d’E/S. Il existe 3 réplicas des données hello dans hello même centre de données Azure d’une région Azure. Hello copies seront dans différents domaines d’erreur et mettre à niveau (pour voir des concepts [cela] [ planning-guide-3.2] chapitre Bonjour [Guide de planification][planning-guide]). En cas d’un réplica de données hello hors service en raison de la défaillance de nœud de stockage tooa ou de défaillance du disque, un nouveau réplica est généré automatiquement.
* **Stockage localement redondant (LRS)**: dans ce cas, il existe 3 réplicas des données hello dans hello même centre de données Azure d’une région Azure. Hello copies seront dans différents domaines d’erreur et mettre à niveau (pour voir des concepts [cela] [ planning-guide-3.2] chapitre Bonjour [Guide de planification][planning-guide]). En cas d’un réplica de données hello hors service en raison de la défaillance de nœud de stockage tooa ou de défaillance du disque, un nouveau réplica est généré automatiquement.
* **Stockage redondant de géo-réplication (GRS)**: dans ce cas, il existe une réplication asynchrone qui alimente supplémentaire 3 réplicas des données hello dans une autre région Azure qui se trouve dans la plupart des cas de hello dans hello même région géographique (par exemple, Europe du Nord et l’ouest Europe). Il y a donc au total 6 réplicas des données. Une variante de ce est un complément où les données de hello dans hello répliquées région Azure peuvent être utilisées à des fins lecture (Read-Access géo-redondant).
* **Zone de stockage redondants (ZRS)**: dans ce cas réplicas hello 3 Hello données restent dans hello même région Azure. Comme expliqué dans [cela] [ planning-guide-3.1] chapitre Hello [Guide de planification] [ planning-guide] une région Azure peut être un nombre de centres de données à proximité. Dans les cas de hello de LRS les réplicas hello seraient distribuées sur hello différents centres de données constituant une région Azure.

Des informations supplémentaires sont disponibles [ici][storage-redundancy].

> [!NOTE]
> Pour les déploiements SGBD, hello stockage géo-redondant n'est pas recommandé d’utiliser des
>
> La géo-réplication Azure Storage est asynchrone. Réplication des disques durs virtuels individuels monté tooa seule machine virtuelle ne sont pas synchronisées à l’étape de verrou. Par conséquent, il n’est pas approprié tooreplicate SGBD que les fichiers distribués sur différents disques durs virtuels ou déployés sur un logiciel RAID basé sur plusieurs disques durs virtuels. Les logiciels SGBD requièrent que le stockage de disque persistant hello soit synchronisé précisément sur différents numéros d’unités logiques et les disques/VHD/piles sous-jacent. Les logiciels SGBD utilisent différents mécanismes toosequence activités d’écriture e/s et un SGBD signalera que le stockage sur disque hello ciblé par la réplication de hello est endommagé si ces séquences varient même de quelques millisecondes. Si vous avez vraiment une configuration de base de données avec une base de données répartie sur plusieurs VHD géo-répliquées, ce type de réplication doit donc toobe effectuée avec des moyens de la base de données et les fonctionnalités. Un fiez pas à la géo-réplication du stockage Azure tooperform ce travail.
>
> problème de Hello est la plus simple tooexplain avec un exemple de système. Supposons que vous disposez d’un système SAP chargé dans Azure qui utilise 8 VHD contenant les fichiers de données de hello SGBD plus un disque dur virtuel contenant hello fichier journal des transactions. Chacune de ces 9 VHD aura les données écrites toothem dans une méthode cohérente selon toohello SGBD, si hello écriture des données en fichiers de journaux de transaction ou des données toohello.
>
> Dans l’ordre tooproperly géo-répliquer hello des données et mettre à jour une image de base de données cohérente, le contenu de hello de ces neuf VHD auraient toobe géo-répliquées dans les opérations de hello ordre exact hello d’e/s ont été exécutées par rapport à hello neuf différents VHD. Toutefois, le stockage Azure géo-réplication n’autorise pas toodeclare les dépendances entre les disques durs virtuels. Cela signifie que Microsoft Azure Storage géo-réplication ne connaît pas hello fait que contenu hello dans ces neuf différents VHD sont associée tooeach autres que les modifications de données hello sont cohérentes uniquement lors de la réplication dans les opérations d’e/s hello commande hello s’est produite sur tous les disques durs virtuels de hello 9.
>
> En plus des risques soit élevée que les images hello géo-répliquées dans un scénario de hello ne fournissent pas une image cohérente de la base de données, il existe également une baisse des performances qui s’affiche avec le stockage géo-redondant peut sérieusement nuire aux performances. En résumé, n’utilisez pas ce type de redondance de stockage pour les charges de travail du type SGBD.
>
>

#### <a name="mapping-vhds-into-azure-virtual-machine-service-storage-accounts"></a>Mappage de disques durs virtuels à des comptes de stockage du service Azure Virtual Machines
Un compte de stockage Azure est non seulement le fait d’un administrateur, mais également l’objet de limitations. Alors que les limitations de hello varient si nous parlons un compte de stockage Azure Standard ou un compte de stockage Azure Premium. fonctionnalités Hello et limitations sont répertoriées [ici][storage-scalability-targets]

Pour le stockage Azure Standard, il est important toonote hello IOPS par compte de stockage est limitée (de la ligne contenant « Taux de demandes Total » dans [article de hello][storage-scalability-targets]). De plus, il y a une limite initiale de 100 comptes de stockage par abonnement Azure (depuis juillet 2015). Par conséquent, il est recommandé de toobalance IOPS d’ordinateurs virtuels entre plusieurs comptes de stockage lorsque vous utilisez le stockage Azure Standard. alors que dans l’idéal, une machine virtuelle unique doit si possible utiliser un seul compte de stockage. Dans le cas de déploiements SGBD où chaque disque dur virtuel hébergé dans le stockage Azure Standard peut atteindre sa limite de quota, vous devez donc déployer seulement 30 à 40 disques durs virtuels par compte de stockage Azure faisant appel au stockage Azure Standard. Sur hello autre part, si vous tirer parti du stockage Azure Premium et que vous souhaitez toostore des volumes de base de données volumineuse, vous pouvez être précis en termes d’e/s. Cependant, un compte de stockage Azure Premium Storage est beaucoup plus restrictif en matière de volume de données qu’un compte de stockage Azure Standard. Par conséquent, vous pouvez uniquement déployer un nombre limité de disques durs virtuels au sein d’un compte de stockage Azure Premium avant d’atteindre la limite de volume de données hello. À hello fin de réflexion d’un compte de stockage Azure comme un « SAN virtuel » qui a des capacités limitées aux e/s et/ou de capacité. Par conséquent, tâche hello reste, comme dans les déploiements sur site, de mise en page de hello toodefine Hello disques durs virtuels de différents systèmes SAP hello sur hello différents « appareils SAN imaginaires » ou des comptes de stockage Azure.

Pour Azure stockage toopresent tooa de comptes de stockage différent n’est pas recommandé de stockage Standard unique à la machine virtuelle si possible.

Tandis que l’utilisation de type hello DS ou GS-série de machines virtuelles Azure, il est possible de toomount les disques durs virtuels en dehors des comptes de stockage Azure Standard et les comptes de stockage Premium. Cas d’usage, comme l’écriture des sauvegardes dans le stockage Standard sauvegardé les disques durs virtuels tandis que les données du SGBD et les fichiers journaux sur le stockage Premium toomind où ce type de stockage hétérogènes pourrait être exploitée.

Basée sur les déploiements de client et test too40 environ 30 disques durs virtuels contenant les fichiers de données de base de données et les fichiers journaux peuvent être configurés sur un compte de stockage Standard de Azure unique avec des performances acceptables. Comme mentionné précédemment, limitation hello d’un compte de stockage Azure Premium est probablement toobe hello capacité de données que peut contenir et pas les e/s.

Comme avec SAN appareils en local, partage nécessite la surveillance dans l’ordre tooeventually détecter les goulots d’étranglement sur un compte de stockage Azure. Hello, Extension de surveillance Azure pour SAP et hello portail Azure sont des outils qui peuvent être utilisé toodetect occupé des comptes de stockage Azure qui peut être remise des performances d’e/s non optimaux.  Si cette situation se produit, qu'il est recommandé de tooanother des machines virtuelles occupé toomove compte de stockage Azure. Reportez-vous toohello [Guide de déploiement] [ deployment-guide] pour plus d’informations sur comment tooactivate hello SAP héberger les capacités d’analyse.

Un autre article synthétisant les bonnes pratiques relatives au stockage Azure standard et aux comptes de stockage Azure standard est disponible sur la page <https://blogs.msdn.com/b/mast/archive/2014/10/14/configuring-azure-virtual-machines-for-optimal-storage-performance.aspx>.

#### <a name="moving-deployed-dbms-vms-from-azure-standard-storage-tooazure-premium-storage"></a>Déplacement déployé des machines virtuelles SGBD à partir du stockage Standard Azure tooAzure stockage Premium
Nous rencontrons un certain scénarios où vous en tant que client toomove une machine virtuelle déployée depuis le stockage Azure Standard dans le stockage Azure Premium. Cela n’est pas possible sans déplacer physiquement les données de salutation. Il existe plusieurs objectifs de hello tooachieve façons :

* Vous pouvez simplement copier tous les disques durs virtuels, le disque dur virtuel de base, ainsi que les disques durs virtuels de données dans un nouveau compte de stockage Azure Premium Storage. Très souvent choisis nombre hello de disques durs virtuels dans le stockage Azure Standard pas en raison des faits hello que vous avez besoin de volume de données hello. Mais vous avez besoin d’autant de disques durs virtuels en raison de hello IOPS. Maintenant que vous déplacez tooAzure stockage Premium vous ait moyen moins tooachieve de disques durs virtuels hello certains débit d’e/s. Étant donné les faits hello que dans le stockage Azure Standard vous payez pour hello utilisé données et la taille du disque nominal de hello pas, nombre hello de disques durs virtuels vraiment peu en termes de coûts. Toutefois, avec le stockage Azure Premium, vous payeriez pour la taille du disque nominal hello. Par conséquent, la plupart des clients de hello essayez de nombre de hello tookeep de disques durs virtuels de Azure dans un stockage Premium à hello numéro tooachieve nécessaires hello débit d’IOPS nécessaire. Par conséquent, la plupart des clients de décider par rapport à la façon de hello d’un simple 1:1 copie.
* S’il n’est pas encore monté, vous montez un disque dur virtuel unique pouvant contenir une sauvegarde de base de données de votre base de données SAP. Après la sauvegarde de hello, démontage de tous les disques durs virtuels dont hello VHD contenant hello sauvegarde et hello de copie disque dur virtuel de base et hello du disque dur virtuel avec la sauvegarde de hello dans un compte de stockage Azure Premium. Vous déployez ensuite hello que machine virtuelle basée sur hello base VHD et montage hello disque dur virtuel avec la sauvegarde de hello. Maintenant vous créez vide Premium stockage des disques supplémentaires pour hello ordinateurs virtuels qui sont utilisés toorestore hello bases de données. Cela suppose que hello SGBD vous permet de toochange chemins toohello données et fichiers journaux dans le cadre du processus de restauration hello.
* Une autre possibilité est une variante du processus précédent hello, dans lequel vous venez copiez de sauvegarde de hello disque dur virtuel dans le stockage Azure Premium et attachez sur une machine virtuelle qui vient d’être déployé et installé.
* possibilité de quatrième Hello, vous devez choisir lorsque vous êtes dans le besoin de nombre de hello toochange des fichiers de données de votre base de données. Dans ce cas, vous exécutez une copie de système homogène SAP à l’aide d’une exportation/importation. Placez les exporter des fichiers dans un disque dur virtuel est copié dans un compte de stockage Azure Premium et en l’attachant tooa machine virtuelle que vous utilisez le processus d’importation toorun hello. Les clients utilisent cette possibilité principalement quand ils le souhaitent toodecrease hello quantité, pour les fichiers de données.

### <a name="deployment-of-vms-for-sap-in-azure"></a>Déploiement de machines virtuelles pour SAP dans Azure
Microsoft Azure offre plusieurs méthodes de machines virtuelles de toodeploy et de disques associés. Ainsi, il est différences de hello toounderstand très important, car les préparations d’ordinateurs virtuels de hello peuvent différer dépend de la façon de hello du déploiement. En règle générale, nous examinerons les scénarios de hello décrits dans hello suivant chapitres.

#### <a name="deploying-a-vm-from-hello-azure-marketplace"></a>Déploiement d’une machine virtuelle à partir de hello Azure Marketplace
Vous aimez tootake Microsoft ou tiers 3e fournie image à partir de hello Azure Marketplace toodeploy votre machine virtuelle. Une fois que vous avez déployé votre machine virtuelle dans Azure, vous suivez hello mêmes directives et outils tooinstall hello logiciels SAP dans votre machine virtuelle comme vous le feriez dans un environnement sur site. Pour installer le logiciel SAP hello à l’intérieur de hello machine virtuelle Azure, SAP et Microsoft recommandons tooupload et stockent support d’installation SAP hello dans les disques durs virtuels de Azure ou toocreate une machine virtuelle Azure fonctionne comme un serveur de fichiers' ' qui contient tous les hello support d’installation SAP nécessaires.

#### <a name="deploying-a-vm-with-a-customer-specific-generalized-image"></a>Déploiement d’une machine virtuelle avec une image généralisée propre au client
En raison des exigences spécifiques toospecific ce qui concerne les tooyour du système d’exploitation ou de la version du SGBD, les images hello fourni Bonjour Azure Marketplace ne répondent pas à vos besoins. Par conséquent, vous devrez peut-être toocreate une machine virtuelle à l’aide de votre propre image de machine virtuelle du système d’exploitation/SGBD 'private', qui peut être déployé plusieurs fois par la suite. tooprepare cette image « privée » pour la duplication, hello que système d’exploitation doit être généralisé sur hello local machine virtuelle. Reportez-vous toohello [Guide de déploiement] [ deployment-guide] pour plus d’informations sur la façon de toogeneralize une machine virtuelle.

Si vous avez déjà installé le contenu SAP dans votre machine locale virtuelle (en particulier pour les systèmes de niveau 2), vous pouvez adapter les paramètres du système SAP hello après déploiement hello Hello machine virtuelle Azure via une instance de hello renommer procédure pris en charge par hello approvisionnement en logiciels SAP Manager (Note SAP [1619720]). Dans le cas contraire, vous pouvez installer les logiciels SAP hello plus tard après le déploiement de hello Hello machine virtuelle Azure.

À compter de contenu de base de données hello utilisé par hello application SAP, vous pouvez générer de hello contenu fraîchement une installation SAP ou vous pouvez importer votre contenu dans Azure à l’aide d’un disque dur virtuel avec une sauvegarde de base de données SGBD ou en exploitant les fonctionnalités de hello SGBD toodirectly sauvegarde dans Microsoft Azure Storage. Dans ce cas, vous pourriez également préparer les disques durs virtuels avec hello données SGBD et journal des fichiers locaux et puis importer ces en tant que disques dans Azure. Mais transfert hello des données SGBD locales tooAzure chargées fonctionne sur des disques VHD toobe préparé localement.

#### <a name="moving-a-vm-from-on-premises-tooazure-with-a-non-generalized-disk"></a>Déplacement d’une machine virtuelle à partir de tooAzure local avec un disque non généralisé
Vous envisagez de toomove un système SAP spécifique à partir de tooAzure local (courbes d’élévation et MAJ). Cela peut être effectuée en téléchargeant le disque dur virtuel qui contient hello du système d’exploitation de hello, hello binaires SAP et les éventuels binaires SGBD plus hello des disques durs virtuels avec des fichiers de données et journaux hello de hello SGBD tooAzure. Dans opposé tooscenario #2 ci-dessus, vous conservez hello hostname, les SID SAP et les comptes d’utilisateur SAP Bonjour Azure VM qu’ils ont été configurés dans l’environnement local de hello. Par conséquent, il n’est pas nécessaire de généraliser l’image de hello. Ce cas s’applique tout particulièrement pour les scénarios de coexistence où une partie de hello paysage SAP est exécutée localement et les parties sur Azure.

## <a name="871dfc27-e509-4222-9370-ab1de77021c3"></a>Haute disponibilité et récupération d’urgence avec les machines virtuelles Azure
Azure offre hello suivant les fonctionnalités de haute disponibilité (HA) et de récupération d’urgence (DR) qui s’appliquent toodifferent les composants utilisés pour les déploiements SAP et SGBD

### <a name="vms-deployed-on-azure-nodes"></a>Machines virtuelles déployées sur des nœuds Azure
Hello plateforme Azure n’offre pas de fonctionnalités telles que la Migration dynamique pour les machines virtuelles déployées. Cela signifie si une maintenance est nécessaire sur un cluster de serveur sur lequel un ordinateur virtuel est déployé, hello machine virtuelle doit tooget arrêté et redémarré. La maintenance dans Azure est effectuée à l’aide de domaines de mise à niveau au sein des clusters de serveurs. Seul un domaine de mise à niveau à la fois fait l’objet de la maintenance. Pendant le redémarrage il y aura une interruption de service hello que machine virtuelle est arrêtée lors de la maintenance est effectuée et redémarrage de la machine virtuelle. Toutefois, la plupart des fournisseurs de SGBD fournissent des fonctionnalités haute disponibilité et récupération d’urgence qui redémarrent rapidement les services de SGBD hello sur un autre nœud si le nœud principal de hello n’est pas disponible. Hello plateforme Azure offre une fonctionnalité toodistribute machines virtuelles, de stockage et autres services Azure entre les domaines de mise à niveau tooensure planifié des échecs d’infrastructure ou de maintenance aurait un impact uniquement sur un petit sous-ensemble de machines virtuelles ou services.  Avec une planification rigoureuse, il est infrastructures de local tooon comparables de niveaux de disponibilité tooachieve possible.

Groupes de disponibilité de Microsoft Azure sont un regroupement logique des machines virtuelles ou Services qui garantissent que les machines virtuelles et autres services sont distribuée toodifferent erreur et domaines de mise à niveau au sein d’un cluster de sorte qu’il uniquement un arrêt de nœuds à un point quelconque dans le temps (en lecture [cela] [ virtual-machines-manage-availability] article pour plus d’informations).

Il doit toobe configuré selon leur fonction lors du déploiement de machines virtuelles, comme illustré ci-après :

![Définition du groupe à haute disponibilité pour les configurations haute disponibilité SGBD][dbms-guide-figure-200]

Si nous voulons toocreate des configurations hautement disponibles de déploiements SGBD (indépendantes de hello individuels à haute disponibilité SGBD fonctionnalité utilisée), machines virtuelles de SGBD hello devra :

* Ajouter toohello de machines virtuelles hello même réseau virtuel Azure (<https://azure.microsoft.com/documentation/services/virtual-network/>)
* Hello machines virtuelles de configuration de haute disponibilité hello doit également être Bonjour même sous-réseau. Résolution de noms entre des sous-réseaux différents hello n’est pas possible dans les déploiements de Cloud uniquement, seule la résolution IP fonctionne. Avec une connectivité de site à site ou ExpressRoute pour des déploiements entre différents locaux, un réseau comportant au moins un sous-réseau sera déjà établi. Résolution de noms est effectuée en fonction de toohello localement les stratégies Active Directory et votre infrastructure réseau.

[comment]: <> (MSSedusch TODO Test if still true in ARM)

#### <a name="ip-addresses"></a>Adresses IP
Il est vivement recommandé toosetup hello machines virtuelles pour les configurations à haute disponibilité de façon résistante. Partie de confiance sur IP adresses tooaddress hello HA partenaires au sein de la configuration de haute disponibilité hello n’est pas fiable dans Azure, sauf si des adresses IP statiques sont utilisées. Il existe deux concepts d’« arrêt » dans Azure :

* Arrêt via le portail Azure ou Azure PowerShell applet de commande Stop-AzureRmVM : dans ce cas hello Machine virtuelle est arrêtée et désallouée. Votre compte Azure ne plus être facturé pour cette machine virtuelle afin de rendre hello ne serez facturé que pour le stockage hello utilisé. Toutefois, si les adresse IP privée hello d’interface de réseau hello ne sont pas statique, adresse IP de hello est libérée et cette interface de réseau hello Obtient l’ancienne adresse IP hello, attribué à nouveau après un redémarrage de hello VM n’est pas garanti. Exécution hello arrêt via hello portail Azure ou en appelant Stop-AzureRmVM sera automatiquement la désallocation. Si vous ne souhaitez pas toodeallocat hello machine, utilisez Stop-AzureRmVM - StayProvisioned
* Si vous arrêtez la machine virtuelle à partir d’un niveau de système d’exploitation de hello, hello VM obtient arrêté et n’est pas désallouée. Toutefois, dans ce cas, votre compte Azure sera facturé pour hello machine virtuelle, bien qu’il s’agit d’arrêt hello. Dans ce cas, hello attribution de hello IP adresse tooa machine virtuelle arrêtée sera conservée. Arrêt hello machine virtuelle à partir de n'est pas automatiquement forcer la désallocation.

Même pour les scénarios de coexistence, par défaut un arrêt et une désallocation signifient la désallocation de hello hello machine virtuelle, les adresses IP même si les stratégies locales dans les paramètres DHCP sont différentes.

* Hello exception si une affecte une statique IP adresse tooa comme interface décrit [ici][virtual-networks-reserved-private-ip].
* Dans ce cas, adresse IP de hello reste fixe tant qu’interface de réseau hello n’est pas supprimé.

> [!IMPORTANT]
> Dans l’ordre tookeep hello ensemble déploiement simple et facile à gérer, hello clairement recommandation est toosetup hello partenariat dans une configuration à haute disponibilité SGBD ou récupération d’urgence dans Azure de façon qu’il existe une résolution de noms fonctionne entre hello impliqués des différentes machines virtuelles des machines virtuelles.
>
>

## <a name="deployment-of-host-monitoring"></a>Déploiement de la surveillance d’hôte
Pour une utilisation en production des Applications de SAP dans Azure Virtual Machines, SAP a besoin hello capacité tooget de surveillance d’hôte données à partir d’ordinateurs hôtes physiques hello hello des Machines virtuelles Azure en cours d’exécution. Un niveau de correctif logiciel SAP HostAgent spécifique est requis pour activer cette fonctionnalité dans SAPOSCOL et SAP HostAgent. niveau de correctif exact Hello est documenté dans la Note SAP [1409604].

Pour plus d’informations hello en matière de déploiement des composants qui fournissent des tooSAPOSCOL de données hôte et SAPHostAgent et hello gestion du cycle de vie de ces composants, consultez toohello [Guide de déploiement][deployment-guide]

## <a name="3264829e-075e-4d25-966e-a49dad878737"></a>Spécificités tooMicrosoft SQL Server
### <a name="sql-server-iaas"></a>IaaS SQL Server
À partir de Microsoft Azure, vous pouvez facilement migrer vos applications SQL Server existantes basées sur Windows Server platform tooAzure Machines virtuelles. SQL Server dans une Machine virtuelle permet de vous tooreduce hello coût total de possession de déploiement, la gestion et maintenance des applications d’entreprise à l’échelle en effectuant une migration facilement ces tooMicrosoft applications Azure. Avec SQL Server dans une Machine virtuelle Azure, les administrateurs et développeurs peuvent utiliser hello mêmes outils de développement et d’administration qui sont disponibles sur site.

> [!IMPORTANT]
> Notez que nous traiterons pas de base de données SQL Microsoft Azure qui est une plateforme en tant qu’une offre de Service de hello plateforme Microsoft Azure. discussion Hello dans ce document est sur l’exécution de produit de SQL Server hello tel qu’il est connu pour les déploiements sur site de Machines virtuelles dans Azure, en tirant parti hello Infrastructure comme une fonctionnalité de Service de Azure. Les capacités et fonctionnalités de base de données de ces deux services sont différentes et ne doivent pas être confondues. Voir aussi : <https://azure.microsoft.com/services/sql-database/>
>
>

Il est fortement recommandé de tooreview [cela] [ virtual-machines-sql-server-infrastructure-services] documentation avant de continuer.

Bonjour les pièces de sections suivantes des parties de documentation hello sous lien hello ci-dessus seront agrégées et mentionnés. Les particularités concernant SAP sont également indiquées et certains concepts décrits plus en détail. Toutefois, il est vivement recommandé toowork via hello documentation avant de lire la documentation spécifique de SQL Server hello.

Avant de continuer, il y a certaines informations spécifiques sur SQL Server dans IaaS que vous devez connaître :

* **Contrat de niveau de service pour les machines virtuelles** : il existe un contrat de niveau de service pour les machines virtuelles exécutées dans Azure. Il est disponible ici : <https://azure.microsoft.com/support/legal/sla/>  
* **Prise en charge des versions SQL**: pour les clients SAP, nous prenons en charge SQL Server 2008 R2 et versions ultérieures sur Microsoft Azure Virtual Machine. Les éditions antérieures ne sont pas prises en charge. Pour plus d’informations, voir cette [déclaration officielle](https://support.microsoft.com/kb/956893) générale. Notez qu’en règle générale, SQL Server 2008 est également pris en charge par Microsoft. Toutefois, en raison de la fonctionnalité toosignificant pour SAP qui a été introduit avec SQL Server 2008 R2, SQL Server 2008 R2 est la version minimale requise de hello pour SAP. Gardez à l’esprit que SQL Server 2012 et 2014 est étendu une meilleure intégration hello IaaS scénario (sauvegarde directement sur Azure Storage). Par conséquent, nous limiter cette tooSQL papier Server 2012 et 2014 avec son niveau de correctif plus récent pour Azure.
* **Prise en charge des fonctionnalités SQL**: la plupart des fonctionnalités SQL Server sont prises en charge sur Microsoft Azure Virtual Machines, à quelques exceptions près. **Le clustering de basculement SQL Server à l’aide de disques partagés n’est pas pris en charge**.  Les technologies distribuées telles que la mise en miroir de bases de données, les groupes de disponibilité AlwaysOn, la réplication, la copie des journaux de transaction et l’envoi de journaux et Service Broker sont prises en charge au sein d’une même région Azure. SQL Server AlwaysOn est également pris en charge entre différentes régions Azure comme indiqué ici : <https://blogs.technet.com/b/dataplatforminsider/archive/2014/06/19/sql-server-alwayson-availability-groups-supported-between-microsoft-azure-regions.aspx>.  Hello de révision [instruction de prise en charge](https://support.microsoft.com/kb/956893) pour plus d’informations. Un exemple montrant comment toodeploy une configuration AlwaysOn est présentée dans [cela] [ virtual-machines-workload-template-sql-alwayson] l’article. En outre, découvrez hello meilleures pratiques documentées [ici][virtual-machines-sql-server-infrastructure-services]
* **Performances SQL**: nous sommes persuadés que Microsoft Azure effectue très bien les ordinateurs virtuels hébergés dans les offres de virtualisation de cloud public tooother comparaison, mais les résultats peuvent varier. Pour en savoir plus, consultez [cet article][virtual-machines-sql-server-performance-best-practices].
* **L’utilisation d’Images à partir d’Azure Marketplace**: toodeploy de manière plus rapide hello une nouvelle machine virtuelle Microsoft Azure est toouse une image à partir de hello Azure Marketplace. Il existe des images Bonjour Azure Marketplace qui contiennent SQL Server. images Hello où SQL Server est déjà installé ne peut pas être utilisés immédiatement pour les applications SAP NetWeaver. raison de Hello est le classement de SQL Server par défaut hello est installé dans ces images et le classement de hello pas requis par les systèmes SAP NetWeaver. Dans commande toouse ces images, vérifiez les étapes hello décrites dans le chapitre [à l’aide d’un serveur SQL Server de l’image en dehors de Microsoft Azure Marketplace de hello][dbms-guide-5.6].
* Pour en savoir plus, voir la rubrique [Tarification](https://azure.microsoft.com/pricing/) . Hello [Guide des licences SQL Server 2012](https://download.microsoft.com/download/7/3/C/73CAD4E0-D0B5-4BE5-AB49-D5B886A5AE00/SQL_Server_2012_Licensing_Reference_Guide.pdf) et [Guide des licences SQL Server 2014](https://download.microsoft.com/download/B/4/E/B4E604D9-9D38-4BBA-A927-56E4C872E41C/SQL_Server_2014_Licensing_Guide.pdf) constituent également une ressource importante.

### <a name="sql-server-configuration-guidelines-for-sap-related-sql-server-installations-in-azure-vms"></a>Recommandations en matière de configuration de SQL Server pour les installations associées à SAP sur des machines virtuelles Azure
#### <a name="recommendations-on-vmvhd-structure-for-sap-related-sql-server-deployments"></a>Recommandations portant sur la structure des machines virtuelles/disques VHD pour les déploiements de SQL Server associés à SAP
En fonction de la description générale de hello, les exécutables SQL Server doivent être situés ou installés dans le lecteur du système de disque dur virtuel de base de machine virtuelle hello hello (le lecteur C:\).  En règle générale, la plupart des bases de données système de SQL Server hello n’est pas utilisée par la charge de travail SAP NetWeaver à un niveau élevé. Par conséquent, les bases de données système hello de SQL Server (master, msdb et model) peuvent demeurer sur hello lecteur C:\. Une exception peut être tempdb, ce qui peut nécessiter plus grand volume de données ou de volume d’opérations d’e/s qui ne rentrent pas dans hello dans les cas de hello de certains SAP ERP et toutes les charges BW, ordinateur virtuel d’origine. Pour ces systèmes, hello suit doit être effectuée :

* Déplacer hello tempdb principaux données ou les fichiers toohello même lecteur logique que hello des fichiers de données primaire de la base de données SAP hello.
* Ajoutez tout tooeach de fichiers de données tempdb supplémentaire de hello lecteur logique contenant un fichier de données de base de données utilisateur hello SAP.
* Ajoutez hello tempdb logfile toohello lecteur logique qui contient le fichier de journal hello utilisateur de base de données.
* **Exclusivement pour les types d’ordinateurs virtuels qui utilisent des disques SSD local** sur les journaux et de données tempdb du nœud de calcul hello fichiers peuvent être placés sur hello lecteur D:\. Néanmoins, il peut être recommandé toouse plusieurs fichiers de données tempdb. Être prenant en charge les volumes de lecteur D:\ sont différentes selon hello type d’ordinateurs virtuels.

Ces configurations activer tempdb tooconsume plus d’espace que le lecteur du système hello est en mesure de tooprovide. Dans la taille de commande toodetermine hello correcte de tempdb, consultez les tailles de tempdb hello sur des systèmes existants qui s’exécutent sur site. En outre, une telle configuration permettrait IOPS sur tempdb qui ne peut pas être fourni avec le lecteur du système hello. Là encore, les systèmes qui sont exécutent localement peuvent être utilisés toomonitor d’e/s des charges de travail sur tempdb afin que vous pouvez dériver des numéros d’IOPS hello souhaitées toosee sur tempdb.

Une configuration d’ordinateur virtuel qui exécute SQL Server avec une base de données SAP et où les données tempdb et le fichier journal tempdb sont placés sur le lecteur D:\ de hello ressemble à :

![Configuration de référence de la machine virtuelle IaaS Azure pour SAP][dbms-guide-figure-300]

N’oubliez pas que ce lecteur D:\ hello a dépendantes hello type d’ordinateurs virtuels de tailles différentes. Dépend de la spécification de taille hello de tempdb vous peut-être toopair forcé de données tempdb et les fichiers journaux par hello SAP de base de données et fichiers journaux dans le cas où le lecteur D:\ est trop petite.

#### <a name="formatting-hello-vhds"></a>Mise en forme de disques durs virtuels hello
Hello de SQL Server taille du bloc NTFS pour les disques durs virtuels contenant les journaux et données de SQL Server pour les fichiers doivent être 64 Ko. Il n’existe aucun hello de tooformat lecteur D:\ nécessaire. En effet, ce lecteur est déjà mis en forme.

Dans l’ordre toomake d’assurer que hello restauration ou la création de bases de données n’initialise pas les fichiers de données hello en supprimant le contenu des fichiers de hello hello, vous devez vous assurer que le service SQL Server hello hello utilisateur contexte s’exécute une autorisation donnée est. Les utilisateurs dans le groupe d’administrateurs Windows hello ont généralement ces autorisations. Si hello service SQL Server est exécuté dans le contexte de l’utilisateur de l’utilisateur non administrateur Windows hello, vous devez tooassign que hello utilisateur droit d’utilisateur « Effectuer des tâches de maintenance d’un volume ».  Afficher les détails de hello dans cet Article de la Base de connaissances Microsoft : <https://support.microsoft.com/kb/2574695>

#### <a name="impact-of-database-compression"></a>Impact de la compression de base de données
Dans les configurations où la bande passante d’e/s peut devenir un facteur de limitation, toutes les mesures qui réduisent les IOPS peuvent aider les charges de travail toostretch hello exécutée dans un scénario IaaS comme Azure. Par conséquent, si pas encore fait, appliquer la compression de PAGE de SQL Server est fortement recommandé par SAP et Microsoft avant de télécharger un SAP existant tooAzure des bases de données.

Hello recommandation tooperform Compression de la base de données avant de le télécharger tooAzure reçoit deux raisons :

* Hello toobe données téléchargé est inférieure.
* Durée Hello d’exécution de la compression hello est plus courte, en supposant que possible d’utiliser un matériel plus performant avec plus de processeurs ou de bande passante d’e/s ou moins d’e/s latence locale.
* De plus petite taille de base de données peut entraîner des coûts accessible sans pour l’allocation de disque

La compression de bases de données fonctionne aussi bien dans une machine virtuelle Azure qu’en local. Pour plus d’informations sur comment toocompress une base de données SQL Server SAP existante Vérifiez ici : <https://blogs.msdn.com/b/saponsqlserver/archive/2010/10/08/compressing-an-sap-database-using-report-msscompress.aspx>

### <a name="sql-server-2014--storing-database-files-directly-on-azure-blog-storage"></a>SQL Server 2014 : placement de fichiers de base de données directement sur le stockage d’objets blob Azure
SQL Server 2014 ouvre les fichiers de base de données hello possibilité toostore directement sur le magasin d’objets Blob Azure sans hello « wrapper » d’un disque dur virtuel autour d’elles. Tout particulièrement avec le stockage Azure Standard ou les types de machine virtuelle plus petites Cela permet des scénarios où vous pouvez relever les limites hello d’IOPS qui est appliquée par un nombre limité de disques durs virtuels qui peuvent être des types de machine virtuelle plus petites toosome monté. Toutefois, ce genre de scénario fonctionne dans le cas des bases de données utilisateur, mais non pour les bases de données système SQL Server. Il peut également être appliqué aux fichiers journaux et données de SQL Server. Si vous souhaitez que toodeploy un serveur SQL de SAP de base de données ainsi à la place de 'habillage » dans les disques durs virtuels, gardez suivant de hello à l’esprit :

* toobe de besoins de compte de stockage utilisé Hello dans hello même région Azure comme hello est hello utilisé toodeploy machine virtuelle SQL Server est en cours d’exécution dans.
* Répertoriées plus haut dans ce qui concerne les toodistribute disques durs virtuels sur différents comptes de stockage Azure en considération pour cette méthode de déploiements également. Signifie hello nombre d’opérations d’e/s par rapport aux limites hello Hello compte de stockage Azure.

[comment]: <> (MSSedusch TODO Cette opération utilise la bande passante du réseau et non celle du stockage, n’est-ce pas ?)

Pour plus d’informations sur ce type de déploiement, voir la page : <https://msdn.microsoft.com/library/dn385720.aspx>

Dans les fichiers de données SQL Server ordre toostore directement sur le stockage Azure Premium, vous avez besoin d’un correctif toohave un minimum de SQL Server 2014, qui est décrit ici : <https://support.microsoft.com/kb/3063054>. Le stockage des fichiers de données SQL Server sur le stockage Azure Standard fonctionne avec la version de hello publié de SQL Server 2014. Toutefois, les correctifs même hello contient une autre série de correctifs qui rendent hello direct l’utilisation du stockage d’objets Blob Azure pour les fichiers de données SQL Server et les sauvegardes plus fiable. Par conséquent, nous vous recommandons toouse ces correctifs en général.

### <a name="sql-server-2014-buffer-pool-extension"></a>Fonctionnalité d’extension du pool de mémoires tampons de SQL Server 2014
SQL Server 2014 propose une nouvelle fonctionnalité appelée « extension du pool de mémoires tampons ». Cette fonctionnalité étend le pool de mémoires tampons hello de SQL Server qui est conservée en mémoire avec un cache de niveau second qui est sauvegardé par SSDs locales d’un serveur ou la machine virtuelle. Cela permet de tookeep une plage de travail plus volumineuse de données « dans la mémoire ». Comparés tooaccessing accès hello de stockage Standard Azure dans l’extension de hello du pool de mémoires tampons hello qui est stocké sur des disques SSD de local d’une machine virtuelle Azure est plus rapide des nombreux facteurs.  Par conséquent, en exploitant hello D:\ lecteur local de types de machine virtuelle hello qui ont une excellente IOPS et le débit peut être un hello tooreduce de façon très raisonnables IOPS charger sur Azure Storage et améliorer considérablement les temps de réponse des requêtes. Cela se révèle d’autant plus vrai lorsque vous n’utilisez pas Premium Storage. En cas de stockage Premium et l’utilisation de hello Hello Premium, Azure Cache en lecture sur le nœud de calcul hello, comme cela est recommandé pour les fichiers de données, aucune différences importantes ne sont attendus. Raison est que les deux caches (Extension du Pool de mémoire tampon de SQL Server et Cache de lecture de stockage Premium) sont à l’aide de disques locaux de hello hello de nœuds de calcul.
Pour en savoir plus sur cette fonctionnalité, voir cette documentation : <https://msdn.microsoft.com/library/dn133176.aspx>

### <a name="backuprecovery-considerations-for-sql-server"></a>Considérations relatives à la sauvegarde/restauration pour SQL Server
Lors du déploiement de SQL Server dans Azure, votre méthodologie de sauvegarde doit être passée en revue. Même si le système de hello n’est pas un système de production, base de données SAP hello hébergée par SQL Server doit être sauvegardée régulièrement. Étant donné que le stockage Azure conserve trois images, une sauvegarde est dorénavant moins nécessaire dans le toocompensating en ce qui concerne une panne du stockage. raison priorité Hello maintien d’un plan de sauvegarde et de récupération correct est plus que vous pouvez compenser ce décalage erreurs manuelles/logiques en fournissant le point de restauration de temps. Objectif de hello est tooeither utilisation sauvegardes toorestore hello base de données principale tooa certain de points de temps ou toouse sauvegardes hello dans Azure tooseed un autre système en copiant la base de données existante hello. Par exemple, vous pouvez transférer une installation de système de couche 3 à 2 couches SAP configuration tooa Hello même système en restaurant une sauvegarde.

Il existe trois façons différentes toobackup SQL Server tooAzure stockage :

1. SQL Server 2012 CU4 et l’URL de tooa de bases de données de sauvegarde en mode natif peuvent plus élevée. Cela est détaillée dans le blog de hello [nouvelles fonctionnalités de SQL Server 2014 – partie 5 – améliorations de la sauvegarde/restauration](https://blogs.msdn.com/b/saponsqlserver/archive/2014/02/15/new-functionality-in-sql-server-2014-part-5-backup-restore-enhancements.aspx). Voir le chapitre [SQL Server 2012 SP1 CU4 et versions ultérieures][dbms-guide-5.5.1].
2. TooSQL préalable de versions de SQL Server 2012 CU4 un tooa de toobackup de fonctionnalité de redirection disque dur virtuel et de flux d’écriture hello déplacer vers un emplacement de stockage Azure qui a été configuré. Voir le chapitre [SQL Server 2012 SP1 CU3 et versions antérieures][dbms-guide-5.5.2].
3. méthode finale Hello est tooperform une commande de sauvegarde toodisk SQL Server classique sur une unité de disque du disque dur virtuel.  Ceci est le modèle de déploiement local toohello identiques et n’est pas décrite en détail dans ce document.

#### <a name="0fef0e79-d3fe-4ae2-85af-73666a6f7268"></a>SQL Server 2012 SP1 CU4 et versions ultérieures
Cette fonctionnalité permet le stockage d’objets BLOB toodirectly tooAzure sauvegarde. Sans cette méthode, vous devez sauvegarder les disques durs virtuels de Azure tooother qui est d’utiliser le disque dur virtuel et des IOPS. Hello idée est essentiellement la :

 ![À l’aide de la sauvegarde de SQL Server 2012 tooMicrosoft objet BLOB de stockage Azure][dbms-guide-figure-400]

Hello avantage dans ce cas que de sauvegardes de SQL Server toostore toospend disques durs virtuels sur ne pas utiliser. Par conséquent, vous avez moins de disques durs virtuels alloués et la bande passante entière de hello des IOPS VHD peut être utilisée pour les fichiers journaux et de données. Veuillez noter que hello taille maximale d’une sauvegarde est de 1 To au maximum tooa limité comme décrit dans la section hello « Limitations » dans cet article : <https://msdn.microsoft.com/library/dn435916.aspx#limitations>. Si la taille de la sauvegarde hello, malgré l’utilisation de la compression de sauvegarde de SQL Server dépasse 1 To de taille, hello fonctionnalités décrites dans le chapitre [SQL Server 2012 SP1 CU3 et aux versions antérieures] [ dbms-guide-5.5.2] dans ce document doit toobe utilisé.

[Documentation connexe](https://msdn.microsoft.com/library/dn449492.aspx) décrivant la restauration hello des bases de données à partir de sauvegardes sur le magasin d’objets Blob Azure ne recommandons pas toorestore directement à partir de magasin d’objets BLOB Azure si les sauvegardes hello est > 25 Go. Hello recommandation dans cet article est simplement basée sur les considérations relatives aux performances et pas en raison de restrictions de toofunctional. Par conséquent, différentes conditions peuvent s’appliquer au cas par cas.

Pour des informations sur la configuration et l’exploitation de ce type de sauvegarde, voir [ce](https://msdn.microsoft.com/library/dn466438.aspx) didacticiel

Un exemple de séquence hello d’étapes peut être lues [ici](https://msdn.microsoft.com/library/dn435916.aspx).

Automatisation des sauvegardes, il est plus élevé toomake importance assurer que les objets BLOB de hello pour chaque sauvegarde sont nommés différemment. Dans le cas contraire, ils seront remplacés et chaîne de restauration hello est rompue.

Pas toomix les choses entre hello 3 différents types de sauvegardes, il est conseillé de toocreate différents conteneurs sous le compte de stockage hello utilisé pour les sauvegardes. les conteneurs Hello peut être uniquement par la machine virtuelle ou par type de sauvegarde et de la machine virtuelle. schéma de Hello pourrait ressembler à :

 ![À l’aide de la sauvegarde SQL Server 2012 tooMicrosoft objet BLOB de stockage Azure – différents conteneurs sous des comptes de stockage séparés][dbms-guide-figure-500]

Dans l’exemple hello ci-dessus, hello sauvegardes ne seront pas exécutées dans hello où hello du compte de stockage même les ordinateurs virtuels sont déployés. Il y aura un nouveau compte de stockage, en particulier pour les sauvegardes de hello. Dans les comptes de stockage hello, il y aura différents conteneurs créés avec une matrice de type hello de sauvegarde et hello nom d’ordinateur virtuel. Ce type facilement des sauvegardes de hello tooadministrate plus faciles de hello différentes machines virtuelles.

BLOB Hello écrites directement les sauvegardes hello, n’ajoutez pas de nombre toohello Hello disques durs virtuels d’une machine virtuelle. Par conséquent, un peut optimiser maximum hello VHD montés d’hello spécifique VM SKU pour les données de hello et fichier journal des transactions et toujours exécuter une sauvegarde sur un conteneur de stockage.

#### <a name="f9071eff-9d72-4f47-9da4-1852d782087b"></a>SQL Server 2012 SP1 CU3 et versions antérieures
Hello première étape doit effectuer dans l’ordre tooachieve une sauvegarde directement sur Azure Storage serait toodownload hello msi, qui est lié trop[cela](https://www.microsoft.com/download/details.aspx?id=40740) trouve dans l’article.

Téléchargez le fichier d’installation de hello x64 et une documentation hello. fichier de Hello installe un programme appelé : « Microsoft SQL Server Backup tooMicrosoft Azure Tool ». Lire la documentation produit de hello hello attentivement.  outil de Hello fonctionne hello de configuration suivant :

* À partir de hello côté SQL Server, un emplacement de disque pour la sauvegarde de SQL Server hello est défini (n’utilisez pas lecteur D:\ de hello pour cela).
* outil de Hello vous permettra de règles toodefine qui peuvent être utilisé toodirect différents types de conteneurs de stockage Azure toodifferent de sauvegardes.
* Une fois que les règles de hello sont en place, hello outil redirige les flux d’écriture hello de tooone de sauvegarde hello de hello VHD/disque toohello emplacement de stockage Azure qui a été précédemment défini.
* Hello outil conservera un fichier stub petite de quelques Ko sur hello VHD/disque a été défini pour hello SQL Server sauvegarde. **Ce fichier doit rester sur l’emplacement de stockage hello, car elle est requise toorestore à nouveau depuis le stockage Azure.**
  * Si vous avez perdu un fichier stub hello (par exemple, via la perte de supports de stockage hello contenant un fichier stub hello) et que vous avez choisi d’option hello de sauvegarde tooa compte de stockage Microsoft Azure, vous pouvez récupérer un fichier stub via Microsoft Azure Storage par hello télécharger à partir du conteneur de stockage hello dans lequel il a été placé. Vous devez ensuite placer un fichier stub hello dans un dossier sur l’ordinateur local de hello où hello outil est configuré toohello de toodetect et le téléchargement même conteneur avec hello même mot de passe de chiffrement si le chiffrement a été utilisé avec la règle d’origine de hello.

Cela signifie que le schéma de hello comme décrit ci-dessus pour les versions plus récentes de SQL Server peut être mis en place également pour les versions de SQL Server qui ne permettent pas d’adressage direct vers un emplacement de stockage Azure.

Cette méthode ne doit pas être utilisée avec les versions plus récentes de SQL Server qui prennent en charge la sauvegarde en mode natif sur Azure Storage. Les exceptions sont les limitations de la sauvegarde en mode natif hello dans Azure où bloquent l’exécution de sauvegarde native dans Azure.

#### <a name="other-possibilities-toobackup-sql-server-databases"></a>Autres possibilités toobackup bases de données SQL
Autres bases de données toobackup possibilités est tooa de disques durs virtuels supplémentaire tooattach machine virtuelle que vous utilisez des sauvegardes de toostore sur. Dans ce cas vous devez toomake que ce hello disques durs virtuels ne sont pas exécutés complète. Si tel est le cas de hello, vous devez toounmount hello disque dur virtuel et donc toospeak « archive » et remplacez-le par un nouveau disque dur virtuel vide. Si vous passez ce chemin d’accès vers le bas, vous souhaitez tookeep ces disques durs virtuels dans des comptes de stockage Azure distinct à partir de hello ceux qui hello des disques durs virtuels avec des fichiers de base de données hello.

Une deuxième possibilité est toouse une machine virtuelle large qui peut avoir plusieurs disques durs virtuels attachés. Par exemple, un système D14 avec 32 disques VHD. Utilisez toobuild des espaces de stockage un environnement flexible dans lequel vous pouvez générer des partages qui servent ensuite en tant que cibles de sauvegarde pour différents serveurs de SGBD hello.

Certaines meilleures pratiques sont également décrites [ici](https://blogs.msdn.com/b/sqlcat/archive/2015/02/26/large-sql-server-database-backup-on-an-azure-vm-and-archiving.aspx) .

#### <a name="performance-considerations-for-backupsrestores"></a>Considérations sur les performances des sauvegardes/restaurations
Comme dans les déploiements de système nu, les performances de sauvegarde/restauration sont dépend du nombre de volumes peut être lues en parallèle et quelles débit hello de ces volumes peut être. En outre, hello consommation d’UC utilisée par la compression de sauvegarde peut jouent un rôle significatif sur les machines virtuelles avec uniquement les threads de l’UC de too8. Par conséquent, on peut partir des hypothèses suivantes :

* Hello moins hello nombre de disques durs virtuels utilisé des fichiers de données hello toostore, hello plus petites hello débit global de lecture.
* Hello plus petit nombre de hello de threads d’UC Bonjour VM, hello plus grave impact hello de compression de la sauvegarde.
* Hello moins cibles (objets BLOB ou des disques durs virtuels) toowrite hello de sauvegarde vers, hello débit de hello moindre.
* Bonjour Bonjour plus petite taille de machine virtuelle, hello plus petits hello débit quota de stockage l’écriture et la lecture depuis le stockage Azure. Indépendamment de si les sauvegardes hello sont stockées directement sur les objets Blob Azure, ou s’ils sont stockés dans les disques durs virtuels stockés à nouveau dans les objets BLOB Azure.

Lorsque vous utilisez un objet de stockage BLOB Microsoft Azure en tant que cible de sauvegarde hello dans les versions plus récentes, vous êtes limité toodesignating une seule URL cible pour chaque sauvegarde spécifique.

Mais lorsque vous utilisez hello « Microsoft SQL Server Backup tooMicrosoft Azure Tool » dans les versions antérieures, vous pouvez définir plusieurs cibles de fichier. Avec plusieurs cibles, faites évoluer les sauvegarde hello et hello débit de sauvegarde de hello est plus élevé. Cela se traduirait ensuite dans plusieurs fichiers ainsi hello compte de stockage Azure. Dans nos tests, à l’aide de plusieurs destinations de fichiers permet d’obtenir un débit hello celui avec les extensions de sauvegarde hello implémentées dans à partir de SQL Server 2012 SP1 CU4 sur. Vous également ne sont pas bloquées par la limite de 1 to hello comme sauvegarde en mode natif hello dans Azure.

Toutefois, gardez à l’esprit, débit de hello est également dépendant de l’emplacement hello Hello vous utilisez pour la sauvegarde de hello de compte de stockage Azure. Une idée peut être le compte de stockage toolocate hello dans une région différente de celle hello dans que machines virtuelles s’exécutent. Par exemple, vous serez exécuter la configuration d’ordinateur virtuel hello en Europe occidentale, mais placer hello compte de stockage que vous utilisez tooback contre dans Europe du Nord. Qui certainement aura un impact sur le débit de sauvegarde hello et qui est probablement pas toogenerate un débit de 150 Mo/s, telle qu’elle apparaît toobe possible dans les cas où hello de stockage cible et hello des machines virtuelles s’exécutent dans hello même centre de données régional.

#### <a name="managing-backup-blobs"></a>Gestion des objets blob de sauvegarde
Est une sauvegarde de hello exigence toomanage sur votre propre. Attente de hello étant que plusieurs objets BLOB sera créé par l’exécution de sauvegardes fréquentes du journal, administration de ces objets BLOB peut facilement surcharger hello portail Azure. Par conséquent, il est tooleverage pourquoi un Explorateur de stockage Azure. Il existe plusieurs qui peuvent aider à toomanage un compte de stockage Azure

* Microsoft Visual Studio avec le Kit de développement logiciel (SDK) Azure installé (<https://azure.microsoft.com/downloads/>)
* Explorateur de stockage Microsoft Azure (<https://azure.microsoft.com/downloads/>)
* Outils tiers

[comment]: <> (Pas encore pris en charge sur ARM)
[comment]: <> (#### Sauvegarde de machine virtuelle Azure)
[comment]: <> (Machines virtuelles au sein de hello système SAP peuvent être sauvegardées à l’aide de la fonctionnalité de sauvegarde des machines virtuelles Azure. Sauvegarde des machines virtuelles Azure introduite au début de l’année hello 2015 et pendant ce temps est une méthode standard de toobackup un VM complète dans Azure. Sauvegarde Azure stocke les sauvegardes de hello dans Azure et permet une restauration d’une machine virtuelle.)
[comment]: <> (Machines virtuelles que l’exécution des bases de données peuvent être sauvegardées de façon cohérente si prend en charge des systèmes de SGBD hello hello Windows VSS Volume Shadow Copy Service < https://msdn.microsoft.com/library/windows/desktop/bb968832.aspx> que SQL Server est. À l’aide de la sauvegarde de la machine virtuelle Azure peut donc être une tooa de tooget de manière récupérable sauvegarde de base de données SAP. L’utilisation de la fonctionnalité de sauvegarde de machine virtuelle Azure peut permettre d’obtenir une sauvegarde de base de données SAP susceptible d’être restaurée. Par conséquent, la recommandation de hello est tooperform les sauvegardes de bases de données avec des fonctionnalités SGBD au lieu de compter sur la sauvegarde de machine virtuelle Azure.)
[comment]: <> (tooget familiarisé avec la sauvegarde des machines virtuelles Azure Démarrez ici < https://azure.microsoft.com/documentation/services/backup/>)

### <a name="1b353e38-21b3-4310-aeb6-a77e7c8e81c8"></a>À l’aide d’images SQL Server hors hello Microsoft Azure Marketplace
Microsoft propose des machines virtuelles Bonjour Azure Marketplace qui contiennent déjà des versions de SQL Server. Pour les clients SAP qui ont besoin de licences pour SQL Server et Windows, cela peut être un besoin de hello opportunité toobasically garde de licences par les machines virtuelles avec SQL Server est déjà installé. Commande toouse ces images pour SAP, hello suivant considérations doivent être toobe apportée :

* les versions d’évaluation non SQL Server Hello coûtent plus chers simplement un 'Windows uniquement' ordinateur virtuel déployé à partir d’Azure Marketplace. Consultez ces prix de toocompare articles : <https://azure.microsoft.com/pricing/details/virtual-machines/> et <https://azure.microsoft.com/pricing/details/virtual-machines/#Sql>.
* Vous pouvez uniquement utiliser les versions de SQL Server qui sont prises en charge par SAP, telles que SQL Server 2012.
* classement de Hello de l’instance de SQL Server de hello qui est installé sur des machines virtuelles proposées Bonjour Azure Marketplace hello n’est pas le classement hello SAP NetWeaver requiert hello SQL Server instance toorun. Vous pouvez modifier le classement de hello mais avec directions hello Bonjour suivant la section.

#### <a name="changing-hello-sql-server-collation-of-a-microsoft-windowssql-server-vm"></a>La modification hello classement SQL Server d’une machine virtuelle de Microsoft Windows/SQL Server
Étant donné que les images de SQL Server hello Bonjour Azure Marketplace ne sont pas configurés classement de hello toouse qui est requis par les applications SAP NetWeaver, il doit toobe modifié immédiatement après le déploiement de hello. Pour SQL Server 2012, cela est possible avec hello comme suit dès que hello machine virtuelle a été déployée et un administrateur est en mesure de toolog dans hello déployé machine virtuelle :

* Ouvrez une fenêtre de commande Windows en tant qu’« administrateur ».
* Modifier hello Active tooC:\Program Files\Microsoft SQL Server\110\Setup Bootstrap\SQLServer2012.
* Exécutez la commande hello : Setup.exe /QUIET/action = REBUILDDATABASE/InstanceName = MSSQLSERVER/sqlsysadminaccounts =`<local_admin_account_name`>/SQLCOLLATION = SQL_Latin1_General_Cp850_BIN2   
  * `<local_admin_account_name`> Bonjour compte a été défini en tant que compte d’administrateur hello lors du déploiement hello VM pour hello première exécution de la galerie de hello.

processus de Hello doit uniquement prendre quelques minutes. Dans toomake de commande que si l’étape de hello terminé avec le résultat correct de hello, veuillez effectuer hello comme suit :

* Ouvrez SQL Server Management Studio.
* Ouvrez une fenêtre Requête.
* Exécutez hello commande sp_helpsort dans la base de données master de SQL Server de hello.

résultat de Hello souhaité doit ressembler à :

    Latin1-General, binary code point comparison sort for Unicode Data, SQL Server Sort Order 40 on Code Page 850 for non-Unicode Data

Si ce n’est pas le résultat de hello, arrêter le déploiement SAP et examinez pourquoi commande de hello le programme d’installation n’a pas fonctionné comme prévu. Déploiement d’applications SAP NetWeaver sur l’instance SQL Server avec des pages de codes SQL Server autre que celui mentionné ci-dessus hello est **pas** pris en charge.

### <a name="sql-server-high-availability-for-sap-in-azure"></a>Solutions SQL Server haute disponibilité pour SAP dans Azure
Comme mentionné plus haut dans ce document, aucun risque toocreate partagé stockage n’est nécessaire pour l’utilisation de hello hello plus ancienne fonctionnalité de SQL Server haute disponibilité. Cette fonctionnalité installerait plusieurs instances de SQL Server dans un Windows Server Cluster de basculement (WSFC) à l’aide d’un disque partagé pour les bases de données utilisateur hello (et, finalement, tempdb). Il s’agit de méthode de haute disponibilité standard de beaucoup de temps hello également pris en charge par SAP. Comme Azure ne prend pas en charge le stockage partagé, les configurations de haute disponibilité de SQL Server reposant sur un cluster de disque partagé sont impossibles. Toutefois, d’autres méthodes de haute disponibilité sont toujours possibles et sont décrits dans les sections suivantes de hello.

[comment]: <> (L’article est toujours tooASM de référence)
[comment]: <> (Avant de lire les technologies de haute disponibilité hello utilisables pour SQL Server dans Azure, il existe un document de très bon qui donne plus de détails et des pointeurs [[[[ici] Virtual-machines-SQL-Server-High-Availability-and-Disaster-Recovery-Solutions])

#### <a name="sql-server-log-shipping"></a>Copie des journaux de transaction SQL Server
Une des méthodes de hello de haute disponibilité (HA) est l’envoi de journaux SQL Server. Si les machines virtuelles hello de configuration de haute disponibilité hello ont l’utilisation de la résolution de noms, il n’existe aucun problème et le programme d’installation de hello dans Azure ne diffère pas à une installation est effectuée localement. Il n’est pas recommandé toorely sur la résolution d’adresses IP. En ce qui concerne toosetting des principes hello autour de l’envoi de journaux et les journaux, consultez la documentation :

<https://technet.microsoft.com/library/ms187103.aspx>

Dans l’ordre tooreally obtenir la haute disponibilité, doivent être toodeploy hello machines virtuelles qui sont dans ce un toobe de configuration d’envoi de journaux au sein de hello même à haute disponibilité Azure.

#### <a name="database-mirroring"></a>Mise en miroir de bases de données
Mise en miroir de base de données pris en charge par SAP (voir la Note SAP [965908]) s’appuie sur la définition d’un partenaire de basculement dans la chaîne de connexion SAP de hello. Pour les cas de hello entre différents locaux, nous partons du principe que hello deux machines virtuelles sont Bonjour même domaine que les instances de SQL Server hello utilisateur contexte hello deux sont exécutent sous sont également les utilisateurs du domaine et dispose des privilèges dans les instances de SQL Server hello deux impliqués. Par conséquent, le programme d’installation de hello de mise en miroir de base de données dans Azure ne diffère pas entre une programme d’installation/de configuration local.

Comme des déploiements de Cloud uniquement, méthode la plus simple hello est toohave un autre domaine d’installation dans Azure toohave ces machines virtuelles SGBD (et les machines virtuelles SAP dédiées) dans un seul domaine.

Si un domaine n’est pas possible, un peut également utiliser des certificats pour les points de terminaison de mise en miroir comme décrit ici de la base de données hello : <https://technet.microsoft.com/library/ms191477.aspx>

Un didacticiel tooset des base de données mise en miroir dans Azure se trouve ici : <https://technet.microsoft.com/library/ms189852.aspx>

#### <a name="alwayson"></a>AlwaysOn
AlwaysOn est pris en charge pour SAP local (voir la Note SAP [1772688]), il est pris en charge toobe utilisé en combinaison avec SAP dans Azure. faits Hello que vous n’êtes pas en mesure de toocreate partagé des disques dans Azure ne signifie pas qu’une ne peut pas créer une configuration de Cluster de basculement AlwaysOn Windows Server (WSFC) entre les différentes machines virtuelles. Il uniquement signifie que vous n’avez pas hello possibilité toouse un disque partagé en tant qu’un quorum dans la configuration de cluster hello. Par conséquent, vous pouvez créer une configuration WSFC AlwaysOn dans Azure et ne pas sélectionner de type hello quorum qui utilise un disque partagé. Hello environnement Azure ces machines virtuelles sont déployées dans doit se résoudre hello des machines virtuelles par nom et hello machines virtuelles doit être Bonjour même domaine. Cela se révèle vrai pour Azure uniquement, dans le cas de déploiement entre différents locaux. Il existe certaines considérations spéciales déploiement hello écouteur de groupe de disponibilité de SQL Server (pas toobe confondue avec hello haute disponibilité Azure), car Azure ne permet pas à ce stade toosimply créer un objet AD/DNS comme il est possible en local. Par conséquent, les étapes d’installation différentes sont comportement spécifique de hello tooovercome nécessaire d’Azure.

Lors de l’utilisation de l’écouteur de groupe de disponibilité, tenez compte des considérations suivantes :

* À l’aide d’un écouteur de groupe de disponibilité est uniquement possible avec Windows Server 2012 ou Windows Server 2012 R2 comme système d’exploitation invité de hello machine virtuelle. Pour Windows Server 2012, vous devez assurer que ce correctif est appliqué de toomake : <https://support.microsoft.com/kb/2854082>
* Pour Windows Server 2008 R2 ce correctif n’existe pas et AlwaysOn doit toobe utilisé Bonjour même manière que la mise en miroir de base de données en spécifiant un partenaire de basculement dans la chaîne de connexion hello (via hello SAP default.pfl paramètre dbs/mss/server : consultez la Note SAP [965908]).
* Lorsque l’aide d’un écouteur de groupe de disponibilité, les machines virtuelles de base de données hello devez toobe connecté tooa dédié équilibrage de charge. Nom de résolution dans les déploiements de Cloud uniquement nécessiterait soit toutes les machines virtuelles d’un système SAP (serveurs d’applications, SGBD serveurs et (A) SCS) figurent dans hello même réseau virtuel ou nécessiterait à partir d’une maintenance hello couche des applications SAP du fichier etc\host de hello dans commande tooget hello noms de machine virtuelle hello machines virtuelles SQL Server résolu. Dans l’ordre les tooavoid que Azure est assigne de nouvelles adresses IP dans les cas où les deux machines virtuelles sont arrêtées, une doit affecter des adresses IP statiques toohello les interfaces réseau de ces ordinateurs virtuels dans la configuration d’AlwaysOn hello (définition d’une adresse IP statique est décrit dans [cela] [ virtual-networks-reserved-private-ip] article)

[comment]: <> (Anciens blogs)
[comment]: <> (&lt;https://blogs.msdn.com/b/alwaysonpro/archive/2014/08/29/recommendations-and-best-practices-when-deploying-sql-server-alwayson-availability-groups-in-windows-azure-iaas.aspx&gt;, &lt;https://blogs.technet.com/b/rmilne/archive/2015/07/27/how-to-set-static-ip-on-azure-vm.aspx&gt;)
* Il étapes spéciales sont nécessaires lorsque la création de la configuration de cluster WSFC hello où les cluster hello a besoin d’une adresse IP particulière assignée, car Azure avec la fonctionnalité actuelle affecterait le nom du cluster hello hello la même adresse IP en tant que cluster de hello hello nœud est créé sur. Cela signifie qu'une étape manuelle doit être effectuée tooassign un autre cluster de toohello d’adresse IP.
* Hello écouteur du groupe de disponibilité va toobe créé dans Azure avec les points de terminaison TCP/IP qui sont affectés des machines virtuelles toohello en exécutant les réplicas principal et secondaire de hello hello du groupe de disponibilité.
* Il peut y avoir un toosecure besoin de ces points de terminaison avec des ACL.

[comment]: <> (Ancien blog TODO)
[comment]: <> (les étapes détaillées de Hello et expliqués installation d’une configuration AlwaysOn sur Azure sont encore mieux lorsque vous parcourez par hello didacticiel disponible [here][virtual-machines-windows-classic-ps-sql-alwayson-availability-groups])
[comment]: <> (Préconfiguré configuration AlwaysOn via hello la galerie Azure < https://blogs.technet.com/b/dataplatforminsider/archive/2014/08/25/sql-server-alwayson-offering-in-microsoft-azure-portal-gallery.aspx>)
[comment]: <> (Creating an Availability Group Listener is best described in [this][virtual-machines-windows-classic-ps-sql-int-listener] tutorial)
[comment]: <> (Securing network endpoints with ACLs are explained best here:)
[comment]: <> (*    &lt;https://michaelwasham.com/windows-azure-powershell-reference-guide/network-access-control-list-capability-in-windows-azure-powershell/&gt;)
[comment]: <> (*    &lt;https://blogs.technet.com/b/heyscriptingguy/archive/2013/08/31/weekend-scripter-creating-acls-for-windows-azure-endpoints-part-1-of-2.aspx&gt; )
[comment]: <> (*    &lt;https://blogs.technet.com/b/heyscriptingguy/archive/2013/09/01/weekend-scripter-creating-acls-for-windows-azure-endpoints-part-2-of-2.aspx&gt;)  
[comment]: <> (*    &lt;https://blogs.technet.com/b/heyscriptingguy/archive/2013/09/18/creating-acls-for-windows-azure-endpoints.aspx&gt;)

Il est possible de toodeploy un groupe de disponibilité AlwaysOn de SQL Server sur différentes régions Azure également. Cette fonctionnalité sera exploitent la connectivité de réseau Azure de hello ([plus de détails][virtual-networks-configure-vnet-to-vnet-connection]).

[comment]: <> (Ancien blog TODO)
[comment]: <> (Hello le programme d’installation de groupes de disponibilité AlwaysOn de SQL Server dans un tel scénario est décrit ici : < https://blogs.technet.com/b/dataplatforminsider/archive/2014/06/19/sql-server-alwayson-availability-groups-supported-between-microsoft-azure-regions.aspx>.)

#### <a name="summary-on-sql-server-high-availability-in-azure"></a>Haute disponibilité SQL Server dans Azure - Résumé
Hello sachant que le stockage Azure protège le contenu hello, il existe un moins tooinsist raison sur une image de secours. Cela signifie que votre scénario de haute disponibilité doit tooonly contre hello suivant cas :

* Indisponibilité de hello VM dans son ensemble en raison de toomaintenance sur le cluster de serveurs hello dans Azure ou d’autres raisons
* Problèmes de logiciels dans l’instance de SQL Server hello
* protection contre les erreurs manuelles, lorsque les données sont supprimées et qu’une récupération jusqu’à une date et heure est requise.

Consulte les technologies correspondance un peut dire que les deux premiers cas de hello peuvent être couverts par la mise en miroir de base de données ou AlwaysOn, tandis que le troisième cas de hello peuvent uniquement être couverts par envoi de journaux.

Vous devez toobalance hello configuration plus complexe de AlwaysOn, comparé tooDatabase mise en miroir, avec les avantages de hello de AlwaysOn. Parmi ces avantages, on peut citer :

* des réplicas secondaires accessibles en lecture ;
* des sauvegardes à partir des réplicas secondaires ;
* meilleure extensibilité ;
* possibilités de disposer de plusieurs réplicas secondaires.

### <a name="9053f720-6f3b-4483-904d-15dc54141e30"></a>Résumé – SQL Server général pour SAP sur Azure
Ce guide offre de nombreuses recommandations. Nous vous invitons à les parcourir plusieurs fois avant de planifier votre déploiement Azure. En général, toutefois, être vraiment toofollow hello supérieur dix système SGBD dans Azure :

[comment]: <> (Débit multiplié par 2,3 par rapport à quoi ? Than one VHD?)
1. Utilisez hello dernière version du système SGBD, comme SQL Server 2014, ce qui a des avantages de la plupart des hello dans Azure. Pour SQL Server, il s’agit de SQL Server 2012 SP1 CU4, qui comprend la fonctionnalité de hello de sauvegarde se stockage Azure. Toutefois, conjointement avec SAP nous recommandons au moins SQL Server 2014 SP1 CU1 ou SQL Server 2012 SP2 et hello CU plus récente.
2. Planifiez avec soin votre paysage SAP dans la disposition du fichier de données Azure toobalance hello et restrictions Azure :
   * N’avez pas trop grand nombre de disques durs virtuels, mais ont suffisamment tooensure que vous pouvez atteindre votre IOPS requises.
   * N’oubliez pas que les E/S par seconde sont limitées pour chaque compte Stockage Azure, et que les comptes de stockage sont limités au sein de chaque abonnement Azure ([plus d’informations ici][azure-subscription-service-limits]).
   * Uniquement par bande entre les disques durs virtuels, si vous avez besoin de tooachieve un débit plus élevé.
3. Ne jamais installer de logiciel ou de fichiers qui nécessitent la persistance sur hello lecteur D:\ non permanente et rien sur ce lecteur ne sera pas conservé au redémarrage de Windows.
4. N’utilisez pas la mise en cache de disque VHD Azure pour le stockage Azure standard.
5. N’utilisez pas un compte de stockage Azure géorépliqué.  Utilisez des systèmes localement redondants pour les charges de travail SGBD (système de gestion de base de données).
6. Utiliser des données de base de données de votre fournisseur SGBD HA/DR solution tooreplicate.
7. Utilisez toujours la fonction de résolution de noms ; ne vous fiez pas aux adresses IP.
8. Utilisez la compression de base de données hello plus élevée possible. Dans le cas de SQL Server, il s’agit de la compression de page.
9. Veillez à l’aide d’images de SQL Server à partir de hello Azure Marketplace. Si vous utilisez hello SQL Server, vous devez modifier le classement d’instance hello avant d’installer un système SAP NetWeaver dessus.
10. Installer et configurer hello surveillance d’hôte SAP pour Azure, comme décrit dans [Guide de déploiement][deployment-guide].

## <a name="specifics-toosap-ase-on-windows"></a>Spécificités tooSAP ASE sur Windows
À partir de Microsoft Azure, vous pouvez facilement migrer votre tooAzure d’applications SAP ASE existant Machines virtuelles. SAP ASE dans une Machine virtuelle permet de vous tooreduce hello coût total de possession de déploiement, la gestion et maintenance des applications d’entreprise à l’échelle en effectuant une migration facilement ces tooMicrosoft applications Azure. Avec SAP ASE dans une Machine virtuelle Azure, les administrateurs et développeurs peuvent utiliser hello mêmes outils de développement et d’administration qui sont disponibles sur site.

Il existe un contrat SLA pour hello des Machines virtuelles Azure qui se trouve ici : <https://azure.microsoft.com/support/legal/sla>

Nous sommes persuadés que Microsoft Azure effectue très bien les ordinateurs virtuels hébergés dans les offres de virtualisation de cloud public tooother comparaison, mais les résultats peuvent varier. Numéros SAP de hello SAP différents certifié SKU de machine virtuelle sera fournie dans une Note SAP distinct de dimensionnement de SAP [1928533].

Instructions et recommandations de l’utilisation de toohello de tenir compte de stockage Azure, de déploiement de SAP machines virtuelles ou de surveillance SAP s’appliquent toodeployments de SAP ASE conjointement avec les applications SAP comme indiqué dans l’ensemble de hello quatre premiers chapitres de ce document.

### <a name="sap-ase-version-support"></a>Prise en charge des versions SAP ASE
Actuellement, SAP prend en charge SAP ASE version 16.0 pour une utilisation avec les produits SAP Business Suite. Toutes les mises à jour pour le serveur de SAP ASE ou toobe de pilotes JDBC et ODBC utilisé avec SAP Business Suite de produits sont fournis uniquement via hello SAP Service Marketplace à : <https://support.sap.com/swdc>.

Comme pour les installations locales, ne téléchargez pas les mises à jour pour le serveur de SAP ASE hello, ou hello JDBC et des pilotes ODBC directement à partir de sites Web de Sybase. Pour plus d’informations sur les correctifs qui sont pris en charge pour une utilisation avec les produits SAP Business Suite en local et dans les Machines virtuelles Azure, consultez hello suit les Notes SAP :

* [1590719]
* [1973241]

Vous trouverez des informations générales sur l’exécution de SAP Business Suite sur SAP ASE Bonjour [SCN](https://scn.sap.com/community/ase)

### <a name="sap-ase-configuration-guidelines-for-sap-related-sap-ase-installations-in-azure-vms"></a>Instructions de configuration de SAP ASE pour les installations SAP ASE sur des machines virtuelles Azure
#### <a name="structure-of-hello-sap-ase-deployment"></a>Structure de hello SAP ASE déploiement
En fonction de la description générale de hello, SAP ASE exécutables doivent être situés ou installés dans le lecteur du système de disque dur virtuel de base de machine virtuelle hello hello (le lecteur c:\). En règle générale, la plupart des bases de données hello SAP ASE système et les outils n'est pas réellement exploitée forcée par charge de travail SAP NetWeaver. Par conséquent, hello système et bases de données outils (master, model, saptools, sybmgmtdb et sybsystemdb) peuvent demeurer sur hello C:\drive.

Une exception peut être la base de données temporaire hello contenant toutes les tables de travail et les tables temporaires créées par SAP ASE, qui, en cas de certains SAP ERP et toutes les charges BW, peuvent nécessiter plus grand volume de données ou de volume d’opérations d’e/s qui ne rentrent pas dans hello d’origine Disque dur virtuel de base de la machine virtuelle (lecteur c:\).

Hello selon la version de SAPInst/toujours pas pris utilisée système de hello tooinstall, hello de base de données peut contenir :

* une seule base de données tempdb SAP ASE, créée lors de l’installation de SAP ASE ;
* Un tempdb SAP ASE créé par l’installation de SAP ASE et un saptempdb supplémentaire créés par hello routine d’installation SAP
* Un tempdb SAP ASE créé par l’installation de SAP ASE et un tempdb supplémentaires qui a été créé manuellement (par exemple, en suivant la Note SAP [1752266]) configuration requise de toomeet ERP/BW tempdb spécifique

En cas de ERP spécifique ou toutes les charges BW justifiée, dans le respect des tooperformance, périphériques de tempdb hello tookeep de tempdb hello en outre créé (par toujours pas pris ou manuellement) sur un lecteur autre que C:\. Si aucun tempdb supplémentaires n’existe, il est recommandé de toocreate une (Note SAP [1752266]).

Pour ce type hello systèmes étapes suivantes doivent être exécutées pour hello en outre créés tempdb :

* Déplacer hello première tempdb périphérique toohello premier périphérique de la base de données SAP hello
* Ajouter tooeach de périphériques tempdb de hello VHD contenant une unité de base de données SAP hello

Cette tooeither de tempdb de configuration permet de consommer davantage d’espace que le lecteur du système hello est en mesure de tooprovide. Consultez tailles de périphérique hello tempdb sur des systèmes existants qui s’exécutent sur site en tant que référence. Ou bien, une telle configuration permettrait IOPS sur tempdb qui ne peut pas être fourni avec le lecteur du système hello. À nouveau les systèmes qui sont exécutent localement peuvent être utilisés toomonitor d’e/s des charges de travail sur tempdb.

Ne placez jamais tous les périphériques SAP ASE sur hello lecteur D:\ de hello machine virtuelle. Cela s’applique également toohello tempdb, même si les objets hello conservées dans tempdb de hello sont temporaires.

#### <a name="impact-of-database-compression"></a>Impact de la compression de base de données
Dans les configurations où la bande passante d’e/s peut devenir un facteur de limitation, toutes les mesures qui réduisent les IOPS peuvent aider les charges de travail toostretch hello exécutée dans un scénario IaaS comme Azure. Par conséquent, il est fortement recommandé toomake assurer que la compression de SAP ASE est utilisée avant de télécharger un tooAzure de base de données SAP existante.

compression de tooperform Hello recommandation avant de le télécharger tooAzure si elle n’est pas implémentée est donnée hors pour plusieurs raisons :

* Hello tooAzure toobe téléchargé de données est inférieure
* Durée Hello d’exécution de la compression hello est plus courte, en supposant que possible d’utiliser un matériel plus performant avec plus de processeurs ou de bande passante d’e/s ou moins d’e/s latence locale
* De plus petite taille de base de données peut entraîner des coûts accessible sans pour l’allocation de disque

La compression des données et des éléments LOB fonctionne au sein d’une machine virtuelle hébergée dans Azure Virtual Machines comme en local. Pour plus d’informations sur l’utilisation de toocheck si la compression est déjà dans un environnement app service SAP existante base de données Vérifiez la Note SAP [1750510].

#### <a name="using-dbacockpit-toomonitor-database-instances"></a>À l’aide d’Instances de base de données DBACockpit toomonitor
Pour les systèmes SAP qui sont à l’aide de SAP ASE en tant que plateforme de base de données, hello DBACockpit est accessible en tant que des fenêtres de navigateur intégré dans la transaction DBACockpit ou Webdynpro. Toutefois hello toutes les fonctionnalités de surveillance et administration hello est disponible dans la mise en œuvre de Webdynpro hello Hello DBACockpit.

En tant que locale systèmes que plusieurs étapes sont requises tooenable toutes les fonctionnalités de SAP NetWeaver utilisée par l’implémentation de Webdynpro hello Hello DBACockpit. Veuillez suivre la Note SAP [1245200] tooenable hello d’utilisation de webdynpros et générer hello requis ceux. Lorsque des instructions hello suivantes Bonjour au-dessus de notes, avec que vous devez également configurer hello Gestionnaire des communications Internet (icm) hello toobe ports utilisé pour les connexions http et https. paramètre par défaut de Hello pour http ressemble à ceci :

> icm/server_port_0 = PROT=HTTP,PORT=8000,PROCTIMEOUT=600,TIMEOUT=600
>
> icm/server_port_1 = PROT=HTTPS,PORT=443$$,PROCTIMEOUT=600,TIMEOUT=600
>
>

et les liens hello générés dans la transaction DBACockpit toothis similaire :

> https://`<fullyqualifiedhostname`>:44300/sap/bc/webdynpro/sap/dba_cockpit
>
> http://`<fullyqualifiedhostname`>:8000/sap/bc/webdynpro/sap/dba_cockpit
>
>

Selon si et comment l’hébergement de Machine virtuelle Azure Bonjour Bonjour système SAP est connecté via le site à site, multisites ou ExpressRoute (déploiement entre différents locaux), vous devez toomake que ce ICM utilise un nom d’hôte complet qui peut être résolu sur hello ordinateur sur lequel vous essayez tooopen hello DBACockpit à partir de. Consultez la Note SAP [773830] toounderstand comment ICM détermine hello du nom d’hôte en fonction des paramètres de profil et paramètre de jeu icm/host_name_full explicitement si nécessaire.

Si vous avez déployé hello machine virtuelle dans un scénario de Cloud uniquement sans connectivité intersite entre Azure et locaux, vous devez toodefine une adresse IP publique et un domainlabel. puis, format Hello de hello nom DNS public du hello VM ressemble à ceci :

> `<custom domainlabel`&gt;.`<azure region`&gt;.cloudapp.azure.com
>
>

Plus de détails liés trouverez le nom DNS de toohello [ici][virtual-machines-azurerm-versus-azuresm].

Paramètre hello SAP profil paramètre icm/host_name_full toohello nom DNS du lien de hello hello Azure VM peut ressembler à :

> https://mydomainlabel.westeurope.cloudapp.net:44300/sap/bc/webdynpro/sap/dba_cockpit
>
> http://mydomainlabel.westeurope.cloudapp.net:8000/sap/bc/webdynpro/sap/dba_cockpit
>
>

Dans ce cas vous devez toomake Assurez-vous de :

* Ajouter des règles de trafic entrant toohello groupe de sécurité réseau Bonjour portail Azure pour les ports TCP/IP hello utilisé toocommunicate avec ICM
* Ajouter la configuration du pare-feu Windows toohello règles de trafic entrant pour hello TCP/IP ports utilisés toocommunicate avec hello ICM

Pour un moyen automatisé importé de toutes les corrections disponibles, il est recommandé de tooperiodically appliquer hello correction collection SAP Remarque tooyour applicable SAP version :

* [1558958]
* [1619967]
* [1882376]

Vous trouverez plus d’informations sur le Cockpit de DBA pour SAP ASE Bonjour suit les Notes SAP :

* [1605680]
* [1757924]
* [1757928]
* [1758182]
* [1758496]    
* [1814258]
* [1922555]
* [1956005]

#### <a name="backuprecovery-considerations-for-sap-ase"></a>Considérations relatives à la sauvegarde/restauration pour SAP ASE
Lors du déploiement de SAP ASE dans Azure, votre méthodologie de sauvegarde doit être passée en revue. Même si le système de hello n’est pas un système de production, base de données SAP hello hébergé par SAP ASE doit être sauvegardée régulièrement. Étant donné que le stockage Azure conserve trois images, une sauvegarde est dorénavant moins nécessaire dans le toocompensating en ce qui concerne une panne du stockage. Bonjour la raison principale pour la gestion d’un plan de sauvegarde et de restauration correct est plus que vous pouvez compenser ce décalage erreurs manuelles/logiques en fournissant le point de restauration de temps. Objectif de hello est tooeither utilisation sauvegardes toorestore hello base de données principale tooa certain de points de temps ou toouse sauvegardes hello dans Azure tooseed un autre système en copiant la base de données existante hello. Par exemple, vous pouvez transférer une installation de système de couche 3 à 2 couches SAP configuration tooa Hello même système en restaurant une sauvegarde.

Sauvegarde et restauration d’une base de données dans Azure fonctionne même hello façon comme il le fait sur site. Consultez les notes SAP suivantes :

* [1588316]
* [1585981]

pour plus d’informations sur la création de configurations d’images mémoire et la planification des sauvegardes. Selon vos besoins, vous pouvez configurer et de stratégie de base de données et journal exporte toodisk sur l’un des hello existante des disques durs virtuels ou ajouter un disque dur virtuel supplémentaire pour la sauvegarde de hello.  risque de hello tooreduce de perte de données en cas d’erreur, il est recommandé de toouse un disque dur virtuel où se trouve aucun périphérique de la base de données.

Outre les données et la compression des éléments LOB, SAP ASE propose la compression de sauvegarde. toooccupy espace avec hello database et log dumps il est recommandé de toouse de compression de la sauvegarde. Pour plus d’informations, voir la Note de SAP [1588316] . La compression de sauvegarde de hello est également essentiel tooreduce hello toobe données transférée si vous planifiez des sauvegardes toodownload ou disques durs virtuels contenant des vidages de sauvegarde à partir de hello tooon local Machine virtuelle Azure.

N’utilisez pas le lecteur D:\ comme destination des images mémoire de bases de données ou de journaux.

#### <a name="performance-considerations-for-backupsrestores"></a>Considérations sur les performances des sauvegardes/restaurations
Comme dans les déploiements de système nu, les performances de sauvegarde/restauration sont dépend du nombre de volumes peut être lues en parallèle et quelles débit hello de ces volumes peut être. En outre, hello consommation d’UC utilisée par la compression de sauvegarde peut jouent un rôle significatif sur les machines virtuelles avec uniquement les threads de l’UC de too8. Par conséquent, on peut partir des hypothèses suivantes :

* Hello moins hello nombre de disques durs virtuels utilisés périphériques de base de données toostore hello, hello plus petites hello débit global de lecture
* Hello plus petit nombre de hello de threads d’UC Bonjour VM, hello plus grave impact hello de compression de la sauvegarde
* Bonjour de sauvegarde vers Hello moins toowrite de cibles (Stripe répertoires, disques durs virtuels), hello moindre débit de hello

nombre de hello tooincrease de cibles toowrite toothere existe deux options qui peuvent être utilisé/combinée selon vos besoins :

* Répartition du volume de cible de sauvegarde hello sur plusieurs disques durs virtuels montés dans un ordre tooimprove hello e/s de débit sur ce volume agrégé par bandes
* Création d’une configuration du vidage sur niveau SAP ASE qui utilise plusieurs cible répertoire toowrite hello de vidage à

L’agrégation d’un volume par bandes sur plusieurs disques durs virtuels montés a été évoquée précédemment dans ce guide. Pour plus d’informations sur l’utilisation de plusieurs répertoires dans la configuration du vidage SAP ASE hello consultez la documentation du toohello sur sp_config_dump de procédure stockée qui est la configuration du vidage hello toocreate utilisés sur hello [Sybase Infocenter](http://infocenter.sybase.com/help/index.jsp).

### <a name="disaster-recovery-with-azure-vms"></a>Récupération d’urgence avec les machines virtuelles Azure
#### <a name="data-replication-with-sap-sybase-replication-server"></a>Réplication de données avec le serveur de réplication Sybase SAP
Avec hello SAP Sybase serveur de réplication SAP ASE regroupe solution de secours semi-automatique tootransfer de base de données transactions tooa éloigné asynchrone.

installation de Hello et du fonctionnement de SRS fonctionne également fonctionnellement dans une machine virtuelle hébergée dans Azure Virtual Machine Services, comme il le fait sur site.

La fonction ASE HADR (haute disponibilité et récupération d’urgence) via le serveur de réplication SAP est prévue avec une version ultérieure. Elle sera testée et publiée pour les plateformes Microsoft Azure dès qu’elle sera disponible.

## <a name="specifics-toosap-ase-on-linux"></a>Spécificités tooSAP ASE sur Linux
À partir de Microsoft Azure, vous pouvez facilement migrer votre tooAzure d’applications SAP ASE existant Machines virtuelles. SAP ASE dans une Machine virtuelle permet de vous tooreduce hello coût total de possession de déploiement, la gestion et maintenance des applications d’entreprise à l’échelle en effectuant une migration facilement ces tooMicrosoft applications Azure. Avec SAP ASE dans une Machine virtuelle Azure, les administrateurs et développeurs peuvent utiliser hello mêmes outils de développement et d’administration qui sont disponibles sur site.

Pour le déploiement de machines virtuelles de Azure tooknow important ses hello SLA officiel qui se trouve ici : <https://azure.microsoft.com/support/legal/sla>

Les informations de dimensionnement SAP et une liste des références de machines virtuelles certifiées SAP seront fournies dans la Note de SAP [1928533]. Des documents supplémentaires sur le dimensionnement SAP pour les machines virtuelles Azure sont disponibles ici <http://blogs.msdn.com/b/saponsqlserver/archive/2015/06/19/how-to-size-sap-systems-running-on-azure-vms.aspx> et ici <http://blogs.msdn.com/b/saponsqlserver/archive/2015/12/01/new-white-paper-on-sizing-sap-solutions-on-azure-public-cloud.aspx>

Instructions et recommandations de l’utilisation de toohello de tenir compte de stockage Azure, de déploiement de SAP machines virtuelles ou de surveillance SAP s’appliquent toodeployments de SAP ASE conjointement avec les applications SAP comme indiqué dans l’ensemble de hello quatre premiers chapitres de ce document.

Hello deux de Notes SAP suivantes incluent des informations générales sur ASE sur Linux et ASE Bonjour Cloud :

* [2134316]
* [1941500]

### <a name="sap-ase-version-support"></a>Prise en charge des versions SAP ASE
Actuellement, SAP prend en charge SAP ASE version 16.0 pour une utilisation avec les produits SAP Business Suite. Toutes les mises à jour pour le serveur de SAP ASE ou toobe de pilotes JDBC et ODBC utilisé avec SAP Business Suite de produits sont fournis uniquement via hello SAP Service Marketplace à : <https://support.sap.com/swdc>.

Comme pour les installations locales, ne téléchargez pas les mises à jour pour le serveur de SAP ASE hello, ou hello JDBC et des pilotes ODBC directement à partir de sites Web de Sybase. Pour plus d’informations sur les correctifs qui sont pris en charge pour une utilisation avec les produits SAP Business Suite en local et dans les Machines virtuelles Azure, consultez hello suit les Notes SAP :

* [1590719]
* [1973241]

Vous trouverez des informations générales sur l’exécution de SAP Business Suite sur SAP ASE Bonjour [SCN](https://scn.sap.com/community/ase)

### <a name="sap-ase-configuration-guidelines-for-sap-related-sap-ase-installations-in-azure-vms"></a>Instructions de configuration de SAP ASE pour les installations SAP ASE sur des machines virtuelles Azure
#### <a name="structure-of-hello-sap-ase-deployment"></a>Structure de hello SAP ASE déploiement
En fonction de la description générale de hello, SAP ASE exécutables doivent être situés ou installés dans le système de fichiers racine hello Hello VM (/sybase). En règle générale, la plupart des bases de données hello SAP ASE système et les outils n'est pas réellement exploitée forcée par charge de travail SAP NetWeaver. Par conséquent, hello système et bases de données outils (master, model, saptools, sybmgmtdb et sybsystemdb) peuvent rester sur le système de fichiers racine hello également.

Une exception peut être la base de données temporaire hello contenant toutes les tables de travail et les tables temporaires créées par SAP ASE, qui, en cas de certains SAP ERP et toutes les charges BW, peuvent nécessiter plus grand volume de données ou de volume d’opérations d’e/s qui ne rentrent pas dans hello d’origine Disque de système d’exploitation de l’ordinateur virtuel.

Hello selon la version de SAPInst/toujours pas pris utilisée système de hello tooinstall, hello de base de données peut contenir :

* une seule base de données tempdb SAP ASE, créée lors de l’installation de SAP ASE ;
* Un tempdb SAP ASE créé par l’installation de SAP ASE et un saptempdb supplémentaire créés par hello routine d’installation SAP
* Un tempdb SAP ASE créé par l’installation de SAP ASE et un tempdb supplémentaires qui a été créé manuellement (par exemple, en suivant la Note SAP [1752266]) configuration requise de toomeet ERP/BW tempdb spécifique

En cas de ERP spécifique ou toutes les charges BW il est judicieux, dans le respect des tooperformance, les appareils tookeep hello tempdb de tempdb hello en outre créé (par toujours pas pris ou manuellement) sur un système de fichiers distinct qui peut être représenté par un disque de données Azure unique ou un volume RAID Linux fractionnement de plusieurs disques de données Azure. Si aucun tempdb supplémentaires n’existe, il est recommandé de toocreate une (Note SAP [1752266]).

Pour ce type hello systèmes étapes suivantes doivent être exécutées pour hello en outre créés tempdb :

* Déplacer hello première tempdb Active toohello premier système de fichiers de base de données SAP hello
* Ajouter tooeach de répertoires tempdb de hello disques durs virtuels contenant un système de fichiers de base de données SAP hello

Cette tooeither de tempdb de configuration permet de consommer davantage d’espace que le lecteur du système hello est en mesure de tooprovide. Consultez tailles de répertoire hello tempdb sur des systèmes existants qui s’exécutent sur site en tant que référence. Ou bien, une telle configuration permettrait IOPS sur tempdb qui ne peut pas être fourni avec le lecteur du système hello. À nouveau les systèmes qui sont exécutent localement peuvent être utilisés toomonitor d’e/s des charges de travail sur tempdb.

Ne placez jamais les répertoires SAP ASE sur/mnt ou/mnt/Resource Hello machine virtuelle. Cela s’applique également toohello tempdb, même si les objets hello conservées dans tempdb de hello sont temporaires étant/mnt ou/mnt/Resource un espace temporaire de machine virtuelle Azure par défaut qui n’est pas persistant. Vous trouverez plus de détails sur hello espace temporaire de machine virtuelle Azure dans [cet article][virtual-machines-linux-how-to-attach-disk]

#### <a name="impact-of-database-compression"></a>Impact de la compression de base de données
Dans les configurations où la bande passante d’e/s peut devenir un facteur de limitation, toutes les mesures qui réduisent les IOPS peuvent aider les charges de travail toostretch hello exécutée dans un scénario IaaS comme Azure. Par conséquent, il est fortement recommandé toomake assurer que la compression de SAP ASE est utilisée avant de télécharger un tooAzure de base de données SAP existante.

compression de tooperform Hello recommandation avant de le télécharger tooAzure si elle n’est pas implémentée est donnée hors pour plusieurs raisons :

* Hello tooAzure toobe téléchargé de données est inférieure
* Durée Hello d’exécution de la compression hello est plus courte, en supposant que possible d’utiliser un matériel plus performant avec plus de processeurs ou de bande passante d’e/s ou moins d’e/s latence locale
* De plus petite taille de base de données peut entraîner des coûts accessible sans pour l’allocation de disque

La compression des données et des éléments LOB fonctionne au sein d’une machine virtuelle hébergée dans Azure Virtual Machines comme en local. Pour plus d’informations sur l’utilisation de toocheck si la compression est déjà dans un environnement app service SAP existante base de données Vérifiez la Note SAP [1750510]. Pour plus d’informations sur la compression des bases de données, voir la Note de SAP [2121797] .

#### <a name="using-dbacockpit-toomonitor-database-instances"></a>À l’aide d’Instances de base de données DBACockpit toomonitor
Pour les systèmes SAP qui sont à l’aide de SAP ASE en tant que plateforme de base de données, hello DBACockpit est accessible en tant que des fenêtres de navigateur intégré dans la transaction DBACockpit ou Webdynpro. Toutefois hello toutes les fonctionnalités de surveillance et administration hello est disponible dans la mise en œuvre de Webdynpro hello Hello DBACockpit.

En tant que locale systèmes que plusieurs étapes sont requises tooenable toutes les fonctionnalités de SAP NetWeaver utilisée par l’implémentation de Webdynpro hello Hello DBACockpit. Veuillez suivre la Note SAP [1245200] tooenable hello d’utilisation de webdynpros et générer hello requis ceux. Lorsque des instructions hello suivantes Bonjour au-dessus de notes, avec que vous devez également configurer hello Gestionnaire des communications Internet (icm) hello toobe ports utilisé pour les connexions http et https. paramètre par défaut de Hello pour http ressemble à ceci :

> icm/server_port_0 = PROT=HTTP,PORT=8000,PROCTIMEOUT=600,TIMEOUT=600
>
> icm/server_port_1 = PROT=HTTPS,PORT=443$$,PROCTIMEOUT=600,TIMEOUT=600
>
>

et les liens hello générés dans la transaction DBACockpit toothis similaire :

> https://`<fullyqualifiedhostname`>:44300/sap/bc/webdynpro/sap/dba_cockpit
>
> http://`<fullyqualifiedhostname`>:8000/sap/bc/webdynpro/sap/dba_cockpit
>
>

Selon si et comment l’hébergement de Machine virtuelle Azure Bonjour Bonjour système SAP est connecté via le site à site, multisites ou ExpressRoute (déploiement entre différents locaux), vous devez toomake que ce ICM utilise un nom d’hôte complet qui peut être résolu sur hello ordinateur sur lequel vous essayez tooopen hello DBACockpit à partir de. Consultez la Note SAP [773830] toounderstand comment ICM détermine hello du nom d’hôte en fonction des paramètres de profil et paramètre de jeu icm/host_name_full explicitement si nécessaire.

Si vous avez déployé hello machine virtuelle dans un scénario de Cloud uniquement sans connectivité intersite entre Azure et locaux, vous devez toodefine une adresse IP publique et un domainlabel. puis, format Hello de hello nom DNS public du hello VM ressemble à ceci :

> `<custom domainlabel`&gt;.`<azure region`&gt;.cloudapp.azure.com
>
>

Plus de détails liés trouverez le nom DNS de toohello [ici][virtual-machines-azurerm-versus-azuresm].

Paramètre hello SAP profil paramètre icm/host_name_full toohello nom DNS du lien de hello hello Azure VM peut ressembler à :

> https://mydomainlabel.westeurope.cloudapp.net:44300/sap/bc/webdynpro/sap/dba_cockpit
>
> http://mydomainlabel.westeurope.cloudapp.net:8000/sap/bc/webdynpro/sap/dba_cockpit
>
>

Dans ce cas vous devez toomake Assurez-vous de :

* Ajouter des règles de trafic entrant toohello groupe de sécurité réseau Bonjour portail Azure pour les ports TCP/IP hello utilisé toocommunicate avec ICM
* Ajouter la configuration du pare-feu Windows toohello règles de trafic entrant pour hello TCP/IP ports utilisés toocommunicate avec hello ICM

Pour un moyen automatisé importé de toutes les corrections disponibles, il est recommandé de tooperiodically appliquer hello correction collection SAP Remarque tooyour applicable SAP version :

* [1558958]
* [1619967]
* [1882376]

Vous trouverez plus d’informations sur le Cockpit de DBA pour SAP ASE Bonjour suit les Notes SAP :

* [1605680]
* [1757924]
* [1757928]
* [1758182]
* [1758496]    
* [1814258]
* [1922555]
* [1956005]

#### <a name="backuprecovery-considerations-for-sap-ase"></a>Considérations relatives à la sauvegarde/restauration pour SAP ASE
Lors du déploiement de SAP ASE dans Azure, votre méthodologie de sauvegarde doit être passée en revue. Même si le système de hello n’est pas un système de production, base de données SAP hello hébergé par SAP ASE doit être sauvegardée régulièrement. Étant donné que le stockage Azure conserve trois images, une sauvegarde est dorénavant moins nécessaire dans le toocompensating en ce qui concerne une panne du stockage. Bonjour la raison principale pour la gestion d’un plan de sauvegarde et de restauration correct est plus que vous pouvez compenser ce décalage erreurs manuelles/logiques en fournissant le point de restauration de temps. Objectif de hello est tooeither utilisation sauvegardes toorestore hello base de données principale tooa certain de points de temps ou toouse sauvegardes hello dans Azure tooseed un autre système en copiant la base de données existante hello. Par exemple, vous pouvez transférer une installation de système de couche 3 à 2 couches SAP configuration tooa Hello même système en restaurant une sauvegarde.

Sauvegarde et restauration d’une base de données dans Azure fonctionne même hello façon comme il le fait sur site. Consultez les notes SAP suivantes :

* [1588316]
* [1585981]

pour plus d’informations sur la création de configurations d’images mémoire et la planification des sauvegardes. Selon vos besoins, vous pouvez configurer et de stratégie de base de données et journal exporte toodisk sur l’un des hello existante des disques durs virtuels ou ajouter un disque dur virtuel supplémentaire pour la sauvegarde de hello.  risque de hello tooreduce de perte de données en cas d’erreur, il est recommandé de toouse un disque dur virtuel où se trouve aucun fichier ou répertoire de base de données.

Outre les données et la compression des éléments LOB, SAP ASE propose la compression de sauvegarde. toooccupy espace avec hello database et log dumps il est recommandé de toouse de compression de la sauvegarde. Pour plus d’informations, voir la Note de SAP [1588316] . La compression de sauvegarde de hello est également essentiel tooreduce hello toobe données transférée si vous planifiez des sauvegardes toodownload ou disques durs virtuels contenant des vidages de sauvegarde à partir de hello tooon local Machine virtuelle Azure.

N’utilisez pas d’espace temporaire/mnt de la machine virtuelle Azure hello ou/mnt/Resource comme destination de vidage de base de données ou journal.

#### <a name="performance-considerations-for-backupsrestores"></a>Considérations sur les performances des sauvegardes/restaurations
Comme dans les déploiements de système nu, les performances de sauvegarde/restauration sont dépend du nombre de volumes peut être lues en parallèle et quelles débit hello de ces volumes peut être. En outre, hello consommation d’UC utilisée par la compression de sauvegarde peut jouent un rôle significatif sur les machines virtuelles avec uniquement les threads de l’UC de too8. Par conséquent, on peut partir des hypothèses suivantes :

* Hello moins hello nombre de disques durs virtuels utilisés périphériques de base de données toostore hello, hello plus petites hello débit global de lecture
* Hello plus petit nombre de hello de threads d’UC Bonjour VM, hello plus grave impact hello de compression de la sauvegarde
* Bonjour de sauvegarde vers Hello moins toowrite de cibles (Linux logiciel RAID, disques durs virtuels), hello moindre débit de hello

nombre de hello tooincrease de cibles toowrite toothere existe deux options qui peuvent être utilisé/combinée selon vos besoins :

* Répartition du volume de cible de sauvegarde hello sur plusieurs disques durs virtuels montés dans un ordre tooimprove hello e/s de débit sur ce volume agrégé par bandes
* Création d’une configuration du vidage sur niveau SAP ASE qui utilise plusieurs cible répertoire toowrite hello de vidage à

L’agrégation d’un volume par bandes sur plusieurs disques durs virtuels montés a été évoquée précédemment dans ce guide. Pour plus d’informations sur l’utilisation de plusieurs répertoires dans la configuration du vidage SAP ASE hello consultez la documentation du toohello sur sp_config_dump de procédure stockée qui est la configuration du vidage hello toocreate utilisés sur hello [Sybase Infocenter](http://infocenter.sybase.com/help/index.jsp).

### <a name="disaster-recovery-with-azure-vms"></a>Récupération d’urgence avec les machines virtuelles Azure
#### <a name="data-replication-with-sap-sybase-replication-server"></a>Réplication de données avec le serveur de réplication Sybase SAP
Avec hello SAP Sybase serveur de réplication SAP ASE regroupe solution de secours semi-automatique tootransfer de base de données transactions tooa éloigné asynchrone.

installation de Hello et du fonctionnement de SRS fonctionne également fonctionnellement dans une machine virtuelle hébergée dans Azure Virtual Machine Services, comme il le fait sur site.

La fonction ASE HADR (haute disponibilité et récupération d’urgence) via le serveur de réplication SAP n’est PAS prise en charge pour le moment. Il peut être testé avec et publiée pour les plateformes Microsoft Azure Bonjour futures.

## <a name="specifics-toooracle-database-on-windows"></a>Caractéristiques tooOracle de base de données sur Windows
Depuis midyear 2013, le logiciel Oracle prend en charge toorun Oracle sur Microsoft Windows Hyper-V et Azure. Lisez cet article de tooget plus d’informations sur la prise en charge générale de hello de Windows Hyper-V et Azure par Oracle : <https://blogs.oracle.com/cloud/entry/oracle_and_microsoft_join_forces>

Après la prise en charge générale hello, scénario spécifique hello dans les applications SAP en exploitant des bases de données Oracle est également pris en charge. Détails sont nommés dans cette partie de document de hello.

### <a name="oracle-version-support"></a>Prise en charge des versions Oracle
Tous les détails sur les versions d’Oracle et les versions de système d’exploitation correspondantes qui sont pris en charge pour SAP en cours d’exécution sur Oracle sur des Machines virtuelles Azure sont accessibles dans hello suivant la Note SAP [2039619]

Pour des informations générales sur l’exécution de SAP Business Suite sur Oracle dans SCN, voir : <https://scn.sap.com/community/oracle>

### <a name="oracle-configuration-guidelines-for-sap-installations-in-azure-vms"></a>Instructions de configuration Oracle pour les installations SAP sur des machines virtuelles Azure
#### <a name="storage-configuration"></a>Configuration du stockage
Une seule instance Oracle utilisant les disques au format NTFS est prise en charge. Tous les fichiers de base de données doivent être stockées sur le système de fichiers NTFS hello basée sur des disques de disque dur virtuel. Ces VHD sont monté toohello machine virtuelle Azure et sont basées sur le stockage d’objets BLOB Azure Page (<https://msdn.microsoft.com/library/azure/ee691964.aspx>).
Tous les types de lecteurs réseau ou de partages distants tels que les services de fichiers Azure :

* <https://blogs.msdn.com/b/windowsazurestorage/archive/2014/05/12/introducing-microsoft-azure-file-service.aspx>
* <https://blogs.msdn.com/b/windowsazurestorage/archive/2014/05/27/persisting-connections-to-microsoft-azure-files.aspx>

ne sont **PAS** pris en charge pour les fichiers de base de données Oracle !

À l’aide de disques durs virtuels de Azure basé sur le stockage d’objets BLOB Azure Page hello instructions effectuées dans ce document dans le chapitre [mise en cache pour les machines virtuelles et disques durs virtuels] [ dbms-guide-2.1] et [Microsoft Azure Storage] [ dbms-guide-2.3] appliquer toodeployments avec hello de base de données Oracle.

Comme expliqué plus haut dans la partie générale de hello du document de hello, les quotas sur le débit d’e/s pour les disques durs virtuels de Azure existent. les quotas exacte Hello selon le type de machine virtuelle hello servent. Une liste des types de machines virtuelles avec leurs quotas est disponible [ici][virtual-machines-sizes]

tooidentify hello pris en charge les types de machine virtuelle Azure, consultez tooSAP Remarque [1928533]

Tant que hello actuel quota d’IOPS par disque répond aux exigences de hello, il est possible toostore tous les fichiers hello DB sur un seul monté le disque dur virtuel de Azure.

Si plus d’IOPS sont requis, il est fortement recommandé de toouse fenêtre les Pools de stockage (uniquement disponible dans Windows Server 2012 et versions ultérieures) ou Windows en distribuant pour Windows 2008 R2 toocreate un périphérique logique big sur plusieurs disques VHD montés. Voir également le chapitre [RAID logiciel][dbms-guide-2.2] de ce document. Cette approche simplifie l’espace disque de hello administration toomanage généraux hello et évite les efforts hello toomanually distribuer les fichiers sur plusieurs disques durs virtuels montés.

#### <a name="backup--restore"></a>Sauvegarde / restauration
Pour la sauvegarde / restauration, hello SAP BR * Tools pour Oracle sont prises en charge dans hello même façon que sur standard les systèmes d’exploitation Windows Server et Hyper-V. Oracle, Gestionnaire de récupération (RMAN) est également pris en charge pour toodisk de sauvegardes et de restauration à partir du disque.

#### <a name="high-availability"></a>Haute disponibilité
[comment]: <> (lien fait référence tooASM)
Oracle Data Guard est pris en charge à des fins de haute disponibilité et de récupération d’urgence. Pour plus d’informations, consultez [cette][virtual-machines-windows-classic-configure-oracle-data-guard] documentation.

#### <a name="other"></a>Autres
Toutes les autres rubriques générales telles que la surveillance de groupes à haute disponibilité Azure ou SAP s’appliquent comme décrit dans hello trois premiers chapitres de ce document pour les déploiements d’ordinateurs virtuels avec hello de base de données Oracle.

## <a name="specifics-for-hello-sap-maxdb-database-on-windows"></a>Caractéristiques de hello de base de données SAP MaxDB sur Windows
### <a name="sap-maxdb-version-support"></a>Prise en charge des versions SAP MaxDB
Actuellement, SAP prend en charge SAP MaxDB version 7.9 pour une utilisation avec les produits reposant sur SAP NetWeaver dans Azure. Toutes les mises à jour pour le serveur de SAP MaxDB ou toobe de pilotes JDBC et ODBC utilisé avec des produits basés sur SAP NetWeaver sont fournis uniquement par le biais de hello SAP Service Marketplace à <https://support.sap.com/swdc>.
Vous trouverez des informations générales sur l’exécution de SAP NetWeaver sur SAP MaxDB à l’adresse <https://scn.sap.com/community/maxdb>.

### <a name="supported-microsoft-windows-versions-and-azure-vm-types-for-sap-maxdb-dbms"></a>Versions de Microsoft Windows et types de machines virtuelles Azure pris en charge pour SGBD SAP MaxDB
version de Microsoft Windows toofind hello pris en charge pour les SGBD MaxDB de SAP sur Azure, consultez :

* [Tableau de disponibilité des produits SAP][sap-pam]
* Note SAP [1928533]

Il est vivement recommandé toouse version la plus récente hello hello système d’exploitation Microsoft Windows, qui est Microsoft Windows 2012 R2.

### <a name="available-sap-maxdb-documentation"></a>Documentation SAP MaxDB disponible
Vous trouverez la liste hello mis à jour de la documentation de SAP MaxDB Bonjour suivant la Note SAP [767598 ]

### <a name="sap-maxdb-configuration-guidelines-for-sap-installations-in-azure-vms"></a>Instructions de configuration SAP MaxDB pour les installations SAP sur des machines virtuelles Azure
#### <a name="b48cfe3b-48e9-4f5b-a783-1d29155bd573"></a>Configuration du stockage
Meilleures pratiques de stockage Azure pour SAP MaxDB suivent les recommandations générales hello mentionnées dans le chapitre [Structure d’un déploiement SGBDR][dbms-guide-2].

> [!IMPORTANT]
> Comme d’autres bases de données, SAP MaxDB possède des données et des fichiers journaux. Toutefois, dans la terminologie de SAP MaxDB terme correct de hello est « volume » (pas « fichier »). Par exemple, il existe des volumes de données et des volumes de journaux SAP MaxDB. Ne les confondez pas avec les volumes de disque du système d’exploitation.
>
>

En bref, voici que vous avez à faire :

* Définir le compte de stockage Azure hello qui contient trop de hello SAP MaxDB journaux et des données des volumes (c'est-à-dire des fichiers)**Local stockage redondant (LRS)** comme indiqué dans le chapitre [Microsoft Azure Storage] [ dbms-guide-2.3].
* Chemin d’accès des e/s hello distincts pour les volumes de données SAP MaxDB (c'est-à-dire des fichiers) à partir du chemin d’accès d’e/s de hello pour les volumes de journal (autrement dit, les fichiers). Cela signifie que que des volumes de données SAP MaxDB (c'est-à-dire des fichiers) ont toobe installé sur un lecteur logique SAP MaxDB des volumes de journal (autrement dit, les fichiers) ont toobe installé sur un autre lecteur logique.
* Définir hello correct des fichiers de mise en cache pour chaque objet blob Azure, selon si vous l’utilisez pour SAP MaxDB volumes de données ou de journal (c'est-à-dire des fichiers), et que vous utilisez Azure Standard ou le stockage Azure Premium, comme décrit dans le chapitre [mise en cache pour les machines virtuelles] [ dbms-guide-2.1].
* Tant que hello actuel quota d’IOPS par disque répond aux exigences de hello, il est possible de toostore tous les volumes de données hello sur un disque dur virtuel monté Azure unique et également de stocker tous les volumes de journal de base de données sur un autre disque VHD Azure monté unique.
* Si plus d’IOPS et/ou espace est requis, il est fortement recommandé de Pools de stockage de fenêtre toouse Microsoft (uniquement disponible dans Microsoft Windows Server 2012 et versions ultérieures) ou Microsoft Windows pour Microsoft Windows 2008 R2 toocreate en distribuant un périphérique logique volumineux sur plusieurs disques VHD montés. Voir également le chapitre [RAID logiciel][dbms-guide-2.2] de ce document. Cette approche simplifie l’espace disque de hello administration toomanage généraux hello et évite les efforts de hello de distribution manuellement des fichiers sur plusieurs disques durs virtuels montés.
* Pour les exigences d’e/s la plus élevées hello, vous pouvez utiliser le stockage Azure Premium, qui est disponible sur la série DS et les machines virtuelles de série GS.

![Configuration de référence de la machine virtuelle IaaS Azure pour SGBD SAP MaxDB][dbms-guide-figure-600]

#### <a name="23c78d3b-ca5a-4e72-8a24-645d141a3f5d"></a>Sauvegarde et restauration
Lors du déploiement de SAP MaxDB dans Azure, vous devez passer en revue votre méthodologie de sauvegarde. Même si le système de hello n’est pas un système de production, base de données SAP hello hébergé par SAP MaxDB doit être sauvegardée régulièrement. Étant donné qu’Azure Storage conserve trois images, une sauvegarde est désormais moins importante en termes de protection de votre système contre les défaillances de stockage, ou les défaillances opérationnelles ou administratives plus sérieuses. Hello recherché pour maintenir une sauvegarde correcte et le plan de restauration est afin que vous pouvez compenser pour les erreurs de logiques ou manuelles en fournissant des fonctionnalités de récupération de point-à-temps. Donc hello objectif consiste tooeither utilisation sauvegardes toorestore hello de base de données tooa certains de points de temps ou toouse sauvegardes hello dans Azure tooseed un autre système en copiant la base de données existante hello. Par exemple, vous pouvez transférer une installation de système de couche 3 à 2 couches SAP configuration tooa Hello même système en restaurant une sauvegarde.

Sauvegarde et restauration d’une base de données Azure works hello comme il le fait pour les systèmes locaux, vous pouvez donc utiliser standard SAP MaxDB outils, qui sont décrites dans un des documents de documentation de SAP MaxDB hello sauvegarde/restauration répertoriés dans la Note SAP [767598 ].

#### <a name="77cd2fbb-307e-4cbf-a65f-745553f72d2c"></a>Considérations sur les performances de sauvegarde et de restauration
Comme dans les déploiements de système nu, les performances de sauvegarde et de restauration sont dépend du nombre de volumes peut être lues en parallèle et hello débit de ces volumes. En outre, hello consommation d’UC utilisée par la compression de sauvegarde peut jouer un rôle significatif sur les machines virtuelles avec des threads de processeur too8. Par conséquent, on peut partir des hypothèses suivantes :

* Hello plus petit nombre de hello de périphériques de base de données de disques durs virtuels utilisés toostore hello, hello inférieur hello globale débit de lecture
* Hello plus petit nombre de hello de threads d’UC Bonjour VM, hello plus grave impact hello de compression de la sauvegarde
* Hello moins sauvegarde hello toowrite de cibles (Stripe répertoires, disques durs virtuels) pour la réduction du débit hello hello

nombre de hello tooincrease de cible toowrite à, il existe deux options que vous pouvez utiliser, éventuellement en combinaison, selon vos besoins :

* Dédier des volumes distincts pour la sauvegarde
* Volume de cible de sauvegarde hello en distribuant sur plusieurs disques durs virtuels montés dans le débit d’IOPS ordre tooimprove hello sur ce volume de disque agrégé par bandes
* Disposer d’unités de disque logiques dédiées distinctes pour les éléments suivants :
  * Volumes de sauvegarde SAP MaxDB (c’est-à-dire les fichiers)
  * Volumes de données SAP MaxDB (c’est-à-dire les fichiers)
  * Volumes de journaux SAP MaxDB (c’est-à-dire les fichiers)

L’agrégation d’un volume par bandes sur plusieurs disques durs virtuels montés a été évoquée précédemment dans le chapitre [RAID logiciel][dbms-guide-2.2] de ce document.

#### <a name="f77c1436-9ad8-44fb-a331-8671342de818"></a>Autres
Toutes les autres rubriques générales telles que l’analyse des groupes à haute disponibilité Azure ou SAP s’appliquent également comme décrit dans hello trois premiers chapitres de ce document pour les déploiements d’ordinateurs virtuels avec la base de données SAP MaxDB hello.
Autres paramètres spécifiques MaxDB SAP sont des machines virtuelles de tooAzure transparent et sont décrits dans des documents figurant dans la Note SAP [767598 ] et dans les notes SAP :

* [826037]
* [1139904]
* [1173395]

## <a name="specifics-for-sap-livecache-on-windows"></a>Caractéristiques de SAP liveCache sur Windows
### <a name="sap-livecache-version-support"></a>Prise en charge des versions SAP liveCache
La version minimale de SAP liveCache prise en charge dans les machines virtuelles Azure est **SAP LC/LCAPPS 10.0 SP 25** incluant **liveCache 7.9.08.31** et **LCA-Build 25** pour **EhP 2 for SAP SCM 7.0** et les versions ultérieures.

### <a name="supported-microsoft-windows-versions-and-azure-vm-types-for-sap-livecache-dbms"></a>Versions de Microsoft Windows et types de machines virtuelles Azure pris en charge pour SGBD SAP liveCache
version de Microsoft Windows toofind hello pris en charge pour liveCache SAP sur Azure, consultez :

* [Tableau de disponibilité des produits SAP][sap-pam]
* Note SAP [1928533]

Il est vivement recommandé toouse version la plus récente hello hello système d’exploitation Microsoft Windows, qui est Microsoft Windows 2012 R2.

### <a name="sap-livecache-configuration-guidelines-for-sap-installations-in-azure-vms"></a>Instructions de configuration SAP liveCache pour les installations SAP sur des machines virtuelles Azure
#### <a name="recommended-azure-vm-types"></a>Types de machines virtuelles Azure recommandés
Comme SAP liveCache est une application qui effectue des calculs volumineux, montant de hello et la vitesse de la RAM et de processeur a un impact important sur les performances de liveCache SAP.

Pour les types de machine virtuelle Azure hello pris en charge par SAP (Note SAP [1928533]), toutes les ressources du processeur virtuels alloué toohello machine virtuelle sont soutenus par des ressources de processeur physiques dédiés de hello hyperviseur. Aucun surprovisionnement (et par conséquent aucune concurrence pour les ressources UC) n’a lieu.

De même, pour tous les types d’instance de machine virtuelle Azure pris en charge par SAP, de mémoire virtuelle hello est 100 % mappé toohello mémoire physique – un surapprovisionnement (débordement de capacité), par exemple, n’est pas utilisée.

À partir de ce point de vue il est recommandé toouse hello nouvelle série D ou la machine virtuelle Azure de la série DS (en association avec le stockage Azure Premium) type, car ils ont 60 % des processeurs plus rapides que hello série. Pour hello RAM et processeur charge la plus élevée, vous pouvez utiliser série G et les machines virtuelles de série GS (en association avec le stockage Azure Premium) avec processeur Intel® Xeon® plus récente de hello famille E5 v3, qui ont deux fois plus de mémoire hello et quatre fois hello solid state drive lecteur de stockage (disques SSD) Hello D / Série DS.

#### <a name="storage-configuration"></a>Configuration du stockage
Comme SAP liveCache est basé sur la technologie de SAP MaxDB, tous les hello stockage Azure recommandations mentionnées pour SAP MaxDB chapitre [configuration du stockage] [ dbms-guide-8.4.1] sont également valides pour SAP liveCache.

#### <a name="dedicated-azure-vm-for-livecache"></a>Machine virtuelle Azure dédiée pour liveCache
Comme SAP liveCache utilise intensivement la puissance de calcul, pour une utilisation en production il est vivement recommandé toodeploy sur une Machine virtuelle Azure dédié.

![Machine virtuelle Azure dédiée à liveCache pour les cas d’utilisation productive][dbms-guide-figure-700]

#### <a name="backup-and-restore"></a>Sauvegarde et restauration
Sauvegarde et restauration, y compris les considérations relatives aux performances, sont déjà décrits dans les chapitres SAP MaxDB pertinents hello [sauvegarde et restauration] [ dbms-guide-8.4.2] et [considérations sur les performances de sauvegarde et de restauration][dbms-guide-8.4.3].

#### <a name="other"></a>Autres
Toutes les autres rubriques générales sont déjà décrits dans hello pertinentes SAP MaxDB [cela] [ dbms-guide-8.4.4] chapitre.

## <a name="specifics-for-hello-sap-content-server-on-windows"></a>Caractéristiques de hello serveur de contenu SAP sur Windows
Hello serveur de contenu SAP est un contenu de toostore composant distinct, basé sur le serveur tels que des documents électroniques dans des formats différents. Hello du serveur de contenu SAP est fournie par le développement de la technologie et est inter-applications toobe utilisé pour toutes les applications SAP. Il est installé sur un système distinct. Contenu par défaut est d’apprentissage matériel et la documentation à partir de l’entrepôt de base de connaissances ou de dessins provenant de hello mySAP PLM système de gestion de documents.

### <a name="sap-content-server-version-support"></a>Prise en charge des versions SAP Content Server
Actuellement, SAP prend en charge :

* **SAP Content Server** version **6.50 (et versions supérieures)**
* **SAP MaxDB version 7.9**
* **Microsoft IIS (Internet Information Server) version 8.0 (et versions supérieures)**

Il est vivement recommandé version la plus récente hello toouse SAP du serveur de contenu, c'est-à-dire au moment de l’écriture de ce document de hello **6.50 SP4**et la version la plus récente de hello **Microsoft IIS 8.5**.

Vérifiez hello plus récentes prises en charge les versions de serveur de contenu SAP et Microsoft IIS Bonjour [SAP produit disponibilité matrice (PAM)][sap-pam].

### <a name="supported-microsoft-windows-and-azure-vm-types-for-sap-content-server"></a>Versions de Microsoft Windows et types de machines virtuelles Azure pris en charge pour SAP Content Server
toofind à la version de Windows prise en charge pour le serveur de contenu SAP sur Azure, consultez :

* [Tableau de disponibilité des produits SAP][sap-pam]
* Note SAP [1928533]

Il est vivement recommandé toouse hello dernière version de Microsoft Windows, c'est-à-dire au moment de l’écriture de ce document de hello **Windows Server 2012 R2**.

### <a name="sap-content-server-configuration-guidelines-for-sap-installations-in-azure-vms"></a>Instructions de configuration SAP Content Server pour les installations SAP sur des machines virtuelles Azure
#### <a name="storage-configuration"></a>Configuration du stockage
Si vous configurez des fichiers de serveur de contenu SAP toostore dans la base de données SAP MaxDB hello, le stockage Azure toutes les meilleures pratiques de recommandation mentionnée pour SAP MaxDB chapitre [Configuration du stockage] [ dbms-guide-8.4.1] sont également valide pour le scénario de serveur de contenu SAP hello.

Si vous configurez des fichiers de serveur de contenu SAP toostore hello système de fichiers, il est recommandé de toouse un lecteur logique. À l’aide des espaces de stockage vous permet d’augmenter la taille de disque logique tooalso et débit d’e/s, comme figurant dans le chapitre [logiciel RAID][dbms-guide-2.2].

#### <a name="sap-content-server-location"></a>Emplacement de SAP Content Server
Serveur de contenu SAP a toobe déployé Bonjour même région Azure et réseau virtuel de Azure où hello système SAP est déployé. Vous êtes libre toodecide si vous souhaitez que les composants de serveur de contenu SAP toodeploy sur une machine virtuelle de Azure dédiée ou hello même machine virtuelle où hello système SAP est en cours d’exécution.

![Machine virtuelle Azure dédiée pour SAP Content Server][dbms-guide-figure-800]

#### <a name="sap-cache-server-location"></a>Emplacement de SAP Cache Server
Hello serveur de Cache SAP est un composant serveur supplémentaires tooprovide accès too(cached) documents localement. Hello serveur de Cache SAP met en cache des documents d’un serveur de contenu SAP hello. Il s’agit d’un trafic réseau toooptimize si les documents ont toobe de récupérer plusieurs fois à partir de différents emplacements. règle générale de Hello est que ce serveur de Cache SAP hello a toobe toohello physiquement fermer client qui accède au serveur de Cache de SAP de hello.

Ici, deux options s’offrent à vous :

1. **Client est un système SAP d’arrière-plan** si un système SAP d’arrière-plan est configuré tooaccess du serveur de contenu SAP, ce système SAP est un client. Comme le système SAP et le serveur de contenu SAP sont déployés dans hello même région Azure – Bonjour même centre de données Azure : ils sont physiquement proches tooeach autres. Par conséquent, il n’existe aucun toohave besoin un serveur de Cache dédié SAP. L’interface utilisateur SAP (interface GUI SAP ou un navigateur web) de clients accès hello système SAP directement et hello SAP documents récupère du système à partir de hello du serveur de contenu SAP.
2. **Client est un navigateur local** hello du serveur de contenu SAP peut être configuré toobe accédé directement par le navigateur web de hello. Dans ce cas, un navigateur web en cours d’exécution locale est un client de hello du serveur de contenu SAP. Centre de données sur site et le centre de données Azure sont placées dans différents lieux géographiques (tooeach Fermer dans l’idéal, autres). Votre centre de données local est connecté tooAzure via Azure VPN de Site à Site ou ExpressRoute. Même si les deux options offrent tooAzure de connexion de réseau VPN sécurisée, connexion site à site réseau n’offre pas un SLA de la bande passante et la latence réseau entre le centre de données local hello et hello centre de données Azure. toospeed des toodocuments d’accès, vous pouvez effectuer hello suivantes :
   1. Installer le serveur de Cache SAP locale, de fermer le navigateur web de local toohello (option [cela] [ dbms-guide-900-sap-cache-server-on-premises] Figure)
   2. Configurer Azure ExpressRoute, qui offre une connexion réseau dédiée à haut débit et à faible latence entre le centre de données local et le centre de données Azure.

![Option tooinstall serveur de Cache SAP local][dbms-guide-figure-900]
<a name="642f746c-e4d4-489d-bf63-73e80177a0a8"></a>

#### <a name="backup--restore"></a>Sauvegarde / restauration
Si vous configurez des fichiers de toostore hello du serveur de contenu SAP dans la base de données SAP MaxDB hello, considérations de performances et de la procédure de sauvegarde/restauration hello sont déjà décrits dans le chapitre de SAP MaxDB [sauvegarde et restauration] [ dbms-guide-8.4.2] et chapitre [considérations sur les performances de sauvegarde et de restauration][dbms-guide-8.4.3].

Si vous configurez des fichiers de toostore hello du serveur de contenu SAP dans le système de fichiers hello, une option consiste à tooexecute sauvegarde/restauration manuelle de structure d’ensemble du fichier hello dans lequel se trouvent les documents hello. TooSAP similaire MaxDB sauvegarde/restauration, il est recommandé d’un volume de disque dédié toohave fins de sauvegarde.

#### <a name="other"></a>Autres
Autres paramètres spécifiques du serveur de contenu SAP sont des machines virtuelles de tooAzure transparent et sont décrites dans les divers documents et les Notes SAP :

* <https://service.sap.com/contentserver>
* Note de SAP [1619726]  

## <a name="specifics-tooibm-db2-for-luw-on-windows"></a>Spécificités tooIBM DB2 pour LUW sur Windows
Avec Microsoft Azure, vous pouvez facilement migrer votre application SAP existante en cours d’exécution sur IBM DB2 pour Linux, UNIX et Windows (LUW) tooAzure virtuels. Avec SAP sur IBM DB2 pour LUW, les administrateurs et développeurs peuvent utiliser hello mêmes outils de développement et d’administration qui sont disponibles sur site.
Informations générales sur l’exécution de SAP Business Suite sur IBM DB2 pour LUW se trouvent dans hello SAP Communauté réseau (SCN) à <https://scn.sap.com/community/db2-for-linux-unix-windows>.

Pour des informations et des mises à jour supplémentaires de SAP sur DB2 pour LUW sur Azure, voir la Note de SAP [2233094].

### <a name="ibm-db2-for-linux-unix-and-windows-version-support"></a>Prise en charge des versions IBM DB2 pour Linux, UNIX et Windows
SAP sur IBM DB2 pour LUW est pris en charge sur les services de machines virtuelles Microsoft Azure à compter de la version DB2 10.5.

Pour plus d’informations sur les produits SAP pris en charge et les types de machine virtuelle Azure, reportez-vous à la Remarque de tooSAP [1928533].

### <a name="ibm-db2-for-linux-unix-and-windows-configuration-guidelines-for-sap-installations-in-azure-vms"></a>Instructions de configuration IBM DB2 pour Linux, UNIX et Windows pour les installations SAP sur des machines virtuelles Azure
#### <a name="storage-configuration"></a>Configuration du stockage
Tous les fichiers de base de données doivent être stockées sur le système de fichiers NTFS hello basée sur des disques de disque dur virtuel. Ces disques durs virtuels monté toohello machine virtuelle Azure et sont basés dans le stockage d’objets BLOB Azure Page (<https://msdn.microsoft.com/library/azure/ee691964.aspx>).
Tout type de lecteurs réseau ou des partages distants comme hello suivant des services de fichiers Azure est **pas** pris en charge pour les fichiers de base de données :

* <https://blogs.msdn.com/b/windowsazurestorage/archive/2014/05/12/introducing-microsoft-azure-file-service.aspx>
* <https://blogs.msdn.com/b/windowsazurestorage/archive/2014/05/27/persisting-connections-to-microsoft-azure-files.aspx>

Si vous utilisez des disques durs virtuels de Azure basé sur le stockage d’objets BLOB Azure Page, hello instructions effectuées dans ce document dans le chapitre [Structure d’un déploiement SGBDR] [ dbms-guide-2] s’appliquent également toodeployments avec hello IBM DB2 pour LUW Base de données.

Comme expliqué plus haut dans la partie générale de hello du document de hello, les quotas sur le débit d’e/s pour les disques durs virtuels de Azure existent. les quotas exacte Hello dépendent de type de machine virtuelle hello utilisé. Une liste des types de machines virtuelles avec leurs quotas est disponible [ici][virtual-machines-sizes]

Tant que hello actuel quota d’IOPS par disque est suffisant, qu'il est possible de toostore sur que tous hello des fichiers de base de données un seul monté disque VHD Azure.

Pour des performances considérations également faire référence toochapter sécurité et performances considérations pour base de données « répertoires de données » dans les guides d’installation SAP.

Ou bien, vous pouvez utiliser des Pools de stockage Windows (uniquement disponible dans Windows Server 2012 et versions ultérieures) ou répartition de Windows pour Windows 2008 R2 en tant que décrit dans le chapitre [logiciel RAID] [ dbms-guide-2.2] de ce document toocreate une grande unité logique sur plusieurs disques VHD montés.
Pour les disques hello contenant les chemins d’accès de stockage hello DB2 pour vos répertoires de données et saptmp, vous devez spécifier une taille de secteur de disque physique de 512 Ko. Lors de l’utilisation de Pools de stockage Windows, vous devez créer hello pools de stockage manuellement via l’interface de ligne de commande à l’aide du paramètre hello »-LogicalSectorSizeDefault ». Pour plus d’informations, voir <https://technet.microsoft.com/library/hh848689.aspx>.

#### <a name="backuprestore"></a>Sauvegarde/restauration
fonctionnalité de sauvegarde/restauration Hello pour IBM DB2 pour LUW est pris en charge dans hello même façon que sur standard les systèmes d’exploitation Windows Server et Hyper-V.

Vous devez vous assurer que vous disposez d’une stratégie de sauvegarde de base de données valide en place.

Comme dans les déploiements de système nu, les performances de sauvegarde/restauration dépendent de combien de volumes peut être lues en parallèle et quelles débit hello de ces volumes peut-être être. En outre, hello consommation d’UC utilisée par la compression de sauvegarde peut jouent un rôle significatif sur les machines virtuelles avec uniquement les threads de l’UC de too8. Par conséquent, on peut partir des hypothèses suivantes :

* Hello moins hello nombre de disques durs virtuels utilisés périphériques de base de données toostore hello, hello plus petites hello débit global de lecture
* Hello plus petit nombre de hello de threads d’UC Bonjour VM, hello plus grave impact hello de compression de la sauvegarde
* Hello moins sauvegarde hello toowrite de cibles (Stripe répertoires, disques durs virtuels) pour la réduction du débit hello hello

nombre de hello de tooincrease de toowrite cibles pour, les deux options peuvent être utilisé/combinée selon vos besoins :

* Répartition du volume de cible de sauvegarde hello sur plusieurs disques durs virtuels montés dans un ordre tooimprove hello e/s de débit sur ce volume agrégé par bandes
* À l’aide de plusieurs annuaires toowrite hello sauvegarde pour

#### <a name="high-availability-and-disaster-recovery"></a>Haute disponibilité et récupération d’urgence
Microsoft Cluster Server (MSCS) n’est pas pris en charge.

La fonction HADR (haute disponibilité et récupération d’urgence) DB2 est prise en charge. Si hello ordinateurs virtuels de la configuration de haute disponibilité hello ont l’utilisation de la résolution de noms, le programme d’installation de hello dans Azure ne diffère pas à une installation est effectuée localement. Il n’est pas recommandé toorely sur la résolution d’adresses IP.

N’utilisez pas la géoréplication Azure Store. Pour plus d’informations, consultez toochapter [Microsoft Azure Storage] [ dbms-guide-2.3] et chapitre [haute disponibilité et récupération d’urgence avec des machines virtuelles Azure] [ dbms-guide-3].

#### <a name="other"></a>Autres
Toutes les autres rubriques générales telles que la surveillance de groupes à haute disponibilité Azure ou SAP s’appliquent comme décrit dans hello trois premiers chapitres de ce document pour les déploiements d’ordinateurs virtuels avec IBM DB2 pour LUW également.

Consultez également toochapter [générale sur SQL Server pour SAP sur Azure Résumé][dbms-guide-5.8].
