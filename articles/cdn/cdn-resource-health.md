---
title: "contrôle d’intégrité de hello aaaMonitor des ressources d’Azure CDN | Documents Microsoft"
description: "Découvrez comment toomonitor hello d’intégrité de vos ressources Azure CDN à l’aide de l’intégrité des ressources Azure."
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
ms.openlocfilehash: 0a77e56d2fecae4bde6c83730c05375853a6638a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-hello-health-of-azure-cdn-resources"></a><span data-ttu-id="82d78-103">Surveiller la santé hello des ressources d’Azure CDN</span><span class="sxs-lookup"><span data-stu-id="82d78-103">Monitor hello health of Azure CDN resources</span></span>
  
<span data-ttu-id="82d78-104">Azure CDN Resource Health est un sous-ensemble [d’Azure Resource Health](../resource-health/resource-health-overview.md).</span><span class="sxs-lookup"><span data-stu-id="82d78-104">Azure CDN Resource health is a subset of [Azure resource health](../resource-health/resource-health-overview.md).</span></span>  <span data-ttu-id="82d78-105">Vous pouvez utiliser Azure d’intégrité toomonitor hello contrôle d’intégrité des ressources CDN et recevoir des problèmes de tootroubleshoot des instructions.</span><span class="sxs-lookup"><span data-stu-id="82d78-105">You can use Azure resource health toomonitor hello health of CDN resources and receive actionable guidance tootroubleshoot problems.</span></span>

>[!IMPORTANT] 
><span data-ttu-id="82d78-106">L’intégrité des ressources Azure CDN comptes uniquement actuellement pour la santé hello de remise globale du CDN et les fonctionnalités de l’API.</span><span class="sxs-lookup"><span data-stu-id="82d78-106">Azure CDN resource health only currently accounts for hello health of global CDN delivery and API capabilities.</span></span>  <span data-ttu-id="82d78-107">Azure CDN Resource Health ne vérifie pas les points de terminaison CDN individuels.</span><span class="sxs-lookup"><span data-stu-id="82d78-107">Azure CDN resource health does not verify individual CDN endpoints.</span></span>
>
><span data-ttu-id="82d78-108">signaux Hello ce flux de contrôle d’intégrité Azure CDN peuvent être up minutes too15 retardées.</span><span class="sxs-lookup"><span data-stu-id="82d78-108">hello signals that feed Azure CDN resource health may be up too15 minutes delayed.</span></span>

## <a name="how-toofind-azure-cdn-resource-health"></a><span data-ttu-id="82d78-109">Comment toofind l’intégrité des ressources Azure CDN</span><span class="sxs-lookup"><span data-stu-id="82d78-109">How toofind Azure CDN resource health</span></span>

1. <span data-ttu-id="82d78-110">Bonjour [portail Azure](https://portal.azure.com), recherchez le profil CDN tooyour.</span><span class="sxs-lookup"><span data-stu-id="82d78-110">In hello [Azure portal](https://portal.azure.com), browse tooyour CDN profile.</span></span>

2. <span data-ttu-id="82d78-111">Cliquez sur hello **paramètres** bouton.</span><span class="sxs-lookup"><span data-stu-id="82d78-111">Click hello **Settings** button.</span></span>

    ![Bouton Paramètres](./media/cdn-resource-health/cdn-profile-settings.png)

3. <span data-ttu-id="82d78-113">Sous *Support + dépannage*, cliquez sur **Intégrité des ressources**.</span><span class="sxs-lookup"><span data-stu-id="82d78-113">Under *Support + troubleshooting*, click **Resource health**.</span></span>

    ![Intégrité des ressources CDN](./media/cdn-resource-health/cdn-resource-health3.png)

>[!TIP] 
><span data-ttu-id="82d78-115">Vous pouvez également trouver des ressources CDN dans hello *l’intégrité des ressources* vignette Bonjour *aide + support* panneau.</span><span class="sxs-lookup"><span data-stu-id="82d78-115">You can also find CDN resources listed in hello *Resource health* tile in hello *Help + support* blade.</span></span>  <span data-ttu-id="82d78-116">Vous pouvez obtenir rapidement trop*aide + support* en cliquant sur hello encerclé **?**</span><span class="sxs-lookup"><span data-stu-id="82d78-116">You can quickly get too*Help + support* by clicking hello circled **?**</span></span> <span data-ttu-id="82d78-117">dans hello coin supérieur droit du portail de hello.</span><span class="sxs-lookup"><span data-stu-id="82d78-117">in hello upper right corner of hello portal.</span></span>
>
> ![Aide + Support](./media/cdn-resource-health/cdn-help-support.png)

## <a name="azure-cdn-specific-messages"></a><span data-ttu-id="82d78-119">Messages propres à CDN Azure</span><span class="sxs-lookup"><span data-stu-id="82d78-119">Azure CDN-specific messages</span></span>

<span data-ttu-id="82d78-120">Vous trouverez les États associés tooAzure CDN l’intégrité des ressources ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="82d78-120">Statuses related tooAzure CDN resource health can be found below.</span></span>

|<span data-ttu-id="82d78-121">Message</span><span class="sxs-lookup"><span data-stu-id="82d78-121">Message</span></span> | <span data-ttu-id="82d78-122">Action recommandée</span><span class="sxs-lookup"><span data-stu-id="82d78-122">Recommended Action</span></span> |
|---|---|
|<span data-ttu-id="82d78-123">Vous avez peut-être arrêté, supprimé ou incorrectement configuré un ou plusieurs points de terminaison CDN</span><span class="sxs-lookup"><span data-stu-id="82d78-123">You may have stopped, removed, or misconfigured one or more of your CDN endpoints</span></span> | <span data-ttu-id="82d78-124">Vous avez peut-être arrêté, supprimé ou incorrectement configuré un ou plusieurs points de terminaison CDN.</span><span class="sxs-lookup"><span data-stu-id="82d78-124">You may have stopped, removed, or misconfigured one or more of your CDN endpoints.</span></span>|
|<span data-ttu-id="82d78-125">Nous sommes désolés, hello service de gestion CDN est actuellement indisponible</span><span class="sxs-lookup"><span data-stu-id="82d78-125">We are sorry, hello CDN management service is currently unavailable</span></span> | <span data-ttu-id="82d78-126">À vérifier les mises à jour d’état ; Si le problème persiste après que hello attendu le temps de résolution, contactez le support technique.</span><span class="sxs-lookup"><span data-stu-id="82d78-126">Check back here for status updates; If your problem persists after hello expected resolution time, contact support.</span></span>|
|<span data-ttu-id="82d78-127">Désolé. Vos points de terminaison CDN peuvent être affectés par des problèmes courants liés à certains de nos fournisseurs CDN</span><span class="sxs-lookup"><span data-stu-id="82d78-127">We're sorry, your CDN endpoints may be impacted by ongoing issues with some of our CDN providers</span></span> | <span data-ttu-id="82d78-128">À vérifier les mises à jour d’état ; Utilisez toolearn d’outil de résolution des problèmes de hello comment tootest votre origine et le point de terminaison CDN Si le problème persiste après que hello attendu le temps de résolution, contactez le support technique.</span><span class="sxs-lookup"><span data-stu-id="82d78-128">Check back here for status updates; Use hello Troubleshoot tool toolearn how tootest your origin and CDN endpoint; If your problem persists after hello expected resolution time, contact support.</span></span> |
|<span data-ttu-id="82d78-129">Nous sommes désolés, les modifications de la configuration des points de terminaison CDN subissent des retards de propagation</span><span class="sxs-lookup"><span data-stu-id="82d78-129">We're sorry, CDN endpoint configuration changes are experiencing propagation delays</span></span> | <span data-ttu-id="82d78-130">À vérifier les mises à jour d’état ; Si vos modifications de configuration ne sont pas complètement propagées dans le temps de hello attendu, contactez le support technique.</span><span class="sxs-lookup"><span data-stu-id="82d78-130">Check back here for status updates; If your configuration changes are not fully propagated in hello expected time, contact support.</span></span>|
|<span data-ttu-id="82d78-131">Nous sommes désolés, que nous rencontrons des problèmes lors du chargement du portail supplémentaire du hello</span><span class="sxs-lookup"><span data-stu-id="82d78-131">We're sorry, we are experiencing issues loading hello supplemental portal</span></span> | <span data-ttu-id="82d78-132">À vérifier les mises à jour d’état ; Si le problème persiste après que hello attendu le temps de résolution, contactez le support technique.</span><span class="sxs-lookup"><span data-stu-id="82d78-132">Check back here for status updates; If your problem persists after hello expected resolution time, contact support.</span></span>|
<span data-ttu-id="82d78-133">Nous sommes désolés, nous rencontrons des problèmes avec certains de nos fournisseurs CDN</span><span class="sxs-lookup"><span data-stu-id="82d78-133">We are sorry, we are experiencing issues with some of our CDN providers</span></span> | <span data-ttu-id="82d78-134">À vérifier les mises à jour d’état ; Si le problème persiste après que hello attendu le temps de résolution, contactez le support technique.</span><span class="sxs-lookup"><span data-stu-id="82d78-134">Check back here for status updates; If your problem persists after hello expected resolution time, contact support.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="82d78-135">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="82d78-135">Next steps</span></span>

- [<span data-ttu-id="82d78-136">Vue d’ensemble d’Azure Resource Health</span><span class="sxs-lookup"><span data-stu-id="82d78-136">Read an overview of Azure resource health</span></span>](../resource-health/resource-health-overview.md)
- [<span data-ttu-id="82d78-137">Résolution des problèmes de compression des fichiers CDN</span><span class="sxs-lookup"><span data-stu-id="82d78-137">Troubleshoot issues with CDN compression</span></span>](./cdn-troubleshoot-compression.md)
- [<span data-ttu-id="82d78-138">Dépannage des points de terminaison de CDN renvoyant des états 404</span><span class="sxs-lookup"><span data-stu-id="82d78-138">Troubleshoot issues with 404 errors</span></span>](./cdn-troubleshoot-endpoint.md)