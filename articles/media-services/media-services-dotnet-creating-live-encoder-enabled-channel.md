---
title: "aaaHow tooperform diffusion en continu à l’aide de flux de débits toocreate Azure Media Services avec .NET | Documents Microsoft"
description: "Parcours de ce didacticiel vous guide dans les étapes de hello de création d’un canal qui reçoit une vitesse de transmission unique flux dynamique et le code toomulti débits de flux de données à l’aide du Kit de développement .NET."
services: media-services
documentationcenter: 
author: anilmur
manager: cfowler
editor: 
ms.assetid: 4df5e690-ff63-47cc-879b-9c57cb8ec240
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/17/2017
ms.author: juliako;anilmur
ms.openlocfilehash: 22088e6a78a49bd839575614a7c17a411ae8081c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooperform-live-streaming-using-azure-media-services-toocreate-multi-bitrate-streams-with-net"></a><span data-ttu-id="e02a4-103">Comment tooperform diffusion en continu à l’aide de débits toocreate d’Azure Media Services diffuse en continu avec .NET</span><span class="sxs-lookup"><span data-stu-id="e02a4-103">How tooperform live streaming using Azure Media Services toocreate multi-bitrate streams with .NET</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="e02a4-104">Portail</span><span class="sxs-lookup"><span data-stu-id="e02a4-104">Portal</span></span>](media-services-portal-creating-live-encoder-enabled-channel.md)
> * [<span data-ttu-id="e02a4-105">.NET</span><span class="sxs-lookup"><span data-stu-id="e02a4-105">.NET</span></span>](media-services-dotnet-creating-live-encoder-enabled-channel.md)
> * [<span data-ttu-id="e02a4-106">API REST</span><span class="sxs-lookup"><span data-stu-id="e02a4-106">REST API</span></span>](https://docs.microsoft.com/rest/api/media/operations/channel)
> 
> [!NOTE]
> <span data-ttu-id="e02a4-107">toocomplete ce didacticiel, vous avez besoin d’un compte Azure.</span><span class="sxs-lookup"><span data-stu-id="e02a4-107">toocomplete this tutorial, you need an Azure account.</span></span> <span data-ttu-id="e02a4-108">Pour plus d'informations, consultez la page [Version d'évaluation gratuite d'Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F).</span><span class="sxs-lookup"><span data-stu-id="e02a4-108">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F).</span></span>
> 
> 

## <a name="overview"></a><span data-ttu-id="e02a4-109">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="e02a4-109">Overview</span></span>
<span data-ttu-id="e02a4-110">Ce didacticiel vous guide tout au long des étapes hello de création d’un **canal** qui reçoit un flux en direct à vitesse de transmission unique et qu’elle l’encode les flux de débits binaires toomulti.</span><span class="sxs-lookup"><span data-stu-id="e02a4-110">This tutorial walks you through hello steps of creating a **Channel** that receives a single-bitrate live stream and encodes it toomulti-bitrate stream.</span></span>

<span data-ttu-id="e02a4-111">Pour plus d’informations conceptuelles tooChannels connexes qui sont activés pour l’encodage live, consultez [en continu à l’aide de flux de débits Azure Media Services toocreate](media-services-manage-live-encoder-enabled-channels.md).</span><span class="sxs-lookup"><span data-stu-id="e02a4-111">For more conceptual information related tooChannels that are enabled for live encoding, see [Live streaming using Azure Media Services toocreate multi-bitrate streams](media-services-manage-live-encoder-enabled-channels.md).</span></span>

## <a name="common-live-streaming-scenario"></a><span data-ttu-id="e02a4-112">Scénario courant de diffusion dynamique en continu</span><span class="sxs-lookup"><span data-stu-id="e02a4-112">Common Live Streaming Scenario</span></span>
<span data-ttu-id="e02a4-113">Hello suit décrire les tâches impliquées dans la création d’applications de diffusion en continu live courantes.</span><span class="sxs-lookup"><span data-stu-id="e02a4-113">hello following steps describe tasks involved in creating common live streaming applications.</span></span>

> [!NOTE]
> <span data-ttu-id="e02a4-114">Actuellement, hello maximum recommandé de durée d’un événement en direct est de 8 heures.</span><span class="sxs-lookup"><span data-stu-id="e02a4-114">Currently, hello max recommended duration of a live event is 8 hours.</span></span> <span data-ttu-id="e02a4-115">Si vous avez besoin d’un canal de toorun pour de longues périodes, contactez amslived Microsoft.com.</span><span class="sxs-lookup"><span data-stu-id="e02a4-115">Please contact amslived at Microsoft.com if you need toorun a Channel for longer periods of time.</span></span>
> 
> 

1. <span data-ttu-id="e02a4-116">Connecter un ordinateur de tooa caméra vidéo.</span><span class="sxs-lookup"><span data-stu-id="e02a4-116">Connect a video camera tooa computer.</span></span> <span data-ttu-id="e02a4-117">Lancer et configurer un encodeur dynamique local qui peut afficher un flux à débit binaire unique dans un des hello suivant protocoles : RTMP, diffusion en continu lisse ou RTP (MPEG-TS).</span><span class="sxs-lookup"><span data-stu-id="e02a4-117">Launch and configure an on-premises live encoder that can output a single bitrate stream in one of hello following protocols: RTMP, Smooth Streaming, or RTP (MPEG-TS).</span></span> <span data-ttu-id="e02a4-118">Pour plus d’informations, voir [Prise en charge RTMP et encodeurs dynamiques dans Azure Media Services](http://go.microsoft.com/fwlink/?LinkId=532824).</span><span class="sxs-lookup"><span data-stu-id="e02a4-118">For more information, see [Azure Media Services RTMP Support and Live Encoders](http://go.microsoft.com/fwlink/?LinkId=532824).</span></span>

    <span data-ttu-id="e02a4-119">Cette étape peut également être effectuée après la création du canal.</span><span class="sxs-lookup"><span data-stu-id="e02a4-119">This step could also be performed after you create your Channel.</span></span>

2. <span data-ttu-id="e02a4-120">Créez et démarrez un canal.</span><span class="sxs-lookup"><span data-stu-id="e02a4-120">Create and start a Channel.</span></span>
3. <span data-ttu-id="e02a4-121">URL de réception récupérer hello canal.</span><span class="sxs-lookup"><span data-stu-id="e02a4-121">Retrieve hello Channel ingest URL.</span></span>

    <span data-ttu-id="e02a4-122">URL de réception Hello est utilisé par hello encodeur en temps réel toosend hello flux toohello canal.</span><span class="sxs-lookup"><span data-stu-id="e02a4-122">hello ingest URL is used by hello live encoder toosend hello stream toohello Channel.</span></span>

4. <span data-ttu-id="e02a4-123">Récupérer l’URL d’aperçu hello canal.</span><span class="sxs-lookup"><span data-stu-id="e02a4-123">Retrieve hello Channel preview URL.</span></span>

    <span data-ttu-id="e02a4-124">Utilisez cette tooverify URL que votre canal reçoit correctement les flux live hello.</span><span class="sxs-lookup"><span data-stu-id="e02a4-124">Use this URL tooverify that your channel is properly receiving hello live stream.</span></span>

5. <span data-ttu-id="e02a4-125">Créez un élément multimédia.</span><span class="sxs-lookup"><span data-stu-id="e02a4-125">Create an asset.</span></span>
6. <span data-ttu-id="e02a4-126">Si vous souhaitez pour hello asset toobe est chiffré dynamiquement pendant la lecture, hello suivant :</span><span class="sxs-lookup"><span data-stu-id="e02a4-126">If you want for hello asset toobe dynamically encrypted during playback, do hello following:</span></span>
7. <span data-ttu-id="e02a4-127">Créez une clé de contenu.</span><span class="sxs-lookup"><span data-stu-id="e02a4-127">Create a content key.</span></span>
8. <span data-ttu-id="e02a4-128">Configurez la stratégie d’autorisation de la clé de contenu hello.</span><span class="sxs-lookup"><span data-stu-id="e02a4-128">Configure hello content key's authorization policy.</span></span>
9. <span data-ttu-id="e02a4-129">Configurez la stratégie de remise de ressources (utilisée par l’empaquetage dynamique et le chiffrement dynamique).</span><span class="sxs-lookup"><span data-stu-id="e02a4-129">Configure asset delivery policy (used by dynamic packaging and dynamic encryption).</span></span>
10. <span data-ttu-id="e02a4-130">Créer un programme et spécifiez asset hello toouse que vous avez créé.</span><span class="sxs-lookup"><span data-stu-id="e02a4-130">Create a program and specify toouse hello asset that you created.</span></span>
11. <span data-ttu-id="e02a4-131">Publier la ressource hello associée au programme de hello en créant un localisateur OnDemand.</span><span class="sxs-lookup"><span data-stu-id="e02a4-131">Publish hello asset associated with hello program by creating an OnDemand locator.</span></span>

    >[!NOTE]
    ><span data-ttu-id="e02a4-132">Création de votre compte AMS un **par défaut** point de terminaison de diffusion en continu est ajoutée tooyour compte Bonjour **arrêté** état.</span><span class="sxs-lookup"><span data-stu-id="e02a4-132">When your AMS account is created a **default** streaming endpoint is added tooyour account in hello **Stopped** state.</span></span> <span data-ttu-id="e02a4-133">Hello, point de terminaison à partir de laquelle vous souhaitez toostream contenu de diffusion en continu a toobe Bonjour **en cours d’exécution** état.</span><span class="sxs-lookup"><span data-stu-id="e02a4-133">hello streaming endpoint from which you want toostream content has toobe in hello **Running** state.</span></span> 

12. <span data-ttu-id="e02a4-134">Démarrer le programme de hello lorsque vous êtes prêt toostart diffusion et l’archivage.</span><span class="sxs-lookup"><span data-stu-id="e02a4-134">Start hello program when you are ready toostart streaming and archiving.</span></span>
13. <span data-ttu-id="e02a4-135">Si vous le souhaitez, encodeur en direct de hello peut être signalé toostart une publication.</span><span class="sxs-lookup"><span data-stu-id="e02a4-135">Optionally, hello live encoder can be signaled toostart an advertisement.</span></span> <span data-ttu-id="e02a4-136">publication de Hello est insérée dans le flux de sortie hello.</span><span class="sxs-lookup"><span data-stu-id="e02a4-136">hello advertisement is inserted in hello output stream.</span></span>
14. <span data-ttu-id="e02a4-137">Arrêter le programme de hello chaque fois que vous souhaitez toostop de diffusion en continu et l’archivage des événements de hello.</span><span class="sxs-lookup"><span data-stu-id="e02a4-137">Stop hello program whenever you want toostop streaming and archiving hello event.</span></span>
15. <span data-ttu-id="e02a4-138">Supprimer le programme de hello (et éventuellement supprimer actif de hello).</span><span class="sxs-lookup"><span data-stu-id="e02a4-138">Delete hello Program (and optionally delete hello asset).</span></span>

## <a name="what-youll-learn"></a><span data-ttu-id="e02a4-139">Ce que vous allez apprendre</span><span class="sxs-lookup"><span data-stu-id="e02a4-139">What you'll learn</span></span>
<span data-ttu-id="e02a4-140">Cette rubrique vous montre comment tooexecute différentes opérations sur les canaux et les programmes à l’aide de Media Services .NET SDK.</span><span class="sxs-lookup"><span data-stu-id="e02a4-140">This topic shows you how tooexecute different operations on channels and programs using Media Services .NET SDK.</span></span> <span data-ttu-id="e02a4-141">Bon nombre d'opérations étant de longue durée, les API .NET qui gèrent les opérations de ce type sont utilisées.</span><span class="sxs-lookup"><span data-stu-id="e02a4-141">Because many operations are long-running .NET APIs that manage long running operations are used.</span></span>

<span data-ttu-id="e02a4-142">Hello rubrique montre comment suivant de hello toodo :</span><span class="sxs-lookup"><span data-stu-id="e02a4-142">hello topic shows how toodo hello following:</span></span>

1. <span data-ttu-id="e02a4-143">Créez et démarrez un canal.</span><span class="sxs-lookup"><span data-stu-id="e02a4-143">Create and start a channel.</span></span> <span data-ttu-id="e02a4-144">Des API de longue durée sont utilisées.</span><span class="sxs-lookup"><span data-stu-id="e02a4-144">Long-running APIs are used.</span></span>
2. <span data-ttu-id="e02a4-145">Obtenir les canaux hello réception du point de terminaison (entrée).</span><span class="sxs-lookup"><span data-stu-id="e02a4-145">Get hello channels ingest (input) endpoint.</span></span> <span data-ttu-id="e02a4-146">Encodeur toohello qui peut envoyer un flux en direct à débit binaire unique doit être fourni à ce point de terminaison.</span><span class="sxs-lookup"><span data-stu-id="e02a4-146">This endpoint should be provided toohello encoder that can send a single bitrate live stream.</span></span>
3. <span data-ttu-id="e02a4-147">Obtenir le point de terminaison hello aperçu.</span><span class="sxs-lookup"><span data-stu-id="e02a4-147">Get hello preview endpoint.</span></span> <span data-ttu-id="e02a4-148">Ce point de terminaison est utilisé toopreview votre flux de données.</span><span class="sxs-lookup"><span data-stu-id="e02a4-148">This endpoint is used toopreview your stream.</span></span>
4. <span data-ttu-id="e02a4-149">Créer un élément multimédia qui sera utilisé toostore votre contenu.</span><span class="sxs-lookup"><span data-stu-id="e02a4-149">Create an asset that will be used toostore your content.</span></span> <span data-ttu-id="e02a4-150">stratégies de remise Hello actif doivent être configurés ainsi, comme illustré dans cet exemple.</span><span class="sxs-lookup"><span data-stu-id="e02a4-150">hello asset delivery policies should be configured as well, as shown in this example.</span></span>
5. <span data-ttu-id="e02a4-151">Créer un programme et spécifiez asset hello toouse qui a été créé précédemment.</span><span class="sxs-lookup"><span data-stu-id="e02a4-151">Create a program and specify toouse hello asset that was created earlier.</span></span> <span data-ttu-id="e02a4-152">Démarrer le programme hello.</span><span class="sxs-lookup"><span data-stu-id="e02a4-152">Start hello program.</span></span> <span data-ttu-id="e02a4-153">Des API de longue durée sont utilisées.</span><span class="sxs-lookup"><span data-stu-id="e02a4-153">Long-running APIs are used.</span></span>
6. <span data-ttu-id="e02a4-154">Créer un localisateur pour un composant de hello, afin que le contenu hello est publié et peut être diffusé tooyour clients.</span><span class="sxs-lookup"><span data-stu-id="e02a4-154">Create a locator for hello asset, so hello content gets published and can be streamed tooyour clients.</span></span>
7. <span data-ttu-id="e02a4-155">Afficher et masquer des slates.</span><span class="sxs-lookup"><span data-stu-id="e02a4-155">Show and hide slates.</span></span> <span data-ttu-id="e02a4-156">Démarrer et arrêter des publicités.</span><span class="sxs-lookup"><span data-stu-id="e02a4-156">Start and stop advertisements.</span></span> <span data-ttu-id="e02a4-157">Des API de longue durée sont utilisées.</span><span class="sxs-lookup"><span data-stu-id="e02a4-157">Long-running APIs are used.</span></span>
8. <span data-ttu-id="e02a4-158">Nettoyer votre canal et tous les hello ressources associées.</span><span class="sxs-lookup"><span data-stu-id="e02a4-158">Clean up your channel and all hello associated resources.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e02a4-159">Composants requis</span><span class="sxs-lookup"><span data-stu-id="e02a4-159">Prerequisites</span></span>
<span data-ttu-id="e02a4-160">Hello Voici didacticiel de hello toocomplete requis.</span><span class="sxs-lookup"><span data-stu-id="e02a4-160">hello following are required toocomplete hello tutorial.</span></span>

* <span data-ttu-id="e02a4-161">Un compte Azure.</span><span class="sxs-lookup"><span data-stu-id="e02a4-161">An Azure account.</span></span> <span data-ttu-id="e02a4-162">Si vous ne possédez pas de compte, vous pouvez créer un compte d'évaluation gratuit en quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="e02a4-162">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="e02a4-163">Pour plus d'informations, consultez la page [Version d'évaluation gratuite d'Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F).</span><span class="sxs-lookup"><span data-stu-id="e02a4-163">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F).</span></span> <span data-ttu-id="e02a4-164">Vous obtenez des crédits qui peuvent être utilisé tootry out à payer des services Azure.</span><span class="sxs-lookup"><span data-stu-id="e02a4-164">You get credits that can be used tootry out paid Azure services.</span></span> <span data-ttu-id="e02a4-165">Même après que hello crédits épuisés, vous pouvez conserver le compte de hello et utiliser des services Azure gratuits et des fonctionnalités, telles que les fonctionnalités des applications Web hello dans Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="e02a4-165">Even after hello credits are used up, you can keep hello account and use free Azure services and features, such as hello Web Apps feature in Azure App Service.</span></span>
* <span data-ttu-id="e02a4-166">Un compte Media Services.</span><span class="sxs-lookup"><span data-stu-id="e02a4-166">A Media Services account.</span></span> <span data-ttu-id="e02a4-167">toocreate un compte Media Services, consultez [créer un compte](media-services-portal-create-account.md).</span><span class="sxs-lookup"><span data-stu-id="e02a4-167">toocreate a Media Services account, see [Create Account](media-services-portal-create-account.md).</span></span>
* <span data-ttu-id="e02a4-168">Visual Studio 2010 SP1 (Professional, Premium, Ultimate ou Express) ou une version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="e02a4-168">Visual Studio 2010 SP1 (Professional, Premium, Ultimate, or Express) or later versions.</span></span>
* <span data-ttu-id="e02a4-169">Vous devez utiliser le Kit de développement logiciel (SDK) .NET de Media Services version 3.2.0.0 ou ultérieure.</span><span class="sxs-lookup"><span data-stu-id="e02a4-169">You must use Media Services .NET SDK version 3.2.0.0 or newer.</span></span>
* <span data-ttu-id="e02a4-170">Une webcam et un encodeur capable d’envoyer un flux dynamique à débit binaire unique.</span><span class="sxs-lookup"><span data-stu-id="e02a4-170">A webcam and an encoder that can send a single bitrate live stream.</span></span>

## <a name="considerations"></a><span data-ttu-id="e02a4-171">Considérations</span><span class="sxs-lookup"><span data-stu-id="e02a4-171">Considerations</span></span>
* <span data-ttu-id="e02a4-172">Actuellement, hello maximum recommandé de durée d’un événement en direct est de 8 heures.</span><span class="sxs-lookup"><span data-stu-id="e02a4-172">Currently, hello max recommended duration of a live event is 8 hours.</span></span> <span data-ttu-id="e02a4-173">Si vous avez besoin d’un canal de toorun pour de longues périodes, contactez amslived Microsoft.com.</span><span class="sxs-lookup"><span data-stu-id="e02a4-173">Please contact amslived at Microsoft.com if you need toorun a Channel for longer periods of time.</span></span>
* <span data-ttu-id="e02a4-174">Un nombre limite de 1 000 000 a été défini pour les différentes stratégies AMS (par exemple, pour la stratégie de localisateur ou pour ContentKeyAuthorizationPolicy).</span><span class="sxs-lookup"><span data-stu-id="e02a4-174">There is a limit of 1,000,000 policies for different AMS policies (for example, for Locator policy or ContentKeyAuthorizationPolicy).</span></span> <span data-ttu-id="e02a4-175">Vous devez utiliser hello ID de stratégie même si vous utilisez toujours hello même jours / autorisations d’accès, par exemple, les stratégies pour les localisateurs sont tooremain prévue en place pendant une longue période (non-téléchargement stratégies).</span><span class="sxs-lookup"><span data-stu-id="e02a4-175">You should use hello same policy ID if you are always using hello same days / access permissions, for example, policies for locators that are intended tooremain in place for a long time (non-upload policies).</span></span> <span data-ttu-id="e02a4-176">Pour plus d’informations, consultez [cette rubrique](media-services-dotnet-manage-entities.md#limit-access-policies) .</span><span class="sxs-lookup"><span data-stu-id="e02a4-176">For more information, see [this](media-services-dotnet-manage-entities.md#limit-access-policies) topic.</span></span>

## <a name="download-sample"></a><span data-ttu-id="e02a4-177">Charger l’exemple</span><span class="sxs-lookup"><span data-stu-id="e02a4-177">Download sample</span></span>

<span data-ttu-id="e02a4-178">Vous pouvez télécharger des exemple hello qui sont décrite dans cette rubrique à partir de [ici](https://azure.microsoft.com/documentation/samples/media-services-dotnet-encode-live-stream-with-ams-clear/).</span><span class="sxs-lookup"><span data-stu-id="e02a4-178">You can download hello sample that is described in this topic from [here](https://azure.microsoft.com/documentation/samples/media-services-dotnet-encode-live-stream-with-ams-clear/).</span></span>

## <a name="set-up-for-development-with-media-services-sdk-for-net"></a><span data-ttu-id="e02a4-179">Configurer le développement avec le Kit de développement logiciel (SDK) Media Services pour .NET</span><span class="sxs-lookup"><span data-stu-id="e02a4-179">Set up for development with Media Services SDK for .NET</span></span>

<span data-ttu-id="e02a4-180">Configurer votre environnement de développement et de remplir le fichier app.config de hello avec les informations de connexion, comme décrit dans [développement Media Services avec .NET](media-services-dotnet-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="e02a4-180">Set up your development environment and populate hello app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 

## <a name="code-example"></a><span data-ttu-id="e02a4-181">Exemple de code</span><span class="sxs-lookup"><span data-stu-id="e02a4-181">Code example</span></span>

    using System;
    using System.Collections.Generic;
    using System.Configuration;
    using System.IO;
    using System.Linq;
    using System.Net;
    using Microsoft.WindowsAzure.MediaServices.Client;
    using Microsoft.WindowsAzure.MediaServices.Client.DynamicEncryption;

    namespace EncodeLiveStreamWithAmsClear
    {
        class Program
        {
        private const string ChannelName = "channel001";
        private const string AssetlName = "asset001";
        private const string ProgramlName = "program001";

        // Read values from hello App.config file.
        private static readonly string _AADTenantDomain =
        ConfigurationManager.AppSettings["AADTenantDomain"];
        private static readonly string _RESTAPIEndpoint =
        ConfigurationManager.AppSettings["MediaServiceRESTAPIEndpoint"];

        private static CloudMediaContext _context = null;

        static void Main(string[] args)
        {
            var tokenCredentials = new AzureAdTokenCredentials(_AADTenantDomain, AzureEnvironments.AzureCloudEnvironment);
            var tokenProvider = new AzureAdTokenProvider(tokenCredentials);

            _context = new CloudMediaContext(new Uri(_RESTAPIEndpoint), tokenProvider);

            IChannel channel = CreateAndStartChannel();

            // hello channel's input endpoint:
            string ingestUrl = channel.Input.Endpoints.FirstOrDefault().Url.ToString();

            Console.WriteLine("Intest URL: {0}", ingestUrl);


            // Use hello previewEndpoint toopreview and verify 
            // that hello input from hello encoder is actually reaching hello Channel. 
            string previewEndpoint = channel.Preview.Endpoints.FirstOrDefault().Url.ToString();

            Console.WriteLine("Preview URL: {0}", previewEndpoint);

            // When Live Encoding is enabled, you can now get a preview of hello live feed as it reaches hello Channel. 
            // This can be a valuable tool toocheck whether your live feed is actually reaching hello Channel. 
            // hello thumbnail is exposed via hello same end-point as hello Channel Preview URL.
            string thumbnailUri = new UriBuilder
            {
            Scheme = Uri.UriSchemeHttps,
            Host = channel.Preview.Endpoints.FirstOrDefault().Url.Host,
            Path = "thumbnails/input.jpg"
            }.Uri.ToString();

            Console.WriteLine("Thumbain URL: {0}", thumbnailUri);

            // Once you previewed your stream and verified that it is flowing into your Channel, 
            // you can create an event by creating an Asset, Program, and Streaming Locator. 
            IAsset asset = CreateAndConfigureAsset();

            IProgram program = CreateAndStartProgram(channel, asset);

            ILocator locator = CreateLocatorForAsset(program.Asset, program.ArchiveWindowLength);

            // You can use slates and ads only if hello channel type is Standard.  
            StartStopAdsSlates(channel);

            // Once you are done streaming, clean up your resources.
            Cleanup(channel);
        }

        public static IChannel CreateAndStartChannel()
        {
            var channelInput = CreateChannelInput();
            var channePreview = CreateChannelPreview();
            var channelEncoding = CreateChannelEncoding();

            ChannelCreationOptions options = new ChannelCreationOptions
            {
            EncodingType = ChannelEncodingType.Standard,
            Name = ChannelName,
            Input = channelInput,
            Preview = channePreview,
            Encoding = channelEncoding
            };

            Log("Creating channel");
            IOperation channelCreateOperation = _context.Channels.SendCreateOperation(options);
            string channelId = TrackOperation(channelCreateOperation, "Channel create");

            IChannel channel = _context.Channels.Where(c => c.Id == channelId).FirstOrDefault();

            Log("Starting channel");
            var channelStartOperation = channel.SendStartOperation();
            TrackOperation(channelStartOperation, "Channel start");

            return channel;
        }

        /// <summary>
        /// Create channel input, used in channel creation options. 
        /// </summary>
        /// <returns></returns>
        private static ChannelInput CreateChannelInput()
        {
            return new ChannelInput
            {
            StreamingProtocol = StreamingProtocol.RTPMPEG2TS,
            AccessControl = new ChannelAccessControl
            {
                IPAllowList = new List<IPRange>
                {
                    new IPRange
                    {
                    Name = "TestChannelInput001",
                    Address = IPAddress.Parse("0.0.0.0"),
                    SubnetPrefixLength = 0
                    }
                }
            }
            };
        }

        /// <summary>
        /// Create channel preview, used in channel creation options. 
        /// </summary>
        /// <returns></returns>
        private static ChannelPreview CreateChannelPreview()
        {
            return new ChannelPreview
            {
            AccessControl = new ChannelAccessControl
            {
                IPAllowList = new List<IPRange>
                {
                    new IPRange
                    {
                    Name = "TestChannelPreview001",
                    Address = IPAddress.Parse("0.0.0.0"),
                    SubnetPrefixLength = 0
                    }
                }
            }
            };
        }

        /// <summary>
        /// Create channel encoding, used in channel creation options. 
        /// </summary>
        /// <returns></returns>
        private static ChannelEncoding CreateChannelEncoding()
        {
            return new ChannelEncoding
            {
            SystemPreset = "Default720p",
            IgnoreCea708ClosedCaptions = false,
            AdMarkerSource = AdMarkerSource.Api,
            // You can only set audio if streaming protocol is set tooStreamingProtocol.RTPMPEG2TS.
            AudioStreams = new List<AudioStream> { new AudioStream { Index = 103, Language = "eng" } }.AsReadOnly()
            };
        }

        /// <summary>
        /// Create an asset and configure asset delivery policies.
        /// </summary>
        /// <returns></returns>
        public static IAsset CreateAndConfigureAsset()
        {
            IAsset asset = _context.Assets.Create(AssetlName, AssetCreationOptions.None);

            IAssetDeliveryPolicy policy =
            _context.AssetDeliveryPolicies.Create("Clear Policy",
            AssetDeliveryPolicyType.NoDynamicEncryption,
            AssetDeliveryProtocol.HLS | AssetDeliveryProtocol.SmoothStreaming | AssetDeliveryProtocol.Dash, null);

            asset.DeliveryPolicies.Add(policy);

            return asset;
        }

        /// <summary>
        /// Create a Program on hello Channel. You can have multiple Programs that overlap or are sequential;
        /// however each Program must have a unique name within your Media Services account.
        /// </summary>
        /// <param name="channel"></param>
        /// <param name="asset"></param>
        /// <returns></returns>
        public static IProgram CreateAndStartProgram(IChannel channel, IAsset asset)
        {
            IProgram program = channel.Programs.Create(ProgramlName, TimeSpan.FromHours(3), asset.Id);
            Log("Program created", program.Id);

            Log("Starting program");
            var programStartOperation = program.SendStartOperation();
            TrackOperation(programStartOperation, "Program start");

            return program;
        }

        /// <summary>
        /// Create locators in order toobe able toopublish and stream hello video.
        /// </summary>
        /// <param name="asset"></param>
        /// <param name="ArchiveWindowLength"></param>
        /// <returns></returns>
        public static ILocator CreateLocatorForAsset(IAsset asset, TimeSpan ArchiveWindowLength)
        {
            // You cannot create a streaming locator using an AccessPolicy that includes write or delete permissions.            
            var locator = _context.Locators.CreateLocator
            (
                LocatorType.OnDemandOrigin,
                asset,
                _context.AccessPolicies.Create
                (
                    "Live Stream Policy",
                    ArchiveWindowLength,
                    AccessPermissions.Read
                )
            );

            return locator;
        }

        /// <summary>
        /// Perform operations on slates.
        /// </summary>
        /// <param name="channel"></param>
        public static void StartStopAdsSlates(IChannel channel)
        {
            int cueId = new Random().Next(int.MaxValue);
            var path = Path.GetFullPath(Path.Combine(AppDomain.CurrentDomain.BaseDirectory, @"..\\..\\SlateJPG\\DefaultAzurePortalSlate.jpg"));

            Log("Creating asset");
            var slateAsset = _context.Assets.Create("Slate test asset " + DateTime.Now.ToString("yyyy-MM-dd HH-mm"), AssetCreationOptions.None);
            Log("Slate asset created", slateAsset.Id);

            Log("Uploading file");
            var assetFile = slateAsset.AssetFiles.Create("DefaultAzurePortalSlate.jpg");
            assetFile.Upload(path);
            assetFile.IsPrimary = true;
            assetFile.Update();

            Log("Showing slate");
            var showSlateOpeartion = channel.SendShowSlateOperation(TimeSpan.FromMinutes(1), slateAsset.Id);
            TrackOperation(showSlateOpeartion, "Show slate");

            Log("Hiding slate");
            var hideSlateOperation = channel.SendHideSlateOperation();
            TrackOperation(hideSlateOperation, "Hide slate");

            Log("Starting ad");
            var startAdOperation = channel.SendStartAdvertisementOperation(TimeSpan.FromMinutes(1), cueId, false);
            TrackOperation(startAdOperation, "Start ad");

            Log("Ending ad");
            var endAdOperation = channel.SendEndAdvertisementOperation(cueId);
            TrackOperation(endAdOperation, "End ad");

            Log("Deleting slate asset");
            slateAsset.Delete();
        }

        /// <summary>
        /// Clean up resources associated with hello channel.
        /// </summary>
        /// <param name="channel"></param>
        public static void Cleanup(IChannel channel)
        {
            IAsset asset;
            if (channel != null)
            {
            foreach (var program in channel.Programs)
            {
                asset = _context.Assets.Where(se => se.Id == program.AssetId)
                            .FirstOrDefault();

                Log("Stopping program");
                var programStopOperation = program.SendStopOperation();
                TrackOperation(programStopOperation, "Program stop");

                program.Delete();

                if (asset != null)
                {
                Log("Deleting locators");
                foreach (var l in asset.Locators)
                    l.Delete();

                Log("Deleting asset");
                asset.Delete();
                }
            }

            Log("Stopping channel");
            var channelStopOperation = channel.SendStopOperation();
            TrackOperation(channelStopOperation, "Channel stop");

            Log("Deleting channel");
            var channelDeleteOperation = channel.SendDeleteOperation();
            TrackOperation(channelDeleteOperation, "Channel delete");
            }
        }

        /// <summary>
        /// Track long running operations.
        /// </summary>
        /// <param name="operation"></param>
        /// <param name="description"></param>
        /// <returns></returns>
        public static string TrackOperation(IOperation operation, string description)
        {
            string entityId = null;
            bool isCompleted = false;

            Log("starting tootrack ", null, operation.Id);
            while (isCompleted == false)
            {
            operation = _context.Operations.GetOperation(operation.Id);
            isCompleted = IsCompleted(operation, out entityId);
            System.Threading.Thread.Sleep(TimeSpan.FromSeconds(30));
            }
            // If we got here, hello operation succeeded.
            Log(description + " in completed", operation.TargetEntityId, operation.Id);

            return entityId;
        }

        /// <summary> 
        /// Checks if hello operation has been completed. 
        /// If hello operation succeeded, hello created entity Id is returned in hello out parameter.
        /// </summary> 
        /// <param name="operationId">hello operation Id.</param> 
        /// <param name="channel">
        /// If hello operation succeeded, 
        /// hello entity Id associated with hello sucessful operation is returned in hello out parameter.</param>
        /// <returns>Returns false if hello operation is still in progress; otherwise, true.</returns> 
        private static bool IsCompleted(IOperation operation, out string entityId)
        {
            bool completed = false;

            entityId = null;

            switch (operation.State)
            {
            case OperationState.Failed:
                // Handle hello failure. 
                // For example, throw an exception. 
                // Use hello following information in hello exception: operationId, operation.ErrorMessage.
                Log("operation failed", operation.TargetEntityId, operation.Id);
                break;
            case OperationState.Succeeded:
                completed = true;
                entityId = operation.TargetEntityId;
                break;
            case OperationState.InProgress:
                completed = false;
                Log("operation in progress", operation.TargetEntityId, operation.Id);
                break;
            }
            return completed;
        }

        private static void Log(string action, string entityId = null, string operationId = null)
        {
            Console.WriteLine(
            "{0,-21}{1,-51}{2,-51}{3,-51}",
            DateTime.Now.ToString("yyyy'-'MM'-'dd HH':'mm':'ss"),
            action,
            entityId ?? string.Empty,
            operationId ?? string.Empty);
        }
        }
    }

## <a name="next-step"></a><span data-ttu-id="e02a4-182">Étape suivante</span><span class="sxs-lookup"><span data-stu-id="e02a4-182">Next step</span></span>
<span data-ttu-id="e02a4-183">Consultez les parcours d’apprentissage de Media Services.</span><span class="sxs-lookup"><span data-stu-id="e02a4-183">Review Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="e02a4-184">Fournir des commentaires</span><span class="sxs-lookup"><span data-stu-id="e02a4-184">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]


