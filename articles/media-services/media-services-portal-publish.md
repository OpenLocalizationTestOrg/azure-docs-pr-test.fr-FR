---
title: "AAA » publier du contenu avec hello portail Azure | Documents Microsoft »"
description: "Ce didacticiel vous guide tout au long des étapes hello de publication de votre contenu avec hello portail Azure."
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
ms.openlocfilehash: a7a3867a6939b4b9da883176c6cc20c99d6c54e7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="publish-content-with-hello-azure-portal"></a><span data-ttu-id="90a0f-103">Publier du contenu avec hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="90a0f-103">Publish content with hello Azure portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="90a0f-104">Portail</span><span class="sxs-lookup"><span data-stu-id="90a0f-104">Portal</span></span>](media-services-portal-publish.md)
> * [<span data-ttu-id="90a0f-105">.NET</span><span class="sxs-lookup"><span data-stu-id="90a0f-105">.NET</span></span>](media-services-deliver-streaming-content.md)
> * [<span data-ttu-id="90a0f-106">REST</span><span class="sxs-lookup"><span data-stu-id="90a0f-106">REST</span></span>](media-services-rest-deliver-streaming-content.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="90a0f-107">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="90a0f-107">Overview</span></span>
> [!NOTE]
> <span data-ttu-id="90a0f-108">toocomplete ce didacticiel, vous avez besoin d’un compte Azure.</span><span class="sxs-lookup"><span data-stu-id="90a0f-108">toocomplete this tutorial, you need an Azure account.</span></span> <span data-ttu-id="90a0f-109">Pour plus d'informations, consultez la page [Version d'évaluation gratuite d'Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="90a0f-109">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 
> 
> 

<span data-ttu-id="90a0f-110">tooprovide votre utilisateur avec une URL qui peut être utilisé toostream ou télécharger votre contenu, vous tout d’abord besoin trop « publier » votre élément multimédia en créant un localisateur.</span><span class="sxs-lookup"><span data-stu-id="90a0f-110">tooprovide your user with a  URL that can be used toostream or download your content, you first need too"publish" your asset by creating a locator.</span></span> <span data-ttu-id="90a0f-111">Les localisateurs offrent toofiles accès contenues dans l’élément multimédia de hello.</span><span class="sxs-lookup"><span data-stu-id="90a0f-111">Locators provide access toofiles contained in hello asset.</span></span> <span data-ttu-id="90a0f-112">Media Services prend en charge deux types de localisateurs :</span><span class="sxs-lookup"><span data-stu-id="90a0f-112">Media Services supports two types of locators:</span></span> 

* <span data-ttu-id="90a0f-113">Diffusion en continu les localisateurs (OnDemandOrigin), utilisés pour la diffusion adaptative en continu (par exemple, toostream MPEG DASH, HLS ou Smooth Streaming).</span><span class="sxs-lookup"><span data-stu-id="90a0f-113">Streaming (OnDemandOrigin) locators, used for adaptive streaming (for example, toostream MPEG DASH, HLS, or Smooth Streaming).</span></span> <span data-ttu-id="90a0f-114">toocreate un localisateur de diffusion en continu votre élément multimédia doit contenir un fichier .ism.</span><span class="sxs-lookup"><span data-stu-id="90a0f-114">toocreate a streaming locator your asset must contain an .ism file.</span></span> 
* <span data-ttu-id="90a0f-115">les localisateurs progressifs (SAS), utilisés pour la diffusion de vidéo par téléchargement progressif.</span><span class="sxs-lookup"><span data-stu-id="90a0f-115">Progressive (SAS) locators, used for delivery of video via progressive download.</span></span>

<span data-ttu-id="90a0f-116">Une URL de diffusion en continu a hello suivant le format et vous pouvez l’utiliser de ressources de diffusion en continu lisse tooplay.</span><span class="sxs-lookup"><span data-stu-id="90a0f-116">A streaming URL has hello following format and you can use it tooplay Smooth Streaming assets.</span></span>

    {streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest

<span data-ttu-id="90a0f-117">ajouter des toobuild une URL de diffusion en continu de TLS (format = m3u8-aapl) toohello URL.</span><span class="sxs-lookup"><span data-stu-id="90a0f-117">toobuild an HLS streaming URL, append (format=m3u8-aapl) toohello URL.</span></span>

    {streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=m3u8-aapl)

<span data-ttu-id="90a0f-118">ajouter des toobuild une URL de diffusion en continu de MPEG DASH (format = mpd-heure-csf) toohello URL.</span><span class="sxs-lookup"><span data-stu-id="90a0f-118">toobuild an  MPEG DASH streaming URL, append (format=mpd-time-csf) toohello URL.</span></span>

    {streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=mpd-time-csf)

<span data-ttu-id="90a0f-119">Une URL SAS a hello suivant le format.</span><span class="sxs-lookup"><span data-stu-id="90a0f-119">A SAS URL has hello following format.</span></span>

    {blob container name}/{asset name}/{file name}/{SAS signature}

<span data-ttu-id="90a0f-120">Pour plus d’informations, consultez [Fournir du contenu (vue d’ensemble)](media-services-deliver-content-overview.md).</span><span class="sxs-lookup"><span data-stu-id="90a0f-120">For more information, see [Delivering content overview](media-services-deliver-content-overview.md).</span></span>

> [!NOTE]
> <span data-ttu-id="90a0f-121">Si vous avez utilisé les localisateurs toocreate portail hello avant mars 2015, les localisateurs avec une date d’expiration de deux ans ont été créés.</span><span class="sxs-lookup"><span data-stu-id="90a0f-121">If you used hello portal toocreate locators before March 2015, locators with a two year expiration date were created.</span></span>  
> 
> 

<span data-ttu-id="90a0f-122">tooupdate une date d’expiration sur un localisateur, utilisez [reste](https://docs.microsoft.com/rest/api/media/operations/locator#update_a_locator) ou [.NET](http://go.microsoft.com/fwlink/?LinkID=533259) API.</span><span class="sxs-lookup"><span data-stu-id="90a0f-122">tooupdate an expiration date on a locator, use [REST](https://docs.microsoft.com/rest/api/media/operations/locator#update_a_locator) or [.NET](http://go.microsoft.com/fwlink/?LinkID=533259) APIs.</span></span> <span data-ttu-id="90a0f-123">Notez que lorsque vous mettez à jour date d’expiration de hello d’un localisateur SAS, hello URL change.</span><span class="sxs-lookup"><span data-stu-id="90a0f-123">Note that when you update hello expiration date of a SAS locator, hello URL changes.</span></span>

### <a name="toouse-hello-portal-toopublish-an-asset"></a><span data-ttu-id="90a0f-124">toouse hello toopublish portail un élément multimédia</span><span class="sxs-lookup"><span data-stu-id="90a0f-124">toouse hello portal toopublish an asset</span></span>
<span data-ttu-id="90a0f-125">toouse hello toopublish portail un élément multimédia, hello suivant :</span><span class="sxs-lookup"><span data-stu-id="90a0f-125">toouse hello portal toopublish an asset, do hello following:</span></span>

1. <span data-ttu-id="90a0f-126">Bonjour [portail Azure](https://portal.azure.com/), sélectionnez votre compte Azure Media Services.</span><span class="sxs-lookup"><span data-stu-id="90a0f-126">In hello [Azure portal](https://portal.azure.com/), select your Azure Media Services account.</span></span>
2. <span data-ttu-id="90a0f-127">Sélectionnez **Paramètres** > **Éléments multimédias**.</span><span class="sxs-lookup"><span data-stu-id="90a0f-127">Select **Settings** > **Assets**.</span></span>
3. <span data-ttu-id="90a0f-128">Sélectionnez asset hello que vous souhaitez toopublish.</span><span class="sxs-lookup"><span data-stu-id="90a0f-128">Select hello asset that you want toopublish.</span></span>
4. <span data-ttu-id="90a0f-129">Cliquez sur hello **publier** bouton.</span><span class="sxs-lookup"><span data-stu-id="90a0f-129">Click hello **Publish** button.</span></span>
5. <span data-ttu-id="90a0f-130">Sélectionnez le type de localisateur hello.</span><span class="sxs-lookup"><span data-stu-id="90a0f-130">Select hello locator type.</span></span>
6. <span data-ttu-id="90a0f-131">Cliquez sur **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="90a0f-131">Press **Add**.</span></span>
   
    ![Publier](./media/media-services-portal-vod-get-started/media-services-publish1.png)

<span data-ttu-id="90a0f-133">URL de Hello sera ajouté toohello la liste des **URL de publication**.</span><span class="sxs-lookup"><span data-stu-id="90a0f-133">hello URL will be added toohello list of **Published URLs**.</span></span>

## <a name="play-content-from-hello-portal"></a><span data-ttu-id="90a0f-134">Lire le contenu à partir du portail de hello</span><span class="sxs-lookup"><span data-stu-id="90a0f-134">Play content from hello portal</span></span>
<span data-ttu-id="90a0f-135">portail Azure Hello fournit un lecteur de contenu que vous pouvez utiliser tootest votre vidéo.</span><span class="sxs-lookup"><span data-stu-id="90a0f-135">hello Azure portal provides a content player that you can use tootest your video.</span></span>

<span data-ttu-id="90a0f-136">Vidéo de hello souhaité, puis cliquez sur hello **lire** bouton.</span><span class="sxs-lookup"><span data-stu-id="90a0f-136">Click hello desired video and then click hello **Play** button.</span></span>

![Publier](./media/media-services-portal-vod-get-started/media-services-play.png)

<span data-ttu-id="90a0f-138">Certaines considérations s’appliquent :</span><span class="sxs-lookup"><span data-stu-id="90a0f-138">Some considerations apply:</span></span>

* <span data-ttu-id="90a0f-139">Vérifiez que hello vidéo a été publié.</span><span class="sxs-lookup"><span data-stu-id="90a0f-139">Make sure hello video has been published.</span></span>
* <span data-ttu-id="90a0f-140">Cela **Media player** est lu à partir du point de terminaison de diffusion en continu de la valeur par défaut hello.</span><span class="sxs-lookup"><span data-stu-id="90a0f-140">This **Media player** plays from hello default streaming endpoint.</span></span> <span data-ttu-id="90a0f-141">Si vous souhaitez tooplay à partir d’un élément non défini par défaut diffusion en continu de point de terminaison, cliquez sur l’URL toocopy hello et utilisez un autre lecteur.</span><span class="sxs-lookup"><span data-stu-id="90a0f-141">If you want tooplay from a non-default streaming endpoint, click toocopy hello URL and use another player.</span></span> <span data-ttu-id="90a0f-142">par exemple, le [lecteur Azure Media Services](http://amsplayer.azurewebsites.net/azuremediaplayer.html).</span><span class="sxs-lookup"><span data-stu-id="90a0f-142">For example, [Azure Media Services Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html).</span></span>
* <span data-ttu-id="90a0f-143">Bonjour à partir de laquelle vous diffusiez en continu un point de terminaison de diffusion en continu doit s’exécuter.</span><span class="sxs-lookup"><span data-stu-id="90a0f-143">hello streaming endpoint from which you are streaming must be running.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="90a0f-144">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="90a0f-144">Next steps</span></span>
<span data-ttu-id="90a0f-145">Consultez les parcours d’apprentissage de Media Services.</span><span class="sxs-lookup"><span data-stu-id="90a0f-145">Review Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="90a0f-146">Fournir des commentaires</span><span class="sxs-lookup"><span data-stu-id="90a0f-146">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

