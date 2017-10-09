---
title: "aaaEncode un élément multimédia à l’aide de Media Encoder Standard avec hello portail Azure | Documents Microsoft"
description: "Ce didacticiel vous guide tout au long des étapes hello de codage d’un élément multimédia à l’aide de Media Encoder Standard avec hello portail Azure."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 107d9e9a-71e9-43e5-b17c-6e00983aceab
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/07/2017
ms.author: juliako
ms.openlocfilehash: 0d118bbbe1fa9f4ba0bfa3ea3b10fb541d1d6379
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="encode-an-asset-using-media-encoder-standard-with-hello-azure-portal"></a><span data-ttu-id="5b0f3-103">Encoder un élément multimédia à l’aide de Media Encoder Standard avec hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="5b0f3-103">Encode an asset using Media Encoder Standard with hello Azure portal</span></span>
> [!NOTE]
> <span data-ttu-id="5b0f3-104">toocomplete ce didacticiel, vous avez besoin d’un compte Azure.</span><span class="sxs-lookup"><span data-stu-id="5b0f3-104">toocomplete this tutorial, you need an Azure account.</span></span> <span data-ttu-id="5b0f3-105">Pour plus d'informations, consultez la page [Version d'évaluation gratuite d'Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="5b0f3-105">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 
> 
> 

<span data-ttu-id="5b0f3-106">Lorsque vous travaillez avec un des scénarios les plus courants de hello transmet les clients tooyour de diffusion en continu à débit adaptatif Azure Media Services.</span><span class="sxs-lookup"><span data-stu-id="5b0f3-106">When working with Azure Media Services one of hello most common scenarios is delivering adaptive bitrate streaming tooyour clients.</span></span> <span data-ttu-id="5b0f3-107">Media Services prend en charge hello suivant des technologies de diffusion en continu de fichiers à débit adaptatif : HTTP Live Streaming (HLS), la diffusion en continu lisse, MPEG DASH.</span><span class="sxs-lookup"><span data-stu-id="5b0f3-107">Media Services supports hello following adaptive bitrate streaming technologies: HTTP Live Streaming (HLS), Smooth Streaming, MPEG DASH.</span></span> <span data-ttu-id="5b0f3-108">tooprepare vos vidéos pour de diffusion en continu à débit adaptatif, vous devez tooencode votre source vidéo dans des fichiers de débits.</span><span class="sxs-lookup"><span data-stu-id="5b0f3-108">tooprepare your videos for adaptive bitrate streaming, you need tooencode your source video into multi-bitrate files.</span></span> <span data-ttu-id="5b0f3-109">Vous devez utiliser hello **Media Encoder Standard** encodeur tooencode vos vidéos.</span><span class="sxs-lookup"><span data-stu-id="5b0f3-109">You should use hello **Media Encoder Standard** encoder tooencode your videos.</span></span>  

<span data-ttu-id="5b0f3-110">Media Services fournit également un empaquetage dynamique qui vous permet de toodeliver votre MP4s débits Bonjour suivant les formats de diffusion en continu : MPEG DASH, HLS, Smooth Streaming, sans que vous ayez toore-package dans ces formats de diffusion en continu.</span><span class="sxs-lookup"><span data-stu-id="5b0f3-110">Media Services also provides dynamic packaging which allows you toodeliver your multi-bitrate MP4s in hello following streaming formats: MPEG DASH, HLS, Smooth Streaming, without you having toore-package into these streaming formats.</span></span> <span data-ttu-id="5b0f3-111">Avec l’empaquetage dynamique vous devez uniquement toostore et payer pour les fichiers hello dans un seul format de stockage et les Services de support pour la génération et fournit hello de réponse appropriée en fonction des demandes d’un client.</span><span class="sxs-lookup"><span data-stu-id="5b0f3-111">With dynamic packaging you only need toostore and pay for hello files in single storage format and Media Services will build and serve hello appropriate response based on requests from a client.</span></span>

<span data-ttu-id="5b0f3-112">tootake parti de l’empaquetage dynamique, vous devez tooencode votre fichier source en un ensemble de fichiers MP4 à plusieurs débits (étapes de codage hello sont décrites plus loin dans cette section).</span><span class="sxs-lookup"><span data-stu-id="5b0f3-112">tootake advantage of dynamic packaging, you need tooencode your source file into a set of multi-bitrate MP4 files (hello encoding steps are demonstrated later in this section).</span></span>

<span data-ttu-id="5b0f3-113">support tooscale du traitement, consultez [cela](media-services-portal-scale-media-processing.md) rubrique.</span><span class="sxs-lookup"><span data-stu-id="5b0f3-113">tooscale media processing, see [this](media-services-portal-scale-media-processing.md) topic.</span></span>

## <a name="encode-with-hello-azure-portal"></a><span data-ttu-id="5b0f3-114">Encoder avec hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="5b0f3-114">Encode with hello Azure portal</span></span>
<span data-ttu-id="5b0f3-115">Cette section décrit les étapes à suivre tooencode votre contenu avec Media Encoder Standard hello.</span><span class="sxs-lookup"><span data-stu-id="5b0f3-115">This section describes hello steps you can take tooencode your content with Media Encoder Standard.</span></span>

1. <span data-ttu-id="5b0f3-116">Bonjour [portail Azure](https://portal.azure.com/), sélectionnez votre compte Azure Media Services.</span><span class="sxs-lookup"><span data-stu-id="5b0f3-116">In hello [Azure portal](https://portal.azure.com/), select your Azure Media Services account.</span></span>
2. <span data-ttu-id="5b0f3-117">Bonjour **paramètres** fenêtre, sélectionnez **actifs**.</span><span class="sxs-lookup"><span data-stu-id="5b0f3-117">In hello **Settings** window, select **Assets**.</span></span>  
3. <span data-ttu-id="5b0f3-118">Bonjour **actifs** fenêtre, asset hello select que vous aimeriez tooencode.</span><span class="sxs-lookup"><span data-stu-id="5b0f3-118">In hello **Assets** window, select hello asset that you would like tooencode.</span></span>
4. <span data-ttu-id="5b0f3-119">Hello de presse **Encode** bouton.</span><span class="sxs-lookup"><span data-stu-id="5b0f3-119">Press hello **Encode** button.</span></span>
5. <span data-ttu-id="5b0f3-120">Bonjour **encoder un élément multimédia** fenêtre, processeur de « Media Encoder Standard » hello select et une présélection.</span><span class="sxs-lookup"><span data-stu-id="5b0f3-120">In hello **Encode an asset** window, select hello "Media Encoder Standard" processor and a preset.</span></span> <span data-ttu-id="5b0f3-121">Pour plus d’informations sur les présélections, consultez les articles [Utilisation d’Azure Media Encoder Standard pour générer automatiquement une échelle des vitesses de transmission](media-services-autogen-bitrate-ladder-with-mes.md) et [Présélections de travaux pour MES (Media Encoder Standard)](media-services-mes-presets-overview.md).</span><span class="sxs-lookup"><span data-stu-id="5b0f3-121">For information about presets, see [auto-generate a bitrate ladder](media-services-autogen-bitrate-ladder-with-mes.md) and [Task Presets for MES](media-services-mes-presets-overview.md).</span></span> <span data-ttu-id="5b0f3-122">Si vous envisagez toocontrol quelle valeur prédéfinie d’encodage est utilisée, gardez cela à l’esprit : il est important de tooselect hello prédéfini qui convient le mieux pour votre vidéo d’entrée.</span><span class="sxs-lookup"><span data-stu-id="5b0f3-122">If you plan toocontrol which encoding preset is used, keep this in mind: it is important tooselect hello preset that is most appropriate for your input video.</span></span> <span data-ttu-id="5b0f3-123">Par exemple, si vous connaissez votre vidéo d’entrée d’une résolution de 1920 x 1080 pixels, vous pouvez utiliser hello « H264 plusieurs débits binaires 1080p » prédéfini.</span><span class="sxs-lookup"><span data-stu-id="5b0f3-123">For example, if you know your input video has a resolution of 1920x1080 pixels, then you could use hello "H264 Multiple Bitrate 1080p" preset.</span></span> <span data-ttu-id="5b0f3-124">Si vous disposez d’une vidéo basse résolution (640 x 360), il est préférable de ne pas utiliser la présélection « H264 – Vitesse de transmission multiple – 1 080 pixels ».</span><span class="sxs-lookup"><span data-stu-id="5b0f3-124">If you have a low resolution (640x360) video, then you should not be using "H264 Multiple Bitrate 1080p" preset.</span></span>
   
   <span data-ttu-id="5b0f3-125">Pour faciliter la gestion, vous avez une option de modification de nom hello de ressource en sortie hello et nom hello du travail de hello.</span><span class="sxs-lookup"><span data-stu-id="5b0f3-125">For easier management, you have an option of editing hello name of hello output asset, and hello name of hello job.</span></span>
   
   ![Encoder des éléments multimédias](./media/media-services-portal-vod-get-started/media-services-encode1.png)
6. <span data-ttu-id="5b0f3-127">Appuyez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="5b0f3-127">Press **Create**.</span></span>

## <a name="next-step"></a><span data-ttu-id="5b0f3-128">Étape suivante</span><span class="sxs-lookup"><span data-stu-id="5b0f3-128">Next step</span></span>
<span data-ttu-id="5b0f3-129">Vous pouvez surveiller la progression de la tâche encodage avec hello portail Azure, comme décrit dans [cela](media-services-portal-check-job-progress.md) l’article.</span><span class="sxs-lookup"><span data-stu-id="5b0f3-129">You can monitor encoding job progress with hello Azure portal, as described in [this](media-services-portal-check-job-progress.md) article.</span></span>  

## <a name="media-services-learning-paths"></a><span data-ttu-id="5b0f3-130">Parcours d’apprentissage de Media Services</span><span class="sxs-lookup"><span data-stu-id="5b0f3-130">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="5b0f3-131">Fournir des commentaires</span><span class="sxs-lookup"><span data-stu-id="5b0f3-131">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

