---
title: "aaaAzure recommandations de l’Assistant sécurité | Documents Microsoft"
description: "Utilisez l’Assistant Azure toohelp améliorer la sécurité de hello de vos déploiements Azure."
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
ms.openlocfilehash: e01ac29eb6e02bff0b1e846e320e7c36f85c7343
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="advisor-security-recommendations"></a><span data-ttu-id="ee4cd-103">Recommandations de sécurité du conseiller</span><span class="sxs-lookup"><span data-stu-id="ee4cd-103">Advisor Security recommendations</span></span>

<span data-ttu-id="ee4cd-104">Azure Advisor vous offre une vue cohérente et consolidée des recommandations pour toutes vos ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="ee4cd-104">Azure Advisor provides you with a consistent, consolidated view of recommendations for all your Azure resources.</span></span> <span data-ttu-id="ee4cd-105">Il s’intègre à Azure Security Center toobring vous recommandations de sécurité.</span><span class="sxs-lookup"><span data-stu-id="ee4cd-105">It integrates with Azure Security Center toobring you security recommendations.</span></span> <span data-ttu-id="ee4cd-106">Vous pouvez obtenir des recommandations de sécurité à partir de hello **sécurité** onglet tableau de bord de conseiller hello.</span><span class="sxs-lookup"><span data-stu-id="ee4cd-106">You can get security recommendations from hello **Security** tab on hello Advisor dashboard.</span></span>

![bouton de l’Assistant sécurité Hello](./media/advisor-security-recommendations/advisor-security-tab.png)

<span data-ttu-id="ee4cd-108">Centre de sécurité vous permet d’empêcher, détecter et répondre toothreats avec une meilleure visibilité et un contrôle accru de la sécurité hello de vos ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="ee4cd-108">Security Center helps you prevent, detect, and respond toothreats with increased visibility into and control over hello security of your Azure resources.</span></span> <span data-ttu-id="ee4cd-109">Il analyse régulièrement état de la sécurité de vos ressources Azure hello.</span><span class="sxs-lookup"><span data-stu-id="ee4cd-109">It periodically analyzes hello security state of your Azure resources.</span></span> <span data-ttu-id="ee4cd-110">Lorsqu’il identifie des failles de sécurité potentielles, il crée des recommandations.</span><span class="sxs-lookup"><span data-stu-id="ee4cd-110">When Security Center identifies potential security vulnerabilities, it creates recommendations.</span></span> <span data-ttu-id="ee4cd-111">recommandations de Hello vous guident tout au long des processus de hello de configuration de contrôles hello que vous avez besoin.</span><span class="sxs-lookup"><span data-stu-id="ee4cd-111">hello recommendations guide you through hello process of configuring hello controls you need.</span></span> 

![onglet de l’Assistant sécurité Hello](./media/advisor-security-recommendations/advisor-security-recommendations.png)

<span data-ttu-id="ee4cd-113">Pour plus d’informations sur les recommandations de sécurité, consultez [Gestion des recommandations de sécurité dans Azure Security Center](https://azure.microsoft.com/en-us/documentation/articles/security-center-recommendations/).</span><span class="sxs-lookup"><span data-stu-id="ee4cd-113">For more information about security recommendations, see [Managing security recommendations in Azure Security Center](https://azure.microsoft.com/en-us/documentation/articles/security-center-recommendations/).</span></span>

## <a name="how-tooaccess-security-recommendations-in-azure-advisor"></a><span data-ttu-id="ee4cd-114">Comment tooaccess les recommandations de sécurité dans l’Assistant d’Azure</span><span class="sxs-lookup"><span data-stu-id="ee4cd-114">How tooaccess Security recommendations in Azure Advisor</span></span>

1. <span data-ttu-id="ee4cd-115">Connectez-vous à toohello [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="ee4cd-115">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="ee4cd-116">Dans le volet gauche de hello, cliquez sur **davantage de services**.</span><span class="sxs-lookup"><span data-stu-id="ee4cd-116">In hello left pane, click **More services**.</span></span>

3. <span data-ttu-id="ee4cd-117">Bonjour service sous le volet de menu, **analyse et gestion**, cliquez sur **Azure Advisor**.</span><span class="sxs-lookup"><span data-stu-id="ee4cd-117">In hello service menu pane, under **Monitoring and Management**, click **Azure Advisor**.</span></span>  
 <span data-ttu-id="ee4cd-118">tableau de bord Hello Advisor s’affiche.</span><span class="sxs-lookup"><span data-stu-id="ee4cd-118">hello Advisor dashboard is displayed.</span></span>

4. <span data-ttu-id="ee4cd-119">Tableau de bord du conseiller hello, cliquez sur hello **sécurité** onglet.</span><span class="sxs-lookup"><span data-stu-id="ee4cd-119">On hello Advisor dashboard, click hello **Security** tab.</span></span>

5. <span data-ttu-id="ee4cd-120">Sélectionnez l’abonnement hello pour lequel vous souhaitez que les recommandations tooreceive, puis cliquez sur **obtenir des recommandations**.</span><span class="sxs-lookup"><span data-stu-id="ee4cd-120">Select hello subscription for which you want tooreceive recommendations, and then click **Get recommendations**.</span></span>

> [!NOTE]
> <span data-ttu-id="ee4cd-121">tooaccess recommandations de l’Assistant, vous devez d’abord *enregistrer votre abonnement* avec l’Assistant.</span><span class="sxs-lookup"><span data-stu-id="ee4cd-121">tooaccess Advisor recommendations, you must first *register your subscription* with Advisor.</span></span> <span data-ttu-id="ee4cd-122">Un abonnement est enregistré quand un *abonnement propriétaire* lance hello hello de tableau de bord et clique sur Advisor **obtenir des recommandations** bouton.</span><span class="sxs-lookup"><span data-stu-id="ee4cd-122">A subscription is registered when a *subscription Owner* launches hello Advisor dashboard and clicks hello **Get recommendations** button.</span></span> <span data-ttu-id="ee4cd-123">Cette opération ne doit être *exécutée qu’une seule fois*.</span><span class="sxs-lookup"><span data-stu-id="ee4cd-123">This is a *one-time operation*.</span></span> <span data-ttu-id="ee4cd-124">Une fois l’abonnement de hello est enregistré, vous pouvez accéder à des recommandations de l’Assistant en tant que *propriétaire*, *collaborateur*, ou *lecteur* pour un abonnement, un groupe de ressources, ou un ressource spécifique.</span><span class="sxs-lookup"><span data-stu-id="ee4cd-124">After hello subscription is registered, you can access Advisor recommendations as *Owner*, *Contributor*, or *Reader* for a subscription, a resource group, or a specific resource.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ee4cd-125">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="ee4cd-125">Next steps</span></span>

<span data-ttu-id="ee4cd-126">toolearn en savoir plus sur les recommandations de l’Assistant, consultez :</span><span class="sxs-lookup"><span data-stu-id="ee4cd-126">toolearn more about Advisor recommendations, see:</span></span>
* [<span data-ttu-id="ee4cd-127">Introduction tooAdvisor</span><span class="sxs-lookup"><span data-stu-id="ee4cd-127">Introduction tooAdvisor</span></span>](advisor-overview.md)
* [<span data-ttu-id="ee4cd-128">Prise en main du conseiller</span><span class="sxs-lookup"><span data-stu-id="ee4cd-128">Get started with Advisor</span></span>](advisor-get-started.md)
* [<span data-ttu-id="ee4cd-129">Recommandations du conseiller en matière de coûts</span><span class="sxs-lookup"><span data-stu-id="ee4cd-129">Advisor Cost recommendations</span></span>](advisor-performance-recommendations.md)
* [<span data-ttu-id="ee4cd-130">Recommandations du conseiller en matière de performances</span><span class="sxs-lookup"><span data-stu-id="ee4cd-130">Advisor Performance recommendations</span></span>](advisor-performance-recommendations.md)
* [<span data-ttu-id="ee4cd-131">Recommandations du conseiller en matière de haute disponibilité</span><span class="sxs-lookup"><span data-stu-id="ee4cd-131">Advisor High Availability recommendations</span></span>](advisor-high-availability-recommendations.md)


 
