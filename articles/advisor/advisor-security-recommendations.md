---
title: "Recommandations de sécurité du conseiller Azure | Microsoft Docs"
description: "Utilisez le conseiller Azure pour améliorer la sécurité de vos déploiements Azure."
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
ms.openlocfilehash: 53be05593c3733ccb27979a3a026414013125779
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="advisor-security-recommendations"></a><span data-ttu-id="bbe66-103">Recommandations de sécurité du conseiller</span><span class="sxs-lookup"><span data-stu-id="bbe66-103">Advisor Security recommendations</span></span>

<span data-ttu-id="bbe66-104">Azure Advisor vous offre une vue cohérente et consolidée des recommandations pour toutes vos ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="bbe66-104">Azure Advisor provides you with a consistent, consolidated view of recommendations for all your Azure resources.</span></span> <span data-ttu-id="bbe66-105">Il s’intègre avec Azure Security Center pour vous proposer des recommandations de sécurité.</span><span class="sxs-lookup"><span data-stu-id="bbe66-105">It integrates with Azure Security Center to bring you security recommendations.</span></span> <span data-ttu-id="bbe66-106">Vous pouvez obtenir des recommandations en matière de sécurité à partir de l’onglet **Sécurité** du tableau de bord Advisor.</span><span class="sxs-lookup"><span data-stu-id="bbe66-106">You can get security recommendations from the **Security** tab on the Advisor dashboard.</span></span>

![Bouton Sécurité Advisor](./media/advisor-security-recommendations/advisor-security-tab.png)

<span data-ttu-id="bbe66-108">Le Centre de sécurité vous aide à prévenir, détecter et résoudre les menaces grâce à une visibilité et un contrôle accrus de la sécurité de vos ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="bbe66-108">Security Center helps you prevent, detect, and respond to threats with increased visibility into and control over the security of your Azure resources.</span></span> <span data-ttu-id="bbe66-109">Il analyse l’état de sécurité de vos ressources Azure à intervalles réguliers.</span><span class="sxs-lookup"><span data-stu-id="bbe66-109">It periodically analyzes the security state of your Azure resources.</span></span> <span data-ttu-id="bbe66-110">Lorsqu’il identifie des failles de sécurité potentielles, il crée des recommandations.</span><span class="sxs-lookup"><span data-stu-id="bbe66-110">When Security Center identifies potential security vulnerabilities, it creates recommendations.</span></span> <span data-ttu-id="bbe66-111">Ces recommandations vous guident tout au long du processus de configuration des contrôles nécessaires.</span><span class="sxs-lookup"><span data-stu-id="bbe66-111">The recommendations guide you through the process of configuring the controls you need.</span></span> 

![Onglet Sécurité Advisor](./media/advisor-security-recommendations/advisor-security-recommendations.png)

<span data-ttu-id="bbe66-113">Pour plus d’informations sur les recommandations de sécurité, consultez [Gestion des recommandations de sécurité dans Azure Security Center](https://azure.microsoft.com/en-us/documentation/articles/security-center-recommendations/).</span><span class="sxs-lookup"><span data-stu-id="bbe66-113">For more information about security recommendations, see [Managing security recommendations in Azure Security Center](https://azure.microsoft.com/en-us/documentation/articles/security-center-recommendations/).</span></span>

## <a name="how-to-access-security-recommendations-in-azure-advisor"></a><span data-ttu-id="bbe66-114">Accès aux recommandations de sécurité dans Azure Advisor</span><span class="sxs-lookup"><span data-stu-id="bbe66-114">How to access Security recommendations in Azure Advisor</span></span>

1. <span data-ttu-id="bbe66-115">Connectez-vous au [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="bbe66-115">Sign in to the [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="bbe66-116">Dans le volet gauche, cliquez sur **Autres services**.</span><span class="sxs-lookup"><span data-stu-id="bbe66-116">In the left pane, click **More services**.</span></span>

3. <span data-ttu-id="bbe66-117">Dans le volet du menu de services, sous **Surveillance et gestion**, cliquez sur **Azure Advisor**.</span><span class="sxs-lookup"><span data-stu-id="bbe66-117">In the service menu pane, under **Monitoring and Management**, click **Azure Advisor**.</span></span>  
 <span data-ttu-id="bbe66-118">Le tableau de bord Advisor s’affiche.</span><span class="sxs-lookup"><span data-stu-id="bbe66-118">The Advisor dashboard is displayed.</span></span>

4. <span data-ttu-id="bbe66-119">Dans le tableau de bord Advisor, cliquez sur l’onglet **Sécurité**.</span><span class="sxs-lookup"><span data-stu-id="bbe66-119">On the Advisor dashboard, click the **Security** tab.</span></span>

5. <span data-ttu-id="bbe66-120">Sélectionnez l’abonnement pour lequel vous souhaitez recevoir des recommandations, puis cliquez sur **Obtenir des recommandations**.</span><span class="sxs-lookup"><span data-stu-id="bbe66-120">Select the subscription for which you want to receive recommendations, and then click **Get recommendations**.</span></span>

> [!NOTE]
> <span data-ttu-id="bbe66-121">Pour accéder aux recommandations d’Advisor, vous devez d’abord *inscrire votre abonnement*  auprès d’Advisor.</span><span class="sxs-lookup"><span data-stu-id="bbe66-121">To access Advisor recommendations, you must first *register your subscription* with Advisor.</span></span> <span data-ttu-id="bbe66-122">L’abonnement est inscrit lorsque son *propriétaire* lance le tableau de bord Advisor, puis clique sur le bouton **Obtenir des recommandations**.</span><span class="sxs-lookup"><span data-stu-id="bbe66-122">A subscription is registered when a *subscription Owner* launches the Advisor dashboard and clicks the **Get recommendations** button.</span></span> <span data-ttu-id="bbe66-123">Cette opération ne doit être *exécutée qu’une seule fois*.</span><span class="sxs-lookup"><span data-stu-id="bbe66-123">This is a *one-time operation*.</span></span> <span data-ttu-id="bbe66-124">Une fois l’abonnement inscrit, vous pouvez accéder aux recommandations d’Advisor en tant que *propriétaire*, *collaborateur* ou *lecteur* d’un abonnement, d’un groupe de ressources ou d’une ressource spécifique.</span><span class="sxs-lookup"><span data-stu-id="bbe66-124">After the subscription is registered, you can access Advisor recommendations as *Owner*, *Contributor*, or *Reader* for a subscription, a resource group, or a specific resource.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bbe66-125">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="bbe66-125">Next steps</span></span>

<span data-ttu-id="bbe66-126">Pour en savoir plus sur les recommandations d’Advisor, consultez les ressources suivantes :</span><span class="sxs-lookup"><span data-stu-id="bbe66-126">To learn more about Advisor recommendations, see:</span></span>
* [<span data-ttu-id="bbe66-127">Présentation d’Azure</span><span class="sxs-lookup"><span data-stu-id="bbe66-127">Introduction to Advisor</span></span>](advisor-overview.md)
* [<span data-ttu-id="bbe66-128">Prise en main du conseiller</span><span class="sxs-lookup"><span data-stu-id="bbe66-128">Get started with Advisor</span></span>](advisor-get-started.md)
* [<span data-ttu-id="bbe66-129">Recommandations du conseiller en matière de coûts</span><span class="sxs-lookup"><span data-stu-id="bbe66-129">Advisor Cost recommendations</span></span>](advisor-performance-recommendations.md)
* [<span data-ttu-id="bbe66-130">Recommandations du conseiller en matière de performances</span><span class="sxs-lookup"><span data-stu-id="bbe66-130">Advisor Performance recommendations</span></span>](advisor-performance-recommendations.md)
* [<span data-ttu-id="bbe66-131">Recommandations du conseiller en matière de haute disponibilité</span><span class="sxs-lookup"><span data-stu-id="bbe66-131">Advisor High Availability recommendations</span></span>](advisor-high-availability-recommendations.md)


 
