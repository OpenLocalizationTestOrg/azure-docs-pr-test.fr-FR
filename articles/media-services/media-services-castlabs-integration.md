---
title: aaaUsing castLabs toodeliver Widevine licences tooAzure Media Services | Documents Microsoft
description: "Cet article décrit comment vous pouvez utiliser Azure Media Services (AMS) toodeliver un flux qui est chiffré dynamiquement par AMS avec PlayReady et Widevine DRMs. la licence PlayReady Hello est fourni à partir du serveur de licences PlayReady de Media Services et les licences Widevine sont remis par le serveur de licences castLabs."
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
ms.openlocfilehash: 80d2778fb283a96361e7e511990a36c2f551a310
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="using-castlabs-toodeliver-widevine-licenses-tooazure-media-services"></a><span data-ttu-id="e9fc0-104">À l’aide de tooAzure de licences Widevine castLabs toodeliver Media Services</span><span class="sxs-lookup"><span data-stu-id="e9fc0-104">Using castLabs toodeliver Widevine licenses tooAzure Media Services</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="e9fc0-105">Axinom</span><span class="sxs-lookup"><span data-stu-id="e9fc0-105">Axinom</span></span>](media-services-axinom-integration.md)
> * [<span data-ttu-id="e9fc0-106">castLabs</span><span class="sxs-lookup"><span data-stu-id="e9fc0-106">castLabs</span></span>](media-services-castlabs-integration.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="e9fc0-107">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="e9fc0-107">Overview</span></span>
<span data-ttu-id="e9fc0-108">Cet article décrit comment vous pouvez utiliser Azure Media Services (AMS) toodeliver un flux qui est chiffré dynamiquement par AMS avec PlayReady et Widevine DRMs.</span><span class="sxs-lookup"><span data-stu-id="e9fc0-108">This article describes how you can use Azure Media Services (AMS) toodeliver a stream that is dynamically encrypted by AMS with both PlayReady and Widevine DRMs.</span></span> <span data-ttu-id="e9fc0-109">la licence PlayReady Hello est fourni à partir du serveur de licences PlayReady de Media Services et les licences Widevine sont remis par **castLabs** serveur de licences.</span><span class="sxs-lookup"><span data-stu-id="e9fc0-109">hello PlayReady license comes from Media Services PlayReady license server and Widevine license is delivered by **castLabs** license server.</span></span>

<span data-ttu-id="e9fc0-110">tooplayback de diffusion en continu de contenu protégé par CENC (PlayReady et/ou Widevine), vous pouvez utiliser [Azure Media Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html).</span><span class="sxs-lookup"><span data-stu-id="e9fc0-110">tooplayback streaming content protected by CENC (PlayReady and/or Widevine), you can use  [Azure Media Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html).</span></span> <span data-ttu-id="e9fc0-111">Pour plus d’informations, consultez le [document AMP](http://amp.azure.net/libs/amp/latest/docs/) .</span><span class="sxs-lookup"><span data-stu-id="e9fc0-111">See [AMP document](http://amp.azure.net/libs/amp/latest/docs/) for details.</span></span>

<span data-ttu-id="e9fc0-112">Hello suivant schéma montre une architecture d’intégration Azure Media Services et castLabs globale.</span><span class="sxs-lookup"><span data-stu-id="e9fc0-112">hello following diagram demonstrates a high-level Azure Media Services and castLabs integration architecture.</span></span>

![intégration](./media/media-services-castlabs-integration/media-services-castlabs-integration.png)

## <a name="typical-system-set-up"></a><span data-ttu-id="e9fc0-114">Configuration système classique</span><span class="sxs-lookup"><span data-stu-id="e9fc0-114">Typical system set up</span></span>
* <span data-ttu-id="e9fc0-115">Le contenu multimédia est stocké dans AMS.</span><span class="sxs-lookup"><span data-stu-id="e9fc0-115">Media content is stored in AMS.</span></span>
* <span data-ttu-id="e9fc0-116">Les ID des clés de contenu sont stockées à la fois dans castLabs et AMS.</span><span class="sxs-lookup"><span data-stu-id="e9fc0-116">Key IDs of content keys are stored in both castLabs and AMS.</span></span>
* <span data-ttu-id="e9fc0-117">castLabs et AMS intègrent une authentification par jeton.</span><span class="sxs-lookup"><span data-stu-id="e9fc0-117">castLabs and AMS both have token authentication built in.</span></span> <span data-ttu-id="e9fc0-118">Hello les sections suivantes traite des jetons d’authentification.</span><span class="sxs-lookup"><span data-stu-id="e9fc0-118">hello following sections discuss authentication tokens.</span></span> 
* <span data-ttu-id="e9fc0-119">Lorsqu’un client demande vidéo de hello toostream, hello le contenu est dynamiquement chiffré avec **chiffrement commun** (CENC) et de façon dynamique AMS tooSmooth tiret et diffusion en continu.</span><span class="sxs-lookup"><span data-stu-id="e9fc0-119">When a client requests toostream hello video, hello content is dynamically encrypted with **Common Encryption** (CENC) and dynamically packaged by AMS tooSmooth Streaming and DASH.</span></span> <span data-ttu-id="e9fc0-120">Nous offrons également un chiffrement de flux élémentaire PlayReady M2TS pour le protocole de diffusion en continu HLS.</span><span class="sxs-lookup"><span data-stu-id="e9fc0-120">We also deliver PlayReady M2TS elementary stream encryption for HLS streaming protocol.</span></span>
* <span data-ttu-id="e9fc0-121">La licence PlayReady est récupérée auprès du serveur de licences AMS et licence Widevine est récupérée auprès du serveur de licences castLabs.</span><span class="sxs-lookup"><span data-stu-id="e9fc0-121">PlayReady license is retrieved from AMS license server and Widevine license is retrieved from castLabs license server.</span></span> 
* <span data-ttu-id="e9fc0-122">Media Player décide automatiquement le toofetch de licence en fonction de la capacité de plate-forme client hello.</span><span class="sxs-lookup"><span data-stu-id="e9fc0-122">Media Player automatically decides which license toofetch based on hello client platform capability.</span></span> 

## <a name="authentication-token-generation-for-getting-a-license"></a><span data-ttu-id="e9fc0-123">Génération de jetons d'authentification pour l'obtention d'une licence</span><span class="sxs-lookup"><span data-stu-id="e9fc0-123">Authentication token generation for getting a license</span></span>
<span data-ttu-id="e9fc0-124">CastLabs et AMS prend en charge de JWT (JSON Web Token) format de jeton utilisée tooauthorize une licence.</span><span class="sxs-lookup"><span data-stu-id="e9fc0-124">Both castLabs and AMS support JWT (JSON Web Token) token format used tooauthorize a license.</span></span> 

### <a name="jwt-token-in-ams"></a><span data-ttu-id="e9fc0-125">Jeton JWT dans AMS</span><span class="sxs-lookup"><span data-stu-id="e9fc0-125">JWT token in AMS</span></span>
<span data-ttu-id="e9fc0-126">Hello tableau suivant décrit le jeton JWT dans AMS.</span><span class="sxs-lookup"><span data-stu-id="e9fc0-126">hello following table describes JWT token in AMS.</span></span> 

| <span data-ttu-id="e9fc0-127">Émetteur</span><span class="sxs-lookup"><span data-stu-id="e9fc0-127">Issuer</span></span> | <span data-ttu-id="e9fc0-128">Chaîne de l’émetteur hello choisi Service (jeton de sécurité)</span><span class="sxs-lookup"><span data-stu-id="e9fc0-128">Issuer string from hello chosen Secure Token Service (STS)</span></span> |
| --- | --- |
| <span data-ttu-id="e9fc0-129">Public ciblé</span><span class="sxs-lookup"><span data-stu-id="e9fc0-129">Audience</span></span> |<span data-ttu-id="e9fc0-130">Chaîne d’audience à partir de hello utilisé STS</span><span class="sxs-lookup"><span data-stu-id="e9fc0-130">Audience string from hello used STS</span></span> |
| <span data-ttu-id="e9fc0-131">Revendications</span><span class="sxs-lookup"><span data-stu-id="e9fc0-131">Claims</span></span> |<span data-ttu-id="e9fc0-132">Ensemble de revendications</span><span class="sxs-lookup"><span data-stu-id="e9fc0-132">A set of claims</span></span> |
| <span data-ttu-id="e9fc0-133">NotBefore</span><span class="sxs-lookup"><span data-stu-id="e9fc0-133">NotBefore</span></span> |<span data-ttu-id="e9fc0-134">Démarrer la validité du jeton de hello</span><span class="sxs-lookup"><span data-stu-id="e9fc0-134">Start validity of hello token</span></span> |
| <span data-ttu-id="e9fc0-135">Expires</span><span class="sxs-lookup"><span data-stu-id="e9fc0-135">Expires</span></span> |<span data-ttu-id="e9fc0-136">Validité de fin du jeton de hello</span><span class="sxs-lookup"><span data-stu-id="e9fc0-136">End validity of hello token</span></span> |
| <span data-ttu-id="e9fc0-137">SigningCredentials</span><span class="sxs-lookup"><span data-stu-id="e9fc0-137">SigningCredentials</span></span> |<span data-ttu-id="e9fc0-138">clé Hello qui est partagé entre le serveur de licences PlayReady, castLabs serveur de licences et STS, il peut être la clé symétrique ou asymétrique.</span><span class="sxs-lookup"><span data-stu-id="e9fc0-138">hello key that is shared among PlayReady License Server, castLabs License Server and STS, it could be either symmetric or asymmetric key.</span></span> |

### <a name="jwt-token-in-castlabs"></a><span data-ttu-id="e9fc0-139">Jeton JWT dans castLabs</span><span class="sxs-lookup"><span data-stu-id="e9fc0-139">JWT token in castLabs</span></span>
<span data-ttu-id="e9fc0-140">Hello tableau suivant décrit le jeton JWT dans castLabs.</span><span class="sxs-lookup"><span data-stu-id="e9fc0-140">hello following table describes JWT token in castLabs.</span></span> 

| <span data-ttu-id="e9fc0-141">Nom</span><span class="sxs-lookup"><span data-stu-id="e9fc0-141">Name</span></span> | <span data-ttu-id="e9fc0-142">Description</span><span class="sxs-lookup"><span data-stu-id="e9fc0-142">Description</span></span> |
| --- | --- |
| <span data-ttu-id="e9fc0-143">optData</span><span class="sxs-lookup"><span data-stu-id="e9fc0-143">optData</span></span> |<span data-ttu-id="e9fc0-144">Chaîne JSON contenant des informations sur vous.</span><span class="sxs-lookup"><span data-stu-id="e9fc0-144">A JSON string containing information about you.</span></span> |
| <span data-ttu-id="e9fc0-145">crt</span><span class="sxs-lookup"><span data-stu-id="e9fc0-145">crt</span></span> |<span data-ttu-id="e9fc0-146">Une JSON chaîne contenant des informations sur les actifs de hello, ses droits de lecture et les informations de licence.</span><span class="sxs-lookup"><span data-stu-id="e9fc0-146">A JSON string containing information about hello asset, its license info and playback rights.</span></span> |
| <span data-ttu-id="e9fc0-147">iat</span><span class="sxs-lookup"><span data-stu-id="e9fc0-147">iat</span></span> |<span data-ttu-id="e9fc0-148">Hello date/heure actuelle dans une époque déterminée.</span><span class="sxs-lookup"><span data-stu-id="e9fc0-148">hello current datetime in epoch.</span></span> |
| <span data-ttu-id="e9fc0-149">jti</span><span class="sxs-lookup"><span data-stu-id="e9fc0-149">jti</span></span> |<span data-ttu-id="e9fc0-150">Un identificateur unique sur ce jeton (chaque jeton peut uniquement servir une fois dans le système de castLabs hello).</span><span class="sxs-lookup"><span data-stu-id="e9fc0-150">A unique identifier about this token (every token can only be used once in hello castLabs system).</span></span> |

## <a name="sample-solution-set-up"></a><span data-ttu-id="e9fc0-151">Exemple de configuration de solution</span><span class="sxs-lookup"><span data-stu-id="e9fc0-151">Sample solution set up</span></span>
<span data-ttu-id="e9fc0-152">Hello [exemple de solution](https://github.com/AzureMediaServicesSamples/CastlabsIntegration) se compose de deux projets :</span><span class="sxs-lookup"><span data-stu-id="e9fc0-152">hello [sample solution](https://github.com/AzureMediaServicesSamples/CastlabsIntegration) consists of two projects:</span></span>

* <span data-ttu-id="e9fc0-153">Une application console qui peut être des restrictions de DRM tooset utilisé sur un élément multimédia déjà réceptionné, PlayReady et Widevine.</span><span class="sxs-lookup"><span data-stu-id="e9fc0-153">A console app that can be used tooset DRM restrictions on an already ingested asset, for both PlayReady and Widevine.</span></span>
* <span data-ttu-id="e9fc0-154">Une application web qui délivre les jetons, qui peut être considérée comme une version TRÈS SIMPLIFIÉE d'un STS.</span><span class="sxs-lookup"><span data-stu-id="e9fc0-154">A Web Application that hands out tokens, which could be seen as a VERY SIMPLIFIED version of an STS.</span></span>

<span data-ttu-id="e9fc0-155">application de console toouse hello :</span><span class="sxs-lookup"><span data-stu-id="e9fc0-155">toouse hello console application:</span></span>

1. <span data-ttu-id="e9fc0-156">Modifier les informations d’identification de hello app.config toosetup AMS, informations d’identification castLabs, configuration du service STS et une clé partagée.</span><span class="sxs-lookup"><span data-stu-id="e9fc0-156">Change hello app.config toosetup AMS credentials, castLabs credentials, STS configuration and shared key.</span></span>
2. <span data-ttu-id="e9fc0-157">Téléchargez un élément multimédia dans AMS.</span><span class="sxs-lookup"><span data-stu-id="e9fc0-157">Upload an Asset into AMS.</span></span>
3. <span data-ttu-id="e9fc0-158">Get hello UUID de hello téléchargé Asset et modifiez 32 de ligne dans le fichier Program.cs de hello :</span><span class="sxs-lookup"><span data-stu-id="e9fc0-158">Get hello UUID from hello uploaded Asset, and change Line 32 in hello Program.cs file:</span></span>
   
      <span data-ttu-id="e9fc0-159">var objIAsset = _context.Assets.Where(x => x.Id == "nb:cid:UUID:dac53a5d-1500-80bd-b864-f1e4b62594cf").FirstOrDefault();</span><span class="sxs-lookup"><span data-stu-id="e9fc0-159">var objIAsset = _context.Assets.Where(x => x.Id == "nb:cid:UUID:dac53a5d-1500-80bd-b864-f1e4b62594cf").FirstOrDefault();</span></span>
4. <span data-ttu-id="e9fc0-160">Utiliser un AssetId pour nommer des ressources de hello dans le système de castLabs hello (44 de ligne dans le fichier Program.cs de hello).</span><span class="sxs-lookup"><span data-stu-id="e9fc0-160">Use an AssetId for naming hello asset in hello castLabs system (Line 44 in hello Program.cs file).</span></span>
   
   <span data-ttu-id="e9fc0-161">Vous devez définir AssetId pour **castLabs**; il doit toobe une chaîne alphanumérique unique.</span><span class="sxs-lookup"><span data-stu-id="e9fc0-161">You must set AssetId for **castLabs**; it needs toobe a unique alphanumeric string.</span></span>
5. <span data-ttu-id="e9fc0-162">Exécutez le programme de hello.</span><span class="sxs-lookup"><span data-stu-id="e9fc0-162">Run hello program.</span></span>

<span data-ttu-id="e9fc0-163">toouse hello Web Application (STS) :</span><span class="sxs-lookup"><span data-stu-id="e9fc0-163">toouse hello Web Application (STS):</span></span>

1. <span data-ttu-id="e9fc0-164">Vendeur de modification hello web.config toosetup castlabs ID, configuration du service STS hello et la clé partagée de hello.</span><span class="sxs-lookup"><span data-stu-id="e9fc0-164">Change hello web.config toosetup castlabs merchant ID, hello STS configuration and hello shared key.</span></span>
2. <span data-ttu-id="e9fc0-165">Déployer tooAzure sites Web.</span><span class="sxs-lookup"><span data-stu-id="e9fc0-165">Deploy tooAzure Websites.</span></span>
3. <span data-ttu-id="e9fc0-166">Accédez du site Web toohello.</span><span class="sxs-lookup"><span data-stu-id="e9fc0-166">Navigate toohello website.</span></span>

## <a name="playing-back-a-video"></a><span data-ttu-id="e9fc0-167">Lecture d'une vidéo</span><span class="sxs-lookup"><span data-stu-id="e9fc0-167">Playing back a video</span></span>
<span data-ttu-id="e9fc0-168">tooplayback une vidéo chiffrées avec un chiffrement commun (PlayReady et/ou Widevine), vous pouvez utiliser hello [Azure Media Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html).</span><span class="sxs-lookup"><span data-stu-id="e9fc0-168">tooplayback a video encrypted with common encryption (PlayReady and/or Widevine), you can use hello [Azure Media Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html).</span></span> <span data-ttu-id="e9fc0-169">Lorsque vous exécutez l’application de console hello, hello ID de clé de contenu et hello URL de manifeste sont renvoyées.</span><span class="sxs-lookup"><span data-stu-id="e9fc0-169">When running hello console app, hello Content Key ID and hello Manifest URL are echoed.</span></span>

1. <span data-ttu-id="e9fc0-170">Ouvrez un nouvel onglet et lancez votre STS : http://[nom_sts].azurewebsites.net/api/token/assetid/[id_élément_multimédia_castlabs]/contentkeyid/[id_clé_contenu].</span><span class="sxs-lookup"><span data-stu-id="e9fc0-170">Open a new tab and launch your STS: http://[yourStsName].azurewebsites.net/api/token/assetid/[yourCastLabsAssetId]/contentkeyid/[thecontentkeyid].</span></span>
2. <span data-ttu-id="e9fc0-171">Accédez trop[Azure Media Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html).</span><span class="sxs-lookup"><span data-stu-id="e9fc0-171">Go too[Azure Media Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html).</span></span>
3. <span data-ttu-id="e9fc0-172">Collez hello URL de diffusion en continu.</span><span class="sxs-lookup"><span data-stu-id="e9fc0-172">Paste in hello streaming URL.</span></span>
4. <span data-ttu-id="e9fc0-173">Cliquez sur hello **Options avancées** case à cocher.</span><span class="sxs-lookup"><span data-stu-id="e9fc0-173">Click hello **Advanced Options** checkbox.</span></span>
5. <span data-ttu-id="e9fc0-174">Bonjour **Protection** liste déroulante, sélectionnez PlayReady et/ou Widevine.</span><span class="sxs-lookup"><span data-stu-id="e9fc0-174">In hello **Protection** dropdown, select PlayReady and/or Widevine.</span></span>
6. <span data-ttu-id="e9fc0-175">Collez le jeton hello que vous avez obtenu votre STS dans la zone de texte de jeton hello.</span><span class="sxs-lookup"><span data-stu-id="e9fc0-175">Paste hello token that you got from your STS in hello Token textbox.</span></span> 
   
   <span data-ttu-id="e9fc0-176">serveur de licences Hello castLab n’a pas besoin hello « support = « préfixe devant le jeton de hello.</span><span class="sxs-lookup"><span data-stu-id="e9fc0-176">hello castLab license server does not need hello “Bearer=” prefix in front of hello token.</span></span> <span data-ttu-id="e9fc0-177">Par conséquent, veuillez supprimer avant d’envoyer le jeton de hello.</span><span class="sxs-lookup"><span data-stu-id="e9fc0-177">So please remove that before submitting hello token.</span></span>
7. <span data-ttu-id="e9fc0-178">Mettre à jour le lecteur hello.</span><span class="sxs-lookup"><span data-stu-id="e9fc0-178">Update hello player.</span></span>
8. <span data-ttu-id="e9fc0-179">Hello vidéo doit jouer.</span><span class="sxs-lookup"><span data-stu-id="e9fc0-179">hello video should be playing.</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="e9fc0-180">Parcours d’apprentissage de Media Services</span><span class="sxs-lookup"><span data-stu-id="e9fc0-180">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="e9fc0-181">Fournir des commentaires</span><span class="sxs-lookup"><span data-stu-id="e9fc0-181">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

