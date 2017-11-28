---
title: "statistiques d’aaaReal au moment d’Azure CDN | Documents Microsoft"
description: "Statistiques en temps réel fournissent des données en temps réel sur les performances de hello du CDN Azure lors de la remise de contenu tooyour clients."
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: c7989340-1172-4315-acbb-186ba34dd52a
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: 68900a5092b767e45c1fdf9cef2cd03f55f38a6e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="real-time-stats-in-microsoft-azure-cdn"></a><span data-ttu-id="2aa44-103">Statistiques en temps réel dans Microsoft Azure CDN</span><span class="sxs-lookup"><span data-stu-id="2aa44-103">Real-time stats in Microsoft Azure CDN</span></span>
[!INCLUDE [cdn-premium-feature](../../includes/cdn-premium-feature.md)]

## <a name="overview"></a><span data-ttu-id="2aa44-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="2aa44-104">Overview</span></span>
<span data-ttu-id="2aa44-105">Ce document explique les statistiques en temps réel dans Microsoft Azure CDN.</span><span class="sxs-lookup"><span data-stu-id="2aa44-105">This document explains real-time stats in Microsoft Azure CDN.</span></span>  <span data-ttu-id="2aa44-106">Cette fonctionnalité fournit des données en temps réel, telles que la bande passante, les États de cache et les connexions simultanées tooyour CDN profil lors de la remise de contenu tooyour clients.</span><span class="sxs-lookup"><span data-stu-id="2aa44-106">This functionality provides real-time data, such as bandwidth, cache statuses, and concurrent connections tooyour CDN profile when delivering content tooyour clients.</span></span> <span data-ttu-id="2aa44-107">Cela permet la surveillance continue de l’intégrité hello de votre service à tout moment, y compris les événements de mise en production.</span><span class="sxs-lookup"><span data-stu-id="2aa44-107">This enables continuous monitoring of hello health of your service at any time, including go-live events.</span></span>

<span data-ttu-id="2aa44-108">Hello suivant graphiques est disponible :</span><span class="sxs-lookup"><span data-stu-id="2aa44-108">hello following graphs are available:</span></span>

* [<span data-ttu-id="2aa44-109">Bande passante</span><span class="sxs-lookup"><span data-stu-id="2aa44-109">Bandwidth</span></span>](#bandwidth)
* [<span data-ttu-id="2aa44-110">Codes d’état</span><span class="sxs-lookup"><span data-stu-id="2aa44-110">Status Codes</span></span>](#status-codes)
* [<span data-ttu-id="2aa44-111">États du cache</span><span class="sxs-lookup"><span data-stu-id="2aa44-111">Cache Statuses</span></span>](#cache-statuses)
* [<span data-ttu-id="2aa44-112">Connexions</span><span class="sxs-lookup"><span data-stu-id="2aa44-112">Connections</span></span>](#connections)

## <a name="accessing-real-time-stats"></a><span data-ttu-id="2aa44-113">Accès à des statistiques en temps réel</span><span class="sxs-lookup"><span data-stu-id="2aa44-113">Accessing real-time stats</span></span>
1. <span data-ttu-id="2aa44-114">Bonjour [Azure Portal](https://portal.azure.com), recherchez le profil CDN tooyour.</span><span class="sxs-lookup"><span data-stu-id="2aa44-114">In hello [Azure Portal](https://portal.azure.com), browse tooyour CDN profile.</span></span>
   
    ![Panneau du profil CDN](./media/cdn-real-time-stats/cdn-profile-blade.png)
2. <span data-ttu-id="2aa44-116">À partir du Panneau de profil hello CDN, cliquez sur hello **gérer** bouton.</span><span class="sxs-lookup"><span data-stu-id="2aa44-116">From hello CDN profile blade, click hello **Manage** button.</span></span>
   
    ![Bouton de gestion du panneau de profil CDN](./media/cdn-real-time-stats/cdn-manage-btn.png)
   
    <span data-ttu-id="2aa44-118">portail de gestion CDN Hello s’ouvre.</span><span class="sxs-lookup"><span data-stu-id="2aa44-118">hello CDN management portal opens.</span></span>
3. <span data-ttu-id="2aa44-119">Placez votre curseur sur hello **Analytique** tab, puis pointez sur hello **les statistiques en temps réel** menu volant.</span><span class="sxs-lookup"><span data-stu-id="2aa44-119">Hover over hello **Analytics** tab, then hover over hello **Real-Time Stats** flyout.</span></span>  <span data-ttu-id="2aa44-120">Cliquez sur **HTTP Large Object**.</span><span class="sxs-lookup"><span data-stu-id="2aa44-120">Click on **HTTP Large Object**.</span></span>
   
    ![Portail de gestion CDN](./media/cdn-real-time-stats/cdn-premium-portal.png)
   
    <span data-ttu-id="2aa44-122">Hello statistiques en temps réel graphiques sont affichés.</span><span class="sxs-lookup"><span data-stu-id="2aa44-122">hello real-time stats graphs are displayed.</span></span>

<span data-ttu-id="2aa44-123">Chacun des graphiques de hello affiche des statistiques en temps réel pour l’intervalle de temps hello sélectionné, lorsque le chargement de la page hello.</span><span class="sxs-lookup"><span data-stu-id="2aa44-123">Each of hello graphs displays real-time statistics for hello selected time span, starting when hello page loads.</span></span>  <span data-ttu-id="2aa44-124">graphiques de Hello mettre à jour automatiquement après quelques secondes.</span><span class="sxs-lookup"><span data-stu-id="2aa44-124">hello graphs update automatically every few seconds.</span></span>  <span data-ttu-id="2aa44-125">Hello **actualiser le graphique** bouton, le cas échéant, effacera graphique hello, après quoi, il affiche uniquement les données de salutation sélectionnée.</span><span class="sxs-lookup"><span data-stu-id="2aa44-125">hello **Refresh Graph** button, if present, will clear hello graph, after which it will only display hello selected data.</span></span>

## <a name="bandwidth"></a><span data-ttu-id="2aa44-126">Bande passante</span><span class="sxs-lookup"><span data-stu-id="2aa44-126">Bandwidth</span></span>
![Graphique Bande passante](./media/cdn-real-time-stats/cdn-bandwidth.png)

<span data-ttu-id="2aa44-128">Hello **la bande passante** graphique affiche la quantité hello de bande passante utilisée pour la plateforme actuelle de hello sur un intervalle de temps hello sélectionné.</span><span class="sxs-lookup"><span data-stu-id="2aa44-128">hello **Bandwidth** graph displays hello amount of bandwidth used for hello current platform over hello selected time span.</span></span> <span data-ttu-id="2aa44-129">la partie ombrée Hello du graphique de hello indique l’utilisation de la bande passante.</span><span class="sxs-lookup"><span data-stu-id="2aa44-129">hello shaded portion of hello graph indicates bandwidth usage.</span></span> <span data-ttu-id="2aa44-130">Hello exacte de la bande passante en cours d’utilisation s’affiche directement sous le graphique en courbes hello.</span><span class="sxs-lookup"><span data-stu-id="2aa44-130">hello exact amount of bandwidth currently being used is displayed directly below hello line graph.</span></span>

## <a name="status-codes"></a><span data-ttu-id="2aa44-131">Codes d’état</span><span class="sxs-lookup"><span data-stu-id="2aa44-131">Status Codes</span></span>
![Graphique Code d’état](./media/cdn-real-time-stats/cdn-status-codes.png)

<span data-ttu-id="2aa44-133">Hello **Codes d’état** graphique indique la fréquence à laquelle certains codes de réponse HTTP sont produisent sur un intervalle de temps hello sélectionné.</span><span class="sxs-lookup"><span data-stu-id="2aa44-133">hello **Status Codes** graph indicates how often certain HTTP response codes are occurring over hello selected time span.</span></span>

> [!TIP]
> <span data-ttu-id="2aa44-134">Pour obtenir une description de chaque option de code d’état HTTP, consultez la page [Azure CDN HTTP Status Codes](https://msdn.microsoft.com/library/mt759238.aspx)(Codes d’état HTTP d’Azure CDN).</span><span class="sxs-lookup"><span data-stu-id="2aa44-134">For a description of each HTTP status code option, see [Azure CDN HTTP Status Codes](https://msdn.microsoft.com/library/mt759238.aspx).</span></span>
> 
> 

<span data-ttu-id="2aa44-135">Une liste des codes d’état HTTP s’affiche directement au-dessus de graphique de hello.</span><span class="sxs-lookup"><span data-stu-id="2aa44-135">A list of HTTP status codes is displayed directly above hello graph.</span></span> <span data-ttu-id="2aa44-136">Cette liste indique chaque code d’état qui peut être inclus dans le graphique en courbes hello et nombre actuel de hello d’occurrences par seconde pour ce code d’état.</span><span class="sxs-lookup"><span data-stu-id="2aa44-136">This list indicates each status code that can be included in hello line graph and hello current number of occurrences per second for that status code.</span></span> <span data-ttu-id="2aa44-137">Par défaut, une ligne est affichée pour chacun de ces codes d’état dans le graphique de hello.</span><span class="sxs-lookup"><span data-stu-id="2aa44-137">By default, a line is displayed for each of these status codes in hello graph.</span></span> <span data-ttu-id="2aa44-138">Toutefois, vous pouvez choisir tooonly codes d’état hello moniteur qui ont une signification spéciale pour votre configuration CDN.</span><span class="sxs-lookup"><span data-stu-id="2aa44-138">However, you can choose tooonly monitor hello status codes that have special significance for your CDN configuration.</span></span> <span data-ttu-id="2aa44-139">toodo, les codes d’état souhaité de hello et désactivez toutes les autres options, puis cliquez sur **actualiser le graphique**.</span><span class="sxs-lookup"><span data-stu-id="2aa44-139">toodo this, check hello desired status codes and clear all other options, then click **Refresh Graph**.</span></span> 

<span data-ttu-id="2aa44-140">Vous pouvez masquer temporairement les données consignées pour un code d’état spécifique.</span><span class="sxs-lookup"><span data-stu-id="2aa44-140">You can temporarily hide logged data for a particular status code.</span></span>  <span data-ttu-id="2aa44-141">À partir de la légende hello directement sous le graphique de hello, cliquez sur hello code de statut toohide.</span><span class="sxs-lookup"><span data-stu-id="2aa44-141">From hello legend directly below hello graph, click hello status code you want toohide.</span></span> <span data-ttu-id="2aa44-142">code d’état Hello est immédiatement masquée dans le graphique de hello.</span><span class="sxs-lookup"><span data-stu-id="2aa44-142">hello status code will be immediately hidden from hello graph.</span></span> <span data-ttu-id="2aa44-143">Cliquez à nouveau sur ce code d’état entraîne que toobe option affichée de nouveau.</span><span class="sxs-lookup"><span data-stu-id="2aa44-143">Clicking that status code again will cause that option toobe displayed again.</span></span>

## <a name="cache-statuses"></a><span data-ttu-id="2aa44-144">États du cache</span><span class="sxs-lookup"><span data-stu-id="2aa44-144">Cache Statuses</span></span>
![Graphique États du cache](./media/cdn-real-time-stats/cdn-cache-status.png)

<span data-ttu-id="2aa44-146">Hello **Cache états** graphique indique la fréquence à laquelle certains types d’états de cache sont produisent sur un intervalle de temps hello sélectionné.</span><span class="sxs-lookup"><span data-stu-id="2aa44-146">hello **Cache Statuses** graph indicates how often certain types of cache statuses are occurring over hello selected time span.</span></span> 

> [!TIP]
> <span data-ttu-id="2aa44-147">Pour obtenir une description de chaque option de code d’état du cache, consultez la page [Azure CDN Cache Status Codes](https://msdn.microsoft.com/library/mt759237.aspx)(Codes d’état du cache d’Azure CDN).</span><span class="sxs-lookup"><span data-stu-id="2aa44-147">For a description of each cache status code option, see [Azure CDN Cache Status Codes](https://msdn.microsoft.com/library/mt759237.aspx).</span></span>
> 
> 

<span data-ttu-id="2aa44-148">Une liste des codes d’état du cache s’affiche directement au-dessus de graphique de hello.</span><span class="sxs-lookup"><span data-stu-id="2aa44-148">A list of cache status codes is displayed directly above hello graph.</span></span> <span data-ttu-id="2aa44-149">Cette liste indique chaque code d’état qui peut être inclus dans le graphique en courbes hello et nombre actuel de hello d’occurrences par seconde pour ce code d’état.</span><span class="sxs-lookup"><span data-stu-id="2aa44-149">This list indicates each status code that can be included in hello line graph and hello current number of occurrences per second for that status code.</span></span> <span data-ttu-id="2aa44-150">Par défaut, une ligne est affichée pour chacun de ces codes d’état dans le graphique de hello.</span><span class="sxs-lookup"><span data-stu-id="2aa44-150">By default, a line is displayed for each of these status codes in hello graph.</span></span> <span data-ttu-id="2aa44-151">Toutefois, vous pouvez choisir tooonly codes d’état hello moniteur qui ont une signification spéciale pour votre configuration CDN.</span><span class="sxs-lookup"><span data-stu-id="2aa44-151">However, you can choose tooonly monitor hello status codes that have special significance for your CDN configuration.</span></span> <span data-ttu-id="2aa44-152">toodo, les codes d’état souhaité de hello et désactivez toutes les autres options, puis cliquez sur **actualiser le graphique**.</span><span class="sxs-lookup"><span data-stu-id="2aa44-152">toodo this, check hello desired status codes and clear all other options, then click **Refresh Graph**.</span></span> 

<span data-ttu-id="2aa44-153">Vous pouvez masquer temporairement les données consignées pour un code d’état spécifique.</span><span class="sxs-lookup"><span data-stu-id="2aa44-153">You can temporarily hide logged data for a particular status code.</span></span>  <span data-ttu-id="2aa44-154">À partir de la légende hello directement sous le graphique de hello, cliquez sur hello code de statut toohide.</span><span class="sxs-lookup"><span data-stu-id="2aa44-154">From hello legend directly below hello graph, click hello status code you want toohide.</span></span> <span data-ttu-id="2aa44-155">code d’état Hello est immédiatement masquée dans le graphique de hello.</span><span class="sxs-lookup"><span data-stu-id="2aa44-155">hello status code will be immediately hidden from hello graph.</span></span> <span data-ttu-id="2aa44-156">Cliquez à nouveau sur ce code d’état entraîne que toobe option affichée de nouveau.</span><span class="sxs-lookup"><span data-stu-id="2aa44-156">Clicking that status code again will cause that option toobe displayed again.</span></span>

## <a name="connections"></a><span data-ttu-id="2aa44-157">Connexions</span><span class="sxs-lookup"><span data-stu-id="2aa44-157">Connections</span></span>
![Graphique Connexions](./media/cdn-real-time-stats/cdn-connections.png)

<span data-ttu-id="2aa44-159">Ce graphique indique le nombre de connexions qui ont été établies tooyour bord serveurs.</span><span class="sxs-lookup"><span data-stu-id="2aa44-159">This graph indicates how many connections have been established tooyour edge servers.</span></span> <span data-ttu-id="2aa44-160">Chaque demande de ressource qui traverse notre CDN entraîne une connexion.</span><span class="sxs-lookup"><span data-stu-id="2aa44-160">Each request for an asset that passes through our CDN results in a connection.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2aa44-161">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="2aa44-161">Next Steps</span></span>
* <span data-ttu-id="2aa44-162">Tenez-vous informé en consultant la page [Real-time alerts in Azure CDN](cdn-real-time-alerts.md)</span><span class="sxs-lookup"><span data-stu-id="2aa44-162">Get notified with [Real-time alerts in Azure CDN](cdn-real-time-alerts.md)</span></span>
* <span data-ttu-id="2aa44-163">Allez plus loin en vous familiarisant avec les [rapports HTTP avancés](cdn-advanced-http-reports.md)</span><span class="sxs-lookup"><span data-stu-id="2aa44-163">Dig deeper with [advanced HTTP reports](cdn-advanced-http-reports.md)</span></span>
* <span data-ttu-id="2aa44-164">Analysez les [modes d’utilisation](cdn-analyze-usage-patterns.md)</span><span class="sxs-lookup"><span data-stu-id="2aa44-164">Analyze [usage patterns](cdn-analyze-usage-patterns.md)</span></span>

