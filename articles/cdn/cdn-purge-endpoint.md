---
title: "Purger un point de terminaison CDN Azure | Microsoft Docs"
description: "Découvrez comment vider tout le contenu mis en cache à partir d’un point de terminaison CDN Azure."
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
ms.openlocfilehash: b035c232bb58d653960190d4974cc3789d55a51d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="purge-an-azure-cdn-endpoint"></a><span data-ttu-id="38d16-103">Purger un point de terminaison CDN Azure</span><span class="sxs-lookup"><span data-stu-id="38d16-103">Purge an Azure CDN endpoint</span></span>
## <a name="overview"></a><span data-ttu-id="38d16-104">Vue d’ensemble</span><span class="sxs-lookup"><span data-stu-id="38d16-104">Overview</span></span>
<span data-ttu-id="38d16-105">Les nœuds de périmètre CDN Azure mettent en cache les éléments multimédias jusqu’à l’expiration de leur durée de vie.</span><span class="sxs-lookup"><span data-stu-id="38d16-105">Azure CDN edge nodes will cache assets until the asset's time-to-live (TTL) expires.</span></span>  <span data-ttu-id="38d16-106">Une fois la durée de vie de l’élément multimédia expirée, lorsqu’un client demande l’élément multimédia à partir du nœud de périmètre, ce dernier récupère une nouvelle copie mise à jour de l’élément pour répondre à la demande du client et actualiser le cache.</span><span class="sxs-lookup"><span data-stu-id="38d16-106">After the asset's TTL expires, when a client requests the asset from the edge node, the edge node will retrieve a new updated copy of the asset to serve the client request and store refresh the cache.</span></span>

<span data-ttu-id="38d16-107">La bonne pratique pour vous assurer que vos utilisateurs obtiennent toujours la dernière copie de vos éléments multimédia consiste à établir une version de vos ressources pour chaque mise à jour et à les publier en tant que nouvelles URL.</span><span class="sxs-lookup"><span data-stu-id="38d16-107">The best practice to make sure your users always obtain the latest copy of your assets is to version your assets for each update and publish them as new URLs.</span></span>  <span data-ttu-id="38d16-108">CDN récupère immédiatement les nouveaux éléments multimédia pour les demandes suivantes du client.</span><span class="sxs-lookup"><span data-stu-id="38d16-108">CDN will immediately retrieve the new assets for the next client requests.</span></span>  <span data-ttu-id="38d16-109">Il est parfois souhaitable de vider le contenu mis en cache sur tous les nœuds de périmètre et de tous les forcer à récupérer de nouveaux éléments multimédias mis à jour.</span><span class="sxs-lookup"><span data-stu-id="38d16-109">Sometimes you may wish to purge cached content from all edge nodes and force them all to retrieve new updated assets.</span></span>  <span data-ttu-id="38d16-110">Ce besoin peut être dû à des mises à jour de votre application web, ou à la nécessité de mettre à jour rapidement les éléments multimédias qui contiennent des informations incorrectes.</span><span class="sxs-lookup"><span data-stu-id="38d16-110">This might be due to updates to your web application, or to quickly update assets that contain incorrect information.</span></span>

> [!TIP]
> <span data-ttu-id="38d16-111">Notez que le vidage efface uniquement le contenu mis en cache sur les serveurs de périmètre CDN.</span><span class="sxs-lookup"><span data-stu-id="38d16-111">Note that purging only clears the cached content on the CDN edge servers.</span></span>  <span data-ttu-id="38d16-112">Les caches en aval, tels que les serveurs proxy et les caches de navigateurs locaux, peuvent toujours contenir une copie mise en cache du fichier.</span><span class="sxs-lookup"><span data-stu-id="38d16-112">Any downstream caches, such as proxy servers and local browser caches, may still hold a cached copy of the file.</span></span>  <span data-ttu-id="38d16-113">Il est important de s’en rappeler au moment où vous définissez la durée de vie d’un fichier.</span><span class="sxs-lookup"><span data-stu-id="38d16-113">It's important to remember this when you set a file's time-to-live.</span></span>  <span data-ttu-id="38d16-114">Vous pouvez forcer un client en aval à demander la dernière version de votre fichier en lui donnant un nom unique chaque fois que vous le mettez à jour ou en tirant parti de la [mise en cache de chaîne de requête](cdn-query-string.md).</span><span class="sxs-lookup"><span data-stu-id="38d16-114">You can force a downstream client to request the latest version of your file by giving it a unique name every time you update it, or by taking advantage of [query string caching](cdn-query-string.md).</span></span>  
> 
> 

<span data-ttu-id="38d16-115">Ce didacticiel vous guide dans le processus de vidage des éléments multimédias de tous les nœuds d’un point de terminaison.</span><span class="sxs-lookup"><span data-stu-id="38d16-115">This tutorial walks you through purging assets from all edge nodes of an endpoint.</span></span>

## <a name="walkthrough"></a><span data-ttu-id="38d16-116">Procédure pas à pas</span><span class="sxs-lookup"><span data-stu-id="38d16-116">Walkthrough</span></span>
1. <span data-ttu-id="38d16-117">Dans le [portail Azure](https://portal.azure.com), recherchez le profil CDN qui contient le point de terminaison que vous souhaitez vider.</span><span class="sxs-lookup"><span data-stu-id="38d16-117">In the [Azure Portal](https://portal.azure.com), browse to the CDN profile containing the endpoint you wish to purge.</span></span>
2. <span data-ttu-id="38d16-118">Dans le panneau du profil CDN, cliquez sur le bouton de vidage.</span><span class="sxs-lookup"><span data-stu-id="38d16-118">From the CDN profile blade, click the purge button.</span></span>
   
    ![Panneau du profil CDN](./media/cdn-purge-endpoint/cdn-profile-blade.png)
   
    <span data-ttu-id="38d16-120">Le panneau correspondant s’ouvre.</span><span class="sxs-lookup"><span data-stu-id="38d16-120">The Purge blade opens.</span></span>
   
    ![Panneau de vidage CDN](./media/cdn-purge-endpoint/cdn-purge-blade.png)
3. <span data-ttu-id="38d16-122">Dans le panneau de vidage, sélectionnez l’adresse de service que vous souhaitez vider dans la liste déroulante des URL.</span><span class="sxs-lookup"><span data-stu-id="38d16-122">On the Purge blade, select the service address you wish to purge from the URL dropdown.</span></span>
   
    ![Formulaire de vidage](./media/cdn-purge-endpoint/cdn-purge-form.png)
   
   > [!NOTE]
   > <span data-ttu-id="38d16-124">Vous pouvez également accéder au panneau de vidage en cliquant sur le bouton **Vider** dans le panneau des points de terminaison CDN.</span><span class="sxs-lookup"><span data-stu-id="38d16-124">You can also get to the Purge blade by clicking the **Purge** button on the CDN endpoint blade.</span></span>  <span data-ttu-id="38d16-125">Dans ce cas, le champ **URL** sera déjà renseigné avec l’adresse de service de ce point de terminaison spécifique.</span><span class="sxs-lookup"><span data-stu-id="38d16-125">In that case, the **URL** field will be pre-populated with the service address of that specific endpoint.</span></span>
   > 
   > 
4. <span data-ttu-id="38d16-126">Sélectionnez les éléments multimédias que vous souhaitez vider sur les nœuds de périmètre.</span><span class="sxs-lookup"><span data-stu-id="38d16-126">Select what assets you wish to purge from the edge nodes.</span></span>  <span data-ttu-id="38d16-127">Si vous souhaitez effacer tous les éléments multimédias, cochez la case **Vider tout** .</span><span class="sxs-lookup"><span data-stu-id="38d16-127">If you wish to clear all assets, click the **Purge all** checkbox.</span></span>  <span data-ttu-id="38d16-128">Sinon, tapez le chemin de chaque élément multimédia que vous souhaitez vider dans la zone de texte **Chemin d’accès**.</span><span class="sxs-lookup"><span data-stu-id="38d16-128">Otherwise, type the path of each asset you wish to purge in the **Path** textbox.</span></span> <span data-ttu-id="38d16-129">Les formats suivants sont pris en charge dans le chemin d’accès.</span><span class="sxs-lookup"><span data-stu-id="38d16-129">Below formats are supported in the path.</span></span>
    1. <span data-ttu-id="38d16-130">**Vidage d’URL unique** : vidage d’un élément multimédia individuel en spécifiant l’URL complète, avec ou sans l’extension de fichier, par exemple,`/pictures/strasbourg.png` ; `/pictures/strasbourg`</span><span class="sxs-lookup"><span data-stu-id="38d16-130">**Single URL purge**: Purge individual asset by specifying the full URL, with or without the file extension, e.g.,`/pictures/strasbourg.png`; `/pictures/strasbourg`</span></span>
    2. <span data-ttu-id="38d16-131">**Vidage de caractères génériques** : l’astérisque (\*) peut être utilisé comme caractère générique.</span><span class="sxs-lookup"><span data-stu-id="38d16-131">**Wildcard purge**: Asterisk (\*) may be used as a wildcard.</span></span> <span data-ttu-id="38d16-132">Videz tous les dossiers, sous-dossiers et fichiers dans un point de terminaison avec `/*` dans le chemin d’accès ou videz tous les sous-dossiers et fichiers dans un dossier spécifique en spécifiant le dossier suivi de `/*`, par exemple,`/pictures/*`.</span><span class="sxs-lookup"><span data-stu-id="38d16-132">Purge all folders, sub-folders and files under an endpoint with `/*` in the path or purge all sub-folders and files under a specific folder by specifying the folder followed by `/*`, e.g.,`/pictures/*`.</span></span>  <span data-ttu-id="38d16-133">Notez que le vidage de caractère générique n’est pas compatible avec Azure CDN par Akamai.</span><span class="sxs-lookup"><span data-stu-id="38d16-133">Note that wildcard purge is not supported by Azure CDN from Akamai currently.</span></span> 
    3. <span data-ttu-id="38d16-134">**Vidage du domaine racine** : videz la racine du point de terminaison avec « / » dans le chemin d’accès.</span><span class="sxs-lookup"><span data-stu-id="38d16-134">**Root domain purge**: Purge the root of the endpoint with "/" in the path.</span></span>
   
   > [!TIP]
   > <span data-ttu-id="38d16-135">Les chemins doivent être spécifiés pour le vidage et doivent être une URL relative qui satisfait à [l’expression régulière](https://msdn.microsoft.com/library/az24scfc.aspx) suivante.</span><span class="sxs-lookup"><span data-stu-id="38d16-135">Paths must be specified for purge and must be a relative URL that fit the following [regular expression](https://msdn.microsoft.com/library/az24scfc.aspx).</span></span> <span data-ttu-id="38d16-136">Le **vidage totale** et le **vidage de caractère générique** ne sont pas pris en charge par compatible avec **Azure CDN par Akamai**.</span><span class="sxs-lookup"><span data-stu-id="38d16-136">**Purge all** and **Wildcard purge** not supported by **Azure CDN from Akamai** currently.</span></span>
   > > <span data-ttu-id="38d16-137">Vidage d’URL unique `@"^\/(?>(?:[a-zA-Z0-9-_.%=\(\)\u0020]+\/?)*)$";`</span><span class="sxs-lookup"><span data-stu-id="38d16-137">Single URL purge `@"^\/(?>(?:[a-zA-Z0-9-_.%=\(\)\u0020]+\/?)*)$";`</span></span>  
   > > <span data-ttu-id="38d16-138">Chaîne de requête `@"^(?:\?[-\@_a-zA-Z0-9\/%:;=!,.\+'&\(\)\u0020]*)?$";`</span><span class="sxs-lookup"><span data-stu-id="38d16-138">Query string `@"^(?:\?[-\@_a-zA-Z0-9\/%:;=!,.\+'&\(\)\u0020]*)?$";`</span></span>  
   > > <span data-ttu-id="38d16-139">Vidage de caractère générique `@"^\/(?:[a-zA-Z0-9-_.%=\(\)\u0020]+\/)*\*$";`.</span><span class="sxs-lookup"><span data-stu-id="38d16-139">Wildcard purge `@"^\/(?:[a-zA-Z0-9-_.%=\(\)\u0020]+\/)*\*$";`.</span></span> 
   > 
   > <span data-ttu-id="38d16-140">Après avoir saisi du texte, d’autres zones de texte **Chemin d’accès** s’afficheront pour vous permettre de créer une liste de plusieurs éléments multimédias.</span><span class="sxs-lookup"><span data-stu-id="38d16-140">More **Path** textboxes will appear after you enter text to allow you to build a list of multiple assets.</span></span>  <span data-ttu-id="38d16-141">Vous pouvez supprimer des éléments multimédias de la liste en cliquant sur le bouton points de suspension (...).</span><span class="sxs-lookup"><span data-stu-id="38d16-141">You can delete assets from the list by clicking the ellipsis (...) button.</span></span>
   > 
5. <span data-ttu-id="38d16-142">Cliquez sur le bouton **Vider** .</span><span class="sxs-lookup"><span data-stu-id="38d16-142">Click the **Purge** button.</span></span>
   
    ![Bouton Vider](./media/cdn-purge-endpoint/cdn-purge-button.png)

> [!IMPORTANT]
> <span data-ttu-id="38d16-144">Le traitement des demandes de vidage prend environ 2 à 3 minutes avec le **CDN Azure fourni par Verizon** (Standard et Premium) et environ 7 minutes avec le **CDN Azure fourni par Akamai**.</span><span class="sxs-lookup"><span data-stu-id="38d16-144">Purge requests take approximately 2-3 minutes to process with **Azure CDN from Verizon** (Standard and Premium), and approximately 7 minutes with **Azure CDN from Akamai**.</span></span>  <span data-ttu-id="38d16-145">Le CDN Azure impose une limite de 50 demandes de vidage simultanées à un moment donné.</span><span class="sxs-lookup"><span data-stu-id="38d16-145">Azure CDN has a limit of 50 concurrent purge requests at any given time.</span></span> 
> 
> 

## <a name="see-also"></a><span data-ttu-id="38d16-146">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="38d16-146">See also</span></span>
* [<span data-ttu-id="38d16-147">Préchargement d’éléments multimédias sur un point de terminaison CDN Azure</span><span class="sxs-lookup"><span data-stu-id="38d16-147">Pre-load assets on an Azure CDN endpoint</span></span>](cdn-preload-endpoint.md)
* [<span data-ttu-id="38d16-148">Référence API REST du CDN Azure - Vider ou pré-charger un point de terminaison</span><span class="sxs-lookup"><span data-stu-id="38d16-148">Azure CDN REST API reference - Purge or Pre-Load an Endpoint</span></span>](https://msdn.microsoft.com/library/mt634451.aspx)

