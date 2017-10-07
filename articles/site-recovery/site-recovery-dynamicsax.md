---
title: "aaaReplicate un déploiement de Dynamics AX à plusieurs niveaux à l’aide d’Azure Site Recovery | Documents Microsoft"
description: "Cet article décrit comment tooreplicate et protéger Dynamics AX à l’aide d’Azure Site Recovery"
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
ms.openlocfilehash: b974315ec50ab2ec43846b3d3f95c7de88b72fc3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-a-multi-tier-dynamics-ax-application-using-azure-site-recovery"></a><span data-ttu-id="60fdc-103">Répliquer une application Dynamics AX multiniveau à l’aide d’Azure Site Recovery</span><span class="sxs-lookup"><span data-stu-id="60fdc-103">Replicate a multi-tier Dynamics AX application using Azure Site Recovery</span></span>

## <a name="overview"></a><span data-ttu-id="60fdc-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="60fdc-104">Overview</span></span>


<span data-ttu-id="60fdc-105">Microsoft Dynamics AX est une des solution ERP les plus populaires de hello parmi les processus de toostandardized entreprises dans différents emplacements, gérer les ressources et simplifier la conformité.</span><span class="sxs-lookup"><span data-stu-id="60fdc-105">Microsoft Dynamics AX is one of hello most popular ERP solution among enterprises toostandardized process across locations, manage resources and simplifying compliance.</span></span> <span data-ttu-id="60fdc-106">Rassembler application hello est entreprise ou organisation tooan critiques il est très important toobe que que si un sinistre, application doit être en cours d’exécution dans le temps minimal.</span><span class="sxs-lookup"><span data-stu-id="60fdc-106">Considering hello application is business critical tooan organization it is very important toobe sure that if any disaster, application should be up and running in minimum time.</span></span>

<span data-ttu-id="60fdc-107">Aujourd'hui, Microsoft Dynamics AX ne fournit aucune capacité de récupération d’urgence prête à l’emploi.</span><span class="sxs-lookup"><span data-stu-id="60fdc-107">Today, Microsoft Dynamics AX  does not provide any out-of-the-box disaster recovery capabilities.</span></span> <span data-ttu-id="60fdc-108">Microsoft Dynamics AX comprend de nombreux composants de serveur comme base de données objet serveur d’applications, Active Directory (AD), SQL Server, SharePoint Server, etc. de serveur Reporting toomanage hello la récupération d’urgence de chacun de ces composants manuellement est non seulement coûteux, mais également sujette à erreurs.</span><span class="sxs-lookup"><span data-stu-id="60fdc-108">Microsoft Dynamics AX consists of many server components like Application Object Server, Active Directory (AD), SQL Database Server, SharePoint Server, Reporting Server etc. toomanage hello disaster recovery of each of these components manually is not only expensive but also error-prone.</span></span>

<span data-ttu-id="60fdc-109">Cet article explique en détail comment créer une solution de récupération d’urgence pour votre application Dynamics AX à l’aide d’[Azure Site Recovery](site-recovery-overview.md).</span><span class="sxs-lookup"><span data-stu-id="60fdc-109">This article explains in detail about how you can create a disaster recovery solution for your Dynamics AX application using [Azure Site Recovery](site-recovery-overview.md).</span></span> <span data-ttu-id="60fdc-110">Sont également couverts les basculements planifiés/non planifiés/de test à l’aide d’un plan de récupération en un seul clic, les configurations prises en charge et les prérequis.</span><span class="sxs-lookup"><span data-stu-id="60fdc-110">It also covers planned/unplanned/test failovers using one-click recovery plan, supported configurations, and prerequisites.</span></span>
<span data-ttu-id="60fdc-111">La solution de récupération d’urgence basée sur Azure Site Recovery est entièrement testée, certifiée et recommandée par Microsoft Dynamics AX.</span><span class="sxs-lookup"><span data-stu-id="60fdc-111">Azure Site Recovery based disaster recovery solution is fully tested, certified, and recommended by Microsoft Dynamics AX.</span></span>



## <a name="prerequisites"></a><span data-ttu-id="60fdc-112">Composants requis</span><span class="sxs-lookup"><span data-stu-id="60fdc-112">Prerequisites</span></span>

<span data-ttu-id="60fdc-113">Implémentation de la récupération d’urgence pour l’application Dynamics AX à l’aide d’Azure Site Recovery nécessite hello suivant des conditions préalables terminées.</span><span class="sxs-lookup"><span data-stu-id="60fdc-113">Implementing disaster recovery for Dynamics AX application using Azure Site Recovery requires hello following pre-requisites completed.</span></span>

<span data-ttu-id="60fdc-114">•    Un déploiement local de Dynamics AX a été configuré</span><span class="sxs-lookup"><span data-stu-id="60fdc-114">•   An on-premises Dynamics AX deployment has been set up</span></span>

<span data-ttu-id="60fdc-115">•    Un coffre Azure Site Recovery Services a été créé dans un abonnement Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="60fdc-115">•   Azure Site Recovery Services vault has been created in Microsoft Azure subscription</span></span>

<span data-ttu-id="60fdc-116">• Si Azure est le site de récupération, exécutez hello Azure Virtual Machine Readiness Assessment outil sur des machines virtuelles tooensure qu’ils sont compatibles avec les machines virtuelles Azure et Azure Site Recovery Services</span><span class="sxs-lookup"><span data-stu-id="60fdc-116">•   If Azure is your recovery site, run hello Azure Virtual Machine Readiness Assessment tool  on VMs tooensure that they are compatible with Azure VMs and Azure Site Recovery Services</span></span>


## <a name="site-recovery-support"></a><span data-ttu-id="60fdc-117">Prise en charge de Site Recovery</span><span class="sxs-lookup"><span data-stu-id="60fdc-117">Site Recovery support</span></span>

<span data-ttu-id="60fdc-118">Pour les besoins de hello de création de cet article, les machines virtuelles VMware 2012R3 Dynamics AX sur Windows Server 2012 R2, Enterprise ont été utilisés.</span><span class="sxs-lookup"><span data-stu-id="60fdc-118">For hello purpose of creating this article, VMware virtual machines with Dynamics AX  2012R3 on Windows Server 2012 R2 Enterprise were used.</span></span> <span data-ttu-id="60fdc-119">Réplication de récupération de site est agnostique en termes d’application, les recommandations hello fournies ici sont toohold attendu sur également les scénarios suivants.</span><span class="sxs-lookup"><span data-stu-id="60fdc-119">As site recovery replication is application agnostic, hello recommendations provided here are expected toohold on following scenarios as well.</span></span>

### <a name="source-and-target"></a><span data-ttu-id="60fdc-120">Source et cible</span><span class="sxs-lookup"><span data-stu-id="60fdc-120">Source and target</span></span>

<span data-ttu-id="60fdc-121">**Scénario**</span><span class="sxs-lookup"><span data-stu-id="60fdc-121">**Scenario**</span></span> | <span data-ttu-id="60fdc-122">**site secondaire de tooa**</span><span class="sxs-lookup"><span data-stu-id="60fdc-122">**tooa secondary site**</span></span> | <span data-ttu-id="60fdc-123">**tooAzure**</span><span class="sxs-lookup"><span data-stu-id="60fdc-123">**tooAzure**</span></span>
--- | --- | ---
<span data-ttu-id="60fdc-124">**Hyper-V**</span><span class="sxs-lookup"><span data-stu-id="60fdc-124">**Hyper-V**</span></span> | <span data-ttu-id="60fdc-125">Oui</span><span class="sxs-lookup"><span data-stu-id="60fdc-125">Yes</span></span> | <span data-ttu-id="60fdc-126">Oui</span><span class="sxs-lookup"><span data-stu-id="60fdc-126">Yes</span></span>
<span data-ttu-id="60fdc-127">**VMware**</span><span class="sxs-lookup"><span data-stu-id="60fdc-127">**VMware**</span></span> | <span data-ttu-id="60fdc-128">Oui</span><span class="sxs-lookup"><span data-stu-id="60fdc-128">Yes</span></span> | <span data-ttu-id="60fdc-129">Oui</span><span class="sxs-lookup"><span data-stu-id="60fdc-129">Yes</span></span>
<span data-ttu-id="60fdc-130">**Serveur physique**</span><span class="sxs-lookup"><span data-stu-id="60fdc-130">**Physical server**</span></span> | <span data-ttu-id="60fdc-131">Oui</span><span class="sxs-lookup"><span data-stu-id="60fdc-131">Yes</span></span> | <span data-ttu-id="60fdc-132">Oui</span><span class="sxs-lookup"><span data-stu-id="60fdc-132">Yes</span></span>

## <a name="enable-dr-of-dynamics-ax-application-using-azure-site-recovery"></a><span data-ttu-id="60fdc-133">Activer la récupération d’urgence de l’application Dynamics AX à l’aide d’Azure Site Recovery</span><span class="sxs-lookup"><span data-stu-id="60fdc-133">Enable DR of Dynamics AX application using Azure Site Recovery</span></span>
### <a name="protect-your-dynamics-ax-application"></a><span data-ttu-id="60fdc-134">Protéger votre application Dynamics AX</span><span class="sxs-lookup"><span data-stu-id="60fdc-134">Protect your Dynamics AX application</span></span>
<span data-ttu-id="60fdc-135">Chaque composant de hello Dynamics AX besoins toobe protégé tooenable hello application complète réplication et la récupération.</span><span class="sxs-lookup"><span data-stu-id="60fdc-135">Each component of hello Dynamics AX needs toobe protected tooenable hello complete application replication and recovery.</span></span> <span data-ttu-id="60fdc-136">Cette section couvre les points suivants :</span><span class="sxs-lookup"><span data-stu-id="60fdc-136">This section covers:</span></span>

<span data-ttu-id="60fdc-137">**1. Protection d’Active Directory**</span><span class="sxs-lookup"><span data-stu-id="60fdc-137">**1. Protection of Active Directory**</span></span>

<span data-ttu-id="60fdc-138">**2. Protection du niveau SQL**</span><span class="sxs-lookup"><span data-stu-id="60fdc-138">**2. Protection of SQL Tier**</span></span>

<span data-ttu-id="60fdc-139">**3. Protection des niveaux application et web**</span><span class="sxs-lookup"><span data-stu-id="60fdc-139">**3. Protection of App and Web Tiers**</span></span>

<span data-ttu-id="60fdc-140">**4. Configuration de la mise en réseau**</span><span class="sxs-lookup"><span data-stu-id="60fdc-140">**4. Networking configuration**</span></span>

<span data-ttu-id="60fdc-141">**5. Plan de récupération**</span><span class="sxs-lookup"><span data-stu-id="60fdc-141">**5. Recovery Plan**</span></span>

### <a name="1-setup-ad-and-dns-replication"></a><span data-ttu-id="60fdc-142">1. Configurer la réplication Active Directory et DNS</span><span class="sxs-lookup"><span data-stu-id="60fdc-142">1. Setup AD and DNS replication</span></span>

<span data-ttu-id="60fdc-143">Active Directory est requis sur le site de récupération d’urgence hello pour Dynamics AX application toofunction.</span><span class="sxs-lookup"><span data-stu-id="60fdc-143">Active Directory is required on hello DR site for Dynamics AX application toofunction.</span></span> <span data-ttu-id="60fdc-144">Il existe deux choix recommandés en fonction de la complexité de hello de l’environnement local du client de l’hello.</span><span class="sxs-lookup"><span data-stu-id="60fdc-144">There are two recommended choices based on hello complexity of hello customer’s on-premises environment.</span></span>

<span data-ttu-id="60fdc-145">**Option 1 :**</span><span class="sxs-lookup"><span data-stu-id="60fdc-145">**Option 1**</span></span>

<span data-ttu-id="60fdc-146">Si hello client dispose d’un petit nombre d’applications et un seul contrôleur de domaine pour l’ensemble de son site local et sera en cas d’échec sur l’intégralité du site hello ensemble, il est recommandé à l’aide de réplication ASR tooreplicate hello DC machine toosecondary site ( applicable pour le Site tooSite et tooAzure de Site).</span><span class="sxs-lookup"><span data-stu-id="60fdc-146">If hello customer has a small number of applications and a single domain controller for his entire on-premises site and will be failing over hello entire site together, then we recommend using ASR-Replication tooreplicate hello DC machine toosecondary site (applicable for both Site tooSite and Site tooAzure).</span></span>

<span data-ttu-id="60fdc-147">**Option 2 :**</span><span class="sxs-lookup"><span data-stu-id="60fdc-147">**Option 2**</span></span>

<span data-ttu-id="60fdc-148">Si hello client comporte un grand nombre d’applications et une forêt Active Directory est en cours d’exécution et bascule peu d’applications à la fois, nous vous recommandons de configurer le contrôleur de domaine supplémentaire sur le site de récupération d’urgence de hello (site secondaire ou dans Azure).</span><span class="sxs-lookup"><span data-stu-id="60fdc-148">If hello customer has a large number of applications and is running an Active Directory forest and will fail-over few applications at a time, then we recommend setting up an additional domain controller on hello DR site (secondary site or in Azure).</span></span>

<span data-ttu-id="60fdc-149">Reportez-vous trop[guide d’accompagnement sur la création d’un contrôleur de domaine disponible sur le site de récupération d’urgence](site-recovery-active-directory.md).</span><span class="sxs-lookup"><span data-stu-id="60fdc-149">Please refer too[companion guide on making a domain controller available on DR site](site-recovery-active-directory.md).</span></span> <span data-ttu-id="60fdc-150">Pour le reste de ce document, nous supposons qu'un contrôleur de domaine est disponible sur le site de récupération d’urgence.</span><span class="sxs-lookup"><span data-stu-id="60fdc-150">For remainder of this document we will assume a DC is available on DR site.</span></span>

### <a name="2-setup-sql-server-replication"></a><span data-ttu-id="60fdc-151">2. Configurer la réplication SQL Server</span><span class="sxs-lookup"><span data-stu-id="60fdc-151">2. Setup SQL Server replication</span></span>
<span data-ttu-id="60fdc-152">Pour des conseils techniques détaillés sur hello recommandé de l’option de protection, consultez guide de toocompanion [niveau SQL](site-recovery-sql.md).</span><span class="sxs-lookup"><span data-stu-id="60fdc-152">Please refer toocompanion guide  for detailed technical guidance on hello recommended option for protecting [SQL tier](site-recovery-sql.md).</span></span>

### <a name="3-enable-protection-for-dynamics-ax-client-and-aos-vms"></a><span data-ttu-id="60fdc-153">3. Activer la protection des machines virtuelles AOS et du client Dynamics AX</span><span class="sxs-lookup"><span data-stu-id="60fdc-153">3. Enable protection for Dynamics AX client and AOS VMs</span></span>
<span data-ttu-id="60fdc-154">Effectuer une configuration Azure Site Recovery applique selon que les ordinateurs virtuels de hello sont déployés sur [Hyper-V](site-recovery-hyper-v-site-to-azure.md) ou sur [VMware](site-recovery-vmware-to-azure.md).</span><span class="sxs-lookup"><span data-stu-id="60fdc-154">Perform relevant Azure Site Recovery configuration based on whether hello VMs are deployed on [Hyper-V](site-recovery-hyper-v-site-to-azure.md) or on [VMware](site-recovery-vmware-to-azure.md).</span></span>

> [!TIP]
> <span data-ttu-id="60fdc-155">Tooconfigure de fréquence de cohérence incident recommandée est de 15 minutes.</span><span class="sxs-lookup"><span data-stu-id="60fdc-155">Recommended Crash consistent frequency tooconfigure is 15 minutes.</span></span>
>

<span data-ttu-id="60fdc-156">Hello ci-dessous instantané montre état de protection de hello des machines virtuelles de composant Dynamics dans le scénario de protection « TooAzure de site VMware ».</span><span class="sxs-lookup"><span data-stu-id="60fdc-156">hello below snapshot shows hello protection status of Dynamics component VMs in ‘VMware site tooAzure’ protection scenario.</span></span>
<span data-ttu-id="60fdc-157">![Éléments protégés ](./media/site-recovery-dynamics-ax/protecteditems.png)</span><span class="sxs-lookup"><span data-stu-id="60fdc-157">![Protected items ](./media/site-recovery-dynamics-ax/protecteditems.png)</span></span>

### <a name="4-configure-networking"></a><span data-ttu-id="60fdc-158">4. Configurer la mise en réseau</span><span class="sxs-lookup"><span data-stu-id="60fdc-158">4. Configure Networking</span></span>
<span data-ttu-id="60fdc-159">Configurer les paramètres Calcul et réseau des machines virtuelles</span><span class="sxs-lookup"><span data-stu-id="60fdc-159">Configure VM Compute and Network Settings</span></span>

<span data-ttu-id="60fdc-160">Pour le client AX hello et les machines virtuelles de AOS configurer les paramètres réseau dans Azure Site Recovery afin que les réseaux d’ordinateurs virtuels hello toohello attaché droite DR réseau après le basculement.</span><span class="sxs-lookup"><span data-stu-id="60fdc-160">For hello AX client and AOS VMs configure network settings in Azure Site Recovery so that hello VM networks get attached toohello right DR network after failover.</span></span> <span data-ttu-id="60fdc-161">Vérifiez le réseau de récupération d’urgence hello pour ces niveaux est le niveau SQL toohello routable.</span><span class="sxs-lookup"><span data-stu-id="60fdc-161">Ensure hello DR network for these tiers is routable toohello SQL tier.</span></span>

<span data-ttu-id="60fdc-162">Vous pouvez sélectionner hello VM Bonjour répliquées de paramètres de réseau éléments tooconfigure hello comme indiqué dans l’instantané hello ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="60fdc-162">You can select hello VM in hello replicated items tooconfigure hello network settings as shown in hello snapshot below.</span></span>

* <span data-ttu-id="60fdc-163">Pour les serveurs AOS sélectionnez hello à haute disponibilité correct.</span><span class="sxs-lookup"><span data-stu-id="60fdc-163">For AOS servers select hello correct availability set.</span></span>

* <span data-ttu-id="60fdc-164">Si vous utilisez une adresse IP statique, puis spécifiez IP hello souhaité hello tootake de machine virtuelle Bonjour **adresse IP cible** champ ![paramètres réseau](./media/site-recovery-dynamics-ax/vmpropertiesaos1.png)</span><span class="sxs-lookup"><span data-stu-id="60fdc-164">If you are using a static IP then specify hello IP that you want hello virtual machine tootake in hello **Target IP** field ![Network Settings ](./media/site-recovery-dynamics-ax/vmpropertiesaos1.png)</span></span>



### <a name="5-creating-a-recovery-plan"></a><span data-ttu-id="60fdc-165">5. Création d’un plan de récupération</span><span class="sxs-lookup"><span data-stu-id="60fdc-165">5. Creating a recovery plan</span></span>

<span data-ttu-id="60fdc-166">Vous pouvez créer un plan de récupération dans le processus de basculement d’Azure Site Recovery tooautomate hello.</span><span class="sxs-lookup"><span data-stu-id="60fdc-166">You can create a recovery plan in Azure Site Recovery tooautomate hello failover process.</span></span> <span data-ttu-id="60fdc-167">Ajouter des couches d’application et web Bonjour un Plan de récupération.</span><span class="sxs-lookup"><span data-stu-id="60fdc-167">Add app tier and web tier in hello Recovery Plan.</span></span> <span data-ttu-id="60fdc-168">Ordre dans différents groupes afin que hello frontal arrêt avant la couche application.</span><span class="sxs-lookup"><span data-stu-id="60fdc-168">Order them in different groups so that hello front-end shutdown before app tier.</span></span>

1)  <span data-ttu-id="60fdc-169">Sélectionnez le coffre Azure Site Recovery hello dans votre abonnement, puis cliquez sur la vignette de Plans de la récupération.</span><span class="sxs-lookup"><span data-stu-id="60fdc-169">Select hello Azure Site Recovery vault in your subscription and click on ‘Recovery Plans’ tile.</span></span>

2)  <span data-ttu-id="60fdc-170">Cliquez sur « + Plan de récupération » et spécifiez un nom.</span><span class="sxs-lookup"><span data-stu-id="60fdc-170">Click on ‘+ Recovery plan and specify a name.</span></span>

3)  <span data-ttu-id="60fdc-171">Sélectionnez hello 'Source' et 'Target'.</span><span class="sxs-lookup"><span data-stu-id="60fdc-171">Select hello ‘Source’ and ‘Target’.</span></span> <span data-ttu-id="60fdc-172">cible de Hello peut être le site Azure ou secondaire.</span><span class="sxs-lookup"><span data-stu-id="60fdc-172">hello target can be Azure or secondary site.</span></span> <span data-ttu-id="60fdc-173">Si vous choisissez d’Azure, vous devez spécifier le modèle de déploiement hello</span><span class="sxs-lookup"><span data-stu-id="60fdc-173">In case you choose Azure, you must specify hello deployment model</span></span>

![Créer un plan de récupération](./media/site-recovery-dynamics-ax/recoveryplancreation1.png)

4)  <span data-ttu-id="60fdc-175">Sélectionnez hello AOS et un plan de récupération client machines virtuelles toohello et cliquez sur ✓.</span><span class="sxs-lookup"><span data-stu-id="60fdc-175">Select hello AOS and client VMs toohello recovery plan and click ✓.</span></span>
<span data-ttu-id="60fdc-176">![Créer un plan de récupération](./media/site-recovery-dynamics-ax/selectvms.png)</span><span class="sxs-lookup"><span data-stu-id="60fdc-176">![Create Recovery Plan](./media/site-recovery-dynamics-ax/selectvms.png)</span></span>


![Plan de récupération](./media/site-recovery-dynamics-ax/recoveryplan.png)

<span data-ttu-id="60fdc-178">Vous pouvez personnaliser le plan de récupération hello pour l’application Dynamics AX en ajoutant plusieurs étapes comme indiqué ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="60fdc-178">You can customize hello recovery plan for Dynamics AX application by adding various steps as detailed below.</span></span> <span data-ttu-id="60fdc-179">Hello ci-dessus instantané montre hello plan de récupération complète après avoir ajouté toutes les étapes de hello.</span><span class="sxs-lookup"><span data-stu-id="60fdc-179">hello above snapshot shows hello complete recovery plan after adding all hello steps.</span></span>

<span data-ttu-id="60fdc-180">*Étapes :*</span><span class="sxs-lookup"><span data-stu-id="60fdc-180">*Steps:*</span></span>

<span data-ttu-id="60fdc-181">*1. Étapes du basculement SQL Server*</span><span class="sxs-lookup"><span data-stu-id="60fdc-181">*1. SQL Server fail over steps*</span></span>

<span data-ttu-id="60fdc-182">Consultez trop['Solution de récupération d’urgence de SQL Server'](site-recovery-sql.md) guide d’accompagnement pour plus d’informations sur le serveur de récupération étapes tooSQL spécifique.</span><span class="sxs-lookup"><span data-stu-id="60fdc-182">Refer too[‘SQL Server DR Solution’](site-recovery-sql.md) companion guide  for details about recovery steps specific tooSQL server.</span></span>

<span data-ttu-id="60fdc-183">*2. Basculement groupe 1 : Basculer les machines virtuelles de hello AOS*</span><span class="sxs-lookup"><span data-stu-id="60fdc-183">*2. Failover Group 1: Fail over hello AOS VMs*</span></span>

<span data-ttu-id="60fdc-184">Assurez-vous que le point de récupération de hello sélectionné est aussi proche que possible toohello de base de données PIT mais pas de manière anticipée.</span><span class="sxs-lookup"><span data-stu-id="60fdc-184">Make sure that hello recovery point selected is as close as possible toohello database PIT but not ahead.</span></span>

<span data-ttu-id="60fdc-185">*3. Script : Équilibrage de charge ajouter (uniquement E-A)* ajouter un script (via Azure automation) après le groupe de AOS VM apparaît tooadd un tooit d’équilibrage de charge.</span><span class="sxs-lookup"><span data-stu-id="60fdc-185">*3. Script: Add load balancer (Only E-A)* Add a script (via Azure automation) after AOS VM group comes up tooadd a load balancer tooit.</span></span> <span data-ttu-id="60fdc-186">Vous pouvez utiliser un script toodo cette tâche.</span><span class="sxs-lookup"><span data-stu-id="60fdc-186">You can use a script toodo this task.</span></span> <span data-ttu-id="60fdc-187">Consultez l’article [comment tooadd équilibrage de charge pour l’application à plusieurs niveaux récupération d’urgence](https://azure.microsoft.com/blog/cloud-migration-and-disaster-recovery-of-load-balanced-multi-tier-applications-using-azure-site-recovery/)</span><span class="sxs-lookup"><span data-stu-id="60fdc-187">Refer article [how tooadd load balancer for multi-tier application DR](https://azure.microsoft.com/blog/cloud-migration-and-disaster-recovery-of-load-balanced-multi-tier-applications-using-azure-site-recovery/)</span></span>

<span data-ttu-id="60fdc-188">*4. Basculement groupe 2 : Basculer hello AX client machines virtuelles.*</span><span class="sxs-lookup"><span data-stu-id="60fdc-188">*4. Failover Group 2: Fail over hello AX client VMs.*</span></span>
<span data-ttu-id="60fdc-189">Basculer le niveau hello web machines virtuelles dans le cadre du plan de récupération hello.</span><span class="sxs-lookup"><span data-stu-id="60fdc-189">Fail over hello web tier VMs as part of hello recovery plan.</span></span>


### <a name="doing-a-test-failover"></a><span data-ttu-id="60fdc-190">Exécution d’un test de basculement</span><span class="sxs-lookup"><span data-stu-id="60fdc-190">Doing a test failover</span></span>

<span data-ttu-id="60fdc-191">Consultez too'AD Solution de récupération d’urgence » et « Solution de récupération d’urgence de SQL Server » guides d’accompagnement pour tooAD spécifiques des considérations et SQL server respectivement durant le Test de basculement.</span><span class="sxs-lookup"><span data-stu-id="60fdc-191">Refer too‘AD DR Solution ’ and ‘SQL Server DR solution ’ companion guides for considerations specific tooAD and SQL server respectively during Test Failover.</span></span>

1.  <span data-ttu-id="60fdc-192">TooAzure portail, sélectionnez votre archivage Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="60fdc-192">Go tooAzure  portal and select your Site Recovery vault.</span></span>
2.  <span data-ttu-id="60fdc-193">Cliquez sur le plan de récupération hello créé pour Dynamics AX.</span><span class="sxs-lookup"><span data-stu-id="60fdc-193">Click on hello recovery plan created for Dynamics AX.</span></span>
3.  <span data-ttu-id="60fdc-194">Cliquez sur « Test de basculement ».</span><span class="sxs-lookup"><span data-stu-id="60fdc-194">Click on ‘Test Failover’.</span></span>
4.  <span data-ttu-id="60fdc-195">Sélectionnez le processus de basculement de test hello réseau virtuel toostart hello.</span><span class="sxs-lookup"><span data-stu-id="60fdc-195">Select hello virtual network toostart hello test fail-over process.</span></span>
5.  <span data-ttu-id="60fdc-196">Une fois les environnement secondaire hello, vous pouvez effectuer vos validations.</span><span class="sxs-lookup"><span data-stu-id="60fdc-196">Once hello secondary environment is up, you can perform your validations.</span></span>
6.  <span data-ttu-id="60fdc-197">Une fois les validations hello sont terminées, vous pouvez sélectionner 'Validations Terminer' et environnement de test de basculement hello est supprimé.</span><span class="sxs-lookup"><span data-stu-id="60fdc-197">Once hello validations are complete, you can select ‘Validations complete’ and hello test failover environment will be cleaned.</span></span>

<span data-ttu-id="60fdc-198">Suivez [ce guide](site-recovery-test-failover-to-azure.md) toodo un test de basculement.</span><span class="sxs-lookup"><span data-stu-id="60fdc-198">Follow [this guidance](site-recovery-test-failover-to-azure.md) toodo a test failover.</span></span>

### <a name="doing-a-failover"></a><span data-ttu-id="60fdc-199">Exécution d’un basculement</span><span class="sxs-lookup"><span data-stu-id="60fdc-199">Doing a failover</span></span>

1.  <span data-ttu-id="60fdc-200">TooAzure portail, sélectionnez votre archivage Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="60fdc-200">Go tooAzure  portal and select your Site Recovery vault.</span></span>
2.  <span data-ttu-id="60fdc-201">Cliquez sur le plan de récupération hello créé pour Dynamics AX.</span><span class="sxs-lookup"><span data-stu-id="60fdc-201">Click on hello recovery plan created for Dynamics AX.</span></span>
3.  <span data-ttu-id="60fdc-202">Cliquez sur « Basculement » et sélectionnez « Basculement ».</span><span class="sxs-lookup"><span data-stu-id="60fdc-202">Click on ‘Failover’ and select ‘ Failover’.</span></span>
4.  <span data-ttu-id="60fdc-203">Sélectionnez le réseau cible de hello et cliquez sur le processus de basculement ✓ toostart hello.</span><span class="sxs-lookup"><span data-stu-id="60fdc-203">Select hello target network and click ✓ toostart hello failover process.</span></span>

<span data-ttu-id="60fdc-204">Suivez [ce guide](site-recovery-failover.md) lorsque vous effectuez un basculement.</span><span class="sxs-lookup"><span data-stu-id="60fdc-204">Follow [this guidance](site-recovery-failover.md) when you are doing a failover.</span></span>

### <a name="perform-a-failback"></a><span data-ttu-id="60fdc-205">Effectuer une restauration automatique</span><span class="sxs-lookup"><span data-stu-id="60fdc-205">Perform a Failback</span></span>

<span data-ttu-id="60fdc-206">Consultez too'SQL Solution de récupération d’urgence du serveur « guide d’accompagnement pour le serveur de tooSQL spécifique de considérations lors de la restauration automatique.</span><span class="sxs-lookup"><span data-stu-id="60fdc-206">Refer too‘SQL Server DR Solution ’ companion guide for considerations specific tooSQL server during Failback.</span></span>

1.  <span data-ttu-id="60fdc-207">TooAzure portail, sélectionnez votre archivage Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="60fdc-207">Go tooAzure  portal and select your Site Recovery vault.</span></span>
2.  <span data-ttu-id="60fdc-208">Cliquez sur le plan de récupération hello créé pour Dynamics AX.</span><span class="sxs-lookup"><span data-stu-id="60fdc-208">Click on hello recovery plan created for Dynamics AX.</span></span>
3.  <span data-ttu-id="60fdc-209">Cliquez sur « Basculement » et sélectionnez le basculement.</span><span class="sxs-lookup"><span data-stu-id="60fdc-209">Click on ‘Failover’ and select failover.</span></span>
4.  <span data-ttu-id="60fdc-210">Cliquez sur « Changer de direction ».</span><span class="sxs-lookup"><span data-stu-id="60fdc-210">Click on ‘Change Direction’.</span></span>
5.  <span data-ttu-id="60fdc-211">Sélectionner les options appropriées hello - synchronisation des données et les options de création de machines virtuelles</span><span class="sxs-lookup"><span data-stu-id="60fdc-211">Select hello appropriate options - data synchronization and VM creation options</span></span>
6.  <span data-ttu-id="60fdc-212">Cliquez sur le processus de 'restauration automatique' ✓ toostart hello.</span><span class="sxs-lookup"><span data-stu-id="60fdc-212">Click ✓ toostart hello ‘Failback’ process.</span></span>


<span data-ttu-id="60fdc-213">Suivez [ce guide](site-recovery-failback-azure-to-vmware.md) lorsque vous effectuez une restauration automatique.</span><span class="sxs-lookup"><span data-stu-id="60fdc-213">Follow [this guidance](site-recovery-failback-azure-to-vmware.md) when you are doing a failback.</span></span>

##<a name="summary"></a><span data-ttu-id="60fdc-214">Résumé</span><span class="sxs-lookup"><span data-stu-id="60fdc-214">Summary</span></span>
<span data-ttu-id="60fdc-215">À l’aide d’Azure Site Recovery, vous pouvez créer un plan de récupération d’urgence automatisée complet pour votre application Dynamics AX.</span><span class="sxs-lookup"><span data-stu-id="60fdc-215">Using Azure Site Recovery, you can create a complete automated disaster recovery plan for your Dynamics AX application.</span></span> <span data-ttu-id="60fdc-216">Vous pouvez opérer le basculement de hello en quelques secondes à partir de n’importe où dans hello des événements d’une interruption de service et obtenir l’application hello opérationnel en quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="60fdc-216">You can initiate hello failover within seconds from anywhere in hello event of a disruption and get hello application up and running in minutes.</span></span>

## <a name="next-steps"></a><span data-ttu-id="60fdc-217">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="60fdc-217">Next steps</span></span>
<span data-ttu-id="60fdc-218">Lecture [les charges de travail puis-je protéger ?](site-recovery-workload.md) toolearn plus sur la protection des charges de travail enterprise avec Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="60fdc-218">Read [What workloads can I protect?](site-recovery-workload.md) toolearn more about protecting enterprise workloads with Azure Site Recovery.</span></span>
