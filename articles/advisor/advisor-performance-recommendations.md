---
title: "Recommandations Azure Advisor en matière de performances | Microsoft Docs"
description: "Utilisez Advisor pour optimiser les performances de vos déploiements Azure."
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
ms.openlocfilehash: 5fb86c60b2d1f258dde5636ff8854b6f30f7f1c8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="advisor-performance-recommendations"></a><span data-ttu-id="bd86d-103">Recommandations Azure Advisor en matière de performances</span><span class="sxs-lookup"><span data-stu-id="bd86d-103">Advisor Performance recommendations</span></span>

<span data-ttu-id="bd86d-104">Les recommandations d’Azure Advisor en matière de performances vous aident à optimiser la vitesse et la réactivité de vos applications stratégiques.</span><span class="sxs-lookup"><span data-stu-id="bd86d-104">Azure Advisor performance recommendations help improve the speed and responsiveness of your business-critical applications.</span></span> <span data-ttu-id="bd86d-105">Vous pouvez obtenir des recommandations en matière de performances à l’aide d’Advisor dans l’onglet **Performances** du tableau de bord d’Advisor.</span><span class="sxs-lookup"><span data-stu-id="bd86d-105">You can get performance recommendations from Advisor on the **Performance** tab of the Advisor dashboard.</span></span>

![Onglet Performances du conseiller](./media/advisor-performance-recommendations/advisor-performance-tab.png)

## <a name="improve-database-performance-with-sql-db-advisor"></a><span data-ttu-id="bd86d-107">Améliorer les performances de base de données avec SQL DB Advisor</span><span class="sxs-lookup"><span data-stu-id="bd86d-107">Improve database performance with SQL DB Advisor</span></span>

<span data-ttu-id="bd86d-108">Le conseiller vous offre une vue cohérente et consolidée des recommandations pour toutes vos ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="bd86d-108">Advisor provides you with a consistent, consolidated view of recommendations for all your Azure resources.</span></span> <span data-ttu-id="bd86d-109">Il s’intègre à SQL Database Advisor pour vous proposer des recommandations en vue d’améliorer les performances de votre base de données SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="bd86d-109">It integrates with SQL Database Advisor to bring you recommendations for improving the performance of your SQL Azure database.</span></span> <span data-ttu-id="bd86d-110">SQL Database Advisor évalue les performances de vos bases de données SQL Azure en analysant votre historique d’utilisation.</span><span class="sxs-lookup"><span data-stu-id="bd86d-110">SQL Database Advisor assesses the performance of your SQL Azure databases by analyzing your usage history.</span></span> <span data-ttu-id="bd86d-111">Il propose alors les recommandations les plus adaptées pour exécuter la charge de travail standard de la base de données.</span><span class="sxs-lookup"><span data-stu-id="bd86d-111">It then offers recommendations that are best suited for running the database’s typical workload.</span></span> 

> [!NOTE]
> <span data-ttu-id="bd86d-112">Pour obtenir des recommandations, une base de données doit avoir été utilisée pendant environ une semaine et avoir fait l’objet d’une activité cohérente au cours de cette semaine.</span><span class="sxs-lookup"><span data-stu-id="bd86d-112">To get recommendations, a database must have about a week of usage, and within that week there must be some consistent activity.</span></span> <span data-ttu-id="bd86d-113">SQL Database Advisor peut plus facilement optimiser les modèles de requête cohérents que les pics d’activité aléatoires.</span><span class="sxs-lookup"><span data-stu-id="bd86d-113">SQL Database Advisor can optimize more easily for consistent query patterns than for random bursts of activity.</span></span>

<span data-ttu-id="bd86d-114">Pour plus d’informations sur SQL Database Advisor, consultez la page [SQL Database Advisor](https://azure.microsoft.com/en-us/documentation/articles/sql-database-advisor/).</span><span class="sxs-lookup"><span data-stu-id="bd86d-114">For more information about SQL Database Advisor, see [SQL Database Advisor](https://azure.microsoft.com/en-us/documentation/articles/sql-database-advisor/).</span></span>

![Recommandations SQL Database](./media/advisor-performance-recommendations/advisor-performance-sql.png)

## <a name="improve-redis-cache-performance-and-reliability"></a><span data-ttu-id="bd86d-116">Améliorer la fiabilité et les performances du Cache Redis</span><span class="sxs-lookup"><span data-stu-id="bd86d-116">Improve Redis Cache performance and reliability</span></span>

<span data-ttu-id="bd86d-117">Advisor identifie les instances de Cache Redis où les performances peuvent être défavorablement affectées par une utilisation intensive de la mémoire, la charge du serveur, la bande passante réseau ou un grand nombre de connexions clientes.</span><span class="sxs-lookup"><span data-stu-id="bd86d-117">Advisor identifies Redis Cache instances where performance may be adversely affected by high memory usage, server load, network bandwidth, or a large number of client connections.</span></span> <span data-ttu-id="bd86d-118">Il fournit également des recommandations quant aux meilleures pratiques pour vous éviter les problèmes potentiels.</span><span class="sxs-lookup"><span data-stu-id="bd86d-118">Advisor also provides best practices recommendations to help you avoid potential issues.</span></span> <span data-ttu-id="bd86d-119">Pour plus d’informations concernant les recommandations de Cache Redis, consultez [Redis Cache Advisor](https://azure.microsoft.com/en-us/documentation/articles/cache-configure/#redis-cache-advisor).</span><span class="sxs-lookup"><span data-stu-id="bd86d-119">For more information about Redis Cache recommendations, see [Redis Cache Advisor](https://azure.microsoft.com/en-us/documentation/articles/cache-configure/#redis-cache-advisor).</span></span>


## <a name="improve-app-service-performance-and-reliability"></a><span data-ttu-id="bd86d-120">Améliorer la fiabilité et les performances d’App Service</span><span class="sxs-lookup"><span data-stu-id="bd86d-120">Improve App Service performance and reliability</span></span>

<span data-ttu-id="bd86d-121">Le conseiller Azure intègre des recommandations quant aux meilleures pratiques pour améliorer votre expérience App Services et vous faire découvrir des fonctionnalités appropriées de la plateforme.</span><span class="sxs-lookup"><span data-stu-id="bd86d-121">Azure Advisor integrates best practices recommendations for improving your App Services experience and discovering relevant platform capabilities.</span></span> <span data-ttu-id="bd86d-122">Exemples de recommandations App Services :</span><span class="sxs-lookup"><span data-stu-id="bd86d-122">Examples of App Services recommendations are:</span></span>
* <span data-ttu-id="bd86d-123">Détection des instances où les ressources de mémoire ou de processeur sont épuisées par des exécutions d’application avec options d’atténuation.</span><span class="sxs-lookup"><span data-stu-id="bd86d-123">Detection of instances where memory or CPU resources are exhausted by app runtimes with mitigation options.</span></span>
* <span data-ttu-id="bd86d-124">Détection des instances où la colocalisation de ressources telles que les applications web et les bases de données peut améliorer les performances et réduire les coûts.</span><span class="sxs-lookup"><span data-stu-id="bd86d-124">Detection of instances where collocating resources like web apps and databases can improve performance and lower cost.</span></span> 

<span data-ttu-id="bd86d-125">Pour plus d’informations sur les recommandations App Services, consultez [Meilleures pratiques pour Azure App Service](https://azure.microsoft.com/en-us/documentation/articles/app-service-best-practices/).</span><span class="sxs-lookup"><span data-stu-id="bd86d-125">For more information about App Services recommendations, see [Best Practices for Azure App Service](https://azure.microsoft.com/en-us/documentation/articles/app-service-best-practices/).</span></span>
<span data-ttu-id="bd86d-126">![Recommandations App Services](./media/advisor-performance-recommendations/advisor-performance-app-service.png)</span><span class="sxs-lookup"><span data-stu-id="bd86d-126">![App Services recommendations](./media/advisor-performance-recommendations/advisor-performance-app-service.png)</span></span>

## <a name="how-to-access-performance-recommendations-in-advisor"></a><span data-ttu-id="bd86d-127">Comment accéder aux recommandations en matière de performances dans le conseiller</span><span class="sxs-lookup"><span data-stu-id="bd86d-127">How to access Performance recommendations in Advisor</span></span>

1. <span data-ttu-id="bd86d-128">Connectez-vous au [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="bd86d-128">Sign in to the [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="bd86d-129">Dans le volet gauche, cliquez sur **Autres services**.</span><span class="sxs-lookup"><span data-stu-id="bd86d-129">In the left pane, click **More services**.</span></span>

3. <span data-ttu-id="bd86d-130">Dans le volet du menu de services, sous **Surveillance et gestion**, cliquez sur **Azure Advisor**.</span><span class="sxs-lookup"><span data-stu-id="bd86d-130">In the service menu pane, under **Monitoring and Management**, click **Azure Advisor**.</span></span>  
 <span data-ttu-id="bd86d-131">Le tableau de bord Advisor s’affiche.</span><span class="sxs-lookup"><span data-stu-id="bd86d-131">The Advisor dashboard is displayed.</span></span>

4. <span data-ttu-id="bd86d-132">Dans le tableau de bord Advisor, cliquez sur l’onglet **Performances**.</span><span class="sxs-lookup"><span data-stu-id="bd86d-132">On the Advisor dashboard, click the **Performance** tab.</span></span>

5. <span data-ttu-id="bd86d-133">Sélectionnez l’abonnement pour lequel vous souhaitez recevoir des recommandations, puis cliquez sur **Obtenir des recommandations**.</span><span class="sxs-lookup"><span data-stu-id="bd86d-133">Select the subscription for which you want to receive recommendations, and then click **Get recommendations**.</span></span>

> [!NOTE]
> <span data-ttu-id="bd86d-134">Pour accéder aux recommandations d’Advisor, vous devez d’abord *inscrire votre abonnement*  auprès d’Advisor.</span><span class="sxs-lookup"><span data-stu-id="bd86d-134">To access Advisor recommendations, you must first *register your subscription* with Advisor.</span></span> <span data-ttu-id="bd86d-135">L’abonnement est inscrit lorsque son *propriétaire* lance le tableau de bord Advisor, puis clique sur le bouton **Obtenir des recommandations**.</span><span class="sxs-lookup"><span data-stu-id="bd86d-135">A subscription is registered when a *subscription Owner* launches the Advisor dashboard and clicks the **Get recommendations** button.</span></span> <span data-ttu-id="bd86d-136">Cette opération ne doit être *exécutée qu’une seule fois*.</span><span class="sxs-lookup"><span data-stu-id="bd86d-136">This is a *one-time operation*.</span></span> <span data-ttu-id="bd86d-137">Une fois l’abonnement inscrit, vous pouvez accéder aux recommandations d’Advisor en tant que *propriétaire*, *collaborateur* ou *lecteur* d’un abonnement, d’un groupe de ressources ou d’une ressource spécifique.</span><span class="sxs-lookup"><span data-stu-id="bd86d-137">After the subscription is registered, you can access Advisor recommendations as *Owner*, *Contributor*, or *Reader* for a subscription, a resource group, or a specific resource.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bd86d-138">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="bd86d-138">Next steps</span></span>

<span data-ttu-id="bd86d-139">Pour en savoir plus sur les recommandations d’Advisor, consultez les ressources suivantes :</span><span class="sxs-lookup"><span data-stu-id="bd86d-139">To learn more about Advisor recommendations, see:</span></span>

* [<span data-ttu-id="bd86d-140">Présentation d’Azure</span><span class="sxs-lookup"><span data-stu-id="bd86d-140">Introduction to Advisor</span></span>](advisor-overview.md)
* [<span data-ttu-id="bd86d-141">Prise en main du conseiller</span><span class="sxs-lookup"><span data-stu-id="bd86d-141">Get started with Advisor</span></span>](advisor-get-started.md)
* [<span data-ttu-id="bd86d-142">Recommandations du conseiller en matière de coûts</span><span class="sxs-lookup"><span data-stu-id="bd86d-142">Advisor Cost recommendations</span></span>](advisor-performance-recommendations.md)
* [<span data-ttu-id="bd86d-143">Recommandations du conseiller en matière de haute disponibilité</span><span class="sxs-lookup"><span data-stu-id="bd86d-143">Advisor High Availability recommendations</span></span>](advisor-high-availability-recommendations.md)
* [<span data-ttu-id="bd86d-144">Recommandations du conseiller en matière de sécurité</span><span class="sxs-lookup"><span data-stu-id="bd86d-144">Advisor Security recommendations</span></span>](advisor-security-recommendations.md)

