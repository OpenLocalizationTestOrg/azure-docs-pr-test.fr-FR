---
title: "Statistiques en temps réel dans Azure CDN | Microsoft Docs"
description: "Les statistiques en temps réel fournissent des données en temps réel sur les performances du CDN Azure lors de la diffusion de contenu à vos clients."
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
ms.openlocfilehash: e9b9522de6b2c54dc794b00100ffe358296ecfdd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="real-time-stats-in-microsoft-azure-cdn"></a><span data-ttu-id="e9926-103">Statistiques en temps réel dans Microsoft Azure CDN</span><span class="sxs-lookup"><span data-stu-id="e9926-103">Real-time stats in Microsoft Azure CDN</span></span>
[!INCLUDE [cdn-premium-feature](../../includes/cdn-premium-feature.md)]

## <a name="overview"></a><span data-ttu-id="e9926-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="e9926-104">Overview</span></span>
<span data-ttu-id="e9926-105">Ce document explique les statistiques en temps réel dans Microsoft Azure CDN.</span><span class="sxs-lookup"><span data-stu-id="e9926-105">This document explains real-time stats in Microsoft Azure CDN.</span></span>  <span data-ttu-id="e9926-106">Cette fonctionnalité fournit des données en temps réel (par exemple, relatives à la bande passante, aux états du cache et aux connexions simultanées) à votre profil CDN lors de la diffusion de contenu à vos clients.</span><span class="sxs-lookup"><span data-stu-id="e9926-106">This functionality provides real-time data, such as bandwidth, cache statuses, and concurrent connections to your CDN profile when delivering content to your clients.</span></span> <span data-ttu-id="e9926-107">Elle permet une surveillance continue de l’intégrité de votre service à tout moment, y compris lors des événements de mise en service.</span><span class="sxs-lookup"><span data-stu-id="e9926-107">This enables continuous monitoring of the health of your service at any time, including go-live events.</span></span>

<span data-ttu-id="e9926-108">Les graphiques suivants sont disponibles :</span><span class="sxs-lookup"><span data-stu-id="e9926-108">The following graphs are available:</span></span>

* [<span data-ttu-id="e9926-109">Bande passante</span><span class="sxs-lookup"><span data-stu-id="e9926-109">Bandwidth</span></span>](#bandwidth)
* [<span data-ttu-id="e9926-110">Codes d’état</span><span class="sxs-lookup"><span data-stu-id="e9926-110">Status Codes</span></span>](#status-codes)
* [<span data-ttu-id="e9926-111">États du cache</span><span class="sxs-lookup"><span data-stu-id="e9926-111">Cache Statuses</span></span>](#cache-statuses)
* [<span data-ttu-id="e9926-112">Connexions</span><span class="sxs-lookup"><span data-stu-id="e9926-112">Connections</span></span>](#connections)

## <a name="accessing-real-time-stats"></a><span data-ttu-id="e9926-113">Accès à des statistiques en temps réel</span><span class="sxs-lookup"><span data-stu-id="e9926-113">Accessing real-time stats</span></span>
1. <span data-ttu-id="e9926-114">Dans le [portail Azure](https://portal.azure.com), accédez à votre profil CDN.</span><span class="sxs-lookup"><span data-stu-id="e9926-114">In the [Azure Portal](https://portal.azure.com), browse to your CDN profile.</span></span>
   
    ![Panneau du profil CDN](./media/cdn-real-time-stats/cdn-profile-blade.png)
2. <span data-ttu-id="e9926-116">Dans le panneau de profil CDN, cliquez sur le bouton **Gérer** .</span><span class="sxs-lookup"><span data-stu-id="e9926-116">From the CDN profile blade, click the **Manage** button.</span></span>
   
    ![Bouton de gestion du panneau de profil CDN](./media/cdn-real-time-stats/cdn-manage-btn.png)
   
    <span data-ttu-id="e9926-118">Le portail de gestion CDN s'ouvre.</span><span class="sxs-lookup"><span data-stu-id="e9926-118">The CDN management portal opens.</span></span>
3. <span data-ttu-id="e9926-119">Pointez sur l’onglet **Analyse**, puis sur le menu volant **Statistiques en temps réel**.</span><span class="sxs-lookup"><span data-stu-id="e9926-119">Hover over the **Analytics** tab, then hover over the **Real-Time Stats** flyout.</span></span>  <span data-ttu-id="e9926-120">Cliquez sur **HTTP Large Object**.</span><span class="sxs-lookup"><span data-stu-id="e9926-120">Click on **HTTP Large Object**.</span></span>
   
    ![Portail de gestion CDN](./media/cdn-real-time-stats/cdn-premium-portal.png)
   
    <span data-ttu-id="e9926-122">Les graphiques de statistiques en temps réel s’affichent.</span><span class="sxs-lookup"><span data-stu-id="e9926-122">The real-time stats graphs are displayed.</span></span>

<span data-ttu-id="e9926-123">Chacun de ces graphiques affiche des statistiques en temps réel pour la période sélectionnée. L’affichage débute dès le chargement de la page.</span><span class="sxs-lookup"><span data-stu-id="e9926-123">Each of the graphs displays real-time statistics for the selected time span, starting when the page loads.</span></span>  <span data-ttu-id="e9926-124">Les graphiques se mettent automatiquement à jour après quelques secondes.</span><span class="sxs-lookup"><span data-stu-id="e9926-124">The graphs update automatically every few seconds.</span></span>  <span data-ttu-id="e9926-125">Le bouton **Actualiser le graphique**, le cas échéant, permet d’effacer le graphique. En cliquant sur ce bouton, seules les données sélectionnées s’afficheront.</span><span class="sxs-lookup"><span data-stu-id="e9926-125">The **Refresh Graph** button, if present, will clear the graph, after which it will only display the selected data.</span></span>

## <a name="bandwidth"></a><span data-ttu-id="e9926-126">Bande passante</span><span class="sxs-lookup"><span data-stu-id="e9926-126">Bandwidth</span></span>
![Graphique Bande passante](./media/cdn-real-time-stats/cdn-bandwidth.png)

<span data-ttu-id="e9926-128">Le graphique **Bande passante** montre la quantité de bande passante utilisée pour la plateforme actuelle sur l’intervalle de temps sélectionné.</span><span class="sxs-lookup"><span data-stu-id="e9926-128">The **Bandwidth** graph displays the amount of bandwidth used for the current platform over the selected time span.</span></span> <span data-ttu-id="e9926-129">La partie ombrée du graphique indique l’utilisation de la bande passante.</span><span class="sxs-lookup"><span data-stu-id="e9926-129">The shaded portion of the graph indicates bandwidth usage.</span></span> <span data-ttu-id="e9926-130">La quantité exacte de bande passante en cours d’utilisation s’affiche directement sous le graphique linéaire.</span><span class="sxs-lookup"><span data-stu-id="e9926-130">The exact amount of bandwidth currently being used is displayed directly below the line graph.</span></span>

## <a name="status-codes"></a><span data-ttu-id="e9926-131">Codes d’état</span><span class="sxs-lookup"><span data-stu-id="e9926-131">Status Codes</span></span>
![Graphique Code d’état](./media/cdn-real-time-stats/cdn-status-codes.png)

<span data-ttu-id="e9926-133">Le graphique **Codes d’état** indique la fréquence à laquelle certains codes de réponse HTTP se produisent sur l’intervalle de temps sélectionné.</span><span class="sxs-lookup"><span data-stu-id="e9926-133">The **Status Codes** graph indicates how often certain HTTP response codes are occurring over the selected time span.</span></span>

> [!TIP]
> <span data-ttu-id="e9926-134">Pour obtenir une description de chaque option de code d’état HTTP, consultez la page [Azure CDN HTTP Status Codes](https://msdn.microsoft.com/library/mt759238.aspx)(Codes d’état HTTP d’Azure CDN).</span><span class="sxs-lookup"><span data-stu-id="e9926-134">For a description of each HTTP status code option, see [Azure CDN HTTP Status Codes](https://msdn.microsoft.com/library/mt759238.aspx).</span></span>
> 
> 

<span data-ttu-id="e9926-135">La liste des codes d’état HTTP s’affiche directement au-dessus du graphique.</span><span class="sxs-lookup"><span data-stu-id="e9926-135">A list of HTTP status codes is displayed directly above the graph.</span></span> <span data-ttu-id="e9926-136">Cette liste indique chaque code d’état pouvant être inclus dans le graphique linéaire et le nombre actuel d’occurrences par seconde pour ce code d’état.</span><span class="sxs-lookup"><span data-stu-id="e9926-136">This list indicates each status code that can be included in the line graph and the current number of occurrences per second for that status code.</span></span> <span data-ttu-id="e9926-137">Par défaut, une ligne s’affiche pour chacun de ces codes d’état dans le graphique.</span><span class="sxs-lookup"><span data-stu-id="e9926-137">By default, a line is displayed for each of these status codes in the graph.</span></span> <span data-ttu-id="e9926-138">Toutefois, vous pouvez choisir de surveiller uniquement les codes d’état qui ont une importance spéciale pour votre configuration CDN.</span><span class="sxs-lookup"><span data-stu-id="e9926-138">However, you can choose to only monitor the status codes that have special significance for your CDN configuration.</span></span> <span data-ttu-id="e9926-139">Pour ce faire, cochez les codes d’état souhaité et désactivez toutes les autres options, puis cliquez sur **Actualiser le graphique**.</span><span class="sxs-lookup"><span data-stu-id="e9926-139">To do this, check the desired status codes and clear all other options, then click **Refresh Graph**.</span></span> 

<span data-ttu-id="e9926-140">Vous pouvez masquer temporairement les données consignées pour un code d’état spécifique.</span><span class="sxs-lookup"><span data-stu-id="e9926-140">You can temporarily hide logged data for a particular status code.</span></span>  <span data-ttu-id="e9926-141">Dans la légende qui se trouve directement sous le graphique, cliquez sur le code d’état que vous souhaitez masquer.</span><span class="sxs-lookup"><span data-stu-id="e9926-141">From the legend directly below the graph, click the status code you want to hide.</span></span> <span data-ttu-id="e9926-142">Le code d’état est immédiatement masqué dans le graphique.</span><span class="sxs-lookup"><span data-stu-id="e9926-142">The status code will be immediately hidden from the graph.</span></span> <span data-ttu-id="e9926-143">Pour le faire réapparaître, cochez de nouveau cette option de code d’état.</span><span class="sxs-lookup"><span data-stu-id="e9926-143">Clicking that status code again will cause that option to be displayed again.</span></span>

## <a name="cache-statuses"></a><span data-ttu-id="e9926-144">États du cache</span><span class="sxs-lookup"><span data-stu-id="e9926-144">Cache Statuses</span></span>
![Graphique États du cache](./media/cdn-real-time-stats/cdn-cache-status.png)

<span data-ttu-id="e9926-146">Le graphique **États du cache** indique la fréquence à laquelle certains types d’états du cache se produisent sur l’intervalle de temps sélectionné.</span><span class="sxs-lookup"><span data-stu-id="e9926-146">The **Cache Statuses** graph indicates how often certain types of cache statuses are occurring over the selected time span.</span></span> 

> [!TIP]
> <span data-ttu-id="e9926-147">Pour obtenir une description de chaque option de code d’état du cache, consultez la page [Azure CDN Cache Status Codes](https://msdn.microsoft.com/library/mt759237.aspx)(Codes d’état du cache d’Azure CDN).</span><span class="sxs-lookup"><span data-stu-id="e9926-147">For a description of each cache status code option, see [Azure CDN Cache Status Codes](https://msdn.microsoft.com/library/mt759237.aspx).</span></span>
> 
> 

<span data-ttu-id="e9926-148">La liste des codes d’état du cache s’affiche directement au-dessus du graphique.</span><span class="sxs-lookup"><span data-stu-id="e9926-148">A list of cache status codes is displayed directly above the graph.</span></span> <span data-ttu-id="e9926-149">Cette liste indique chaque code d’état pouvant être inclus dans le graphique linéaire et le nombre actuel d’occurrences par seconde pour ce code d’état.</span><span class="sxs-lookup"><span data-stu-id="e9926-149">This list indicates each status code that can be included in the line graph and the current number of occurrences per second for that status code.</span></span> <span data-ttu-id="e9926-150">Par défaut, une ligne s’affiche pour chacun de ces codes d’état dans le graphique.</span><span class="sxs-lookup"><span data-stu-id="e9926-150">By default, a line is displayed for each of these status codes in the graph.</span></span> <span data-ttu-id="e9926-151">Toutefois, vous pouvez choisir de surveiller uniquement les codes d’état qui ont une importance spéciale pour votre configuration CDN.</span><span class="sxs-lookup"><span data-stu-id="e9926-151">However, you can choose to only monitor the status codes that have special significance for your CDN configuration.</span></span> <span data-ttu-id="e9926-152">Pour ce faire, cochez les codes d’état souhaité et désactivez toutes les autres options, puis cliquez sur **Actualiser le graphique**.</span><span class="sxs-lookup"><span data-stu-id="e9926-152">To do this, check the desired status codes and clear all other options, then click **Refresh Graph**.</span></span> 

<span data-ttu-id="e9926-153">Vous pouvez masquer temporairement les données consignées pour un code d’état spécifique.</span><span class="sxs-lookup"><span data-stu-id="e9926-153">You can temporarily hide logged data for a particular status code.</span></span>  <span data-ttu-id="e9926-154">Dans la légende qui se trouve directement sous le graphique, cliquez sur le code d’état que vous souhaitez masquer.</span><span class="sxs-lookup"><span data-stu-id="e9926-154">From the legend directly below the graph, click the status code you want to hide.</span></span> <span data-ttu-id="e9926-155">Le code d’état est immédiatement masqué dans le graphique.</span><span class="sxs-lookup"><span data-stu-id="e9926-155">The status code will be immediately hidden from the graph.</span></span> <span data-ttu-id="e9926-156">Pour le faire réapparaître, cochez de nouveau cette option de code d’état.</span><span class="sxs-lookup"><span data-stu-id="e9926-156">Clicking that status code again will cause that option to be displayed again.</span></span>

## <a name="connections"></a><span data-ttu-id="e9926-157">Connexions</span><span class="sxs-lookup"><span data-stu-id="e9926-157">Connections</span></span>
![Graphique Connexions](./media/cdn-real-time-stats/cdn-connections.png)

<span data-ttu-id="e9926-159">Ce graphique indique le nombre de connexions qui ont été établies pour vos serveurs Edge.</span><span class="sxs-lookup"><span data-stu-id="e9926-159">This graph indicates how many connections have been established to your edge servers.</span></span> <span data-ttu-id="e9926-160">Chaque demande de ressource qui traverse notre CDN entraîne une connexion.</span><span class="sxs-lookup"><span data-stu-id="e9926-160">Each request for an asset that passes through our CDN results in a connection.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e9926-161">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="e9926-161">Next Steps</span></span>
* <span data-ttu-id="e9926-162">Tenez-vous informé en consultant la page [Real-time alerts in Azure CDN](cdn-real-time-alerts.md)</span><span class="sxs-lookup"><span data-stu-id="e9926-162">Get notified with [Real-time alerts in Azure CDN](cdn-real-time-alerts.md)</span></span>
* <span data-ttu-id="e9926-163">Allez plus loin en vous familiarisant avec les [rapports HTTP avancés](cdn-advanced-http-reports.md)</span><span class="sxs-lookup"><span data-stu-id="e9926-163">Dig deeper with [advanced HTTP reports](cdn-advanced-http-reports.md)</span></span>
* <span data-ttu-id="e9926-164">Analysez les [modes d’utilisation](cdn-analyze-usage-patterns.md)</span><span class="sxs-lookup"><span data-stu-id="e9926-164">Analyze [usage patterns](cdn-analyze-usage-patterns.md)</span></span>

