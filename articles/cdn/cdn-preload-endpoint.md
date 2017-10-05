---
title: "Préchargement d’éléments multimédias sur un point de terminaison CDN Azure | Microsoft Docs"
description: "Découvrez comment précharger du contenu mis en cache sur un point de terminaison CDN Azure."
services: cdn
documentationcenter: 
author: smcevoy
manager: erikre
editor: 
ms.assetid: 5ea3eba5-1335-413e-9af3-3918ce608a83
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: 1f2dcd9a91bb6e883cbef06373c1acd98bf8d45f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="pre-load-assets-on-an-azure-cdn-endpoint"></a><span data-ttu-id="e784b-103">Préchargement d’éléments multimédias sur un point de terminaison CDN Azure</span><span class="sxs-lookup"><span data-stu-id="e784b-103">Pre-load assets on an Azure CDN endpoint</span></span>
[!INCLUDE [cdn-verizon-only](../../includes/cdn-verizon-only.md)]

<span data-ttu-id="e784b-104">Par défaut, les éléments sont d'abord mis en cache lorsqu'ils sont demandés.</span><span class="sxs-lookup"><span data-stu-id="e784b-104">By default, assets are first cached as they are requested.</span></span> <span data-ttu-id="e784b-105">Cela signifie que la première requête de chaque région peut prendre plus de temps puisque le contenu des serveurs Edge ne sera pas mis en cache et que vous devrez transmettre la requête au serveur d'origine.</span><span class="sxs-lookup"><span data-stu-id="e784b-105">This means that the first request from each region may take longer, since the edge servers will not have the content cached and will need to forward the request to the origin server.</span></span> <span data-ttu-id="e784b-106">Le préchargement du contenu permet d'éviter cette latence à la première occurrence.</span><span class="sxs-lookup"><span data-stu-id="e784b-106">Pre-loading content avoids this first hit latency.</span></span>

<span data-ttu-id="e784b-107">En plus d’offrir une meilleure expérience client, le préchargement de vos ressources mises en cache peut également réduire le trafic réseau sur le serveur d'origine.</span><span class="sxs-lookup"><span data-stu-id="e784b-107">In addition to providing a better customer experience, pre-loading your cached assets can also reduce network traffic on the origin server.</span></span>

> [!NOTE]
> <span data-ttu-id="e784b-108">Le préchargement des ressources est utile lors de grands événements ou lorsque le contenu est disponible simultanément pour un grand nombre d’utilisateurs, par exemple lors de la sortie d’un film ou d’une mise à jour logicielle.</span><span class="sxs-lookup"><span data-stu-id="e784b-108">Pre-loading assets is useful for  large events or content that becomes simultaneously available to a large number of users, such as a new movie release or a software update.</span></span>
> 
> 

<span data-ttu-id="e784b-109">Ce didacticiel vous guide tout au long du préchargement de contenu mis en cache sur tous les nœuds de périphérie CDN Azure.</span><span class="sxs-lookup"><span data-stu-id="e784b-109">This tutorial walks you through pre-loading cached content on all Azure CDN edge nodes.</span></span>

## <a name="walkthrough"></a><span data-ttu-id="e784b-110">Procédure pas à pas</span><span class="sxs-lookup"><span data-stu-id="e784b-110">Walkthrough</span></span>
1. <span data-ttu-id="e784b-111">Dans le [portail Azure](https://portal.azure.com), recherchez le profil CDN qui contient le point de terminaison que vous souhaitez précharger.</span><span class="sxs-lookup"><span data-stu-id="e784b-111">In the [Azure Portal](https://portal.azure.com), browse to the CDN profile containing the endpoint you wish to pre-load.</span></span>  <span data-ttu-id="e784b-112">Le panneau Profil s’ouvre.</span><span class="sxs-lookup"><span data-stu-id="e784b-112">The profile blade opens.</span></span>
2. <span data-ttu-id="e784b-113">Cliquez sur le point de terminaison dans la liste.</span><span class="sxs-lookup"><span data-stu-id="e784b-113">Click the endpoint in the list.</span></span>  <span data-ttu-id="e784b-114">Le panneau du point de terminaison s’ouvre.</span><span class="sxs-lookup"><span data-stu-id="e784b-114">The endpoint blade opens.</span></span>
3. <span data-ttu-id="e784b-115">Dans le panneau du point de terminaison CDN, cliquez sur le bouton Charger.</span><span class="sxs-lookup"><span data-stu-id="e784b-115">From the CDN endpoint blade, click the load button.</span></span>
   
    ![Panneau du point de terminaison CDN](./media/cdn-preload-endpoint/cdn-endpoint-blade.png)
   
    <span data-ttu-id="e784b-117">Le panneau Charger s’ouvre.</span><span class="sxs-lookup"><span data-stu-id="e784b-117">The Load blade opens.</span></span>
   
    ![Panneau de chargement CDN](./media/cdn-preload-endpoint/cdn-load-blade.png)
4. <span data-ttu-id="e784b-119">Entrez le chemin complet de chaque élément multimédia que vous souhaitez charger (par exemple, `/pictures/kitten.png`) dans la zone de texte **Chemin d’accès** .</span><span class="sxs-lookup"><span data-stu-id="e784b-119">Enter the full path of each asset you wish to load (e.g., `/pictures/kitten.png`) in the **Path** textbox.</span></span>
   
   > [!TIP]
   > <span data-ttu-id="e784b-120">Après avoir saisi du texte, d’autres zones de texte **Chemin d’accès** s’afficheront pour vous permettre de créer une liste de plusieurs éléments multimédias.</span><span class="sxs-lookup"><span data-stu-id="e784b-120">More **Path** textboxes will appear after you enter text to allow you to build a list of multiple assets.</span></span>  <span data-ttu-id="e784b-121">Vous pouvez supprimer des éléments multimédias de la liste en cliquant sur le bouton points de suspension (...).</span><span class="sxs-lookup"><span data-stu-id="e784b-121">You can delete assets from the list by clicking the ellipsis (...) button.</span></span>
   > 
   > <span data-ttu-id="e784b-122">Les chemins d’accès doivent être une URL relative qui satisfait à [l’expression régulière](https://msdn.microsoft.com/library/az24scfc.aspx) suivante :</span><span class="sxs-lookup"><span data-stu-id="e784b-122">Paths must be a relative URL that fits the following [regular expression](https://msdn.microsoft.com/library/az24scfc.aspx):</span></span>  
   > ><span data-ttu-id="e784b-123">Chargement d’un fichier unique `@"^(?:\/[a-zA-Z0-9-_.%=\u0020]+)+$"`;</span><span class="sxs-lookup"><span data-stu-id="e784b-123">Load a single file path `@"^(?:\/[a-zA-Z0-9-_.%=\u0020]+)+$"`;</span></span>  
   > ><span data-ttu-id="e784b-124">Chargement d’un fichier unique avec chaîne de requête `@"^(?:\?[-_a-zA-Z0-9\/%:;=!,.\+'&\u0020]*)?$";`</span><span class="sxs-lookup"><span data-stu-id="e784b-124">Load a single file with query string `@"^(?:\?[-_a-zA-Z0-9\/%:;=!,.\+'&\u0020]*)?$";`</span></span>  
   > 
   > <span data-ttu-id="e784b-125">Chaque élément multimédia doit avoir son propre chemin d’accès.</span><span class="sxs-lookup"><span data-stu-id="e784b-125">Each asset must have its own path.</span></span>  <span data-ttu-id="e784b-126">Il n’existe aucune fonctionnalité de caractère générique pour le préchargement d’éléments multimédias.</span><span class="sxs-lookup"><span data-stu-id="e784b-126">There is no wildcard functionality for pre-loading assets.</span></span>
   > 
   > 
   
    ![Bouton Charger](./media/cdn-preload-endpoint/cdn-load-paths.png)
5. <span data-ttu-id="e784b-128">Cliquez sur le bouton **Charger** .</span><span class="sxs-lookup"><span data-stu-id="e784b-128">Click the **Load** button.</span></span>
   
    ![Bouton Charger](./media/cdn-preload-endpoint/cdn-load-button.png)

> [!NOTE]
> <span data-ttu-id="e784b-130">Il existe une limite de 10 demandes de chargement par minute et par profil CDN.</span><span class="sxs-lookup"><span data-stu-id="e784b-130">There is a limitation of 10 load requests per minute per CDN profile.</span></span> <span data-ttu-id="e784b-131">50 chemins sont autorisés par demande.</span><span class="sxs-lookup"><span data-stu-id="e784b-131">50 paths are allowed per request.</span></span> <span data-ttu-id="e784b-132">Chaque chemin a une longueur limitée à 1 024 caractères.</span><span class="sxs-lookup"><span data-stu-id="e784b-132">Each path has a path-length limit of 1024 characters.</span></span>
> 
> 

## <a name="see-also"></a><span data-ttu-id="e784b-133">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="e784b-133">See also</span></span>
* [<span data-ttu-id="e784b-134">Purger un point de terminaison CDN Azure</span><span class="sxs-lookup"><span data-stu-id="e784b-134">Purge an Azure CDN endpoint</span></span>](cdn-purge-endpoint.md)
* [<span data-ttu-id="e784b-135">Référence API REST du CDN Azure - Vider ou pré-charger un point de terminaison</span><span class="sxs-lookup"><span data-stu-id="e784b-135">Azure CDN REST API reference - Purge or Pre-Load an Endpoint</span></span>](https://msdn.microsoft.com/library/mt634451.aspx)

