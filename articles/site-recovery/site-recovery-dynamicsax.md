---
title: "Répliquer un déploiement Dynamics AX multiniveau à l’aide d’Azure Site Recovery | Microsoft Docs"
description: "Cet article explique comment répliquer et protéger Dynamics AX à l’aide d’Azure Site Recovery"
services: site-recovery
documentationcenter: 
author: asgang
manager: rochakm
editor: 
ms.assetid: 9126f5e8-e9ed-4c31-b6b4-bf969c12c184
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 8/24/2017
ms.author: asgang
ms.openlocfilehash: 03127c8f4841b67436c4819628319705af0b2cd5
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="replicate-a-multi-tier-dynamics-ax-application-using-azure-site-recovery"></a><span data-ttu-id="76348-103">Répliquer une application Dynamics AX multiniveau à l’aide d’Azure Site Recovery</span><span class="sxs-lookup"><span data-stu-id="76348-103">Replicate a multi-tier Dynamics AX application using Azure Site Recovery</span></span>

## <a name="overview"></a><span data-ttu-id="76348-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="76348-104">Overview</span></span>


<span data-ttu-id="76348-105">Microsoft Dynamics AX est une des solutions ERP les plus populaires parmi les entreprises pour standardiser le processus dans tous les emplacements, gérer les ressources et simplifier la conformité.</span><span class="sxs-lookup"><span data-stu-id="76348-105">Microsoft Dynamics AX is one of the most popular ERP solution among enterprises to standardized process across locations, manage resources and simplifying compliance.</span></span> <span data-ttu-id="76348-106">Étant donné que cette application est essentielle pour une entreprise, il est très important de s’assurer qu’en cas d’incident, l’application est opérationnelle en un minimum de temps.</span><span class="sxs-lookup"><span data-stu-id="76348-106">Considering the application is business critical to an organization it is very important to be sure that if any disaster, application should be up and running in minimum time.</span></span>

<span data-ttu-id="76348-107">Aujourd'hui, Microsoft Dynamics AX ne fournit aucune capacité de récupération d’urgence prête à l’emploi.</span><span class="sxs-lookup"><span data-stu-id="76348-107">Today, Microsoft Dynamics AX  does not provide any out-of-the-box disaster recovery capabilities.</span></span> <span data-ttu-id="76348-108">Microsoft Dynamics AX comprend de nombreux composants de serveur comme Application Object Server, Active Directory (AD), SQL Database Server, SharePoint Server, Reporting Server, etc. La gestion manuelle de la récupération d’urgence de chacun de ces composants est non seulement coûteuse, mais elle est également sujette aux erreurs.</span><span class="sxs-lookup"><span data-stu-id="76348-108">Microsoft Dynamics AX consists of many server components like Application Object Server, Active Directory (AD), SQL Database Server, SharePoint Server, Reporting Server etc. To manage the disaster recovery of each of these components manually is not only expensive but also error-prone.</span></span>

<span data-ttu-id="76348-109">Cet article explique en détail comment créer une solution de récupération d’urgence pour votre application Dynamics AX à l’aide d’[Azure Site Recovery](site-recovery-overview.md).</span><span class="sxs-lookup"><span data-stu-id="76348-109">This article explains in detail about how you can create a disaster recovery solution for your Dynamics AX application using [Azure Site Recovery](site-recovery-overview.md).</span></span> <span data-ttu-id="76348-110">Sont également couverts les basculements planifiés/non planifiés/de test à l’aide d’un plan de récupération en un seul clic, les configurations prises en charge et les prérequis.</span><span class="sxs-lookup"><span data-stu-id="76348-110">It also covers planned/unplanned/test failovers using one-click recovery plan, supported configurations, and prerequisites.</span></span>
<span data-ttu-id="76348-111">La solution de récupération d’urgence basée sur Azure Site Recovery est entièrement testée, certifiée et recommandée par Microsoft Dynamics AX.</span><span class="sxs-lookup"><span data-stu-id="76348-111">Azure Site Recovery based disaster recovery solution is fully tested, certified, and recommended by Microsoft Dynamics AX.</span></span>



## <a name="prerequisites"></a><span data-ttu-id="76348-112">Composants requis</span><span class="sxs-lookup"><span data-stu-id="76348-112">Prerequisites</span></span>

<span data-ttu-id="76348-113">L’implémentation de la récupération d’urgence pour l’application Dynamics AX à l’aide d’Azure Site Recovery nécessite de remplir les conditions requises préalables suivantes.</span><span class="sxs-lookup"><span data-stu-id="76348-113">Implementing disaster recovery for Dynamics AX application using Azure Site Recovery requires the following pre-requisites completed.</span></span>

<span data-ttu-id="76348-114">•    Un déploiement local de Dynamics AX a été configuré</span><span class="sxs-lookup"><span data-stu-id="76348-114">•   An on-premises Dynamics AX deployment has been set up</span></span>

<span data-ttu-id="76348-115">•    Un coffre Azure Site Recovery Services a été créé dans un abonnement Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="76348-115">•   Azure Site Recovery Services vault has been created in Microsoft Azure subscription</span></span>

<span data-ttu-id="76348-116">•    Si Azure est votre site de récupération d’urgence, exécutez l’outil d’évaluation de la disponibilité des machines virtuelles Azure sur des machines virtuelles afin de vérifier qu’elles sont compatibles avec les machines virtuelles Azure et Azure Site Recovery Services</span><span class="sxs-lookup"><span data-stu-id="76348-116">•   If Azure is your recovery site, run the Azure Virtual Machine Readiness Assessment tool  on VMs to ensure that they are compatible with Azure VMs and Azure Site Recovery Services</span></span>


## <a name="site-recovery-support"></a><span data-ttu-id="76348-117">Prise en charge de Site Recovery</span><span class="sxs-lookup"><span data-stu-id="76348-117">Site Recovery support</span></span>

<span data-ttu-id="76348-118">Pour les besoins de création de cet article, des machines virtuelles VMware avec Dynamics AX 2012 R3 sur Windows Server 2012 R2 Enterprise ont été utilisées.</span><span class="sxs-lookup"><span data-stu-id="76348-118">For the purpose of creating this article, VMware virtual machines with Dynamics AX  2012R3 on Windows Server 2012 R2 Enterprise were used.</span></span> <span data-ttu-id="76348-119">Comme la réplication Site Recovery est indépendante des applications, les recommandations indiquées ici sont censées également s’appliquer aux scénarios suivants.</span><span class="sxs-lookup"><span data-stu-id="76348-119">As site recovery replication is application agnostic, the recommendations provided here are expected to hold on following scenarios as well.</span></span>

### <a name="source-and-target"></a><span data-ttu-id="76348-120">Source et cible</span><span class="sxs-lookup"><span data-stu-id="76348-120">Source and target</span></span>

<span data-ttu-id="76348-121">**Scénario**</span><span class="sxs-lookup"><span data-stu-id="76348-121">**Scenario**</span></span> | <span data-ttu-id="76348-122">**Vers un site secondaire**</span><span class="sxs-lookup"><span data-stu-id="76348-122">**To a secondary site**</span></span> | <span data-ttu-id="76348-123">**Vers Azure**</span><span class="sxs-lookup"><span data-stu-id="76348-123">**To Azure**</span></span>
--- | --- | ---
<span data-ttu-id="76348-124">**Hyper-V**</span><span class="sxs-lookup"><span data-stu-id="76348-124">**Hyper-V**</span></span> | <span data-ttu-id="76348-125">Oui</span><span class="sxs-lookup"><span data-stu-id="76348-125">Yes</span></span> | <span data-ttu-id="76348-126">Oui</span><span class="sxs-lookup"><span data-stu-id="76348-126">Yes</span></span>
<span data-ttu-id="76348-127">**VMware**</span><span class="sxs-lookup"><span data-stu-id="76348-127">**VMware**</span></span> | <span data-ttu-id="76348-128">Oui</span><span class="sxs-lookup"><span data-stu-id="76348-128">Yes</span></span> | <span data-ttu-id="76348-129">Oui</span><span class="sxs-lookup"><span data-stu-id="76348-129">Yes</span></span>
<span data-ttu-id="76348-130">**Serveur physique**</span><span class="sxs-lookup"><span data-stu-id="76348-130">**Physical server**</span></span> | <span data-ttu-id="76348-131">Oui</span><span class="sxs-lookup"><span data-stu-id="76348-131">Yes</span></span> | <span data-ttu-id="76348-132">Oui</span><span class="sxs-lookup"><span data-stu-id="76348-132">Yes</span></span>

## <a name="enable-dr-of-dynamics-ax-application-using-azure-site-recovery"></a><span data-ttu-id="76348-133">Activer la récupération d’urgence de l’application Dynamics AX à l’aide d’Azure Site Recovery</span><span class="sxs-lookup"><span data-stu-id="76348-133">Enable DR of Dynamics AX application using Azure Site Recovery</span></span>
### <a name="protect-your-dynamics-ax-application"></a><span data-ttu-id="76348-134">Protéger votre application Dynamics AX</span><span class="sxs-lookup"><span data-stu-id="76348-134">Protect your Dynamics AX application</span></span>
<span data-ttu-id="76348-135">Chaque composant de Dynamics AX doit être protégé pour activer la réplication et la récupération de l’application complète.</span><span class="sxs-lookup"><span data-stu-id="76348-135">Each component of the Dynamics AX needs to be protected to enable the complete application replication and recovery.</span></span> <span data-ttu-id="76348-136">Cette section couvre les points suivants :</span><span class="sxs-lookup"><span data-stu-id="76348-136">This section covers:</span></span>

<span data-ttu-id="76348-137">**1. Protection d’Active Directory**</span><span class="sxs-lookup"><span data-stu-id="76348-137">**1. Protection of Active Directory**</span></span>

<span data-ttu-id="76348-138">**2. Protection du niveau SQL**</span><span class="sxs-lookup"><span data-stu-id="76348-138">**2. Protection of SQL Tier**</span></span>

<span data-ttu-id="76348-139">**3. Protection des niveaux application et web**</span><span class="sxs-lookup"><span data-stu-id="76348-139">**3. Protection of App and Web Tiers**</span></span>

<span data-ttu-id="76348-140">**4. Configuration de la mise en réseau**</span><span class="sxs-lookup"><span data-stu-id="76348-140">**4. Networking configuration**</span></span>

<span data-ttu-id="76348-141">**5. Plan de récupération**</span><span class="sxs-lookup"><span data-stu-id="76348-141">**5. Recovery Plan**</span></span>

### <a name="1-setup-ad-and-dns-replication"></a><span data-ttu-id="76348-142">1. Configurer la réplication Active Directory et DNS</span><span class="sxs-lookup"><span data-stu-id="76348-142">1. Setup AD and DNS replication</span></span>

<span data-ttu-id="76348-143">Active Directory est requis sur le site de récupération d’urgence pour que l’application Dynamics AX fonctionne.</span><span class="sxs-lookup"><span data-stu-id="76348-143">Active Directory is required on the DR site for Dynamics AX application to function.</span></span> <span data-ttu-id="76348-144">En fonction de la complexité de l’environnement local du client, deux choix vous sont recommandés.</span><span class="sxs-lookup"><span data-stu-id="76348-144">There are two recommended choices based on the complexity of the customer’s on-premises environment.</span></span>

<span data-ttu-id="76348-145">**Option 1 :**</span><span class="sxs-lookup"><span data-stu-id="76348-145">**Option 1**</span></span>

<span data-ttu-id="76348-146">Si le client dispose d’un nombre d’applications limité et d’un seul contrôleur de domaine pour l’ensemble de son site local, et qu’il souhaite basculer l’intégralité du site, nous recommandons l’utilisation de la réplication ASR pour répliquer l’ordinateur contrôleur de domaine sur un site secondaire (applicable à la fois pour les scénarios de site à site et de site à Azure).</span><span class="sxs-lookup"><span data-stu-id="76348-146">If the customer has a small number of applications and a single domain controller for his entire on-premises site and will be failing over the entire site together, then we recommend using ASR-Replication to replicate the DC machine to secondary site (applicable for both Site to Site and Site to Azure).</span></span>

<span data-ttu-id="76348-147">**Option 2 :**</span><span class="sxs-lookup"><span data-stu-id="76348-147">**Option 2**</span></span>

<span data-ttu-id="76348-148">Si le client possède un grand nombre d’applications, qu’il exécute une forêt Active Directory et qu’il souhaite basculer quelques applications à la fois, nous recommandons de configurer un contrôleur de domaine supplémentaire sur le site de récupération d’urgence (sur un site secondaire ou dans Azure).</span><span class="sxs-lookup"><span data-stu-id="76348-148">If the customer has a large number of applications and is running an Active Directory forest and will fail-over few applications at a time, then we recommend setting up an additional domain controller on the DR site (secondary site or in Azure).</span></span>

<span data-ttu-id="76348-149">Reportez-vous au [guide d’accompagnement sur la mise à disposition d’un contrôleur de domaine sur le site de récupération d’urgence](site-recovery-active-directory.md).</span><span class="sxs-lookup"><span data-stu-id="76348-149">Please refer to [companion guide on making a domain controller available on DR site](site-recovery-active-directory.md).</span></span> <span data-ttu-id="76348-150">Pour le reste de ce document, nous supposons qu'un contrôleur de domaine est disponible sur le site de récupération d’urgence.</span><span class="sxs-lookup"><span data-stu-id="76348-150">For remainder of this document we will assume a DC is available on DR site.</span></span>

### <a name="2-setup-sql-server-replication"></a><span data-ttu-id="76348-151">2. Configurer la réplication SQL Server</span><span class="sxs-lookup"><span data-stu-id="76348-151">2. Setup SQL Server replication</span></span>
<span data-ttu-id="76348-152">Reportez-vous au guide d’accompagnement pour des conseils techniques détaillés sur l’option recommandée pour la protection du [niveau SQL](site-recovery-sql.md).</span><span class="sxs-lookup"><span data-stu-id="76348-152">Please refer to companion guide  for detailed technical guidance on the recommended option for protecting [SQL tier](site-recovery-sql.md).</span></span>

### <a name="3-enable-protection-for-dynamics-ax-client-and-aos-vms"></a><span data-ttu-id="76348-153">3. Activer la protection des machines virtuelles AOS et du client Dynamics AX</span><span class="sxs-lookup"><span data-stu-id="76348-153">3. Enable protection for Dynamics AX client and AOS VMs</span></span>
<span data-ttu-id="76348-154">Effectuez la configuration Azure Site Recovery appropriée selon que les machines virtuelles sont déployées sur [Hyper-V](site-recovery-hyper-v-site-to-azure.md) ou sur [VMware](site-recovery-vmware-to-azure.md).</span><span class="sxs-lookup"><span data-stu-id="76348-154">Perform relevant Azure Site Recovery configuration based on whether the VMs are deployed on [Hyper-V](site-recovery-hyper-v-site-to-azure.md) or on [VMware](site-recovery-vmware-to-azure.md).</span></span>

> [!TIP]
> <span data-ttu-id="76348-155">Pour la fréquence cohérente en cas d’incident, le réglage recommandé est de 15 minutes.</span><span class="sxs-lookup"><span data-stu-id="76348-155">Recommended Crash consistent frequency to configure is 15 minutes.</span></span>
>

<span data-ttu-id="76348-156">La capture instantanée ci-après montre l’état de la protection des machines virtuelles des composants Dynamics dans le scénario de protection « Site VMware vers Azure ».</span><span class="sxs-lookup"><span data-stu-id="76348-156">The below snapshot shows the protection status of Dynamics component VMs in ‘VMware site to Azure’ protection scenario.</span></span>
<span data-ttu-id="76348-157">![Éléments protégés ](./media/site-recovery-dynamics-ax/protecteditems.png)</span><span class="sxs-lookup"><span data-stu-id="76348-157">![Protected items ](./media/site-recovery-dynamics-ax/protecteditems.png)</span></span>

### <a name="4-configure-networking"></a><span data-ttu-id="76348-158">4. Configurer la mise en réseau</span><span class="sxs-lookup"><span data-stu-id="76348-158">4. Configure Networking</span></span>
<span data-ttu-id="76348-159">Configurer les paramètres Calcul et réseau des machines virtuelles</span><span class="sxs-lookup"><span data-stu-id="76348-159">Configure VM Compute and Network Settings</span></span>

<span data-ttu-id="76348-160">Pour le client AX et les machines virtuelles AOS, configurez les paramètres réseau dans Azure Site Recovery, afin que les réseaux des machines virtuelles soient associés au bon serveur de récupération d’urgence après le basculement.</span><span class="sxs-lookup"><span data-stu-id="76348-160">For the AX client and AOS VMs configure network settings in Azure Site Recovery so that the VM networks get attached to the right DR network after failover.</span></span> <span data-ttu-id="76348-161">Vérifiez que le réseau de récupération d’urgence pour ces niveaux est routable vers le niveau SQL.</span><span class="sxs-lookup"><span data-stu-id="76348-161">Ensure the DR network for these tiers is routable to the SQL tier.</span></span>

<span data-ttu-id="76348-162">Vous pouvez sélectionner la machine virtuelle dans les éléments répliqués afin de configurer les paramètres réseau comme indiqué dans la capture instantanée ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="76348-162">You can select the VM in the replicated items to configure the network settings as shown in the snapshot below.</span></span>

* <span data-ttu-id="76348-163">Pour les serveurs AOS, sélectionnez le bon groupe à haute disponibilité.</span><span class="sxs-lookup"><span data-stu-id="76348-163">For AOS servers select the correct availability set.</span></span>

* <span data-ttu-id="76348-164">Si vous utilisez une adresse IP statique, spécifiez l’adresse IP que vous souhaitez attribuer à la machine virtuelle dans le champ **Adresse IP cible** des ![paramètres réseau ](./media/site-recovery-dynamics-ax/vmpropertiesaos1.png)</span><span class="sxs-lookup"><span data-stu-id="76348-164">If you are using a static IP then specify the IP that you want the virtual machine to take in the **Target IP** field ![Network Settings ](./media/site-recovery-dynamics-ax/vmpropertiesaos1.png)</span></span>



### <a name="5-creating-a-recovery-plan"></a><span data-ttu-id="76348-165">5. Création d’un plan de récupération</span><span class="sxs-lookup"><span data-stu-id="76348-165">5. Creating a recovery plan</span></span>

<span data-ttu-id="76348-166">Vous pouvez créer un plan de récupération dans Azure Site Recovery pour automatiser le processus de basculement.</span><span class="sxs-lookup"><span data-stu-id="76348-166">You can create a recovery plan in Azure Site Recovery to automate the failover process.</span></span> <span data-ttu-id="76348-167">Ajoutez un niveau application et un niveau web dans le plan de récupération.</span><span class="sxs-lookup"><span data-stu-id="76348-167">Add app tier and web tier in the Recovery Plan.</span></span> <span data-ttu-id="76348-168">Organisez-les en différents groupes afin que les frontales s’arrêtent avant celles de niveau application.</span><span class="sxs-lookup"><span data-stu-id="76348-168">Order them in different groups so that the front-end shutdown before app tier.</span></span>

1)  <span data-ttu-id="76348-169">Sélectionnez le coffre Azure Site Recovery dans votre abonnement, puis cliquez sur la vignette Plans de récupération.</span><span class="sxs-lookup"><span data-stu-id="76348-169">Select the Azure Site Recovery vault in your subscription and click on ‘Recovery Plans’ tile.</span></span>

2)  <span data-ttu-id="76348-170">Cliquez sur « + Plan de récupération » et spécifiez un nom.</span><span class="sxs-lookup"><span data-stu-id="76348-170">Click on ‘+ Recovery plan and specify a name.</span></span>

3)  <span data-ttu-id="76348-171">Sélectionnez la « Source » et la « Cible ».</span><span class="sxs-lookup"><span data-stu-id="76348-171">Select the ‘Source’ and ‘Target’.</span></span> <span data-ttu-id="76348-172">La cible peut être Azure ou un site secondaire.</span><span class="sxs-lookup"><span data-stu-id="76348-172">The target can be Azure or secondary site.</span></span> <span data-ttu-id="76348-173">Si vous choisissez Azure, vous devez spécifier le modèle de déploiement</span><span class="sxs-lookup"><span data-stu-id="76348-173">In case you choose Azure, you must specify the deployment model</span></span>

![Créer un plan de récupération](./media/site-recovery-dynamics-ax/recoveryplancreation1.png)

4)  <span data-ttu-id="76348-175">Sélectionnez les machines virtuelles AOS et machines virtuelles du client pour le plan de récupération puis cliquez sur ✓.</span><span class="sxs-lookup"><span data-stu-id="76348-175">Select the AOS and client VMs to the recovery plan and click ✓.</span></span>
<span data-ttu-id="76348-176">![Créer un plan de récupération](./media/site-recovery-dynamics-ax/selectvms.png)</span><span class="sxs-lookup"><span data-stu-id="76348-176">![Create Recovery Plan](./media/site-recovery-dynamics-ax/selectvms.png)</span></span>


![Plan de récupération](./media/site-recovery-dynamics-ax/recoveryplan.png)

<span data-ttu-id="76348-178">Vous pouvez personnaliser le plan de récupération pour l’application Dynamics AX en ajoutant plusieurs étapes détaillées ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="76348-178">You can customize the recovery plan for Dynamics AX application by adding various steps as detailed below.</span></span> <span data-ttu-id="76348-179">La capture instantanée ci-dessus montre l’intégralité du plan de récupération après avoir ajouté toutes les étapes.</span><span class="sxs-lookup"><span data-stu-id="76348-179">The above snapshot shows the complete recovery plan after adding all the steps.</span></span>

<span data-ttu-id="76348-180">*Étapes :*</span><span class="sxs-lookup"><span data-stu-id="76348-180">*Steps:*</span></span>

<span data-ttu-id="76348-181">*1. Étapes du basculement SQL Server*</span><span class="sxs-lookup"><span data-stu-id="76348-181">*1. SQL Server fail over steps*</span></span>

<span data-ttu-id="76348-182">Reportez-vous au guide d’accompagnement [« Solution de récupération d’urgence de SQL Server »](site-recovery-sql.md) pour plus d’informations sur les étapes de récupération spécifiques à SQL Server.</span><span class="sxs-lookup"><span data-stu-id="76348-182">Refer to [‘SQL Server DR Solution’](site-recovery-sql.md) companion guide  for details about recovery steps specific to SQL server.</span></span>

<span data-ttu-id="76348-183">*2. Groupe de basculement 1 : basculement des machines virtuelles AOS*</span><span class="sxs-lookup"><span data-stu-id="76348-183">*2. Failover Group 1: Fail over the AOS VMs*</span></span>

<span data-ttu-id="76348-184">Assurez-vous que le point de récupération sélectionné est aussi proche que possible du PIT de la base de données mais pas antérieur à lui.</span><span class="sxs-lookup"><span data-stu-id="76348-184">Make sure that the recovery point selected is as close as possible to the database PIT but not ahead.</span></span>

<span data-ttu-id="76348-185">*3. Script : ajouter un équilibrage de charge (E-A uniquement)* Ajouter un script (via Azure Automation) après l’affichage du groupe de machines virtuelles AOS pour lui ajouter un équilibrage de charge.</span><span class="sxs-lookup"><span data-stu-id="76348-185">*3. Script: Add load balancer (Only E-A)* Add a script (via Azure automation) after AOS VM group comes up to add a load balancer to it.</span></span> <span data-ttu-id="76348-186">Vous pouvez utiliser un script pour effectuer cette tâche.</span><span class="sxs-lookup"><span data-stu-id="76348-186">You can use a script to do this task.</span></span> <span data-ttu-id="76348-187">Consultez l’article [Comment ajouter un équilibrage de charge pour la récupération d’urgence d’application multiniveau](https://azure.microsoft.com/blog/cloud-migration-and-disaster-recovery-of-load-balanced-multi-tier-applications-using-azure-site-recovery/)</span><span class="sxs-lookup"><span data-stu-id="76348-187">Refer article [how to add load balancer for multi-tier application DR](https://azure.microsoft.com/blog/cloud-migration-and-disaster-recovery-of-load-balanced-multi-tier-applications-using-azure-site-recovery/)</span></span>

<span data-ttu-id="76348-188">*4. Groupe de basculement 2 : basculement des machines virtuelles du client AX.*</span><span class="sxs-lookup"><span data-stu-id="76348-188">*4. Failover Group 2: Fail over the AX client VMs.*</span></span>
<span data-ttu-id="76348-189">Basculez les machines virtuelles de niveau web dans le cadre du plan de récupération.</span><span class="sxs-lookup"><span data-stu-id="76348-189">Fail over the web tier VMs as part of the recovery plan.</span></span>


### <a name="doing-a-test-failover"></a><span data-ttu-id="76348-190">Exécution d’un test de basculement</span><span class="sxs-lookup"><span data-stu-id="76348-190">Doing a test failover</span></span>

<span data-ttu-id="76348-191">Reportez-vous aux guides d’accompagnement « Solution de récupération d’urgence d’Active Directory » et « Solution de récupération d’urgence de SQL Server » pour obtenir des considérations spécifiques à Active Directory et SQL Server durant le test de basculement.</span><span class="sxs-lookup"><span data-stu-id="76348-191">Refer to ‘AD DR Solution ’ and ‘SQL Server DR solution ’ companion guides for considerations specific to AD and SQL server respectively during Test Failover.</span></span>

1.  <span data-ttu-id="76348-192">Accédez au portail Azure et sélectionnez votre coffre Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="76348-192">Go to Azure  portal and select your Site Recovery vault.</span></span>
2.  <span data-ttu-id="76348-193">Cliquez sur le plan de récupération créé pour Dynamics AX.</span><span class="sxs-lookup"><span data-stu-id="76348-193">Click on the recovery plan created for Dynamics AX.</span></span>
3.  <span data-ttu-id="76348-194">Cliquez sur « Test de basculement ».</span><span class="sxs-lookup"><span data-stu-id="76348-194">Click on ‘Test Failover’.</span></span>
4.  <span data-ttu-id="76348-195">Sélectionnez le réseau virtuel pour démarrer le processus de test de basculement.</span><span class="sxs-lookup"><span data-stu-id="76348-195">Select the virtual network to start the test fail-over process.</span></span>
5.  <span data-ttu-id="76348-196">Lorsque l’environnement secondaire est opérationnel, vous pouvez effectuer vos validations.</span><span class="sxs-lookup"><span data-stu-id="76348-196">Once the secondary environment is up, you can perform your validations.</span></span>
6.  <span data-ttu-id="76348-197">Une fois les validations terminées, vous pouvez sélectionner « Validations terminées ». L’environnement de test de basculement est alors nettoyé.</span><span class="sxs-lookup"><span data-stu-id="76348-197">Once the validations are complete, you can select ‘Validations complete’ and the test failover environment will be cleaned.</span></span>

<span data-ttu-id="76348-198">Suivez [ce guide](site-recovery-test-failover-to-azure.md) pour effectuer un test de basculement.</span><span class="sxs-lookup"><span data-stu-id="76348-198">Follow [this guidance](site-recovery-test-failover-to-azure.md) to do a test failover.</span></span>

### <a name="doing-a-failover"></a><span data-ttu-id="76348-199">Exécution d’un basculement</span><span class="sxs-lookup"><span data-stu-id="76348-199">Doing a failover</span></span>

1.  <span data-ttu-id="76348-200">Accédez au portail Azure et sélectionnez votre coffre Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="76348-200">Go to Azure  portal and select your Site Recovery vault.</span></span>
2.  <span data-ttu-id="76348-201">Cliquez sur le plan de récupération créé pour Dynamics AX.</span><span class="sxs-lookup"><span data-stu-id="76348-201">Click on the recovery plan created for Dynamics AX.</span></span>
3.  <span data-ttu-id="76348-202">Cliquez sur « Basculement » et sélectionnez « Basculement ».</span><span class="sxs-lookup"><span data-stu-id="76348-202">Click on ‘Failover’ and select ‘ Failover’.</span></span>
4.  <span data-ttu-id="76348-203">Sélectionnez le réseau cible et cliquez sur ✓ pour démarrer le processus de basculement.</span><span class="sxs-lookup"><span data-stu-id="76348-203">Select the target network and click ✓ to start the failover process.</span></span>

<span data-ttu-id="76348-204">Suivez [ce guide](site-recovery-failover.md) lorsque vous effectuez un basculement.</span><span class="sxs-lookup"><span data-stu-id="76348-204">Follow [this guidance](site-recovery-failover.md) when you are doing a failover.</span></span>

### <a name="perform-a-failback"></a><span data-ttu-id="76348-205">Effectuer une restauration automatique</span><span class="sxs-lookup"><span data-stu-id="76348-205">Perform a Failback</span></span>

<span data-ttu-id="76348-206">Reportez-vous au guide d’accompagnement « Solution de récupération d’urgence de SQL Server » pour obtenir des considérations spécifiques à SQL Server lors de la restauration automatique.</span><span class="sxs-lookup"><span data-stu-id="76348-206">Refer to ‘SQL Server DR Solution ’ companion guide for considerations specific to SQL server during Failback.</span></span>

1.  <span data-ttu-id="76348-207">Accédez au portail Azure et sélectionnez votre coffre Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="76348-207">Go to Azure  portal and select your Site Recovery vault.</span></span>
2.  <span data-ttu-id="76348-208">Cliquez sur le plan de récupération créé pour Dynamics AX.</span><span class="sxs-lookup"><span data-stu-id="76348-208">Click on the recovery plan created for Dynamics AX.</span></span>
3.  <span data-ttu-id="76348-209">Cliquez sur « Basculement » et sélectionnez le basculement.</span><span class="sxs-lookup"><span data-stu-id="76348-209">Click on ‘Failover’ and select failover.</span></span>
4.  <span data-ttu-id="76348-210">Cliquez sur « Changer de direction ».</span><span class="sxs-lookup"><span data-stu-id="76348-210">Click on ‘Change Direction’.</span></span>
5.  <span data-ttu-id="76348-211">Sélectionnez les options de synchronisation de données et de création de machines virtuelles appropriées</span><span class="sxs-lookup"><span data-stu-id="76348-211">Select the appropriate options - data synchronization and VM creation options</span></span>
6.  <span data-ttu-id="76348-212">Cliquez sur ✓ pour démarrer le processus de « restauration automatique ».</span><span class="sxs-lookup"><span data-stu-id="76348-212">Click ✓ to start the ‘Failback’ process.</span></span>


<span data-ttu-id="76348-213">Suivez [ce guide](site-recovery-failback-azure-to-vmware.md) lorsque vous effectuez une restauration automatique.</span><span class="sxs-lookup"><span data-stu-id="76348-213">Follow [this guidance](site-recovery-failback-azure-to-vmware.md) when you are doing a failback.</span></span>

##<a name="summary"></a><span data-ttu-id="76348-214">Résumé</span><span class="sxs-lookup"><span data-stu-id="76348-214">Summary</span></span>
<span data-ttu-id="76348-215">À l’aide d’Azure Site Recovery, vous pouvez créer un plan de récupération d’urgence automatisée complet pour votre application Dynamics AX.</span><span class="sxs-lookup"><span data-stu-id="76348-215">Using Azure Site Recovery, you can create a complete automated disaster recovery plan for your Dynamics AX application.</span></span> <span data-ttu-id="76348-216">Vous pouvez lancer le basculement en quelques secondes, où que vous soyez, et bénéficier d’une application opérationnelle en quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="76348-216">You can initiate the failover within seconds from anywhere in the event of a disruption and get the application up and running in minutes.</span></span>

## <a name="next-steps"></a><span data-ttu-id="76348-217">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="76348-217">Next steps</span></span>
<span data-ttu-id="76348-218">Pour en savoir plus sur la protection des charges de travail d’entreprise avec Azure Site Recovery, consultez [Quelles charges de travail pouvez-vous protéger avec Azure Site Recovery ?](site-recovery-workload.md).</span><span class="sxs-lookup"><span data-stu-id="76348-218">Read [What workloads can I protect?](site-recovery-workload.md) to learn more about protecting enterprise workloads with Azure Site Recovery.</span></span>
