---
title: "  Publier du contenu avec le Portail Azure | Microsoft Docs"
description: "Ce didacticiel vous guide à travers les étapes de publication de votre contenu avec le Portail Azure."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 92c364eb-5a5f-4f4e-8816-b162c031bb40
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/07/2017
ms.author: juliako
ms.openlocfilehash: 68a2fbdda0996cf4ba5ea3b09816bf845af756f4
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="publish-content-with-the-azure-portal"></a><span data-ttu-id="aee44-103">Publier du contenu avec le Portail Azure</span><span class="sxs-lookup"><span data-stu-id="aee44-103">Publish content with the Azure portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="aee44-104">Portail</span><span class="sxs-lookup"><span data-stu-id="aee44-104">Portal</span></span>](media-services-portal-publish.md)
> * [<span data-ttu-id="aee44-105">.NET</span><span class="sxs-lookup"><span data-stu-id="aee44-105">.NET</span></span>](media-services-deliver-streaming-content.md)
> * [<span data-ttu-id="aee44-106">REST</span><span class="sxs-lookup"><span data-stu-id="aee44-106">REST</span></span>](media-services-rest-deliver-streaming-content.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="aee44-107">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="aee44-107">Overview</span></span>
> [!NOTE]
> <span data-ttu-id="aee44-108">Pour suivre ce didacticiel, vous avez besoin d'un compte Azure.</span><span class="sxs-lookup"><span data-stu-id="aee44-108">To complete this tutorial, you need an Azure account.</span></span> <span data-ttu-id="aee44-109">Pour plus d'informations, consultez la page [Version d'évaluation gratuite d'Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="aee44-109">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 
> 
> 

<span data-ttu-id="aee44-110">Pour fournir aux utilisateurs une URL pouvant être utilisée pour diffuser en continu ou télécharger votre contenu, vous devez d’abord « publier » votre élément multimédia en créant un localisateur.</span><span class="sxs-lookup"><span data-stu-id="aee44-110">To provide your user with a  URL that can be used to stream or download your content, you first need to "publish" your asset by creating a locator.</span></span> <span data-ttu-id="aee44-111">Les localisateurs assurent l’accès aux fichiers contenus dans l’élément multimédia.</span><span class="sxs-lookup"><span data-stu-id="aee44-111">Locators provide access to files contained in the asset.</span></span> <span data-ttu-id="aee44-112">Media Services prend en charge deux types de localisateurs :</span><span class="sxs-lookup"><span data-stu-id="aee44-112">Media Services supports two types of locators:</span></span> 

* <span data-ttu-id="aee44-113">les localisateurs de diffusion en continu (OnDemandOrigin), utilisés pour la diffusion adaptative (par exemple, MPEG DASH, HLS ou Smooth Streaming) ;</span><span class="sxs-lookup"><span data-stu-id="aee44-113">Streaming (OnDemandOrigin) locators, used for adaptive streaming (for example, to stream MPEG DASH, HLS, or Smooth Streaming).</span></span> <span data-ttu-id="aee44-114">Pour créer un localisateur de diffusion en continu, votre élément multimédia doit contenir un fichier .ism ;</span><span class="sxs-lookup"><span data-stu-id="aee44-114">To create a streaming locator your asset must contain an .ism file.</span></span> 
* <span data-ttu-id="aee44-115">les localisateurs progressifs (SAS), utilisés pour la diffusion de vidéo par téléchargement progressif.</span><span class="sxs-lookup"><span data-stu-id="aee44-115">Progressive (SAS) locators, used for delivery of video via progressive download.</span></span>

<span data-ttu-id="aee44-116">Les URL de diffusion en continu, que vous pouvez utiliser pour lire des éléments multimédias Smooth Streaming, ont le format suivant.</span><span class="sxs-lookup"><span data-stu-id="aee44-116">A streaming URL has the following format and you can use it to play Smooth Streaming assets.</span></span>

    {streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest

<span data-ttu-id="aee44-117">Pour créer une URL de diffusion en continu HLS, ajoutez (format=m3u8-aapl) à l’URL.</span><span class="sxs-lookup"><span data-stu-id="aee44-117">To build an HLS streaming URL, append (format=m3u8-aapl) to the URL.</span></span>

    {streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=m3u8-aapl)

<span data-ttu-id="aee44-118">Pour créer une URL de diffusion en continu MPEG DASH, ajoutez (format=mpd-time-csf) à l’URL.</span><span class="sxs-lookup"><span data-stu-id="aee44-118">To build an  MPEG DASH streaming URL, append (format=mpd-time-csf) to the URL.</span></span>

    {streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=mpd-time-csf)

<span data-ttu-id="aee44-119">Une URL SAS a le format suivant :</span><span class="sxs-lookup"><span data-stu-id="aee44-119">A SAS URL has the following format.</span></span>

    {blob container name}/{asset name}/{file name}/{SAS signature}

<span data-ttu-id="aee44-120">Pour plus d’informations, consultez [Fournir du contenu (vue d’ensemble)](media-services-deliver-content-overview.md).</span><span class="sxs-lookup"><span data-stu-id="aee44-120">For more information, see [Delivering content overview](media-services-deliver-content-overview.md).</span></span>

> [!NOTE]
> <span data-ttu-id="aee44-121">Si vous avez utilisé le portail pour créer des localisateurs avant mars 2015, des localisateurs présentant une date d’expiration de deux ans ont été créés.</span><span class="sxs-lookup"><span data-stu-id="aee44-121">If you used the portal to create locators before March 2015, locators with a two year expiration date were created.</span></span>  
> 
> 

<span data-ttu-id="aee44-122">Pour mettre à jour la date d’expiration d’un localisateur, utilisez les API [REST](https://docs.microsoft.com/rest/api/media/operations/locator#update_a_locator) ou [.NET](http://go.microsoft.com/fwlink/?LinkID=533259).</span><span class="sxs-lookup"><span data-stu-id="aee44-122">To update an expiration date on a locator, use [REST](https://docs.microsoft.com/rest/api/media/operations/locator#update_a_locator) or [.NET](http://go.microsoft.com/fwlink/?LinkID=533259) APIs.</span></span> <span data-ttu-id="aee44-123">Notez que lorsque vous mettez à jour la date d’expiration d’un localisateur SAS, l’URL est modifiée.</span><span class="sxs-lookup"><span data-stu-id="aee44-123">Note that when you update the expiration date of a SAS locator, the URL changes.</span></span>

### <a name="to-use-the-portal-to-publish-an-asset"></a><span data-ttu-id="aee44-124">Pour publier un élément multimédia à l’aide du portail</span><span class="sxs-lookup"><span data-stu-id="aee44-124">To use the portal to publish an asset</span></span>
<span data-ttu-id="aee44-125">Pour utiliser le portail pour publier un élément multimédia, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="aee44-125">To use the portal to publish an asset, do the following:</span></span>

1. <span data-ttu-id="aee44-126">Dans le [portail Azure](https://portal.azure.com/), sélectionnez votre compte Azure Media Services.</span><span class="sxs-lookup"><span data-stu-id="aee44-126">In the [Azure portal](https://portal.azure.com/), select your Azure Media Services account.</span></span>
2. <span data-ttu-id="aee44-127">Sélectionnez **Paramètres** > **Éléments multimédias**.</span><span class="sxs-lookup"><span data-stu-id="aee44-127">Select **Settings** > **Assets**.</span></span>
3. <span data-ttu-id="aee44-128">Sélectionnez l’élément que vous souhaitez publier.</span><span class="sxs-lookup"><span data-stu-id="aee44-128">Select the asset that you want to publish.</span></span>
4. <span data-ttu-id="aee44-129">Cliquez sur le bouton **Publier** .</span><span class="sxs-lookup"><span data-stu-id="aee44-129">Click the **Publish** button.</span></span>
5. <span data-ttu-id="aee44-130">Sélectionnez le type de localisateur.</span><span class="sxs-lookup"><span data-stu-id="aee44-130">Select the locator type.</span></span>
6. <span data-ttu-id="aee44-131">Cliquez sur **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="aee44-131">Press **Add**.</span></span>
   
    ![Publier](./media/media-services-portal-vod-get-started/media-services-publish1.png)

<span data-ttu-id="aee44-133">L’URL sera ajoutée à la liste des **URL publiées**.</span><span class="sxs-lookup"><span data-stu-id="aee44-133">The URL will be added to the list of **Published URLs**.</span></span>

## <a name="play-content-from-the-portal"></a><span data-ttu-id="aee44-134">Lecture de contenu sur le portail</span><span class="sxs-lookup"><span data-stu-id="aee44-134">Play content from the portal</span></span>
<span data-ttu-id="aee44-135">Le portail Azure propose un lecteur de contenu que vous pouvez utiliser pour tester votre vidéo.</span><span class="sxs-lookup"><span data-stu-id="aee44-135">The Azure portal provides a content player that you can use to test your video.</span></span>

<span data-ttu-id="aee44-136">Cliquez sur la vidéo de votre choix, puis sur le bouton **Lire** .</span><span class="sxs-lookup"><span data-stu-id="aee44-136">Click the desired video and then click the **Play** button.</span></span>

![Publier](./media/media-services-portal-vod-get-started/media-services-play.png)

<span data-ttu-id="aee44-138">Certaines considérations s’appliquent :</span><span class="sxs-lookup"><span data-stu-id="aee44-138">Some considerations apply:</span></span>

* <span data-ttu-id="aee44-139">Assurez-vous que la vidéo a été publiée.</span><span class="sxs-lookup"><span data-stu-id="aee44-139">Make sure the video has been published.</span></span>
* <span data-ttu-id="aee44-140">Le **lecteur multimédia** effectue la lecture à partir du point de terminaison de diffusion en continu par défaut.</span><span class="sxs-lookup"><span data-stu-id="aee44-140">This **Media player** plays from the default streaming endpoint.</span></span> <span data-ttu-id="aee44-141">Si vous souhaitez lire à partir d’un autre point de terminaison de diffusion en continu que celui par défaut, cliquez sur l’URL pour la copier et utilisez un autre lecteur,</span><span class="sxs-lookup"><span data-stu-id="aee44-141">If you want to play from a non-default streaming endpoint, click to copy the URL and use another player.</span></span> <span data-ttu-id="aee44-142">par exemple, le [lecteur Azure Media Services](http://amsplayer.azurewebsites.net/azuremediaplayer.html).</span><span class="sxs-lookup"><span data-stu-id="aee44-142">For example, [Azure Media Services Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html).</span></span>
* <span data-ttu-id="aee44-143">Le point de terminaison de streaming à partir duquel vous diffusez en continu doit être en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="aee44-143">The streaming endpoint from which you are streaming must be running.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="aee44-144">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="aee44-144">Next steps</span></span>
<span data-ttu-id="aee44-145">Consultez les parcours d’apprentissage de Media Services.</span><span class="sxs-lookup"><span data-stu-id="aee44-145">Review Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="aee44-146">Fournir des commentaires</span><span class="sxs-lookup"><span data-stu-id="aee44-146">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

