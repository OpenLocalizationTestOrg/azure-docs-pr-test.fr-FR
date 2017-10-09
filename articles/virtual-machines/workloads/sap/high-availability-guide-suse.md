---
title: "aaaAzure Machines virtuelles de haute disponibilité pour SAP NetWeaver sur SUSE Linux Enterprise Server, pour les applications SAP | Documents Microsoft"
description: "Guide de haute disponibilité pour SAP NetWeaver sur SUSE Linux Enterprise Server pour les applications SAP"
services: virtual-machines-windows,virtual-network,storage
documentationcenter: saponazure
author: mssedusch
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
ms.date: 04/27/2017
ms.author: sedusch
ms.openlocfilehash: e944103df92d5ffec9196189f138e25972bea79f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="high-availability-for-sap-netweaver-on-azure-vms-on-suse-linux-enterprise-server-for-sap-applications"></a><span data-ttu-id="6a7dd-103">Haute disponibilité pour SAP NetWeaver sur les machines virtuelles Azure sur SUSE Linux Enterprise Server pour les applications SAP</span><span class="sxs-lookup"><span data-stu-id="6a7dd-103">High availability for SAP NetWeaver on Azure VMs on SUSE Linux Enterprise Server for SAP applications</span></span>

[dbms-guide]:dbms-guide.md
[deployment-guide]:deployment-guide.md
[planning-guide]:planning-guide.md

[2205917]:https://launchpad.support.sap.com/#/notes/2205917
[1944799]:https://launchpad.support.sap.com/#/notes/1944799
[1928533]:https://launchpad.support.sap.com/#/notes/1928533
[2015553]:https://launchpad.support.sap.com/#/notes/2015553
[2178632]:https://launchpad.support.sap.com/#/notes/2178632
[2191498]:https://launchpad.support.sap.com/#/notes/2191498
[2243692]:https://launchpad.support.sap.com/#/notes/2243692
[1984787]:https://launchpad.support.sap.com/#/notes/1984787
[1999351]:https://launchpad.support.sap.com/#/notes/1999351
[1410736]:https://launchpad.support.sap.com/#/notes/1410736

[sap-swcenter]:https://support.sap.com/en/my-support/software-downloads.html

[suse-hana-ha-guide]:https://www.suse.com/docrep/documents/ir8w88iwu7/suse_linux_enterprise_server_for_sap_applications_12_sp1.pdf
[suse-drbd-guide]:https://www.suse.com/documentation/sle-ha-12/singlehtml/book_sleha_techguides/book_sleha_techguides.html

[template-multisid-xscs]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image-multi-sid-xscs-md%2Fazuredeploy.json
[template-converged]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image-converged-md%2Fazuredeploy.json
[template-file-server]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-file-server-md%2Fazuredeploy.json

[sap-hana-ha]:sap-hana-high-availability.md

<span data-ttu-id="6a7dd-113">Cet article décrit comment les machines virtuelles toodeploy hello, configurer des machines virtuelles de hello, installer hello cluster framework et installer un système SAP NetWeaver 7.50 hautement disponible.</span><span class="sxs-lookup"><span data-stu-id="6a7dd-113">This article describes how toodeploy hello virtual machines, configure hello virtual machines, install hello cluster framework and install a highly available SAP NetWeaver 7.50 system.</span></span>
<span data-ttu-id="6a7dd-114">Dans les configurations d’exemple hello, etc. des commandes d’installation. nous utilisons le numéro d’instance ASCS 00, le numéro d’instance ERS 02 et l’ID de système SAP NWS.</span><span class="sxs-lookup"><span data-stu-id="6a7dd-114">In hello example configurations, installation commands etc. ASCS instance number 00, ERS instance number 02 and SAP System ID NWS is used.</span></span> <span data-ttu-id="6a7dd-115">Hello noms de ressources hello (par exemple les machines virtuelles, les réseaux virtuels) dans l’exemple de hello supposent que vous avez utilisé hello [convergé modèle] [ template-converged] avec les ressources SAP système ID NWS toocreate hello.</span><span class="sxs-lookup"><span data-stu-id="6a7dd-115">hello names of hello resources (for example virtual machines, virtual networks) in hello example assume that you have used hello [converged template][template-converged] with SAP system ID NWS toocreate hello resources.</span></span>

<span data-ttu-id="6a7dd-116">Lire hello suivant tout d’abord les Notes SAP et livres</span><span class="sxs-lookup"><span data-stu-id="6a7dd-116">Read hello following SAP Notes and papers first</span></span>

* <span data-ttu-id="6a7dd-117">Note SAP [1928533], qui contient :</span><span class="sxs-lookup"><span data-stu-id="6a7dd-117">SAP Note [1928533], which has:</span></span>
  * <span data-ttu-id="6a7dd-118">Liste des tailles de machine virtuelle Azure qui sont pris en charge pour le déploiement de hello de logiciels SAP</span><span class="sxs-lookup"><span data-stu-id="6a7dd-118">List of Azure VM sizes that are supported for hello deployment of SAP software</span></span>
  * <span data-ttu-id="6a7dd-119">des informations importantes sur la capacité en fonction de la taille des machines virtuelles Azure</span><span class="sxs-lookup"><span data-stu-id="6a7dd-119">Important capacity information for Azure VM sizes</span></span>
  * <span data-ttu-id="6a7dd-120">les logiciels SAP pris en charge et les combinaisons entre système d’exploitation et base de données</span><span class="sxs-lookup"><span data-stu-id="6a7dd-120">Supported SAP software, and operating system (OS) and database combinations</span></span>
  * <span data-ttu-id="6a7dd-121">la version du noyau SAP requise pour Windows et Linux sur Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="6a7dd-121">Required SAP kernel version for Windows and Linux on Microsoft Azure</span></span>

* <span data-ttu-id="6a7dd-122">La note SAP [2015553] répertorie les conditions préalables au déploiement de logiciels SAP pris en charge par SAP sur Azure.</span><span class="sxs-lookup"><span data-stu-id="6a7dd-122">SAP Note [2015553] lists prerequisites for SAP-supported SAP software deployments in Azure.</span></span>
* <span data-ttu-id="6a7dd-123">La note SAP [2205917] contient des paramètres de système d’exploitation recommandés pour SUSE Linux Enterprise Server pour les applications SAP</span><span class="sxs-lookup"><span data-stu-id="6a7dd-123">SAP Note [2205917] has recommended OS settings for SUSE Linux Enterprise Server for SAP Applications</span></span>
* <span data-ttu-id="6a7dd-124">La note SAP [1944799] contient des instructions SAP HANA pour SUSE Linux Enterprise Server pour les applications SAP</span><span class="sxs-lookup"><span data-stu-id="6a7dd-124">SAP Note [1944799] has SAP HANA Guidelines for SUSE Linux Enterprise Server for SAP Applications</span></span>
* <span data-ttu-id="6a7dd-125">La note SAP [2178632] contient des informations détaillées sur toutes les métriques de surveillance rapportées pour SAP sur Azure.</span><span class="sxs-lookup"><span data-stu-id="6a7dd-125">SAP Note [2178632] has detailed information about all monitoring metrics reported for SAP in Azure.</span></span>
* <span data-ttu-id="6a7dd-126">La Note SAP [2191498] hello requise version de l’Agent hôte SAP pour Linux dans Azure.</span><span class="sxs-lookup"><span data-stu-id="6a7dd-126">SAP Note [2191498] has hello required SAP Host Agent version for Linux in Azure.</span></span>
* <span data-ttu-id="6a7dd-127">La note SAP [2243692] contient des informations sur les licences SAP sur Linux dans Azure.</span><span class="sxs-lookup"><span data-stu-id="6a7dd-127">SAP Note [2243692] has information about SAP licensing on Linux in Azure.</span></span>
* <span data-ttu-id="6a7dd-128">La note SAP [1984787] contient des informations sur SUSE Linux Enterprise Server 12.</span><span class="sxs-lookup"><span data-stu-id="6a7dd-128">SAP Note [1984787] has general information about SUSE Linux Enterprise Server 12.</span></span>
* <span data-ttu-id="6a7dd-129">La Note SAP [1999351] a des informations de dépannage supplémentaires pour hello améliorée Extension de surveillance Azure pour SAP.</span><span class="sxs-lookup"><span data-stu-id="6a7dd-129">SAP Note [1999351] has additional troubleshooting information for hello Azure Enhanced Monitoring Extension for SAP.</span></span>
* <span data-ttu-id="6a7dd-130">Le [WIKI de la communauté SAP](https://wiki.scn.sap.com/wiki/display/HOME/SAPonLinuxNotes) contient toutes les notes SAP requises pour Linux.</span><span class="sxs-lookup"><span data-stu-id="6a7dd-130">[SAP Community WIKI](https://wiki.scn.sap.com/wiki/display/HOME/SAPonLinuxNotes) has all required SAP Notes for Linux.</span></span>
* <span data-ttu-id="6a7dd-131">[Planification et implémentation de Machines virtuelles Azure pour SAP sur Linux][planning-guide]</span><span class="sxs-lookup"><span data-stu-id="6a7dd-131">[Azure Virtual Machines planning and implementation for SAP on Linux][planning-guide]</span></span>
* <span data-ttu-id="6a7dd-132">[Déploiement de Machines virtuelles Azure pour SAP sur Linux (cet article)][deployment-guide]</span><span class="sxs-lookup"><span data-stu-id="6a7dd-132">[Azure Virtual Machines deployment for SAP on Linux (this article)][deployment-guide]</span></span>
* <span data-ttu-id="6a7dd-133">[Déploiement SGBD de Machines virtuelles Azure pour SAP sur Linux][dbms-guide]</span><span class="sxs-lookup"><span data-stu-id="6a7dd-133">[Azure Virtual Machines DBMS deployment for SAP on Linux][dbms-guide]</span></span>
* <span data-ttu-id="6a7dd-134">[SAP HANA SR Performance Optimized Scenario][suse-hana-ha-guide] (Scénario d’optimisation des performances de réplication système de SAP HANA)</span><span class="sxs-lookup"><span data-stu-id="6a7dd-134">[SAP HANA SR Performance Optimized Scenario][suse-hana-ha-guide]</span></span>  
  <span data-ttu-id="6a7dd-135">guide de Hello contient toutes les informations requises tooset, réplication du système SAP HANA en local.</span><span class="sxs-lookup"><span data-stu-id="6a7dd-135">hello guide contains all required information tooset up SAP HANA System Replication on-premises.</span></span> <span data-ttu-id="6a7dd-136">Utilisez ce guide comme référence.</span><span class="sxs-lookup"><span data-stu-id="6a7dd-136">Use this guide as a baseline.</span></span>
* <span data-ttu-id="6a7dd-137">[Hautement disponible stockage NFS avec DRBD et STIMULATEUR] [ suse-drbd-guide] guide de hello contient toutes les informations requises tooset, d’un serveur NFS à haute disponibilité.</span><span class="sxs-lookup"><span data-stu-id="6a7dd-137">[Highly Available NFS Storage with DRBD and Pacemaker][suse-drbd-guide] hello guide contains all required information tooset up a highly available NFS server.</span></span> <span data-ttu-id="6a7dd-138">Utilisez ce guide comme référence.</span><span class="sxs-lookup"><span data-stu-id="6a7dd-138">Use this guide as a baseline.</span></span>


## <a name="overview"></a><span data-ttu-id="6a7dd-139">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="6a7dd-139">Overview</span></span>

<span data-ttu-id="6a7dd-140">tooachieve haute disponibilité, SAP NetWeaver requiert un serveur NFS.</span><span class="sxs-lookup"><span data-stu-id="6a7dd-140">tooachieve high availability, SAP NetWeaver requires an NFS server.</span></span> <span data-ttu-id="6a7dd-141">serveur NFS de Hello est configuré dans un cluster distinct et peut être utilisé par plusieurs systèmes SAP.</span><span class="sxs-lookup"><span data-stu-id="6a7dd-141">hello NFS server is configured in a separate cluster and can be used by multiple SAP systems.</span></span>

![Vue d’ensemble de la haute disponibilité SAP NetWeaver](./media/high-availability-guide-suse/img_001.png)

<span data-ttu-id="6a7dd-143">Hello serveur NFS, SAP NetWeaver ASC, SAP NetWeaver SCS, SAP NetWeaver ERS et base de données SAP HANA hello utiliser le nom d’hôte virtuel et les adresses IP virtuelles.</span><span class="sxs-lookup"><span data-stu-id="6a7dd-143">hello NFS server, SAP NetWeaver ASCS, SAP NetWeaver SCS, SAP NetWeaver ERS and hello SAP HANA database use virtual hostname and virtual IP addresses.</span></span> <span data-ttu-id="6a7dd-144">Sur Azure, un équilibreur de charge est requis toouse une adresse IP virtuelle.</span><span class="sxs-lookup"><span data-stu-id="6a7dd-144">On Azure, a load balancer is required toouse a virtual IP address.</span></span> <span data-ttu-id="6a7dd-145">Hello liste suivante présente configuration hello d’équilibrage de charge hello.</span><span class="sxs-lookup"><span data-stu-id="6a7dd-145">hello following list shows hello configuration of hello load balancer.</span></span>

### <a name="nfs-server"></a><span data-ttu-id="6a7dd-146">Serveur NFS</span><span class="sxs-lookup"><span data-stu-id="6a7dd-146">NFS Server</span></span>
* <span data-ttu-id="6a7dd-147">Configuration du frontend</span><span class="sxs-lookup"><span data-stu-id="6a7dd-147">Frontend configuration</span></span>
  * <span data-ttu-id="6a7dd-148">Adresse IP 10.0.0.4</span><span class="sxs-lookup"><span data-stu-id="6a7dd-148">IP address 10.0.0.4</span></span>
* <span data-ttu-id="6a7dd-149">Configuration du backend</span><span class="sxs-lookup"><span data-stu-id="6a7dd-149">Backend configuration</span></span>
  * <span data-ttu-id="6a7dd-150">Connecté tooprimary les interfaces de réseau de tous les ordinateurs virtuels qui doivent faire partie du cluster NFS hello</span><span class="sxs-lookup"><span data-stu-id="6a7dd-150">Connected tooprimary network interfaces of all virtual machines that should be part of hello NFS cluster</span></span>
* <span data-ttu-id="6a7dd-151">Port de la sonde</span><span class="sxs-lookup"><span data-stu-id="6a7dd-151">Probe Port</span></span>
  * <span data-ttu-id="6a7dd-152">Port 61000</span><span class="sxs-lookup"><span data-stu-id="6a7dd-152">Port 61000</span></span>
* <span data-ttu-id="6a7dd-153">Règles d’équilibrage de charge</span><span class="sxs-lookup"><span data-stu-id="6a7dd-153">Loadbalancing rules</span></span>
  * <span data-ttu-id="6a7dd-154">TCP 2049</span><span class="sxs-lookup"><span data-stu-id="6a7dd-154">2049 TCP</span></span> 
  * <span data-ttu-id="6a7dd-155">UDP 2049</span><span class="sxs-lookup"><span data-stu-id="6a7dd-155">2049 UDP</span></span>

### <a name="ascs"></a><span data-ttu-id="6a7dd-156">(A)SCS</span><span class="sxs-lookup"><span data-stu-id="6a7dd-156">(A)SCS</span></span>
* <span data-ttu-id="6a7dd-157">Configuration du frontend</span><span class="sxs-lookup"><span data-stu-id="6a7dd-157">Frontend configuration</span></span>
  * <span data-ttu-id="6a7dd-158">Adresse IP 10.0.0.10</span><span class="sxs-lookup"><span data-stu-id="6a7dd-158">IP address 10.0.0.10</span></span>
* <span data-ttu-id="6a7dd-159">Configuration du backend</span><span class="sxs-lookup"><span data-stu-id="6a7dd-159">Backend configuration</span></span>
  * <span data-ttu-id="6a7dd-160">Interfaces de réseau connecté tooprimary de tous les ordinateurs virtuels qui doivent faire partie du cluster SCS/ERS hello (A)</span><span class="sxs-lookup"><span data-stu-id="6a7dd-160">Connected tooprimary network interfaces of all virtual machines that should be part of hello (A)SCS/ERS cluster</span></span>
* <span data-ttu-id="6a7dd-161">Port de la sonde</span><span class="sxs-lookup"><span data-stu-id="6a7dd-161">Probe Port</span></span>
  * <span data-ttu-id="6a7dd-162">Port 620**&lt;nr&gt;**</span><span class="sxs-lookup"><span data-stu-id="6a7dd-162">Port 620**&lt;nr&gt;**</span></span>
* <span data-ttu-id="6a7dd-163">Règles d’équilibrage de charge</span><span class="sxs-lookup"><span data-stu-id="6a7dd-163">Loadbalancing rules</span></span>
  * <span data-ttu-id="6a7dd-164">TCP 32**&lt;nr&gt;**</span><span class="sxs-lookup"><span data-stu-id="6a7dd-164">32**&lt;nr&gt;** TCP</span></span>
  * <span data-ttu-id="6a7dd-165">TCP 36**&lt;nr&gt;**</span><span class="sxs-lookup"><span data-stu-id="6a7dd-165">36**&lt;nr&gt;** TCP</span></span>
  * <span data-ttu-id="6a7dd-166">TCP 39**&lt;nr&gt;**</span><span class="sxs-lookup"><span data-stu-id="6a7dd-166">39**&lt;nr&gt;** TCP</span></span>
  * <span data-ttu-id="6a7dd-167">TCP 81**&lt;nr&gt;**</span><span class="sxs-lookup"><span data-stu-id="6a7dd-167">81**&lt;nr&gt;** TCP</span></span>
  * <span data-ttu-id="6a7dd-168">TCP 5**&lt;nr&gt;**13</span><span class="sxs-lookup"><span data-stu-id="6a7dd-168">5**&lt;nr&gt;**13 TCP</span></span>
  * <span data-ttu-id="6a7dd-169">TCP 5**&lt;nr&gt;**14</span><span class="sxs-lookup"><span data-stu-id="6a7dd-169">5**&lt;nr&gt;**14 TCP</span></span>
  * <span data-ttu-id="6a7dd-170">TCP 5**&lt;nr&gt;**16</span><span class="sxs-lookup"><span data-stu-id="6a7dd-170">5**&lt;nr&gt;**16 TCP</span></span>

### <a name="ers"></a><span data-ttu-id="6a7dd-171">ERS</span><span class="sxs-lookup"><span data-stu-id="6a7dd-171">ERS</span></span>
* <span data-ttu-id="6a7dd-172">Configuration du frontend</span><span class="sxs-lookup"><span data-stu-id="6a7dd-172">Frontend configuration</span></span>
  * <span data-ttu-id="6a7dd-173">Adresse IP 10.0.0.11</span><span class="sxs-lookup"><span data-stu-id="6a7dd-173">IP address 10.0.0.11</span></span>
* <span data-ttu-id="6a7dd-174">Configuration du backend</span><span class="sxs-lookup"><span data-stu-id="6a7dd-174">Backend configuration</span></span>
  * <span data-ttu-id="6a7dd-175">Interfaces de réseau connecté tooprimary de tous les ordinateurs virtuels qui doivent faire partie du cluster SCS/ERS hello (A)</span><span class="sxs-lookup"><span data-stu-id="6a7dd-175">Connected tooprimary network interfaces of all virtual machines that should be part of hello (A)SCS/ERS cluster</span></span>
* <span data-ttu-id="6a7dd-176">Port de la sonde</span><span class="sxs-lookup"><span data-stu-id="6a7dd-176">Probe Port</span></span>
  * <span data-ttu-id="6a7dd-177">Port 621**&lt;nr&gt;**</span><span class="sxs-lookup"><span data-stu-id="6a7dd-177">Port 621**&lt;nr&gt;**</span></span>
* <span data-ttu-id="6a7dd-178">Règles d’équilibrage de charge</span><span class="sxs-lookup"><span data-stu-id="6a7dd-178">Loadbalancing rules</span></span>
  * <span data-ttu-id="6a7dd-179">TCP 33**&lt;nr&gt;**</span><span class="sxs-lookup"><span data-stu-id="6a7dd-179">33**&lt;nr&gt;** TCP</span></span>
  * <span data-ttu-id="6a7dd-180">TCP 5**&lt;nr&gt;**13</span><span class="sxs-lookup"><span data-stu-id="6a7dd-180">5**&lt;nr&gt;**13 TCP</span></span>
  * <span data-ttu-id="6a7dd-181">TCP 5**&lt;nr&gt;**14</span><span class="sxs-lookup"><span data-stu-id="6a7dd-181">5**&lt;nr&gt;**14 TCP</span></span>
  * <span data-ttu-id="6a7dd-182">TCP 5**&lt;nr&gt;**16</span><span class="sxs-lookup"><span data-stu-id="6a7dd-182">5**&lt;nr&gt;**16 TCP</span></span>

### <a name="sap-hana"></a><span data-ttu-id="6a7dd-183">SAP HANA</span><span class="sxs-lookup"><span data-stu-id="6a7dd-183">SAP HANA</span></span>
* <span data-ttu-id="6a7dd-184">Configuration du frontend</span><span class="sxs-lookup"><span data-stu-id="6a7dd-184">Frontend configuration</span></span>
  * <span data-ttu-id="6a7dd-185">Adresse IP 10.0.0.12</span><span class="sxs-lookup"><span data-stu-id="6a7dd-185">IP address 10.0.0.12</span></span>
* <span data-ttu-id="6a7dd-186">Configuration du backend</span><span class="sxs-lookup"><span data-stu-id="6a7dd-186">Backend configuration</span></span>
  * <span data-ttu-id="6a7dd-187">Connecté tooprimary les interfaces de réseau de tous les ordinateurs virtuels qui doivent faire partie du cluster HANA hello</span><span class="sxs-lookup"><span data-stu-id="6a7dd-187">Connected tooprimary network interfaces of all virtual machines that should be part of hello HANA cluster</span></span>
* <span data-ttu-id="6a7dd-188">Port de la sonde</span><span class="sxs-lookup"><span data-stu-id="6a7dd-188">Probe Port</span></span>
  * <span data-ttu-id="6a7dd-189">Port 625**&lt;nr&gt;**</span><span class="sxs-lookup"><span data-stu-id="6a7dd-189">Port 625**&lt;nr&gt;**</span></span>
* <span data-ttu-id="6a7dd-190">Règles d’équilibrage de charge</span><span class="sxs-lookup"><span data-stu-id="6a7dd-190">Loadbalancing rules</span></span>
  * <span data-ttu-id="6a7dd-191">TCP 3**&lt;nr&gt;**15</span><span class="sxs-lookup"><span data-stu-id="6a7dd-191">3**&lt;nr&gt;**15 TCP</span></span>
  * <span data-ttu-id="6a7dd-192">TCP 3**&lt;nr&gt;**17</span><span class="sxs-lookup"><span data-stu-id="6a7dd-192">3**&lt;nr&gt;**17 TCP</span></span>

## <a name="setting-up-a-highly-available-nfs-server"></a><span data-ttu-id="6a7dd-193">Configuration d’un serveur NFS à haute disponibilité</span><span class="sxs-lookup"><span data-stu-id="6a7dd-193">Setting up a highly available NFS server</span></span>

### <a name="deploying-linux"></a><span data-ttu-id="6a7dd-194">Déploiement de Linux</span><span class="sxs-lookup"><span data-stu-id="6a7dd-194">Deploying Linux</span></span>

<span data-ttu-id="6a7dd-195">Bonjour Azure Marketplace contient une image pour SUSE Linux Enterprise Server 12 d’Applications SAP que vous pouvez utiliser les nouveaux ordinateurs virtuels de toodeploy.</span><span class="sxs-lookup"><span data-stu-id="6a7dd-195">hello Azure Marketplace contains an image for SUSE Linux Enterprise Server for SAP Applications 12 that you can use toodeploy new virtual machines.</span></span>
<span data-ttu-id="6a7dd-196">Vous pouvez utiliser un des modèles de démarrage rapide de hello sur github toodeploy toutes les ressources requises.</span><span class="sxs-lookup"><span data-stu-id="6a7dd-196">You can use one of hello quick start templates on github toodeploy all required resources.</span></span> <span data-ttu-id="6a7dd-197">modèle de Hello déploie les machines virtuelles de hello, équilibrage de charge hello, haute disponibilité etc.. Suivez ces modèles de hello toodeploy comme suit :</span><span class="sxs-lookup"><span data-stu-id="6a7dd-197">hello template deploys hello virtual machines, hello load balancer, availability set etc. Follow these steps toodeploy hello template:</span></span>

1. <span data-ttu-id="6a7dd-198">Ouvrez hello [modèle de serveur de fichiers SAP] [ template-file-server] Bonjour portail Azure</span><span class="sxs-lookup"><span data-stu-id="6a7dd-198">Open hello [SAP file server template][template-file-server] in hello Azure portal</span></span>   
1. <span data-ttu-id="6a7dd-199">Entrez les paramètres suivants de hello</span><span class="sxs-lookup"><span data-stu-id="6a7dd-199">Enter hello following parameters</span></span>
   1. <span data-ttu-id="6a7dd-200">Préfixe de ressource</span><span class="sxs-lookup"><span data-stu-id="6a7dd-200">Resource Prefix</span></span>  
      <span data-ttu-id="6a7dd-201">Entrez le préfixe hello toouse.</span><span class="sxs-lookup"><span data-stu-id="6a7dd-201">Enter hello prefix you want toouse.</span></span> <span data-ttu-id="6a7dd-202">valeur de Hello est utilisé en tant que préfixe pour les ressources hello qui sont déployés.</span><span class="sxs-lookup"><span data-stu-id="6a7dd-202">hello value is used as a prefix for hello resources that are deployed.</span></span>
   2. <span data-ttu-id="6a7dd-203">Type de système d’exploitation</span><span class="sxs-lookup"><span data-stu-id="6a7dd-203">Os Type</span></span>  
      <span data-ttu-id="6a7dd-204">Sélectionnez une des distributions de Linux hello.</span><span class="sxs-lookup"><span data-stu-id="6a7dd-204">Select one of hello Linux distributions.</span></span> <span data-ttu-id="6a7dd-205">Dans cet exemple, sélectionnez SLES 12.</span><span class="sxs-lookup"><span data-stu-id="6a7dd-205">For this example, select SLES 12</span></span>
   3. <span data-ttu-id="6a7dd-206">Nom d’utilisateur et mot de passe d’administrateur</span><span class="sxs-lookup"><span data-stu-id="6a7dd-206">Admin Username and Admin Password</span></span>  
      <span data-ttu-id="6a7dd-207">Création d’un utilisateur qui peut être utilisé toolog sur l’ordinateur de toohello.</span><span class="sxs-lookup"><span data-stu-id="6a7dd-207">A new user is created that can be used toolog on toohello machine.</span></span>
   4. <span data-ttu-id="6a7dd-208">ID du sous-réseau</span><span class="sxs-lookup"><span data-stu-id="6a7dd-208">Subnet Id</span></span>  
      <span data-ttu-id="6a7dd-209">ID de Hello d’ordinateurs virtuels hello sous-réseau toowhich hello doit être connecté à.</span><span class="sxs-lookup"><span data-stu-id="6a7dd-209">hello ID of hello subnet toowhich hello virtual machines should be connected to.</span></span> <span data-ttu-id="6a7dd-210">Laissez vide si vous voulez toocreate un nouveau réseau virtuel ou sélectionnez sous-réseau hello de votre VPN ou Express Route réseau virtuel tooconnect hello tooyour local réseau d’ordinateurs virtuels.</span><span class="sxs-lookup"><span data-stu-id="6a7dd-210">Leave empty if you want toocreate a new virtual network or select hello subnet of your VPN or Express Route virtual network tooconnect hello virtual machine tooyour on-premises network.</span></span> <span data-ttu-id="6a7dd-211">ID de Hello ressemble généralement à /subscriptions/**&lt;id d’abonnement&gt;**/resourceGroups/**&lt;nom de groupe de ressources&gt;**/providers/ Microsoft.Network/virtualNetworks/**&lt;nom de réseau virtuel&gt;**/subnets/**&lt;nom de sous-réseau&gt;**</span><span class="sxs-lookup"><span data-stu-id="6a7dd-211">hello ID usually looks like /subscriptions/**&lt;subscription id&gt;**/resourceGroups/**&lt;resource group name&gt;**/providers/Microsoft.Network/virtualNetworks/**&lt;virtual network name&gt;**/subnets/**&lt;subnet name&gt;**</span></span>

### <a name="installation"></a><span data-ttu-id="6a7dd-212">Installation</span><span class="sxs-lookup"><span data-stu-id="6a7dd-212">Installation</span></span>

<span data-ttu-id="6a7dd-213">Hello éléments suivants portent le préfixe soit **[A]** -tooall applicable nœuds, **[1]** -uniquement applicable toonode 1 ou **[2]** -uniquement applicable toonode 2.</span><span class="sxs-lookup"><span data-stu-id="6a7dd-213">hello following items are prefixed with either **[A]** - applicable tooall nodes, **[1]** - only applicable toonode 1 or **[2]** - only applicable toonode 2.</span></span>

1. <span data-ttu-id="6a7dd-214">**[A]** Mettre à jour SLES</span><span class="sxs-lookup"><span data-stu-id="6a7dd-214">**[A]** Update SLES</span></span>

   <pre><code>
   sudo zypper update
   </code></pre>

1. <span data-ttu-id="6a7dd-215">**[1]** Activer l’accès SSH</span><span class="sxs-lookup"><span data-stu-id="6a7dd-215">**[1]** Enable ssh access</span></span>

   <pre><code>
   sudo ssh-keygen -tdsa
   
   # Enter file in which toosave hello key (/root/.ssh/id_dsa): -> ENTER
   # Enter passphrase (empty for no passphrase): -> ENTER
   # Enter same passphrase again: -> ENTER
   
   # copy hello public key
   sudo cat /root/.ssh/id_dsa.pub
   </code></pre>

2. <span data-ttu-id="6a7dd-216">**[2**] Activer l’accès SSH</span><span class="sxs-lookup"><span data-stu-id="6a7dd-216">**[2]** Enable ssh access</span></span>

   <pre><code>
   sudo ssh-keygen -tdsa

   # insert hello public key you copied in hello last step into hello authorized keys file on hello second server
   sudo vi /root/.ssh/authorized_keys
   
   # Enter file in which toosave hello key (/root/.ssh/id_dsa): -> ENTER
   # Enter passphrase (empty for no passphrase): -> ENTER
   # Enter same passphrase again: -> ENTER
   
   # copy hello public key   
   sudo cat /root/.ssh/id_dsa.pub
   </code></pre>

1. <span data-ttu-id="6a7dd-217">**[1]** Activer l’accès SSH</span><span class="sxs-lookup"><span data-stu-id="6a7dd-217">**[1]** Enable ssh access</span></span>

   <pre><code>
   # insert hello public key you copied in hello last step into hello authorized keys file on hello first server
   sudo vi /root/.ssh/authorized_keys
   </code></pre>

1. <span data-ttu-id="6a7dd-218">**[A]** Installer l’extension de haute disponibilité</span><span class="sxs-lookup"><span data-stu-id="6a7dd-218">**[A]** Install HA extension</span></span>
   
   <pre><code>
   sudo zypper install sle-ha-release fence-agents
   </code></pre>

1. <span data-ttu-id="6a7dd-219">**[A]** Configurer la résolution de nom d’hôte</span><span class="sxs-lookup"><span data-stu-id="6a7dd-219">**[A]** Setup host name resolution</span></span>   

   <span data-ttu-id="6a7dd-220">Vous pouvez utiliser un serveur DNS ou modifier/etc/hosts de hello sur tous les nœuds.</span><span class="sxs-lookup"><span data-stu-id="6a7dd-220">You can either use a DNS server or modify hello /etc/hosts on all nodes.</span></span> <span data-ttu-id="6a7dd-221">Cet exemple montre comment toouse hello les fichier/etc/hosts.</span><span class="sxs-lookup"><span data-stu-id="6a7dd-221">This example shows how toouse hello /etc/hosts file.</span></span>
   <span data-ttu-id="6a7dd-222">Remplacez l’adresse IP de hello et un nom d’hôte hello Bonjour suivant les commandes</span><span class="sxs-lookup"><span data-stu-id="6a7dd-222">Replace hello IP address and hello hostname in hello following commands</span></span>

   <pre><code>
   sudo vi /etc/hosts
   </code></pre>
   
   <span data-ttu-id="6a7dd-223">Insérez hello suivant lignes trop/etc/hosts.</span><span class="sxs-lookup"><span data-stu-id="6a7dd-223">Insert hello following lines too/etc/hosts.</span></span> <span data-ttu-id="6a7dd-224">Modifiez les toomatch hello IP adresse et le nom d’hôte de votre environnement</span><span class="sxs-lookup"><span data-stu-id="6a7dd-224">Change hello IP address and hostname toomatch your environment</span></span>   
   
   <pre><code>
   # IP address of hello load balancer frontend configuration for NFS
   <b>10.0.0.4 nws-nfs</b>
   </code></pre>

1. <span data-ttu-id="6a7dd-225">**[1]** Installer le cluster</span><span class="sxs-lookup"><span data-stu-id="6a7dd-225">**[1]** Install Cluster</span></span>
   
   <pre><code>
   sudo ha-cluster-init
   
   # Do you want toocontinue anyway? [y/N] -> y
   # Network address toobind too(for example: 192.168.1.0) [10.79.227.0] -> ENTER
   # Multicast address (for example: 239.x.x.x) [239.174.218.125] -> ENTER
   # Multicast port [5405] -> ENTER
   # Do you wish toouse SBD? [y/N] -> N
   # Do you wish tooconfigure an administration IP? [y/N] -> N
   </code></pre>

1. <span data-ttu-id="6a7dd-226">**[2]**  Ajouter toocluster de nœud</span><span class="sxs-lookup"><span data-stu-id="6a7dd-226">**[2]** Add node toocluster</span></span>
   
   <pre><code> 
   sudo ha-cluster-join

   # WARNING: NTP is not configured toostart at system boot.
   # WARNING: No watchdog device found. If SBD is used, hello cluster will be unable toostart without a watchdog.
   # Do you want toocontinue anyway? [y/N] -> y
   # IP address or hostname of existing node (for example: 192.168.1.1) [] -> IP address of node 1 for example 10.0.0.10
   # /root/.ssh/id_dsa already exists - overwrite? [y/N] N
   </code></pre>

1. <span data-ttu-id="6a7dd-227">**[A]**  Toohello de mot de passe de modification hacluster même mot de passe</span><span class="sxs-lookup"><span data-stu-id="6a7dd-227">**[A]** Change hacluster password toohello same password</span></span>

   <pre><code> 
   sudo passwd hacluster
   </code></pre>

1. <span data-ttu-id="6a7dd-228">**[A]**  Configurer corosync toouse autre transport et ajouter la liste de nœuds.</span><span class="sxs-lookup"><span data-stu-id="6a7dd-228">**[A]** Configure corosync toouse other transport and add nodelist.</span></span> <span data-ttu-id="6a7dd-229">Le cluster ne fonctionnera pas dans le cas contraire.</span><span class="sxs-lookup"><span data-stu-id="6a7dd-229">Cluster will not work otherwise.</span></span>
   
   <pre><code> 
   sudo vi /etc/corosync/corosync.conf   
   </code></pre>

   <span data-ttu-id="6a7dd-230">Ajoutez hello toohello contenu gras le fichier suivant.</span><span class="sxs-lookup"><span data-stu-id="6a7dd-230">Add hello following bold content toohello file.</span></span>
   
   <pre><code> 
   [...]
     interface { 
        [...] 
     }
     <b>transport:      udpu</b>
   } 
   <b>nodelist {
     node {
      # IP address of <b>prod-nfs-0</b>
      ring0_addr:10.0.0.5
     }
     node {
      # IP address of <b>prod-nfs-1</b>
      ring0_addr:10.0.0.6
     } 
   }</b>
   logging {
     [...]
   </code></pre>

   <span data-ttu-id="6a7dd-231">Ensuite, redémarrez le service corosync hello</span><span class="sxs-lookup"><span data-stu-id="6a7dd-231">Then restart hello corosync service</span></span>

   <pre><code>
   sudo service corosync restart
   </code></pre>

1. <span data-ttu-id="6a7dd-232">**[A]** Installer les composants drbd</span><span class="sxs-lookup"><span data-stu-id="6a7dd-232">**[A]** Install drbd components</span></span>

   <pre><code>
   sudo zypper install drbd drbd-kmp-default drbd-utils
   </code></pre>

1. <span data-ttu-id="6a7dd-233">**[A]**  Créer une partition pour appareil de drbd hello</span><span class="sxs-lookup"><span data-stu-id="6a7dd-233">**[A]** Create a partition for hello drbd device</span></span>

   <pre><code>
   sudo sh -c 'echo -e "n\n\n\n\n\nw\n" | fdisk /dev/sdc'
   </code></pre>

1. <span data-ttu-id="6a7dd-234">**[A]** Créer des configurations LVM</span><span class="sxs-lookup"><span data-stu-id="6a7dd-234">**[A]** Create LVM configurations</span></span>

   <pre><code>
   sudo pvcreate /dev/sdc1   
   sudo vgcreate vg_NFS /dev/sdc1
   sudo lvcreate -l 100%FREE -n <b>NWS</b> vg_NFS
   </code></pre>

1. <span data-ttu-id="6a7dd-235">**[A]**  Dispositif de drbd créer hello NFS</span><span class="sxs-lookup"><span data-stu-id="6a7dd-235">**[A]** Create hello NFS drbd device</span></span>

   <pre><code>
   sudo vi /etc/drbd.d/<b>NWS</b>_nfs.res
   </code></pre>

   <span data-ttu-id="6a7dd-236">Insérer configuration hello pour le nouveau périphérique de drbd hello et quitter</span><span class="sxs-lookup"><span data-stu-id="6a7dd-236">Insert hello configuration for hello new drbd device and exit</span></span>

   <pre><code>
   resource <b>NWS</b>_nfs {
      protocol     C;
      disk {
         on-io-error       pass_on;
      }
      on <b>prod-nfs-0</b> {
         address   <b>10.0.0.5</b>:7790;
         device    /dev/drbd0;
         disk      /dev/vg_NFS/NWS;
         meta-disk internal;
      }
      on <b>prod-nfs-1</b> {
         address   <b>10.0.0.6</b>:7790;
         device    /dev/drbd0;
         disk      /dev/vg_NFS/NWS;
         meta-disk internal;
      }
   }
   </code></pre>

   <span data-ttu-id="6a7dd-237">Créer un appareil drbd hello et démarrez-le</span><span class="sxs-lookup"><span data-stu-id="6a7dd-237">Create hello drbd device and start it</span></span>

   <pre><code>
   sudo drbdadm create-md <b>NWS</b>_nfs
   sudo drbdadm up <b>NWS</b>_nfs
   </code></pre>

1. <span data-ttu-id="6a7dd-238">**[1]** Ignorer la synchronisation initiale</span><span class="sxs-lookup"><span data-stu-id="6a7dd-238">**[1]** Skip initial synchronization</span></span>

   <pre><code>
   sudo drbdadm new-current-uuid --clear-bitmap <b>NWS</b>_nfs
   </code></pre>

1. <span data-ttu-id="6a7dd-239">**[1]**  Nœud principal de l’ensemble hello</span><span class="sxs-lookup"><span data-stu-id="6a7dd-239">**[1]** Set hello primary node</span></span>

   <pre><code>
   sudo drbdadm primary --force <b>NWS</b>_nfs
   </code></pre>

1. <span data-ttu-id="6a7dd-240">**[1]**  Patienter jusqu'à ce que les nouveaux appareils de drbd hello sont synchronisés</span><span class="sxs-lookup"><span data-stu-id="6a7dd-240">**[1]** Wait until hello new drbd devices are synchronized</span></span>

   <pre><code>
   sudo cat /proc/drbd

   # version: 8.4.6 (api:1/proto:86-101)
   # GIT-hash: 833d830e0152d1e457fa7856e71e11248ccf3f70 build by abuild@sheep14, 2016-05-09 23:14:56
   # 0: cs:Connected ro:Primary/Secondary ds:UpToDate/UpToDate C r-----
   #    ns:0 nr:0 dw:0 dr:912 al:8 bm:0 lo:0 pe:0 ua:0 ap:0 ep:1 wo:f oos:0
   </code></pre>

1. <span data-ttu-id="6a7dd-241">**[1]**  Créer des systèmes de fichiers sur hello drbd périphériques</span><span class="sxs-lookup"><span data-stu-id="6a7dd-241">**[1]** Create file systems on hello drbd devices</span></span>

   <pre><code>
   sudo mkfs.xfs /dev/drbd0
   </code></pre>


### <a name="configure-cluster-framework"></a><span data-ttu-id="6a7dd-242">Configurer le framework du cluster</span><span class="sxs-lookup"><span data-stu-id="6a7dd-242">Configure Cluster Framework</span></span>

1. <span data-ttu-id="6a7dd-243">**[1]**  Modifier les paramètres par défaut de hello</span><span class="sxs-lookup"><span data-stu-id="6a7dd-243">**[1]** Change hello default settings</span></span>

   <pre><code>
   sudo crm configure

   crm(live)configure# rsc_defaults resource-stickiness="1"

   crm(live)configure# commit
   crm(live)configure# exit
   </code></pre>

1. <span data-ttu-id="6a7dd-244">**[1]**  Configuration du cluster ajouter hello NFS drbd périphérique toohello</span><span class="sxs-lookup"><span data-stu-id="6a7dd-244">**[1]** Add hello NFS drbd device toohello cluster configuration</span></span>

   <pre><code>
   sudo crm configure

   crm(live)configure# primitive drbd_<b>NWS</b>_nfs \
     ocf:linbit:drbd \
     params drbd_resource="<b>NWS</b>_nfs" \
     op monitor interval="15" role="Master" \
     op monitor interval="30" role="Slave"

   crm(live)configure# ms ms-drbd_<b>NWS</b>_nfs drbd_<b>NWS</b>_nfs \
     meta master-max="1" master-node-max="1" clone-max="2" \
     clone-node-max="1" notify="true" interleave="true"

   crm(live)configure# commit
   crm(live)configure# exit
   </code></pre>

1. <span data-ttu-id="6a7dd-245">**[1]**  Du serveur NFS hello créer</span><span class="sxs-lookup"><span data-stu-id="6a7dd-245">**[1]** Create hello NFS server</span></span>

   <pre><code>
   sudo crm configure

   crm(live)configure# primitive nfsserver \
     systemd:nfs-server \
     op monitor interval="30s"

   crm(live)configure# clone cl-nfsserver nfsserver interleave="true"

   crm(live)configure# commit
   crm(live)configure# exit
   </code></pre>

1. <span data-ttu-id="6a7dd-246">**[1]**  Créer des ressources de système de fichiers NFS hello</span><span class="sxs-lookup"><span data-stu-id="6a7dd-246">**[1]** Create hello NFS File System resources</span></span>

   <pre><code>
   sudo crm configure

   crm(live)configure# primitive fs_<b>NWS</b>_sapmnt \
     ocf:heartbeat:Filesystem \
     params device=/dev/drbd0 \
     directory=/srv/nfs/<b>NWS</b>  \
     fstype=xfs \
     op monitor interval="10s"

   crm(live)configure# group g-<b>NWS</b>_nfs fs_<b>NWS</b>_sapmnt

   crm(live)configure# order o-<b>NWS</b>_drbd_before_nfs inf: \
     ms-drbd_<b>NWS</b>_nfs:promote g-<b>NWS</b>_nfs:start
   
   crm(live)configure# colocation col-<b>NWS</b>_nfs_on_drbd inf: \
     g-<b>NWS</b>_nfs ms-drbd_<b>NWS</b>_nfs:Master

   crm(live)configure# commit
   crm(live)configure# exit
   </code></pre>

1. <span data-ttu-id="6a7dd-247">**[1]**  Créer hello NFS exports</span><span class="sxs-lookup"><span data-stu-id="6a7dd-247">**[1]** Create hello NFS exports</span></span>

   <pre><code>
   sudo mkdir /srv/nfs/<b>NWS</b>/sidsys
   sudo mkdir /srv/nfs/<b>NWS</b>/sapmntsid
   sudo mkdir /srv/nfs/<b>NWS</b>/trans

   sudo crm configure

   crm(live)configure# primitive exportfs_<b>NWS</b> \
     ocf:heartbeat:exportfs \
     params directory="/srv/nfs/<b>NWS</b>" \
     options="rw,no_root_squash" \
     clientspec="*" fsid=0 \
     wait_for_leasetime_on_stop=true \
     op monitor interval="30s"

   crm(live)configure# modgroup g-<b>NWS</b>_nfs add exportfs_<b>NWS</b>

   crm(live)configure# commit
   crm(live)configure# exit
   </code></pre>

1. <span data-ttu-id="6a7dd-248">**[1]**  Créer une ressource IP virtuel et un contrôle d’intégrité-sonde d’équilibreur de charge interne hello</span><span class="sxs-lookup"><span data-stu-id="6a7dd-248">**[1]** Create a virtual IP resource and health-probe for hello internal load balancer</span></span>

   <pre><code>
   sudo crm configure

   crm(live)configure# primitive vip_<b>NWS</b>_nfs IPaddr2 \
     params ip=<b>10.0.0.4</b> cidr_netmask=24 \
     op monitor interval=10 timeout=20

   crm(live)configure# primitive nc_<b>NWS</b>_nfs anything \
     params binfile="/usr/bin/nc" cmdline_options="-l -k 610<b>00</b>" \
     op monitor timeout=20s interval=10 depth=0

   crm(live)configure# modgroup g-<b>NWS</b>_nfs add nc_<b>NWS</b>_nfs
   crm(live)configure# modgroup g-<b>NWS</b>_nfs add vip_<b>NWS</b>_nfs

   crm(live)configure# commit
   crm(live)configure# exit
   </code></pre>

### <a name="create-stonith-device"></a><span data-ttu-id="6a7dd-249">Créer l’appareil STONITH</span><span class="sxs-lookup"><span data-stu-id="6a7dd-249">Create STONITH device</span></span>

<span data-ttu-id="6a7dd-250">APPAREIL STONITH Hello utilise un tooauthorize de Principal du Service par rapport à Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="6a7dd-250">hello STONITH device uses a Service Principal tooauthorize against Microsoft Azure.</span></span> <span data-ttu-id="6a7dd-251">Suivez ces étapes de toocreate un Principal de Service.</span><span class="sxs-lookup"><span data-stu-id="6a7dd-251">Follow these steps toocreate a Service Principal.</span></span>

1. <span data-ttu-id="6a7dd-252">Accédez trop<https://portal.azure.com></span><span class="sxs-lookup"><span data-stu-id="6a7dd-252">Go too<https://portal.azure.com></span></span>
1. <span data-ttu-id="6a7dd-253">Panneau d’Azure Active Directory hello ouvert</span><span class="sxs-lookup"><span data-stu-id="6a7dd-253">Open hello Azure Active Directory blade</span></span>  
   <span data-ttu-id="6a7dd-254">Accédez tooProperties et écrivez hello ID de répertoire. Il s’agit de hello **id client**.</span><span class="sxs-lookup"><span data-stu-id="6a7dd-254">Go tooProperties and write down hello Directory Id. This is hello **tenant id**.</span></span>
1. <span data-ttu-id="6a7dd-255">Cliquez sur Inscriptions d’applications</span><span class="sxs-lookup"><span data-stu-id="6a7dd-255">Click App registrations</span></span>
1. <span data-ttu-id="6a7dd-256">Cliquez sur Ajouter.</span><span class="sxs-lookup"><span data-stu-id="6a7dd-256">Click Add</span></span>
1. <span data-ttu-id="6a7dd-257">Entrez un nom, sélectionnez le type d’application « Application web/API », entrez une URL de connexion (par exemple, http://localhost) et cliquez sur Créer</span><span class="sxs-lookup"><span data-stu-id="6a7dd-257">Enter a Name, select Application Type "Web app/API", enter a sign-on URL (for example http://localhost) and click Create</span></span>
1. <span data-ttu-id="6a7dd-258">URL de connexion Hello n’est pas utilisé et peut être une URL valide</span><span class="sxs-lookup"><span data-stu-id="6a7dd-258">hello sign-on URL is not used and can be any valid URL</span></span>
1. <span data-ttu-id="6a7dd-259">Sélectionnez hello nouvelle application et cliquez sur les clés dans l’onglet Paramètres de hello</span><span class="sxs-lookup"><span data-stu-id="6a7dd-259">Select hello new App and click Keys in hello Settings tab</span></span>
1. <span data-ttu-id="6a7dd-260">Entrez une description pour la nouvelle clé, sélectionnez « N’expire jamais » et cliquez sur Enregistrer</span><span class="sxs-lookup"><span data-stu-id="6a7dd-260">Enter a description for a new key, select "Never expires" and click Save</span></span>
1. <span data-ttu-id="6a7dd-261">Écrivez hello valeur.</span><span class="sxs-lookup"><span data-stu-id="6a7dd-261">Write down hello Value.</span></span> <span data-ttu-id="6a7dd-262">Il est utilisé comme hello **mot de passe** pour hello Principal du Service</span><span class="sxs-lookup"><span data-stu-id="6a7dd-262">It is used as hello **password** for hello Service Principal</span></span>
1. <span data-ttu-id="6a7dd-263">Écrivez hello ID d’Application. Il est utilisé comme nom d’utilisateur de hello (**id de connexion** dans suit hello) de hello Principal du Service</span><span class="sxs-lookup"><span data-stu-id="6a7dd-263">Write down hello Application Id. It is used as hello username (**login id** in hello steps below) of hello Service Principal</span></span>

<span data-ttu-id="6a7dd-264">Hello Principal du Service n’a pas les autorisations tooaccess vos ressources Azure par défaut.</span><span class="sxs-lookup"><span data-stu-id="6a7dd-264">hello Service Principal does not have permissions tooaccess your Azure resources by default.</span></span> <span data-ttu-id="6a7dd-265">Vous devez toostart d’autorisations toogive hello Principal du Service et arrêter (désallouer) tous les ordinateurs virtuels du cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="6a7dd-265">You need toogive hello Service Principal permissions toostart and stop (deallocate) all virtual machines of hello cluster.</span></span>

1. <span data-ttu-id="6a7dd-266">Accédez toohttps://portal.azure.com</span><span class="sxs-lookup"><span data-stu-id="6a7dd-266">Go toohttps://portal.azure.com</span></span>
1. <span data-ttu-id="6a7dd-267">Ouvrez hello toutes les lames de ressources</span><span class="sxs-lookup"><span data-stu-id="6a7dd-267">Open hello All resources blade</span></span>
1. <span data-ttu-id="6a7dd-268">Sélectionnez l’ordinateur virtuel de hello</span><span class="sxs-lookup"><span data-stu-id="6a7dd-268">Select hello virtual machine</span></span>
1. <span data-ttu-id="6a7dd-269">Cliquez sur Contrôle d’accès (IAM)</span><span class="sxs-lookup"><span data-stu-id="6a7dd-269">Click Access control (IAM)</span></span>
1. <span data-ttu-id="6a7dd-270">Cliquez sur Ajouter.</span><span class="sxs-lookup"><span data-stu-id="6a7dd-270">Click Add</span></span>
1. <span data-ttu-id="6a7dd-271">Sélectionnez le rôle hello propriétaire</span><span class="sxs-lookup"><span data-stu-id="6a7dd-271">Select hello role Owner</span></span>
1. <span data-ttu-id="6a7dd-272">Entrez les nom hello d’application hello créé ci-dessus</span><span class="sxs-lookup"><span data-stu-id="6a7dd-272">Enter hello name of hello application you created above</span></span>
1. <span data-ttu-id="6a7dd-273">Cliquez sur OK</span><span class="sxs-lookup"><span data-stu-id="6a7dd-273">Click OK</span></span>

#### <a name="1-create-hello-stonith-devices"></a><span data-ttu-id="6a7dd-274">**[1]**  Créer des unités de STONITH hello</span><span class="sxs-lookup"><span data-stu-id="6a7dd-274">**[1]** Create hello STONITH devices</span></span>

<span data-ttu-id="6a7dd-275">Une fois que vous avez modifié les autorisations hello pour les ordinateurs virtuels de hello, vous pouvez configurer les appareils STONITH hello dans un cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="6a7dd-275">After you edited hello permissions for hello virtual machines, you can configure hello STONITH devices in hello cluster.</span></span>

<pre><code>
sudo crm configure

# replace hello bold string with your subscription id, resource group, tenant id, service principal id and password

crm(live)configure# primitive rsc_st_azure_1 stonith:fence_azure_arm \
   params subscriptionId="<b>subscription id</b>" resourceGroup="<b>resource group</b>" tenantId="<b>tenant id</b>" login="<b>login id</b>" passwd="<b>password</b>"

crm(live)configure# primitive rsc_st_azure_2 stonith:fence_azure_arm \
   params subscriptionId="<b>subscription id</b>" resourceGroup="<b>resource group</b>" tenantId="<b>tenant id</b>" login="<b>login id</b>" passwd="<b>password</b>"

crm(live)configure# colocation col_st_azure -2000: rsc_st_azure_1:Started rsc_st_azure_2:Started

crm(live)configure# commit
crm(live)configure# exit
</code></pre>

#### <a name="1-enable-hello-use-of-a-stonith-device"></a><span data-ttu-id="6a7dd-276">**[1]**  Activer l’utilisation de hello d’un périphérique STONITH</span><span class="sxs-lookup"><span data-stu-id="6a7dd-276">**[1]** Enable hello use of a STONITH device</span></span>

<pre><code>
sudo crm configure property stonith-enabled=true 
</code></pre>

## <a name="setting-up-ascs"></a><span data-ttu-id="6a7dd-277">Configuration de (A)SCS</span><span class="sxs-lookup"><span data-stu-id="6a7dd-277">Setting up (A)SCS</span></span>

### <a name="deploying-linux"></a><span data-ttu-id="6a7dd-278">Déploiement de Linux</span><span class="sxs-lookup"><span data-stu-id="6a7dd-278">Deploying Linux</span></span>

<span data-ttu-id="6a7dd-279">Bonjour Azure Marketplace contient une image pour SUSE Linux Enterprise Server 12 d’Applications SAP que vous pouvez utiliser les nouveaux ordinateurs virtuels de toodeploy.</span><span class="sxs-lookup"><span data-stu-id="6a7dd-279">hello Azure Marketplace contains an image for SUSE Linux Enterprise Server for SAP Applications 12 that you can use toodeploy new virtual machines.</span></span> <span data-ttu-id="6a7dd-280">image de marketplace Hello contient un agent de ressource de hello pour SAP NetWeaver.</span><span class="sxs-lookup"><span data-stu-id="6a7dd-280">hello marketplace image contains hello resource agent for SAP NetWeaver.</span></span>

<span data-ttu-id="6a7dd-281">Vous pouvez utiliser un des modèles de démarrage rapide de hello sur github toodeploy toutes les ressources requises.</span><span class="sxs-lookup"><span data-stu-id="6a7dd-281">You can use one of hello quick start templates on github toodeploy all required resources.</span></span> <span data-ttu-id="6a7dd-282">modèle de Hello déploie les machines virtuelles de hello, équilibrage de charge hello, haute disponibilité etc.. Suivez ces modèles de hello toodeploy comme suit :</span><span class="sxs-lookup"><span data-stu-id="6a7dd-282">hello template deploys hello virtual machines, hello load balancer, availability set etc. Follow these steps toodeploy hello template:</span></span>

1. <span data-ttu-id="6a7dd-283">Ouvrez hello [modèle du SID de multiples ASCS/SCS] [ template-multisid-xscs] ou hello [convergé modèle] [ template-converged] sur le modèle hello Azure hello portail ASCS/SCS uniquement crée des règles de l’équilibrage de charge de hello pour hello SAP NetWeaver ASCS/SCS et les instances ERS (Linux uniquement) alors que le modèle de convergé hello crée également des règles d’équilibrage de charge hello pour une base de données (par exemple Microsoft SQL Server ou SAP HANA).</span><span class="sxs-lookup"><span data-stu-id="6a7dd-283">Open hello [ASCS/SCS Multi SID template][template-multisid-xscs] or hello [converged template][template-converged] on hello Azure portal hello ASCS/SCS template only creates hello load-balancing rules for hello SAP NetWeaver ASCS/SCS and ERS (Linux only) instances whereas hello converged template also creates hello load-balancing rules for a database (for example Microsoft SQL Server or SAP HANA).</span></span> <span data-ttu-id="6a7dd-284">Si vous prévoyez d’un système SAP NetWeaver en fonction de tooinstall et que vous souhaitez également de base de données de tooinstall hello en hello les mêmes ordinateurs, utilisez hello [convergé modèle][template-converged].</span><span class="sxs-lookup"><span data-stu-id="6a7dd-284">If you plan tooinstall an SAP NetWeaver based system and you also want tooinstall hello database on hello same machines, use hello [converged template][template-converged].</span></span>
1. <span data-ttu-id="6a7dd-285">Entrez les paramètres suivants de hello</span><span class="sxs-lookup"><span data-stu-id="6a7dd-285">Enter hello following parameters</span></span>
   1. <span data-ttu-id="6a7dd-286">Préfixe de ressource (modèle ASCS/SCS Multi SID uniquement)</span><span class="sxs-lookup"><span data-stu-id="6a7dd-286">Resource Prefix (ASCS/SCS Multi SID template only)</span></span>  
      <span data-ttu-id="6a7dd-287">Entrez le préfixe hello toouse.</span><span class="sxs-lookup"><span data-stu-id="6a7dd-287">Enter hello prefix you want toouse.</span></span> <span data-ttu-id="6a7dd-288">valeur de Hello est utilisé en tant que préfixe pour les ressources hello qui sont déployés.</span><span class="sxs-lookup"><span data-stu-id="6a7dd-288">hello value is used as a prefix for hello resources that are deployed.</span></span>
   3. <span data-ttu-id="6a7dd-289">ID du système SAP (modèle convergé uniquement)</span><span class="sxs-lookup"><span data-stu-id="6a7dd-289">Sap System Id (converged template only)</span></span>  
      <span data-ttu-id="6a7dd-290">Entrez le système hello SAP Id Hello système SAP tooinstall.</span><span class="sxs-lookup"><span data-stu-id="6a7dd-290">Enter hello SAP system Id of hello SAP system you want tooinstall.</span></span> <span data-ttu-id="6a7dd-291">Hello Id est utilisé en tant que préfixe pour les ressources hello qui sont déployés.</span><span class="sxs-lookup"><span data-stu-id="6a7dd-291">hello Id is used as a prefix for hello resources that are deployed.</span></span>
   4. <span data-ttu-id="6a7dd-292">Type de pile</span><span class="sxs-lookup"><span data-stu-id="6a7dd-292">Stack Type</span></span>  
      <span data-ttu-id="6a7dd-293">Sélectionnez le type de pile hello SAP NetWeaver</span><span class="sxs-lookup"><span data-stu-id="6a7dd-293">Select hello SAP NetWeaver stack type</span></span>
   5. <span data-ttu-id="6a7dd-294">Type de système d’exploitation</span><span class="sxs-lookup"><span data-stu-id="6a7dd-294">Os Type</span></span>  
      <span data-ttu-id="6a7dd-295">Sélectionnez une des distributions de Linux hello.</span><span class="sxs-lookup"><span data-stu-id="6a7dd-295">Select one of hello Linux distributions.</span></span> <span data-ttu-id="6a7dd-296">Dans cet exemple, sélectionnez SLES 12 BYOS</span><span class="sxs-lookup"><span data-stu-id="6a7dd-296">For this example, select SLES 12 BYOS</span></span>
   6. <span data-ttu-id="6a7dd-297">Type de base de données</span><span class="sxs-lookup"><span data-stu-id="6a7dd-297">Db Type</span></span>  
      <span data-ttu-id="6a7dd-298">Sélectionnez HANA</span><span class="sxs-lookup"><span data-stu-id="6a7dd-298">Select HANA</span></span>
   7. <span data-ttu-id="6a7dd-299">Taille du système SAP</span><span class="sxs-lookup"><span data-stu-id="6a7dd-299">Sap System Size</span></span>  
      <span data-ttu-id="6a7dd-300">quantité Hello du nouveau système SAP hello fournit.</span><span class="sxs-lookup"><span data-stu-id="6a7dd-300">hello amount of SAPS hello new system provides.</span></span> <span data-ttu-id="6a7dd-301">Si vous n’êtes pas sûr du système de hello combien SAP, veuillez demander à votre partenaire technologique SAP ou l’intégrateur système</span><span class="sxs-lookup"><span data-stu-id="6a7dd-301">If you are not sure how many SAPS hello system requires, please ask your SAP Technology Partner or System Integrator</span></span>
   8. <span data-ttu-id="6a7dd-302">Disponibilité du système</span><span class="sxs-lookup"><span data-stu-id="6a7dd-302">System Availability</span></span>  
      <span data-ttu-id="6a7dd-303">Sélectionnez la haute disponibilité (HA).</span><span class="sxs-lookup"><span data-stu-id="6a7dd-303">Select HA</span></span>
   9. <span data-ttu-id="6a7dd-304">Nom d’utilisateur et mot de passe d’administrateur</span><span class="sxs-lookup"><span data-stu-id="6a7dd-304">Admin Username and Admin Password</span></span>  
      <span data-ttu-id="6a7dd-305">Création d’un utilisateur qui peut être utilisé toolog sur l’ordinateur de toohello.</span><span class="sxs-lookup"><span data-stu-id="6a7dd-305">A new user is created that can be used toolog on toohello machine.</span></span>
   10. <span data-ttu-id="6a7dd-306">ID du sous-réseau</span><span class="sxs-lookup"><span data-stu-id="6a7dd-306">Subnet Id</span></span>  
   <span data-ttu-id="6a7dd-307">ID de Hello d’ordinateurs virtuels hello sous-réseau toowhich hello doit être connecté à.</span><span class="sxs-lookup"><span data-stu-id="6a7dd-307">hello ID of hello subnet toowhich hello virtual machines should be connected to.</span></span>  <span data-ttu-id="6a7dd-308">Laissez vide si vous voulez toocreate un nouveau réseau virtuel ou sélectionnez hello même sous-réseau que vous utilisés ou créés dans le cadre du déploiement de serveur NFS hello.</span><span class="sxs-lookup"><span data-stu-id="6a7dd-308">Leave empty if you want toocreate a new virtual network or select hello same subnet that you used or created as part of hello NFS server deployment.</span></span> <span data-ttu-id="6a7dd-309">ID de Hello ressemble généralement à /subscriptions/**&lt;id d’abonnement&gt;**/resourceGroups/**&lt;nom de groupe de ressources&gt;**/providers/ Microsoft.Network/virtualNetworks/**&lt;nom de réseau virtuel&gt;**/subnets/**&lt;nom de sous-réseau&gt;**</span><span class="sxs-lookup"><span data-stu-id="6a7dd-309">hello ID usually looks like /subscriptions/**&lt;subscription id&gt;**/resourceGroups/**&lt;resource group name&gt;**/providers/Microsoft.Network/virtualNetworks/**&lt;virtual network name&gt;**/subnets/**&lt;subnet name&gt;**</span></span>

### <a name="installation"></a><span data-ttu-id="6a7dd-310">Installation</span><span class="sxs-lookup"><span data-stu-id="6a7dd-310">Installation</span></span>

<span data-ttu-id="6a7dd-311">Hello éléments suivants portent le préfixe soit **[A]** -tooall applicable nœuds, **[1]** -uniquement applicable toonode 1 ou **[2]** -uniquement applicable toonode 2.</span><span class="sxs-lookup"><span data-stu-id="6a7dd-311">hello following items are prefixed with either **[A]** - applicable tooall nodes, **[1]** - only applicable toonode 1 or **[2]** - only applicable toonode 2.</span></span>

1. <span data-ttu-id="6a7dd-312">**[A]** Mettre à jour SLES</span><span class="sxs-lookup"><span data-stu-id="6a7dd-312">**[A]** Update SLES</span></span>

   <pre><code>
   sudo zypper update
   </code></pre>

1. <span data-ttu-id="6a7dd-313">**[1]** Activer l’accès SSH</span><span class="sxs-lookup"><span data-stu-id="6a7dd-313">**[1]** Enable ssh access</span></span>

   <pre><code>
   sudo ssh-keygen -tdsa
   
   # Enter file in which toosave hello key (/root/.ssh/id_dsa): -> ENTER
   # Enter passphrase (empty for no passphrase): -> ENTER
   # Enter same passphrase again: -> ENTER
   
   # copy hello public key
   sudo cat /root/.ssh/id_dsa.pub
   </code></pre>

2. <span data-ttu-id="6a7dd-314">**[2**] Activer l’accès SSH</span><span class="sxs-lookup"><span data-stu-id="6a7dd-314">**[2]** Enable ssh access</span></span>

   <pre><code>
   sudo ssh-keygen -tdsa

   # insert hello public key you copied in hello last step into hello authorized keys file on hello second server
   sudo vi /root/.ssh/authorized_keys
   
   # Enter file in which toosave hello key (/root/.ssh/id_dsa): -> ENTER
   # Enter passphrase (empty for no passphrase): -> ENTER
   # Enter same passphrase again: -> ENTER
   
   # copy hello public key   
   sudo cat /root/.ssh/id_dsa.pub
   </code></pre>

1. <span data-ttu-id="6a7dd-315">**[1]** Activer l’accès SSH</span><span class="sxs-lookup"><span data-stu-id="6a7dd-315">**[1]** Enable ssh access</span></span>

   <pre><code>
   # insert hello public key you copied in hello last step into hello authorized keys file on hello first server
   sudo vi /root/.ssh/authorized_keys
   </code></pre>

1. <span data-ttu-id="6a7dd-316">**[A]** Installer l’extension de haute disponibilité</span><span class="sxs-lookup"><span data-stu-id="6a7dd-316">**[A]** Install HA extension</span></span>
   
   <pre><code>
   sudo zypper install sle-ha-release fence-agents
   </code></pre>

1. <span data-ttu-id="6a7dd-317">**[A]** Mettre à jour les agents de ressources SAP</span><span class="sxs-lookup"><span data-stu-id="6a7dd-317">**[A]** Update SAP resource agents</span></span>  
   
   <span data-ttu-id="6a7dd-318">Un correctif pour hello agents de la ressource est obligatoire toouse hello nouvelle configuration, qui est décrite dans cet article.</span><span class="sxs-lookup"><span data-stu-id="6a7dd-318">A patch for hello resource-agents package is required toouse hello new configuration, that is described in this article.</span></span> <span data-ttu-id="6a7dd-319">Vous pouvez vérifier si hello correctif est déjà installé avec hello commande suivante</span><span class="sxs-lookup"><span data-stu-id="6a7dd-319">You can check, if hello patch is already installed with hello following command</span></span>

   <pre><code>
   sudo grep 'parameter name="IS_ERS"' /usr/lib/ocf/resource.d/heartbeat/SAPInstance
   </code></pre>

   <span data-ttu-id="6a7dd-320">sortie de Hello doit être similaire à</span><span class="sxs-lookup"><span data-stu-id="6a7dd-320">hello output should be similar to</span></span>

   <pre><code>
   &lt;parameter name="IS_ERS" unique="0" required="0"&gt;
   </code></pre>

   <span data-ttu-id="6a7dd-321">Si la commande grep de hello ne trouve pas de paramètre IS_ERS hello, vous avez besoin de correctifs de hello tooinstall répertoriées sur [hello SUSE page de téléchargement](https://download.suse.com/patch/finder/#bu=suse&familyId=&productId=&dateRange=&startDate=&endDate=&priority=&architecture=&keywords=resource-agents)</span><span class="sxs-lookup"><span data-stu-id="6a7dd-321">If hello grep command does not find hello IS_ERS parameter, you need tooinstall hello patch listed on [hello SUSE download page](https://download.suse.com/patch/finder/#bu=suse&familyId=&productId=&dateRange=&startDate=&endDate=&priority=&architecture=&keywords=resource-agents)</span></span>

   <pre><code>
   # example for patch for SLES 12 SP1
   sudo zypper in -t patch SUSE-SLE-HA-12-SP1-2017-885=1
   # example for patch for SLES 12 SP2
   sudo zypper in -t patch SUSE-SLE-HA-12-SP2-2017-886=1
   </code></pre>

1. <span data-ttu-id="6a7dd-322">**[A]** Configurer la résolution de nom d’hôte</span><span class="sxs-lookup"><span data-stu-id="6a7dd-322">**[A]** Setup host name resolution</span></span>   

   <span data-ttu-id="6a7dd-323">Vous pouvez utiliser un serveur DNS ou modifier/etc/hosts de hello sur tous les nœuds.</span><span class="sxs-lookup"><span data-stu-id="6a7dd-323">You can either use a DNS server or modify hello /etc/hosts on all nodes.</span></span> <span data-ttu-id="6a7dd-324">Cet exemple montre comment toouse hello les fichier/etc/hosts.</span><span class="sxs-lookup"><span data-stu-id="6a7dd-324">This example shows how toouse hello /etc/hosts file.</span></span>
   <span data-ttu-id="6a7dd-325">Remplacez l’adresse IP de hello et un nom d’hôte hello Bonjour suivant les commandes</span><span class="sxs-lookup"><span data-stu-id="6a7dd-325">Replace hello IP address and hello hostname in hello following commands</span></span>

   <pre><code>
   sudo vi /etc/hosts
   </code></pre>
   
   <span data-ttu-id="6a7dd-326">Insérez hello suivant lignes trop/etc/hosts.</span><span class="sxs-lookup"><span data-stu-id="6a7dd-326">Insert hello following lines too/etc/hosts.</span></span> <span data-ttu-id="6a7dd-327">Modifiez les toomatch hello IP adresse et le nom d’hôte de votre environnement</span><span class="sxs-lookup"><span data-stu-id="6a7dd-327">Change hello IP address and hostname toomatch your environment</span></span>   
   
   <pre><code>
   # IP address of hello load balancer frontend configuration for NFS
   <b>10.0.0.4 nws-nfs</b>
   # IP address of hello load balancer frontend configuration for SAP NetWeaver ASCS/SCS
   <b>10.0.0.10 nws-ascs</b>
   # IP address of hello load balancer frontend configuration for SAP NetWeaver ERS
   <b>10.0.0.11 nws-ers</b>
   # IP address of hello load balancer frontend configuration for database
   <b>10.0.0.12 nws-db</b>
   </code></pre>

1. <span data-ttu-id="6a7dd-328">**[1]** Installer le cluster</span><span class="sxs-lookup"><span data-stu-id="6a7dd-328">**[1]** Install Cluster</span></span>
   
   <pre><code>
   sudo ha-cluster-init
   
   # Do you want toocontinue anyway? [y/N] -> y
   # Network address toobind too(for example: 192.168.1.0) [10.79.227.0] -> ENTER
   # Multicast address (for example: 239.x.x.x) [239.174.218.125] -> ENTER
   # Multicast port [5405] -> ENTER
   # Do you wish toouse SBD? [y/N] -> N
   # Do you wish tooconfigure an administration IP? [y/N] -> N
   </code></pre>

1. <span data-ttu-id="6a7dd-329">**[2]**  Ajouter toocluster de nœud</span><span class="sxs-lookup"><span data-stu-id="6a7dd-329">**[2]** Add node toocluster</span></span>
   
   <pre><code> 
   sudo ha-cluster-join

   # WARNING: NTP is not configured toostart at system boot.
   # WARNING: No watchdog device found. If SBD is used, hello cluster will be unable toostart without a watchdog.
   # Do you want toocontinue anyway? [y/N] -> y
   # IP address or hostname of existing node (for example: 192.168.1.1) [] -> IP address of node 1 for example 10.0.0.10
   # /root/.ssh/id_dsa already exists - overwrite? [y/N] N
   </code></pre>

1. <span data-ttu-id="6a7dd-330">**[A]**  Toohello de mot de passe de modification hacluster même mot de passe</span><span class="sxs-lookup"><span data-stu-id="6a7dd-330">**[A]** Change hacluster password toohello same password</span></span>

   <pre><code> 
   sudo passwd hacluster
   </code></pre>

1. <span data-ttu-id="6a7dd-331">**[A]**  Configurer corosync toouse autre transport et ajouter la liste de nœuds.</span><span class="sxs-lookup"><span data-stu-id="6a7dd-331">**[A]** Configure corosync toouse other transport and add nodelist.</span></span> <span data-ttu-id="6a7dd-332">Le cluster ne fonctionnera pas dans le cas contraire.</span><span class="sxs-lookup"><span data-stu-id="6a7dd-332">Cluster will not work otherwise.</span></span>
   
   <pre><code> 
   sudo vi /etc/corosync/corosync.conf   
   </code></pre>

   <span data-ttu-id="6a7dd-333">Ajoutez hello toohello contenu gras le fichier suivant.</span><span class="sxs-lookup"><span data-stu-id="6a7dd-333">Add hello following bold content toohello file.</span></span>
   
   <pre><code> 
   [...]
     interface { 
        [...] 
     }
     <b>transport:      udpu</b>
   } 
   <b>nodelist {
     node {
      # IP address of <b>nws-cl-0</b>
      ring0_addr:     10.0.0.14
     }
     node {
      # IP address of <b>nws-cl-1</b>
      ring0_addr:     10.0.0.13
     } 
   }</b>
   logging {
     [...]
   </code></pre>

   <span data-ttu-id="6a7dd-334">Ensuite, redémarrez le service corosync hello</span><span class="sxs-lookup"><span data-stu-id="6a7dd-334">Then restart hello corosync service</span></span>

   <pre><code>
   sudo service corosync restart
   </code></pre>

1. <span data-ttu-id="6a7dd-335">**[A]** Installer les composants drbd</span><span class="sxs-lookup"><span data-stu-id="6a7dd-335">**[A]** Install drbd components</span></span>

   <pre><code>
   sudo zypper install drbd drbd-kmp-default drbd-utils
   </code></pre>

1. <span data-ttu-id="6a7dd-336">**[A]**  Créer une partition pour appareil de drbd hello</span><span class="sxs-lookup"><span data-stu-id="6a7dd-336">**[A]** Create a partition for hello drbd device</span></span>

   <pre><code>
   sudo sh -c 'echo -e "n\n\n\n\n\nw\n" | fdisk /dev/sdc'
   </code></pre>

1. <span data-ttu-id="6a7dd-337">**[A]** Créer des configurations LVM</span><span class="sxs-lookup"><span data-stu-id="6a7dd-337">**[A]** Create LVM configurations</span></span>

   <pre><code>
   sudo pvcreate /dev/sdc1   
   sudo vgcreate vg_<b>NWS</b> /dev/sdc1
   sudo lvcreate -l 50%FREE -n <b>NWS</b>_ASCS vg_<b>NWS</b>
   sudo lvcreate -l 50%FREE -n <b>NWS</b>_ERS vg_<b>NWS</b>
   </code></pre>

1. <span data-ttu-id="6a7dd-338">**[A]**  Dispositif de drbd créer hello SCS</span><span class="sxs-lookup"><span data-stu-id="6a7dd-338">**[A]** Create hello SCS drbd device</span></span>

   <pre><code>
   sudo vi /etc/drbd.d/<b>NWS</b>_ascs.res
   </code></pre>

   <span data-ttu-id="6a7dd-339">Insérer configuration hello pour le nouveau périphérique de drbd hello et quitter</span><span class="sxs-lookup"><span data-stu-id="6a7dd-339">Insert hello configuration for hello new drbd device and exit</span></span>

   <pre><code>
   resource <b>NWS</b>_ascs {
      protocol     C;
      disk {
         on-io-error       pass_on;
      }
      on <b>nws-cl-0</b> {
         address   <b>10.0.0.14</b>:7791;
         device    /dev/drbd0;
         disk      /dev/vg_NWS/NWS_ASCS;
         meta-disk internal;
      }
      on <b>nws-cl-1</b> {
         address   <b>10.0.0.13</b>:7791;
         device    /dev/drbd0;
         disk      /dev/vg_NWS/NWS_ASCS;
         meta-disk internal;
      }
   }
   </code></pre>

   <span data-ttu-id="6a7dd-340">Créer un appareil drbd hello et démarrez-le</span><span class="sxs-lookup"><span data-stu-id="6a7dd-340">Create hello drbd device and start it</span></span>

   <pre><code>
   sudo drbdadm create-md <b>NWS</b>_ascs
   sudo drbdadm up <b>NWS</b>_ascs
   </code></pre>

1. <span data-ttu-id="6a7dd-341">**[A]**  Dispositif de drbd créer hello ERS</span><span class="sxs-lookup"><span data-stu-id="6a7dd-341">**[A]** Create hello ERS drbd device</span></span>

   <pre><code>
   sudo vi /etc/drbd.d/<b>NWS</b>_ers.res
   </code></pre>

   <span data-ttu-id="6a7dd-342">Insérer configuration hello pour le nouveau périphérique de drbd hello et quitter</span><span class="sxs-lookup"><span data-stu-id="6a7dd-342">Insert hello configuration for hello new drbd device and exit</span></span>

   <pre><code>
   resource <b>NWS</b>_ers {
      protocol     C;
      disk {
         on-io-error       pass_on;
      }
      on <b>nws-cl-0</b> {
         address   <b>10.0.0.14</b>:7792;
         device    /dev/drbd1;
         disk      /dev/vg_NWS/NWS_ERS;
         meta-disk internal;
      }
      on <b>nws-cl-1</b> {
         address   <b>10.0.0.13</b>:7792;
         device    /dev/drbd1;
         disk      /dev/vg_NWS/NWS_ERS;
         meta-disk internal;
      }
   }
   </code></pre>

   <span data-ttu-id="6a7dd-343">Créer un appareil drbd hello et démarrez-le</span><span class="sxs-lookup"><span data-stu-id="6a7dd-343">Create hello drbd device and start it</span></span>

   <pre><code>
   sudo drbdadm create-md <b>NWS</b>_ers
   sudo drbdadm up <b>NWS</b>_ers
   </code></pre>

1. <span data-ttu-id="6a7dd-344">**[1]** Ignorer la synchronisation initiale</span><span class="sxs-lookup"><span data-stu-id="6a7dd-344">**[1]** Skip initial synchronization</span></span>

   <pre><code>
   sudo drbdadm new-current-uuid --clear-bitmap <b>NWS</b>_ascs
   sudo drbdadm new-current-uuid --clear-bitmap <b>NWS</b>_ers
   </code></pre>

1. <span data-ttu-id="6a7dd-345">**[1]**  Nœud principal de l’ensemble hello</span><span class="sxs-lookup"><span data-stu-id="6a7dd-345">**[1]** Set hello primary node</span></span>

   <pre><code>
   sudo drbdadm primary --force <b>NWS</b>_ascs
   sudo drbdadm primary --force <b>NWS</b>_ers
   </code></pre>

1. <span data-ttu-id="6a7dd-346">**[1]**  Patienter jusqu'à ce que les nouveaux appareils de drbd hello sont synchronisés</span><span class="sxs-lookup"><span data-stu-id="6a7dd-346">**[1]** Wait until hello new drbd devices are synchronized</span></span>

   <pre><code>
   sudo cat /proc/drbd

   # version: 8.4.6 (api:1/proto:86-101)
   # GIT-hash: 833d830e0152d1e457fa7856e71e11248ccf3f70 build by abuild@sheep14, 2016-05-09 23:14:56
   # 0: cs:<b>Connected</b> ro:Primary/Secondary ds:<b>UpToDate/UpToDate</b> C r-----
   #     ns:93991268 nr:0 dw:93991268 dr:93944920 al:383 bm:0 lo:0 pe:0 ua:0 ap:0 ep:1 wo:f oos:0
   # 1: cs:<b>Connected</b> ro:Primary/Secondary ds:<b>UpToDate/UpToDate</b> C r-----
   #     ns:6047920 nr:0 dw:6047920 dr:6039112 al:34 bm:0 lo:0 pe:0 ua:0 ap:0 ep:1 wo:f oos:0
   # 2: cs:<b>Connected</b> ro:Primary/Secondary ds:<b>UpToDate/UpToDate</b> C r-----
   #     ns:5142732 nr:0 dw:5142732 dr:5133924 al:30 bm:0 lo:0 pe:0 ua:0 ap:0 ep:1 wo:f oos:0
   </code></pre>

1. <span data-ttu-id="6a7dd-347">**[1]**  Créer des systèmes de fichiers sur hello drbd périphériques</span><span class="sxs-lookup"><span data-stu-id="6a7dd-347">**[1]** Create file systems on hello drbd devices</span></span>

   <pre><code>
   sudo mkfs.xfs /dev/drbd0
   sudo mkfs.xfs /dev/drbd1
   </code></pre>


### <a name="configure-cluster-framework"></a><span data-ttu-id="6a7dd-348">Configurer le framework du cluster</span><span class="sxs-lookup"><span data-stu-id="6a7dd-348">Configure Cluster Framework</span></span>

<span data-ttu-id="6a7dd-349">**[1]**  Modifier les paramètres par défaut de hello</span><span class="sxs-lookup"><span data-stu-id="6a7dd-349">**[1]** Change hello default settings</span></span>

   <pre><code>
   sudo crm configure

   crm(live)configure# rsc_defaults resource-stickiness="1"

   crm(live)configure# commit
   crm(live)configure# exit
   </code></pre>

## <a name="prepare-for-sap-netweaver-installation"></a><span data-ttu-id="6a7dd-350">Préparer l’installation de SAP NetWeaver</span><span class="sxs-lookup"><span data-stu-id="6a7dd-350">Prepare for SAP NetWeaver installation</span></span>

1. <span data-ttu-id="6a7dd-351">**[A]**  Hello de créer les répertoires partagés</span><span class="sxs-lookup"><span data-stu-id="6a7dd-351">**[A]** Create hello shared directories</span></span>

   <pre><code>
   sudo mkdir -p /sapmnt/<b>NWS</b>
   sudo mkdir -p /usr/sap/trans
   sudo mkdir -p /usr/sap/<b>NWS</b>/SYS

   sudo chattr +i /sapmnt/<b>NWS</b>
   sudo chattr +i /usr/sap/trans
   sudo chattr +i /usr/sap/<b>NWS</b>/SYS
   </code></pre>

1. <span data-ttu-id="6a7dd-352">**[A]** Configurer autofs</span><span class="sxs-lookup"><span data-stu-id="6a7dd-352">**[A]** Configure autofs</span></span>
 
   <pre><code>
   sudo vi /etc/auto.master

   # Add hello following line toohello file, save and exit
   +auto.master
   /- /etc/auto.direct
   </code></pre>

   <span data-ttu-id="6a7dd-353">Créer un fichier avec</span><span class="sxs-lookup"><span data-stu-id="6a7dd-353">Create a file with</span></span>

   <pre><code>
   sudo vi /etc/auto.direct

   # Add hello following lines toohello file, save and exit
   /sapmnt/<b>NWS</b> -nfsvers=4,nosymlink,sync <b>nws-nfs</b>:/sapmntsid
   /usr/sap/trans -nfsvers=4,nosymlink,sync <b>nws-nfs</b>:/trans
   /usr/sap/<b>NWS</b>/SYS -nfsvers=4,nosymlink,sync <b>nws-nfs</b>:/sidsys
   </code></pre>

   <span data-ttu-id="6a7dd-354">Redémarrez les nouveaux partages autofs toomount hello</span><span class="sxs-lookup"><span data-stu-id="6a7dd-354">Restart autofs toomount hello new shares</span></span>

   <pre><code>
   sudo systemctl enable autofs
   sudo service autofs restart
   </code></pre>

1. <span data-ttu-id="6a7dd-355">**[A]** Configurer le fichier SWAP</span><span class="sxs-lookup"><span data-stu-id="6a7dd-355">**[A]** Configure SWAP file</span></span>
 
   <pre><code>
   sudo vi /etc/waagent.conf

   # Set hello property ResourceDisk.EnableSwap tooy
   # Create and use swapfile on resource disk.
   ResourceDisk.EnableSwap=<b>y</b>

   # Set hello size of hello SWAP file with property ResourceDisk.SwapSizeMB
   # hello free space of resource disk varies by virtual machine size. Make sure that you do not set a value that is too big. You can check hello SWAP space with command swapon
   # Size of hello swapfile.
   ResourceDisk.SwapSizeMB=<b>2000</b>
   </code></pre>

   <span data-ttu-id="6a7dd-356">Redémarrez le changement d’hello hello Agent tooactivate</span><span class="sxs-lookup"><span data-stu-id="6a7dd-356">Restart hello Agent tooactivate hello change</span></span>

   <pre><code>
   sudo service waagent restart
   </code></pre>

### <a name="installing-sap-netweaver-ascsers"></a><span data-ttu-id="6a7dd-357">Installation de SAP NetWeaver ASC/ERS</span><span class="sxs-lookup"><span data-stu-id="6a7dd-357">Installing SAP NetWeaver ASCS/ERS</span></span>

1. <span data-ttu-id="6a7dd-358">**[1]**  Créer une ressource IP virtuel et un contrôle d’intégrité-sonde d’équilibreur de charge interne hello</span><span class="sxs-lookup"><span data-stu-id="6a7dd-358">**[1]** Create a virtual IP resource and health-probe for hello internal load balancer</span></span>

   <pre><code>
   sudo crm node standby <b>nws-cl-1</b>
   sudo crm configure

   crm(live)configure# primitive drbd_<b>NWS</b>_ASCS \
     ocf:linbit:drbd \
     params drbd_resource="<b>NWS</b>_ascs" \
     op monitor interval="15" role="Master" \
     op monitor interval="30" role="Slave"

   crm(live)configure# ms ms-drbd_<b>NWS</b>_ASCS drbd_<b>NWS</b>_ASCS \
     meta master-max="1" master-node-max="1" clone-max="2" \
     clone-node-max="1" notify="true"

   crm(live)configure# primitive fs_<b>NWS</b>_ASCS \
     ocf:heartbeat:Filesystem \
     params device=/dev/drbd0 \
     directory=/usr/sap/<b>NWS</b>/ASCS<b>00</b>  \
     fstype=xfs \
     op monitor interval="10s"

   crm(live)configure# primitive vip_<b>NWS</b>_ASCS IPaddr2 \
     params ip=<b>10.0.0.10</b> cidr_netmask=24 \
     op monitor interval=10 timeout=20

   crm(live)configure# primitive nc_<b>NWS</b>_ASCS anything \
     params binfile="/usr/bin/nc" cmdline_options="-l -k 620<b>00</b>" \
     op monitor timeout=20s interval=10 depth=0
   
   crm(live)configure# group g-<b>NWS</b>_ASCS nc_<b>NWS</b>_ASCS vip_<b>NWS</b>_ASCS fs_<b>NWS</b>_ASCS \
      meta resource-stickiness=3000

   crm(live)configure# order o-<b>NWS</b>_drbd_before_ASCS inf: \
     ms-drbd_<b>NWS</b>_ASCS:promote g-<b>NWS</b>_ASCS:start
   
   crm(live)configure# colocation col-<b>NWS</b>_ASCS_on_drbd inf: \
     ms-drbd_<b>NWS</b>_ASCS:Master g-<b>NWS</b>_ASCS
   
   crm(live)configure# commit
   crm(live)configure# exit
   </code></pre>

   <span data-ttu-id="6a7dd-359">Assurez-vous que l’état du cluster hello est OK et que toutes les ressources sont démarrés.</span><span class="sxs-lookup"><span data-stu-id="6a7dd-359">Make sure that hello cluster status is ok and that all resources are started.</span></span> <span data-ttu-id="6a7dd-360">Il n’est pas important sur les ressources de hello de nœud sont en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="6a7dd-360">It is not important on which node hello resources are running.</span></span>

   <pre><code>
   sudo crm_mon -r

   # Node nws-cl-1: standby
   # <b>Online: [ nws-cl-0 ]</b>
   # 
   # Full list of resources:
   # 
   #  Master/Slave Set: ms-drbd_NWS_ASCS [drbd_NWS_ASCS]
   #      <b>Masters: [ nws-cl-0 ]</b>
   #      Stopped: [ nws-cl-1 ]
   #  Resource Group: g-NWS_ASCS
   #      nc_NWS_ASCS        (ocf::heartbeat:anything):      <b>Started nws-cl-0</b>
   #      vip_NWS_ASCS       (ocf::heartbeat:IPaddr2):       <b>Started nws-cl-0</b>
   #      fs_NWS_ASCS        (ocf::heartbeat:Filesystem):    <b>Started nws-cl-0</b>
   </code></pre>

1. <span data-ttu-id="6a7dd-361">**[1]** Installer SAP NetWeaver ASCS</span><span class="sxs-lookup"><span data-stu-id="6a7dd-361">**[1]** Install SAP NetWeaver ASCS</span></span>  

   <span data-ttu-id="6a7dd-362">Installation de SAP NetWeaver ASC en tant que racine sur hello premier nœud à l’aide d’un nom d’hôte virtuel qui mappe les adresses IP de toohello de configuration de serveur frontal d’équilibrage de charge de hello pour hello ASC par exemple <b>nws-ASC</b>, <b>10.0.0.10</b>et numéro d’instance hello que vous avez utilisé pour la sonde hello d’équilibrage de charge hello, par exemple <b>00</b>.</span><span class="sxs-lookup"><span data-stu-id="6a7dd-362">Install SAP NetWeaver ASCS as root on hello first node using a virtual hostname that maps toohello IP address of hello load balancer frontend configuration for hello ASCS for example <b>nws-ascs</b>, <b>10.0.0.10</b> and hello instance number that you used for hello probe of hello load balancer for example <b>00</b>.</span></span>

   <span data-ttu-id="6a7dd-363">Vous pouvez utiliser hello sapinst paramètre SAPINST_REMOTE_ACCESS_USER tooallow un toosapinst de tooconnect utilisateur non racine.</span><span class="sxs-lookup"><span data-stu-id="6a7dd-363">You can use hello sapinst parameter SAPINST_REMOTE_ACCESS_USER tooallow a non-root user tooconnect toosapinst.</span></span>

   <pre><code>
   sudo &lt;swpm&gt;/sapinst SAPINST_REMOTE_ACCESS_USER=<b>sapadmin</b>
   </code></pre>

1. <span data-ttu-id="6a7dd-364">**[1]**  Créer une ressource IP virtuel et un contrôle d’intégrité-sonde d’équilibreur de charge interne hello</span><span class="sxs-lookup"><span data-stu-id="6a7dd-364">**[1]** Create a virtual IP resource and health-probe for hello internal load balancer</span></span>

   <pre><code>
   sudo crm node standby <b>nws-cl-0</b>
   sudo crm node online <b>nws-cl-1</b>
   sudo crm configure

   crm(live)configure# primitive drbd_<b>NWS</b>_ERS \
     ocf:linbit:drbd \
     params drbd_resource="<b>NWS</b>_ers" \
     op monitor interval="15" role="Master" \
     op monitor interval="30" role="Slave"

   crm(live)configure# ms ms-drbd_<b>NWS</b>_ERS drbd_<b>NWS</b>_ERS \
     meta master-max="1" master-node-max="1" clone-max="2" \
     clone-node-max="1" notify="true"

   crm(live)configure# primitive fs_<b>NWS</b>_ERS \
     ocf:heartbeat:Filesystem \
     params device=/dev/drbd1 \
     directory=/usr/sap/<b>NWS</b>/ERS<b>02</b>  \
     fstype=xfs \
     op monitor interval="10s"

   crm(live)configure# primitive vip_<b>NWS</b>_ERS IPaddr2 \
     params ip=<b>10.0.0.11</b> cidr_netmask=24 \
     op monitor interval=10 timeout=20

   crm(live)configure# primitive nc_<b>NWS</b>_ERS anything \
    params binfile="/usr/bin/nc" cmdline_options="-l -k 621<b>02</b>" \
    op monitor timeout=20s interval=10 depth=0

   crm(live)configure# group g-<b>NWS</b>_ERS nc_<b>NWS</b>_ERS vip_<b>NWS</b>_ERS fs_<b>NWS</b>_ERS

   crm(live)configure# order o-<b>NWS</b>_drbd_before_ERS inf: \
     ms-drbd_<b>NWS</b>_ERS:promote g-<b>NWS</b>_ERS:start
   
   crm(live)configure# colocation col-<b>NWS</b>_ERS_on_drbd inf: \
     ms-drbd_<b>NWS</b>_ERS:Master g-<b>NWS</b>_ERS
   
   crm(live)configure# commit
   # WARNING: Resources nc_NWS_ASCS,nc_NWS_ERS,nc_NWS_nfs violate uniqueness for parameter "binfile": "/usr/bin/nc"
   # Do you still want toocommit (y/n)? y

   crm(live)configure# exit
   
   </code></pre>
 
   <span data-ttu-id="6a7dd-365">Assurez-vous que l’état du cluster hello est OK et que toutes les ressources sont démarrés.</span><span class="sxs-lookup"><span data-stu-id="6a7dd-365">Make sure that hello cluster status is ok and that all resources are started.</span></span> <span data-ttu-id="6a7dd-366">Il n’est pas important sur les ressources de hello de nœud sont en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="6a7dd-366">It is not important on which node hello resources are running.</span></span>

   <pre><code>
   sudo crm_mon -r

   # Node <b>nws-cl-0: standby</b>
   # <b>Online: [ nws-cl-1 ]</b>
   # 
   # Full list of resources:
   # 
   #  Master/Slave Set: ms-drbd_NWS_ASCS [drbd_NWS_ASCS]
   #      <b>Masters: [ nws-cl-1 ]</b>
   #      Stopped: [ nws-cl-0 ]
   #  Resource Group: g-NWS_ASCS
   #      nc_NWS_ASCS        (ocf::heartbeat:anything):      <b>Started nws-cl-1</b>
   #      vip_NWS_ASCS       (ocf::heartbeat:IPaddr2):       <b>Started nws-cl-1</b>
   #      fs_NWS_ASCS        (ocf::heartbeat:Filesystem):    <b>Started nws-cl-1</b>
   #  Master/Slave Set: ms-drbd_NWS_ERS [drbd_NWS_ERS]
   #      <b>Masters: [ nws-cl-1 ]</b>
   #      Stopped: [ nws-cl-0 ]
   #  Resource Group: g-NWS_ERS
   #      nc_NWS_ERS (ocf::heartbeat:anything):      <b>Started nws-cl-1</b>
   #      vip_NWS_ERS        (ocf::heartbeat:IPaddr2):       <b>Started nws-cl-1</b>
   #      fs_NWS_ERS (ocf::heartbeat:Filesystem):    <b>Started nws-cl-1</b>
   </code></pre>

1. <span data-ttu-id="6a7dd-367">**[2]** Installer SAP NetWeaver ERS</span><span class="sxs-lookup"><span data-stu-id="6a7dd-367">**[2]** Install SAP NetWeaver ERS</span></span>  

   <span data-ttu-id="6a7dd-368">Installation de SAP NetWeaver ERS en tant que racine sur le nœud de deuxième hello à l’aide d’un nom d’hôte virtuel qui mappe les adresses IP de toohello de configuration de serveur frontal d’équilibrage de charge de hello pour hello ERS par exemple <b>nws-ers</b>, <b>10.0.0.11</b> et le numéro d’instance hello que vous avez utilisé pour la sonde hello d’équilibrage de charge hello, par exemple <b>02</b>.</span><span class="sxs-lookup"><span data-stu-id="6a7dd-368">Install SAP NetWeaver ERS as root on hello second node using a virtual hostname that maps toohello IP address of hello load balancer frontend configuration for hello ERS for example <b>nws-ers</b>, <b>10.0.0.11</b> and hello instance number that you used for hello probe of hello load balancer for example <b>02</b>.</span></span>

   <span data-ttu-id="6a7dd-369">Vous pouvez utiliser hello sapinst paramètre SAPINST_REMOTE_ACCESS_USER tooallow un toosapinst de tooconnect utilisateur non racine.</span><span class="sxs-lookup"><span data-stu-id="6a7dd-369">You can use hello sapinst parameter SAPINST_REMOTE_ACCESS_USER tooallow a non-root user tooconnect toosapinst.</span></span>

   <pre><code>
   sudo &lt;swpm&gt;/sapinst SAPINST_REMOTE_ACCESS_USER=<b>sapadmin</b>
   </code></pre>

   > [!NOTE]
   > <span data-ttu-id="6a7dd-370">Utilisez SWPM SP 20 PL 05 ou ultérieur.</span><span class="sxs-lookup"><span data-stu-id="6a7dd-370">Please use SWPM SP 20 PL 05 or higher.</span></span> <span data-ttu-id="6a7dd-371">Versions inférieures ne définissez pas correctement les autorisations de hello et hello installation échouera.</span><span class="sxs-lookup"><span data-stu-id="6a7dd-371">Lower versions do not set hello permissions correctly and hello installation will fail.</span></span>
   > 

1. <span data-ttu-id="6a7dd-372">**[1]**  Adapter hello ASCS/SCS et ERS instance des profils</span><span class="sxs-lookup"><span data-stu-id="6a7dd-372">**[1]** Adapt hello ASCS/SCS and ERS instance profiles</span></span>
 
   * <span data-ttu-id="6a7dd-373">Profil ASCS/SCS</span><span class="sxs-lookup"><span data-stu-id="6a7dd-373">ASCS/SCS profile</span></span>

   <pre><code> 
   sudo vi /sapmnt/<b>NWS</b>/profile/<b>NWS</b>_<b>ASCS00</b>_<b>nws-ascs</b>

   # Change hello restart command tooa start command
   #Restart_Program_01 = local $(_EN) pf=$(_PF)
   Start_Program_01 = local $(_EN) pf=$(_PF)

   # Add hello following lines
   service/halib = $(DIR_CT_RUN)/saphascriptco.so
   service/halib_cluster_connector = /usr/bin/sap_suse_cluster_connector

   # Add hello keep alive parameter
   enque/encni/set_so_keepalive = true
   </code></pre>

   * <span data-ttu-id="6a7dd-374">Profil ERS</span><span class="sxs-lookup"><span data-stu-id="6a7dd-374">ERS profile</span></span>

   <pre><code> 
   sudo vi /sapmnt/<b>NWS</b>/profile/<b>NWS</b>_ERS<b>02</b>_<b>nws-ers</b>

   # Add hello following lines
   service/halib = $(DIR_CT_RUN)/saphascriptco.so
   service/halib_cluster_connector = /usr/bin/sap_suse_cluster_connector
   </code></pre>


1. <span data-ttu-id="6a7dd-375">**[A]** Configurer Keep Alive</span><span class="sxs-lookup"><span data-stu-id="6a7dd-375">**[A]** Configure Keep Alive</span></span>

   <span data-ttu-id="6a7dd-376">communication Hello entre le serveur d’applications SAP NetWeaver hello et hello ASCS/SCS est routée via un équilibrage de charge du logiciel.</span><span class="sxs-lookup"><span data-stu-id="6a7dd-376">hello communication between hello SAP NetWeaver application server and hello ASCS/SCS is routed through a software load balancer.</span></span> <span data-ttu-id="6a7dd-377">équilibrage de charge Hello déconnecte les connexions inactives après un délai configurable.</span><span class="sxs-lookup"><span data-stu-id="6a7dd-377">hello load balancer disconnects inactive connections after a configurable timeout.</span></span> <span data-ttu-id="6a7dd-378">tooprevent vous devez tooset un paramètre dans le profil de SAP NetWeaver ASCS/SCS de hello et modifiez les paramètres de système de Linux hello.</span><span class="sxs-lookup"><span data-stu-id="6a7dd-378">tooprevent this you need tooset a parameter in hello SAP NetWeaver ASCS/SCS profile and change hello Linux system settings.</span></span> <span data-ttu-id="6a7dd-379">Pour plus d’informations, consultez la [Note SAP 1410736][1410736].</span><span class="sxs-lookup"><span data-stu-id="6a7dd-379">Please read [SAP Note 1410736][1410736] for more information.</span></span>
   
   <span data-ttu-id="6a7dd-380">Hello ASCS/SCS profil paramètre terminer/encni/set_so_keepalive a déjà été ajoutée dans la dernière étape de hello.</span><span class="sxs-lookup"><span data-stu-id="6a7dd-380">hello ASCS/SCS profile parameter enque/encni/set_so_keepalive was already added in hello last step.</span></span>

   <pre><code> 
   # Change hello Linux system configuration
   sudo sysctl net.ipv4.tcp_keepalive_time=120
   </code></pre>

1. <span data-ttu-id="6a7dd-381">**[A]**  Configurer des utilisateurs SAP hello après l’installation de hello</span><span class="sxs-lookup"><span data-stu-id="6a7dd-381">**[A]** Configure hello SAP users after hello installation</span></span>
 
   <pre><code>
   # Add sidadm toohello haclient group
   sudo usermod -aG haclient <b>nws</b>adm   
   </code></pre>

1. <span data-ttu-id="6a7dd-382">**[1]**  Ajouter hello ASC et ERS SAP toohello sapservice fichier services</span><span class="sxs-lookup"><span data-stu-id="6a7dd-382">**[1]** Add hello ASCS and ERS SAP services toohello sapservice file</span></span>

   <span data-ttu-id="6a7dd-383">Ajouter hello ASC service entrée toohello second nœud et copie hello ERS service toohello premier nœud d’entrée.</span><span class="sxs-lookup"><span data-stu-id="6a7dd-383">Add hello ASCS service entry toohello second node and copy hello ERS service entry toohello first node.</span></span>

   <pre><code>
   cat /usr/sap/sapservices | grep ASCS<b>00</b> | sudo ssh <b>nws-cl-1</b> "cat >>/usr/sap/sapservices"
   sudo ssh <b>nws-cl-1</b> "cat /usr/sap/sapservices" | grep ERS<b>02</b> | sudo tee -a /usr/sap/sapservices
   </code></pre>

1. <span data-ttu-id="6a7dd-384">**[1]**  Créer des ressources de cluster hello SAP</span><span class="sxs-lookup"><span data-stu-id="6a7dd-384">**[1]** Create hello SAP cluster resources</span></span>

   <pre><code>
   sudo crm configure property maintenance-mode="true"

   sudo crm configure

   crm(live)configure# primitive rsc_sap_<b>NWS</b>_ASCS<b>00</b> SAPInstance \
    operations $id=rsc_sap_<b>NWS</b>_ASCS<b>00</b>-operations \
    op monitor interval=11 timeout=60 on_fail=restart \
    params InstanceName=<b>NWS</b>_ASCS<b>00</b>_<b>nws-ascs</b> START_PROFILE="/sapmnt/<b>NWS</b>/profile/<b>NWS</b>_ASCS<b>00</b>_<b>nws-ascs</b>" \
    AUTOMATIC_RECOVER=false \
    meta resource-stickiness=5000 failure-timeout=60 migration-threshold=1 priority=10

   crm(live)configure# primitive rsc_sap_<b>NWS</b>_ERS<b>02</b> SAPInstance \
    operations $id=rsc_sap_<b>NWS</b>_ERS<b>02</b>-operations \
    op monitor interval=11 timeout=60 on_fail=restart \
    params InstanceName=<b>NWS</b>_ERS<b>02</b>_<b>nws-ers</b> START_PROFILE="/sapmnt/<b>NWS</b>/profile/<b>NWS</b>_ERS<b>02</b>_<b>nws-ers</b>" AUTOMATIC_RECOVER=false IS_ERS=true \
    meta priority=1000

   crm(live)configure# modgroup g-<b>NWS</b>_ASCS add rsc_sap_<b>NWS</b>_ASCS<b>00</b>
   crm(live)configure# modgroup g-<b>NWS</b>_ERS add rsc_sap_<b>NWS</b>_ERS<b>02</b>

   crm(live)configure# colocation col_sap_<b>NWS</b>_no_both -5000: g-<b>NWS</b>_ERS g-<b>NWS</b>_ASCS
   crm(live)configure# location loc_sap_<b>NWS</b>_failover_to_ers rsc_sap_<b>NWS</b>_ASCS<b>00</b> rule 2000: runs_ers_<b>NWS</b> eq 1
   crm(live)configure# order ord_sap_<b>NWS</b>_first_start_ascs Optional: rsc_sap_<b>NWS</b>_ASCS<b>00</b>:start rsc_sap_<b>NWS</b>_ERS<b>02</b>:stop symmetrical=false

   crm(live)configure# commit
   crm(live)configure# exit

   sudo crm configure property maintenance-mode="false"
   sudo crm node online <b>nws-cl-0</b>
   </code></pre>

   <span data-ttu-id="6a7dd-385">Assurez-vous que l’état du cluster hello est OK et que toutes les ressources sont démarrés.</span><span class="sxs-lookup"><span data-stu-id="6a7dd-385">Make sure that hello cluster status is ok and that all resources are started.</span></span> <span data-ttu-id="6a7dd-386">Il n’est pas important sur les ressources de hello de nœud sont en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="6a7dd-386">It is not important on which node hello resources are running.</span></span>

   <pre><code>
   sudo crm_mon -r

   # Online: <b>[ nws-cl-0 nws-cl-1 ]</b>
   # 
   # Full list of resources:
   # 
   #  Master/Slave Set: ms-drbd_NWS_ASCS [drbd_NWS_ASCS]
   #      <b>Masters: [ nws-cl-0 ]</b>
   #      <b>Slaves: [ nws-cl-1 ]</b>
   #  Resource Group: g-NWS_ASCS
   #      nc_NWS_ASCS        (ocf::heartbeat:anything):      <b>Started nws-cl-0</b>
   #      vip_NWS_ASCS       (ocf::heartbeat:IPaddr2):       <b>Started nws-cl-0</b>
   #      fs_NWS_ASCS        (ocf::heartbeat:Filesystem):    <b>Started nws-cl-0</b>
   #      rsc_sap_NWS_ASCS00 (ocf::heartbeat:SAPInstance):   <b>Started nws-cl-0</b>
   #  Master/Slave Set: ms-drbd_NWS_ERS [drbd_NWS_ERS]
   #      <b>Masters: [ nws-cl-1 ]</b>
   #      <b>Slaves: [ nws-cl-0 ]</b>
   #  Resource Group: g-NWS_ERS
   #      nc_NWS_ERS (ocf::heartbeat:anything):      <b>Started nws-cl-1</b>
   #      vip_NWS_ERS        (ocf::heartbeat:IPaddr2):       <b>Started nws-cl-1</b>
   #      fs_NWS_ERS (ocf::heartbeat:Filesystem):    <b>Started nws-cl-1</b>
   #      rsc_sap_NWS_ERS02  (ocf::heartbeat:SAPInstance):   <b>Started nws-cl-1</b>
   </code></pre>

### <a name="create-stonith-device"></a><span data-ttu-id="6a7dd-387">Créer l’appareil STONITH</span><span class="sxs-lookup"><span data-stu-id="6a7dd-387">Create STONITH device</span></span>

<span data-ttu-id="6a7dd-388">APPAREIL STONITH Hello utilise un tooauthorize de Principal du Service par rapport à Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="6a7dd-388">hello STONITH device uses a Service Principal tooauthorize against Microsoft Azure.</span></span> <span data-ttu-id="6a7dd-389">Suivez ces étapes de toocreate un Principal de Service.</span><span class="sxs-lookup"><span data-stu-id="6a7dd-389">Follow these steps toocreate a Service Principal.</span></span>

1. <span data-ttu-id="6a7dd-390">Accédez trop<https://portal.azure.com></span><span class="sxs-lookup"><span data-stu-id="6a7dd-390">Go too<https://portal.azure.com></span></span>
1. <span data-ttu-id="6a7dd-391">Panneau d’Azure Active Directory hello ouvert</span><span class="sxs-lookup"><span data-stu-id="6a7dd-391">Open hello Azure Active Directory blade</span></span>  
   <span data-ttu-id="6a7dd-392">Accédez tooProperties et écrivez hello ID de répertoire. Il s’agit de hello **id client**.</span><span class="sxs-lookup"><span data-stu-id="6a7dd-392">Go tooProperties and write down hello Directory Id. This is hello **tenant id**.</span></span>
1. <span data-ttu-id="6a7dd-393">Cliquez sur Inscriptions d’applications</span><span class="sxs-lookup"><span data-stu-id="6a7dd-393">Click App registrations</span></span>
1. <span data-ttu-id="6a7dd-394">Cliquez sur Ajouter.</span><span class="sxs-lookup"><span data-stu-id="6a7dd-394">Click Add</span></span>
1. <span data-ttu-id="6a7dd-395">Entrez un nom, sélectionnez le type d’application « Application web/API », entrez une URL de connexion (par exemple, http://localhost) et cliquez sur Créer</span><span class="sxs-lookup"><span data-stu-id="6a7dd-395">Enter a Name, select Application Type "Web app/API", enter a sign-on URL (for example http://localhost) and click Create</span></span>
1. <span data-ttu-id="6a7dd-396">URL de connexion Hello n’est pas utilisé et peut être une URL valide</span><span class="sxs-lookup"><span data-stu-id="6a7dd-396">hello sign-on URL is not used and can be any valid URL</span></span>
1. <span data-ttu-id="6a7dd-397">Sélectionnez hello nouvelle application et cliquez sur les clés dans l’onglet Paramètres de hello</span><span class="sxs-lookup"><span data-stu-id="6a7dd-397">Select hello new App and click Keys in hello Settings tab</span></span>
1. <span data-ttu-id="6a7dd-398">Entrez une description pour la nouvelle clé, sélectionnez « N’expire jamais » et cliquez sur Enregistrer</span><span class="sxs-lookup"><span data-stu-id="6a7dd-398">Enter a description for a new key, select "Never expires" and click Save</span></span>
1. <span data-ttu-id="6a7dd-399">Écrivez hello valeur.</span><span class="sxs-lookup"><span data-stu-id="6a7dd-399">Write down hello Value.</span></span> <span data-ttu-id="6a7dd-400">Il est utilisé comme hello **mot de passe** pour hello Principal du Service</span><span class="sxs-lookup"><span data-stu-id="6a7dd-400">It is used as hello **password** for hello Service Principal</span></span>
1. <span data-ttu-id="6a7dd-401">Écrivez hello ID d’Application. Il est utilisé comme nom d’utilisateur de hello (**id de connexion** dans suit hello) de hello Principal du Service</span><span class="sxs-lookup"><span data-stu-id="6a7dd-401">Write down hello Application Id. It is used as hello username (**login id** in hello steps below) of hello Service Principal</span></span>

<span data-ttu-id="6a7dd-402">Hello Principal du Service n’a pas les autorisations tooaccess vos ressources Azure par défaut.</span><span class="sxs-lookup"><span data-stu-id="6a7dd-402">hello Service Principal does not have permissions tooaccess your Azure resources by default.</span></span> <span data-ttu-id="6a7dd-403">Vous devez toostart d’autorisations toogive hello Principal du Service et arrêter (désallouer) tous les ordinateurs virtuels du cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="6a7dd-403">You need toogive hello Service Principal permissions toostart and stop (deallocate) all virtual machines of hello cluster.</span></span>

1. <span data-ttu-id="6a7dd-404">Accédez toohttps://portal.azure.com</span><span class="sxs-lookup"><span data-stu-id="6a7dd-404">Go toohttps://portal.azure.com</span></span>
1. <span data-ttu-id="6a7dd-405">Ouvrez hello toutes les lames de ressources</span><span class="sxs-lookup"><span data-stu-id="6a7dd-405">Open hello All resources blade</span></span>
1. <span data-ttu-id="6a7dd-406">Sélectionnez l’ordinateur virtuel de hello</span><span class="sxs-lookup"><span data-stu-id="6a7dd-406">Select hello virtual machine</span></span>
1. <span data-ttu-id="6a7dd-407">Cliquez sur Contrôle d’accès (IAM)</span><span class="sxs-lookup"><span data-stu-id="6a7dd-407">Click Access control (IAM)</span></span>
1. <span data-ttu-id="6a7dd-408">Cliquez sur Ajouter.</span><span class="sxs-lookup"><span data-stu-id="6a7dd-408">Click Add</span></span>
1. <span data-ttu-id="6a7dd-409">Sélectionnez le rôle hello propriétaire</span><span class="sxs-lookup"><span data-stu-id="6a7dd-409">Select hello role Owner</span></span>
1. <span data-ttu-id="6a7dd-410">Entrez les nom hello d’application hello créé ci-dessus</span><span class="sxs-lookup"><span data-stu-id="6a7dd-410">Enter hello name of hello application you created above</span></span>
1. <span data-ttu-id="6a7dd-411">Cliquez sur OK</span><span class="sxs-lookup"><span data-stu-id="6a7dd-411">Click OK</span></span>

#### <a name="1-create-hello-stonith-devices"></a><span data-ttu-id="6a7dd-412">**[1]**  Créer des unités de STONITH hello</span><span class="sxs-lookup"><span data-stu-id="6a7dd-412">**[1]** Create hello STONITH devices</span></span>

<span data-ttu-id="6a7dd-413">Une fois que vous avez modifié les autorisations hello pour les ordinateurs virtuels de hello, vous pouvez configurer les appareils STONITH hello dans un cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="6a7dd-413">After you edited hello permissions for hello virtual machines, you can configure hello STONITH devices in hello cluster.</span></span>

<pre><code>
sudo crm configure

# replace hello bold string with your subscription id, resource group, tenant id, service principal id and password

crm(live)configure# primitive rsc_st_azure_1 stonith:fence_azure_arm \
   params subscriptionId="<b>subscription id</b>" resourceGroup="<b>resource group</b>" tenantId="<b>tenant id</b>" login="<b>login id</b>" passwd="<b>password</b>"

crm(live)configure# primitive rsc_st_azure_2 stonith:fence_azure_arm \
   params subscriptionId="<b>subscription id</b>" resourceGroup="<b>resource group</b>" tenantId="<b>tenant id</b>" login="<b>login id</b>" passwd="<b>password</b>"

crm(live)configure# colocation col_st_azure -2000: rsc_st_azure_1:Started rsc_st_azure_2:Started

crm(live)configure# commit
crm(live)configure# exit
</code></pre>

#### <a name="1-enable-hello-use-of-a-stonith-device"></a><span data-ttu-id="6a7dd-414">**[1]**  Activer l’utilisation de hello d’un périphérique STONITH</span><span class="sxs-lookup"><span data-stu-id="6a7dd-414">**[1]** Enable hello use of a STONITH device</span></span>

<span data-ttu-id="6a7dd-415">Activer l’utilisation de hello d’un périphérique STONITH</span><span class="sxs-lookup"><span data-stu-id="6a7dd-415">Enable hello use of a STONITH device</span></span>

<pre><code>
sudo crm configure property stonith-enabled=true 
</code></pre>

## <a name="install-database"></a><span data-ttu-id="6a7dd-416">Installer la base de données</span><span class="sxs-lookup"><span data-stu-id="6a7dd-416">Install database</span></span>

<span data-ttu-id="6a7dd-417">Dans cet exemple, une réplication du système SAP HANA est installée et configurée.</span><span class="sxs-lookup"><span data-stu-id="6a7dd-417">In this example an SAP HANA System Replication is installed and configured.</span></span> <span data-ttu-id="6a7dd-418">SAP HANA s’exécute dans le même cluster comme hello SAP NetWeaver ASCS/SCS et ERS de hello.</span><span class="sxs-lookup"><span data-stu-id="6a7dd-418">SAP HANA will run in hello same cluster as hello SAP NetWeaver ASCS/SCS and ERS.</span></span> <span data-ttu-id="6a7dd-419">Vous pouvez également installer SAP HANA dans un cluster dédié.</span><span class="sxs-lookup"><span data-stu-id="6a7dd-419">You can also install SAP HANA on a dedicated cluster.</span></span> <span data-ttu-id="6a7dd-420">Consultez [Haute disponibilité de SAP HANA sur des machines virtuelles Azure][sap-hana-ha].</span><span class="sxs-lookup"><span data-stu-id="6a7dd-420">See [High Availability of SAP HANA on Azure Virtual Machines (VMs)][sap-hana-ha] for more information.</span></span>

### <a name="prepare-for-sap-hana-installation"></a><span data-ttu-id="6a7dd-421">Préparer l’installation de SAP HANA</span><span class="sxs-lookup"><span data-stu-id="6a7dd-421">Prepare for SAP HANA installation</span></span>

<span data-ttu-id="6a7dd-422">En général, nous recommandons d’utiliser LVM pour les volumes qui stockent des données et des fichiers journaux.</span><span class="sxs-lookup"><span data-stu-id="6a7dd-422">We generally recommend using LVM for volumes that store data and log files.</span></span> <span data-ttu-id="6a7dd-423">À des fins de test, vous pouvez également choisir toostore hello données et le fichier journal directement sur un disque brut.</span><span class="sxs-lookup"><span data-stu-id="6a7dd-423">For testing purposes, you can also choose toostore hello data and log file directly on a plain disk.</span></span>

1. <span data-ttu-id="6a7dd-424">**[A]** LVM</span><span class="sxs-lookup"><span data-stu-id="6a7dd-424">**[A]** LVM</span></span>  
   <span data-ttu-id="6a7dd-425">exemple Hello ci-dessous suppose que les ordinateurs virtuels hello avez quatre disques de données attachés doivent être utilisé toocreate deux volumes.</span><span class="sxs-lookup"><span data-stu-id="6a7dd-425">hello example below assumes that hello virtual machines have four data disks attached that should be used toocreate two volumes.</span></span>
   
   <span data-ttu-id="6a7dd-426">Créer des volumes physiques de tous les disques que vous souhaitez toouse.</span><span class="sxs-lookup"><span data-stu-id="6a7dd-426">Create physical volumes for all disks that you want toouse.</span></span>
   
   <pre><code>
   sudo pvcreate /dev/sdd
   sudo pvcreate /dev/sde
   sudo pvcreate /dev/sdf
   sudo pvcreate /dev/sdg
   </code></pre>
   
   <span data-ttu-id="6a7dd-427">Créer un groupe de volumes pour les fichiers de données hello, un groupe de volumes pour les fichiers de journaux hello et un pour le répertoire partagé de hello de SAP HANA</span><span class="sxs-lookup"><span data-stu-id="6a7dd-427">Create a volume group for hello data files, one volume group for hello log files and one for hello shared directory of SAP HANA</span></span>
   
   <pre><code>
   sudo vgcreate vg_hana_data /dev/sdd /dev/sde
   sudo vgcreate vg_hana_log /dev/sdf
   sudo vgcreate vg_hana_shared /dev/sdg
   </code></pre>
   
   <span data-ttu-id="6a7dd-428">Créer des volumes logiques hello</span><span class="sxs-lookup"><span data-stu-id="6a7dd-428">Create hello logical volumes</span></span>
   
   <pre><code>
   sudo lvcreate -l 100%FREE -n hana_data vg_hana_data
   sudo lvcreate -l 100%FREE -n hana_log vg_hana_log
   sudo lvcreate -l 100%FREE -n hana_shared vg_hana_shared
   sudo mkfs.xfs /dev/vg_hana_data/hana_data
   sudo mkfs.xfs /dev/vg_hana_log/hana_log
   sudo mkfs.xfs /dev/vg_hana_shared/hana_shared
   </code></pre>
   
   <span data-ttu-id="6a7dd-429">Créer des répertoires de montage hello et copiez hello UUID de tous les volumes logiques</span><span class="sxs-lookup"><span data-stu-id="6a7dd-429">Create hello mount directories and copy hello UUID of all logical volumes</span></span>
   
   <pre><code>
   sudo mkdir -p /hana/data
   sudo mkdir -p /hana/log
   sudo mkdir -p /hana/shared
   sudo chattr +i /hana/data
   sudo chattr +i /hana/log
   sudo chattr +i /hana/shared
   # write down hello id of /dev/vg_hana_data/hana_data, /dev/vg_hana_log/hana_log and /dev/vg_hana_shared/hana_shared
   sudo blkid
   </code></pre>
   
   <span data-ttu-id="6a7dd-430">Créer des volumes logiques trois entrées autofs pour hello</span><span class="sxs-lookup"><span data-stu-id="6a7dd-430">Create autofs entries for hello three logical volumes</span></span>
   
   <pre><code>
   sudo vi /etc/auto.direct
   </code></pre>
   
   <span data-ttu-id="6a7dd-431">Insérer cette ligne toosudo vi /etc/auto.direct</span><span class="sxs-lookup"><span data-stu-id="6a7dd-431">Insert this line toosudo vi /etc/auto.direct</span></span>
   
   <pre><code>
   /hana/data -fstype=xfs :UUID=<b>&lt;UUID of /dev/vg_hana_data/hana_data&gt;</b>
   /hana/log -fstype=xfs :UUID=<b>&lt;UUID of /dev/vg_hana_log/hana_log&gt;</b>
   /hana/shared -fstype=xfs :UUID=<b>&lt;UUID of /dev/vg_hana_shared/hana_shared&gt;</b>
   </code></pre>
   
   <span data-ttu-id="6a7dd-432">Monter des volumes de nouveau hello</span><span class="sxs-lookup"><span data-stu-id="6a7dd-432">Mount hello new volumes</span></span>
   
   <pre><code>
   sudo service autofs restart 
   </code></pre>

1. <span data-ttu-id="6a7dd-433">**[A]** Disques simples</span><span class="sxs-lookup"><span data-stu-id="6a7dd-433">**[A]** Plain Disks</span></span>  

   <span data-ttu-id="6a7dd-434">Pour les petits systèmes ou les systèmes de démonstration, vous pouvez placer vos données et fichiers journaux HANA sur un disque.</span><span class="sxs-lookup"><span data-stu-id="6a7dd-434">For small or demo systems, you can place your HANA data and log files on one disk.</span></span> <span data-ttu-id="6a7dd-435">Hello commandes suivantes créent une partition sur /dev/sdc puis formater xfs.</span><span class="sxs-lookup"><span data-stu-id="6a7dd-435">hello following commands create a partition on /dev/sdc and format it with xfs.</span></span>
   ```bash
   sudo sh -c 'echo -e "n\n\n\n\n\nw\n" | fdisk /dev/sdd'
   sudo mkfs.xfs /dev/sdd1
   
   # write down hello id of /dev/sdd1
   sudo /sbin/blkid
   sudo vi /etc/auto.direct
   ```
   
   <span data-ttu-id="6a7dd-436">Insérer cette ligne de too/etc/auto.direct</span><span class="sxs-lookup"><span data-stu-id="6a7dd-436">Insert this line too/etc/auto.direct</span></span>
   <pre><code>
   /hana -fstype=xfs :UUID=<b>&lt;UUID&gt;</b>
   </code></pre>
   
   <span data-ttu-id="6a7dd-437">Créer le répertoire cible de hello et monter le disque de hello.</span><span class="sxs-lookup"><span data-stu-id="6a7dd-437">Create hello target directory and mount hello disk.</span></span>
   
   <pre><code>
   sudo mkdir /hana
   sudo chattr +i /hana
   sudo service autofs restart
   </code></pre>

### <a name="installing-sap-hana"></a><span data-ttu-id="6a7dd-438">Installation de SAP HANA</span><span class="sxs-lookup"><span data-stu-id="6a7dd-438">Installing SAP HANA</span></span>

<span data-ttu-id="6a7dd-439">étapes suivantes Hello sont basées sur le chapitre 4 Hello [SAP HANA SR performances optimisées Scenario guide] [ suse-hana-ha-guide] tooinstall réplication du système SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="6a7dd-439">hello following steps are based on chapter 4 of hello [SAP HANA SR Performance Optimized Scenario guide][suse-hana-ha-guide] tooinstall SAP HANA System Replication.</span></span> <span data-ttu-id="6a7dd-440">Veuillez lire avant de poursuivre hello.</span><span class="sxs-lookup"><span data-stu-id="6a7dd-440">Please read it before you continue hello installation.</span></span>

1. <span data-ttu-id="6a7dd-441">**[A]**  Exécuter hdblcm à partir de hello HANA DVD</span><span class="sxs-lookup"><span data-stu-id="6a7dd-441">**[A]** Run hdblcm from hello HANA DVD</span></span>
   
   <pre><code>
   sudo hdblcm --sid=<b>HDB</b> --number=<b>03</b> --action=install --batch --password=<b>&lt;password&gt;</b> --system_user_password=<b>&lt;password for system user&gt;</b>

   sudo /hana/shared/<b>HDB</b>/hdblcm/hdblcm --action=configure_internal_network --listen_interface=internal --internal_network=<b>10.0.0/24</b> --password=<b>&lt;password for system user&gt;</b> --batch
   </code></pre>

1. <span data-ttu-id="6a7dd-442">**[A]** Mettre à niveau l’agent hôte SAP</span><span class="sxs-lookup"><span data-stu-id="6a7dd-442">**[A]** Upgrade SAP Host Agent</span></span>

   <span data-ttu-id="6a7dd-443">Télécharger des archives de l’Agent hôte SAP hello plus récente à partir de hello [SAP Softwarecenter] [ sap-swcenter] et exécution hello après la commande tooupgrade hello agent.</span><span class="sxs-lookup"><span data-stu-id="6a7dd-443">Download hello latest SAP Host Agent archive from hello [SAP Softwarecenter][sap-swcenter] and run hello following command tooupgrade hello agent.</span></span> <span data-ttu-id="6a7dd-444">Remplacez hello chemin d’accès toohello toopoint toohello fichier d’archive que vous avez téléchargé.</span><span class="sxs-lookup"><span data-stu-id="6a7dd-444">Replace hello path toohello archive toopoint toohello file you downloaded.</span></span>
   <pre><code>
   sudo /usr/sap/hostctrl/exe/saphostexec -upgrade -archive <b>&lt;path tooSAP Host Agent SAR&gt;</b> 
   </code></pre>

1. <span data-ttu-id="6a7dd-445">**[1]** Créer la réplication HANA (en tant que racine)</span><span class="sxs-lookup"><span data-stu-id="6a7dd-445">**[1]** Create HANA replication (as root)</span></span>  

   <span data-ttu-id="6a7dd-446">Exécutez hello commande suivante.</span><span class="sxs-lookup"><span data-stu-id="6a7dd-446">Run hello following command.</span></span> <span data-ttu-id="6a7dd-447">Assurez-vous que tooreplace chaînes en gras (HANA système ID HDB et numéro d’instance 03) avec des valeurs de votre installation de SAP HANA hello.</span><span class="sxs-lookup"><span data-stu-id="6a7dd-447">Make sure tooreplace bold strings (HANA System ID HDB and instance number 03) with hello values of your SAP HANA installation.</span></span>
   <pre><code>
   PATH="$PATH:/usr/sap/<b>HDB</b>/HDB<b>03</b>/exe"
   hdbsql -u system -i <b>03</b> 'CREATE USER <b>hdb</b>hasync PASSWORD "<b>passwd</b>"' 
   hdbsql -u system -i <b>03</b> 'GRANT DATA ADMIN too<b>hdb</b>hasync' 
   hdbsql -u system -i <b>03</b> 'ALTER USER <b>hdb</b>hasync DISABLE PASSWORD LIFETIME' 
   </code></pre>

1. <span data-ttu-id="6a7dd-448">**[A]** Créer l’entrée keystore (en tant que racine)</span><span class="sxs-lookup"><span data-stu-id="6a7dd-448">**[A]** Create keystore entry (as root)</span></span>

   <pre><code>
   PATH="$PATH:/usr/sap/<b>HDB</b>/HDB<b>03</b>/exe"
   hdbuserstore SET <b>hdb</b>haloc localhost:3<b>03</b>15 <b>hdb</b>hasync <b>&lt;passwd&gt;</b>
   </code></pre>

1. <span data-ttu-id="6a7dd-449">**[1]** Sauvegarder la base de données (en tant que racine)</span><span class="sxs-lookup"><span data-stu-id="6a7dd-449">**[1]** Backup database (as root)</span></span>

   <pre><code>
   PATH="$PATH:/usr/sap/<b>HDB</b>/HDB<b>03</b>/exe"
   hdbsql -u system -i <b>03</b> "BACKUP DATA USING FILE ('<b>initialbackup</b>')" 
   </code></pre>

1. <span data-ttu-id="6a7dd-450">**[1]**  Permuter toohello HANA sapsid utilisateur et créer un site principal de hello.</span><span class="sxs-lookup"><span data-stu-id="6a7dd-450">**[1]** Switch toohello HANA sapsid user and create hello primary site.</span></span>

   <pre><code>
   su - <b>hdb</b>adm
   hdbnsutil -sr_enable –-name=<b>SITE1</b>
   </code></pre>

1. <span data-ttu-id="6a7dd-451">**[2]**  Permuter toohello HANA sapsid utilisateur et créer un site secondaire de hello.</span><span class="sxs-lookup"><span data-stu-id="6a7dd-451">**[2]** Switch toohello HANA sapsid user and create hello secondary site.</span></span>

   <pre><code>
   su - <b>hdb</b>adm
   sapcontrol -nr <b>03</b> -function StopWait 600 10
   hdbnsutil -sr_register --remoteHost=<b>nws-cl-0</b> --remoteInstance=<b>03</b> --replicationMode=sync --name=<b>SITE2</b> 
   </code></pre>

1. <span data-ttu-id="6a7dd-452">**[1]** Créer les ressources de cluster SAP HANA</span><span class="sxs-lookup"><span data-stu-id="6a7dd-452">**[1]** Create SAP HANA cluster resources</span></span>

   <span data-ttu-id="6a7dd-453">Commencez par créer la topologie de hello.</span><span class="sxs-lookup"><span data-stu-id="6a7dd-453">First, create hello topology.</span></span>
   
   <pre><code>
   sudo crm configure

   # replace hello bold string with your instance number and HANA system id
   
   crm(live)configure# primitive rsc_SAPHanaTopology_<b>HDB</b>_HDB<b>03</b>   ocf:suse:SAPHanaTopology \
     operations $id="rsc_sap2_<b>HDB</b>_HDB<b>03</b>-operations" \
     op monitor interval="10" timeout="600" \
     op start interval="0" timeout="600" \
     op stop interval="0" timeout="300" \
     params SID="<b>HDB</b>" InstanceNumber="<b>03</b>"
    
   crm(live)configure# clone cln_SAPHanaTopology_<b>HDB</b>_HDB<b>03</b> rsc_SAPHanaTopology_<b>HDB</b>_HDB<b>03</b> \
     meta is-managed="true" clone-node-max="1" target-role="Started" interleave="true"

   crm(live)configure# commit
   crm(live)configure# exit
   </code></pre>
   
   <span data-ttu-id="6a7dd-454">Créez ensuite les ressources HANA hello</span><span class="sxs-lookup"><span data-stu-id="6a7dd-454">Next, create hello HANA resources</span></span>
   
   <pre><code>
   sudo crm configure

   # replace hello bold string with your instance number, HANA system id and hello frontend IP address of hello Azure load balancer. 
    
   crm(live)configure# primitive rsc_SAPHana_<b>HDB</b>_HDB<b>03</b> ocf:suse:SAPHana \
     operations $id="rsc_sap_<b>HDB</b>_HDB<b>03</b>-operations" \
     op start interval="0" timeout="3600" \
     op stop interval="0" timeout="3600" \
     op promote interval="0" timeout="3600" \
     op monitor interval="60" role="Master" timeout="700" \
     op monitor interval="61" role="Slave" timeout="700" \
     params SID="<b>HDB</b>" InstanceNumber="<b>03</b>" PREFER_SITE_TAKEOVER="true" \
     DUPLICATE_PRIMARY_TIMEOUT="7200" AUTOMATED_REGISTER="false"
    
   crm(live)configure# ms msl_SAPHana_<b>HDB</b>_HDB<b>03</b> rsc_SAPHana_<b>HDB</b>_HDB<b>03</b> \
     meta is-managed="true" notify="true" clone-max="2" clone-node-max="1" \
     target-role="Started" interleave="true"
    
   crm(live)configure# primitive rsc_ip_<b>HDB</b>_HDB<b>03</b> ocf:heartbeat:IPaddr2 \ 
     meta target-role="Started" is-managed="true" \ 
     operations $id="rsc_ip_<b>HDB</b>_HDB<b>03</b>-operations" \ 
     op monitor interval="10s" timeout="20s" \ 
     params ip="<b>10.0.0.12</b>" 

   crm(live)configure# primitive rsc_nc_<b>HDB</b>_HDB<b>03</b> anything \ 
     params binfile="/usr/bin/nc" cmdline_options="-l -k 625<b>03</b>" \ 
     op monitor timeout=20s interval=10 depth=0 

   crm(live)configure# group g_ip_<b>HDB</b>_HDB<b>03</b> rsc_ip_<b>HDB</b>_HDB<b>03</b> rsc_nc_<b>HDB</b>_HDB<b>03</b>
    
   crm(live)configure# colocation col_saphana_ip_<b>HDB</b>_HDB<b>03</b> 2000: g_ip_<b>HDB</b>_HDB<b>03</b>:Started \ 
     msl_SAPHana_<b>HDB</b>_HDB<b>03</b>:Master  

   crm(live)configure# order ord_SAPHana_<b>HDB</b>_HDB<b>03</b> 2000: cln_SAPHanaTopology_<b>HDB</b>_HDB<b>03</b> \ 
     msl_SAPHana_<b>HDB</b>_HDB<b>03</b>
    
   crm(live)configure# commit
   crm(live)configure# exit
   </code></pre>

   <span data-ttu-id="6a7dd-455">Assurez-vous que l’état du cluster hello est OK et que toutes les ressources sont démarrés.</span><span class="sxs-lookup"><span data-stu-id="6a7dd-455">Make sure that hello cluster status is ok and that all resources are started.</span></span> <span data-ttu-id="6a7dd-456">Il n’est pas important sur les ressources de hello de nœud sont en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="6a7dd-456">It is not important on which node hello resources are running.</span></span>

   <pre><code>
   sudo crm_mon -r

   # <b>Online: [ nws-cl-0 nws-cl-1 ]</b>
   # 
   # Full list of resources:
   # 
   #  Master/Slave Set: ms-drbd_NWS_ASCS [drbd_NWS_ASCS]
   #      <b>Masters: [ nws-cl-1 ]</b>
   #      <b>Slaves: [ nws-cl-0 ]</b>
   #  Resource Group: g-NWS_ASCS
   #      nc_NWS_ASCS        (ocf::heartbeat:anything):      <b>Started nws-cl-1</b>
   #      vip_NWS_ASCS       (ocf::heartbeat:IPaddr2):       <b>Started nws-cl-1</b>
   #      fs_NWS_ASCS        (ocf::heartbeat:Filesystem):    <b>Started nws-cl-1</b>
   #      rsc_sap_NWS_ASCS00 (ocf::heartbeat:SAPInstance):   <b>Started nws-cl-1</b>
   #  Master/Slave Set: ms-drbd_NWS_ERS [drbd_NWS_ERS]
   #      <b>Masters: [ nws-cl-0 ]</b>
   #      <b>Slaves: [ nws-cl-1 ]</b>
   #  Resource Group: g-NWS_ERS
   #      nc_NWS_ERS (ocf::heartbeat:anything):      <b>Started nws-cl-0</b>
   #      vip_NWS_ERS        (ocf::heartbeat:IPaddr2):       <b>Started nws-cl-0</b>
   #      fs_NWS_ERS (ocf::heartbeat:Filesystem):    <b>Started nws-cl-0</b>
   #      rsc_sap_NWS_ERS02  (ocf::heartbeat:SAPInstance):   <b>Started nws-cl-0</b>
   #  Clone Set: cln_SAPHanaTopology_HDB_HDB03 [rsc_SAPHanaTopology_HDB_HDB03]
   #      <b>Started: [ nws-cl-0 nws-cl-1 ]</b>
   #  Master/Slave Set: msl_SAPHana_HDB_HDB03 [rsc_SAPHana_HDB_HDB03]
   #      <b>Masters: [ nws-cl-0 ]</b>
   #      <b>Slaves: [ nws-cl-1 ]</b>
   #  Resource Group: g_ip_HDB_HDB03
   #      rsc_ip_HDB_HDB03   (ocf::heartbeat:IPaddr2):       <b>Started nws-cl-0</b>
   #      rsc_nc_HDB_HDB03   (ocf::heartbeat:anything):      <b>Started nws-cl-0</b>
   # rsc_st_azure_1  (stonith:fence_azure_arm):      <b>Started nws-cl-0</b>
   # rsc_st_azure_2  (stonith:fence_azure_arm):      <b>Started nws-cl-1</b>
   </code></pre>

1. <span data-ttu-id="6a7dd-457">**[1]**  Instance de base de données SAP NetWeaver installation Bonjour</span><span class="sxs-lookup"><span data-stu-id="6a7dd-457">**[1]** Install hello SAP NetWeaver database instance</span></span>

   <span data-ttu-id="6a7dd-458">Instance de base de données SAP NetWeaver installation hello en tant que racine à l’aide d’un nom d’hôte virtuel qui mappe les adresses IP de toohello de configuration de serveur frontal d’équilibrage de charge de hello pour la base de données hello par exemple <b>nws-db</b> et <b>10.0.0.12</b>.</span><span class="sxs-lookup"><span data-stu-id="6a7dd-458">Install hello SAP NetWeaver database instance as root using a virtual hostname that maps toohello IP address of hello load balancer frontend configuration for hello database for example <b>nws-db</b> and <b>10.0.0.12</b>.</span></span>

   <span data-ttu-id="6a7dd-459">Vous pouvez utiliser hello sapinst paramètre SAPINST_REMOTE_ACCESS_USER tooallow un toosapinst de tooconnect utilisateur non racine.</span><span class="sxs-lookup"><span data-stu-id="6a7dd-459">You can use hello sapinst parameter SAPINST_REMOTE_ACCESS_USER tooallow a non-root user tooconnect toosapinst.</span></span>

   <pre><code>
   sudo &lt;swpm&gt;/sapinst SAPINST_REMOTE_ACCESS_USER=<b>sapadmin</b>
   </code></pre>

## <a name="sap-netweaver-application-server-installation"></a><span data-ttu-id="6a7dd-460">Installation de serveur d’applications SAP NetWeaver</span><span class="sxs-lookup"><span data-stu-id="6a7dd-460">SAP NetWeaver application server installation</span></span>

<span data-ttu-id="6a7dd-461">Suivez ces étapes de tooinstall un serveur d’applications SAP.</span><span class="sxs-lookup"><span data-stu-id="6a7dd-461">Follow these steps tooinstall an SAP application server.</span></span> <span data-ttu-id="6a7dd-462">Hello étapes ci-dessous supposent que vous installez un serveur d’applications hello sur un serveur différent de hello ASCS/SCS et les serveurs HANA.</span><span class="sxs-lookup"><span data-stu-id="6a7dd-462">hello steps bellow assume that you install hello application server on a server different from hello ASCS/SCS and HANA servers.</span></span> <span data-ttu-id="6a7dd-463">Sinon, certaines des étapes hello ci-dessous (par exemple, la configuration de la résolution de nom d’hôte) ne sont pas nécessaires.</span><span class="sxs-lookup"><span data-stu-id="6a7dd-463">Otherwise some of hello steps below (like configuring host name resolution) are not needed.</span></span>

1. <span data-ttu-id="6a7dd-464">Configurer la résolution de nom d’hôte</span><span class="sxs-lookup"><span data-stu-id="6a7dd-464">Setup host name resolution</span></span>    
   <span data-ttu-id="6a7dd-465">Vous pouvez utiliser un serveur DNS ou modifier/etc/hosts de hello sur tous les nœuds.</span><span class="sxs-lookup"><span data-stu-id="6a7dd-465">You can either use a DNS server or modify hello /etc/hosts on all nodes.</span></span> <span data-ttu-id="6a7dd-466">Cet exemple montre comment toouse hello les fichier/etc/hosts.</span><span class="sxs-lookup"><span data-stu-id="6a7dd-466">This example shows how toouse hello /etc/hosts file.</span></span>
   <span data-ttu-id="6a7dd-467">Remplacez l’adresse IP de hello et un nom d’hôte hello Bonjour suivant les commandes</span><span class="sxs-lookup"><span data-stu-id="6a7dd-467">Replace hello IP address and hello hostname in hello following commands</span></span>
   ```bash
   sudo vi /etc/hosts
   ```
   <span data-ttu-id="6a7dd-468">Insérez hello suivant lignes trop/etc/hosts.</span><span class="sxs-lookup"><span data-stu-id="6a7dd-468">Insert hello following lines too/etc/hosts.</span></span> <span data-ttu-id="6a7dd-469">Modifiez les toomatch hello IP adresse et le nom d’hôte de votre environnement</span><span class="sxs-lookup"><span data-stu-id="6a7dd-469">Change hello IP address and hostname toomatch your environment</span></span>    
    
   <pre><code>
   # IP address of hello load balancer frontend configuration for NFS
   <b>10.0.0.4 nws-nfs</b>
   # IP address of hello load balancer frontend configuration for SAP NetWeaver ASCS/SCS
   <b>10.0.0.10 nws-ascs</b>
   # IP address of hello load balancer frontend configuration for SAP NetWeaver ERS
   <b>10.0.0.11 nws-ers</b>
   # IP address of hello load balancer frontend configuration for database
   <b>10.0.0.12 nws-db</b>
   # IP address of hello application server
   <b>10.0.0.8 nws-di-0</b>
   </code></pre>

1. <span data-ttu-id="6a7dd-470">Créer le répertoire de sapmnt hello</span><span class="sxs-lookup"><span data-stu-id="6a7dd-470">Create hello sapmnt directory</span></span>

   <pre><code>
   sudo mkdir -p /sapmnt/<b>NWS</b>
   sudo mkdir -p /usr/sap/trans

   sudo chattr +i /sapmnt/<b>NWS</b>
   sudo chattr +i /usr/sap/trans
   </code></pre>

1. <span data-ttu-id="6a7dd-471">Configurer autofs</span><span class="sxs-lookup"><span data-stu-id="6a7dd-471">Configure autofs</span></span>
 
   <pre><code>
   sudo vi /etc/auto.master

   # Add hello following line toohello file, save and exit
   +auto.master
   /- /etc/auto.direct
   </code></pre>

   <span data-ttu-id="6a7dd-472">Créer un fichier avec</span><span class="sxs-lookup"><span data-stu-id="6a7dd-472">Create a new file with</span></span>

   <pre><code>
   sudo vi /etc/auto.direct

   # Add hello following lines toohello file, save and exit
   /sapmnt/<b>NWS</b> -nfsvers=4,nosymlink,sync <b>nws-nfs</b>:/sapmntsid
   /usr/sap/trans -nfsvers=4,nosymlink,sync <b>nws-nfs</b>:/trans
   </code></pre>

   <span data-ttu-id="6a7dd-473">Redémarrez les nouveaux partages autofs toomount hello</span><span class="sxs-lookup"><span data-stu-id="6a7dd-473">Restart autofs toomount hello new shares</span></span>

   <pre><code>
   sudo systemctl enable autofs
   sudo service autofs restart
   </code></pre>

1. <span data-ttu-id="6a7dd-474">Configurer le fichier SWAP</span><span class="sxs-lookup"><span data-stu-id="6a7dd-474">Configure SWAP file</span></span>
 
   <pre><code>
   sudo vi /etc/waagent.conf

   # Set hello property ResourceDisk.EnableSwap tooy
   # Create and use swapfile on resource disk.
   ResourceDisk.EnableSwap=<b>y</b>

   # Set hello size of hello SWAP file with property ResourceDisk.SwapSizeMB
   # hello free space of resource disk varies by virtual machine size. Make sure that you do not set a value that is too big. You can check hello SWAP space with command swapon
   # Size of hello swapfile.
   ResourceDisk.SwapSizeMB=<b>2000</b>
   </code></pre>

   <span data-ttu-id="6a7dd-475">Redémarrez le changement d’hello hello Agent tooactivate</span><span class="sxs-lookup"><span data-stu-id="6a7dd-475">Restart hello Agent tooactivate hello change</span></span>

   <pre><code>
   sudo service waagent restart
   </code></pre>

1. <span data-ttu-id="6a7dd-476">Installer le serveur d’applications SAP NetWeaver</span><span class="sxs-lookup"><span data-stu-id="6a7dd-476">Install SAP NetWeaver application server</span></span>

   <span data-ttu-id="6a7dd-477">Installer un serveur d’applications SAP NetWeaver principal ou supplémentaire.</span><span class="sxs-lookup"><span data-stu-id="6a7dd-477">Install a primary or additional SAP NetWeaver applications server.</span></span>

   <span data-ttu-id="6a7dd-478">Vous pouvez utiliser hello sapinst paramètre SAPINST_REMOTE_ACCESS_USER tooallow un toosapinst de tooconnect utilisateur non racine.</span><span class="sxs-lookup"><span data-stu-id="6a7dd-478">You can use hello sapinst parameter SAPINST_REMOTE_ACCESS_USER tooallow a non-root user tooconnect toosapinst.</span></span>

   <pre><code>
   sudo &lt;swpm&gt;/sapinst SAPINST_REMOTE_ACCESS_USER=<b>sapadmin</b>
   </code></pre>

1. <span data-ttu-id="6a7dd-479">Mettre à jour la banque d’informations sécurisée SAP HANA</span><span class="sxs-lookup"><span data-stu-id="6a7dd-479">Update SAP HANA secure store</span></span>

   <span data-ttu-id="6a7dd-480">Hello de mise à jour sécurisée à SAP HANA stocker le nom virtuel de toopoint toohello du programme d’installation de la réplication du système SAP HANA hello.</span><span class="sxs-lookup"><span data-stu-id="6a7dd-480">Update hello SAP HANA secure store toopoint toohello virtual name of hello SAP HANA System Replication setup.</span></span>
   <pre><code>
   su - <b>nws</b>adm
   hdbuserstore SET DEFAULT <b>nws-db</b>:3<b>03</b>15 <b>SAPABAP1</b> <b>&lt;password of ABAP schema&gt;</b>
   </code></pre>

## <a name="next-steps"></a><span data-ttu-id="6a7dd-481">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="6a7dd-481">Next steps</span></span>
* <span data-ttu-id="6a7dd-482">[Planification et implémentation de machines virtuelles Azure pour SAP][planning-guide]</span><span class="sxs-lookup"><span data-stu-id="6a7dd-482">[Azure Virtual Machines planning and implementation for SAP][planning-guide]</span></span>
* <span data-ttu-id="6a7dd-483">[Déploiement de machines virtuelles Azure pour SAP][deployment-guide]</span><span class="sxs-lookup"><span data-stu-id="6a7dd-483">[Azure Virtual Machines deployment for SAP][deployment-guide]</span></span>
* <span data-ttu-id="6a7dd-484">[Déploiement SGBD de machines virtuelles Azure pour SAP][dbms-guide]</span><span class="sxs-lookup"><span data-stu-id="6a7dd-484">[Azure Virtual Machines DBMS deployment for SAP][dbms-guide]</span></span>
* <span data-ttu-id="6a7dd-485">toolearn comment tooestablish haute disponibilité et le plan de récupération d’urgence de SAP HANA sur Azure (instances de grande taille), consultez [SAP HANA (instances de grande taille) haute disponibilité et récupération d’urgence sur Azure](hana-overview-high-availability-disaster-recovery.md).</span><span class="sxs-lookup"><span data-stu-id="6a7dd-485">toolearn how tooestablish high availability and plan for disaster recovery of SAP HANA on Azure (large instances), see [SAP HANA (large instances) high availability and disaster recovery on Azure](hana-overview-high-availability-disaster-recovery.md).</span></span>
* <span data-ttu-id="6a7dd-486">toolearn comment tooestablish haute disponibilité et le plan de récupération d’urgence de SAP HANA sur des machines virtuelles Azure, consultez [disponibilité élevée de SAP HANA sur Azure des Machines virtuelles (VM)][sap-hana-ha]</span><span class="sxs-lookup"><span data-stu-id="6a7dd-486">toolearn how tooestablish high availability and plan for disaster recovery of SAP HANA on Azure VMs, see [High Availability of SAP HANA on Azure Virtual Machines (VMs)][sap-hana-ha]</span></span>
