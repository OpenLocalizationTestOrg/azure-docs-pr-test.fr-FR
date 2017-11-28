---
title: aaaPurge un point de terminaison CDN Azure | Documents Microsoft
description: "Découvrez comment toopurge toutes les mises en cache contenu à partir d’un point de terminaison CDN Azure."
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: 0b50230b-fe82-4740-90aa-95d4dde8bd4f
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: a09f4a49aa1e2d7655ecae44b5126c11c28fd599
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="purge-an-azure-cdn-endpoint"></a><span data-ttu-id="5de5e-103">Purger un point de terminaison CDN Azure</span><span class="sxs-lookup"><span data-stu-id="5de5e-103">Purge an Azure CDN endpoint</span></span>
## <a name="overview"></a><span data-ttu-id="5de5e-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="5de5e-104">Overview</span></span>
<span data-ttu-id="5de5e-105">Noeuds CDN Azure mettra en cache les ressources jusqu'à ce que time-to-live (TTL) l’élément multimédia hello expire.</span><span class="sxs-lookup"><span data-stu-id="5de5e-105">Azure CDN edge nodes will cache assets until hello asset's time-to-live (TTL) expires.</span></span>  <span data-ttu-id="5de5e-106">Après expiration de durée de vie de l’élément multimédia hello, lorsqu’un client demande un élément multimédia de hello à partir du nœud de périmètre hello, nœud de périmètre hello récupère une copie mise à jour de demande du client hello asset tooserve hello et stocker hello l’actualisation du cache.</span><span class="sxs-lookup"><span data-stu-id="5de5e-106">After hello asset's TTL expires, when a client requests hello asset from hello edge node, hello edge node will retrieve a new updated copy of hello asset tooserve hello client request and store refresh hello cache.</span></span>

<span data-ttu-id="5de5e-107">toomake pratique Hello meilleures que vos utilisateurs obtiennent toujours copie la plus récente de vos ressources hello est tooversion actifs pour chaque mise à jour et les publier en tant que nouvelles URL.</span><span class="sxs-lookup"><span data-stu-id="5de5e-107">hello best practice toomake sure your users always obtain hello latest copy of your assets is tooversion your assets for each update and publish them as new URLs.</span></span>  <span data-ttu-id="5de5e-108">CDN récupère immédiatement les nouvelles ressources de hello pour les demandes de client suivants hello.</span><span class="sxs-lookup"><span data-stu-id="5de5e-108">CDN will immediately retrieve hello new assets for hello next client requests.</span></span>  <span data-ttu-id="5de5e-109">Vous souhaiterez parfois toopurge mis en cache le contenu à partir de tous les nœuds de bord et les forcer tous les composants mis à jour de tooretrieve de nouveau.</span><span class="sxs-lookup"><span data-stu-id="5de5e-109">Sometimes you may wish toopurge cached content from all edge nodes and force them all tooretrieve new updated assets.</span></span>  <span data-ttu-id="5de5e-110">Cela peut être dû à application web de tooyour tooupdates ou des ressources de mise à jour tooquickly qui contiennent des informations incorrectes.</span><span class="sxs-lookup"><span data-stu-id="5de5e-110">This might be due tooupdates tooyour web application, or tooquickly update assets that contain incorrect information.</span></span>

> [!TIP]
> <span data-ttu-id="5de5e-111">Notez que la purge efface uniquement hello mis en cache le contenu sur les serveurs de périmètre CDN hello.</span><span class="sxs-lookup"><span data-stu-id="5de5e-111">Note that purging only clears hello cached content on hello CDN edge servers.</span></span>  <span data-ttu-id="5de5e-112">Les caches en aval, tels que les serveurs proxy et les caches de navigateur local, peuvent contenir toujours une copie mise en cache du fichier de hello.</span><span class="sxs-lookup"><span data-stu-id="5de5e-112">Any downstream caches, such as proxy servers and local browser caches, may still hold a cached copy of hello file.</span></span>  <span data-ttu-id="5de5e-113">Il est important tooremember cela lorsque vous définissez un fichier durée de vie.</span><span class="sxs-lookup"><span data-stu-id="5de5e-113">It's important tooremember this when you set a file's time-to-live.</span></span>  <span data-ttu-id="5de5e-114">Vous pouvez forcer une client en aval toorequest hello version la plus récente de votre fichier en lui donnant un nom unique chaque fois que vous mettez à jour, ou en tirant parti des [mise en cache de la chaîne de requête](cdn-query-string.md).</span><span class="sxs-lookup"><span data-stu-id="5de5e-114">You can force a downstream client toorequest hello latest version of your file by giving it a unique name every time you update it, or by taking advantage of [query string caching](cdn-query-string.md).</span></span>  
> 
> 

<span data-ttu-id="5de5e-115">Ce didacticiel vous guide dans le processus de vidage des éléments multimédias de tous les nœuds d’un point de terminaison.</span><span class="sxs-lookup"><span data-stu-id="5de5e-115">This tutorial walks you through purging assets from all edge nodes of an endpoint.</span></span>

## <a name="walkthrough"></a><span data-ttu-id="5de5e-116">Procédure pas à pas</span><span class="sxs-lookup"><span data-stu-id="5de5e-116">Walkthrough</span></span>
1. <span data-ttu-id="5de5e-117">Bonjour [Azure Portal](https://portal.azure.com), recherchez le profil CDN toohello contenant le point de terminaison hello toopurge vous le souhaitez.</span><span class="sxs-lookup"><span data-stu-id="5de5e-117">In hello [Azure Portal](https://portal.azure.com), browse toohello CDN profile containing hello endpoint you wish toopurge.</span></span>
2. <span data-ttu-id="5de5e-118">À partir du Panneau de profil CDN hello, cliquez sur le bouton de purge hello.</span><span class="sxs-lookup"><span data-stu-id="5de5e-118">From hello CDN profile blade, click hello purge button.</span></span>
   
    ![Panneau du profil CDN](./media/cdn-purge-endpoint/cdn-profile-blade.png)
   
    <span data-ttu-id="5de5e-120">Panneau de Purge Hello s’ouvre.</span><span class="sxs-lookup"><span data-stu-id="5de5e-120">hello Purge blade opens.</span></span>
   
    ![Panneau de vidage CDN](./media/cdn-purge-endpoint/cdn-purge-blade.png)
3. <span data-ttu-id="5de5e-122">Sur hello purger panneau, sélectionnez hello service adresse toopurge à partir de la liste déroulante de hello URL.</span><span class="sxs-lookup"><span data-stu-id="5de5e-122">On hello Purge blade, select hello service address you wish toopurge from hello URL dropdown.</span></span>
   
    ![Formulaire de vidage](./media/cdn-purge-endpoint/cdn-purge-form.png)
   
   > [!NOTE]
   > <span data-ttu-id="5de5e-124">Vous pouvez également obtenir le panneau de Purge toohello en cliquant sur hello **purger** bouton sur le panneau de point de terminaison CDN hello.</span><span class="sxs-lookup"><span data-stu-id="5de5e-124">You can also get toohello Purge blade by clicking hello **Purge** button on hello CDN endpoint blade.</span></span>  <span data-ttu-id="5de5e-125">Dans ce cas, hello **URL** champ sera prérempli avec l’adresse du service hello de ce point de terminaison spécifique.</span><span class="sxs-lookup"><span data-stu-id="5de5e-125">In that case, hello **URL** field will be pre-populated with hello service address of that specific endpoint.</span></span>
   > 
   > 
4. <span data-ttu-id="5de5e-126">Sélectionnez les ressources toopurge de hello noeuds.</span><span class="sxs-lookup"><span data-stu-id="5de5e-126">Select what assets you wish toopurge from hello edge nodes.</span></span>  <span data-ttu-id="5de5e-127">Si vous le souhaitez tooclear tous les éléments multimédias, cliquez sur hello **effacera tous les** case à cocher.</span><span class="sxs-lookup"><span data-stu-id="5de5e-127">If you wish tooclear all assets, click hello **Purge all** checkbox.</span></span>  <span data-ttu-id="5de5e-128">Dans le cas contraire, chemin d’accès de type hello de chaque élément multimédia vous souhaitez toopurge Bonjour **chemin d’accès** zone de texte.</span><span class="sxs-lookup"><span data-stu-id="5de5e-128">Otherwise, type hello path of each asset you wish toopurge in hello **Path** textbox.</span></span> <span data-ttu-id="5de5e-129">Sous les formats sont pris en charge dans le chemin d’accès hello.</span><span class="sxs-lookup"><span data-stu-id="5de5e-129">Below formats are supported in hello path.</span></span>
    1. <span data-ttu-id="5de5e-130">**Purge d’URL unique**: immobilisation de Purge en spécifiant une URL complète hello, avec ou sans l’extension de fichier hello, par exemple,`/pictures/strasbourg.png`;`/pictures/strasbourg`</span><span class="sxs-lookup"><span data-stu-id="5de5e-130">**Single URL purge**: Purge individual asset by specifying hello full URL, with or without hello file extension, e.g.,`/pictures/strasbourg.png`; `/pictures/strasbourg`</span></span>
    2. <span data-ttu-id="5de5e-131">**Vidage de caractères génériques** : l’astérisque (\*) peut être utilisé comme caractère générique.</span><span class="sxs-lookup"><span data-stu-id="5de5e-131">**Wildcard purge**: Asterisk (\*) may be used as a wildcard.</span></span> <span data-ttu-id="5de5e-132">Purger tous les dossiers, sous-dossiers et fichiers sous un point de terminaison avec `/*` hello du chemin d’accès ou purger tous les sous-dossiers et fichiers dans un dossier spécifique en spécifiant le dossier hello suivie `/*`, par exemple,`/pictures/*`.</span><span class="sxs-lookup"><span data-stu-id="5de5e-132">Purge all folders, sub-folders and files under an endpoint with `/*` in hello path or purge all sub-folders and files under a specific folder by specifying hello folder followed by `/*`, e.g.,`/pictures/*`.</span></span>  <span data-ttu-id="5de5e-133">Notez que le vidage de caractère générique n’est pas compatible avec Azure CDN par Akamai.</span><span class="sxs-lookup"><span data-stu-id="5de5e-133">Note that wildcard purge is not supported by Azure CDN from Akamai currently.</span></span> 
    3. <span data-ttu-id="5de5e-134">**Vider le domaine racine**: racine hello de Purge du point de terminaison hello avec « / » dans le chemin d’accès hello.</span><span class="sxs-lookup"><span data-stu-id="5de5e-134">**Root domain purge**: Purge hello root of hello endpoint with "/" in hello path.</span></span>
   
   > [!TIP]
   > <span data-ttu-id="5de5e-135">Chemins d’accès doit être spécifiés pour purger et doit être une URL relative qui correspondent à des éléments suivants de hello [expression régulière](https://msdn.microsoft.com/library/az24scfc.aspx).</span><span class="sxs-lookup"><span data-stu-id="5de5e-135">Paths must be specified for purge and must be a relative URL that fit hello following [regular expression](https://msdn.microsoft.com/library/az24scfc.aspx).</span></span> <span data-ttu-id="5de5e-136">Le **vidage totale** et le **vidage de caractère générique** ne sont pas pris en charge par compatible avec **Azure CDN par Akamai**.</span><span class="sxs-lookup"><span data-stu-id="5de5e-136">**Purge all** and **Wildcard purge** not supported by **Azure CDN from Akamai** currently.</span></span>
   > > <span data-ttu-id="5de5e-137">Vidage d’URL unique `@"^\/(?>(?:[a-zA-Z0-9-_.%=\(\)\u0020]+\/?)*)$";`</span><span class="sxs-lookup"><span data-stu-id="5de5e-137">Single URL purge `@"^\/(?>(?:[a-zA-Z0-9-_.%=\(\)\u0020]+\/?)*)$";`</span></span>  
   > > <span data-ttu-id="5de5e-138">Chaîne de requête `@"^(?:\?[-\@_a-zA-Z0-9\/%:;=!,.\+'&\(\)\u0020]*)?$";`</span><span class="sxs-lookup"><span data-stu-id="5de5e-138">Query string `@"^(?:\?[-\@_a-zA-Z0-9\/%:;=!,.\+'&\(\)\u0020]*)?$";`</span></span>  
   > > <span data-ttu-id="5de5e-139">Vidage de caractère générique `@"^\/(?:[a-zA-Z0-9-_.%=\(\)\u0020]+\/)*\*$";`.</span><span class="sxs-lookup"><span data-stu-id="5de5e-139">Wildcard purge `@"^\/(?:[a-zA-Z0-9-_.%=\(\)\u0020]+\/)*\*$";`.</span></span> 
   > 
   > <span data-ttu-id="5de5e-140">Plus **chemin d’accès** zones de texte s’affiche après que vous entrez le texte tooallow toobuild une liste de plusieurs ressources.</span><span class="sxs-lookup"><span data-stu-id="5de5e-140">More **Path** textboxes will appear after you enter text tooallow you toobuild a list of multiple assets.</span></span>  <span data-ttu-id="5de5e-141">Vous pouvez supprimer des éléments multimédias à partir de la liste de hello en cliquant sur le bouton de sélection (...) hello.</span><span class="sxs-lookup"><span data-stu-id="5de5e-141">You can delete assets from hello list by clicking hello ellipsis (...) button.</span></span>
   > 
5. <span data-ttu-id="5de5e-142">Cliquez sur hello **purger** bouton.</span><span class="sxs-lookup"><span data-stu-id="5de5e-142">Click hello **Purge** button.</span></span>
   
    ![Bouton Vider](./media/cdn-purge-endpoint/cdn-purge-button.png)

> [!IMPORTANT]
> <span data-ttu-id="5de5e-144">Vider les demandes de prendre environ 2 à 3 minutes tooprocess avec **Azure CDN de Verizon** (Standard ou Premium) et environ 7 minutes avec **CDN Azure à partir d’Akamai**.</span><span class="sxs-lookup"><span data-stu-id="5de5e-144">Purge requests take approximately 2-3 minutes tooprocess with **Azure CDN from Verizon** (Standard and Premium), and approximately 7 minutes with **Azure CDN from Akamai**.</span></span>  <span data-ttu-id="5de5e-145">Le CDN Azure impose une limite de 50 demandes de vidage simultanées à un moment donné.</span><span class="sxs-lookup"><span data-stu-id="5de5e-145">Azure CDN has a limit of 50 concurrent purge requests at any given time.</span></span> 
> 
> 

## <a name="see-also"></a><span data-ttu-id="5de5e-146">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="5de5e-146">See also</span></span>
* [<span data-ttu-id="5de5e-147">Préchargement d’éléments multimédias sur un point de terminaison CDN Azure</span><span class="sxs-lookup"><span data-stu-id="5de5e-147">Pre-load assets on an Azure CDN endpoint</span></span>](cdn-preload-endpoint.md)
* [<span data-ttu-id="5de5e-148">Référence API REST du CDN Azure - Vider ou pré-charger un point de terminaison</span><span class="sxs-lookup"><span data-stu-id="5de5e-148">Azure CDN REST API reference - Purge or Pre-Load an Endpoint</span></span>](https://msdn.microsoft.com/library/mt634451.aspx)

