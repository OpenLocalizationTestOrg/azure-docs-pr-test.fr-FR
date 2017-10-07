---
title: performances aaaImprove en compressant les fichiers dans le CDN Azure | Documents Microsoft
description: "Découvrez comment tooimprove fichier transférer les performances de chargement de page vitesse et augmentent par la compression des fichiers dans le CDN Azure."
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
ms.openlocfilehash: 9a1698b6c29233c2e2e6fb17cdd8e919ae8bfa1c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="improve-performance-by-compressing-files-in-azure-cdn"></a><span data-ttu-id="d5ef3-103">Compression des fichiers dans Azure CDN pour améliorer les performances</span><span class="sxs-lookup"><span data-stu-id="d5ef3-103">Improve performance by compressing files in Azure CDN</span></span>
<span data-ttu-id="d5ef3-104">La compression est une vitesse de transfert de fichier tooimprove méthode simple et efficace et performances de chargement de page augmentation en réduisant la taille du fichier avant qu’il sont envoyé à partir du serveur de hello.</span><span class="sxs-lookup"><span data-stu-id="d5ef3-104">Compression is a simple and effective method tooimprove file transfer speed and increase page load performance by reducing file size before it is sent from hello server.</span></span> <span data-ttu-id="d5ef3-105">Elle permet de réduire les coûts de bande passante et offre à vos utilisateurs davantage de réactivité.</span><span class="sxs-lookup"><span data-stu-id="d5ef3-105">It reduces bandwidth costs and provides a more responsive experience for your users.</span></span>

<span data-ttu-id="d5ef3-106">Il existe deux façons de tooenable compression :</span><span class="sxs-lookup"><span data-stu-id="d5ef3-106">There are two ways tooenable compression:</span></span>

* <span data-ttu-id="d5ef3-107">Vous pouvez activer la compression sur votre serveur d’origine, auquel cas hello CDN traverse hello des fichiers compressés et remettre les fichiers compressés tooclients qui les demandent.</span><span class="sxs-lookup"><span data-stu-id="d5ef3-107">You can enable compression on your origin server, in which case hello CDN passes through hello compressed files and deliver compressed files tooclients that request them.</span></span>
* <span data-ttu-id="d5ef3-108">Vous pouvez activer la compression directement sur les serveurs de bord CDN, dans lequel cas hello CDN compresse hello des fichiers et servir les utilisateurs tooend, même si elles ne sont pas compressées par le serveur d’origine hello.</span><span class="sxs-lookup"><span data-stu-id="d5ef3-108">You can enable compression directly on CDN edge servers, in which case hello CDN compresses hello files and serve them tooend users, even if they are not compressed by hello origin server.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d5ef3-109">Modifications de configuration CDN prendront certaines toopropagate de temps via le réseau de hello.</span><span class="sxs-lookup"><span data-stu-id="d5ef3-109">CDN configuration changes take some time toopropagate through hello network.</span></span>  <span data-ttu-id="d5ef3-110">Pour les profils du <b>CDN Azure fourni par Akamai</b> , la propagation s’effectue généralement en moins d’une minute.</span><span class="sxs-lookup"><span data-stu-id="d5ef3-110">For <b>Azure CDN from Akamai</b> profiles, propagation usually completes in under one minute.</span></span>  <span data-ttu-id="d5ef3-111">Pour les profils du <b>CDN Azure fourni par Verizon</b> , vous verrez généralement vos changements s’appliquer dans un délai de 90 minutes.</span><span class="sxs-lookup"><span data-stu-id="d5ef3-111">For <b>Azure CDN from Verizon</b> profiles, you will usually see your changes apply within 90 minutes.</span></span>  <span data-ttu-id="d5ef3-112">S’il s’agit hello première fois que vous avez configuré la compression pour votre point de terminaison CDN, vous devez envisager d’attente toobe 1 et 2 heures que la propagation des paramètres de compression de hello POP toohello avant la résolution des problèmes</span><span class="sxs-lookup"><span data-stu-id="d5ef3-112">If this is hello first time you've set up compression for your CDN endpoint, you should consider waiting 1-2 hours toobe sure hello compression settings have propagated toohello POPs before troubleshooting</span></span>
> 
> 

## <a name="enabling-compression"></a><span data-ttu-id="d5ef3-113">Activation de la compression</span><span class="sxs-lookup"><span data-stu-id="d5ef3-113">Enabling compression</span></span>
> [!NOTE]
> <span data-ttu-id="d5ef3-114">fournissent Hello niveaux Standard et Premium CDN hello les mêmes fonctionnalités de compression, mais diffère hello interface utilisateur.</span><span class="sxs-lookup"><span data-stu-id="d5ef3-114">hello Standard and Premium CDN tiers provide hello same compression functionality, but hello user interface differs.</span></span>  <span data-ttu-id="d5ef3-115">Pour plus d’informations sur les différences de hello entre les niveaux Standard et Premium CDN, consultez [vue d’ensemble du CDN Azure](cdn-overview.md).</span><span class="sxs-lookup"><span data-stu-id="d5ef3-115">For more information about hello differences between Standard and Premium CDN tiers, see [Azure CDN Overview](cdn-overview.md).</span></span>
> 
> 

### <a name="standard-tier"></a><span data-ttu-id="d5ef3-116">Niveau standard</span><span class="sxs-lookup"><span data-stu-id="d5ef3-116">Standard tier</span></span>
> [!NOTE]
> <span data-ttu-id="d5ef3-117">Cette section s’applique également**Azure CDN Standard de Verizon** et **Azure CDN Standard à partir d’Akamai** profils.</span><span class="sxs-lookup"><span data-stu-id="d5ef3-117">This section applies too**Azure CDN Standard from Verizon** and **Azure CDN Standard from Akamai** profiles.</span></span>
> 
> 

1. <span data-ttu-id="d5ef3-118">À partir de la page de profil CDN hello, cliquez sur le point de terminaison CDN hello toomanage vous le souhaitez.</span><span class="sxs-lookup"><span data-stu-id="d5ef3-118">From hello CDN profile page, click hello CDN endpoint you wish toomanage.</span></span>
   
    ![Points de terminaison de la page de profil CDN](./media/cdn-file-compression/cdn-endpoints.png)
   
    <span data-ttu-id="d5ef3-120">page de point de terminaison CDN Hello s’ouvre.</span><span class="sxs-lookup"><span data-stu-id="d5ef3-120">hello CDN endpoint page opens.</span></span>
2. <span data-ttu-id="d5ef3-121">Cliquez sur hello **configurer** bouton.</span><span class="sxs-lookup"><span data-stu-id="d5ef3-121">Click hello **Configure** button.</span></span>
   
    ![Bouton de gestion de la page de profil CDN](./media/cdn-file-compression/cdn-config-btn.png)
   
    <span data-ttu-id="d5ef3-123">page de Configuration CDN Hello s’ouvre.</span><span class="sxs-lookup"><span data-stu-id="d5ef3-123">hello CDN Configuration page opens.</span></span>
3. <span data-ttu-id="d5ef3-124">Activez **Compression**.</span><span class="sxs-lookup"><span data-stu-id="d5ef3-124">Turn on **Compression**.</span></span>
   
    ![Options de compression CDN](./media/cdn-file-compression/cdn-compress-standard.png)
4. <span data-ttu-id="d5ef3-126">Utiliser des types de valeur par défaut de hello, ou modifier la liste de hello en supprimant ou en ajoutant des types de fichiers.</span><span class="sxs-lookup"><span data-stu-id="d5ef3-126">Use hello default types, or modify hello list by removing or adding file types.</span></span>
   
   > [!TIP]
   > <span data-ttu-id="d5ef3-127">Tant que possible, il n’est pas recommandé tooapply compression toocompressed formats, tels que ZIP, MP3, MP4, JPG, etc..</span><span class="sxs-lookup"><span data-stu-id="d5ef3-127">While possible, it is not recommended tooapply compression toocompressed formats, such as ZIP, MP3, MP4, JPG, etc.</span></span>
   > 
   > 
5. <span data-ttu-id="d5ef3-128">Après avoir apporté vos modifications, cliquez sur hello **enregistrer** bouton.</span><span class="sxs-lookup"><span data-stu-id="d5ef3-128">After making your changes, click hello **Save** button.</span></span>

### <a name="premium-tier"></a><span data-ttu-id="d5ef3-129">Niveau Premium</span><span class="sxs-lookup"><span data-stu-id="d5ef3-129">Premium tier</span></span>
> [!NOTE]
> <span data-ttu-id="d5ef3-130">Cette section s’applique également**Azure CDN Premium de Verizon** profils.</span><span class="sxs-lookup"><span data-stu-id="d5ef3-130">This section applies too**Azure CDN Premium from Verizon** profiles.</span></span>
> 
> 

1. <span data-ttu-id="d5ef3-131">À partir de la page de profil hello CDN, cliquez sur hello **gérer** bouton.</span><span class="sxs-lookup"><span data-stu-id="d5ef3-131">From hello CDN profile page, click hello **Manage** button.</span></span>
   
    ![Bouton de gestion de la page de profil CDN](./media/cdn-file-compression/cdn-manage-btn.png)
   
    <span data-ttu-id="d5ef3-133">portail de gestion CDN Hello s’ouvre.</span><span class="sxs-lookup"><span data-stu-id="d5ef3-133">hello CDN management portal opens.</span></span>
2. <span data-ttu-id="d5ef3-134">Pointage hello **grand HTTP** tab, puis pointez sur hello **paramètres de Cache** menu volant.</span><span class="sxs-lookup"><span data-stu-id="d5ef3-134">Hover over hello **HTTP Large** tab, then hover over hello **Cache Settings** flyout.</span></span>  <span data-ttu-id="d5ef3-135">Cliquez sur **Compression**.</span><span class="sxs-lookup"><span data-stu-id="d5ef3-135">Click on **Compression**.</span></span>

    ![Sélection de la compression de fichiers](./media/cdn-file-compression/cdn-compress-select.png)
   
    <span data-ttu-id="d5ef3-137">Les options de compression sont affichées.</span><span class="sxs-lookup"><span data-stu-id="d5ef3-137">Compression options are displayed.</span></span>
   
    ![Compression de fichiers](./media/cdn-file-compression/cdn-compress-files.png)
3. <span data-ttu-id="d5ef3-139">Activer la compression en cliquant sur hello **Compression activée** case d’option.</span><span class="sxs-lookup"><span data-stu-id="d5ef3-139">Enable compression by clicking hello **Compression Enabled** radio button.</span></span>  <span data-ttu-id="d5ef3-140">Entrez les types MIME hello vous souhaitez toocompress sous la forme d’une liste délimitée par des virgules (sans espaces) Bonjour **Types de fichiers** zone de texte.</span><span class="sxs-lookup"><span data-stu-id="d5ef3-140">Enter hello MIME types you wish toocompress as a comma-delimited list (no spaces) in hello **File Types** textbox.</span></span>
   
   > [!TIP]
   > <span data-ttu-id="d5ef3-141">Tant que possible, il n’est pas recommandé tooapply compression toocompressed formats, tels que ZIP, MP3, MP4, JPG, etc..</span><span class="sxs-lookup"><span data-stu-id="d5ef3-141">While possible, it is not recommended tooapply compression toocompressed formats, such as ZIP, MP3, MP4, JPG, etc.</span></span> 
   > 
   > 
4. <span data-ttu-id="d5ef3-142">Après avoir apporté vos modifications, cliquez sur hello **mise à jour** bouton.</span><span class="sxs-lookup"><span data-stu-id="d5ef3-142">After making your changes, click hello **Update** button.</span></span>

## <a name="compression-rules"></a><span data-ttu-id="d5ef3-143">Règles de compression</span><span class="sxs-lookup"><span data-stu-id="d5ef3-143">Compression rules</span></span>
<span data-ttu-id="d5ef3-144">Ces tableaux décrivent le comportement de compression du CDN Azure pour chaque scénario.</span><span class="sxs-lookup"><span data-stu-id="d5ef3-144">These tables describe Azure CDN compression behavior for every scenario.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d5ef3-145">Pour le **CDN Azure fourni par Verizon** (Standard et Premium), seuls les fichiers éligibles sont compressés.</span><span class="sxs-lookup"><span data-stu-id="d5ef3-145">For **Azure CDN from Verizon** (Standard and Premium), only eligible files are compressed.</span></span>  <span data-ttu-id="d5ef3-146">un fichier de toobe éligible pour la compression, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="d5ef3-146">toobe eligible for compression, a file must:</span></span>
> 
> * <span data-ttu-id="d5ef3-147">Être supérieur à 128 octets.</span><span class="sxs-lookup"><span data-stu-id="d5ef3-147">Be larger than 128 bytes.</span></span>
> * <span data-ttu-id="d5ef3-148">Être inférieur à 1 Mo.</span><span class="sxs-lookup"><span data-stu-id="d5ef3-148">Be smaller than 1 MB.</span></span>
> 
> <span data-ttu-id="d5ef3-149">Pour le **CDN Azure fourni par Akamai**, tous les fichiers sont éligibles à la compression.</span><span class="sxs-lookup"><span data-stu-id="d5ef3-149">For **Azure CDN from Akamai**, all files are eligible for compression.</span></span>
> 
> <span data-ttu-id="d5ef3-150">Pour tous les produits Azure CDN, un fichier doit être de type MIME qui a été [configuré pour la compression](#enabling-compression).</span><span class="sxs-lookup"><span data-stu-id="d5ef3-150">For all Azure CDN products, a file must be a MIME type that has been [configured for compression](#enabling-compression).</span></span>
> 
> <span data-ttu-id="d5ef3-151">Les profils **Azure CDN fourni par Verizon** (Standard et Premium) prennent en charge l’encodage **gzip** (zip GNU), **deflate**, **bzip2** ou **br** (Brotli).</span><span class="sxs-lookup"><span data-stu-id="d5ef3-151">**Azure CDN from Verizon** profiles (Standard and Premium) support **gzip** (GNU zip), **deflate**, **bzip2**, or  **br** (Brotli) encoding.</span></span> <span data-ttu-id="d5ef3-152">Pour l’encodage de Brotli, la compression de hello est effectuée uniquement sur le bord de hello.</span><span class="sxs-lookup"><span data-stu-id="d5ef3-152">For Brotli encoding, hello compression is done only at hello edge.</span></span> <span data-ttu-id="d5ef3-153">Hello client/navigateur doit envoyer la demande hello pour l’encodage de Brotli et asset compressé de hello doit avoir été compressé côté hello d’origine tout d’abord.</span><span class="sxs-lookup"><span data-stu-id="d5ef3-153">hello client/browser must send hello request for Brotli encoding and hello compressed asset must have been compressed on hello origin side first.</span></span> 
>
><span data-ttu-id="d5ef3-154">Les profils du **CDN Azure fourni par Akamai** prennent uniquement en charge l’encodage **gzip**.</span><span class="sxs-lookup"><span data-stu-id="d5ef3-154">**Azure CDN from Akamai** profiles support only **gzip** encoding.</span></span>
> 
> <span data-ttu-id="d5ef3-155">**CDN Azure à partir d’Akamai** demande toujours des points de terminaison **gzip** de fichiers à partir de l’origine de hello, quelle que soit la demande du client hello codés.</span><span class="sxs-lookup"><span data-stu-id="d5ef3-155">**Azure CDN from Akamai** endpoints always request **gzip** encoded files from hello origin, regardless of hello client request.</span></span> 

### <a name="compression-disabled-or-file-is-ineligible-for-compression"></a><span data-ttu-id="d5ef3-156">Compression désactivée ou le fichier n’est pas éligible pour la compression</span><span class="sxs-lookup"><span data-stu-id="d5ef3-156">Compression disabled or file is ineligible for compression</span></span>
| <span data-ttu-id="d5ef3-157">Format demandé par le client (via l’en-tête Accept-Encoding)</span><span class="sxs-lookup"><span data-stu-id="d5ef3-157">Client requested format (via Accept-Encoding header)</span></span> | <span data-ttu-id="d5ef3-158">Format de fichier mis en cache</span><span class="sxs-lookup"><span data-stu-id="d5ef3-158">Cached file format</span></span> | <span data-ttu-id="d5ef3-159">Client de toohello réponse CDN</span><span class="sxs-lookup"><span data-stu-id="d5ef3-159">CDN response toohello client</span></span> | <span data-ttu-id="d5ef3-160">Remarques</span><span class="sxs-lookup"><span data-stu-id="d5ef3-160">Notes</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="d5ef3-161">Compressé</span><span class="sxs-lookup"><span data-stu-id="d5ef3-161">Compressed</span></span> |<span data-ttu-id="d5ef3-162">Compressé</span><span class="sxs-lookup"><span data-stu-id="d5ef3-162">Compressed</span></span> |<span data-ttu-id="d5ef3-163">Compressé</span><span class="sxs-lookup"><span data-stu-id="d5ef3-163">Compressed</span></span> | |
| <span data-ttu-id="d5ef3-164">Compressé</span><span class="sxs-lookup"><span data-stu-id="d5ef3-164">Compressed</span></span> |<span data-ttu-id="d5ef3-165">Non compressé</span><span class="sxs-lookup"><span data-stu-id="d5ef3-165">Uncompressed</span></span> |<span data-ttu-id="d5ef3-166">Non compressé</span><span class="sxs-lookup"><span data-stu-id="d5ef3-166">Uncompressed</span></span> | |
| <span data-ttu-id="d5ef3-167">Compressé</span><span class="sxs-lookup"><span data-stu-id="d5ef3-167">Compressed</span></span> |<span data-ttu-id="d5ef3-168">Non mis en cache</span><span class="sxs-lookup"><span data-stu-id="d5ef3-168">Not cached</span></span> |<span data-ttu-id="d5ef3-169">Compressés ou non compressé</span><span class="sxs-lookup"><span data-stu-id="d5ef3-169">Compressed or Uncompressed</span></span> |<span data-ttu-id="d5ef3-170">Dépend de la réponse d’origine</span><span class="sxs-lookup"><span data-stu-id="d5ef3-170">Depends on origin response</span></span> |
| <span data-ttu-id="d5ef3-171">Non compressé</span><span class="sxs-lookup"><span data-stu-id="d5ef3-171">Uncompressed</span></span> |<span data-ttu-id="d5ef3-172">Compressé</span><span class="sxs-lookup"><span data-stu-id="d5ef3-172">Compressed</span></span> |<span data-ttu-id="d5ef3-173">Non compressé</span><span class="sxs-lookup"><span data-stu-id="d5ef3-173">Uncompressed</span></span> | |
| <span data-ttu-id="d5ef3-174">Non compressé</span><span class="sxs-lookup"><span data-stu-id="d5ef3-174">Uncompressed</span></span> |<span data-ttu-id="d5ef3-175">Non compressé</span><span class="sxs-lookup"><span data-stu-id="d5ef3-175">Uncompressed</span></span> |<span data-ttu-id="d5ef3-176">Non compressé</span><span class="sxs-lookup"><span data-stu-id="d5ef3-176">Uncompressed</span></span> | |
| <span data-ttu-id="d5ef3-177">Non compressé</span><span class="sxs-lookup"><span data-stu-id="d5ef3-177">Uncompressed</span></span> |<span data-ttu-id="d5ef3-178">Non mis en cache</span><span class="sxs-lookup"><span data-stu-id="d5ef3-178">Not cached</span></span> |<span data-ttu-id="d5ef3-179">Non compressé</span><span class="sxs-lookup"><span data-stu-id="d5ef3-179">Uncompressed</span></span> | |

### <a name="compression-enabled-and-file-is-eligible-for-compression"></a><span data-ttu-id="d5ef3-180">La compression est activée et le fichier est éligible pour la compression</span><span class="sxs-lookup"><span data-stu-id="d5ef3-180">Compression enabled and file is eligible for compression</span></span>
| <span data-ttu-id="d5ef3-181">Format demandé par le client (via l’en-tête Accept-Encoding)</span><span class="sxs-lookup"><span data-stu-id="d5ef3-181">Client requested format (via Accept-Encoding header)</span></span> | <span data-ttu-id="d5ef3-182">Format de fichier mis en cache</span><span class="sxs-lookup"><span data-stu-id="d5ef3-182">Cached file format</span></span> | <span data-ttu-id="d5ef3-183">Client de toohello réponse CDN</span><span class="sxs-lookup"><span data-stu-id="d5ef3-183">CDN response toohello client</span></span> | <span data-ttu-id="d5ef3-184">Remarques</span><span class="sxs-lookup"><span data-stu-id="d5ef3-184">Notes</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="d5ef3-185">Compressé</span><span class="sxs-lookup"><span data-stu-id="d5ef3-185">Compressed</span></span> |<span data-ttu-id="d5ef3-186">Compressé</span><span class="sxs-lookup"><span data-stu-id="d5ef3-186">Compressed</span></span> |<span data-ttu-id="d5ef3-187">Compressé</span><span class="sxs-lookup"><span data-stu-id="d5ef3-187">Compressed</span></span> |<span data-ttu-id="d5ef3-188">Transcode CDN entre les formats pris en charge</span><span class="sxs-lookup"><span data-stu-id="d5ef3-188">CDN transcodes between supported formats</span></span> |
| <span data-ttu-id="d5ef3-189">Compressé</span><span class="sxs-lookup"><span data-stu-id="d5ef3-189">Compressed</span></span> |<span data-ttu-id="d5ef3-190">Non compressé</span><span class="sxs-lookup"><span data-stu-id="d5ef3-190">Uncompressed</span></span> |<span data-ttu-id="d5ef3-191">Compressé</span><span class="sxs-lookup"><span data-stu-id="d5ef3-191">Compressed</span></span> |<span data-ttu-id="d5ef3-192">CDN effectue la compression</span><span class="sxs-lookup"><span data-stu-id="d5ef3-192">CDN performs compression</span></span> |
| <span data-ttu-id="d5ef3-193">Compressé</span><span class="sxs-lookup"><span data-stu-id="d5ef3-193">Compressed</span></span> |<span data-ttu-id="d5ef3-194">Non mis en cache</span><span class="sxs-lookup"><span data-stu-id="d5ef3-194">Not cached</span></span> |<span data-ttu-id="d5ef3-195">Compressé</span><span class="sxs-lookup"><span data-stu-id="d5ef3-195">Compressed</span></span> |<span data-ttu-id="d5ef3-196">CDN effectue la compression si l’origine renvoie le format non compressé.</span><span class="sxs-lookup"><span data-stu-id="d5ef3-196">CDN performs compression if origin returns uncompressed.</span></span>  <span data-ttu-id="d5ef3-197">**Azure CDN de Verizon** passe hello fichier non compressé sur la première demande de hello et puis compresse et caches hello fichier pour les demandes suivantes.</span><span class="sxs-lookup"><span data-stu-id="d5ef3-197">**Azure CDN from Verizon** passes hello uncompressed file on hello first request and then compresses and caches hello file for subsequent requests.</span></span>  <span data-ttu-id="d5ef3-198">Les fichiers avec l’en-tête `Cache-Control: no-cache` ne seront jamais compressés.</span><span class="sxs-lookup"><span data-stu-id="d5ef3-198">Files with `Cache-Control: no-cache` header will never be compressed.</span></span> |
| <span data-ttu-id="d5ef3-199">Non compressé</span><span class="sxs-lookup"><span data-stu-id="d5ef3-199">Uncompressed</span></span> |<span data-ttu-id="d5ef3-200">Compressé</span><span class="sxs-lookup"><span data-stu-id="d5ef3-200">Compressed</span></span> |<span data-ttu-id="d5ef3-201">Non compressé</span><span class="sxs-lookup"><span data-stu-id="d5ef3-201">Uncompressed</span></span> |<span data-ttu-id="d5ef3-202">CDN effectue la décompression</span><span class="sxs-lookup"><span data-stu-id="d5ef3-202">CDN performs decompression</span></span> |
| <span data-ttu-id="d5ef3-203">Non compressé</span><span class="sxs-lookup"><span data-stu-id="d5ef3-203">Uncompressed</span></span> |<span data-ttu-id="d5ef3-204">Non compressé</span><span class="sxs-lookup"><span data-stu-id="d5ef3-204">Uncompressed</span></span> |<span data-ttu-id="d5ef3-205">Non compressé</span><span class="sxs-lookup"><span data-stu-id="d5ef3-205">Uncompressed</span></span> | |
| <span data-ttu-id="d5ef3-206">Non compressé</span><span class="sxs-lookup"><span data-stu-id="d5ef3-206">Uncompressed</span></span> |<span data-ttu-id="d5ef3-207">Non mis en cache</span><span class="sxs-lookup"><span data-stu-id="d5ef3-207">Not cached</span></span> |<span data-ttu-id="d5ef3-208">Non compressé</span><span class="sxs-lookup"><span data-stu-id="d5ef3-208">Uncompressed</span></span> | |

## <a name="media-services-cdn-compression"></a><span data-ttu-id="d5ef3-209">Compression CDN Media Services</span><span class="sxs-lookup"><span data-stu-id="d5ef3-209">Media Services CDN Compression</span></span>
<span data-ttu-id="d5ef3-210">Media Services CDN activé des points de terminaison de diffusion en continu, la compression est activée par défaut pour les types de contenu suivants de hello : application/vnd.ms-sstr + xml, application/dash+xml,application/vnd.apple.mpegurl, application/f4m + xml.</span><span class="sxs-lookup"><span data-stu-id="d5ef3-210">For Media Services CDN enabled streaming endpoints, compression is enabled by default for hello following content types: application/vnd.ms-sstr+xml, application/dash+xml,application/vnd.apple.mpegurl, application/f4m+xml.</span></span> <span data-ttu-id="d5ef3-211">Vous ne pouvez pas activer/désactiver la compression pour hello mentionné types à l’aide de hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="d5ef3-211">You cannot enable/disable compression for hello mentioned types using hello Azure portal.</span></span>  

## <a name="see-also"></a><span data-ttu-id="d5ef3-212">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="d5ef3-212">See also</span></span>
* [<span data-ttu-id="d5ef3-213">Résolution des problèmes de compression des fichiers CDN</span><span class="sxs-lookup"><span data-stu-id="d5ef3-213">Troubleshooting CDN file compression</span></span>](cdn-troubleshoot-compression.md)    

