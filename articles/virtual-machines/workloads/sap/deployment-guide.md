---
title: "déploiement de Machines virtuelles pour SAP NetWeaver d’aaaAzure | Documents Microsoft"
description: "Découvrez comment toodeploy SAP logiciel sur les ordinateurs virtuels Linux dans Azure."
services: virtual-machines-linux,virtual-machines-windows
documentationcenter: 
author: MSSedusch
manager: timlt
editor: 
tags: azure-resource-manager
keywords: 
ms.assetid: 1c4f1951-3613-4a5a-a0af-36b85750c84e
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 11/08/2016
ms.author: sedusch
ms.openlocfilehash: 42f1d8a3eff51e113729dbfe2848b67deaf06936
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-virtual-machines-deployment-for-sap-netweaver"></a>Déploiement de machines virtuelles Azure pour SAP NetWeaver
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
[2069760]:https://launchpad.support.sap.com/#/notes/2069760
[2121797]:https://launchpad.support.sap.com/#/notes/2121797
[2134316]:https://launchpad.support.sap.com/#/notes/2134316
[2178632]:https://launchpad.support.sap.com/#/notes/2178632
[2191498]:https://launchpad.support.sap.com/#/notes/2191498
[2233094]:https://launchpad.support.sap.com/#/notes/2233094
[2243692]:https://launchpad.support.sap.com/#/notes/2243692
[2367194]:https://launchpad.support.sap.com/#/notes/2367194

[azure-cli]:../../../cli-install-nodejs.md
[azure-portal]:https://portal.azure.com
[azure-ps]:/powershell/azureps-cmdlets-docs
[azure-quickstart-templates-github]:https://github.com/Azure/azure-quickstart-templates
[azure-script-ps]:https://go.microsoft.com/fwlink/p/?LinkID=395017
[azure-subscription-service-limits]:../../../azure-subscription-service-limits.md
[azure-subscription-service-limits-subscription]:../../../azure-subscription-service-limits.md#subscription-limits

[dbms-guide]:dbms-guide.md (Azure Virtual Machines DBMS deployment for SAP)
[dbms-guide-2.1]:dbms-guide.md#c7abf1f0-c927-4a7c-9c1d-c7b5b3b7212f (Caching for VMs and VHDs)
[dbms-guide-2.2]:dbms-guide.md#c8e566f9-21b7-4457-9f7f-126036971a91 (Software RAID)
[dbms-guide-2.3]:dbms-guide.md#10b041ef-c177-498a-93ed-44b3441ab152 (Microsoft Azure Storage)
[dbms-guide-2]:dbms-guide.md#65fa79d6-a85f-47ee-890b-22e794f51a64 (Structure of a RDBMS deployment)
[dbms-guide-3]:dbms-guide.md#871dfc27-e509-4222-9370-ab1de77021c3 (High availability and disaster recovery with Azure VMs)
[dbms-guide-5.5.1]:dbms-guide.md#0fef0e79-d3fe-4ae2-85af-73666a6f7268 (SQL Server 2012 SP1 CU4 and later)
[dbms-guide-5.5.2]:dbms-guide.md#f9071eff-9d72-4f47-9da4-1852d782087b (SQL Server 2012 SP1 CU3 and earlier releases)
[dbms-guide-5.6]:dbms-guide.md#1b353e38-21b3-4310-aeb6-a77e7c8e81c8 (Using a SQL Server image from hello Azure Marketplace)
[dbms-guide-5.8]:dbms-guide.md#9053f720-6f3b-4483-904d-15dc54141e30 (General SQL Server for SAP on Azure summary)
[dbms-guide-5]:dbms-guide.md#3264829e-075e-4d25-966e-a49dad878737 (Specifics tooSQL Server RDBMS)
[dbms-guide-8.4.1]:dbms-guide.md#b48cfe3b-48e9-4f5b-a783-1d29155bd573 (Storage configuration)
[dbms-guide-8.4.2]:dbms-guide.md#23c78d3b-ca5a-4e72-8a24-645d141a3f5d (Backup and restore)
[dbms-guide-8.4.3]:dbms-guide.md#77cd2fbb-307e-4cbf-a65f-745553f72d2c (Performance considerations for backup and restore)
[dbms-guide-8.4.4]:dbms-guide.md#f77c1436-9ad8-44fb-a331-8671342de818 (Other)
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

[deployment-guide]:deployment-guide.md (Azure Virtual Machines deployment for SAP)
[deployment-guide-2.2]:deployment-guide.md#42ee2bdb-1efc-4ec7-ab31-fe4c22769b94 (SAP resources)
[deployment-guide-3.1.2]:deployment-guide.md#3688666f-281f-425b-a312-a77e7db2dfab (Deploying a VM by using a custom image)
[deployment-guide-3.2]:deployment-guide.md#db477013-9060-4602-9ad4-b0316f8bb281 (Scenario 1: Deploying a VM from hello Azure Marketplace for SAP)
[deployment-guide-3.3]:deployment-guide.md#54a1fc6d-24fd-4feb-9c57-ac588a55dff2 (Scenario 2: Deploying a VM with a custom image for SAP)
[deployment-guide-3.4]:deployment-guide.md#a9a60133-a763-4de8-8986-ac0fa33aa8c1 (Scenario 3: Moving a VM from on-premises using a non-generalized Azure VHD with SAP)
[deployment-guide-3]:deployment-guide.md#b3253ee3-d63b-4d74-a49b-185e76c4088e (Deployment scenarios of VMs for SAP on Microsoft Azure)
[deployment-guide-4.1]:deployment-guide.md#604bcec2-8b6e-48d2-a944-61b0f5dee2f7 (Deploying Azure PowerShell cmdlets)
[deployment-guide-4.2]:deployment-guide.md#7ccf6c3e-97ae-4a7a-9c75-e82c37beb18e (Download and import SAP-relevant PowerShell cmdlets)
[deployment-guide-4.3]:deployment-guide.md#31d9ecd6-b136-4c73-b61e-da4a29bbc9cc (Join a VM tooan on-premises domain - Windows only)
[deployment-guide-4.4.2]:deployment-guide.md#6889ff12-eaaf-4f3c-97e1-7c9edc7f7542 (Linux)
[deployment-guide-4.4]:deployment-guide.md#c7cbb0dc-52a4-49db-8e03-83e7edc2927d (Download, install, and enable hello Azure VM Agent)
[deployment-guide-4.5.1]:deployment-guide.md#987cf279-d713-4b4c-8143-6b11589bb9d4 (Azure PowerShell)
[deployment-guide-4.5.2]:deployment-guide.md#408f3779-f422-4413-82f8-c57a23b4fc2f (Azure CLI)
[deployment-guide-4.5]:deployment-guide.md#d98edcd3-f2a1-49f7-b26a-07448ceb60ca (Configure hello Azure Enhanced Monitoring Extension for SAP)
[deployment-guide-5.1]:deployment-guide.md#bb61ce92-8c5c-461f-8c53-39f5e5ed91f2 (Readiness check for Azure Enhanced Monitoring for SAP)
[deployment-guide-5.2]:deployment-guide.md#e2d592ff-b4ea-4a53-a91a-e5521edb6cd1 (Health check for hello Azure monitoring infrastructure)
[deployment-guide-5.3]:deployment-guide.md#fe25a7da-4e4e-4388-8907-8abc2d33cfd8 (Troubleshooting Azure monitoring for SAP)

[deployment-guide-configure-monitoring-scenario-1]:deployment-guide.md#ec323ac3-1de9-4c3a-b770-4ff701def65b (Configure monitoring)
[deployment-guide-configure-proxy]:deployment-guide.md#baccae00-6f79-4307-ade4-40292ce4e02d (Configure hello proxy)
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
[deployment-guide-troubleshooting-chapter]:deployment-guide.md#564adb4f-5c95-4041-9616-6635e83a810b (Checks and troubleshooting for setting up end-to-end monitoring)

[deploy-template-cli]:../../../resource-group-template-deploy-cli.md
[deploy-template-portal]:../../../resource-group-template-deploy-portal.md
[deploy-template-powershell]:../../../resource-group-template-deploy.md

[dr-guide-classic]:http://go.microsoft.com/fwlink/?LinkID=521971

[getting-started]:get-started.md
[getting-started-dbms]:get-started.md#1343ffe1-8021-4ce6-a08d-3a1553a4db82
[getting-started-deployment]:get-started.md#6aadadd2-76b5-46d8-8713-e8d63630e955
[getting-started-planning]:get-started.md#3da0389e-708b-4e82-b2a2-e92f132df89c

[getting-started-windows-classic]:../../virtual-machines-windows-classic-sap-get-started.md
[getting-started-windows-classic-dbms]:../../virtual-machines-windows-classic-sap-get-started.md#c5b77a14-f6b4-44e9-acab-4d28ff72a930
[getting-started-windows-classic-deployment]:../../virtual-machines-windows-classic-sap-get-started.md#f84ea6ce-bbb4-41f7-9965-34d31b0098ea
[getting-started-windows-classic-dr]:../../virtual-machines-windows-classic-sap-get-started.md#cff10b4a-01a5-4dc3-94b6-afb8e55757d3
[getting-started-windows-classic-ha-sios]:../../virtual-machines-windows-classic-sap-get-started.md#4bb7512c-0fa0-4227-9853-4004281b1037
[getting-started-windows-classic-planning]:../../virtual-machines-windows-classic-sap-get-started.md#f2a5e9d8-49e4-419e-9900-af783173481c

[ha-guide-classic]:http://go.microsoft.com/fwlink/?LinkId=613056

[install-extension-cli]:virtual-machines-linux-enable-aem.md

[Logo_Linux]:media/virtual-machines-shared-sap-shared/Linux.png
[Logo_Windows]:media/virtual-machines-shared-sap-shared/Windows.png

[msdn-set-azurermvmaemextension]:https://msdn.microsoft.com/library/azure/mt670598.aspx

[planning-guide]:planning-guide.md (Azure Virtual Machines planning and implementation for SAP)
[planning-guide-1.2]:planning-guide.md#e55d1e22-c2c8-460b-9897-64622a34fdff (Resources)
[planning-guide-11]:planning-guide.md#7cf991a1-badd-40a9-944e-7baae842a058 (High availability and disaster recovery for SAP NetWeaver running on Azure Virtual Machines)
[planning-guide-11.4.1]:planning-guide.md#5d9d36f9-9058-435d-8367-5ad05f00de77 (High availability for SAP Application Servers)
[planning-guide-11.5]:planning-guide.md#4e165b58-74ca-474f-a7f4-5e695a93204f (Using Autostart for SAP instances)
[planning-guide-2.1]:planning-guide.md#1625df66-4cc6-4d60-9202-de8a0b77f803 (Cloud-only - Virtual Machine deployments in Azure without dependencies on hello on-premises customer network)
[planning-guide-2.2]:planning-guide.md#f5b3b18c-302c-4bd8-9ab2-c388f1ab3d10 (Cross-premises - Deployment of single or multiple SAP VMs in Azure fully integrated with hello on-premises network)
[planning-guide-3.1]:planning-guide.md#be80d1b9-a463-4845-bd35-f4cebdb5424a (Azure regions)
[planning-guide-3.2.1]:planning-guide.md#df49dc09-141b-4f34-a4a2-990913b30358 (Fault domains)
[planning-guide-3.2.2]:planning-guide.md#fc1ac8b2-e54a-487c-8581-d3cc6625e560 (Upgrade domains)
[planning-guide-3.2.3]:planning-guide.md#18810088-f9be-4c97-958a-27996255c665 (Azure availability sets)
[planning-guide-3.2]:planning-guide.md#8d8ad4b8-6093-4b91-ac36-ea56d80dbf77 (Microsoft Azure virtual machines concept)
[planning-guide-3.3.2]:planning-guide.md#ff5ad0f9-f7f4-4022-9102-af07aef3bc92 (Azure Premium Storage)
[planning-guide-5.1.1]:planning-guide.md#4d175f1b-7353-4137-9d2f-817683c26e53 (Moving a VM from on-premises tooAzure with a non-generalized disk)
[planning-guide-5.1.2]:planning-guide.md#e18f7839-c0e2-4385-b1e6-4538453a285c (Deploying a VM with a customer specific image)
[planning-guide-5.2.1]:planning-guide.md#1b287330-944b-495d-9ea7-94b83aff73ef (Preparation for moving a VM from on-premises tooAzure with a non-generalized disk)
[planning-guide-5.2.2]:planning-guide.md#57f32b1c-0cba-4e57-ab6e-c39fe22b6ec3 (Preparation for deploying a VM with a customer specific image for SAP)
[planning-guide-5.2]:planning-guide.md#6ffb9f41-a292-40bf-9e70-8204448559e7 (Preparing VMs with SAP for Azure)
[planning-guide-5.3.1]:planning-guide.md#6e835de8-40b1-4b71-9f18-d45b20959b79 (Difference between an Azure disk and an Azure image)
[planning-guide-5.3.2]:planning-guide.md#a43e40e6-1acc-4633-9816-8f095d5a7b6a (Uploading a VHD from on-premises tooAzure)
[planning-guide-5.4.2]:planning-guide.md#9789b076-2011-4afa-b2fe-b07a8aba58a1 (Copying disks between Azure Storage accounts)
[planning-guide-5.5.1]:planning-guide.md#4efec401-91e0-40c0-8e64-f2dceadff646 (VM/VHD structure for SAP deployments)
[planning-guide-5.5.3]:planning-guide.md#17e0d543-7e8c-4160-a7da-dd7117a1ad9d (Setting automount for attached disks)
[planning-guide-7.1]:planning-guide.md#3e9c3690-da67-421a-bc3f-12c520d99a30 (Single VM with SAP NetWeaver demo/training scenario)
[planning-guide-7]:planning-guide.md#96a77628-a05e-475d-9df3-fb82217e8f14 (Concepts of Cloud-Only deployment of SAP instances)
[planning-guide-9.1]:planning-guide.md#6f0a47f3-a289-4090-a053-2521618a28c3 (Azure Monitoring Solution for SAP)
[planning-guide-azure-premium-storage]:planning-guide.md#ff5ad0f9-f7f4-4022-9102-af07aef3bc92 (Azure Premium Storage)
[planning-guide-managed-disks]:planning-guide.md#c55b2c6e-3ca1-4476-be16-16c81927550f (Managed Disks)
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
[planning-guide-microsoft-azure-networking]:planning-guide.md#61678387-8868-435d-9f8c-450b2424f5bd (Microsoft Azure networking)
[planning-guide-storage-microsoft-azure-storage-and-data-disks]:planning-guide.md#a72afa26-4bf4-4a25-8cf7-855d6032157f (Storage: Microsoft Azure Storage and data disks)

[powershell-install-configure]:https://docs.microsoft.com/powershell/azure/install-azurerm-ps
[resource-group-authoring-templates]:../../../resource-group-authoring-templates.md
[resource-group-overview]:../../../azure-resource-manager/resource-group-overview.md
[resource-groups-networking]:../../../virtual-network/resource-groups-networking.md
[sap-pam]:https://support.sap.com/pam (SAP Product Availability Matrix)
[sap-templates-2-tier-marketplace-image]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-2-tier-marketplace-image%2Fazuredeploy.json
[sap-templates-2-tier-marketplace-image-md]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-2-tier-marketplace-image-md%2Fazuredeploy.json
[sap-templates-2-tier-os-disk]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-2-tier-user-disk%2Fazuredeploy.json
[sap-templates-2-tier-os-disk-md]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-2-tier-user-disk-md%2Fazuredeploy.json
[sap-templates-2-tier-user-image]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-2-tier-user-image%2Fazuredeploy.json
[sap-templates-2-tier-user-image-md]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-2-tier-user-image-md%2Fazuredeploy.json
[sap-templates-3-tier-marketplace-image]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image%2Fazuredeploy.json
[sap-templates-3-tier-marketplace-image-md]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image-md%2Fazuredeploy.json
[sap-templates-3-tier-user-image]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-user-image%2Fazuredeploy.json
[sap-templates-3-tier-user-image-md]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-user-image-md%2Fazuredeploy.json
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
[virtual-machines-linux-cli-deploy-templates]:../../linux/cli-deploy-templates.md (Deploy and manage virtual machines by using Azure Resource Manager templates and hello Azure CLI)
[virtual-machines-deploy-rmtemplates-powershell]:../../virtual-machines-windows-ps-manage.md (Manage virtual machines by using Azure Resource Manager and PowerShell)
[virtual-machines-windows-agent-user-guide]:../../windows/agent-user-guide.md
[virtual-machines-linux-agent-user-guide]:../../linux/agent-user-guide.md
[virtual-machines-linux-agent-user-guide-command-line-options]:../../linux/agent-user-guide.md#command-line-options
[virtual-machines-linux-capture-image]:../../linux/capture-image.md
[virtual-machines-linux-capture-image-resource-manager]:../../linux/capture-image.md
[virtual-machines-linux-capture-image-resource-manager-capture]:../../linux/capture-image.md#step-2-capture-the-vm
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
[virtual-machines-ps-create-preconfigure-windows-resource-manager-vms]:../../virtual-machines-windows-ps-create.md
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

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-rm-include.md)]

Machines virtuelles Azure est la solution hello pour les organisations qui ont besoin de ressources de calcul et de stockage dans le temps minimal et sans par de longs cycles. Vous pouvez utiliser des applications Azure Virtual Machines toodeploy classique, comme les applications basées sur SAP NetWeaver dans Azure. Élargissez la fiabilité et la disponibilité d’une application sans ressources locales supplémentaires. Comme le service Machines virtuelles Azure prend en charge la connectivité intersite, vous pouvez intégrer les machines virtuelles Azure dans les domaines locaux, les clouds privés et le paysage SAP de votre organisation.

Dans cet article, nous couvrent les applications de hello étapes toodeploy SAP sur des machines virtuelles (VM) dans Azure, y compris les options de déploiement de remplacement et la résolution des problèmes. Cet article s’appuie sur les informations de hello dans [planification des Machines virtuelles Azure et implémentation pour SAP NetWeaver][planning-guide]. Il complète également la documentation d’installation SAP et les Notes SAP, qui sont des ressources principales de hello pour l’installation et de déploiement de logiciels SAP.

## <a name="prerequisites"></a>Composants requis
La configuration d’une machine virtuelle Azure pour le déploiement des logiciels SAP implique plusieurs étapes et diverses ressources. Avant de commencer, assurez-vous que conditions préalables hello pour l’installation des logiciels SAP sur des machines virtuelles dans Azure.

### <a name="local-computer"></a>Ordinateur local
toomanage Windows ou les machines virtuelles Linux, vous pouvez utiliser un script PowerShell et les hello portail Azure. Dans les deux cas, vous devez disposer d’un ordinateur local exécutant Windows 7 ou une version ultérieure de Windows. Si vous souhaitez toomanage uniquement les machines virtuelles Linux et que vous voulez toouse un ordinateur Linux pour cette tâche, vous pouvez utiliser CLI d’Azure.

### <a name="internet-connection"></a>Connexion Internet
toodownload, exécution hello outils et scripts qui sont requis pour le déploiement de logiciel SAP, vous devez être connecté toohello Internet. Hello machine virtuelle Azure qui est en cours d’exécution hello améliorée Extension de surveillance Azure pour SAP doit également toohello d’accès Internet. Si hello machine virtuelle Azure fait partie d’un réseau virtuel Azure ou le domaine local, assurez-vous que les paramètres de proxy appropriés hello sont définis, comme décrit dans [configurer le proxy de hello][deployment-guide-configure-proxy].

### <a name="microsoft-azure-subscription"></a>Abonnement Microsoft Azure
Vous avez besoin d’un compte Azure actif.

### <a name="topology-and-networking"></a>Topologie et mise en réseau
Vous devez la topologie de hello toodefine et l’architecture de hello déploiement SAP dans Azure :

* Toobe de comptes de stockage Azure utilisé
* Réseau virtuel où vous souhaitez le système SAP de hello toodeploy
* Toowhich de groupe de ressources que toodeploy hello SAP système
* Région Azure où vous souhaitez le système SAP de hello toodeploy
* Configuration SAP (à deux ou trois niveaux)
* Tailles de machine virtuelle et de nombre de hello de toobe de disques de données supplémentaires montés toohello VMs
* Configuration du système de transport et correction SAP (CTS)

Créer et configurer des comptes de stockage Azure (si nécessaire) ou des réseaux virtuels Azure avant de commencer le processus de déploiement de logiciel SAP hello. Pour plus d’informations sur la façon toocreate et configurer ces ressources, consultez [planification des Machines virtuelles Azure et implémentation pour SAP NetWeaver][planning-guide].

### <a name="sap-sizing"></a>Dimensionnement SAP
Savoir hello suivant d’informations, pour le dimensionnement de SAP :

* Prévue de charge de travail SAP, par exemple, en utilisant l’outil de dimensionnement rapide de SAP de hello et le numéro de performances Standard SAP Application (SAP) hello
* Consommation de ressources et de la mémoire du processeur requise du système SAP de hello
* Opérations d’entrée/sortie (E/S) par seconde requises
* Bande passante réseau requise pour la communication éventuelle entre les différentes machines virtuelles dans Azure
* Besoins en bande passante entre les ressources locales et hello système déployé Azure SAP

### <a name="resource-groups"></a>Groupes de ressources
Dans le Gestionnaire de ressources Azure, vous pouvez utiliser toomanage de groupes de ressources toutes les ressources de l’application hello dans votre abonnement Azure. Pour plus d’informations, consultez [Présentation d’Azure Resource Manager][resource-group-overview].

## <a name="resources"></a>Ressources

### <a name="42ee2bdb-1efc-4ec7-ab31-fe4c22769b94"></a>Ressources SAP
Lorsque vous configurez votre déploiement de logiciel SAP, vous devez hello suivant les ressources SAP :

* Note SAP [1928533], qui contient :
  * Liste des tailles de machine virtuelle Azure qui sont pris en charge pour le déploiement de hello de logiciels SAP
  * des informations importantes sur la capacité en fonction de la taille des machines virtuelles Azure
  * les logiciels SAP pris en charge et les combinaisons entre système d’exploitation et base de données
  * la version du noyau SAP requise pour Windows et Linux sur Microsoft Azure

* La note SAP [2015553] répertorie les conditions préalables au déploiement de logiciels SAP pris en charge par SAP sur Azure.
* La note SAP [2178632] contient des informations détaillées sur toutes les métriques de surveillance rapportées pour SAP sur Azure.
* La Note SAP [1409604] hello requise version de l’Agent hôte SAP pour Windows dans Azure.
* La Note SAP [2191498] hello requise version de l’Agent hôte SAP pour Linux dans Azure.
* La note SAP [2243692] contient des informations sur les licences SAP sur Linux dans Azure.
* La note SAP [1984787] contient des informations sur SUSE Linux Enterprise Server 12.
* La note SAP [2002167] contient des informations sur Red Hat Enterprise Linux 7.x.
* La note SAP [2069760] contient des informations générales sur Oracle Linux 7.x.
* La Note SAP [1999351] a des informations de dépannage supplémentaires pour hello améliorée Extension de surveillance Azure pour SAP.
* La note SAP [1597355] contient des informations générales sur l’espace d’échange pour Linux.
* La [page SAP sur Microsoft Azure](https://wiki.scn.sap.com/wiki/x/Pia7Gg) comprend des actualités, ainsi qu’une collection de ressources utiles.
* Le [WIKI de la communauté SAP](https://wiki.scn.sap.com/wiki/display/HOME/SAPonLinuxNotes) contient toutes les notes SAP requises pour Linux.
* Applets de commande PowerShell spécifiques à SAP qui font partie [d’Azure PowerShell][azure-ps].
* Commandes de l’interface de ligne de commande Azure spécifique à SAP faisant partie de [l’interface de ligne de commande Azure][azure-cli].

### <a name="42ee2bdb-1efc-4ec7-ab31-fe4c22769b94"></a>Ressources Windows
Ces articles Microsoft couvrent les déploiements SAP dans Azure :

* [Planification et implémentation de machines virtuelles Azure pour SAP NetWeaver][planning-guide]
* [Déploiement de machines virtuelles Azure pour SAP NetWeaver (le présent article)][deployment-guide]
* [Déploiement SGBD de machines virtuelles Azure pour SAP NetWeaver][dbms-guide]

## <a name="b3253ee3-d63b-4d74-a49b-185e76c4088e"></a>Scénarios de déploiement de logiciels SAP sur des machines virtuelles Azure
Vous avez plusieurs possibilités pour déployer des machines virtuelles et les disques associés dans Azure. Il est important toounderstand les différences de hello entre les options de déploiement, car vous pouvez effectuer différentes étapes tooprepare vos machines virtuelles pour le déploiement en fonction du type de déploiement hello que vous choisissez.

### <a name="db477013-9060-4602-9ad4-b0316f8bb281"></a>Scénario 1 : Déploiement d’une machine virtuelle à partir de hello Azure Marketplace pour SAP
Vous pouvez utiliser une image fournie par Microsoft ou par un tiers dans hello Azure Marketplace toodeploy votre machine virtuelle. Hello Marketplace offre certaines images de système d’exploitation standards de Windows Server et les différentes distributions de Linux. Vous pouvez également déployer une image qui inclut les SKU du système de gestion de la base de données (SGBD), par exemple Microsoft SQL Server. Pour plus d’informations sur l’utilisation des images avec les SKU SGBD, consultez [Déploiement SGBD de machines virtuelles Azure pour SAP NetWeaver][dbms-guide].

Hello organigramme suivant présente séquence de SAP spécifique de hello d’étapes de déploiement d’une machine virtuelle à partir de hello Azure Marketplace :

![Organigramme de déploiement des ordinateurs virtuels pour les systèmes SAP à l’aide d’une image de machine virtuelle à partir de hello Azure Marketplace][deployment-guide-figure-100]

#### <a name="create-a-virtual-machine-by-using-hello-azure-portal"></a>Créer un ordinateur virtuel à l’aide de hello portail Azure
toocreate de façon plus simple Hello un nouvel ordinateur virtuel avec une image à partir de hello Azure Marketplace est à l’aide de hello portail Azure.

1.  Accédez trop<https://portal.azure.com/#create/hub>.  Ou, dans hello menus du portail Azure, sélectionnez **+ nouveau**.
2.  Sélectionnez **de calcul**, puis sélectionnez le type hello de souhaité toodeploy de système d’exploitation. Par exemple, Windows Server 2012 R2, SUSE Linux Enterprise Server 12 (SLES 12) ou Red Hat Enterprise Linux 7.2 (RHEL 7.2) ou Oracle Linux 7.2. affichage de liste par défaut Hello n’affiche pas que toutes prises en charge des systèmes d’exploitation. Pour obtenir une liste complète, sélectionnez **Afficher tout**. Pour plus d’informations sur les systèmes d’exploitation pris en charge pour le déploiement de logiciels SAP, consultez la note SAP [1928533].
3.  Sur la page suivante de hello, examinez les termes et conditions.
4.  Bonjour **sélectionner un modèle de déploiement** , sélectionnez **le Gestionnaire de ressources**.
5.  Sélectionnez **Créer**.

vous guide tout au long de la configuration d’ordinateur virtuel de hello requis paramètres toocreate hello Assistant de Hello, en outre tooall requis des ressources, telles que les interfaces réseau et les comptes de stockage. Voici certains exemples de paramètres :

1. **Paramètres de base**:
 * **Nom**: nom hello de ressource de hello (nom de machine virtuelle hello).
 * **Type de disque de machine virtuelle**: sélectionnez le type de disque hello du disque de hello du système d’exploitation. Si vous souhaitez toouse stockage Premium pour vos disques de données, nous recommandons d’utiliser le stockage Premium pour le disque de système d’exploitation hello également.
 * **Nom d’utilisateur et mot de passe** ou **la clé publique SSH**: entrez le nom d’utilisateur hello et le mot de passe utilisateur hello qui est créé lors de la configuration de hello. Pour une machine virtuelle Linux, vous pouvez entrer la clé SSH (Secure Shell) publique hello utiliser toosign dans toohello machine.
 * **Abonnement**: sélectionnez l’abonnement hello que vous souhaitez toouse tooprovision hello machine virtuelle.
 * **Groupe de ressources**: nom hello hello du groupe de ressources pour hello machine virtuelle. Vous pouvez entrer le nom hello un nouveau groupe ou hello du nom de ressource d’un groupe de ressources existe déjà.
 * **Emplacement**: où toodeploy hello nouvel ordinateur virtuel. Si vous souhaitez que le réseau local tooyour tooconnect hello machine virtuelle, veillez à que sélectionner emplacement hello du réseau virtuel hello qui connecte le réseau local de tooyour Azure. Pour plus d’informations, consultez [Mise en réseau Microsoft Azure][planning-guide-microsoft-azure-networking] dans [SAP NetWeaver sur machines virtuelles Azure – Guide de planification et d’implémentation][planning-guide].
2. **Taille**:

     Pour obtenir la liste des types de machine virtuelle pris en charge, consultez la note SAP [1928533]. Assurez-vous que vous sélectionnez le type de machine virtuelle hello correct si vous souhaitez toouse stockage Azure Premium. Tous les types de machine virtuelle ne prennent pas en charge le stockage Premium. Pour plus d’informations, consultez [Stockage : stockage Microsoft Azure et disques de données][planning-guide-storage-microsoft-azure-storage-and-data-disks] et [Stockage Microsoft Azure][planning-guide-azure-premium-storage] dans [SAP NetWeaver sur machines virtuelles Azure – Guide de planification et d’implémentation][planning-guide].

3. **Paramètres**:
  * **Stockage**
    * **Type de disque**: sélectionnez le type de disque hello du disque de hello du système d’exploitation. Si vous souhaitez toouse stockage Premium pour vos disques de données, nous recommandons d’utiliser le stockage Premium pour le disque de système d’exploitation hello également.
    * **Utiliser des disques gérés**: Si vous souhaitez que les disques gérés toouse, sélectionnez Oui. Pour plus d’informations sur les disques gérés, consultez le chapitre [disques gérés] [ planning-guide-managed-disks] dans le guide de planification hello.
    * **Compte de stockage**: sélectionnez un compte de stockage existant ou créez un nouveau compte de stockage. Notez que tous les types de stockage ne peuvent pas être utilisés pour l’exécution d’applications SAP. Pour plus d’informations sur les types de stockage, consultez [Stockage Microsoft Azure][dbms-guide-2.3] dans [Déploiement SGBD de machines virtuelles Azure pour SAP NetWeaver][dbms-guide].
  * **Réseau**
    * **Réseau virtuel** et **sous-réseau**: machine virtuelle toointegrate hello votre intranet, le réseau virtuel hello select qui n’est connecté tooyour sur site réseau.
    * **Adresse IP publique**: sélectionnez hello adresse IP publique que vous souhaitez toouse ou entrez les paramètres toocreate une nouvelle adresse IP publique. Vous pouvez utiliser un tooaccess d’adresse IP publique de votre machine virtuelle sur hello Internet. Assurez-vous que vous créez également un ordinateur virtuel de réseau sécurité groupe toohelp un accès sécurisé tooyour.
    * **Groupe de sécurité réseau** : pour plus d’informations, consultez [Contrôler le flux de trafic réseau avec les groupes de sécurité réseau][virtual-networks-nsg].
  * **Extensions**: vous pouvez installer des extensions de machine virtuelle en les ajoutant toohello déploiement. Vous n’avez pas besoin d’extensions tooadd dans cette étape. extensions Hello requises pour la prise en charge SAP sont installées ultérieurement. Consultez le chapitre [configurer hello améliorée Extension de surveillance Azure pour SAP] [ deployment-guide-4.5] dans ce guide.
  * **Haute disponibilité**: sélectionnez un ensemble de disponibilité, ou entrez hello paramètres toocreate disponibilité d’une nouvelle valeur. Pour plus d’informations, consultez [Groupes à haute disponibilité Azure][planning-guide-3.2.3].
  * **Surveillance**
    * **Diagnostics de démarrage** : vous pouvez sélectionner **Désactiver** pour le diagnostic de démarrage.
    * **Diagnostics du système d’exploitation invité** : vous pouvez sélectionner **Désactiver** pour le diagnostic de surveillance.

4. **Résumé**:

  Passez en revue vos sélections, puis sélectionnez **OK**.

Votre ordinateur virtuel est déployé dans le groupe de ressources hello que vous avez sélectionné.

#### <a name="create-a-virtual-machine-by-using-a-template"></a>Création d’une machine virtuelle à l’aide d’un modèle
Vous pouvez créer un ordinateur virtuel à l’aide d’un des modèles SAP hello publiés Bonjour [référentiel GitHub d’azure-démarrage rapide-modèles][azure-quickstart-templates-github]. Vous pouvez également manuellement créer une machine virtuelle à l’aide de hello [portail Azure][virtual-machines-windows-tutorial], [PowerShell][virtual-machines-ps-create-preconfigure-windows-resource-manager-vms], ou [CLI d’Azure ][virtual-machines-linux-tutorial].

* [**Modèle de configuration à deux niveaux (une seule machine virtuelle)** (sap-2-tier-user-disk)][sap-templates-2-tier-marketplace-image]

  toocreate un système à deux niveaux en utilisant uniquement une machine virtuelle, utilisez ce modèle.
* [**Modèle de configuration à deux niveaux (une seule machine virtuelle) - Disques managés** (sap-2-tier-marketplace-image-md)][sap-templates-2-tier-marketplace-image-md]

  toocreate un système à deux niveaux en utilisant qu’un seul ordinateur virtuel et disques gérés, utilisez ce modèle.
* [**Modèle de configuration à trois niveaux (plusieurs machines virtuelles)** (sap-3-tier-marketplace-image)][sap-templates-3-tier-marketplace-image]

  toocreate un système à trois niveaux à l’aide de plusieurs ordinateurs virtuels, utilisez ce modèle.
* [**Modèle de configuration à trois niveaux (plusieurs machines virtuelles) - Disques managés** (sap-3-tier-marketplace-image-md)][sap-templates-3-tier-marketplace-image-md]

  toocreate un système à trois niveaux à l’aide de plusieurs machines virtuelles et disques gérés, utilisez ce modèle.

Bonjour portail Azure, entrez hello paramètres pour le modèle de hello suivants :

1. **Paramètres de base**:
  * **Abonnement**: modèle de hello abonnement toouse toodeploy hello.
  * **Groupe de ressources**: modèle de hello ressource groupe toouse toodeploy hello. Vous pouvez créer un nouveau groupe de ressources, ou vous pouvez sélectionner un groupe de ressources existant dans l’abonnement de hello.
  * **Emplacement**: où toodeploy hello modèle. Si vous avez sélectionné un groupe de ressources existant, emplacement hello ce groupe de ressources est utilisé.

2. **Paramètres**:
  * **ID du système SAP**: hello SAP système ID (SID).
  * **Type de système d’exploitation**: hello système d’exploitation toodeploy, par exemple, Windows Server 2012 R2, SUSE Linux Enterprise Server 12 (SLES 12), Red Hat Enterprise Linux 7.2 (RHEL 7.2) ou Oracle Linux 7.2.

    affichage de liste Hello n’affiche pas que toutes prises en charge des systèmes d’exploitation. Pour plus d’informations sur les systèmes d’exploitation pris en charge pour le déploiement de logiciels SAP, consultez la note SAP [1928533].
  * **Taille du système SAP**: hello taille Hello système SAP.

    nombre de Hello du nouveau système SAP hello fournit. Si vous n’êtes pas sûr du système de hello combien SAP, demandez à votre partenaire technologique SAP ou un intégrateur de système.
  * **Disponibilité du système** (modèle à trois niveaux uniquement) : hello la disponibilité du système.

    Sélectionnez la haute disponibilité (**HA**) si la configuration est adaptée à une installation haute disponibilité. Deux serveurs de base de données et deux serveurs pour ABAP SAP Central Services (ASC) sont créés.
  * **Type de stockage** (modèle de couche 2 uniquement) : hello du type de stockage toouse.

    Pour les grands systèmes, nous vous recommandons l’utilisation du stockage Premium Azure. Pour plus d’informations sur les types de stockage, consultez ces ressources :
      * [Utilisation du stockage SSD Azure Premium pour l’instance de SGBD SAP][2367194]
      * [Stockage Microsoft Azure][dbms-guide-2.3] dans [Déploiement SGBD de machines virtuelles Azure pour SAP NetWeaver][dbms-guide]
      * [Stockage Premium : stockage hautes performances pour les charges de travail des machines virtuelles Azure][storage-premium-storage-preview-portal]
      * [Introduction tooMicrosoft stockage Azure][storage-introduction]
  * **Nom d’utilisateur administrateur** et **Mot de passe administrateur** : nom d’utilisateur et mot de passe.
    Un nouvel utilisateur est créé pour la signature dans la machine virtuelle de toohello.
  * **Sous-réseau nouveau ou existant** : détermine si un réseau virtuel et un sous-réseau doivent être créés ou si un sous-réseau existant doit être utilisé. Si vous disposez déjà d’un réseau virtuel qui est le réseau local de tooyour connecté, sélectionnez **existant**.
  * **ID de sous-réseau**: hello les ID de sous-réseau hello hello ordinateurs virtuels se connectera. Sélectionnez sous-réseau hello de votre réseau privé virtuel (VPN) ou de Azure ExpressRoute réseau virtuel toouse tooconnect hello machine virtuelle tooyour sur réseau local. ID de Hello ressemble généralement à ceci : /subscriptions/&lt;id d’abonnement > /resourceGroups/&lt;nom de groupe de ressources > /providers/Microsoft.Network/virtualNetworks/&lt;nom de réseau virtuel > /subnets/&lt;nom de sous-réseau >

3. **Conditions générales** :  
    Lisez et acceptez les conditions juridiques hello.

4.  Sélectionnez **Achat**.

Hello Agent de machine virtuelle Azure est déployé par défaut lorsque vous utilisez une image à partir de hello Azure Marketplace.

#### <a name="configure-proxy-settings"></a>Configuration des paramètres de proxy
Selon la configuration de votre réseau local, vous devrez peut-être tooset un proxy de hello sur votre machine virtuelle. Si votre machine virtuelle est connectée tooyour du réseau local via un VPN ou ExpressRoute, hello machine virtuelle ne peut pas être en mesure de tooaccess hello Internet et ne seront pas être en mesure de toodownload extensions de hello requis ou collecter des données d’analyse. Pour plus d’informations, consultez [configurer le proxy de hello][deployment-guide-configure-proxy].

#### <a name="join-a-domain-windows-only"></a>Joindre un domaine (Windows uniquement)
Si votre déploiement Azure est instance d’Active Directory ou DNS de locale via un réseau VPN site à site Azure ou une ExpressRoute tooan connecté (on parle *intersite* dans [planification des Machines virtuelles Azure et l’implémentation de SAP NetWeaver][planning-guide]), il est probable que hello machine virtuelle rejoint un domaine local. Pour plus d’informations sur les considérations pour cette tâche, consultez [joindre un domaine local du tooan VM (Windows uniquement)][deployment-guide-4.3].

#### <a name="ec323ac3-1de9-4c3a-b770-4ff701def65b"></a>Configuration de l’analyse
toobe que SAP prend en charge votre environnement, configurez hello Extension de surveillance Azure pour SAP comme décrit dans [configurer hello améliorée Extension de surveillance Azure pour SAP][deployment-guide-4.5]. Vérifier la configuration requise de hello pour la surveillance SAP et la version minimale requise du noyau SAP et de l’Agent hôte SAP, dans les ressources hello dans [les ressources SAP][deployment-guide-2.2].

#### <a name="monitoring-check"></a>Vérification de l’analyse
Vérifiez si l’analyse fonctionne comme décrit dans [Vérifications et résolution des problèmes pour la configuration de l’analyse de bout en bout][deployment-guide-troubleshooting-chapter].

#### <a name="post-deployment-steps"></a>Étapes de post-déploiement
Après avoir créé hello VM et hello machine virtuelle est déployée, vous devez disposer des composants de logiciel de hello requis tooinstall Bonjour machine virtuelle. En raison de la séquence d’installation hello/logiciels de déploiement dans ce type de déploiement des ordinateurs virtuels, hello toobe de logiciel installé doit être déjà disponible, soit dans Azure, sur une autre machine virtuelle, ou en tant que disque pouvant être attachés. Ou, à l’aide d’un scénario de coexistence, de connectivité qui toohello locales (partages d’installation) de ressources est donné.

Après avoir déployé votre machine virtuelle dans Azure, suivez hello même indications et des outils tooinstall hello logiciels SAP sur votre machine virtuelle que vous le feriez dans un environnement sur site. tooinstall les logiciels SAP sur une machine virtuelle Azure, à la fois SAP et Microsoft vous recommandent de Téléchargez et stockez le support d’installation SAP hello sur les disques durs virtuels de Azure ou de disques gérés, ou que vous créez une machine virtuelle Azure qui fonctionne comme un serveur de fichiers qui a toutes les hello requis support d’installation SAP.

### <a name="54a1fc6d-24fd-4feb-9c57-ac588a55dff2"></a>Scénario 2 : Déploiement d’une machine virtuelle avec une image personnalisée pour SAP
Étant donné que les différentes versions de système d’exploitation ou SGBD ont des exigences différentes, images hello que vous trouvez Bonjour Azure Marketplace répondra ne peut-être pas à vos besoins. Au lieu de cela, vous pourriez toocreate une machine virtuelle à l’aide de votre propre image de machine virtuelle du système d’exploitation/SGBD, que vous pouvez déployer ultérieurement.
Vous utilisez des étapes différentes toocreate une image privée pour Linux à un toocreate pour Windows.

- - -
> ![Windows][Logo_Windows] Windows
>
> tooprepare une image de Windows que vous pouvez utiliser toodeploy plusieurs machines virtuelles, les paramètres de Windows hello (par exemple, le SID Windows et le nom d’hôte) doivent être abstraits ou généralisé sur hello local machine virtuelle. Vous pouvez utiliser [sysprep](https://msdn.microsoft.com/library/hh825084.aspx) toodo cela.
>
> ![Linux][Logo_Linux] Linux
>
> tooprepare une image Linux que vous pouvez utiliser toodeploy plusieurs machines virtuelles, certains paramètres Linux doivent être abstraite ou généralisé sur hello local machine virtuelle. Vous pouvez utiliser `waagent -deprovision` toodo cela. Pour plus d’informations, consultez [capturer une machine virtuelle de Linux en cours d’exécution sur Azure] [ virtual-machines-linux-capture-image] et hello [guide de l’utilisateur l’agent Azure Linux][virtual-machines-linux-agent-user-guide-command-line-options].
>
>

- - -
Vous pouvez préparer et créer une image personnalisée et réutilisez-la toocreate plusieurs nouveaux ordinateurs virtuels. Cette opération est décrite dans [SAP NetWeaver sur machines virtuelles Azure – Guide de planification et d’implémentation][planning-guide]. Configuration de votre base de données de contenu à l’aide du Gestionnaire de configuration de logiciels SAP tooinstall un nouveau système SAP (restaure une sauvegarde de base de données à partir d’un disque est attaché toohello virtual machine) ou par la restauration d’une sauvegarde de base de données directement à partir du stockage Azure, si votre SGBD prend en charge. Pour plus d’informations, consultez [Déploiement SGBD de machines virtuelles Azure pour SAP NetWeaver][dbms-guide]. Si vous avez déjà installé un système SAP sur votre machine locale virtuelle (en particulier pour les systèmes à deux niveaux), vous pouvez adapter les paramètres de système SAP hello après le déploiement de hello Hello machine virtuelle Azure à l’aide de procédure de système renommer hello pris en charge par la configuration du logiciel SAP Manager (Note SAP [1619720]). Sinon, vous pouvez installer les logiciels SAP hello après avoir déployé hello machine virtuelle Azure.

Hello organigramme suivant présente séquence de SAP spécifique de hello d’étapes de déploiement d’une machine virtuelle à partir d’une image personnalisée :

![Organigramme de déploiement de machines virtuelles pour les systèmes SAP à l’aide d’une image de machine virtuelle provenant du Marketplace privé][deployment-guide-figure-300]

#### <a name="create-a-virtual-machine-by-using-hello-azure-portal"></a>Créer un ordinateur virtuel à l’aide de hello portail Azure
toocreate de façon plus simple Hello une machine virtuelle à partir d’une image de disque de géré est à l’aide de hello portail Azure. Pour plus d’informations sur comment toocreate lire une Image de disque gérer, [capturer une image managée d’une machine virtuelle généralisée dans Azure](https://docs.microsoft.com/azure/virtual-machines/windows/capture-image-resource)

1.  Accédez trop<https://ms.portal.azure.com/#blade/HubsExtension/Resources/resourceType/Microsoft.Compute%2Fimages>. Ou, dans hello menus du portail Azure, sélectionnez **Images**.
2.  Image de disques gérés hello sélectionnez voulu toodeploy et cliquez sur **créer un ordinateur virtuel**

vous guide tout au long de la configuration d’ordinateur virtuel de hello requis paramètres toocreate hello Assistant de Hello, en outre tooall requis des ressources, telles que les interfaces réseau et les comptes de stockage. Voici certains exemples de paramètres :

1. **Paramètres de base**:
 * **Nom**: nom hello de ressource de hello (nom de machine virtuelle hello).
 * **Type de disque de machine virtuelle**: sélectionnez le type de disque hello du disque de hello du système d’exploitation. Si vous souhaitez toouse stockage Premium pour vos disques de données, nous recommandons d’utiliser le stockage Premium pour le disque de système d’exploitation hello également.
 * **Nom d’utilisateur et mot de passe** ou **la clé publique SSH**: entrez le nom d’utilisateur hello et le mot de passe utilisateur hello qui est créé lors de la configuration de hello. Pour une machine virtuelle Linux, vous pouvez entrer la clé SSH (Secure Shell) publique hello utiliser toosign dans toohello machine.
 * **Abonnement**: sélectionnez l’abonnement hello que vous souhaitez toouse tooprovision hello machine virtuelle.
 * **Groupe de ressources**: nom hello hello du groupe de ressources pour hello machine virtuelle. Vous pouvez entrer le nom hello un nouveau groupe ou hello du nom de ressource d’un groupe de ressources existe déjà.
 * **Emplacement**: où toodeploy hello nouvel ordinateur virtuel. Si vous souhaitez que le réseau local tooyour tooconnect hello machine virtuelle, veillez à que sélectionner emplacement hello du réseau virtuel hello qui connecte le réseau local de tooyour Azure. Pour plus d’informations, consultez [Mise en réseau Microsoft Azure][planning-guide-microsoft-azure-networking] dans [SAP NetWeaver sur machines virtuelles Azure – Guide de planification et d’implémentation][planning-guide].
2. **Taille**:

     Pour obtenir la liste des types de machine virtuelle pris en charge, consultez la note SAP [1928533]. Assurez-vous que vous sélectionnez le type de machine virtuelle hello correct si vous souhaitez toouse stockage Azure Premium. Tous les types de machine virtuelle ne prennent pas en charge le stockage Premium. Pour plus d’informations, consultez [Stockage : stockage Microsoft Azure et disques de données][planning-guide-storage-microsoft-azure-storage-and-data-disks] et [Stockage Microsoft Azure][planning-guide-azure-premium-storage] dans [SAP NetWeaver sur machines virtuelles Azure – Guide de planification et d’implémentation][planning-guide].

3. **Paramètres**:
  * **Stockage**
    * **Type de disque**: sélectionnez le type de disque hello du disque de hello du système d’exploitation. Si vous souhaitez toouse stockage Premium pour vos disques de données, nous recommandons d’utiliser le stockage Premium pour le disque de système d’exploitation hello également.
    * **Utiliser des disques gérés**: Si vous souhaitez que les disques gérés toouse, sélectionnez Oui. Pour plus d’informations sur les disques gérés, consultez le chapitre [disques gérés] [ planning-guide-managed-disks] dans le guide de planification hello.
  * **Réseau**
    * **Réseau virtuel** et **sous-réseau**: machine virtuelle toointegrate hello votre intranet, le réseau virtuel hello select qui n’est connecté tooyour sur site réseau.
    * **Adresse IP publique**: sélectionnez hello adresse IP publique que vous souhaitez toouse ou entrez les paramètres toocreate une nouvelle adresse IP publique. Vous pouvez utiliser un tooaccess d’adresse IP publique de votre machine virtuelle sur hello Internet. Assurez-vous que vous créez également un ordinateur virtuel de réseau sécurité groupe toohelp un accès sécurisé tooyour.
    * **Groupe de sécurité réseau** : pour plus d’informations, consultez [Contrôler le flux de trafic réseau avec les groupes de sécurité réseau][virtual-networks-nsg].
  * **Extensions**: vous pouvez installer des extensions de machine virtuelle en les ajoutant toohello déploiement. Vous n’avez pas besoin d’extension tooadd dans cette étape. extensions Hello requises pour la prise en charge SAP sont installées ultérieurement. Consultez le chapitre [configurer hello améliorée Extension de surveillance Azure pour SAP] [ deployment-guide-4.5] dans ce guide.
  * **Haute disponibilité**: sélectionnez un ensemble de disponibilité, ou entrez hello paramètres toocreate disponibilité d’une nouvelle valeur. Pour plus d’informations, consultez [Groupes à haute disponibilité Azure][planning-guide-3.2.3].
  * **Surveillance**
    * **Diagnostics de démarrage** : vous pouvez sélectionner **Désactiver** pour le diagnostic de démarrage.
    * **Diagnostics du système d’exploitation invité** : vous pouvez sélectionner **Désactiver** pour le diagnostic de surveillance.

4. **Résumé**:

  Passez en revue vos sélections, puis sélectionnez **OK**.

Votre ordinateur virtuel est déployé dans le groupe de ressources hello que vous avez sélectionné.
#### <a name="create-a-virtual-machine-by-using-a-template"></a>Création d’une machine virtuelle à l’aide d’un modèle
toocreate un déploiement à l’aide d’une image de système d’exploitation privée hello portail Azure, utilisez une des hello suivant modèles SAP. Ces modèles sont publiés dans hello [référentiel GitHub d’azure-démarrage rapide-modèles][azure-quickstart-templates-github]. Vous pouvez également créer une machine virtuelle manuellement à l’aide de [PowerShell][virtual-machines-upload-image-windows-resource-manager].

* [**Modèle de configuration à deux niveaux (une seule machine virtuelle)** (sap-2-tier-user-image)][sap-templates-2-tier-user-image]

  toocreate un système à deux niveaux en utilisant uniquement une machine virtuelle, utilisez ce modèle.
* [**Modèle de configuration à deux niveaux (une seule machine virtuelle) - Image de disque managé** (sap-2-tier-user-image-md)][sap-templates-2-tier-user-image-md]

  toocreate un système à deux couches à l’aide d’un seul ordinateur virtuel et une image de disque gérée, utilisez ce modèle.
* [**Modèle de configuration à trois niveaux (plusieurs machines virtuelles)** (sap-3-tier-user-image)][sap-templates-3-tier-user-image]

  toocreate un système à trois niveaux à l’aide de plusieurs machines virtuelles ou votre propre image de système d’exploitation, utilisez ce modèle.
* [**Modèle de configuration à trois niveaux (plusieurs machines virtuelles) - Image de disque managé** (sap-3-tier-user-image-md)][sap-templates-3-tier-user-image-md]

  toocreate un système à trois niveaux à l’aide de plusieurs machines virtuelles ou votre propre image de système d’exploitation et une image de disque gérée, utilisez ce modèle.

Bonjour portail Azure, entrez hello paramètres pour le modèle de hello suivants :

1. **Paramètres de base**:
  * **Abonnement**: modèle de hello abonnement toouse toodeploy hello.
  * **Groupe de ressources**: modèle de hello ressource groupe toouse toodeploy hello. Vous pouvez créer un nouveau groupe de ressources ou sélectionnez un groupe de ressources existant dans l’abonnement de hello.
  * **Emplacement**: où toodeploy hello modèle. Si vous avez sélectionné un groupe de ressources existant, emplacement hello ce groupe de ressources est utilisé.
2. **Paramètres**:
  * **ID du système SAP**: hello ID système de SAP.
  * **Type de système d’exploitation**: hello du type de système d’exploitation souhaité toodeploy (Windows ou Linux).
  * **Taille du système SAP**: hello taille Hello système SAP.

    nombre de Hello du nouveau système SAP hello fournit. Si vous n’êtes pas sûr du système de hello combien SAP, demandez à votre partenaire technologique SAP ou un intégrateur de système.
  * **Disponibilité du système** (modèle à trois niveaux uniquement) : hello la disponibilité du système.

    Sélectionnez la haute disponibilité (**HA**) si la configuration est adaptée à une installation haute disponibilité. Deux serveurs de base de données et deux serveurs pour l’ASCS sont créés.
  * **Type de stockage** (modèle de couche 2 uniquement) : hello du type de stockage toouse.

    Pour les grands systèmes, nous vous recommandons l’utilisation du stockage Premium Azure. Pour plus d’informations sur les types de stockage, consultez hello suivant des ressources :
      * [Utilisation du stockage SSD Azure Premium pour l’instance de SGBD SAP][2367194]
      * [Stockage Microsoft Azure][dbms-guide-2.3] dans [Déploiement SGBD de machines virtuelles Azure pour SAP NetWeaver][dbms-guide]
      * [Stockage Premium : stockage hautes performances pour les charges de travail des machines virtuelles Azure][storage-premium-storage-preview-portal]
      * [Introduction tooMicrosoft stockage Azure][storage-introduction]
  * **URI du VHD de l’image utilisateur** (modèle d’image de disque non managé uniquement) : hello URI d’image de système d’exploitation privée hello disque dur virtuel, par exemple, https://&lt;accountname >.blob.core.windows.net/vhds/userimage.vhd.
  * **Le compte de stockage d’image utilisateur** (modèle d’image de disque non managé uniquement) : nom hello hello du compte de stockage où est stockée hello privé image de système d’exploitation, par exemple, &lt;accountname > https://&lt;accountname >. BLOB.Core.Windows.NET/vhds/userimage.vhd.
  * **userImageId** (modèle d’image de disque géré uniquement) : Id de hello disques gérés image de toouse
  * **Nom d’utilisateur administrateur** et **mot de passe administrateur**: hello nom d’utilisateur et mot de passe.

    Un nouvel utilisateur est créé pour la signature dans la machine virtuelle de toohello.
  * **Sous-réseau nouveau ou existant** : détermine si un réseau virtuel et un sous-réseau doivent être créés ou si un sous-réseau existant doit être utilisé. Si vous disposez déjà d’un réseau virtuel qui est le réseau local de tooyour connecté, sélectionnez **existant**.
  * **ID de sous-réseau**: hello des ID d’ordinateurs virtuels hello sous-réseau toowhich hello se connecte à. Sélectionnez sous-réseau hello de votre VPN ou ExpressRoute réseau virtuel toouse tooconnect hello tooyour local réseau d’ordinateurs virtuels. ID de Hello ressemble généralement à ceci :

    /subscriptions/&lt;id d’abonnement>/resourceGroups/&lt;nom du groupe de ressources>/providers/Microsoft.Network/virtualNetworks/&lt;nom du réseau virtuel>/subnets/&lt;nom du sous-réseau>

3. **Conditions générales** :  
    Lisez et acceptez les conditions juridiques hello.

4.  Sélectionnez **Achat**.

#### <a name="install-hello-vm-agent-linux-only"></a>Installer hello Agent de machine virtuelle (Linux uniquement)
modèles de hello toouse décrits dans la précédente section de hello, hello Qu'agent Linux doit déjà être installé dans l’image utilisateur hello ou hello déploiement échoue. Téléchargez et installez hello Agent de machine virtuelle dans l’image utilisateur hello, comme décrit dans [télécharger, installer et activer hello Agent de machine virtuelle Azure][deployment-guide-4.4]. Si vous n’utilisez pas les modèles de hello, vous pouvez également installer hello Agent de machine virtuelle plus tard.

#### <a name="join-a-domain-windows-only"></a>Joindre un domaine (Windows uniquement)
Si votre déploiement Azure est instance d’Active Directory ou DNS de local via un réseau VPN site à site Azure ou une Azure ExpressRoute tooan connecté (on parle *intersite* dans [des Machines virtuelles Azure planification et implémentation de SAP NetWeaver][planning-guide]), il est probable que hello machine virtuelle rejoint un domaine local. Pour plus d’informations sur les considérations pour cette étape, consultez [joindre un domaine local du tooan VM (Windows uniquement)][deployment-guide-4.3].

#### <a name="configure-proxy-settings"></a>Configuration des paramètres de proxy
Selon la configuration de votre réseau local, vous devrez peut-être tooset un proxy de hello sur votre machine virtuelle. Si votre machine virtuelle est connectée tooyour du réseau local via un VPN ou ExpressRoute, hello machine virtuelle ne peut pas être en mesure de tooaccess hello Internet et ne seront pas être en mesure de toodownload extensions de hello requis ou collecter des données d’analyse. Pour plus d’informations, consultez [configurer le proxy de hello][deployment-guide-configure-proxy].

#### <a name="configure-monitoring"></a>Configuration de l’analyse
toobe que SAP prend en charge votre environnement, configurez hello Extension de surveillance Azure pour SAP comme décrit dans [configurer hello améliorée Extension de surveillance Azure pour SAP][deployment-guide-4.5]. Vérifier la configuration requise de hello pour la surveillance SAP et la version minimale requise du noyau SAP et de l’Agent hôte SAP, dans les ressources hello dans [les ressources SAP][deployment-guide-2.2].

#### <a name="monitoring-check"></a>Vérification de l’analyse
Vérifiez si l’analyse fonctionne comme décrit dans [Vérifications et résolution des problèmes pour la configuration de l’analyse de bout en bout][deployment-guide-troubleshooting-chapter].


### <a name="a9a60133-a763-4de8-8986-ac0fa33aa8c1"></a>Scénario 3 : Déplacement d’une machine virtuelle locale à l’aide d’un disque dur virtuel Azure non généralisé avec SAP
Dans ce scénario, vous planifiez toomove un système SAP spécifique à partir d’un tooAzure d’environnement sur site. Vous pouvez cela en téléchargeant hello disque dur virtuel qui a hello du système d’exploitation, les fichiers binaires SAP hello, et finalement hello binaires SGBD, ainsi que les disques durs virtuels avec les données de salutation hello et fichiers journaux d’hello SGBD, tooAzure. Contrairement au scénario hello décrit dans [scénario 2 : déploiement d’une machine virtuelle avec une image personnalisée pour SAP][deployment-guide-3.3], dans ce cas, vous conservez le nom d’hôte hello, SID SAP, et des comptes d’utilisateurs SAP Bonjour Azure VM, car ils ont été configuré dans l’environnement local de hello. Vous n’avez pas besoin de toogeneralize hello du système d’exploitation. Ce scénario s’applique plus souvent les scénarios où la partie de hello paysage SAP s’exécute localement et partie de celui-ci s’exécute sur Azure de site toocross.

Dans ce scénario, hello Agent de machine virtuelle est **pas** installé automatiquement pendant le déploiement. Hello Agent de machine virtuelle et hello améliorée Extension de surveillance Azure pour SAP étant requis toorun SAP NetWeaver sur Azure, vous devez toodownload, installation et activer les deux composants manuellement une fois que vous créez la machine virtuelle de hello.

Pour plus d’informations sur hello Agent de machine virtuelle Azure, consultez hello suivant des ressources.

- - -
> ![Windows][Logo_Windows] Windows
>
> [Vue d’ensemble d’agent de machine virtuelle Azure][virtual-machines-windows-agent-user-guide]
>
> ![Linux][Logo_Linux] Linux
>
> [Guide d'utilisateur de l'agent Linux Azure][virtual-machines-linux-agent-user-guide]
>
>

- - -

Hello suivant Organigramme affiche hello séquence d’étapes pour le déplacement d’une machine virtuelle locale à l’aide d’un disque dur virtuel Azure non généralisé :

![Organigramme d’un déploiement de machine virtuelle pour les systèmes SAP à l’aide d’un disque de machine virtuelle][deployment-guide-figure-400]

Si le disque de hello est déjà téléchargé et défini dans Azure (consultez [planification des Machines virtuelles Azure et implémentation pour SAP NetWeaver][planning-guide]), effectuez les tâches hello décrites dans hello ensuite sections suivantes.

#### <a name="create-a-virtual-machine"></a>Création d'une machine virtuelle
toocreate un déploiement à l’aide d’un disque de système d’exploitation privé via hello portail Azure, utilisez le modèle SAP de hello publié Bonjour [référentiel GitHub d’azure-démarrage rapide-modèles][azure-quickstart-templates-github]. Vous pouvez également créer une machine virtuelle manuellement à l’aide de PowerShell.

* [**Modèle de configuration à deux niveaux (une seule machine virtuelle)** (sap-2-tier-user-disk)][sap-templates-2-tier-os-disk]

  toocreate un système à deux niveaux en utilisant uniquement une machine virtuelle, utilisez ce modèle.
* [**Modèle de configuration à deux niveaux (une seule machine virtuelle) - Disque managé** (sap-2-tier-user-disk-md)][sap-templates-2-tier-os-disk-md]

  toocreate un système à deux niveaux en utilisant qu’un seul ordinateur virtuel et un disque géré, utilisez ce modèle.

Bonjour portail Azure, entrez hello paramètres pour le modèle de hello suivants :

1. **Paramètres de base**:
  * **Abonnement**: modèle de hello abonnement toouse toodeploy hello.
  * **Groupe de ressources**: modèle de hello ressource groupe toouse toodeploy hello. Vous pouvez créer un nouveau groupe de ressources ou sélectionnez un groupe de ressources existant dans l’abonnement de hello.
  * **Emplacement**: où toodeploy hello modèle. Si vous avez sélectionné un groupe de ressources existant, emplacement hello ce groupe de ressources est utilisé.
2. **Paramètres**:
  * **ID du système SAP**: hello ID système de SAP.
  * **Type de système d’exploitation**: hello du type de système d’exploitation souhaité toodeploy (Windows ou Linux).
  * **Taille du système SAP**: hello taille Hello système SAP.

    nombre de Hello du nouveau système SAP hello fournit. Si vous n’êtes pas sûr du système de hello combien SAP, demandez à votre partenaire technologique SAP ou un intégrateur de système.
  * **Type de stockage** (modèle de couche 2 uniquement) : hello du type de stockage toouse.

    Pour les grands systèmes, nous vous recommandons l’utilisation du stockage Premium Azure. Pour plus d’informations sur les types de stockage, consultez hello suivant des ressources :
      * [Utilisation du stockage SSD Azure Premium pour l’instance de SGBD SAP][2367194]
      * [Stockage Microsoft Azure][dbms-guide-2.3] dans [Déploiement SGBD de machines virtuelles Azure pour SAP NetWeaver][dbms-guide]
      * [Stockage Premium : stockage hautes performances pour les charges de travail des machines virtuelles Azure][storage-premium-storage-preview-portal]
      * [Introduction tooMicrosoft stockage Azure][storage-introduction]
  * **URI VHD du disque de système d’exploitation** (modèle de disque non managé uniquement) : hello URI de disque du système d’exploitation hello privé, par exemple, https://&lt;accountname >.blob.core.windows.net/vhds/osdisk.vhd.
  * **Id de disque géré de disque du système d’exploitation** (modèle de disque géré uniquement) : hello Id Hello disque de système d’exploitation de disque géré, /subscriptions/92d102f7-81a5-4df7-9877-54987ba97dd9/resourceGroups/group/providers/Microsoft.Compute/disks/WIN
  * **Sous-réseau nouveau ou existant** : détermine si un réseau virtuel et un sous-réseau doivent être créés ou si un sous-réseau existant doit être utilisé. Si vous disposez déjà d’un réseau virtuel qui est le réseau local de tooyour connecté, sélectionnez **existant**.
  * **ID de sous-réseau**: hello des ID d’ordinateurs virtuels hello sous-réseau toowhich hello se connecte à. Sélectionnez sous-réseau hello de votre Azure ExpressRoute ou VPN réseau virtuel toouse tooconnect hello machine virtuelle tooyour sur réseau local. ID de Hello ressemble généralement à ceci :

    /subscriptions/&lt;id d’abonnement>/resourceGroups/&lt;nom du groupe de ressources>/providers/Microsoft.Network/virtualNetworks/&lt;nom du réseau virtuel>/subnets/&lt;nom du sous-réseau>

3. **Conditions générales** :  
    Lisez et acceptez les conditions juridiques hello.

4.  Sélectionnez **Achat**.

#### <a name="install-hello-vm-agent"></a>Installer l’Agent de machine virtuelle de hello
hello toouse modèles décrits dans hello la section précédente, hello Agent de machine virtuelle doit être installé sur le disque de hello du système d’exploitation ou hello va échouer. Téléchargez et installez hello Agent de machine virtuelle Bonjour machine virtuelle, comme décrit dans [télécharger, installer et activer hello Agent de machine virtuelle Azure][deployment-guide-4.4].

Si vous n’utilisez pas les modèles de hello décrits dans hello précédant la section, vous pouvez également installer par la suite hello Agent de machine virtuelle.

#### <a name="join-a-domain-windows-only"></a>Joindre un domaine (Windows uniquement)
Si votre déploiement Azure est instance d’Active Directory ou DNS de locale via un réseau VPN site à site Azure ou une ExpressRoute tooan connecté (on parle *intersite* dans [planification des Machines virtuelles Azure et l’implémentation de SAP NetWeaver][planning-guide]), il est probable que hello machine virtuelle rejoint un domaine local. Pour plus d’informations sur les considérations pour cette tâche, consultez [joindre un domaine local du tooan VM (Windows uniquement)][deployment-guide-4.3].

#### <a name="configure-proxy-settings"></a>Configuration des paramètres de proxy
Selon la configuration de votre réseau local, vous devrez peut-être tooset un proxy de hello sur votre machine virtuelle. Si votre machine virtuelle est connectée tooyour du réseau local via un VPN ou ExpressRoute, hello machine virtuelle ne peut pas être en mesure de tooaccess hello Internet et ne seront pas être en mesure de toodownload extensions de hello requis ou collecter des données d’analyse. Pour plus d’informations, consultez [configurer le proxy de hello][deployment-guide-configure-proxy].

#### <a name="configure-monitoring"></a>Configuration de l’analyse
toobe que SAP prend en charge votre environnement, configurez hello Extension de surveillance Azure pour SAP comme décrit dans [configurer hello améliorée Extension de surveillance Azure pour SAP][deployment-guide-4.5]. Vérifier la configuration requise de hello pour la surveillance SAP et la version minimale requise du noyau SAP et de l’Agent hôte SAP, dans les ressources hello dans [les ressources SAP][deployment-guide-2.2].

#### <a name="monitoring-check"></a>Vérification de l’analyse
Vérifiez si l’analyse fonctionne comme décrit dans [Vérifications et résolution des problèmes pour la configuration de l’analyse de bout en bout][deployment-guide-troubleshooting-chapter].

## <a name="update-hello-monitoring-configuration-for-sap"></a>Mettre à jour la configuration de la surveillance hello pour SAP
Mise à jour de la configuration d’analyse hello SAP dans un des hello les scénarios suivants :
* équipe Microsoft/SAP commune de Hello étend les capacités d’analyse de hello et demande des compteurs plus ou moins.
* Microsoft introduit une nouvelle version de hello infrastructure Azure sous-jacente qui remet hello données d’analyse, et hello Extension de surveillance améliorée Azure pour SAP besoins toobe adaptée toothose modifications.
* Montage de disques de données supplémentaires tooyour machine virtuelle Azure ou supprimer un disque de données. Dans ce scénario, mettez à jour collection hello de données liées au stockage. Modifier votre configuration en ajoutant ou supprimant des points de terminaison ou en assignant IP adresses tooa VM n’affecte pas les configuration d’analyse hello.
* Vous modifiez hello taille de votre machine virtuelle Azure, par exemple, à partir de la taille A5 tooany autre taille de machine virtuelle.
* Vous ajoutez de nouveau tooyour d’interfaces réseau Azure VM.

tooupdate paramètres, hello de mise à jour en suivant les hello infrastructure d’analyse de surveillance des étapes dans [configurer hello améliorée Extension de surveillance Azure pour SAP][deployment-guide-4.5].

## <a name="detailed-tasks-for-sap-software-deployment"></a>Détail des tâches pour le déploiement de logiciels SAP
Cette section détaille les étapes permettant d’effectuer des tâches spécifiques dans le processus de configuration et de déploiement hello.

### <a name="604bcec2-8b6e-48d2-a944-61b0f5dee2f7"></a>Déploiement d’applets de commande Azure PowerShell
1.  Accédez trop[téléchargements Microsoft Azure](https://azure.microsoft.com/downloads/).
2.  Sous **Outils de ligne de commande**, sous **PowerShell**, sélectionnez **Installation Windows**.
3.  Dans la boîte de dialogue Gestionnaire de téléchargement Microsoft hello, pour le fichier hello téléchargé (par exemple, WindowsAzurePowershellGet.3f.3f.3fnew.exe), sélectionnez **exécuter**.
4.  toorun Microsoft Web Platform Installer (Web PI Microsoft), sélectionnez **Oui**.
5.  Une page ressemblant à ceci s’affiche :

  ![Page d’installation pour les applets de commande Azure PowerShell][deployment-guide-figure-500]<a name="figure-5"></a>

6.  Sélectionnez **installer**, puis acceptez le contrat de licence logiciel Microsoft hello.
7.  Powershell est installé. Sélectionnez **Terminer** Assistant d’installation tooclose hello.

Vérifiez fréquemment les mises à jour toohello applets de commande PowerShell, généralement mises à jour de chaque mois. Hello toocheck de façon plus simple pour les mises à jour est hello toodo précédant les étapes d’installation, page d’installation toohello indiqué à l’étape 5. nombre de date et version de version des applets de commande hello Hello est inclus dans la page hello indiqué à l’étape 5. Sauf indication contraire dans la Note SAP [1928533] ou la Note SAP [2015553], nous vous conseillons de travailler avec la version la plus récente des applets de commande PowerShell Azure hello.

version de hello toocheck Hello applets de commande Azure PowerShell qui sont installés sur votre ordinateur, exécutez cette commande PowerShell :
```powershell
(Get-Module AzureRm.Compute).Version
```
résultat de Hello ressemble à ceci :

![Résultat du contrôle de version de l’applet de commande Azure PowerShell][deployment-guide-figure-600]
<a name="figure-6"></a>

Si hello applet de commande Azure version installée sur votre ordinateur est hello actuel, hello première page de l’Assistant installation hello indique qu’elle en ajoutant **(installé)** toohello nom du produit (voir hello suivant capture d’écran). Vos applets de commande Azure PowerShell sont à jour. tooclose hello Assistant installation, sélectionnez **Exit**.

![Page d’installation des applets de commande Azure PowerShell indiquant la version la plus récente que hello d’applets de commande Azure PowerShell sont installés.][deployment-guide-figure-700]
<a name="figure-7"></a>

### <a name="1ded9453-1330-442a-86ea-e0fd8ae8cab3"></a>Déploiement de l’interface de ligne de commande Azure
1.  Accédez trop[téléchargements Microsoft Azure](https://azure.microsoft.com/downloads/).
2.  Sous **des outils de ligne de commande**, sous **interface de ligne de commande Azure**, sélectionnez hello **installer** lien à votre système d’exploitation.
3.  Dans la boîte de dialogue Gestionnaire de téléchargement Microsoft hello, pour le fichier hello téléchargé (par exemple, WindowsAzureXPlatCLI.3f.3f.3fnew.exe), sélectionnez **exécuter**.
4.  toorun Microsoft Web Platform Installer (Web PI Microsoft), sélectionnez **Oui**.
5.  Une page ressemblant à ceci s’affiche :

  ![Page d’installation pour les applets de commande Azure PowerShell][deployment-guide-figure-500]<a name="figure-5"></a>

6.  Sélectionnez **installer**, puis acceptez le contrat de licence logiciel Microsoft hello.
7.  L’interface de ligne de commande Azure est installée. Sélectionnez **Terminer** Assistant d’installation tooclose hello.

Vérifiez fréquemment les mises à jour tooAzure CLI, généralement mis à jour de chaque mois. Hello toocheck de façon plus simple pour les mises à jour est hello toodo précédant les étapes d’installation, page d’installation toohello indiqué à l’étape 5.

version de hello toocheck de CLI d’Azure qui est installé sur votre ordinateur, exécutez la commande suivante :
```
azure --version
```

résultat de Hello ressemble à ceci :

![Résultat du contrôle de la version de l’interface de ligne de commande Azure][deployment-guide-figure-760]
<a name="0ad010e6-f9b5-4c21-9c09-bb2e5efb3fda"></a>

### <a name="31d9ecd6-b136-4c73-b61e-da4a29bbc9cc"></a>Joindre un domaine local du tooan VM (Windows uniquement)
Si vous déployez des machines virtuelles SAP dans un scénario de coexistence, où locale Active Directory et DNS ont été étendues dans Azure, il est probable que les machines virtuelles de hello joignez un domaine local. Hello détaillées étapes toojoin un domaine local de tooan VM et hello toobe des logiciels supplémentaires requis pour un membre d’un domaine local, varie en fonction du client. En règle générale, toojoin un tooan de machine virtuelle locale domaine, vous devez tooinstall des logiciels supplémentaires, telles que les logiciels anti-programme malveillant et les logiciels de sauvegarde ou de surveillance.

Dans ce scénario, vous devez également toomake que si les paramètres du proxy Internet sont forcés lorsqu’une machine virtuelle rejoint un domaine dans votre environnement, Windows hello le compte système Local (S-1-5-18) Bonjour machine virtuelle invitée a hello mêmes paramètres de proxy. option la plus simple Hello est un proxy de hello tooforce à l’aide d’une stratégie de groupe qui s’applique toosystems dans le domaine de hello de domaine.

### <a name="c7cbb0dc-52a4-49db-8e03-83e7edc2927d"></a>Télécharger, installer et activer hello Agent de machine virtuelle Azure
Pour les ordinateurs virtuels qui sont déployés à partir d’une image de système d’exploitation qui n’est pas généralisée (par exemple, une image qui ne provient pas de l’outil de préparation système Windows, ou de sysprep, hello), vous devez toomanually télécharger, installer et activer hello Agent de machine virtuelle Azure.

Si vous déployez une machine virtuelle à partir de hello Azure Marketplace, cette étape n’est pas requise. Images à partir de hello Azure Marketplace ont déjà hello Agent de machine virtuelle Azure.

#### <a name="b2db5c9a-a076-42c6-9835-16945868e866"></a>Windows
1.  Vous pouvez télécharger hello Agent de machine virtuelle Azure :
  1.  Télécharger hello [package de programme d’installation de l’Agent de machine virtuelle Azure](https://go.microsoft.com/fwlink/?LinkId=394789).
  2.  Stocker le package MSI de l’Agent de machine virtuelle de hello localement sur un ordinateur personnel ou un serveur.
2.  Installez hello Agent de machine virtuelle Azure :
  1.  Se connecter toohello déployé la machine virtuelle Azure à l’aide du protocole RDP (Remote Desktop).
  2.  Ouvrez une fenêtre de l’Explorateur Windows sur la machine virtuelle de hello et le répertoire cible hello Sélectionnez fichier MSI de hello Hello Agent de machine virtuelle.
  3.  Faire glisser un fichier MSI de programme d’installation de l’Agent de machine virtuelle Azure hello du répertoire cible toohello ordinateur locales/serveur Hello Agent de machine virtuelle sur hello machine virtuelle.
  4.  Double-cliquez sur fichier MSI hello hello machine virtuelle.
3.  Pour les machines virtuelles sont les domaines joints tooon local, assurez-vous que les paramètres de proxy Internet finaux s’appliquent également compte de système Local Windows toohello (S-1-5-18) Bonjour machine virtuelle, comme décrit dans [configurer le proxy de hello] [ deployment-guide-configure-proxy]. Hello Agent de machine virtuelle s’exécute dans ce contexte et doit être toobe en mesure de tooconnect tooAzure.

Aucune interaction utilisateur n’est requise tooupdate hello Agent de machine virtuelle Azure. Hello Agent de machine virtuelle est automatiquement mis à jour et ne nécessite pas un redémarrage de l’ordinateur virtuel.

#### <a name="6889ff12-eaaf-4f3c-97e1-7c9edc7f7542"></a>Linux
Utilisez hello suivant commandes tooinstall hello Agent de machine virtuelle Linux :

* **SUSE Linux Enterprise Server (SLES)**

  ```
  sudo zypper install WALinuxAgent
  ```

* **Red Hat Enterprise Linux (RHEL) ou Oracle Linux**

  ```
  sudo yum install WALinuxAgent
  ```

Si l’agent de hello est déjà installé, tooupdate hello Azure Linux Agent, procédez comme hello étapes décrites dans [hello de mise à jour le Linux Agent Azure sur une machine virtuelle toohello dernière version à partir de GitHub][virtual-machines-linux-update-agent].

### <a name="baccae00-6f79-4307-ade4-40292ce4e02d"></a>Configurer le proxy de hello
Hello étapes proxy de hello tooconfigure dans Windows sont différents à partir de la façon de hello que vous configurez le proxy de hello dans Linux.

#### <a name="windows"></a>Windows
Paramètres de proxy doivent être configurées correctement pour hello compte système Local tooaccess hello Internet. Si vos paramètres de proxy ne sont pas définies par la stratégie de groupe, vous pouvez configurer les paramètres de hello pour hello compte système Local.

1. Accédez trop**Démarrer**, entrez **gpedit.msc**, puis sélectionnez **entrée**.
2. Sélectionnez **Configuration ordinateur** > **Modèles d’administration** > **Composants Windows** > **Internet Explorer**. Assurez-vous que ce paramètre hello **rendre le proxy de paramètres par ordinateur (plutôt que par l’utilisateur)** est désactivé ou non configuré.
3. Dans **le panneau de configuration**, accédez trop**Centre réseau et partage** > **Options Internet**.
4. Sur hello **connexions** onglet, sélectionnez hello **paramètres LAN** bouton.
5. Désactivez hello **détecter automatiquement les paramètres** case à cocher.
6. Sélectionnez hello **utiliser un serveur proxy pour votre réseau local** case à cocher, puis entrez l’adresse du proxy hello et le port.
7. Sélectionnez hello **avancé** bouton.
8. Bonjour **Exceptions** , entrez l’adresse IP de hello **168.63.129.16**. Sélectionnez **OK**.

#### <a name="linux"></a>Linux
Configurer le proxy correcte de hello dans le fichier de configuration hello Hello Agent invité Microsoft Azure, qui se trouve dans \\etc.\\waagent.conf.

Hello du jeu de paramètres suivants :

1.  **Hôte proxy HTTP**. Par exemple, le définir trop**proxy.corp.local**.
  ```
  HttpProxy.Host=<proxy host>

  ```
2.  **Port proxy HTTP**. Par exemple, le définir trop**80**.
  ```
  HttpProxy.Port=<port of hello proxy host>

  ```
3.  Redémarrez l’agent de hello.

  ```
  sudo service waagent restart
  ```

Hello des paramètres de proxy dans \\etc.\\waagent.conf s’appliquent également des extensions de machine virtuelle toohello requis. Si vous souhaitez toouse hello référentiels Azure, assurez-vous que les référentiels toothese hello le trafic ne va pas via votre intranet local. Si vous avez créé défini par l’utilisateur itinéraires tooenable le tunneling forcé, assurez-vous que vous ajoutez un itinéraire qui achemine les référentiels toohello trafic directement toohello Internet et non par le biais de votre connexion VPN de site à site.

* **SLES**

  Vous devez également les itinéraires tooadd sur les adresses IP de hello répertoriées dans \\etc.\\regionserverclnt.cfg. Hello figure ci-dessous illustre un exemple :

  ![Tunneling forcé][deployment-guide-figure-50]


* **RHEL**

  Vous devez également les itinéraires tooadd sur les adresses IP de hello des hôtes de hello répertoriées dans \\etc.\\yum.repos.d\\rhui équilibreurs de charge. Pour obtenir un exemple, consultez hello précédant figure.

* **Oracle Linux**

  Il n’existe aucun référentiel pour Oracle Linux sur Azure. Vous devez tooconfigure votre propre référentiels pour Oracle Linux ou utilisez les référentiels publics hello.

Pour plus d’informations sur les itinéraires définis par l’utilisateur, consultez [Itinéraires définis par l’utilisateur et transfert IP][virtual-networks-udr-overview].

### <a name="d98edcd3-f2a1-49f7-b26a-07448ceb60ca"></a>Configurer hello améliorée Extension de surveillance Azure pour SAP
Lorsque vous avez préparé hello machine virtuelle comme décrit dans [des scénarios de déploiement de machines virtuelles pour SAP sur Azure][deployment-guide-3], hello Agent de machine virtuelle Azure est installé sur l’ordinateur virtuel de hello. étape suivante de Hello est toodeploy hello améliorée Extension de surveillance Azure pour SAP, qui est disponible dans hello référentiel d’extensions Azure dans les centres de données Azure hello global. Pour plus d’informations, consultez [SAP NetWeaver sur machines virtuelles Azure – Guide de planification et d’implémentation][planning-guide-9.1].

Vous pouvez utiliser tooinstall PowerShell ou CLI d’Azure et configurer hello améliorée Extension de surveillance Azure pour SAP. extension de hello tooinstall sur Linux VM de Windows à l’aide d’un ordinateur Windows, consultez [Azure PowerShell][deployment-guide-4.5.1]. extension de hello tooinstall sur un VM Linux à l’aide d’un ordinateur Linux, consultez [CLI d’Azure][deployment-guide-4.5.2].

#### <a name="987cf279-d713-4b4c-8143-6b11589bb9d4"></a>Azure PowerShell pour les machines virtuelles Linux et Windows
tooinstall hello améliorée Extension de surveillance Azure pour SAP à l’aide de PowerShell :

1. Assurez-vous que vous avez installé la version la plus récente de l’applet de commande PowerShell Azure hello hello. Pour plus d’informations, consultez [Déploiement d’applets de commande Azure PowerShell][deployment-guide-4.1].  
2. Exécutez hello suivant l’applet de commande PowerShell.
    Pour afficher la liste des environnements disponibles, exécutez `commandlet Get-AzureRmEnvironment` . Si vous souhaitez toouse global Azure, votre environnement est **cloud Azure**. Pour Azure en Chine, sélectionnez **AzureChinaCloud**.

    ```powershell
    $env = Get-AzureRmEnvironment -Name <name of hello environment>
    Login-AzureRmAccount -Environment $env
    Set-AzureRmContext -SubscriptionName <subscription name>

    Set-AzureRmVMAEMExtension -ResourceGroupName <resource group name> -VMName <virtual machine name>
    ```

Une fois que vous entrez des données de votre compte et identifiez hello machine virtuelle Azure, script de hello déploie les extensions hello requis et Active les fonctionnalités de hello requis. Ceci peut prendre plusieurs minutes.
Pour plus d’informations sur `Set-AzureRmVMAEMExtension`, consultez [Set-AzureRmVMAEMExtension][msdn-set-azurermvmaemextension].

![Exécution réussie de l’applet de commande Azure spécifique à SAP Set-AzureRmVMAEMExtension][deployment-guide-figure-900]

Hello `Set-AzureRmVMAEMExtension` tous les hôtes tooconfigure étapes hello surveillance pour SAP fait de configuration.

sortie du script Hello inclut hello informations suivantes :

* Confirmation que pour les disques de hello du système d’exploitation et tous les autres disques de données d’analyse a été configuré.
* deux messages de type Hello confirmer configuration hello des métriques de stockage pour un compte de stockage.
* Une ligne de sortie permet hello l’état de mise à jour réelle de hello hello configuration des analyses.
* Une autre ligne de sortie confirme que la configuration hello a été déployée ou mis à jour.
* Hello dernière ligne de sortie est informative. Il montre les options de test configuration de la surveillance hello.
* toocheck par toutes les étapes de surveillance améliorée Azure ont été correctement exécutées et que hello Infrastructure Azure fournit les données nécessaires hello, procédez avec vérification de la disponibilité hello pour hello améliorée Extension de surveillance Azure pour SAP, comme décrit dans [Vérification de la disponibilité de surveillance améliorée Azure pour SAP][deployment-guide-5.1].
* Patientez 15 à 30 minutes pour que les données de Diagnostics Azure toocollect hello.

#### <a name="408f3779-f422-4413-82f8-c57a23b4fc2f"></a>Interface de ligne de commande Azure pour machines virtuelles Linux
tooinstall hello améliorée Extension de surveillance Azure pour SAP à l’aide d’Azure CLI :

1. Installez Azure CLI 1.0, comme décrit dans [installation Bonjour Azure CLI 1.0][azure-cli].
2. Connectez-vous à votre compte Azure :

  ```
  azure login
  ```

3. Basculez en mode de gestionnaire de ressources tooAzure :

  ```
  azure config mode arm
  ```

4. Activez la surveillance Azure améliorée :

  ```
  azure vm enable-aem <resource-group-name> <vm-name>
  ```

5. Vérifiez que cette Extension de surveillance améliorée Azure hello est active sur hello Azure Linux VM. Vérification hello indique si le fichier \\var\\lib\\AzureEnhancedMonitor\\PerfCounters existe. Si elle existe, à l’invite de commandes, exécutez cette commande toodisplay les informations collectées par hello moniteur renforcée de Windows Azure :
```
cat /var/lib/AzureEnhancedMonitor/PerfCounters
```

sortie de Hello ressemble à ceci :
```
2;cpu;Current Hw Frequency;;0;2194.659;MHz;60;1444036656;saplnxmon;
2;cpu;Max Hw Frequency;;0;2194.659;MHz;0;1444036656;saplnxmon;
…
…
```

## <a name="564adb4f-5c95-4041-9616-6635e83a810b"></a>Vérifications et résolution des problèmes pour la configuration de l’analyse de bout en bout
Après avoir déployé votre machine virtuelle Azure et configurer d’infrastructure de surveillance Azure pertinentes hello, vérifiez si tous les composants hello Hello Extension de surveillance améliorée Azure fonctionnent comme prévu.

Exécuter la vérification de la disponibilité hello pour hello améliorée Extension de surveillance Azure pour SAP comme décrit dans [vérification de disponibilité pour hello améliorée Extension de surveillance Azure pour SAP][deployment-guide-5.1]. Si tous les résultats de la vérification de disponibilité sont positifs et que tous les compteurs de performances ont le statut OK, la surveillance Azure a été correctement configurée. Vous pouvez poursuivre installation Bonjour de l’Agent hôte SAP comme décrit dans les Notes SAP hello [les ressources SAP][deployment-guide-2.2]. Si la vérification de la disponibilité hello indique que les compteurs sont manquants, exécutez le contrôle d’intégrité de hello pour hello infrastructure de surveillance Azure, comme décrit dans [contrôle d’intégrité pour la configuration d’infrastructure de surveillance Azure] [ deployment-guide-5.2]. Pour obtenir davantage d’options de résolution des problèmes, consultez [Résolution des problèmes d’analyse Azure pour SAP][deployment-guide-5.3].

### <a name="bb61ce92-8c5c-461f-8c53-39f5e5ed91f2"></a>Vérification de disponibilité pour hello améliorée Extension de surveillance Azure pour SAP
Cette vérification permet de s’assurer que toutes les métriques de performances qui s’affichent à l’intérieur de votre application SAP sont fournies par hello sous-jacent d’infrastructure de surveillance Azure.

#### <a name="run-hello-readiness-check-on-a-windows-vm"></a>Exécuter la vérification de la disponibilité hello sur une machine virtuelle Windows

1.  Connectez-vous à toohello machine virtuelle Azure (à l’aide d’un compte d’administrateur n’est pas nécessaire).
2.  Ouvrez une fenêtre d’invite de commandes.
3.  À l’invite de commandes hello modifier le dossier d’installation de toohello d’hello active de hello améliorée Extension de surveillance Azure pour SAP : c :\\Packages\\plug-ins\\ Microsoft.AzureCAT.AzureEnhancedMonitoring.AzureCATExtensionHandler\\&lt;version >\\supprimer

  Hello *version* toohello de chemin d’accès hello extension de surveillance peut varier. Si vous voyez les dossiers de plusieurs versions de hello analyse d’extension dans le dossier d’installation Bonjour, vérifiez la configuration de service Windows de AzureEnhancedMonitoring, de hello hello et puis commutateur toohello dossier indiqué sous la forme *tooexecutable de chemin d’accès* .

  ![Propriétés de l’exécution du service hello améliorée Extension de surveillance Azure pour SAP][deployment-guide-figure-1000]

4.  À l’invite de commandes hello exécuter **azperflib.exe** sans aucun paramètre.

  > [!NOTE]
  > Azperflib.exe s’exécute dans une boucle et met à jour les compteurs de hello collectée toutes les 60 secondes. boucle de hello tooend, fenêtre d’invite de commandes hello fermer.
  >
  >

Si hello Qu'extension de surveillance améliorée Azure n’est pas installée ou hello AzureEnhancedMonitoring service ne fonctionne pas, extension de hello n'a pas été configurée correctement. Pour obtenir des informations détaillées sur la façon dont toodeploy hello extension, consultez [dépannage hello infrastructure de surveillance Azure pour SAP][deployment-guide-5.3].

##### <a name="check-hello-output-of-azperflibexe"></a>Vérifier la sortie hello de azperflib.exe
La sortie de azperflib.exe indique tous les compteurs de performances Azure remplis pour SAP. Bas hello de hello liste de compteurs collectés, un indicateur de résumé et d’intégrité afficher l’état de hello de surveillance Azure.

![Sortie du contrôle d’intégrité effectué avec azperflib.exe indiquant l’absence de problèmes][deployment-guide-figure-1100]
<a name="figure-11"></a>

Vérifiez le résultat de hello pour hello **total de compteurs** sortie, qui est signalée comme vide et pour **l’état d’intégrité**, comme illustré dans hello précédant figure.

Interpréter les valeurs résultantes hello comme suit :

| Résultats du fichier exécutable azperflib.exe | État d’intégrité de l’analyse Azure |
| --- | --- |
| **Appels de l’API - non disponibles** | Les compteurs ne sont pas disponibles peuvent être une configuration de machine virtuelle toohello non applicable ou d’erreurs. Voir **État d’intégrité**. |
| **Nombre total de compteurs : vide** |Hello suivant deux compteurs de stockage Azure peut être vide : <ul><li>Stockage Lecture Op Latence Serveur msec</li><li>Stockage Lecture Op Latence E2E msec</li></ul>Tous les autres compteurs doivent contenir des valeurs. |
| **État d’intégrité** |Uniquement OK si l’état renvoyé est **OK**. |
| **Diagnostics** |Informations détaillées sur l’état d’intégrité. |

Si hello **l’état d’intégrité** valeur n’est pas **OK**, suivez les instructions de hello dans [contrôle d’intégrité pour la configuration d’infrastructure de surveillance Azure] [ deployment-guide-5.2].

#### <a name="run-hello-readiness-check-on-a-linux-vm"></a>Exécuter la vérification de la disponibilité hello sur un VM Linux

1.  Se connecter toohello Machine virtuelle Azure à l’aide de SSH.

2.  Vérifiez la sortie hello Hello Extension de surveillance Azure améliorée.

  a.  Exécutez `more /var/lib/AzureEnhancedMonitor/PerfCounters`.

   **Résultat attendu** : renvoie la liste des compteurs de performances. fichier de Hello ne doit pas être vide.

 b. Exécutez `cat /var/lib/AzureEnhancedMonitor/PerfCounters | grep Error`.

   **Résultat attendu**: retourne une ligne où les erreurs hello sont **aucun**, par exemple, **3 ; Configuration ; Erreur ; 0 ; 0 ; Aucun ; 0 ; 1456416792 ; tst-servercs ;**

  c. Exécutez `more /var/lib/AzureEnhancedMonitor/LatestErrorRecord`.

    **Résultat attendu** : revient vide ou n’existe pas.

Si hello cocher précédente n’a pas réussi, exécutez ces contrôles supplémentaires :

1.  Assurez-vous que waagent hello est installé et activé.

  a.  Exécutez `sudo ls -al /var/lib/waagent/`.

      **Résultat attendu**: répertorie le contenu du répertoire de waagent hello hello.

  b.  Exécutez `ps -ax | grep waagent`.

   **Résultat attendu** : affiche une entrée similaire à : `python /usr/sbin/waagent -daemon`

3.   Assurez-vous que cette Extension de surveillance améliorée Azure hello est installé et en cours d’exécution.

  a.  Exécutez `sudo sh -c 'ls -al /var/lib/waagent/Microsoft.OSTCExtensions.AzureEnhancedMonitorForLinux-*/'`.

    **Résultat attendu**: répertorie le contenu du répertoire d’Extension de surveillance améliorée Azure hello hello.

  b. Exécutez `ps -ax | grep AzureEnhanced`.

     **Résultat attendu** : affiche une entrée similaire à : `python /var/lib/waagent/Microsoft.OSTCExtensions.AzureEnhancedMonitorForLinux-2.0.0.2/handler.py daemon`

3. Installer l’Agent hôte SAP comme décrit dans la Note SAP [1031096]et vérifiez la sortie hello de `saposcol`.

  a.  Exécutez `/usr/sap/hostctrl/exe/saposcol -d`.

  b.  Exécutez `dump ccm`.

  c.  Vérifiez si hello **accès d’analyse Virtualization_Configuration\Enhanced** métrique est **true**.

Si vous avez déjà installé un serveur d’applications ABAP NetWeaver SAP, ouvrez la transaction ST06 et regardez si l’analyse améliorée est activée.

Si une de ces vérifications échoue et pour obtenir des informations détaillées sur la façon dont tooredeploy hello extension, consultez [dépannage hello infrastructure de surveillance Azure pour SAP][deployment-guide-5.3].

### <a name="e2d592ff-b4ea-4a53-a91a-e5521edb6cd1"></a>Le contrôle d’intégrité pour hello configuration d’infrastructure de surveillance Azure
Si certains des hello données d’analyse n’est pas remis correctement, comme indiqué par le test de hello décrit dans [vérification de la disponibilité de surveillance améliorée Azure pour SAP][deployment-guide-5.1], hello exécutez `Test-AzureRmVMAEMExtension` toocheck de l’applet de commande Si hello Azure analyse d’infrastructure et hello extension de surveillance pour SAP est configuré correctement.

1.  Assurez-vous que vous avez installé la version la plus récente de l’applet de commande PowerShell de Azure hello hello comme décrit dans [applets de commande de déploiement d’Azure PowerShell][deployment-guide-4.1].
2.  Exécutez hello suivant l’applet de commande PowerShell. Pour obtenir la liste des environnements disponibles, exécutez l’applet de commande hello `Get-AzureRmEnvironment`. Sélectionnez d’Azure, global toouse hello **cloud Azure** environnement. Pour Azure en Chine, sélectionnez **AzureChinaCloud**.
  ```powershell
  $env = Get-AzureRmEnvironment -Name <name of hello environment>
  Login-AzureRmAccount -Environment $env
  Set-AzureRmContext -SubscriptionName <subscription name>
  Test-AzureRmVMAEMExtension -ResourceGroupName <resource group name> -VMName <virtual machine name>
  ```

3.  Entrez les données de votre compte et identifier hello machine virtuelle Azure.

  ![Page d’entrée de l’applet de commande Azure spécifique à SAP Test-VMConfigForSAP_GUI][deployment-guide-figure-1200]

4. configuration de hello Hello script tests de la machine virtuelle de hello que vous sélectionnez.

  ![Sortie du test réussi de hello infrastructure de surveillance Azure pour SAP][deployment-guide-figure-1300]

Assurez-vous que le résultat de chaque vérification d’intégrité est **OK**. Si des vérifications n’affichent pas **OK**, exécutez l’applet de commande de mise à jour hello comme décrit dans [configurer hello améliorée Extension de surveillance Azure pour SAP][deployment-guide-4.5]. Attendez 15 minutes, et les vérifications de répétition hello décrites dans [vérification de la disponibilité de surveillance améliorée Azure pour SAP] [ deployment-guide-5.1] et [contrôle d’intégrité pour la Configuration de l’Infrastructure d’analyse Azure] [deployment-guide-5.2]. Si les vérifications hello indiquent toujours un problème avec certains ou tous les compteurs, consultez [dépannage hello infrastructure de surveillance Azure pour SAP][deployment-guide-5.3].

### <a name="fe25a7da-4e4e-4388-8907-8abc2d33cfd8"></a>Résolution des problèmes de hello infrastructure de surveillance Azure pour SAP

#### <a name="windowslogowindows-azure-performance-counters-do-not-show-up-at-all"></a>![Windows][Logo_Windows] Les compteurs de performances Azure ne s’affichent pas
Hello service AzureEnhancedMonitoring Windows collecte les mesures de performances dans Azure. Si le service de hello n’a pas été installé correctement ou si elle n’est pas en cours d’exécution dans votre machine virtuelle, aucune mesure de performance ne peut être collectés.

##### <a name="hello-installation-directory-of-hello-azure-enhanced-monitoring-extension-is-empty"></a>répertoire d’installation Hello Hello Extension de surveillance améliorée Azure est vide

###### <a name="issue"></a>Problème
répertoire d’installation Hello C:\\Packages\\plug-ins\\Microsoft.AzureCAT.AzureEnhancedMonitoring.AzureCATExtensionHandler\\&lt;version >\\dépôt est vide.

###### <a name="solution"></a>Solution
extension de Hello n’est pas installée. Déterminez s’il s’agit d’un problème de proxy (comme décrit précédemment). Vous devrez peut-être machine de hello toorestart ou réexécuter hello `Set-AzureRmVMAEMExtension` script de configuration.

##### <a name="service-for-azure-enhanced-monitoring-does-not-exist"></a>Le service d’analyse Azure améliorée n’existe pas.

###### <a name="issue"></a>Problème
Hello service AzureEnhancedMonitoring Windows n’existe pas.

La sortie de azperflib.exe génère une erreur :

![L’exécution de azperflib.exe indique que le service hello Hello Extension de surveillance améliorée Azure pour SAP n’exécute pas][deployment-guide-figure-1400]
<a name="figure-14"></a>

###### <a name="solution"></a>Solution
Si le service de hello n’existe pas, hello améliorée Extension de surveillance Azure pour SAP n'a pas été installé correctement. Redéployez l’extension de hello à l’aide des étapes de hello décrites pour votre scénario de déploiement dans [des scénarios de déploiement de machines virtuelles pour SAP dans Azure][deployment-guide-3].

Après avoir déployé l’extension de hello, après une heure, vérifiez de nouveau si les compteurs de performance Azure hello sont fournies dans hello machine virtuelle Azure.

##### <a name="service-for-azure-enhanced-monitoring-exists-but-fails-toostart"></a>Service de surveillance améliorée Azure existe, mais échoue toostart

###### <a name="issue"></a>Problème
Hello service AzureEnhancedMonitoring Windows existe et est activé, mais échoue toostart. Pour plus d’informations, vérifiez le journal des événements application hello.

###### <a name="solution"></a>Solution
configuration de Hello est incorrecte. Redémarrez hello analyse d’extension pour hello machine virtuelle, comme décrit dans [configurer hello améliorée Extension de surveillance Azure pour SAP][deployment-guide-4.5].

#### <a name="windowslogowindows-some-azure-performance-counters-are-missing"></a>![Windows][Logo_Windows] Certains compteurs de performances Azure sont manquants
Hello service AzureEnhancedMonitoring Windows collecte les mesures de performances dans Azure. service de Hello Obtient des données provenant de plusieurs sources. Certaines données de configuration sont collectées localement, et certains indicateurs de performance sont lus à partir des diagnostics Azure. Compteurs de stockage sont utilisés à partir de la journalisation sur le niveau d’abonnement de stockage de hello.

Si le dépannage à l’aide de la Note SAP [1999351] n’hello de problème, réexécutez hello `Set-AzureRmVMAEMExtension` script de configuration. Vous pouvez avoir toowait une heure, car les compteurs analytique ou les diagnostics de stockage ne sont pas nécessairement créés immédiatement après avoir été activés. Si hello problème persiste, ouvrez un message de prise en charge du client SAP sur hello composant BC-OP-NT-AZR pour Windows ou BC-OP-LNX-AZR pour une machine virtuelle Linux.

#### <a name="linuxlogolinux-azure-performance-counters-do-not-show-up-at-all"></a>![Linux][Logo_Linux] Les compteurs de performances Azure ne s’affichent pas
Les indicateurs de performance dans Azure sont collectés par un démon. Si le démon de hello ne fonctionne pas, aucune mesure de performance ne peut être collectés.

##### <a name="hello-installation-directory-of-hello-azure-enhanced-monitoring-extension-is-empty"></a>répertoire d’installation Hello Hello extension de surveillance améliorée Azure est vide

###### <a name="issue"></a>Problème
répertoire de Hello \\var\\lib\\waagent\\ n’a pas un sous-répertoire pour hello extension de surveillance améliorée Azure.

###### <a name="solution"></a>Solution
extension de Hello n’est pas installée. Déterminez s’il s’agit d’un problème de proxy (comme décrit précédemment). Vous devrez peut-être toorestart hello ordinateur ou pour exécuter à nouveau hello `Set-AzureRmVMAEMExtension` script de configuration.

#### <a name="linuxlogolinux-some-azure-performance-counters-are-missing"></a>![Linux][Logo_Linux] Certains compteurs de performances Azure sont manquants
Les indicateurs de performance sur Azure sont collectés par un démon, qui obtient des données de plusieurs sources. Certaines données de configuration sont collectées localement, et certains indicateurs de performance sont lus à partir des diagnostics Azure. Compteurs de stockage proviennent des journaux hello dans votre abonnement de stockage.

Pour obtenir une liste complète et à jour des problèmes connus, consultez la note SAP [1999351], qui contient des informations de dépannage supplémentaires pour l’analyse Azure améliorée pour SAP.

Si le dépannage à l’aide de la Note SAP [1999351] ne pas résoudre le problème de hello, réexécutez hello `Set-AzureRmVMAEMExtension` un script de configuration comme décrit dans [configurer hello améliorée Extension de surveillance Azure pour SAP][deployment-guide-4.5]. Vous pouvez avoir toowait pendant une heure, car les compteurs analytique ou les diagnostics de stockage ne sont pas nécessairement créés immédiatement après avoir été activés. Si hello problème persiste, ouvrez un message de prise en charge du client SAP sur hello composant BC-OP-NT-AZR pour Windows ou BC-OP-LNX-AZR pour une machine virtuelle Linux.
