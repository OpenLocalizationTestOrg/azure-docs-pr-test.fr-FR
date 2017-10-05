---
title: "Contrôle du comportement de mise en cache du CDN Azure avec des chaînes de requête - Premium | Microsoft Docs"
description: "La mise en cache des chaînes de requête CDN Azure contrôle la manière dont les fichiers doivent être mis en cache lorsqu’ils contiennent des chaînes de requête."
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: 99db4a85-4f5f-431f-ac3a-69e05518c997
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: 145067c2ce50b41c4783f4de4052c0e7cb529fc7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="control-azure-cdn-caching-behavior-with-query-strings---premium"></a><span data-ttu-id="83894-103">Contrôle du comportement de mise en cache du CDN Azure avec des chaînes de requête - Premium</span><span class="sxs-lookup"><span data-stu-id="83894-103">Control Azure CDN caching behavior with query strings - Premium</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="83894-104">Standard</span><span class="sxs-lookup"><span data-stu-id="83894-104">Standard</span></span>](cdn-query-string.md)
> * [<span data-ttu-id="83894-105">CDN Azure Premium fourni par Verizon</span><span class="sxs-lookup"><span data-stu-id="83894-105">Azure CDN Premium from Verizon</span></span>](cdn-query-string-premium.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="83894-106">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="83894-106">Overview</span></span>
<span data-ttu-id="83894-107">La mise en cache des chaînes de requête contrôle la manière dont les fichiers doivent être mis en cache lorsqu'ils contiennent des chaînes de requête.</span><span class="sxs-lookup"><span data-stu-id="83894-107">Query string caching controls how files are to be cached when they contain query strings.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="83894-108">Les produits CDN Standard et Premium proposent les mêmes fonctionnalités de mise en cache des chaînes de requête, mais l’interface utilisateur est différente.</span><span class="sxs-lookup"><span data-stu-id="83894-108">The Standard and Premium CDN products provide the same query string caching functionality, but the user interface differs.</span></span>  <span data-ttu-id="83894-109">Ce document décrit l’interface du **CDN Azure Premium fourni par Verizon**.</span><span class="sxs-lookup"><span data-stu-id="83894-109">This document describes the interface for **Azure CDN Premium from Verizon**.</span></span>  <span data-ttu-id="83894-110">Pour la mise en cache des chaînes de requête avec le **CDN Azure Standard fourni par Akamai** et le **CDN Azure Standard fourni par Verizon**, consultez [Contrôle du comportement de mise en cache des demandes CDN avec des chaînes de requête](cdn-query-string.md).</span><span class="sxs-lookup"><span data-stu-id="83894-110">For query string caching with **Azure CDN Standard from Akamai** and **Azure CDN Standard from Verizon**, see [Controlling caching behavior of CDN requests with query strings](cdn-query-string.md).</span></span>
> 
> 

<span data-ttu-id="83894-111">Trois modes sont disponibles :</span><span class="sxs-lookup"><span data-stu-id="83894-111">Three modes are available:</span></span>

* <span data-ttu-id="83894-112">**standard-cache** : il s’agit du mode par défaut.</span><span class="sxs-lookup"><span data-stu-id="83894-112">**standard-cache**:  This is the default mode.</span></span>  <span data-ttu-id="83894-113">Le nœud de périmètre CDN transmet la chaîne de requête du demandeur vers l’origine de la première demande et met en cache l’élément multimédia.</span><span class="sxs-lookup"><span data-stu-id="83894-113">The CDN edge node will pass the query string from the requestor to the origin on the first request and cache the asset.</span></span>  <span data-ttu-id="83894-114">Toutes les demandes ultérieures concernant cet élément multimédia traitées à partir du nœud de périmètre ignorent la chaîne de requête jusqu’à l’arrivée à expiration de l’élément multimédia mis en cache.</span><span class="sxs-lookup"><span data-stu-id="83894-114">All subsequent requests for that asset that are served from the edge node will ignore the query string until the cached asset expires.</span></span>
* <span data-ttu-id="83894-115">**no-cache** : dans ce mode, les demandes avec des chaînes de requête ne sont pas mises en cache au niveau du nœud de périmètre CDN.</span><span class="sxs-lookup"><span data-stu-id="83894-115">**no-cache**:  In this mode, requests with query strings are not cached at the CDN edge node.</span></span>  <span data-ttu-id="83894-116">Le nœud de périmètre récupère l’élément multimédia directement à partir de l’origine et le transmet au demandeur avec chaque demande.</span><span class="sxs-lookup"><span data-stu-id="83894-116">The edge node retrieves the asset directly from the origin and passes it to the requestor with each request.</span></span>
* <span data-ttu-id="83894-117">**unique-cache** : ce mode traite chaque demande avec une chaîne de requête comme élément multimédia unique avec son propre cache.</span><span class="sxs-lookup"><span data-stu-id="83894-117">**unique-cache**:  This mode treats each request with a query string as a unique asset with its own cache.</span></span>  <span data-ttu-id="83894-118">Par exemple, la réponse depuis l’origine d’une demande pour *foo.ashx?q=bar* est mise en cache au niveau du nœud de périmètre et renvoyée pour les caches suivants avec la même chaîne de requête.</span><span class="sxs-lookup"><span data-stu-id="83894-118">For example, the response from the origin for a request for *foo.ashx?q=bar* would be cached at the edge node and returned for subsequent caches with that same query string.</span></span>  <span data-ttu-id="83894-119">Une demande pour *foo.ashx?q=somethingelse* est mise en cache comme un élément multimédia distinct avec sa propre durée de vie.</span><span class="sxs-lookup"><span data-stu-id="83894-119">A request for *foo.ashx?q=somethingelse* would be cached as a separate asset with its own time to live.</span></span>

## <a name="changing-query-string-caching-settings-for-premium-cdn-profiles"></a><span data-ttu-id="83894-120">Modification des paramètres de mise en cache des chaînes de requête pour les profils CDN Premium</span><span class="sxs-lookup"><span data-stu-id="83894-120">Changing query string caching settings for premium CDN profiles</span></span>
1. <span data-ttu-id="83894-121">Dans le panneau de profil CDN, cliquez sur le bouton **Gérer** .</span><span class="sxs-lookup"><span data-stu-id="83894-121">From the CDN profile blade, click the **Manage** button.</span></span>
   
    ![Bouton de gestion du panneau de profil CDN](./media/cdn-query-string-premium/cdn-manage-btn.png)
   
    <span data-ttu-id="83894-123">Le portail de gestion CDN s'ouvre.</span><span class="sxs-lookup"><span data-stu-id="83894-123">The CDN management portal opens.</span></span>
2. <span data-ttu-id="83894-124">Pointez sur l’onglet **HTTP volumineux**, puis pointez sur le menu volant **Paramètres de cache**.</span><span class="sxs-lookup"><span data-stu-id="83894-124">Hover over the **HTTP Large** tab, then hover over the **Cache Settings** flyout.</span></span>  <span data-ttu-id="83894-125">Cliquez sur **Mise en cache des chaînes de requête**.</span><span class="sxs-lookup"><span data-stu-id="83894-125">Click on **Query-String Caching**.</span></span>
   
    <span data-ttu-id="83894-126">Les options de mise en cache des chaînes de requête s'affichent.</span><span class="sxs-lookup"><span data-stu-id="83894-126">Query string caching options are displayed.</span></span>
   
    ![Options de mise en cache des chaînes de requête CDN](./media/cdn-query-string-premium/cdn-query-string.png)
3. <span data-ttu-id="83894-128">Une fois vos sélections effectuées, cliquez sur le bouton **Mettre à jour** .</span><span class="sxs-lookup"><span data-stu-id="83894-128">After making your selection, click the **Update** button.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="83894-129">La modification des paramètres peut ne pas être visible immédiatement, car la propagation de l’inscription dans le CDN prend un certain temps.</span><span class="sxs-lookup"><span data-stu-id="83894-129">The settings changes may not be immediately visible, as it takes time for the registration to propagate through the CDN.</span></span>  <span data-ttu-id="83894-130">Pour les profils du <b>CDN Azure fourni par Verizon</b>, la propagation s’effectue généralement dans un délai de 90 minutes, mais elle peut prendre plus de temps dans certains cas.</span><span class="sxs-lookup"><span data-stu-id="83894-130">For <b>Azure CDN from Verizon</b> profiles, propagation will usually complete within 90 minutes, but in some cases can take longer.</span></span>
> 
> 

