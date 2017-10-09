---
title: "aaaSAP NetWeaver sur machines virtuelles Azure – planification et implémentation | Documents Microsoft"
description: "SAP NetWeaver sur machines virtuelles Azure – Guide de planification et d’implémentation"
services: virtual-machines-windows
documentationcenter: 
author: MSSedusch
manager: timlt
editor: 
tags: azure-resource-manager
keywords: 
ms.assetid: 2b58a419-c892-4722-8cb6-2f8beef4430c
ms.service: virtual-machines-windows
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 11/08/2016
ms.author: sedusch
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 53d63240760282b409f7e9412e8240689bcbcc6a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="sap-netweaver-on-azure-windows-virtual-machines-vms--planning-and-implementation-guide"></a>SAP NetWeaver sur machines virtuelles Azure Windows – Guide de planification et d’implémentation
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

[azure-cli]:../../cli-install-nodejs.md
[azure-portal]:https://portal.azure.com
[azure-ps]:/powershell/azureps-cmdlets-docs
[azure-quickstart-templates-github]:https://github.com/Azure/azure-quickstart-templates
[azure-script-ps]:https://go.microsoft.com/fwlink/p/?LinkID=395017
[azure-subscription-service-limits]:../../azure-subscription-service-limits.md
[azure-subscription-service-limits-subscription]:../../azure-subscription-service-limits.md#subscription-limits

[dbms-guide]:sap-dbms-guide.md
[dbms-guide-2.1]:sap-dbms-guide.md#c7abf1f0-c927-4a7c-9c1d-c7b5b3b7212f
[dbms-guide-2.2]:sap-dbms-guide.md#c8e566f9-21b7-4457-9f7f-126036971a91
[dbms-guide-2.3]:sap-dbms-guide.md#10b041ef-c177-498a-93ed-44b3441ab152
[dbms-guide-2]:sap-dbms-guide.md#65fa79d6-a85f-47ee-890b-22e794f51a64
[dbms-guide-3]:sap-dbms-guide.md#871dfc27-e509-4222-9370-ab1de77021c3
[dbms-guide-5.5.1]:sap-dbms-guide.md#0fef0e79-d3fe-4ae2-85af-73666a6f7268
[dbms-guide-5.5.2]:sap-dbms-guide.md#f9071eff-9d72-4f47-9da4-1852d782087b
[dbms-guide-5.6]:sap-dbms-guide.md#1b353e38-21b3-4310-aeb6-a77e7c8e81c8
[dbms-guide-5.8]:sap-dbms-guide.md#9053f720-6f3b-4483-904d-15dc54141e30
[dbms-guide-5]:sap-dbms-guide.md#3264829e-075e-4d25-966e-a49dad878737
[dbms-guide-8.4.1]:sap-dbms-guide.md#b48cfe3b-48e9-4f5b-a783-1d29155bd573
[dbms-guide-8.4.2]:sap-dbms-guide.md#23c78d3b-ca5a-4e72-8a24-645d141a3f5d
[dbms-guide-8.4.3]:sap-dbms-guide.md#77cd2fbb-307e-4cbf-a65f-745553f72d2c
[dbms-guide-8.4.4]:sap-dbms-guide.md#f77c1436-9ad8-44fb-a331-8671342de818
[dbms-guide-900-sap-cache-server-on-premises]:sap-dbms-guide.md#642f746c-e4d4-489d-bf63-73e80177a0a8

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

[getting-started-windows-classic]:classic/sap-get-started.mdsap-dbms-guide.md
[getting-started-windows-classic-dbms]:classic/sap-get-started.mdsap-dbms-guide.md#c5b77a14-f6b4-44e9-acab-4d28ff72a930
[getting-started-windows-classic-deployment]:classic/sap-get-started.mdsap-dbms-guide.md#f84ea6ce-bbb4-41f7-9965-34d31b0098ea
[getting-started-windows-classic-dr]:classic/sap-get-started.mdsap-dbms-guide.md#cff10b4a-01a5-4dc3-94b6-afb8e55757d3
[getting-started-windows-classic-ha-sios]:classic/sap-get-started.mdsap-dbms-guide.md#4bb7512c-0fa0-4227-9853-4004281b1037
[getting-started-windows-classic-planning]:classic/sap-get-started.mdsap-dbms-guide.md#f2a5e9d8-49e4-419e-9900-af783173481c

[ha-guide-classic]:http://go.microsoft.com/fwlink/?LinkId=613056

[ha-guide]:sap-high-availability-guide.md

[install-extension-cli]:virtual-machines-linux-enable-aem.md

[Logo_Linux]:./media/virtual-machines-shared-sap-shared/Linux.png
[Logo_Windows]:./media/virtual-machines-shared-sap-shared/Windows.png

[msdn-set-azurermvmaemextension]:https://msdn.microsoft.com/library/azure/mt670598.aspx

[planning-guide]:sap-planning-guide.md
[planning-guide-1.2]:sap-planning-guide.md#e55d1e22-c2c8-460b-9897-64622a34fdff
[planning-guide-11.4]:sap-planning-guide.md#7cf991a1-badd-40a9-944e-7baae842a058
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
[virtual-machines-windows-attach-disk-portal]:../virtual-machines-windows-attach-disk-portal.md
[virtual-machines-azure-resource-manager-architecture]:../../resource-manager-deployment-model.md
[virtual-machines-azurerm-versus-azuresm]:virtual-machines-windows-compare-deployment-models.md
[virtual-machines-windows-classic-configure-oracle-data-guard]:../virtual-machines-windows-classic-configure-oracle-data-guard.md
[virtual-machines-linux-cli-deploy-templates]:../linux/cli-deploy-templates.md
[virtual-machines-deploy-rmtemplates-powershell]:../virtual-machines-windows-ps-manage.md
[virtual-machines-linux-agent-user-guide]:../linux/agent-user-guide.md
[virtual-machines-linux-agent-user-guide-command-line-options]:../linux/agent-user-guide.md#command-line-options
[virtual-machines-linux-capture-image]:../linux/capture-image.md
[virtual-machines-linux-capture-image-capture]:../linux/capture-image.md#step-2-create-vm-image
[virtual-machines-windows-capture-image]:../virtual-machines-windows-create-vm-generalized.md
[virtual-machines-windows-capture-image-prepare-the-vm-for-image-capture]:../virtual-machines-windows-create-vm-generalized.md
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

Microsoft Azure permet aux ressources de calcul et de stockage de tooacquire entreprises dans le temps minimal sans par de longs cycles. Machines virtuelles permettent aux entreprises toodeploy des applications classique, comme SAP NetWeaver en fonction des applications dans Azure et étendre leur fiabilité et disponibilité sans avoir davantage de ressources disponibles sur site. Azure Virtual Machine Services prend également en charge la connectivité entre différents locaux, le tooactively de sociétés permet d’intégrer des Machines virtuelles Azure dans leurs domaines locaux, leurs Clouds privés et leur paysage système SAP.
Ce livre blanc décrit les notions de base hello de la Machine virtuelle Microsoft Azure fournit une vue d’ensemble des considérations de planification et d’implémentation pour les installations SAP NetWeaver dans Azure et devez donc hello document tooread avant de commencer déploiement de SAP NetWeaver sur Azure.
Hello papier complète hello Documentation d’Installation SAP et les Notes SAP, qui représentent les ressources principales de hello pour les installations et les déploiements de logiciels SAP sur obtiennent des plateformes.

## <a name="summary"></a>Résumé
Le Cloud Computing est un terme couramment utilisé qui prend de plus en plus d’importance dans hello secteur informatique, des petites entreprises, les sociétés toolarge et multinationale.

Microsoft Azure est la plateforme de Services de Cloud de Microsoft, qui offre un large éventail de nouvelles possibilités de hello. Maintenant les clients sont des applications d’approvisionner et configurer des toorapidly en mesure d’en tant que service de cloud de hello, afin qu’ils ne sont pas tootechnical limité ou restrictions budgétisation. Au lieu de consacrer du temps et budget à l’infrastructure matérielle, les entreprises peuvent se concentrer sur l’application hello, des processus d’entreprise et ses avantages pour les clients et les utilisateurs.

Avec le service Machines virtuelles Microsoft Azure, Microsoft propose une infrastructure complète sous forme d’infrastructure en tant que service (IaaS). Les applications basées sur SAP NetWeaver sont prises en charge sur Machines virtuelles Azure (IaaS). Ce livre blanc décrit comment tooplan implémentez SAP NetWeaver applications basées sur et dans Microsoft Azure comme plateforme hello de choix.

Hello document aborde notamment deux aspects principaux :

* Hello première partie décrit deux modèles de déploiement pris en charge pour les applications basées sur SAP NetWeaver sur Azure. La gestion générale d’Azure avec les déploiements SAP est également abordée.
* Hello deuxième partie détaille l’implémentation hello deux scénarios décrits dans la première partie de hello.

Pour obtenir des ressources supplémentaires, consultez le chapitre [Ressources][planning-guide-1.2] de ce document.

### <a name="definitions-upfront"></a>Préambule : définitions
Dans l’ensemble de documents de hello, nous allons utiliser hello dispositions suivantes :

* IaaS : Infrastructure as a Service.
* PaaS : Platform as a Service.
* SaaS : Software as a Service.
* ARM : Azure Resource Manager.
* Composant SAP : une application SAP individuelle telle que ECC, BW, Solution Manager ou EP.  Les composants SAP peuvent être basés sur des technologies ABAP ou Java traditionnelles ou une application non basée sur NetWeaver telle que Business Objects.
* Environnement SAP : un ou plusieurs composants SAP regroupement logiquement tooperform une fonction d’entreprise telles que le développement, Choisissons, formation, récupération d’urgence ou de Production.
* Paysage SAP : Cela fait référence à toohello des ressources SAP ensemble dans un client paysage informatique. Hello paysage SAP comprend tous les environnements de production et de non-production.
* Système SAP : combinaison de hello de la couche SGBD et de la couche application, par exemple un système de développement ERP SAP, système de test SAP BW, système de production CRM SAP, etc... Dans Azure les déploiements, qu'il n’est pas pris en charge toodivide ces deux couches entre locaux et Azure. Cela signifie qu’un système SAP doit être déployé en local ou dans Azure. Toutefois, vous pouvez déployer hello différents systèmes d’un paysage SAP dans Azure ou localement. Par exemple, vous pourriez déployer des systèmes de développement et de test de CRM SAP dans Azure hello mais hello production CRM SAP/système sur site.
* Déploiement de cloud uniquement : un déploiement où hello abonnement Azure n’est pas connecté via un site à site ou ExpressRoute connexion toohello localement l’infrastructure du réseau. Dans la documentation Azure courante, ces types de déploiements sont également décrits comme des déploiements « cloud uniquement ». Ordinateurs virtuels déployés avec cette méthode sont accessibles via hello internet et une adresse IP publique et/ou un DNS public nommez les machines virtuelles de toohello attribué dans Azure. Pour Microsoft Windows hello locale Active Directory (AD) et DNS n’est pas étendu tooAzure dans ces types de déploiement. Par conséquent, les machines virtuelles de hello ne font pas partie de hello locale Active Directory. Il en est de même pour les implémentations de Linux qui utilisent par exemple OpenLDAP + Kerberos.

> [!NOTE]
> Les déploiements cloud uniquement dans ce document sont définis comme des paysages SAP complets, exécutés exclusivement dans Azure sans extension du répertoire Active Directory/OpenLDAP ou résolution de noms du site local au cloud public. Les configurations uniquement dans le cloud ne sont pas pris en charge pour les systèmes SAP de production ou les configurations où SAP STMS ou autres ressources sur site doivent toobe utilisé entre les systèmes SAP hébergés sur Azure et aux ressources locales.
>
>

* Intersite : Décrit un scénario dans lequel les machines virtuelles sont déployée tooan abonnement Azure qui utilise le site à site, plusieurs site ou ExpressRoute la connectivité entre les centres de local hello et Azure. Dans la documentation Azure courante, ces types de déploiements sont également décrits comme des scénarios intersites. raison de Hello pour les connexions hello sont tooextend domaines locaux, sur site Active Directory / OpenLDAP et DNS sur site dans Azure. Hello local paysage est étendue toohello ressources Azure de l’abonnement de hello. Avoir cette extension, hello machines virtuelles peut être la partie du domaine local de hello. Les utilisateurs du domaine local de hello peuvent accéder aux serveurs de hello et exécuter des services sur ces machines virtuelles (comme les services SGBD). La communication et la résolution de noms entre les machines virtuelles déployées en local et les machines virtuelles déployées dans Azure sont possibles. Il s’agit de scénario hello nous pensons que la plupart des toobe de ressources SAP déployé dans.  Pour plus d’informations, consultez [cet][vpn-gateway-cross-premises-options] article et [celui-ci][vpn-gateway-site-to-site-create].

> [!NOTE]
> Les déploiements intersites de systèmes SAP dans lesquels des machines virtuelles Azure exécutant des systèmes SAP font partie d’un domaine local sont pris en charge pour les systèmes SAP de production. Les configurations entre différents locaux sont prises en charge pour le déploiement d’éléments ou de l’intégralité des paysages SAP dans Azure. Même en paysage SAP complète de hello Azure requiert ayant ces machines virtuelles faisant partie d’un domaine local et des annonces / OpenLDAP. Dans les versions précédentes de la documentation de hello, nous avons parlé des scénarios hybrides, où le terme hello « Hybride » associé à des faits hello qu’il existe une connectivité intersite entre locaux et Azure. De plus, les faits hello que machines virtuelles dans Azure hello font partie de hello locale Active Directory / OpenLDAP.
>
>

Certaines documentations Microsoft décrivent les scénarios intersites de façon légèrement différente, en particulier pour les configurations haute disponibilité SGBD. Bonjour documents relatifs au cas de hello SAP, scénario de hello intersite simplement résume toohaving un site à site ou privé (ExpressRoute) connectivité et hello fait que le paysage SAP de hello est distribué entre locaux et Azure.  

### <a name="e55d1e22-c2c8-460b-9897-64622a34fdff"></a>Ressources
Hello guides supplémentaires suivants sont disponibles pour la rubrique hello des déploiements SAP sur Azure :

* [SAP NetWeaver sur les machines virtuelles Azure – Guide de planification et d’implémentation (ce document)][planning-guide]
* [SAP NetWeaver sur machines virtuelles Azure – Guide de déploiement][deployment-guide]
* [SAP NetWeaver sur machines virtuelles Azure – Guide de déploiement SGBD][dbms-guide]
* [SAP NetWeaver sur machines virtuelles Azure – Guide de déploiement haute disponibilité][ha-guide]

> [!IMPORTANT]
> Chaque fois que possible un toohello lien référence Guide d’Installation SAP est utilisé (référence InstGuide-01, consultez <http://service.sap.com/instguides>). Lorsqu’il s’agit de conditions préalables de toohello et les processus d’installation, Guides d’Installation hello SAP NetWeaver doit toujours être lecture attentive, car ce document couvre uniquement les tâches spécifiques pour les systèmes SAP NetWeaver installés dans une Machine virtuelle Microsoft Azure.
>
>

Hello suit les Notes SAP est rubrique toohello connexes de SAP sur Azure :

| Numéro de la note | Intitulé |
| --- | --- |
| [1928533] |Applications SAP sur Azure : dimensionnement et produits pris en charge |
| [2015553] |SAP sur Microsoft Azure : configuration requise |
| [1999351] |Résolution des problèmes de surveillance Azure améliorée pour SAP |
| [2178632] |Métriques de surveillance clés pour SAP sur Microsoft Azure |
| [1409604] |Virtualisation sur Windows : surveillance améliorée |
| [2191498] |SAP sur Linux avec Azure : surveillance améliorée |
| [2243692] |Linux sur Microsoft Azure Virtual Machines (IaaS) : problèmes de licence SAP |
| [1984787] |SUSE LINUX Enterprise Server 12 : Notes d’installation |
| [2002167] |Red Hat Enterprise Linux 7.x : Installation et mise à niveau |

Lisez aussi hello [SCN Wiki](https://wiki.scn.sap.com/wiki/display/HOME/SAPonLinuxNotes) qui contient toutes les Notes SAP pour Linux.

Les limitations générales par défaut et les limitations maximales des abonnements Azure sont exposées dans [cet article][azure-subscription-service-limits-subscription]

## <a name="possible-scenarios"></a>Scénarios possibles
SAP est souvent considéré comme une des applications plus critiques de hello au sein des entreprises. architecture de Hello et les opérations de ces applications sont généralement très complexes, et il est important de s’assurer que vous répondent aux exigences de disponibilité et les performances.

Les entreprises doivent donc toothink avec précaution sur les applications peuvent être exécutées dans un environnement de Cloud Public, indépendant du fournisseur de Cloud hello choisi.

Les types de systèmes possibles pour le déploiement des applications basées sur SAP NetWeaver dans des environnements de cloud public sont répertoriés ci-dessous :

1. les systèmes de production de taille moyenne ;
2. les systèmes de développement ;
3. Systèmes de test
4. Systèmes de prototype
5. Systèmes de démonstration/formation

Dans l’ordre toosuccessfully déployer des systèmes SAP dans Azure IaaS ou IaaS en général, il est important toounderstand hello différences entre les offres hello d’Infogérants traditionnels ou des hébergeurs et offres IaaS. Alors que l’hébergeur traditionnelles de hello ou infogérant s’adapte à la charge de travail infrastructure (réseau, stockage et type de serveur) toohello un client souhaite toohost, il est à la place responsabilité toochoose hello charge de travail du client hello pour les déploiements IaaS.

Dans un premier temps, les clients doivent hello tooverify éléments suivants :

* Hello SAP pris en charge les types de machine virtuelle de Azure
* Hello SAP pris en charge les produits/versions sur Azure
* Hello pris en charge les versions de système d’exploitation et SGBD pour hello que des versions SAP dans Azure
* Le débit SAPS (SAP Application Performance Standard) fourni par différentes références Azure

Hello réponses toothese questions peuvent être lus dans la Note SAP [1928533].

Dans un deuxième temps, des limitations de la bande passante et de ressources Azure doivent la consommation des ressources tooactual toobe comparée de systèmes locaux. Par conséquent, toobe du besoin clients familiarisé avec des fonctionnalités différentes hello de hello types Azure pris en charge avec SAP dans la zone hello de :

* Les ressources processeur et mémoire des différents types de machines virtuelles
* La bande passante et les E/S par seconde des différents types de machines virtuelles
* les fonctionnalités réseau des différents types de machines virtuelles.

Vous pouvez trouver la plupart de ces données [ici][virtual-machines-sizes]

N’oubliez pas que hello limites indiquées dans le lien hello ci-dessus sont des limites supérieures. Cela ne signifie pas que hello limite pour une des ressources de hello, par exemple, les e/s peut être fourni en toutes circonstances. exceptions de Hello sont bien que les ressources de processeur et mémoire hello d’un type de machine virtuelle choisi. Pour les types de machine virtuelle hello pris en charge par SAP, les ressources processeur et mémoire hello sont réservées et donc consommables à n’importe quel point dans le temps pour la consommation dans hello machine virtuelle.

plateforme de Microsoft Azure Hello, comme d’autres plateformes IaaS est une plateforme mutualisée. Cela signifie que le stockage, le réseau et toutes les autres ressources sont partagés entre des locataires. Logique de limitation et de quota intelligente est locataire utilisé tooprevent celui d’affecter les performances hello d’une autre locataire (syndrome du voisin) de manière drastique. Bien que la logique des variations de tookeep Azure essaie de plateformes de petite taille, hautement partagées bande passante expérimentés ont tendance à toointroduce les écarts dans la disponibilité des ressources et bande passante à un grand nombre de clients est utilisé tooin leurs déploiements sur site. Par conséquent, vous pouvez rencontrer des différents niveaux de bande passante en ce qui concerne les toonetworking ou le stockage d’e/s (volume de hello ainsi que la latence) à partir de toominute minute. probabilité Hello qu’un système SAP sur Azure écarts supérieurs à un système local doit toobe pris en compte.

La dernière étape consiste à tooevaluate des exigences de disponibilité. Il peut se produire, ce hello sous-jacent d’infrastructure Azure nécessite des hôtes hello toobe de machines virtuelles redémarré en cours d’exécution et tooget mis à jour. Dans ce cas, les machines virtuelles en cours d’exécution sur ces hôtes doivent également être arrêtées et redémarrées. minutage Hello de maintenance de ce type est effectuée pendant les heures non principal pour une région particulière, mais fenêtre potentielle de hello de quelques heures pendant lesquelles un redémarrage a lieu est relativement large. Il existe différentes technologies dans hello plateforme Azure qui peut être configuré toomitigate certaines ou toutes hello une incidence sur ces mises à jour. Améliorations futures de hello plateforme Azure, sont des applications SGBD et SAP conçu impact de hello toominimize de ces redémarrages.

Dans l’ordre toosuccessfully déployer un système SAP sur Azure, hello local SAP systèmes système d’exploitation, la base de données et applications SAP doit s’affichent sur hello matrice de prise en charge Azure de SAP, tenir dans hello de ressources hello peut fournir une infrastructure Azure et qui peut travailler avec hello que disponibilité SLA Microsoft Azure offre. Une fois ces systèmes identifiés, vous devez toodecide sur l’un des hello deux scénarios de déploiement suivants.

### <a name="1625df66-4cc6-4d60-9202-de8a0b77f803"></a>Uniquement dans le cloud - déploiements d’ordinateurs virtuels dans Azure sans dépendances sur hello local réseau client
![Machine virtuelle unique avec scénario de démonstration ou de formation SAP dans Azure][planning-guide-figure-100]

Ce scénario est caractéristique de formations ou de systèmes de démonstration, où tous les composants de hello de SAP et de logiciels non-SAP sont installés au sein d’une seule machine virtuelle. Les systèmes SAP de production ne sont pas pris en charge dans ce scénario de déploiement. En général, ce scénario répond aux hello suivant les exigences :

* machines virtuelles Hello elles-mêmes sont accessibles via un réseau public hello. Connectivité réseau directe pour les applications hello en cours d’exécution dans toohello de machines virtuelles hello local réseau de l’entreprise hello propriétaire de contenu de démonstrations ou de formations hello ou client de hello n’est pas nécessaire.
* En cas de plusieurs machines virtuelles de la représentant les formations hello ou scénario de démonstration, résolution de communications et le nom de réseau doit toowork entre les machines virtuelles de hello. Mais les communications entre le groupe hello de machines virtuelles doivent toobe isolé afin que plusieurs ensembles d’ordinateurs virtuels peuvent être déployées côte à côte sans interférence.  
* Connectivité Internet est nécessaire pour la connexion de tooremote hello utilisateur final dans toohello que machines virtuelles hébergées dans Azure. Selon le système d’exploitation invité de hello, les Services Terminal Server/RDS ou VNC/ssh est utilisé tooaccess hello VM tooeither répondre aux tâches de formation hello ou effectuer des démonstrations de hello. Si les ports de SAP comme 3200, 3300 et 3600 peut également être exposés instance d’application SAP hello est accessible à partir de n’importe quel bureau connecté Internet.
* Hello ou les systèmes SAP (et constituent un scénario autonome dans Azure qui seulement requiert la connectivité internet pour l’accès de l’utilisateur final et ne nécessite pas un tooother de connexion des machines virtuelles dans Azure.
* Interface utilisateur graphique SAP et un navigateur sont installés et exécutés directement sur hello machine virtuelle.
* Une réinitialisation rapide d’un état d’origine toohello des ordinateurs virtuels et le nouveau déploiement de cet état d’origine sont requises.
* Dans les cas de hello de démonstration et les scénarios d’apprentissage sont effectués sur plusieurs machines virtuelles, un annuaire Active Directory OpenLDAP et/ou un service DNS est obligatoire pour chaque groupe de machines virtuelles.

![Groupe de machines virtuelles représentant un scénario de formation ou de démonstration dans un service cloud Azure][planning-guide-figure-200]

Il est important de tookeep à l’esprit que hello des machines virtuelles dans chacun des hello définit toobe besoin déployée en parallèle, où les noms de machine virtuelle hello dans chaque jeu de hello sont même hello.

### <a name="f5b3b18c-302c-4bd8-9ab2-c388f1ab3d10"></a>entre sites - déploiement d’une ou plusieurs machines virtuelles SAP dans Azure avec spécification hello intégration complète dans le réseau local de hello
![Réseau privé virtuel avec connectivité de site à site (intersite)][planning-guide-figure-300]

Ce scénario est un scénario intersite où de nombreux modèles de déploiement sont possibles. Il peut être décrit comme simplement que l’exécution de certaines parties de hello SAP paysage local et d’autres parties de hello paysage SAP sur Azure. Tous les aspects de faits de hello partie des composants SAP hello s’exécutent dans Azure doivent être transparentes pour les utilisateurs finaux. Par conséquent, hello SAP Transport Correction système STMS (), la Communication RFC, l’impression, la sécurité (comme SSO), etc. fonctionnent de façon transparente pour les systèmes SAP hello s’exécutant sur Azure. Mais le scénario de coexistence hello décrit également un scénario où les paysage SAP complète hello s’exécute dans Azure avec le domaine du client hello et DNS étendu dans Azure.

> [!NOTE]
> Il s’agit de scénario de déploiement hello est pris en charge pour l’exécution de systèmes SAP de production.
>
>

Lecture [cet article] [ vpn-gateway-create-site-to-site-rm-powershell] pour plus d’informations sur la façon de tooconnect votre site réseau tooMicrosoft Azure

> [!IMPORTANT]
> Lorsque nous parlons de scénarios intersite entre les déploiements de clients locaux et Azure, nous recherchons la granularité hello de systèmes SAP entiers. Les scénarios *non pris en charge* pour les situations intersites sont les suivants :
>
> * L’exécution de différentes couches des applications SAP avec diverses méthodes de déploiement. Par exemple, en cours d’exécution hello SGBD couche localement, mais couche d’application hello SAP dans des machines virtuelles déployées en tant que machines virtuelles Azure ou vice versa.
> * Le fractionnement de certains composants d’une couche SAP dans Azure et d’autres en local. Par exemple, fractionnement des Instances de la couche d’application SAP hello entre les machines virtuelles Azure et locaux.
> * La répartition de machines virtuelles exécutant des instances d’un système dans plusieurs régions Azure n’est pas prise en charge.
>
> Hello ces restrictions fait exigence hello pour un réseau de haute performance très faible latence dans un système SAP, en particulier entre les instances de l’application hello et la couche de SGBD hello d’un système SAP.
>
>

### <a name="supported-os-and-database-releases"></a>Versions de base de données et de système d’exploitation prises en charge
* Les logiciels serveurs Microsoft pris en charge par les services de machine virtuelle Azure sont répertoriés dans l’article suivant : <http://support.microsoft.com/kb/2721672>.
* Les versions de système d’exploitation et de base de données prises en charge sur les services de machine virtuelle Azure conjointement avec les logiciels SAP sont mentionnées dans la Note de SAP [1928533].
* Les applications et versions de SAP prises en charge sur les services de machine virtuelle Azure sont mentionnées dans la Note de SAP [1928533].
* Seules les images 64 bits sont toorun pris en charge en tant que machines virtuelles invitées dans Azure pour les scénarios SAP. Cela signifie également que seules les bases de données et applications SAP 64 bits sont prises en charge.

## <a name="microsoft-azure-virtual-machine-services"></a>Microsoft Azure Virtual Machine Services
plateforme de Microsoft Azure Hello est un nuage internet à l’échelle de plateforme de services hébergés et exploitée dans Microsoft les données des centres de. plateforme de Hello inclut hello Microsoft Azure Virtual Machine Services (Infrastructure en tant que Service, ou IaaS) et un ensemble de la plateforme en tant que des fonctionnalités de Service (PaaS).

Hello plateforme Azure évite hello investir dans des technologies et des achats de l’infrastructure. Elle simplifie la gestion et fonctionnement des applications en fournissant des toohost de calcul et de stockage à la demande, de l’échelle et de gérer les applications web et des applications connectées. Gestion de l’infrastructure est dynamique toomatch des besoins d’utilisation avec l’option hello d’un modèle de tarification de paiement à l’utilisation de mise à l’échelle et automatisée avec une plateforme qui est conçue pour la haute disponibilité.

![Positionnement des services Microsoft Azure Virtual Machine][planning-guide-figure-400]

Avec les Services de Machine virtuelle Azure, Microsoft est ce qui vous toodeploy serveur personnalisé images tooAzure en tant qu’instances IaaS (voir Figure 4). Hello Machines virtuelles dans Azure reposent sur des disques durs virtuels (VHD) Hyper-V et sont en mesure de toorun différents systèmes d’exploitation en tant que système d’exploitation invité.

À partir d’un point de vue opérationnel, hello Qu'azure Virtual Machine Services offre semblable expériences en tant que machines virtuelles déployées en local. Toutefois, il présente l’avantage significatif hello que vous n’avez pas besoin tooprocure, administrer et gérer l’infrastructure de hello. Les développeurs et les administrateurs ont un contrôle total de l’image de système d’exploitation hello dans ces machines virtuelles. Les administrateurs peuvent ouvrir une session à distance dans ces maintenance tooperform de machines virtuelles et le dépannage des tâches, ainsi que les tâches de déploiement de logiciel. Dans compte toodeployment, seules restrictions de hello sont les tailles de hello et les capacités de machines virtuelles Azure. Celles-ci peuvent ne pas être aussi granulaires dans la configuration que lorsque le déploiement est effectué en local. Vous avez le choix entre plusieurs types de machines virtuelles qui combinent les éléments suivants :

* nombre de processeurs virtuels ;
* mémoire ;
* nombre de disques durs virtuels pouvant être attachés ;
* bande passante réseau et de stockage.

taille de Hello et les limitations de différentes tailles différentes machines virtuelles proposent peuvent être consultés dans une table dans [cet article][virtual-machines-sizes]

Comme vous allez le voir, il existe diverses familles ou séries de machines virtuelles. Depuis décembre 2015, vous pouvez distinguer hello suivant des familles de machines virtuelles :

* Types de machines virtuelles A0-A7 : elles ne sont pas toutes certifiées pour SAP. Première série de machines virtuelles pour laquelle Azure IaaS a été introduit.
* Types de machines virtuelles A8-A11 : instances de calcul haute performance. Exécution sur des hôtes de calcul différents et plus performants que les autres machines virtuelles de la série A.
* Types de machines virtuelles de la série D : plus performantes que les A0-A7. Tous les types de machine virtuelle hello sont certifiés avec SAP.
* Types de machine virtuelle de la série DS : utiliser les mêmes hôtes en tant que série D, mais sont en mesure de tooconnect tooAzure stockage Premium (consultez le chapitre [stockage Azure Premium] [ planning-guide-3.3.2] de ce document). Une fois encore, tous les types de machines virtuelles ne sont pas certifiés pour SAP.
* Types de machines virtuelles de la série G : types de machines virtuelles à mémoire élevée.
* Types de machine virtuelle de série GS : comme série G mais notamment hello option toouse stockage Azure Premium (consultez le chapitre [stockage Azure Premium] [ planning-guide-3.3.2] de ce document). Lors de l’utilisation de machines virtuelles de série GS en tant que serveurs de base de données qu’il est obligatoire toouse stockage Premium pour les fichiers de journaux de transaction et de données base de données

Vous pouvez trouver des configurations de processeur et mémoire mêmes hello dans différentes séries de machines virtuelles. Néanmoins, lorsque vous recherchez des performances hello de ces ordinateurs virtuels en dehors de la série de différentes hello, elles peuvent différer considérablement. Bien qu’ils aient hello même configuration de l’UC et de la mémoire. Du fait que hello sous-jacent hôte matériel de serveur introduction hello de différents types de machine virtuelle hello a les caractéristiques de débit différentes.  Généralement différence hello indiqué dans les performances de débit également est répercutée dans les prix hello Hello différentes machines virtuelles.

Veuillez noter que pas toutes différentes séries de machines virtuelles pourront être offertes dans chacun d’eux de hello régions Azure (pour les régions Azure consultez le chapitre suivant). Sachez également que toutes les machines virtuelles ou séries de machines virtuelles ne sont pas certifiées pour SAP.

> [!IMPORTANT]
> Pour une utilisation hello les applications basées sur SAP NetWeaver, seul sous-ensemble hello des types de machine virtuelle et des configurations répertoriées dans la Note SAP [1928533] sont pris en charge.
>
>

### <a name="be80d1b9-a463-4845-bd35-f4cebdb5424a"></a>Régions Azure
Microsoft permet toodeploy Machines virtuelles en soi-disant « régions Azure ». Une région Azure peut correspondre à un ou plusieurs centres de données situés à proximité les uns des autres. Pour la plupart des hello géopolitiques régions dans Bonjour Microsoft a au moins deux régions Azure. Par exemple, l’Europe contient les régions Azure « Europe du Nord » et « Europe de l’Ouest ». Ces deux régions Azure dans une région géopolitique sont séparées par une distance suffisamment significative afin que des catastrophes naturelles ou techniques n’affectent pas les deux régions Azure Bonjour même région géopolitique. Étant donné que Microsoft est en création de nouvelles régions Azure dans différentes régions géopolitiques globalement, nombre de hello de ces régions est en constante augmentation et depuis décembre 2015 atteint le nombre de hello de 20 régions Azure avec d’autres régions annoncées déjà. Comme un client peut déployer des systèmes SAP dans ces régions, y compris des régions Azure hello deux en Chine. En cours de toodate plus d’informations sur les régions Azure consultez ce site Web : <https://azure.microsoft.com/regions/>

### <a name="8d8ad4b8-6093-4b91-ac36-ea56d80dbf77"></a>Hello Concept de Machine virtuelle Microsoft Azure
Microsoft Azure offre une Infrastructure en tant qu’un toohost de solution de Service (IaaS) Machines virtuelles avec des fonctionnalités similaires en tant qu’une solution de virtualisation sur site. Vous êtes en mesure de toocreate Machines virtuelles à partir de hello portail Azure, PowerShell ou CLI, qui proposent également des fonctionnalités de gestion et de déploiement.

Le Gestionnaire de ressources Azure vous permet de tooprovision vos applications à l’aide d’un modèle déclaratif. Dans un modèle unique, vous pouvez déployer plusieurs services ainsi que leurs dépendances. Vous utilisez hello même modèle toorepeatedly déployer votre application au cours de chaque étape du cycle de vie d’application hello.

Vous trouverez plus d’informations sur les modèles ARM ici :

* [Déployer et gérer des ordinateurs virtuels à l’aide de modèles Azure Resource Manager et hello CLI d’Azure][virtual-machines-linux-cli-deploy-templates]
* [Gestion des machines virtuelles à l’aide de modèles Azure Resource Manager et de PowerShell][virtual-machines-deploy-rmtemplates-powershell]
* <https://azure.microsoft.com/documentation/templates/>

Une autre fonctionnalité intéressante est images de toocreate hello possibilité à partir d’ordinateurs virtuels, ce qui vous permet de tooprepare certain référentiels à partir de laquelle vous êtes tooquickly en mesure de déploiement les instances de machine virtuelle qui répondent à vos besoins.

Pour plus d’informations sur la création d’images à partir de machines virtuelles, consultez [cet article (Windows)][virtual-machines-windows-capture-image] ou [celui-ci (Linux)][virtual-machines-linux-capture-image].

#### <a name="df49dc09-141b-4f34-a4a2-990913b30358"></a>Domaines d’erreur
Domaines d’erreur représentent une unité physique de l’échec, toohello très proches d’infrastructure physique contenu dans des centres de données, et pendant une lame physique ou un rack peut être considéré comme un domaine d’erreur, il n’existe aucun mappage direct entre deux de hello.

Lorsque vous déployez plusieurs Machines virtuelles dans le cadre d’un système SAP dans Microsoft Azure Virtual Machine Services, vous pouvez influencer toodeploy de contrôleur de structure Azure hello votre application dans différents domaines d’erreur, répondant ainsi aux exigences de hello de hello Contrat SLA de Microsoft Azure. Toutefois, hello distribution des domaines d’erreur sur une unité d’échelle Azure (collection de centaines de nœuds de calcul ou de nœuds de stockage et de mise en réseau) ou l’attribution de machines virtuelles tooa hello domaine d’erreur spécifique est un élément sur lequel vous n’avez pas contrôle direct. Dans l’ordre toodirect hello Azure fabric contrôleur toodeploy un ensemble de machines virtuelles sur différents domaines d’erreur, vous devez tooassign une toohello à haute disponibilité Azure VMs au moment du déploiement. Pour plus d’informations sur les groupes à haute disponibilité Azure, voir le chapitre [Groupes à haute disponibilité Azure][planning-guide-3.2.3] dans ce document.

#### <a name="fc1ac8b2-e54a-487c-8581-d3cc6625e560"></a>Domaines de mise à niveau
Domaines de mise à niveau constituent une unité logique qui aident à la mise à jour une machine virtuelle dans un système SAP, qui se compose d’instances SAP s’exécutant sur plusieurs machines virtuelles, de toodetermine. Lorsqu’une mise à niveau se produit, Microsoft Azure exécute hello les processus de mise à jour de ces domaines de mise à niveau un par un. En répartissant les machines virtuelles dans différents domaines de mise à niveau au moment du déploiement, vous pouvez protéger, en partie, votre système SAP des interruptions potentielles. Dans commande tooforce toodeploy Azure VMs hello d’un système SAP réparties sur différents domaines de mise à niveau, vous devez tooset un attribut spécifique au moment du déploiement de chaque machine virtuelle. Domaines tooFault similaires, une unité d’échelle Azure est divisé en plusieurs domaines de mise à niveau. Dans l’ordre toodirect hello Azure fabric contrôleur toodeploy un ensemble de machines virtuelles sur différents domaines de mise à niveau, vous devez tooassign une toohello à haute disponibilité Azure VMs au moment du déploiement. Pour plus d’informations sur les groupes à haute disponibilité Azure, voir le chapitre[ Groupes à haute disponibilité Azure][planning-guide-3.2.3] ci-dessous.

#### <a name="18810088-f9be-4c97-958a-27996255c665"></a>Groupes à haute disponibilité Azure
Machines virtuelles au sein d’un à haute disponibilité Azure seront distribuées par hello contrôleur de structure Azure sur différents domaines d’erreur et mettre à niveau. Hello distribution hello sur différents domaines d’erreur et mettre à niveau vise tooprevent que toutes les machines virtuelles d’un système SAP d’être arrêtés dans le cas de hello de maintenance de l’infrastructure ou d’un échec dans un domaine d’erreur. Par défaut, les machines virtuelles ne font pas partie d’un groupe à haute disponibilité. la participation de Hello d’une machine virtuelle dans un ensemble de disponibilité est définie au moment du déploiement ou ultérieurement par une reconfiguration et le redéploiement d’une machine virtuelle.

concept de hello toounderstand de façon à haute disponibilité Azure et hello relation entre les groupes de disponibilité tooFault et les domaines de mise à niveau, veuillez lire [cet article][virtual-machines-manage-availability]

consultez des groupes à haute disponibilité toodefine pour ARM via un modèle json [hello des spécifications de l’api rest](https://github.com/Azure/azure-rest-api-specs/blob/master/arm-compute/2015-06-15/swagger/compute.json) et recherchez « availability ».

### <a name="a72afa26-4bf4-4a25-8cf7-855d6032157f"></a>Stockage : Microsoft Azure Storage et disques de données
Les Microsoft Azure Virtual Machines utilisent différents types de stockage. Quand vous implémentez SAP sur Azure Virtual Machine Services, il est important toounderstand les différences de hello entre ces deux principaux types de stockage :

* stockage volatil non persistant ;
* stockage persistant.

stockage non permanent de Hello est directement attaché toohello Machines virtuelles en cours d’exécution et réside sur les nœuds de calcul hello proprement dits : stockage d’instance local hello (temporaire). taille de Hello dépend de la taille de hello Hello Machine virtuelle choisie au démarrage du déploiement de hello. Ce type de stockage est volatil et par conséquent hello disque initialisé au redémarrage d’une instance de Machine virtuelle. En règle générale, fichier d’échange hello hello système d’exploitation se trouve sur ce disque temporaire.

- - -
> ![Windows][Logo_Windows] Windows
>
> Sur les machines virtuelles Windows lecteur temp de hello est monté en tant que lecteur D:\ dans une machine virtuelle déployée.
>
> ![Linux][Logo_Linux] Linux
>
> Sur les machines virtuelles Linux, il est monté en tant que/mnt/resource ou /mnt. Vous trouverez plus de détails ici :
>
> * [Comment tooAttach un tooa de disque de données Machine virtuelle Linux][virtual-machines-linux-how-to-attach-disk]
> * <http://blogs.msdn.com/b/mast/archive/2013/12/07/understanding-the-temporary-drive-on-windows-azure-virtual-machines.aspx>
>
>

- - -
lecteur Hello est volatile, car il est stocké sur le serveur hôte de hello proprement dit. Si hello VM déplacé dans un redéploiement (par exemple, échéance toomaintenance sur l’hôte de hello ou l’arrêt et redémarrage) le contenu du lecteur de hello hello est perdu. Par conséquent, il n’est pas une option toostore toutes les données importantes sur ce lecteur. type de média utilisé pour ce type de stockage de Hello diffère entre différentes séries de machines virtuelles avec les caractéristiques de performances très différentes qui depuis juin 2015 ressemblent à :

* A5-A7 : performances très limitées. Déconseillées pour le stockage autre que celui de fichier d’échange.
* A8-A11 : très bonnes caractéristiques de performances avec quelque 10 000 E/S par seconde et un débit supérieur à 1 Go/s.
* Série D : très bonnes caractéristiques de performances, avec quelque 10 000 E/S par seconde et un débit supérieur à 1 Go/s.
* Série DS : très bonnes caractéristiques de performances, avec quelque 10 000 E/S par seconde et un débit supérieur à 1 Go/s.
* Série G : très bonnes caractéristiques de performances, avec quelque 10 000 E/S par seconde et un débit supérieur à 1 Go/s.
* Série GS : très bonnes caractéristiques de performances, avec quelque 10 000 E/S par seconde et un débit supérieur à 1 Go/s.

Les instructions ci-dessus appliquez des types de machine virtuelle toohello certifiées avec SAP. Hello séries de machines virtuelles avec une excellente IOPS et le débit qualifier pour tirer parti de certaines fonctionnalités du SGBD. Consultez hello [Guide de déploiement de système SGBD] [ dbms-guide] pour plus d’informations.

Microsoft Azure Storage fournit persistante hello et stockage des niveaux de protection et de redondance généralement constatés sur un stockage SAN. Disques basés sur le stockage Azure sont un disque dur virtuel (VHD) situé dans les Services de stockage Azure hello. Hello du système d’exploitation-disque local (C: de Windows\, Linux / (/ dev/sda1)) est stocké sur hello le stockage Azure et les Volumes/disques supplémentaires monté toohello VM obtenir y sont stockées, trop.

Il est possible de tooupload un disque dur virtuel existant sur site ou créer des conteneurs vides depuis Azure et attacher ces machines virtuelles toodeployed. Ces disques durs virtuels sont référencés en tant que disques Azure.

Après avoir créé ou téléchargement d’un disque dur virtuel dans le stockage Azure, il est possible toomount et attacher ces tooan existant de machines virtuelles et toocopy existants (démonté) de disque dur virtuel.

Comme ces disques durs virtuels sont conservés, les données et les modifications dans ceux-ci sont protégées lors du redémarrage et de la nouvelle création d’une instance de machine virtuelle. Même si une instance est supprimée, ces disques durs virtuels demeurent sécurisés et peuvent être redéployés ou dans le cas des disques du système d’exploitation non peuvent être monté tooother VMs.

Au sein de hello réseau des niveaux de stockage Azure redondance différents peut être configuré :

* Niveau minimal qui peut être sélectionné est 'redondance locale », qui est équivalent toothree-réplica des données hello dans hello même centre de données d’une région Azure (consultez le chapitre [régions Azure][planning-guide-3.1]).
* Stockage redondant dans une zone qui est réparties entre différents centres de données dans les images hello trois hello même région Azure.
* Niveau de redondance de valeur par défaut est la redondance géographique qui réplique de façon asynchrone le contenu hello dans un autre images 3 de données hello dans une autre région Azure qui est hébergé dans hello même région géopolitique.

Consultez également la table hello au-dessus de cet article dans les options de redondance différents toohello ce qui concerne : <https://azure.microsoft.com/pricing/details/storage/>

Plus d’informations en ce qui concerne les tooAzure que stockage se trouve ici :

* <https://azure.microsoft.com/documentation/services/storage/>
* <https://azure.microsoft.com/services/site-recovery>
* <https://msdn.microsoft.com/library/windowsazure/ee691964.aspx>
* <https://blogs.msdn.com/b/azuresecurity/archive/2015/11/17/azure-disk-encryption-for-linux-and-windows-virtual-machines-public-preview.aspx>

#### <a name="azure-standard-storage"></a>Stockage Azure Standard
Le stockage Azure BLOB Standard lors de type hello de stockage IaaS Azure a été libéré. Des quotas d’E/S par seconde étaient appliqués pour chaque disque dur virtuel. En raison d’une latence n’était pas hello même classe, comme les périphériques SAN/NAS généralement déployés pour les systèmes haut de gamme SAP hébergée sur site. Néanmoins, les hello le stockage Azure Standard a été identifié comme suffisant pour des centaines de nombreux systèmes SAP pendant ce temps déployés dans Azure.

Le stockage Azure Standard est facturé en fonction de hello données réelles qui sont stockées, hello volume des transactions de stockage, les transferts de données sortantes et option de redondance choisi. Nombre de disques durs virtuels peuvent être créés au hello maximum à 1 To de taille, mais tant que ces derniers rester vides est gratuit. Si vous remplissez ensuite un VHD avec 100 Go, vous serez facturé pour le stockage de 100 Go et non pour hello de taille nominale hello avec que disque dur virtuel a été créé.

#### <a name="ff5ad0f9-f7f4-4022-9102-af07aef3bc92"></a>Azure Premium Storage
En avril 2015, Microsoft a introduit Stockage Premium Azure. Stockage Premium a été introduit avec hello objectif tooprovide :

* une meilleure latence d’E/S ;
* un meilleur débit ;
* une latence d’E/S plus stable.

À cette fin, de nombreuses modifications ont été introduites de quels hello deux principaux sont :

* Utilisation de disques SSD dans les nœuds de stockage Azure hello
* Un cache de lecture qui est sauvegardé par hello SSD local d’un nœud de calcul Azure

Dans opposé stockage tooStandard où les fonctionnalités n’ont pas changé dépend de la taille de hello du disque hello (ou disque dur virtuel), stockage Premium actuellement a 3 catégories de disque différent qui sont affichent à la fin de hello de cet article avant la section de hello FAQ : <https:/ /Azure.Microsoft.com/Pricing/Details/Storage/>

Vous voyez que débit/VHD IOPS/disque dur virtuel et le disque sont dépendantes de la catégorie de taille hello de disques de hello

Coût de base dans les cas de hello du stockage Premium n’est pas volume de données réelles hello stockée dans ces disques durs virtuels, mais la catégorie de taille hello de cet un disque dur virtuel, indépendamment de la quantité hello de données hello qui sont stockées dans hello disque dur virtuel.

Vous pouvez également créer des disques durs virtuels sur un stockage Premium ne sont pas directement mappage en catégories de taille hello indiqués. Cela peut être le cas de hello, particulièrement lors de la copie des disques durs virtuels à partir du stockage Standard dans le stockage Premium. Dans ce cas une mappage toohello plus grand stockage Premium disque option suivante est effectuée.

Sachez que seulement certaines séries de machines virtuelles peuvent bénéficier de hello stockage Azure Premium. Depuis décembre 2015, il s’agit de hello et GS-série DS. Hello série DS est fondamentalement hello même série D avec l’exception hello que la série DS a hello capacité toomount stockage Premium en fonction des machines virtuelles en outre tooVHDs qui sont hébergés sur le stockage Azure Standard. Même chose est valide pour la série G comparée tooGS-série.

Si vous retirez partie hello de machines virtuelles de hello série DS dans [cet article] [ virtual-machines-sizes] vous également bénéficiera que sont les limitations de volume de données tooPremium stockage VHD sur la granularité de niveau d’ordinateur virtuel hello hello. Différent de la série DS ou des machines virtuelles de série GS également ont différentes limitations exprimée en ce qui concerne les toohello disques durs virtuels qui peut être monté. Ces limites sont documentées dans article hello également indiqué ci-dessus. Mais elle signifie que si vous montez par exemple 32 tooa de disques/VHD x P30 seule DS14 machine virtuelle vous Impossible d’obtenir 32 x débit maximal de hello d’un disque P30. Au lieu de cela hello débit maximal sur le niveau de la machine virtuelle comme décrit dans l’article de hello limite le débit des données.

Pour plus d’informations sur le Stockage Premium, consultez la page : <http://azure.microsoft.com/blog/2015/04/16/azure-premium-storage-now-generally-available-2>

#### <a name="azure-storage-accounts"></a>Comptes Stockage Azure
Lors du déploiement de services ou de machines virtuelles dans Azure, le déploiement de disques durs virtuels et d’images de machine virtuelle doit être organisé dans des unités appelées comptes Stockage Azure. Lorsque vous planifiez un déploiement d’Azure, vous devez toocarefully tenir compte des restrictions de hello de Azure. Hello un côté, il est un nombre limité de comptes de stockage par abonnement Azure. Bien que chaque compte de stockage Azure peut contenir un grand nombre de fichiers de disque dur virtuel, il existe une limite donnée sur hello total IOPS par compte de stockage. Lorsque vous déployez des centaines de machines virtuelles SAP avec des systèmes SGBD création d’appels d’e/s importantes, il est recommandé de toodistribute machines virtuelles SGBD IOPS élevé entre plusieurs comptes de stockage Azure. Il convient pas tooexceed hello limite actuelle de comptes de stockage Azure par abonnement. Étant donné que le stockage est une partie vitale du déploiement de base de données hello pour un système SAP, ce concept est abordé plus en détail dans hello déjà référencé [Guide de déploiement de système SGBD][dbms-guide].

Pour plus d’informations sur les comptes de stockage Azure, consultez [cet article][storage-scalability-targets]. La lecture de cet article, vous bénéficiez des avantages qu’il existe des différences de limitations de hello entre les comptes de stockage Azure Standard et les comptes de stockage Premium. Principales différences sont volume hello de données qui peuvent être stockées dans un tel compte de stockage. Dans le stockage Standard volume de hello est une magnitude supérieure à stockage Premium. Sur hello autres hello côté compte de stockage Standard est strictement limitée IOPS (consultez la colonne « Taux de demandes Total »), tandis que le compte de stockage Azure Premium de hello n’a aucune limitation de ce type. Nous allons décrire les détails et les résultats de ces différences lorsque vous présentez des déploiements de systèmes SAP, notamment les serveurs de SGBD hello hello.

Dans un compte de stockage, vous avez hello possibilité toocreate des conteneurs différents à des fins de hello d’organisation et de classement différents disques durs virtuels. Ces conteneurs sont généralement utilisés tooe.g. Séparez les disques durs virtuels des différentes machines virtuelles. Peu importe le nombre de conteneurs que vous utilisez pour un seul compte Stockage Azure, les performances n’en seront pas affectées.

Dans Azure, un nom de disque dur virtuel suit hello suivant d’affectation de noms connexion nécessitant tooprovide un nom unique pour hello disque dur virtuel dans Azure :

    http(s)://<storage account name>.blob.core.windows.net/<container name>/<vhd name>

En tant que chaîne hello mentionnées ci-dessus toouniquely doit identifier hello disque dur virtuel qui est stocké sur le stockage Azure.

### <a name="61678387-8868-435d-9f8c-450b2424f5bd"></a>Mise en réseau Microsoft Azure
Microsoft Azure fournit une infrastructure de réseau qui permet la mise en correspondance de tous les scénarios que nous souhaitons hello toorealize avec les logiciels SAP. fonctionnalités de Hello sont :

* Accès à partir de hello extérieur, directement toohello machines virtuelles via les Services Windows Terminal Server ou de ssh/VNC
* Tooservices d’accès et des ports spécifiques utilisés par les applications dans des machines virtuelles de hello
* communication interne et résolution de noms entre un groupe de machines virtuelles déployées en tant que machines virtuelles Azure ;
* La connectivité intersite entre d’un client réseau local et hello réseau Azure
* connectivité entre le centre de données ou la région Azure entre les sites Azure.

Pour plus d’informations, consultez la page : <https://azure.microsoft.com/documentation/services/virtual-network/>

Il existe de nombreuses façons tooconfigure nom d’et résolution IP dans Azure. Dans ce document, les scénarios de Cloud uniquement s’appuient sur par défaut hello utilisant Azure DNS (en contraste toodefining un service DNS propre). Il existe également un nouveau service DNS Azure qui peut être utilisé au lieu de configurer votre propre serveur DNS. Pour plus d’informations, consultez [cet article][virtual-networks-manage-dns-in-vnet] et [cette page](https://azure.microsoft.com/services/dns/).

Pour les scénarios de coexistence que partent les faits hello qui hello local OpenLDAP/AD/DNS a été étendu via VPN ou connexion privée tooAzure. Pour certains scénarios décrits ici, il peut être nécessaire toohave un réplica AD/OpenLDAP installé dans Azure.

Étant donné que la mise en réseau et la résolution de noms est une partie vitale du déploiement de base de données hello pour un système SAP, ce concept est abordé plus en détail dans hello [Guide de déploiement de système SGBD][dbms-guide].

##### <a name="azure-virtual-networks"></a>Réseaux virtuels Azure
En créant un réseau virtuel Azure vous pouvez définir la plage d’adresses hello d’adresses IP privées hello allouée par la fonctionnalité Azure DHCP. Dans les scénarios de coexistence, plage d’adresses IP hello définie demeure allouée à l’aide de DHCP par Azure. Toutefois, la résolution de noms de domaine est effectuée localement (en supposant que les machines virtuelles de hello sont une partie d’un domaine local) et par conséquent, peut résoudre les adresses au-delà de différents Services Cloud Azure.

[comment]: <> (MSSedusch still needed? TÂCHES à l’origine à un réseau virtuel Azure a été liée tooan groupe d’affinités. Avec qui un réseau virtuel dans Azure a été restreint toohello unité d’échelle Azure que hello À que groupe d’affinités est-il attribué. En fin de hello, cette hello revient de réseau virtuel a été ressources toohello restreint Bonjour Azure unité d’échelle. Depuis, des modifications ont été apportées et les réseaux virtuels Azure peuvent désormais être étendus à plus d’une unité d’échelle Azure. Toutefois, il est nécessaire que les réseaux virtuels Azure ne soient **PLUS** associés à des groupes d’affinités lors de la création. Nous avons déjà mentionné que dans toorecommendations opposées un an, vous devez ** pas tirer parti des groupes d’affinités Azure plus **. Pour plus d’informations, consultez <https://azure.microsoft.com/blog/regional-virtual-networks/>)

Chaque Machine virtuelle dans Azure besoins toobe connecté tooa réseau virtuel.

Pour plus d’informations, consultez [cet article][resource-groups-networking] et [cette page](https://azure.microsoft.com/documentation/services/virtual-network/).

[comment]: <> (MShermannd, TODO n’a pas pu trouver un article qui comprend une rubrique de OpenLDAP hello + ARM ;)
[comment]: <> (MSSedusch &lt;https://channel9.msdn.com/Blogs/Open/Load-balancing-highly-available-Linux-services-on-Windows-Azure-OpenLDAP-and-MySQL&gt;)

> [!NOTE]
> Par défaut, une fois qu’un ordinateur virtuel est déployé, vous ne pouvez pas modifier configuration du réseau virtuel hello. les paramètres TCP/IP Hello doivent rester serveur DHCP Azure de toohello. Le comportement par défaut est l’attribution d’adresse IP dynamique.
>
>

adresse MAC de Hello de carte de réseau virtuel hello peut-être changer, par exemple après Windows hello et de redimensionner ou système d’exploitation invité de Linux prennent en charge les cartes réseau nouvelle hello et utilise automatiquement DHCP tooassign hello DNS les adresses IP et dans ce cas.

##### <a name="static-ip-assignment"></a>Attribution d’adresse IP statique
Il est possible de tooassign fixée ou tooVMs au sein d’un réseau virtuel Azure d’adresses IP réservées. Machines virtuelles de hello en cours d’exécution dans un réseau virtuel Azure s’ouvre un tooleverage possibilité excellent cette fonctionnalité si nécessaire ou requis pour certains scénarios. attribution d’adresses IP Hello reste valable pour l’ensemble de l’existence de hello Hello machine virtuelle, indépendamment de si hello machine virtuelle est en cours d’exécution ou de l’arrêt. Par conséquent, vous devez tootake hello nombre total de machines virtuelles (machines virtuelles en cours d’exécution et arrêtés) en compte lors de la définition hello plage d’adresses IP pour hello réseau virtuel. adresse IP de Hello reste associé jusqu'à la suppression hello machine virtuelle et son Interface réseau ou jusqu'à ce que l’adresse IP de hello est désallouée à nouveau. Pour des informations détaillées, consultez [cet article][virtual-networks-static-private-ip-arm-pportal].

##### <a name="multiple-nics-per-vm"></a>Plusieurs cartes d’interface réseau par machine virtuelle
Vous pouvez définir plusieurs cartes d’interface de réseau virtuel pour une machine virtuelle Azure. Hello capacité toohave plusieurs cartes réseau permet de démarrer tooset de séparation du trafic réseau où par exemple, le trafic du client est routé via une carte réseau et le trafic du serveur principal est routé via une carte réseau virtuelle deuxième. En fonction de type hello de l’ordinateur virtuel comporte des limites différentes ce qui concerne le nombre toohello de cartes réseau. Vous trouverez des informations précises et des renseignements sur les fonctions et les restrictions dans ces articles :

* [Créer une machine virtuelle avec plusieurs cartes d’interface réseau][virtual-networks-multiple-nics]
* [Déployer des machines virtuelles avec plusieurs cartes réseau à l’aide d’un modèle][virtual-network-deploy-multinic-arm-template]
* [Déployer des machines virtuelles avec plusieurs cartes réseau à l’aide de PowerShell][virtual-network-deploy-multinic-arm-ps]
* [Déployer des machines virtuelles de cartes réseau multiples à l’aide de hello CLI d’Azure][virtual-network-deploy-multinic-arm-cli]

#### <a name="site-to-site-connectivity"></a>Connectivité de site à site
La connectivité intersite consiste à lier, via une connexion VPN transparente et permanente, les machines virtuelles Azure et les sites locaux. Il est attendu toobecome hello courants modèle de déploiement SAP dans Azure. hypothèse de Hello est que les procédures d’exploitation et les processus avec des instances SAP dans Azure doivent fonctionner en toute transparence. Cela signifie que vous devez être en mesure de tooprint depuis ces systèmes, ainsi que hello tootransport de système de gestion de Transport SAP (TMS) change à partir d’un système de développement dans le système de test tooa Azure est déployé sur site. Pour plus d’informations sur la connectivité intersite, consultez [cet article][vpn-gateway-create-site-to-site-rm-powershell]

##### <a name="vpn-tunnel-device"></a>Tunnel VPN
Dans commande toocreate une connexion site à site (local données center tooAzure centre de données), vous devez tooeither obtenir et configurer un périphérique VPN ou utiliser le routage et accès distant Service (RRAS) qui a été introduit en tant que composant logiciel avec Windows Server 2012.

* [Créer un réseau virtuel avec une connexion VPN site à site à l’aide de PowerShell][vpn-gateway-create-site-to-site-rm-powershell]
* [À propos des périphériques VPN pour les connexions de la passerelle VPN de site à site][vpn-gateway-about-vpn-devices]
* [FAQ sur la passerelle VPN][vpn-gateway-vpn-faq]

![Connexion de site à site entre des systèmes locaux et dans Azure][planning-guide-figure-600]

Hello Figure ci-dessus montre deux abonnements Azure ont des sous-plages d’adresse IP réservée pour une utilisation dans des réseaux virtuels dans Azure. connectivité Hello de hello local tooAzure de réseau est établie via VPN.

#### <a name="point-to-site-vpn"></a>VPN de point à site
Point-to-site VPN requiert chaque tooconnect d’ordinateur client avec son propre réseau privé virtuel dans Azure. Pour des scénarios SAP hello que nous étudions, la connectivité de point à site n’est pas pratique. Par conséquent, aucune référence supplémentaire n’a connectivité VPN de site à toopoint.

[comment]: <> (MSSedusch -- More information can be found here)
[comment]: <> (MShermannd TODO Link no longer valid; But ARM is anyway not supported - see next link below)
[comment]: <> (MSSedusch -- &lt;http://msdn.microsoft.com/library/azure/dn133798.aspx&gt;.)
[comment]: <> (TooSite MShermannd TODO Point ne pas encore pris en charge avec ARM)
[comment]: <> (MSSedusch -- &lt;https://azure.microsoft.com/documentation/articles/vpn-gateway-point-to-site-create/&gt;)

#### <a name="multi-site-vpn"></a>VPN multisite
Azure propose également de nos connectivité de VPN multisite toocreate hello possibilité pour un abonnement Azure. Un seul abonnement était auparavant une connexion VPN de site à site tooone limité. Cette limitation a disparu et vous pouvez désormais bénéficier de connexions VPN multisites par abonnement. Il est ainsi possible de tooleverage plus d’une région Azure pour un abonnement spécifique par le biais des configurations intersite.

Pour plus d’informations, consultez [cet article][vpn-gateway-create-site-to-site-rm-powershell]

[comment]: <> (MShermannd TODO found no ARM docu link)

#### <a name="vnet-toovnet-connection"></a>Réseau virtuel tooVNet connexion
À l’aide de VPN multisite, vous devez tooconfigure un réseau virtuel Azure distinct dans chacune des régions de hello. Toutefois très souvent, vous avez besoin de hello des composants logiciels hello dans des régions différentes hello doivent communiquer entre eux. Dans l’idéal, cette communication ne doit pas être acheminée à partir d’une région Azure tooon local et en provenance toohello il autre région Azure. tooshortcut, Azure offre hello possibilité tooconfigure une connexion à partir d’un réseau virtuel Azure dans une région tooanother que réseau virtuel Azure hébergé dans une autre région. Cette fonctionnalité est appelée connexion de réseau virtuel à réseau virtuel. Pour plus d’informations sur cette fonctionnalité, consultez : <https://azure.microsoft.com/documentation/articles/vpn-gateway-vnet-vnet-rm-ps/>.

#### <a name="private-connection-tooazure--expressroute"></a>TooAzure de connexion privée – ExpressRoute
Microsoft Azure ExpressRoute permet la création de hello des connexions privées entre des centres de données Azure et l’infrastructure du client hello-locale ou dans un environnement de colocalisation. ExpressRoute est proposé par divers fournisseurs VPN (commutation de paquets) MPLS ou d’autres fournisseurs de services réseau. Les connexions ExpressRoute ne sont pas établies via hello Internet public. Et offrent une sécurité accrue, une fiabilité accrue via plusieurs circuits parallèles, des débits plus importants et des latences moindres rapport aux connexions classiques sur Internet de hello.

Vous trouverez plus d’informations sur Azure ExpressRoute et les offres ici : 

* <https://azure.microsoft.com/documentation/services/expressroute/>
* <https://azure.microsoft.com/pricing/details/expressroute/>
* <https://azure.microsoft.com/documentation/articles/expressroute-faqs/>

ExpressRoute permet d’utiliser plusieurs abonnements Azure via un seul circuit ExpressRoute, comme décrit ici

* <https://azure.microsoft.com/documentation/articles/expressroute-howto-linkvnet-arm/>
* <https://azure.microsoft.com/documentation/articles/expressroute-howto-circuit-arm/>

#### <a name="forced-tunneling-in-case-of-cross-premises"></a>Tunneling forcé en cas de scénario intersite
Pour les ordinateurs virtuels de l’adhésion à des domaines sur site à site à site, point-to-site ou ExpressRoute, vous devez toomake assurer que les paramètres de proxy Internet hello sont déployés pour tous les utilisateurs de hello dans ces machines virtuelles ainsi. Par défaut, les logiciels exécutés dans ces machines virtuelles ou les utilisateurs à l’aide d’un Bonjour tooaccess de navigateur internet ne passe pas par le proxy d’entreprise hello, mais qu’il se connecte directement par le biais d’Azure toohello internet. Mais le paramètre de proxy même hello n’est pas un solution de 100 % toodirect hello du trafic via le proxy d’entreprise hello, car il incombe de logiciels et services toocheck pour le proxy de hello. Si le logiciel en cours d’exécution dans la machine virtuelle de hello n'est pas cette opération ou qu’un administrateur manipule les paramètres de hello, toohello de trafic Internet peut être à nouveau détournée directement par le biais d’Azure toohello Internet.

Dans commande tooavoid cela, vous pouvez configurer la Tunneling forcé avec une connectivité de site à site entre Azure et locaux. Hello description détaillée de la fonctionnalité de Tunneling forcé hello est publiée ici <https://azure.microsoft.com/documentation/articles/vpn-gateway-forced-tunneling-rm/>

Tunneling forcé avec ExpressRoute est activé par des clients annonçant un itinéraire par défaut via hello BGP ExpressRoute sessions d’homologation.

#### <a name="summary-of-azure-networking"></a>Résumé de la mise en réseau Azure
Ce chapitre abordait plusieurs points importants sur la mise en réseau Azure. Voici un résumé des points principaux de hello :

* Réseaux virtuels Azure permet de tooset réseau hello en fonction des besoins propres tooyour
* Réseaux virtuels Azure peut être exploitée tooassign IP adresse plages tooVMs ou affecter tooVMs d’adresses IP fixes
* tooset configuration d’un Site à Site ou d’une connexion de Point-To-Site vous devez tout d’abord les toocreate un réseau virtuel Azure
* Une fois qu’un ordinateur virtuel a été déployé. il n’est plus hello toochange possible de que réseau virtuel affecté toohello machine virtuelle

### <a name="quotas-in-azure-virtual-machine-services"></a>Quotas dans Azure Virtual Machine Services
Nous avons besoin toobe effacer sur les faits hello que le stockage hello et l’infrastructure réseau est partagée entre les ordinateurs virtuels en cours d’exécution une variété de services Bonjour infrastructure Azure. Et, comme dans des centres de données hello du client, un approvisionnement de certains des ressources d’infrastructure hello prend place tooa degré. Hello plateforme Microsoft Azure utilise le disque, du processeur, réseau et autres quotas toolimit hello la consommation des ressources toopreserve des performances cohérentes et déterministes.  Hello différents types de machine virtuelle (A5, A6, etc.) ont des quotas différents pour le nombre de hello de disques, processeur, mémoire RAM et du réseau.

> [!NOTE]
> Ressources processeur et mémoire de types de machine virtuelle hello pris en charge par SAP sont pré-allouées sur les nœuds d’hôte hello. Cela signifie qu’une fois hello machine virtuelle est déployée, les ressources hello sur l’ordinateur hôte de hello seront disponibles comme défini par hello type d’ordinateurs virtuels.
>
>

Lorsque la planification et le dimensionnement de SAP sur les solutions Azure hello quotas pour chaque taille de machine virtuelle doit être pris en compte.  Décrit des quotas de machine virtuelle Hello [ici][virtual-machines-sizes].

les quotas de Hello décrits représentent les valeurs maximales théoriques de hello.  limite de Hello d’IOPS par disque dur virtuel peut être obtenu avec IOs petits (8 Ko), mais ne peut peut-être pas être atteint avec IOs volumineux (1 Mo).  limite d’IOPS Hello est appliquée à l’échelle de hello d’un disque dur virtuel.

Comme un toodecide d’arbre de décision approximative si un système SAP s’adapte à Azure Virtual Machine Services et ses fonctionnalités ou si un système existant doit toobe configuré différemment dans un système de hello commande toodeploy sur Azure, arbre de décision hello ci-dessous peut être utilisé :

![La décision d’arborescence toodecide capacité toodeploy SAP sur Azure][planning-guide-figure-700]

**Étape 1**: hello plus importantes informations toostart avec est hello saps pour un système SAP donné. Hello SAP exigences besoin toobe séparée dans hello SGBD partie et hello SAP application, même si hello système SAP est déjà déployé localement dans une configuration de couche 2. Pour les systèmes existants, hello SAP liées toohello matériel utilisé souvent peut être déterminé ou estimé en fonction de tests d’évaluation SAP existants. résultats de Hello se trouve ici : <http://global.sap.com/campaigns/benchmark/index.epx>.
Pour les systèmes SAP nouvellement déployés, vous devez avoir effectué un exercice de dimensionnement qui doit déterminer la configuration requise hello du système de hello.
Consultez également ce blog et le document joint concernant le dimensionnement de SAP sur Azure : <http://blogs.msdn.com/b/saponsqlserver/archive/2015/12/01/new-white-paper-on-sizing-sap-solutions-on-azure-public-cloud.aspx>

**Étape 2**: pour les systèmes existants, hello volume d’e/s et d’opérations d’e/s par seconde sur le serveur de SGBD hello doivent être mesurées. Pour les systèmes qui vient d’être planifiés, hello dimensionnement exercice pour le nouveau système de hello également doit donner un aperçu des exigences d’e/s de hello sur hello côté SGBD. En cas de doute, vous devez éventuellement tooconduct une preuve de Concept.

**Étape 3**: configuration requise des SAP comparaison hello pour hello serveur SGBD aux hello SAP hello différents types de machine virtuelle de Azure peut fournir. des informations sur SAP Hello de différents types de machine virtuelle Azure hello sont documentées dans la Note SAP [1928533]. le focus de Hello hello DBMS VM doit être tout d’abord, car la couche de base de données hello est la couche de hello dans un système SAP NetWeaver qui n’évolue pas de majorité hello des déploiements. En revanche, couche d’application hello SAP peut être monté en charge. Si aucun des hello SAP pris en charge les types de machine virtuelle Azure peuvent offrir une SAP de hello requis, la charge de travail hello du système SAP de hello planifié ne peut pas être exécuté sur Azure. Vous devez soit toodeploy hello système local ou volume de charge de travail toochange hello pour système de hello.

**Étape 4** : comme indiqué [ici][virtual-machines-sizes], Azure applique un quota d’E/S par seconde par disque dur virtuel, que vous utilisiez un stockage Standard ou Premium. Dépend hello type d’ordinateurs virtuels, nombre hello de disques durs virtuels qui peut être monté varie. Par conséquent, vous pouvez calculer un nombre d’IOPS maximal qui peut être réalisé avec chacun des types de machine virtuelle hello. Dépend de la structure des fichiers de base de données hello, vous pouvez distribuer des disques durs virtuels toobecome un volume dans le système d’exploitation invité de hello. Toutefois, si le volume hello de IOPS actuel d’un système SAP déployé dépasse les limites de hello calculé du type de machine virtuelle plus grande hello d’Azure et s’il n’existe aucun toocompensate risque plus de mémoire, la charge de travail hello Hello système SAP peut être sensiblement. Dans ce cas, vous pouvez appuyer sur un point où vous ne devez pas déployer système hello sur Azure.

**Étape 5**: en particulier dans SAP systèmes qui sont déployés localement dans les configurations à 2 couches, hello chances que système de hello peut-être toobe configuré sur Azure dans une configuration de niveau 3. Dans cette étape, vous devez toocheck s’il existe un composant dans la couche d’application hello SAP qui ne peut pas être monté en charge et qui est plus grande que hello du processeur et mémoire ressources hello autre offre les types de machine virtuelle Azure. S’il existe un tel composant, système SAP hello et sa charge de travail ne peut pas être déployés dans Azure. Mais si vous pouvez monter en charge hello application SAP composants dans plusieurs machines virtuelles Azure, système de hello peuvent être déployés dans Azure.

**Étape 6**: si hello SGBD et les composants de la couche application SAP peuvent être exécutés dans des machines virtuelles Azure, configuration de hello doit toobe définie aux :

* Nombre de machines virtuelles Azure
* Types de machine virtuelle pour les composants individuels hello
* Nombre de disques durs virtuels de DBMS VM tooprovide suffisamment d’IOPS

## <a name="managing-azure-assets"></a>Gestion des ressources Azure
### <a name="azure-portal"></a>Portail Azure
Hello portail Azure est l’un des déploiements de machine virtuelle Azure de trois interfaces toomanage. tâches de gestion de base de Hello, comme le déploiement de machines virtuelles à partir d’images, peuvent être effectuées via hello portail Azure. En outre, la création de comptes de stockage, les réseaux virtuels et les autres composants Azure hello sont également hello tâches Azure portail peut très bien gérer. Toutefois, des fonctionnalités telles que le téléchargement de disques durs virtuels à partir des locaux tooAzure ou copie d’un disque dur virtuel dans Azure sont des tâches qui nécessitent des outils tiers ou administration via PowerShell ou CLI.

![Portail Microsoft Azure - vue d’ensemble de la machine virtuelle][planning-guide-figure-800]

[comment]: <> (MSSedusch * &lt;https://azure.microsoft.com/documentation/articles/virtual-networks-create-vnet-arm-pportal/&gt;)
[comment]: <> (MSSedusch * &lt;https://azure.microsoft.com/documentation/articles/virtual-machines-windows-tutorial/&gt;)

Tâches d’administration et de configuration de Machine virtuelle hello sont possibles à partir de hello portail Azure.

Outre redémarrer et arrêter une Machine virtuelle vous pouvez également attacher, détacher et créer des disques de données pour l’instance de Machine virtuelle hello, instance de hello toocapture pour la préparation de l’image et configurer hello taille de l’instance de Machine virtuelle hello.

Hello portail Azure fournit des fonctionnalités de base toodeploy et configurer les ordinateurs virtuels et nombreux autres services Azure. Cependant pas toutes les fonctionnalités disponibles sont couverte par hello portail Azure. Bonjour portail Azure, il n’est pas possible tooperform des tâches telles que :

* Téléchargement de disques durs virtuels tooAzure
* la copie de machines virtuelles.

[comment]: <> (MShermannd TODO what about automation service for SAP VMs ? )
[comment]: <> (MSSedusch deployment of multiple VMs os meanwhile possible)
[comment]: <> (MSSedusch également n’importe quel type d’automatisation concernant le déploiement n’est pas possible avec hello portail Azure. Des tâches telles que des scripts de déploiement de plusieurs machines virtuelles n’est pas possible via hello portail Azure.)

### <a name="management-via-microsoft-azure-powershell-cmdlets"></a>Gestion par le biais des applets de commande Microsoft Azure PowerShell
Windows PowerShell est une infrastructure puissante et extensible, largement adoptée par les clients qui déploient un nombre plus important de systèmes dans Azure. Après l’installation de hello d’applets de commande PowerShell sur le bureau, ordinateur portable ou station de gestion dédiée, hello applets de commande PowerShell peut être exécuté à distance.

Hello processus tooenable bureau/portable local pour l’utilisation de hello des applets de commande PowerShell de Azure et comment tooconfigure celles hello d’utilisation avec hello Azure ou les abonnements sont décrit dans [cet article][powershell-install-configure].

Les étapes plus détaillées sur le tooinstall, mettre à jour et configurer les applets de commande PowerShell Azure hello figurent également dans [ce chapitre du Guide de déploiement de hello][deployment-guide-4.1].

Expérience utilisateur a jusqu'à présent été que PowerShell (PS) constitue certainement hello plus puissant outil toodeploy machines virtuelles et toocreate personnalisé étapes de déploiement hello de machines virtuelles. Tous les clients hello exécutant des instances SAP dans Azure sont à l’aide des tâches de gestion de toosupplement applets de commande PS ils dans hello portail Azure ou sont même à l’aide d’applets de commande PS exclusivement toomanage leurs déploiements dans Azure. Étant donné que le partage des applets de commande Azure spécifique hello hello même convention d’affectation de noms que hello plus de 2 000 applets de commande Windows, il est facile de tâche pour Windows administrateurs tooleverage ces applets de commande.

Consultez l’exemple présenté ici : <http://blogs.technet.com/b/keithmayer/archive/2015/07/07/18-steps-for-end-to-end-iaas-provisioning-in-the-cloud-with-azure-resource-manager-arm-powershell-and-desired-state-configuration-dsc.aspx>

[comment]: <> (MShermannd TODO describe new CLI command when tested )
Déploiement de hello Extension de surveillance Azure pour SAP (voir le chapitre [Solution de surveillance Azure pour SAP] [ planning-guide-9.1] dans ce document) est uniquement possible via PowerShell ou CLI. Par conséquent, il est obligatoire toosetup et configurez PowerShell ou CLI lors du déploiement ou d’administration d’un système SAP NetWeaver dans Azure.  

Comme Azure fournit davantage de fonctionnalités, nouvelles applets de commande PS allez toobe ajouté qui requiert une mise à jour des applets de commande hello. Il est donc hello toocheck de sens site de téléchargement Azure au moins une fois les mois hello <https://azure.microsoft.com/downloads/> pour une nouvelle version des applets de commande hello. nouvelle version de Hello sera installée uniquement sur une version antérieure de hello.

Pour une liste générale des commandes Azure PowerShell, consultez : <https://msdn.microsoft.com/library/azure/dn708514.aspx>.

### <a name="management-via-microsoft-azure-cli-commands"></a>Gestion à l’aide des commandes CLI Microsoft Azure
Pour les clients qui utilisent Linux et qui veulent toomanage Azure ressources Powershell ne peuvent pas être une option. Microsoft propose la CLI Microsoft Azure en guise d’alternative.
Hello CLI d’Azure fournit un ensemble d’open source d’inter-plateformes commandes sur l’utilisation de hello plateforme Azure. Hello CLI d’Azure fournit la majeure partie de hello même fonctionnalité trouvée dans hello portail Azure.

Pour plus d’informations sur l’installation, la configuration et le fonctionnement des commandes toouse CLI tooaccomplish tâches Azure, consultez

* [Installer hello CLI d’Azure][xplat-cli]
* [Déployer et gérer des ordinateurs virtuels à l’aide de modèles Azure Resource Manager et hello CLI d’Azure][virtual-machines-linux-cli-deploy-templates]
* [Utilisez hello CLI d’Azure pour Mac, Linux et Windows avec Azure Resource Manager][xplat-cli-azure-resource-manager]

Consultez également le chapitre [CLI d’Azure pour les machines virtuelles Linux] [ deployment-guide-4.5.2] Bonjour [Guide de déploiement] [ planning-guide] sur la façon dont toouse CLI d’Azure toodeploy hello Azure Extension de surveillance pour SAP.

## <a name="different-ways-toodeploy-vms-for-sap-in-azure"></a>Toodeploy de façons différentes machines virtuelles pour SAP dans Azure
Dans ce chapitre, vous allez apprendre toodeploy de différentes façons hello une machine virtuelle dans Azure. Des procédures de préparation supplémentaires, ainsi que la gestion des disques durs virtuels et des machines virtuelles dans Azure, sont présentées dans ce chapitre.

### <a name="deployment-of-vms-for-sap"></a>Déploiement de machines virtuelles pour SAP
Microsoft Azure offre plusieurs méthodes de machines virtuelles de toodeploy et de disques associés. Il est donc les différences de hello toounderstand très important, car la préparation des machines virtuelles de hello peut-être différer selon la méthode hello de déploiement. En règle générale, nous allons examiner hello les scénarios suivants :

#### <a name="4d175f1b-7353-4137-9d2f-817683c26e53"></a>Déplacement d’une machine virtuelle à partir de tooAzure local avec un disque non généralisé
Vous envisagez de toomove un système SAP spécifique à partir de local tooAzure. Cela peut être effectuée en téléchargeant le disque dur virtuel qui contient hello du système d’exploitation de hello, hello binaires binaires SAP et SGBD plus hello disques durs virtuels avec des données hello et fichiers journaux d’hello SGBD tooAzure. En revanche trop[scénario #2 ci-dessous][planning-guide-5.1.2], vous conservez le nom d’hôte hello, SID SAP et comptes d’utilisateur SAP dans hello Azure VM qu’ils ont été configurés dans l’environnement local de hello. Par conséquent, il n’est pas nécessaire de généraliser l’image de hello. Consultez les chapitres [pour préparer le déplacement d’une machine virtuelle à partir de tooAzure local avec un disque non généralisé] [ planning-guide-5.2.1] de ce document pour les étapes de préparation locale et de télécharger des disques durs virtuels non généralisé de machines virtuelles tooAzure. Consultez le chapitre [scénario 3 : déplacer un ordinateur virtuel à l’aide d’un disque dur virtuel Azure non généralisé avec SAP en local] [ deployment-guide-3.4] Bonjour [Guide de déploiement] [ deployment-guide]pour savoir comment déployer une image dans Azure.

#### <a name="e18f7839-c0e2-4385-b1e6-4538453a285c"></a>Déploiement d’une machine virtuelle avec une image spécifique du client
En raison des exigences spécifiques toospecific de votre version du système d’exploitation ou SGBD, les images hello fourni Bonjour Azure Marketplace ne répondent pas à vos besoins. Par conséquent, vous devrez peut-être toocreate une machine virtuelle à l’aide de votre propre image de machine virtuelle du système d’exploitation/SGBD 'private', qui peut être déployé plusieurs fois par la suite. tooprepare cette image « privée » pour la duplication, hello éléments suivants ont toobe pris en compte :


[comment]: <> (MSSedusch &gt; See more details here :)
[comment]: <> (MShermannd TODO first link is about classic model. Didn’t find an Azure docu article)
[comment]: <> (MSSedusch &gt; &lt;https://azure.microsoft.com/documentation/articles/virtual-machines-create-upload-vhd-windows-server/&gt;)
[comment]: <> (MSSedusch &gt; &lt;http://blogs.technet.com/b/blainbar/archive/2014/09/12/modernizing-your-infrastructure-with-hybrid-cloud-using-custom-vm-images-and-resource-groups-in-microsoft-azure-part-21-blain-barton.aspx&gt;)
- - -
> ![Windows][Logo_Windows] Windows
>
> Hello Windows Paramètres (tels que les SID Windows et le nom d’hôte) doivent être abstraits/généralisés sur hello local machine virtuelle via la commande sysprep de hello.
>
>
> ![Linux][Logo_Linux] Linux
>
> Suivez les étapes de hello décrits dans les articles suivants pour [SUSE] [ virtual-machines-linux-create-upload-vhd-suse] ou [Red Hat] [ virtual-machines-linux-redhat-create-upload-vhd] tooprepare un toobe de disque dur virtuel téléchargé tooAzure.
>
>

- - -
Si vous avez déjà installé le contenu SAP dans votre machine locale virtuelle (en particulier pour les systèmes de niveau 2), vous pouvez adapter les paramètres du système SAP hello après déploiement hello Hello machine virtuelle Azure via une instance de hello renommer procédure pris en charge par hello approvisionnement en logiciels SAP Manager (Note SAP [1619720]). Reportez-vous aux chapitres [préparation du déploiement d’une machine virtuelle avec une image propre au client pour SAP] [ planning-guide-5.2.2] et [télécharger un disque dur virtuel à partir de local tooAzure] [ planning-guide-5.3.2]de ce document pour les étapes de préparation locale et téléchargement d’un tooAzure de machine virtuelle généralisée. Consultez le chapitre [scénario 2 : déploiement d’une machine virtuelle avec une image personnalisée pour SAP] [ deployment-guide-3.3] Bonjour [Guide de déploiement] [ deployment-guide] pour les étapes détaillées de déploiement d’une image dans Azure.

#### <a name="deploying-a-vm-out-of-hello-azure-marketplace"></a>Déploiement d’une machine virtuelle hors hello Azure Marketplace
Vous aimeriez toouse Microsoft ou tiers 3e fournie image de machine virtuelle à partir de hello Azure Marketplace toodeploy votre machine virtuelle. Une fois que vous avez déployé votre machine virtuelle dans Azure, vous suivez hello mêmes directives et outils tooinstall hello logiciels SAP et/ou le SGBD dans votre machine virtuelle comme vous le feriez dans un environnement sur site. Pour plus de description du déploiement, consultez le chapitre [scénario 1 : déploiement d’une machine virtuelle hors hello Azure Marketplace pour SAP] [ deployment-guide-3.2] Bonjour [Guide de déploiement] [ deployment-guide].

### <a name="6ffb9f41-a292-40bf-9e70-8204448559e7"></a>Préparation de machines virtuelles avec SAP pour Azure
Avant de télécharger des machines virtuelles dans Azure, vous devez toomake que les machines virtuelles de hello et disques durs virtuels répondre à certaines exigences. Il existe de petites différences selon la méthode de déploiement hello qui est utilisé.

#### <a name="1b287330-944b-495d-9ea7-94b83aff73ef"></a>Préparation du déplacement d’une machine virtuelle à partir de tooAzure local avec un disque non généralisé
Une méthode courante de déploiement est toomove un ordinateur virtuel existant qui exécute un système SAP à partir de local tooAzure. Que machine virtuelle et hello système SAP dans la machine virtuelle doit exécuter uniquement dans Azure à l’aide de hello hello du même nom d’hôte et très probablement hello même SID SAP. Dans ce cas hello du système d’exploitation d’ordinateur virtuel invité ne doit pas être généralisée pour plusieurs déploiements. Si le réseau local de hello est étendu à Azure (consultez le chapitre [intersite - déploiement d’une ou plusieurs machines virtuelles SAP dans Azure avec spécification hello intégration complète dans le réseau local de hello] [ planning-guide-2.2] dans ce document), puis même hello même comptes de domaine peuvent être utilisés au sein de hello VM que ceux utilisés localement avant de.

Les exigences à respecter pour la préparation de votre propre disque de machine virtuelle Azure sont les suivantes :

* À l’origine, système d’exploitation hello contenant hello disque dur virtuel peut avoir uniquement une taille maximale de 127 Go. Cette limitation a été éliminée à fin hello de mars 2015. Maintenant hello disque dur virtuel contenant le système d’exploitation de hello possible too1TB taille comme tout autre stockage de Azure hébergé le disque dur virtuel également.

[comment]: <> (MShermannd TODO ont toocheck si CLI convertit également toostatic)
* Il doit toobe Bonjour format de disque dur virtuel fixe. Les disques durs virtuels ou les disques durs virtuels au format VHDx ne sont pas encore pris en charge sur Azure. Les disques durs virtuels dynamiques sera converti toostatic VHD lorsque vous téléchargez hello VHD avec les applets de commande PowerShell ou CLI
* Disques durs virtuels qui sont monté toohello VM et doivent être de nouveau montés dans toohello Azure VM besoin toobe dans un format de disque dur virtuel fixe. Hello même limite de taille de disque de système d’exploitation hello s’applique aussi bien les disques toodata. Les disques durs virtuels peuvent avoir une taille maximale de 1 To. Les disques durs virtuels dynamiques sera converti toostatic VHD lorsque vous téléchargez hello VHD avec les applets de commande PowerShell ou CLI
* Ajoutez un autre compte local doté de privilèges d’administrateur qui peut être utilisé par le support technique de Microsoft ou qui peut être affecté en tant que contexte pour les services et applications toorun dans jusqu'à hello que machine virtuelle est déployée et les utilisateurs plus appropriés peut être utilisé.
* Pour les cas de hello d’à l’aide d’un scénario de déploiement de Cloud uniquement (consultez le chapitre [uniquement dans le Cloud - déploiements d’ordinateurs virtuels dans Azure sans dépendances sur hello local réseau client] [ planning-guide-2.1] de ce document) en association avec cette méthode de déploiement, le domaine de comptes peuvent ne pas fonctionnent une fois hello disque Azure déployé dans Azure. Cela est particulièrement vrai pour les comptes qui sont des services de toorun utilisés comme des applications SGBD ou SAP hello. Par conséquent, vous devez tooreplace ces comptes de domaine avec des comptes locaux de machine virtuelle et supprimez des comptes de domaine local hello Bonjour machine virtuelle. Conservation des utilisateurs du domaine local dans l’image de machine virtuelle hello n’est pas un problème lorsque hello machine virtuelle est déployé dans un scénario de hello entre différents locaux, comme décrit dans le chapitre [intersite - déploiement d’une ou plusieurs machines virtuelles SAP dans Azure avec spécification hello en cours entièrement intégré à un réseau local de hello] [ planning-guide-2.2] dans ce document.
* Si les comptes de domaine ont été utilisés en tant que comptes de connexion SGBD ou les utilisateurs lors de l’exécution hello système locaux et les machines virtuelles sont censés toobe déployée dans des scénarios de Cloud uniquement, les utilisateurs de domaine de hello doivent toobe supprimé. Vous devez toomake sûr qu’administrateur local de hello et un autre utilisateur local d’ordinateur virtuel est ajouté en tant qu’un utilisateur dans hello SGBD en tant qu’administrateurs.
* Ajoutez des comptes locaux, comme ceux peuvent être nécessaire pour le scénario de déploiement spécifique hello.

- - -
> ![Windows][Logo_Windows] Windows
>
> Dans ce scénario, aucune généralisation (sysprep) de hello machine virtuelle est tooupload requis et déployer hello sur Azure.
> Assurez-vous que le lecteur D:\ n’est pas un montage automatique de disque défini pour les disques attachés, comme décrit dans le chapitre [Paramétrage du montage automatique pour les disques attachés][planning-guide-5.5.3] dans ce document.
>
> ![Linux][Logo_Linux] Linux
>
> Dans ce scénario aucune généralisation (waagent-deprovision) hello VM est requis tooupload et déployer hello sur Azure.
> Assurez-vous que/mnt/resource n’est pas utilisée et que TOUS les disques sont montés via uuid. Pour le disque de hello du système d’exploitation, assurez-vous qu’entrée du chargeur de démarrage hello reflète également montage basée sur l’uuid de hello.
>
>

- - -
#### <a name="57f32b1c-0cba-4e57-ab6e-c39fe22b6ec3"></a>Préparation du déploiement d’une machine virtuelle avec une image spécifique du client pour SAP
Les fichiers VHD contenant un système d’exploitation généralisé sont également stockés dans des conteneurs dans les comptes Azure Storage. Vous pouvez déployer une nouvelle machine virtuelle à partir d’une image du disque dur virtuel en référençant hello disque dur virtuel comme source de disque dur virtuel dans vos fichiers de modèle de déploiement comme décrit dans le chapitre [scénario 2 : déploiement d’une machine virtuelle avec une image personnalisée pour SAP] [ deployment-guide-3.3] de hello [Guide de déploiement][deployment-guide].

Les exigences à respecter pour la préparation de votre propre image de machine virtuelle Azure sont les suivantes :

* À l’origine, système d’exploitation hello contenant hello disque dur virtuel peut avoir uniquement une taille maximale de 127 Go. Cette limitation a été éliminée à fin hello de mars 2015. Maintenant hello disque dur virtuel contenant le système d’exploitation de hello possible too1TB taille comme tout autre stockage de Azure hébergé le disque dur virtuel également.

[comment]: <> (MShermannd TODO ont toocheck si CLI convertit également toostatic)
* Il doit toobe Bonjour format de disque dur virtuel fixe. Les disques durs virtuels ou les disques durs virtuels au format VHDx ne sont pas encore pris en charge sur Azure. Les disques durs virtuels dynamiques sera converti toostatic VHD lorsque vous téléchargez hello VHD avec les applets de commande PowerShell ou CLI
* Disques durs virtuels qui sont monté toohello VM et doivent être de nouveau montés dans toohello Azure VM besoin toobe dans un format de disque dur virtuel fixe. Hello même limite de taille de disque de système d’exploitation hello s’applique aussi bien les disques toodata. Les disques durs virtuels peuvent avoir une taille maximale de 1 To. Les disques durs virtuels dynamiques sera converti toostatic VHD lorsque vous téléchargez hello VHD avec les applets de commande PowerShell ou CLI
* Étant donné que tous les hello inscrits en tant que les utilisateurs de hello VM n’existent pas dans un scénario de Cloud uniquement les utilisateurs de domaine (consultez le chapitre [uniquement dans le Cloud - déploiements d’ordinateurs virtuels dans Azure sans dépendances sur hello local réseau client] [ planning-guide-2.1] de ce document), les services à l’aide de ce domaine de comptes peuvent ne pas fonctionnent une fois hello Image est déployée dans Azure. Cela est particulièrement vrai pour les comptes qui sont des services de toorun utilisés comme des applications SGBD ou SAP. Par conséquent, vous devez tooreplace ces comptes de domaine avec des comptes locaux de machine virtuelle et supprimez des comptes de domaine local hello Bonjour machine virtuelle. Conservation des utilisateurs du domaine local dans l’image de machine virtuelle hello peut ne pas être un problème lorsque hello machine virtuelle est déployée dans hello scénario intersite comme décrit dans le chapitre [intersite - déploiement d’une ou plusieurs machines virtuelles SAP dans Azure avec spécification hello intégration complète dans le réseau local de hello] [ planning-guide-2.2] dans ce document.
* Ajoutez un autre compte local doté de privilèges d’administrateur qui peut être utilisé par le support technique de Microsoft dans les enquêtes de problème ou qui peut être affecté en tant que contexte pour les services et applications toorun dans jusqu'à hello que machine virtuelle est déployée et les utilisateurs plus appropriés peut être utilisé.
* Dans les déploiements de Cloud uniquement et où les comptes de domaine ont été utilisés en tant que comptes de connexion SGBD ou les utilisateurs lors de l’exécution hello système local, les utilisateurs du domaine hello doivent être supprimés. Vous devez toomake assurer que l’administrateur local de hello et un autre utilisateur local d’ordinateur virtuel est ajouté en tant qu’un utilisateur de hello SGBD en tant qu’administrateurs.
* Ajoutez des comptes locaux, comme ceux peuvent être nécessaire pour le scénario de déploiement spécifique hello.
* Si l’image de hello contient une installation de SAP NetWeaver et est susceptible de changement de nom d’un nom d’hôte hello le nom d’origine hello hello au moment même de hello déploiement d’Azure, il est recommandé toocopy hello dernières versions hello SAP Software Provisioning Manager DVD dans modèle de Hello. Cela vous permettra tooeasily utilisation hello SAP fournie renommer fonctionnalité tooadapt hello modifié nom d’hôte et/ou modification hello SID de hello système SAP dans hello déployé l’image de machine virtuelle dès qu’une nouvelle copie est démarrée.

- - -
> ![Windows][Logo_Windows] Windows
>
> Assurez-vous que le lecteur D:\ n’est pas un montage automatique de disque défini pour les disques attachés, comme décrit dans le chapitre [Paramétrage du montage automatique pour les disques attachés][planning-guide-5.5.3] dans ce document.
>
> ![Linux][Logo_Linux] Linux
>
> Assurez-vous que/mnt/resource n’est pas utilisée et que TOUS les disques sont montés via uuid. Pour hello du système d’exploitation disque Assurez-vous entrée du chargeur de démarrage hello reflète également le montage de hello basée sur un uuid.
>
>

- - -
* L’interface utilisateur graphique SAP peut être installée dans un tel modèle (à des fins administratives et de configuration).
* Autres logiciels nécessaires toorun hello machines virtuelles avec succès dans les scénarios de coexistence peut être installé tant que ce logiciel peut fonctionner avec hello renommer Hello machine virtuelle.

Si hello machine virtuelle est préparée suffisamment toobe générique et de comptes/utilisateurs non disponibles dans hello ciblé scénario de déploiement Azure, hello dernière étape de préparation généraliser une image de ce type est effectuée.

##### <a name="generalizing-a-vm"></a>Généralisation d’une machine virtuelle
- - -
[comment]: <> (MShermannd TODO a des articles d’une meilleure toofind / docu sur la généralisation hello des machines virtuelles pour ARM)
> ![Windows][Logo_Windows] Windows
>
> dernière étape de Hello est toolog dans tooa machine virtuelle avec un compte d’administrateur. Ouvrez une fenêtre de commande Windows en tant qu’« administrateur ». Too...\windows\system32\sysprep et exécutez sysprep.exe.
> Une petite fenêtre s’affiche. C’est important toocheck hello 'Generalize' option (valeur par défaut hello n’est pas cochée) et modifiez sa valeur par défaut « Redémarrer » de too'Shutdown hello l’Option d’arrêt ». Cette procédure suppose que le processus de sysprep hello est exécutée localement dans le système d’exploitation invité d’une machine virtuelle de hello.
> Si vous souhaitez la procédure de hello tooperform avec une machine virtuelle en cours d’exécution dans Azure, suivez les étapes de hello décrites dans [cet article][virtual-machines-windows-capture-image].
>
> ![Linux][Logo_Linux] Linux
>
> [Comment toocapture un toouse de la machine virtuelle Linux en tant que gestionnaire de ressources du modèle][virtual-machines-linux-capture-image]
>
>

- - -
### <a name="transferring-vms-and-vhds-between-on-premises-tooazure"></a>Transfert de machines virtuelles et disques durs virtuels entre local tooAzure
Étant donné que le téléchargement tooAzure images et des disques de machine virtuelle n’est pas possible via hello portail Azure, vous devez applets de commande Azure PowerShell toouse ou l’interface CLI. Une autre solution consiste à utiliser l’outil hello 'AzCopy' hello. outil de Hello peut copier des disques durs virtuels entre Azure et locaux (dans les deux directions). Il peut également copier les disques durs virtuels entre différentes régions Azure. Consultez [la documentation suivante][storage-use-azcopy] pour en savoir plus sur le téléchargement et l’utilisation d’AzCopy.

Une troisième alternative serait toouse divers outils d’interface utilisateur orientée services tiers. Toutefois, assurez-vous que ces outils prennent en charge les objets blob de pages Azure. Dans notre cas, nous devons toouse objet Blob de pages Azure stockez (hello différences sont décrites ici : <https://msdn.microsoft.com/library/windowsazure/ee691964.aspx>). Outils hello fournies par Azure sont également très efficaces pour compresser les machines virtuelles de hello et disques durs virtuels toobe téléchargé. Ceci est important, car cette efficacité dans la compression réduit le temps de téléchargement de hello (qui varie quand même selon toohello de lien de téléchargement hello internet à partir d’installation locale de hello et région de déploiement Azure hello ciblés). Il s’agit juste de croire que le téléchargement d’une machine virtuelle ou un disque dur virtuel à partir de données Azure emplacement européen toohello résidant aux États-Unis prendront plus de temps que le chargement des centres de hello mêmes centres de données Azure européens toohello machines virtuelles/disques durs virtuels.

#### <a name="a43e40e6-1acc-4633-9816-8f095d5a7b6a"></a>Téléchargement d’un disque dur virtuel à partir de local tooAzure
une machine virtuelle existante ou un disque dur virtuel à partir de hello localement cette machine virtuelle de réseau ou de disque dur virtuel a besoin d’exigences de hello toomeet comme indiqué dans le chapitre de tooupload [pour préparer le déplacement d’une machine virtuelle à partir de tooAzure local avec un disque non généralisé] [ planning-guide-5.2.1] de ce document.

Cette machine virtuelle n’a pas besoin toobe généralisé et peut être téléchargée en état de hello et forme qu’après que l’arrêt de hello local côté. Hello même a la valeur true pour les disques durs virtuels supplémentaires dépourvus de tout système d’exploitation.

##### <a name="uploading-a-vhd-and-making-it-an-azure-disk"></a>Chargement d’un disque dur virtuel en vue d’en faire un disque Azure
Dans ce cas nous souhaitez tooupload un disque dur virtuel, avec ou sans un système d’exploitation et monter tooa machine virtuelle comme disque de données ou l’utiliser comme disque de système d’exploitation. Ce processus comprend plusieurs étapes

**PowerShell**

* Abonnement de tooyour de connexion avec *AzureRmAccount de connexion*
* Définir l’abonnement hello de votre contexte avec *Set-AzureRmContext* et le paramètre SubscriptionId ou SubscriptionName - voir <https://msdn.microsoft.com/library/mt619263.aspx>
* Télécharger hello VHD avec *Add-AzureRmVhd* tooan compte de stockage Azure - consultez <https://msdn.microsoft.com/library/mt603554.aspx>
* Disque hello du système d’exploitation de jeu d’un toohello de configuration de machine virtuelle nouveau disque dur virtuel avec *Set-AzureRmVMOSDisk* -consultez <https://msdn.microsoft.com/library/mt603746.aspx>
* Créer une machine virtuelle à partir de la configuration de machine virtuelle hello avec *New-AzureRmVM* -consultez <https://msdn.microsoft.com/library/mt603754.aspx>
* Ajouter un tooa de disque de données nouvelle machine virtuelle avec *Add-AzureRmVMDataDisk* -consultez <https://msdn.microsoft.com/library/mt603673.aspx>

**Interface de ligne de commande Azure**

* Le Gestionnaire de ressources tooAzure avec le mode *arm en mode de configuration azure*
* Abonnement de tooyour de connexion avec *connexion azure*
* Sélectionnez votre abonnement en entrant *azure account set `<subscription name or id`>*
* Télécharger hello VHD avec *téléchargement d’objet blob de stockage azure* -consultez [Using hello CLI d’Azure avec le stockage Azure][storage-azure-cli]
* Créer une machine virtuelle en spécifiant hello téléchargé un disque dur virtuel en tant que disque de système d’exploitation avec *créer de machine virtuelle azure* et le paramètre -d
* Ajouter un tooa de disque de données nouvelle machine virtuelle avec *vm disque attacher-nouveau*

**Modèle**

* Télécharger hello disque dur virtuel avec Powershell ou CLI d’Azure
* Déployer hello machine virtuelle avec un modèle JSON référençant hello disque dur virtuel, comme indiqué dans [cet exemple de modèle JSON](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vm-from-specialized-vhd/azuredeploy.json).

#### <a name="deployment-of-a-vm-image"></a>Déploiement d’une image de machine virtuelle
une machine virtuelle existante ou un disque dur virtuel à partir de hello sur site de réseau dans l’ordre toouse comme une image de machine virtuelle Azure cette machine virtuelle ou disque dur virtuel nécessitent toomeet hello répertoriées dans le chapitre de tooupload [préparation du déploiement d’une machine virtuelle avec une image propre au client pour SAP] [ planning-guide-5.2.2] de ce document.

* Utilisez *sysprep* sur Windows ou *waagent-deprovision* sur Linux toogeneralize votre machine virtuelle - consultez [comment toocapture une machine virtuelle de Windows Bonjour déploiement du Gestionnaire de ressources du modèle] [ virtual-machines-windows-capture-image-prepare-the-vm-for-image-capture] ou [comment toocapture un toouse de la machine virtuelle Linux en tant que gestionnaire de ressources du modèle][virtual-machines-linux-capture-image-capture]
* Abonnement de tooyour de connexion avec *AzureRmAccount de connexion*
* Définir l’abonnement hello de votre contexte avec *Set-AzureRmContext* et le paramètre SubscriptionId ou SubscriptionName - voir <https://msdn.microsoft.com/library/mt619263.aspx>
* Télécharger hello VHD avec *Add-AzureRmVhd* tooan compte de stockage Azure - consultez <https://msdn.microsoft.com/library/mt603554.aspx>
* Disque hello du système d’exploitation de jeu d’un toohello de configuration de machine virtuelle nouveau disque dur virtuel avec *Set-AzureRmVMOSDisk - SourceImageUri - CreateOption fromImage* -consultez <https://msdn.microsoft.com/library/mt603746.aspx>
* Créer une machine virtuelle à partir de la configuration de machine virtuelle hello avec *New-AzureRmVM* -consultez <https://msdn.microsoft.com/library/mt603754.aspx>

**Interface de ligne de commande Azure**

* Utilisez *sysprep* sur Windows ou *waagent-deprovision* sur Linux toogeneralize votre machine virtuelle - consultez [comment toocapture une machine virtuelle de Windows Bonjour déploiement du Gestionnaire de ressources du modèle] [ virtual-machines-windows-capture-image-prepare-the-vm-for-image-capture] ou [comment toocapture un toouse de la machine virtuelle Linux en tant que gestionnaire de ressources du modèle] [ virtual-machines-linux-capture-image-capture] pour Linux
* Le Gestionnaire de ressources tooAzure avec le mode *arm en mode de configuration azure*
* Abonnement de tooyour de connexion avec *connexion azure*
* Sélectionnez votre abonnement en entrant *azure account set `<subscription name or id`>*
* Télécharger hello VHD avec *téléchargement d’objet blob de stockage azure* -consultez [Using hello CLI d’Azure avec le stockage Azure][storage-azure-cli]
* Créer une machine virtuelle en spécifiant hello téléchargé un disque dur virtuel en tant que disque de système d’exploitation avec *créer de machine virtuelle azure* et le paramètre -Q

**Modèle**

* Utilisez *sysprep* sur Windows ou *waagent-deprovision* sur Linux toogeneralize votre machine virtuelle - consultez [comment toocapture une machine virtuelle de Windows Bonjour déploiement du Gestionnaire de ressources du modèle] [ virtual-machines-windows-capture-image-prepare-the-vm-for-image-capture] ou [comment toocapture un toouse de la machine virtuelle Linux en tant que gestionnaire de ressources du modèle] [ virtual-machines-linux-capture-image-capture] pour Linux
* Télécharger hello disque dur virtuel avec Powershell ou CLI d’Azure
* Déployer hello machine virtuelle avec un modèle JSON faisant référence à l’image hello disque dur virtuel, comme indiqué dans [cet exemple de modèle JSON](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-from-user-image/azuredeploy.json).

#### <a name="downloading-vhds-tooon-premises"></a>Téléchargement de disques durs virtuels tooon local
L’Infrastructure Azure en tant que Service n’est pas un sens uniquement être en mesure de tooupload de disques durs virtuels et les systèmes SAP. Vous pouvez déplacer SAP Bonjour local ainsi de nouveau systèmes à partir d’Azure.

Au moment de hello du téléchargement de hello hello disques durs virtuels ne peut pas être active. Même lors du téléchargement de disques durs virtuels qui sont montés tooVMs, hello machine virtuelle doit toobe arrêt. Si vous souhaitez uniquement toodownload hello base de données de contenu qui doit ensuite être utilisé tooset d’un nouveau système local et s’il est acceptable que pendant la durée hello Hello télécharger et hello le programme d’installation du système de nouveau hello hello système dans Azure peut encore être opérationnelle , vous pouvez éviter un long temps d’arrêt en effectuant une sauvegarde de base de données compressée dans un disque dur virtuel et simplement télécharger que le disque dur virtuel au lieu de télécharger également hello machine virtuelle de base du système d’exploitation.

#### <a name="powershell"></a>PowerShell
Une fois que le système SAP de hello est arrêté et hello machine virtuelle est arrêtée, vous pouvez utiliser hello PowerShell applet de commande Save-AzureRmVhd hello local disques de disque dur virtuel cible toodownload hello sauvegarder world local de toohello. Toodo, vous avez besoin des URL de hello Hello disque dur virtuel que vous pouvez trouver dans hello 'Stockage Section' Hello le portail Azure (nécessaire toonavigate toohello compte de stockage et hello conteneur de stockage où hello disque dur virtuel a été créé) et vous devez tooknow où hello disque dur virtuel doit être copié dans.

Ensuite, vous pouvez exploiter commande hello, définissez simplement le paramètre hello SourceUri en tant qu’URL hello de toodownload de disque dur virtuel hello et hello LocalFilePath en tant qu’emplacement physique de hello Hello disque dur virtuel (y compris son nom). commande Hello pourrait ressembler à :

```powerhell
Save-AzureRmVhd -ResourceGroupName <resource group name of storage account> -SourceUri http://<storage account name>.blob.core.windows.net/<container name>/sapidedata.vhd -LocalFilePath E:\Azure_downloads\sapidesdata.vhd
```

Pour plus de détails d’applet de commande hello AzureRmVhd de sauvegarde, consultez la page <https://msdn.microsoft.com/library/mt622705.aspx>.

#### <a name="cli"></a>Interface de ligne de commande
Une fois que le système SAP de hello est arrêté et hello machine virtuelle est arrêtée, vous pouvez utiliser hello CLI d’Azure commande stockage azure blob téléchargement sur hello local disques de disque dur virtuel cible toodownload hello sauvegarder world local de toohello. Toodo, vous avez besoin nom de hello et conteneur hello Hello disque dur virtuel que vous pouvez trouver dans hello 'Stockage Section' Hello le portail Azure (nécessaire toonavigate toohello compte de stockage et hello conteneur de stockage où hello disque dur virtuel a été créé) et vous devez tooknow où Hello disque dur virtuel doit être copiée dans.

Ensuite, vous pouvez exploiter commande hello en définissant simplement des objets blob de paramètres hello et conteneur de toodownload de disque dur virtuel hello et de destination de hello comme hello physique l’emplacement cible du disque dur virtuel (y compris son nom) de hello. commande Hello pourrait ressembler à :

```
azure storage blob download --blob <name of hello VHD toodownload> --container <container of hello VHD toodownload> --account-name <storage account name of hello VHD toodownload> --account-key <storage account key> --destination <destination of hello VHD toodownload>
```

### <a name="transferring-vms-and-vhds-within-azure"></a>Transfert de machines virtuelles et de disques durs virtuels au sein d’Azure
#### <a name="copying-sap-systems-within-azure"></a>Copie des systèmes SAP au sein d’Azure
Un système SAP ou même un serveur SGBD dédié prenant en charge de la couche application SAP sera probablement sont constitués de plusieurs disques durs virtuels qui contiennent soit hello du système d’exploitation avec des fichiers binaires de hello ou hello des données et de base de données SAP hello ou les fichiers journaux. Hello fonctionnalité Azure de copie des disques durs virtuels ni hello fonctionnalité Azure d’enregistrement des disques durs virtuels toodisk a un mécanisme de synchronisation qui serait instantané plusieurs disques durs virtuels de façon synchrone. Par conséquent, état hello Hello copiés ou enregistrés disques durs virtuels, même si ces derniers sont montés sur hello même machine virtuelle est différent. Cela signifie que dans hello concrète cas d’avoir des données différentes et finirait hello différents disques durs virtuels, hello de base de données en fin de hello serait incohérent.

**Conclusion : Dans l’ordre toocopy ou enregistrer les disques durs virtuels qui font partie de la configuration d’un système SAP vous besoin toostop hello SAP système et que vous devez également tooshut vers le bas hello déployé machine virtuelle. Seulement peut copier ou ensemble de hello de téléchargement de disques durs virtuels tooeither créer une copie de hello système SAP dans Azure ou localement.**

Disques de données sont stockés en tant que fichiers de disque dur virtuel dans un compte de stockage Azure et peuvent être directement joindre l’ordinateur virtuel de tooa ou être utilisé en tant qu’image. Dans ce cas, hello disque dur virtuel est copié tooanother emplacement avant beeing jointe toohello virtual machine. nom complet de Hello du fichier de disque dur virtuel hello dans Azure doit être unique dans Azure. Comme mentionné précédemment déjà, nom de hello est un type de nom en trois parties qui ressemble à :

    http(s)://<storage account name>.blob.core.windows.net/<container name>/<vhd name>

##### <a name="powershell"></a>PowerShell
Vous pouvez utiliser les applets de commande de Azure PowerShell toocopy un disque dur virtuel comme indiqué dans [cet article][storage-powershell-guide-full-copy-vhd].

##### <a name="cli"></a>Interface de ligne de commande
Vous pouvez utiliser Azure CLI toocopy un disque dur virtuel comme indiqué dans [cet article][storage-azure-cli-copy-blobs]

##### <a name="azure-storage-tools"></a>Outils Azure Storage
* <http://azurestorageexplorer.codeplex.com/releases/view/125870>

Des éditions professionnelles d’Azure Storage Explorer se trouvent également ici :

* <http://www.cerebrata.com/>
* <http://clumsyleaf.com/products/cloudxplorer>

copie de Hello d’un disque dur virtuel proprement dit au sein d’un compte de stockage est un processus qui ne prend que quelques secondes (tooSAN un matériel similaire création d’instantanés avec copie différée et copie sur écriture). Une fois que vous avez une copie du fichier de disque dur virtuel hello attachez-le tooa virtual machine ou l’utilisation en tant qu’une image tooattach copie des ordinateurs de toovirtual de disque dur virtuel hello.

##### <a name="powershell"></a>PowerShell
```powershell
# attach a vhd tooa vm
$vm = Get-AzureRmVM -ResourceGroupName <resource group name> -Name <vm name>
$vm = Add-AzureRmVMDataDisk -VM $vm -Name newdatadisk -VhdUri <path toovhd> -Caching <caching option> -DiskSizeInGB $null -Lun <lun e.g. 0> -CreateOption attach
$vm | Update-AzureRmVM

# attach a copy of hello vhd tooa vm
$vm = Get-AzureRmVM -ResourceGroupName <resource group name> -Name <vm name>
$vm = Add-AzureRmVMDataDisk -VM $vm -Name newdatadisk -VhdUri <new path of vhd> -SourceImageUri <path tooimage vhd> -Caching <caching option> -DiskSizeInGB $null -Lun <lun e.g. 0> -CreateOption fromImage
$vm | Update-AzureRmVM
```
##### <a name="cli"></a>Interface de ligne de commande
```
azure config mode arm

# attach a vhd tooa vm
azure vm disk attach <resource group name> <vm name> <path toovhd>

# attach a copy of hello vhd tooa vm
# this scenario is currently not possible with Azure CLI. A workaround is toomanually copy hello vhd toohello destination.
```

#### <a name="9789b076-2011-4afa-b2fe-b07a8aba58a1"></a>Copie de disques entre comptes Azure Storage
Cette tâche ne peut pas être effectuée sur hello portail Azure. Vous pouvez utiliser les applets de commande Azure PowerShell, l’interface de ligne de commande Azure ou un navigateur de stockage tiers. Hello applets de commande PowerShell ou des commandes CLI peuvent créer et gérer des objets BLOB, qui incluent des objets BLOB de hello capacité tooasynchronously copie entre les comptes de stockage et entre des régions dans hello abonnement Azure.

##### <a name="powershell"></a>PowerShell
La copie de disques durs virtuels entre abonnements est également possible. Pour plus d’informations, consultez [cet article][storage-powershell-guide-full-copy-vhd].

flux de base Hello Hello logique d’applet de commande PS ressemble à ceci :

* Créer un contexte de compte de stockage pour le compte de stockage source hello avec *New-AzureStorageContext* -consultez <https://msdn.microsoft.com/library/dn806380.aspx>
* Créer un contexte de compte de stockage pour le compte de stockage cible hello avec *New-AzureStorageContext* -consultez <https://msdn.microsoft.com/library/dn806380.aspx>
* Démarrer la copie hello avec

```powershell
Start-AzureStorageBlobCopy -SrcBlob <source blob name> -SrcContainer <source container name> -SrcContext <variable containing context of source storage account> -DestBlob <target blob name> -DestContainer <target container name> -DestContext <variable containing context of target storage account>
```

* Vérifier l’état de hello de copie hello dans une boucle avec

```powershell
Get-AzureStorageBlobCopyState -Blob <target blob name> -Container <target container name> -Context <variable containing context of target storage account>
```

* Attachez hello VHD tooa machine virtuelle comme décrit ci-dessus.

Pour découvrir des exemples, consultez [cet article][storage-powershell-guide-full-copy-vhd]

##### <a name="cli"></a>Interface de ligne de commande
* Démarrer la copie hello avec

```
  azure storage blob copy start --source-blob <source blob name> --source-container <source container name> --account-name <source storage account name> --account-key <source storage account key> --dest-container <target container name> --dest-blob <target blob name> --dest-account-name <target storage account name> --dest-account-key <target storage account name>
```

* Vérifier l’état de hello si hello copie dans une boucle avec

```
azure storage blob copy show --blob <target blob name> --container <target container name> --account-name <target storage account name> --account-key <target storage account name>
```

* Attachez hello VHD tooa machine virtuelle comme décrit ci-dessus.

Pour découvrir des exemples, consultez [cet article][storage-azure-cli-copy-blobs]

### <a name="disk-handling"></a>Gestion de disque
#### <a name="4efec401-91e0-40c0-8e64-f2dceadff646"></a>Structure de machine virtuelle/disque dur virtuel pour les déploiements SAP
Dans l’idéal, hello gestion de structure hello d’une machine virtuelle et disques durs virtuels hello associé doivent être très simples. Dans les installations locales, les clients ont développé de nombreuses méthodes pour structurer une installation du serveur.

* Un fichier VHD de base qui contient hello du système d’exploitation et tous les fichiers binaires de hello de hello SGBD ou SAP. Depuis mars 2015, ce disque dur virtuel peut être des too1TB taille au lieu de restrictions antérieures dont il limitée too127GB.
* Un ou plusieurs disques durs virtuels qui contient le fichier de journal SGBD hello de base de données SAP hello et hello journal Hello zone de stockage temporaire SGBD (en cas de hello SGBD prend en charge). Si les exigences d’e/s de journal de base de données hello sont élevées, vous devez toostripe plusieurs disques durs virtuels dans le volume d’IOPS ordre tooreach hello requis.
* Nombre de disques durs virtuels contenant un ou deux fichiers de base de données de base de données SAP hello et les fichiers de données temporaires SGBD hello ainsi (si hello SGBD prend en charge).

![Configuration de référence de la machine virtuelle IaaS Azure pour SAP][planning-guide-figure-1300]

[comment]: <> (MShermannd  TODO describe Linux structure  )

- - -
> ![Windows][Logo_Windows] Windows
>
> Avec de nombreux clients, nous avons vu configurations où, par exemple, les binaires SAP et SGBD n’étaient pas installés sur le lecteur c:\ de hello où hello système d’exploitation a été installé. Différentes raisons pour cela, mais lorsque nous avons précédent toohello racine, il était généralement que hello lecteurs étaient petits et mises à niveau du système d’exploitation nécessaires espace supplémentaire de 10 à 15 ans. Ces deux conditions s’appliquent bien moins souvent de nos jours. Aujourd'hui, lecteur c:\ de hello peut être mappée sur des machines virtuelles ou des disques des volumes de grande taille. Dans les déploiements de tookeep de commande simples dans leur structure, il est recommandé de toofollow le modèle de déploiement suivantes pour les systèmes SAP NetWeaver dans Azure
>
> fichier d’échange de système d’exploitation de Windows Hello doit se trouver sur hello D: (disque non persistant)
>
> ![Linux][Logo_Linux] Linux
>
> Placez le fichier d’échange hello Linux sous/mnt/mnt/resource sur Linux comme décrit dans [cet article][virtual-machines-linux-agent-user-guide]. fichier d’échange Hello peut être configuré dans le fichier de configuration hello Hello /etc/waagent.conf de le Linux Agent. Ajoutez ou modifiez hello suivant les paramètres :
>
>

```
ResourceDisk.EnableSwap=y
ResourceDisk.SwapSizeMB=30720
```

modifications de hello tooactivate, vous devez toorestart hello Linux Agent avec

```
sudo service waagent restart
```

Veuillez lire la Note SAP [1597355] pour plus d’informations sur hello recommandé de taille du fichier d’échange

- - -
nombre de Hello de disques durs virtuels utilisés pour les fichiers de données du SGBD hello et de type hello de ces disques durs virtuels sont hébergés sur le stockage Azure doit être déterminé en matière d’IOPS hello et latence hello requise. Les quotas exacts sont décrits dans [cet article][virtual-machines-sizes]

Expérience des déploiements SAP sur hello 2 dernières années nous appris certaines leçons qui peuvent se résumer ainsi :

* Fichiers de données d’e/s du trafic toodifferent n’est pas toujours hello identiques étant donné que les systèmes clients existants peuvent avoir différemment des données de taille des fichiers représentant leurs bases de données SAP. Par conséquent, il s’est avéré toobe mieux à l’aide d’une configuration RAID sur plusieurs disques durs virtuels tooplace hello des fichiers de données que numéros d’unités logiques diviser en dehors de celles. A été le cas, en particulier avec le stockage Azure Standard dans laquelle un taux d’IOPS atteint le quota hello d’un VHD sur le journal des transactions SGBD hello. Dans une telle utilisation hello de scénarios de stockage Premium est recommandé ou également agréger plusieurs vhd de stockage Standard avec un logiciel RAID.

- - -
> ![Windows][Logo_Windows] Windows
>
> * [Meilleures pratiques relatives aux performances de SQL Server dans les machines virtuelles Azure][virtual-machines-sql-server-performance-best-practices]
>
> ![Linux][Logo_Linux] Linux
>
> * [Configuration d’un RAID logiciel sur Linux][virtual-machines-linux-configure-raid]
> * [Configurer LVM sur une machine virtuelle Linux dans Azure][virtual-machines-linux-configure-lvm]
> * [Secrets d’Azure Storage et optimisations d’E/S dans Linux](http://blogs.msdn.com/b/igorpag/archive/2014/10/23/azure-storage-secrets-and-linux-i-o-optimizations.aspx)
>
>

- - -
* Premium Storage affiche des performances en hausse, en particulier pour les écritures du journal des transactions critiques. Pour les scénarios SAP qui sont les performances en production toodeliver attendu, il est vivement recommandé de toouse série de machines virtuelles qui peut tirer parti de stockage Azure Premium.

N’oubliez pas que hello du disque dur virtuel qui contient hello du système d’exploitation, et que nous vous recommandons, hello binaires de base de données SAP et hello (machine virtuelle de base), n’est plus limitée too127GB. Il peut désormais avoir au plus too1TB taille. Cela doit être suffisamment tookeep espace tous hello fichier nécessaire, y compris les journaux de travaux par lots SAP, par exemple.

Pour obtenir des suggestions et plus de détails, en particulier pour les machines virtuelles SGBD, consultez hello [Guide de déploiement de système SGBD][dbms-guide]

#### <a name="disk-handling"></a>Gestion de disque
Dans la plupart des scénarios, vous devez toocreate des disques supplémentaires dans la base de données SAP ordre toodeploy hello en hello machine virtuelle. Nous avons abordé les considérations hello sur le nombre de disques durs virtuels dans le chapitre [structure VM/VHD pour les déploiements SAP] [ planning-guide-5.5.1] de ce document. Hello portail Azure permet de tooattach et détachement des disques une fois qu’une machine virtuelle de base est déployée. les disques Hello peuvent être Attacher/Détacher lorsque hello machine virtuelle est activé et en cours d’exécution ainsi que quand il est arrêté. Lors de l’attachement d’un disque, hello portail Azure offre tooattach un disque vide ou un disque existant à ce stade n’est pas attaché tooanother machine virtuelle.

**Remarque**: disques durs virtuels ne peuvent être attaché tooone machine virtuelle à un moment donné.

![Attacher/Détacher des disques avec le stockage Azure standard][planning-guide-figure-1400]

Vous devez toodecide si vous souhaitez toocreate un nouveau disque dur virtuel vide (qui serait créé dans hello en que même compte de stockage hello machine virtuelle de base est) ou si vous souhaitez tooselect un disque dur virtuel existant qui a été téléchargé précédemment et qui doit être attaché toohello VM maintenant.

**IMPORTANT**: vous **ne sont pas** souhaitez toouse mise en cache de l’hôte avec le stockage Azure Standard. Vous conservez les préférences de Cache de l’hôte de hello hello comme valeur par défaut NONE. Avec le stockage Azure Premium vous devez activer la mise en cache de lecture si caractéristique d’e/s de hello est en lecture principalement comme classique de trafic d’e/s sur les fichiers de données de base de données. En présence d’un fichier journal des transactions de base de données, la mise en cache n’est pas recommandée.

- - -
> ![Windows][Logo_Windows] Windows
>
> [Disque tooattach données Bonjour portail Azure][virtual-machines-windows-attach-disk-portal]
>
> Si les disques sont attachés, vous devez toolog dans hello tooopen de machine virtuelle hello Gestionnaire de disque Windows. Si le montage automatique n’est pas activé comme indiqué dans le chapitre [activation du montage automatique pour les disques attachés][planning-guide-5.5.3], hello volume nouvellement attaché doit toobe effectuée en ligne et initialisé.
>
> ![Linux][Logo_Linux] Linux
>
> Si les disques sont attachés, vous devez toolog dans hello machine virtuelle et que vous initialiser des disques de hello comme décrit dans [cet article][virtual-machines-linux-how-to-attach-disk-how-to-initialize-a-new-data-disk-in-linux]
>
>

- - -
Si le nouveau disque de hello est un disque vide, vous devez tooformat hello disquette. Pour mettre en forme, en particulier pour les SGBD, données et fichiers journaux hello mêmes recommandations que pour les déploiements complets de hello que SGBD s’appliquent.

Comme indiqué précédemment dans le chapitre [hello le Concept de Machine virtuelle Microsoft Azure][planning-guide-3.2], un compte de stockage Azure ne fournit pas une infinité de ressources en termes de volume d’e/s, e/s et les données du volume. Généralement, les machines virtuelles SGBD en sont les plus affectées. Il peut être un compte de stockage distinct pour chaque ordinateur virtuel de toouse meilleures si vous avez peu élevé toodeploy de machines virtuelles de volume d’e/s dans toostay ordre limite hello Hello volume de compte de stockage Azure. Sinon, vous devez toosee comment vous pouvez équilibrer ces machines virtuelles entre les différents comptes de stockage sans atteindre la limite de hello de chaque compte de stockage. Plus de détails sont présentés dans hello [Guide de déploiement de système SGBD][dbms-guide]. Vous devez également garder ces limitations à l’esprit pour les machines virtuelles de serveur d’application SAP pures ou d’autres machines virtuelles pouvant potentiellement nécessiter des disques durs virtuels supplémentaires.

Un autre aspect pertinent pour les comptes de stockage est si hello disques durs virtuels dans un compte de stockage sont géo-répliqués. Géo-réplication est activée ou désactivée sur hello au niveau du compte de stockage et non sur hello au niveau de la machine virtuelle. Si la géo-réplication est activée, les disques durs virtuels hello dans hello dans que compte de stockage sont répliqué dans un autre centre de données Azure hello même région. Avant de décider cela, vous devez penser hello suivant restriction :

Géo-réplication Azure fonctionne localement sur chaque disque dur virtuel sur un ordinateur virtuel et ne réplique pas IOs hello dans l’ordre chronologique sur plusieurs disques durs virtuels dans une machine virtuelle. Par conséquent, hello VHD que représente hello machine virtuelle de base, ainsi que n’importe quel toohello de disques durs virtuels attachés supplémentaire machine virtuelle sont répliquées indépendante des autres. Ainsi, qu'il n’existe aucune synchronisation entre les changements de hello dans hello différents disques durs virtuels. Hello fait que hello IOs répliquées indépendamment de commande hello dans lequel elles sont écrites signifiant que la géo-réplication n’est pas de valeur pour les serveurs de base de données qui ont leurs bases de données distribuées sur plusieurs disques durs virtuels. En outre toohello SGBD, il également peut-être d’autres applications où les processus écrivent ou manipulent des données dans différents disques durs virtuels et son ordre de hello tookeep important de modifications. Si ce dernier est important, la géo-réplication dans Azure ne doit pas être activée. Si vous souhaitez ou avez besoin de la géo-réplication pour un ensemble de machines virtuelles, mais pas pour un autre ensemble, vous pouvez déjà catégoriser les machines virtuelles et leurs disques durs virtuels correspondants dans différents comptes de stockage dont la géo-réplication est activée ou désactivée.

#### <a name="17e0d543-7e8c-4160-a7da-dd7117a1ad9d"></a>Paramétrage du montage automatique pour les disques attachés
- - -
> ![Windows][Logo_Windows] Windows
>
> Pour les ordinateurs virtuels qui sont créés à partir des Images ou des disques propres, il est nécessaire toocheck et définissez éventuellement de paramètre de montage hello. Ce paramètre autorise hello machine virtuelle après qu’un redémarrage ou un redéploiement dans Azure toomount hello attachés/montés lecteurs à nouveau automatiquement.
> paramètre Hello est définie pour les images hello fournis par Microsoft Bonjour Azure Marketplace.
>
> Dans l’ordre tooset hello automount, veuillez consultez la documentation de hello de hello ligne de commande diskpart.exe exécutable ici :
>
> * [Options de ligne de commande DiskPart](https://technet.microsoft.com/library/cc766465.aspx)
> * [Montage automatique](http://technet.microsoft.com/library/cc753703.aspx)
>
> en tant qu’administrateur, vous devez ouvrir la fenêtre de ligne de commande de Windows Hello.
>
> Si les disques sont attachés, vous devez toolog dans hello tooopen de machine virtuelle hello Gestionnaire de disque Windows. Si le montage automatique n’est pas activé comme indiqué dans le chapitre [activation du montage automatique pour les disques attachés][planning-guide-5.5.3], hello nouvellement attachés volume > doit toobe effectuée en ligne et initialisé.
>
> ![Linux][Logo_Linux] Linux
>
> Vous devez tooinitialize un disque vide qui vient d’être attaché, comme décrit dans [cet article][virtual-machines-linux-how-to-attach-disk-how-to-initialize-a-new-data-disk-in-linux].
> Vous devez également/etc/fstab tooadd nouveaux disques toohello.
>
>

- - -
### <a name="final-deployment"></a>Déploiement final
Pour hello déploiement final et les étapes exactes, surtout avec ce qui concerne les déploiement de toohello de surveillance étendue SAP, consultez toohello [Guide de déploiement][deployment-guide].

## <a name="accessing-sap-systems-running-within-azure-vms"></a>Accès aux systèmes SAP s’exécutant dans des machines virtuelles Azure
Pour les scénarios de Cloud uniquement, vous pouvez baliser des systèmes SAP tooconnect toothose parmi hello internet public à l’aide d’interface utilisateur graphique SAP. Dans ce cas, hello suivant les procédures doivent toobe appliqué.

Plus loin dans le document hello que nous aborderons hello autre scénario principales, des systèmes de tooSAP connexion dans les déploiements entre différents locaux qui ont une connexion de site à site (tunnel VPN) ou de connexion Azure ExpressRoute entre les systèmes sur site de hello et Azure.

### <a name="remote-access-toosap-systems"></a>Systèmes tooSAP d’accès à distance
Avec Azure Resource Manager modèle comporte des aucune valeur par défaut les points de terminaison plus hello ancien classique. Tous les ports d’une machine virtuelle ARM Azure sont ouverts tant que :

1. Aucun groupe de sécurité réseau n’est défini pour le sous-réseau de hello ou l’interface de réseau hello. TooAzure du trafic réseau machines virtuelles peut être sécurisé via dite « groupes de sécurité réseau ». Pour plus d’informations, consultez [Présentation du groupe de sécurité réseau][virtual-networks-nsg]
2. Aucun équilibrage de charge Azure n’est défini pour l’interface de réseau hello   

Consultez hello architecture différence classique et ARM, comme décrit dans [cet article][virtual-machines-azure-resource-manager-architecture].

#### <a name="configuration-of-hello-sap-system-and-sap-gui-connectivity-for-cloud-only-scenario"></a>Configuration de hello connectivité système SAP et l’interface utilisateur graphique SAP pour le scénario de Cloud uniquement
Consultez cet article décrit la rubrique de toothis détails : <http://blogs.msdn.com/b/saponsqlserver/archive/2014/06/24/sap-gui-connection-closed-when-connecting-to-sap-system-in-azure.aspx>

#### <a name="changing-firewall-settings-within-vm"></a>Modification des paramètres de pare-feu au sein de la machine virtuelle
Il est possible de pare-feu de hello tooconfigure nécessaires sur vos ordinateurs virtuels de tooallow trafic tooyour SAP système en entrée.

- - -
> ![Windows][Logo_Windows] Windows
>
> Par défaut, hello au sein d’une machine virtuelle déployée Azure le pare-feu Windows est activé. Vous devez maintenant tooallow hello SAP Port toobe est ouvert, hello interface GUI SAP ne sera plus en mesure de tooconnect.
> toodo cela :
>
> * Ouvrez le panneau de configuration\système et sécurité\Pare-feu too'Advanced paramètres.
> * Cliquez avec le bouton droit sur Règles de trafic entrant, puis cliquez sur Nouvelle règle.
> * Bonjour Assistant suivant choisi toocreate une nouvelle règle « Port ».
> * Dans l’étape suivante de hello d’Assistant de hello, laissez paramètre hello TCP et tapez dans le numéro de port hello tooopen. Étant donné que notre ID d’instance SAP est 00, nous avons choisi 3200. Si votre instance possède un numéro différent, le port de hello vous avez défini précédemment en fonction du nombre d’instances hello doit être ouvert.
> * Dans la partie suivante de hello d’Assistant de hello, vous avez besoin d’un élément de hello tooleave « Autoriser la connexion ».
> * Dans l’étape suivante de hello d’Assistant de hello, vous devez toodefine si la règle de hello s’applique pour le réseau de domaine, privés et publics. Ajustez ces paramètres si nécessaire tooyour a besoin. Toutefois, avec interface GUI SAP, reliant hello à l’extérieur via un réseau public hello, vous devez toohave hello règle appliquée toohello réseau public.
> * Hello dernière étape de l’Assistant de hello, vous devez toogive hello un nom de règle, puis enregistrez la règle de hello en appuyant sur « Terminer »
>
> règle de Hello immédiatement en vigueur.
>
> ![Définition des règles de port][planning-guide-figure-1600]
>
> ![Linux][Logo_Linux] Linux
>
> images de Linux Hello Bonjour Azure Marketplace n’activent pas le pare-feu hello iptables par défaut et le système SAP de hello connexion tooyour doit fonctionner. Si vous avez activé iptables ou un autre pare-feu, veuillez consultez la documentation du toohello d’iptables ou hello utilisé pare-feu tooallow trafic entrant du trafic tcp port 32xx (où xx est le numéro du système de votre système SAP hello).
>
>

- - -
#### <a name="security-recommendations"></a>Recommandations de sécurité
Hello interface GUI SAP ne connecte pas immédiatement tooany hello d’instances de SAP (port 32xx) qui sont en cours d’exécution, mais se connecte d’abord via hello port ouvert toohello SAP message processus serveur (port 36xx). Bonjour au-delà de ce même port hello a été utilisé par le serveur de messages hello pour les instances d’application toohello hello communication interne. tooprevent local serveurs d’applications de communiquer par inadvertance avec un serveur message Bonjour Azure interne des ports de communication peuvent être modifiés. Il est recommandé de communication interne de hello toochange entre le serveur de messages SAP hello et son application instances tooa autre numéro de port sur les systèmes qui ont été clonés à partir de systèmes sur site, par exemple un clone de développement pour le projet de test etc. Cela est possible avec le paramètre de profil par défaut hello :

> rdisp/msserv_internal
>
>

comme indiqué dans : <https://help.sap.com/saphelp_nwpi71/helpdata/en/47/c56a6938fb2d65e10000000a42189c/content.htm>

## <a name="96a77628-a05e-475d-9df3-fb82217e8f14"></a>Concepts de déploiement cloud uniquement d’instances SAP
### <a name="3e9c3690-da67-421a-bc3f-12c520d99a30"></a>Machine virtuelle unique avec scénario de démonstration/formation SAP NetWeaver
![En cours d’exécution unique machine virtuelle systèmes de démonstration SAP avec hello mêmes noms de machine virtuelle, isolé dans Azure Cloud Services][planning-guide-figure-1700]

Dans ce scénario (consultez le chapitre [uniquement dans le Cloud] [ planning-guide-2.1] de ce document), nous implémentons un scénario de système de formation/démonstration classique où le scénario de formation/démonstration complète hello est contenue dans une seule machine virtuelle. Nous partons du principe que le déploiement de hello est effectuée via les modèles d’image de machine virtuelle. Nous supposons également que plusieurs de ces toobe de besoin de machines virtuelles de démonstration/formations déployé avec hello machines virtuelles ayant hello même nom.

hypothèse de Hello est que vous avez créé une Image de machine virtuelle comme décrit dans les sections du chapitre [préparation de machines virtuelles avec SAP pour Azure] [ planning-guide-5.2] dans ce document.

séquence Hello du scénario de hello tooimplement événements ressemble à ceci :

[comment]: <> (MShermannd TODO ont des exemples ARM tooprovide / description à l’aide de modèle json + éclaircissement concernant le nom de machine virtuelle unique au sein du réseau virtuel de ARM)   
##### <a name="powershell"></a>PowerShell
* Création d’un groupe de ressources pour chaque paysage de formation et de démonstration

```powershell
$rgName = "SAPERPDemo1"
New-AzureRmResourceGroup -Name $rgName -Location "North Europe"
```

* Création d’un nouveau compte de stockage

```powershell
$suffix = Get-Random -Minimum 100000 -Maximum 999999
$account = New-AzureRmStorageAccount -ResourceGroupName $rgName -Name "saperpdemo$suffix" -SkuName Standard_LRS -Kind "Storage" -Location "North Europe"
```

* Créez un réseau virtuel pour chaque utilisation hello de formation/démonstration paysage tooenable Hello même nom d’hôte et les adresses IP. réseau virtuel de Hello est protégé par un groupe de sécurité réseau qui autorise uniquement l’accès Bureau à distance de trafic tooport 3389 tooenable et le port 22 pour SSH.

```powershell
# Create a new Virtual Network
$rdpRule = New-AzureRmNetworkSecurityRuleConfig -Name SAPERPDemoNSGRDP -Protocol * -SourcePortRange * -DestinationPortRange 3389 -Access Allow -Direction Inbound -SourceAddressPrefix * -DestinationAddressPrefix * -Priority 100
$sshRule = New-AzureRmNetworkSecurityRuleConfig -Name SAPERPDemoNSGSSH -Protocol * -SourcePortRange * -DestinationPortRange 22 -Access Allow -Direction Inbound -SourceAddressPrefix * -DestinationAddressPrefix * -Priority 101
$nsg = New-AzureRmNetworkSecurityGroup -Name SAPERPDemoNSG -ResourceGroupName $rgName -Location  "North Europe" -SecurityRules $rdpRule,$sshRule

$subnetConfig = New-AzureRmVirtualNetworkSubnetConfig -Name Subnet1 -AddressPrefix  10.0.1.0/24 -NetworkSecurityGroup $nsg
$vnet = New-AzureRmVirtualNetwork -Name SAPERPDemoVNet -ResourceGroupName $rgName -Location "North Europe"  -AddressPrefix 10.0.1.0/24 -Subnet $subnetConfig
```

* Créer une nouvelle adresse IP publique qui peut être l’ordinateur virtuel utilisé tooaccess hello hello internet

```powershell
# Create a public IP address with a DNS name
$pip = New-AzureRmPublicIpAddress -Name SAPERPDemoPIP -ResourceGroupName $rgName -Location "North Europe" -DomainNameLabel $rgName.ToLower() -AllocationMethod Dynamic
```

* Créer une nouvelle interface réseau pour l’ordinateur virtuel de hello

```powershell
# Create a new Network Interface
$nic = New-AzureRmNetworkInterface -Name SAPERPDemoNIC -ResourceGroupName $rgName -Location "North Europe" -Subnet $vnet.Subnets[0] -PublicIpAddress $pip
```

* Création d’une machine virtuelle Pour le scénario de Cloud uniquement hello chaque machine virtuelle aura hello même nom. Hello SID SAP Hello SAP NetWeaver instances dans ces machines virtuelles seront identiques hello également. Au sein de hello le groupe de ressources Azure, nom hello Hello machine virtuelle doit toobe unique, mais dans différents groupes de ressources Azure vous pouvez exécuter des machines virtuelles avec hello même nom. Hello compte « Administrateur » de valeur par défaut de Windows, ou « root » pour Linux n’est pas valide. Par conséquent, un nouveau nom d’utilisateur administrateur doit toobe défini, ainsi qu’un mot de passe. taille de Hello Hello machine virtuelle doit également toobe défini.

```powershell
#####
# Create a new virtual machine with an official image from hello Azure Marketplace
#####
$cred=Get-Credential -Message "Type hello name and password of hello local administrator account."
$vmconfig = New-AzureRmVMConfig -VMName SAPERPDemo -VMSize Standard_D11

# select image
$vmconfig = Set-AzureRmVMSourceImage -VM $vmconfig -PublisherName "MicrosoftWindowsServer" -Offer "WindowsServer" -Skus "2012-R2-Datacenter" -Version "latest"
$vmconfig = Set-AzureRmVMOperatingSystem -VM $vmconfig -Windows -ComputerName "SAPERPDemo" -Credential $cred -ProvisionVMAgent -EnableAutoUpdate
# $vmconfig = Set-AzureRmVMSourceImage -VM $vmconfig -PublisherName "SUSE" -Offer "SLES" -Skus "12" -Version "latest"
# $vmconfig = Set-AzureRmVMSourceImage -VM $vmconfig -PublisherName "RedHat" -Offer "RHEL" -Skus "7.2" -Version "latest"
# $vmconfig = Set-AzureRmVMOperatingSystem -VM $vmconfig -Linux -ComputerName "SAPERPDemo" -Credential $cred

$vmconfig = Add-AzureRmVMNetworkInterface -VM $vmconfig -Id $nic.Id

$diskName="os"
$osDiskUri=$account.PrimaryEndpoints.Blob.ToString() + "vhds/" + $diskName  + ".vhd"
$vmconfig = Set-AzureRmVMOSDisk -VM $vmconfig -Name $diskName -VhdUri $osDiskUri -CreateOption fromImage
$vm = New-AzureRmVM -ResourceGroupName $rgName -Location "North Europe" -VM $vmconfig
```

```powershell
#####
# Create a new virtual machine with a VHD that contains hello private image that you want toouse
#####
$cred=Get-Credential -Message "Type hello name and password of hello local administrator account."
$vmconfig = New-AzureRmVMConfig -VMName SAPERPDemo -VMSize Standard_D11

$vmconfig = Add-AzureRmVMNetworkInterface -VM $vmconfig -Id $nic.Id

$diskName="osfromimage"
$osDiskUri=$account.PrimaryEndpoints.Blob.ToString() + "vhds/" + $diskName  + ".vhd"

$vmconfig = Set-AzureRmVMOSDisk -VM $vmconfig -Name $diskName -VhdUri $osDiskUri -CreateOption fromImage -SourceImageUri <path tooVHD that contains hello OS image> -Windows
$vmconfig = Set-AzureRmVMOperatingSystem -VM $vmconfig -Windows -ComputerName "SAPERPDemo" -Credential $cred
#$vmconfig = Set-AzureRmVMOSDisk -VM $vmconfig -Name $diskName -VhdUri $osDiskUri -CreateOption fromImage -SourceImageUri <path tooVHD that contains hello OS image> -Linux
#$vmconfig = Set-AzureRmVMOperatingSystem -VM $vmconfig -Linux -ComputerName "SAPERPDemo" -Credential $cred

$vm = New-AzureRmVM -ResourceGroupName $rgName -Location "North Europe" -VM $vmconfig
```

* Si vous le souhaitez, ajoutez des disques supplémentaires et restaurez le contenu nécessaire. N’oubliez pas que tous les noms d’objets blob (BLOB toohello de l’URL) doivent être uniques dans Azure.

```powershell
# Optional: Attach additional data disks
$vm = Get-AzureRmVM -ResourceGroupName $rgName -Name SAPERPDemo
$dataDiskUri = $account.PrimaryEndpoints.Blob.ToString() + "vhds/datadisk.vhd"
Add-AzureRmVMDataDisk -VM $vm -Name datadisk -VhdUri $dataDiskUri -DiskSizeInGB 1023 -CreateOption empty | Update-AzureRmVM
```

##### <a name="cli"></a>Interface de ligne de commande
Hello suivant l’exemple de code peut être utilisé sur Linux. Pour Windows, soit utilisez PowerShell comme décrit ci-dessus ou adapter hello exemple toouse % rgName % au lieu de $rgName et définir la variable d’environnement hello à l’aide de la commande de Windows hello *définir*.

* Création d’un groupe de ressources pour chaque paysage de formation et de démonstration

```
rgName=SAPERPDemo1
rgNameLower=saperpdemo1
azure group create $rgName "North Europe"
```

* Création d’un nouveau compte de stockage

```
azure storage account create --resource-group $rgName --location "North Europe" --kind Storage --sku-name LRS $rgNameLower
```

* Créez un réseau virtuel pour chaque utilisation hello de formation/démonstration paysage tooenable Hello même nom d’hôte et les adresses IP. réseau virtuel de Hello est protégé par un groupe de sécurité réseau qui autorise uniquement l’accès Bureau à distance de trafic tooport 3389 tooenable et le port 22 pour SSH.

```
azure network nsg create --resource-group $rgName --location "North Europe" --name SAPERPDemoNSG
azure network nsg rule create --resource-group $rgName --nsg-name SAPERPDemoNSG --name SAPERPDemoNSGRDP --protocol \* --source-address-prefix \* --source-port-range \* --destination-address-prefix \* --destination-port-range 3389 --access Allow --priority 100 --direction Inbound
azure network nsg rule create --resource-group $rgName --nsg-name SAPERPDemoNSG --name SAPERPDemoNSGSSH --protocol \* --source-address-prefix \* --source-port-range \* --destination-address-prefix \* --destination-port-range 22 --access Allow --priority 101 --direction Inbound

azure network vnet create --resource-group $rgName --name SAPERPDemoVNet --location "North Europe" --address-prefixes 10.0.1.0/24
azure network vnet subnet create --resource-group $rgName --vnet-name SAPERPDemoVNet --name Subnet1 --address-prefix 10.0.1.0/24 --network-security-group-name SAPERPDemoNSG
```

* Créer une nouvelle adresse IP publique qui peut être l’ordinateur virtuel utilisé tooaccess hello hello internet

```
azure network public-ip create --resource-group $rgName --name SAPERPDemoPIP --location "North Europe" --domain-name-label $rgNameLower --allocation-method Dynamic
```

* Créer une nouvelle interface réseau pour l’ordinateur virtuel de hello

```
azure network nic create --resource-group $rgName --location "North Europe" --name SAPERPDemoNIC --public-ip-name SAPERPDemoPIP --subnet-name Subnet1 --subnet-vnet-name SAPERPDemoVNet
```

* Création d’une machine virtuelle Pour le scénario de Cloud uniquement hello chaque machine virtuelle aura hello même nom. Hello SID SAP Hello SAP NetWeaver instances dans ces machines virtuelles seront identiques hello également. Au sein de hello le groupe de ressources Azure, nom hello Hello machine virtuelle doit toobe unique, mais dans différents groupes de ressources Azure vous pouvez exécuter des machines virtuelles avec hello même nom. Hello compte « Administrateur » de valeur par défaut de Windows, ou « root » pour Linux n’est pas valide. Par conséquent, un nouveau nom d’utilisateur administrateur doit toobe défini, ainsi qu’un mot de passe. taille de Hello Hello machine virtuelle doit également toobe défini.

```
azure vm create --resource-group $rgName --location "North Europe" --name SAPERPDemo --nic-name SAPERPDemoNIC --image-urn MicrosoftWindowsServer:WindowsServer:2012-R2-Datacenter:latest --os-type Windows --admin-username <username> --admin-password <password> --vm-size Standard_D11 --os-disk-vhd https://$rgNameLower.blob.core.windows.net/vhds/os.vhd --disable-boot-diagnostics
# azure vm create --resource-group $rgName --location "North Europe" --name SAPERPDemo --nic-name SAPERPDemoNIC --image-urn SUSE:SLES:12:latest --os-type Linux --admin-username <username> --admin-password <password> --vm-size Standard_D11 --os-disk-vhd https://$rgNameLower.blob.core.windows.net/vhds/os.vhd --disable-boot-diagnostics
# azure vm create --resource-group $rgName --location "North Europe" --name SAPERPDemo --nic-name SAPERPDemoNIC --image-urn RedHat:RHEL:7.2:latest --os-type Linux --admin-username <username> --admin-password <password> --vm-size Standard_D11 --os-disk-vhd https://$rgNameLower.blob.core.windows.net/vhds/os.vhd --disable-boot-diagnostics
```

```
#####
# Create a new virtual machine with a VHD that contains hello private image that you want toouse
#####
azure vm create --resource-group $rgName --location "North Europe" --name SAPERPDemo --nic-name SAPERPDemoNIC --os-type Windows --admin-username <username> --admin-password <password> --vm-size Standard_D11 --os-disk-vhd https://$rgNameLower.blob.core.windows.net/vhds/os.vhd -Q <path tooimage vhd> --disable-boot-diagnostics
#azure vm create --resource-group $rgName --location "North Europe" --name SAPERPDemo --nic-name SAPERPDemoNIC --os-type Linux --admin-username <username> --admin-password <password> --vm-size Standard_D11 --os-disk-vhd https://$rgNameLower.blob.core.windows.net/vhds/os.vhd -Q <path tooimage vhd> --disable-boot-diagnostics
```

* Si vous le souhaitez, ajoutez des disques supplémentaires et restaurez le contenu nécessaire. N’oubliez pas que tous les noms d’objets blob (BLOB toohello de l’URL) doivent être uniques dans Azure.

```
# Optional: Attach additional data disks
azure vm disk attach-new --resource-group $rgName --vm-name SAPERPDemo --size-in-gb 1023 --vhd-name datadisk
```

##### <a name="template"></a>Modèle
Vous pouvez utiliser les exemples de modèles hello sur le référentiel d’azure-démarrage rapide-modèles hello sur github.

* [Machine virtuelle Linux simple](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-simple-linux)
* [Machine virtuelle Windows simple](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-simple-windows)
* [Machine virtuelle à partir d’une image](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-from-user-image)

### <a name="implement-a-set-of-vms-which-need-toocommunicate-within-azure"></a>Implémentation d’un ensemble de machines virtuelles qui doivent toocommunicate dans Azure
Ce scénario uniquement dans le Cloud est un scénario classique pour les besoins de formation et de démonstration où hello logiciel représentant hello scénario de démonstration/formation est réparti sur plusieurs machines virtuelles. Hello différents composants installés dans hello différentes machines virtuelles besoin toocommunicate entre eux. Dans ce scénario, aucune communication réseau locale ou scénario entre sites locaux n’est nécessaire.

Ce scénario est une extension de l’installation de hello décrite au chapitre [machines virtuelles avec SAP NetWeaver scénario de démonstration/formation] [ planning-guide-7.1] de ce document. Dans ce cas d’autres machines virtuelles figurera tooan groupe de ressources existant. Bonjour paysage de formation suivant exemple hello se compose d’un virtuelle ASCS/SCS SAP, une machine virtuelle exécutant un SGBD et une instance de serveur d’applications SAP machine virtuelle.

Avant de créer ce scénario, vous devez toothink sur les paramètres de base déjà testés dans un scénario de hello avant.

#### <a name="resource-group-and-virtual-machine-naming"></a>Dénomination des groupes de ressources et des machines virtuelles
Tous les noms de groupe de ressources doivent être uniques. Développez votre propre schéma de dénomination de vos ressources, tel que `<rg-name`>-suffixe.

nom d’ordinateur virtuel Hello a toobe unique au sein du groupe de ressources hello.

#### <a name="setup-network-for-communication-between-hello-different-vms"></a>Configurer un réseau pour la communication entre hello différentes machines virtuelles
![Ensemble de machines virtuelles au sein d’un réseau virtuel Azure][planning-guide-figure-1900]

tooprevent d’affectation de noms collisions avec les clones de hello même paysages de formations/démonstration, vous devez toocreate un réseau virtuel Azure pour chaque paysage. Résolution de noms DNS est assurée par Azure, ou vous pouvez configurer votre propre serveur DNS en dehors d’Azure (pas toobe expliquée ici). Dans ce scénario, nous ne configurons pas nos propres serveurs DNS. La communication via les noms d’hôte sera activée pour toutes les machines virtuelles du réseau virtuel Azure.

Hello raisons paysages de formations ou de démonstration tooseparate par les réseaux virtuels et non seulement les ressources de groupes peut être :

* Hello SAP paysage en tant qu’ensemble les besoins de son propre AD/OpenLDAP et une partie de toobe des besoins de serveur de domaine de chacun des paysages de hello.  
* Bonjour paysage SAP comme configuration comprend les composants que toowork besoin des adresses IP fixes.

Plus de détails sur les réseaux virtuels Azure et comment toodefine les trouverez dans [cet article][virtual-networks-create-vnet-arm-pportal].

## <a name="deploying-sap-vms-with-corporate-network-connectivity-cross-premises"></a>Déployer des machines virtuelles SAP avec une connectivité réseau d’entreprise (intersite)
Vous exécutez un paysage SAP et que vous souhaitez que le déploiement de hello toodivide entre complète pour les serveurs haut de gamme SGBD, les environnements virtualisées locales pour les couches application et de couche 2 plus petit configuré Azure IaaS et les systèmes SAP. principe Hello est que les systèmes SAP dans un paysage SAP toocommunicate entre eux et avec de nombreux autres composants logiciels déployés dans l’entreprise hello, indépendamment de leur forme de déploiement. Il ne doit avoir également aucune différence introduits par formulaire de déploiement hello pour se connecter avec l’interface utilisateur graphique SAP ou d’autres interfaces d’utilisateur final hello. Ces conditions peuvent uniquement être remplies lorsque nous avons hello locaux Active Directory/OpenLDAP et les services DNS étendus toohello systèmes Azure via la connectivité de site-à-site/plusieurs sites ou des connexions privées comme Azure ExpressRoute.

Dans l’ordre tooget de plus en arrière-plan sur les détails d’implémentation hello de SAP sur Azure, nous vous conseillons de tooread chapitre [déploiement Concepts de cloud uniquement des instances SAP] [ planning-guide-7] de ce document qui explique certains des concepts de base hello construit d’Azure et comment il doivent être utilisés avec les applications SAP dans Azure.

### <a name="scenario-of-a-sap-landscape"></a>Scénario d’un paysage SAP
scénario de Hello intersite peut être décrite à peu près comme dans les graphiques hello ci-après :

![Connectivité de site à site entre des ressources locales et Azure][planning-guide-figure-2100]

Hello scénario ci-dessus décrit un scénario où hello local AD/OpenLDAP et DNS est étendu tooAzure. Côté hello locale, une certaine plage d’adresses IP est réservée par abonnement Azure. plage d’adresses IP Hello sera attribué tooan réseau virtuel Azure sur hello côté Azure.

#### <a name="security-considerations"></a>Considérations relatives à la sécurité
Hello configuration minimale requise est hello utilisation de protocoles de communication sécurisée comme SSL/TLS pour l’accès du navigateur ou les connexions VPN pour le système d’accès toohello Azure services. hypothèse de Hello est que sociétés gérer un réseau VPN hello entre Azure et de leur réseau d’entreprise très différemment. Certaines entreprises ouvriront indifféremment tous les ports hello. Certains autres choisiront toobe très précise les ports dont ils ont besoin tooopen, etc..

Dans la table hello ci-dessous SAP classiques, les ports de communication sont répertoriés. En fait, il est suffisant tooopen hello port de passerelle SAP.

| Service | Nom du port | Exemple `<nn`> = 01 | Plage par défaut (min-max.) | Commentaire |
| --- | --- | --- | --- | --- |
| Répartiteur |sapdp`<nn>` voir * |3201 |3200 – 3299 |Répartiteur SAP, utilisé par l’interface utilisateur graphique SAP pour Windows et Java |
| Serveur de messagerie |sapms`<sid`> voir ** |3600 |sapms gratuit`<anySID`> |sid = SAP-System-ID |
| Passerelle |sapgw`<nn`> voir * |3301 |gratuit |Passerelle SAP, utilisée pour les communications CPIC et RFC |
| Routeur SAP |sapdp99 |3299 |gratuit |Uniquement les noms de Service de l’élément de configuration (instance centrale) peuvent être réaffectées dans valeur arbitraire de tooan/etc/services après l’installation. |

*) nn = Numéro d’instance SAP

**) sid = SAP-System-ID

Pour plus d’informations sur les ports nécessaires pour les différents produits ou services SAP, consultez <http://scn.sap.com/docs/DOC-17124>.
Avec ce document, vous devez être en mesure de tooopen dédié des ports dans le périphérique VPN de hello nécessaire pour les scénarios et les produits SAP spécifiques.

Autres mesures lorsque le déploiement de machines virtuelles dans un tel scénario peut être toocreate un [groupe de sécurité réseau] [ virtual-networks-nsg] toodefine les règles d’accès.

### <a name="dealing-with-different-virtual-machine-series"></a>Traiter les différentes séries de machines virtuelles
Cours hello 12 derniers mois Microsoft a ajouté des types de machine virtuelle plus nombreuses qui diffèrent dans le nombre de processeurs virtuels, mémoire ou plus important sur le matériel, il s’exécute sur. Toutes ces machines virtuelles ne sont pas prises en charge par SAP (voir les types de machines virtuelles pris en charge dans la Note de SAP [1928533]). Certaines de ces machines virtuelles s’exécutent sur diverses générations de matériel hôte. Ces générations de matériel hôte sont mise en route déployées dans la granularité de hello d’une unité d’échelle Azure. Signifie pourrait être le cas où les différentes tailles de machine virtuelle hello que vous avez choisi ne peut pas être exécuté sur hello même unité d’échelle. Un ensemble de disponibilité est limité hello toospan de capacité que des unités d’échelle en fonction de différents périphériques matériels.  Par exemple, Si vous souhaitez toorun hello SGBD sur des machines virtuelles de A5 à A11 et hello couche d’application SAP sur des machines virtuelles de série G, vous serez forcé toodeploy un système SAP ou différents systèmes SAP dans différents groupes à haute disponibilité.

#### <a name="printing-on-a-local-network-printer-from-sap-instance-in-azure"></a>Imprimer sur une imprimante réseau local à partir d’une instance SAP dans Azure
##### <a name="printing-over-tcpip-in-cross-premises-scenario"></a>Impression via TCP/IP dans un scénario intersite
Configuration des imprimantes réseau locales TCP/IP basés dans une machine virtuelle Azure est global hello identique à celle de votre réseau d’entreprise, en supposant que vous n’avez pas un tunnel VPN de Site à Site ou une connexion ExpressRoute.

- - -
> ![Windows][Logo_Windows] Windows
>
> toodo cela :
>
> * Certaines imprimantes réseau sont fournis avec un Assistant de configuration, ce qui la rend facile tooset de l’imprimante dans une machine virtuelle Azure. Si aucun logiciel de l’Assistant n’a été distribuée avec la façon de « manual » hello imprimante tooset d’imprimante de hello est toocreate un nouveau port d’imprimante TCP/IP.
> * Ouvrez Panneau de configuration -> Périphériques et imprimantes -> Ajouter une imprimante.
> * Cliquez sur Ajouter une imprimante à l’aide d’une adresse TCP/IP ou d’un nom d’hôte
> * Tapez Bonjour adresse IP de l’imprimante de hello
> * Le port standard de l’imprimante est 9100
> * Si nécessaire installer manuellement le pilote d’imprimante approprié hello.
>
> ![Linux][Logo_Linux] Linux
>
> * comme pour Windows juste suivez la procédure standard de hello tooinstall une imprimante réseau
> * Suivez les guides Linux publiques hello pour [SUSE](https://www.suse.com/documentation/sles-12/book_sle_deployment/data/sec_y2_hw_print.html) ou [Red Hat](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/6/html/Deployment_Guide/sec-Printer_Configuration.html) sur la façon de tooadd une imprimante.
>
>

- - -
![Impression en réseau][planning-guide-figure-2200]

##### <a name="host-based-printer-over-smb-shared-printer-in-cross-premises-scenario"></a>Imprimante basée sur l’hôte via SMB (imprimante partagée) dans un scénario intersite
Les imprimantes basées sur l’hôte ne sont pas compatibles réseau par défaut. Mais une imprimante basée sur l’hôte peut être partagée entre les ordinateurs d’un réseau tant que les imprimantes hello sont connecté tooa ordinateur sous tension. Connectez votre réseau via une connexion de site à site ou ExpressRoute et partagez votre imprimante locale. Hello protocole SMB utilise NetBIOS au lieu de DNS comme service de noms. nom d’hôte NetBIOS Hello peut être différent de nom d’hôte DNS hello. minuscules Hello est que le nom d’hôte NetBIOS hello et le nom d’hôte DNS hello sont identiques. domaine DNS de Hello ne se justifie pas dans l’espace de noms NetBIOS hello. En conséquence, hello nom d’hôte DNS complet, constitué du nom d’hôte DNS hello et de domaine DNS ne doit pas être utilisé dans l’espace de noms NetBIOS hello.

partage d’imprimante Hello est identifiée par un nom unique dans le réseau de hello :

* Nom d’hôte SMB hello (toujours obligatoire).
* Nom de partage hello (toujours obligatoire).
* Nom de domaine hello si le partage d’imprimante n’est pas hello même domaine que le système SAP.
* En outre, un nom d’utilisateur et un mot de passe peut-être partage d’imprimante hello tooaccess requis.

Activation

- - -
> ![Windows][Logo_Windows] Windows
>
> Partagez votre imprimante locale.
> Bonjour Azure VM ouvrez hello l’Explorateur Windows et type dans le nom de partage hello d’imprimante de hello.
> Un Assistant installation d’imprimante vous guidera tout au long des processus d’installation hello.
>
> ![Linux][Logo_Linux] Linux
>
> Voici quelques exemples de documents relatifs à la configuration des imprimantes réseau sous Linux ou comprenant un chapitre concernant l’impression sous Linux. Il fonctionnera hello est identique dans une machine virtuelle de Linux Azure tant que machine virtuelle de hello fait partie d’un réseau VPN :
>
> * SLES <https://en.opensuse.org/SDB:Printing_via_SMB_(Samba)_Share_or_Windows_Share>
> * RHEL <https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/6/html/Deployment_Guide/s1-printing-smb-printer.html>
>
>

- - -
##### <a name="usb-printer-printer-forwarding"></a>Imprimante USB (réacheminement d’imprimante)
Capacité hello Azure d’accès de hello hello Services Bureau à distance tooprovide utilisateurs tootheir périphérique d’impression local dans une session distante n’est pas disponible.

- - -
> ![Windows][Logo_Windows] Windows
>
> Pour plus d’informations sur l’impression avec Windows, consultez : <http://technet.microsoft.com/library/jj590748.aspx>.
>
>

- - -
#### <a name="integration-of-sap-azure-systems-into-correction-and-transport-system-tms-in-cross-premises"></a>Intégration de systèmes Azure SAP au système de transport et correction SAP (TMS) en local
Hello modification de SAP et le système de Transport (TMS) tooexport toobe configuré de besoins et importer la demande de transport entre les systèmes paysage de hello. Nous supposons que les instances de développement hello d’un système SAP (DEV) sont trouvent dans Azure tandis que l’assurance qualité hello (AQ) et les systèmes de production (PRD) sont locaux. En outre, nous supposons qu’il existe un répertoire de transport central.

##### <a name="configuring-hello-transport-domain"></a>Configuration hello domaine de Transport
Configurer votre domaine de Transport sur système hello vous avez désigné comme hello contrôleur de domaine de Transport, comme décrit dans [configuration hello contrôleur de domaine de Transport](http://help.sap.com/erp2005_ehp_04/helpdata/en/44/b4a0b47acc11d1899e0000e829fbbd/content.htm). Un utilisateur système que TMSADM sera créé et une hello requis de la destination RFC sera générée. Vous pouvez vérifier ces connexions RFC à l’aide de la transaction de hello SM59. La résolution de nom d’hôte doit être activée dans votre domaine de transport.

Activation

* Dans notre scénario, nous avons décidé hello local système de Choisissons sera le contrôleur de domaine CTS hello. Appelez le STMS de transaction. boîte de dialogue TMS Hello s’affiche. Une boîte de dialogue de configuration du domaine de transport s’affiche. (cette boîte de dialogue apparaît uniquement si vous n’avez pas encore configuré de domaine de transport).
* Assurez-vous que cet utilisateur hello créé automatiquement TMSADM est autorisé (SM59 -> connexion ABAP -> TMSADM@E61.DOMAIN_E61 -> Détails -> Utilitaires (m) -> Test d’autorisation). écran initial de Hello de la transaction STMS doit indiquer que ce système SAP fonctionne désormais comme contrôleur hello du domaine de transport hello comme indiqué ici :

![Écran initial de la transaction STMS sur le contrôleur de domaine hello][planning-guide-figure-2300]

#### <a name="including-sap-systems-in-hello-transport-domain"></a>Inclusion de systèmes SAP dans le domaine de Transport de hello
séquence Hello d’intégration d’un système SAP dans un domaine de transport se présente comme suit :

* Sur hello système de développement dans Azure, accédez toohello système de transport (Client 000) et appelez la transaction STMS. Choisissez un autre Configuration à partir de la boîte de dialogue hello et continuez à inclure le système dans le domaine. Spécifiez hello contrôleur de domaine comme hôte cible ([, y compris les systèmes SAP dans le domaine de Transport de hello](http://help.sap.com/erp2005_ehp_04/helpdata/en/44/b4a0c17acc11d1899e0000e829fbbd/content.htm?frameset=/en/44/b4a0b47acc11d1899e0000e829fbbd/frameset.htm)). Hello système est maintenant toobe attente inclus dans le domaine de transport hello.
* Pour des raisons de sécurité, vous devez ensuite tooconfirm de contrôleur de domaine de retour toohello toogo votre demande. Choisir vue d’ensemble du système et approuver de système de hello en attente. Vérifiez ensuite la configuration invite et hello hello sera distribuée.

Ce système SAP contient désormais hello informations hello tous les autres systèmes SAP dans le domaine de transport hello. À hello même moment, adresse hello données du système SAP de la nouvelle hello sont envoyées, hello système SAP est entré dans le profil de transport hello du programme de contrôle de transport hello et tooall hello autres systèmes SAP. Vérifiez si les RFC et le répertoire de transport accès toohello du domaine de hello fonctionnent.

Poursuivre la configuration de hello de votre système de transport comme d’habitude comme décrit dans la documentation de hello [Change and Transport System](http://help.sap.com/saphelp_nw70ehp3/helpdata/en/48/c4300fca5d581ce10000000a42189c/content.htm?frameset=/en/44/b4a0b47acc11d1899e0000e829fbbd/frameset.htm).

Activation

* Assurez-vous que votre STMS en local est configuré correctement.
* Assurez-vous que le nom d’hôte hello Hello contrôleur de domaine de Transport peut être résolu par votre machine virtuelle sur Azure et vice versa.
* Appelez le STMS de transaction -> Other Configuration -> Include System in Domain (-> Autre configuration -> Inclure le système dans le domaine).
* Vérifiez la connexion hello Bonjour sur le système de site TMS.
* Configurez les itinéraires de transport, les groupes et les couches comme d’habitude.

Dans les scénarios d’entre différents locaux connectés de site à site, latence hello entre locaux et Azure peut néanmoins être substantielle. Si nous suive hello de transport d’objets via tooproduction de systèmes de développement et de test ou que vous pensez à appliquer des transports ou toohello différents systèmes de packages de prise en charge, vous gardez à l’esprit que, dépendant de l’emplacement hello de transport central de hello répertoire, certains des systèmes de hello rencontrent une latence élevée lors de la lecture ou l’écriture des données dans le répertoire de transport central hello. Hello est les configurations de paysage tooSAP similaires où les différents systèmes de hello sont répartis sur différents centres de données éloignés les uns hello des centres de données.

Dans commande toowork autour de cette latence et de disposer de systèmes de hello travail rapide dans lecture ou écriture tooor à partir du répertoire de transport hello, vous pouvez configurer deux domaines de transport STMS (un pour local. et l’autre avec les systèmes hello dans les domaines de transport hello Azure et de lien Consultez la documentation qui explique les principes de hello ce concept dans hello SAP TMS : <http://help.sap.com/saphelp_me60/helpdata/en/c4/6045377b52253de10000009b38f889/content.htm?frameset=/en/57/ 38dd924eb711d182bf0000e829fbfe/FRAMESET.htm>.

Activation

* Configurer un domaine de transport sur chaque emplacement (local et Azure) à l’aide du STMS de transaction <http://help.sap.com/saphelp_nw70ehp3/helpdata/en/44/b4a0b47acc11d1899e0000e829fbbd/content.htm>
* Liez les domaines de hello avec un lien de domaine et confirmer le lien hello entre deux domaines de hello.
  <http://help.sap.com/saphelp_nw73ehp1/helpdata/en/a3/139838280c4f18e10000009b38f8cf/content.htm>
* Distribuer hello configuration toohello lié système.

#### <a name="rfc-traffic-between-sap-instances-located-in-azure-and-on-premises-cross-premises"></a>Trafic RFC entre des instances SAP situées dans Azure et en local (intersite)
Trafic RFC entre les systèmes locaux et dans Azure doit toowork. toosetup une connexion appeler transaction SM59 dans un système source où vous devez toodefine une connexion RFC vers le système cible de hello. configuration de Hello est similaire toohello standard le programme d’installation d’une connexion RFC.

Nous partons du principe que dans un scénario de coexistence hello, machines virtuelles de hello se trouvent dans les systèmes SAP exécution nécessitant toocommunicate entre eux hello même domaine. Par conséquent hello le programme d’installation d’une connexion RFC entre les systèmes SAP ne diffère pas d’étapes de configuration hello et les entrées dans les scénarios sur site.

#### <a name="accessing-local-fileshares-from-sap-instances-located-in-azure-or-vice-versa"></a>Accéder à des partages de fichiers locaux à partir d’instances SAP situées dans Azure ou inversement.
Les instances SAP situées dans Azure doivent tooaccess les partages de fichiers qui se trouvent dans les locaux d’entreprise hello. En outre, les instances SAP locales doivent tooaccess les partages de fichiers qui sont trouvent dans Azure. partages de fichiers hello tooenable vous devez configurer les options de partage sur le système local de hello et les autorisations de hello. Assurez-vous que tooopen hello ports hello VPN ou une connexion ExpressRoute entre Azure et votre centre de données.

## <a name="supportability"></a>Prise en charge
### <a name="6f0a47f3-a289-4090-a053-2521618a28c3"></a>Solution de surveillance Azure pour SAP
Outils de surveillance SAPOSCOL ou l’Agent hôte SAP récupèrent les données hôte de Service de Machine virtuelle Azure hello via une Extension de surveillance Azure pour SAP dans l’ordre tooenable hello analyse des systèmes SAP stratégiques sur Azure hello SAP. Depuis les applications très spécifiques tooSAP hello les exigences de SAP, Microsoft a décidé de pas toogenerically implémentent hello requis fonctionnalités dans Azure, mais laisser pour les clients toodeploy hello nécessaire analyse les configurations et les composants tootheir Machines virtuelles s’exécutant dans Azure. Toutefois, gestion du cycle de vie et de déploiement de hello analyse des composants est en grande partie automatisée par Azure.

#### <a name="solution-design"></a>Conception de la solution
solution de Hello développé tooenable que surveillance SAP repose sur l’architecture hello de l’Agent de machine virtuelle Azure et une structure d’Extension. idée Hello du framework de l’Agent de machine virtuelle Azure et l’Extension hello est installation tooallow d’applications logicielles disponibles dans la galerie d’Extension de machine virtuelle Azure hello dans une machine virtuelle. Hello principe idée de ce concept est tooallow (dans ce cas hello Extension de surveillance Azure pour SAP), hello du déploiement de fonctionnalités spéciales dans une configuration de machine virtuelle et hello de ces logiciels au moment du déploiement.

Depuis février 2014, hello 'Agent de machine virtuelle Azure' qui permet de gérer des Extensions de machine virtuelle Azure spécifique au sein de hello que machine virtuelle est injecté dans les machines virtuelles Windows par défaut sur la création d’ordinateurs virtuels dans hello portail Azure. En cas de hello SUSE ou Red Hat Linux agent de machine virtuelle est déjà partie de l’image Azure Marketplace. Dans le cas où une serait télécharger un VM Linux à partir d’agent de machine virtuelle locale tooAzure hello a toobe installé manuellement.

Hello des blocs de construction de la solution de surveillance hello dans Azure pour SAP ressemble à ceci :

![Composants d’extension Microsoft Azure][planning-guide-figure-2400]

Comme indiqué dans le diagramme de blocs hello ci-dessus, une partie de la solution de surveillance pour SAP de hello est hébergée dans hello Image de machine virtuelle Azure et de la galerie d’extensions Azure est un référentiel à réplication globale qui est géré par Azure Operations. Il incombe hello équipe hello commune SAP/MS travaillant sur hello implémentation Azure de SAP toowork avec les opérations Azure toopublish nouvelles versions de hello Extension de surveillance Azure pour SAP. Cette Extension de surveillance Azure pour SAP utilisera hello de l’Extension Microsoft Azure Diagnostics (WAD) ou Linux Azure Diagnostics (SCÉNARISTE) tooget hello les informations nécessaires.

Lorsque vous déployez une machine virtuelle Windows, hello « Agent de machine virtuelle Azure » est automatiquement ajoutée dans hello machine virtuelle. fonction Hello de cet agent est hello toocoordinate chargement configuration Hello Extensions Azure pour l’analyse des systèmes SAP NetWeaver. Pour les machines virtuelles Linux hello Agent de machine virtuelle Azure est déjà partie d’une image de système d’exploitation de Azure Marketplace hello.

Toutefois, il est une étape qui doit tout de même toobe exécutée par le client de hello. C’est l’activation du hello et configuration de la collecte des performances hello. processus de Hello liées toohello 'configuration' est automatisée par un script PowerShell ou d’une commande CLI. Hello script PowerShell peut être téléchargé dans hello Microsoft Azure Script Center, comme décrit dans hello [Guide de déploiement][deployment-guide].

Hello Architecture globale de hello Azure solution de surveillance pour SAP ressemble à ceci :

![Solution de surveillance Azure pour SAP NetWeaver][planning-guide-figure-2500]

**Pour hello exacte procédure-tooand pour une procédure détaillée de l’utilisation de ces applets de commande PowerShell ou d’une commande CLI pendant les déploiements, suivez les instructions hello Bonjour [Guide de déploiement][deployment-guide].**

### <a name="integration-of-azure-located-sap-instance-into-saprouter"></a>Intégration d’instances SAP situées dans Azure dans SAProuter
Instances SAP s’exécutant dans Azure doivent toobe accessible à partir de SAProuter également.

![Connexion réseau du routeur SAP][planning-guide-figure-2600]

Un programme SAProuter permet hello TCP/IP à des systèmes si aucune connexion IP directe. Cela présente des avantages de hello qu’aucune connexion de bout en bout entre les partenaires de communication hello est nécessaire au niveau du réseau. Hello SAProuter écoute sur le port 3299 par défaut.
instances de tooconnect SAP via un programme SAProuter vous devez toogive hello chaîne SAProuter et le nom d’hôte avec n’importe quel tooconnect tentative.

## <a name="sap-netweaver-as-java"></a>SAP NetWeaver AS Java
Jusqu'à présent hello essentiellement sur les documents hello a été SAP NetWeaver en général ou hello les pile ABAP SAP NetWeaver. Dans cette petite section Considérations spécifiques sur la pile Java de SAP de hello sont répertoriés. Une des plus importante Java de SAP NetWeaver exclusivement les applications basées sur des hello est hello SAP Enterprise Portal. Autres SAP NetWeaver en fonction des applications comme SAP PI et SAP Solution Manager hello ABAP SAP NetWeaver et les piles de Java. Par conséquent, il certainement est une nécessité tooconsider des aspects spécifiques connexes toohello Java de SAP NetWeaver pile également.

### <a name="sap-enterprise-portal"></a>Portail d’entreprise SAP
le programme d’installation de Hello d’un portail SAP dans une Machine virtuelle Azure ne diffère pas d’une installation locale sur si vous déployez dans les scénarios de coexistence. Depuis hello que DNS est effectué en local, les paramètres de port hello des instances individuelles de hello peuvent faire configurés localement. recommandations de Hello et restrictions décrites jusque-là dans ce document s’appliquent pour une application comme SAP Enterprise Portal ou la pile Java de SAP NetWeaver de hello en général.

![Portail SAP exposé][planning-guide-figure-2700]

Un scénario de déploiement spécifique à certains clients est une exposition directe hello de hello SAP Enterprise Portal toohello Internet pendant que l’hôte d’ordinateur virtuel hello est connecté toohello réseau d’entreprise via un tunnel VPN ou ExpressRoute de site à site. Pour ce scénario, vous avez toomake que des ports spécifiques sont ouverts et pas bloqué par un pare-feu réseau ou un groupe de sécurité. Hello même approche doit toobe appliquée lorsque vous souhaitez tooconnect tooan Java de SAP instance sur site dans un scénario de Cloud uniquement.

URI de portail initial Hello est http (s) :`<Portalserver`> : 5XX00/irj où le port de hello est formé par 50000 signe plus (Numéro_système × 100). Bonjour par défaut portail URI du système SAP 00 est `<dns name`>.`<azure region` >.Cloudapp.azure.com:PublicPort/irj. Pour plus de détails, consultez <http://help.sap.com/saphelp_nw70ehp1/helpdata/de/a2/f9d7fed2adc340ab462ae159d19509/frameset.htm>.

![Configuration du point de terminaison][planning-guide-figure-2800]

Si vous souhaitez toocustomize hello URL et/ou les ports de SAP Enterprise Portal, consultez la documentation :

* [Change Portal URL (Modifier l’URL du portail)](http://wiki.scn.sap.com/wiki/display/EP/Change+Portal+URL)
* [Change Default port numbers, Portal port numbers (Modifier les numéros de port par défaut et les numéros de ports du portail)](http://wiki.scn.sap.com/wiki/display/NWTech/Change+Default++port+numbers%2C+Portal+port+numbers)

<a name="7cf991a1-badd-40a9-944e-7baae842a058"></a>
## <a name="high-availability-ha-and-disaster-recovery-dr-for-sap-netweaver-running-on-azure-virtual-machines"></a>Haute disponibilité (HA) et récupération d’urgence (DR)pour SAP NetWeaver s’exécutant sur des machines virtuelles Azure
### <a name="definition-of-terminologies"></a>Définition des termes
Hello terme **haute disponibilité (HA)** est généralement connexe tooa un ensemble de technologies qui réduit les interruptions d’informatique en fournissant la continuité des services informatiques via redondants et à tolérance de panne ou composants protégés de basculement à l’intérieur de hello **même** centre de données. Dans notre cas, au sein d’une région Azure.

La **récupération d’urgence (DR)** vise également à réduire l’interruption des services informatiques et leur récupération, mais entre **différents** centres de données, généralement éloignés de plusieurs centaines de kilomètres les uns des autres. Dans notre cas généralement entre les différentes régions Azure dans hello même région géopolitique ou établie par vous, en tant que client.

### <a name="overview-of-high-availability"></a>Vue d’ensemble de la haute disponibilité
Nous pouvons séparer discussion hello sur SAP haute disponibilité dans Azure en deux parties :

* La **haute disponibilité de l’infrastructure Azure**, par exemple, celle du calcul (machines virtuelles), du réseau, du stockage, etc., et ses avantages en termes d’augmentation de la disponibilité des applications SAP.
* La **haute disponibilité des applications SAP**, par exemple, celle des composants logiciels SAP :
  * Serveurs d’application SAP
  * Instance SAP ASCS/SCS
  * Serveur de base de données

et comment il peut être combiné avec la haute disponibilité de l’infrastructure Azure.

Haute disponibilité SAP dans Azure a certaines différences par rapport de tooSAP haute disponibilité dans un environnement physique ou virtuel de local. Hello suivant document SAP suivant décrit les configurations de la haute disponibilité SAP standard dans des environnements virtualisés sur Windows : <http://scn.sap.com/docs/DOC-44415>. Il n’existe aucune configuration haute disponibilité SAP intégrée pour Linux comparable à celle de Windows. Des informations concernant la haute disponibilité SAP en local pour Linux sont disponibles ici : <http://scn.sap.com/docs/DOC-8541>.

### <a name="azure-infrastructure-high-availability"></a>haute disponibilité de l’infrastructure Azure
Aucun contrat de niveau de service (SLA) de machine virtuelle unique n’est disponible actuellement sur les machines virtuelles Azure. tooget une idée de la disponibilité de hello d’une seule machine virtuelle peut se présenter comme vous pouvez générer simplement produit hello de hello différents contrats SLA de Azure disponibles : <https://azure.microsoft.com/support/legal/sla/>.

base Hello pour le calcul de hello est de 30 jours par mois ou 43 200 minutes. Par conséquent, le temps mort de 0,05 % correspond too21.6 minutes. Comme d’habitude, disponibilité hello différents services de hello multiplie Bonjour de configuration suivant :

(Service de disponibilité #1/100) * (Service de disponibilité #2/100) * (Service de disponibilité #3/100) *…

comme ce qui suit :

(99,95/100) * (99,9/100) * (99,9/100) = 0,9975, soit une disponibilité globale de 99,75 %.

#### <a name="virtual-machine-vm-high-availability"></a>Haute disponibilité de la machine virtuelle
Il existe deux types d’événements de plateforme Azure qui peuvent affecter la disponibilité de hello de vos machines virtuelles : planifié la maintenance et la maintenance non planifiés.

* Événements de maintenance planifiée sont mises à jour périodiques effectuées par toohello Microsoft sous-jacent tooimprove de la plateforme Azure fiabilité, les performances et sécurité de l’infrastructure de plateforme hello vos machines virtuelles s’exécutent sur.
* Maintenance non planifiés se produisent lorsque le matériel de hello ou infrastructure physique sous-jacent de votre machine virtuelle a généré une erreur d’une certaine façon. Cela comprend les défaillances du réseau local, du disque local ou au niveau du rack. Lorsqu’un tel échec est détecté, hello plateforme Azure migrerez automatiquement votre machine virtuelle à partir du serveur physique défectueux hello qui héberge votre serveur physique ordinateur virtuel tooa sain. Ces événements sont rares, mais peuvent aussi causer tooreboot de votre machine virtuelle.

Vous trouverez plus de détails dans cette documentation : <http://azure.microsoft.com/documentation/articles/virtual-machines-manage-availability>

#### <a name="azure-storage-redundancy"></a>Redondance d’Azure Storage
les données de salutation dans votre compte de stockage Microsoft Azure soient toujours tooensure répliqué durabilité et une haute disponibilité, réunion hello SLA du stockage Azure, même en face de hello de défaillances matérielles temporaires

Étant donné que le stockage Azure reste 3 images des données de hello par défaut, RAID5 ou RAID1 sur plusieurs disques Azure ne sont pas nécessaires.

Vous trouverez plus de détails dans cet article : <http://azure.microsoft.com/documentation/articles/storage-redundancy/>.

#### <a name="utilizing-azure-infrastructure-vm-restart-tooachieve-higher-availability-of-sap-applications"></a>Utilisation de machine virtuelle d’Infrastructure Azure redémarre tooAchieve « Disponibilité élevée » des Applications SAP
Si vous ne décidez pas les fonctionnalités toouse comme serveur de basculement Windows (WSFC) ou un équivalent Linux (hello ce dernier une n'est pas encore pris en charge sur Azure en combinaison avec les logiciels SAP), redémarrer des ordinateurs virtuels Azure est tooprotect utilisé un système SAP sur planifié et temps d’arrêt non planifié de hello Azure infrastructure physique et l’ensemble de la plate-forme Azure sous-jacente.

> [!NOTE]
> Il est importante toomention que principalement redémarrer des ordinateurs virtuels Azure protège les machines virtuelles et les applications non. Le redémarrage de la machine virtuelle n’offre pas de haute disponibilité pour les applications SAP, mais un certain niveau de disponibilité de l’infrastructure et, par conséquent, indirectement une « plus haute disponibilité » des systèmes SAP. Il n’existe également aucun contrat SLA pour hello durée toorestart une machine virtuelle après une panne de l’hôte planifié ou non. Par conséquent, cette méthode de haute disponibilité n’est pas adaptée aux composants essentiels d’un système SAP, tel qu’un (A)SCS ou un SGBD (système de gestion de base de données).
>
>

Le stockage est un autre élément important d’infrastructure pour la haute disponibilité. Par exemple, Le contrat de niveau de service SLA assure une disponibilité de 99,9 %. Si une personne déploie toutes les machines virtuelles et ses disques sur un compte Azure Storage unique, l’indisponibilité potentielle d’Azure Storage entraînera celle de toutes les machines virtuelles placées dans ce compte Azure Storage et également celle de tous les composants SAP s’exécutant sur ces dernières.  

Au lieu de placer toutes les machines virtuelles dans un seul compte Azure Storage, vous pouvez également utiliser les comptes de stockage dédiés pour chaque machine virtuelle et ainsi augmenter la disponibilité globale des machines virtuelles et des applications SAP en utilisant plusieurs comptes Azure Storage indépendants.

Voici un exemple de ce à quoi une architecture de système SAP NetWeaver utilisant la haute disponibilité d’infrastructure Azure pourrait ressembler :

![Utilisation de l’infrastructure Azure HA tooachieve SAP « supérieur » des disponibilités des applications][planning-guide-figure-2900]

Pour les composants SAP critiques, nous avons obtenu hello suivant jusqu'à présent :

* La haute disponibilité des serveurs d’applications SAP

Les instances de serveur d’applications SAP sont des composants redondants. Chaque instance de serveur d’applications SAP est déployée sur sa propre machine virtuelle s’exécutant dans un domaine de mise à niveau et d’erreur différent (voir les chapitres [Domaines d’erreur][planning-guide-3.2.1] et [Domaines de mise à niveau][planning-guide-3.2.2]). Cela est assuré par l’utilisation des groupes à haute disponibilité Azure (voir le chapitre [Groupes à haute disponibilité Azure][planning-guide-3.2.3]). L’indisponibilité planifiée ou non planifiée potentielle d’un domaine de mise à niveau ou d’erreur Azure entraîne l’indisponibilité d’un nombre limité de machines virtuelles avec leurs instances de serveurs d’applications SAP.
Chaque instance de serveur d’applications SAP est placée dans son propre compte Azure Storage : l’indisponibilité potentielle d’un compte de stockage Azure provoquera l’indisponibilité d’une seule machine virtuelle et de son instance de serveur d’applications SAP. Toutefois, sachez qu’un abonnement Azure est limité quand au nombre de comptes Azure Storage. tooensure le démarrage automatique de l’instance de (A) SCS après le redémarrage de la machine virtuelle de hello, assurez-vous que tooset Autostart (paramètre) dans l’instance de (A) SCS démarrer profil décrite au chapitre [à l’aide du démarrage automatique pour les instances SAP][planning-guide-11.5].
Pour plus de détails, voir également le chapitre [Haute disponibilité pour les serveurs d’applications SAP][planning-guide-11.4.1].

* *plus haute* disponibilité de l’instance (A)SCS SAP

Ici, nous allons utiliser hello de tooprotect redémarrer des ordinateurs virtuels Azure VM avec l’instance (A) SCS SAP installée. Dans serveurs hello cas d’un arrêt planifié ou d’Azure, machines virtuelles seront redémarrés sur un autre serveur disponible. Comme mentionné précédemment, principalement redémarrer des ordinateurs virtuels Azure protège les machines virtuelles et pas les applications, dans ce cas hello (A) instance SCS. Via hello machine virtuelle redémarre nous contacterons indirectement « disponibilité » de l’instance SAP (A) SCS. tooinsure le démarrage automatique de l’instance de (A) SCS après le redémarrage de la machine virtuelle de hello, assurez-vous que tooset Autostart (paramètre) dans l’instance de (A) SCS démarrer profil décrite au chapitre [à l’aide du démarrage automatique pour les instances SAP][planning-guide-11.5]. Cela signifie hello (A) SCS l’instance comme un Point de défaillance unique (se) en cours d’exécution dans une seule machine virtuelle sera facteur déterminant de hello pour la disponibilité de l’ensemble du paysage SAP hello hello.

* *plus haute* disponibilité du serveur du SGBD (système de gestion de base de données)

Ici, instance de (A) SCS SAP similaire toohello cas d’utilisation, nous allons utiliser la machine virtuelle de Azure redémarre tooprotect hello machine virtuelle avec le logiciel de SGBD et nous disponibilité « supérieur » du logiciel SGBD par machine virtuelle redémarre.
SGBD en cours d’exécution dans une seule machine virtuelle est également un s’il est donc facteur déterminant de hello pour la disponibilité de l’ensemble du paysage SAP hello hello.

### <a name="sap-application-high-availability-on-azure-iaas"></a>Haute disponibilité de l’application SAP sur Azure IaaS
tooachieve complète SAP haute disponibilité du système, nous avons besoin de tous les composants SAP critiques système, des serveurs d’applications SAP redondants, par exemple, tooprotect et composants uniques (par exemple, Point de défaillance unique), comme instance de (A) SCS SAP et SGBD.

#### <a name="5d9d36f9-9058-435d-8367-5ad05f00de77"></a>Haute disponibilité pour les serveurs d’applications SAP
Pour les instances de serveurs/boîte de dialogue application hello SAP n’est pas nécessaire toothink sur une solution de haute disponibilité. La haute disponibilité peut être obtenue simplement par la redondance afin d’obtenir une présence suffisante dans les différentes machines virtuelles. Ils doivent tous être placés dans hello même tooavoid à haute disponibilité Azure qui hello des machines virtuelles peut-être être mises à jour hello même temps pendant le temps mort de maintenance planifiée. fonctionnalités de base Hello qui repose sur l’autre mise à niveau et domaines d’erreur au sein d’une unité d’échelle Azure a été déjà introduite dans le chapitre [mise à niveau des domaines][planning-guide-3.2.2]. Les groupes à haute disponibilité Azure ont été présentés dans le chapitre [Groupes à haute disponibilité Azure][planning-guide-3.2.3] dans ce document.

Le nombre de domaines de mise à niveau et d’erreur pouvant être utilisé par un groupe à haute disponibilité Azure au sein d’une unité d’échelle Azure est limité. Cela signifie que si un nombre d’ordinateurs virtuels dans un groupe à haute disponibilité plus tôt ou tard dans les faits hello qui finit par plusieurs machines virtuelles dans hello même erreur ou un domaine de mise à niveau

Déploiement de serveur d’applications SAP quelques instances de leurs ordinateurs virtuels dédiés et en supposant que nous avons obtenu des domaines de mise à niveau 5, hello illustration suivante aboutit au final de hello. Hello réel nombre maximal de domaines d’erreur et de mise à jour au sein d’un ensemble de disponibilité peut être modifiée de hello ultérieure :

![Haute disponibilité des serveurs d’applications SAP dans Azure][planning-guide-figure-3000]

Vous trouverez plus de détails dans cette documentation : <http://azure.microsoft.com/documentation/articles/virtual-machines-manage-availability>

#### <a name="high-availability-for-hello-sap-ascs-instance-on-windows"></a>Haute disponibilité pour l’instance de (A) SCS SAP hello sur Windows
Cluster de basculement Windows Server (WSFC) est une instance de (A) SCS SAP solution fréquemment utilisées tooprotect hello. Il est également intégré à sapinst sous forme d’une « installation à haute disponibilité ». À ce stade hello infrastructure Azure n’est pas en mesure de tooprovide hello fonctionnalité tooset des hello du Cluster de basculement Windows Server hello nécessaire comme cela est effectué localement.

À compter de janvier 2016 plateforme de cloud computing Azure hello exécutant le système d’exploitation de Windows hello ne fournit pas de possibilité de hello de l’utilisation d’un volume partagé de cluster sur un disque partagé entre les deux ordinateurs virtuels de Azure.

Cependant, une solution valide est l’utilisation de hello du logiciel 3 rd-party qui fournit un volume partagé par la réplication synchrone et transparent de disque qui peut être intégrée dans WSFC. Cette approche implique que seul nœud de cluster actif hello est en mesure de tooaccess un des disques de hello copie à un point dans le temps. À compter de janvier 2016 cette HA configuration est instance de (A) SCS SAP hello tooprotect pris en charge sur Windows système d’exploitation invité sur les machines virtuelles Azure en combinaison avec 3 rd-party logiciel SIOS DataKeeper.

Hello SIOS DataKeeper solution fournit un tooWindows de ressource de cluster de disque partagé des Clusters de basculement en ayant :

* Un disque dur virtuel de Azure supplémentaires attaché tooeach de hello machines () qui se trouvent dans une configuration de Cluster Windows
* SIOS DataKeeper Cluster Edition s’exécutant sur les deux nœuds de machine virtuelle
* Avoir SIOS DataKeeper Cluster Edition est configuré de sorte qu’il reflète synchrone contenu hello Hello supplémentaires disque dur virtuel attaché volume à partir du volume de disque dur virtuel attaché tooadditional source machines virtuelles de cible de machine virtuelle.
* SIOS DataKeeper est en faisant abstraction des volumes locaux hello source et cible et les présenter tooWindows Cluster de basculement en tant qu’un seul disque partagé.

Vous trouverez tous les détails sur la façon de tooinstall un Cluster de basculement Windows avec SIOS Datakeeper et SAP Bonjour [Clustering d’Instance ASC SAP à l’aide de Cluster de basculement Windows Server sur Azure avec SIOS DataKeeper] [ ha-guide-classic]livre blanc.

#### <a name="high-availability-for-hello-sap-ascs-instance-on-linux"></a>Haute disponibilité pour l’instance de (A) SCS SAP hello sur Linux
Depuis décembre 2015 n’a également aucun disque équivalent tooshared WSFC pour les machines virtuelles Linux sur Azure. Les autres solutions consistant à utiliser un logiciel tiers, tel que SISO pour Windows, ne sont pas encore validée pour l’exécution de SAP sous Linux sur Azure.

#### <a name="high-availability-for-hello-sap-database-instance"></a>Haute disponibilité pour l’instance de base de données SAP hello
Hello SAP à haute disponibilité SGBD installation par défaut est basée sur deux machines virtuelles de SGBD où les fonctionnalités de haute disponibilité SGBD sont utilisée tooreplicate des données à partir de toohello instance SGBD active de hello deuxième machine virtuelle dans une instance SGBD passive.

Haute fonctionnalité de récupération d’urgence et disponibilité pour les SGBD en général ainsi que des SGBD sont décrits dans hello [Guide de déploiement de système SGBD][dbms-guide].

#### <a name="end-to-end-high-availability-for-hello-complete-sap-system"></a>Haute disponibilité de bout en bout pour hello complète du système SAP
Voici deux exemples d’architecture de haute disponibilité SAP NetWeaver complète dans Azure (un concernant Windows et un autre pour Linux).
concepts de Hello comme expliqué ci-dessous peut-être toobe compromis un peu lorsque vous déployez de nombreux systèmes SAP et nombre hello d’ordinateurs virtuels déployés est limite hello maximal de comptes de stockage par abonnement. Dans ce cas, disques durs virtuels de machines virtuelles doivent toobe combinée au sein d’un compte de stockage. En général, vous pourriez procéder ainsi en combinant les disques virtuels des machines virtuelles de la couche d’application SAP de différents systèmes SAP.  Nous avons également associé différents disques durs virtuels de plusieurs machines virtuelles de SGBD (système de gestion de base de données) de différents systèmes SAP dans un compte Azure Storage. En gardant les limites d’IOPS hello de comptes de stockage Azure à l’esprit ( <https://azure.microsoft.com/documentation/articles/storage-scalability-targets> )

##### <a name="windowslogowindows-ha-on-windows"></a>![Windows][Logo_Windows] Haute disponibilité sous Windows
![Architecture de haute disponibilité de l’application SAP NetWeaver avec SQL Server dans Azure IaaS][planning-guide-figure-3200]

Hello suivant constructions Azure est utilisé pour le système SAP NetWeaver de hello, impact toominimize par des problèmes d’infrastructure et l’ordinateur hôte de la mise à jour corrective :

* système complet de Hello est déployé sur Azure (obligatoire, la couche SGBD, (A) SCS instance et toorun de nécessité de couche application complète dans hello même emplacement).
* système complet de Hello s’exécute dans un abonnement Azure (obligatoire).
* système complet de Hello s’exécute au sein d’un réseau virtuel Azure (obligatoire).
* séparation Hello Hello machines virtuelles d’un système SAP en trois ensembles de disponibilité est possible même avec toutes les machines virtuelles de hello appartenant toohello même réseau virtuel.
* Toutes les machines virtuelles exécutant des instances de SGBD (système de gestion de base de données) d’un système SAP se trouvent dans un groupe à haute disponibilité. Nous partons du principe qu’il existe plusieurs machines virtuelles exécutant des instances de SGBD (système de gestion de base de données) par système depuis l’utilisation des fonctionnalités de haute disponibilité de SGBD natives, telles que SQL Server AlwaysOn ou Oracle Data Guard.
* Toutes les machines virtuelles exécutant des instances de SGBD (système de gestion de base de données) utilisent leur propre compte de stockage. Les fichiers journaux et de données SGBD sont répliquées à partir d’un stockage compte tooanother compte de stockage à l’aide des fonctions de haute disponibilité SGBD qui synchronisent les données de hello. Indisponibilité d’un compte de stockage entraîne l’indisponibilité d’un nœud de cluster Windows SQL, mais pas hello SQL Server service entier.
* Toutes les machines virtuelles exécutant l’instance (A)SCS d’un système SAP se trouvent dans un groupe à haute disponibilité. À l’intérieur de ces ordinateurs virtuels est configurer l’instance de Cluster de basculement du serveur Windows (WSFC) tooprotect (A) SCS.
* Toutes les machines virtuelles exécutant des instances (A)SCS utilisent leur propre compte de stockage. (A) Fichiers d’instance SCS et dossier global de SAP sont répliquées à partir d’un stockage compte tooanother compte de stockage à l’aide de la réplication de SIOS DataKeeper. Indisponibilité d’un compte de stockage entraîne l’indisponibilité de l’un (A) SCS Windows nœud de cluster, mais pas hello ensemble (A) service SCS.
* Tous les ordinateurs virtuels de hello représentant la couche de server application hello SAP sont dans un troisième groupe à haute disponibilité.
* Tous les ordinateurs virtuels de hello exécutant des serveurs d’applications SAP utilisent leur propre compte de stockage. Indisponibilité d’un compte de stockage entraîne l’indisponibilité d’un serveur d’applications SAP, où les autres comme SAP continuer toorun.

##### <a name="linuxlogolinux-ha-on-linux"></a>![Linux][Logo_Linux] Haute disponibilité sous Linux
Hello architecture de haute disponibilité SAP sur Linux sur Azure est fondamentalement hello même que pour Windows comme décrit ci-dessus. Depuis janvier 2016, il existe cependant deux restrictions :

* Seuls 16 ASE SAP sont actuellement pris en charge sous Linux sur Azure sans aucune fonctionnalité de réplication ASE.
* Il n’existe encore aucune solution de haute disponibilité (A)SCS SAP prise en charge sous Linux sur Azure.

En conséquence de janvier 2016 ne proposent pas un système SAP-Linux-Azure hello du même groupe de disponibilité comme un système SAP-Windows-Azure car il manque à haute disponibilité pour l’instance de hello (A) SCS et hello de base de données SAP ASE à instance unique.

### <a name="4e165b58-74ca-474f-a7f4-5e695a93204f"></a>Utilisation du démarrage automatique pour les instances SAP
SAP proposé des fonctionnalités hello des instances SAP toostart immédiatement après le démarrage hello Hello du système d’exploitation dans hello machine virtuelle. les étapes exactes Hello documentés dans l’Article de Base de connaissances SAP [1909114] - comment toostart SAP instances automatiquement à l’aide du paramètre de démarrage automatique. Toutefois, SAP ne recommande pas toouse hello paramètre, car le contrôle n’existe pas dans l’ordre de hello de redémarrages d’instance, en supposant que plusieurs machines virtuelles ont été affectées ou exécution de plusieurs instances par ordinateur virtuel. Un scénario classique Azure d’une instance de serveur d’application SAP dans un cas de machine virtuelle et hello d’une seule machine virtuelle finalement redémarré la mise en route, hello Autostart n’est pas réellement critique et peut être activée en ajoutant ce paramètre :

    Autostart = 1

Dans hello démarrer le profil de l’instance SAP ABAP ou Java de hello.

> [!NOTE]
> Autostart (paramètre) Hello peut avoir également des inconvénients. Plus en détail, les déclencheurs de paramètre hello hello début d’une instance SAP ABAP ou Java lorsque hello associées service Windows/Linux de l’instance de hello est démarré. Qui est certainement des cas de hello au démarrage de systèmes d’exploitation de hello. Toutefois, les redémarrages des services SAP sont également courants pour la fonctionnalité de gestion du cycle de vie du logiciel SAP, telle que SUM ou d’autres mises à jour et mises à niveau. Ces fonctionnalités n’attendez un toobe instance redémarrée automatiquement à tous. Par conséquent, Autostart (paramètre) hello doit être désactivée avant d’exécuter ces tâches. également, Hello Autostart paramètre ne doit pas être utilisé pour les instances SAP qui sont en cluster, tels que ASCS/SCS / l’élément de configuration.
>
>

Consultez les informations supplémentaires concernant le démarrage automatique des instances SAP ici :

* [Start/Stop SAP along with your Unix Server Start/Stop (Démarrage/Arrêt de SAP à l’aide de la fonctionnalité correspondante de votre serveur Unix)](http://scn.sap.com/community/unix/blog/2012/08/07/startstop-sap-along-with-your-unix-server-startstop)
* [Starting and Stopping SAP NetWeaver Management Agents (Démarrage et arrêt des agents de gestion SAP NetWeaver)](https://help.sap.com/saphelp_nwpi711/helpdata/en/49/9a15525b20423ee10000000a421938/content.htm)
* [Comment tooenable automatiquement démarrer de base de données HANA](http://www.freehanatutorials.com/2012/10/how-to-enable-auto-start-of-hana.html)

### <a name="larger-3-tier-sap-systems"></a>Systèmes SAP à 3 couches plus vastes
Les aspects relatifs à la haute disponibilité des configurations SAP à 3 couches ont déjà été abordés dans les sections précédentes. Mais qu’en est-il des systèmes où la configuration requise du serveur hello SGBD est trop grandes toohave situé dans Azure, mais la couche d’application hello SAP peut être déployé dans Azure ?

#### <a name="location-of-3-tier-sap-configurations"></a>Emplacement des configurations SAP à 3 couches
Il n’est pas pris en charge toosplit hello lui-même ou application hello couche application et SGBD entre locaux et Azure. Un système SAP est totalement déployé localement OU dans Azure. Il n’est pas également toohave pris en charge certains des serveurs d’applications hello exécutent localement et autres dans Azure. Qui est hello point de départ d’une discussion de hello. Aussi, nous ne prennent pas en charge des composants de SGBD hello toohave d’un système SAP et hello de niveau serveur d’application SAP déployé dans des régions Azure différents. Par exemple, le SGBD (système de gestion de base de données) ( à l’ouest des États-Unis et la couche d’application SAP au centre des États-Unis. Ne prend ne pas en charge des configurations de fait la sensibilité de latence hello Hello architecture de SAP NetWeaver.

Cependant, au fil de hello de données de l’année dernière partenaires center développement des emplacements tooAzure régions. Ces emplacements de collaboration sont souvent de proximité toohello Azure de données physiques centres d’une région Azure. distance de courte Hello et connexion des ressources dans la colocalisation de hello via ExpressRoute dans Azure peuvent entraîner une latence est inférieure à 2 ms. Dans ce cas, toolocate hello couche SGBD (y compris le stockage SAN/NAS) dans un tel colocalisation et couche d’application hello SAP dans Azure est possible. Depuis décembre 2015, nous n’assistons à aucun déploiement de ce type. Toutefois, divers clients effectuant des déploiements d’applications autres que SAP utilisent déjà de telles approches.

### <a name="offline-backup-of-sap-systems"></a>Sauvegarde hors connexion de systèmes SAP
Dépend de hello configuration SAP choisie (2 ou 3 niveaux) d’il peut être un toobackup nécessaire. contenu Hello de machine virtuelle proprement dite de hello plus toohave une sauvegarde de base de données hello. Hello SGBD associés sauvegardes sont attendu toobe terminé avec des méthodes de base de données. Vous trouverez une description détaillée de hello différentes bases de données, dans [SGBD Guide][dbms-guide]. Sur hello autre part, hello données SAP peut être sauvegardé de manière hors connexion (y compris le contenu de base de données hello ainsi) comme décrit dans cette section ou en ligne comme décrit dans la section suivante de hello.

sauvegarde hors connexion de Hello fondamentalement nécessite un arrêt de hello machine virtuelle via hello portail Azure et une copie du disque de machine virtuelle base hello ainsi que tous les attaché toohello de disques durs virtuels de machine virtuelle. Cela préserve un point d’image dans le temps de hello machine virtuelle et de son disque associé. Il est recommandé de toocopy hello « sauvegardes » dans un autre compte de stockage Azure. Par conséquent, hello procédure décrite dans le chapitre [copie de disques entre les comptes de stockage Azure] [ planning-guide-5.4.2] de ce document s’appliquent.
Outre hello à l’aide de l’arrêt hello portail Azure un peut également le faire via Powershell ou CLI comme décrit ici : <https://azure.microsoft.com/documentation/articles/virtual-machines-deploy-rmtemplates-powershell/>

Une restauration de cet état se compose de la suppression de hello machine virtuelle de base, ainsi que les disques d’origine hello Hello machine virtuelle de base et disques durs virtuels montés, copie toohello de disques durs virtuels hello précédent enregistré compte de stockage d’origine, puis le redéployer hello système.
Cet article montre comment tooscript ce processus dans Powershell : <http://www.westerndevs.com/azure-snapshots/>

Assurez-vous que tooinstall une nouvelle licence SAP depuis restoing une sauvegarde de la machine virtuelle comme décrit ci-dessus crée une clé matérielle.

### <a name="online-backup-of-an-sap-system"></a>Sauvegarde en ligne d’un système SAP
Sauvegarde de hello SGBD est exécutée avec des méthodes spécifiques SGBD comme décrit dans hello [SGBD Guide][dbms-guide].

Autres ordinateurs virtuels au sein de hello système SAP peuvent être sauvegardées à l’aide de la fonctionnalité de sauvegarde des machines virtuelles Azure. Sauvegarde des machines virtuelles Azure introduite au début de 2015 et pendant ce temps est une méthode standard de toobackup un VM complète dans Azure. Sauvegarde Azure stocke les sauvegardes de hello dans Azure et permet une restauration d’une machine virtuelle.

> [!NOTE]
> À compter de décembre 2015 à l’aide de la sauvegarde de la machine virtuelle ne conserve pas de hello unique ID de machine virtuelle qui est utilisé pour SAP Gestionnaire de licences. Cela signifie qu’une restauration à partir d’une sauvegarde de la machine virtuelle nécessite l’installation d’une nouvelle clé de licence SAP que hello restauré l’ordinateur virtuel est considéré comme toobe un nouvel ordinateur virtuel et non pas le remplacement de l’ancien a été enregistré.
> Depuis janvier 2016, la sauvegarde de machine virtuelle Azure ne prend pas encore en charge les machines virtuelles déployées avec Azure Resource Manager.
>
> ![Windows][Logo_Windows] Windows
>
> En théorie machines virtuelles que l’exécution des bases de données peuvent être sauvegardées de façon cohérente si prend en charge des systèmes de SGBD hello hello Windows VSS (Volume Shadow Copy Service <https://msdn.microsoft.com/library/windows/desktop/bb968832 (v=vs.85).aspx > ) comme par exemple, SQL Server.
> Toutefois, n’oubliez pas qu’une restauration dans le temps des bases de données peut ne pas être possible, selon les sauvegardes de machine virtuelle Azure. Par conséquent, il est recommandé tooperform des sauvegardes de bases de données avec des fonctionnalités SGBD au lieu de compter sur la sauvegarde de machine virtuelle Azure
>
> tooget familiarisé avec la sauvegarde des machines virtuelles Azure Démarrez ici : <https://azure.microsoft.com/documentation/articles/backup-azure-vms/>.
>
> Autres possibilités sont toouse une combinaison de Microsoft Data Protection Manager est installé dans une machine virtuelle Azure et Azure Backup pour la sauvegarde/restauration de bases de données. Pour plus d’informations, consultez : <https://azure.microsoft.com/documentation/articles/backup-azure-dpm-introduction/>.  
>
> ![Linux][Logo_Linux] Linux
>
> Il n’existe aucun équivalent tooWindows VSS dans Linux. Par conséquent, seules les sauvegardes cohérentes au niveau des fichiers sont possibles. Les sauvegardes cohérentes au niveau de l’application ne sont pas prises en charge. Hello SGBD SAP sauvegarde doit être effectuée à l’aide des fonctionnalités SGBD. Hello fichier incluant hello SAP liées au système données peuvent être enregistrées, par exemple, à l’aide de tar comme décrit ici : <http://help.sap.com/saphelp_nw70ehp2/helpdata/en/d3/c0da3ccbb04d35b186041ba6ac301f/content.htm>
>
>

### <a name="azure-as-dr-site-for-production-sap-landscapes"></a>Azure comme site de récupération d’urgence pour les paysages SAP de production
Depuis 2014 Mid, composants de toovarious extensions autour de Hyper-V, System Center et Azure ctiver hello de Azure en tant que site de récupération d’urgence pour les machines virtuelles en cours d’exécution local basé sur Hyper-V.

Blog de détaillant comment toodeploy cette solution est documenté ici : <http://blogs.msdn.com/b/saponsqlserver/archive/2014/11/19/protecting-sap-solutions-with-azure-site-recovery.aspx>

## <a name="summary"></a>Résumé
Hello des points clés de la haute disponibilité pour les systèmes SAP dans Azure sont :

* À ce stade, hello point de défaillance unique de SAP ne peut pas être sécurisé exactement hello même façon qu’il peut être effectué dans des déploiements sur site. Hello parce que les clusters de disque partagé ne peut pas encore générés dans Azure sans utiliser hello 3e logiciels tiers.
* Pour la couche de SGBD hello, vous avez besoin de fonctionnalités SGBD toouse qui ne reposent pas sur la technologie de cluster de disque partagé. Détails sont documentés dans hello [SGBD Guide][dbms-guide].
* impact de hello toominimize des problèmes dans les domaines d’erreur Bonjour Azure maintenance d’infrastructure ou un hôte, vous devez utiliser des groupes à haute disponibilité Azure :
  * Il est recommandé de toohave une haute disponibilité pour la couche d’application SAP hello.
  * Il est recommandé de toohave une disponibilité distinct définie pour la couche SGBD SAP de hello.
  * Il n’est pas recommandé hello tooapply à haute disponibilité même pour les machines virtuelles de différents systèmes SAP.
* Pour des raisons de sauvegarde de la couche SGBD SAP de hello, vérifiez hello [SGBD Guide][dbms-guide].
* Sauvegarde des instances de la boîte de dialogue SAP judicieux peu puisqu’il s’agit d’instances de boîte de dialogue simple tooredeploy généralement plus rapides.
* Hello machine virtuelle qui contient le répertoire global de hello Hello système SAP et il sauvegarde de tous les profils hello des instances différentes de hello, se justifie et doit être effectuée avec la sauvegarde Windows ou par exemple tar sur Linux. Dans la mesure où il existe des différences entre Windows Server 2008 (R2) et Windows Server 2012 (R2), ce qui rend plus facile toobackup hello plus récente à l’aide de mises à jour de Windows Server, nous vous recommandons de toorun Windows Server 2012 (R2) en tant que système de d’exploitation invité de Windows.
