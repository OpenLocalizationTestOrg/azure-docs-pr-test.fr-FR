---
title: "Recommandations de coûts du conseiller Azure | Microsoft Docs"
description: "Le conseiller Azure permet d’optimiser le coût de vos déploiements Azure."
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
ms.openlocfilehash: 5eef2116f238b477fa8de46ce7b25728c393739c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="advisor-cost-recommendations"></a><span data-ttu-id="7dbcc-103">Recommandations en matière de coûts du conseiller</span><span class="sxs-lookup"><span data-stu-id="7dbcc-103">Advisor Cost recommendations</span></span>

<span data-ttu-id="7dbcc-104">Le conseiller vous aide à optimiser et à réduire votre dépense Azure globale en identifiant les ressources inactives et sous-utilisées.</span><span class="sxs-lookup"><span data-stu-id="7dbcc-104">Advisor helps you optimize and reduce your overall Azure spend by identifying idle and underutilized resources.</span></span> <span data-ttu-id="7dbcc-105">Vous pouvez obtenir des recommandations en matière de coûts dans l’onglet **Coût** du tableau de bord Advisor.</span><span class="sxs-lookup"><span data-stu-id="7dbcc-105">You can get cost recommendations from the **Cost** tab on the Advisor dashboard.</span></span>

![Onglet Coût dans Advisor](./media/advisor-cost-recommendations/advisor-cost-tab2.png)

## <a name="optimize-virtual-machine-spend-by-resizing-underutilized-instances"></a><span data-ttu-id="7dbcc-107">Optimiser le coût de la machine virtuelle en redimensionnant les instances sous-utilisées</span><span class="sxs-lookup"><span data-stu-id="7dbcc-107">Optimize virtual machine spend by resizing underutilized instances</span></span> 
<span data-ttu-id="7dbcc-108">Alors que certains scénarios d’application peuvent par définition entraîner une faible utilisation, vous pouvez souvent faire des économies grâce à la gestion de la taille de vos machines virtuelles et de leur nombre.</span><span class="sxs-lookup"><span data-stu-id="7dbcc-108">Although certain application scenarios can result in low utilization by design, you can often save money by managing the size and number of your virtual machines.</span></span> <span data-ttu-id="7dbcc-109">Advisor surveille l’utilisation de votre machine virtuelle pendant 14 jours et identifie les machines virtuelles faiblement utilisées.</span><span class="sxs-lookup"><span data-stu-id="7dbcc-109">Advisor monitors your virtual machine usage for 14 days and then identifies low-utilization virtual machines.</span></span> <span data-ttu-id="7dbcc-110">Les machines virtuelles dont l’utilisation du processeur est inférieure ou égale à 5 % et celle du réseau est inférieure ou égale à 7 Mo pendant quatre jours ou plus sont considérées comme des machines virtuelles faiblement utilisées.</span><span class="sxs-lookup"><span data-stu-id="7dbcc-110">Virtual machines whose CPU utilization is 5 percent or less and network usage is 7 MB or less for four or more days are considered low-utilization virtual machines.</span></span>

<span data-ttu-id="7dbcc-111">Advisor vous présente une estimation du coût de l’exécution de votre machine virtuelle, pour que vous puissiez choisir de l’arrêter ou de la redimensionner.</span><span class="sxs-lookup"><span data-stu-id="7dbcc-111">Advisor shows you the estimated cost of continuing to run your virtual machine, so that you can choose to shut it down or resize it.</span></span>  

![Recommandations de coûts du conseiller pour le redimensionnement des machines virtuelles](./media/advisor-cost-recommendations/advisor-cost-resizevms.png)

## <a name="use-a-cost-effective-solution-to-manage-performance-goals-of-multiple-sql-databases"></a><span data-ttu-id="7dbcc-113">Utiliser une solution économique pour gérer les objectifs de performances de plusieurs bases de données SQL</span><span class="sxs-lookup"><span data-stu-id="7dbcc-113">Use a cost effective solution to manage performance goals of multiple SQL databases</span></span>
<span data-ttu-id="7dbcc-114">Le conseiller identifie les instances de serveur SQL pouvant bénéficier de la création de pools de bases de données élastiques.</span><span class="sxs-lookup"><span data-stu-id="7dbcc-114">Advisor identifies SQL server instances that can benefit from creating elastic database pools.</span></span> <span data-ttu-id="7dbcc-115">Les pools de bases de données élastiques offrent une solution simple et économique pour gérer les objectifs de performances de plusieurs bases de données ayant des modèles d’utilisation variables.</span><span class="sxs-lookup"><span data-stu-id="7dbcc-115">Elastic database pools provide a simple, cost-effective solution to manage the performance goals of multiple databases that have varying usage patterns.</span></span> <span data-ttu-id="7dbcc-116">Pour plus d’informations sur les pools élastiques Azure, consultez la page [Qu’est-ce qu’un pool élastique Azure ?](https://azure.microsoft.com/en-us/documentation/articles/sql-database-elastic-pool/).</span><span class="sxs-lookup"><span data-stu-id="7dbcc-116">For more information about Azure elastic pools, see [What is an Azure Elastic pool?](https://azure.microsoft.com/en-us/documentation/articles/sql-database-elastic-pool/).</span></span>

![Recommandations de coût du conseiller pour les pools de bases de données élastiques](./media/advisor-cost-recommendations/advisor-cost-elasticdbpools.png)

## <a name="how-to-access-cost-recommendations-in-azure-advisor"></a><span data-ttu-id="7dbcc-118">Accès aux recommandations de coût dans le conseiller Azure</span><span class="sxs-lookup"><span data-stu-id="7dbcc-118">How to access cost recommendations in Azure Advisor</span></span>

1. <span data-ttu-id="7dbcc-119">Connectez-vous au [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="7dbcc-119">Sign in to the [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="7dbcc-120">Dans le volet gauche, cliquez sur **Autres services**.</span><span class="sxs-lookup"><span data-stu-id="7dbcc-120">In the left pane, click **More services**.</span></span>

3. <span data-ttu-id="7dbcc-121">Dans le volet du menu de services, sous **Surveillance et gestion**, cliquez sur **Azure Advisor**.</span><span class="sxs-lookup"><span data-stu-id="7dbcc-121">In the service menu pane, under **Monitoring and Management**, click **Azure Advisor**.</span></span>  
 <span data-ttu-id="7dbcc-122">Le tableau de bord Advisor s’affiche.</span><span class="sxs-lookup"><span data-stu-id="7dbcc-122">The Advisor dashboard is displayed.</span></span>

4. <span data-ttu-id="7dbcc-123">Dans le tableau de bord Advisor, cliquez sur l’onglet **Coût**.</span><span class="sxs-lookup"><span data-stu-id="7dbcc-123">On the Advisor dashboard, click the **Cost** tab.</span></span>

5. <span data-ttu-id="7dbcc-124">Sélectionnez l’abonnement pour lequel vous souhaitez recevoir des recommandations, puis cliquez sur **Obtenir des recommandations**.</span><span class="sxs-lookup"><span data-stu-id="7dbcc-124">Select the subscription for which you want to receive recommendations, and then click **Get recommendations**.</span></span>

> [!NOTE]
> <span data-ttu-id="7dbcc-125">Pour accéder aux recommandations d’Advisor, vous devez d’abord *inscrire votre abonnement*  auprès d’Advisor.</span><span class="sxs-lookup"><span data-stu-id="7dbcc-125">To access Advisor recommendations, you must first *register your subscription* with Advisor.</span></span> <span data-ttu-id="7dbcc-126">L’abonnement est inscrit lorsque son *propriétaire* lance le tableau de bord Advisor, puis clique sur le bouton **Obtenir des recommandations**.</span><span class="sxs-lookup"><span data-stu-id="7dbcc-126">A subscription is registered when a *subscription Owner* launches the Advisor dashboard and clicks the **Get recommendations** button.</span></span> <span data-ttu-id="7dbcc-127">Cette opération ne doit être *exécutée qu’une seule fois*.</span><span class="sxs-lookup"><span data-stu-id="7dbcc-127">This is a *one-time operation*.</span></span> <span data-ttu-id="7dbcc-128">Une fois l’abonnement inscrit, vous pouvez accéder aux recommandations d’Advisor en tant que *propriétaire*, *collaborateur* ou *lecteur* d’un abonnement, d’un groupe de ressources ou d’une ressource spécifique.</span><span class="sxs-lookup"><span data-stu-id="7dbcc-128">After the subscription is registered, you can access Advisor recommendations as *Owner*, *Contributor*, or *Reader* for a subscription, a resource group, or a specific resource.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7dbcc-129">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="7dbcc-129">Next steps</span></span>

<span data-ttu-id="7dbcc-130">Pour en savoir plus sur les recommandations d’Advisor, consultez les ressources suivantes :</span><span class="sxs-lookup"><span data-stu-id="7dbcc-130">To learn more about Advisor recommendations, see:</span></span>
* [<span data-ttu-id="7dbcc-131">Présentation d’Azure</span><span class="sxs-lookup"><span data-stu-id="7dbcc-131">Introduction to Advisor</span></span>](advisor-overview.md)
* [<span data-ttu-id="7dbcc-132">Prise en main</span><span class="sxs-lookup"><span data-stu-id="7dbcc-132">Get Started</span></span>](advisor-get-started.md)
* [<span data-ttu-id="7dbcc-133">Recommandations du conseiller en matière de performances</span><span class="sxs-lookup"><span data-stu-id="7dbcc-133">Advisor Performance recommendations</span></span>](advisor-cost-recommendations.md)
* [<span data-ttu-id="7dbcc-134">Recommandations du conseiller en matière de haute disponibilité</span><span class="sxs-lookup"><span data-stu-id="7dbcc-134">Advisor High Availability recommendations</span></span>](advisor-cost-recommendations.md)
* [<span data-ttu-id="7dbcc-135">Recommandations du conseiller en matière de sécurité</span><span class="sxs-lookup"><span data-stu-id="7dbcc-135">Advisor Security recommendations</span></span>](advisor-cost-recommendations.md)
