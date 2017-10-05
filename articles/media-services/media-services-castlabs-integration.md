---
title: "Utilisation de castLabs pour fournir des licences Widevine à Azure Media Services | Microsoft Docs"
description: "Cet article décrit comment vous pouvez utiliser Azure Media Services (AMS) pour fournir un flux chiffré dynamiquement par AMS avec des DRM PlayReady et Widevine. La licence PlayReady provient du serveur de licences Media Services PlayReady et la licence Widevine est délivrée par le serveur de licences castLabs."
services: media-services
documentationcenter: 
author: Mingfeiy
manager: cfowler
editor: 
ms.assetid: 2a9a408a-a995-49e1-8d8f-ac5b51e17d40
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: Mingfeiy;willzhan;Juliako
ms.openlocfilehash: 5b69e804809f834e81221fb2787a997a52dbe286
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="using-castlabs-to-deliver-widevine-licenses-to-azure-media-services"></a><span data-ttu-id="e65d7-104">Utilisation de castLabs pour fournir des licences Widevine à Azure Media Services</span><span class="sxs-lookup"><span data-stu-id="e65d7-104">Using castLabs to deliver Widevine licenses to Azure Media Services</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="e65d7-105">Axinom</span><span class="sxs-lookup"><span data-stu-id="e65d7-105">Axinom</span></span>](media-services-axinom-integration.md)
> * [<span data-ttu-id="e65d7-106">castLabs</span><span class="sxs-lookup"><span data-stu-id="e65d7-106">castLabs</span></span>](media-services-castlabs-integration.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="e65d7-107">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="e65d7-107">Overview</span></span>
<span data-ttu-id="e65d7-108">Cet article décrit comment vous pouvez utiliser Azure Media Services (AMS) pour fournir un flux chiffré dynamiquement par AMS avec des DRM PlayReady et Widevine.</span><span class="sxs-lookup"><span data-stu-id="e65d7-108">This article describes how you can use Azure Media Services (AMS) to deliver a stream that is dynamically encrypted by AMS with both PlayReady and Widevine DRMs.</span></span> <span data-ttu-id="e65d7-109">La licence PlayReady provient du serveur de licences Media Services PlayReady et la licence Widevine est délivrée par le serveur de licences **castLabs** .</span><span class="sxs-lookup"><span data-stu-id="e65d7-109">The PlayReady license comes from Media Services PlayReady license server and Widevine license is delivered by **castLabs** license server.</span></span>

<span data-ttu-id="e65d7-110">Pour lire un contenu en streaming protégé par CENC (PlayReady et/ou Widevine), vous pouvez utiliser [Azure Media Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html).</span><span class="sxs-lookup"><span data-stu-id="e65d7-110">To playback streaming content protected by CENC (PlayReady and/or Widevine), you can use  [Azure Media Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html).</span></span> <span data-ttu-id="e65d7-111">Pour plus d’informations, consultez le [document AMP](http://amp.azure.net/libs/amp/latest/docs/) .</span><span class="sxs-lookup"><span data-stu-id="e65d7-111">See [AMP document](http://amp.azure.net/libs/amp/latest/docs/) for details.</span></span>

<span data-ttu-id="e65d7-112">Le diagramme suivant représente une architecture qui intègre Azure Media Services et castLabs.</span><span class="sxs-lookup"><span data-stu-id="e65d7-112">The following diagram demonstrates a high-level Azure Media Services and castLabs integration architecture.</span></span>

![intégration](./media/media-services-castlabs-integration/media-services-castlabs-integration.png)

## <a name="typical-system-set-up"></a><span data-ttu-id="e65d7-114">Configuration système classique</span><span class="sxs-lookup"><span data-stu-id="e65d7-114">Typical system set up</span></span>
* <span data-ttu-id="e65d7-115">Le contenu multimédia est stocké dans AMS.</span><span class="sxs-lookup"><span data-stu-id="e65d7-115">Media content is stored in AMS.</span></span>
* <span data-ttu-id="e65d7-116">Les ID des clés de contenu sont stockées à la fois dans castLabs et AMS.</span><span class="sxs-lookup"><span data-stu-id="e65d7-116">Key IDs of content keys are stored in both castLabs and AMS.</span></span>
* <span data-ttu-id="e65d7-117">castLabs et AMS intègrent une authentification par jeton.</span><span class="sxs-lookup"><span data-stu-id="e65d7-117">castLabs and AMS both have token authentication built in.</span></span> <span data-ttu-id="e65d7-118">Les sections suivantes décrivent les jetons d'authentification.</span><span class="sxs-lookup"><span data-stu-id="e65d7-118">The following sections discuss authentication tokens.</span></span> 
* <span data-ttu-id="e65d7-119">Quand un client demande à diffuser en continu la vidéo, le contenu est chiffré dynamiquement par **chiffrement commun** (CENC) et empaqueté dynamiquement par AMS en Smooth Streaming ou DASH.</span><span class="sxs-lookup"><span data-stu-id="e65d7-119">When a client requests to stream the video, the content is dynamically encrypted with **Common Encryption** (CENC) and dynamically packaged by AMS to Smooth Streaming and DASH.</span></span> <span data-ttu-id="e65d7-120">Nous offrons également un chiffrement de flux élémentaire PlayReady M2TS pour le protocole de diffusion en continu HLS.</span><span class="sxs-lookup"><span data-stu-id="e65d7-120">We also deliver PlayReady M2TS elementary stream encryption for HLS streaming protocol.</span></span>
* <span data-ttu-id="e65d7-121">La licence PlayReady est récupérée auprès du serveur de licences AMS et licence Widevine est récupérée auprès du serveur de licences castLabs.</span><span class="sxs-lookup"><span data-stu-id="e65d7-121">PlayReady license is retrieved from AMS license server and Widevine license is retrieved from castLabs license server.</span></span> 
* <span data-ttu-id="e65d7-122">Media Player détermine automatiquement quelles licences récupérer en fonction de la capacité de la plateforme client.</span><span class="sxs-lookup"><span data-stu-id="e65d7-122">Media Player automatically decides which license to fetch based on the client platform capability.</span></span> 

## <a name="authentication-token-generation-for-getting-a-license"></a><span data-ttu-id="e65d7-123">Génération de jetons d'authentification pour l'obtention d'une licence</span><span class="sxs-lookup"><span data-stu-id="e65d7-123">Authentication token generation for getting a license</span></span>
<span data-ttu-id="e65d7-124">AMS et castLabs prennent en charge le format de jeton JWT (jeton web JSON) utilisé pour autoriser une licence.</span><span class="sxs-lookup"><span data-stu-id="e65d7-124">Both castLabs and AMS support JWT (JSON Web Token) token format used to authorize a license.</span></span> 

### <a name="jwt-token-in-ams"></a><span data-ttu-id="e65d7-125">Jeton JWT dans AMS</span><span class="sxs-lookup"><span data-stu-id="e65d7-125">JWT token in AMS</span></span>
<span data-ttu-id="e65d7-126">Le tableau suivant décrit le jeton JWT dans AMS.</span><span class="sxs-lookup"><span data-stu-id="e65d7-126">The following table describes JWT token in AMS.</span></span> 

| <span data-ttu-id="e65d7-127">Émetteur</span><span class="sxs-lookup"><span data-stu-id="e65d7-127">Issuer</span></span> | <span data-ttu-id="e65d7-128">Chaîne d'émetteur issue du service de jeton sécurisé (STS) choisi</span><span class="sxs-lookup"><span data-stu-id="e65d7-128">Issuer string from the chosen Secure Token Service (STS)</span></span> |
| --- | --- |
| <span data-ttu-id="e65d7-129">Public ciblé</span><span class="sxs-lookup"><span data-stu-id="e65d7-129">Audience</span></span> |<span data-ttu-id="e65d7-130">Chaîne de public issue du STS utilisé</span><span class="sxs-lookup"><span data-stu-id="e65d7-130">Audience string from the used STS</span></span> |
| <span data-ttu-id="e65d7-131">Revendications</span><span class="sxs-lookup"><span data-stu-id="e65d7-131">Claims</span></span> |<span data-ttu-id="e65d7-132">Ensemble de revendications</span><span class="sxs-lookup"><span data-stu-id="e65d7-132">A set of claims</span></span> |
| <span data-ttu-id="e65d7-133">NotBefore</span><span class="sxs-lookup"><span data-stu-id="e65d7-133">NotBefore</span></span> |<span data-ttu-id="e65d7-134">Début de validité du jeton</span><span class="sxs-lookup"><span data-stu-id="e65d7-134">Start validity of the token</span></span> |
| <span data-ttu-id="e65d7-135">Expires</span><span class="sxs-lookup"><span data-stu-id="e65d7-135">Expires</span></span> |<span data-ttu-id="e65d7-136">Fin de validité du jeton</span><span class="sxs-lookup"><span data-stu-id="e65d7-136">End validity of the token</span></span> |
| <span data-ttu-id="e65d7-137">SigningCredentials</span><span class="sxs-lookup"><span data-stu-id="e65d7-137">SigningCredentials</span></span> |<span data-ttu-id="e65d7-138">Clé partagée entre le serveur de licences PlayReady, le serveur de licences castLabs et le STS. Elle peut être symétrique ou asymétrique.</span><span class="sxs-lookup"><span data-stu-id="e65d7-138">The key that is shared among PlayReady License Server, castLabs License Server and STS, it could be either symmetric or asymmetric key.</span></span> |

### <a name="jwt-token-in-castlabs"></a><span data-ttu-id="e65d7-139">Jeton JWT dans castLabs</span><span class="sxs-lookup"><span data-stu-id="e65d7-139">JWT token in castLabs</span></span>
<span data-ttu-id="e65d7-140">Le tableau suivant décrit le jeton JWT dans castLabs.</span><span class="sxs-lookup"><span data-stu-id="e65d7-140">The following table describes JWT token in castLabs.</span></span> 

| <span data-ttu-id="e65d7-141">Nom</span><span class="sxs-lookup"><span data-stu-id="e65d7-141">Name</span></span> | <span data-ttu-id="e65d7-142">Description</span><span class="sxs-lookup"><span data-stu-id="e65d7-142">Description</span></span> |
| --- | --- |
| <span data-ttu-id="e65d7-143">optData</span><span class="sxs-lookup"><span data-stu-id="e65d7-143">optData</span></span> |<span data-ttu-id="e65d7-144">Chaîne JSON contenant des informations sur vous.</span><span class="sxs-lookup"><span data-stu-id="e65d7-144">A JSON string containing information about you.</span></span> |
| <span data-ttu-id="e65d7-145">crt</span><span class="sxs-lookup"><span data-stu-id="e65d7-145">crt</span></span> |<span data-ttu-id="e65d7-146">Chaîne JSON contenant des informations sur l'élément multimédia, ses informations de licence et ses droits de lecture.</span><span class="sxs-lookup"><span data-stu-id="e65d7-146">A JSON string containing information about the asset, its license info and playback rights.</span></span> |
| <span data-ttu-id="e65d7-147">iat</span><span class="sxs-lookup"><span data-stu-id="e65d7-147">iat</span></span> |<span data-ttu-id="e65d7-148">Date/heure actuelle de l'époque.</span><span class="sxs-lookup"><span data-stu-id="e65d7-148">The current datetime in epoch.</span></span> |
| <span data-ttu-id="e65d7-149">jti</span><span class="sxs-lookup"><span data-stu-id="e65d7-149">jti</span></span> |<span data-ttu-id="e65d7-150">Identificateur unique relatif à ce jeton (chaque jeton peut être utilisé une seule fois dans le système castLabs).</span><span class="sxs-lookup"><span data-stu-id="e65d7-150">A unique identifier about this token (every token can only be used once in the castLabs system).</span></span> |

## <a name="sample-solution-set-up"></a><span data-ttu-id="e65d7-151">Exemple de configuration de solution</span><span class="sxs-lookup"><span data-stu-id="e65d7-151">Sample solution set up</span></span>
<span data-ttu-id="e65d7-152">L' [exemple de solution](https://github.com/AzureMediaServicesSamples/CastlabsIntegration) se compose de deux projets :</span><span class="sxs-lookup"><span data-stu-id="e65d7-152">The [sample solution](https://github.com/AzureMediaServicesSamples/CastlabsIntegration) consists of two projects:</span></span>

* <span data-ttu-id="e65d7-153">Une application console qui peut être utilisée pour définir des restrictions DRM sur un élément multimédia déjà ingéré, à la fois pour PlayReady et Widevine.</span><span class="sxs-lookup"><span data-stu-id="e65d7-153">A console app that can be used to set DRM restrictions on an already ingested asset, for both PlayReady and Widevine.</span></span>
* <span data-ttu-id="e65d7-154">Une application web qui délivre les jetons, qui peut être considérée comme une version TRÈS SIMPLIFIÉE d'un STS.</span><span class="sxs-lookup"><span data-stu-id="e65d7-154">A Web Application that hands out tokens, which could be seen as a VERY SIMPLIFIED version of an STS.</span></span>

<span data-ttu-id="e65d7-155">Pour utiliser l'application console :</span><span class="sxs-lookup"><span data-stu-id="e65d7-155">To use the console application:</span></span>

1. <span data-ttu-id="e65d7-156">Modifiez le fichier app.config pour configurer les informations d'identification AMS, les informations d'identification castLabs, la configuration du STS et la clé partagée.</span><span class="sxs-lookup"><span data-stu-id="e65d7-156">Change the app.config to setup AMS credentials, castLabs credentials, STS configuration and shared key.</span></span>
2. <span data-ttu-id="e65d7-157">Téléchargez un élément multimédia dans AMS.</span><span class="sxs-lookup"><span data-stu-id="e65d7-157">Upload an Asset into AMS.</span></span>
3. <span data-ttu-id="e65d7-158">Obtenez l'UUID de l'élément multimédia téléchargé et modifiez la ligne 32 dans le fichier Program.cs :</span><span class="sxs-lookup"><span data-stu-id="e65d7-158">Get the UUID from the uploaded Asset, and change Line 32 in the Program.cs file:</span></span>
   
      <span data-ttu-id="e65d7-159">var objIAsset = _context.Assets.Where(x => x.Id == "nb:cid:UUID:dac53a5d-1500-80bd-b864-f1e4b62594cf").FirstOrDefault();</span><span class="sxs-lookup"><span data-stu-id="e65d7-159">var objIAsset = _context.Assets.Where(x => x.Id == "nb:cid:UUID:dac53a5d-1500-80bd-b864-f1e4b62594cf").FirstOrDefault();</span></span>
4. <span data-ttu-id="e65d7-160">Utilisez un AssetId pour nommer l'élément multimédia dans le système castLabs (ligne 44 dans le fichier Program.cs).</span><span class="sxs-lookup"><span data-stu-id="e65d7-160">Use an AssetId for naming the asset in the castLabs system (Line 44 in the Program.cs file).</span></span>
   
   <span data-ttu-id="e65d7-161">Vous devez définir AssetId pour **castLabs**; il doit s'agir d'une chaîne alphanumérique unique.</span><span class="sxs-lookup"><span data-stu-id="e65d7-161">You must set AssetId for **castLabs**; it needs to be a unique alphanumeric string.</span></span>
5. <span data-ttu-id="e65d7-162">Exécutez le programme.</span><span class="sxs-lookup"><span data-stu-id="e65d7-162">Run the program.</span></span>

<span data-ttu-id="e65d7-163">Pour utiliser l'application web (STS) :</span><span class="sxs-lookup"><span data-stu-id="e65d7-163">To use the Web Application (STS):</span></span>

1. <span data-ttu-id="e65d7-164">Modifiez le fichier web.config pour configurer l'ID du prestataire castlabs, le STS et la clé partagée.</span><span class="sxs-lookup"><span data-stu-id="e65d7-164">Change the web.config to setup castlabs merchant ID, the STS configuration and the shared key.</span></span>
2. <span data-ttu-id="e65d7-165">Déployez-le sur des sites web Azure.</span><span class="sxs-lookup"><span data-stu-id="e65d7-165">Deploy to Azure Websites.</span></span>
3. <span data-ttu-id="e65d7-166">Accédez au site web.</span><span class="sxs-lookup"><span data-stu-id="e65d7-166">Navigate to the website.</span></span>

## <a name="playing-back-a-video"></a><span data-ttu-id="e65d7-167">Lecture d'une vidéo</span><span class="sxs-lookup"><span data-stu-id="e65d7-167">Playing back a video</span></span>
<span data-ttu-id="e65d7-168">Pour lire une vidéo chiffrée par chiffrement commun (PlayReady et/ou Widevine), vous pouvez utiliser [Azure Media Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html).</span><span class="sxs-lookup"><span data-stu-id="e65d7-168">To playback a video encrypted with common encryption (PlayReady and/or Widevine), you can use the [Azure Media Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html).</span></span> <span data-ttu-id="e65d7-169">Pendant l'exécution de l'application console, l'ID de la clé de contenu et l'URL du manifeste sont renvoyés.</span><span class="sxs-lookup"><span data-stu-id="e65d7-169">When running the console app, the Content Key ID and the Manifest URL are echoed.</span></span>

1. <span data-ttu-id="e65d7-170">Ouvrez un nouvel onglet et lancez votre STS : http://[nom_sts].azurewebsites.net/api/token/assetid/[id_élément_multimédia_castlabs]/contentkeyid/[id_clé_contenu].</span><span class="sxs-lookup"><span data-stu-id="e65d7-170">Open a new tab and launch your STS: http://[yourStsName].azurewebsites.net/api/token/assetid/[yourCastLabsAssetId]/contentkeyid/[thecontentkeyid].</span></span>
2. <span data-ttu-id="e65d7-171">Accédez à [Azure Media Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html).</span><span class="sxs-lookup"><span data-stu-id="e65d7-171">Go to [Azure Media Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html).</span></span>
3. <span data-ttu-id="e65d7-172">Collez l'URL de diffusion en continu.</span><span class="sxs-lookup"><span data-stu-id="e65d7-172">Paste in the streaming URL.</span></span>
4. <span data-ttu-id="e65d7-173">Cochez la case **Options avancées** .</span><span class="sxs-lookup"><span data-stu-id="e65d7-173">Click the **Advanced Options** checkbox.</span></span>
5. <span data-ttu-id="e65d7-174">Dans la liste déroulante **Protection** , sélectionnez PlayReady et/ou Widevine.</span><span class="sxs-lookup"><span data-stu-id="e65d7-174">In the **Protection** dropdown, select PlayReady and/or Widevine.</span></span>
6. <span data-ttu-id="e65d7-175">Collez le jeton que vous avez obtenu de votre STS dans la zone de texte Jeton.</span><span class="sxs-lookup"><span data-stu-id="e65d7-175">Paste the token that you got from your STS in the Token textbox.</span></span> 
   
   <span data-ttu-id="e65d7-176">Le serveur de licences castLab n'a pas besoin du préfixe « Bearer= » devant le jeton.</span><span class="sxs-lookup"><span data-stu-id="e65d7-176">The castLab license server does not need the “Bearer=” prefix in front of the token.</span></span> <span data-ttu-id="e65d7-177">Par conséquent, supprimez-le avant d'envoyer le jeton.</span><span class="sxs-lookup"><span data-stu-id="e65d7-177">So please remove that before submitting the token.</span></span>
7. <span data-ttu-id="e65d7-178">Mettez à jour le lecteur.</span><span class="sxs-lookup"><span data-stu-id="e65d7-178">Update the player.</span></span>
8. <span data-ttu-id="e65d7-179">La vidéo doit pouvoir être lue.</span><span class="sxs-lookup"><span data-stu-id="e65d7-179">The video should be playing.</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="e65d7-180">Parcours d’apprentissage de Media Services</span><span class="sxs-lookup"><span data-stu-id="e65d7-180">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="e65d7-181">Fournir des commentaires</span><span class="sxs-lookup"><span data-stu-id="e65d7-181">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

