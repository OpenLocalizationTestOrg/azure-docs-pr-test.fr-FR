---
title: "Prise en main de la diffusion de contenu vidéo à la demande (VoD) à l’aide du portail Azure | Microsoft Docs"
description: "Ce didacticiel explique comment implémenter un service de base de diffusion de contenu vidéo à la demande (VoD) avec l’application Azure Media Services (AMS) à l’aide du portail Azure."
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
ms.openlocfilehash: a8eeeeff412837acba14b441a3c590edf7e3597a
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="get-started-with-delivering-content-on-demand-using-the-azure-portal"></a><span data-ttu-id="1a256-103">Prendre en main la diffusion de contenus à la demande à l’aide du portail Azure</span><span class="sxs-lookup"><span data-stu-id="1a256-103">Get started with delivering content on demand using the Azure portal</span></span>
[!INCLUDE [media-services-selector-get-started](../../includes/media-services-selector-get-started.md)]

<span data-ttu-id="1a256-104">Ce didacticiel explique comment implémenter un service de base de diffusion de contenu vidéo à la demande (VoD) avec l’application Azure Media Services (AMS) à l’aide du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="1a256-104">This tutorial walks you through the steps of implementing a basic Video-on-Demand (VoD) content delivery service with Azure Media Services (AMS) application using the Azure portal.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1a256-105">Composants requis</span><span class="sxs-lookup"><span data-stu-id="1a256-105">Prerequisites</span></span>
<span data-ttu-id="1a256-106">Les éléments suivants sont requis pour suivre le didacticiel :</span><span class="sxs-lookup"><span data-stu-id="1a256-106">The following are required to complete the tutorial:</span></span>

* <span data-ttu-id="1a256-107">Un compte Azure.</span><span class="sxs-lookup"><span data-stu-id="1a256-107">An Azure account.</span></span> <span data-ttu-id="1a256-108">Pour plus d'informations, consultez la page [Version d'évaluation gratuite d'Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="1a256-108">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 
* <span data-ttu-id="1a256-109">Un compte Media Services.</span><span class="sxs-lookup"><span data-stu-id="1a256-109">A Media Services account.</span></span> <span data-ttu-id="1a256-110">Pour créer un compte Media Services, consultez [Création d’un compte Media Services](media-services-portal-create-account.md).</span><span class="sxs-lookup"><span data-stu-id="1a256-110">To create a Media Services account, see [How to Create a Media Services Account](media-services-portal-create-account.md).</span></span>

<span data-ttu-id="1a256-111">Ce didacticiel comprend les tâches suivantes :</span><span class="sxs-lookup"><span data-stu-id="1a256-111">This tutorial includes the following tasks:</span></span>

1. <span data-ttu-id="1a256-112">Démarrer un point de terminaison de streaming.</span><span class="sxs-lookup"><span data-stu-id="1a256-112">Start streaming endpoint.</span></span>
2. <span data-ttu-id="1a256-113">Télécharger un fichier vidéo.</span><span class="sxs-lookup"><span data-stu-id="1a256-113">Upload a video file.</span></span>
3. <span data-ttu-id="1a256-114">Encoder le fichier source en un ensemble de fichiers MP4 à débit adaptatif.</span><span class="sxs-lookup"><span data-stu-id="1a256-114">Encode the source file into a set of adaptive bitrate MP4 files.</span></span>
4. <span data-ttu-id="1a256-115">Publier l'élément multimédia et obtenir les URL de diffusion et de téléchargement progressif.</span><span class="sxs-lookup"><span data-stu-id="1a256-115">Publish the asset and get streaming and progressive download URLs.</span></span>  
5. <span data-ttu-id="1a256-116">Lire votre contenu.</span><span class="sxs-lookup"><span data-stu-id="1a256-116">Play your content.</span></span>

## <a name="start-streaming-endpoints"></a><span data-ttu-id="1a256-117">Démarrer les points de terminaison de streaming</span><span class="sxs-lookup"><span data-stu-id="1a256-117">Start streaming endpoints</span></span> 

<span data-ttu-id="1a256-118">Lorsque vous utilisez Azure Media Services, la diffusion de vidéos en continu à débit binaire adaptatif constitue l’un des scénarios les plus courants.</span><span class="sxs-lookup"><span data-stu-id="1a256-118">When working with Azure Media Services one of the most common scenarios is delivering video via adaptive bitrate streaming.</span></span> <span data-ttu-id="1a256-119">Media Services assure l’empaquetage dynamique, qui vous permet de distribuer juste-à-temps un contenu encodé en MP4 à débit adaptatif dans un format de diffusion en continu pris en charge par Media Services (MPEG DASH, HLS, Smooth Streaming), sans qu’il vous soit nécessaire de stocker des versions pré-empaquetées de chacun de ces formats.</span><span class="sxs-lookup"><span data-stu-id="1a256-119">Media Services provides dynamic packaging, which allows you to deliver your adaptive bitrate MP4 encoded content in streaming formats supported by Media Services (MPEG DASH, HLS, Smooth Streaming) just-in-time, without you having to store pre-packaged versions of each of these streaming formats.</span></span>

>[!NOTE]
><span data-ttu-id="1a256-120">Une fois votre compte AMS créé, un point de terminaison de streaming **par défaut** est ajouté à votre compte à l’état **Arrêté**.</span><span class="sxs-lookup"><span data-stu-id="1a256-120">When your AMS account is created a **default** streaming endpoint is added to your account in the **Stopped** state.</span></span> <span data-ttu-id="1a256-121">Pour démarrer la diffusion en continu de votre contenu et tirer parti de l’empaquetage et du chiffrement dynamiques, le point de terminaison de streaming à partir duquel vous souhaitez diffuser du contenu doit se trouver à l’état **En cours d’exécution**.</span><span class="sxs-lookup"><span data-stu-id="1a256-121">To start streaming your content and take advantage of dynamic packaging and dynamic encryption, the streaming endpoint from which you want to stream content has to be in the **Running** state.</span></span> 

<span data-ttu-id="1a256-122">Pour démarrer le point de terminaison de streaming, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="1a256-122">To start the streaming endpoint, do the following:</span></span>

1. <span data-ttu-id="1a256-123">Connectez-vous au [portail Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="1a256-123">Log in at the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="1a256-124">Dans la fenêtre Paramètres, cliquez sur Points de terminaison de streaming.</span><span class="sxs-lookup"><span data-stu-id="1a256-124">In the Settings window, click Streaming endpoints.</span></span> 
3. <span data-ttu-id="1a256-125">Cliquez sur le point de terminaison de diffusion en continu par défaut.</span><span class="sxs-lookup"><span data-stu-id="1a256-125">Click the default streaming endpoint.</span></span> 

    <span data-ttu-id="1a256-126">La fenêtre DEFAULT STREAMING ENDPOINT DETAILS (DÉTAILS DU POINT DE TERMINAISON DE STREAMING PAR DÉFAUT) s’affiche.</span><span class="sxs-lookup"><span data-stu-id="1a256-126">The DEFAULT STREAMING ENDPOINT DETAILS window appears.</span></span>

4. <span data-ttu-id="1a256-127">Cliquez sur l’icône de démarrage.</span><span class="sxs-lookup"><span data-stu-id="1a256-127">Click the Start icon.</span></span>
5. <span data-ttu-id="1a256-128">Cliquez sur le bouton Enregistrer pour enregistrer vos modifications.</span><span class="sxs-lookup"><span data-stu-id="1a256-128">Click the Save button to save your changes.</span></span>

## <a name="upload-files"></a><span data-ttu-id="1a256-129">Charger des fichiers</span><span class="sxs-lookup"><span data-stu-id="1a256-129">Upload files</span></span>
<span data-ttu-id="1a256-130">Pour diffuser des vidéos en continu à l’aide d’Azure Media Services, vous devez télécharger les vidéos source, les encoder en plusieurs débits binaires et publier le résultat.</span><span class="sxs-lookup"><span data-stu-id="1a256-130">To stream videos using Azure Media Services, you need to upload the source videos, encode them into multiple bitrates, and publish the result.</span></span> <span data-ttu-id="1a256-131">Cette section décrit la première étape du processus.</span><span class="sxs-lookup"><span data-stu-id="1a256-131">The first step is covered in this section.</span></span> 

1. <span data-ttu-id="1a256-132">Dans la fenêtre **Paramètres**, cliquez sur **Éléments multimédias**.</span><span class="sxs-lookup"><span data-stu-id="1a256-132">In the **Setting** window, click **Assets**.</span></span>
   
    ![Charger des fichiers](./media/media-services-portal-vod-get-started/media-services-upload.png)
2. <span data-ttu-id="1a256-134">Cliquez sur le bouton **Télécharger** .</span><span class="sxs-lookup"><span data-stu-id="1a256-134">Click the **Upload** button.</span></span>
   
    <span data-ttu-id="1a256-135">La fenêtre **Upload a video asset** (Charger un élément multimédia vidéo) s’affiche.</span><span class="sxs-lookup"><span data-stu-id="1a256-135">The **Upload a video asset** window appears.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="1a256-136">Il n’existe aucune limite de taille de fichier.</span><span class="sxs-lookup"><span data-stu-id="1a256-136">There is no file size limitation.</span></span>
   > 
   > 
3. <span data-ttu-id="1a256-137">Accédez à la vidéo de votre choix sur votre ordinateur, sélectionnez-la, puis cliquez sur OK.</span><span class="sxs-lookup"><span data-stu-id="1a256-137">Browse to the desired video on your computer, select it, and hit OK.</span></span>  
   
    <span data-ttu-id="1a256-138">Le chargement démarre ; vous pouvez en voir la progression sous le nom du fichier.</span><span class="sxs-lookup"><span data-stu-id="1a256-138">The upload starts and you can see the progress under the file name.</span></span>  

<span data-ttu-id="1a256-139">Une fois le chargement terminé, le nouvel élément multimédia s’affiche dans la fenêtre **Éléments multimédias** .</span><span class="sxs-lookup"><span data-stu-id="1a256-139">Once the upload completes, you see the new asset listed in the **Assets** window.</span></span> 

## <a name="encode-assets"></a><span data-ttu-id="1a256-140">Encoder des éléments multimédias</span><span class="sxs-lookup"><span data-stu-id="1a256-140">Encode assets</span></span>

<span data-ttu-id="1a256-141">Lorsque vous travaillez avec Azure Media Services, un des scénarios les plus courants est la diffusion de contenu à débit adaptatif à vos clients.</span><span class="sxs-lookup"><span data-stu-id="1a256-141">When working with Azure Media Services one of the most common scenarios is delivering adaptive bitrate streaming to your clients.</span></span> <span data-ttu-id="1a256-142">Media Services prend en charge les technologies de streaming à débit adaptatif suivantes : HTTP Live Streaming (HLS), Smooth Streaming, MPEG DASH.</span><span class="sxs-lookup"><span data-stu-id="1a256-142">Media Services supports the following adaptive bitrate streaming technologies: HTTP Live Streaming (HLS), Smooth Streaming, MPEG DASH.</span></span> <span data-ttu-id="1a256-143">Pour préparer vos vidéos au streaming à débit adaptatif, vous devez encoder votre vidéo source en fichiers à débit binaire multiple.</span><span class="sxs-lookup"><span data-stu-id="1a256-143">To prepare your videos for adaptive bitrate streaming, you need to encode your source video into multi-bitrate files.</span></span> <span data-ttu-id="1a256-144">Vous devez utiliser **Media Encoder Standard** pour encoder vos vidéos.</span><span class="sxs-lookup"><span data-stu-id="1a256-144">You should use the **Media Encoder Standard** encoder to encode your videos.</span></span>  

<span data-ttu-id="1a256-145">Media Services assure également l’empaquetage dynamique qui vous permet de diffuser des fichiers MP4 multidébit dans les formats de diffusion en continu MPEG DASH, HLS ou Smooth Streaming sans avoir à effectuer de ré-empaquetage dans ces formats.</span><span class="sxs-lookup"><span data-stu-id="1a256-145">Media Services also provides dynamic packaging, which allows you to deliver your multi-bitrate MP4s in the following streaming formats: MPEG DASH, HLS, Smooth Streaming, without you having to repackage into these streaming formats.</span></span> <span data-ttu-id="1a256-146">L’empaquetage dynamique vous permet de ne stocker et payer les fichiers que dans un seul format de stockage. Ensuite, Media Services crée et fournit la réponse appropriée en fonction des demandes des clients.</span><span class="sxs-lookup"><span data-stu-id="1a256-146">With dynamic packaging, you only need to store and pay for the files in single storage format and Media Services builds and serves the appropriate response based on requests from a client.</span></span>

<span data-ttu-id="1a256-147">Pour tirer parti de l’empaquetage dynamique, vous devez encoder votre fichier source dans un ensemble de fichiers MP4 multidébit (les étapes de l’encodage sont décrites plus loin dans cette section).</span><span class="sxs-lookup"><span data-stu-id="1a256-147">To take advantage of dynamic packaging, you need to encode your source file into a set of multi-bitrate MP4 files (the encoding steps are demonstrated later in this section).</span></span>

### <a name="to-use-the-portal-to-encode"></a><span data-ttu-id="1a256-148">Pour effectuer l’encodage à l’aide du portail</span><span class="sxs-lookup"><span data-stu-id="1a256-148">To use the portal to encode</span></span>
<span data-ttu-id="1a256-149">Cette section décrit les étapes à suivre pour encoder votre contenu avec Media Encoder Standard.</span><span class="sxs-lookup"><span data-stu-id="1a256-149">This section describes the steps you can take to encode your content with Media Encoder Standard.</span></span>

1. <span data-ttu-id="1a256-150">Dans la fenêtre **Paramètres**, sélectionnez **Éléments multimédias**.</span><span class="sxs-lookup"><span data-stu-id="1a256-150">In the **Settings** window, select **Assets**.</span></span>  
2. <span data-ttu-id="1a256-151">Dans la fenêtre **Éléments multimédias** , sélectionnez l’élément que vous souhaitez encoder.</span><span class="sxs-lookup"><span data-stu-id="1a256-151">In the **Assets** window, select the asset that you would like to encode.</span></span>
3. <span data-ttu-id="1a256-152">Appuyez sur le bouton **Encoder** .</span><span class="sxs-lookup"><span data-stu-id="1a256-152">Press the **Encode** button.</span></span>
4. <span data-ttu-id="1a256-153">Dans la fenêtre **Encoder un élément multimédia**, sélectionnez le processeur Media Encoder Standard et choisissez une présélection.</span><span class="sxs-lookup"><span data-stu-id="1a256-153">In the **Encode an asset** window, select the "Media Encoder Standard" processor and a preset.</span></span> <span data-ttu-id="1a256-154">Pour plus d’informations sur les présélections, consultez les articles [Utilisation d’Azure Media Encoder Standard pour générer automatiquement une échelle des vitesses de transmission](media-services-autogen-bitrate-ladder-with-mes.md) et [Présélections de travaux pour MES (Media Encoder Standard)](media-services-mes-presets-overview.md).</span><span class="sxs-lookup"><span data-stu-id="1a256-154">For information about presets, see [auto-generate a bitrate ladder](media-services-autogen-bitrate-ladder-with-mes.md) and [Task Presets for MES](media-services-mes-presets-overview.md).</span></span> <span data-ttu-id="1a256-155">Si vous envisagez de contrôler la présélection d’encodage à utiliser, n’oubliez pas qu’il est important de sélectionner la présélection qui convient le mieux à votre vidéo d’entrée.</span><span class="sxs-lookup"><span data-stu-id="1a256-155">If you plan to control which encoding preset is used, keep this in mind: it is important to select the preset that is most appropriate for your input video.</span></span> <span data-ttu-id="1a256-156">Par exemple, si vous savez que votre vidéo d’entrée possède une résolution de 1920 x 1080 pixels, vous pouvez utiliser la présélection « H264 Multiple Bitrate 1080p ».</span><span class="sxs-lookup"><span data-stu-id="1a256-156">For example, if you know your input video has a resolution of 1920x1080 pixels, then you could use the "H264 Multiple Bitrate 1080p" preset.</span></span> <span data-ttu-id="1a256-157">Si vous disposez d’une vidéo basse résolution (640 x 360), il est préférable de ne pas utiliser la présélection « H264 – Vitesse de transmission multiple – 1 080 pixels ».</span><span class="sxs-lookup"><span data-stu-id="1a256-157">If you have a low resolution (640x360) video, then you should not be using "H264 Multiple Bitrate 1080p" preset.</span></span>
   
   <span data-ttu-id="1a256-158">Pour des questions pratiques, vous avez la possibilité de modifier le nom de l’élément multimédia de sortie ainsi que le nom de la tâche.</span><span class="sxs-lookup"><span data-stu-id="1a256-158">For easier management, you have an option of editing the name of the output asset, and the name of the job.</span></span>
   
   ![Encoder des éléments multimédias](./media/media-services-portal-vod-get-started/media-services-encode1.png)
5. <span data-ttu-id="1a256-160">Appuyez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="1a256-160">Press **Create**.</span></span>

### <a name="monitor-encoding-job-progress"></a><span data-ttu-id="1a256-161">Suivi de la progression de la tâche d’encodage</span><span class="sxs-lookup"><span data-stu-id="1a256-161">Monitor encoding job progress</span></span>
<span data-ttu-id="1a256-162">Pour surveiller la progression du travail d’encodage, cliquez sur **Paramètres** (en haut de la page), puis sélectionnez **Travaux**.</span><span class="sxs-lookup"><span data-stu-id="1a256-162">To monitor the progress of the encoding job, click **Settings** (at the top of the page) and then select **Jobs**.</span></span>

![Travaux](./media/media-services-portal-vod-get-started/media-services-jobs.png)

## <a name="publish-content"></a><span data-ttu-id="1a256-164">Publication de contenu</span><span class="sxs-lookup"><span data-stu-id="1a256-164">Publish content</span></span>
<span data-ttu-id="1a256-165">Pour fournir aux utilisateurs une URL pouvant être utilisée pour diffuser en continu ou télécharger votre contenu, vous devez d’abord « publier » votre élément multimédia en créant un localisateur.</span><span class="sxs-lookup"><span data-stu-id="1a256-165">To provide your user with a  URL that can be used to stream or download your content, you first need to "publish" your asset by creating a locator.</span></span> <span data-ttu-id="1a256-166">Les localisateurs assurent l’accès aux fichiers contenus dans l’élément multimédia.</span><span class="sxs-lookup"><span data-stu-id="1a256-166">Locators provide access to files contained in the asset.</span></span> <span data-ttu-id="1a256-167">Media Services prend en charge deux types de localisateurs :</span><span class="sxs-lookup"><span data-stu-id="1a256-167">Media Services supports two types of locators:</span></span> 

* <span data-ttu-id="1a256-168">les localisateurs de diffusion en continu (OnDemandOrigin), utilisés pour la diffusion adaptative (par exemple, MPEG DASH, HLS ou Smooth Streaming) ;</span><span class="sxs-lookup"><span data-stu-id="1a256-168">Streaming (OnDemandOrigin) locators, used for adaptive streaming (for example, to stream MPEG DASH, HLS, or Smooth Streaming).</span></span> <span data-ttu-id="1a256-169">Pour créer un localisateur de diffusion en continu, votre élément multimédia doit contenir un fichier .ism ;</span><span class="sxs-lookup"><span data-stu-id="1a256-169">To create a streaming locator your asset must contain an .ism file.</span></span> 
* <span data-ttu-id="1a256-170">les localisateurs progressifs (SAS), utilisés pour la diffusion de vidéo par téléchargement progressif.</span><span class="sxs-lookup"><span data-stu-id="1a256-170">Progressive (SAS) locators, used for delivery of video via progressive download.</span></span>

<span data-ttu-id="1a256-171">Les URL de diffusion en continu, que vous pouvez utiliser pour lire des éléments multimédias Smooth Streaming, ont le format suivant.</span><span class="sxs-lookup"><span data-stu-id="1a256-171">A streaming URL has the following format and you can use it to play Smooth Streaming assets.</span></span>

    {streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest

<span data-ttu-id="1a256-172">Pour créer une URL de diffusion en continu HLS, ajoutez (format=m3u8-aapl) à l’URL.</span><span class="sxs-lookup"><span data-stu-id="1a256-172">To build an HLS streaming URL, append (format=m3u8-aapl) to the URL.</span></span>

    {streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=m3u8-aapl)

<span data-ttu-id="1a256-173">Pour créer une URL de diffusion en continu MPEG DASH, ajoutez (format=mpd-time-csf) à l’URL.</span><span class="sxs-lookup"><span data-stu-id="1a256-173">To build an  MPEG DASH streaming URL, append (format=mpd-time-csf) to the URL.</span></span>

    {streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=mpd-time-csf)


<span data-ttu-id="1a256-174">Une URL SAS a le format suivant :</span><span class="sxs-lookup"><span data-stu-id="1a256-174">A SAS URL has the following format.</span></span>

    {blob container name}/{asset name}/{file name}/{SAS signature}

> [!NOTE]
> <span data-ttu-id="1a256-175">Si vous avez utilisé le portail pour créer des localisateurs avant mars 2015, les localisateurs présentant une date d’expiration de deux ans sont ceux qui ont été créés.</span><span class="sxs-lookup"><span data-stu-id="1a256-175">If you used the portal to create locators before March 2015, locators with a two-year expiration date were created.</span></span>  
> 
> 

<span data-ttu-id="1a256-176">Pour mettre à jour la date d’expiration d’un localisateur, utilisez les API [REST](https://docs.microsoft.com/rest/api/media/operations/locator#update_a_locator) ou [.NET](http://go.microsoft.com/fwlink/?LinkID=533259).</span><span class="sxs-lookup"><span data-stu-id="1a256-176">To update an expiration date on a locator, use [REST](https://docs.microsoft.com/rest/api/media/operations/locator#update_a_locator) or [.NET](http://go.microsoft.com/fwlink/?LinkID=533259) APIs.</span></span> <span data-ttu-id="1a256-177">Lorsque vous mettez à jour la date d’expiration d’un localisateur SAS, l’URL est modifiée.</span><span class="sxs-lookup"><span data-stu-id="1a256-177">When you update the expiration date of a SAS locator, the URL changes.</span></span>

### <a name="to-use-the-portal-to-publish-an-asset"></a><span data-ttu-id="1a256-178">Pour publier un élément multimédia à l’aide du portail</span><span class="sxs-lookup"><span data-stu-id="1a256-178">To use the portal to publish an asset</span></span>
<span data-ttu-id="1a256-179">Pour utiliser le portail pour publier un élément multimédia, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="1a256-179">To use the portal to publish an asset, do the following:</span></span>

1. <span data-ttu-id="1a256-180">Sélectionnez **Paramètres** > **Éléments multimédias**.</span><span class="sxs-lookup"><span data-stu-id="1a256-180">Select **Settings** > **Assets**.</span></span>
2. <span data-ttu-id="1a256-181">Sélectionnez l’élément que vous souhaitez publier.</span><span class="sxs-lookup"><span data-stu-id="1a256-181">Select the asset that you want to publish.</span></span>
3. <span data-ttu-id="1a256-182">Cliquez sur le bouton **Publier** .</span><span class="sxs-lookup"><span data-stu-id="1a256-182">Click the **Publish** button.</span></span>
4. <span data-ttu-id="1a256-183">Sélectionnez le type de localisateur.</span><span class="sxs-lookup"><span data-stu-id="1a256-183">Select the locator type.</span></span>
5. <span data-ttu-id="1a256-184">Cliquez sur **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="1a256-184">Press **Add**.</span></span>
   
    ![Publier](./media/media-services-portal-vod-get-started/media-services-publish1.png)

<span data-ttu-id="1a256-186">L’URL est ajoutée à la liste des **URL publiées**.</span><span class="sxs-lookup"><span data-stu-id="1a256-186">The URL is added to the list of **Published URLs**.</span></span>

## <a name="play-content-from-the-portal"></a><span data-ttu-id="1a256-187">Lecture de contenu sur le portail</span><span class="sxs-lookup"><span data-stu-id="1a256-187">Play content from the portal</span></span>
<span data-ttu-id="1a256-188">Le portail Azure propose un lecteur de contenu que vous pouvez utiliser pour tester votre vidéo.</span><span class="sxs-lookup"><span data-stu-id="1a256-188">The Azure portal provides a content player that you can use to test your video.</span></span>

<span data-ttu-id="1a256-189">Cliquez sur la vidéo de votre choix, puis sur le bouton **Lire** .</span><span class="sxs-lookup"><span data-stu-id="1a256-189">Click the desired video and then click the **Play** button.</span></span>

![Publier](./media/media-services-portal-vod-get-started/media-services-play.png)

<span data-ttu-id="1a256-191">Certaines considérations s’appliquent :</span><span class="sxs-lookup"><span data-stu-id="1a256-191">Some considerations apply:</span></span>

* <span data-ttu-id="1a256-192">Pour commencer le streaming, démarrez l’exécution du point de terminaison de streaming **par défaut**.</span><span class="sxs-lookup"><span data-stu-id="1a256-192">To begin streaming, start running the **default** streaming endpoint.</span></span>
* <span data-ttu-id="1a256-193">Assurez-vous que la vidéo a été publiée.</span><span class="sxs-lookup"><span data-stu-id="1a256-193">Make sure the video has been published.</span></span>
* <span data-ttu-id="1a256-194">Le **lecteur multimédia** effectue la lecture à partir du point de terminaison de diffusion en continu par défaut.</span><span class="sxs-lookup"><span data-stu-id="1a256-194">This **Media player** plays from the default streaming endpoint.</span></span> <span data-ttu-id="1a256-195">Si vous souhaitez lire à partir d’un autre point de terminaison de diffusion en continu que celui par défaut, cliquez sur l’URL pour la copier et utilisez un autre lecteur,</span><span class="sxs-lookup"><span data-stu-id="1a256-195">If you want to play from a non-default streaming endpoint, click to copy the URL and use another player.</span></span> <span data-ttu-id="1a256-196">par exemple, le [lecteur Azure Media Services](http://amsplayer.azurewebsites.net/azuremediaplayer.html).</span><span class="sxs-lookup"><span data-stu-id="1a256-196">For example, [Azure Media Services Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html).</span></span>

## <a name="next-steps"></a><span data-ttu-id="1a256-197">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="1a256-197">Next steps</span></span>
<span data-ttu-id="1a256-198">Consultez les parcours d’apprentissage de Media Services.</span><span class="sxs-lookup"><span data-stu-id="1a256-198">Review Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="1a256-199">Fournir des commentaires</span><span class="sxs-lookup"><span data-stu-id="1a256-199">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

