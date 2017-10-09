---
title: "comportement de mise en cache CDN Azure avec les chaînes de requête d’aaaControl | Documents Microsoft"
description: "Chaîne de requête Azure CDN mise en cache des contrôles de façon dont les fichiers sont toobe mis en cache s’ils contiennent des chaînes de requête."
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: 17410e4f-130e-489c-834e-7ca6d6f9778d
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: e7a138b2decec624a29eb703ad9a291d19c44ee8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="control-azure-cdn-caching-behavior-with-query-strings"></a><span data-ttu-id="09672-103">Contrôle du comportement de mise en cache du CDN Azure avec des chaînes de requête</span><span class="sxs-lookup"><span data-stu-id="09672-103">Control Azure CDN caching behavior with query strings</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="09672-104">Standard</span><span class="sxs-lookup"><span data-stu-id="09672-104">Standard</span></span>](cdn-query-string.md)
> * [<span data-ttu-id="09672-105">CDN Azure Premium fourni par Verizon</span><span class="sxs-lookup"><span data-stu-id="09672-105">Azure CDN Premium from Verizon</span></span>](cdn-query-string-premium.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="09672-106">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="09672-106">Overview</span></span>
<span data-ttu-id="09672-107">Chaîne de requête mise en cache des contrôles de façon dont les fichiers sont toobe mis en cache s’ils contiennent des chaînes de requête.</span><span class="sxs-lookup"><span data-stu-id="09672-107">Query string caching controls how files are toobe cached when they contain query strings.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="09672-108">produits Standard et Premium CDN Hello fournissent hello même fonctionnalité de mise en cache de chaîne de requête, mais diffère de l’interface utilisateur de hello.</span><span class="sxs-lookup"><span data-stu-id="09672-108">hello Standard and Premium CDN products provide hello same query string caching functionality, but hello user interface differs.</span></span>  <span data-ttu-id="09672-109">Ce document décrit l’interface hello pour **Azure CDN Standard à partir d’Akamai** et **Azure CDN Standard de Verizon**.</span><span class="sxs-lookup"><span data-stu-id="09672-109">This document describes hello interface for **Azure CDN Standard from Akamai** and **Azure CDN Standard from Verizon**.</span></span>  <span data-ttu-id="09672-110">Pour la mise en cache des chaînes de requête avec le **CDN Azure Premium fourni par Verizon**, consultez [Contrôle du comportement de mise en cache des demandes CDN avec des chaînes de requête – Premium](cdn-query-string-premium.md).</span><span class="sxs-lookup"><span data-stu-id="09672-110">For query string caching with **Azure CDN Premium from Verizon**, see [Controlling caching behavior of CDN requests with query strings - Premium](cdn-query-string-premium.md).</span></span>
> 
> 

<span data-ttu-id="09672-111">Trois modes sont disponibles :</span><span class="sxs-lookup"><span data-stu-id="09672-111">Three modes are available:</span></span>

* <span data-ttu-id="09672-112">**Ignorer les chaînes de requête**: c’est le mode par défaut hello.</span><span class="sxs-lookup"><span data-stu-id="09672-112">**Ignore query strings**:  This is hello default mode.</span></span>  <span data-ttu-id="09672-113">nœud de périmètre CDN Hello passera la chaîne de requête hello à partir de l’origine de toohello hello demandeur sur la première demande de hello et asset hello de cache.</span><span class="sxs-lookup"><span data-stu-id="09672-113">hello CDN edge node will pass hello query string from hello requestor toohello origin on hello first request and cache hello asset.</span></span>  <span data-ttu-id="09672-114">Toutes les demandes ultérieures pour cet élément multimédia qui sont pris en charge à partir du nœud de périmètre hello ignore la chaîne de requête hello jusqu'à ce que les ressources mises en cache hello expire.</span><span class="sxs-lookup"><span data-stu-id="09672-114">All subsequent requests for that asset that are served from hello edge node will ignore hello query string until hello cached asset expires.</span></span>
* <span data-ttu-id="09672-115">**Ignorer la mise en cache pour les URL avec des chaînes de requête**: dans ce mode, les demandes de chaînes de requête ne sont pas mis en cache au niveau du nœud de périmètre CDN hello.</span><span class="sxs-lookup"><span data-stu-id="09672-115">**Bypass caching for URL with query strings**:  In this mode, requests with query strings are not cached at hello CDN edge node.</span></span>  <span data-ttu-id="09672-116">nœud de périmètre Hello récupère les ressources hello directement à partir de l’origine de hello et lui transmet demandeur toohello avec chaque demande.</span><span class="sxs-lookup"><span data-stu-id="09672-116">hello edge node retrieves hello asset directly from hello origin and passes it toohello requestor with each request.</span></span>
* <span data-ttu-id="09672-117">**Mettre en cache chaque URL unique** : ce mode traite chaque demande avec une chaîne de requête comme élément multimédia unique avec son propre cache.</span><span class="sxs-lookup"><span data-stu-id="09672-117">**Cache every unique URL**:  This mode treats each request with a query string as a unique asset with its own cache.</span></span>  <span data-ttu-id="09672-118">Par exemple, hello origine hello pour une demande de réponse *foo.ashx?q=bar* seraient mis en cache dans le nœud de périmètre hello et retourné pour les caches suivantes avec cette même chaîne de requête.</span><span class="sxs-lookup"><span data-stu-id="09672-118">For example, hello response from hello origin for a request for *foo.ashx?q=bar* would be cached at hello edge node and returned for subsequent caches with that same query string.</span></span>  <span data-ttu-id="09672-119">Une demande de *foo.ashx?q=somethingelse* mise en cache comme un actif distinct avec sa propre toolive le temps.</span><span class="sxs-lookup"><span data-stu-id="09672-119">A request for *foo.ashx?q=somethingelse* would be cached as a separate asset with its own time toolive.</span></span>

## <a name="changing-query-string-caching-settings-for-standard-cdn-profiles"></a><span data-ttu-id="09672-120">Modification des paramètres de mise en cache des chaînes de requête pour les profils CDN Standard</span><span class="sxs-lookup"><span data-stu-id="09672-120">Changing query string caching settings for standard CDN profiles</span></span>
1. <span data-ttu-id="09672-121">À partir du Panneau de profil CDN hello, cliquez sur le point de terminaison CDN hello toomanage vous le souhaitez.</span><span class="sxs-lookup"><span data-stu-id="09672-121">From hello CDN profile blade, click hello CDN endpoint you wish toomanage.</span></span>
   
    ![Points de terminaison du panneau de profil CDN](./media/cdn-query-string/cdn-endpoints.png)
   
    <span data-ttu-id="09672-123">Panneau de point de terminaison CDN Hello s’ouvre.</span><span class="sxs-lookup"><span data-stu-id="09672-123">hello CDN endpoint blade opens.</span></span>
2. <span data-ttu-id="09672-124">Cliquez sur hello **configurer** bouton.</span><span class="sxs-lookup"><span data-stu-id="09672-124">Click hello **Configure** button.</span></span>
   
    ![Bouton de gestion du panneau de profil CDN](./media/cdn-query-string/cdn-config-btn.png)
   
    <span data-ttu-id="09672-126">Panneau de Configuration CDN Hello s’ouvre.</span><span class="sxs-lookup"><span data-stu-id="09672-126">hello CDN Configuration blade opens.</span></span>
3. <span data-ttu-id="09672-127">Sélectionnez un paramètre de hello **comportement de mise en cache de chaîne de requête** liste déroulante.</span><span class="sxs-lookup"><span data-stu-id="09672-127">Select a setting from hello **Query string caching behavior** dropdown.</span></span>
   
    ![Options de mise en cache des chaînes de requête CDN](./media/cdn-query-string/cdn-query-string.png)
4. <span data-ttu-id="09672-129">Après avoir effectué votre sélection, cliquez sur hello **enregistrer** bouton.</span><span class="sxs-lookup"><span data-stu-id="09672-129">After making your selection, click hello **Save** button.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="09672-130">modifications apportées aux paramètres de Hello n’est peut-être pas immédiatement visible, comme le temps requis pour toopropagate d’inscription hello via hello CDN.</span><span class="sxs-lookup"><span data-stu-id="09672-130">hello settings changes may not be immediately visible, as it takes time for hello registration toopropagate through hello CDN.</span></span>  <span data-ttu-id="09672-131">Pour <b>Azure CDN fourni par Akamai</b> , la propagation s’effectue généralement dans un délai d’une minute.</span><span class="sxs-lookup"><span data-stu-id="09672-131">For <b>Azure CDN from Akamai</b> profiles, propagation will usually complete within one minute.</span></span>  <span data-ttu-id="09672-132">Pour les profils du <b>CDN Azure fourni par Verizon</b>, la propagation s’effectue généralement dans un délai de 90 minutes, mais elle peut prendre plus de temps dans certains cas.</span><span class="sxs-lookup"><span data-stu-id="09672-132">For <b>Azure CDN from Verizon</b> profiles, propagation will usually complete within 90 minutes, but in some cases can take longer.</span></span>
> 
> 

