---
title: "Haute disponibilité des machines virtuelles Azure pour SAP NetWeaver sur SUSE Linux Enterprise Server pour les applications SAP | Microsoft Docs"
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
ms.openlocfilehash: 16e09797926f29bc18cb05671c986c74f9c2d4f8
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="high-availability-for-sap-netweaver-on-azure-vms-on-suse-linux-enterprise-server-for-sap-applications"></a><span data-ttu-id="9953e-103">Haute disponibilité pour SAP NetWeaver sur les machines virtuelles Azure sur SUSE Linux Enterprise Server pour les applications SAP</span><span class="sxs-lookup"><span data-stu-id="9953e-103">High availability for SAP NetWeaver on Azure VMs on SUSE Linux Enterprise Server for SAP applications</span></span>

[dbms-guide]:dbms-guide.md
[deployment-guide]:deployment-guide.md
[planning-guide]:planning-guide.md

<span data-ttu-id="9953e-104">[2205917]:https://launchpad.support.sap.com/#/notes/2205917</span><span class="sxs-lookup"><span data-stu-id="9953e-104">[2205917]:https://launchpad.support.sap.com/#/notes/2205917</span></span>
<span data-ttu-id="9953e-105">[1944799]:https://launchpad.support.sap.com/#/notes/1944799</span><span class="sxs-lookup"><span data-stu-id="9953e-105">[1944799]:https://launchpad.support.sap.com/#/notes/1944799</span></span>
<span data-ttu-id="9953e-106">[1928533]:https://launchpad.support.sap.com/#/notes/1928533</span><span class="sxs-lookup"><span data-stu-id="9953e-106">[1928533]:https://launchpad.support.sap.com/#/notes/1928533</span></span>
<span data-ttu-id="9953e-107">[2015553]:https://launchpad.support.sap.com/#/notes/2015553</span><span class="sxs-lookup"><span data-stu-id="9953e-107">[2015553]:https://launchpad.support.sap.com/#/notes/2015553</span></span>
<span data-ttu-id="9953e-108">[2178632]:https://launchpad.support.sap.com/#/notes/2178632</span><span class="sxs-lookup"><span data-stu-id="9953e-108">[2178632]:https://launchpad.support.sap.com/#/notes/2178632</span></span>
<span data-ttu-id="9953e-109">[2191498]:https://launchpad.support.sap.com/#/notes/2191498</span><span class="sxs-lookup"><span data-stu-id="9953e-109">[2191498]:https://launchpad.support.sap.com/#/notes/2191498</span></span>
<span data-ttu-id="9953e-110">[2243692]:https://launchpad.support.sap.com/#/notes/2243692</span><span class="sxs-lookup"><span data-stu-id="9953e-110">[2243692]:https://launchpad.support.sap.com/#/notes/2243692</span></span>
<span data-ttu-id="9953e-111">[1984787]:https://launchpad.support.sap.com/#/notes/1984787</span><span class="sxs-lookup"><span data-stu-id="9953e-111">[1984787]:https://launchpad.support.sap.com/#/notes/1984787</span></span>
<span data-ttu-id="9953e-112">[1999351]:https://launchpad.support.sap.com/#/notes/1999351</span><span class="sxs-lookup"><span data-stu-id="9953e-112">[1999351]:https://launchpad.support.sap.com/#/notes/1999351</span></span>
[1410736]:https://launchpad.support.sap.com/#/notes/1410736

[sap-swcenter]:https://support.sap.com/en/my-support/software-downloads.html

[suse-hana-ha-guide]:https://www.suse.com/docrep/documents/ir8w88iwu7/suse_linux_enterprise_server_for_sap_applications_12_sp1.pdf
[suse-drbd-guide]:https://www.suse.com/documentation/sle-ha-12/singlehtml/book_sleha_techguides/book_sleha_techguides.html

[template-multisid-xscs]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image-multi-sid-xscs-md%2Fazuredeploy.json
[template-converged]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image-converged-md%2Fazuredeploy.json
[template-file-server]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-file-server-md%2Fazuredeploy.json

[sap-hana-ha]:sap-hana-high-availability.md

<span data-ttu-id="9953e-113">Cet article décrit comment déployer et configurer les machines virtuelles, installer l’infrastructure de cluster et installer et un système SAP NetWeaver 7.50 à haute disponibilité.</span><span class="sxs-lookup"><span data-stu-id="9953e-113">This article describes how to deploy the virtual machines, configure the virtual machines, install the cluster framework and install a highly available SAP NetWeaver 7.50 system.</span></span>
<span data-ttu-id="9953e-114">Dans les exemples de configuration, commandes d’installation, et ainsi de suite, nous utilisons le numéro d’instance ASCS 00, le numéro d’instance ERS 02 et l’ID de système SAP NWS.</span><span class="sxs-lookup"><span data-stu-id="9953e-114">In the example configurations, installation commands etc. ASCS instance number 00, ERS instance number 02 and SAP System ID NWS is used.</span></span> <span data-ttu-id="9953e-115">Les noms des ressources (telles que les machines virtuelles et les réseaux virtuels) dans l’exemple partent du principe que vous avez utilisé le [modèle convergé][template-converged] avec l’ID de système SAP NWS pour créer les ressources.</span><span class="sxs-lookup"><span data-stu-id="9953e-115">The names of the resources (for example virtual machines, virtual networks) in the example assume that you have used the [converged template][template-converged] with SAP system ID NWS to create the resources.</span></span>

<span data-ttu-id="9953e-116">Commencez par lire les notes et publications SAP suivantes</span><span class="sxs-lookup"><span data-stu-id="9953e-116">Read the following SAP Notes and papers first</span></span>

* <span data-ttu-id="9953e-117">Note SAP [1928533], qui contient :</span><span class="sxs-lookup"><span data-stu-id="9953e-117">SAP Note [1928533], which has:</span></span>
  * <span data-ttu-id="9953e-118">une liste des tailles de machines virtuelles Azure prises en charge pour le déploiement de logiciels SAP</span><span class="sxs-lookup"><span data-stu-id="9953e-118">List of Azure VM sizes that are supported for the deployment of SAP software</span></span>
  * <span data-ttu-id="9953e-119">des informations importantes sur la capacité en fonction de la taille des machines virtuelles Azure</span><span class="sxs-lookup"><span data-stu-id="9953e-119">Important capacity information for Azure VM sizes</span></span>
  * <span data-ttu-id="9953e-120">les logiciels SAP pris en charge et les combinaisons entre système d’exploitation et base de données</span><span class="sxs-lookup"><span data-stu-id="9953e-120">Supported SAP software, and operating system (OS) and database combinations</span></span>
  * <span data-ttu-id="9953e-121">la version du noyau SAP requise pour Windows et Linux sur Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="9953e-121">Required SAP kernel version for Windows and Linux on Microsoft Azure</span></span>

* <span data-ttu-id="9953e-122">La note SAP [2015553] répertorie les conditions préalables au déploiement de logiciels SAP pris en charge par SAP sur Azure.</span><span class="sxs-lookup"><span data-stu-id="9953e-122">SAP Note [2015553] lists prerequisites for SAP-supported SAP software deployments in Azure.</span></span>
* <span data-ttu-id="9953e-123">La note SAP [2205917] contient des paramètres de système d’exploitation recommandés pour SUSE Linux Enterprise Server pour les applications SAP</span><span class="sxs-lookup"><span data-stu-id="9953e-123">SAP Note [2205917] has recommended OS settings for SUSE Linux Enterprise Server for SAP Applications</span></span>
* <span data-ttu-id="9953e-124">La note SAP [1944799] contient des instructions SAP HANA pour SUSE Linux Enterprise Server pour les applications SAP</span><span class="sxs-lookup"><span data-stu-id="9953e-124">SAP Note [1944799] has SAP HANA Guidelines for SUSE Linux Enterprise Server for SAP Applications</span></span>
* <span data-ttu-id="9953e-125">La note SAP [2178632] contient des informations détaillées sur toutes les métriques de surveillance rapportées pour SAP sur Azure.</span><span class="sxs-lookup"><span data-stu-id="9953e-125">SAP Note [2178632] has detailed information about all monitoring metrics reported for SAP in Azure.</span></span>
* <span data-ttu-id="9953e-126">La note SAP [2191498] contient la version requise de l’agent hôte SAP pour Linux sur Azure.</span><span class="sxs-lookup"><span data-stu-id="9953e-126">SAP Note [2191498] has the required SAP Host Agent version for Linux in Azure.</span></span>
* <span data-ttu-id="9953e-127">La note SAP [2243692] contient des informations sur les licences SAP sur Linux dans Azure.</span><span class="sxs-lookup"><span data-stu-id="9953e-127">SAP Note [2243692] has information about SAP licensing on Linux in Azure.</span></span>
* <span data-ttu-id="9953e-128">La note SAP [1984787] contient des informations sur SUSE Linux Enterprise Server 12.</span><span class="sxs-lookup"><span data-stu-id="9953e-128">SAP Note [1984787] has general information about SUSE Linux Enterprise Server 12.</span></span>
* <span data-ttu-id="9953e-129">La note SAP [1999351] contient des informations de dépannage supplémentaires pour l’extension d’analyse Azure améliorée pour SAP.</span><span class="sxs-lookup"><span data-stu-id="9953e-129">SAP Note [1999351] has additional troubleshooting information for the Azure Enhanced Monitoring Extension for SAP.</span></span>
* <span data-ttu-id="9953e-130">Le [WIKI de la communauté SAP](https://wiki.scn.sap.com/wiki/display/HOME/SAPonLinuxNotes) contient toutes les notes SAP requises pour Linux.</span><span class="sxs-lookup"><span data-stu-id="9953e-130">[SAP Community WIKI](https://wiki.scn.sap.com/wiki/display/HOME/SAPonLinuxNotes) has all required SAP Notes for Linux.</span></span>
* <span data-ttu-id="9953e-131">[Planification et implémentation de Machines virtuelles Azure pour SAP sur Linux][planning-guide]</span><span class="sxs-lookup"><span data-stu-id="9953e-131">[Azure Virtual Machines planning and implementation for SAP on Linux][planning-guide]</span></span>
* <span data-ttu-id="9953e-132">[Déploiement de Machines virtuelles Azure pour SAP sur Linux (cet article)][deployment-guide]</span><span class="sxs-lookup"><span data-stu-id="9953e-132">[Azure Virtual Machines deployment for SAP on Linux (this article)][deployment-guide]</span></span>
* <span data-ttu-id="9953e-133">[Déploiement SGBD de Machines virtuelles Azure pour SAP sur Linux][dbms-guide]</span><span class="sxs-lookup"><span data-stu-id="9953e-133">[Azure Virtual Machines DBMS deployment for SAP on Linux][dbms-guide]</span></span>
* <span data-ttu-id="9953e-134">[SAP HANA SR Performance Optimized Scenario][suse-hana-ha-guide] (Scénario d’optimisation des performances de réplication système de SAP HANA)</span><span class="sxs-lookup"><span data-stu-id="9953e-134">[SAP HANA SR Performance Optimized Scenario][suse-hana-ha-guide]</span></span>  
  <span data-ttu-id="9953e-135">Le guide contient toutes les informations requises pour configurer la réplication système SAP HANA en local.</span><span class="sxs-lookup"><span data-stu-id="9953e-135">The guide contains all required information to set up SAP HANA System Replication on-premises.</span></span> <span data-ttu-id="9953e-136">Utilisez ce guide comme référence.</span><span class="sxs-lookup"><span data-stu-id="9953e-136">Use this guide as a baseline.</span></span>
* <span data-ttu-id="9953e-137">[Stockage NFS hautement disponible avec DRBD et Pacemaker][suse-drbd-guide] Ce guide contient toutes les informations nécessaires pour configurer un serveur NFS à haute disponibilité.</span><span class="sxs-lookup"><span data-stu-id="9953e-137">[Highly Available NFS Storage with DRBD and Pacemaker][suse-drbd-guide] The guide contains all required information to set up a highly available NFS server.</span></span> <span data-ttu-id="9953e-138">Utilisez ce guide comme référence.</span><span class="sxs-lookup"><span data-stu-id="9953e-138">Use this guide as a baseline.</span></span>


## <a name="overview"></a><span data-ttu-id="9953e-139">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="9953e-139">Overview</span></span>

<span data-ttu-id="9953e-140">Pour obtenir une haute disponibilité, SAP NetWeaver nécessite un serveur NFS.</span><span class="sxs-lookup"><span data-stu-id="9953e-140">To achieve high availability, SAP NetWeaver requires an NFS server.</span></span> <span data-ttu-id="9953e-141">Le serveur NFS est configuré dans un cluster distinct et peut être utilisé par plusieurs systèmes SAP.</span><span class="sxs-lookup"><span data-stu-id="9953e-141">The NFS server is configured in a separate cluster and can be used by multiple SAP systems.</span></span>

![Vue d’ensemble de la haute disponibilité SAP NetWeaver](./media/high-availability-guide-suse/img_001.png)

<span data-ttu-id="9953e-143">Le serveur NFS, SAP NetWeaver ASCS, SAP NetWeaver SCS, SAP NetWeaver ERS et la base de données SAP HANA utilisent un nom d’hôte virtuel et des adresses IP virtuelles.</span><span class="sxs-lookup"><span data-stu-id="9953e-143">The NFS server, SAP NetWeaver ASCS, SAP NetWeaver SCS, SAP NetWeaver ERS and the SAP HANA database use virtual hostname and virtual IP addresses.</span></span> <span data-ttu-id="9953e-144">Sur Azure, un équilibreur de charge est nécessaire pour utiliser une adresse IP virtuelle.</span><span class="sxs-lookup"><span data-stu-id="9953e-144">On Azure, a load balancer is required to use a virtual IP address.</span></span> <span data-ttu-id="9953e-145">La liste suivante illustre la configuration de l’équilibreur de charge.</span><span class="sxs-lookup"><span data-stu-id="9953e-145">The following list shows the configuration of the load balancer.</span></span>

### <a name="nfs-server"></a><span data-ttu-id="9953e-146">Serveur NFS</span><span class="sxs-lookup"><span data-stu-id="9953e-146">NFS Server</span></span>
* <span data-ttu-id="9953e-147">Configuration du frontend</span><span class="sxs-lookup"><span data-stu-id="9953e-147">Frontend configuration</span></span>
  * <span data-ttu-id="9953e-148">Adresse IP 10.0.0.4</span><span class="sxs-lookup"><span data-stu-id="9953e-148">IP address 10.0.0.4</span></span>
* <span data-ttu-id="9953e-149">Configuration du backend</span><span class="sxs-lookup"><span data-stu-id="9953e-149">Backend configuration</span></span>
  * <span data-ttu-id="9953e-150">Connecté aux interfaces réseau principales de toutes les machines virtuelles qui doivent faire partie du cluster NFS</span><span class="sxs-lookup"><span data-stu-id="9953e-150">Connected to primary network interfaces of all virtual machines that should be part of the NFS cluster</span></span>
* <span data-ttu-id="9953e-151">Port de la sonde</span><span class="sxs-lookup"><span data-stu-id="9953e-151">Probe Port</span></span>
  * <span data-ttu-id="9953e-152">Port 61000</span><span class="sxs-lookup"><span data-stu-id="9953e-152">Port 61000</span></span>
* <span data-ttu-id="9953e-153">Règles d’équilibrage de charge</span><span class="sxs-lookup"><span data-stu-id="9953e-153">Loadbalancing rules</span></span>
  * <span data-ttu-id="9953e-154">TCP 2049</span><span class="sxs-lookup"><span data-stu-id="9953e-154">2049 TCP</span></span> 
  * <span data-ttu-id="9953e-155">UDP 2049</span><span class="sxs-lookup"><span data-stu-id="9953e-155">2049 UDP</span></span>

### <a name="ascs"></a><span data-ttu-id="9953e-156">(A)SCS</span><span class="sxs-lookup"><span data-stu-id="9953e-156">(A)SCS</span></span>
* <span data-ttu-id="9953e-157">Configuration du frontend</span><span class="sxs-lookup"><span data-stu-id="9953e-157">Frontend configuration</span></span>
  * <span data-ttu-id="9953e-158">Adresse IP 10.0.0.10</span><span class="sxs-lookup"><span data-stu-id="9953e-158">IP address 10.0.0.10</span></span>
* <span data-ttu-id="9953e-159">Configuration du backend</span><span class="sxs-lookup"><span data-stu-id="9953e-159">Backend configuration</span></span>
  * <span data-ttu-id="9953e-160">Connecté aux interfaces réseau principales de toutes les machines virtuelles qui doivent faire partie du cluster (A)SCS/ERS</span><span class="sxs-lookup"><span data-stu-id="9953e-160">Connected to primary network interfaces of all virtual machines that should be part of the (A)SCS/ERS cluster</span></span>
* <span data-ttu-id="9953e-161">Port de la sonde</span><span class="sxs-lookup"><span data-stu-id="9953e-161">Probe Port</span></span>
  * <span data-ttu-id="9953e-162">Port 620**&lt;nr&gt;**</span><span class="sxs-lookup"><span data-stu-id="9953e-162">Port 620**&lt;nr&gt;**</span></span>
* <span data-ttu-id="9953e-163">Règles d’équilibrage de charge</span><span class="sxs-lookup"><span data-stu-id="9953e-163">Loadbalancing rules</span></span>
  * <span data-ttu-id="9953e-164">TCP 32**&lt;nr&gt;**</span><span class="sxs-lookup"><span data-stu-id="9953e-164">32**&lt;nr&gt;** TCP</span></span>
  * <span data-ttu-id="9953e-165">TCP 36**&lt;nr&gt;**</span><span class="sxs-lookup"><span data-stu-id="9953e-165">36**&lt;nr&gt;** TCP</span></span>
  * <span data-ttu-id="9953e-166">TCP 39**&lt;nr&gt;**</span><span class="sxs-lookup"><span data-stu-id="9953e-166">39**&lt;nr&gt;** TCP</span></span>
  * <span data-ttu-id="9953e-167">TCP 81**&lt;nr&gt;**</span><span class="sxs-lookup"><span data-stu-id="9953e-167">81**&lt;nr&gt;** TCP</span></span>
  * <span data-ttu-id="9953e-168">TCP 5**&lt;nr&gt;**13</span><span class="sxs-lookup"><span data-stu-id="9953e-168">5**&lt;nr&gt;**13 TCP</span></span>
  * <span data-ttu-id="9953e-169">TCP 5**&lt;nr&gt;**14</span><span class="sxs-lookup"><span data-stu-id="9953e-169">5**&lt;nr&gt;**14 TCP</span></span>
  * <span data-ttu-id="9953e-170">TCP 5**&lt;nr&gt;**16</span><span class="sxs-lookup"><span data-stu-id="9953e-170">5**&lt;nr&gt;**16 TCP</span></span>

### <a name="ers"></a><span data-ttu-id="9953e-171">ERS</span><span class="sxs-lookup"><span data-stu-id="9953e-171">ERS</span></span>
* <span data-ttu-id="9953e-172">Configuration du frontend</span><span class="sxs-lookup"><span data-stu-id="9953e-172">Frontend configuration</span></span>
  * <span data-ttu-id="9953e-173">Adresse IP 10.0.0.11</span><span class="sxs-lookup"><span data-stu-id="9953e-173">IP address 10.0.0.11</span></span>
* <span data-ttu-id="9953e-174">Configuration du backend</span><span class="sxs-lookup"><span data-stu-id="9953e-174">Backend configuration</span></span>
  * <span data-ttu-id="9953e-175">Connecté aux interfaces réseau principales de toutes les machines virtuelles qui doivent faire partie du cluster (A)SCS/ERS</span><span class="sxs-lookup"><span data-stu-id="9953e-175">Connected to primary network interfaces of all virtual machines that should be part of the (A)SCS/ERS cluster</span></span>
* <span data-ttu-id="9953e-176">Port de la sonde</span><span class="sxs-lookup"><span data-stu-id="9953e-176">Probe Port</span></span>
  * <span data-ttu-id="9953e-177">Port 621**&lt;nr&gt;**</span><span class="sxs-lookup"><span data-stu-id="9953e-177">Port 621**&lt;nr&gt;**</span></span>
* <span data-ttu-id="9953e-178">Règles d’équilibrage de charge</span><span class="sxs-lookup"><span data-stu-id="9953e-178">Loadbalancing rules</span></span>
  * <span data-ttu-id="9953e-179">TCP 33**&lt;nr&gt;**</span><span class="sxs-lookup"><span data-stu-id="9953e-179">33**&lt;nr&gt;** TCP</span></span>
  * <span data-ttu-id="9953e-180">TCP 5**&lt;nr&gt;**13</span><span class="sxs-lookup"><span data-stu-id="9953e-180">5**&lt;nr&gt;**13 TCP</span></span>
  * <span data-ttu-id="9953e-181">TCP 5**&lt;nr&gt;**14</span><span class="sxs-lookup"><span data-stu-id="9953e-181">5**&lt;nr&gt;**14 TCP</span></span>
  * <span data-ttu-id="9953e-182">TCP 5**&lt;nr&gt;**16</span><span class="sxs-lookup"><span data-stu-id="9953e-182">5**&lt;nr&gt;**16 TCP</span></span>

### <a name="sap-hana"></a><span data-ttu-id="9953e-183">SAP HANA</span><span class="sxs-lookup"><span data-stu-id="9953e-183">SAP HANA</span></span>
* <span data-ttu-id="9953e-184">Configuration du frontend</span><span class="sxs-lookup"><span data-stu-id="9953e-184">Frontend configuration</span></span>
  * <span data-ttu-id="9953e-185">Adresse IP 10.0.0.12</span><span class="sxs-lookup"><span data-stu-id="9953e-185">IP address 10.0.0.12</span></span>
* <span data-ttu-id="9953e-186">Configuration du backend</span><span class="sxs-lookup"><span data-stu-id="9953e-186">Backend configuration</span></span>
  * <span data-ttu-id="9953e-187">Connecté aux interfaces réseau principales de toutes les machines virtuelles qui doivent faire partie du cluster HANA</span><span class="sxs-lookup"><span data-stu-id="9953e-187">Connected to primary network interfaces of all virtual machines that should be part of the HANA cluster</span></span>
* <span data-ttu-id="9953e-188">Port de la sonde</span><span class="sxs-lookup"><span data-stu-id="9953e-188">Probe Port</span></span>
  * <span data-ttu-id="9953e-189">Port 625**&lt;nr&gt;**</span><span class="sxs-lookup"><span data-stu-id="9953e-189">Port 625**&lt;nr&gt;**</span></span>
* <span data-ttu-id="9953e-190">Règles d’équilibrage de charge</span><span class="sxs-lookup"><span data-stu-id="9953e-190">Loadbalancing rules</span></span>
  * <span data-ttu-id="9953e-191">TCP 3**&lt;nr&gt;**15</span><span class="sxs-lookup"><span data-stu-id="9953e-191">3**&lt;nr&gt;**15 TCP</span></span>
  * <span data-ttu-id="9953e-192">TCP 3**&lt;nr&gt;**17</span><span class="sxs-lookup"><span data-stu-id="9953e-192">3**&lt;nr&gt;**17 TCP</span></span>

## <a name="setting-up-a-highly-available-nfs-server"></a><span data-ttu-id="9953e-193">Configuration d’un serveur NFS à haute disponibilité</span><span class="sxs-lookup"><span data-stu-id="9953e-193">Setting up a highly available NFS server</span></span>

### <a name="deploying-linux"></a><span data-ttu-id="9953e-194">Déploiement de Linux</span><span class="sxs-lookup"><span data-stu-id="9953e-194">Deploying Linux</span></span>

<span data-ttu-id="9953e-195">La Place de marché Azure contient une image de SUSE Linux Enterprise Server for SAP Applications 12 que vous pouvez utiliser pour déployer de nouvelles machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="9953e-195">The Azure Marketplace contains an image for SUSE Linux Enterprise Server for SAP Applications 12 that you can use to deploy new virtual machines.</span></span>
<span data-ttu-id="9953e-196">Vous pouvez utiliser un des modèles de démarrage rapide disponibles sur github pour déployer toutes les ressources requises.</span><span class="sxs-lookup"><span data-stu-id="9953e-196">You can use one of the quick start templates on github to deploy all required resources.</span></span> <span data-ttu-id="9953e-197">Le modèle déploie les machines virtuelles, l’équilibrage de charge, le groupe à haute disponibilité, etc. Suivez ces étapes pour déployer le modèle :</span><span class="sxs-lookup"><span data-stu-id="9953e-197">The template deploys the virtual machines, the load balancer, availability set etc. Follow these steps to deploy the template:</span></span>

1. <span data-ttu-id="9953e-198">Ouvrez le [modèle de serveur de fichiers SAP][template-file-server] dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="9953e-198">Open the [SAP file server template][template-file-server] in the Azure portal</span></span>   
1. <span data-ttu-id="9953e-199">Entrez les paramètres suivants.</span><span class="sxs-lookup"><span data-stu-id="9953e-199">Enter the following parameters</span></span>
   1. <span data-ttu-id="9953e-200">Préfixe de ressource</span><span class="sxs-lookup"><span data-stu-id="9953e-200">Resource Prefix</span></span>  
      <span data-ttu-id="9953e-201">Entrez le préfixe à utiliser.</span><span class="sxs-lookup"><span data-stu-id="9953e-201">Enter the prefix you want to use.</span></span> <span data-ttu-id="9953e-202">Cette valeur sera utilisée comme préfixe pour les ressources déployées.</span><span class="sxs-lookup"><span data-stu-id="9953e-202">The value is used as a prefix for the resources that are deployed.</span></span>
   2. <span data-ttu-id="9953e-203">Type de système d’exploitation</span><span class="sxs-lookup"><span data-stu-id="9953e-203">Os Type</span></span>  
      <span data-ttu-id="9953e-204">Sélectionnez l’une des distributions Linux.</span><span class="sxs-lookup"><span data-stu-id="9953e-204">Select one of the Linux distributions.</span></span> <span data-ttu-id="9953e-205">Dans cet exemple, sélectionnez SLES 12.</span><span class="sxs-lookup"><span data-stu-id="9953e-205">For this example, select SLES 12</span></span>
   3. <span data-ttu-id="9953e-206">Nom d’utilisateur et mot de passe d’administrateur</span><span class="sxs-lookup"><span data-stu-id="9953e-206">Admin Username and Admin Password</span></span>  
      <span data-ttu-id="9953e-207">Un utilisateur pouvant être utilisé pour ouvrir une session sur la machine est créé.</span><span class="sxs-lookup"><span data-stu-id="9953e-207">A new user is created that can be used to log on to the machine.</span></span>
   4. <span data-ttu-id="9953e-208">ID du sous-réseau</span><span class="sxs-lookup"><span data-stu-id="9953e-208">Subnet Id</span></span>  
      <span data-ttu-id="9953e-209">ID du sous-réseau auquel les machines virtuelles doivent être connectées.</span><span class="sxs-lookup"><span data-stu-id="9953e-209">The ID of the subnet to which the virtual machines should be connected to.</span></span> <span data-ttu-id="9953e-210">Laissez vide si vous souhaitez créer un réseau virtuel, ou sélectionnez le sous-réseau de votre VPN ou réseau virtuel Express Route pour connecter la machine virtuelle à votre réseau local.</span><span class="sxs-lookup"><span data-stu-id="9953e-210">Leave empty if you want to create a new virtual network or select the subnet of your VPN or Express Route virtual network to connect the virtual machine to your on-premises network.</span></span> <span data-ttu-id="9953e-211">L’ID se présente généralement comme suit : /subscriptions/**&lt;ID_abonnement&gt;**/resourceGroups/**&lt;nom_groupe_ressources&gt;**/providers/Microsoft.Network/virtualNetworks/**&lt;nom_réseau_virtuel&gt;**/subnets/**&lt;nom_sous_réseau&gt;**</span><span class="sxs-lookup"><span data-stu-id="9953e-211">The ID usually looks like /subscriptions/**&lt;subscription id&gt;**/resourceGroups/**&lt;resource group name&gt;**/providers/Microsoft.Network/virtualNetworks/**&lt;virtual network name&gt;**/subnets/**&lt;subnet name&gt;**</span></span>

### <a name="installation"></a><span data-ttu-id="9953e-212">Installation</span><span class="sxs-lookup"><span data-stu-id="9953e-212">Installation</span></span>

<span data-ttu-id="9953e-213">Les éléments suivants sont précédés de **[A]** (applicable à tous les nœuds), de **[1]** (applicable uniquement au nœud 1) ou de **[2]** (applicable uniquement au nœud 2).</span><span class="sxs-lookup"><span data-stu-id="9953e-213">The following items are prefixed with either **[A]** - applicable to all nodes, **[1]** - only applicable to node 1 or **[2]** - only applicable to node 2.</span></span>

1. <span data-ttu-id="9953e-214">**[A]** Mettre à jour SLES</span><span class="sxs-lookup"><span data-stu-id="9953e-214">**[A]** Update SLES</span></span>

   <pre><code>
   sudo zypper update
   </code></pre>

1. <span data-ttu-id="9953e-215">**[1]** Activer l’accès SSH</span><span class="sxs-lookup"><span data-stu-id="9953e-215">**[1]** Enable ssh access</span></span>

   <pre><code>
   sudo ssh-keygen -tdsa
   
   # Enter file in which to save the key (/root/.ssh/id_dsa): -> ENTER
   # Enter passphrase (empty for no passphrase): -> ENTER
   # Enter same passphrase again: -> ENTER
   
   # copy the public key
   sudo cat /root/.ssh/id_dsa.pub
   </code></pre>

2. <span data-ttu-id="9953e-216">**[2**] Activer l’accès SSH</span><span class="sxs-lookup"><span data-stu-id="9953e-216">**[2]** Enable ssh access</span></span>

   <pre><code>
   sudo ssh-keygen -tdsa

   # insert the public key you copied in the last step into the authorized keys file on the second server
   sudo vi /root/.ssh/authorized_keys
   
   # Enter file in which to save the key (/root/.ssh/id_dsa): -> ENTER
   # Enter passphrase (empty for no passphrase): -> ENTER
   # Enter same passphrase again: -> ENTER
   
   # copy the public key   
   sudo cat /root/.ssh/id_dsa.pub
   </code></pre>

1. <span data-ttu-id="9953e-217">**[1]** Activer l’accès SSH</span><span class="sxs-lookup"><span data-stu-id="9953e-217">**[1]** Enable ssh access</span></span>

   <pre><code>
   # insert the public key you copied in the last step into the authorized keys file on the first server
   sudo vi /root/.ssh/authorized_keys
   </code></pre>

1. <span data-ttu-id="9953e-218">**[A]** Installer l’extension de haute disponibilité</span><span class="sxs-lookup"><span data-stu-id="9953e-218">**[A]** Install HA extension</span></span>
   
   <pre><code>
   sudo zypper install sle-ha-release fence-agents
   </code></pre>

1. <span data-ttu-id="9953e-219">**[A]** Configurer la résolution de nom d’hôte</span><span class="sxs-lookup"><span data-stu-id="9953e-219">**[A]** Setup host name resolution</span></span>   

   <span data-ttu-id="9953e-220">Vous pouvez utiliser un serveur DNS ou modifier le fichier /etc/hosts sur tous les nœuds.</span><span class="sxs-lookup"><span data-stu-id="9953e-220">You can either use a DNS server or modify the /etc/hosts on all nodes.</span></span> <span data-ttu-id="9953e-221">Cet exemple montre comment utiliser le fichier /etc/hosts.</span><span class="sxs-lookup"><span data-stu-id="9953e-221">This example shows how to use the /etc/hosts file.</span></span>
   <span data-ttu-id="9953e-222">Remplacez l’adresse IP et le nom d’hôte dans les commandes suivantes</span><span class="sxs-lookup"><span data-stu-id="9953e-222">Replace the IP address and the hostname in the following commands</span></span>

   <pre><code>
   sudo vi /etc/hosts
   </code></pre>
   
   <span data-ttu-id="9953e-223">Insérez les lignes suivantes dans le fichier /etc/hosts.</span><span class="sxs-lookup"><span data-stu-id="9953e-223">Insert the following lines to /etc/hosts.</span></span> <span data-ttu-id="9953e-224">Modifiez l’adresse IP et le nom d’hôte en fonction de votre environnement</span><span class="sxs-lookup"><span data-stu-id="9953e-224">Change the IP address and hostname to match your environment</span></span>   
   
   <pre><code>
   # IP address of the load balancer frontend configuration for NFS
   <b>10.0.0.4 nws-nfs</b>
   </code></pre>

1. <span data-ttu-id="9953e-225">**[1]** Installer le cluster</span><span class="sxs-lookup"><span data-stu-id="9953e-225">**[1]** Install Cluster</span></span>
   
   <pre><code>
   sudo ha-cluster-init
   
   # Do you want to continue anyway? [y/N] -> y
   # Network address to bind to (for example: 192.168.1.0) [10.79.227.0] -> ENTER
   # Multicast address (for example: 239.x.x.x) [239.174.218.125] -> ENTER
   # Multicast port [5405] -> ENTER
   # Do you wish to use SBD? [y/N] -> N
   # Do you wish to configure an administration IP? [y/N] -> N
   </code></pre>

1. <span data-ttu-id="9953e-226">**[2]** Ajouter un nœud au cluster</span><span class="sxs-lookup"><span data-stu-id="9953e-226">**[2]** Add node to cluster</span></span>
   
   <pre><code> 
   sudo ha-cluster-join

   # WARNING: NTP is not configured to start at system boot.
   # WARNING: No watchdog device found. If SBD is used, the cluster will be unable to start without a watchdog.
   # Do you want to continue anyway? [y/N] -> y
   # IP address or hostname of existing node (for example: 192.168.1.1) [] -> IP address of node 1 for example 10.0.0.10
   # /root/.ssh/id_dsa already exists - overwrite? [y/N] N
   </code></pre>

1. <span data-ttu-id="9953e-227">**[A]** Changer le mot de passe hacluster pour utiliser le même mot de passe</span><span class="sxs-lookup"><span data-stu-id="9953e-227">**[A]** Change hacluster password to the same password</span></span>

   <pre><code> 
   sudo passwd hacluster
   </code></pre>

1. <span data-ttu-id="9953e-228">**[A]** Configurer corosync pour utiliser les autres transports et ajouter la liste de nœuds</span><span class="sxs-lookup"><span data-stu-id="9953e-228">**[A]** Configure corosync to use other transport and add nodelist.</span></span> <span data-ttu-id="9953e-229">Le cluster ne fonctionnera pas dans le cas contraire.</span><span class="sxs-lookup"><span data-stu-id="9953e-229">Cluster will not work otherwise.</span></span>
   
   <pre><code> 
   sudo vi /etc/corosync/corosync.conf   
   </code></pre>

   <span data-ttu-id="9953e-230">Ajoutez le contenu en gras ci-dessous au fichier.</span><span class="sxs-lookup"><span data-stu-id="9953e-230">Add the following bold content to the file.</span></span>
   
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

   <span data-ttu-id="9953e-231">Redémarrez ensuite le service corosync</span><span class="sxs-lookup"><span data-stu-id="9953e-231">Then restart the corosync service</span></span>

   <pre><code>
   sudo service corosync restart
   </code></pre>

1. <span data-ttu-id="9953e-232">**[A]** Installer les composants drbd</span><span class="sxs-lookup"><span data-stu-id="9953e-232">**[A]** Install drbd components</span></span>

   <pre><code>
   sudo zypper install drbd drbd-kmp-default drbd-utils
   </code></pre>

1. <span data-ttu-id="9953e-233">**[A]** Créer une partition pour l’appareil drbd</span><span class="sxs-lookup"><span data-stu-id="9953e-233">**[A]** Create a partition for the drbd device</span></span>

   <pre><code>
   sudo sh -c 'echo -e "n\n\n\n\n\nw\n" | fdisk /dev/sdc'
   </code></pre>

1. <span data-ttu-id="9953e-234">**[A]** Créer des configurations LVM</span><span class="sxs-lookup"><span data-stu-id="9953e-234">**[A]** Create LVM configurations</span></span>

   <pre><code>
   sudo pvcreate /dev/sdc1   
   sudo vgcreate vg_NFS /dev/sdc1
   sudo lvcreate -l 100%FREE -n <b>NWS</b> vg_NFS
   </code></pre>

1. <span data-ttu-id="9953e-235">**[A]** Créer l’appareil drbd NFS</span><span class="sxs-lookup"><span data-stu-id="9953e-235">**[A]** Create the NFS drbd device</span></span>

   <pre><code>
   sudo vi /etc/drbd.d/<b>NWS</b>_nfs.res
   </code></pre>

   <span data-ttu-id="9953e-236">Insérer la configuration pour le nouvel appareil drbd et quitter</span><span class="sxs-lookup"><span data-stu-id="9953e-236">Insert the configuration for the new drbd device and exit</span></span>

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

   <span data-ttu-id="9953e-237">Créer l’appareil drbd et le démarrer</span><span class="sxs-lookup"><span data-stu-id="9953e-237">Create the drbd device and start it</span></span>

   <pre><code>
   sudo drbdadm create-md <b>NWS</b>_nfs
   sudo drbdadm up <b>NWS</b>_nfs
   </code></pre>

1. <span data-ttu-id="9953e-238">**[1]** Ignorer la synchronisation initiale</span><span class="sxs-lookup"><span data-stu-id="9953e-238">**[1]** Skip initial synchronization</span></span>

   <pre><code>
   sudo drbdadm new-current-uuid --clear-bitmap <b>NWS</b>_nfs
   </code></pre>

1. <span data-ttu-id="9953e-239">**[1]** Définir le nœud principal</span><span class="sxs-lookup"><span data-stu-id="9953e-239">**[1]** Set the primary node</span></span>

   <pre><code>
   sudo drbdadm primary --force <b>NWS</b>_nfs
   </code></pre>

1. <span data-ttu-id="9953e-240">**[1]** Patienter jusqu’à ce que les nouveaux appareils drbd soient synchronisés</span><span class="sxs-lookup"><span data-stu-id="9953e-240">**[1]** Wait until the new drbd devices are synchronized</span></span>

   <pre><code>
   sudo cat /proc/drbd

   # version: 8.4.6 (api:1/proto:86-101)
   # GIT-hash: 833d830e0152d1e457fa7856e71e11248ccf3f70 build by abuild@sheep14, 2016-05-09 23:14:56
   # 0: cs:Connected ro:Primary/Secondary ds:UpToDate/UpToDate C r-----
   #    ns:0 nr:0 dw:0 dr:912 al:8 bm:0 lo:0 pe:0 ua:0 ap:0 ep:1 wo:f oos:0
   </code></pre>

1. <span data-ttu-id="9953e-241">**[1]** Créer des systèmes de fichiers sur les appareils drbd</span><span class="sxs-lookup"><span data-stu-id="9953e-241">**[1]** Create file systems on the drbd devices</span></span>

   <pre><code>
   sudo mkfs.xfs /dev/drbd0
   </code></pre>


### <a name="configure-cluster-framework"></a><span data-ttu-id="9953e-242">Configurer le framework du cluster</span><span class="sxs-lookup"><span data-stu-id="9953e-242">Configure Cluster Framework</span></span>

1. <span data-ttu-id="9953e-243">**[1]** Changer les paramètres par défaut</span><span class="sxs-lookup"><span data-stu-id="9953e-243">**[1]** Change the default settings</span></span>

   <pre><code>
   sudo crm configure

   crm(live)configure# rsc_defaults resource-stickiness="1"

   crm(live)configure# commit
   crm(live)configure# exit
   </code></pre>

1. <span data-ttu-id="9953e-244">**[1]** Ajouter l’appareil drbd NFS à la configuration de cluster</span><span class="sxs-lookup"><span data-stu-id="9953e-244">**[1]** Add the NFS drbd device to the cluster configuration</span></span>

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

1. <span data-ttu-id="9953e-245">**[1]** Créer le serveur NFS</span><span class="sxs-lookup"><span data-stu-id="9953e-245">**[1]** Create the NFS server</span></span>

   <pre><code>
   sudo crm configure

   crm(live)configure# primitive nfsserver \
     systemd:nfs-server \
     op monitor interval="30s"

   crm(live)configure# clone cl-nfsserver nfsserver interleave="true"

   crm(live)configure# commit
   crm(live)configure# exit
   </code></pre>

1. <span data-ttu-id="9953e-246">**[1]** Créer les ressources de système de fichiers NFS</span><span class="sxs-lookup"><span data-stu-id="9953e-246">**[1]** Create the NFS File System resources</span></span>

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

1. <span data-ttu-id="9953e-247">**[1]** Créer les exportations NFS</span><span class="sxs-lookup"><span data-stu-id="9953e-247">**[1]** Create the NFS exports</span></span>

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

1. <span data-ttu-id="9953e-248">**[1]** Créer une ressource IP virtuelle et la sonde d’intégrité pour l’équilibreur de charge interne</span><span class="sxs-lookup"><span data-stu-id="9953e-248">**[1]** Create a virtual IP resource and health-probe for the internal load balancer</span></span>

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

### <a name="create-stonith-device"></a><span data-ttu-id="9953e-249">Créer l’appareil STONITH</span><span class="sxs-lookup"><span data-stu-id="9953e-249">Create STONITH device</span></span>

<span data-ttu-id="9953e-250">L’appareil STONITH utilise un principal de service pour l’autorisation sur Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="9953e-250">The STONITH device uses a Service Principal to authorize against Microsoft Azure.</span></span> <span data-ttu-id="9953e-251">Pour créer un principal de service, effectuez les étapes suivantes.</span><span class="sxs-lookup"><span data-stu-id="9953e-251">Follow these steps to create a Service Principal.</span></span>

1. <span data-ttu-id="9953e-252">Accédez à <https://portal.azure.com></span><span class="sxs-lookup"><span data-stu-id="9953e-252">Go to <https://portal.azure.com></span></span>
1. <span data-ttu-id="9953e-253">Ouvrez le panneau Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="9953e-253">Open the Azure Active Directory blade</span></span>  
   <span data-ttu-id="9953e-254">Accédez aux propriétés et notez l’ID de répertoire.</span><span class="sxs-lookup"><span data-stu-id="9953e-254">Go to Properties and write down the Directory Id.</span></span> <span data-ttu-id="9953e-255">Il s’agit de **l’ID client**.</span><span class="sxs-lookup"><span data-stu-id="9953e-255">This is the **tenant id**.</span></span>
1. <span data-ttu-id="9953e-256">Cliquez sur Inscriptions d’applications</span><span class="sxs-lookup"><span data-stu-id="9953e-256">Click App registrations</span></span>
1. <span data-ttu-id="9953e-257">Cliquez sur Ajouter.</span><span class="sxs-lookup"><span data-stu-id="9953e-257">Click Add</span></span>
1. <span data-ttu-id="9953e-258">Entrez un nom, sélectionnez le type d’application « Application web/API », entrez une URL de connexion (par exemple, http://localhost) et cliquez sur Créer</span><span class="sxs-lookup"><span data-stu-id="9953e-258">Enter a Name, select Application Type "Web app/API", enter a sign-on URL (for example http://localhost) and click Create</span></span>
1. <span data-ttu-id="9953e-259">L’URL de connexion n’est pas utilisée et peut être une URL valide</span><span class="sxs-lookup"><span data-stu-id="9953e-259">The sign-on URL is not used and can be any valid URL</span></span>
1. <span data-ttu-id="9953e-260">Sélectionnez la nouvelle application et cliquez sur Clés dans l’onglet Paramètres</span><span class="sxs-lookup"><span data-stu-id="9953e-260">Select the new App and click Keys in the Settings tab</span></span>
1. <span data-ttu-id="9953e-261">Entrez une description pour la nouvelle clé, sélectionnez « N’expire jamais » et cliquez sur Enregistrer</span><span class="sxs-lookup"><span data-stu-id="9953e-261">Enter a description for a new key, select "Never expires" and click Save</span></span>
1. <span data-ttu-id="9953e-262">Notez la valeur.</span><span class="sxs-lookup"><span data-stu-id="9953e-262">Write down the Value.</span></span> <span data-ttu-id="9953e-263">Cette valeur est utilisée comme **mot de passe** pour le principal de service</span><span class="sxs-lookup"><span data-stu-id="9953e-263">It is used as the **password** for the Service Principal</span></span>
1. <span data-ttu-id="9953e-264">Notez l’ID de l’application.</span><span class="sxs-lookup"><span data-stu-id="9953e-264">Write down the Application Id.</span></span> <span data-ttu-id="9953e-265">Cet identifiant est utilisé comme nom d’utilisateur (**ID de connexion** dans la procédure ci-dessous) du principal de service</span><span class="sxs-lookup"><span data-stu-id="9953e-265">It is used as the username (**login id** in the steps below) of the Service Principal</span></span>

<span data-ttu-id="9953e-266">Par défaut, le principal de service ne possède pas les autorisations d’accéder à vos ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="9953e-266">The Service Principal does not have permissions to access your Azure resources by default.</span></span> <span data-ttu-id="9953e-267">Vous devez accorder au principal de service les autorisations de démarrer et arrêter (libérer) toutes les machines virtuelles du cluster.</span><span class="sxs-lookup"><span data-stu-id="9953e-267">You need to give the Service Principal permissions to start and stop (deallocate) all virtual machines of the cluster.</span></span>

1. <span data-ttu-id="9953e-268">Accédez à https://portal.azure.com</span><span class="sxs-lookup"><span data-stu-id="9953e-268">Go to https://portal.azure.com</span></span>
1. <span data-ttu-id="9953e-269">Ouvrez le panneau Toutes les ressources</span><span class="sxs-lookup"><span data-stu-id="9953e-269">Open the All resources blade</span></span>
1. <span data-ttu-id="9953e-270">Sélectionnez la machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="9953e-270">Select the virtual machine</span></span>
1. <span data-ttu-id="9953e-271">Cliquez sur Contrôle d’accès (IAM)</span><span class="sxs-lookup"><span data-stu-id="9953e-271">Click Access control (IAM)</span></span>
1. <span data-ttu-id="9953e-272">Cliquez sur Ajouter.</span><span class="sxs-lookup"><span data-stu-id="9953e-272">Click Add</span></span>
1. <span data-ttu-id="9953e-273">Sélectionnez le rôle de propriétaire</span><span class="sxs-lookup"><span data-stu-id="9953e-273">Select the role Owner</span></span>
1. <span data-ttu-id="9953e-274">Entrez le nom de l’application que vous avez créée ci-dessus</span><span class="sxs-lookup"><span data-stu-id="9953e-274">Enter the name of the application you created above</span></span>
1. <span data-ttu-id="9953e-275">Cliquez sur OK</span><span class="sxs-lookup"><span data-stu-id="9953e-275">Click OK</span></span>

#### <a name="1-create-the-stonith-devices"></a><span data-ttu-id="9953e-276">**[1]**  Créer les appareils STONITH</span><span class="sxs-lookup"><span data-stu-id="9953e-276">**[1]** Create the STONITH devices</span></span>

<span data-ttu-id="9953e-277">Une fois que vous avez modifié les autorisations pour les machines virtuelles, vous pouvez configurer les appareils STONITH dans le cluster.</span><span class="sxs-lookup"><span data-stu-id="9953e-277">After you edited the permissions for the virtual machines, you can configure the STONITH devices in the cluster.</span></span>

<pre><code>
sudo crm configure

# replace the bold string with your subscription id, resource group, tenant id, service principal id and password

crm(live)configure# primitive rsc_st_azure_1 stonith:fence_azure_arm \
   params subscriptionId="<b>subscription id</b>" resourceGroup="<b>resource group</b>" tenantId="<b>tenant id</b>" login="<b>login id</b>" passwd="<b>password</b>"

crm(live)configure# primitive rsc_st_azure_2 stonith:fence_azure_arm \
   params subscriptionId="<b>subscription id</b>" resourceGroup="<b>resource group</b>" tenantId="<b>tenant id</b>" login="<b>login id</b>" passwd="<b>password</b>"

crm(live)configure# colocation col_st_azure -2000: rsc_st_azure_1:Started rsc_st_azure_2:Started

crm(live)configure# commit
crm(live)configure# exit
</code></pre>

#### <a name="1-enable-the-use-of-a-stonith-device"></a><span data-ttu-id="9953e-278">**[1]**  Activer l’utilisation d’un appareil STONITH</span><span class="sxs-lookup"><span data-stu-id="9953e-278">**[1]** Enable the use of a STONITH device</span></span>

<pre><code>
sudo crm configure property stonith-enabled=true 
</code></pre>

## <a name="setting-up-ascs"></a><span data-ttu-id="9953e-279">Configuration de (A)SCS</span><span class="sxs-lookup"><span data-stu-id="9953e-279">Setting up (A)SCS</span></span>

### <a name="deploying-linux"></a><span data-ttu-id="9953e-280">Déploiement de Linux</span><span class="sxs-lookup"><span data-stu-id="9953e-280">Deploying Linux</span></span>

<span data-ttu-id="9953e-281">La Place de marché Azure contient une image de SUSE Linux Enterprise Server for SAP Applications 12 que vous pouvez utiliser pour déployer de nouvelles machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="9953e-281">The Azure Marketplace contains an image for SUSE Linux Enterprise Server for SAP Applications 12 that you can use to deploy new virtual machines.</span></span> <span data-ttu-id="9953e-282">L’image Place de marché contient l’agent de ressource pour SAP NetWeaver.</span><span class="sxs-lookup"><span data-stu-id="9953e-282">The marketplace image contains the resource agent for SAP NetWeaver.</span></span>

<span data-ttu-id="9953e-283">Vous pouvez utiliser un des modèles de démarrage rapide disponibles sur github pour déployer toutes les ressources requises.</span><span class="sxs-lookup"><span data-stu-id="9953e-283">You can use one of the quick start templates on github to deploy all required resources.</span></span> <span data-ttu-id="9953e-284">Le modèle déploie les machines virtuelles, l’équilibrage de charge, le groupe à haute disponibilité, etc. Suivez ces étapes pour déployer le modèle :</span><span class="sxs-lookup"><span data-stu-id="9953e-284">The template deploys the virtual machines, the load balancer, availability set etc. Follow these steps to deploy the template:</span></span>

1. <span data-ttu-id="9953e-285">Ouvrez le [modèle ASCS/SCS Multi SID][template-multisid-xscs] ou le [modèle convergé][template-converged] dans le portail Azure. Le modèle ASCS/SCS crée uniquement les règles d’équilibrage de charge pour les instances de SAP NetWeaver ASCS/SCS et ERS (Linux uniquement), tandis que le modèle convergé crée également les règles d’équilibrage de charge pour une base de données (par exemple Microsoft SQL Server ou SAP HANA).</span><span class="sxs-lookup"><span data-stu-id="9953e-285">Open the [ASCS/SCS Multi SID template][template-multisid-xscs] or the [converged template][template-converged] on the Azure portal The ASCS/SCS template only creates the load-balancing rules for the SAP NetWeaver ASCS/SCS and ERS (Linux only) instances whereas the converged template also creates the load-balancing rules for a database (for example Microsoft SQL Server or SAP HANA).</span></span> <span data-ttu-id="9953e-286">Si vous prévoyez d’installer un système SAP NetWeaver et que vous souhaitez également installer la base de données sur les mêmes machines, utilisez le [modèle convergé][template-converged].</span><span class="sxs-lookup"><span data-stu-id="9953e-286">If you plan to install an SAP NetWeaver based system and you also want to install the database on the same machines, use the [converged template][template-converged].</span></span>
1. <span data-ttu-id="9953e-287">Entrez les paramètres suivants</span><span class="sxs-lookup"><span data-stu-id="9953e-287">Enter the following parameters</span></span>
   1. <span data-ttu-id="9953e-288">Préfixe de ressource (modèle ASCS/SCS Multi SID uniquement)</span><span class="sxs-lookup"><span data-stu-id="9953e-288">Resource Prefix (ASCS/SCS Multi SID template only)</span></span>  
      <span data-ttu-id="9953e-289">Entrez le préfixe à utiliser.</span><span class="sxs-lookup"><span data-stu-id="9953e-289">Enter the prefix you want to use.</span></span> <span data-ttu-id="9953e-290">Cette valeur sera utilisée comme préfixe pour les ressources déployées.</span><span class="sxs-lookup"><span data-stu-id="9953e-290">The value is used as a prefix for the resources that are deployed.</span></span>
   3. <span data-ttu-id="9953e-291">ID du système SAP (modèle convergé uniquement)</span><span class="sxs-lookup"><span data-stu-id="9953e-291">Sap System Id (converged template only)</span></span>  
      <span data-ttu-id="9953e-292">Entrez l’ID du système SAP que vous souhaitez installer.</span><span class="sxs-lookup"><span data-stu-id="9953e-292">Enter the SAP system Id of the SAP system you want to install.</span></span> <span data-ttu-id="9953e-293">Cet ID est utilisé comme préfixe pour les ressources déployées.</span><span class="sxs-lookup"><span data-stu-id="9953e-293">The Id is used as a prefix for the resources that are deployed.</span></span>
   4. <span data-ttu-id="9953e-294">Type de pile</span><span class="sxs-lookup"><span data-stu-id="9953e-294">Stack Type</span></span>  
      <span data-ttu-id="9953e-295">Sélectionnez le type de pile de SAP NetWeaver</span><span class="sxs-lookup"><span data-stu-id="9953e-295">Select the SAP NetWeaver stack type</span></span>
   5. <span data-ttu-id="9953e-296">Type de système d’exploitation</span><span class="sxs-lookup"><span data-stu-id="9953e-296">Os Type</span></span>  
      <span data-ttu-id="9953e-297">Sélectionnez l’une des distributions Linux.</span><span class="sxs-lookup"><span data-stu-id="9953e-297">Select one of the Linux distributions.</span></span> <span data-ttu-id="9953e-298">Dans cet exemple, sélectionnez SLES 12 BYOS</span><span class="sxs-lookup"><span data-stu-id="9953e-298">For this example, select SLES 12 BYOS</span></span>
   6. <span data-ttu-id="9953e-299">Type de base de données</span><span class="sxs-lookup"><span data-stu-id="9953e-299">Db Type</span></span>  
      <span data-ttu-id="9953e-300">Sélectionnez HANA</span><span class="sxs-lookup"><span data-stu-id="9953e-300">Select HANA</span></span>
   7. <span data-ttu-id="9953e-301">Taille du système SAP</span><span class="sxs-lookup"><span data-stu-id="9953e-301">Sap System Size</span></span>  
      <span data-ttu-id="9953e-302">Nombre de SAP fournis par le nouveau système.</span><span class="sxs-lookup"><span data-stu-id="9953e-302">The amount of SAPS the new system provides.</span></span> <span data-ttu-id="9953e-303">Si vous ne savez pas combien de SAP sont requis par le système, demandez à votre partenaire SAP Technology ou à votre intégrateur système.</span><span class="sxs-lookup"><span data-stu-id="9953e-303">If you are not sure how many SAPS the system requires, please ask your SAP Technology Partner or System Integrator</span></span>
   8. <span data-ttu-id="9953e-304">Disponibilité du système</span><span class="sxs-lookup"><span data-stu-id="9953e-304">System Availability</span></span>  
      <span data-ttu-id="9953e-305">Sélectionnez la haute disponibilité (HA).</span><span class="sxs-lookup"><span data-stu-id="9953e-305">Select HA</span></span>
   9. <span data-ttu-id="9953e-306">Nom d’utilisateur et mot de passe d’administrateur</span><span class="sxs-lookup"><span data-stu-id="9953e-306">Admin Username and Admin Password</span></span>  
      <span data-ttu-id="9953e-307">Un utilisateur pouvant être utilisé pour ouvrir une session sur la machine est créé.</span><span class="sxs-lookup"><span data-stu-id="9953e-307">A new user is created that can be used to log on to the machine.</span></span>
   10. <span data-ttu-id="9953e-308">ID du sous-réseau</span><span class="sxs-lookup"><span data-stu-id="9953e-308">Subnet Id</span></span>  
   <span data-ttu-id="9953e-309">ID du sous-réseau auquel les machines virtuelles doivent être connectées.</span><span class="sxs-lookup"><span data-stu-id="9953e-309">The ID of the subnet to which the virtual machines should be connected to.</span></span>  <span data-ttu-id="9953e-310">Laissez vide si vous souhaitez créer un réseau virtuel, ou sélectionnez le même sous-réseau que celui que vous avez utilisé ou créé dans le cadre du déploiement de serveur NFS.</span><span class="sxs-lookup"><span data-stu-id="9953e-310">Leave empty if you want to create a new virtual network or select the same subnet that you used or created as part of the NFS server deployment.</span></span> <span data-ttu-id="9953e-311">L’ID se présente généralement comme suit : /subscriptions/**&lt;ID_abonnement&gt;**/resourceGroups/**&lt;nom_groupe_ressources&gt;**/providers/Microsoft.Network/virtualNetworks/**&lt;nom_réseau_virtuel&gt;**/subnets/**&lt;nom_sous_réseau&gt;**</span><span class="sxs-lookup"><span data-stu-id="9953e-311">The ID usually looks like /subscriptions/**&lt;subscription id&gt;**/resourceGroups/**&lt;resource group name&gt;**/providers/Microsoft.Network/virtualNetworks/**&lt;virtual network name&gt;**/subnets/**&lt;subnet name&gt;**</span></span>

### <a name="installation"></a><span data-ttu-id="9953e-312">Installation</span><span class="sxs-lookup"><span data-stu-id="9953e-312">Installation</span></span>

<span data-ttu-id="9953e-313">Les éléments suivants sont précédés de **[A]** (applicable à tous les nœuds), de **[1]** (applicable uniquement au nœud 1) ou de **[2]** (applicable uniquement au nœud 2).</span><span class="sxs-lookup"><span data-stu-id="9953e-313">The following items are prefixed with either **[A]** - applicable to all nodes, **[1]** - only applicable to node 1 or **[2]** - only applicable to node 2.</span></span>

1. <span data-ttu-id="9953e-314">**[A]** Mettre à jour SLES</span><span class="sxs-lookup"><span data-stu-id="9953e-314">**[A]** Update SLES</span></span>

   <pre><code>
   sudo zypper update
   </code></pre>

1. <span data-ttu-id="9953e-315">**[1]** Activer l’accès SSH</span><span class="sxs-lookup"><span data-stu-id="9953e-315">**[1]** Enable ssh access</span></span>

   <pre><code>
   sudo ssh-keygen -tdsa
   
   # Enter file in which to save the key (/root/.ssh/id_dsa): -> ENTER
   # Enter passphrase (empty for no passphrase): -> ENTER
   # Enter same passphrase again: -> ENTER
   
   # copy the public key
   sudo cat /root/.ssh/id_dsa.pub
   </code></pre>

2. <span data-ttu-id="9953e-316">**[2**] Activer l’accès SSH</span><span class="sxs-lookup"><span data-stu-id="9953e-316">**[2]** Enable ssh access</span></span>

   <pre><code>
   sudo ssh-keygen -tdsa

   # insert the public key you copied in the last step into the authorized keys file on the second server
   sudo vi /root/.ssh/authorized_keys
   
   # Enter file in which to save the key (/root/.ssh/id_dsa): -> ENTER
   # Enter passphrase (empty for no passphrase): -> ENTER
   # Enter same passphrase again: -> ENTER
   
   # copy the public key   
   sudo cat /root/.ssh/id_dsa.pub
   </code></pre>

1. <span data-ttu-id="9953e-317">**[1]** Activer l’accès SSH</span><span class="sxs-lookup"><span data-stu-id="9953e-317">**[1]** Enable ssh access</span></span>

   <pre><code>
   # insert the public key you copied in the last step into the authorized keys file on the first server
   sudo vi /root/.ssh/authorized_keys
   </code></pre>

1. <span data-ttu-id="9953e-318">**[A]** Installer l’extension de haute disponibilité</span><span class="sxs-lookup"><span data-stu-id="9953e-318">**[A]** Install HA extension</span></span>
   
   <pre><code>
   sudo zypper install sle-ha-release fence-agents
   </code></pre>

1. <span data-ttu-id="9953e-319">**[A]** Mettre à jour les agents de ressources SAP</span><span class="sxs-lookup"><span data-stu-id="9953e-319">**[A]** Update SAP resource agents</span></span>  
   
   <span data-ttu-id="9953e-320">Un correctif pour les agents de ressources est nécessaire pour utiliser la nouvelle configuration décrite dans cet article.</span><span class="sxs-lookup"><span data-stu-id="9953e-320">A patch for the resource-agents package is required to use the new configuration, that is described in this article.</span></span> <span data-ttu-id="9953e-321">Vous pouvez vérifier si le correctif est déjà installé avec la commande suivante.</span><span class="sxs-lookup"><span data-stu-id="9953e-321">You can check, if the patch is already installed with the following command</span></span>

   <pre><code>
   sudo grep 'parameter name="IS_ERS"' /usr/lib/ocf/resource.d/heartbeat/SAPInstance
   </code></pre>

   <span data-ttu-id="9953e-322">La sortie doit ressembler à ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="9953e-322">The output should be similar to</span></span>

   <pre><code>
   &lt;parameter name="IS_ERS" unique="0" required="0"&gt;
   </code></pre>

   <span data-ttu-id="9953e-323">Si la commande grep ne trouve pas le paramètre IS_ERS, vous devez installer le correctif logiciel répertorié dans la [page de téléchargement SUSE](https://download.suse.com/patch/finder/#bu=suse&familyId=&productId=&dateRange=&startDate=&endDate=&priority=&architecture=&keywords=resource-agents).</span><span class="sxs-lookup"><span data-stu-id="9953e-323">If the grep command does not find the IS_ERS parameter, you need to install the patch listed on [the SUSE download page](https://download.suse.com/patch/finder/#bu=suse&familyId=&productId=&dateRange=&startDate=&endDate=&priority=&architecture=&keywords=resource-agents)</span></span>

   <pre><code>
   # example for patch for SLES 12 SP1
   sudo zypper in -t patch SUSE-SLE-HA-12-SP1-2017-885=1
   # example for patch for SLES 12 SP2
   sudo zypper in -t patch SUSE-SLE-HA-12-SP2-2017-886=1
   </code></pre>

1. <span data-ttu-id="9953e-324">**[A]** Configurer la résolution de nom d’hôte</span><span class="sxs-lookup"><span data-stu-id="9953e-324">**[A]** Setup host name resolution</span></span>   

   <span data-ttu-id="9953e-325">Vous pouvez utiliser un serveur DNS ou modifier le fichier /etc/hosts sur tous les nœuds.</span><span class="sxs-lookup"><span data-stu-id="9953e-325">You can either use a DNS server or modify the /etc/hosts on all nodes.</span></span> <span data-ttu-id="9953e-326">Cet exemple montre comment utiliser le fichier /etc/hosts.</span><span class="sxs-lookup"><span data-stu-id="9953e-326">This example shows how to use the /etc/hosts file.</span></span>
   <span data-ttu-id="9953e-327">Remplacez l’adresse IP et le nom d’hôte dans les commandes suivantes</span><span class="sxs-lookup"><span data-stu-id="9953e-327">Replace the IP address and the hostname in the following commands</span></span>

   <pre><code>
   sudo vi /etc/hosts
   </code></pre>
   
   <span data-ttu-id="9953e-328">Insérez les lignes suivantes dans le fichier /etc/hosts.</span><span class="sxs-lookup"><span data-stu-id="9953e-328">Insert the following lines to /etc/hosts.</span></span> <span data-ttu-id="9953e-329">Modifiez l’adresse IP et le nom d’hôte en fonction de votre environnement</span><span class="sxs-lookup"><span data-stu-id="9953e-329">Change the IP address and hostname to match your environment</span></span>   
   
   <pre><code>
   # IP address of the load balancer frontend configuration for NFS
   <b>10.0.0.4 nws-nfs</b>
   # IP address of the load balancer frontend configuration for SAP NetWeaver ASCS/SCS
   <b>10.0.0.10 nws-ascs</b>
   # IP address of the load balancer frontend configuration for SAP NetWeaver ERS
   <b>10.0.0.11 nws-ers</b>
   # IP address of the load balancer frontend configuration for database
   <b>10.0.0.12 nws-db</b>
   </code></pre>

1. <span data-ttu-id="9953e-330">**[1]** Installer le cluster</span><span class="sxs-lookup"><span data-stu-id="9953e-330">**[1]** Install Cluster</span></span>
   
   <pre><code>
   sudo ha-cluster-init
   
   # Do you want to continue anyway? [y/N] -> y
   # Network address to bind to (for example: 192.168.1.0) [10.79.227.0] -> ENTER
   # Multicast address (for example: 239.x.x.x) [239.174.218.125] -> ENTER
   # Multicast port [5405] -> ENTER
   # Do you wish to use SBD? [y/N] -> N
   # Do you wish to configure an administration IP? [y/N] -> N
   </code></pre>

1. <span data-ttu-id="9953e-331">**[2]** Ajouter un nœud au cluster</span><span class="sxs-lookup"><span data-stu-id="9953e-331">**[2]** Add node to cluster</span></span>
   
   <pre><code> 
   sudo ha-cluster-join

   # WARNING: NTP is not configured to start at system boot.
   # WARNING: No watchdog device found. If SBD is used, the cluster will be unable to start without a watchdog.
   # Do you want to continue anyway? [y/N] -> y
   # IP address or hostname of existing node (for example: 192.168.1.1) [] -> IP address of node 1 for example 10.0.0.10
   # /root/.ssh/id_dsa already exists - overwrite? [y/N] N
   </code></pre>

1. <span data-ttu-id="9953e-332">**[A]** Changer le mot de passe hacluster pour utiliser le même mot de passe</span><span class="sxs-lookup"><span data-stu-id="9953e-332">**[A]** Change hacluster password to the same password</span></span>

   <pre><code> 
   sudo passwd hacluster
   </code></pre>

1. <span data-ttu-id="9953e-333">**[A]** Configurer corosync pour utiliser les autres transports et ajouter la liste de nœuds</span><span class="sxs-lookup"><span data-stu-id="9953e-333">**[A]** Configure corosync to use other transport and add nodelist.</span></span> <span data-ttu-id="9953e-334">Le cluster ne fonctionnera pas dans le cas contraire.</span><span class="sxs-lookup"><span data-stu-id="9953e-334">Cluster will not work otherwise.</span></span>
   
   <pre><code> 
   sudo vi /etc/corosync/corosync.conf   
   </code></pre>

   <span data-ttu-id="9953e-335">Ajoutez le contenu en gras ci-dessous au fichier.</span><span class="sxs-lookup"><span data-stu-id="9953e-335">Add the following bold content to the file.</span></span>
   
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

   <span data-ttu-id="9953e-336">Redémarrez ensuite le service corosync</span><span class="sxs-lookup"><span data-stu-id="9953e-336">Then restart the corosync service</span></span>

   <pre><code>
   sudo service corosync restart
   </code></pre>

1. <span data-ttu-id="9953e-337">**[A]** Installer les composants drbd</span><span class="sxs-lookup"><span data-stu-id="9953e-337">**[A]** Install drbd components</span></span>

   <pre><code>
   sudo zypper install drbd drbd-kmp-default drbd-utils
   </code></pre>

1. <span data-ttu-id="9953e-338">**[A]** Créer une partition pour l’appareil drbd</span><span class="sxs-lookup"><span data-stu-id="9953e-338">**[A]** Create a partition for the drbd device</span></span>

   <pre><code>
   sudo sh -c 'echo -e "n\n\n\n\n\nw\n" | fdisk /dev/sdc'
   </code></pre>

1. <span data-ttu-id="9953e-339">**[A]** Créer des configurations LVM</span><span class="sxs-lookup"><span data-stu-id="9953e-339">**[A]** Create LVM configurations</span></span>

   <pre><code>
   sudo pvcreate /dev/sdc1   
   sudo vgcreate vg_<b>NWS</b> /dev/sdc1
   sudo lvcreate -l 50%FREE -n <b>NWS</b>_ASCS vg_<b>NWS</b>
   sudo lvcreate -l 50%FREE -n <b>NWS</b>_ERS vg_<b>NWS</b>
   </code></pre>

1. <span data-ttu-id="9953e-340">**[A]** Créer l’appareil drbd SCS</span><span class="sxs-lookup"><span data-stu-id="9953e-340">**[A]** Create the SCS drbd device</span></span>

   <pre><code>
   sudo vi /etc/drbd.d/<b>NWS</b>_ascs.res
   </code></pre>

   <span data-ttu-id="9953e-341">Insérer la configuration pour le nouvel appareil drbd et quitter</span><span class="sxs-lookup"><span data-stu-id="9953e-341">Insert the configuration for the new drbd device and exit</span></span>

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

   <span data-ttu-id="9953e-342">Créer l’appareil drbd et le démarrer</span><span class="sxs-lookup"><span data-stu-id="9953e-342">Create the drbd device and start it</span></span>

   <pre><code>
   sudo drbdadm create-md <b>NWS</b>_ascs
   sudo drbdadm up <b>NWS</b>_ascs
   </code></pre>

1. <span data-ttu-id="9953e-343">**[A]** Créer l’appareil drbd ERS</span><span class="sxs-lookup"><span data-stu-id="9953e-343">**[A]** Create the ERS drbd device</span></span>

   <pre><code>
   sudo vi /etc/drbd.d/<b>NWS</b>_ers.res
   </code></pre>

   <span data-ttu-id="9953e-344">Insérer la configuration pour le nouvel appareil drbd et quitter</span><span class="sxs-lookup"><span data-stu-id="9953e-344">Insert the configuration for the new drbd device and exit</span></span>

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

   <span data-ttu-id="9953e-345">Créer l’appareil drbd et le démarrer</span><span class="sxs-lookup"><span data-stu-id="9953e-345">Create the drbd device and start it</span></span>

   <pre><code>
   sudo drbdadm create-md <b>NWS</b>_ers
   sudo drbdadm up <b>NWS</b>_ers
   </code></pre>

1. <span data-ttu-id="9953e-346">**[1]** Ignorer la synchronisation initiale</span><span class="sxs-lookup"><span data-stu-id="9953e-346">**[1]** Skip initial synchronization</span></span>

   <pre><code>
   sudo drbdadm new-current-uuid --clear-bitmap <b>NWS</b>_ascs
   sudo drbdadm new-current-uuid --clear-bitmap <b>NWS</b>_ers
   </code></pre>

1. <span data-ttu-id="9953e-347">**[1]** Définir le nœud principal</span><span class="sxs-lookup"><span data-stu-id="9953e-347">**[1]** Set the primary node</span></span>

   <pre><code>
   sudo drbdadm primary --force <b>NWS</b>_ascs
   sudo drbdadm primary --force <b>NWS</b>_ers
   </code></pre>

1. <span data-ttu-id="9953e-348">**[1]** Patienter jusqu’à ce que les nouveaux appareils drbd soient synchronisés</span><span class="sxs-lookup"><span data-stu-id="9953e-348">**[1]** Wait until the new drbd devices are synchronized</span></span>

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

1. <span data-ttu-id="9953e-349">**[1]** Créer des systèmes de fichiers sur les appareils drbd</span><span class="sxs-lookup"><span data-stu-id="9953e-349">**[1]** Create file systems on the drbd devices</span></span>

   <pre><code>
   sudo mkfs.xfs /dev/drbd0
   sudo mkfs.xfs /dev/drbd1
   </code></pre>


### <a name="configure-cluster-framework"></a><span data-ttu-id="9953e-350">Configurer le framework du cluster</span><span class="sxs-lookup"><span data-stu-id="9953e-350">Configure Cluster Framework</span></span>

<span data-ttu-id="9953e-351">**[1]** Changer les paramètres par défaut</span><span class="sxs-lookup"><span data-stu-id="9953e-351">**[1]** Change the default settings</span></span>

   <pre><code>
   sudo crm configure

   crm(live)configure# rsc_defaults resource-stickiness="1"

   crm(live)configure# commit
   crm(live)configure# exit
   </code></pre>

## <a name="prepare-for-sap-netweaver-installation"></a><span data-ttu-id="9953e-352">Préparer l’installation de SAP NetWeaver</span><span class="sxs-lookup"><span data-stu-id="9953e-352">Prepare for SAP NetWeaver installation</span></span>

1. <span data-ttu-id="9953e-353">**[A]** Créer les répertoires partagés</span><span class="sxs-lookup"><span data-stu-id="9953e-353">**[A]** Create the shared directories</span></span>

   <pre><code>
   sudo mkdir -p /sapmnt/<b>NWS</b>
   sudo mkdir -p /usr/sap/trans
   sudo mkdir -p /usr/sap/<b>NWS</b>/SYS

   sudo chattr +i /sapmnt/<b>NWS</b>
   sudo chattr +i /usr/sap/trans
   sudo chattr +i /usr/sap/<b>NWS</b>/SYS
   </code></pre>

1. <span data-ttu-id="9953e-354">**[A]** Configurer autofs</span><span class="sxs-lookup"><span data-stu-id="9953e-354">**[A]** Configure autofs</span></span>
 
   <pre><code>
   sudo vi /etc/auto.master

   # Add the following line to the file, save and exit
   +auto.master
   /- /etc/auto.direct
   </code></pre>

   <span data-ttu-id="9953e-355">Créer un fichier avec</span><span class="sxs-lookup"><span data-stu-id="9953e-355">Create a file with</span></span>

   <pre><code>
   sudo vi /etc/auto.direct

   # Add the following lines to the file, save and exit
   /sapmnt/<b>NWS</b> -nfsvers=4,nosymlink,sync <b>nws-nfs</b>:/sapmntsid
   /usr/sap/trans -nfsvers=4,nosymlink,sync <b>nws-nfs</b>:/trans
   /usr/sap/<b>NWS</b>/SYS -nfsvers=4,nosymlink,sync <b>nws-nfs</b>:/sidsys
   </code></pre>

   <span data-ttu-id="9953e-356">Redémarrer autofs pour monter les nouveaux partages</span><span class="sxs-lookup"><span data-stu-id="9953e-356">Restart autofs to mount the new shares</span></span>

   <pre><code>
   sudo systemctl enable autofs
   sudo service autofs restart
   </code></pre>

1. <span data-ttu-id="9953e-357">**[A]** Configurer le fichier SWAP</span><span class="sxs-lookup"><span data-stu-id="9953e-357">**[A]** Configure SWAP file</span></span>
 
   <pre><code>
   sudo vi /etc/waagent.conf

   # Set the property ResourceDisk.EnableSwap to y
   # Create and use swapfile on resource disk.
   ResourceDisk.EnableSwap=<b>y</b>

   # Set the size of the SWAP file with property ResourceDisk.SwapSizeMB
   # The free space of resource disk varies by virtual machine size. Make sure that you do not set a value that is too big. You can check the SWAP space with command swapon
   # Size of the swapfile.
   ResourceDisk.SwapSizeMB=<b>2000</b>
   </code></pre>

   <span data-ttu-id="9953e-358">Redémarrer l’Agent pour activer la modification</span><span class="sxs-lookup"><span data-stu-id="9953e-358">Restart the Agent to activate the change</span></span>

   <pre><code>
   sudo service waagent restart
   </code></pre>

### <a name="installing-sap-netweaver-ascsers"></a><span data-ttu-id="9953e-359">Installation de SAP NetWeaver ASC/ERS</span><span class="sxs-lookup"><span data-stu-id="9953e-359">Installing SAP NetWeaver ASCS/ERS</span></span>

1. <span data-ttu-id="9953e-360">**[1]** Créer une ressource IP virtuelle et la sonde d’intégrité pour l’équilibreur de charge interne</span><span class="sxs-lookup"><span data-stu-id="9953e-360">**[1]** Create a virtual IP resource and health-probe for the internal load balancer</span></span>

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

   <span data-ttu-id="9953e-361">Vérifiez que l’état du cluster est OK et que toutes les ressources sont démarrées.</span><span class="sxs-lookup"><span data-stu-id="9953e-361">Make sure that the cluster status is ok and that all resources are started.</span></span> <span data-ttu-id="9953e-362">Le nœud sur lequel les ressources s’exécutent n’a aucune importance.</span><span class="sxs-lookup"><span data-stu-id="9953e-362">It is not important on which node the resources are running.</span></span>

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

1. <span data-ttu-id="9953e-363">**[1]** Installer SAP NetWeaver ASCS</span><span class="sxs-lookup"><span data-stu-id="9953e-363">**[1]** Install SAP NetWeaver ASCS</span></span>  

   <span data-ttu-id="9953e-364">Installez SAP NetWeaver ASCS en tant que racine sur le premier nœud à l’aide d’un nom d’hôte virtuel mappé à l’adresse IP de la configuration frontend de l’équilibreur de charge pour l’ASCS, par exemple <b>nws-ascs</b>, <b>10.0.0.10</b>, et du numéro d’instance que vous avez utilisé pour la sonde de l’équilibreur de charge, par exemple <b>00</b>.</span><span class="sxs-lookup"><span data-stu-id="9953e-364">Install SAP NetWeaver ASCS as root on the first node using a virtual hostname that maps to the IP address of the load balancer frontend configuration for the ASCS for example <b>nws-ascs</b>, <b>10.0.0.10</b> and the instance number that you used for the probe of the load balancer for example <b>00</b>.</span></span>

   <span data-ttu-id="9953e-365">Vous pouvez utiliser le paramètre sapinst SAPINST_REMOTE_ACCESS_USER pour autoriser un utilisateur non racine à se connecter à sapinst.</span><span class="sxs-lookup"><span data-stu-id="9953e-365">You can use the sapinst parameter SAPINST_REMOTE_ACCESS_USER to allow a non-root user to connect to sapinst.</span></span>

   <pre><code>
   sudo &lt;swpm&gt;/sapinst SAPINST_REMOTE_ACCESS_USER=<b>sapadmin</b>
   </code></pre>

1. <span data-ttu-id="9953e-366">**[1]** Créer une ressource IP virtuelle et la sonde d’intégrité pour l’équilibreur de charge interne</span><span class="sxs-lookup"><span data-stu-id="9953e-366">**[1]** Create a virtual IP resource and health-probe for the internal load balancer</span></span>

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
   # Do you still want to commit (y/n)? y

   crm(live)configure# exit
   
   </code></pre>
 
   <span data-ttu-id="9953e-367">Vérifiez que l’état du cluster est OK et que toutes les ressources sont démarrées.</span><span class="sxs-lookup"><span data-stu-id="9953e-367">Make sure that the cluster status is ok and that all resources are started.</span></span> <span data-ttu-id="9953e-368">Le nœud sur lequel les ressources s’exécutent n’a aucune importance.</span><span class="sxs-lookup"><span data-stu-id="9953e-368">It is not important on which node the resources are running.</span></span>

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

1. <span data-ttu-id="9953e-369">**[2]** Installer SAP NetWeaver ERS</span><span class="sxs-lookup"><span data-stu-id="9953e-369">**[2]** Install SAP NetWeaver ERS</span></span>  

   <span data-ttu-id="9953e-370">Installez SAP NetWeaver ERS en tant que racine sur le deuxième nœud à l’aide d’un nom d’hôte virtuel mappé à l’adresse IP de la configuration frontend de l’équilibreur de charge pour l’ERS, par exemple <b>nws-ers</b>, <b>10.0.0.11</b>, et du numéro d’instance que vous avez utilisé pour la sonde de l’équilibreur de charge, par exemple <b>02</b>.</span><span class="sxs-lookup"><span data-stu-id="9953e-370">Install SAP NetWeaver ERS as root on the second node using a virtual hostname that maps to the IP address of the load balancer frontend configuration for the ERS for example <b>nws-ers</b>, <b>10.0.0.11</b> and the instance number that you used for the probe of the load balancer for example <b>02</b>.</span></span>

   <span data-ttu-id="9953e-371">Vous pouvez utiliser le paramètre sapinst SAPINST_REMOTE_ACCESS_USER pour autoriser un utilisateur non racine à se connecter à sapinst.</span><span class="sxs-lookup"><span data-stu-id="9953e-371">You can use the sapinst parameter SAPINST_REMOTE_ACCESS_USER to allow a non-root user to connect to sapinst.</span></span>

   <pre><code>
   sudo &lt;swpm&gt;/sapinst SAPINST_REMOTE_ACCESS_USER=<b>sapadmin</b>
   </code></pre>

   > [!NOTE]
   > <span data-ttu-id="9953e-372">Utilisez SWPM SP 20 PL 05 ou ultérieur.</span><span class="sxs-lookup"><span data-stu-id="9953e-372">Please use SWPM SP 20 PL 05 or higher.</span></span> <span data-ttu-id="9953e-373">Les versions antérieures ne définissent pas les autorisations correctement et l’installation échouera.</span><span class="sxs-lookup"><span data-stu-id="9953e-373">Lower versions do not set the permissions correctly and the installation will fail.</span></span>
   > 

1. <span data-ttu-id="9953e-374">**[1]** Adapter les profils d’instance ASCS/SCS et ERS</span><span class="sxs-lookup"><span data-stu-id="9953e-374">**[1]** Adapt the ASCS/SCS and ERS instance profiles</span></span>
 
   * <span data-ttu-id="9953e-375">Profil ASCS/SCS</span><span class="sxs-lookup"><span data-stu-id="9953e-375">ASCS/SCS profile</span></span>

   <pre><code> 
   sudo vi /sapmnt/<b>NWS</b>/profile/<b>NWS</b>_<b>ASCS00</b>_<b>nws-ascs</b>

   # Change the restart command to a start command
   #Restart_Program_01 = local $(_EN) pf=$(_PF)
   Start_Program_01 = local $(_EN) pf=$(_PF)

   # Add the following lines
   service/halib = $(DIR_CT_RUN)/saphascriptco.so
   service/halib_cluster_connector = /usr/bin/sap_suse_cluster_connector

   # Add the keep alive parameter
   enque/encni/set_so_keepalive = true
   </code></pre>

   * <span data-ttu-id="9953e-376">Profil ERS</span><span class="sxs-lookup"><span data-stu-id="9953e-376">ERS profile</span></span>

   <pre><code> 
   sudo vi /sapmnt/<b>NWS</b>/profile/<b>NWS</b>_ERS<b>02</b>_<b>nws-ers</b>

   # Add the following lines
   service/halib = $(DIR_CT_RUN)/saphascriptco.so
   service/halib_cluster_connector = /usr/bin/sap_suse_cluster_connector
   </code></pre>


1. <span data-ttu-id="9953e-377">**[A]** Configurer Keep Alive</span><span class="sxs-lookup"><span data-stu-id="9953e-377">**[A]** Configure Keep Alive</span></span>

   <span data-ttu-id="9953e-378">La communication entre le serveur d’applications SAP NetWeaver et l’ASCS/SCS est routée par l’intermédiaire d’un équilibreur de charge logiciel.</span><span class="sxs-lookup"><span data-stu-id="9953e-378">The communication between the SAP NetWeaver application server and the ASCS/SCS is routed through a software load balancer.</span></span> <span data-ttu-id="9953e-379">L’équilibreur de charge déconnecte les connexions inactives après un délai configurable.</span><span class="sxs-lookup"><span data-stu-id="9953e-379">The load balancer disconnects inactive connections after a configurable timeout.</span></span> <span data-ttu-id="9953e-380">Pour éviter ce problème, vous devez définir un paramètre dans le profil SAP NetWeaver ASCS/SCS et changer les paramètres système de Linux.</span><span class="sxs-lookup"><span data-stu-id="9953e-380">To prevent this you need to set a parameter in the SAP NetWeaver ASCS/SCS profile and change the Linux system settings.</span></span> <span data-ttu-id="9953e-381">Pour plus d’informations, consultez la [Note SAP 1410736][1410736].</span><span class="sxs-lookup"><span data-stu-id="9953e-381">Please read [SAP Note 1410736][1410736] for more information.</span></span>
   
   <span data-ttu-id="9953e-382">Le paramètre de profil ASCS/SCS enque/encni/set_so_keepalive a déjà été ajouté lors de la dernière étape.</span><span class="sxs-lookup"><span data-stu-id="9953e-382">The ASCS/SCS profile parameter enque/encni/set_so_keepalive was already added in the last step.</span></span>

   <pre><code> 
   # Change the Linux system configuration
   sudo sysctl net.ipv4.tcp_keepalive_time=120
   </code></pre>

1. <span data-ttu-id="9953e-383">**[A]** Configurer les utilisateurs SAP après l’installation</span><span class="sxs-lookup"><span data-stu-id="9953e-383">**[A]** Configure the SAP users after the installation</span></span>
 
   <pre><code>
   # Add sidadm to the haclient group
   sudo usermod -aG haclient <b>nws</b>adm   
   </code></pre>

1. <span data-ttu-id="9953e-384">**[1]** Ajouter les services ASCS et ERS SAP au fichier sapservice</span><span class="sxs-lookup"><span data-stu-id="9953e-384">**[1]** Add the ASCS and ERS SAP services to the sapservice file</span></span>

   <span data-ttu-id="9953e-385">Ajoutez l’entrée de service ASCS au deuxième nœud et copiez l’entrée de service ERS dans le premier nœud.</span><span class="sxs-lookup"><span data-stu-id="9953e-385">Add the ASCS service entry to the second node and copy the ERS service entry to the first node.</span></span>

   <pre><code>
   cat /usr/sap/sapservices | grep ASCS<b>00</b> | sudo ssh <b>nws-cl-1</b> "cat >>/usr/sap/sapservices"
   sudo ssh <b>nws-cl-1</b> "cat /usr/sap/sapservices" | grep ERS<b>02</b> | sudo tee -a /usr/sap/sapservices
   </code></pre>

1. <span data-ttu-id="9953e-386">**[1]** Créer les ressources de cluster SAP</span><span class="sxs-lookup"><span data-stu-id="9953e-386">**[1]** Create the SAP cluster resources</span></span>

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

   <span data-ttu-id="9953e-387">Vérifiez que l’état du cluster est OK et que toutes les ressources sont démarrées.</span><span class="sxs-lookup"><span data-stu-id="9953e-387">Make sure that the cluster status is ok and that all resources are started.</span></span> <span data-ttu-id="9953e-388">Le nœud sur lequel les ressources s’exécutent n’a aucune importance.</span><span class="sxs-lookup"><span data-stu-id="9953e-388">It is not important on which node the resources are running.</span></span>

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

### <a name="create-stonith-device"></a><span data-ttu-id="9953e-389">Créer l’appareil STONITH</span><span class="sxs-lookup"><span data-stu-id="9953e-389">Create STONITH device</span></span>

<span data-ttu-id="9953e-390">L’appareil STONITH utilise un principal de service pour l’autorisation sur Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="9953e-390">The STONITH device uses a Service Principal to authorize against Microsoft Azure.</span></span> <span data-ttu-id="9953e-391">Pour créer un principal de service, effectuez les étapes suivantes.</span><span class="sxs-lookup"><span data-stu-id="9953e-391">Follow these steps to create a Service Principal.</span></span>

1. <span data-ttu-id="9953e-392">Accédez à <https://portal.azure.com></span><span class="sxs-lookup"><span data-stu-id="9953e-392">Go to <https://portal.azure.com></span></span>
1. <span data-ttu-id="9953e-393">Ouvrez le panneau Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="9953e-393">Open the Azure Active Directory blade</span></span>  
   <span data-ttu-id="9953e-394">Accédez aux propriétés et notez l’ID de répertoire.</span><span class="sxs-lookup"><span data-stu-id="9953e-394">Go to Properties and write down the Directory Id.</span></span> <span data-ttu-id="9953e-395">Il s’agit de **l’ID client**.</span><span class="sxs-lookup"><span data-stu-id="9953e-395">This is the **tenant id**.</span></span>
1. <span data-ttu-id="9953e-396">Cliquez sur Inscriptions d’applications</span><span class="sxs-lookup"><span data-stu-id="9953e-396">Click App registrations</span></span>
1. <span data-ttu-id="9953e-397">Cliquez sur Ajouter.</span><span class="sxs-lookup"><span data-stu-id="9953e-397">Click Add</span></span>
1. <span data-ttu-id="9953e-398">Entrez un nom, sélectionnez le type d’application « Application web/API », entrez une URL de connexion (par exemple, http://localhost) et cliquez sur Créer</span><span class="sxs-lookup"><span data-stu-id="9953e-398">Enter a Name, select Application Type "Web app/API", enter a sign-on URL (for example http://localhost) and click Create</span></span>
1. <span data-ttu-id="9953e-399">L’URL de connexion n’est pas utilisée et peut être une URL valide</span><span class="sxs-lookup"><span data-stu-id="9953e-399">The sign-on URL is not used and can be any valid URL</span></span>
1. <span data-ttu-id="9953e-400">Sélectionnez la nouvelle application et cliquez sur Clés dans l’onglet Paramètres</span><span class="sxs-lookup"><span data-stu-id="9953e-400">Select the new App and click Keys in the Settings tab</span></span>
1. <span data-ttu-id="9953e-401">Entrez une description pour la nouvelle clé, sélectionnez « N’expire jamais » et cliquez sur Enregistrer</span><span class="sxs-lookup"><span data-stu-id="9953e-401">Enter a description for a new key, select "Never expires" and click Save</span></span>
1. <span data-ttu-id="9953e-402">Notez la valeur.</span><span class="sxs-lookup"><span data-stu-id="9953e-402">Write down the Value.</span></span> <span data-ttu-id="9953e-403">Cette valeur est utilisée comme **mot de passe** pour le principal de service</span><span class="sxs-lookup"><span data-stu-id="9953e-403">It is used as the **password** for the Service Principal</span></span>
1. <span data-ttu-id="9953e-404">Notez l’ID de l’application.</span><span class="sxs-lookup"><span data-stu-id="9953e-404">Write down the Application Id.</span></span> <span data-ttu-id="9953e-405">Cet identifiant est utilisé comme nom d’utilisateur (**ID de connexion** dans la procédure ci-dessous) du principal de service</span><span class="sxs-lookup"><span data-stu-id="9953e-405">It is used as the username (**login id** in the steps below) of the Service Principal</span></span>

<span data-ttu-id="9953e-406">Par défaut, le principal de service ne possède pas les autorisations d’accéder à vos ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="9953e-406">The Service Principal does not have permissions to access your Azure resources by default.</span></span> <span data-ttu-id="9953e-407">Vous devez accorder au principal de service les autorisations de démarrer et arrêter (libérer) toutes les machines virtuelles du cluster.</span><span class="sxs-lookup"><span data-stu-id="9953e-407">You need to give the Service Principal permissions to start and stop (deallocate) all virtual machines of the cluster.</span></span>

1. <span data-ttu-id="9953e-408">Accédez à https://portal.azure.com</span><span class="sxs-lookup"><span data-stu-id="9953e-408">Go to https://portal.azure.com</span></span>
1. <span data-ttu-id="9953e-409">Ouvrez le panneau Toutes les ressources</span><span class="sxs-lookup"><span data-stu-id="9953e-409">Open the All resources blade</span></span>
1. <span data-ttu-id="9953e-410">Sélectionnez la machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="9953e-410">Select the virtual machine</span></span>
1. <span data-ttu-id="9953e-411">Cliquez sur Contrôle d’accès (IAM)</span><span class="sxs-lookup"><span data-stu-id="9953e-411">Click Access control (IAM)</span></span>
1. <span data-ttu-id="9953e-412">Cliquez sur Ajouter.</span><span class="sxs-lookup"><span data-stu-id="9953e-412">Click Add</span></span>
1. <span data-ttu-id="9953e-413">Sélectionnez le rôle de propriétaire</span><span class="sxs-lookup"><span data-stu-id="9953e-413">Select the role Owner</span></span>
1. <span data-ttu-id="9953e-414">Entrez le nom de l’application que vous avez créée ci-dessus</span><span class="sxs-lookup"><span data-stu-id="9953e-414">Enter the name of the application you created above</span></span>
1. <span data-ttu-id="9953e-415">Cliquez sur OK</span><span class="sxs-lookup"><span data-stu-id="9953e-415">Click OK</span></span>

#### <a name="1-create-the-stonith-devices"></a><span data-ttu-id="9953e-416">**[1]**  Créer les appareils STONITH</span><span class="sxs-lookup"><span data-stu-id="9953e-416">**[1]** Create the STONITH devices</span></span>

<span data-ttu-id="9953e-417">Une fois que vous avez modifié les autorisations pour les machines virtuelles, vous pouvez configurer les appareils STONITH dans le cluster.</span><span class="sxs-lookup"><span data-stu-id="9953e-417">After you edited the permissions for the virtual machines, you can configure the STONITH devices in the cluster.</span></span>

<pre><code>
sudo crm configure

# replace the bold string with your subscription id, resource group, tenant id, service principal id and password

crm(live)configure# primitive rsc_st_azure_1 stonith:fence_azure_arm \
   params subscriptionId="<b>subscription id</b>" resourceGroup="<b>resource group</b>" tenantId="<b>tenant id</b>" login="<b>login id</b>" passwd="<b>password</b>"

crm(live)configure# primitive rsc_st_azure_2 stonith:fence_azure_arm \
   params subscriptionId="<b>subscription id</b>" resourceGroup="<b>resource group</b>" tenantId="<b>tenant id</b>" login="<b>login id</b>" passwd="<b>password</b>"

crm(live)configure# colocation col_st_azure -2000: rsc_st_azure_1:Started rsc_st_azure_2:Started

crm(live)configure# commit
crm(live)configure# exit
</code></pre>

#### <a name="1-enable-the-use-of-a-stonith-device"></a><span data-ttu-id="9953e-418">**[1]**  Activer l’utilisation d’un appareil STONITH</span><span class="sxs-lookup"><span data-stu-id="9953e-418">**[1]** Enable the use of a STONITH device</span></span>

<span data-ttu-id="9953e-419">Activer l’utilisation d’un appareil STONITH</span><span class="sxs-lookup"><span data-stu-id="9953e-419">Enable the use of a STONITH device</span></span>

<pre><code>
sudo crm configure property stonith-enabled=true 
</code></pre>

## <a name="install-database"></a><span data-ttu-id="9953e-420">Installer la base de données</span><span class="sxs-lookup"><span data-stu-id="9953e-420">Install database</span></span>

<span data-ttu-id="9953e-421">Dans cet exemple, une réplication du système SAP HANA est installée et configurée.</span><span class="sxs-lookup"><span data-stu-id="9953e-421">In this example an SAP HANA System Replication is installed and configured.</span></span> <span data-ttu-id="9953e-422">SAP HANA s’exécutera dans le même cluster que SAP NetWeaver ASCS/SCS et ERS.</span><span class="sxs-lookup"><span data-stu-id="9953e-422">SAP HANA will run in the same cluster as the SAP NetWeaver ASCS/SCS and ERS.</span></span> <span data-ttu-id="9953e-423">Vous pouvez également installer SAP HANA dans un cluster dédié.</span><span class="sxs-lookup"><span data-stu-id="9953e-423">You can also install SAP HANA on a dedicated cluster.</span></span> <span data-ttu-id="9953e-424">Consultez [Haute disponibilité de SAP HANA sur des machines virtuelles Azure][sap-hana-ha].</span><span class="sxs-lookup"><span data-stu-id="9953e-424">See [High Availability of SAP HANA on Azure Virtual Machines (VMs)][sap-hana-ha] for more information.</span></span>

### <a name="prepare-for-sap-hana-installation"></a><span data-ttu-id="9953e-425">Préparer l’installation de SAP HANA</span><span class="sxs-lookup"><span data-stu-id="9953e-425">Prepare for SAP HANA installation</span></span>

<span data-ttu-id="9953e-426">En général, nous recommandons d’utiliser LVM pour les volumes qui stockent des données et des fichiers journaux.</span><span class="sxs-lookup"><span data-stu-id="9953e-426">We generally recommend using LVM for volumes that store data and log files.</span></span> <span data-ttu-id="9953e-427">À des fins de test, vous pouvez également choisir de stocker les données et les fichiers journaux directement sur un disque simple.</span><span class="sxs-lookup"><span data-stu-id="9953e-427">For testing purposes, you can also choose to store the data and log file directly on a plain disk.</span></span>

1. <span data-ttu-id="9953e-428">**[A]** LVM</span><span class="sxs-lookup"><span data-stu-id="9953e-428">**[A]** LVM</span></span>  
   <span data-ttu-id="9953e-429">L’exemple ci-dessous part du principe que les machines virtuelles disposent de quatre disques de données qui doivent être utilisés pour créer deux volumes.</span><span class="sxs-lookup"><span data-stu-id="9953e-429">The example below assumes that the virtual machines have four data disks attached that should be used to create two volumes.</span></span>
   
   <span data-ttu-id="9953e-430">Créez des volumes physiques pour tous les disques que vous souhaitez utiliser.</span><span class="sxs-lookup"><span data-stu-id="9953e-430">Create physical volumes for all disks that you want to use.</span></span>
   
   <pre><code>
   sudo pvcreate /dev/sdd
   sudo pvcreate /dev/sde
   sudo pvcreate /dev/sdf
   sudo pvcreate /dev/sdg
   </code></pre>
   
   <span data-ttu-id="9953e-431">Créez un groupe de volumes pour les fichiers de données, un groupe de volumes pour les fichiers journaux et l’autre pour le répertoire partagé de SAP HANA</span><span class="sxs-lookup"><span data-stu-id="9953e-431">Create a volume group for the data files, one volume group for the log files and one for the shared directory of SAP HANA</span></span>
   
   <pre><code>
   sudo vgcreate vg_hana_data /dev/sdd /dev/sde
   sudo vgcreate vg_hana_log /dev/sdf
   sudo vgcreate vg_hana_shared /dev/sdg
   </code></pre>
   
   <span data-ttu-id="9953e-432">Créez les volumes logiques</span><span class="sxs-lookup"><span data-stu-id="9953e-432">Create the logical volumes</span></span>
   
   <pre><code>
   sudo lvcreate -l 100%FREE -n hana_data vg_hana_data
   sudo lvcreate -l 100%FREE -n hana_log vg_hana_log
   sudo lvcreate -l 100%FREE -n hana_shared vg_hana_shared
   sudo mkfs.xfs /dev/vg_hana_data/hana_data
   sudo mkfs.xfs /dev/vg_hana_log/hana_log
   sudo mkfs.xfs /dev/vg_hana_shared/hana_shared
   </code></pre>
   
   <span data-ttu-id="9953e-433">Créez les répertoires de montage et copiez l’UUID de tous les volumes logiques</span><span class="sxs-lookup"><span data-stu-id="9953e-433">Create the mount directories and copy the UUID of all logical volumes</span></span>
   
   <pre><code>
   sudo mkdir -p /hana/data
   sudo mkdir -p /hana/log
   sudo mkdir -p /hana/shared
   sudo chattr +i /hana/data
   sudo chattr +i /hana/log
   sudo chattr +i /hana/shared
   # write down the id of /dev/vg_hana_data/hana_data, /dev/vg_hana_log/hana_log and /dev/vg_hana_shared/hana_shared
   sudo blkid
   </code></pre>
   
   <span data-ttu-id="9953e-434">Créez des entrées autofs pour les trois volumes logiques</span><span class="sxs-lookup"><span data-stu-id="9953e-434">Create autofs entries for the three logical volumes</span></span>
   
   <pre><code>
   sudo vi /etc/auto.direct
   </code></pre>
   
   <span data-ttu-id="9953e-435">Insérez cette ligne dans sudo vi /etc/auto.direct</span><span class="sxs-lookup"><span data-stu-id="9953e-435">Insert this line to sudo vi /etc/auto.direct</span></span>
   
   <pre><code>
   /hana/data -fstype=xfs :UUID=<b>&lt;UUID of /dev/vg_hana_data/hana_data&gt;</b>
   /hana/log -fstype=xfs :UUID=<b>&lt;UUID of /dev/vg_hana_log/hana_log&gt;</b>
   /hana/shared -fstype=xfs :UUID=<b>&lt;UUID of /dev/vg_hana_shared/hana_shared&gt;</b>
   </code></pre>
   
   <span data-ttu-id="9953e-436">Montez les nouveaux volumes</span><span class="sxs-lookup"><span data-stu-id="9953e-436">Mount the new volumes</span></span>
   
   <pre><code>
   sudo service autofs restart 
   </code></pre>

1. <span data-ttu-id="9953e-437">**[A]** Disques simples</span><span class="sxs-lookup"><span data-stu-id="9953e-437">**[A]** Plain Disks</span></span>  

   <span data-ttu-id="9953e-438">Pour les petits systèmes ou les systèmes de démonstration, vous pouvez placer vos données et fichiers journaux HANA sur un disque.</span><span class="sxs-lookup"><span data-stu-id="9953e-438">For small or demo systems, you can place your HANA data and log files on one disk.</span></span> <span data-ttu-id="9953e-439">Les commandes suivantes permettent de créer une partition au format xfs sur /dev/sdc.</span><span class="sxs-lookup"><span data-stu-id="9953e-439">The following commands create a partition on /dev/sdc and format it with xfs.</span></span>
   ```bash
   sudo sh -c 'echo -e "n\n\n\n\n\nw\n" | fdisk /dev/sdd'
   sudo mkfs.xfs /dev/sdd1
   
   # write down the id of /dev/sdd1
   sudo /sbin/blkid
   sudo vi /etc/auto.direct
   ```
   
   <span data-ttu-id="9953e-440">Insérez cette ligne dans /etc/auto.direct</span><span class="sxs-lookup"><span data-stu-id="9953e-440">Insert this line to /etc/auto.direct</span></span>
   <pre><code>
   /hana -fstype=xfs :UUID=<b>&lt;UUID&gt;</b>
   </code></pre>
   
   <span data-ttu-id="9953e-441">Créez le répertoire cible et montez le disque.</span><span class="sxs-lookup"><span data-stu-id="9953e-441">Create the target directory and mount the disk.</span></span>
   
   <pre><code>
   sudo mkdir /hana
   sudo chattr +i /hana
   sudo service autofs restart
   </code></pre>

### <a name="installing-sap-hana"></a><span data-ttu-id="9953e-442">Installation de SAP HANA</span><span class="sxs-lookup"><span data-stu-id="9953e-442">Installing SAP HANA</span></span>

<span data-ttu-id="9953e-443">Les étapes suivantes se basent sur le chapitre 4 de la publication [SAP HANA SR Performance Optimized Scenario][suse-hana-ha-guide] (Scénario d’optimisation des performances de réplication système de SAP HANA) pour installer la réplication système SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="9953e-443">The following steps are based on chapter 4 of the [SAP HANA SR Performance Optimized Scenario guide][suse-hana-ha-guide] to install SAP HANA System Replication.</span></span> <span data-ttu-id="9953e-444">Veuillez lire ce document avant de poursuivre l’installation.</span><span class="sxs-lookup"><span data-stu-id="9953e-444">Please read it before you continue the installation.</span></span>

1. <span data-ttu-id="9953e-445">**[A]** Exécuter hdblcm à partir du DVD HANA</span><span class="sxs-lookup"><span data-stu-id="9953e-445">**[A]** Run hdblcm from the HANA DVD</span></span>
   
   <pre><code>
   sudo hdblcm --sid=<b>HDB</b> --number=<b>03</b> --action=install --batch --password=<b>&lt;password&gt;</b> --system_user_password=<b>&lt;password for system user&gt;</b>

   sudo /hana/shared/<b>HDB</b>/hdblcm/hdblcm --action=configure_internal_network --listen_interface=internal --internal_network=<b>10.0.0/24</b> --password=<b>&lt;password for system user&gt;</b> --batch
   </code></pre>

1. <span data-ttu-id="9953e-446">**[A]** Mettre à niveau l’agent hôte SAP</span><span class="sxs-lookup"><span data-stu-id="9953e-446">**[A]** Upgrade SAP Host Agent</span></span>

   <span data-ttu-id="9953e-447">Téléchargez la dernière archive de l’agent hôte SAP à partir du [SAP Softwarecenter][sap-swcenter] et exécutez la commande suivante pour mettre à niveau l’agent.</span><span class="sxs-lookup"><span data-stu-id="9953e-447">Download the latest SAP Host Agent archive from the [SAP Softwarecenter][sap-swcenter] and run the following command to upgrade the agent.</span></span> <span data-ttu-id="9953e-448">Remplacez le chemin d’accès à l’archive pour pointer vers le fichier que vous avez téléchargé.</span><span class="sxs-lookup"><span data-stu-id="9953e-448">Replace the path to the archive to point to the file you downloaded.</span></span>
   <pre><code>
   sudo /usr/sap/hostctrl/exe/saphostexec -upgrade -archive <b>&lt;path to SAP Host Agent SAR&gt;</b> 
   </code></pre>

1. <span data-ttu-id="9953e-449">**[1]** Créer la réplication HANA (en tant que racine)</span><span class="sxs-lookup"><span data-stu-id="9953e-449">**[1]** Create HANA replication (as root)</span></span>  

   <span data-ttu-id="9953e-450">Exécutez la commande ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="9953e-450">Run the following command.</span></span> <span data-ttu-id="9953e-451">Veillez à remplacer les chaînes en gras (ID du système HANA HDB et numéro d’instance 03) par les valeurs de votre installation SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="9953e-451">Make sure to replace bold strings (HANA System ID HDB and instance number 03) with the values of your SAP HANA installation.</span></span>
   <pre><code>
   PATH="$PATH:/usr/sap/<b>HDB</b>/HDB<b>03</b>/exe"
   hdbsql -u system -i <b>03</b> 'CREATE USER <b>hdb</b>hasync PASSWORD "<b>passwd</b>"' 
   hdbsql -u system -i <b>03</b> 'GRANT DATA ADMIN TO <b>hdb</b>hasync' 
   hdbsql -u system -i <b>03</b> 'ALTER USER <b>hdb</b>hasync DISABLE PASSWORD LIFETIME' 
   </code></pre>

1. <span data-ttu-id="9953e-452">**[A]** Créer l’entrée keystore (en tant que racine)</span><span class="sxs-lookup"><span data-stu-id="9953e-452">**[A]** Create keystore entry (as root)</span></span>

   <pre><code>
   PATH="$PATH:/usr/sap/<b>HDB</b>/HDB<b>03</b>/exe"
   hdbuserstore SET <b>hdb</b>haloc localhost:3<b>03</b>15 <b>hdb</b>hasync <b>&lt;passwd&gt;</b>
   </code></pre>

1. <span data-ttu-id="9953e-453">**[1]** Sauvegarder la base de données (en tant que racine)</span><span class="sxs-lookup"><span data-stu-id="9953e-453">**[1]** Backup database (as root)</span></span>

   <pre><code>
   PATH="$PATH:/usr/sap/<b>HDB</b>/HDB<b>03</b>/exe"
   hdbsql -u system -i <b>03</b> "BACKUP DATA USING FILE ('<b>initialbackup</b>')" 
   </code></pre>

1. <span data-ttu-id="9953e-454">**[1]** Basculer vers l’utilisateur sapsid HANA et créer le site principal.</span><span class="sxs-lookup"><span data-stu-id="9953e-454">**[1]** Switch to the HANA sapsid user and create the primary site.</span></span>

   <pre><code>
   su - <b>hdb</b>adm
   hdbnsutil -sr_enable –-name=<b>SITE1</b>
   </code></pre>

1. <span data-ttu-id="9953e-455">**[2]** Basculer vers l’utilisateur sapsid HANA et créer le site secondaire.</span><span class="sxs-lookup"><span data-stu-id="9953e-455">**[2]** Switch to the HANA sapsid user and create the secondary site.</span></span>

   <pre><code>
   su - <b>hdb</b>adm
   sapcontrol -nr <b>03</b> -function StopWait 600 10
   hdbnsutil -sr_register --remoteHost=<b>nws-cl-0</b> --remoteInstance=<b>03</b> --replicationMode=sync --name=<b>SITE2</b> 
   </code></pre>

1. <span data-ttu-id="9953e-456">**[1]** Créer les ressources de cluster SAP HANA</span><span class="sxs-lookup"><span data-stu-id="9953e-456">**[1]** Create SAP HANA cluster resources</span></span>

   <span data-ttu-id="9953e-457">Tout d’abord, créez la topologie.</span><span class="sxs-lookup"><span data-stu-id="9953e-457">First, create the topology.</span></span>
   
   <pre><code>
   sudo crm configure

   # replace the bold string with your instance number and HANA system id
   
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
   
   <span data-ttu-id="9953e-458">Ensuite, créez les ressources HANA.</span><span class="sxs-lookup"><span data-stu-id="9953e-458">Next, create the HANA resources</span></span>
   
   <pre><code>
   sudo crm configure

   # replace the bold string with your instance number, HANA system id and the frontend IP address of the Azure load balancer. 
    
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

   <span data-ttu-id="9953e-459">Vérifiez que l’état du cluster est OK et que toutes les ressources sont démarrées.</span><span class="sxs-lookup"><span data-stu-id="9953e-459">Make sure that the cluster status is ok and that all resources are started.</span></span> <span data-ttu-id="9953e-460">Le nœud sur lequel les ressources s’exécutent n’a aucune importance.</span><span class="sxs-lookup"><span data-stu-id="9953e-460">It is not important on which node the resources are running.</span></span>

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

1. <span data-ttu-id="9953e-461">**[1]** Installer l’instance de base de données SAP NetWeaver</span><span class="sxs-lookup"><span data-stu-id="9953e-461">**[1]** Install the SAP NetWeaver database instance</span></span>

   <span data-ttu-id="9953e-462">Installez l’instance de base de données SAP NetWeaver en tant que racine à l’aide d’un nom d’hôte virtuel mappé à l’adresse IP de la configuration frontend d’équilibreur de charge pour la base de données, par exemple <b>nws-db</b> et <b>10.0.0.12</b>.</span><span class="sxs-lookup"><span data-stu-id="9953e-462">Install the SAP NetWeaver database instance as root using a virtual hostname that maps to the IP address of the load balancer frontend configuration for the database for example <b>nws-db</b> and <b>10.0.0.12</b>.</span></span>

   <span data-ttu-id="9953e-463">Vous pouvez utiliser le paramètre sapinst SAPINST_REMOTE_ACCESS_USER pour autoriser un utilisateur non racine à se connecter à sapinst.</span><span class="sxs-lookup"><span data-stu-id="9953e-463">You can use the sapinst parameter SAPINST_REMOTE_ACCESS_USER to allow a non-root user to connect to sapinst.</span></span>

   <pre><code>
   sudo &lt;swpm&gt;/sapinst SAPINST_REMOTE_ACCESS_USER=<b>sapadmin</b>
   </code></pre>

## <a name="sap-netweaver-application-server-installation"></a><span data-ttu-id="9953e-464">Installation de serveur d’applications SAP NetWeaver</span><span class="sxs-lookup"><span data-stu-id="9953e-464">SAP NetWeaver application server installation</span></span>

<span data-ttu-id="9953e-465">Suivez ces étapes pour installer un serveur d’applications SAP.</span><span class="sxs-lookup"><span data-stu-id="9953e-465">Follow these steps to install an SAP application server.</span></span> <span data-ttu-id="9953e-466">Les étapes ci-dessous partent du principe que vous installez le serveur d’applications sur un serveur différent des serveurs ASCS/SCS et HANA.</span><span class="sxs-lookup"><span data-stu-id="9953e-466">The steps bellow assume that you install the application server on a server different from the ASCS/SCS and HANA servers.</span></span> <span data-ttu-id="9953e-467">Dans le cas contraire, certaines des étapes ci-dessous (par exemple la configuration de la résolution de nom d’hôte) ne sont pas nécessaires.</span><span class="sxs-lookup"><span data-stu-id="9953e-467">Otherwise some of the steps below (like configuring host name resolution) are not needed.</span></span>

1. <span data-ttu-id="9953e-468">Configurer la résolution de nom d’hôte</span><span class="sxs-lookup"><span data-stu-id="9953e-468">Setup host name resolution</span></span>    
   <span data-ttu-id="9953e-469">Vous pouvez utiliser un serveur DNS ou modifier le fichier /etc/hosts sur tous les nœuds.</span><span class="sxs-lookup"><span data-stu-id="9953e-469">You can either use a DNS server or modify the /etc/hosts on all nodes.</span></span> <span data-ttu-id="9953e-470">Cet exemple montre comment utiliser le fichier /etc/hosts.</span><span class="sxs-lookup"><span data-stu-id="9953e-470">This example shows how to use the /etc/hosts file.</span></span>
   <span data-ttu-id="9953e-471">Remplacez l’adresse IP et le nom d’hôte dans les commandes suivantes</span><span class="sxs-lookup"><span data-stu-id="9953e-471">Replace the IP address and the hostname in the following commands</span></span>
   ```bash
   sudo vi /etc/hosts
   ```
   <span data-ttu-id="9953e-472">Insérez les lignes suivantes dans le fichier /etc/hosts.</span><span class="sxs-lookup"><span data-stu-id="9953e-472">Insert the following lines to /etc/hosts.</span></span> <span data-ttu-id="9953e-473">Modifiez l’adresse IP et le nom d’hôte en fonction de votre environnement</span><span class="sxs-lookup"><span data-stu-id="9953e-473">Change the IP address and hostname to match your environment</span></span>    
    
   <pre><code>
   # IP address of the load balancer frontend configuration for NFS
   <b>10.0.0.4 nws-nfs</b>
   # IP address of the load balancer frontend configuration for SAP NetWeaver ASCS/SCS
   <b>10.0.0.10 nws-ascs</b>
   # IP address of the load balancer frontend configuration for SAP NetWeaver ERS
   <b>10.0.0.11 nws-ers</b>
   # IP address of the load balancer frontend configuration for database
   <b>10.0.0.12 nws-db</b>
   # IP address of the application server
   <b>10.0.0.8 nws-di-0</b>
   </code></pre>

1. <span data-ttu-id="9953e-474">Créer le répertoire sapmnt</span><span class="sxs-lookup"><span data-stu-id="9953e-474">Create the sapmnt directory</span></span>

   <pre><code>
   sudo mkdir -p /sapmnt/<b>NWS</b>
   sudo mkdir -p /usr/sap/trans

   sudo chattr +i /sapmnt/<b>NWS</b>
   sudo chattr +i /usr/sap/trans
   </code></pre>

1. <span data-ttu-id="9953e-475">Configurer autofs</span><span class="sxs-lookup"><span data-stu-id="9953e-475">Configure autofs</span></span>
 
   <pre><code>
   sudo vi /etc/auto.master

   # Add the following line to the file, save and exit
   +auto.master
   /- /etc/auto.direct
   </code></pre>

   <span data-ttu-id="9953e-476">Créer un fichier avec</span><span class="sxs-lookup"><span data-stu-id="9953e-476">Create a new file with</span></span>

   <pre><code>
   sudo vi /etc/auto.direct

   # Add the following lines to the file, save and exit
   /sapmnt/<b>NWS</b> -nfsvers=4,nosymlink,sync <b>nws-nfs</b>:/sapmntsid
   /usr/sap/trans -nfsvers=4,nosymlink,sync <b>nws-nfs</b>:/trans
   </code></pre>

   <span data-ttu-id="9953e-477">Redémarrer autofs pour monter les nouveaux partages</span><span class="sxs-lookup"><span data-stu-id="9953e-477">Restart autofs to mount the new shares</span></span>

   <pre><code>
   sudo systemctl enable autofs
   sudo service autofs restart
   </code></pre>

1. <span data-ttu-id="9953e-478">Configurer le fichier SWAP</span><span class="sxs-lookup"><span data-stu-id="9953e-478">Configure SWAP file</span></span>
 
   <pre><code>
   sudo vi /etc/waagent.conf

   # Set the property ResourceDisk.EnableSwap to y
   # Create and use swapfile on resource disk.
   ResourceDisk.EnableSwap=<b>y</b>

   # Set the size of the SWAP file with property ResourceDisk.SwapSizeMB
   # The free space of resource disk varies by virtual machine size. Make sure that you do not set a value that is too big. You can check the SWAP space with command swapon
   # Size of the swapfile.
   ResourceDisk.SwapSizeMB=<b>2000</b>
   </code></pre>

   <span data-ttu-id="9953e-479">Redémarrer l’Agent pour activer la modification</span><span class="sxs-lookup"><span data-stu-id="9953e-479">Restart the Agent to activate the change</span></span>

   <pre><code>
   sudo service waagent restart
   </code></pre>

1. <span data-ttu-id="9953e-480">Installer le serveur d’applications SAP NetWeaver</span><span class="sxs-lookup"><span data-stu-id="9953e-480">Install SAP NetWeaver application server</span></span>

   <span data-ttu-id="9953e-481">Installer un serveur d’applications SAP NetWeaver principal ou supplémentaire.</span><span class="sxs-lookup"><span data-stu-id="9953e-481">Install a primary or additional SAP NetWeaver applications server.</span></span>

   <span data-ttu-id="9953e-482">Vous pouvez utiliser le paramètre sapinst SAPINST_REMOTE_ACCESS_USER pour autoriser un utilisateur non racine à se connecter à sapinst.</span><span class="sxs-lookup"><span data-stu-id="9953e-482">You can use the sapinst parameter SAPINST_REMOTE_ACCESS_USER to allow a non-root user to connect to sapinst.</span></span>

   <pre><code>
   sudo &lt;swpm&gt;/sapinst SAPINST_REMOTE_ACCESS_USER=<b>sapadmin</b>
   </code></pre>

1. <span data-ttu-id="9953e-483">Mettre à jour la banque d’informations sécurisée SAP HANA</span><span class="sxs-lookup"><span data-stu-id="9953e-483">Update SAP HANA secure store</span></span>

   <span data-ttu-id="9953e-484">Mettez à jour la banque d’informations sécurisée SAP HANA pour qu’elle pointe vers le nom virtuel de la configuration de la réplication système SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="9953e-484">Update the SAP HANA secure store to point to the virtual name of the SAP HANA System Replication setup.</span></span>
   <pre><code>
   su - <b>nws</b>adm
   hdbuserstore SET DEFAULT <b>nws-db</b>:3<b>03</b>15 <b>SAPABAP1</b> <b>&lt;password of ABAP schema&gt;</b>
   </code></pre>

## <a name="next-steps"></a><span data-ttu-id="9953e-485">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="9953e-485">Next steps</span></span>
* <span data-ttu-id="9953e-486">[Planification et implémentation de machines virtuelles Azure pour SAP][planning-guide]</span><span class="sxs-lookup"><span data-stu-id="9953e-486">[Azure Virtual Machines planning and implementation for SAP][planning-guide]</span></span>
* <span data-ttu-id="9953e-487">[Déploiement de machines virtuelles Azure pour SAP][deployment-guide]</span><span class="sxs-lookup"><span data-stu-id="9953e-487">[Azure Virtual Machines deployment for SAP][deployment-guide]</span></span>
* <span data-ttu-id="9953e-488">[Déploiement SGBD de machines virtuelles Azure pour SAP][dbms-guide]</span><span class="sxs-lookup"><span data-stu-id="9953e-488">[Azure Virtual Machines DBMS deployment for SAP][dbms-guide]</span></span>
* <span data-ttu-id="9953e-489">Pour savoir comment établir une haute disponibilité et planifier la récupération d’urgence de SAP HANA sur Azure (grandes instances), consultez [Haute disponibilité et récupération d’urgence de SAP HANA (grandes instances) sur Azure](hana-overview-high-availability-disaster-recovery.md).</span><span class="sxs-lookup"><span data-stu-id="9953e-489">To learn how to establish high availability and plan for disaster recovery of SAP HANA on Azure (large instances), see [SAP HANA (large instances) high availability and disaster recovery on Azure](hana-overview-high-availability-disaster-recovery.md).</span></span>
* <span data-ttu-id="9953e-490">Pour savoir comment établir une haute disponibilité et planifier la récupération d’urgence de SAP HANA sur des machines virtuelles Azure, consultez [Haute disponibilité de SAP HANA sur des machines virtuelles Azure][sap-hana-ha].</span><span class="sxs-lookup"><span data-stu-id="9953e-490">To learn how to establish high availability and plan for disaster recovery of SAP HANA on Azure VMs, see [High Availability of SAP HANA on Azure Virtual Machines (VMs)][sap-hana-ha]</span></span>