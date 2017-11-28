---
title: "Prise en main du conseiller Azure | Microsoft Docs"
description: Prise en main du conseiller Azure.
services: advisor
documentationcenter: NA
author: manbeenkohli
manager: carmonm
editor: 
ms.assetid: 
ms.service: advisor
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 02/10/2017
ms.author: makohli
ms.openlocfilehash: a662841bebda460d4225e080f16705b3f16fdc46
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-azure-advisor"></a><span data-ttu-id="3f606-103">Prise en main d’Azure Advisor</span><span class="sxs-lookup"><span data-stu-id="3f606-103">Get started with Azure Advisor</span></span>

<span data-ttu-id="3f606-104">Découvrez comment accéder à Advisor à l’aide du portail Azure, et comment obtenir, implémenter, rechercher et actualiser des recommandations.</span><span class="sxs-lookup"><span data-stu-id="3f606-104">Learn how to access Advisor through the Azure portal, get recommendations, implement recommendations, search for recommendations, and refresh recommendations.</span></span>

## <a name="get-advisor-recommendations"></a><span data-ttu-id="3f606-105">Obtenir des recommandations du conseiller</span><span class="sxs-lookup"><span data-stu-id="3f606-105">Get Advisor recommendations</span></span>

1. <span data-ttu-id="3f606-106">Connectez-vous au [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="3f606-106">Sign in to the [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="3f606-107">Dans le volet gauche, cliquez sur **Autres services**.</span><span class="sxs-lookup"><span data-stu-id="3f606-107">In the left pane, click **More services**.</span></span>

3. <span data-ttu-id="3f606-108">Dans le volet du menu de services, sous **Surveillance et gestion**, cliquez sur **Azure Advisor**.</span><span class="sxs-lookup"><span data-stu-id="3f606-108">In the service menu pane, under **Monitoring and Management**, click **Azure Advisor**.</span></span>  
 <span data-ttu-id="3f606-109">Le tableau de bord Advisor s’affiche.</span><span class="sxs-lookup"><span data-stu-id="3f606-109">The Advisor dashboard is displayed.</span></span>

   ![Accéder au conseiller Azure avec le portail Azure](./media/advisor-overview/advisor-azure-portal-menu.png) 

4. <span data-ttu-id="3f606-111">Dans le tableau de bord d’Advisor, sélectionnez l’abonnement pour lequel vous souhaitez recevoir des recommandations.</span><span class="sxs-lookup"><span data-stu-id="3f606-111">On the Advisor dashboard, select the subscription for which you want to receive recommendations.</span></span>  
<span data-ttu-id="3f606-112">Le tableau de bord du conseiller affiche des recommandations personnalisées pour un abonnement sélectionné.</span><span class="sxs-lookup"><span data-stu-id="3f606-112">The Advisor dashboard displays personalized recommendations for a selected subscription.</span></span> 

5. <span data-ttu-id="3f606-113">Pour obtenir des recommandations pour une catégorie particulière, cliquez sur l’un des onglets **Haute disponibilité**, **Sécurité**, **Performances** ou **Coût**.</span><span class="sxs-lookup"><span data-stu-id="3f606-113">To get recommendations for a particular category, click one of the tabs: **High Availability**, **Security**, **Performance**, or **Cost**.</span></span>
 
> [!NOTE]
> <span data-ttu-id="3f606-114">Pour accéder aux recommandations d’Advisor, vous devez d’abord *inscrire votre abonnement*  auprès d’Advisor.</span><span class="sxs-lookup"><span data-stu-id="3f606-114">To access Advisor recommendations, you must first *register your subscription* with Advisor.</span></span> <span data-ttu-id="3f606-115">L’abonnement est inscrit lorsque son *propriétaire* lance le tableau de bord Advisor, puis clique sur le bouton **Obtenir des recommandations**.</span><span class="sxs-lookup"><span data-stu-id="3f606-115">A subscription is registered when a *subscription Owner* launches the Advisor dashboard and clicks the **Get recommendations** button.</span></span> <span data-ttu-id="3f606-116">Cette opération ne doit être *exécutée qu’une seule fois*.</span><span class="sxs-lookup"><span data-stu-id="3f606-116">This is a *one-time operation*.</span></span> <span data-ttu-id="3f606-117">Une fois l’abonnement inscrit, vous pouvez accéder aux recommandations d’Advisor en tant que *propriétaire*, *collaborateur* ou *lecteur* d’un abonnement, d’un groupe de ressources ou d’une ressource spécifique.</span><span class="sxs-lookup"><span data-stu-id="3f606-117">After the subscription is registered, you can access Advisor recommendations as *Owner*, *Contributor*, or *Reader* for a subscription, a resource group, or a specific resource.</span></span>

  ![Tableau de bord du conseiller Azure](./media/advisor-overview/advisor-all-tab.png)

## <a name="get-advisor-recommendation-details-and-implement-a-solution"></a><span data-ttu-id="3f606-119">Obtenir les détails de recommandation d’Advisor et implémenter une solution</span><span class="sxs-lookup"><span data-stu-id="3f606-119">Get Advisor recommendation details, and implement a solution</span></span>

<span data-ttu-id="3f606-120">Le panneau **Recommandation** d’Advisor offre des informations supplémentaires sur la recommandation.</span><span class="sxs-lookup"><span data-stu-id="3f606-120">The **Recommendation** blade in Advisor offers additional information about the recommendation.</span></span> 

1. <span data-ttu-id="3f606-121">Connectez-vous au [portail Azure](https://portal.azure.com), puis lancez [Azure Advisor](https://aka.ms/azureadvisordashboard).</span><span class="sxs-lookup"><span data-stu-id="3f606-121">Sign in to the [Azure portal](https://portal.azure.com), and then start [Azure Advisor](https://aka.ms/azureadvisordashboard).</span></span>

2. <span data-ttu-id="3f606-122">Dans le tableau de bord **Recommandations du conseiller**, cliquez sur **Obtenir des recommandations**.</span><span class="sxs-lookup"><span data-stu-id="3f606-122">On the **Advisor recommendations** dashboard, click **Get recommendations**.</span></span>

3. <span data-ttu-id="3f606-123">Dans la liste des recommandations, cliquez sur une recommandation que vous souhaitez examiner en détail.</span><span class="sxs-lookup"><span data-stu-id="3f606-123">In the list of recommendations, click a recommendation that you want to review in detail.</span></span>  
<span data-ttu-id="3f606-124">Le panneau **Recommandation** s’affiche.</span><span class="sxs-lookup"><span data-stu-id="3f606-124">The **Recommendation** blade is displayed.</span></span>

4. <span data-ttu-id="3f606-125">Dans le panneau **Recommandations**, passez en revue les informations sur les actions que vous pouvez effectuer pour résoudre un problème potentiel ou tirer parti d’une opportunité d’économies.</span><span class="sxs-lookup"><span data-stu-id="3f606-125">On the **Recommendations** blade, review information about actions that you can perform to resolve a potential issue, or take advantage of a cost-saving opportunity.</span></span> 
  
  ![Panneau des recommandations d’Advisor](./media/advisor-overview/advisor-recommendation-action-example.png)

## <a name="search-for-advisor-recommendations"></a><span data-ttu-id="3f606-127">Recherchez des recommandations du conseiller</span><span class="sxs-lookup"><span data-stu-id="3f606-127">Search for Advisor recommendations</span></span>

<span data-ttu-id="3f606-128">Vous pouvez rechercher des recommandations pour un abonnement ou un groupe de ressources spécifiques.</span><span class="sxs-lookup"><span data-stu-id="3f606-128">You can search for recommendations for a particular subscription or resource group.</span></span> <span data-ttu-id="3f606-129">Vous pouvez également rechercher des recommandations par état.</span><span class="sxs-lookup"><span data-stu-id="3f606-129">You can also search for recommendations by status.</span></span>

1. <span data-ttu-id="3f606-130">Connectez-vous au [portail Azure](https://portal.azure.com), puis lancez [Azure Advisor](https://aka.ms/azureadvisordashboard).</span><span class="sxs-lookup"><span data-stu-id="3f606-130">Sign in to the [Azure portal](https://portal.azure.com), and then start [Azure Advisor](https://aka.ms/azureadvisordashboard).</span></span>

2. <span data-ttu-id="3f606-131">Recherchez des recommandations en filtrant sur les abonnements, les groupes de ressources et les états de recommandation (**Active** ou **Répétée**).</span><span class="sxs-lookup"><span data-stu-id="3f606-131">Search for recommendations by filtering for subscriptions, resource groups, and recommendation status (**Active** or **Snoozed**).</span></span>

3. <span data-ttu-id="3f606-132">Cliquez sur **Obtenir des recommandations** pour obtenir une liste de recommandations d’Advisor en fonction de vos filtres de recherche.</span><span class="sxs-lookup"><span data-stu-id="3f606-132">To display a list of Advisor recommendations that are based on your search-filter criteria, click **Get recommendations**.</span></span>

  ![Critères de filtre de recherche d’Advisor](./media/advisor-get-started/advisor-search.png)

## <a name="snooze-or-dismiss-advisor-recommendations"></a><span data-ttu-id="3f606-134">Répéter ou ignorer les recommandations d’Advisor</span><span class="sxs-lookup"><span data-stu-id="3f606-134">Snooze or dismiss Advisor recommendations</span></span>

1. <span data-ttu-id="3f606-135">Connectez-vous au [portail Azure](https://portal.azure.com), puis lancez [Azure Advisor](https://aka.ms/azureadvisordashboard).</span><span class="sxs-lookup"><span data-stu-id="3f606-135">Sign in to the [Azure portal](https://portal.azure.com), and then start [Azure Advisor](https://aka.ms/azureadvisordashboard).</span></span>

2. <span data-ttu-id="3f606-136">Cliquez sur **Obtenir des recommandations**, puis dans la liste des recommandations, cliquez sur une recommandation.</span><span class="sxs-lookup"><span data-stu-id="3f606-136">Click **Get recommendations**, and then, in the list of recommendations, click a recommendation.</span></span>

3. <span data-ttu-id="3f606-137">Dans le panneau **Recommandations**, cliquez sur **Répéter**.</span><span class="sxs-lookup"><span data-stu-id="3f606-137">On the **Recommendation** blade, click **Snooze**.</span></span>  

   ![Exemple d’action recommandée du conseiller](./media/advisor-get-started/advisor-snooze.png)

4. <span data-ttu-id="3f606-139">Spécifiez une période de répétition ou sélectionnez **Jamais** pour faire disparaître la recommandation.</span><span class="sxs-lookup"><span data-stu-id="3f606-139">Specify a snooze time period, or select **Never** to dismiss the recommendation.</span></span>


## <a name="next-steps"></a><span data-ttu-id="3f606-140">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="3f606-140">Next steps</span></span>

<span data-ttu-id="3f606-141">Pour en savoir plus sur Advisor, consultez les ressources suivantes :</span><span class="sxs-lookup"><span data-stu-id="3f606-141">To learn more about Advisor, see:</span></span>
* [<span data-ttu-id="3f606-142">Présentation du conseiller Azure</span><span class="sxs-lookup"><span data-stu-id="3f606-142">Introduction to Azure Advisor</span></span>](advisor-overview.md)
* [<span data-ttu-id="3f606-143">Recommandations du conseiller en matière de haute disponibilité</span><span class="sxs-lookup"><span data-stu-id="3f606-143">Advisor High Availability recommendations</span></span>](advisor-high-availability-recommendations.md)
* [<span data-ttu-id="3f606-144">Recommandations du conseiller en matière de sécurité</span><span class="sxs-lookup"><span data-stu-id="3f606-144">Advisor Security recommendations</span></span>](advisor-security-recommendations.md)
-  [<span data-ttu-id="3f606-145">Recommandations du conseiller en matière de performances</span><span class="sxs-lookup"><span data-stu-id="3f606-145">Advisor Performance recommendations</span></span>](advisor-performance-recommendations.md)
* [<span data-ttu-id="3f606-146">Recommandations du conseiller en matière de coûts</span><span class="sxs-lookup"><span data-stu-id="3f606-146">Advisor Cost recommendations</span></span>](advisor-performance-recommendations.md)
