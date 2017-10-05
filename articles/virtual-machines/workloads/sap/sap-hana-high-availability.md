---
title: "Haute disponibilité de SAP HANA sur les machines virtuelles Azure | Microsoft Docs"
description: "Créer une haute disponibilité de SAP HANA sur des machines virtuelles Azure."
services: virtual-machines-linux
documentationcenter: 
author: MSSedusch
manager: timlt
editor: 
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 04/25/2017
ms.author: sedusch
ms.openlocfilehash: 951150e621d21037b0adde7287b9f985290d8d11
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="high-availability-of-sap-hana-on-azure-virtual-machines-vms"></a><span data-ttu-id="7a005-103">Haute disponibilité de SAP HANA sur des machines virtuelles Azure</span><span class="sxs-lookup"><span data-stu-id="7a005-103">High Availability of SAP HANA on Azure Virtual Machines (VMs)</span></span>

[dbms-guide]:dbms-guide.md
[deployment-guide]:deployment-guide.md
[planning-guide]:planning-guide.md

<span data-ttu-id="7a005-104">[2205917]:https://launchpad.support.sap.com/#/notes/2205917</span><span class="sxs-lookup"><span data-stu-id="7a005-104">[2205917]:https://launchpad.support.sap.com/#/notes/2205917</span></span>
<span data-ttu-id="7a005-105">[1944799]:https://launchpad.support.sap.com/#/notes/1944799</span><span class="sxs-lookup"><span data-stu-id="7a005-105">[1944799]:https://launchpad.support.sap.com/#/notes/1944799</span></span>
<span data-ttu-id="7a005-106">[1928533]:https://launchpad.support.sap.com/#/notes/1928533</span><span class="sxs-lookup"><span data-stu-id="7a005-106">[1928533]:https://launchpad.support.sap.com/#/notes/1928533</span></span>
<span data-ttu-id="7a005-107">[2015553]:https://launchpad.support.sap.com/#/notes/2015553</span><span class="sxs-lookup"><span data-stu-id="7a005-107">[2015553]:https://launchpad.support.sap.com/#/notes/2015553</span></span>
<span data-ttu-id="7a005-108">[2178632]:https://launchpad.support.sap.com/#/notes/2178632</span><span class="sxs-lookup"><span data-stu-id="7a005-108">[2178632]:https://launchpad.support.sap.com/#/notes/2178632</span></span>
<span data-ttu-id="7a005-109">[2191498]:https://launchpad.support.sap.com/#/notes/2191498</span><span class="sxs-lookup"><span data-stu-id="7a005-109">[2191498]:https://launchpad.support.sap.com/#/notes/2191498</span></span>
<span data-ttu-id="7a005-110">[2243692]:https://launchpad.support.sap.com/#/notes/2243692</span><span class="sxs-lookup"><span data-stu-id="7a005-110">[2243692]:https://launchpad.support.sap.com/#/notes/2243692</span></span>
<span data-ttu-id="7a005-111">[1984787]:https://launchpad.support.sap.com/#/notes/1984787</span><span class="sxs-lookup"><span data-stu-id="7a005-111">[1984787]:https://launchpad.support.sap.com/#/notes/1984787</span></span>
<span data-ttu-id="7a005-112">[1999351]:https://launchpad.support.sap.com/#/notes/1999351</span><span class="sxs-lookup"><span data-stu-id="7a005-112">[1999351]:https://launchpad.support.sap.com/#/notes/1999351</span></span>

[hana-ha-guide-replication]:sap-hana-high-availability.md#14c19f65-b5aa-4856-9594-b81c7e4df73d
[hana-ha-guide-shared-storage]:sap-hana-high-availability.md#498de331-fa04-490b-997c-b078de457c9d

[suse-hana-ha-guide]:https://www.suse.com/docrep/documents/ir8w88iwu7/suse_linux_enterprise_server_for_sap_applications_12_sp1.pdf
[sap-swcenter]:https://launchpad.support.sap.com/#/softwarecenter
[template-multisid-db]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image-multi-sid-db%2Fazuredeploy.json
[template-converged]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image-converged%2Fazuredeploy.json

<span data-ttu-id="7a005-113">En local, vous pouvez utiliser soit la réplication système HANA soit un stockage partagé pour établir une haute disponibilité pour SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="7a005-113">On-premises, you can use either HANA System Replication or use shared storage to establish high availability for SAP HANA.</span></span>
<span data-ttu-id="7a005-114">Azure ne prend en charge actuellement que la configuration de la réplication système HANA.</span><span class="sxs-lookup"><span data-stu-id="7a005-114">We currently only support setting up HANA System Replication on Azure.</span></span> <span data-ttu-id="7a005-115">La réplication SAP HANA se compose d’un nœud principal et d’au moins un nœud subordonné.</span><span class="sxs-lookup"><span data-stu-id="7a005-115">SAP HANA Replication consists of one master node and at least one slave node.</span></span> <span data-ttu-id="7a005-116">Les modifications apportées aux données sur le nœud principal sont répliquées vers les nœuds subordonnés de manière synchrone ou asynchrone.</span><span class="sxs-lookup"><span data-stu-id="7a005-116">Changes to the data on the master node are replicated to the slave nodes synchronously or asynchronously.</span></span>

<span data-ttu-id="7a005-117">Cet article décrit comment déployer et configurer les machines virtuelles, installer l’infrastructure de cluster, et installer et configurer la réplication système SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="7a005-117">This article describes how to deploy the virtual machines, configure the virtual machines, install the cluster framework, install and configure SAP HANA System Replication.</span></span>
<span data-ttu-id="7a005-118">Les exemples de configuration et les commandes d’installation utilisent le numéro d’instance 03 et l’ID système HANA HDB.</span><span class="sxs-lookup"><span data-stu-id="7a005-118">In the example configurations, installation commands etc. instance number 03 and HANA System ID HDB is used.</span></span>

<span data-ttu-id="7a005-119">Commencez par lire les notes et publications SAP suivantes</span><span class="sxs-lookup"><span data-stu-id="7a005-119">Read the following SAP Notes and papers first</span></span>

* <span data-ttu-id="7a005-120">Note SAP [1928533], qui contient :</span><span class="sxs-lookup"><span data-stu-id="7a005-120">SAP Note [1928533], which has:</span></span>
  * <span data-ttu-id="7a005-121">une liste des tailles de machines virtuelles Azure prises en charge pour le déploiement de logiciels SAP</span><span class="sxs-lookup"><span data-stu-id="7a005-121">List of Azure VM sizes that are supported for the deployment of SAP software</span></span>
  * <span data-ttu-id="7a005-122">des informations importantes sur la capacité en fonction de la taille des machines virtuelles Azure</span><span class="sxs-lookup"><span data-stu-id="7a005-122">Important capacity information for Azure VM sizes</span></span>
  * <span data-ttu-id="7a005-123">les logiciels SAP pris en charge et les combinaisons entre système d’exploitation et base de données</span><span class="sxs-lookup"><span data-stu-id="7a005-123">Supported SAP software, and operating system (OS) and database combinations</span></span>
  * <span data-ttu-id="7a005-124">la version du noyau SAP requise pour Windows et Linux sur Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="7a005-124">Required SAP kernel version for Windows and Linux on Microsoft Azure</span></span>
* <span data-ttu-id="7a005-125">La note SAP [2015553] répertorie les conditions préalables au déploiement de logiciels SAP pris en charge par SAP sur Azure.</span><span class="sxs-lookup"><span data-stu-id="7a005-125">SAP Note [2015553] lists prerequisites for SAP-supported SAP software deployments in Azure.</span></span>
* <span data-ttu-id="7a005-126">La note SAP [2205917] contient des paramètres de système d’exploitation recommandés pour SUSE Linux Enterprise Server pour les applications SAP</span><span class="sxs-lookup"><span data-stu-id="7a005-126">SAP Note [2205917] has recommended OS settings for SUSE Linux Enterprise Server for SAP Applications</span></span>
* <span data-ttu-id="7a005-127">La note SAP [1944799] contient des instructions SAP HANA pour SUSE Linux Enterprise Server pour les applications SAP</span><span class="sxs-lookup"><span data-stu-id="7a005-127">SAP Note [1944799] has SAP HANA Guidelines for SUSE Linux Enterprise Server for SAP Applications</span></span>
* <span data-ttu-id="7a005-128">La note SAP [2178632] contient des informations détaillées sur toutes les métriques de surveillance rapportées pour SAP sur Azure.</span><span class="sxs-lookup"><span data-stu-id="7a005-128">SAP Note [2178632] has detailed information about all monitoring metrics reported for SAP in Azure.</span></span>
* <span data-ttu-id="7a005-129">La note SAP [2191498] contient la version requise de l’agent hôte SAP pour Linux sur Azure.</span><span class="sxs-lookup"><span data-stu-id="7a005-129">SAP Note [2191498] has the required SAP Host Agent version for Linux in Azure.</span></span>
* <span data-ttu-id="7a005-130">La note SAP [2243692] contient des informations sur les licences SAP sur Linux dans Azure.</span><span class="sxs-lookup"><span data-stu-id="7a005-130">SAP Note [2243692] has information about SAP licensing on Linux in Azure.</span></span>
* <span data-ttu-id="7a005-131">La note SAP [1984787] contient des informations sur SUSE Linux Enterprise Server 12.</span><span class="sxs-lookup"><span data-stu-id="7a005-131">SAP Note [1984787] has general information about SUSE Linux Enterprise Server 12.</span></span>
* <span data-ttu-id="7a005-132">La note SAP [1999351] contient des informations de dépannage supplémentaires pour l’extension d’analyse Azure améliorée pour SAP.</span><span class="sxs-lookup"><span data-stu-id="7a005-132">SAP Note [1999351] has additional troubleshooting information for the Azure Enhanced Monitoring Extension for SAP.</span></span>
* <span data-ttu-id="7a005-133">Le [WIKI de la communauté SAP](https://wiki.scn.sap.com/wiki/display/HOME/SAPonLinuxNotes) contient toutes les notes SAP requises pour Linux.</span><span class="sxs-lookup"><span data-stu-id="7a005-133">[SAP Community WIKI](https://wiki.scn.sap.com/wiki/display/HOME/SAPonLinuxNotes) has all required SAP Notes for Linux.</span></span>
* <span data-ttu-id="7a005-134">[Planification et implémentation de Machines virtuelles Azure pour SAP sur Linux][planning-guide]</span><span class="sxs-lookup"><span data-stu-id="7a005-134">[Azure Virtual Machines planning and implementation for SAP on Linux][planning-guide]</span></span>
* <span data-ttu-id="7a005-135">[Déploiement de Machines virtuelles Azure pour SAP sur Linux (cet article)][deployment-guide]</span><span class="sxs-lookup"><span data-stu-id="7a005-135">[Azure Virtual Machines deployment for SAP on Linux (this article)][deployment-guide]</span></span>
* <span data-ttu-id="7a005-136">[Déploiement SGBD de Machines virtuelles Azure pour SAP sur Linux][dbms-guide]</span><span class="sxs-lookup"><span data-stu-id="7a005-136">[Azure Virtual Machines DBMS deployment for SAP on Linux][dbms-guide]</span></span>
* <span data-ttu-id="7a005-137">[Scénario d’optimisation des performances de réplication système de SAP HANA][suse-hana-ha-guide] Le guide contient toutes les informations nécessaires pour configurer la réplication système SAP HANA locale.</span><span class="sxs-lookup"><span data-stu-id="7a005-137">[SAP HANA SR Performance Optimized Scenario][suse-hana-ha-guide] The guide contains all required information to set up SAP HANA System Replication on-premises.</span></span> <span data-ttu-id="7a005-138">Utilisez ce guide comme référence.</span><span class="sxs-lookup"><span data-stu-id="7a005-138">Use this guide as a baseline.</span></span>

## <a name="deploying-linux"></a><span data-ttu-id="7a005-139">Déploiement de Linux</span><span class="sxs-lookup"><span data-stu-id="7a005-139">Deploying Linux</span></span>

<span data-ttu-id="7a005-140">L’agent de ressource pour SAP HANA est inclus dans SUSE Linux Enterprise Server for SAP Applications.</span><span class="sxs-lookup"><span data-stu-id="7a005-140">The resource agent for SAP HANA is included in SUSE Linux Enterprise Server for SAP Applications.</span></span>
<span data-ttu-id="7a005-141">La Place de marché Azure contient une image de SUSE Linux Enterprise Server for SAP Applications 12 avec BYOS (Bring Your Own Subscription), que vous pouvez utiliser pour déployer de nouvelles machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="7a005-141">The Azure Marketplace contains an image for SUSE Linux Enterprise Server for SAP Applications 12 with BYOS (Bring Your Own Subscription) that you can use to deploy new virtual machines.</span></span>

### <a name="manual-deployment"></a><span data-ttu-id="7a005-142">Déploiement manuel</span><span class="sxs-lookup"><span data-stu-id="7a005-142">Manual Deployment</span></span>

1. <span data-ttu-id="7a005-143">Création d’un groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="7a005-143">Create a Resource Group</span></span>
1. <span data-ttu-id="7a005-144">Création d'un réseau virtuel</span><span class="sxs-lookup"><span data-stu-id="7a005-144">Create a Virtual Network</span></span>
1. <span data-ttu-id="7a005-145">Créer deux comptes de stockage</span><span class="sxs-lookup"><span data-stu-id="7a005-145">Create two Storage Accounts</span></span>
1. <span data-ttu-id="7a005-146">Créer un groupe à haute disponibilité</span><span class="sxs-lookup"><span data-stu-id="7a005-146">Create an Availability Set</span></span>  
   <span data-ttu-id="7a005-147">Définir un domaine de mise à jour maximal</span><span class="sxs-lookup"><span data-stu-id="7a005-147">Set max update domain</span></span>
1. <span data-ttu-id="7a005-148">Créer un équilibrage de charge (interne)</span><span class="sxs-lookup"><span data-stu-id="7a005-148">Create a Load Balancer (internal)</span></span>  
   <span data-ttu-id="7a005-149">Sélectionner le réseau virtuel de l’étape précédente</span><span class="sxs-lookup"><span data-stu-id="7a005-149">Select VNET of step above</span></span>
1. <span data-ttu-id="7a005-150">Créer la machine virtuelle 1</span><span class="sxs-lookup"><span data-stu-id="7a005-150">Create Virtual Machine 1</span></span>  
   <span data-ttu-id="7a005-151">https://portal.azure.com/#create/suse-byos.sles-for-sap-byos12-sp1</span><span class="sxs-lookup"><span data-stu-id="7a005-151">https://portal.azure.com/#create/suse-byos.sles-for-sap-byos12-sp1</span></span>  
   <span data-ttu-id="7a005-152">SLES For SAP Applications 12 SP1 (BYOS)</span><span class="sxs-lookup"><span data-stu-id="7a005-152">SLES For SAP Applications 12 SP1 (BYOS)</span></span>  
   <span data-ttu-id="7a005-153">Sélectionner le compte de stockage 1</span><span class="sxs-lookup"><span data-stu-id="7a005-153">Select Storage Account 1</span></span>  
   <span data-ttu-id="7a005-154">Sélectionner le groupe à haute disponibilité</span><span class="sxs-lookup"><span data-stu-id="7a005-154">Select Availability Set</span></span>  
1. <span data-ttu-id="7a005-155">Créer la machine virtuelle 2</span><span class="sxs-lookup"><span data-stu-id="7a005-155">Create Virtual Machine 2</span></span>  
   <span data-ttu-id="7a005-156">https://portal.azure.com/#create/suse-byos.sles-for-sap-byos12-sp1</span><span class="sxs-lookup"><span data-stu-id="7a005-156">https://portal.azure.com/#create/suse-byos.sles-for-sap-byos12-sp1</span></span>  
   <span data-ttu-id="7a005-157">SLES For SAP Applications 12 SP1 (BYOS)</span><span class="sxs-lookup"><span data-stu-id="7a005-157">SLES For SAP Applications 12 SP1 (BYOS)</span></span>  
   <span data-ttu-id="7a005-158">Sélectionner le compte de stockage 2</span><span class="sxs-lookup"><span data-stu-id="7a005-158">Select Storage Account 2</span></span>   
   <span data-ttu-id="7a005-159">Sélectionner le groupe à haute disponibilité</span><span class="sxs-lookup"><span data-stu-id="7a005-159">Select Availability Set</span></span>  
1. <span data-ttu-id="7a005-160">Ajouter des disques de données</span><span class="sxs-lookup"><span data-stu-id="7a005-160">Add Data Disks</span></span>
1. <span data-ttu-id="7a005-161">Configurer l’équilibrage de charge</span><span class="sxs-lookup"><span data-stu-id="7a005-161">Configure the load balancer</span></span>
    1. <span data-ttu-id="7a005-162">Créer un pool d’adresse IP frontal</span><span class="sxs-lookup"><span data-stu-id="7a005-162">Create a frontend IP pool</span></span>
        1. <span data-ttu-id="7a005-163">Ouvrir l’équilibrage de charge, sélectionner le pool d’adresses IP frontal et cliquer sur Ajouter</span><span class="sxs-lookup"><span data-stu-id="7a005-163">Open the load balancer, select frontend IP pool and click Add</span></span>
        1. <span data-ttu-id="7a005-164">Entrer le nom du nouveau pool d’adresses IP frontal (par exemple hana-frontend)</span><span class="sxs-lookup"><span data-stu-id="7a005-164">Enter the name of the new frontend IP pool (for example hana-frontend)</span></span>
       1. <span data-ttu-id="7a005-165">Click OK</span><span class="sxs-lookup"><span data-stu-id="7a005-165">Click OK</span></span>
        1. <span data-ttu-id="7a005-166">Une fois le pool d’adresses IP frontal créé, noter son adresse IP</span><span class="sxs-lookup"><span data-stu-id="7a005-166">After the new frontend IP pool is created, write down its IP address</span></span>
    1. <span data-ttu-id="7a005-167">Créer un pool principal</span><span class="sxs-lookup"><span data-stu-id="7a005-167">Create a backend pool</span></span>
        1. <span data-ttu-id="7a005-168">Ouvrir l’équilibrage de charge, sélectionner les pools principaux et cliquer sur Ajouter</span><span class="sxs-lookup"><span data-stu-id="7a005-168">Open the load balancer, select backend pools and click Add</span></span>
        1. <span data-ttu-id="7a005-169">Entrer le nom du nouveau pool principal (par exemple hana-backend)</span><span class="sxs-lookup"><span data-stu-id="7a005-169">Enter the name of the new backend pool (for example hana-backend)</span></span>
        1. <span data-ttu-id="7a005-170">Cliquer sur Ajouter une machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="7a005-170">Click Add a virtual machine</span></span>
        1. <span data-ttu-id="7a005-171">Sélectionner le groupe à haute disponibilité créé précédemment</span><span class="sxs-lookup"><span data-stu-id="7a005-171">Select the Availability Set you created earlier</span></span>
        1. <span data-ttu-id="7a005-172">Sélectionner les machines virtuelles du cluster SAP HANA</span><span class="sxs-lookup"><span data-stu-id="7a005-172">Select the virtual machines of the SAP HANA cluster</span></span>
        1. <span data-ttu-id="7a005-173">Click OK</span><span class="sxs-lookup"><span data-stu-id="7a005-173">Click OK</span></span>
    1. <span data-ttu-id="7a005-174">Créer une sonde d’intégrité</span><span class="sxs-lookup"><span data-stu-id="7a005-174">Create a health probe</span></span>
       1. <span data-ttu-id="7a005-175">Ouvrir l’équilibrage de charge, sélectionner les sondes d’intégrité et cliquer sur Ajouter</span><span class="sxs-lookup"><span data-stu-id="7a005-175">Open the load balancer, select health probes and click Add</span></span>
        1. <span data-ttu-id="7a005-176">Entrer le nom de la nouvelle sonde d’intégrité (par exemple hana-hp)</span><span class="sxs-lookup"><span data-stu-id="7a005-176">Enter the name of the new health probe (for example hana-hp)</span></span>
        1. <span data-ttu-id="7a005-177">Sélectionner le protocole TCP et le port 625**03**, et conserver un intervalle de 5 et un seuil de défaillance de 2</span><span class="sxs-lookup"><span data-stu-id="7a005-177">Select TCP as protocol, port 625**03**, keep Interval 5 and Unhealthy threshold 2</span></span>
        1. <span data-ttu-id="7a005-178">Click OK</span><span class="sxs-lookup"><span data-stu-id="7a005-178">Click OK</span></span>
    1. <span data-ttu-id="7a005-179">Créer des règles d’équilibrage de charge</span><span class="sxs-lookup"><span data-stu-id="7a005-179">Create load balancing rules</span></span>
        1. <span data-ttu-id="7a005-180">Ouvrir l’équilibrage de charge, sélectionner les règles d’équilibrage de charge et cliquer sur Ajouter</span><span class="sxs-lookup"><span data-stu-id="7a005-180">Open the load balancer, select load balancing rules and click Add</span></span>
        1. <span data-ttu-id="7a005-181">Entrer le nom de la nouvelle règle d’équilibrage de charge (par exemple hana-lb-3**03**15)</span><span class="sxs-lookup"><span data-stu-id="7a005-181">Enter the name of the new load balancer rule (for example hana-lb-3**03**15)</span></span>
        1. <span data-ttu-id="7a005-182">Sélectionner l’adresse IP du serveur frontal, le pool principal et la sonde d’intégrité créés précédemment (par exemple hana-frontend)</span><span class="sxs-lookup"><span data-stu-id="7a005-182">Select the frontend IP address, backend pool and health probe you created earlier (for example hana-frontend)</span></span>
        1. <span data-ttu-id="7a005-183">Conserver le protocole TCP et choisir le port 3**03**15</span><span class="sxs-lookup"><span data-stu-id="7a005-183">Keep protocol TCP, enter port 3**03**15</span></span>
        1. <span data-ttu-id="7a005-184">Augmenter le délai d’inactivité à 30 minutes</span><span class="sxs-lookup"><span data-stu-id="7a005-184">Increase idle timeout to 30 minutes</span></span>
       1. <span data-ttu-id="7a005-185">**Veiller à activer IP flottante**</span><span class="sxs-lookup"><span data-stu-id="7a005-185">**Make sure to enable Floating IP**</span></span>
        1. <span data-ttu-id="7a005-186">Click OK</span><span class="sxs-lookup"><span data-stu-id="7a005-186">Click OK</span></span>
        1. <span data-ttu-id="7a005-187">Répéter les étapes ci-dessus pour le port 3**03**17</span><span class="sxs-lookup"><span data-stu-id="7a005-187">Repeat the steps above for port 3**03**17</span></span>

### <a name="deploy-with-template"></a><span data-ttu-id="7a005-188">Déployer avec un modèle</span><span class="sxs-lookup"><span data-stu-id="7a005-188">Deploy with template</span></span>
<span data-ttu-id="7a005-189">Vous pouvez utiliser un des modèles de démarrage rapide disponibles sur github pour déployer toutes les ressources requises.</span><span class="sxs-lookup"><span data-stu-id="7a005-189">You can use one of the quick start templates on github to deploy all required resources.</span></span> <span data-ttu-id="7a005-190">Le modèle déploie les machines virtuelles, l’équilibrage de charge, le groupe à haute disponibilité, etc. Suivez ces étapes pour déployer le modèle :</span><span class="sxs-lookup"><span data-stu-id="7a005-190">The template deploys the virtual machines, the load balancer, availability set etc. Follow these steps to deploy the template:</span></span>

1. <span data-ttu-id="7a005-191">Ouvrez le [modèle de base de données][template-multisid-db] ou le [modèle convergé][template-converged] sur le portail Azure. Le modèle de base de données crée uniquement les règles d’équilibrage de charge pour une base de données, tandis que le modèle convergé crée également les règles d’équilibrage de charge pour une instance ASCS/SCS et une instance ERS (Linux uniquement).</span><span class="sxs-lookup"><span data-stu-id="7a005-191">Open the [database template][template-multisid-db] or the [converged template][template-converged] on the Azure Portal The database template only creates the load-balancing rules for a database whereas the converged template also creates the load-balancing rules for an ASCS/SCS and ERS (Linux only) instance.</span></span> <span data-ttu-id="7a005-192">Si vous prévoyez d’installer un système SAP NetWeaver et souhaitez également installer l’instance ASC/SCS sur les mêmes machines, utilisez le [modèle convergé][template-converged].</span><span class="sxs-lookup"><span data-stu-id="7a005-192">If you plan to install an SAP NetWeaver based system and you also want to install the ASCS/SCS instance on the same machines, use the [converged template][template-converged].</span></span>
1. <span data-ttu-id="7a005-193">Entrez les paramètres suivants</span><span class="sxs-lookup"><span data-stu-id="7a005-193">Enter the following parameters</span></span>
    1. <span data-ttu-id="7a005-194">ID du système SAP</span><span class="sxs-lookup"><span data-stu-id="7a005-194">Sap System Id</span></span>  
       <span data-ttu-id="7a005-195">Entrez l’ID du système SAP que vous souhaitez installer.</span><span class="sxs-lookup"><span data-stu-id="7a005-195">Enter the SAP system Id of the SAP system you want to install.</span></span> <span data-ttu-id="7a005-196">Cet ID sera utilisé comme préfixe pour les ressources déployées.</span><span class="sxs-lookup"><span data-stu-id="7a005-196">The Id will be used as a prefix for the resources that are deployed.</span></span>
    1. <span data-ttu-id="7a005-197">Type de pile (applicable uniquement si vous utilisez le modèle convergé)</span><span class="sxs-lookup"><span data-stu-id="7a005-197">Stack Type (only applicable if you use the converged template)</span></span>  
       <span data-ttu-id="7a005-198">Sélectionnez le type de pile de SAP NetWeaver</span><span class="sxs-lookup"><span data-stu-id="7a005-198">Select the SAP NetWeaver stack type</span></span>
    1. <span data-ttu-id="7a005-199">Type de système d’exploitation</span><span class="sxs-lookup"><span data-stu-id="7a005-199">Os Type</span></span>  
       <span data-ttu-id="7a005-200">Sélectionnez l’une des distributions Linux.</span><span class="sxs-lookup"><span data-stu-id="7a005-200">Select one of the Linux distributions.</span></span> <span data-ttu-id="7a005-201">Dans cet exemple, sélectionnez SLES 12 BYOS</span><span class="sxs-lookup"><span data-stu-id="7a005-201">For this example, select SLES 12 BYOS</span></span>
    1. <span data-ttu-id="7a005-202">Type de base de données</span><span class="sxs-lookup"><span data-stu-id="7a005-202">Db Type</span></span>  
       <span data-ttu-id="7a005-203">Sélectionnez HANA</span><span class="sxs-lookup"><span data-stu-id="7a005-203">Select HANA</span></span>
    1. <span data-ttu-id="7a005-204">Taille du système SAP</span><span class="sxs-lookup"><span data-stu-id="7a005-204">Sap System Size</span></span>  
       <span data-ttu-id="7a005-205">Le nombre de SAP fournis par le nouveau système.</span><span class="sxs-lookup"><span data-stu-id="7a005-205">The amount of SAPS the new system will provide.</span></span> <span data-ttu-id="7a005-206">Si vous ne savez pas combien de SAP sont requis par le système, demandez à votre partenaire technologique SAP ou un intégrateur système</span><span class="sxs-lookup"><span data-stu-id="7a005-206">If you are not sure how many SAPS the system will require, please ask your SAP Technology Partner or System Integrator</span></span>
    1. <span data-ttu-id="7a005-207">Disponibilité du système</span><span class="sxs-lookup"><span data-stu-id="7a005-207">System Availability</span></span>  
       <span data-ttu-id="7a005-208">Sélectionnez la haute disponibilité (HA).</span><span class="sxs-lookup"><span data-stu-id="7a005-208">Select HA</span></span>
    1. <span data-ttu-id="7a005-209">Nom d’utilisateur et mot de passe d’administrateur</span><span class="sxs-lookup"><span data-stu-id="7a005-209">Admin Username and Admin Password</span></span>  
       <span data-ttu-id="7a005-210">Un utilisateur pouvant être utilisé pour ouvrir une session sur la machine est créé.</span><span class="sxs-lookup"><span data-stu-id="7a005-210">A new user is created that can be used to log on to the machine.</span></span>
    1. <span data-ttu-id="7a005-211">Sous-réseau nouveau ou existant</span><span class="sxs-lookup"><span data-stu-id="7a005-211">New Or Existing Subnet</span></span>  
       <span data-ttu-id="7a005-212">Détermine s’il faut créer un réseau virtuel et un sous-réseau, ou utiliser un sous-réseau existant.</span><span class="sxs-lookup"><span data-stu-id="7a005-212">Determines whether a new virtual network and subnet should be created or an existing subnet should be used.</span></span> <span data-ttu-id="7a005-213">Si vous disposez déjà d’un réseau virtuel connecté à votre réseau local, sélectionnez existant.</span><span class="sxs-lookup"><span data-stu-id="7a005-213">If you already have a virtual network that is connected to your on-premises network, select existing.</span></span>
    1. <span data-ttu-id="7a005-214">ID du sous-réseau</span><span class="sxs-lookup"><span data-stu-id="7a005-214">Subnet Id</span></span>  
    <span data-ttu-id="7a005-215">ID du sous-réseau auquel les machines virtuelles doivent être connectées.</span><span class="sxs-lookup"><span data-stu-id="7a005-215">The ID of the subnet to which the virtual machines should be connected to.</span></span> <span data-ttu-id="7a005-216">Sélectionnez le sous-réseau de votre VPN ou réseau virtuel ExpressRoute pour connecter la machine virtuelle à votre réseau local.</span><span class="sxs-lookup"><span data-stu-id="7a005-216">Select the subnet of your VPN or Express Route virtual network to connect the virtual machine to your on-premises network.</span></span> <span data-ttu-id="7a005-217">L’identifiant se présente généralement comme suit : /abonnements/`<subscription id`>/groupesderessources/`<resource group name`>/fournisseurs/Réseau.Microsoft/réseauxVirtuels/`<virtual network name`>/sous-réseaux/`<subnet name`></span><span class="sxs-lookup"><span data-stu-id="7a005-217">The ID usually looks like /subscriptions/`<subscription id`>/resourceGroups/`<resource group name`>/providers/Microsoft.Network/virtualNetworks/`<virtual network name`>/subnets/`<subnet name`></span></span>

## <a name="setting-up-linux-ha"></a><span data-ttu-id="7a005-218">Configuration de la haute disponibilité Linux</span><span class="sxs-lookup"><span data-stu-id="7a005-218">Setting up Linux HA</span></span>

<span data-ttu-id="7a005-219">Les éléments suivants sont précédés de [A] \(applicable à tous les nœuds), de [1] \(applicable uniquement au nœud 1) ou de [2] \(applicable uniquement au nœud 2).</span><span class="sxs-lookup"><span data-stu-id="7a005-219">The following items are prefixed with either [A] - applicable to all nodes, [1] - only applicable to node 1 or [2] - only applicable to node 2.</span></span>

1. <span data-ttu-id="7a005-220">[A] SLES for SAP BYOS uniquement : inscrire SLES pour pouvoir utiliser les référentiels</span><span class="sxs-lookup"><span data-stu-id="7a005-220">[A] SLES for SAP BYOS only - Register SLES to be able to use the repositories</span></span>
1. <span data-ttu-id="7a005-221">[A] SLES for SAP BYOS uniquement : ajouter un module de cloud public</span><span class="sxs-lookup"><span data-stu-id="7a005-221">[A] SLES for SAP BYOS only - Add public-cloud module</span></span>
1. <span data-ttu-id="7a005-222">[A] Mettre à jour SLES</span><span class="sxs-lookup"><span data-stu-id="7a005-222">[A] Update SLES</span></span>
    ```bash
    sudo zypper update

    ```

1. <span data-ttu-id="7a005-223">[1] Activer l’accès SSH</span><span class="sxs-lookup"><span data-stu-id="7a005-223">[1] Enable ssh access</span></span>
    ```bash
    sudo ssh-keygen -tdsa
    
    # Enter file in which to save the key (/root/.ssh/id_dsa): -> ENTER
    # Enter passphrase (empty for no passphrase): -> ENTER
    # Enter same passphrase again: -> ENTER
    
    # copy the public key
    sudo cat /root/.ssh/id_dsa.pub
    ```

2. <span data-ttu-id="7a005-224">[2] Activer l’accès SSH</span><span class="sxs-lookup"><span data-stu-id="7a005-224">[2] Enable ssh access</span></span>
    ```bash
    sudo ssh-keygen -tdsa

    # insert the public key you copied in the last step into the authorized keys file on the second server
    sudo vi /root/.ssh/authorized_keys
    
    # Enter file in which to save the key (/root/.ssh/id_dsa): -> ENTER
    # Enter passphrase (empty for no passphrase): -> ENTER
    # Enter same passphrase again: -> ENTER
    
    # copy the public key    
    sudo cat /root/.ssh/id_dsa.pub
    ```

1. <span data-ttu-id="7a005-225">[1] Activer l’accès SSH</span><span class="sxs-lookup"><span data-stu-id="7a005-225">[1] Enable ssh access</span></span>
    ```bash
    # insert the public key you copied in the last step into the authorized keys file on the first server
    sudo vi /root/.ssh/authorized_keys
    
    ```

1. <span data-ttu-id="7a005-226">[A] installer l’extension de haute disponibilité</span><span class="sxs-lookup"><span data-stu-id="7a005-226">[A] Install HA extension</span></span>
    ```bash
    sudo zypper install sle-ha-release fence-agents
    
    ```

1. <span data-ttu-id="7a005-227">[A] Configurer la disposition du disque</span><span class="sxs-lookup"><span data-stu-id="7a005-227">[A] Setup disk layout</span></span>
    1. <span data-ttu-id="7a005-228">LVM</span><span class="sxs-lookup"><span data-stu-id="7a005-228">LVM</span></span>  
    <span data-ttu-id="7a005-229">En général, nous recommandons d’utiliser LVM pour les volumes qui stockent des données et des fichiers journaux.</span><span class="sxs-lookup"><span data-stu-id="7a005-229">We generally recommend to use LVM for volumes that store data and log files.</span></span> <span data-ttu-id="7a005-230">L’exemple ci-dessous part du principe que les machines virtuelles disposent de quatre disques de données joints qui doivent être utilisés pour créer deux volumes.</span><span class="sxs-lookup"><span data-stu-id="7a005-230">The example below assumes that the virtual machines have four data disks attached that should be used to create two volumes.</span></span>
        * <span data-ttu-id="7a005-231">Créez des volumes physiques pour tous les disques que vous souhaitez utiliser.</span><span class="sxs-lookup"><span data-stu-id="7a005-231">Create physical volumes for all disks that you want to use.</span></span>
    <pre><code>
    sudo pvcreate /dev/sdc
    sudo pvcreate /dev/sdd
    sudo pvcreate /dev/sde
    sudo pvcreate /dev/sdf
    </code></pre>
        * <span data-ttu-id="7a005-232">Créez un groupe de volumes pour les fichiers de données, un groupe de volumes pour les fichiers journaux et l’autre pour le répertoire partagé de SAP HANA</span><span class="sxs-lookup"><span data-stu-id="7a005-232">Create a volume group for the data files, one volume group for the log files and one for the shared directory of SAP HANA</span></span>
    <pre><code>
    sudo vgcreate vg_hana_data /dev/sdc /dev/sdd
    sudo vgcreate vg_hana_log /dev/sde
    sudo vgcreate vg_hana_shared /dev/sdf
    </code></pre>
        * <span data-ttu-id="7a005-233">Créez les volumes logiques</span><span class="sxs-lookup"><span data-stu-id="7a005-233">Create the logical volumes</span></span>
    <pre><code>
    sudo lvcreate -l 100%FREE -n hana_data vg_hana_data
    sudo lvcreate -l 100%FREE -n hana_log vg_hana_log
    sudo lvcreate -l 100%FREE -n hana_shared vg_hana_shared
    sudo mkfs.xfs /dev/vg_hana_data/hana_data
    sudo mkfs.xfs /dev/vg_hana_log/hana_log
    sudo mkfs.xfs /dev/vg_hana_shared/hana_shared
    </code></pre>
        * <span data-ttu-id="7a005-234">Créez les répertoires de montage et copiez l’UUID de tous les volumes logiques</span><span class="sxs-lookup"><span data-stu-id="7a005-234">Create the mount directories and copy the UUID of all logical volumes</span></span>
    <pre><code>
    sudo mkdir -p /hana/data
    sudo mkdir -p /hana/log
    sudo mkdir -p /hana/shared
    # write down the id of /dev/vg_hana_data/hana_data, /dev/vg_hana_log/hana_log and /dev/vg_hana_shared/hana_shared
    sudo blkid
    </code></pre>
        * <span data-ttu-id="7a005-235">Créez des entrées fstab pour les trois volumes logiques</span><span class="sxs-lookup"><span data-stu-id="7a005-235">Create fstab entries for the three logical volumes</span></span>
    <pre><code>
    sudo vi /etc/fstab
    </code></pre>
    <span data-ttu-id="7a005-236">Insérez cette ligne dans /etc/fstab</span><span class="sxs-lookup"><span data-stu-id="7a005-236">Insert this line to /etc/fstab</span></span>
    <pre><code>
    /dev/disk/by-uuid/<b>&lt;UUID of /dev/vg_hana_data/hana_data&gt;</b> /hana/data xfs  defaults,nofail  0  2
    /dev/disk/by-uuid/<b>&lt;UUID of /dev/vg_hana_log/hana_log&gt;</b> /hana/log xfs  defaults,nofail  0  2
    /dev/disk/by-uuid/<b>&lt;UUID of /dev/vg_hana_shared/hana_shared&gt;</b> /hana/shared xfs  defaults,nofail  0  2
    </code></pre>
        * <span data-ttu-id="7a005-237">Montez les nouveaux volumes</span><span class="sxs-lookup"><span data-stu-id="7a005-237">Mount the new volumes</span></span>
    <pre><code>
    sudo mount -a
    </code></pre>
    1. <span data-ttu-id="7a005-238">Disques simples</span><span class="sxs-lookup"><span data-stu-id="7a005-238">Plain Disks</span></span>  
       <span data-ttu-id="7a005-239">Pour les petits systèmes ou les systèmes de démonstration, vous pouvez placer vos données et fichiers journaux HANA sur un disque.</span><span class="sxs-lookup"><span data-stu-id="7a005-239">For small or demo systems, you can place your HANA data and log files on one disk.</span></span> <span data-ttu-id="7a005-240">Les commandes suivantes permettent de créer une partition au format xfs sur /dev/sdc.</span><span class="sxs-lookup"><span data-stu-id="7a005-240">The following commands create a partition on /dev/sdc and format it with xfs.</span></span>
    ```bash
    sudo fdisk /dev/sdc
    sudo mkfs.xfs /dev/sdc1
    
    # <a name="write-down-the-id-of-devsdc1"></a><span data-ttu-id="7a005-241">notez l’id de /dev/sdc1</span><span class="sxs-lookup"><span data-stu-id="7a005-241">write down the id of /dev/sdc1</span></span>
    <span data-ttu-id="7a005-242">sudo /sbin/blkid  sudo vi /etc/fstab</span><span class="sxs-lookup"><span data-stu-id="7a005-242">sudo /sbin/blkid  sudo vi /etc/fstab</span></span>
    ```

    Insert this line to /etc/fstab
    <pre><code>
    /dev/disk/by-uuid/<b>&lt;UUID&gt;</b> /hana xfs  defaults,nofail  0  2
    </code></pre>

    Create the target directory and mount the disk.

    ```bash
    sudo mkdir /hana
    sudo mount -a
    ```

1. <span data-ttu-id="7a005-243">[A] Configurer la résolution de nom d’hôte pour tous les hôtes</span><span class="sxs-lookup"><span data-stu-id="7a005-243">[A] Setup host name resolution for all hosts</span></span>  
    <span data-ttu-id="7a005-244">Vous pouvez utiliser un serveur DNS ou modifier le fichier /etc/hosts sur tous les nœuds.</span><span class="sxs-lookup"><span data-stu-id="7a005-244">You can either use a DNS server or modify the /etc/hosts on all nodes.</span></span> <span data-ttu-id="7a005-245">Cet exemple montre comment utiliser le fichier /etc/hosts.</span><span class="sxs-lookup"><span data-stu-id="7a005-245">This example shows how to use the /etc/hosts file.</span></span>
   <span data-ttu-id="7a005-246">Remplacez l’adresse IP et le nom d’hôte dans les commandes suivantes</span><span class="sxs-lookup"><span data-stu-id="7a005-246">Replace the IP address and the hostname in the following commands</span></span>
    ```bash
    sudo vi /etc/hosts
    ```
    <span data-ttu-id="7a005-247">Insérez les lignes suivantes dans le fichier /etc/hosts.</span><span class="sxs-lookup"><span data-stu-id="7a005-247">Insert the following lines to /etc/hosts.</span></span> <span data-ttu-id="7a005-248">Modifiez l’adresse IP et le nom d’hôte en fonction de votre environnement</span><span class="sxs-lookup"><span data-stu-id="7a005-248">Change the IP address and hostname to match your environment</span></span>    
    
    <pre><code>
    <b>&lt;IP address of host 1&gt; &lt;hostname of host 1&gt;</b>
    <b>&lt;IP address of host 2&gt; &lt;hostname of host 2&gt;</b>
    </code></pre>

1. <span data-ttu-id="7a005-249">[1] Installer le cluster</span><span class="sxs-lookup"><span data-stu-id="7a005-249">[1] Install Cluster</span></span>
    ```bash
    sudo ha-cluster-init
    
    # Do you want to continue anyway? [y/N] -> y
    # Network address to bind to (e.g.: 192.168.1.0) [10.79.227.0] -> ENTER
    # Multicast address (e.g.: 239.x.x.x) [239.174.218.125] -> ENTER
    # Multicast port [5405] -> ENTER
    # Do you wish to use SBD? [y/N] -> N
    # Do you wish to configure an administration IP? [y/N] -> N
    ```
        
1. <span data-ttu-id="7a005-250">[2] Ajouter un nœud au cluster</span><span class="sxs-lookup"><span data-stu-id="7a005-250">[2] Add node to cluster</span></span>
    ```bash
    sudo ha-cluster-join
        
    # WARNING: NTP is not configured to start at system boot.
    # WARNING: No watchdog device found. If SBD is used, the cluster will be unable to start without a watchdog.
    # Do you want to continue anyway? [y/N] -> y
    # IP address or hostname of existing node (e.g.: 192.168.1.1) [] -> IP address of node 1 e.g. 10.0.0.5
    # /root/.ssh/id_dsa already exists - overwrite? [y/N] N
    ```

1. <span data-ttu-id="7a005-251">[A] Modifier le mot de passe hacluster pour utiliser le même mot de passe</span><span class="sxs-lookup"><span data-stu-id="7a005-251">[A] Change hacluster password to the same password</span></span>
    ```bash
    sudo passwd hacluster
    
    ```

1. <span data-ttu-id="7a005-252">[A] Configurer corosync pour utiliser les autres transports et ajouter la liste de nœuds.</span><span class="sxs-lookup"><span data-stu-id="7a005-252">[A] Configure corosync to use other transport and add nodelist.</span></span> <span data-ttu-id="7a005-253">Le cluster ne fonctionnera pas dans le cas contraire.</span><span class="sxs-lookup"><span data-stu-id="7a005-253">Cluster will not work otherwise.</span></span>
    ```bash
    sudo vi /etc/corosync/corosync.conf    
    
    ```

    <span data-ttu-id="7a005-254">Ajoutez le contenu en gras ci-dessous au fichier.</span><span class="sxs-lookup"><span data-stu-id="7a005-254">Add the following bold content to the file.</span></span>
    
    <pre><code> 
    [...]
      interface { 
          [...] 
      }
      <b>transport:      udpu</b>
    } 
    <b>nodelist {
      node {
        ring0_addr:     < ip address of node 1 >
      }
      node {
        ring0_addr:     < ip address of node 2 > 
      } 
    }</b>
    logging {
      [...]
    </code></pre>

    <span data-ttu-id="7a005-255">Redémarrez ensuite le service corosync</span><span class="sxs-lookup"><span data-stu-id="7a005-255">Then restart the corosync service</span></span>

    ```bash
    sudo service corosync restart
    
    ```

1. <span data-ttu-id="7a005-256">[A] Installer les packages haute disponibilité HANA</span><span class="sxs-lookup"><span data-stu-id="7a005-256">[A] Install HANA HA packages</span></span>  
    ```bash
    sudo zypper install SAPHanaSR
    
    ```

## <a name="installing-sap-hana"></a><span data-ttu-id="7a005-257">Installation de SAP HANA</span><span class="sxs-lookup"><span data-stu-id="7a005-257">Installing SAP HANA</span></span>

<span data-ttu-id="7a005-258">Consultez le chapitre 4 de la publication [SAP HANA SR Performance Optimized Scenario guide][suse-hana-ha-guide] (Scénario d’optimisation des performances de réplication système de SAP HANA) pour installer la réplication système SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="7a005-258">Follow chapter 4 of the [SAP HANA SR Performance Optimized Scenario guide][suse-hana-ha-guide] to install SAP HANA System Replication.</span></span>

1. <span data-ttu-id="7a005-259">[A] Exécuter hdblcm à partir du DVD HANA</span><span class="sxs-lookup"><span data-stu-id="7a005-259">[A] Run hdblcm from the HANA DVD</span></span>
    * <span data-ttu-id="7a005-260">Choose installation -> 1</span><span class="sxs-lookup"><span data-stu-id="7a005-260">Choose installation -> 1</span></span>
    * <span data-ttu-id="7a005-261">Select additional components for installation -> 1</span><span class="sxs-lookup"><span data-stu-id="7a005-261">Select additional components for installation -> 1</span></span>
    * <span data-ttu-id="7a005-262">Enter Installation Path [/hana/shared]: -> ENTRÉE</span><span class="sxs-lookup"><span data-stu-id="7a005-262">Enter Installation Path [/hana/shared]: -> ENTER</span></span>
    * <span data-ttu-id="7a005-263">Enter Local Host Name [..]: -> ENTRÉE</span><span class="sxs-lookup"><span data-stu-id="7a005-263">Enter Local Host Name [..]: -> ENTER</span></span>
    * <span data-ttu-id="7a005-264">Do you want to add additional hosts to the system?</span><span class="sxs-lookup"><span data-stu-id="7a005-264">Do you want to add additional hosts to the system?</span></span> <span data-ttu-id="7a005-265">(y/n) [n] : -> ENTRÉE</span><span class="sxs-lookup"><span data-stu-id="7a005-265">(y/n) [n]: -> ENTER</span></span>
    * <span data-ttu-id="7a005-266">Enter SAP HANA System ID : <SID of HANA e.g. HDB></span><span class="sxs-lookup"><span data-stu-id="7a005-266">Enter SAP HANA System ID: <SID of HANA e.g. HDB></span></span>
    * <span data-ttu-id="7a005-267">Enter Instance Number [00] :</span><span class="sxs-lookup"><span data-stu-id="7a005-267">Enter Instance Number [00]:</span></span>   
  <span data-ttu-id="7a005-268">Numéro d’instance HANA.</span><span class="sxs-lookup"><span data-stu-id="7a005-268">HANA Instance number.</span></span> <span data-ttu-id="7a005-269">Utilisez 03 si vous avez utilisé le modèle Azure ou si vous avez suivi l’exemple ci-dessus</span><span class="sxs-lookup"><span data-stu-id="7a005-269">Use 03 if you used the Azure Template or followed the example above</span></span>
    * <span data-ttu-id="7a005-270">Select Database Mode / Enter Index [1] : -> ENTRÉE</span><span class="sxs-lookup"><span data-stu-id="7a005-270">Select Database Mode / Enter Index [1]: -> ENTER</span></span>
    * <span data-ttu-id="7a005-271">Select System Usage / Enter Index [4] :</span><span class="sxs-lookup"><span data-stu-id="7a005-271">Select System Usage / Enter Index [4]:</span></span>  
  <span data-ttu-id="7a005-272">Select the system Usage</span><span class="sxs-lookup"><span data-stu-id="7a005-272">Select the system Usage</span></span>
    * <span data-ttu-id="7a005-273">Enter Location of Data Volumes [/hana/data/HDB] : -> ENTRÉE</span><span class="sxs-lookup"><span data-stu-id="7a005-273">Enter Location of Data Volumes [/hana/data/HDB]: -> ENTER</span></span>
    * <span data-ttu-id="7a005-274">Enter Location of Log Volumes [/hana/log/HDB] : -> ENTRÉE</span><span class="sxs-lookup"><span data-stu-id="7a005-274">Enter Location of Log Volumes [/hana/log/HDB]: -> ENTER</span></span>
    * <span data-ttu-id="7a005-275">Restrict maximum memory allocation?</span><span class="sxs-lookup"><span data-stu-id="7a005-275">Restrict maximum memory allocation?</span></span> <span data-ttu-id="7a005-276">[n] : -> ENTRÉE</span><span class="sxs-lookup"><span data-stu-id="7a005-276">[n]: -> ENTER</span></span>
    * <span data-ttu-id="7a005-277">Enter Certificate Host Name For Host '...'</span><span class="sxs-lookup"><span data-stu-id="7a005-277">Enter Certificate Host Name For Host '...'</span></span> <span data-ttu-id="7a005-278">[...] : -> ENTRÉE</span><span class="sxs-lookup"><span data-stu-id="7a005-278">[...]: -> ENTER</span></span>
    * <span data-ttu-id="7a005-279">Enter SAP Host Agent User (sapadm) Password:</span><span class="sxs-lookup"><span data-stu-id="7a005-279">Enter SAP Host Agent User (sapadm) Password:</span></span>
    * <span data-ttu-id="7a005-280">Confirm SAP Host Agent User (sapadm) Password:</span><span class="sxs-lookup"><span data-stu-id="7a005-280">Confirm SAP Host Agent User (sapadm) Password:</span></span>
    * <span data-ttu-id="7a005-281">Enter System Administrator (hdbadm) Password:</span><span class="sxs-lookup"><span data-stu-id="7a005-281">Enter System Administrator (hdbadm) Password:</span></span>
    * <span data-ttu-id="7a005-282">Confirm System Administrator (hdbadm) Password:</span><span class="sxs-lookup"><span data-stu-id="7a005-282">Confirm System Administrator (hdbadm) Password:</span></span>
    * <span data-ttu-id="7a005-283">Enter System Administrator Home Directory [/usr/sap/HDB/home] : -> ENTRÉE</span><span class="sxs-lookup"><span data-stu-id="7a005-283">Enter System Administrator Home Directory [/usr/sap/HDB/home]: -> ENTER</span></span>
    * <span data-ttu-id="7a005-284">Enter System Administrator Login Shell [/bin/sh] : -> ENTRÉE</span><span class="sxs-lookup"><span data-stu-id="7a005-284">Enter System Administrator Login Shell [/bin/sh]: -> ENTER</span></span>
    * <span data-ttu-id="7a005-285">Enter System Administrator User ID [1001] : -> ENTRÉE</span><span class="sxs-lookup"><span data-stu-id="7a005-285">Enter System Administrator User ID [1001]: -> ENTER</span></span>
    * <span data-ttu-id="7a005-286">Enter ID of User Group (sapsys) [79] : -> ENTRÉE</span><span class="sxs-lookup"><span data-stu-id="7a005-286">Enter ID of User Group (sapsys) [79]: -> ENTER</span></span>
    * <span data-ttu-id="7a005-287">Enter Database User (SYSTEM) Password:</span><span class="sxs-lookup"><span data-stu-id="7a005-287">Enter Database User (SYSTEM) Password:</span></span>
    * <span data-ttu-id="7a005-288">Confirm Database User (SYSTEM) Password:</span><span class="sxs-lookup"><span data-stu-id="7a005-288">Confirm Database User (SYSTEM) Password:</span></span>
    * <span data-ttu-id="7a005-289">Restart system after machine reboot?</span><span class="sxs-lookup"><span data-stu-id="7a005-289">Restart system after machine reboot?</span></span> <span data-ttu-id="7a005-290">[n] : -> ENTRÉE</span><span class="sxs-lookup"><span data-stu-id="7a005-290">[n]: -> ENTER</span></span>
    * <span data-ttu-id="7a005-291">Do you want to continue?</span><span class="sxs-lookup"><span data-stu-id="7a005-291">Do you want to continue?</span></span> <span data-ttu-id="7a005-292">(y/n) :</span><span class="sxs-lookup"><span data-stu-id="7a005-292">(y/n):</span></span>  
  <span data-ttu-id="7a005-293">Validez le résumé et entrez y pour continuer</span><span class="sxs-lookup"><span data-stu-id="7a005-293">Validate the summary and enter y to continue</span></span>
1. <span data-ttu-id="7a005-294">[A] Mettre à niveau l’agent hôte SAP</span><span class="sxs-lookup"><span data-stu-id="7a005-294">[A] Upgrade SAP Host Agent</span></span>  
  <span data-ttu-id="7a005-295">Téléchargez la dernière archive de l’agent hôte SAP à partir du [SAP Softwarecenter][sap-swcenter] et exécutez la commande suivante pour mettre à niveau l’agent.</span><span class="sxs-lookup"><span data-stu-id="7a005-295">Download the latest SAP Host Agent archive from the [SAP Softwarecenter][sap-swcenter] and run the following command to upgrade the agent.</span></span> <span data-ttu-id="7a005-296">Remplacez le chemin d’accès à l’archive pour pointer vers le fichier que vous avez téléchargé.</span><span class="sxs-lookup"><span data-stu-id="7a005-296">Replace the path to the archive to point to the file you downloaded.</span></span>
    ```bash
    sudo /usr/sap/hostctrl/exe/saphostexec -upgrade -archive <path to SAP Host Agent SAR>
    ```

1. <span data-ttu-id="7a005-297">[1] Créer la réplication HANA (en tant que root)</span><span class="sxs-lookup"><span data-stu-id="7a005-297">[1] Create HANA replication (as root)</span></span>  
    <span data-ttu-id="7a005-298">Exécutez la commande ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="7a005-298">Run the following command.</span></span> <span data-ttu-id="7a005-299">Veillez à remplacer les chaînes en gras (ID du système HANA HDB et numéro d’instance 03) par les valeurs de votre installation SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="7a005-299">Make sure to replace bold strings (HANA System ID HDB and instance number 03) with the values of your SAP HANA installation.</span></span>
    <pre><code>
    PATH="$PATH:/usr/sap/<b>HDB</b>/HDB<b>03</b>/exe"
    hdbsql -u system -i <b>03</b> 'CREATE USER <b>hdb</b>hasync PASSWORD "<b>passwd</b>"' 
    hdbsql -u system -i <b>03</b> 'GRANT DATA ADMIN TO <b>hdb</b>hasync' 
    hdbsql -u system -i <b>03</b> 'ALTER USER <b>hdb</b>hasync DISABLE PASSWORD LIFETIME' 
    </code></pre>

1. <span data-ttu-id="7a005-300">[A] Créer l’entrée keystore (en tout que root)</span><span class="sxs-lookup"><span data-stu-id="7a005-300">[A] Create keystore entry (as root)</span></span>
    <pre><code>
    PATH="$PATH:/usr/sap/<b>HDB</b>/HDB<b>03</b>/exe"
    hdbuserstore SET <b>hdb</b>haloc localhost:3<b>03</b>15 <b>hdb</b>hasync <b>passwd</b>
    </code></pre>
1. <span data-ttu-id="7a005-301">[1] Sauvegarder la base de données (en tant que root)</span><span class="sxs-lookup"><span data-stu-id="7a005-301">[1] Backup database (as root)</span></span>
    <pre><code>
    PATH="$PATH:/usr/sap/<b>HDB</b>/HDB<b>03</b>/exe"
    hdbsql -u system -i <b>03</b> "BACKUP DATA USING FILE ('<b>initialbackup</b>')" 
    </code></pre>
1. <span data-ttu-id="7a005-302">[1] Basculer sur l’utilisateur sapsid (par exemple, hdbadm) et créer le site principal.</span><span class="sxs-lookup"><span data-stu-id="7a005-302">[1] Switch to the sapsid user (for example hdbadm) and create the primary site.</span></span>
    <pre><code>
    su - <b>hdb</b>adm
    hdbnsutil -sr_enable –-name=<b>SITE1</b>
    </code></pre>
1. <span data-ttu-id="7a005-303">[2] Basculer sur l’utilisateur sapsid (par exemple, hdbadm) et créer le site secondaire.</span><span class="sxs-lookup"><span data-stu-id="7a005-303">[2] Switch to the sapsid user (for example hdbadm) and create the secondary site.</span></span>
    <pre><code>
    su - <b>hdb</b>adm
    sapcontrol -nr <b>03</b> -function StopWait 600 10
    hdbnsutil -sr_register --remoteHost=<b>saphanavm1</b> --remoteInstance=<b>03</b> --replicationMode=sync --name=<b>SITE2</b> 
    </code></pre>

## <a name="configure-cluster-framework"></a><span data-ttu-id="7a005-304">Configurer le framework du cluster</span><span class="sxs-lookup"><span data-stu-id="7a005-304">Configure Cluster Framework</span></span>

<span data-ttu-id="7a005-305">Modifier les paramètres par défaut</span><span class="sxs-lookup"><span data-stu-id="7a005-305">Change the default settings</span></span>

<pre>
sudo vi crm-defaults.txt
# enter the following to crm-defaults.txt
<code>
property $id="cib-bootstrap-options" \
  no-quorum-policy="ignore" \
  stonith-enabled="true" \
  stonith-action="reboot" \
  stonith-timeout="150s"
rsc_defaults $id="rsc-options" \
  resource-stickiness="1000" \
  migration-threshold="5000"
op_defaults $id="op-options" \
  timeout="600"
</code>

# <a name="now-we-load-the-file-to-the-cluster"></a><span data-ttu-id="7a005-306">nous allons maintenant charger le fichier dans le cluster</span><span class="sxs-lookup"><span data-stu-id="7a005-306">now we load the file to the cluster</span></span>
<span data-ttu-id="7a005-307">sudo crm configure load update crm-defaults.txt</span><span class="sxs-lookup"><span data-stu-id="7a005-307">sudo crm configure load update crm-defaults.txt</span></span>
</pre>

### <a name="create-stonith-device"></a><span data-ttu-id="7a005-308">Créer le périphérique STONITH</span><span class="sxs-lookup"><span data-stu-id="7a005-308">Create STONITH device</span></span>

<span data-ttu-id="7a005-309">Le périphérique STONITH utilise un principal de service pour l’autorisation sur Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="7a005-309">The STONITH device uses a Service Principal to authorize against Microsoft Azure.</span></span> <span data-ttu-id="7a005-310">Pour créer un principal de service, procédez comme suit.</span><span class="sxs-lookup"><span data-stu-id="7a005-310">Please follow these steps to create a Service Principal.</span></span>

1. <span data-ttu-id="7a005-311">Accédez à <https://portal.azure.com></span><span class="sxs-lookup"><span data-stu-id="7a005-311">Go to <https://portal.azure.com></span></span>
1. <span data-ttu-id="7a005-312">Ouvrez le panneau Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="7a005-312">Open the Azure Active Directory blade</span></span>  
   <span data-ttu-id="7a005-313">Accédez aux propriétés et notez l’ID de répertoire.</span><span class="sxs-lookup"><span data-stu-id="7a005-313">Go to Properties and write down the Directory Id.</span></span> <span data-ttu-id="7a005-314">Il s’agit de **l’ID client**.</span><span class="sxs-lookup"><span data-stu-id="7a005-314">This is the **tenant id**.</span></span>
1. <span data-ttu-id="7a005-315">Cliquez sur Inscriptions d’applications</span><span class="sxs-lookup"><span data-stu-id="7a005-315">Click App registrations</span></span>
1. <span data-ttu-id="7a005-316">Cliquez sur Ajouter.</span><span class="sxs-lookup"><span data-stu-id="7a005-316">Click Add</span></span>
1. <span data-ttu-id="7a005-317">Entrez un nom, sélectionnez le type d’application « Application web/API », entrez une URL de connexion (par exemple, http://localhost) et cliquez sur Créer</span><span class="sxs-lookup"><span data-stu-id="7a005-317">Enter a Name, select Application Type "Web app/API", enter a sign-on URL (for example http://localhost) and click Create</span></span>
1. <span data-ttu-id="7a005-318">L’URL de connexion n’est pas utilisée et peut être une URL valide</span><span class="sxs-lookup"><span data-stu-id="7a005-318">The sign-on URL is not used and can be any valid URL</span></span>
1. <span data-ttu-id="7a005-319">Sélectionnez la nouvelle application et cliquez sur Clés dans l’onglet Paramètres</span><span class="sxs-lookup"><span data-stu-id="7a005-319">Select the new App and click Keys in the Settings tab</span></span>
1. <span data-ttu-id="7a005-320">Entrez une description pour la nouvelle clé, sélectionnez « N’expire jamais » et cliquez sur Enregistrer</span><span class="sxs-lookup"><span data-stu-id="7a005-320">Enter a description for a new key, select "Never expires" and click Save</span></span>
1. <span data-ttu-id="7a005-321">Notez la valeur.</span><span class="sxs-lookup"><span data-stu-id="7a005-321">Write down the Value.</span></span> <span data-ttu-id="7a005-322">Cette valeur est utilisée comme **mot de passe** pour le principal de service</span><span class="sxs-lookup"><span data-stu-id="7a005-322">It is used as the **password** for the Service Principal</span></span>
1. <span data-ttu-id="7a005-323">Notez l’ID de l’application.</span><span class="sxs-lookup"><span data-stu-id="7a005-323">Write down the Application Id.</span></span> <span data-ttu-id="7a005-324">Cet identifiant est utilisé comme nom d’utilisateur (**ID de connexion** dans la procédure ci-dessous) du principal de service</span><span class="sxs-lookup"><span data-stu-id="7a005-324">It is used as the username (**login id** in the steps below) of the Service Principal</span></span>

<span data-ttu-id="7a005-325">Par défaut, le principal de service ne possède pas les autorisations d’accéder à vos ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="7a005-325">The Service Principal does not have permissions to access your Azure resources by default.</span></span> <span data-ttu-id="7a005-326">Vous devez accorder au principal de service les autorisations de démarrer et arrêter (libérer) toutes les machines virtuelles du cluster.</span><span class="sxs-lookup"><span data-stu-id="7a005-326">You need to give the Service Principal permissions to start and stop (deallocate) all virtual machines of the cluster.</span></span>

1. <span data-ttu-id="7a005-327">Accédez à https://portal.azure.com</span><span class="sxs-lookup"><span data-stu-id="7a005-327">Go to https://portal.azure.com</span></span>
1. <span data-ttu-id="7a005-328">Ouvrez le panneau Toutes les ressources</span><span class="sxs-lookup"><span data-stu-id="7a005-328">Open the All resources blade</span></span>
1. <span data-ttu-id="7a005-329">Sélectionnez la machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="7a005-329">Select the virtual machine</span></span>
1. <span data-ttu-id="7a005-330">Cliquez sur Contrôle d’accès (IAM)</span><span class="sxs-lookup"><span data-stu-id="7a005-330">Click Access control (IAM)</span></span>
1. <span data-ttu-id="7a005-331">Cliquez sur Ajouter.</span><span class="sxs-lookup"><span data-stu-id="7a005-331">Click Add</span></span>
1. <span data-ttu-id="7a005-332">Sélectionnez le rôle de propriétaire</span><span class="sxs-lookup"><span data-stu-id="7a005-332">Select the role Owner</span></span>
1. <span data-ttu-id="7a005-333">Entrez le nom de l’application que vous avez créée ci-dessus</span><span class="sxs-lookup"><span data-stu-id="7a005-333">Enter the name of the application you created above</span></span>
1. <span data-ttu-id="7a005-334">Click OK</span><span class="sxs-lookup"><span data-stu-id="7a005-334">Click OK</span></span>

<span data-ttu-id="7a005-335">Une fois que vous avez modifié les autorisations pour les machines virtuelles, vous pouvez configurer les périphériques STONITH dans le cluster.</span><span class="sxs-lookup"><span data-stu-id="7a005-335">After you edited the permissions for the virtual machines, you can configure the STONITH devices in the cluster.</span></span>

<pre>
sudo vi crm-fencing.txt
# enter the following to crm-fencing.txt
# replace the bold string with your subscription id, resource group, tenant id, service principal id and password
<code>
primitive rsc_st_azure_1 stonith:fence_azure_arm \
    params subscriptionId="<b>subscription id</b>" resourceGroup="<b>resource group</b>" tenantId="<b>tenant id</b>" login="<b>login id</b>" passwd="<b>password</b>"

primitive rsc_st_azure_2 stonith:fence_azure_arm \
    params subscriptionId="<b>subscription id</b>" resourceGroup="<b>resource group</b>" tenantId="<b>tenant id</b>" login="<b>login id</b>" passwd="<b>password</b>"

colocation col_st_azure -2000: rsc_st_azure_1:Started rsc_st_azure_2:Started
</code>

# <a name="now-we-load-the-file-to-the-cluster"></a><span data-ttu-id="7a005-336">nous allons maintenant charger le fichier dans le cluster</span><span class="sxs-lookup"><span data-stu-id="7a005-336">now we load the file to the cluster</span></span>
<span data-ttu-id="7a005-337">sudo crm configure load update crm-fencing.txt</span><span class="sxs-lookup"><span data-stu-id="7a005-337">sudo crm configure load update crm-fencing.txt</span></span>
</pre>

### <a name="create-sap-hana-resources"></a><span data-ttu-id="7a005-338">Créer des ressources SAP HANA</span><span class="sxs-lookup"><span data-stu-id="7a005-338">Create SAP HANA resources</span></span>

<pre>
sudo vi crm-saphanatop.txt
# enter the following to crm-saphana.txt
# replace the bold string with your instance number and HANA system id
<code>
primitive rsc_SAPHanaTopology_<b>HDB</b>_HDB<b>03</b> ocf:suse:SAPHanaTopology \
    operations $id="rsc_sap2_<b>HDB</b>_HDB<b>03</b>-operations" \
    op monitor interval="10" timeout="600" \
    op start interval="0" timeout="600" \
    op stop interval="0" timeout="300" \
    params SID="<b>HDB</b>" InstanceNumber="<b>03</b>"

clone cln_SAPHanaTopology_<b>HDB</b>_HDB<b>03</b> rsc_SAPHanaTopology_<b>HDB</b>_HDB<b>03</b> \
    meta is-managed="true" clone-node-max="1" target-role="Started" interleave="true"
</code>

# <a name="now-we-load-the-file-to-the-cluster"></a><span data-ttu-id="7a005-339">nous allons maintenant charger le fichier dans le cluster</span><span class="sxs-lookup"><span data-stu-id="7a005-339">now we load the file to the cluster</span></span>
<span data-ttu-id="7a005-340">sudo crm configure load update crm-saphanatop.txt</span><span class="sxs-lookup"><span data-stu-id="7a005-340">sudo crm configure load update crm-saphanatop.txt</span></span>
</pre>

<pre>
sudo vi crm-saphana.txt
# enter the following to crm-saphana.txt
# replace the bold string with your instance number, HANA system id and the frontend IP address of the Azure load balancer. 
<code>
primitive rsc_SAPHana_<b>HDB</b>_HDB<b>03</b> ocf:suse:SAPHana \
    operations $id="rsc_sap_<b>HDB</b>_HDB<b>03</b>-operations" \
    op start interval="0" timeout="3600" \
    op stop interval="0" timeout="3600" \
    op promote interval="0" timeout="3600" \
    op monitor interval="60" role="Master" timeout="700" \
    op monitor interval="61" role="Slave" timeout="700" \
    params SID="<b>HDB</b>" InstanceNumber="<b>03</b>" PREFER_SITE_TAKEOVER="true" \
    DUPLICATE_PRIMARY_TIMEOUT="7200" AUTOMATED_REGISTER="false"

ms msl_SAPHana_<b>HDB</b>_HDB<b>03</b> rsc_SAPHana_<b>HDB</b>_HDB<b>03</b> \
    meta is-managed="true" notify="true" clone-max="2" clone-node-max="1" \
    target-role="Started" interleave="true"

primitive rsc_ip_<b>HDB</b>_HDB<b>03</b> ocf:heartbeat:IPaddr2 \ 
    meta target-role="Started" is-managed="true" \ 
    operations $id="rsc_ip_<b>HDB</b>_HDB<b>03</b>-operations" \ 
    op monitor interval="10s" timeout="20s" \ 
    params ip="<b>10.0.0.21</b>" 
primitive rsc_nc_<b>HDB</b>_HDB<b>03</b> anything \ 
    params binfile="/usr/bin/nc" cmdline_options="-l -k 625<b>03</b>" \ 
    op monitor timeout=20s interval=10 depth=0 
group g_ip_<b>HDB</b>_HDB<b>03</b> rsc_ip_<b>HDB</b>_HDB<b>03</b> rsc_nc_<b>HDB</b>_HDB<b>03</b>
 
colocation col_saphana_ip_<b>HDB</b>_HDB<b>03</b> 2000: g_ip_<b>HDB</b>_HDB<b>03</b>:Started \ 
    msl_SAPHana_<b>HDB</b>_HDB<b>03</b>:Master  
order ord_SAPHana_<b>HDB</b>_HDB<b>03</b> 2000: cln_SAPHanaTopology_<b>HDB</b>_HDB<b>03</b> \ 
    msl_SAPHana_<b>HDB</b>_HDB<b>03</b>
</code>

# <a name="now-we-load-the-file-to-the-cluster"></a><span data-ttu-id="7a005-341">nous allons maintenant charger le fichier dans le cluster</span><span class="sxs-lookup"><span data-stu-id="7a005-341">now we load the file to the cluster</span></span>
<span data-ttu-id="7a005-342">sudo crm configure load update crm-saphana.txt</span><span class="sxs-lookup"><span data-stu-id="7a005-342">sudo crm configure load update crm-saphana.txt</span></span>
</pre>

### <a name="test-cluster-setup"></a><span data-ttu-id="7a005-343">Tester la configuration du cluster</span><span class="sxs-lookup"><span data-stu-id="7a005-343">Test cluster setup</span></span>
<span data-ttu-id="7a005-344">Le chapitre suivant vous explique comment tester votre configuration.</span><span class="sxs-lookup"><span data-stu-id="7a005-344">The following chapter describe how you can test your setup.</span></span> <span data-ttu-id="7a005-345">Chaque test suppose que vous êtes connecté en tant que root et que le nœud principal SAP HANA est en cours d’exécution sur la machine virtuelle saphanavm1.</span><span class="sxs-lookup"><span data-stu-id="7a005-345">Every test assumes that you are root and the SAP HANA master is running on the virtual machine saphanavm1.</span></span>

#### <a name="fencing-test"></a><span data-ttu-id="7a005-346">Test de délimitation</span><span class="sxs-lookup"><span data-stu-id="7a005-346">Fencing Test</span></span>

<span data-ttu-id="7a005-347">Vous pouvez tester l’installation de l’agent de délimitation en désactivant l’interface réseau sur le nœud saphanavm1.</span><span class="sxs-lookup"><span data-stu-id="7a005-347">You can test the setup of the fencing agent by disabling the network interface on node saphanavm1.</span></span>

<pre><code>
sudo ifdown eth0
</code></pre>

<span data-ttu-id="7a005-348">La machine virtuelle doit maintenant être redémarrée ou arrêtée en fonction de la configuration de votre cluster.</span><span class="sxs-lookup"><span data-stu-id="7a005-348">The virtual machine should now get restarted or stopped depending on your cluster configuration.</span></span>
<span data-ttu-id="7a005-349">Si vous désactivez l’action stonith, la machine virtuelle est arrêtée et les ressources sont migrées vers la machine virtuelle en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="7a005-349">If you set the stonith-action to off, the virtual machine will be stopped and the resources are migrated to the running virtual machine.</span></span>

<span data-ttu-id="7a005-350">Une fois que vous redémarrez la machine virtuelle, la ressource SAP HANA ne peut pas démarrer en tant que ressource secondaire si vous définissez AUTOMATED_REGISTER="false".</span><span class="sxs-lookup"><span data-stu-id="7a005-350">Once you start the virtual machine again, the SAP HANA resource will fail to start as secondary if you set AUTOMATED_REGISTER="false".</span></span> <span data-ttu-id="7a005-351">Dans ce cas, vous devez configurer l’instance HANA en tant que ressource secondaire en exécutant la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="7a005-351">In this case, you need to configure the HANA instance as secondary by executing the following command:</span></span>

<pre><code>
su - <b>hdb</b>adm

# Stop the HANA instance just in case it is running
sapcontrol -nr <b>03</b> -function StopWait 600 10
hdbnsutil -sr_register --remoteHost=<b>saphanavm2</b> --remoteInstance=<b>03</b> --replicationMode=sync --name=<b>SITE1</b>

# switch back to root and cleanup the failed state
exit
crm resource cleanup msl_SAPHana_<b>HDB</b>_HDB<b>03</b> <b>saphanavm1</b>
</code></pre>

#### <a name="testing-a-manual-failover"></a><span data-ttu-id="7a005-352">Tester un basculement manuel</span><span class="sxs-lookup"><span data-stu-id="7a005-352">Testing a manual failover</span></span>

<span data-ttu-id="7a005-353">Vous pouvez tester un basculement manuel en arrêtant le service pacemaker sur le nœud saphanavm1.</span><span class="sxs-lookup"><span data-stu-id="7a005-353">You can test a manual failover by stopping the pacemaker service on node saphanavm1.</span></span>
<pre><code>
service pacemaker stop
</code></pre>

<span data-ttu-id="7a005-354">Après le basculement, vous pouvez démarrer de nouveau le service.</span><span class="sxs-lookup"><span data-stu-id="7a005-354">After the failover, you can start the service again.</span></span> <span data-ttu-id="7a005-355">La ressource SAP HANA sur saphanavm1 ne peut pas démarrer en tant que ressource secondaire si vous définissez AUTOMATED_REGISTER="false".</span><span class="sxs-lookup"><span data-stu-id="7a005-355">The SAP HANA resource on saphanavm1 will fail to start as secondary if you set AUTOMATED_REGISTER="false".</span></span> <span data-ttu-id="7a005-356">Dans ce cas, vous devez configurer l’instance HANA en tant que ressource secondaire en exécutant la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="7a005-356">In this case, you need to configure the HANA instance as secondary by executing the following command:</span></span>

<pre><code>
service pacemaker start
su - <b>hdb</b>adm

# Stop the HANA instance just in case it is running
sapcontrol -nr <b>03</b> -function StopWait 600 10
hdbnsutil -sr_register --remoteHost=<b>saphanavm2</b> --remoteInstance=<b>03</b> --replicationMode=sync --name=<b>SITE1</b> 


# switch back to root and cleanup the failed state
exit
crm resource cleanup msl_SAPHana_<b>HDB</b>_HDB<b>03</b> <b>saphanavm1</b>
</code></pre>

#### <a name="testing-a-migration"></a><span data-ttu-id="7a005-357">Tester une migration</span><span class="sxs-lookup"><span data-stu-id="7a005-357">Testing a migration</span></span>

<span data-ttu-id="7a005-358">Vous pouvez migrer le nœud principal SAP HANA en exécutant la commande suivante</span><span class="sxs-lookup"><span data-stu-id="7a005-358">You can migrate the SAP HANA master node by executing the following command</span></span>
<pre><code>
crm resource migrate msl_SAPHana_<b>HDB</b>_HDB<b>03</b> <b>saphanavm2</b>
crm resource migrate g_ip_<b>HDB</b>_HDB<b>03</b> <b>saphanavm2</b>
</code></pre>

<span data-ttu-id="7a005-359">Cette commande permet de migrer vers saphanavm2 le nœud principal SAP HANA et le groupe qui contient l’adresse IP virtuelle.</span><span class="sxs-lookup"><span data-stu-id="7a005-359">This should migrate the SAP HANA master node and the group that contains the virtual IP address to saphanavm2.</span></span>
<span data-ttu-id="7a005-360">La ressource SAP HANA sur saphanavm1 ne peut pas démarrer en tant que ressource secondaire si vous définissez AUTOMATED_REGISTER="false".</span><span class="sxs-lookup"><span data-stu-id="7a005-360">The SAP HANA resource on saphanavm1 will fail to start as secondary if you set AUTOMATED_REGISTER="false".</span></span> <span data-ttu-id="7a005-361">Dans ce cas, vous devez configurer l’instance HANA en tant que ressource secondaire en exécutant la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="7a005-361">In this case, you need to configure the HANA instance as secondary by executing the following command:</span></span>

<pre><code>
su - <b>hdb</b>adm

# Stop the HANA instance just in case it is running
sapcontrol -nr <b>03</b> -function StopWait 600 10
hdbnsutil -sr_register --remoteHost=<b>saphanavm2</b> --remoteInstance=<b>03</b> --replicationMode=sync --name=<b>SITE1</b> 
</code></pre>

<span data-ttu-id="7a005-362">La migration crée des contraintes d’emplacement qui doivent être de nouveau supprimées.</span><span class="sxs-lookup"><span data-stu-id="7a005-362">The migration creates location contraints that need to be deleted again.</span></span>

<pre><code>
crm configure edited

# delete location contraints that are named like the following contraint. You should have two contraints, one for the SAP HANA resource and one for the IP address group.
location cli-prefer-g_ip_<b>HDB</b>_HDB<b>03</b> g_ip_<b>HDB</b>_HDB<b>03</b> role=Started inf: <b>saphanavm2</b>
</code></pre>

<span data-ttu-id="7a005-363">Vous devez également nettoyer l’état de la ressource du nœud secondaire</span><span class="sxs-lookup"><span data-stu-id="7a005-363">You also need to cleanup the state of the secondary node resource</span></span>

<pre><code>
# switch back to root and cleanup the failed state
exit
crm resource cleanup msl_SAPHana_<b>HDB</b>_HDB<b>03</b> <b>saphanavm1</b>
</code></pre>

## <a name="next-steps"></a><span data-ttu-id="7a005-364">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="7a005-364">Next steps</span></span>
* <span data-ttu-id="7a005-365">[Planification et implémentation de machines virtuelles Azure pour SAP][planning-guide]</span><span class="sxs-lookup"><span data-stu-id="7a005-365">[Azure Virtual Machines planning and implementation for SAP][planning-guide]</span></span>
* <span data-ttu-id="7a005-366">[Déploiement de machines virtuelles Azure pour SAP][deployment-guide]</span><span class="sxs-lookup"><span data-stu-id="7a005-366">[Azure Virtual Machines deployment for SAP][deployment-guide]</span></span>
* <span data-ttu-id="7a005-367">[Déploiement SGBD de machines virtuelles Azure pour SAP][dbms-guide]</span><span class="sxs-lookup"><span data-stu-id="7a005-367">[Azure Virtual Machines DBMS deployment for SAP][dbms-guide]</span></span>
* <span data-ttu-id="7a005-368">Pour savoir comment établir une haute disponibilité et planifier la récupération d’urgence de SAP HANA sur Azure (grandes instances), consultez [Haute disponibilité et récupération d’urgence de SAP HANA (grandes instances) sur Azure](hana-overview-high-availability-disaster-recovery.md).</span><span class="sxs-lookup"><span data-stu-id="7a005-368">To learn how to establish high availability and plan for disaster recovery of SAP HANA on Azure (large instances), see [SAP HANA (large instances) high availability and disaster recovery on Azure](hana-overview-high-availability-disaster-recovery.md).</span></span> 
