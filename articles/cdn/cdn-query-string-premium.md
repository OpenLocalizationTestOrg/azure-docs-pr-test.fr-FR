---
title: "aaaControl comportement de mise en cache CDN Azure avec les chaînes de requête - Premium | Documents Microsoft"
description: "Chaîne de requête Azure CDN mise en cache des contrôles de façon dont les fichiers sont toobe mis en cache s’ils contiennent des chaînes de requête."
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
ms.openlocfilehash: 5c97cf0230ae13fd378bfce49481f3135a5ef101
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="control-azure-cdn-caching-behavior-with-query-strings---premium"></a><span data-ttu-id="3c2eb-103">Contrôle du comportement de mise en cache du CDN Azure avec des chaînes de requête - Premium</span><span class="sxs-lookup"><span data-stu-id="3c2eb-103">Control Azure CDN caching behavior with query strings - Premium</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="3c2eb-104">Standard</span><span class="sxs-lookup"><span data-stu-id="3c2eb-104">Standard</span></span>](cdn-query-string.md)
> * [<span data-ttu-id="3c2eb-105">CDN Azure Premium fourni par Verizon</span><span class="sxs-lookup"><span data-stu-id="3c2eb-105">Azure CDN Premium from Verizon</span></span>](cdn-query-string-premium.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="3c2eb-106">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="3c2eb-106">Overview</span></span>
<span data-ttu-id="3c2eb-107">Chaîne de requête mise en cache des contrôles de façon dont les fichiers sont toobe mis en cache s’ils contiennent des chaînes de requête.</span><span class="sxs-lookup"><span data-stu-id="3c2eb-107">Query string caching controls how files are toobe cached when they contain query strings.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3c2eb-108">produits Standard et Premium CDN Hello fournissent hello même fonctionnalité de mise en cache de chaîne de requête, mais diffère de l’interface utilisateur de hello.</span><span class="sxs-lookup"><span data-stu-id="3c2eb-108">hello Standard and Premium CDN products provide hello same query string caching functionality, but hello user interface differs.</span></span>  <span data-ttu-id="3c2eb-109">Ce document décrit l’interface hello pour **Azure CDN Premium de Verizon**.</span><span class="sxs-lookup"><span data-stu-id="3c2eb-109">This document describes hello interface for **Azure CDN Premium from Verizon**.</span></span>  <span data-ttu-id="3c2eb-110">Pour la mise en cache des chaînes de requête avec le **CDN Azure Standard fourni par Akamai** et le **CDN Azure Standard fourni par Verizon**, consultez [Contrôle du comportement de mise en cache des demandes CDN avec des chaînes de requête](cdn-query-string.md).</span><span class="sxs-lookup"><span data-stu-id="3c2eb-110">For query string caching with **Azure CDN Standard from Akamai** and **Azure CDN Standard from Verizon**, see [Controlling caching behavior of CDN requests with query strings](cdn-query-string.md).</span></span>
> 
> 

<span data-ttu-id="3c2eb-111">Trois modes sont disponibles :</span><span class="sxs-lookup"><span data-stu-id="3c2eb-111">Three modes are available:</span></span>

* <span data-ttu-id="3c2eb-112">**standard-cache**: c’est le mode par défaut hello.</span><span class="sxs-lookup"><span data-stu-id="3c2eb-112">**standard-cache**:  This is hello default mode.</span></span>  <span data-ttu-id="3c2eb-113">nœud de périmètre CDN Hello passera la chaîne de requête hello à partir de l’origine de toohello hello demandeur sur la première demande de hello et asset hello de cache.</span><span class="sxs-lookup"><span data-stu-id="3c2eb-113">hello CDN edge node will pass hello query string from hello requestor toohello origin on hello first request and cache hello asset.</span></span>  <span data-ttu-id="3c2eb-114">Toutes les demandes ultérieures pour cet élément multimédia qui sont pris en charge à partir du nœud de périmètre hello ignore la chaîne de requête hello jusqu'à ce que les ressources mises en cache hello expire.</span><span class="sxs-lookup"><span data-stu-id="3c2eb-114">All subsequent requests for that asset that are served from hello edge node will ignore hello query string until hello cached asset expires.</span></span>
* <span data-ttu-id="3c2eb-115">**Aucun cache**: dans ce mode, les demandes de chaînes de requête ne sont pas mis en cache au niveau du nœud de périmètre CDN hello.</span><span class="sxs-lookup"><span data-stu-id="3c2eb-115">**no-cache**:  In this mode, requests with query strings are not cached at hello CDN edge node.</span></span>  <span data-ttu-id="3c2eb-116">nœud de périmètre Hello récupère les ressources hello directement à partir de l’origine de hello et lui transmet demandeur toohello avec chaque demande.</span><span class="sxs-lookup"><span data-stu-id="3c2eb-116">hello edge node retrieves hello asset directly from hello origin and passes it toohello requestor with each request.</span></span>
* <span data-ttu-id="3c2eb-117">**unique-cache** : ce mode traite chaque demande avec une chaîne de requête comme élément multimédia unique avec son propre cache.</span><span class="sxs-lookup"><span data-stu-id="3c2eb-117">**unique-cache**:  This mode treats each request with a query string as a unique asset with its own cache.</span></span>  <span data-ttu-id="3c2eb-118">Par exemple, hello origine hello pour une demande de réponse *foo.ashx?q=bar* seraient mis en cache dans le nœud de périmètre hello et retourné pour les caches suivantes avec cette même chaîne de requête.</span><span class="sxs-lookup"><span data-stu-id="3c2eb-118">For example, hello response from hello origin for a request for *foo.ashx?q=bar* would be cached at hello edge node and returned for subsequent caches with that same query string.</span></span>  <span data-ttu-id="3c2eb-119">Une demande de *foo.ashx?q=somethingelse* mise en cache comme un actif distinct avec sa propre toolive le temps.</span><span class="sxs-lookup"><span data-stu-id="3c2eb-119">A request for *foo.ashx?q=somethingelse* would be cached as a separate asset with its own time toolive.</span></span>

## <a name="changing-query-string-caching-settings-for-premium-cdn-profiles"></a><span data-ttu-id="3c2eb-120">Modification des paramètres de mise en cache des chaînes de requête pour les profils CDN Premium</span><span class="sxs-lookup"><span data-stu-id="3c2eb-120">Changing query string caching settings for premium CDN profiles</span></span>
1. <span data-ttu-id="3c2eb-121">À partir du Panneau de profil hello CDN, cliquez sur hello **gérer** bouton.</span><span class="sxs-lookup"><span data-stu-id="3c2eb-121">From hello CDN profile blade, click hello **Manage** button.</span></span>
   
    ![Bouton de gestion du panneau de profil CDN](./media/cdn-query-string-premium/cdn-manage-btn.png)
   
    <span data-ttu-id="3c2eb-123">portail de gestion CDN Hello s’ouvre.</span><span class="sxs-lookup"><span data-stu-id="3c2eb-123">hello CDN management portal opens.</span></span>
2. <span data-ttu-id="3c2eb-124">Pointage hello **grand HTTP** tab, puis pointez sur hello **paramètres de Cache** menu volant.</span><span class="sxs-lookup"><span data-stu-id="3c2eb-124">Hover over hello **HTTP Large** tab, then hover over hello **Cache Settings** flyout.</span></span>  <span data-ttu-id="3c2eb-125">Cliquez sur **Mise en cache des chaînes de requête**.</span><span class="sxs-lookup"><span data-stu-id="3c2eb-125">Click on **Query-String Caching**.</span></span>
   
    <span data-ttu-id="3c2eb-126">Les options de mise en cache des chaînes de requête s'affichent.</span><span class="sxs-lookup"><span data-stu-id="3c2eb-126">Query string caching options are displayed.</span></span>
   
    ![Options de mise en cache des chaînes de requête CDN](./media/cdn-query-string-premium/cdn-query-string.png)
3. <span data-ttu-id="3c2eb-128">Après avoir effectué votre sélection, cliquez sur hello **mise à jour** bouton.</span><span class="sxs-lookup"><span data-stu-id="3c2eb-128">After making your selection, click hello **Update** button.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3c2eb-129">modifications apportées aux paramètres de Hello n’est peut-être pas immédiatement visible, comme le temps requis pour toopropagate d’inscription hello via hello CDN.</span><span class="sxs-lookup"><span data-stu-id="3c2eb-129">hello settings changes may not be immediately visible, as it takes time for hello registration toopropagate through hello CDN.</span></span>  <span data-ttu-id="3c2eb-130">Pour les profils du <b>CDN Azure fourni par Verizon</b>, la propagation s’effectue généralement dans un délai de 90 minutes, mais elle peut prendre plus de temps dans certains cas.</span><span class="sxs-lookup"><span data-stu-id="3c2eb-130">For <b>Azure CDN from Verizon</b> profiles, propagation will usually complete within 90 minutes, but in some cases can take longer.</span></span>
> 
> 

