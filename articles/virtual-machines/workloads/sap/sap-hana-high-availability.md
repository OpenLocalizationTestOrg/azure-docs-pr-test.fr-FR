---
title: "aaaHigh disponibilité de SAP HANA sur Azure des Machines virtuelles (VM) | Documents Microsoft"
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
ms.openlocfilehash: dcb9bb70594f9d97f8a888cec76300bcbe0bf1ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="high-availability-of-sap-hana-on-azure-virtual-machines-vms"></a><span data-ttu-id="93b8c-103">Haute disponibilité de SAP HANA sur des machines virtuelles Azure</span><span class="sxs-lookup"><span data-stu-id="93b8c-103">High Availability of SAP HANA on Azure Virtual Machines (VMs)</span></span>

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

[hana-ha-guide-replication]:sap-hana-high-availability.md#14c19f65-b5aa-4856-9594-b81c7e4df73d
[hana-ha-guide-shared-storage]:sap-hana-high-availability.md#498de331-fa04-490b-997c-b078de457c9d

[suse-hana-ha-guide]:https://www.suse.com/docrep/documents/ir8w88iwu7/suse_linux_enterprise_server_for_sap_applications_12_sp1.pdf
[sap-swcenter]:https://launchpad.support.sap.com/#/softwarecenter
[template-multisid-db]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image-multi-sid-db%2Fazuredeploy.json
[template-converged]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image-converged%2Fazuredeploy.json

<span data-ttu-id="93b8c-113">Locale, vous pouvez utiliser la réplication du système soit HANA ou utiliser un stockage partagé tooestablish haute disponibilité pour SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="93b8c-113">On-premises, you can use either HANA System Replication or use shared storage tooestablish high availability for SAP HANA.</span></span>
<span data-ttu-id="93b8c-114">Azure ne prend en charge actuellement que la configuration de la réplication système HANA.</span><span class="sxs-lookup"><span data-stu-id="93b8c-114">We currently only support setting up HANA System Replication on Azure.</span></span> <span data-ttu-id="93b8c-115">La réplication SAP HANA se compose d’un nœud principal et d’au moins un nœud subordonné.</span><span class="sxs-lookup"><span data-stu-id="93b8c-115">SAP HANA Replication consists of one master node and at least one slave node.</span></span> <span data-ttu-id="93b8c-116">Toohello de modifications de données sur le nœud principal de hello sont répliquées de nœuds d’esclave toohello synchrone ou asynchrone.</span><span class="sxs-lookup"><span data-stu-id="93b8c-116">Changes toohello data on hello master node are replicated toohello slave nodes synchronously or asynchronously.</span></span>

<span data-ttu-id="93b8c-117">Cet article décrit comment toodeploy hello des machines virtuelles, configurer des machines virtuelles de hello installer hello cluster framework, installer et configurer la réplication du système SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="93b8c-117">This article describes how toodeploy hello virtual machines, configure hello virtual machines, install hello cluster framework, install and configure SAP HANA System Replication.</span></span>
<span data-ttu-id="93b8c-118">Dans les configurations d’exemple hello, numéro d’instance etc. 03 commandes d’installation et HANA système ID HDB est utilisé.</span><span class="sxs-lookup"><span data-stu-id="93b8c-118">In hello example configurations, installation commands etc. instance number 03 and HANA System ID HDB is used.</span></span>

<span data-ttu-id="93b8c-119">Lire hello suivant tout d’abord les Notes SAP et livres</span><span class="sxs-lookup"><span data-stu-id="93b8c-119">Read hello following SAP Notes and papers first</span></span>

* <span data-ttu-id="93b8c-120">Note SAP [1928533], qui contient :</span><span class="sxs-lookup"><span data-stu-id="93b8c-120">SAP Note [1928533], which has:</span></span>
  * <span data-ttu-id="93b8c-121">Liste des tailles de machine virtuelle Azure qui sont pris en charge pour le déploiement de hello de logiciels SAP</span><span class="sxs-lookup"><span data-stu-id="93b8c-121">List of Azure VM sizes that are supported for hello deployment of SAP software</span></span>
  * <span data-ttu-id="93b8c-122">des informations importantes sur la capacité en fonction de la taille des machines virtuelles Azure</span><span class="sxs-lookup"><span data-stu-id="93b8c-122">Important capacity information for Azure VM sizes</span></span>
  * <span data-ttu-id="93b8c-123">les logiciels SAP pris en charge et les combinaisons entre système d’exploitation et base de données</span><span class="sxs-lookup"><span data-stu-id="93b8c-123">Supported SAP software, and operating system (OS) and database combinations</span></span>
  * <span data-ttu-id="93b8c-124">la version du noyau SAP requise pour Windows et Linux sur Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="93b8c-124">Required SAP kernel version for Windows and Linux on Microsoft Azure</span></span>
* <span data-ttu-id="93b8c-125">La note SAP [2015553] répertorie les conditions préalables au déploiement de logiciels SAP pris en charge par SAP sur Azure.</span><span class="sxs-lookup"><span data-stu-id="93b8c-125">SAP Note [2015553] lists prerequisites for SAP-supported SAP software deployments in Azure.</span></span>
* <span data-ttu-id="93b8c-126">La note SAP [2205917] contient des paramètres de système d’exploitation recommandés pour SUSE Linux Enterprise Server pour les applications SAP</span><span class="sxs-lookup"><span data-stu-id="93b8c-126">SAP Note [2205917] has recommended OS settings for SUSE Linux Enterprise Server for SAP Applications</span></span>
* <span data-ttu-id="93b8c-127">La note SAP [1944799] contient des instructions SAP HANA pour SUSE Linux Enterprise Server pour les applications SAP</span><span class="sxs-lookup"><span data-stu-id="93b8c-127">SAP Note [1944799] has SAP HANA Guidelines for SUSE Linux Enterprise Server for SAP Applications</span></span>
* <span data-ttu-id="93b8c-128">La note SAP [2178632] contient des informations détaillées sur toutes les métriques de surveillance rapportées pour SAP sur Azure.</span><span class="sxs-lookup"><span data-stu-id="93b8c-128">SAP Note [2178632] has detailed information about all monitoring metrics reported for SAP in Azure.</span></span>
* <span data-ttu-id="93b8c-129">La Note SAP [2191498] hello requise version de l’Agent hôte SAP pour Linux dans Azure.</span><span class="sxs-lookup"><span data-stu-id="93b8c-129">SAP Note [2191498] has hello required SAP Host Agent version for Linux in Azure.</span></span>
* <span data-ttu-id="93b8c-130">La note SAP [2243692] contient des informations sur les licences SAP sur Linux dans Azure.</span><span class="sxs-lookup"><span data-stu-id="93b8c-130">SAP Note [2243692] has information about SAP licensing on Linux in Azure.</span></span>
* <span data-ttu-id="93b8c-131">La note SAP [1984787] contient des informations sur SUSE Linux Enterprise Server 12.</span><span class="sxs-lookup"><span data-stu-id="93b8c-131">SAP Note [1984787] has general information about SUSE Linux Enterprise Server 12.</span></span>
* <span data-ttu-id="93b8c-132">La Note SAP [1999351] a des informations de dépannage supplémentaires pour hello améliorée Extension de surveillance Azure pour SAP.</span><span class="sxs-lookup"><span data-stu-id="93b8c-132">SAP Note [1999351] has additional troubleshooting information for hello Azure Enhanced Monitoring Extension for SAP.</span></span>
* <span data-ttu-id="93b8c-133">Le [WIKI de la communauté SAP](https://wiki.scn.sap.com/wiki/display/HOME/SAPonLinuxNotes) contient toutes les notes SAP requises pour Linux.</span><span class="sxs-lookup"><span data-stu-id="93b8c-133">[SAP Community WIKI](https://wiki.scn.sap.com/wiki/display/HOME/SAPonLinuxNotes) has all required SAP Notes for Linux.</span></span>
* <span data-ttu-id="93b8c-134">[Planification et implémentation de Machines virtuelles Azure pour SAP sur Linux][planning-guide]</span><span class="sxs-lookup"><span data-stu-id="93b8c-134">[Azure Virtual Machines planning and implementation for SAP on Linux][planning-guide]</span></span>
* <span data-ttu-id="93b8c-135">[Déploiement de Machines virtuelles Azure pour SAP sur Linux (cet article)][deployment-guide]</span><span class="sxs-lookup"><span data-stu-id="93b8c-135">[Azure Virtual Machines deployment for SAP on Linux (this article)][deployment-guide]</span></span>
* <span data-ttu-id="93b8c-136">[Déploiement SGBD de Machines virtuelles Azure pour SAP sur Linux][dbms-guide]</span><span class="sxs-lookup"><span data-stu-id="93b8c-136">[Azure Virtual Machines DBMS deployment for SAP on Linux][dbms-guide]</span></span>
* <span data-ttu-id="93b8c-137">[Scénario d’optimisé de performances SAP HANA SR] [ suse-hana-ha-guide] guide de hello contient toutes les informations requises tooset, réplication du système SAP HANA en local.</span><span class="sxs-lookup"><span data-stu-id="93b8c-137">[SAP HANA SR Performance Optimized Scenario][suse-hana-ha-guide] hello guide contains all required information tooset up SAP HANA System Replication on-premises.</span></span> <span data-ttu-id="93b8c-138">Utilisez ce guide comme référence.</span><span class="sxs-lookup"><span data-stu-id="93b8c-138">Use this guide as a baseline.</span></span>

## <a name="deploying-linux"></a><span data-ttu-id="93b8c-139">Déploiement de Linux</span><span class="sxs-lookup"><span data-stu-id="93b8c-139">Deploying Linux</span></span>

<span data-ttu-id="93b8c-140">l’agent de ressource Hello pour SAP HANA est inclus dans SUSE Linux Enterprise Server pour les Applications SAP.</span><span class="sxs-lookup"><span data-stu-id="93b8c-140">hello resource agent for SAP HANA is included in SUSE Linux Enterprise Server for SAP Applications.</span></span>
<span data-ttu-id="93b8c-141">Bonjour Azure Marketplace contient une image pour SUSE Linux Enterprise Server 12 d’Applications SAP avec BYOS (apportez votre propre abonnement) que vous pouvez utiliser les nouveaux ordinateurs virtuels de toodeploy.</span><span class="sxs-lookup"><span data-stu-id="93b8c-141">hello Azure Marketplace contains an image for SUSE Linux Enterprise Server for SAP Applications 12 with BYOS (Bring Your Own Subscription) that you can use toodeploy new virtual machines.</span></span>

### <a name="manual-deployment"></a><span data-ttu-id="93b8c-142">Déploiement manuel</span><span class="sxs-lookup"><span data-stu-id="93b8c-142">Manual Deployment</span></span>

1. <span data-ttu-id="93b8c-143">Création d’un groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="93b8c-143">Create a Resource Group</span></span>
1. <span data-ttu-id="93b8c-144">Création d'un réseau virtuel</span><span class="sxs-lookup"><span data-stu-id="93b8c-144">Create a Virtual Network</span></span>
1. <span data-ttu-id="93b8c-145">Créer deux comptes de stockage</span><span class="sxs-lookup"><span data-stu-id="93b8c-145">Create two Storage Accounts</span></span>
1. <span data-ttu-id="93b8c-146">Créer un groupe à haute disponibilité</span><span class="sxs-lookup"><span data-stu-id="93b8c-146">Create an Availability Set</span></span>  
   <span data-ttu-id="93b8c-147">Définir un domaine de mise à jour maximal</span><span class="sxs-lookup"><span data-stu-id="93b8c-147">Set max update domain</span></span>
1. <span data-ttu-id="93b8c-148">Créer un équilibrage de charge (interne)</span><span class="sxs-lookup"><span data-stu-id="93b8c-148">Create a Load Balancer (internal)</span></span>  
   <span data-ttu-id="93b8c-149">Sélectionner le réseau virtuel de l’étape précédente</span><span class="sxs-lookup"><span data-stu-id="93b8c-149">Select VNET of step above</span></span>
1. <span data-ttu-id="93b8c-150">Créer la machine virtuelle 1</span><span class="sxs-lookup"><span data-stu-id="93b8c-150">Create Virtual Machine 1</span></span>  
   <span data-ttu-id="93b8c-151">https://portal.azure.com/#create/suse-byos.sles-for-sap-byos12-sp1</span><span class="sxs-lookup"><span data-stu-id="93b8c-151">https://portal.azure.com/#create/suse-byos.sles-for-sap-byos12-sp1</span></span>  
   <span data-ttu-id="93b8c-152">SLES For SAP Applications 12 SP1 (BYOS)</span><span class="sxs-lookup"><span data-stu-id="93b8c-152">SLES For SAP Applications 12 SP1 (BYOS)</span></span>  
   <span data-ttu-id="93b8c-153">Sélectionner le compte de stockage 1</span><span class="sxs-lookup"><span data-stu-id="93b8c-153">Select Storage Account 1</span></span>  
   <span data-ttu-id="93b8c-154">Sélectionner le groupe à haute disponibilité</span><span class="sxs-lookup"><span data-stu-id="93b8c-154">Select Availability Set</span></span>  
1. <span data-ttu-id="93b8c-155">Créer la machine virtuelle 2</span><span class="sxs-lookup"><span data-stu-id="93b8c-155">Create Virtual Machine 2</span></span>  
   <span data-ttu-id="93b8c-156">https://portal.azure.com/#create/suse-byos.sles-for-sap-byos12-sp1</span><span class="sxs-lookup"><span data-stu-id="93b8c-156">https://portal.azure.com/#create/suse-byos.sles-for-sap-byos12-sp1</span></span>  
   <span data-ttu-id="93b8c-157">SLES For SAP Applications 12 SP1 (BYOS)</span><span class="sxs-lookup"><span data-stu-id="93b8c-157">SLES For SAP Applications 12 SP1 (BYOS)</span></span>  
   <span data-ttu-id="93b8c-158">Sélectionner le compte de stockage 2</span><span class="sxs-lookup"><span data-stu-id="93b8c-158">Select Storage Account 2</span></span>   
   <span data-ttu-id="93b8c-159">Sélectionner le groupe à haute disponibilité</span><span class="sxs-lookup"><span data-stu-id="93b8c-159">Select Availability Set</span></span>  
1. <span data-ttu-id="93b8c-160">Ajouter des disques de données</span><span class="sxs-lookup"><span data-stu-id="93b8c-160">Add Data Disks</span></span>
1. <span data-ttu-id="93b8c-161">Configurer l’équilibrage de charge hello</span><span class="sxs-lookup"><span data-stu-id="93b8c-161">Configure hello load balancer</span></span>
    1. <span data-ttu-id="93b8c-162">Créer un pool d’adresse IP frontal</span><span class="sxs-lookup"><span data-stu-id="93b8c-162">Create a frontend IP pool</span></span>
        1. <span data-ttu-id="93b8c-163">Ouvrez hello l’équilibrage de charge, sélectionnez le pool d’adresses IP de serveur frontal et cliquez sur Ajouter</span><span class="sxs-lookup"><span data-stu-id="93b8c-163">Open hello load balancer, select frontend IP pool and click Add</span></span>
        1. <span data-ttu-id="93b8c-164">Entrez le nom hello de hello nouveau serveur frontal pool IP (par exemple hana-frontend)</span><span class="sxs-lookup"><span data-stu-id="93b8c-164">Enter hello name of hello new frontend IP pool (for example hana-frontend)</span></span>
       1. <span data-ttu-id="93b8c-165">Cliquez sur OK</span><span class="sxs-lookup"><span data-stu-id="93b8c-165">Click OK</span></span>
        1. <span data-ttu-id="93b8c-166">Une fois le nouveau pool d’IP frontale hello est créé, notez son adresse IP</span><span class="sxs-lookup"><span data-stu-id="93b8c-166">After hello new frontend IP pool is created, write down its IP address</span></span>
    1. <span data-ttu-id="93b8c-167">Créer un pool principal</span><span class="sxs-lookup"><span data-stu-id="93b8c-167">Create a backend pool</span></span>
        1. <span data-ttu-id="93b8c-168">Ouvrez l’équilibrage de charge hello, pools principaux, cliquez sur Ajouter</span><span class="sxs-lookup"><span data-stu-id="93b8c-168">Open hello load balancer, select backend pools and click Add</span></span>
        1. <span data-ttu-id="93b8c-169">Entrez hello nom hello nouveau serveur principal du pool de (par exemple hana principal)</span><span class="sxs-lookup"><span data-stu-id="93b8c-169">Enter hello name of hello new backend pool (for example hana-backend)</span></span>
        1. <span data-ttu-id="93b8c-170">Cliquer sur Ajouter une machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="93b8c-170">Click Add a virtual machine</span></span>
        1. <span data-ttu-id="93b8c-171">Sélectionnez hello que vous avez créé précédemment à haute disponibilité</span><span class="sxs-lookup"><span data-stu-id="93b8c-171">Select hello Availability Set you created earlier</span></span>
        1. <span data-ttu-id="93b8c-172">Sélectionner des machines virtuelles hello du cluster de SAP HANA hello</span><span class="sxs-lookup"><span data-stu-id="93b8c-172">Select hello virtual machines of hello SAP HANA cluster</span></span>
        1. <span data-ttu-id="93b8c-173">Cliquez sur OK</span><span class="sxs-lookup"><span data-stu-id="93b8c-173">Click OK</span></span>
    1. <span data-ttu-id="93b8c-174">Créer une sonde d’intégrité</span><span class="sxs-lookup"><span data-stu-id="93b8c-174">Create a health probe</span></span>
       1. <span data-ttu-id="93b8c-175">Ouvrez l’équilibrage de charge hello, sondes d’intégrité, cliquez sur Ajouter</span><span class="sxs-lookup"><span data-stu-id="93b8c-175">Open hello load balancer, select health probes and click Add</span></span>
        1. <span data-ttu-id="93b8c-176">Entrez le nom hello de sonde d’intégrité nouvelle hello (par exemple hana hp)</span><span class="sxs-lookup"><span data-stu-id="93b8c-176">Enter hello name of hello new health probe (for example hana-hp)</span></span>
        1. <span data-ttu-id="93b8c-177">Sélectionner le protocole TCP et le port 625**03**, et conserver un intervalle de 5 et un seuil de défaillance de 2</span><span class="sxs-lookup"><span data-stu-id="93b8c-177">Select TCP as protocol, port 625**03**, keep Interval 5 and Unhealthy threshold 2</span></span>
        1. <span data-ttu-id="93b8c-178">Click OK</span><span class="sxs-lookup"><span data-stu-id="93b8c-178">Click OK</span></span>
    1. <span data-ttu-id="93b8c-179">Créer des règles d’équilibrage de charge</span><span class="sxs-lookup"><span data-stu-id="93b8c-179">Create load balancing rules</span></span>
        1. <span data-ttu-id="93b8c-180">Ouvrez l’équilibrage de charge hello, règles d’équilibrage de charge, cliquez sur Ajouter</span><span class="sxs-lookup"><span data-stu-id="93b8c-180">Open hello load balancer, select load balancing rules and click Add</span></span>
        1. <span data-ttu-id="93b8c-181">Entrez le nom hello de nouvelle règle d’équilibrage de charge hello (par exemple hana-lb-3**03**15)</span><span class="sxs-lookup"><span data-stu-id="93b8c-181">Enter hello name of hello new load balancer rule (for example hana-lb-3**03**15)</span></span>
        1. <span data-ttu-id="93b8c-182">Adresse IP de serveur frontal sélectionnez hello, pool principal et l’intégrité de sonde vous avez créé précédemment (par exemple hana-frontend)</span><span class="sxs-lookup"><span data-stu-id="93b8c-182">Select hello frontend IP address, backend pool and health probe you created earlier (for example hana-frontend)</span></span>
        1. <span data-ttu-id="93b8c-183">Conserver le protocole TCP et choisir le port 3**03**15</span><span class="sxs-lookup"><span data-stu-id="93b8c-183">Keep protocol TCP, enter port 3**03**15</span></span>
        1. <span data-ttu-id="93b8c-184">Augmenter le délai d’inactivité too30 minutes</span><span class="sxs-lookup"><span data-stu-id="93b8c-184">Increase idle timeout too30 minutes</span></span>
       1. <span data-ttu-id="93b8c-185">**Assurez-vous que tooenable IP flottante**</span><span class="sxs-lookup"><span data-stu-id="93b8c-185">**Make sure tooenable Floating IP**</span></span>
        1. <span data-ttu-id="93b8c-186">Cliquez sur OK</span><span class="sxs-lookup"><span data-stu-id="93b8c-186">Click OK</span></span>
        1. <span data-ttu-id="93b8c-187">Répétez les étapes de hello ci-dessus pour le port 3**03**17</span><span class="sxs-lookup"><span data-stu-id="93b8c-187">Repeat hello steps above for port 3**03**17</span></span>

### <a name="deploy-with-template"></a><span data-ttu-id="93b8c-188">Déployer avec un modèle</span><span class="sxs-lookup"><span data-stu-id="93b8c-188">Deploy with template</span></span>
<span data-ttu-id="93b8c-189">Vous pouvez utiliser un des modèles de démarrage rapide de hello sur github toodeploy toutes les ressources requises.</span><span class="sxs-lookup"><span data-stu-id="93b8c-189">You can use one of hello quick start templates on github toodeploy all required resources.</span></span> <span data-ttu-id="93b8c-190">modèle de Hello déploie les machines virtuelles de hello, équilibrage de charge hello, haute disponibilité etc.. Suivez ces modèles de hello toodeploy comme suit :</span><span class="sxs-lookup"><span data-stu-id="93b8c-190">hello template deploys hello virtual machines, hello load balancer, availability set etc. Follow these steps toodeploy hello template:</span></span>

1. <span data-ttu-id="93b8c-191">Ouvrez hello [modèle de base de données] [ template-multisid-db] ou hello [convergé modèle] [ template-converged] sur hello Azure Portal modèle de base de données hello crée uniquement hello règles d’équilibrage de charge pour une base de données alors que le modèle de convergé hello crée également hello règles d’équilibrage de charge pour un ASCS/SCS et une instance ERS (Linux uniquement).</span><span class="sxs-lookup"><span data-stu-id="93b8c-191">Open hello [database template][template-multisid-db] or hello [converged template][template-converged] on hello Azure Portal hello database template only creates hello load-balancing rules for a database whereas hello converged template also creates hello load-balancing rules for an ASCS/SCS and ERS (Linux only) instance.</span></span> <span data-ttu-id="93b8c-192">Si vous prévoyez d’un système SAP NetWeaver en fonction de tooinstall et que vous souhaitez également tooinstall hello ASCS/SCS d’instance sur hello mêmes ordinateurs, utilisez hello [convergé modèle][template-converged].</span><span class="sxs-lookup"><span data-stu-id="93b8c-192">If you plan tooinstall an SAP NetWeaver based system and you also want tooinstall hello ASCS/SCS instance on hello same machines, use hello [converged template][template-converged].</span></span>
1. <span data-ttu-id="93b8c-193">Entrez les paramètres suivants de hello</span><span class="sxs-lookup"><span data-stu-id="93b8c-193">Enter hello following parameters</span></span>
    1. <span data-ttu-id="93b8c-194">ID du système SAP</span><span class="sxs-lookup"><span data-stu-id="93b8c-194">Sap System Id</span></span>  
       <span data-ttu-id="93b8c-195">Entrez le système hello SAP Id Hello système SAP tooinstall.</span><span class="sxs-lookup"><span data-stu-id="93b8c-195">Enter hello SAP system Id of hello SAP system you want tooinstall.</span></span> <span data-ttu-id="93b8c-196">Hello Id sera utilisé en tant que préfixe pour les ressources hello qui sont déployés.</span><span class="sxs-lookup"><span data-stu-id="93b8c-196">hello Id will be used as a prefix for hello resources that are deployed.</span></span>
    1. <span data-ttu-id="93b8c-197">Type de la pile (applicable uniquement si vous utilisez le modèle de convergé hello)</span><span class="sxs-lookup"><span data-stu-id="93b8c-197">Stack Type (only applicable if you use hello converged template)</span></span>  
       <span data-ttu-id="93b8c-198">Sélectionnez le type de pile hello SAP NetWeaver</span><span class="sxs-lookup"><span data-stu-id="93b8c-198">Select hello SAP NetWeaver stack type</span></span>
    1. <span data-ttu-id="93b8c-199">Type de système d’exploitation</span><span class="sxs-lookup"><span data-stu-id="93b8c-199">Os Type</span></span>  
       <span data-ttu-id="93b8c-200">Sélectionnez une des distributions de Linux hello.</span><span class="sxs-lookup"><span data-stu-id="93b8c-200">Select one of hello Linux distributions.</span></span> <span data-ttu-id="93b8c-201">Dans cet exemple, sélectionnez SLES 12 BYOS</span><span class="sxs-lookup"><span data-stu-id="93b8c-201">For this example, select SLES 12 BYOS</span></span>
    1. <span data-ttu-id="93b8c-202">Type de base de données</span><span class="sxs-lookup"><span data-stu-id="93b8c-202">Db Type</span></span>  
       <span data-ttu-id="93b8c-203">Sélectionnez HANA</span><span class="sxs-lookup"><span data-stu-id="93b8c-203">Select HANA</span></span>
    1. <span data-ttu-id="93b8c-204">Taille du système SAP</span><span class="sxs-lookup"><span data-stu-id="93b8c-204">Sap System Size</span></span>  
       <span data-ttu-id="93b8c-205">quantité Hello du nouveau système SAP hello fournissent.</span><span class="sxs-lookup"><span data-stu-id="93b8c-205">hello amount of SAPS hello new system will provide.</span></span> <span data-ttu-id="93b8c-206">Si vous n’êtes pas sûr du système de hello SAP combien nécessitera, veuillez demander à votre partenaire technologique SAP ou l’intégrateur système</span><span class="sxs-lookup"><span data-stu-id="93b8c-206">If you are not sure how many SAPS hello system will require, please ask your SAP Technology Partner or System Integrator</span></span>
    1. <span data-ttu-id="93b8c-207">Disponibilité du système</span><span class="sxs-lookup"><span data-stu-id="93b8c-207">System Availability</span></span>  
       <span data-ttu-id="93b8c-208">Sélectionnez la haute disponibilité (HA).</span><span class="sxs-lookup"><span data-stu-id="93b8c-208">Select HA</span></span>
    1. <span data-ttu-id="93b8c-209">Nom d’utilisateur et mot de passe d’administrateur</span><span class="sxs-lookup"><span data-stu-id="93b8c-209">Admin Username and Admin Password</span></span>  
       <span data-ttu-id="93b8c-210">Création d’un utilisateur qui peut être utilisé toolog sur l’ordinateur de toohello.</span><span class="sxs-lookup"><span data-stu-id="93b8c-210">A new user is created that can be used toolog on toohello machine.</span></span>
    1. <span data-ttu-id="93b8c-211">Sous-réseau nouveau ou existant</span><span class="sxs-lookup"><span data-stu-id="93b8c-211">New Or Existing Subnet</span></span>  
       <span data-ttu-id="93b8c-212">Détermine s’il faut créer un réseau virtuel et un sous-réseau, ou utiliser un sous-réseau existant.</span><span class="sxs-lookup"><span data-stu-id="93b8c-212">Determines whether a new virtual network and subnet should be created or an existing subnet should be used.</span></span> <span data-ttu-id="93b8c-213">Si vous disposez déjà d’un réseau virtuel qui est le réseau local de tooyour connecté, sélectionnez existante.</span><span class="sxs-lookup"><span data-stu-id="93b8c-213">If you already have a virtual network that is connected tooyour on-premises network, select existing.</span></span>
    1. <span data-ttu-id="93b8c-214">ID du sous-réseau</span><span class="sxs-lookup"><span data-stu-id="93b8c-214">Subnet Id</span></span>  
    <span data-ttu-id="93b8c-215">ID de Hello d’ordinateurs virtuels hello sous-réseau toowhich hello doit être connecté à.</span><span class="sxs-lookup"><span data-stu-id="93b8c-215">hello ID of hello subnet toowhich hello virtual machines should be connected to.</span></span> <span data-ttu-id="93b8c-216">Sélectionnez sous-réseau hello de votre VPN ou Express Route réseau virtuel tooconnect hello tooyour local réseau d’ordinateurs virtuels.</span><span class="sxs-lookup"><span data-stu-id="93b8c-216">Select hello subnet of your VPN or Express Route virtual network tooconnect hello virtual machine tooyour on-premises network.</span></span> <span data-ttu-id="93b8c-217">ID de Hello ressemble généralement à /subscriptions/`<subscription id`> /resourceGroups/`<resource group name`> /providers/Microsoft.Network/virtualNetworks/`<virtual network name`> /subnets/`<subnet name`></span><span class="sxs-lookup"><span data-stu-id="93b8c-217">hello ID usually looks like /subscriptions/`<subscription id`>/resourceGroups/`<resource group name`>/providers/Microsoft.Network/virtualNetworks/`<virtual network name`>/subnets/`<subnet name`></span></span>

## <a name="setting-up-linux-ha"></a><span data-ttu-id="93b8c-218">Configuration de la haute disponibilité Linux</span><span class="sxs-lookup"><span data-stu-id="93b8c-218">Setting up Linux HA</span></span>

<span data-ttu-id="93b8c-219">Hello éléments suivants est préfixé avec l’option [A] - les nœuds tooall applicable, [1] - applicable uniquement toonode 1 ou [2] - le toonode s’applique seulement 2.</span><span class="sxs-lookup"><span data-stu-id="93b8c-219">hello following items are prefixed with either [A] - applicable tooall nodes, [1] - only applicable toonode 1 or [2] - only applicable toonode 2.</span></span>

1. <span data-ttu-id="93b8c-220">[A] SLES pour SAP BYOS uniquement - inscrire les SLES toobe toouse en mesure de hello des référentiels</span><span class="sxs-lookup"><span data-stu-id="93b8c-220">[A] SLES for SAP BYOS only - Register SLES toobe able toouse hello repositories</span></span>
1. <span data-ttu-id="93b8c-221">[A] SLES for SAP BYOS uniquement : ajouter un module de cloud public</span><span class="sxs-lookup"><span data-stu-id="93b8c-221">[A] SLES for SAP BYOS only - Add public-cloud module</span></span>
1. <span data-ttu-id="93b8c-222">[A] Mettre à jour SLES</span><span class="sxs-lookup"><span data-stu-id="93b8c-222">[A] Update SLES</span></span>
    ```bash
    sudo zypper update

    ```

1. <span data-ttu-id="93b8c-223">[1] Activer l’accès SSH</span><span class="sxs-lookup"><span data-stu-id="93b8c-223">[1] Enable ssh access</span></span>
    ```bash
    sudo ssh-keygen -tdsa
    
    # Enter file in which toosave hello key (/root/.ssh/id_dsa): -> ENTER
    # Enter passphrase (empty for no passphrase): -> ENTER
    # Enter same passphrase again: -> ENTER
    
    # copy hello public key
    sudo cat /root/.ssh/id_dsa.pub
    ```

2. <span data-ttu-id="93b8c-224">[2] Activer l’accès SSH</span><span class="sxs-lookup"><span data-stu-id="93b8c-224">[2] Enable ssh access</span></span>
    ```bash
    sudo ssh-keygen -tdsa

    # insert hello public key you copied in hello last step into hello authorized keys file on hello second server
    sudo vi /root/.ssh/authorized_keys
    
    # Enter file in which toosave hello key (/root/.ssh/id_dsa): -> ENTER
    # Enter passphrase (empty for no passphrase): -> ENTER
    # Enter same passphrase again: -> ENTER
    
    # copy hello public key    
    sudo cat /root/.ssh/id_dsa.pub
    ```

1. <span data-ttu-id="93b8c-225">[1] Activer l’accès SSH</span><span class="sxs-lookup"><span data-stu-id="93b8c-225">[1] Enable ssh access</span></span>
    ```bash
    # insert hello public key you copied in hello last step into hello authorized keys file on hello first server
    sudo vi /root/.ssh/authorized_keys
    
    ```

1. <span data-ttu-id="93b8c-226">[A] installer l’extension de haute disponibilité</span><span class="sxs-lookup"><span data-stu-id="93b8c-226">[A] Install HA extension</span></span>
    ```bash
    sudo zypper install sle-ha-release fence-agents
    
    ```

1. <span data-ttu-id="93b8c-227">[A] Configurer la disposition du disque</span><span class="sxs-lookup"><span data-stu-id="93b8c-227">[A] Setup disk layout</span></span>
    1. <span data-ttu-id="93b8c-228">LVM</span><span class="sxs-lookup"><span data-stu-id="93b8c-228">LVM</span></span>  
    <span data-ttu-id="93b8c-229">Nous déconseillons généralement de toouse Gestionnaire de volume logique pour les volumes qui stockent les données et fichiers journaux.</span><span class="sxs-lookup"><span data-stu-id="93b8c-229">We generally recommend toouse LVM for volumes that store data and log files.</span></span> <span data-ttu-id="93b8c-230">exemple Hello ci-dessous suppose que les ordinateurs virtuels hello avez quatre disques de données attachés doivent être utilisé toocreate deux volumes.</span><span class="sxs-lookup"><span data-stu-id="93b8c-230">hello example below assumes that hello virtual machines have four data disks attached that should be used toocreate two volumes.</span></span>
        * <span data-ttu-id="93b8c-231">Créer des volumes physiques de tous les disques que vous souhaitez toouse.</span><span class="sxs-lookup"><span data-stu-id="93b8c-231">Create physical volumes for all disks that you want toouse.</span></span>
    <pre><code>
    sudo pvcreate /dev/sdc
    sudo pvcreate /dev/sdd
    sudo pvcreate /dev/sde
    sudo pvcreate /dev/sdf
    </code></pre>
        * <span data-ttu-id="93b8c-232">Créer un groupe de volumes pour les fichiers de données hello, un groupe de volumes pour les fichiers de journaux hello et un pour le répertoire partagé de hello de SAP HANA</span><span class="sxs-lookup"><span data-stu-id="93b8c-232">Create a volume group for hello data files, one volume group for hello log files and one for hello shared directory of SAP HANA</span></span>
    <pre><code>
    sudo vgcreate vg_hana_data /dev/sdc /dev/sdd
    sudo vgcreate vg_hana_log /dev/sde
    sudo vgcreate vg_hana_shared /dev/sdf
    </code></pre>
        * <span data-ttu-id="93b8c-233">Créer des volumes logiques hello</span><span class="sxs-lookup"><span data-stu-id="93b8c-233">Create hello logical volumes</span></span>
    <pre><code>
    sudo lvcreate -l 100%FREE -n hana_data vg_hana_data
    sudo lvcreate -l 100%FREE -n hana_log vg_hana_log
    sudo lvcreate -l 100%FREE -n hana_shared vg_hana_shared
    sudo mkfs.xfs /dev/vg_hana_data/hana_data
    sudo mkfs.xfs /dev/vg_hana_log/hana_log
    sudo mkfs.xfs /dev/vg_hana_shared/hana_shared
    </code></pre>
        * <span data-ttu-id="93b8c-234">Créer des répertoires de montage hello et copiez hello UUID de tous les volumes logiques</span><span class="sxs-lookup"><span data-stu-id="93b8c-234">Create hello mount directories and copy hello UUID of all logical volumes</span></span>
    <pre><code>
    sudo mkdir -p /hana/data
    sudo mkdir -p /hana/log
    sudo mkdir -p /hana/shared
    # write down hello id of /dev/vg_hana_data/hana_data, /dev/vg_hana_log/hana_log and /dev/vg_hana_shared/hana_shared
    sudo blkid
    </code></pre>
        * <span data-ttu-id="93b8c-235">Créer des volumes logiques trois entrées fstab pour hello</span><span class="sxs-lookup"><span data-stu-id="93b8c-235">Create fstab entries for hello three logical volumes</span></span>
    <pre><code>
    sudo vi /etc/fstab
    </code></pre>
    <span data-ttu-id="93b8c-236">Insérer cette ligne trop/etc/fstab</span><span class="sxs-lookup"><span data-stu-id="93b8c-236">Insert this line too/etc/fstab</span></span>
    <pre><code>
    /dev/disk/by-uuid/<b>&lt;UUID of /dev/vg_hana_data/hana_data&gt;</b> /hana/data xfs  defaults,nofail  0  2
    /dev/disk/by-uuid/<b>&lt;UUID of /dev/vg_hana_log/hana_log&gt;</b> /hana/log xfs  defaults,nofail  0  2
    /dev/disk/by-uuid/<b>&lt;UUID of /dev/vg_hana_shared/hana_shared&gt;</b> /hana/shared xfs  defaults,nofail  0  2
    </code></pre>
        * <span data-ttu-id="93b8c-237">Monter des volumes de nouveau hello</span><span class="sxs-lookup"><span data-stu-id="93b8c-237">Mount hello new volumes</span></span>
    <pre><code>
    sudo mount -a
    </code></pre>
    1. <span data-ttu-id="93b8c-238">Disques simples</span><span class="sxs-lookup"><span data-stu-id="93b8c-238">Plain Disks</span></span>  
       <span data-ttu-id="93b8c-239">Pour les petits systèmes ou les systèmes de démonstration, vous pouvez placer vos données et fichiers journaux HANA sur un disque.</span><span class="sxs-lookup"><span data-stu-id="93b8c-239">For small or demo systems, you can place your HANA data and log files on one disk.</span></span> <span data-ttu-id="93b8c-240">Hello commandes suivantes créent une partition sur /dev/sdc puis formater xfs.</span><span class="sxs-lookup"><span data-stu-id="93b8c-240">hello following commands create a partition on /dev/sdc and format it with xfs.</span></span>
    ```bash
    sudo fdisk /dev/sdc
    sudo mkfs.xfs /dev/sdc1
    
    # <a name="write-down-hello-id-of-devsdc1"></a><span data-ttu-id="93b8c-241">Notez les id hello de /dev/sdc1</span><span class="sxs-lookup"><span data-stu-id="93b8c-241">write down hello id of /dev/sdc1</span></span>
    <span data-ttu-id="93b8c-242">sudo /sbin/blkid  sudo vi /etc/fstab</span><span class="sxs-lookup"><span data-stu-id="93b8c-242">sudo /sbin/blkid  sudo vi /etc/fstab</span></span>
    ```

    Insert this line too/etc/fstab
    <pre><code>
    /dev/disk/by-uuid/<b>&lt;UUID&gt;</b> /hana xfs  defaults,nofail  0  2
    </code></pre>

    Create hello target directory and mount hello disk.

    ```bash
    sudo mkdir /hana
    sudo mount -a
    ```

1. <span data-ttu-id="93b8c-243">[A] Configurer la résolution de nom d’hôte pour tous les hôtes</span><span class="sxs-lookup"><span data-stu-id="93b8c-243">[A] Setup host name resolution for all hosts</span></span>  
    <span data-ttu-id="93b8c-244">Vous pouvez utiliser un serveur DNS ou modifier/etc/hosts de hello sur tous les nœuds.</span><span class="sxs-lookup"><span data-stu-id="93b8c-244">You can either use a DNS server or modify hello /etc/hosts on all nodes.</span></span> <span data-ttu-id="93b8c-245">Cet exemple montre comment toouse hello les fichier/etc/hosts.</span><span class="sxs-lookup"><span data-stu-id="93b8c-245">This example shows how toouse hello /etc/hosts file.</span></span>
   <span data-ttu-id="93b8c-246">Remplacez l’adresse IP de hello et un nom d’hôte hello Bonjour suivant les commandes</span><span class="sxs-lookup"><span data-stu-id="93b8c-246">Replace hello IP address and hello hostname in hello following commands</span></span>
    ```bash
    sudo vi /etc/hosts
    ```
    <span data-ttu-id="93b8c-247">Insérez hello suivant lignes trop/etc/hosts.</span><span class="sxs-lookup"><span data-stu-id="93b8c-247">Insert hello following lines too/etc/hosts.</span></span> <span data-ttu-id="93b8c-248">Modifiez les toomatch hello IP adresse et le nom d’hôte de votre environnement</span><span class="sxs-lookup"><span data-stu-id="93b8c-248">Change hello IP address and hostname toomatch your environment</span></span>    
    
    <pre><code>
    <b>&lt;IP address of host 1&gt; &lt;hostname of host 1&gt;</b>
    <b>&lt;IP address of host 2&gt; &lt;hostname of host 2&gt;</b>
    </code></pre>

1. <span data-ttu-id="93b8c-249">[1] Installer le cluster</span><span class="sxs-lookup"><span data-stu-id="93b8c-249">[1] Install Cluster</span></span>
    ```bash
    sudo ha-cluster-init
    
    # Do you want toocontinue anyway? [y/N] -> y
    # Network address toobind too(e.g.: 192.168.1.0) [10.79.227.0] -> ENTER
    # Multicast address (e.g.: 239.x.x.x) [239.174.218.125] -> ENTER
    # Multicast port [5405] -> ENTER
    # Do you wish toouse SBD? [y/N] -> N
    # Do you wish tooconfigure an administration IP? [y/N] -> N
    ```
        
1. <span data-ttu-id="93b8c-250">[2] Ajout de nœud toocluster</span><span class="sxs-lookup"><span data-stu-id="93b8c-250">[2] Add node toocluster</span></span>
    ```bash
    sudo ha-cluster-join
        
    # WARNING: NTP is not configured toostart at system boot.
    # WARNING: No watchdog device found. If SBD is used, hello cluster will be unable toostart without a watchdog.
    # Do you want toocontinue anyway? [y/N] -> y
    # IP address or hostname of existing node (e.g.: 192.168.1.1) [] -> IP address of node 1 e.g. 10.0.0.5
    # /root/.ssh/id_dsa already exists - overwrite? [y/N] N
    ```

1. <span data-ttu-id="93b8c-251">[A] toohello de mot de passe de modification hacluster même mot de passe</span><span class="sxs-lookup"><span data-stu-id="93b8c-251">[A] Change hacluster password toohello same password</span></span>
    ```bash
    sudo passwd hacluster
    
    ```

1. <span data-ttu-id="93b8c-252">[A] configurer corosync toouse autre transport et ajouter la liste de nœuds.</span><span class="sxs-lookup"><span data-stu-id="93b8c-252">[A] Configure corosync toouse other transport and add nodelist.</span></span> <span data-ttu-id="93b8c-253">Le cluster ne fonctionnera pas dans le cas contraire.</span><span class="sxs-lookup"><span data-stu-id="93b8c-253">Cluster will not work otherwise.</span></span>
    ```bash
    sudo vi /etc/corosync/corosync.conf    
    
    ```

    <span data-ttu-id="93b8c-254">Ajoutez hello toohello contenu gras le fichier suivant.</span><span class="sxs-lookup"><span data-stu-id="93b8c-254">Add hello following bold content toohello file.</span></span>
    
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

    <span data-ttu-id="93b8c-255">Ensuite, redémarrez le service corosync hello</span><span class="sxs-lookup"><span data-stu-id="93b8c-255">Then restart hello corosync service</span></span>

    ```bash
    sudo service corosync restart
    
    ```

1. <span data-ttu-id="93b8c-256">[A] Installer les packages haute disponibilité HANA</span><span class="sxs-lookup"><span data-stu-id="93b8c-256">[A] Install HANA HA packages</span></span>  
    ```bash
    sudo zypper install SAPHanaSR
    
    ```

## <a name="installing-sap-hana"></a><span data-ttu-id="93b8c-257">Installation de SAP HANA</span><span class="sxs-lookup"><span data-stu-id="93b8c-257">Installing SAP HANA</span></span>

<span data-ttu-id="93b8c-258">Chapitre 4 Hello [SAP HANA SR performances optimisées Scenario guide] [ suse-hana-ha-guide] tooinstall réplication du système SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="93b8c-258">Follow chapter 4 of hello [SAP HANA SR Performance Optimized Scenario guide][suse-hana-ha-guide] tooinstall SAP HANA System Replication.</span></span>

1. <span data-ttu-id="93b8c-259">[A] exécuter hdblcm à partir de hello HANA DVD</span><span class="sxs-lookup"><span data-stu-id="93b8c-259">[A] Run hdblcm from hello HANA DVD</span></span>
    * <span data-ttu-id="93b8c-260">Choose installation -> 1</span><span class="sxs-lookup"><span data-stu-id="93b8c-260">Choose installation -> 1</span></span>
    * <span data-ttu-id="93b8c-261">Select additional components for installation -> 1</span><span class="sxs-lookup"><span data-stu-id="93b8c-261">Select additional components for installation -> 1</span></span>
    * <span data-ttu-id="93b8c-262">Enter Installation Path [/hana/shared]: -> ENTRÉE</span><span class="sxs-lookup"><span data-stu-id="93b8c-262">Enter Installation Path [/hana/shared]: -> ENTER</span></span>
    * <span data-ttu-id="93b8c-263">Enter Local Host Name [..]: -> ENTRÉE</span><span class="sxs-lookup"><span data-stu-id="93b8c-263">Enter Local Host Name [..]: -> ENTER</span></span>
    * <span data-ttu-id="93b8c-264">Voulez-vous que le système de toohello tooadd hôtes supplémentaires ?</span><span class="sxs-lookup"><span data-stu-id="93b8c-264">Do you want tooadd additional hosts toohello system?</span></span> <span data-ttu-id="93b8c-265">(y/n) [n] : -> ENTRÉE</span><span class="sxs-lookup"><span data-stu-id="93b8c-265">(y/n) [n]: -> ENTER</span></span>
    * <span data-ttu-id="93b8c-266">Enter SAP HANA System ID : <SID of HANA e.g. HDB></span><span class="sxs-lookup"><span data-stu-id="93b8c-266">Enter SAP HANA System ID: <SID of HANA e.g. HDB></span></span>
    * <span data-ttu-id="93b8c-267">Enter Instance Number [00] :</span><span class="sxs-lookup"><span data-stu-id="93b8c-267">Enter Instance Number [00]:</span></span>   
  <span data-ttu-id="93b8c-268">Numéro d’instance HANA.</span><span class="sxs-lookup"><span data-stu-id="93b8c-268">HANA Instance number.</span></span> <span data-ttu-id="93b8c-269">Utilisée 03 utilisé hello modèle Azure ou pour suivre l’exemple hello ci-dessus</span><span class="sxs-lookup"><span data-stu-id="93b8c-269">Use 03 if you used hello Azure Template or followed hello example above</span></span>
    * <span data-ttu-id="93b8c-270">Select Database Mode / Enter Index [1] : -> ENTRÉE</span><span class="sxs-lookup"><span data-stu-id="93b8c-270">Select Database Mode / Enter Index [1]: -> ENTER</span></span>
    * <span data-ttu-id="93b8c-271">Select System Usage / Enter Index [4] :</span><span class="sxs-lookup"><span data-stu-id="93b8c-271">Select System Usage / Enter Index [4]:</span></span>  
  <span data-ttu-id="93b8c-272">Sélectionnez le système hello d’utilisation</span><span class="sxs-lookup"><span data-stu-id="93b8c-272">Select hello system Usage</span></span>
    * <span data-ttu-id="93b8c-273">Enter Location of Data Volumes [/hana/data/HDB] : -> ENTRÉE</span><span class="sxs-lookup"><span data-stu-id="93b8c-273">Enter Location of Data Volumes [/hana/data/HDB]: -> ENTER</span></span>
    * <span data-ttu-id="93b8c-274">Enter Location of Log Volumes [/hana/log/HDB] : -> ENTRÉE</span><span class="sxs-lookup"><span data-stu-id="93b8c-274">Enter Location of Log Volumes [/hana/log/HDB]: -> ENTER</span></span>
    * <span data-ttu-id="93b8c-275">Restrict maximum memory allocation?</span><span class="sxs-lookup"><span data-stu-id="93b8c-275">Restrict maximum memory allocation?</span></span> <span data-ttu-id="93b8c-276">[n] : -> ENTRÉE</span><span class="sxs-lookup"><span data-stu-id="93b8c-276">[n]: -> ENTER</span></span>
    * <span data-ttu-id="93b8c-277">Entrez le nom d’hôte de certificat pour l’hôte '...' [...] : -> Entrée</span><span class="sxs-lookup"><span data-stu-id="93b8c-277">Enter Certificate Host Name For Host '...' [...]: -> ENTER</span></span>
    * <span data-ttu-id="93b8c-278">Enter SAP Host Agent User (sapadm) Password:</span><span class="sxs-lookup"><span data-stu-id="93b8c-278">Enter SAP Host Agent User (sapadm) Password:</span></span>
    * <span data-ttu-id="93b8c-279">Confirm SAP Host Agent User (sapadm) Password:</span><span class="sxs-lookup"><span data-stu-id="93b8c-279">Confirm SAP Host Agent User (sapadm) Password:</span></span>
    * <span data-ttu-id="93b8c-280">Enter System Administrator (hdbadm) Password:</span><span class="sxs-lookup"><span data-stu-id="93b8c-280">Enter System Administrator (hdbadm) Password:</span></span>
    * <span data-ttu-id="93b8c-281">Confirm System Administrator (hdbadm) Password:</span><span class="sxs-lookup"><span data-stu-id="93b8c-281">Confirm System Administrator (hdbadm) Password:</span></span>
    * <span data-ttu-id="93b8c-282">Enter System Administrator Home Directory [/usr/sap/HDB/home] : -> ENTRÉE</span><span class="sxs-lookup"><span data-stu-id="93b8c-282">Enter System Administrator Home Directory [/usr/sap/HDB/home]: -> ENTER</span></span>
    * <span data-ttu-id="93b8c-283">Enter System Administrator Login Shell [/bin/sh] : -> ENTRÉE</span><span class="sxs-lookup"><span data-stu-id="93b8c-283">Enter System Administrator Login Shell [/bin/sh]: -> ENTER</span></span>
    * <span data-ttu-id="93b8c-284">Enter System Administrator User ID [1001] : -> ENTRÉE</span><span class="sxs-lookup"><span data-stu-id="93b8c-284">Enter System Administrator User ID [1001]: -> ENTER</span></span>
    * <span data-ttu-id="93b8c-285">Enter ID of User Group (sapsys) [79] : -> ENTRÉE</span><span class="sxs-lookup"><span data-stu-id="93b8c-285">Enter ID of User Group (sapsys) [79]: -> ENTER</span></span>
    * <span data-ttu-id="93b8c-286">Enter Database User (SYSTEM) Password:</span><span class="sxs-lookup"><span data-stu-id="93b8c-286">Enter Database User (SYSTEM) Password:</span></span>
    * <span data-ttu-id="93b8c-287">Confirm Database User (SYSTEM) Password:</span><span class="sxs-lookup"><span data-stu-id="93b8c-287">Confirm Database User (SYSTEM) Password:</span></span>
    * <span data-ttu-id="93b8c-288">Restart system after machine reboot?</span><span class="sxs-lookup"><span data-stu-id="93b8c-288">Restart system after machine reboot?</span></span> <span data-ttu-id="93b8c-289">[n] : -> ENTRÉE</span><span class="sxs-lookup"><span data-stu-id="93b8c-289">[n]: -> ENTER</span></span>
    * <span data-ttu-id="93b8c-290">Voulez-vous toocontinue ?</span><span class="sxs-lookup"><span data-stu-id="93b8c-290">Do you want toocontinue?</span></span> <span data-ttu-id="93b8c-291">(y/n) :</span><span class="sxs-lookup"><span data-stu-id="93b8c-291">(y/n):</span></span>  
  <span data-ttu-id="93b8c-292">Valider hello résumé et entrez y toocontinue</span><span class="sxs-lookup"><span data-stu-id="93b8c-292">Validate hello summary and enter y toocontinue</span></span>
1. <span data-ttu-id="93b8c-293">[A] Mettre à niveau l’agent hôte SAP</span><span class="sxs-lookup"><span data-stu-id="93b8c-293">[A] Upgrade SAP Host Agent</span></span>  
  <span data-ttu-id="93b8c-294">Télécharger des archives de l’Agent hôte SAP hello plus récente à partir de hello [SAP Softwarecenter] [ sap-swcenter] et exécution hello après la commande tooupgrade hello agent.</span><span class="sxs-lookup"><span data-stu-id="93b8c-294">Download hello latest SAP Host Agent archive from hello [SAP Softwarecenter][sap-swcenter] and run hello following command tooupgrade hello agent.</span></span> <span data-ttu-id="93b8c-295">Remplacez hello chemin d’accès toohello toopoint toohello fichier d’archive que vous avez téléchargé.</span><span class="sxs-lookup"><span data-stu-id="93b8c-295">Replace hello path toohello archive toopoint toohello file you downloaded.</span></span>
    ```bash
    sudo /usr/sap/hostctrl/exe/saphostexec -upgrade -archive <path tooSAP Host Agent SAR>
    ```

1. <span data-ttu-id="93b8c-296">[1] Créer la réplication HANA (en tant que root)</span><span class="sxs-lookup"><span data-stu-id="93b8c-296">[1] Create HANA replication (as root)</span></span>  
    <span data-ttu-id="93b8c-297">Exécutez hello commande suivante.</span><span class="sxs-lookup"><span data-stu-id="93b8c-297">Run hello following command.</span></span> <span data-ttu-id="93b8c-298">Assurez-vous que tooreplace chaînes en gras (HANA système ID HDB et numéro d’instance 03) avec des valeurs de votre installation de SAP HANA hello.</span><span class="sxs-lookup"><span data-stu-id="93b8c-298">Make sure tooreplace bold strings (HANA System ID HDB and instance number 03) with hello values of your SAP HANA installation.</span></span>
    <pre><code>
    PATH="$PATH:/usr/sap/<b>HDB</b>/HDB<b>03</b>/exe"
    hdbsql -u system -i <b>03</b> 'CREATE USER <b>hdb</b>hasync PASSWORD "<b>passwd</b>"' 
    hdbsql -u system -i <b>03</b> 'GRANT DATA ADMIN too<b>hdb</b>hasync' 
    hdbsql -u system -i <b>03</b> 'ALTER USER <b>hdb</b>hasync DISABLE PASSWORD LIFETIME' 
    </code></pre>

1. <span data-ttu-id="93b8c-299">[A] Créer l’entrée keystore (en tout que root)</span><span class="sxs-lookup"><span data-stu-id="93b8c-299">[A] Create keystore entry (as root)</span></span>
    <pre><code>
    PATH="$PATH:/usr/sap/<b>HDB</b>/HDB<b>03</b>/exe"
    hdbuserstore SET <b>hdb</b>haloc localhost:3<b>03</b>15 <b>hdb</b>hasync <b>passwd</b>
    </code></pre>
1. <span data-ttu-id="93b8c-300">[1] Sauvegarder la base de données (en tant que root)</span><span class="sxs-lookup"><span data-stu-id="93b8c-300">[1] Backup database (as root)</span></span>
    <pre><code>
    PATH="$PATH:/usr/sap/<b>HDB</b>/HDB<b>03</b>/exe"
    hdbsql -u system -i <b>03</b> "BACKUP DATA USING FILE ('<b>initialbackup</b>')" 
    </code></pre>
1. <span data-ttu-id="93b8c-301">[1] commutateur toohello sapsid utilisateur (par exemple hdbadm) et créer un site principal de hello.</span><span class="sxs-lookup"><span data-stu-id="93b8c-301">[1] Switch toohello sapsid user (for example hdbadm) and create hello primary site.</span></span>
    <pre><code>
    su - <b>hdb</b>adm
    hdbnsutil -sr_enable –-name=<b>SITE1</b>
    </code></pre>
1. <span data-ttu-id="93b8c-302">[2] commutateur toohello sapsid utilisateur (par exemple hdbadm) et créer un site secondaire de hello.</span><span class="sxs-lookup"><span data-stu-id="93b8c-302">[2] Switch toohello sapsid user (for example hdbadm) and create hello secondary site.</span></span>
    <pre><code>
    su - <b>hdb</b>adm
    sapcontrol -nr <b>03</b> -function StopWait 600 10
    hdbnsutil -sr_register --remoteHost=<b>saphanavm1</b> --remoteInstance=<b>03</b> --replicationMode=sync --name=<b>SITE2</b> 
    </code></pre>

## <a name="configure-cluster-framework"></a><span data-ttu-id="93b8c-303">Configurer le framework du cluster</span><span class="sxs-lookup"><span data-stu-id="93b8c-303">Configure Cluster Framework</span></span>

<span data-ttu-id="93b8c-304">Modifier les paramètres par défaut hello</span><span class="sxs-lookup"><span data-stu-id="93b8c-304">Change hello default settings</span></span>

<pre>
sudo vi crm-defaults.txt
# enter hello following toocrm-defaults.txt
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

# <a name="now-we-load-hello-file-toohello-cluster"></a><span data-ttu-id="93b8c-305">maintenant que nous charger toohello de fichiers hello</span><span class="sxs-lookup"><span data-stu-id="93b8c-305">now we load hello file toohello cluster</span></span>
<span data-ttu-id="93b8c-306">sudo crm configure load update crm-defaults.txt</span><span class="sxs-lookup"><span data-stu-id="93b8c-306">sudo crm configure load update crm-defaults.txt</span></span>
</pre>

### <a name="create-stonith-device"></a><span data-ttu-id="93b8c-307">Créer l’appareil STONITH</span><span class="sxs-lookup"><span data-stu-id="93b8c-307">Create STONITH device</span></span>

<span data-ttu-id="93b8c-308">APPAREIL STONITH Hello utilise un tooauthorize de Principal du Service par rapport à Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="93b8c-308">hello STONITH device uses a Service Principal tooauthorize against Microsoft Azure.</span></span> <span data-ttu-id="93b8c-309">Suivez ces étapes de toocreate un Principal de Service.</span><span class="sxs-lookup"><span data-stu-id="93b8c-309">Please follow these steps toocreate a Service Principal.</span></span>

1. <span data-ttu-id="93b8c-310">Accédez trop<https://portal.azure.com></span><span class="sxs-lookup"><span data-stu-id="93b8c-310">Go too<https://portal.azure.com></span></span>
1. <span data-ttu-id="93b8c-311">Panneau d’Azure Active Directory hello ouvert</span><span class="sxs-lookup"><span data-stu-id="93b8c-311">Open hello Azure Active Directory blade</span></span>  
   <span data-ttu-id="93b8c-312">Accédez tooProperties et écrivez hello ID de répertoire. Il s’agit de hello **id client**.</span><span class="sxs-lookup"><span data-stu-id="93b8c-312">Go tooProperties and write down hello Directory Id. This is hello **tenant id**.</span></span>
1. <span data-ttu-id="93b8c-313">Cliquez sur Inscriptions d’applications</span><span class="sxs-lookup"><span data-stu-id="93b8c-313">Click App registrations</span></span>
1. <span data-ttu-id="93b8c-314">Cliquez sur Ajouter.</span><span class="sxs-lookup"><span data-stu-id="93b8c-314">Click Add</span></span>
1. <span data-ttu-id="93b8c-315">Entrez un nom, sélectionnez le type d’application « Application web/API », entrez une URL de connexion (par exemple, http://localhost) et cliquez sur Créer</span><span class="sxs-lookup"><span data-stu-id="93b8c-315">Enter a Name, select Application Type "Web app/API", enter a sign-on URL (for example http://localhost) and click Create</span></span>
1. <span data-ttu-id="93b8c-316">URL de connexion Hello n’est pas utilisé et peut être une URL valide</span><span class="sxs-lookup"><span data-stu-id="93b8c-316">hello sign-on URL is not used and can be any valid URL</span></span>
1. <span data-ttu-id="93b8c-317">Sélectionnez hello nouvelle application et cliquez sur les clés dans l’onglet Paramètres de hello</span><span class="sxs-lookup"><span data-stu-id="93b8c-317">Select hello new App and click Keys in hello Settings tab</span></span>
1. <span data-ttu-id="93b8c-318">Entrez une description pour la nouvelle clé, sélectionnez « N’expire jamais » et cliquez sur Enregistrer</span><span class="sxs-lookup"><span data-stu-id="93b8c-318">Enter a description for a new key, select "Never expires" and click Save</span></span>
1. <span data-ttu-id="93b8c-319">Écrivez hello valeur.</span><span class="sxs-lookup"><span data-stu-id="93b8c-319">Write down hello Value.</span></span> <span data-ttu-id="93b8c-320">Il est utilisé comme hello **mot de passe** pour hello Principal du Service</span><span class="sxs-lookup"><span data-stu-id="93b8c-320">It is used as hello **password** for hello Service Principal</span></span>
1. <span data-ttu-id="93b8c-321">Écrivez hello ID d’Application. Il est utilisé comme nom d’utilisateur de hello (**id de connexion** dans suit hello) de hello Principal du Service</span><span class="sxs-lookup"><span data-stu-id="93b8c-321">Write down hello Application Id. It is used as hello username (**login id** in hello steps below) of hello Service Principal</span></span>

<span data-ttu-id="93b8c-322">Hello Principal du Service n’a pas les autorisations tooaccess vos ressources Azure par défaut.</span><span class="sxs-lookup"><span data-stu-id="93b8c-322">hello Service Principal does not have permissions tooaccess your Azure resources by default.</span></span> <span data-ttu-id="93b8c-323">Vous devez toostart d’autorisations toogive hello Principal du Service et arrêter (désallouer) tous les ordinateurs virtuels du cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="93b8c-323">You need toogive hello Service Principal permissions toostart and stop (deallocate) all virtual machines of hello cluster.</span></span>

1. <span data-ttu-id="93b8c-324">Accédez toohttps://portal.azure.com</span><span class="sxs-lookup"><span data-stu-id="93b8c-324">Go toohttps://portal.azure.com</span></span>
1. <span data-ttu-id="93b8c-325">Ouvrez hello toutes les lames de ressources</span><span class="sxs-lookup"><span data-stu-id="93b8c-325">Open hello All resources blade</span></span>
1. <span data-ttu-id="93b8c-326">Sélectionnez l’ordinateur virtuel de hello</span><span class="sxs-lookup"><span data-stu-id="93b8c-326">Select hello virtual machine</span></span>
1. <span data-ttu-id="93b8c-327">Cliquez sur Contrôle d’accès (IAM)</span><span class="sxs-lookup"><span data-stu-id="93b8c-327">Click Access control (IAM)</span></span>
1. <span data-ttu-id="93b8c-328">Cliquez sur Ajouter.</span><span class="sxs-lookup"><span data-stu-id="93b8c-328">Click Add</span></span>
1. <span data-ttu-id="93b8c-329">Sélectionnez le rôle hello propriétaire</span><span class="sxs-lookup"><span data-stu-id="93b8c-329">Select hello role Owner</span></span>
1. <span data-ttu-id="93b8c-330">Entrez les nom hello d’application hello créé ci-dessus</span><span class="sxs-lookup"><span data-stu-id="93b8c-330">Enter hello name of hello application you created above</span></span>
1. <span data-ttu-id="93b8c-331">Cliquez sur OK</span><span class="sxs-lookup"><span data-stu-id="93b8c-331">Click OK</span></span>

<span data-ttu-id="93b8c-332">Une fois que vous avez modifié les autorisations hello pour les ordinateurs virtuels de hello, vous pouvez configurer les appareils STONITH hello dans un cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="93b8c-332">After you edited hello permissions for hello virtual machines, you can configure hello STONITH devices in hello cluster.</span></span>

<pre>
sudo vi crm-fencing.txt
# enter hello following toocrm-fencing.txt
# replace hello bold string with your subscription id, resource group, tenant id, service principal id and password
<code>
primitive rsc_st_azure_1 stonith:fence_azure_arm \
    params subscriptionId="<b>subscription id</b>" resourceGroup="<b>resource group</b>" tenantId="<b>tenant id</b>" login="<b>login id</b>" passwd="<b>password</b>"

primitive rsc_st_azure_2 stonith:fence_azure_arm \
    params subscriptionId="<b>subscription id</b>" resourceGroup="<b>resource group</b>" tenantId="<b>tenant id</b>" login="<b>login id</b>" passwd="<b>password</b>"

colocation col_st_azure -2000: rsc_st_azure_1:Started rsc_st_azure_2:Started
</code>

# <a name="now-we-load-hello-file-toohello-cluster"></a><span data-ttu-id="93b8c-333">maintenant que nous charger toohello de fichiers hello</span><span class="sxs-lookup"><span data-stu-id="93b8c-333">now we load hello file toohello cluster</span></span>
<span data-ttu-id="93b8c-334">sudo crm configure load update crm-fencing.txt</span><span class="sxs-lookup"><span data-stu-id="93b8c-334">sudo crm configure load update crm-fencing.txt</span></span>
</pre>

### <a name="create-sap-hana-resources"></a><span data-ttu-id="93b8c-335">Créer des ressources SAP HANA</span><span class="sxs-lookup"><span data-stu-id="93b8c-335">Create SAP HANA resources</span></span>

<pre>
sudo vi crm-saphanatop.txt
# enter hello following toocrm-saphana.txt
# replace hello bold string with your instance number and HANA system id
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

# <a name="now-we-load-hello-file-toohello-cluster"></a><span data-ttu-id="93b8c-336">maintenant que nous charger toohello de fichiers hello</span><span class="sxs-lookup"><span data-stu-id="93b8c-336">now we load hello file toohello cluster</span></span>
<span data-ttu-id="93b8c-337">sudo crm configure load update crm-saphanatop.txt</span><span class="sxs-lookup"><span data-stu-id="93b8c-337">sudo crm configure load update crm-saphanatop.txt</span></span>
</pre>

<pre>
sudo vi crm-saphana.txt
# enter hello following toocrm-saphana.txt
# replace hello bold string with your instance number, HANA system id and hello frontend IP address of hello Azure load balancer. 
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

# <a name="now-we-load-hello-file-toohello-cluster"></a><span data-ttu-id="93b8c-338">maintenant que nous charger toohello de fichiers hello</span><span class="sxs-lookup"><span data-stu-id="93b8c-338">now we load hello file toohello cluster</span></span>
<span data-ttu-id="93b8c-339">sudo crm configure load update crm-saphana.txt</span><span class="sxs-lookup"><span data-stu-id="93b8c-339">sudo crm configure load update crm-saphana.txt</span></span>
</pre>

### <a name="test-cluster-setup"></a><span data-ttu-id="93b8c-340">Tester la configuration du cluster</span><span class="sxs-lookup"><span data-stu-id="93b8c-340">Test cluster setup</span></span>
<span data-ttu-id="93b8c-341">Hello chapitre décrire comment vous pouvez tester votre configuration.</span><span class="sxs-lookup"><span data-stu-id="93b8c-341">hello following chapter describe how you can test your setup.</span></span> <span data-ttu-id="93b8c-342">Chaque test suppose que vous êtes racine principale de SAP HANA hello s’exécute sur saphanavm1 de machine virtuelle hello.</span><span class="sxs-lookup"><span data-stu-id="93b8c-342">Every test assumes that you are root and hello SAP HANA master is running on hello virtual machine saphanavm1.</span></span>

#### <a name="fencing-test"></a><span data-ttu-id="93b8c-343">Test de délimitation</span><span class="sxs-lookup"><span data-stu-id="93b8c-343">Fencing Test</span></span>

<span data-ttu-id="93b8c-344">Vous pouvez tester le programme d’installation de hello de l’agent de délimitation hello en désactivant l’interface réseau hello sur saphanavm1 de nœud.</span><span class="sxs-lookup"><span data-stu-id="93b8c-344">You can test hello setup of hello fencing agent by disabling hello network interface on node saphanavm1.</span></span>

<pre><code>
sudo ifdown eth0
</code></pre>

<span data-ttu-id="93b8c-345">Hello machine virtuelle doit désormais obtenir redémarré ou arrêté, selon votre configuration de cluster.</span><span class="sxs-lookup"><span data-stu-id="93b8c-345">hello virtual machine should now get restarted or stopped depending on your cluster configuration.</span></span>
<span data-ttu-id="93b8c-346">Si vous définissez hello stonith-action toooff, hello virtual machine va être arrêté, et les ressources de hello sont migré toohello machine virtuelle en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="93b8c-346">If you set hello stonith-action toooff, hello virtual machine will be stopped and hello resources are migrated toohello running virtual machine.</span></span>

<span data-ttu-id="93b8c-347">Une fois que vous démarrez à nouveau hello virtual machine, hello ressource de SAP HANA échoue toostart en tant que base de données secondaire si vous définissez AUTOMATED_REGISTER = « false ».</span><span class="sxs-lookup"><span data-stu-id="93b8c-347">Once you start hello virtual machine again, hello SAP HANA resource will fail toostart as secondary if you set AUTOMATED_REGISTER="false".</span></span> <span data-ttu-id="93b8c-348">Dans ce cas, vous avez besoin d’instance HANA de hello tooconfigure secondaire en exécutant hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="93b8c-348">In this case, you need tooconfigure hello HANA instance as secondary by executing hello following command:</span></span>

<pre><code>
su - <b>hdb</b>adm

# Stop hello HANA instance just in case it is running
sapcontrol -nr <b>03</b> -function StopWait 600 10
hdbnsutil -sr_register --remoteHost=<b>saphanavm2</b> --remoteInstance=<b>03</b> --replicationMode=sync --name=<b>SITE1</b>

# switch back tooroot and cleanup hello failed state
exit
crm resource cleanup msl_SAPHana_<b>HDB</b>_HDB<b>03</b> <b>saphanavm1</b>
</code></pre>

#### <a name="testing-a-manual-failover"></a><span data-ttu-id="93b8c-349">Tester un basculement manuel</span><span class="sxs-lookup"><span data-stu-id="93b8c-349">Testing a manual failover</span></span>

<span data-ttu-id="93b8c-350">Vous pouvez tester un basculement manuel en arrêtant le service de STIMULATEUR hello sur le nœud saphanavm1.</span><span class="sxs-lookup"><span data-stu-id="93b8c-350">You can test a manual failover by stopping hello pacemaker service on node saphanavm1.</span></span>
<pre><code>
service pacemaker stop
</code></pre>

<span data-ttu-id="93b8c-351">Après le basculement de hello, vous pouvez démarrer le service de hello à nouveau.</span><span class="sxs-lookup"><span data-stu-id="93b8c-351">After hello failover, you can start hello service again.</span></span> <span data-ttu-id="93b8c-352">Hello ressources SAP HANA sur saphanavm1 échoue toostart en tant que base de données secondaire si vous définissez AUTOMATED_REGISTER = « false ».</span><span class="sxs-lookup"><span data-stu-id="93b8c-352">hello SAP HANA resource on saphanavm1 will fail toostart as secondary if you set AUTOMATED_REGISTER="false".</span></span> <span data-ttu-id="93b8c-353">Dans ce cas, vous avez besoin d’instance HANA de hello tooconfigure secondaire en exécutant hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="93b8c-353">In this case, you need tooconfigure hello HANA instance as secondary by executing hello following command:</span></span>

<pre><code>
service pacemaker start
su - <b>hdb</b>adm

# Stop hello HANA instance just in case it is running
sapcontrol -nr <b>03</b> -function StopWait 600 10
hdbnsutil -sr_register --remoteHost=<b>saphanavm2</b> --remoteInstance=<b>03</b> --replicationMode=sync --name=<b>SITE1</b> 


# switch back tooroot and cleanup hello failed state
exit
crm resource cleanup msl_SAPHana_<b>HDB</b>_HDB<b>03</b> <b>saphanavm1</b>
</code></pre>

#### <a name="testing-a-migration"></a><span data-ttu-id="93b8c-354">Tester une migration</span><span class="sxs-lookup"><span data-stu-id="93b8c-354">Testing a migration</span></span>

<span data-ttu-id="93b8c-355">Vous pouvez migrer le nœud principal de SAP HANA hello en exécutant hello commande suivante</span><span class="sxs-lookup"><span data-stu-id="93b8c-355">You can migrate hello SAP HANA master node by executing hello following command</span></span>
<pre><code>
crm resource migrate msl_SAPHana_<b>HDB</b>_HDB<b>03</b> <b>saphanavm2</b>
crm resource migrate g_ip_<b>HDB</b>_HDB<b>03</b> <b>saphanavm2</b>
</code></pre>

<span data-ttu-id="93b8c-356">Cette migration nœud maître de SAP HANA hello et groupe hello contenant toosaphanavm2 adresse IP virtuelle de hello.</span><span class="sxs-lookup"><span data-stu-id="93b8c-356">This should migrate hello SAP HANA master node and hello group that contains hello virtual IP address toosaphanavm2.</span></span>
<span data-ttu-id="93b8c-357">Hello ressources SAP HANA sur saphanavm1 échoue toostart en tant que base de données secondaire si vous définissez AUTOMATED_REGISTER = « false ».</span><span class="sxs-lookup"><span data-stu-id="93b8c-357">hello SAP HANA resource on saphanavm1 will fail toostart as secondary if you set AUTOMATED_REGISTER="false".</span></span> <span data-ttu-id="93b8c-358">Dans ce cas, vous avez besoin d’instance HANA de hello tooconfigure secondaire en exécutant hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="93b8c-358">In this case, you need tooconfigure hello HANA instance as secondary by executing hello following command:</span></span>

<pre><code>
su - <b>hdb</b>adm

# Stop hello HANA instance just in case it is running
sapcontrol -nr <b>03</b> -function StopWait 600 10
hdbnsutil -sr_register --remoteHost=<b>saphanavm2</b> --remoteInstance=<b>03</b> --replicationMode=sync --name=<b>SITE1</b> 
</code></pre>

<span data-ttu-id="93b8c-359">migration de Hello crée des contraintes d’emplacement qui doivent toobe supprimé à nouveau.</span><span class="sxs-lookup"><span data-stu-id="93b8c-359">hello migration creates location contraints that need toobe deleted again.</span></span>

<pre><code>
crm configure edited

# delete location contraints that are named like hello following contraint. You should have two contraints, one for hello SAP HANA resource and one for hello IP address group.
location cli-prefer-g_ip_<b>HDB</b>_HDB<b>03</b> g_ip_<b>HDB</b>_HDB<b>03</b> role=Started inf: <b>saphanavm2</b>
</code></pre>

<span data-ttu-id="93b8c-360">Vous devez également l’état de hello toocleanup de ressource du nœud secondaire hello</span><span class="sxs-lookup"><span data-stu-id="93b8c-360">You also need toocleanup hello state of hello secondary node resource</span></span>

<pre><code>
# switch back tooroot and cleanup hello failed state
exit
crm resource cleanup msl_SAPHana_<b>HDB</b>_HDB<b>03</b> <b>saphanavm1</b>
</code></pre>

## <a name="next-steps"></a><span data-ttu-id="93b8c-361">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="93b8c-361">Next steps</span></span>
* <span data-ttu-id="93b8c-362">[Planification et implémentation de machines virtuelles Azure pour SAP][planning-guide]</span><span class="sxs-lookup"><span data-stu-id="93b8c-362">[Azure Virtual Machines planning and implementation for SAP][planning-guide]</span></span>
* <span data-ttu-id="93b8c-363">[Déploiement de machines virtuelles Azure pour SAP][deployment-guide]</span><span class="sxs-lookup"><span data-stu-id="93b8c-363">[Azure Virtual Machines deployment for SAP][deployment-guide]</span></span>
* <span data-ttu-id="93b8c-364">[Déploiement SGBD de machines virtuelles Azure pour SAP][dbms-guide]</span><span class="sxs-lookup"><span data-stu-id="93b8c-364">[Azure Virtual Machines DBMS deployment for SAP][dbms-guide]</span></span>
* <span data-ttu-id="93b8c-365">toolearn comment tooestablish haute disponibilité et le plan de récupération d’urgence de SAP HANA sur Azure (instances de grande taille), consultez [SAP HANA (instances de grande taille) haute disponibilité et récupération d’urgence sur Azure](hana-overview-high-availability-disaster-recovery.md).</span><span class="sxs-lookup"><span data-stu-id="93b8c-365">toolearn how tooestablish high availability and plan for disaster recovery of SAP HANA on Azure (large instances), see [SAP HANA (large instances) high availability and disaster recovery on Azure](hana-overview-high-availability-disaster-recovery.md).</span></span> 
