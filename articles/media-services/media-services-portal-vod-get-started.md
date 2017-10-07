---
title: "aaaGet démarré à la livraison de demande (VOD) à l’aide de hello portail Azure | Documents Microsoft"
description: "Ce didacticiel vous guide tout au long des étapes hello d’implémentation d’un service de diffusion de contenu vidéo à la demande (VoD) base avec l’application Azure Media Services (AMS) à l’aide de hello portail Azure."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 6c98fcfa-39e6-43a5-83a5-d4954788f8a4
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/07/2017
ms.author: juliako
ms.openlocfilehash: 5c1c1b1f74ec1f1301120fe8e5a5ae183fe0338f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-delivering-content-on-demand-using-hello-azure-portal"></a><span data-ttu-id="e5a6e-103">Prise en main la diffusion de contenu sur demande à l’aide de hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="e5a6e-103">Get started with delivering content on demand using hello Azure portal</span></span>
[!INCLUDE [media-services-selector-get-started](../../includes/media-services-selector-get-started.md)]

<span data-ttu-id="e5a6e-104">Ce didacticiel vous guide tout au long des étapes hello d’implémentation d’un service de diffusion de contenu vidéo à la demande (VoD) base avec l’application Azure Media Services (AMS) à l’aide de hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="e5a6e-104">This tutorial walks you through hello steps of implementing a basic Video-on-Demand (VoD) content delivery service with Azure Media Services (AMS) application using hello Azure portal.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e5a6e-105">Composants requis</span><span class="sxs-lookup"><span data-stu-id="e5a6e-105">Prerequisites</span></span>
<span data-ttu-id="e5a6e-106">Hello Voici didacticiel de hello toocomplete requis :</span><span class="sxs-lookup"><span data-stu-id="e5a6e-106">hello following are required toocomplete hello tutorial:</span></span>

* <span data-ttu-id="e5a6e-107">Un compte Azure.</span><span class="sxs-lookup"><span data-stu-id="e5a6e-107">An Azure account.</span></span> <span data-ttu-id="e5a6e-108">Pour plus d'informations, consultez la page [Version d'évaluation gratuite d'Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="e5a6e-108">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 
* <span data-ttu-id="e5a6e-109">Un compte Media Services.</span><span class="sxs-lookup"><span data-stu-id="e5a6e-109">A Media Services account.</span></span> <span data-ttu-id="e5a6e-110">toocreate un compte Media Services, consultez [comment tooCreate un compte Media Services](media-services-portal-create-account.md).</span><span class="sxs-lookup"><span data-stu-id="e5a6e-110">toocreate a Media Services account, see [How tooCreate a Media Services Account](media-services-portal-create-account.md).</span></span>

<span data-ttu-id="e5a6e-111">Ce didacticiel inclut hello tâches suivantes :</span><span class="sxs-lookup"><span data-stu-id="e5a6e-111">This tutorial includes hello following tasks:</span></span>

1. <span data-ttu-id="e5a6e-112">Démarrer un point de terminaison de streaming.</span><span class="sxs-lookup"><span data-stu-id="e5a6e-112">Start streaming endpoint.</span></span>
2. <span data-ttu-id="e5a6e-113">Télécharger un fichier vidéo.</span><span class="sxs-lookup"><span data-stu-id="e5a6e-113">Upload a video file.</span></span>
3. <span data-ttu-id="e5a6e-114">Encoder le fichier de source de hello en un ensemble de fichiers MP4 à débit adaptatif.</span><span class="sxs-lookup"><span data-stu-id="e5a6e-114">Encode hello source file into a set of adaptive bitrate MP4 files.</span></span>
4. <span data-ttu-id="e5a6e-115">Publier les actifs hello et get de diffusion en continu et URL de téléchargement progressif.</span><span class="sxs-lookup"><span data-stu-id="e5a6e-115">Publish hello asset and get streaming and progressive download URLs.</span></span>  
5. <span data-ttu-id="e5a6e-116">Lire votre contenu.</span><span class="sxs-lookup"><span data-stu-id="e5a6e-116">Play your content.</span></span>

## <a name="start-streaming-endpoints"></a><span data-ttu-id="e5a6e-117">Démarrer les points de terminaison de streaming</span><span class="sxs-lookup"><span data-stu-id="e5a6e-117">Start streaming endpoints</span></span> 

<span data-ttu-id="e5a6e-118">Lorsque vous travaillez avec un des scénarios les plus courants de hello est diffusion vidéo via à débit adaptatif de diffusion en continu Azure Media Services.</span><span class="sxs-lookup"><span data-stu-id="e5a6e-118">When working with Azure Media Services one of hello most common scenarios is delivering video via adaptive bitrate streaming.</span></span> <span data-ttu-id="e5a6e-119">Media Services propose un empaquetage dynamique, ce qui vous permet de toodeliver votre vitesse de transmission adaptative MP4 encodés le contenu de diffusion en continu des formats pris en charge par Media Services (MPEG DASH, HLS, Smooth Streaming) juste-à-temps, sans que vous ayez toostore préconçue versions de chacune de ces formats de diffusion en continu.</span><span class="sxs-lookup"><span data-stu-id="e5a6e-119">Media Services provides dynamic packaging, which allows you toodeliver your adaptive bitrate MP4 encoded content in streaming formats supported by Media Services (MPEG DASH, HLS, Smooth Streaming) just-in-time, without you having toostore pre-packaged versions of each of these streaming formats.</span></span>

>[!NOTE]
><span data-ttu-id="e5a6e-120">Création de votre compte AMS un **par défaut** point de terminaison de diffusion en continu est ajoutée tooyour compte Bonjour **arrêté** état.</span><span class="sxs-lookup"><span data-stu-id="e5a6e-120">When your AMS account is created a **default** streaming endpoint is added tooyour account in hello **Stopped** state.</span></span> <span data-ttu-id="e5a6e-121">toostart de diffusion en continu de votre contenu et profitez de l’empaquetage dynamique et chiffrement dynamique, hello de point de terminaison de diffusion en continu à partir de laquelle vous souhaitez que le contenu toostream a toobe Bonjour **en cours d’exécution** état.</span><span class="sxs-lookup"><span data-stu-id="e5a6e-121">toostart streaming your content and take advantage of dynamic packaging and dynamic encryption, hello streaming endpoint from which you want toostream content has toobe in hello **Running** state.</span></span> 

<span data-ttu-id="e5a6e-122">toostart hello du point de terminaison de diffusion en continu, hello suivant :</span><span class="sxs-lookup"><span data-stu-id="e5a6e-122">toostart hello streaming endpoint, do hello following:</span></span>

1. <span data-ttu-id="e5a6e-123">Connectez-vous à l’adresse hello [portail Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="e5a6e-123">Log in at hello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="e5a6e-124">Dans la fenêtre des paramètres hello, cliquez sur les points de terminaison de diffusion en continu.</span><span class="sxs-lookup"><span data-stu-id="e5a6e-124">In hello Settings window, click Streaming endpoints.</span></span> 
3. <span data-ttu-id="e5a6e-125">Cliquez sur le point de terminaison de diffusion en continu de la valeur par défaut hello.</span><span class="sxs-lookup"><span data-stu-id="e5a6e-125">Click hello default streaming endpoint.</span></span> 

    <span data-ttu-id="e5a6e-126">fenêtre de détails par défaut du point de terminaison de diffusion en continu Hello s’affiche.</span><span class="sxs-lookup"><span data-stu-id="e5a6e-126">hello DEFAULT STREAMING ENDPOINT DETAILS window appears.</span></span>

4. <span data-ttu-id="e5a6e-127">Cliquez sur l’icône Démarrer hello.</span><span class="sxs-lookup"><span data-stu-id="e5a6e-127">Click hello Start icon.</span></span>
5. <span data-ttu-id="e5a6e-128">Cliquez sur toosave de bouton hello enregistrer vos modifications.</span><span class="sxs-lookup"><span data-stu-id="e5a6e-128">Click hello Save button toosave your changes.</span></span>

## <a name="upload-files"></a><span data-ttu-id="e5a6e-129">Charger des fichiers</span><span class="sxs-lookup"><span data-stu-id="e5a6e-129">Upload files</span></span>
<span data-ttu-id="e5a6e-130">toostream vidéos à l’aide d’Azure Media Services, vous devez les vidéos de source tooupload hello, les encoder en plusieurs vitesses de transmission et publier les résultats hello.</span><span class="sxs-lookup"><span data-stu-id="e5a6e-130">toostream videos using Azure Media Services, you need tooupload hello source videos, encode them into multiple bitrates, and publish hello result.</span></span> <span data-ttu-id="e5a6e-131">première étape de Hello est décrite dans cette section.</span><span class="sxs-lookup"><span data-stu-id="e5a6e-131">hello first step is covered in this section.</span></span> 

1. <span data-ttu-id="e5a6e-132">Bonjour **paramètre** fenêtre, cliquez sur **actifs**.</span><span class="sxs-lookup"><span data-stu-id="e5a6e-132">In hello **Setting** window, click **Assets**.</span></span>
   
    ![Charger des fichiers](./media/media-services-portal-vod-get-started/media-services-upload.png)
2. <span data-ttu-id="e5a6e-134">Cliquez sur hello **télécharger** bouton.</span><span class="sxs-lookup"><span data-stu-id="e5a6e-134">Click hello **Upload** button.</span></span>
   
    <span data-ttu-id="e5a6e-135">Hello **télécharger un élément multimédia vidéo** fenêtre s’affiche.</span><span class="sxs-lookup"><span data-stu-id="e5a6e-135">hello **Upload a video asset** window appears.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="e5a6e-136">Il n’existe aucune limite de taille de fichier.</span><span class="sxs-lookup"><span data-stu-id="e5a6e-136">There is no file size limitation.</span></span>
   > 
   > 
3. <span data-ttu-id="e5a6e-137">Parcourir vidéo toohello souhaité sur votre ordinateur, sélectionnez-le, puis appuyez sur OK.</span><span class="sxs-lookup"><span data-stu-id="e5a6e-137">Browse toohello desired video on your computer, select it, and hit OK.</span></span>  
   
    <span data-ttu-id="e5a6e-138">téléchargement de Hello démarre et vous pouvez voir la progression hello sous le nom de fichier hello.</span><span class="sxs-lookup"><span data-stu-id="e5a6e-138">hello upload starts and you can see hello progress under hello file name.</span></span>  

<span data-ttu-id="e5a6e-139">Une fois le téléchargement de hello terminé, vous voyez hello un nouveau composant répertorié dans hello **actifs** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="e5a6e-139">Once hello upload completes, you see hello new asset listed in hello **Assets** window.</span></span> 

## <a name="encode-assets"></a><span data-ttu-id="e5a6e-140">Encoder des éléments multimédias</span><span class="sxs-lookup"><span data-stu-id="e5a6e-140">Encode assets</span></span>

<span data-ttu-id="e5a6e-141">Lorsque vous travaillez avec un des scénarios les plus courants de hello transmet les clients tooyour de diffusion en continu à débit adaptatif Azure Media Services.</span><span class="sxs-lookup"><span data-stu-id="e5a6e-141">When working with Azure Media Services one of hello most common scenarios is delivering adaptive bitrate streaming tooyour clients.</span></span> <span data-ttu-id="e5a6e-142">Media Services prend en charge hello suivant des technologies de diffusion en continu de fichiers à débit adaptatif : HTTP Live Streaming (HLS), la diffusion en continu lisse, MPEG DASH.</span><span class="sxs-lookup"><span data-stu-id="e5a6e-142">Media Services supports hello following adaptive bitrate streaming technologies: HTTP Live Streaming (HLS), Smooth Streaming, MPEG DASH.</span></span> <span data-ttu-id="e5a6e-143">tooprepare vos vidéos pour de diffusion en continu à débit adaptatif, vous devez tooencode votre source vidéo dans des fichiers de débits.</span><span class="sxs-lookup"><span data-stu-id="e5a6e-143">tooprepare your videos for adaptive bitrate streaming, you need tooencode your source video into multi-bitrate files.</span></span> <span data-ttu-id="e5a6e-144">Vous devez utiliser hello **Media Encoder Standard** encodeur tooencode vos vidéos.</span><span class="sxs-lookup"><span data-stu-id="e5a6e-144">You should use hello **Media Encoder Standard** encoder tooencode your videos.</span></span>  

<span data-ttu-id="e5a6e-145">Media Services fournit également un empaquetage dynamique, ce qui vous permet de toodeliver votre MP4s débits Bonjour suivant les formats de diffusion en continu : MPEG DASH, HLS, Smooth Streaming, sans que vous ayez toorepackage dans ces formats de diffusion en continu.</span><span class="sxs-lookup"><span data-stu-id="e5a6e-145">Media Services also provides dynamic packaging, which allows you toodeliver your multi-bitrate MP4s in hello following streaming formats: MPEG DASH, HLS, Smooth Streaming, without you having toorepackage into these streaming formats.</span></span> <span data-ttu-id="e5a6e-146">Avec l’empaquetage dynamique, vous devez uniquement toostore et payer pour les fichiers hello dans un seul format de stockage et de Media Services génère et sert de réponse appropriée de hello en fonction des demandes d’un client.</span><span class="sxs-lookup"><span data-stu-id="e5a6e-146">With dynamic packaging, you only need toostore and pay for hello files in single storage format and Media Services builds and serves hello appropriate response based on requests from a client.</span></span>

<span data-ttu-id="e5a6e-147">tootake parti de l’empaquetage dynamique, vous devez tooencode votre fichier source en un ensemble de fichiers MP4 à plusieurs débits (étapes de codage hello sont décrites plus loin dans cette section).</span><span class="sxs-lookup"><span data-stu-id="e5a6e-147">tootake advantage of dynamic packaging, you need tooencode your source file into a set of multi-bitrate MP4 files (hello encoding steps are demonstrated later in this section).</span></span>

### <a name="toouse-hello-portal-tooencode"></a><span data-ttu-id="e5a6e-148">tooencode de portail hello toouse</span><span class="sxs-lookup"><span data-stu-id="e5a6e-148">toouse hello portal tooencode</span></span>
<span data-ttu-id="e5a6e-149">Cette section décrit les étapes à suivre tooencode votre contenu avec Media Encoder Standard hello.</span><span class="sxs-lookup"><span data-stu-id="e5a6e-149">This section describes hello steps you can take tooencode your content with Media Encoder Standard.</span></span>

1. <span data-ttu-id="e5a6e-150">Bonjour **paramètres** fenêtre, sélectionnez **actifs**.</span><span class="sxs-lookup"><span data-stu-id="e5a6e-150">In hello **Settings** window, select **Assets**.</span></span>  
2. <span data-ttu-id="e5a6e-151">Bonjour **actifs** fenêtre, asset hello select que vous aimeriez tooencode.</span><span class="sxs-lookup"><span data-stu-id="e5a6e-151">In hello **Assets** window, select hello asset that you would like tooencode.</span></span>
3. <span data-ttu-id="e5a6e-152">Hello de presse **Encode** bouton.</span><span class="sxs-lookup"><span data-stu-id="e5a6e-152">Press hello **Encode** button.</span></span>
4. <span data-ttu-id="e5a6e-153">Bonjour **encoder un élément multimédia** fenêtre, processeur de « Media Encoder Standard » hello select et une présélection.</span><span class="sxs-lookup"><span data-stu-id="e5a6e-153">In hello **Encode an asset** window, select hello "Media Encoder Standard" processor and a preset.</span></span> <span data-ttu-id="e5a6e-154">Pour plus d’informations sur les présélections, consultez les articles [Utilisation d’Azure Media Encoder Standard pour générer automatiquement une échelle des vitesses de transmission](media-services-autogen-bitrate-ladder-with-mes.md) et [Présélections de travaux pour MES (Media Encoder Standard)](media-services-mes-presets-overview.md).</span><span class="sxs-lookup"><span data-stu-id="e5a6e-154">For information about presets, see [auto-generate a bitrate ladder](media-services-autogen-bitrate-ladder-with-mes.md) and [Task Presets for MES](media-services-mes-presets-overview.md).</span></span> <span data-ttu-id="e5a6e-155">Si vous envisagez toocontrol quelle valeur prédéfinie d’encodage est utilisée, gardez cela à l’esprit : il est important de tooselect hello prédéfini qui convient le mieux pour votre vidéo d’entrée.</span><span class="sxs-lookup"><span data-stu-id="e5a6e-155">If you plan toocontrol which encoding preset is used, keep this in mind: it is important tooselect hello preset that is most appropriate for your input video.</span></span> <span data-ttu-id="e5a6e-156">Par exemple, si vous connaissez votre vidéo d’entrée d’une résolution de 1920 x 1080 pixels, vous pouvez utiliser hello « H264 plusieurs débits binaires 1080p » prédéfini.</span><span class="sxs-lookup"><span data-stu-id="e5a6e-156">For example, if you know your input video has a resolution of 1920x1080 pixels, then you could use hello "H264 Multiple Bitrate 1080p" preset.</span></span> <span data-ttu-id="e5a6e-157">Si vous disposez d’une vidéo basse résolution (640 x 360), il est préférable de ne pas utiliser la présélection « H264 – Vitesse de transmission multiple – 1 080 pixels ».</span><span class="sxs-lookup"><span data-stu-id="e5a6e-157">If you have a low resolution (640x360) video, then you should not be using "H264 Multiple Bitrate 1080p" preset.</span></span>
   
   <span data-ttu-id="e5a6e-158">Pour faciliter la gestion, vous avez une option de modification de nom hello de ressource en sortie hello et nom hello du travail de hello.</span><span class="sxs-lookup"><span data-stu-id="e5a6e-158">For easier management, you have an option of editing hello name of hello output asset, and hello name of hello job.</span></span>
   
   ![Encoder des éléments multimédias](./media/media-services-portal-vod-get-started/media-services-encode1.png)
5. <span data-ttu-id="e5a6e-160">Appuyez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="e5a6e-160">Press **Create**.</span></span>

### <a name="monitor-encoding-job-progress"></a><span data-ttu-id="e5a6e-161">Suivi de la progression de la tâche d’encodage</span><span class="sxs-lookup"><span data-stu-id="e5a6e-161">Monitor encoding job progress</span></span>
<span data-ttu-id="e5a6e-162">progression de hello toomonitor Hello encodage de travail, cliquez sur **paramètres** (en hello haut hello), puis sélectionnez **travaux**.</span><span class="sxs-lookup"><span data-stu-id="e5a6e-162">toomonitor hello progress of hello encoding job, click **Settings** (at hello top of hello page) and then select **Jobs**.</span></span>

![Tâches](./media/media-services-portal-vod-get-started/media-services-jobs.png)

## <a name="publish-content"></a><span data-ttu-id="e5a6e-164">Publication de contenu</span><span class="sxs-lookup"><span data-stu-id="e5a6e-164">Publish content</span></span>
<span data-ttu-id="e5a6e-165">tooprovide votre utilisateur avec une URL qui peut être utilisé toostream ou télécharger votre contenu, vous tout d’abord besoin trop « publier » votre élément multimédia en créant un localisateur.</span><span class="sxs-lookup"><span data-stu-id="e5a6e-165">tooprovide your user with a  URL that can be used toostream or download your content, you first need too"publish" your asset by creating a locator.</span></span> <span data-ttu-id="e5a6e-166">Les localisateurs offrent toofiles accès contenues dans l’élément multimédia de hello.</span><span class="sxs-lookup"><span data-stu-id="e5a6e-166">Locators provide access toofiles contained in hello asset.</span></span> <span data-ttu-id="e5a6e-167">Media Services prend en charge deux types de localisateurs :</span><span class="sxs-lookup"><span data-stu-id="e5a6e-167">Media Services supports two types of locators:</span></span> 

* <span data-ttu-id="e5a6e-168">Diffusion en continu les localisateurs (OnDemandOrigin), utilisés pour la diffusion adaptative en continu (par exemple, toostream MPEG DASH, HLS ou Smooth Streaming).</span><span class="sxs-lookup"><span data-stu-id="e5a6e-168">Streaming (OnDemandOrigin) locators, used for adaptive streaming (for example, toostream MPEG DASH, HLS, or Smooth Streaming).</span></span> <span data-ttu-id="e5a6e-169">toocreate un localisateur de diffusion en continu votre élément multimédia doit contenir un fichier .ism.</span><span class="sxs-lookup"><span data-stu-id="e5a6e-169">toocreate a streaming locator your asset must contain an .ism file.</span></span> 
* <span data-ttu-id="e5a6e-170">les localisateurs progressifs (SAS), utilisés pour la diffusion de vidéo par téléchargement progressif.</span><span class="sxs-lookup"><span data-stu-id="e5a6e-170">Progressive (SAS) locators, used for delivery of video via progressive download.</span></span>

<span data-ttu-id="e5a6e-171">Une URL de diffusion en continu a hello suivant le format et vous pouvez l’utiliser de ressources de diffusion en continu lisse tooplay.</span><span class="sxs-lookup"><span data-stu-id="e5a6e-171">A streaming URL has hello following format and you can use it tooplay Smooth Streaming assets.</span></span>

    {streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest

<span data-ttu-id="e5a6e-172">ajouter des toobuild une URL de diffusion en continu de TLS (format = m3u8-aapl) toohello URL.</span><span class="sxs-lookup"><span data-stu-id="e5a6e-172">toobuild an HLS streaming URL, append (format=m3u8-aapl) toohello URL.</span></span>

    {streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=m3u8-aapl)

<span data-ttu-id="e5a6e-173">ajouter des toobuild une URL de diffusion en continu de MPEG DASH (format = mpd-heure-csf) toohello URL.</span><span class="sxs-lookup"><span data-stu-id="e5a6e-173">toobuild an  MPEG DASH streaming URL, append (format=mpd-time-csf) toohello URL.</span></span>

    {streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=mpd-time-csf)


<span data-ttu-id="e5a6e-174">Une URL SAS a hello suivant le format.</span><span class="sxs-lookup"><span data-stu-id="e5a6e-174">A SAS URL has hello following format.</span></span>

    {blob container name}/{asset name}/{file name}/{SAS signature}

> [!NOTE]
> <span data-ttu-id="e5a6e-175">Si vous avez utilisé les localisateurs toocreate portail hello avant mars 2015, les localisateurs avec une date d’expiration de deux ans ont été créés.</span><span class="sxs-lookup"><span data-stu-id="e5a6e-175">If you used hello portal toocreate locators before March 2015, locators with a two-year expiration date were created.</span></span>  
> 
> 

<span data-ttu-id="e5a6e-176">tooupdate une date d’expiration sur un localisateur, utilisez [reste](https://docs.microsoft.com/rest/api/media/operations/locator#update_a_locator) ou [.NET](http://go.microsoft.com/fwlink/?LinkID=533259) API.</span><span class="sxs-lookup"><span data-stu-id="e5a6e-176">tooupdate an expiration date on a locator, use [REST](https://docs.microsoft.com/rest/api/media/operations/locator#update_a_locator) or [.NET](http://go.microsoft.com/fwlink/?LinkID=533259) APIs.</span></span> <span data-ttu-id="e5a6e-177">Lorsque vous mettez à jour date d’expiration de hello d’un localisateur SAS, hello URL change.</span><span class="sxs-lookup"><span data-stu-id="e5a6e-177">When you update hello expiration date of a SAS locator, hello URL changes.</span></span>

### <a name="toouse-hello-portal-toopublish-an-asset"></a><span data-ttu-id="e5a6e-178">toouse hello toopublish portail un élément multimédia</span><span class="sxs-lookup"><span data-stu-id="e5a6e-178">toouse hello portal toopublish an asset</span></span>
<span data-ttu-id="e5a6e-179">toouse hello toopublish portail un élément multimédia, hello suivant :</span><span class="sxs-lookup"><span data-stu-id="e5a6e-179">toouse hello portal toopublish an asset, do hello following:</span></span>

1. <span data-ttu-id="e5a6e-180">Sélectionnez **Paramètres** > **Éléments multimédias**.</span><span class="sxs-lookup"><span data-stu-id="e5a6e-180">Select **Settings** > **Assets**.</span></span>
2. <span data-ttu-id="e5a6e-181">Sélectionnez asset hello que vous souhaitez toopublish.</span><span class="sxs-lookup"><span data-stu-id="e5a6e-181">Select hello asset that you want toopublish.</span></span>
3. <span data-ttu-id="e5a6e-182">Cliquez sur hello **publier** bouton.</span><span class="sxs-lookup"><span data-stu-id="e5a6e-182">Click hello **Publish** button.</span></span>
4. <span data-ttu-id="e5a6e-183">Sélectionnez le type de localisateur hello.</span><span class="sxs-lookup"><span data-stu-id="e5a6e-183">Select hello locator type.</span></span>
5. <span data-ttu-id="e5a6e-184">Cliquez sur **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="e5a6e-184">Press **Add**.</span></span>
   
    ![Publier](./media/media-services-portal-vod-get-started/media-services-publish1.png)

<span data-ttu-id="e5a6e-186">Hello URL est ajouté à la liste des toohello **URL de publication**.</span><span class="sxs-lookup"><span data-stu-id="e5a6e-186">hello URL is added toohello list of **Published URLs**.</span></span>

## <a name="play-content-from-hello-portal"></a><span data-ttu-id="e5a6e-187">Lire le contenu à partir du portail de hello</span><span class="sxs-lookup"><span data-stu-id="e5a6e-187">Play content from hello portal</span></span>
<span data-ttu-id="e5a6e-188">portail Azure Hello fournit un lecteur de contenu que vous pouvez utiliser tootest votre vidéo.</span><span class="sxs-lookup"><span data-stu-id="e5a6e-188">hello Azure portal provides a content player that you can use tootest your video.</span></span>

<span data-ttu-id="e5a6e-189">Vidéo de hello souhaité, puis cliquez sur hello **lire** bouton.</span><span class="sxs-lookup"><span data-stu-id="e5a6e-189">Click hello desired video and then click hello **Play** button.</span></span>

![Publier](./media/media-services-portal-vod-get-started/media-services-play.png)

<span data-ttu-id="e5a6e-191">Certaines considérations s’appliquent :</span><span class="sxs-lookup"><span data-stu-id="e5a6e-191">Some considerations apply:</span></span>

* <span data-ttu-id="e5a6e-192">toobegin de diffusion en continu, démarrage en cours d’exécution hello **par défaut** point de terminaison de diffusion en continu.</span><span class="sxs-lookup"><span data-stu-id="e5a6e-192">toobegin streaming, start running hello **default** streaming endpoint.</span></span>
* <span data-ttu-id="e5a6e-193">Vérifiez que hello vidéo a été publié.</span><span class="sxs-lookup"><span data-stu-id="e5a6e-193">Make sure hello video has been published.</span></span>
* <span data-ttu-id="e5a6e-194">Cela **Media player** est lu à partir du point de terminaison de diffusion en continu de la valeur par défaut hello.</span><span class="sxs-lookup"><span data-stu-id="e5a6e-194">This **Media player** plays from hello default streaming endpoint.</span></span> <span data-ttu-id="e5a6e-195">Si vous souhaitez tooplay à partir d’un élément non défini par défaut diffusion en continu de point de terminaison, cliquez sur l’URL toocopy hello et utilisez un autre lecteur.</span><span class="sxs-lookup"><span data-stu-id="e5a6e-195">If you want tooplay from a non-default streaming endpoint, click toocopy hello URL and use another player.</span></span> <span data-ttu-id="e5a6e-196">par exemple, le [lecteur Azure Media Services](http://amsplayer.azurewebsites.net/azuremediaplayer.html).</span><span class="sxs-lookup"><span data-stu-id="e5a6e-196">For example, [Azure Media Services Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html).</span></span>

## <a name="next-steps"></a><span data-ttu-id="e5a6e-197">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="e5a6e-197">Next steps</span></span>
<span data-ttu-id="e5a6e-198">Consultez les parcours d’apprentissage de Media Services.</span><span class="sxs-lookup"><span data-stu-id="e5a6e-198">Review Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="e5a6e-199">Fournir des commentaires</span><span class="sxs-lookup"><span data-stu-id="e5a6e-199">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

