---
title: "recommandations de coût de l’Assistant aaaAzure | Documents Microsoft"
description: "Utilisez l’Assistant Azure toooptimize hello coût de vos déploiements Azure."
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
ms.openlocfilehash: 50f70c33a17f550c8753795435cdfddd51e409f7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="advisor-cost-recommendations"></a><span data-ttu-id="70ac6-103">Recommandations en matière de coûts du conseiller</span><span class="sxs-lookup"><span data-stu-id="70ac6-103">Advisor Cost recommendations</span></span>

<span data-ttu-id="70ac6-104">Le conseiller vous aide à optimiser et à réduire votre dépense Azure globale en identifiant les ressources inactives et sous-utilisées.</span><span class="sxs-lookup"><span data-stu-id="70ac6-104">Advisor helps you optimize and reduce your overall Azure spend by identifying idle and underutilized resources.</span></span> <span data-ttu-id="70ac6-105">Vous pouvez extraire les coûts recommandations de hello **coût** onglet tableau de bord de conseiller hello.</span><span class="sxs-lookup"><span data-stu-id="70ac6-105">You can get cost recommendations from hello **Cost** tab on hello Advisor dashboard.</span></span>

![Onglet Coût dans Advisor](./media/advisor-cost-recommendations/advisor-cost-tab2.png)

## <a name="optimize-virtual-machine-spend-by-resizing-underutilized-instances"></a><span data-ttu-id="70ac6-107">Optimiser le coût de la machine virtuelle en redimensionnant les instances sous-utilisées</span><span class="sxs-lookup"><span data-stu-id="70ac6-107">Optimize virtual machine spend by resizing underutilized instances</span></span> 
<span data-ttu-id="70ac6-108">Bien que certains scénarios d’application peuvent entraîner une utilisation faible par sa conception, vous pouvez souvent économies grâce à la gestion de la taille de hello et le nombre de vos ordinateurs virtuels.</span><span class="sxs-lookup"><span data-stu-id="70ac6-108">Although certain application scenarios can result in low utilization by design, you can often save money by managing hello size and number of your virtual machines.</span></span> <span data-ttu-id="70ac6-109">Advisor surveille l’utilisation de votre machine virtuelle pendant 14 jours et identifie les machines virtuelles faiblement utilisées.</span><span class="sxs-lookup"><span data-stu-id="70ac6-109">Advisor monitors your virtual machine usage for 14 days and then identifies low-utilization virtual machines.</span></span> <span data-ttu-id="70ac6-110">Les machines virtuelles dont l’utilisation du processeur est inférieure ou égale à 5 % et celle du réseau est inférieure ou égale à 7 Mo pendant quatre jours ou plus sont considérées comme des machines virtuelles faiblement utilisées.</span><span class="sxs-lookup"><span data-stu-id="70ac6-110">Virtual machines whose CPU utilization is 5 percent or less and network usage is 7 MB or less for four or more days are considered low-utilization virtual machines.</span></span>

<span data-ttu-id="70ac6-111">Affiche l’Assistant vous hello coût estimé de continuer toorun votre machine virtuelle, afin que vous puissiez choisir tooshut vers le bas ou le redimensionner.</span><span class="sxs-lookup"><span data-stu-id="70ac6-111">Advisor shows you hello estimated cost of continuing toorun your virtual machine, so that you can choose tooshut it down or resize it.</span></span>  

![Recommandations de coûts du conseiller pour le redimensionnement des machines virtuelles](./media/advisor-cost-recommendations/advisor-cost-resizevms.png)

## <a name="use-a-cost-effective-solution-toomanage-performance-goals-of-multiple-sql-databases"></a><span data-ttu-id="70ac6-113">Utiliser un objectifs de performances toomanage solution économique de plusieurs bases de données SQL</span><span class="sxs-lookup"><span data-stu-id="70ac6-113">Use a cost effective solution toomanage performance goals of multiple SQL databases</span></span>
<span data-ttu-id="70ac6-114">Le conseiller identifie les instances de serveur SQL pouvant bénéficier de la création de pools de bases de données élastiques.</span><span class="sxs-lookup"><span data-stu-id="70ac6-114">Advisor identifies SQL server instances that can benefit from creating elastic database pools.</span></span> <span data-ttu-id="70ac6-115">Pools de bases de données élastiques fournissent une solution simple et économique de toomanage des objectifs de performances hello de plusieurs bases de données qui ont des modèles d’utilisation.</span><span class="sxs-lookup"><span data-stu-id="70ac6-115">Elastic database pools provide a simple, cost-effective solution toomanage hello performance goals of multiple databases that have varying usage patterns.</span></span> <span data-ttu-id="70ac6-116">Pour plus d’informations sur les pools élastiques Azure, consultez la page [Qu’est-ce qu’un pool élastique Azure ?](https://azure.microsoft.com/en-us/documentation/articles/sql-database-elastic-pool/).</span><span class="sxs-lookup"><span data-stu-id="70ac6-116">For more information about Azure elastic pools, see [What is an Azure Elastic pool?](https://azure.microsoft.com/en-us/documentation/articles/sql-database-elastic-pool/).</span></span>

![Recommandations de coût du conseiller pour les pools de bases de données élastiques](./media/advisor-cost-recommendations/advisor-cost-elasticdbpools.png)

## <a name="how-tooaccess-cost-recommendations-in-azure-advisor"></a><span data-ttu-id="70ac6-118">Comment tooaccess coût recommandations dans l’Assistant d’Azure</span><span class="sxs-lookup"><span data-stu-id="70ac6-118">How tooaccess cost recommendations in Azure Advisor</span></span>

1. <span data-ttu-id="70ac6-119">Connectez-vous à toohello [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="70ac6-119">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="70ac6-120">Dans le volet gauche de hello, cliquez sur **davantage de services**.</span><span class="sxs-lookup"><span data-stu-id="70ac6-120">In hello left pane, click **More services**.</span></span>

3. <span data-ttu-id="70ac6-121">Bonjour service sous le volet de menu, **analyse et gestion**, cliquez sur **Azure Advisor**.</span><span class="sxs-lookup"><span data-stu-id="70ac6-121">In hello service menu pane, under **Monitoring and Management**, click **Azure Advisor**.</span></span>  
 <span data-ttu-id="70ac6-122">tableau de bord Hello Advisor s’affiche.</span><span class="sxs-lookup"><span data-stu-id="70ac6-122">hello Advisor dashboard is displayed.</span></span>

4. <span data-ttu-id="70ac6-123">Tableau de bord du conseiller hello, cliquez sur hello **coût** onglet.</span><span class="sxs-lookup"><span data-stu-id="70ac6-123">On hello Advisor dashboard, click hello **Cost** tab.</span></span>

5. <span data-ttu-id="70ac6-124">Sélectionnez l’abonnement hello pour lequel vous souhaitez que les recommandations tooreceive, puis cliquez sur **obtenir des recommandations**.</span><span class="sxs-lookup"><span data-stu-id="70ac6-124">Select hello subscription for which you want tooreceive recommendations, and then click **Get recommendations**.</span></span>

> [!NOTE]
> <span data-ttu-id="70ac6-125">tooaccess recommandations de l’Assistant, vous devez d’abord *enregistrer votre abonnement* avec l’Assistant.</span><span class="sxs-lookup"><span data-stu-id="70ac6-125">tooaccess Advisor recommendations, you must first *register your subscription* with Advisor.</span></span> <span data-ttu-id="70ac6-126">Un abonnement est enregistré quand un *abonnement propriétaire* lance hello hello de tableau de bord et clique sur Advisor **obtenir des recommandations** bouton.</span><span class="sxs-lookup"><span data-stu-id="70ac6-126">A subscription is registered when a *subscription Owner* launches hello Advisor dashboard and clicks hello **Get recommendations** button.</span></span> <span data-ttu-id="70ac6-127">Cette opération ne doit être *exécutée qu’une seule fois*.</span><span class="sxs-lookup"><span data-stu-id="70ac6-127">This is a *one-time operation*.</span></span> <span data-ttu-id="70ac6-128">Une fois l’abonnement de hello est enregistré, vous pouvez accéder à des recommandations de l’Assistant en tant que *propriétaire*, *collaborateur*, ou *lecteur* pour un abonnement, un groupe de ressources, ou un ressource spécifique.</span><span class="sxs-lookup"><span data-stu-id="70ac6-128">After hello subscription is registered, you can access Advisor recommendations as *Owner*, *Contributor*, or *Reader* for a subscription, a resource group, or a specific resource.</span></span>

## <a name="next-steps"></a><span data-ttu-id="70ac6-129">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="70ac6-129">Next steps</span></span>

<span data-ttu-id="70ac6-130">toolearn en savoir plus sur les recommandations de l’Assistant, consultez :</span><span class="sxs-lookup"><span data-stu-id="70ac6-130">toolearn more about Advisor recommendations, see:</span></span>
* [<span data-ttu-id="70ac6-131">Introduction tooAdvisor</span><span class="sxs-lookup"><span data-stu-id="70ac6-131">Introduction tooAdvisor</span></span>](advisor-overview.md)
* [<span data-ttu-id="70ac6-132">Prise en main</span><span class="sxs-lookup"><span data-stu-id="70ac6-132">Get Started</span></span>](advisor-get-started.md)
* [<span data-ttu-id="70ac6-133">Recommandations du conseiller en matière de performances</span><span class="sxs-lookup"><span data-stu-id="70ac6-133">Advisor Performance recommendations</span></span>](advisor-cost-recommendations.md)
* [<span data-ttu-id="70ac6-134">Recommandations du conseiller en matière de haute disponibilité</span><span class="sxs-lookup"><span data-stu-id="70ac6-134">Advisor High Availability recommendations</span></span>](advisor-cost-recommendations.md)
* [<span data-ttu-id="70ac6-135">Recommandations du conseiller en matière de sécurité</span><span class="sxs-lookup"><span data-stu-id="70ac6-135">Advisor Security recommendations</span></span>](advisor-cost-recommendations.md)
