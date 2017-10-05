---
title: "Compression des fichiers dans Azure CDN pour améliorer les performances | Microsoft Docs"
description: "Découvrez comment améliorer la vitesse de transfert de fichiers et les performances de chargement de page en compressant vos fichiers dans Azure CDN."
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: af1cddff-78d8-476b-a9d0-8c2164e4de5d
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: 7546650e6096a880f4fb4d0c94dd4ecc00b70160
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="improve-performance-by-compressing-files-in-azure-cdn"></a><span data-ttu-id="4451b-103">Compression des fichiers dans Azure CDN pour améliorer les performances</span><span class="sxs-lookup"><span data-stu-id="4451b-103">Improve performance by compressing files in Azure CDN</span></span>
<span data-ttu-id="4451b-104">La compression est une méthode simple et efficace qui vise à améliorer la vitesse de transfert des fichiers et à accroître les performances de chargement des pages en réduisant la taille des fichiers avant leur envoi à partir du serveur.</span><span class="sxs-lookup"><span data-stu-id="4451b-104">Compression is a simple and effective method to improve file transfer speed and increase page load performance by reducing file size before it is sent from the server.</span></span> <span data-ttu-id="4451b-105">Elle permet de réduire les coûts de bande passante et offre à vos utilisateurs davantage de réactivité.</span><span class="sxs-lookup"><span data-stu-id="4451b-105">It reduces bandwidth costs and provides a more responsive experience for your users.</span></span>

<span data-ttu-id="4451b-106">Il existe deux façons d’activer la compression :</span><span class="sxs-lookup"><span data-stu-id="4451b-106">There are two ways to enable compression:</span></span>

* <span data-ttu-id="4451b-107">Vous pouvez activer la compression sur votre serveur d’origine. Dans ce cas, le CDN transmet les fichiers compressés et les remet aux clients qui les demandent.</span><span class="sxs-lookup"><span data-stu-id="4451b-107">You can enable compression on your origin server, in which case the CDN passes through the compressed files and deliver compressed files to clients that request them.</span></span>
* <span data-ttu-id="4451b-108">Vous pouvez activer la compression directement sur les serveurs de périmètre CDN. Dans ce cas, le CDN compresse les fichiers et les envoie aux utilisateurs finals, même s’ils ne sont pas compressés par le serveur d’origine.</span><span class="sxs-lookup"><span data-stu-id="4451b-108">You can enable compression directly on CDN edge servers, in which case the CDN compresses the files and serve them to end users, even if they are not compressed by the origin server.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4451b-109">Les changements de configuration CDN prennent un certain temps avant de se propager sur le réseau.</span><span class="sxs-lookup"><span data-stu-id="4451b-109">CDN configuration changes take some time to propagate through the network.</span></span>  <span data-ttu-id="4451b-110">Pour les profils du <b>CDN Azure fourni par Akamai</b> , la propagation s’effectue généralement en moins d’une minute.</span><span class="sxs-lookup"><span data-stu-id="4451b-110">For <b>Azure CDN from Akamai</b> profiles, propagation usually completes in under one minute.</span></span>  <span data-ttu-id="4451b-111">Pour les profils du <b>CDN Azure fourni par Verizon</b> , vous verrez généralement vos changements s’appliquer dans un délai de 90 minutes.</span><span class="sxs-lookup"><span data-stu-id="4451b-111">For <b>Azure CDN from Verizon</b> profiles, you will usually see your changes apply within 90 minutes.</span></span>  <span data-ttu-id="4451b-112">Si c’est la première fois que vous configurez la compression de votre point de terminaison CDN, patientez 1 à 2 heures pour être certain que les paramètres de compression ont été propagés aux POP avant de chercher à résoudre un problème.</span><span class="sxs-lookup"><span data-stu-id="4451b-112">If this is the first time you've set up compression for your CDN endpoint, you should consider waiting 1-2 hours to be sure the compression settings have propagated to the POPs before troubleshooting</span></span>
> 
> 

## <a name="enabling-compression"></a><span data-ttu-id="4451b-113">Activation de la compression</span><span class="sxs-lookup"><span data-stu-id="4451b-113">Enabling compression</span></span>
> [!NOTE]
> <span data-ttu-id="4451b-114">Les niveaux Standard et Premium de CDN fournissent les mêmes fonctionnalités, mais l’interface utilisateur est différente.</span><span class="sxs-lookup"><span data-stu-id="4451b-114">The Standard and Premium CDN tiers provide the same compression functionality, but the user interface differs.</span></span>  <span data-ttu-id="4451b-115">Pour plus d’informations sur les différences entre les niveaux Standard et Premium de CDN, consultez [Vue d’ensemble du réseau de distribution de contenu (CDN) Azure](cdn-overview.md).</span><span class="sxs-lookup"><span data-stu-id="4451b-115">For more information about the differences between Standard and Premium CDN tiers, see [Azure CDN Overview](cdn-overview.md).</span></span>
> 
> 

### <a name="standard-tier"></a><span data-ttu-id="4451b-116">Niveau standard</span><span class="sxs-lookup"><span data-stu-id="4451b-116">Standard tier</span></span>
> [!NOTE]
> <span data-ttu-id="4451b-117">Cette section s’applique au profil **Azure CDN Standard fourni par Verizon** et au profil **Azure CDN Standard fourni par Akamai**.</span><span class="sxs-lookup"><span data-stu-id="4451b-117">This section applies to **Azure CDN Standard from Verizon** and **Azure CDN Standard from Akamai** profiles.</span></span>
> 
> 

1. <span data-ttu-id="4451b-118">Dans la page du profil CDN, cliquez sur le point de terminaison CDN que vous souhaitez gérer.</span><span class="sxs-lookup"><span data-stu-id="4451b-118">From the CDN profile page, click the CDN endpoint you wish to manage.</span></span>
   
    ![Points de terminaison de la page de profil CDN](./media/cdn-file-compression/cdn-endpoints.png)
   
    <span data-ttu-id="4451b-120">La page du point de terminaison CDN s’ouvre.</span><span class="sxs-lookup"><span data-stu-id="4451b-120">The CDN endpoint page opens.</span></span>
2. <span data-ttu-id="4451b-121">Cliquez sur le bouton **Configurer** .</span><span class="sxs-lookup"><span data-stu-id="4451b-121">Click the **Configure** button.</span></span>
   
    ![Bouton de gestion de la page de profil CDN](./media/cdn-file-compression/cdn-config-btn.png)
   
    <span data-ttu-id="4451b-123">La page de configuration CDN s’ouvre.</span><span class="sxs-lookup"><span data-stu-id="4451b-123">The CDN Configuration page opens.</span></span>
3. <span data-ttu-id="4451b-124">Activez **Compression**.</span><span class="sxs-lookup"><span data-stu-id="4451b-124">Turn on **Compression**.</span></span>
   
    ![Options de compression CDN](./media/cdn-file-compression/cdn-compress-standard.png)
4. <span data-ttu-id="4451b-126">Utilisez les types par défaut ou modifiez la liste en supprimant ou en ajoutant des types de fichier.</span><span class="sxs-lookup"><span data-stu-id="4451b-126">Use the default types, or modify the list by removing or adding file types.</span></span>
   
   > [!TIP]
   > <span data-ttu-id="4451b-127">Bien que cela soit possible, il n’est pas recommandé d’appliquer la compression aux formats compressés, tels que ZIP, MP3, MP4, JPG, etc.</span><span class="sxs-lookup"><span data-stu-id="4451b-127">While possible, it is not recommended to apply compression to compressed formats, such as ZIP, MP3, MP4, JPG, etc.</span></span>
   > 
   > 
5. <span data-ttu-id="4451b-128">Une fois vos modifications effectuées, cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="4451b-128">After making your changes, click the **Save** button.</span></span>

### <a name="premium-tier"></a><span data-ttu-id="4451b-129">Niveau Premium</span><span class="sxs-lookup"><span data-stu-id="4451b-129">Premium tier</span></span>
> [!NOTE]
> <span data-ttu-id="4451b-130">Cette section s’applique aux profils du **CDN Azure CDN Premium fourni par Verizon** .</span><span class="sxs-lookup"><span data-stu-id="4451b-130">This section applies to **Azure CDN Premium from Verizon** profiles.</span></span>
> 
> 

1. <span data-ttu-id="4451b-131">Dans la page de profil CDN, cliquez sur le bouton **Gérer**.</span><span class="sxs-lookup"><span data-stu-id="4451b-131">From the CDN profile page, click the **Manage** button.</span></span>
   
    ![Bouton de gestion de la page de profil CDN](./media/cdn-file-compression/cdn-manage-btn.png)
   
    <span data-ttu-id="4451b-133">Le portail de gestion CDN s'ouvre.</span><span class="sxs-lookup"><span data-stu-id="4451b-133">The CDN management portal opens.</span></span>
2. <span data-ttu-id="4451b-134">Pointez sur l’onglet **HTTP volumineux**, puis pointez sur le menu volant **Paramètres de cache**.</span><span class="sxs-lookup"><span data-stu-id="4451b-134">Hover over the **HTTP Large** tab, then hover over the **Cache Settings** flyout.</span></span>  <span data-ttu-id="4451b-135">Cliquez sur **Compression**.</span><span class="sxs-lookup"><span data-stu-id="4451b-135">Click on **Compression**.</span></span>

    ![Sélection de la compression de fichiers](./media/cdn-file-compression/cdn-compress-select.png)
   
    <span data-ttu-id="4451b-137">Les options de compression sont affichées.</span><span class="sxs-lookup"><span data-stu-id="4451b-137">Compression options are displayed.</span></span>
   
    ![Compression de fichiers](./media/cdn-file-compression/cdn-compress-files.png)
3. <span data-ttu-id="4451b-139">Activez la compression en cliquant sur la case d’option **Compression activée** .</span><span class="sxs-lookup"><span data-stu-id="4451b-139">Enable compression by clicking the **Compression Enabled** radio button.</span></span>  <span data-ttu-id="4451b-140">Entrez les types MIME que vous souhaitez compresser sous forme de liste délimitée par des virgules (sans espace) dans la zone de texte **Types de fichiers** .</span><span class="sxs-lookup"><span data-stu-id="4451b-140">Enter the MIME types you wish to compress as a comma-delimited list (no spaces) in the **File Types** textbox.</span></span>
   
   > [!TIP]
   > <span data-ttu-id="4451b-141">Bien que cela soit possible, il n’est pas recommandé d’appliquer la compression aux formats compressés, tels que ZIP, MP3, MP4, JPG, etc.</span><span class="sxs-lookup"><span data-stu-id="4451b-141">While possible, it is not recommended to apply compression to compressed formats, such as ZIP, MP3, MP4, JPG, etc.</span></span> 
   > 
   > 
4. <span data-ttu-id="4451b-142">Après avoir apporté vos modifications, cliquez sur le bouton **Mettre à jour** .</span><span class="sxs-lookup"><span data-stu-id="4451b-142">After making your changes, click the **Update** button.</span></span>

## <a name="compression-rules"></a><span data-ttu-id="4451b-143">Règles de compression</span><span class="sxs-lookup"><span data-stu-id="4451b-143">Compression rules</span></span>
<span data-ttu-id="4451b-144">Ces tableaux décrivent le comportement de compression du CDN Azure pour chaque scénario.</span><span class="sxs-lookup"><span data-stu-id="4451b-144">These tables describe Azure CDN compression behavior for every scenario.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4451b-145">Pour le **CDN Azure fourni par Verizon** (Standard et Premium), seuls les fichiers éligibles sont compressés.</span><span class="sxs-lookup"><span data-stu-id="4451b-145">For **Azure CDN from Verizon** (Standard and Premium), only eligible files are compressed.</span></span>  <span data-ttu-id="4451b-146">Pour être éligible pour la compression, un fichier doit :</span><span class="sxs-lookup"><span data-stu-id="4451b-146">To be eligible for compression, a file must:</span></span>
> 
> * <span data-ttu-id="4451b-147">Être supérieur à 128 octets.</span><span class="sxs-lookup"><span data-stu-id="4451b-147">Be larger than 128 bytes.</span></span>
> * <span data-ttu-id="4451b-148">Être inférieur à 1 Mo.</span><span class="sxs-lookup"><span data-stu-id="4451b-148">Be smaller than 1 MB.</span></span>
> 
> <span data-ttu-id="4451b-149">Pour le **CDN Azure fourni par Akamai**, tous les fichiers sont éligibles à la compression.</span><span class="sxs-lookup"><span data-stu-id="4451b-149">For **Azure CDN from Akamai**, all files are eligible for compression.</span></span>
> 
> <span data-ttu-id="4451b-150">Pour tous les produits Azure CDN, un fichier doit être de type MIME qui a été [configuré pour la compression](#enabling-compression).</span><span class="sxs-lookup"><span data-stu-id="4451b-150">For all Azure CDN products, a file must be a MIME type that has been [configured for compression](#enabling-compression).</span></span>
> 
> <span data-ttu-id="4451b-151">Les profils **Azure CDN fourni par Verizon** (Standard et Premium) prennent en charge l’encodage **gzip** (zip GNU), **deflate**, **bzip2** ou **br** (Brotli).</span><span class="sxs-lookup"><span data-stu-id="4451b-151">**Azure CDN from Verizon** profiles (Standard and Premium) support **gzip** (GNU zip), **deflate**, **bzip2**, or  **br** (Brotli) encoding.</span></span> <span data-ttu-id="4451b-152">Pour l’encodage Brotli, la compression est effectuée uniquement en périphérie.</span><span class="sxs-lookup"><span data-stu-id="4451b-152">For Brotli encoding, the compression is done only at the edge.</span></span> <span data-ttu-id="4451b-153">Le client/navigateur doit envoyer la demande d’encodage Brotli et la ressource compressée doit d’abord avoir été compressée au niveau de l’origine.</span><span class="sxs-lookup"><span data-stu-id="4451b-153">The client/browser must send the request for Brotli encoding and the compressed asset must have been compressed on the origin side first.</span></span> 
>
><span data-ttu-id="4451b-154">Les profils du **CDN Azure fourni par Akamai** prennent uniquement en charge l’encodage **gzip**.</span><span class="sxs-lookup"><span data-stu-id="4451b-154">**Azure CDN from Akamai** profiles support only **gzip** encoding.</span></span>
> 
> <span data-ttu-id="4451b-155">Les points de terminaison **Azure CDN fourni par Akamai** demandent toujours des fichiers encodés **gzip** en provenance de l’origine, quelle que soit la demande du client.</span><span class="sxs-lookup"><span data-stu-id="4451b-155">**Azure CDN from Akamai** endpoints always request **gzip** encoded files from the origin, regardless of the client request.</span></span> 

### <a name="compression-disabled-or-file-is-ineligible-for-compression"></a><span data-ttu-id="4451b-156">Compression désactivée ou le fichier n’est pas éligible pour la compression</span><span class="sxs-lookup"><span data-stu-id="4451b-156">Compression disabled or file is ineligible for compression</span></span>
| <span data-ttu-id="4451b-157">Format demandé par le client (via l’en-tête Accept-Encoding)</span><span class="sxs-lookup"><span data-stu-id="4451b-157">Client requested format (via Accept-Encoding header)</span></span> | <span data-ttu-id="4451b-158">Format de fichier mis en cache</span><span class="sxs-lookup"><span data-stu-id="4451b-158">Cached file format</span></span> | <span data-ttu-id="4451b-159">Réponse du CDN au client</span><span class="sxs-lookup"><span data-stu-id="4451b-159">CDN response to the client</span></span> | <span data-ttu-id="4451b-160">Remarques</span><span class="sxs-lookup"><span data-stu-id="4451b-160">Notes</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="4451b-161">Compressé</span><span class="sxs-lookup"><span data-stu-id="4451b-161">Compressed</span></span> |<span data-ttu-id="4451b-162">Compressé</span><span class="sxs-lookup"><span data-stu-id="4451b-162">Compressed</span></span> |<span data-ttu-id="4451b-163">Compressé</span><span class="sxs-lookup"><span data-stu-id="4451b-163">Compressed</span></span> | |
| <span data-ttu-id="4451b-164">Compressé</span><span class="sxs-lookup"><span data-stu-id="4451b-164">Compressed</span></span> |<span data-ttu-id="4451b-165">Non compressé</span><span class="sxs-lookup"><span data-stu-id="4451b-165">Uncompressed</span></span> |<span data-ttu-id="4451b-166">Non compressé</span><span class="sxs-lookup"><span data-stu-id="4451b-166">Uncompressed</span></span> | |
| <span data-ttu-id="4451b-167">Compressé</span><span class="sxs-lookup"><span data-stu-id="4451b-167">Compressed</span></span> |<span data-ttu-id="4451b-168">Non mis en cache</span><span class="sxs-lookup"><span data-stu-id="4451b-168">Not cached</span></span> |<span data-ttu-id="4451b-169">Compressés ou non compressé</span><span class="sxs-lookup"><span data-stu-id="4451b-169">Compressed or Uncompressed</span></span> |<span data-ttu-id="4451b-170">Dépend de la réponse d’origine</span><span class="sxs-lookup"><span data-stu-id="4451b-170">Depends on origin response</span></span> |
| <span data-ttu-id="4451b-171">Non compressé</span><span class="sxs-lookup"><span data-stu-id="4451b-171">Uncompressed</span></span> |<span data-ttu-id="4451b-172">Compressé</span><span class="sxs-lookup"><span data-stu-id="4451b-172">Compressed</span></span> |<span data-ttu-id="4451b-173">Non compressé</span><span class="sxs-lookup"><span data-stu-id="4451b-173">Uncompressed</span></span> | |
| <span data-ttu-id="4451b-174">Non compressé</span><span class="sxs-lookup"><span data-stu-id="4451b-174">Uncompressed</span></span> |<span data-ttu-id="4451b-175">Non compressé</span><span class="sxs-lookup"><span data-stu-id="4451b-175">Uncompressed</span></span> |<span data-ttu-id="4451b-176">Non compressé</span><span class="sxs-lookup"><span data-stu-id="4451b-176">Uncompressed</span></span> | |
| <span data-ttu-id="4451b-177">Non compressé</span><span class="sxs-lookup"><span data-stu-id="4451b-177">Uncompressed</span></span> |<span data-ttu-id="4451b-178">Non mis en cache</span><span class="sxs-lookup"><span data-stu-id="4451b-178">Not cached</span></span> |<span data-ttu-id="4451b-179">Non compressé</span><span class="sxs-lookup"><span data-stu-id="4451b-179">Uncompressed</span></span> | |

### <a name="compression-enabled-and-file-is-eligible-for-compression"></a><span data-ttu-id="4451b-180">La compression est activée et le fichier est éligible pour la compression</span><span class="sxs-lookup"><span data-stu-id="4451b-180">Compression enabled and file is eligible for compression</span></span>
| <span data-ttu-id="4451b-181">Format demandé par le client (via l’en-tête Accept-Encoding)</span><span class="sxs-lookup"><span data-stu-id="4451b-181">Client requested format (via Accept-Encoding header)</span></span> | <span data-ttu-id="4451b-182">Format de fichier mis en cache</span><span class="sxs-lookup"><span data-stu-id="4451b-182">Cached file format</span></span> | <span data-ttu-id="4451b-183">Réponse du CDN au client</span><span class="sxs-lookup"><span data-stu-id="4451b-183">CDN response to the client</span></span> | <span data-ttu-id="4451b-184">Remarques</span><span class="sxs-lookup"><span data-stu-id="4451b-184">Notes</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="4451b-185">Compressé</span><span class="sxs-lookup"><span data-stu-id="4451b-185">Compressed</span></span> |<span data-ttu-id="4451b-186">Compressé</span><span class="sxs-lookup"><span data-stu-id="4451b-186">Compressed</span></span> |<span data-ttu-id="4451b-187">Compressé</span><span class="sxs-lookup"><span data-stu-id="4451b-187">Compressed</span></span> |<span data-ttu-id="4451b-188">Transcode CDN entre les formats pris en charge</span><span class="sxs-lookup"><span data-stu-id="4451b-188">CDN transcodes between supported formats</span></span> |
| <span data-ttu-id="4451b-189">Compressé</span><span class="sxs-lookup"><span data-stu-id="4451b-189">Compressed</span></span> |<span data-ttu-id="4451b-190">Non compressé</span><span class="sxs-lookup"><span data-stu-id="4451b-190">Uncompressed</span></span> |<span data-ttu-id="4451b-191">Compressé</span><span class="sxs-lookup"><span data-stu-id="4451b-191">Compressed</span></span> |<span data-ttu-id="4451b-192">CDN effectue la compression</span><span class="sxs-lookup"><span data-stu-id="4451b-192">CDN performs compression</span></span> |
| <span data-ttu-id="4451b-193">Compressé</span><span class="sxs-lookup"><span data-stu-id="4451b-193">Compressed</span></span> |<span data-ttu-id="4451b-194">Non mis en cache</span><span class="sxs-lookup"><span data-stu-id="4451b-194">Not cached</span></span> |<span data-ttu-id="4451b-195">Compressé</span><span class="sxs-lookup"><span data-stu-id="4451b-195">Compressed</span></span> |<span data-ttu-id="4451b-196">CDN effectue la compression si l’origine renvoie le format non compressé.</span><span class="sxs-lookup"><span data-stu-id="4451b-196">CDN performs compression if origin returns uncompressed.</span></span>  <span data-ttu-id="4451b-197">**Azure CDN fourni par Verizon** transmet le fichier non compressé à la première demande, puis compresse et met en cache le fichier pour les demandes suivantes.</span><span class="sxs-lookup"><span data-stu-id="4451b-197">**Azure CDN from Verizon** passes the uncompressed file on the first request and then compresses and caches the file for subsequent requests.</span></span>  <span data-ttu-id="4451b-198">Les fichiers avec l’en-tête `Cache-Control: no-cache` ne seront jamais compressés.</span><span class="sxs-lookup"><span data-stu-id="4451b-198">Files with `Cache-Control: no-cache` header will never be compressed.</span></span> |
| <span data-ttu-id="4451b-199">Non compressé</span><span class="sxs-lookup"><span data-stu-id="4451b-199">Uncompressed</span></span> |<span data-ttu-id="4451b-200">Compressé</span><span class="sxs-lookup"><span data-stu-id="4451b-200">Compressed</span></span> |<span data-ttu-id="4451b-201">Non compressé</span><span class="sxs-lookup"><span data-stu-id="4451b-201">Uncompressed</span></span> |<span data-ttu-id="4451b-202">CDN effectue la décompression</span><span class="sxs-lookup"><span data-stu-id="4451b-202">CDN performs decompression</span></span> |
| <span data-ttu-id="4451b-203">Non compressé</span><span class="sxs-lookup"><span data-stu-id="4451b-203">Uncompressed</span></span> |<span data-ttu-id="4451b-204">Non compressé</span><span class="sxs-lookup"><span data-stu-id="4451b-204">Uncompressed</span></span> |<span data-ttu-id="4451b-205">Non compressé</span><span class="sxs-lookup"><span data-stu-id="4451b-205">Uncompressed</span></span> | |
| <span data-ttu-id="4451b-206">Non compressé</span><span class="sxs-lookup"><span data-stu-id="4451b-206">Uncompressed</span></span> |<span data-ttu-id="4451b-207">Non mis en cache</span><span class="sxs-lookup"><span data-stu-id="4451b-207">Not cached</span></span> |<span data-ttu-id="4451b-208">Non compressé</span><span class="sxs-lookup"><span data-stu-id="4451b-208">Uncompressed</span></span> | |

## <a name="media-services-cdn-compression"></a><span data-ttu-id="4451b-209">Compression CDN Media Services</span><span class="sxs-lookup"><span data-stu-id="4451b-209">Media Services CDN Compression</span></span>
<span data-ttu-id="4451b-210">Pour les points de terminaison de diffusion en continu CDN de Media Services, la compression est activée par défaut pour les types de contenu suivants : application/vnd.ms-sstr+xml, application/dash+xml,application/vnd.apple.mpegurl, application/f4m+xml.</span><span class="sxs-lookup"><span data-stu-id="4451b-210">For Media Services CDN enabled streaming endpoints, compression is enabled by default for the following content types: application/vnd.ms-sstr+xml, application/dash+xml,application/vnd.apple.mpegurl, application/f4m+xml.</span></span> <span data-ttu-id="4451b-211">Vous ne pouvez pas activer ou désactiver la compression pour les types mentionnés à l'aide du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="4451b-211">You cannot enable/disable compression for the mentioned types using the Azure portal.</span></span>  

## <a name="see-also"></a><span data-ttu-id="4451b-212">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="4451b-212">See also</span></span>
* [<span data-ttu-id="4451b-213">Résolution des problèmes de compression des fichiers CDN</span><span class="sxs-lookup"><span data-stu-id="4451b-213">Troubleshooting CDN file compression</span></span>](cdn-troubleshoot-compression.md)    

