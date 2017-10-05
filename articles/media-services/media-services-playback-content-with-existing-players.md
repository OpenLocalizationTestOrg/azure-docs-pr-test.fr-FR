---
title: Utiliser des lecteurs existants pour lire du contenu - Azure | Microsoft Docs
description: "Cette rubrique répertorie les lecteurs existants que vous pouvez utiliser pour lire votre contenu."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 7e9fcf89-0fb6-4fa4-96cb-666320684d69
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: juliako
ms.openlocfilehash: 48f373b013b1192c353352b801876d706d91dd28
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="playing-your-content-with-existing-players"></a><span data-ttu-id="41347-103">Lecture de votre contenu à l’aide des lecteurs existants</span><span class="sxs-lookup"><span data-stu-id="41347-103">Playing your content with existing players</span></span>
<span data-ttu-id="41347-104">Azure Media Services prend en charge de nombreux formats de streaming populaires, tels que Smooth Streaming, le streaming HTTP et MPEG-Dash.</span><span class="sxs-lookup"><span data-stu-id="41347-104">Azure Media Services supports many popular streaming formats, such as Smooth Streaming, HTTP Live Streaming, and MPEG-Dash.</span></span> <span data-ttu-id="41347-105">Cette rubrique vous oriente vers les lecteurs existants que vous pouvez utiliser pour tester votre flux de données.</span><span class="sxs-lookup"><span data-stu-id="41347-105">This topic points you to existing players that you can use to test your streams.</span></span>

### <a name="the-azure-portal-media-services-content-player"></a><span data-ttu-id="41347-106">Le lecteur de contenu Media Services sur le portail Azure</span><span class="sxs-lookup"><span data-stu-id="41347-106">The Azure portal Media Services content player</span></span>
<span data-ttu-id="41347-107">Le **portail Azure** propose un lecteur de contenu que vous pouvez utiliser pour tester votre vidéo.</span><span class="sxs-lookup"><span data-stu-id="41347-107">The **Azure** portal provides a content player that you can use to test your video.</span></span>

<span data-ttu-id="41347-108">Cliquez sur la vidéo de votre choix (assurez-vous qu’elle a été [publiée](media-services-portal-publish.md)), puis sur le bouton **Lire** situé en bas du portail.</span><span class="sxs-lookup"><span data-stu-id="41347-108">Click on the desired video (make sure it was [published](media-services-portal-publish.md)) and click the **Play** button at the bottom of the portal.</span></span>

<span data-ttu-id="41347-109">Certaines considérations s’appliquent :</span><span class="sxs-lookup"><span data-stu-id="41347-109">Some considerations apply:</span></span>

* <span data-ttu-id="41347-110">Le **lecteur de contenu de Media Services** assure la lecture depuis le point de terminaison de streaming par défaut.</span><span class="sxs-lookup"><span data-stu-id="41347-110">The **MEDIA SERVICES CONTENT PLAYER** plays from the default streaming endpoint.</span></span> <span data-ttu-id="41347-111">Si vous souhaitez lire à partir d’un autre point de terminaison de streaming que celui par défaut, utilisez un autre lecteur.</span><span class="sxs-lookup"><span data-stu-id="41347-111">If you want to play from a non-default streaming endpoint, use another player.</span></span> <span data-ttu-id="41347-112">Par exemple, [Azure Media Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html).</span><span class="sxs-lookup"><span data-stu-id="41347-112">For example, [Azure Media Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html).</span></span>

![AMSPlayer][AMSPlayer]

### <a name="azure-media-player"></a><span data-ttu-id="41347-114">Azure Media Player</span><span class="sxs-lookup"><span data-stu-id="41347-114">Azure Media Player</span></span>
<span data-ttu-id="41347-115">Utilisez [Azure Media Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html) pour lire votre contenu (protégé ou non) dans l'un des formats suivants :</span><span class="sxs-lookup"><span data-stu-id="41347-115">Use [Azure Media Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html) to playback your content (clear or protected) in any of the following formats:</span></span>

* <span data-ttu-id="41347-116">Smooth Streaming</span><span class="sxs-lookup"><span data-stu-id="41347-116">Smooth Streaming</span></span>
* <span data-ttu-id="41347-117">MPEG DASH</span><span class="sxs-lookup"><span data-stu-id="41347-117">MPEG DASH</span></span>
* <span data-ttu-id="41347-118">HLS</span><span class="sxs-lookup"><span data-stu-id="41347-118">HLS</span></span>
* <span data-ttu-id="41347-119">MP4 progressif</span><span class="sxs-lookup"><span data-stu-id="41347-119">Progressive MP4</span></span>

### <a name="flash-player"></a><span data-ttu-id="41347-120">Flash Player</span><span class="sxs-lookup"><span data-stu-id="41347-120">Flash Player</span></span>
#### <a name="aes-encrypted-with-token"></a><span data-ttu-id="41347-121">Chiffrement AES avec jeton</span><span class="sxs-lookup"><span data-stu-id="41347-121">AES-encrypted with Token</span></span>
[<span data-ttu-id="41347-122">http://aestoken.azurewebsites.net</span><span class="sxs-lookup"><span data-stu-id="41347-122">http://aestoken.azurewebsites.net</span></span>](http://aestoken.azurewebsites.net)

### <a name="silverlight-players"></a><span data-ttu-id="41347-123">Lecteurs Silverlight</span><span class="sxs-lookup"><span data-stu-id="41347-123">Silverlight Players</span></span>
#### <a name="monitoring"></a><span data-ttu-id="41347-124">Surveillance</span><span class="sxs-lookup"><span data-stu-id="41347-124">Monitoring</span></span>
[<span data-ttu-id="41347-125">http://smf.cloudapp.net/healthmonitor</span><span class="sxs-lookup"><span data-stu-id="41347-125">http://smf.cloudapp.net/healthmonitor</span></span>](http://smf.cloudapp.net/healthmonitor)

#### <a name="playready-with-token"></a><span data-ttu-id="41347-126">PlayReady avec jeton</span><span class="sxs-lookup"><span data-stu-id="41347-126">PlayReady with Token</span></span>
[<span data-ttu-id="41347-127">http://sltoken.azurewebsites.net</span><span class="sxs-lookup"><span data-stu-id="41347-127">http://sltoken.azurewebsites.net</span></span>](http://sltoken.azurewebsites.net)

### <a name="dash-players"></a><span data-ttu-id="41347-128">Lecteurs DASH</span><span class="sxs-lookup"><span data-stu-id="41347-128">DASH Players</span></span>
[<span data-ttu-id="41347-129">http://dashplayer.azurewebsites.net</span><span class="sxs-lookup"><span data-stu-id="41347-129">http://dashplayer.azurewebsites.net</span></span>](http://dashplayer.azurewebsites.net)

[<span data-ttu-id="41347-130">http://dashif.org</span><span class="sxs-lookup"><span data-stu-id="41347-130">http://dashif.org</span></span>](http://dashif.org)

### <a name="other"></a><span data-ttu-id="41347-131">Autres</span><span class="sxs-lookup"><span data-stu-id="41347-131">Other</span></span>
<span data-ttu-id="41347-132">Pour tester les URL HLS, vous pouvez également utiliser :</span><span class="sxs-lookup"><span data-stu-id="41347-132">To test HLS URLs you can also use:</span></span>

* <span data-ttu-id="41347-133">**Safari** sur un appareil iOS ou</span><span class="sxs-lookup"><span data-stu-id="41347-133">**Safari** on an iOS device or</span></span>
* <span data-ttu-id="41347-134">**3ivx HLS Player** sous Windows.</span><span class="sxs-lookup"><span data-stu-id="41347-134">**3ivx HLS Player** on Windows.</span></span>

## <a name="developing-video-players"></a><span data-ttu-id="41347-135">Développement de lecteurs vidéo</span><span class="sxs-lookup"><span data-stu-id="41347-135">Developing video players</span></span>
<span data-ttu-id="41347-136">Pour plus d’informations sur le développement de vos propres lecteurs, consultez la page [Développement de lecteurs vidéo](media-services-develop-video-players.md)</span><span class="sxs-lookup"><span data-stu-id="41347-136">For information about how to develop your own players, see [Developing video players](media-services-develop-video-players.md)</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="41347-137">Parcours d’apprentissage de Media Services</span><span class="sxs-lookup"><span data-stu-id="41347-137">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="41347-138">Fournir des commentaires</span><span class="sxs-lookup"><span data-stu-id="41347-138">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

[AMSPlayer]: ./media/media-services-playback-content-with-existing-players/media-services-portal-player.png
