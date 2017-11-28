---
title: "Présentation d’Azure Advisor | Microsoft Docs"
description: "Le conseiller Azure permet d’optimiser vos déploiements Azure."
services: advisor
documentationcenter: NA
author: kumudd
manager: carmonm
editor: 
ms.assetid: 
ms.service: advisor
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 11/16/2016
ms.author: kumud
ms.openlocfilehash: 35678142550f9f887562f311a5e7d9516495cf53
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="introduction-to-azure-advisor"></a><span data-ttu-id="d867a-103">Présentation d’Azure Advisor</span><span class="sxs-lookup"><span data-stu-id="d867a-103">Introduction to Azure Advisor</span></span>

<span data-ttu-id="d867a-104">Découvrez Azure Advisor et ses principales fonctionnalités et obtenez des réponses aux questions fréquemment posées.</span><span class="sxs-lookup"><span data-stu-id="d867a-104">Learn about Azure Advisor and its key capabilities, and get answers to frequently asked questions.</span></span>

## <a name="what-is-advisor"></a><span data-ttu-id="d867a-105">Qu’est-ce qu’Advisor ?</span><span class="sxs-lookup"><span data-stu-id="d867a-105">What is Advisor?</span></span>
<span data-ttu-id="d867a-106">Advisor est un conseiller personnalisé basé dans le cloud qui décrit les meilleures pratiques à suivre pour optimiser vos déploiements Azure.</span><span class="sxs-lookup"><span data-stu-id="d867a-106">Advisor is a personalized cloud consultant that helps you follow best practices to optimize your Azure deployments.</span></span> <span data-ttu-id="d867a-107">Il analyse votre télémétrie de configuration et d’utilisation des ressources, puis recommande des solutions qui peuvent vous aider à améliorer la rentabilité, les performances, la haute disponibilité et la sécurité de vos ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="d867a-107">It analyzes your resource configuration and usage telemetry and then recommends solutions that can help you improve the cost effectiveness, performance, high availability, and security of your Azure resources.</span></span>

<span data-ttu-id="d867a-108">Avec Advisor, vous pouvez :</span><span class="sxs-lookup"><span data-stu-id="d867a-108">With Advisor, you can:</span></span>
* <span data-ttu-id="d867a-109">Bénéficier de recommandations en termes de meilleures pratiques proactives, interactives et personnalisées.</span><span class="sxs-lookup"><span data-stu-id="d867a-109">Get proactive, actionable, and personalized best practices recommendations.</span></span> 
* <span data-ttu-id="d867a-110">Améliorer les performances, la sécurité et la haute disponibilité de vos ressources en identifiant les possibilités de réduction de vos dépenses Azure globales.</span><span class="sxs-lookup"><span data-stu-id="d867a-110">Improve the performance, security, and high availability of your resources, as you identify opportunities to reduce your overall Azure spend.</span></span>
* <span data-ttu-id="d867a-111">Obtenir des recommandations avec des propositions d’actions intégrées.</span><span class="sxs-lookup"><span data-stu-id="d867a-111">Get recommendations with proposed actions inline.</span></span>

<span data-ttu-id="d867a-112">Accéder à Advisor via le [portail Azure](https://aka.ms/azureadvisordashboard).</span><span class="sxs-lookup"><span data-stu-id="d867a-112">You can access Advisor through the [Azure portal](https://aka.ms/azureadvisordashboard).</span></span> <span data-ttu-id="d867a-113">Connectez-vous au [portail](https://portal.azure.com), sélectionnez **Parcourir**, puis faites défiler jusqu’à **Azure Advisor**.</span><span class="sxs-lookup"><span data-stu-id="d867a-113">Sign in to the [portal](https://portal.azure.com), select **Browse**, and then scroll to **Azure Advisor**.</span></span> <span data-ttu-id="d867a-114">Le tableau de bord du conseiller affiche des recommandations personnalisées pour un abonnement sélectionné.</span><span class="sxs-lookup"><span data-stu-id="d867a-114">The Advisor dashboard displays personalized recommendations for a selected subscription.</span></span> 

<span data-ttu-id="d867a-115">Les recommandations sont divisées en quatre catégories :</span><span class="sxs-lookup"><span data-stu-id="d867a-115">The recommendations are divided into four categories:</span></span> 

* <span data-ttu-id="d867a-116">**Haute disponibilité** : pour garantir et améliorer la continuité de vos applications stratégiques.</span><span class="sxs-lookup"><span data-stu-id="d867a-116">**High Availability**: To ensure and improve the continuity of your business-critical applications.</span></span> <span data-ttu-id="d867a-117">Pour plus d’informations, consultez [Recommandations du conseiller en matière de haute disponibilité](advisor-high-availability-recommendations.md).</span><span class="sxs-lookup"><span data-stu-id="d867a-117">For more information, see [Advisor High Availability recommendations](advisor-high-availability-recommendations.md).</span></span>

* <span data-ttu-id="d867a-118">**Sécurité** : permet de détecter les menaces et vulnérabilités pouvant conduire à des failles de sécurité.</span><span class="sxs-lookup"><span data-stu-id="d867a-118">**Security**: To detect threats and vulnerabilities that might lead to security breaches.</span></span> <span data-ttu-id="d867a-119">Pour plus d’informations, consultez [Recommandations du conseiller en matière de sécurité](advisor-security-recommendations.md).</span><span class="sxs-lookup"><span data-stu-id="d867a-119">For more information, see [Advisor Security recommendations](advisor-security-recommendations.md).</span></span>

* <span data-ttu-id="d867a-120">**Performances** : pour améliorer la vitesse de vos applications.</span><span class="sxs-lookup"><span data-stu-id="d867a-120">**Performance**: To improve the speed of your applications.</span></span> <span data-ttu-id="d867a-121">Pour plus d’informations, consultez [Recommandations du conseiller en matière de performances](advisor-performance-recommendations.md).</span><span class="sxs-lookup"><span data-stu-id="d867a-121">For more information, see [Advisor Performance recommendations](advisor-performance-recommendations.md).</span></span>

* <span data-ttu-id="d867a-122">**Coût** : pour optimiser et réduire vos dépenses Azure globales.</span><span class="sxs-lookup"><span data-stu-id="d867a-122">**Cost**: To optimize and reduce your overall Azure spend.</span></span> <span data-ttu-id="d867a-123">Pour plus d’informations, consultez [Recommandations du conseiller en matière de coût](advisor-cost-recommendations.md).</span><span class="sxs-lookup"><span data-stu-id="d867a-123">For more information, see [Advisor Cost recommendations](advisor-cost-recommendations.md).</span></span>

  ![Types de recommandation du conseiller](./media/advisor-overview/advisor-all-tab-examples.png)

> [!NOTE]
> <span data-ttu-id="d867a-125">Pour accéder aux recommandations d’Advisor, vous devez d’abord *inscrire votre abonnement*  auprès d’Advisor.</span><span class="sxs-lookup"><span data-stu-id="d867a-125">To access Advisor recommendations, you must first *register your subscription* with Advisor.</span></span> <span data-ttu-id="d867a-126">L’abonnement est inscrit lorsque son *propriétaire* lance le tableau de bord Advisor, puis clique sur le bouton **Obtenir des recommandations**.</span><span class="sxs-lookup"><span data-stu-id="d867a-126">A subscription is registered when a *subscription Owner* launches the Advisor dashboard and clicks the **Get recommendations** button.</span></span> <span data-ttu-id="d867a-127">Cette opération ne doit être *exécutée qu’une seule fois*.</span><span class="sxs-lookup"><span data-stu-id="d867a-127">This is a *one-time operation*.</span></span> <span data-ttu-id="d867a-128">Une fois l’abonnement inscrit, vous pouvez accéder aux recommandations d’Advisor en tant que *propriétaire*, *collaborateur* ou *lecteur* d’un abonnement, d’un groupe de ressources ou d’une ressource spécifique.</span><span class="sxs-lookup"><span data-stu-id="d867a-128">After the subscription is registered, you can access Advisor recommendations as *Owner*, *Contributor*, or *Reader* for a subscription, a resource group, or a specific resource.</span></span>

<span data-ttu-id="d867a-129">Vous pouvez cliquer sur une recommandation pour en savoir plus.</span><span class="sxs-lookup"><span data-stu-id="d867a-129">You can click a recommendation to learn more about it.</span></span> <span data-ttu-id="d867a-130">Vous pouvez également obtenir des informations sur les actions que vous pouvez effectuer pour tirer parti d’une opportunité ou résoudre un problème.</span><span class="sxs-lookup"><span data-stu-id="d867a-130">You can also learn about actions that you can perform to take advantage of an opportunity or resolve an issue.</span></span> 

<span data-ttu-id="d867a-131">Le conseiller fournit des recommandations accompagnées d’actions intégrées ou de liens vers de la documentation.</span><span class="sxs-lookup"><span data-stu-id="d867a-131">Advisor offers recommendations with inline actions or documentation links.</span></span> <span data-ttu-id="d867a-132">Cliquez sur une action intégrée pour découvrir comment l’implémenter.</span><span class="sxs-lookup"><span data-stu-id="d867a-132">Clicking an inline action takes you through a “guided user journey” to implement it.</span></span> <span data-ttu-id="d867a-133">Cliquez sur un lien de documentation pour accéder à la documentation qui décrit comment implémenter manuellement l’action.</span><span class="sxs-lookup"><span data-stu-id="d867a-133">Clicking a documentation link points you to documentation that describes how to manually implement the action.</span></span> 

<span data-ttu-id="d867a-134">Advisor met à jour les recommandations toutes les heures.</span><span class="sxs-lookup"><span data-stu-id="d867a-134">Advisor updates recommendations hourly.</span></span> <span data-ttu-id="d867a-135">Si vous ne prévoyez pas d’effectuer d’action immédiate sur une recommandation, vous pouvez la répéter pendant une période spécifique ou la faire disparaître.</span><span class="sxs-lookup"><span data-stu-id="d867a-135">If you don’t intend to take immediate action on a recommendation, you can snooze it for a specified time period or dismiss it.</span></span> 

## <a name="frequently-asked-questions"></a><span data-ttu-id="d867a-136">Forum Aux Questions</span><span class="sxs-lookup"><span data-stu-id="d867a-136">Frequently asked questions</span></span>

### <a name="how-do-i-access-advisor"></a><span data-ttu-id="d867a-137">Accès au conseiller</span><span class="sxs-lookup"><span data-stu-id="d867a-137">How do I access Advisor?</span></span>
<span data-ttu-id="d867a-138">Accéder à Advisor via le [portail Azure](https://aka.ms/azureadvisordashboard).</span><span class="sxs-lookup"><span data-stu-id="d867a-138">You can access Advisor through the [Azure portal](https://aka.ms/azureadvisordashboard).</span></span> <span data-ttu-id="d867a-139">Connectez-vous au [portail](https://portal.azure.com), sélectionnez **Parcourir**, puis faites défiler jusqu’à **Azure Advisor**.</span><span class="sxs-lookup"><span data-stu-id="d867a-139">Sign in to the [portal](https://portal.azure.com), select **Browse**, and then scroll to **Azure Advisor**.</span></span> <span data-ttu-id="d867a-140">Le tableau de bord du conseiller affiche des recommandations personnalisées pour un abonnement sélectionné.</span><span class="sxs-lookup"><span data-stu-id="d867a-140">The Advisor dashboard displays personalized recommendations for a selected subscription.</span></span> 

<span data-ttu-id="d867a-141">Vous pouvez également afficher les recommandations du conseiller via le panneau des ressources de la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="d867a-141">You can also view Advisor recommendations through the virtual machine resource blade.</span></span> <span data-ttu-id="d867a-142">Choisissez une machine virtuelle, puis accédez aux recommandations du conseiller dans le menu.</span><span class="sxs-lookup"><span data-stu-id="d867a-142">Choose a virtual machine, and then scroll to Advisor recommendations in the menu.</span></span> 

### <a name="what-permissions-do-i-need-to-access-advisor"></a><span data-ttu-id="d867a-143">Quelles autorisations dois-je avoir pour accéder au conseiller ?</span><span class="sxs-lookup"><span data-stu-id="d867a-143">What permissions do I need to access Advisor?</span></span>

<span data-ttu-id="d867a-144">Pour accéder aux recommandations d’Advisor, vous devez d’abord *inscrire votre abonnement*  auprès d’Advisor.</span><span class="sxs-lookup"><span data-stu-id="d867a-144">To access Advisor recommendations, you must first *register your subscription* with Advisor.</span></span> <span data-ttu-id="d867a-145">L’abonnement est inscrit lorsque son *propriétaire* lance le tableau de bord Advisor, puis clique sur le bouton **Obtenir des recommandations**.</span><span class="sxs-lookup"><span data-stu-id="d867a-145">A subscription is registered when a *subscription Owner* launches the Advisor dashboard and clicks the **Get recommendations** button.</span></span> <span data-ttu-id="d867a-146">Cette opération ne doit être *exécutée qu’une seule fois*.</span><span class="sxs-lookup"><span data-stu-id="d867a-146">This is a *one-time operation*.</span></span> <span data-ttu-id="d867a-147">Une fois l’abonnement inscrit, vous pouvez accéder aux recommandations d’Advisor en tant que *propriétaire*, *collaborateur* ou *lecteur* d’un abonnement, d’un groupe de ressources ou d’une ressource spécifique.</span><span class="sxs-lookup"><span data-stu-id="d867a-147">After the subscription is registered, you can access Advisor recommendations as *Owner*, *Contributor*, or *Reader* for a subscription, a resource group, or a specific resource.</span></span>

### <a name="how-often-are-advisor-recommendations-updated"></a><span data-ttu-id="d867a-148">A quelle fréquence les recommandations du conseiller sont-elles mises à jour ?</span><span class="sxs-lookup"><span data-stu-id="d867a-148">How often are Advisor recommendations updated?</span></span>

<span data-ttu-id="d867a-149">Les recommandations d’Advisor sont mises à jour toutes les heures.</span><span class="sxs-lookup"><span data-stu-id="d867a-149">Advisor recommendations are updated hourly.</span></span>

### <a name="what-resources-does-advisor-provide-recommendations-for"></a><span data-ttu-id="d867a-150">Pour quelles ressources le conseiller fournit-il des recommandations ?</span><span class="sxs-lookup"><span data-stu-id="d867a-150">What resources does Advisor provide recommendations for?</span></span>

<span data-ttu-id="d867a-151">Advisor fournit des recommandations pour les machines virtuelles, les groupes à haute disponibilité, les passerelles d’application, App Services, les serveurs SQL, les bases de données SQL et le Cache Redis.</span><span class="sxs-lookup"><span data-stu-id="d867a-151">Advisor provides recommendations for virtual machines, availability sets, application gateways, App Services, SQL servers, SQL databases, and Redis Cache.</span></span>

### <a name="can-i-snooze-or-dismiss-a-recommendation"></a><span data-ttu-id="d867a-152">Puis-je répéter ou ignorer une recommandation ?</span><span class="sxs-lookup"><span data-stu-id="d867a-152">Can I snooze or dismiss a recommendation?</span></span>

<span data-ttu-id="d867a-153">Pour répéter ou ignorer une recommandation, cliquez sur le bouton ou le lien **Répéter**.</span><span class="sxs-lookup"><span data-stu-id="d867a-153">To snooze or dismiss a recommendation, click the **Snooze** button or link.</span></span> <span data-ttu-id="d867a-154">Vous pouvez spécifier une période de répétition ou sélectionner **Jamais** pour faire disparaître la recommandation.</span><span class="sxs-lookup"><span data-stu-id="d867a-154">You can specify a snooze time period or select **Never** to dismiss the recommendation.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d867a-155">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="d867a-155">Next steps</span></span>

<span data-ttu-id="d867a-156">Pour en savoir plus sur les recommandations d’Advisor, consultez les ressources suivantes :</span><span class="sxs-lookup"><span data-stu-id="d867a-156">To learn more about Advisor recommendations, see:</span></span>

* [<span data-ttu-id="d867a-157">Prise en main du conseiller</span><span class="sxs-lookup"><span data-stu-id="d867a-157">Get started with Advisor</span></span>](advisor-get-started.md)
* [<span data-ttu-id="d867a-158">Recommandations du conseiller en matière de haute disponibilité</span><span class="sxs-lookup"><span data-stu-id="d867a-158">Advisor High Availability recommendations</span></span>](advisor-high-availability-recommendations.md)
* [<span data-ttu-id="d867a-159">Recommandations du conseiller en matière de sécurité</span><span class="sxs-lookup"><span data-stu-id="d867a-159">Advisor Security recommendations</span></span>](advisor-security-recommendations.md)
* [<span data-ttu-id="d867a-160">Recommandations du conseiller en matière de performances</span><span class="sxs-lookup"><span data-stu-id="d867a-160">Advisor Performance recommendations</span></span>](advisor-performance-recommendations.md)
* [<span data-ttu-id="d867a-161">Recommandations du conseiller en matière de coûts</span><span class="sxs-lookup"><span data-stu-id="d867a-161">Advisor Cost recommendations</span></span>](advisor-cost-recommendations.md)
