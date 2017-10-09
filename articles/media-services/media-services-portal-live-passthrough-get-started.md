---
title: "flux aaaLive avec des encodeurs locaux à l’aide de hello portail Azure | Documents Microsoft"
description: "Ce didacticiel vous guide tout au long des étapes de hello de création d’un canal qui est configuré pour une livraison directe."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 6f4acd95-cc64-4dd9-9e2d-8734707de326
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/09/2017
ms.author: juliako
ms.openlocfilehash: 1fb341e022f66f33903e13e07d3e84c0216cad77
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooperform-live-streaming-with-on-premises-encoders-using-hello-azure-portal"></a><span data-ttu-id="bd17b-103">Comment tooperform diffusion en continu avec local encodeurs à l’aide de hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="bd17b-103">How tooperform live streaming with on-premises encoders using hello Azure portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="bd17b-104">Portail</span><span class="sxs-lookup"><span data-stu-id="bd17b-104">Portal</span></span>](media-services-portal-live-passthrough-get-started.md)
> * [<span data-ttu-id="bd17b-105">.NET</span><span class="sxs-lookup"><span data-stu-id="bd17b-105">.NET</span></span>](media-services-dotnet-live-encode-with-onpremises-encoders.md)
> * [<span data-ttu-id="bd17b-106">REST</span><span class="sxs-lookup"><span data-stu-id="bd17b-106">REST</span></span>](https://docs.microsoft.com/rest/api/media/operations/channel)
> 
> 

<span data-ttu-id="bd17b-107">Ce didacticiel vous guide tout au long des étapes hello de l’utilisation de hello toocreate portail Azure un **canal** qui est configuré pour une livraison directe.</span><span class="sxs-lookup"><span data-stu-id="bd17b-107">This tutorial walks you through hello steps of using hello Azure portal toocreate a **Channel** that is configured for a pass-through delivery.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="bd17b-108">Composants requis</span><span class="sxs-lookup"><span data-stu-id="bd17b-108">Prerequisites</span></span>
<span data-ttu-id="bd17b-109">Hello Voici didacticiel de hello toocomplete requis :</span><span class="sxs-lookup"><span data-stu-id="bd17b-109">hello following are required toocomplete hello tutorial:</span></span>

* <span data-ttu-id="bd17b-110">Un compte Azure.</span><span class="sxs-lookup"><span data-stu-id="bd17b-110">An Azure account.</span></span> <span data-ttu-id="bd17b-111">Pour plus d'informations, consultez la page [Version d'évaluation gratuite d'Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="bd17b-111">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 
* <span data-ttu-id="bd17b-112">Un compte Media Services.</span><span class="sxs-lookup"><span data-stu-id="bd17b-112">A Media Services account.</span></span> <span data-ttu-id="bd17b-113">toocreate un compte Media Services, consultez [comment tooCreate un compte Media Services](media-services-portal-create-account.md).</span><span class="sxs-lookup"><span data-stu-id="bd17b-113">toocreate a Media Services account, see [How tooCreate a Media Services Account](media-services-portal-create-account.md).</span></span>
* <span data-ttu-id="bd17b-114">Une webcam.</span><span class="sxs-lookup"><span data-stu-id="bd17b-114">A webcam.</span></span> <span data-ttu-id="bd17b-115">Par exemple, un [encodeur Telestream Wirecast](http://www.telestream.net/wirecast/overview.htm).</span><span class="sxs-lookup"><span data-stu-id="bd17b-115">For example, [Telestream Wirecast encoder](http://www.telestream.net/wirecast/overview.htm).</span></span>

<span data-ttu-id="bd17b-116">Il est fortement recommandé hello tooreview suivant des articles :</span><span class="sxs-lookup"><span data-stu-id="bd17b-116">It is highly recommended tooreview hello following articles:</span></span>

* [<span data-ttu-id="bd17b-117">Prise en charge RTMP et encodeurs dynamiques dans Azure Media Services.</span><span class="sxs-lookup"><span data-stu-id="bd17b-117">Azure Media Services RTMP Support and Live Encoders</span></span>](https://azure.microsoft.com/blog/2014/09/18/azure-media-services-rtmp-support-and-live-encoders/)
* [<span data-ttu-id="bd17b-118">Vue d’ensemble de la vidéo en flux continu à l’aide d’Azure Media Services</span><span class="sxs-lookup"><span data-stu-id="bd17b-118">Overview of Live Steaming using Azure Media Services</span></span>](media-services-manage-channels-overview.md)
* [<span data-ttu-id="bd17b-119">Streaming en direct avec des encodeurs en local qui créent des flux multidébits</span><span class="sxs-lookup"><span data-stu-id="bd17b-119">Live streaming with on-premises encoders that create multi-bitrate streams</span></span>](media-services-live-streaming-with-onprem-encoders.md)

## <span data-ttu-id="bd17b-120"><a id="scenario"></a>Scénario courant de streaming en direct</span><span class="sxs-lookup"><span data-stu-id="bd17b-120"><a id="scenario"></a>Common live streaming scenario</span></span>
<span data-ttu-id="bd17b-121">Hello étapes suivantes décrivent les tâches impliquées dans la création d’applications de diffusion en continu live courants qui utilisent des canaux qui sont configurés pour la remise pass-through.</span><span class="sxs-lookup"><span data-stu-id="bd17b-121">hello following steps describe tasks involved in creating common live streaming applications that use channels that are configured for pass-through delivery.</span></span> <span data-ttu-id="bd17b-122">Ce didacticiel montre comment toocreate et gérer un canal direct et les événements en direct.</span><span class="sxs-lookup"><span data-stu-id="bd17b-122">This tutorial shows how toocreate and manage a pass-through channel and live events.</span></span>

>[!NOTE]
><span data-ttu-id="bd17b-123">Vérifiez que hello point de terminaison à partir de laquelle vous souhaitez toostream contenu de diffusion en continu est Bonjour **en cours d’exécution** état.</span><span class="sxs-lookup"><span data-stu-id="bd17b-123">Make sure hello streaming endpoint from which you want toostream content is in hello **Running** state.</span></span> 
    
1. <span data-ttu-id="bd17b-124">Connecter un ordinateur de tooa caméra vidéo.</span><span class="sxs-lookup"><span data-stu-id="bd17b-124">Connect a video camera tooa computer.</span></span> <span data-ttu-id="bd17b-125">Lancez et configurez un encodeur dynamique local qui produit un flux à débit binaire multiple au format MP4 fragmenté ou RTMP.</span><span class="sxs-lookup"><span data-stu-id="bd17b-125">Launch and configure an on-premises live encoder that outputs a multi-bitrate RTMP or Fragmented MP4 stream.</span></span> <span data-ttu-id="bd17b-126">Pour plus d’informations, voir [Prise en charge RTMP et encodeurs dynamiques dans Azure Media Services](http://go.microsoft.com/fwlink/?LinkId=532824).</span><span class="sxs-lookup"><span data-stu-id="bd17b-126">For more information, see [Azure Media Services RTMP Support and Live Encoders](http://go.microsoft.com/fwlink/?LinkId=532824).</span></span>
   
    <span data-ttu-id="bd17b-127">Cette étape peut également être effectuée après la création du canal.</span><span class="sxs-lookup"><span data-stu-id="bd17b-127">This step could also be performed after you create your Channel.</span></span>
2. <span data-ttu-id="bd17b-128">Créez et démarrez un canal direct.</span><span class="sxs-lookup"><span data-stu-id="bd17b-128">Create and start a pass-through Channel.</span></span>
3. <span data-ttu-id="bd17b-129">URL de réception récupérer hello canal.</span><span class="sxs-lookup"><span data-stu-id="bd17b-129">Retrieve hello Channel ingest URL.</span></span> 
   
    <span data-ttu-id="bd17b-130">URL de réception Hello est utilisé par hello encodeur en temps réel toosend hello flux toohello canal.</span><span class="sxs-lookup"><span data-stu-id="bd17b-130">hello ingest URL is used by hello live encoder toosend hello stream toohello Channel.</span></span>
4. <span data-ttu-id="bd17b-131">Récupérer l’URL d’aperçu hello canal.</span><span class="sxs-lookup"><span data-stu-id="bd17b-131">Retrieve hello Channel preview URL.</span></span> 
   
    <span data-ttu-id="bd17b-132">Utilisez cette tooverify URL que votre canal reçoit correctement les flux live hello.</span><span class="sxs-lookup"><span data-stu-id="bd17b-132">Use this URL tooverify that your channel is properly receiving hello live stream.</span></span>
5. <span data-ttu-id="bd17b-133">Créez un événement/programme en direct.</span><span class="sxs-lookup"><span data-stu-id="bd17b-133">Create a live event/program.</span></span> 
   
    <span data-ttu-id="bd17b-134">Lors de l’aide de hello portail Azure, création d’un événement en direct crée également un élément multimédia.</span><span class="sxs-lookup"><span data-stu-id="bd17b-134">When using hello Azure portal, creating a live event also creates an asset.</span></span> 

6. <span data-ttu-id="bd17b-135">Démarrez hello événement/programme lorsque vous êtes prêt toostart diffusion et l’archivage.</span><span class="sxs-lookup"><span data-stu-id="bd17b-135">Start hello event/program when you are ready toostart streaming and archiving.</span></span>
7. <span data-ttu-id="bd17b-136">Si vous le souhaitez, encodeur en direct de hello peut être signalé toostart une publication.</span><span class="sxs-lookup"><span data-stu-id="bd17b-136">Optionally, hello live encoder can be signaled toostart an advertisement.</span></span> <span data-ttu-id="bd17b-137">publication de Hello est insérée dans le flux de sortie hello.</span><span class="sxs-lookup"><span data-stu-id="bd17b-137">hello advertisement is inserted in hello output stream.</span></span>
8. <span data-ttu-id="bd17b-138">Arrêter/programme hello d’événement chaque fois que vous souhaitez toostop de diffusion en continu et l’archivage des événements de hello.</span><span class="sxs-lookup"><span data-stu-id="bd17b-138">Stop hello event/program whenever you want toostop streaming and archiving hello event.</span></span>
9. <span data-ttu-id="bd17b-139">Supprimer hello événement/programme (et éventuellement supprimer actif de hello).</span><span class="sxs-lookup"><span data-stu-id="bd17b-139">Delete hello event/program (and optionally delete hello asset).</span></span>     

> [!IMPORTANT]
> <span data-ttu-id="bd17b-140">Passez en revue [la diffusion en continu en direct avec les encodeurs locaux qui créent des flux de débits](media-services-live-streaming-with-onprem-encoders.md) toolearn sur les concepts et les considérations liées à la diffusion en continu toolive avec les canaux directs et les encodeurs locaux.</span><span class="sxs-lookup"><span data-stu-id="bd17b-140">Please review [Live streaming with on-premises encoders that create multi-bitrate streams](media-services-live-streaming-with-onprem-encoders.md) toolearn about concepts and considerations related toolive streaming with on-premises encoders and pass-through channels.</span></span>
> 
> 

## <a name="tooview-notifications-and-errors"></a><span data-ttu-id="bd17b-141">erreurs et les notifications de tooview</span><span class="sxs-lookup"><span data-stu-id="bd17b-141">tooview notifications and errors</span></span>
<span data-ttu-id="bd17b-142">Si vous souhaitez que les notifications de tooview et les erreurs générées par hello portail Azure, cliquez sur l’icône de Notification hello.</span><span class="sxs-lookup"><span data-stu-id="bd17b-142">If you want tooview notifications and errors produced by hello Azure portal, click on hello Notification icon.</span></span>

![Notifications](./media/media-services-portal-passthrough-get-started/media-services-notifications.png)

## <a name="create-and-start-pass-through-channels-and-events"></a><span data-ttu-id="bd17b-144">Créer et démarrer des canaux directs et des événements</span><span class="sxs-lookup"><span data-stu-id="bd17b-144">Create and start pass-through channels and events</span></span>
<span data-ttu-id="bd17b-145">Un canal est associé à des événements/des programmes qui vous permettent de la publication toocontrol hello et stockage des segments dans un flux en direct.</span><span class="sxs-lookup"><span data-stu-id="bd17b-145">A channel is associated with events/programs that enable you toocontrol hello publishing and storage of segments in a live stream.</span></span> <span data-ttu-id="bd17b-146">Les canaux gèrent des événements.</span><span class="sxs-lookup"><span data-stu-id="bd17b-146">Channels manage events.</span></span> 

<span data-ttu-id="bd17b-147">Vous pouvez spécifier le nombre de hello d’heures que vous voulez tooretain hello enregistrée contenu pour le programme de hello en définissant un hello **fenêtre d’Archive** longueur.</span><span class="sxs-lookup"><span data-stu-id="bd17b-147">You can specify hello number of hours you want tooretain hello recorded content for hello program by setting hello **Archive Window** length.</span></span> <span data-ttu-id="bd17b-148">Cette valeur peut être définie à partir d’un minimum de 5 minutes tooa 25 heures maximum.</span><span class="sxs-lookup"><span data-stu-id="bd17b-148">This value can be set from a minimum of 5 minutes tooa maximum of 25 hours.</span></span> <span data-ttu-id="bd17b-149">Longueur de fenêtre d’archive détermine également hello durée maximale pendant laquelle les clients peuvent effectuer des recherches dans le temps à partir de la position de diffusion en continu hello actuel.</span><span class="sxs-lookup"><span data-stu-id="bd17b-149">Archive window length also dictates hello maximum amount of time clients can seek back in time from hello current live position.</span></span> <span data-ttu-id="bd17b-150">Les événements peuvent s’exécuter sur la durée spécifiée hello, mais le contenu qui se trouve derrière la longueur de la fenêtre hello est ignoré en continu.</span><span class="sxs-lookup"><span data-stu-id="bd17b-150">Events can run over hello specified amount of time, but content that falls behind hello window length is continuously discarded.</span></span> <span data-ttu-id="bd17b-151">La valeur de cette propriété détermine également la durée pendant laquelle hello client manifestes peuvent atteindre.</span><span class="sxs-lookup"><span data-stu-id="bd17b-151">This value of this property also determines how long hello client manifests can grow.</span></span>

<span data-ttu-id="bd17b-152">Chaque événement est associé à un élément multimédia.</span><span class="sxs-lookup"><span data-stu-id="bd17b-152">Each event is associated with an asset.</span></span> <span data-ttu-id="bd17b-153">événement de hello toopublish, vous devez créer un localisateur OnDemand pour un composant de hello associé.</span><span class="sxs-lookup"><span data-stu-id="bd17b-153">toopublish hello event, you must create an OnDemand locator for hello associated asset.</span></span> <span data-ttu-id="bd17b-154">Ce localisateur permet toobuild une URL de diffusion en continu que vous pouvez fournir tooyour clients.</span><span class="sxs-lookup"><span data-stu-id="bd17b-154">Having this locator enables you toobuild a streaming URL that you can provide tooyour clients.</span></span>

<span data-ttu-id="bd17b-155">Un canal prend en charge jusqu'à toothree qui s’exécutent simultanément des événements, vous pouvez créer plusieurs archives de hello même flux entrant.</span><span class="sxs-lookup"><span data-stu-id="bd17b-155">A channel supports up toothree concurrently running events so you can create multiple archives of hello same incoming stream.</span></span> <span data-ttu-id="bd17b-156">Cela vous permet de toopublish et archivage de différentes parties d’un événement en fonction des besoins.</span><span class="sxs-lookup"><span data-stu-id="bd17b-156">This allows you toopublish and archive different parts of an event as needed.</span></span> <span data-ttu-id="bd17b-157">Par exemple, vos exigences d’entreprise est tooarchive 6 heures d’un programme, mais toobroadcast uniquement les 10 dernières minutes.</span><span class="sxs-lookup"><span data-stu-id="bd17b-157">For example, your business requirement is tooarchive 6 hours of a program, but toobroadcast only last 10 minutes.</span></span> <span data-ttu-id="bd17b-158">tooaccomplish, vous devez toocreate deux des programmes qui s’exécutent simultanément.</span><span class="sxs-lookup"><span data-stu-id="bd17b-158">tooaccomplish this, you need toocreate two concurrently running programs.</span></span> <span data-ttu-id="bd17b-159">Un programme a la valeur tooarchive d’événement de hello les 6 heures, mais les programme hello ne sont pas publié.</span><span class="sxs-lookup"><span data-stu-id="bd17b-159">One program is set tooarchive 6 hours of hello event but hello program is not published.</span></span> <span data-ttu-id="bd17b-160">Hello autre programme est ensemble tooarchive pendant 10 minutes et ce programme est publié.</span><span class="sxs-lookup"><span data-stu-id="bd17b-160">hello other program is set tooarchive for 10 minutes and this program is published.</span></span>

<span data-ttu-id="bd17b-161">Vous ne devez pas réutiliser d’événements en direct existants.</span><span class="sxs-lookup"><span data-stu-id="bd17b-161">You should not reuse existing live events.</span></span> <span data-ttu-id="bd17b-162">Créez et lancez plutôt un nouvel événement pour chaque événement.</span><span class="sxs-lookup"><span data-stu-id="bd17b-162">Instead, create and start a new event for each event.</span></span>

<span data-ttu-id="bd17b-163">Démarrer l’événement hello lorsque vous êtes prêt toostart diffusion et l’archivage.</span><span class="sxs-lookup"><span data-stu-id="bd17b-163">Start hello event when you are ready toostart streaming and archiving.</span></span> <span data-ttu-id="bd17b-164">Arrêter le programme de hello chaque fois que vous souhaitez toostop de diffusion en continu et l’archivage des événements de hello.</span><span class="sxs-lookup"><span data-stu-id="bd17b-164">Stop hello program whenever you want toostop streaming and archiving hello event.</span></span> 

<span data-ttu-id="bd17b-165">contenu de toodelete archivé, arrêter et supprimer un événement de hello et supprimez actif associé de hello.</span><span class="sxs-lookup"><span data-stu-id="bd17b-165">toodelete archived content, stop and delete hello event and then delete hello associated asset.</span></span> <span data-ttu-id="bd17b-166">Un élément multimédia ne peut pas être supprimé s’il est utilisé par un événement ; événement de Hello doit d’abord être supprimée.</span><span class="sxs-lookup"><span data-stu-id="bd17b-166">An asset cannot be deleted if it is used by an event; hello event must be deleted first.</span></span> 

<span data-ttu-id="bd17b-167">Même après l’arrêt et de supprimer un événement de hello, hello les utilisateurs serait en mesure de toostream votre contenu archivé comme une vidéo à la demande, pour tant que vous ne supprimez pas l’élément multimédia de hello.</span><span class="sxs-lookup"><span data-stu-id="bd17b-167">Even after you stop and delete hello event, hello users would be able toostream your archived content as a video on demand, for as long as you do not delete hello asset.</span></span>

<span data-ttu-id="bd17b-168">Si vous souhaitez hello tooretain archivé le contenu, mais n’est pas le disponible pour la diffusion en continu, supprimez hello localisateur de diffusion en continu.</span><span class="sxs-lookup"><span data-stu-id="bd17b-168">If you do want tooretain hello archived content, but not have it available for streaming, delete hello streaming locator.</span></span>

### <a name="toouse-hello-portal-toocreate-a-channel"></a><span data-ttu-id="bd17b-169">toouse hello toocreate portail un canal</span><span class="sxs-lookup"><span data-stu-id="bd17b-169">toouse hello portal toocreate a channel</span></span>
<span data-ttu-id="bd17b-170">Cette section montre comment toouse hello **création rapide** option toocreate un canal direct.</span><span class="sxs-lookup"><span data-stu-id="bd17b-170">This section shows how toouse hello **Quick Create** option toocreate a pass-through channel.</span></span>

<span data-ttu-id="bd17b-171">Pour plus d’informations sur les canaux directs, consultez [Streaming en direct avec des encodeurs locaux qui créent des flux multidébits](media-services-live-streaming-with-onprem-encoders.md).</span><span class="sxs-lookup"><span data-stu-id="bd17b-171">For more details about pass-through channels, see [Live streaming with on-premises encoders that create multi-bitrate streams](media-services-live-streaming-with-onprem-encoders.md).</span></span>

1. <span data-ttu-id="bd17b-172">Bonjour [portail Azure](https://portal.azure.com/), sélectionnez votre compte Azure Media Services.</span><span class="sxs-lookup"><span data-stu-id="bd17b-172">In hello [Azure portal](https://portal.azure.com/), select your Azure Media Services account.</span></span>
2. <span data-ttu-id="bd17b-173">Bonjour **paramètres** fenêtre, cliquez sur **diffusion en continu**.</span><span class="sxs-lookup"><span data-stu-id="bd17b-173">In hello **Settings** window, click **Live streaming**.</span></span> 
   
    ![Prise en main](./media/media-services-portal-passthrough-get-started/media-services-getting-started.png)
   
    <span data-ttu-id="bd17b-175">Hello **continu** fenêtre s’affiche.</span><span class="sxs-lookup"><span data-stu-id="bd17b-175">hello **Live streaming** window appears.</span></span>
3. <span data-ttu-id="bd17b-176">Cliquez sur **création rapide** toocreate un canal direct avec hello RTMP protocole de réception.</span><span class="sxs-lookup"><span data-stu-id="bd17b-176">Click **Quick Create** toocreate a pass-through channel with hello RTMP ingest protocol.</span></span>
   
    <span data-ttu-id="bd17b-177">Hello **créer un nouveau canal** fenêtre s’affiche.</span><span class="sxs-lookup"><span data-stu-id="bd17b-177">hello **CREATE A NEW CHANNEL** window appears.</span></span>
4. <span data-ttu-id="bd17b-178">Donnez un nom à nouveau canal de hello et cliquez sur **créer**.</span><span class="sxs-lookup"><span data-stu-id="bd17b-178">Give hello new channel a name and click **Create**.</span></span> 
   
    <span data-ttu-id="bd17b-179">Cela crée un canal direct avec hello protocole de réception RTMP.</span><span class="sxs-lookup"><span data-stu-id="bd17b-179">This creates a pass-through channel with hello RTMP ingest protocol.</span></span>

## <a name="create-events"></a><span data-ttu-id="bd17b-180">Créer des événements</span><span class="sxs-lookup"><span data-stu-id="bd17b-180">Create events</span></span>
1. <span data-ttu-id="bd17b-181">Sélectionnez un toowhich de canal que vous voulez tooadd un événement.</span><span class="sxs-lookup"><span data-stu-id="bd17b-181">Select a channel toowhich you want tooadd an event.</span></span>
2. <span data-ttu-id="bd17b-182">Appuyez sur le bouton **Événement réel** .</span><span class="sxs-lookup"><span data-stu-id="bd17b-182">Press **Live Event** button.</span></span>

![Événement](./media/media-services-portal-passthrough-get-started/media-services-create-events.png)

## <a name="get-ingest-urls"></a><span data-ttu-id="bd17b-184">Obtenir les URL de réception</span><span class="sxs-lookup"><span data-stu-id="bd17b-184">Get ingest URLs</span></span>
<span data-ttu-id="bd17b-185">Une fois que le canal de hello est créé, vous pouvez obtenir les URL que vous fournirez un encodeur en temps réel de toohello d’ingestion.</span><span class="sxs-lookup"><span data-stu-id="bd17b-185">Once hello channel is created, you can get ingest URLs that you will provide toohello live encoder.</span></span> <span data-ttu-id="bd17b-186">encodeur de Hello utilise ces tooinput URL un flux en direct.</span><span class="sxs-lookup"><span data-stu-id="bd17b-186">hello encoder uses these URLs tooinput a live stream.</span></span>

![Date de création](./media/media-services-portal-passthrough-get-started/media-services-channel-created.png)

## <a name="watch-hello-event"></a><span data-ttu-id="bd17b-188">Événement de hello espion</span><span class="sxs-lookup"><span data-stu-id="bd17b-188">Watch hello event</span></span>
<span data-ttu-id="bd17b-189">événement de hello toowatch, cliquez sur **espion** hello Azure hello portail ou de copie URL de diffusion en continu et utilisez un lecteur de votre choix.</span><span class="sxs-lookup"><span data-stu-id="bd17b-189">toowatch hello event, click **Watch** in hello Azure portal or copy hello streaming URL and use a player of your choice.</span></span> 

![Date de création](./media/media-services-portal-passthrough-get-started/media-services-default-event.png)

<span data-ttu-id="bd17b-191">Événement en direct obtiennent automatiquement le contenu de la demande tooon converti lors de l’arrêt.</span><span class="sxs-lookup"><span data-stu-id="bd17b-191">Live event automatically get converted tooon-demand content when stopped.</span></span>

## <a name="clean-up"></a><span data-ttu-id="bd17b-192">Nettoyer</span><span class="sxs-lookup"><span data-stu-id="bd17b-192">Clean up</span></span>
<span data-ttu-id="bd17b-193">Pour plus d’informations sur les canaux directs, consultez [Streaming en direct avec des encodeurs locaux qui créent des flux multidébits](media-services-live-streaming-with-onprem-encoders.md).</span><span class="sxs-lookup"><span data-stu-id="bd17b-193">For more details about pass-through channels, see [Live streaming with on-premises encoders that create multi-bitrate streams](media-services-live-streaming-with-onprem-encoders.md).</span></span>

* <span data-ttu-id="bd17b-194">Un canal peut être arrêté uniquement lorsque tous les événements de programmes sur un canal de hello ont été arrêtés.</span><span class="sxs-lookup"><span data-stu-id="bd17b-194">A channel can be stopped only when all events/programs on hello channel have been stopped.</span></span>  <span data-ttu-id="bd17b-195">Une fois que le canal de hello est arrêtée, elle n’entraîne pas de tous les frais.</span><span class="sxs-lookup"><span data-stu-id="bd17b-195">Once hello Channel is stopped, it does not incur any charges.</span></span> <span data-ttu-id="bd17b-196">Lorsque vous devez toostart il à nouveau, il aura hello même URL de réception afin de vous n’aurez pas tooreconfigure votre encodeur.</span><span class="sxs-lookup"><span data-stu-id="bd17b-196">When you need toostart it again, it will have hello same ingest URL so you won't need tooreconfigure your encoder.</span></span>
* <span data-ttu-id="bd17b-197">Un canal peut être supprimé uniquement lorsque tous les événements en direct sur le canal de hello ont été supprimés.</span><span class="sxs-lookup"><span data-stu-id="bd17b-197">A channel can be deleted only when all live events on hello channel have been deleted.</span></span>

## <a name="view-archived-content"></a><span data-ttu-id="bd17b-198">Afficher le contenu archivé</span><span class="sxs-lookup"><span data-stu-id="bd17b-198">View archived content</span></span>
<span data-ttu-id="bd17b-199">Même après l’arrêt et de supprimer un événement de hello, hello les utilisateurs serait en mesure de toostream votre contenu archivé comme une vidéo à la demande, pour tant que vous ne supprimez pas l’élément multimédia de hello.</span><span class="sxs-lookup"><span data-stu-id="bd17b-199">Even after you stop and delete hello event, hello users would be able toostream your archived content as a video on demand, for as long as you do not delete hello asset.</span></span> <span data-ttu-id="bd17b-200">Un élément multimédia ne peut pas être supprimé s’il est utilisé par un événement ; événement de Hello doit d’abord être supprimée.</span><span class="sxs-lookup"><span data-stu-id="bd17b-200">An asset cannot be deleted if it is used by an event; hello event must be deleted first.</span></span> 

<span data-ttu-id="bd17b-201">sélectionner de vos éléments multimédias, toomanage **paramètre** et cliquez sur **actifs**.</span><span class="sxs-lookup"><span data-stu-id="bd17b-201">toomanage your assets, select **Setting** and click **Assets**.</span></span>

![Éléments multimédias](./media/media-services-portal-passthrough-get-started/media-services-assets.png)

## <a name="next-step"></a><span data-ttu-id="bd17b-203">Étape suivante</span><span class="sxs-lookup"><span data-stu-id="bd17b-203">Next step</span></span>
<span data-ttu-id="bd17b-204">Consultez les parcours d’apprentissage de Media Services.</span><span class="sxs-lookup"><span data-stu-id="bd17b-204">Review Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="bd17b-205">Fournir des commentaires</span><span class="sxs-lookup"><span data-stu-id="bd17b-205">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

