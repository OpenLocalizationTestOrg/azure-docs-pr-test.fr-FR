---
title: aaaGetting main SAP sur des machines virtuelles Azure | Documents Microsoft
description: "Découvrez les solutions SAP qui s’exécutent sur des machines virtuelles Windows dans Microsoft Azure"
services: virtual-machines-linux
documentationcenter: 
author: RicksterCDN
manager: timlt
editor: 
tags: azure-resource-manager
keywords: 
ms.assetid: ad8e5c75-0cf6-4564-ae62-ea1246b4e5f2
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 03/29/2017
ms.author: rclaus
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 0ac390f8e1c802505b8f9304a12868364fa60f80
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="using-azure-for-hosting-and-running-sap-workload-scenarios"></a>Utilisation d’Azure pour l’hébergement et l’exécution de scénarios de charge de travail SAP
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

[azure-cli]:../../../cli-install-nodejs.md
[azure-portal]:https://portal.azure.com
[azure-ps]:/powershell/azureps-cmdlets-docs
[azure-quickstart-templates-github]:https://github.com/Azure/azure-quickstart-templates
[azure-script-ps]:https://go.microsoft.com/fwlink/p/?LinkID=395017
[azure-subscription-service-limits]:../../../azure-subscription-service-limits.md
[azure-subscription-service-limits-subscription]:../../../azure-subscription-service-limits.md#subscription

[dbms-guide]:dbms-guide.md 
[dbms-guide-2.1]:dbms-guide.md#c7abf1f0-c927-4a7c-9c1d-c7b5b3b7212f 
[dbms-guide-2.2]:dbms-guide.md#c8e566f9-21b7-4457-9f7f-126036971a91 
[dbms-guide-2.3]:dbms-guide.md#10b041ef-c177-498a-93ed-44b3441ab152 
[dbms-guide-2]:dbms-guide.md#65fa79d6-a85f-47ee-890b-22e794f51a64 
[dbms-guide-3]:dbms-guide.md#871dfc27-e509-4222-9370-ab1de77021c3 
[dbms-guide-5.5.1]:dbms-guide.md#0fef0e79-d3fe-4ae2-85af-73666a6f7268 
[dbms-guide-5.5.2]:dbms-guide.md#f9071eff-9d72-4f47-9da4-1852d782087b
[dbms-guide-5.6]:dbms-guide.md#1b353e38-21b3-4310-aeb6-a77e7c8e81c8 
[dbms-guide-5.8]:dbms-guide.md#9053f720-6f3b-4483-904d-15dc54141e30 
[dbms-guide-5]:dbms-guide.md#3264829e-075e-4d25-966e-a49dad878737 
[dbms-guide-8.4.1]:dbms-guide.md#b48cfe3b-48e9-4f5b-a783-1d29155bd573 
[dbms-guide-8.4.2]:dbms-guide.md#23c78d3b-ca5a-4e72-8a24-645d141a3f5d 
[dbms-guide-8.4.3]:dbms-guide.md#77cd2fbb-307e-4cbf-a65f-745553f72d2c 
[dbms-guide-8.4.4]:dbms-guide.md#f77c1436-9ad8-44fb-a331-8671342de818 
[dbms-guide-900-sap-cache-server-on-premises]:dbms-guide.md#642f746c-e4d4-489d-bf63-73e80177a0a8

[dbms-guide-figure-100]:media/virtual-machines-shared-sap-dbms-guide/100_storage_account_types.png
[dbms-guide-figure-200]:media/virtual-machines-shared-sap-dbms-guide/200-ha-set-for-dbms-ha.png
[dbms-guide-figure-300]:media/virtual-machines-shared-sap-dbms-guide/300-reference-config-iaas.png
[dbms-guide-figure-400]:media/virtual-machines-shared-sap-dbms-guide/400-sql-2012-backup-to-blob-storage.png
[dbms-guide-figure-500]:media/virtual-machines-shared-sap-dbms-guide/500-sql-2012-backup-to-blob-storage-different-containers.png
[dbms-guide-figure-600]:media/virtual-machines-shared-sap-dbms-guide/600-iaas-maxdb.png
[dbms-guide-figure-700]:media/virtual-machines-shared-sap-dbms-guide/700-livecach-prod.png
[dbms-guide-figure-800]:media/virtual-machines-shared-sap-dbms-guide/800-azure-vm-sap-content-server.png
[dbms-guide-figure-900]:media/virtual-machines-shared-sap-dbms-guide/900-sap-cache-server-on-premises.png

[deployment-guide]:deployment-guide.md 
[deployment-guide-2.2]:deployment-guide.md#42ee2bdb-1efc-4ec7-ab31-fe4c22769b94 
[deployment-guide-3.1.2]:deployment-guide.md#3688666f-281f-425b-a312-a77e7db2dfab 
[deployment-guide-3.2]:deployment-guide.md#db477013-9060-4602-9ad4-b0316f8bb281 
[deployment-guide-3.3]:deployment-guide.md#54a1fc6d-24fd-4feb-9c57-ac588a55dff2 
[deployment-guide-3.4]:deployment-guide.md#a9a60133-a763-4de8-8986-ac0fa33aa8c1
[deployment-guide-3]:deployment-guide.md#b3253ee3-d63b-4d74-a49b-185e76c4088e 
[deployment-guide-4.1]:deployment-guide.md#604bcec2-8b6e-48d2-a944-61b0f5dee2f7 
[deployment-guide-4.2]:deployment-guide.md#7ccf6c3e-97ae-4a7a-9c75-e82c37beb18e 
[deployment-guide-4.3]:deployment-guide.md#31d9ecd6-b136-4c73-b61e-da4a29bbc9cc 
[deployment-guide-4.4.2]:deployment-guide.md#6889ff12-eaaf-4f3c-97e1-7c9edc7f7542 
[deployment-guide-4.4]:deployment-guide.md#c7cbb0dc-52a4-49db-8e03-83e7edc2927d 
[deployment-guide-4.5.1]:deployment-guide.md#987cf279-d713-4b4c-8143-6b11589bb9d4 
[deployment-guide-4.5.2]:deployment-guide.md#408f3779-f422-4413-82f8-c57a23b4fc2f 
[deployment-guide-4.5]:deployment-guide.md#d98edcd3-f2a1-49f7-b26a-07448ceb60ca 
[deployment-guide-5.1]:deployment-guide.md#bb61ce92-8c5c-461f-8c53-39f5e5ed91f2
[deployment-guide-5.2]:deployment-guide.md#e2d592ff-b4ea-4a53-a91a-e5521edb6cd1 
[deployment-guide-5.3]:deployment-guide.md#fe25a7da-4e4e-4388-8907-8abc2d33cfd8 
[deployment-guide-configure-monitoring-scenario-1]:deployment-guide.md#ec323ac3-1de9-4c3a-b770-4ff701def65b 
[deployment-guide-configure-proxy]:deployment-guide.md#baccae00-6f79-4307-ade4-40292ce4e02d 
[deployment-guide-figure-100]:media/virtual-machines-shared-sap-deployment-guide/100-deploy-vm-image.png
[deployment-guide-figure-1000]:media/virtual-machines-shared-sap-deployment-guide/1000-service-properties.png
[deployment-guide-figure-11]:deployment-guide.md#figure-11
[deployment-guide-figure-1100]:media/virtual-machines-shared-sap-deployment-guide/1100-azperflib.png
[deployment-guide-figure-1200]:media/virtual-machines-shared-sap-deployment-guide/1200-cmd-test-login.png
[deployment-guide-figure-1300]:media/virtual-machines-shared-sap-deployment-guide/1300-cmd-test-executed.png
[deployment-guide-figure-14]:deployment-guide.md#figure-14
[deployment-guide-figure-1400]:media/virtual-machines-shared-sap-deployment-guide/1400-azperflib-error-servicenotstarted.png
[deployment-guide-figure-300]:media/virtual-machines-shared-sap-deployment-guide/300-deploy-private-image.png
[deployment-guide-figure-400]:media/virtual-machines-shared-sap-deployment-guide/400-deploy-using-disk.png
[deployment-guide-figure-5]:deployment-guide.md#figure-5
[deployment-guide-figure-50]:media/virtual-machines-shared-sap-deployment-guide/50-forced-tunneling-suse.png
[deployment-guide-figure-500]:media/virtual-machines-shared-sap-deployment-guide/500-install-powershell.png
[deployment-guide-figure-6]:deployment-guide.md#figure-6
[deployment-guide-figure-600]:media/virtual-machines-shared-sap-deployment-guide/600-powershell-version.png
[deployment-guide-figure-7]:deployment-guide.md#figure-7
[deployment-guide-figure-700]:media/virtual-machines-shared-sap-deployment-guide/700-install-powershell-installed.png
[deployment-guide-figure-760]:media/virtual-machines-shared-sap-deployment-guide/760-azure-cli-version.png
[deployment-guide-figure-900]:media/virtual-machines-shared-sap-deployment-guide/900-cmd-update-executed.png
[deployment-guide-figure-azure-cli-installed]:deployment-guide.md#402488e5-f9bb-4b29-8063-1c5f52a892d0
[deployment-guide-figure-azure-cli-version]:deployment-guide.md#0ad010e6-f9b5-4c21-9c09-bb2e5efb3fda
[deployment-guide-install-vm-agent-windows]:deployment-guide.md#b2db5c9a-a076-42c6-9835-16945868e866
[deployment-guide-troubleshooting-chapter]:deployment-guide.md#564adb4f-5c95-4041-9616-6635e83a810b 
[deploy-template-cli]:../../../resource-group-template-deploy.md
[deploy-template-portal]:../../../resource-group-template-deploy.md
[deploy-template-powershell]:../../../resource-group-template-deploy.md

[dr-guide-classic]:http://go.microsoft.com/fwlink/?LinkID=521971

[getting-started]:get-started.md
[getting-started-dbms]:get-started.md#1343ffe1-8021-4ce6-a08d-3a1553a4db82
[getting-started-deployment]:get-started.md#6aadadd2-76b5-46d8-8713-e8d63630e955
[getting-started-planning]:get-started.md#3da0389e-708b-4e82-b2a2-e92f132df89c


[ha-guide-classic]:http://go.microsoft.com/fwlink/?LinkId=613056
[ha-guide]:sap-high-availability-guide.md

[install-extension-cli]:virtual-machines-linux-enable-aem.md

[Logo_Linux]:media/virtual-machines-shared-sap-shared/Linux.png
[Logo_Windows]:media/virtual-machines-shared-sap-shared/Windows.png

[msdn-set-azurermvmaemextension]:https://msdn.microsoft.com/library/azure/mt670598.aspx

[planning-guide]:planning-guide.md 
[planning-guide-1.2]:planning-guide.md#e55d1e22-c2c8-460b-9897-64622a34fdff 
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

[powershell-install-configure]:https://docs.microsoft.com/powershell/azure/install-azurerm-ps
[resource-group-authoring-templates]:../../../resource-group-authoring-templates.md
[resource-group-overview]:../../../azure-resource-manager/resource-group-overview.md
[resource-groups-networking]:../../../virtual-network/resource-groups-networking.md
[sap-pam]:https://support.sap.com/pam (SAP Product Availability Matrix)
[sap-templates-2-tier-marketplace-image]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-2-tier-marketplace-image%2Fazuredeploy.json
[sap-templates-2-tier-os-disk]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-2-tier-user-disk%2Fazuredeploy.json
[sap-templates-2-tier-user-image]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-2-tier-user-image%2Fazuredeploy.json
[sap-templates-3-tier-marketplace-image]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image%2Fazuredeploy.json
[sap-templates-3-tier-user-image]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-user-image%2Fazuredeploy.json
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
[virtual-machines-azure-resource-manager-architecture]:../../../resource-manager-deployment-model.md
[virtual-machines-azurerm-versus-azuresm]:virtual-machines-linux-compare-deployment-models.md
[virtual-machines-windows-classic-configure-oracle-data-guard]:../../virtual-machines-windows-classic-configure-oracle-data-guard.md
[virtual-machines-linux-cli-deploy-templates]:../../linux/cli-deploy-templates.md 
[virtual-machines-deploy-rmtemplates-powershell]:../../virtual-machines-windows-ps-manage.md 
[virtual-machines-linux-agent-user-guide]:../../linux/agent-user-guide.md
[virtual-machines-linux-agent-user-guide-command-line-options]:../../linux/agent-user-guide.md#command-line-options
[virtual-machines-linux-capture-image]:../../linux/capture-image.md
[virtual-machines-linux-capture-image-resource-manager]:../../linux/capture-image.md
[virtual-machines-linux-capture-image-resource-manager-capture]:../../linux/capture-image.md#capture-the-vm
[virtual-machines-linux-configure-raid]:../../linux/configure-raid.md
[virtual-machines-linux-configure-lvm]:../../linux/configure-lvm.md
[virtual-machines-linux-classic-create-upload-vhd-step-1]:../../virtual-machines-linux-classic-create-upload-vhd.md#step-1-prepare-the-image-to-be-uploaded
[virtual-machines-linux-create-upload-vhd-suse]:../../linux/suse-create-upload-vhd.md
[virtual-machines-linux-redhat-create-upload-vhd]:../../linux/redhat-create-upload-vhd.md
[virtual-machines-linux-how-to-attach-disk]:../../linux/add-disk.md
[virtual-machines-linux-how-to-attach-disk-how-to-initialize-a-new-data-disk-in-linux]:../../linux/add-disk.md#connect-to-the-linux-vm-to-mount-the-new-disk
[virtual-machines-linux-tutorial]:../../linux/quick-create-cli.md
[virtual-machines-linux-update-agent]:../../linux/update-agent.md
[virtual-machines-manage-availability]:../../linux/manage-availability.md
[virtual-machines-ps-create-preconfigure-windows-resource-manager-vms]:virtual-machines-windows-create-powershell.md
[virtual-machines-sizes]:../../linux/sizes.md
[virtual-machines-windows-classic-ps-sql-alwayson-availability-groups]:./../../windows/sqlclassic/virtual-machines-windows-classic-ps-sql-alwayson-availability-groups.md
[virtual-machines-windows-classic-ps-sql-int-listener]:./../../windows/sqlclassic/virtual-machines-windows-classic-ps-sql-int-listener.md
[virtual-machines-sql-server-high-availability-and-disaster-recovery-solutions]:./../../windows/sql/virtual-machines-windows-sql-high-availability-dr.md
[virtual-machines-sql-server-infrastructure-services]:./../../windows/sql/virtual-machines-windows-sql-server-iaas-overview.md
[virtual-machines-sql-server-performance-best-practices]:./../../windows/sql/virtual-machines-windows-sql-performance.md
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
[vpn-gateway-site-to-site-create]:../../../vpn-gateway/vpn-gateway-site-to-site-create.md
[vpn-gateway-vpn-faq]:../../../vpn-gateway/vpn-gateway-vpn-faq.md
[xplat-cli]:../../../cli-install-nodejs.md
[xplat-cli-azure-resource-manager]:../../../xplat-cli-azure-resource-manager.md

En choisissant Microsoft Azure comme partenaire cloud prêt SAP, vous êtes en mesure de tooreliably exécuter vos scénarios et SAP charges de travail critiques sur une plateforme évolutive, conforme et éprouvée en entreprise.  Obtenir l’évolutivité hello, flexibilité et d’économies d’Azure. Avec hello développé le partenariat entre Microsoft et SAP, vous pouvez exécuter des applications SAP sur les scénarios de développement et de test et de production dans Azure - et entièrement pris en charge. À partir de SAP NetWeaver tooSAP S4/HANA SAP BI, Linux tooWindows, tooSQL de SAP HANA, nous qu’il vous faut. 

En plus de l’hébergement des scénarios SAP NetWeaver avec hello autre SGBD sur Azure, vous pouvez héberger différents autres scénarios de charge de travail SAP, comme SAP BI dans Azure. Vous trouverez la documentation concernant les déploiements SAP NetWeaver sur Azure Virtual Machines native de section de hello « SAP NetWeaver sur Machines virtuelles Azure ». 

Azure a native offre de Machine virtuelle Azure qui est en constante augmentation de taille de l’UC et mémoire ressources toocover SAP la charge de travail qui s’appuie sur SAP HANA. Pour plus d’informations sur cette rubrique, rechercher des documents hello section hello SAP HANA sur des Machines virtuelles Azure. »

l’unicité de Hello de Azure pour SAP HANA est une offre unique qui définit Azure en dehors de la concurrence. Dans tooenable commande héberge plus de mémoire et de ressources de processeur SAP exigeantes scénarios impliquant des SAP HANA, Azure propose l’utilisation de hello du client dédié un matériel nu à des fins de hello de l’exécution des déploiements SAP HANA qui nécessitent des too20 to (montée en puissance de 60 To) de mémoire S/4HANA ou d’autres charges de travail SAP HANA. Cette solution Azure unique de HANA SAP sur Azure (Instances de grande taille) vous permet de toorun SAP HANA sur du matériel de système nu hello dédié avec hello SAP application couche ou de la charge de travail intermédiaires hébergé dans native Azure Virtual Machines. Cette solution est documentée dans plusieurs documents dans la section de hello « SAP HANA sur Azure (Instances de grande taille) ».   

Scénarios de charge de travail SAP dans Azure d’hébergement peuvent également créer des spécifications d’intégration d’identité et à authentification unique à l’aide de composants de Azure Active Directory toodifferent SAP et SAP SaaS ou PaaS offre. Une liste d’intégration et de ces scénarios authentification avec Azure Active Directory (AAD) et SAP entités est décrite et documentée dans la section de hello « intégration d’identité AAD SAP et Single-Sign-On. »


## <a name="sap-hana-on-sap-hana-on-azure-large-instances"></a>SAP HANA sur SAP HANA sur Azure (grandes instances)

### <a name="overview-and-architecture-of-sap-hana-on-azure-large-instances"></a>Présentation et architecture de SAP HANA sur Azure (grandes instances)
titre : aaaOverview et Architecture de HANA SAP sur Azure (Instances de grande taille)

Résumé : Cette Architecture et le Guide de déploiement technique fournit toohelp informations déployer de SAP sur hello nouvelle HANA SAP sur Azure (Instances de grande taille) dans Azure. Il n’est pas prévue toobe un guide complet couverture spécifique le programme d’installation de solutions SAP, mais des informations utiles au lieu de cela dans votre déploiement initial et les opérations en cours. Il ne doit pas remplacer documentation SAP liés installation toohello de SAP HANA (ou hello nombreuses Notes de prise en charge SAP qui couvrent les rubrique hello). Il vous donne une vue d’ensemble et fournit des détails supplémentaires hello d’installation de SAP HANA sur Azure (Instances de grande taille).

Mise à jour : juillet 2017

[Ce guide est disponible ici](hana-overview-architecture.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

### <a name="infrastructure-and-connectivity-toosap-hana-on-azure-large-instances"></a>Et la connectivité tooSAP HANA sur Azure (Instances de grande taille)
titre : aaaInfrastructure et connectivité tooSAP HANA sur Azure (Instances de grande taille)

Résumé : Après que l’achat de hello de HANA SAP sur Azure (Instances de grande taille) est finalisé entre vous et hello équipe des comptes Microsoft enterprise, diverses configurations de réseau sont requises dans une connectivité de commande tooensure.  Ces informations de hello de plans de document ayant toobe partagé avec hello informations suivantes sont requises. Ce document décrit les informations qui possèdent toobe collectés et les scripts de configuration toobe exécuter. 

Mise à jour : juillet 2017

[Ce guide est disponible ici](hana-overview-infrastructure-connectivity.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

### <a name="install-sap-hana-in-sap-hana-on-azure-large-instances"></a>Installer SAP HANA dans SAP HANA sur Azure (grandes instances)
titre : aaaInstall SAP HANA sur SAP HANA sur Azure (Instances de grande taille)

Résumé : Ce document décrit les procédures de configuration hello pour l’installation de SAP HANA sur votre Instance Azure est importante. 

Mise à jour : juillet 2017

[Ce guide est disponible ici](hana-installation.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

### <a name="high-availability-and-disaster-recovery-of-sap-hana-on-azure-large-instances"></a>Haute disponibilité et récupération d’urgence de SAP HANA sur Azure (grandes instances)
titre : aaaHigh disponibilité et récupération d’urgence de HANA SAP sur Azure (Instances de grande taille)

Résumé : La haute disponibilité et la récupération d’urgence constituent des aspects fondamentaux de l’exécution de votre SAP HANA critique sur des serveurs Azure (grandes instances). Son toowork importation avec SAP, votre intégrateur de système, et/ou Microsoft tooproperly construire et implémente à droite de hello stratégie HA/DR pour vous. Points importants à considérer comme objectif de Point de récupération (RPO) et objectif de temps de la récupération (RTO), environnement de tooyour spécifique, prenez en considération.  Ce document décrit les options disponibles pour activer le niveau de haute disponibilité et de récupération d’urgence de votre choix.

Mise à jour : décembre 2016

[Ce document est disponible ici](hana-overview-high-availability-disaster-recovery.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

### <a name="troubleshooting-and-monitoring-of-sap-hana-on-azure-large-instances"></a>Résolution des problèmes et surveillance de SAP HANA sur Azure (grandes instances)
titre : aaaTroubleshooting et surveillance de HANA SAP sur Azure (Instances de grande taille)

Résumé : Ce guide contient des informations utiles pour établir la surveillance de votre environnement SAP HANA sur Azure, ainsi que des informations de résolution des problèmes. 

Mise à jour : décembre 2016

[Ce document est disponible ici](troubleshooting-monitoring.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="sap-hana-on-azure-virtual-machines"></a>SAP HANA sur Machines virtuelles Azure

### <a name="getting-started-with-sap-hana-on-azure"></a>Prise en main de SAP HANA sur Azure
titre : guide d’aaaQuickstart pour l’installation manuelle de SAP HANA sur des machines virtuelles Azure

Résumé : Ce guide de démarrage rapide vous aide à tooset un système de SAP HANA uniques sur les machines virtuelles Azure par une installation manuelle de SAP NetWeaver 7.5 et SAP HANA SP12. guide de Hello suppose que le lecteur de hello est familiarisé avec les concepts de base Azure IaaS comme comment toodeploy virtuels ou réseaux virtuels via hello portail Azure ou de Powershell/CLI, y compris hello modèles json de toouse option. En outre, il est probable que hello lecteur connaît SAP HANA, SAP NetWeaver et comment tooinstall il localement.

Mise à jour : juin 2017

[Ce guide est disponible ici](hana-get-started.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

### <a name="s4hana-sap-cal-deployment-on-azure"></a>Déploiement de S/4HANA SAP CAL sur Azure
titre : aaaDeploy SAP S/4HANA ou BW/4HANA sur Azure

Résumé : Ce guide vous aide à déploiement de hello toodemonstrate de S/4HANA SAP sur Azure à l’aide de la bibliothèque de matériel de Cloud de SAP. Bibliothèque de matériel de Cloud SAP est un service par SAP qui permet à des applications toodeploy SAP sur Azure. guide de Hello présente de déploiement étape par étape hello.

Mise à jour : juin 2017

[Ce guide est disponible ici](cal-s4h.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

### <a name="high-availability-of-sap-hana-in-azure-virtual-machines"></a>Haute disponibilité de SAP HANA dans Machines virtuelles Azure
titre : aaaHigh disponibilité de SAP HANA sur des Machines virtuelles Azure

Résumé : Ce guide vous guide dans la configuration à haute disponibilité hello Hello du système d’exploitation de SUSE 12 et la réplication de système de HANA SAP HANA tooaccommodate avec basculement automatique. guide de Hello est spécifique à SUSE et des Machines virtuelles Azure. guide de Hello ne s’applique pas encore pour Red Hat ou nu ou private cloud ou autres déploiements de cloud public non-Azure.

Mise à jour : juin 2017

[Ce guide est disponible ici](sap-hana-high-availability.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

### <a name="sap-hana-backup-overview-on-azure-vms"></a>Vue d’ensemble de la sauvegarde SAP HANA sur des machines virtuelles Azure
titre : aaaBackup guide pour SAP HANA sur des Machines virtuelles Azure

Résumé : Ce guide fournit des informations de base sur les possibilités de sauvegarde en cas d’exécution de SAP HANA sur Machines virtuelles Azure.

Mise à jour : mars 2017

[Ce guide est disponible ici](sap-hana-backup-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

### <a name="sap-hana-file-level-backup-on-azure-vms"></a>Sauvegarde SAP HANA au niveau des fichiers sur des machines virtuelles Azure
titre : sauvegarde HANA aaaSAP basée sur des instantanés de stockage

Résumé : Ce guide fournit des informations sur l’utilisation des sauvegardes de captures instantanées sur des machines virtuelles Azure lors de l’exécution de SAP HANA sur des machines virtuelles Azure.

Mise à jour : mars 2017

[Ce guide est disponible ici](sap-hana-backup-file-level.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)


### <a name="sap-hana-snapshot-based-backups-on-azure-vms"></a>Sauvegardes basées sur des captures instantanées SAP HANA sur des machines virtuelles Azure
titre : aaaSAP HANA Azure Backup sur le niveau des fichiers

Résumé : Ce guide fournit des informations sur l’utilisation de la sauvegarde SAP HANA au niveau du fichier en cas d’exécution de SAP HANA sur Machines virtuelles Azure.

Mise à jour : mars 2017

[Ce guide est disponible ici](sap-hana-backup-storage-snapshots.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)


## <a name="sap-netweaver-deployed-on-azure-virtual-machines"></a>SAP NetWeaver déployé sur Machines virtuelles Azure

### <a name="deploy-sap-ides-system-on-windows-and-sql-server-through-sap-cal-on-azure"></a>Déployer le système SAP IDES sur Windows et SQL Server via SAP CAL sur Azure
titre : aaaTesting SAP NetWeaver sur machines virtuelles de Microsoft Azure SUSE Linux 

Résumé : Ce document décrit déploiement hello d’un système SAP IDE basé sur Windows et SQL Server sur Azure à l’aide de la bibliothèque de matériel de Cloud de SAP. Dispositif de Cloud SAP bibliothèque est un service SAP qui permet de déployer hello produits SAP sur Azure. Ce document traverse étape par étape de déploiement hello d’un système SAP IDE. système de l’IDE de Hello est juste un exemple de plusieurs autres dizaine d’applications qui peuvent être déployées via application Cloud de SAP sur Microsoft Azure.

Mise à jour : juin 2017

[Ce guide est disponible ici](cal-ides-erp6-erp7-sp3-sql.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)


### <a name="quickstart-guide-for-netweaver-on-suse-linux-on-azure"></a>Guide de démarrage rapide pour NetWeaver sous SUSE Linux sur Azure
titre : aaaTesting SAP NetWeaver sur machines virtuelles de Microsoft Azure SUSE Linux 

Résumé : Cet article décrit les différentes choses tooconsider lorsque vous exécutez SAP NetWeaver sur Microsoft Azure SUSE Linux virtual machines virtuelles. SAP NetWeaver est officiellement pris en charge sur les machines virtuelles SUSE Linux dans Azure. Vous trouverez tous les détails concernant les versions de Linux et les versions du noyau SAP, ainsi que d’autres détails, dans la note SAP 1928533 « Applications SAP sur Azure : produits et types de machines virtuelles pris en charge (SAP Applications on Azure: Supported Products and Azure VM types) ».

Mise à jour : septembre 2016

[Ce guide est disponible ici](suse-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

### <a name="3da0389e-708b-4e82-b2a2-e92f132df89c"></a>Planification et mise en œuvre
titre : aaaAzure Machines virtuelles de planification et l’implémentation de SAP NetWeaver

Résumé : Ce document est toostart du guide hello avec si vous envisagez d’exécuter SAP NetWeaver dans Azure Virtual Machines. Ce guide de planification et d’implémentation vous permet de déterminer si un système existant ou planifié SAP NetWeaver peut être déployé tooan un environnement Azure Virtual Machines. Il aborde plusieurs scénarios de déploiement de SAP NetWeaver et inclut des configurations SAP tooAzure spécifique. Hello répertorie et décrit toutes les hello informations de configuration nécessaires, vous devez sur hello toorun du côté SAP/Azure un paysage SAP hybride. Mesures à prendre tooensure haute disponibilité des systèmes SAP NetWeaver sur IaaS sont également abordées.

Mise à jour : juin 2017

[Ce guide est disponible ici][planning-guide]

### <a name="high-availability-configurations-of-sap-netweaver-in-azure-vms"></a>Configurations de la haute disponibilité de SAP NetWeaver sur des machines virtuelles Azure
titre : aaaAzure haute disponibilité de Machines virtuelles pour SAP NetWeaver

Résumé : Dans ce document, nous aborderons les étapes hello que vous pouvez bénéficier toodeploy systèmes SAP à haute disponibilité dans Azure à l’aide du modèle de déploiement du Gestionnaire de ressources Azure hello. Nous vous guidons dans l’exécution de ces tâches principales. Dans le document de hello, nous décrivons comment unique-point de défaillance des composants comme Advanced Business Application Programming (ABAP) SAP Central Services (ASC) / SAP Central Services (SCS) et les systèmes de gestion de base de données (SGBD) et des composants redondants, tels que SAP Serveur d’applications vont toobe protégé lors de l’exécution dans des machines virtuelles Azure. Un exemple détaillé d’installation et de configuration d’un système SAP à haute disponibilité dans un cluster de clustering de basculement Windows Server dans Azure est fourni dans ce document.

Mise à jour : juin 2017

[Ce guide est disponible ici](high-availability-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

### <a name="realizing-multi-sid-deployments-of-sap-netweaver-in-azure-vms"></a>Réalisation de déploiements multi-SID de SAP NetWeaver sur des machines virtuelles Azure
titre : aaaCreate une configuration de multi-SID SAP NetWeaver 

Résumé : Ce document est un document de toohello plus haute disponibilité pour SAP NetWeaver sur machines virtuelles Azure. En raison de la fonctionnalité toonew dans Azure qui a été introduite dans septembre 2016, il est possible toodeploy plusieurs SAP NetWeaver ASCS/SCS instances dans une paire de machines virtuelles Azure. Avec une telle configuration, vous pouvez réduire le nombre de hello de configurations de SAP NetWeaver hautement disponibles de machines virtuelles nécessaires toodeploy toorealize. Hello décrit le programme d’installation de hello de ces configurations de multi-SID.

Mise à jour : décembre 2016

[Ce guide est disponible ici](high-availability-multi-sid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

### <a name="6aadadd2-76b5-46d8-8713-e8d63630e955"></a>Déploiement de SAP NetWeaver sur des machines virtuelles Azure
titre : aaaAzure déploiement de Machines virtuelles pour SAP NetWeaver

Résumé : Ce document fournit des procédures pour le déploiement d’ordinateurs de toovirtual logiciel SAP NetWeaver dans Azure. Ce document se concentre sur les trois scénarios de déploiement spécifique, en mettant l’accent sur l’activation des Extensions d’analyse hello Azure pour SAP, y compris des recommandations pour hello Extensions d’analyse Azure pour SAP. Ce document part du principe que vous avez lu hello planification et implémentation d’un guide.

Mise à jour : juin 2017

[Ce guide est disponible ici][deployment-guide]

### <a name="1343ffe1-8021-4ce6-a08d-3a1553a4db82"></a>Guide de déploiement SGBD
titre : aaaAzure déploiement de Machines virtuelles SGBD pour SAP NetWeaver

Résumé : Ce document traite des considérations relatives à la planification et d’implémentation pour hello de SGBD utilisés conjointement avec SAP. Dans la première partie de hello, les considérations générales sont répertoriées et présentées. Hello les parties suivantes de papier hello concernent toodeployments du SGBD différent dans Azure sont pris en charge par SAP. Les autres SGBD présentés sont SQL Server, SAP ASE et Oracle. Considérations relatives à avoir tooaccount pour lorsque vous exécutez des systèmes SAP sur Azure conjointement avec les SGBD est traitée dans les parties spécifiques. Des sujets tels que les méthodes de sauvegarde et la haute disponibilité qui sont pris en charge par hello qu'autre SGBD sur Azure est présentés à l’usage hello avec les applications SAP.

Mise à jour : juin 2017

[Ce guide est disponible ici][dbms-guide]

### <a name="using-azure-site-recovery-for-sap-workload"></a>Utilisation d’Azure Site Recovery pour les charges de travail SAP
titre : aaaSAP NetWeaver : création d’une Solution de récupération d’urgence avec Azure Site Recovery 

Résumé : Ce document décrit la façon hello comment les services d’Azure Site Recovery peuvent être utilisés à des fins de hello de la gestion des scénarios de récupération d’urgence. Il expose les situations dans lesquelles Azure est utilisé comme emplacement de récupération d’urgence dans un paysage SAP local à l’aide d’Azure Site Recovery Services. Un autre scénario décrit dans le document de hello est le cas de récupération d’urgence hello Aure Azure (A2A) et la façon dont elle est gérée avec Azure Site Recovery.  

Mise à jour : août 2017

[Ce guide est disponible ici](http://aka.ms/asr-sap)

