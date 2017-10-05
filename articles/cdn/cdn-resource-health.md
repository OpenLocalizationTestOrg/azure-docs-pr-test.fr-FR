---
title: "Surveiller l’intégrité des ressources CDN Azure | Microsoft Docs"
description: "Découvrez comment surveiller l’intégrité de vos ressources CDN Azure à l’aide d’Azure Resource Health."
services: cdn
documentationcenter: .net
author: zhangmanling
manager: zhangmanling
editor: 
ms.assetid: bf23bd89-35b2-4aca-ac7f-68ee02953f31
ms.service: cdn
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: 37fe208f5087f318e665e76825127854b4a11c98
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="monitor-the-health-of-azure-cdn-resources"></a><span data-ttu-id="4fb02-103">Surveiller l’intégrité des ressources CDN Azure</span><span class="sxs-lookup"><span data-stu-id="4fb02-103">Monitor the health of Azure CDN resources</span></span>
  
<span data-ttu-id="4fb02-104">Azure CDN Resource Health est un sous-ensemble [d’Azure Resource Health](../resource-health/resource-health-overview.md).</span><span class="sxs-lookup"><span data-stu-id="4fb02-104">Azure CDN Resource health is a subset of [Azure resource health](../resource-health/resource-health-overview.md).</span></span>  <span data-ttu-id="4fb02-105">Vous pouvez utiliser Azure Resource Health pour surveiller l’intégrité des ressources CDN et recevoir des conseils pour résoudre les problèmes.</span><span class="sxs-lookup"><span data-stu-id="4fb02-105">You can use Azure resource health to monitor the health of CDN resources and receive actionable guidance to troubleshoot problems.</span></span>

>[!IMPORTANT] 
><span data-ttu-id="4fb02-106">Pour le moment, Azure CDN Resource Health gère uniquement l’intégrité de la remise CDN générale et des fonctionnalités des API.</span><span class="sxs-lookup"><span data-stu-id="4fb02-106">Azure CDN resource health only currently accounts for the health of global CDN delivery and API capabilities.</span></span>  <span data-ttu-id="4fb02-107">Azure CDN Resource Health ne vérifie pas les points de terminaison CDN individuels.</span><span class="sxs-lookup"><span data-stu-id="4fb02-107">Azure CDN resource health does not verify individual CDN endpoints.</span></span>
>
><span data-ttu-id="4fb02-108">Les signaux qui alimentent Azure CDN Resource Health peuvent être retardés de 15 minutes au plus.</span><span class="sxs-lookup"><span data-stu-id="4fb02-108">The signals that feed Azure CDN resource health may be up to 15 minutes delayed.</span></span>

## <a name="how-to-find-azure-cdn-resource-health"></a><span data-ttu-id="4fb02-109">Comment trouver Azure CDN Resource Health</span><span class="sxs-lookup"><span data-stu-id="4fb02-109">How to find Azure CDN resource health</span></span>

1. <span data-ttu-id="4fb02-110">Dans le [portail Azure](https://portal.azure.com), accédez à votre profil CDN.</span><span class="sxs-lookup"><span data-stu-id="4fb02-110">In the [Azure portal](https://portal.azure.com), browse to your CDN profile.</span></span>

2. <span data-ttu-id="4fb02-111">Cliquez sur le bouton **Settings** .</span><span class="sxs-lookup"><span data-stu-id="4fb02-111">Click the **Settings** button.</span></span>

    ![Bouton Paramètres](./media/cdn-resource-health/cdn-profile-settings.png)

3. <span data-ttu-id="4fb02-113">Sous *Support + dépannage*, cliquez sur **Intégrité des ressources**.</span><span class="sxs-lookup"><span data-stu-id="4fb02-113">Under *Support + troubleshooting*, click **Resource health**.</span></span>

    ![Intégrité des ressources CDN](./media/cdn-resource-health/cdn-resource-health3.png)

>[!TIP] 
><span data-ttu-id="4fb02-115">Vous pouvez également rechercher les ressources CDN répertoriées dans la vignette *Intégrité des ressources* du panneau *Aide + support*.</span><span class="sxs-lookup"><span data-stu-id="4fb02-115">You can also find CDN resources listed in the *Resource health* tile in the *Help + support* blade.</span></span>  <span data-ttu-id="4fb02-116">Pour accéder rapidement à *Aide + support*, cliquez sur le point d’interrogation **?** entouré d’un cercle</span><span class="sxs-lookup"><span data-stu-id="4fb02-116">You can quickly get to *Help + support* by clicking the circled **?**</span></span> <span data-ttu-id="4fb02-117">dans l’angle supérieur droit du portail.</span><span class="sxs-lookup"><span data-stu-id="4fb02-117">in the upper right corner of the portal.</span></span>
>
> ![Aide + Support](./media/cdn-resource-health/cdn-help-support.png)

## <a name="azure-cdn-specific-messages"></a><span data-ttu-id="4fb02-119">Messages propres à CDN Azure</span><span class="sxs-lookup"><span data-stu-id="4fb02-119">Azure CDN-specific messages</span></span>

<span data-ttu-id="4fb02-120">États liés à CDN Azure Resource Health :</span><span class="sxs-lookup"><span data-stu-id="4fb02-120">Statuses related to Azure CDN resource health can be found below.</span></span>

|<span data-ttu-id="4fb02-121">Message</span><span class="sxs-lookup"><span data-stu-id="4fb02-121">Message</span></span> | <span data-ttu-id="4fb02-122">Action recommandée</span><span class="sxs-lookup"><span data-stu-id="4fb02-122">Recommended Action</span></span> |
|---|---|
|<span data-ttu-id="4fb02-123">Vous avez peut-être arrêté, supprimé ou incorrectement configuré un ou plusieurs points de terminaison CDN</span><span class="sxs-lookup"><span data-stu-id="4fb02-123">You may have stopped, removed, or misconfigured one or more of your CDN endpoints</span></span> | <span data-ttu-id="4fb02-124">Vous avez peut-être arrêté, supprimé ou incorrectement configuré un ou plusieurs points de terminaison CDN.</span><span class="sxs-lookup"><span data-stu-id="4fb02-124">You may have stopped, removed, or misconfigured one or more of your CDN endpoints.</span></span>|
|<span data-ttu-id="4fb02-125">Nous sommes désolés, le service de gestion CDN n’est pas disponible pour le moment</span><span class="sxs-lookup"><span data-stu-id="4fb02-125">We are sorry, the CDN management service is currently unavailable</span></span> | <span data-ttu-id="4fb02-126">Revenez ici pour vérifier si la situation a évolué. Si votre problème persiste passé le délai prévu de résolution, contactez le support.</span><span class="sxs-lookup"><span data-stu-id="4fb02-126">Check back here for status updates; If your problem persists after the expected resolution time, contact support.</span></span>|
|<span data-ttu-id="4fb02-127">Désolé. Vos points de terminaison CDN peuvent être affectés par des problèmes courants liés à certains de nos fournisseurs CDN</span><span class="sxs-lookup"><span data-stu-id="4fb02-127">We're sorry, your CDN endpoints may be impacted by ongoing issues with some of our CDN providers</span></span> | <span data-ttu-id="4fb02-128">Revenez ici pour vérifier si la situation a évolué. Utilisez l’outil de dépannage pour découvrir comment tester votre point de terminaison d’origine et CDN. Si votre problème persiste passé le délai prévu de résolution, contactez le support.</span><span class="sxs-lookup"><span data-stu-id="4fb02-128">Check back here for status updates; Use the Troubleshoot tool to learn how to test your origin and CDN endpoint; If your problem persists after the expected resolution time, contact support.</span></span> |
|<span data-ttu-id="4fb02-129">Nous sommes désolés, les modifications de la configuration des points de terminaison CDN subissent des retards de propagation</span><span class="sxs-lookup"><span data-stu-id="4fb02-129">We're sorry, CDN endpoint configuration changes are experiencing propagation delays</span></span> | <span data-ttu-id="4fb02-130">Revenez ici pour vérifier si la situation a évolué. Si vos modifications de la configuration ne sont pas entièrement propagées dans le délai imparti, contactez le support technique.</span><span class="sxs-lookup"><span data-stu-id="4fb02-130">Check back here for status updates; If your configuration changes are not fully propagated in the expected time, contact support.</span></span>|
|<span data-ttu-id="4fb02-131">Nous sommes désolés, nous rencontrons des problèmes pour charger le portail supplémentaire</span><span class="sxs-lookup"><span data-stu-id="4fb02-131">We're sorry, we are experiencing issues loading the supplemental portal</span></span> | <span data-ttu-id="4fb02-132">Revenez ici pour vérifier si la situation a évolué. Si votre problème persiste passé le délai prévu de résolution, contactez le support.</span><span class="sxs-lookup"><span data-stu-id="4fb02-132">Check back here for status updates; If your problem persists after the expected resolution time, contact support.</span></span>|
<span data-ttu-id="4fb02-133">Nous sommes désolés, nous rencontrons des problèmes avec certains de nos fournisseurs CDN</span><span class="sxs-lookup"><span data-stu-id="4fb02-133">We are sorry, we are experiencing issues with some of our CDN providers</span></span> | <span data-ttu-id="4fb02-134">Revenez ici pour vérifier si la situation a évolué. Si votre problème persiste passé le délai prévu de résolution, contactez le support.</span><span class="sxs-lookup"><span data-stu-id="4fb02-134">Check back here for status updates; If your problem persists after the expected resolution time, contact support.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="4fb02-135">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="4fb02-135">Next steps</span></span>

- [<span data-ttu-id="4fb02-136">Vue d’ensemble d’Azure Resource Health</span><span class="sxs-lookup"><span data-stu-id="4fb02-136">Read an overview of Azure resource health</span></span>](../resource-health/resource-health-overview.md)
- [<span data-ttu-id="4fb02-137">Résolution des problèmes de compression des fichiers CDN</span><span class="sxs-lookup"><span data-stu-id="4fb02-137">Troubleshoot issues with CDN compression</span></span>](./cdn-troubleshoot-compression.md)
- [<span data-ttu-id="4fb02-138">Dépannage des points de terminaison de CDN renvoyant des états 404</span><span class="sxs-lookup"><span data-stu-id="4fb02-138">Troubleshoot issues with 404 errors</span></span>](./cdn-troubleshoot-endpoint.md)