---
title: la compression de fichiers aaaTroubleshooting dans Azure CDN | Documents Microsoft
description: "Résolvez les problèmes de compression des fichiers CDN Azure."
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: a6624e65-1a77-4486-b473-8d720ce28f8b
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: f00b98beaf6b3b3cd30108ece65a8191edc06ff5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-cdn-file-compression"></a><span data-ttu-id="a3ca3-103">Résolution des problèmes de compression des fichiers CDN</span><span class="sxs-lookup"><span data-stu-id="a3ca3-103">Troubleshooting CDN file compression</span></span>
<span data-ttu-id="a3ca3-104">Cet article vous aide à résoudre les problèmes de [compression des fichiers CDN](cdn-improve-performance.md).</span><span class="sxs-lookup"><span data-stu-id="a3ca3-104">This article helps you troubleshoot issues with [CDN file compression](cdn-improve-performance.md).</span></span>

<span data-ttu-id="a3ca3-105">Si vous avez besoin d’aide à tout moment dans cet article, vous pouvez contacter hello experts Azure sur [hello MSDN Azure et hello forums de débordement de pile](https://azure.microsoft.com/support/forums/).</span><span class="sxs-lookup"><span data-stu-id="a3ca3-105">If you need more help at any point in this article, you can contact hello Azure experts on [hello MSDN Azure and hello Stack Overflow forums](https://azure.microsoft.com/support/forums/).</span></span> <span data-ttu-id="a3ca3-106">Vous pouvez également signaler un incident au support Azure.</span><span class="sxs-lookup"><span data-stu-id="a3ca3-106">Alternatively, you can also file an Azure support incident.</span></span> <span data-ttu-id="a3ca3-107">Accédez toohello [site de Support technique Azure](https://azure.microsoft.com/support/options/) et cliquez sur **Get Support**.</span><span class="sxs-lookup"><span data-stu-id="a3ca3-107">Go toohello [Azure Support site](https://azure.microsoft.com/support/options/) and click **Get Support**.</span></span>

## <a name="symptom"></a><span data-ttu-id="a3ca3-108">Symptôme</span><span class="sxs-lookup"><span data-stu-id="a3ca3-108">Symptom</span></span>
<span data-ttu-id="a3ca3-109">La compression pour votre point de terminaison est activée, mais les fichiers sont renvoyés non compressés.</span><span class="sxs-lookup"><span data-stu-id="a3ca3-109">Compression for your endpoint is enabled, but files are being returned uncompressed.</span></span>

> [!TIP]
> <span data-ttu-id="a3ca3-110">toocheck si vos fichiers sont retournés compressés, vous devez toouse un outil comme [Fiddler](http://www.telerik.com/fiddler) ou de votre navigateur [outils de développement](https://developer.microsoft.com/microsoft-edge/platform/documentation/f12-devtools-guide/).</span><span class="sxs-lookup"><span data-stu-id="a3ca3-110">toocheck whether your files are being returned compressed, you need toouse a tool like [Fiddler](http://www.telerik.com/fiddler) or your browser's [developer tools](https://developer.microsoft.com/microsoft-edge/platform/documentation/f12-devtools-guide/).</span></span>  <span data-ttu-id="a3ca3-111">En-têtes de réponse HTTP de hello vérification retournée avec votre mise en cache CDN contenus.</span><span class="sxs-lookup"><span data-stu-id="a3ca3-111">Check hello HTTP response headers returned with your cached CDN content.</span></span>  <span data-ttu-id="a3ca3-112">S’il existe un en-tête nommé `Content-Encoding` avec une valeur **gzip**, **bzip2**, ou **deflate**, votre contenu est compressé.</span><span class="sxs-lookup"><span data-stu-id="a3ca3-112">If there is a header named `Content-Encoding` with a value of **gzip**, **bzip2**, or **deflate**, your content is compressed.</span></span>
> 
> ![En-tête d’encodage de contenu](./media/cdn-troubleshoot-compression/cdn-content-header.png)
> 
> 

## <a name="cause"></a><span data-ttu-id="a3ca3-114">Cause :</span><span class="sxs-lookup"><span data-stu-id="a3ca3-114">Cause</span></span>
<span data-ttu-id="a3ca3-115">Il existe plusieurs causes possibles, y compris :</span><span class="sxs-lookup"><span data-stu-id="a3ca3-115">There are several possible causes, including:</span></span>

* <span data-ttu-id="a3ca3-116">Hello a demandé le contenu n’est pas éligible pour la compression.</span><span class="sxs-lookup"><span data-stu-id="a3ca3-116">hello requested content is not eligible for compression.</span></span>
* <span data-ttu-id="a3ca3-117">La compression n’est pas activée pour hello type de fichier demandé.</span><span class="sxs-lookup"><span data-stu-id="a3ca3-117">Compression is not enabled for hello requested file type.</span></span>
* <span data-ttu-id="a3ca3-118">requête HTTP de Hello n’incluait pas un en-tête de demande d’un type de compression valide.</span><span class="sxs-lookup"><span data-stu-id="a3ca3-118">hello HTTP request did not include a header requesting a valid compression type.</span></span>

## <a name="troubleshooting-steps"></a><span data-ttu-id="a3ca3-119">Étapes de dépannage</span><span class="sxs-lookup"><span data-stu-id="a3ca3-119">Troubleshooting steps</span></span>
> [!TIP]
> <span data-ttu-id="a3ca3-120">Comme avec le déploiement de nouveaux points de terminaison CDN les modifications de configuration prennent certaines toopropagate de temps via le réseau de hello.</span><span class="sxs-lookup"><span data-stu-id="a3ca3-120">As with deploying new endpoints, CDN configuration changes take some time toopropagate through hello network.</span></span>  <span data-ttu-id="a3ca3-121">En règle générale, les modifications sont appliquées dans les 90 minutes.</span><span class="sxs-lookup"><span data-stu-id="a3ca3-121">Usually, changes are applied within 90 minutes.</span></span>  <span data-ttu-id="a3ca3-122">S’il s’agit hello première fois que vous avez configuré la compression pour votre point de terminaison CDN, vous devez envisager d’attente toobe 1 et 2 heures que la propagation des paramètres de compression de hello toohello POP.</span><span class="sxs-lookup"><span data-stu-id="a3ca3-122">If this is hello first time you've set up compression for your CDN endpoint, you should consider waiting 1-2 hours toobe sure hello compression settings have propagated toohello POPs.</span></span> 
> 
> 

### <a name="verify-hello-request"></a><span data-ttu-id="a3ca3-123">Vérifiez que la demande de hello</span><span class="sxs-lookup"><span data-stu-id="a3ca3-123">Verify hello request</span></span>
<span data-ttu-id="a3ca3-124">Tout d’abord, nous devons effectuer une vérification de validité rapide à la demande de hello.</span><span class="sxs-lookup"><span data-stu-id="a3ca3-124">First, we should do a quick sanity check on hello request.</span></span>  <span data-ttu-id="a3ca3-125">Vous pouvez utiliser votre navigateur [outils de développement](https://developer.microsoft.com/microsoft-edge/platform/documentation/f12-devtools-guide/) tooview hello des demandes en cours.</span><span class="sxs-lookup"><span data-stu-id="a3ca3-125">You can use your browser's [developer tools](https://developer.microsoft.com/microsoft-edge/platform/documentation/f12-devtools-guide/) tooview hello requests being made.</span></span>

* <span data-ttu-id="a3ca3-126">Vérifiez la demande de hello est envoyé URL de point de terminaison tooyour, `<endpointname>.azureedge.net`et pas votre origine.</span><span class="sxs-lookup"><span data-stu-id="a3ca3-126">Verify hello request is being sent tooyour endpoint URL, `<endpointname>.azureedge.net`, and not your origin.</span></span>
* <span data-ttu-id="a3ca3-127">Vérifiez que la demande hello contient un **Accept-Encoding** en-tête et hello valeur pour cet en-tête contient **gzip**, **deflate**, ou **bzip2** .</span><span class="sxs-lookup"><span data-stu-id="a3ca3-127">Verify hello request contains an **Accept-Encoding** header, and hello value for that header contains **gzip**, **deflate**, or **bzip2**.</span></span>

> [!NOTE]
> <span data-ttu-id="a3ca3-128">Les profils du **CDN Azure fourni par Akamai** prennent uniquement en charge l’encodage **gzip**.</span><span class="sxs-lookup"><span data-stu-id="a3ca3-128">**Azure CDN from Akamai** profiles only support **gzip** encoding.</span></span>
> 
> 

![En-têtes de requête CDN](./media/cdn-troubleshoot-compression/cdn-request-headers.png)

### <a name="verify-compression-settings-standard-cdn-profile"></a><span data-ttu-id="a3ca3-130">Vérifier les paramètres de compression (profil CDN Standard)</span><span class="sxs-lookup"><span data-stu-id="a3ca3-130">Verify compression settings (Standard CDN profile)</span></span>
> [!NOTE]
> <span data-ttu-id="a3ca3-131">Cette étape s’applique uniquement si votre profil CDN est un profil du **CDN Azure Standard fourni par Verizon** ou du **CDN Azure Standard fourni par Akamai**.</span><span class="sxs-lookup"><span data-stu-id="a3ca3-131">This step only applies if your CDN profile is an **Azure CDN Standard from Verizon** or **Azure CDN Standard from Akamai** profile.</span></span> 
> 
> 

<span data-ttu-id="a3ca3-132">Accédez de point de terminaison tooyour Bonjour [portail Azure](https://portal.azure.com) et cliquez sur hello **configurer** bouton.</span><span class="sxs-lookup"><span data-stu-id="a3ca3-132">Navigate tooyour endpoint in hello [Azure portal](https://portal.azure.com) and click hello **Configure** button.</span></span>

* <span data-ttu-id="a3ca3-133">Vérifiez que la compression est activée.</span><span class="sxs-lookup"><span data-stu-id="a3ca3-133">Verify compression is enabled.</span></span>
* <span data-ttu-id="a3ca3-134">Vérifiez le type MIME de hello pour hello contenu toobe compressé est inclus dans la liste hello des formats compressés.</span><span class="sxs-lookup"><span data-stu-id="a3ca3-134">Verify hello MIME type for hello content toobe compressed is included in hello list of compressed formats.</span></span>

![Paramètres de compression CDN](./media/cdn-troubleshoot-compression/cdn-compression-settings.png)

### <a name="verify-compression-settings-premium-cdn-profile"></a><span data-ttu-id="a3ca3-136">Vérifier les paramètres de compression (profil CDN Premium)</span><span class="sxs-lookup"><span data-stu-id="a3ca3-136">Verify compression settings (Premium CDN profile)</span></span>
> [!NOTE]
> <span data-ttu-id="a3ca3-137">Cette étape s’applique uniquement si votre profil CDN est un profil du **CDN Azure Premium fourni par Verizon** .</span><span class="sxs-lookup"><span data-stu-id="a3ca3-137">This step only applies if your CDN profile is an **Azure CDN Premium from Verizon** profile.</span></span>
> 
> 

<span data-ttu-id="a3ca3-138">Accédez de point de terminaison tooyour Bonjour [portail Azure](https://portal.azure.com) et cliquez sur hello **gérer** bouton.</span><span class="sxs-lookup"><span data-stu-id="a3ca3-138">Navigate tooyour endpoint in hello [Azure portal](https://portal.azure.com) and click hello **Manage** button.</span></span>  <span data-ttu-id="a3ca3-139">portail supplémentaire du Hello s’ouvre.</span><span class="sxs-lookup"><span data-stu-id="a3ca3-139">hello supplemental portal will open.</span></span>  <span data-ttu-id="a3ca3-140">Pointage hello **grand HTTP** tab, puis pointez sur hello **paramètres de Cache** menu volant.</span><span class="sxs-lookup"><span data-stu-id="a3ca3-140">Hover over hello **HTTP Large** tab, then hover over hello **Cache Settings** flyout.</span></span>  <span data-ttu-id="a3ca3-141">Cliquez sur **Compression**.</span><span class="sxs-lookup"><span data-stu-id="a3ca3-141">Click **Compression**.</span></span> 

* <span data-ttu-id="a3ca3-142">Vérifiez que la compression est activée.</span><span class="sxs-lookup"><span data-stu-id="a3ca3-142">Verify compression is enabled.</span></span>
* <span data-ttu-id="a3ca3-143">Vérifiez que hello **Types de fichiers** liste contient une liste séparée par des virgules (sans espaces) des types MIME.</span><span class="sxs-lookup"><span data-stu-id="a3ca3-143">Verify hello **File Types** list contains a comma-separated list (no spaces) of MIME types.</span></span>
* <span data-ttu-id="a3ca3-144">Vérifiez le type MIME de hello pour hello contenu toobe compressé est inclus dans la liste hello des formats compressés.</span><span class="sxs-lookup"><span data-stu-id="a3ca3-144">Verify hello MIME type for hello content toobe compressed is included in hello list of compressed formats.</span></span>

![Paramètres de compression Premium CDN](./media/cdn-troubleshoot-compression/cdn-compression-settings-premium.png)

### <a name="verify-hello-content-is-cached"></a><span data-ttu-id="a3ca3-146">Vérifiez le contenu de hello est mis en cache.</span><span class="sxs-lookup"><span data-stu-id="a3ca3-146">Verify hello content is cached</span></span>
> [!NOTE]
> <span data-ttu-id="a3ca3-147">Cette étape vaut uniquement si votre profil CDN est un profil du **CDN Azure fourni par Verizon** (Standard ou Premium).</span><span class="sxs-lookup"><span data-stu-id="a3ca3-147">This step only applies if your CDN profile is an **Azure CDN from Verizon** profile (Standard or Premium).</span></span>
> 
> 

<span data-ttu-id="a3ca3-148">À l’aide des outils de développement de votre navigateur, vérifiez le fichier hello tooensure hello réponse en-têtes est mis en cache dans une région de hello où elle est demandée.</span><span class="sxs-lookup"><span data-stu-id="a3ca3-148">Using your browser's developer tools, check hello response headers tooensure hello file is cached in hello region where it is being requested.</span></span>

* <span data-ttu-id="a3ca3-149">Vérifiez hello **Server** en-tête de réponse.</span><span class="sxs-lookup"><span data-stu-id="a3ca3-149">Check hello **Server** response header.</span></span>  <span data-ttu-id="a3ca3-150">l’en-tête Hello doit avoir le format de hello **plateforme (ID de serveur/POP)**, comme dans hello l’exemple suivant.</span><span class="sxs-lookup"><span data-stu-id="a3ca3-150">hello header should have hello format **Platform (POP/Server ID)**, as seen in hello following example.</span></span>
* <span data-ttu-id="a3ca3-151">Vérifiez hello **X-Cache** en-tête de réponse.</span><span class="sxs-lookup"><span data-stu-id="a3ca3-151">Check hello **X-Cache** response header.</span></span>  <span data-ttu-id="a3ca3-152">Hello en-tête doit indiquer **atteint**.</span><span class="sxs-lookup"><span data-stu-id="a3ca3-152">hello header should read **HIT**.</span></span>  

![En-têtes de réponse CDN](./media/cdn-troubleshoot-compression/cdn-response-headers.png)

### <a name="verify-hello-file-meets-hello-size-requirements"></a><span data-ttu-id="a3ca3-154">Vérifiez le fichier de hello répond aux exigences de taille hello</span><span class="sxs-lookup"><span data-stu-id="a3ca3-154">Verify hello file meets hello size requirements</span></span>
> [!NOTE]
> <span data-ttu-id="a3ca3-155">Cette étape vaut uniquement si votre profil CDN est un profil du **CDN Azure fourni par Verizon** (Standard ou Premium).</span><span class="sxs-lookup"><span data-stu-id="a3ca3-155">This step only applies if your CDN profile is an **Azure CDN from Verizon** profile (Standard or Premium).</span></span>
> 
> 

<span data-ttu-id="a3ca3-156">toobe éligible pour la compression, un fichier doit satisfaire hello suivant les exigences de taille :</span><span class="sxs-lookup"><span data-stu-id="a3ca3-156">toobe eligible for compression, a file must meet hello following size requirements:</span></span>

* <span data-ttu-id="a3ca3-157">Plus de 128 octets.</span><span class="sxs-lookup"><span data-stu-id="a3ca3-157">Larger than 128 bytes.</span></span>
* <span data-ttu-id="a3ca3-158">Moins de 1 Mo.</span><span class="sxs-lookup"><span data-stu-id="a3ca3-158">Smaller than 1 MB.</span></span>

### <a name="check-hello-request-at-hello-origin-server-for-a-via-header"></a><span data-ttu-id="a3ca3-159">Vérifiez la demande hello sur le serveur d’origine hello pour un **Via** en-tête</span><span class="sxs-lookup"><span data-stu-id="a3ca3-159">Check hello request at hello origin server for a **Via** header</span></span>
<span data-ttu-id="a3ca3-160">Hello **Via** en-tête HTTP indique au serveur web toohello qui hello demande est passé par un serveur proxy.</span><span class="sxs-lookup"><span data-stu-id="a3ca3-160">hello **Via** HTTP header indicates toohello web server that hello request is being passed by a proxy server.</span></span>  <span data-ttu-id="a3ca3-161">Par défaut des serveurs web Microsoft IIS ne pas compresser les réponses lors de la demande de hello contient un **Via** en-tête.</span><span class="sxs-lookup"><span data-stu-id="a3ca3-161">Microsoft IIS web servers by default do not compress responses when hello request contains a **Via** header.</span></span>  <span data-ttu-id="a3ca3-162">toooverride ce comportement, hello suivants :</span><span class="sxs-lookup"><span data-stu-id="a3ca3-162">toooverride this behavior, perform hello following:</span></span>

* <span data-ttu-id="a3ca3-163">**IIS 6**: [HcNoCompressionForProxies de définir = « FALSE » dans les propriétés de la métabase IIS hello](https://msdn.microsoft.com/library/ms525390.aspx)</span><span class="sxs-lookup"><span data-stu-id="a3ca3-163">**IIS 6**: [Set HcNoCompressionForProxies="FALSE" in hello IIS Metabase properties](https://msdn.microsoft.com/library/ms525390.aspx)</span></span>
* <span data-ttu-id="a3ca3-164">**IIS 7 et**: [définissez à la fois **noCompressionForHttp10** et **noCompressionForProxies** tooFalse de configuration du serveur hello](http://www.iis.net/configreference/system.webserver/httpcompression)</span><span class="sxs-lookup"><span data-stu-id="a3ca3-164">**IIS 7 and up**: [Set both **noCompressionForHttp10** and **noCompressionForProxies** tooFalse in hello server configuration](http://www.iis.net/configreference/system.webserver/httpcompression)</span></span>

