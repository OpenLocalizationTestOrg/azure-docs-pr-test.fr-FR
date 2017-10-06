---
title: aaaPre-chargement des ressources sur un point de terminaison CDN Azure | Documents Microsoft
description: "Découvrez comment toopre-charge mise en cache le contenu sur un point de terminaison CDN Azure."
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
ms.openlocfilehash: 08ac4b834f1ac8ce59d22e65fa8adea11bafcf17
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="pre-load-assets-on-an-azure-cdn-endpoint"></a><span data-ttu-id="bc3df-103">Préchargement d’éléments multimédias sur un point de terminaison CDN Azure</span><span class="sxs-lookup"><span data-stu-id="bc3df-103">Pre-load assets on an Azure CDN endpoint</span></span>
[!INCLUDE [cdn-verizon-only](../../includes/cdn-verizon-only.md)]

<span data-ttu-id="bc3df-104">Par défaut, les éléments sont d'abord mis en cache lorsqu'ils sont demandés.</span><span class="sxs-lookup"><span data-stu-id="bc3df-104">By default, assets are first cached as they are requested.</span></span> <span data-ttu-id="bc3df-105">Cela signifie que hello première requête de chaque région peut être plus longue, étant donné que les serveurs de périphérie hello n’aura pas le contenu hello mis en cache et devez serveur d’origine toohello tooforward hello demande.</span><span class="sxs-lookup"><span data-stu-id="bc3df-105">This means that hello first request from each region may take longer, since hello edge servers will not have hello content cached and will need tooforward hello request toohello origin server.</span></span> <span data-ttu-id="bc3df-106">Le préchargement du contenu permet d'éviter cette latence à la première occurrence.</span><span class="sxs-lookup"><span data-stu-id="bc3df-106">Pre-loading content avoids this first hit latency.</span></span>

<span data-ttu-id="bc3df-107">En outre tooproviding une meilleure expérience client, préchargement vos ressources mises en cache peut également réduire le trafic réseau sur le serveur d’origine hello.</span><span class="sxs-lookup"><span data-stu-id="bc3df-107">In addition tooproviding a better customer experience, pre-loading your cached assets can also reduce network traffic on hello origin server.</span></span>

> [!NOTE]
> <span data-ttu-id="bc3df-108">Préchargement des ressources est utile pour les événements de grande taille ou de contenu qui devient tooa accessibles simultanément un grand nombre d’utilisateurs, comme une nouvelle version de film ou d’une mise à jour logicielle.</span><span class="sxs-lookup"><span data-stu-id="bc3df-108">Pre-loading assets is useful for  large events or content that becomes simultaneously available tooa large number of users, such as a new movie release or a software update.</span></span>
> 
> 

<span data-ttu-id="bc3df-109">Ce didacticiel vous guide tout au long du préchargement de contenu mis en cache sur tous les nœuds de périphérie CDN Azure.</span><span class="sxs-lookup"><span data-stu-id="bc3df-109">This tutorial walks you through pre-loading cached content on all Azure CDN edge nodes.</span></span>

## <a name="walkthrough"></a><span data-ttu-id="bc3df-110">Procédure pas à pas</span><span class="sxs-lookup"><span data-stu-id="bc3df-110">Walkthrough</span></span>
1. <span data-ttu-id="bc3df-111">Bonjour [Azure Portal](https://portal.azure.com), parcourir le profil CDN toohello contenant hello de point de terminaison souhaité toopre en charge.</span><span class="sxs-lookup"><span data-stu-id="bc3df-111">In hello [Azure Portal](https://portal.azure.com), browse toohello CDN profile containing hello endpoint you wish toopre-load.</span></span>  <span data-ttu-id="bc3df-112">Panneau de profil Hello s’ouvre.</span><span class="sxs-lookup"><span data-stu-id="bc3df-112">hello profile blade opens.</span></span>
2. <span data-ttu-id="bc3df-113">Cliquez sur le point de terminaison hello dans la liste de hello.</span><span class="sxs-lookup"><span data-stu-id="bc3df-113">Click hello endpoint in hello list.</span></span>  <span data-ttu-id="bc3df-114">Panneau de point de terminaison Hello s’ouvre.</span><span class="sxs-lookup"><span data-stu-id="bc3df-114">hello endpoint blade opens.</span></span>
3. <span data-ttu-id="bc3df-115">À partir du Panneau de point de terminaison CDN hello, cliquez sur le bouton charger de hello.</span><span class="sxs-lookup"><span data-stu-id="bc3df-115">From hello CDN endpoint blade, click hello load button.</span></span>
   
    ![Panneau du point de terminaison CDN](./media/cdn-preload-endpoint/cdn-endpoint-blade.png)
   
    <span data-ttu-id="bc3df-117">Panneau de charge Hello s’ouvre.</span><span class="sxs-lookup"><span data-stu-id="bc3df-117">hello Load blade opens.</span></span>
   
    ![Panneau de chargement CDN](./media/cdn-preload-endpoint/cdn-load-blade.png)
4. <span data-ttu-id="bc3df-119">Entrez le chemin d’accès complet de hello de chaque élément multimédia, vous souhaitez tooload (par exemple, `/pictures/kitten.png`) Bonjour **chemin d’accès** zone de texte.</span><span class="sxs-lookup"><span data-stu-id="bc3df-119">Enter hello full path of each asset you wish tooload (e.g., `/pictures/kitten.png`) in hello **Path** textbox.</span></span>
   
   > [!TIP]
   > <span data-ttu-id="bc3df-120">Plus **chemin d’accès** zones de texte s’affiche après que vous entrez le texte tooallow toobuild une liste de plusieurs ressources.</span><span class="sxs-lookup"><span data-stu-id="bc3df-120">More **Path** textboxes will appear after you enter text tooallow you toobuild a list of multiple assets.</span></span>  <span data-ttu-id="bc3df-121">Vous pouvez supprimer des éléments multimédias à partir de la liste de hello en cliquant sur le bouton de sélection (...) hello.</span><span class="sxs-lookup"><span data-stu-id="bc3df-121">You can delete assets from hello list by clicking hello ellipsis (...) button.</span></span>
   > 
   > <span data-ttu-id="bc3df-122">Chemins d’accès doivent être une URL relative qui correspond à la suivante de hello [expression régulière](https://msdn.microsoft.com/library/az24scfc.aspx):</span><span class="sxs-lookup"><span data-stu-id="bc3df-122">Paths must be a relative URL that fits hello following [regular expression](https://msdn.microsoft.com/library/az24scfc.aspx):</span></span>  
   > ><span data-ttu-id="bc3df-123">Chargement d’un fichier unique `@"^(?:\/[a-zA-Z0-9-_.%=\u0020]+)+$"`;</span><span class="sxs-lookup"><span data-stu-id="bc3df-123">Load a single file path `@"^(?:\/[a-zA-Z0-9-_.%=\u0020]+)+$"`;</span></span>  
   > ><span data-ttu-id="bc3df-124">Chargement d’un fichier unique avec chaîne de requête `@"^(?:\?[-_a-zA-Z0-9\/%:;=!,.\+'&\u0020]*)?$";`</span><span class="sxs-lookup"><span data-stu-id="bc3df-124">Load a single file with query string `@"^(?:\?[-_a-zA-Z0-9\/%:;=!,.\+'&\u0020]*)?$";`</span></span>  
   > 
   > <span data-ttu-id="bc3df-125">Chaque élément multimédia doit avoir son propre chemin d’accès.</span><span class="sxs-lookup"><span data-stu-id="bc3df-125">Each asset must have its own path.</span></span>  <span data-ttu-id="bc3df-126">Il n’existe aucune fonctionnalité de caractère générique pour le préchargement d’éléments multimédias.</span><span class="sxs-lookup"><span data-stu-id="bc3df-126">There is no wildcard functionality for pre-loading assets.</span></span>
   > 
   > 
   
    ![Bouton Charger](./media/cdn-preload-endpoint/cdn-load-paths.png)
5. <span data-ttu-id="bc3df-128">Cliquez sur hello **charge** bouton.</span><span class="sxs-lookup"><span data-stu-id="bc3df-128">Click hello **Load** button.</span></span>
   
    ![Bouton Charger](./media/cdn-preload-endpoint/cdn-load-button.png)

> [!NOTE]
> <span data-ttu-id="bc3df-130">Il existe une limite de 10 demandes de chargement par minute et par profil CDN.</span><span class="sxs-lookup"><span data-stu-id="bc3df-130">There is a limitation of 10 load requests per minute per CDN profile.</span></span> <span data-ttu-id="bc3df-131">50 chemins sont autorisés par demande.</span><span class="sxs-lookup"><span data-stu-id="bc3df-131">50 paths are allowed per request.</span></span> <span data-ttu-id="bc3df-132">Chaque chemin a une longueur limitée à 1 024 caractères.</span><span class="sxs-lookup"><span data-stu-id="bc3df-132">Each path has a path-length limit of 1024 characters.</span></span>
> 
> 

## <a name="see-also"></a><span data-ttu-id="bc3df-133">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="bc3df-133">See also</span></span>
* [<span data-ttu-id="bc3df-134">Purger un point de terminaison CDN Azure</span><span class="sxs-lookup"><span data-stu-id="bc3df-134">Purge an Azure CDN endpoint</span></span>](cdn-purge-endpoint.md)
* [<span data-ttu-id="bc3df-135">Référence API REST du CDN Azure - Vider ou pré-charger un point de terminaison</span><span class="sxs-lookup"><span data-stu-id="bc3df-135">Azure CDN REST API reference - Purge or Pre-Load an Endpoint</span></span>](https://msdn.microsoft.com/library/mt634451.aspx)

