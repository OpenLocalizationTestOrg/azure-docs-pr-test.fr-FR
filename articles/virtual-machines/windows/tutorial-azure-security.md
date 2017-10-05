---
title: Azure Security Center et machines virtuelles Windows dans Azure | Microsoft Docs
description: "Découvrez plus d’informations sur la sécurité de votre machine virtuelle Windows Azure avec Azure Security Center."
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 05/01/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: adb00e28b0b204858a763f83836ee2ac96f8f9e4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="monitor-virtual-machine-security-by-using-azure-security-center"></a><span data-ttu-id="b1ec4-103">Surveiller la sécurité des machines virtuelles à l’aide d’Azure Security Center</span><span class="sxs-lookup"><span data-stu-id="b1ec4-103">Monitor virtual machine security by using Azure Security Center</span></span>

<span data-ttu-id="b1ec4-104">Azure Security Center peut vous aider à acquérir une meilleure visibilité des pratiques de sécurité de vos ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="b1ec4-104">Azure Security Center can help you gain visibility into your Azure resource security practices.</span></span> <span data-ttu-id="b1ec4-105">Azure Security Center assure une surveillance intégrée de la sécurité.</span><span class="sxs-lookup"><span data-stu-id="b1ec4-105">Security Center offers integrated security monitoring.</span></span> <span data-ttu-id="b1ec4-106">Il peut détecter des menaces qui sans cela pourraient passer inaperçues.</span><span class="sxs-lookup"><span data-stu-id="b1ec4-106">It can detect threats that otherwise might go unnoticed.</span></span> <span data-ttu-id="b1ec4-107">Ce didacticiel décrit Azure Security Center et comment effectuer les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="b1ec4-107">In this tutorial, you learn about Azure Security Center, and how to:</span></span>
 
> [!div class="checklist"]
> * <span data-ttu-id="b1ec4-108">Configurer la collecte de données</span><span class="sxs-lookup"><span data-stu-id="b1ec4-108">Set up data collection</span></span>
> * <span data-ttu-id="b1ec4-109">Définir des stratégies de sécurité</span><span class="sxs-lookup"><span data-stu-id="b1ec4-109">Set up security policies</span></span>
> * <span data-ttu-id="b1ec4-110">Afficher et résoudre des problèmes d’intégrité de configuration</span><span class="sxs-lookup"><span data-stu-id="b1ec4-110">View and fix configuration health issues</span></span>
> * <span data-ttu-id="b1ec4-111">Examiner les menaces détectées</span><span class="sxs-lookup"><span data-stu-id="b1ec4-111">Review detected threats</span></span>  

## <a name="security-center-overview"></a><span data-ttu-id="b1ec4-112">Vue d’ensemble de Security Center</span><span class="sxs-lookup"><span data-stu-id="b1ec4-112">Security Center overview</span></span>

<span data-ttu-id="b1ec4-113">Security Center identifie des problèmes potentiels de configuration des machines virtuelles et des menaces de sécurité ciblées.</span><span class="sxs-lookup"><span data-stu-id="b1ec4-113">Security Center identifies potential virtual machine (VM) configuration issues and targeted security threats.</span></span> <span data-ttu-id="b1ec4-114">Il peut s’agir de machines virtuelles dépourvues de groupes de sécurité réseau, de disques non chiffrés et d’attaques RDP (Remote Desktop Protocol) par force brute.</span><span class="sxs-lookup"><span data-stu-id="b1ec4-114">These might include VMs that are missing network security groups, unencrypted disks, and brute-force Remote Desktop Protocol (RDP) attacks.</span></span> <span data-ttu-id="b1ec4-115">Les informations s’affichent sur le tableau de bord de Security Center dans des graphiques aisément lisibles.</span><span class="sxs-lookup"><span data-stu-id="b1ec4-115">The information is shown on the Security Center dashboard in easy-to-read graphs.</span></span>

<span data-ttu-id="b1ec4-116">Pour accéder au tableau de bord de Security Center, dans le menu du portail Azure, sélectionnez **Security Center**.</span><span class="sxs-lookup"><span data-stu-id="b1ec4-116">To access the Security Center dashboard, in the Azure portal, on the menu, select  **Security Center**.</span></span> <span data-ttu-id="b1ec4-117">Le tableau de bord montre l’état d’intégrité de la sécurité de votre environnement Azure, différentes recommandations courantes, ainsi que l’état actuel des alertes de menace.</span><span class="sxs-lookup"><span data-stu-id="b1ec4-117">On the dashboard, you can see the security health of your Azure environment, find a count of current recommendations, and view the current state of threat alerts.</span></span> <span data-ttu-id="b1ec4-118">Vous pouvez développer chaque graphique général pour afficher plus de détails.</span><span class="sxs-lookup"><span data-stu-id="b1ec4-118">You can expand each high-level chart to see more detail.</span></span>

![Tableau de bord de Security Center](./media/tutorial-azure-security/asc-dash.png)

<span data-ttu-id="b1ec4-120">Security Center va au-delà de la découverte de données et fournit des recommandations concernant les problèmes qu’il détecte.</span><span class="sxs-lookup"><span data-stu-id="b1ec4-120">Security Center goes beyond data discovery to provide recommendations for issues that it detects.</span></span> <span data-ttu-id="b1ec4-121">Par exemple, si une machine virtuelle a été déployée sans groupe de sécurité réseau associé, Security Center affiche une recommandation ainsi que des étapes de correction que vous pouvez suivre.</span><span class="sxs-lookup"><span data-stu-id="b1ec4-121">For example, if a VM was deployed without an attached network security group, Security Center displays a recommendation, with remediation steps you can take.</span></span> <span data-ttu-id="b1ec4-122">Vous bénéficiez d’une correction automatisée sans quitter le contexte de Security Center.</span><span class="sxs-lookup"><span data-stu-id="b1ec4-122">You get automated remediation without leaving the context of Security Center.</span></span>  

![Recommandations](./media/tutorial-azure-security/recommendations.png)

## <a name="set-up-data-collection"></a><span data-ttu-id="b1ec4-124">Configurer la collecte de données</span><span class="sxs-lookup"><span data-stu-id="b1ec4-124">Set up data collection</span></span>

<span data-ttu-id="b1ec4-125">Avant d’obtenir une visibilité des configurations de sécurité des machines virtuelles, vous devez configurer la collecte de données de Security Center.</span><span class="sxs-lookup"><span data-stu-id="b1ec4-125">Before you can get visibility into VM security configurations, you need to set up Security Center data collection.</span></span> <span data-ttu-id="b1ec4-126">Ceci implique d’activer la collecte de données et de créer un compte de stockage Azure pour stocker les données collectées.</span><span class="sxs-lookup"><span data-stu-id="b1ec4-126">This involves turning on data collection and creating an Azure storage account to hold collected data.</span></span> 

1. <span data-ttu-id="b1ec4-127">Dans le tableau de bord de Security Center, cliquez sur **Stratégie de sécurité** puis sélectionnez votre abonnement.</span><span class="sxs-lookup"><span data-stu-id="b1ec4-127">On the Security Center dashboard, click **Security policy**, and then select your subscription.</span></span> 
2. <span data-ttu-id="b1ec4-128">Pour **Collecte de données**, sélectionnez **Activée**.</span><span class="sxs-lookup"><span data-stu-id="b1ec4-128">For **Data collection**, select **On**.</span></span>
3. <span data-ttu-id="b1ec4-129">Pour créer un compte de stockage, sélectionnez **Choisir un compte de stockage**.</span><span class="sxs-lookup"><span data-stu-id="b1ec4-129">To create a storage account, select **Choose a storage account**.</span></span> <span data-ttu-id="b1ec4-130">Ensuite, sélectionnez **OK**.</span><span class="sxs-lookup"><span data-stu-id="b1ec4-130">Then, select **OK**.</span></span>
4. <span data-ttu-id="b1ec4-131">Dans le panneau **Stratégie de sécurité**, sélectionnez **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="b1ec4-131">On the **Security Policy** blade, select **Save**.</span></span> 

<span data-ttu-id="b1ec4-132">L’agent de collecte de données de Security Center est alors installé sur toutes les machines virtuelles, puis la collecte de données commence.</span><span class="sxs-lookup"><span data-stu-id="b1ec4-132">The Security Center data collection agent is then installed on all VMs, and data collection begins.</span></span> 

## <a name="set-up-a-security-policy"></a><span data-ttu-id="b1ec4-133">Configurer une stratégie de sécurité</span><span class="sxs-lookup"><span data-stu-id="b1ec4-133">Set up a security policy</span></span>

<span data-ttu-id="b1ec4-134">Les stratégies de sécurité permettent de définir les éléments pour lesquels Security Center collecte des données et formule des recommandations.</span><span class="sxs-lookup"><span data-stu-id="b1ec4-134">Security policies are used to define the items for which Security Center collects data and makes recommendations.</span></span> <span data-ttu-id="b1ec4-135">Vous pouvez appliquer des stratégies de sécurité différentes à différents ensembles de ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="b1ec4-135">You can apply different security policies to different sets of Azure resources.</span></span> <span data-ttu-id="b1ec4-136">Bien que par défaut les ressources Azure soient évaluées pour tous les éléments de la stratégie, vous pouvez désactiver des éléments individuels de la stratégie pour toutes les ressources ou pour un groupe de ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="b1ec4-136">Although by default Azure resources are evaluated against all policy items, you can turn off individual policy items for all Azure resources or for a resource group.</span></span> <span data-ttu-id="b1ec4-137">Pour obtenir des informations détaillées sur les stratégies de sécurité de Security Center, consultez [Définir des stratégies de sécurité dans Azure Security Center](../../security-center/security-center-policies.md).</span><span class="sxs-lookup"><span data-stu-id="b1ec4-137">For in-depth information about Security Center security policies, see [Set security policies in Azure Security Center](../../security-center/security-center-policies.md).</span></span> 

<span data-ttu-id="b1ec4-138">Pour configurer une stratégie de sécurité pour toutes les ressources Azure :</span><span class="sxs-lookup"><span data-stu-id="b1ec4-138">To set up a security policy for all Azure resources:</span></span>

1. <span data-ttu-id="b1ec4-139">Dans le tableau de bord de Security Center, cliquez sur **Stratégie de sécurité** puis sélectionnez votre abonnement.</span><span class="sxs-lookup"><span data-stu-id="b1ec4-139">On the Security Center dashboard, select **Security policy**, and then select your subscription.</span></span>
2. <span data-ttu-id="b1ec4-140">Sélectionnez **Stratégie de prévention**.</span><span class="sxs-lookup"><span data-stu-id="b1ec4-140">Select **Prevention policy**.</span></span>
3. <span data-ttu-id="b1ec4-141">Activez ou désactivez les éléments de la stratégie que vous voulez appliquer à toutes les ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="b1ec4-141">Turn on or turn off policy items that you want to apply to all Azure resources.</span></span>
4. <span data-ttu-id="b1ec4-142">Quand vous avez fini de sélectionner vos paramètres, choisissez **OK**.</span><span class="sxs-lookup"><span data-stu-id="b1ec4-142">When you're finished selecting your settings, select **OK**.</span></span>
5. <span data-ttu-id="b1ec4-143">Dans le panneau **Stratégie de sécurité**, sélectionnez **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="b1ec4-143">On the **Security policy** blade, select **Save**.</span></span> 

<span data-ttu-id="b1ec4-144">Pour définir une stratégie pour un groupe de ressources spécifique :</span><span class="sxs-lookup"><span data-stu-id="b1ec4-144">To set up a policy for a specific resource group:</span></span>

1. <span data-ttu-id="b1ec4-145">Dans le tableau de bord de Security Center, sélectionnez **Stratégie de sécurité** puis choisissez un groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="b1ec4-145">On the Security Center dashboard, select **Security policy**, and then select a resource group.</span></span>
2. <span data-ttu-id="b1ec4-146">Sélectionnez **Stratégie de prévention**.</span><span class="sxs-lookup"><span data-stu-id="b1ec4-146">Select **Prevention policy**.</span></span>
3. <span data-ttu-id="b1ec4-147">Activez ou désactivez les éléments de la stratégie que vous voulez appliquer au groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="b1ec4-147">Turn on or turn off policy items that you want to apply to the resource group.</span></span>
4. <span data-ttu-id="b1ec4-148">Sous **HÉRITAGE**, sélectionnez **Unique**.</span><span class="sxs-lookup"><span data-stu-id="b1ec4-148">Under **INHERITANCE**, select **Unique**.</span></span>
5. <span data-ttu-id="b1ec4-149">Quand vous avez fini de sélectionner vos paramètres, choisissez **OK**.</span><span class="sxs-lookup"><span data-stu-id="b1ec4-149">When you're finished selecting your settings, select **OK**.</span></span>
6. <span data-ttu-id="b1ec4-150">Dans le panneau **Stratégie de sécurité**, sélectionnez **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="b1ec4-150">On the **Security policy** blade, select **Save**.</span></span>  

<span data-ttu-id="b1ec4-151">Dans cette page, vous pouvez également désactiver la collecte des données pour un groupe de ressources spécifique.</span><span class="sxs-lookup"><span data-stu-id="b1ec4-151">You also can turn off data collection for a specific resource group on this page.</span></span>

<span data-ttu-id="b1ec4-152">Dans l’exemple suivant, une stratégie unique a été créée pour un groupe de ressources nommé *myResoureGroup*.</span><span class="sxs-lookup"><span data-stu-id="b1ec4-152">In the following example, a unique policy has been created for a resource group named *myResoureGroup*.</span></span> <span data-ttu-id="b1ec4-153">Dans cette stratégie, les recommandations en matière de chiffrement de disque et de pare-feu d’applications web sont désactivées.</span><span class="sxs-lookup"><span data-stu-id="b1ec4-153">In this policy, disk encryption and web application firewall recommendations are turned off.</span></span>

![Stratégie unique](./media/tutorial-azure-security/unique-policy.png)

## <a name="view-vm-configuration-health"></a><span data-ttu-id="b1ec4-155">Afficher l’état de configuration des machines virtuelles</span><span class="sxs-lookup"><span data-stu-id="b1ec4-155">View VM configuration health</span></span>

<span data-ttu-id="b1ec4-156">Après que vous avez activé la collecte de données et défini une stratégie de sécurité, Security Center commence à fournir des alertes et des recommandations.</span><span class="sxs-lookup"><span data-stu-id="b1ec4-156">After you've turned on data collection and set a security policy, Security Center begins to provide alerts and recommendations.</span></span> <span data-ttu-id="b1ec4-157">À mesure que des machines virtuelles sont déployées, l’agent de collecte de données est installé.</span><span class="sxs-lookup"><span data-stu-id="b1ec4-157">As VMs are deployed, the data collection agent is installed.</span></span> <span data-ttu-id="b1ec4-158">Security Center reçoit ensuite des données relatives aux nouvelles machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="b1ec4-158">Security Center is then populated with data for the new VMs.</span></span> <span data-ttu-id="b1ec4-159">Pour des informations détaillées sur l’intégrité de la configuration des machines virtuelles, consultez [Protéger vos machines virtuelles dans Security Center](../../security-center/security-center-virtual-machine-recommendations.md).</span><span class="sxs-lookup"><span data-stu-id="b1ec4-159">For in-depth information about VM configuration health, see [Protect your VMs in Security Center](../../security-center/security-center-virtual-machine-recommendations.md).</span></span> 

<span data-ttu-id="b1ec4-160">À mesure que des données sont collectées, les informations sur l’état d’intégrité des ressources de chaque machine virtuelle et des ressources Azure associées sont agrégées.</span><span class="sxs-lookup"><span data-stu-id="b1ec4-160">As data is collected, the resource health for each VM and related Azure resource is aggregated.</span></span> <span data-ttu-id="b1ec4-161">Les informations sont affichées dans un graphique aisément lisible.</span><span class="sxs-lookup"><span data-stu-id="b1ec4-161">The information is shown in an easy-to-read chart.</span></span> 

<span data-ttu-id="b1ec4-162">Pour afficher l’intégrité des ressources :</span><span class="sxs-lookup"><span data-stu-id="b1ec4-162">To view resource health:</span></span>

1.  <span data-ttu-id="b1ec4-163">Dans le tableau de bord de Security Center, sous **Intégrité de la sécurité des ressources**, sélectionnez **Calcul**.</span><span class="sxs-lookup"><span data-stu-id="b1ec4-163">On the Security Center dashboard, under **Resource security health**, select **Compute**.</span></span> 
2.  <span data-ttu-id="b1ec4-164">Dans le panneau **Calcul**, sélectionnez **Machines virtuelles**.</span><span class="sxs-lookup"><span data-stu-id="b1ec4-164">On the **Compute** blade, select **Virtual machines**.</span></span> <span data-ttu-id="b1ec4-165">Cette vue fournit un récapitulatif de l’état de la configuration de toutes vos machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="b1ec4-165">This view provides a summary of the configuration status for all your VMs.</span></span>

![Calculer l’état d’intégrité](./media/tutorial-azure-security/compute-health.png)

<span data-ttu-id="b1ec4-167">Pour voir toutes les recommandations relatives à une machine virtuelle, sélectionnez celle-ci.</span><span class="sxs-lookup"><span data-stu-id="b1ec4-167">To see all recommendations for a VM, select the VM.</span></span> <span data-ttu-id="b1ec4-168">Les recommandations et la correction sont traitées plus en détail dans la section suivante de ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="b1ec4-168">Recommendations and remediation are covered in more detail in the next section of this tutorial.</span></span>

## <a name="remediate-configuration-issues"></a><span data-ttu-id="b1ec4-169">Corriger les problèmes de configuration</span><span class="sxs-lookup"><span data-stu-id="b1ec4-169">Remediate configuration issues</span></span>

<span data-ttu-id="b1ec4-170">Quand Security Center commence à recevoir des données de configuration, des recommandations sont formulées en fonction de la stratégie de sécurité configurée.</span><span class="sxs-lookup"><span data-stu-id="b1ec4-170">After Security Center begins to populate with configuration data, recommendations are made based on the security policy you set up.</span></span> <span data-ttu-id="b1ec4-171">Par exemple, si une machine virtuelle a été configurée sans groupe de sécurité réseau associé, une recommandation préconise d’en créer un.</span><span class="sxs-lookup"><span data-stu-id="b1ec4-171">For instance, if a VM was set up without an associated network security group, a recommendation is made to create one.</span></span> 

<span data-ttu-id="b1ec4-172">Pour afficher la liste de toutes les recommandations :</span><span class="sxs-lookup"><span data-stu-id="b1ec4-172">To see a list of all recommendations:</span></span> 

1. <span data-ttu-id="b1ec4-173">Dans le tableau de bord de Security Center, sélectionnez **Recommandations**.</span><span class="sxs-lookup"><span data-stu-id="b1ec4-173">On the Security Center dashboard, select **Recommendations**.</span></span>
2. <span data-ttu-id="b1ec4-174">Sélectionnez une recommandation spécifique.</span><span class="sxs-lookup"><span data-stu-id="b1ec4-174">Select a specific recommendation.</span></span> <span data-ttu-id="b1ec4-175">La liste de toutes les ressources auxquelles la recommandation s’applique s’affiche.</span><span class="sxs-lookup"><span data-stu-id="b1ec4-175">A list of all resources for which the recommendation applies appears.</span></span>
3. <span data-ttu-id="b1ec4-176">Pour appliquer une recommandation, sélectionnez une ressource spécifique.</span><span class="sxs-lookup"><span data-stu-id="b1ec4-176">To apply a recommendation, select a specific resource.</span></span> 
4. <span data-ttu-id="b1ec4-177">Suivez les instructions pour les étapes de correction.</span><span class="sxs-lookup"><span data-stu-id="b1ec4-177">Follow the instructions for remediation steps.</span></span> 

<span data-ttu-id="b1ec4-178">Dans de nombreux cas, Security Center propose des mesures que vous pouvez prendre pour suivre une recommandation sans quitter Security Center.</span><span class="sxs-lookup"><span data-stu-id="b1ec4-178">In many cases, Security Center provides actionable steps you can take to address a recommendation without leaving Security Center.</span></span> <span data-ttu-id="b1ec4-179">Dans l’exemple suivant, Security Center détecte un groupe de sécurité réseau qui a une règle de trafic entrant non restreinte.</span><span class="sxs-lookup"><span data-stu-id="b1ec4-179">In the following example, Security Center detects a network security group that has an unrestricted inbound rule.</span></span> <span data-ttu-id="b1ec4-180">Dans la page de recommandation, vous pouvez sélectionner le bouton **Modifier les règles de trafic entrant**.</span><span class="sxs-lookup"><span data-stu-id="b1ec4-180">On the recommendation page, you can select the **Edit inbound rules** button.</span></span> <span data-ttu-id="b1ec4-181">L’interface utilisateur nécessaire pour modifier la règle apparaît.</span><span class="sxs-lookup"><span data-stu-id="b1ec4-181">The UI that is needed to modify the rule appears.</span></span> 

![Recommandations](./media/tutorial-azure-security/remediation.png)

<span data-ttu-id="b1ec4-183">Les recommandations sont marquées comme étant résolues à mesure qu’elles sont appliquées.</span><span class="sxs-lookup"><span data-stu-id="b1ec4-183">As recommendations are remediated, they are marked as resolved.</span></span> 

## <a name="view-detected-threats"></a><span data-ttu-id="b1ec4-184">Consulter les menaces détectées</span><span class="sxs-lookup"><span data-stu-id="b1ec4-184">View detected threats</span></span>

<span data-ttu-id="b1ec4-185">En plus des recommandations concernant la configuration des ressources, Security Center affiche des alertes de détection de menaces.</span><span class="sxs-lookup"><span data-stu-id="b1ec4-185">In addition to resource configuration recommendations, Security Center displays threat detection alerts.</span></span> <span data-ttu-id="b1ec4-186">La fonctionnalité d’alertes de sécurité agrège les données collectées à partir de chaque machine virtuelle, des journaux de réseau Azure et des solutions partenaires connectées pour détecter les menaces de sécurité au niveau des ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="b1ec4-186">The security alerts feature aggregates data collected from each VM, Azure networking logs, and connected partner solutions to detect security threats against Azure resources.</span></span> <span data-ttu-id="b1ec4-187">Pour obtenir des informations détaillées sur les fonctionnalités de détection des menaces de Security Center, consultez [Fonctionnalités de détection d’Azure Security Center](../../security-center/security-center-detection-capabilities.md).</span><span class="sxs-lookup"><span data-stu-id="b1ec4-187">For in-depth information about Security Center threat detection capabilities, see [Azure Security Center detection capabilities](../../security-center/security-center-detection-capabilities.md).</span></span>

<span data-ttu-id="b1ec4-188">La fonctionnalité d’alertes de sécurité nécessite que le niveau tarifaire de Security Center soit porté de *Gratuit* à *Standard*.</span><span class="sxs-lookup"><span data-stu-id="b1ec4-188">The security alerts feature requires the Security Center pricing tier to be increased from *Free* to *Standard*.</span></span> <span data-ttu-id="b1ec4-189">Une **version d’évaluation gratuite** de 30 jours est disponible quand vous passez à ce niveau tarifaire supérieur.</span><span class="sxs-lookup"><span data-stu-id="b1ec4-189">A 30-day **free trial** is available when you move to this higher pricing tier.</span></span> 

<span data-ttu-id="b1ec4-190">Pour changer de niveau tarifaire :</span><span class="sxs-lookup"><span data-stu-id="b1ec4-190">To change the pricing tier:</span></span>  

1. <span data-ttu-id="b1ec4-191">Dans le tableau de bord de Security Center, cliquez sur **Stratégie de sécurité** puis sélectionnez votre abonnement.</span><span class="sxs-lookup"><span data-stu-id="b1ec4-191">On the Security Center dashboard, click **Security policy**, and then select your subscription.</span></span>
2. <span data-ttu-id="b1ec4-192">Sélectionnez **Niveau tarifaire**.</span><span class="sxs-lookup"><span data-stu-id="b1ec4-192">Select **Pricing tier**.</span></span>
3. <span data-ttu-id="b1ec4-193">Sélectionnez le nouveau niveau puis choisissez **Sélectionner**.</span><span class="sxs-lookup"><span data-stu-id="b1ec4-193">Select the new tier, and then select **Select**.</span></span>
4. <span data-ttu-id="b1ec4-194">Dans le panneau **Stratégie de sécurité**, sélectionnez **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="b1ec4-194">On the **Security policy** blade, select **Save**.</span></span> 

<span data-ttu-id="b1ec4-195">Après que vous avez changé le niveau tarifaire, le graphique des alertes de sécurité commence à se remplir à mesure que des menaces de sécurité sont détectées.</span><span class="sxs-lookup"><span data-stu-id="b1ec4-195">After you've changed the pricing tier, the security alerts graph begins to populate as security threats are detected.</span></span>

![Alertes de sécurité](./media/tutorial-azure-security/security-alerts.png)

<span data-ttu-id="b1ec4-197">Sélectionnez une alerte pour afficher des informations la concernant.</span><span class="sxs-lookup"><span data-stu-id="b1ec4-197">Select an alert to view information.</span></span> <span data-ttu-id="b1ec4-198">Par exemple, vous pouvez voir une description de la menace, l’heure de la détection, toutes les tentatives de la menace et la correction recommandée.</span><span class="sxs-lookup"><span data-stu-id="b1ec4-198">For example, you can see a description of the threat, the detection time, all threat attempts, and the recommended remediation.</span></span> <span data-ttu-id="b1ec4-199">Dans l’exemple suivant, une attaque RDP par force brute a été détectée, avec 294 tentatives RDP qui ont échoué.</span><span class="sxs-lookup"><span data-stu-id="b1ec4-199">In the following example, an RDP brute-force attack was detected, with 294 failed RDP attempts.</span></span> <span data-ttu-id="b1ec4-200">Une solution recommandée est fournie.</span><span class="sxs-lookup"><span data-stu-id="b1ec4-200">A recommended resolution is provided.</span></span>

![Attaque RDP](./media/tutorial-azure-security/rdp-attack.png)

## <a name="next-steps"></a><span data-ttu-id="b1ec4-202">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="b1ec4-202">Next steps</span></span>
<span data-ttu-id="b1ec4-203">Ce didacticiel vous a montré comment configurer Azure Security Center, puis examiner les machines virtuelles dans Azure Security Center.</span><span class="sxs-lookup"><span data-stu-id="b1ec4-203">In this tutorial, you set up Azure Security Center, and then reviewed VMs in Security Center.</span></span> <span data-ttu-id="b1ec4-204">Vous avez appris à effectuer les actions suivantes :</span><span class="sxs-lookup"><span data-stu-id="b1ec4-204">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="b1ec4-205">Configurer la collecte de données</span><span class="sxs-lookup"><span data-stu-id="b1ec4-205">Set up data collection</span></span>
> * <span data-ttu-id="b1ec4-206">Définir des stratégies de sécurité</span><span class="sxs-lookup"><span data-stu-id="b1ec4-206">Set up security policies</span></span>
> * <span data-ttu-id="b1ec4-207">Afficher et résoudre des problèmes d’intégrité de configuration</span><span class="sxs-lookup"><span data-stu-id="b1ec4-207">View and fix configuration health issues</span></span>
> * <span data-ttu-id="b1ec4-208">Examiner les menaces détectées</span><span class="sxs-lookup"><span data-stu-id="b1ec4-208">Review detected threats</span></span>

<span data-ttu-id="b1ec4-209">Passez au didacticiel suivant pour découvrir comment créer un pipeline CI/CD avec Visual Studio Team Services et une machine virtuelle Windows exécutant IIS.</span><span class="sxs-lookup"><span data-stu-id="b1ec4-209">Advance to the next tutorial to learn how to create a CI/CD pipeline with Visual Studio Team Services and a Windows VM running IIS.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="b1ec4-210">Pipeline CI/CD de Visual Studio Team Services</span><span class="sxs-lookup"><span data-stu-id="b1ec4-210">Visual Studio Team Services CI/CD pipeline</span></span>](./tutorial-vsts-iis-cicd.md)
