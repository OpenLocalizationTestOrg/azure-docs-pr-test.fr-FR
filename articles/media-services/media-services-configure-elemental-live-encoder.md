---
title: "aaaConfigure hello toosend d’encodeur Live élémentaire un flux à débit binaire unique en continu | Documents Microsoft"
description: "Cette rubrique montre comment tooconfigure hello toosend d’encodeur Live élémentaire un canaux tooAMS de flux à débit binaire unique qui est activés pour l’encodage live."
services: media-services
documentationcenter: 
author: cenkdin
manager: cfowler
editor: 
ms.assetid: 9c6bf6a9-6273-4fdd-9477-f0e565280b5b
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: ne
ms.topic: article
ms.date: 01/05/2017
ms.author: cenkd;anilmur;juliako
ms.openlocfilehash: 9a5de6189bfb123768a9da038b8c8db69cf85e91
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-elemental-live-encoder-toosend-a-single-bitrate-live-stream"></a><span data-ttu-id="36a2f-103">Utilisez hello Live élémentaire encodeur toosend un flux à débit binaire unique en continu.</span><span class="sxs-lookup"><span data-stu-id="36a2f-103">Use hello Elemental Live encoder toosend a single bitrate live stream</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="36a2f-104">Elemental Live</span><span class="sxs-lookup"><span data-stu-id="36a2f-104">Elemental Live</span></span>](media-services-configure-elemental-live-encoder.md)
> * [<span data-ttu-id="36a2f-105">Tricaster</span><span class="sxs-lookup"><span data-stu-id="36a2f-105">Tricaster</span></span>](media-services-configure-tricaster-live-encoder.md)
> * [<span data-ttu-id="36a2f-106">Wirecast</span><span class="sxs-lookup"><span data-stu-id="36a2f-106">Wirecast</span></span>](media-services-configure-wirecast-live-encoder.md)
> * [<span data-ttu-id="36a2f-107">FMLE</span><span class="sxs-lookup"><span data-stu-id="36a2f-107">FMLE</span></span>](media-services-configure-fmle-live-encoder.md)
>
>

<span data-ttu-id="36a2f-108">Cette rubrique montre comment tooconfigure hello [Live élémentaire](http://www.elementaltechnologies.com/products/elemental-live) encodeur toosend canaux tooAMS qui sont activés pour l’encodage live de diffuser un débit binaire unique.</span><span class="sxs-lookup"><span data-stu-id="36a2f-108">This topic shows how tooconfigure hello [Elemental Live](http://www.elementaltechnologies.com/products/elemental-live) encoder toosend a single bitrate stream tooAMS channels that are enabled for live encoding.</span></span>  <span data-ttu-id="36a2f-109">Pour plus d’informations, consultez [utilisation de canaux est à activé tooPerform Live encodage avec Azure Media Services](media-services-manage-live-encoder-enabled-channels.md).</span><span class="sxs-lookup"><span data-stu-id="36a2f-109">For more information, see [Working with Channels that are Enabled tooPerform Live Encoding with Azure Media Services](media-services-manage-live-encoder-enabled-channels.md).</span></span>

<span data-ttu-id="36a2f-110">Ce didacticiel montre comment toomanage Azure Media Services (AMS) avec l’outil d’Azure Media Services Explorer (AMSE).</span><span class="sxs-lookup"><span data-stu-id="36a2f-110">This tutorial shows how toomanage Azure Media Services (AMS) with Azure Media Services Explorer (AMSE) tool.</span></span> <span data-ttu-id="36a2f-111">Cet outil est uniquement compatible avec les PC Windows.</span><span class="sxs-lookup"><span data-stu-id="36a2f-111">This tool only runs on Windows PC.</span></span> <span data-ttu-id="36a2f-112">Si vous êtes sur le Mac ou Linux, utilisez hello toocreate portail Azure [canaux](media-services-portal-creating-live-encoder-enabled-channel.md#create-a-channel) et [programmes](media-services-portal-creating-live-encoder-enabled-channel.md).</span><span class="sxs-lookup"><span data-stu-id="36a2f-112">If you are on Mac or Linux, use hello Azure portal toocreate [channels](media-services-portal-creating-live-encoder-enabled-channel.md#create-a-channel) and [programs](media-services-portal-creating-live-encoder-enabled-channel.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="36a2f-113">Composants requis</span><span class="sxs-lookup"><span data-stu-id="36a2f-113">Prerequisites</span></span>
* <span data-ttu-id="36a2f-114">Doit avoir une connaissance pratique de l’utilisation de Live élémentaire web interface toocreate événements en direct.</span><span class="sxs-lookup"><span data-stu-id="36a2f-114">Must have a working knowledge of using Elemental Live web interface toocreate live events.</span></span>
* [<span data-ttu-id="36a2f-115">Créer un compte Azure Media Services</span><span class="sxs-lookup"><span data-stu-id="36a2f-115">Create an Azure Media Services account</span></span>](media-services-portal-create-account.md)
* <span data-ttu-id="36a2f-116">Vérifiez qu’un point de terminaison de streaming est en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="36a2f-116">Ensure there is a Streaming Endpoint running.</span></span> <span data-ttu-id="36a2f-117">Pour plus d’informations, consultez la rubrique [Gestion des points de terminaison de diffusion en continu dans un compte Media Services](media-services-portal-manage-streaming-endpoints.md).</span><span class="sxs-lookup"><span data-stu-id="36a2f-117">For more information, see [Manage Streaming Endpoints in a Media Services Account](media-services-portal-manage-streaming-endpoints.md).</span></span>
* <span data-ttu-id="36a2f-118">Installer la version la plus récente de hello hello [AMSE](https://github.com/Azure/Azure-Media-Services-Explorer) outil.</span><span class="sxs-lookup"><span data-stu-id="36a2f-118">Install hello latest version of hello [AMSE](https://github.com/Azure/Azure-Media-Services-Explorer) tool.</span></span>
* <span data-ttu-id="36a2f-119">Lancer l’outil de hello et tooyour AMS compte de connexion.</span><span class="sxs-lookup"><span data-stu-id="36a2f-119">Launch hello tool and connect tooyour AMS account.</span></span>

## <a name="tips"></a><span data-ttu-id="36a2f-120">Conseils</span><span class="sxs-lookup"><span data-stu-id="36a2f-120">Tips</span></span>
* <span data-ttu-id="36a2f-121">Si possible, utilisez une connexion Internet câblée.</span><span class="sxs-lookup"><span data-stu-id="36a2f-121">Whenever possible, use a hardwired internet connection.</span></span>
* <span data-ttu-id="36a2f-122">Une règle empirique lors de la détermination de la bande passante est hello toodouble débits binaires de diffusion en continu.</span><span class="sxs-lookup"><span data-stu-id="36a2f-122">A good rule of thumb when determining bandwidth requirements is toodouble hello streaming bitrates.</span></span> <span data-ttu-id="36a2f-123">Alors que cela n’est pas obligatoire, il vous aide à atténuer l’impact hello de congestion du réseau.</span><span class="sxs-lookup"><span data-stu-id="36a2f-123">While this is not a mandatory requirement, it will help mitigate hello impact of network congestion.</span></span>
* <span data-ttu-id="36a2f-124">Lors de l’utilisation d’encodeurs logiciels, fermez tous les programmes inutiles.</span><span class="sxs-lookup"><span data-stu-id="36a2f-124">When using software based encoders, close out any unnecessary programs.</span></span>

## <a name="elemental-live-with-rtp-ingest"></a><span data-ttu-id="36a2f-125">Elemental Live avec réception RTP</span><span class="sxs-lookup"><span data-stu-id="36a2f-125">Elemental Live with RTP ingest</span></span>
<span data-ttu-id="36a2f-126">Cette section montre comment encoder de Live élémentaire tooconfigure hello qui envoie un débit binaire unique flux dynamique sur RTP.</span><span class="sxs-lookup"><span data-stu-id="36a2f-126">This section shows how tooconfigure hello Elemental Live encoder that sends a single bitrate live stream over RTP.</span></span>  <span data-ttu-id="36a2f-127">Pour plus d’informations, consultez la rubrique [Flux MPEG-TS via RTP](media-services-manage-live-encoder-enabled-channels.md#channel).</span><span class="sxs-lookup"><span data-stu-id="36a2f-127">For more information, see [MPEG-TS stream over RTP](media-services-manage-live-encoder-enabled-channels.md#channel).</span></span>

### <a name="create-a-channel"></a><span data-ttu-id="36a2f-128">Créer un canal</span><span class="sxs-lookup"><span data-stu-id="36a2f-128">Create a channel</span></span>

1. <span data-ttu-id="36a2f-129">Dans l’outil AMSE hello, accédez à toohello **Live** onglet et cliquez avec le bouton droit dans la zone de canal hello.</span><span class="sxs-lookup"><span data-stu-id="36a2f-129">In hello AMSE tool, navigate toohello **Live** tab, and right click within hello channel area.</span></span> <span data-ttu-id="36a2f-130">Dans le menu qui s’affiche, sélectionnez **Créer un canal...**</span><span class="sxs-lookup"><span data-stu-id="36a2f-130">Select **Create channel…**</span></span> <span data-ttu-id="36a2f-131">à partir du menu de hello.</span><span class="sxs-lookup"><span data-stu-id="36a2f-131">from hello menu.</span></span>

    ![Elemental](./media/media-services-elemental-live-encoder/media-services-elemental1.png)

2. <span data-ttu-id="36a2f-133">Spécifiez un nom de canal, champ de description hello est facultatif.</span><span class="sxs-lookup"><span data-stu-id="36a2f-133">Specify a channel name, hello description field is optional.</span></span> <span data-ttu-id="36a2f-134">Sous paramètres de canal, sélectionnez **Standard** pour hello option d’encodage Live, avec hello entrée protocole défini trop**RTP (MPEG-TS)**.</span><span class="sxs-lookup"><span data-stu-id="36a2f-134">Under Channel Settings, select **Standard** for hello Live Encoding option, with hello Input Protocol set too**RTP (MPEG-TS)**.</span></span> <span data-ttu-id="36a2f-135">Vous pouvez laisser tous les autres paramètres inchangés.</span><span class="sxs-lookup"><span data-stu-id="36a2f-135">You can leave all other settings as is.</span></span>

    <span data-ttu-id="36a2f-136">Vérifiez que hello **début hello nouveau canal maintenant** est sélectionnée.</span><span class="sxs-lookup"><span data-stu-id="36a2f-136">Make sure hello **Start hello new channel now** is selected.</span></span>

3. <span data-ttu-id="36a2f-137">Cliquez sur **Créer un canal**.</span><span class="sxs-lookup"><span data-stu-id="36a2f-137">Click **Create Channel**.</span></span>

   ![Elemental](./media/media-services-elemental-live-encoder/media-services-elemental12.png)

> [!NOTE]
> <span data-ttu-id="36a2f-139">canal de Hello peut prendre jusqu'à 20 minutes toostart.</span><span class="sxs-lookup"><span data-stu-id="36a2f-139">hello channel can take as long as 20 minutes toostart.</span></span>
>
>

<span data-ttu-id="36a2f-140">Pendant le démarrage du canal de hello, vous pouvez [configurer l’encodeur de hello](media-services-configure-elemental-live-encoder.md#configure_elemental_rtp).</span><span class="sxs-lookup"><span data-stu-id="36a2f-140">While hello channel is starting you can [configure hello encoder](media-services-configure-elemental-live-encoder.md#configure_elemental_rtp).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="36a2f-141">Notez que la facturation commence dès que l’état du canal indique qu’il est prêt à être utilisé.</span><span class="sxs-lookup"><span data-stu-id="36a2f-141">Note that billing starts as soon as Channel goes into a ready state.</span></span> <span data-ttu-id="36a2f-142">Pour plus d’informations, consultez [États du canal](media-services-manage-live-encoder-enabled-channels.md#states).</span><span class="sxs-lookup"><span data-stu-id="36a2f-142">For more information, see [Channel's states](media-services-manage-live-encoder-enabled-channels.md#states).</span></span>
>
>

### <span data-ttu-id="36a2f-143"><a id=configure_elemental_rtp></a>Configurer l’encodeur Live élémentaire de hello</span><span class="sxs-lookup"><span data-stu-id="36a2f-143"><a id=configure_elemental_rtp></a>Configure hello Elemental Live encoder</span></span>
<span data-ttu-id="36a2f-144">Dans ce didacticiel hello des paramètres de sortie suivants sont utilisés.</span><span class="sxs-lookup"><span data-stu-id="36a2f-144">In this tutorial hello following output settings are used.</span></span> <span data-ttu-id="36a2f-145">Hello le reste de cette section décrit les étapes de configuration plus en détail.</span><span class="sxs-lookup"><span data-stu-id="36a2f-145">hello rest of this section describes configuration steps in more detail.</span></span>

<span data-ttu-id="36a2f-146">**Vidéo**:</span><span class="sxs-lookup"><span data-stu-id="36a2f-146">**Video**:</span></span>

* <span data-ttu-id="36a2f-147">Codec : H.264</span><span class="sxs-lookup"><span data-stu-id="36a2f-147">Codec: H.264</span></span>
* <span data-ttu-id="36a2f-148">Profil : Élevé (niveau 4.0)</span><span class="sxs-lookup"><span data-stu-id="36a2f-148">Profile: High (Level 4.0)</span></span>
* <span data-ttu-id="36a2f-149">Débit binaire : 5 000 kbit/s</span><span class="sxs-lookup"><span data-stu-id="36a2f-149">Bitrate: 5000 kbps</span></span>
* <span data-ttu-id="36a2f-150">Image clé : 2 secondes (60 secondes)</span><span class="sxs-lookup"><span data-stu-id="36a2f-150">Keyframe: 2 seconds (60 seconds)</span></span>
* <span data-ttu-id="36a2f-151">Fréquence d’images : 30</span><span class="sxs-lookup"><span data-stu-id="36a2f-151">Frame Rate: 30</span></span>

<span data-ttu-id="36a2f-152">**Audio**:</span><span class="sxs-lookup"><span data-stu-id="36a2f-152">**Audio**:</span></span>

* <span data-ttu-id="36a2f-153">Codec : AAC (LC)</span><span class="sxs-lookup"><span data-stu-id="36a2f-153">Codec: AAC (LC)</span></span>
* <span data-ttu-id="36a2f-154">Débit binaire : 192 kbit/s</span><span class="sxs-lookup"><span data-stu-id="36a2f-154">Bitrate: 192 kbps</span></span>
* <span data-ttu-id="36a2f-155">Taux d’échantillonnage : 44,1 kHz</span><span class="sxs-lookup"><span data-stu-id="36a2f-155">Sample Rate: 44.1 kHz</span></span>

#### <a name="configuration-steps"></a><span data-ttu-id="36a2f-156">Configuration</span><span class="sxs-lookup"><span data-stu-id="36a2f-156">Configuration steps</span></span>
1. <span data-ttu-id="36a2f-157">Accédez toohello **Live élémentaire** interface web et configurer encodeur hello pour **UDP/TS** de diffusion en continu.</span><span class="sxs-lookup"><span data-stu-id="36a2f-157">Navigate toohello **Elemental Live** web interface, and set up hello encoder for **UDP/TS** streaming.</span></span>
2. <span data-ttu-id="36a2f-158">Une fois qu’un nouvel événement est créé, faites défiler la liste des groupes de sorties toohello et ajouter hello **UDP/TS** le groupe de sorties.</span><span class="sxs-lookup"><span data-stu-id="36a2f-158">Once a new event is created, scroll down toohello output groups and add hello **UDP/TS** output group.</span></span>
3. <span data-ttu-id="36a2f-159">Créez une nouvelle sortie en sélectionnant **New Stream**, puis en cliquant sur **Add Output**.</span><span class="sxs-lookup"><span data-stu-id="36a2f-159">Create a new output by selecting **New Stream** and then clicking **Add Output**.</span></span>  

    ![Elemental](./media/media-services-elemental-live-encoder/media-services-elemental13.png)

   > [!NOTE]
   > <span data-ttu-id="36a2f-161">Il est recommandé que l’événement élémentaire hello a timecode hello défini trop encodeur de « L’horloge système » toohelp hello reconnecter dans les cas de hello d’une erreur de flux de données.</span><span class="sxs-lookup"><span data-stu-id="36a2f-161">It is recommended that hello Elemental event has hello timecode set too"System Clock" toohelp hello encoder reconnect in hello case of a stream failure.</span></span>
   >
   >
4. <span data-ttu-id="36a2f-162">Maintenant que hello sortie a été créée, cliquez sur **d’ajouter un flux**.</span><span class="sxs-lookup"><span data-stu-id="36a2f-162">Now that hello Output has been created, click **Add Stream**.</span></span> <span data-ttu-id="36a2f-163">paramètres de sortie Hello peuvent maintenant être configurés.</span><span class="sxs-lookup"><span data-stu-id="36a2f-163">hello output settings can now be configured.</span></span>
5. <span data-ttu-id="36a2f-164">Faites défiler la liste toohello « Stream 1 » qui vient d’être créé, cliquez sur hello **vidéo** onglet hello gauche et développez hello **avancé** section de paramètres.</span><span class="sxs-lookup"><span data-stu-id="36a2f-164">Scroll down toohello "Stream 1" that was just created, click hello **Video** tab on hello left and expand hello **Advanced** settings section.</span></span>

    ![Elemental](./media/media-services-elemental-live-encoder/media-services-elemental4.png)

    <span data-ttu-id="36a2f-166">Alors que Live élémentaire a une grande variété de personnalisation disponibles, hello paramètres suivants sont recommandés pour la mise en route de tooAMS de diffusion en continu.</span><span class="sxs-lookup"><span data-stu-id="36a2f-166">While Elemental Live has a wide range of available customizing, hello following settings are recommended for getting started with streaming tooAMS.</span></span>

   * <span data-ttu-id="36a2f-167">Resolution : 1280 x 720</span><span class="sxs-lookup"><span data-stu-id="36a2f-167">Resolution: 1280 x 720</span></span>
   * <span data-ttu-id="36a2f-168">Framerate : 30</span><span class="sxs-lookup"><span data-stu-id="36a2f-168">Framerate: 30</span></span>
   * <span data-ttu-id="36a2f-169">GOP Size : 60 frames</span><span class="sxs-lookup"><span data-stu-id="36a2f-169">GOP Size: 60 frames</span></span>
   * <span data-ttu-id="36a2f-170">Interlace Mode : Progressive</span><span class="sxs-lookup"><span data-stu-id="36a2f-170">Interlace Mode: Progressive</span></span>
   * <span data-ttu-id="36a2f-171">Bitrate : 5000000 bit/s (cette valeur peut être ajustée en fonction des limitations du réseau)</span><span class="sxs-lookup"><span data-stu-id="36a2f-171">Bitrate: 5000000 bit/s (This can be adjusted based on network limitations)</span></span>

    ![Elemental](./media/media-services-elemental-live-encoder/media-services-elemental5.png)

1. <span data-ttu-id="36a2f-173">Obtient les URL d’entrée du canal hello.</span><span class="sxs-lookup"><span data-stu-id="36a2f-173">Get hello channel's input URL.</span></span>

    <span data-ttu-id="36a2f-174">Accédez outil AMSE toohello précédent et vérifier l’état d’achèvement canal hello.</span><span class="sxs-lookup"><span data-stu-id="36a2f-174">Navigate back toohello AMSE tool, and check on hello channel completion status.</span></span> <span data-ttu-id="36a2f-175">Une fois que l’état de hello a été modifié à partir de **départ** trop**en cours d’exécution**, vous pouvez obtenir les URL d’entrée hello.</span><span class="sxs-lookup"><span data-stu-id="36a2f-175">Once hello State has changed from **Starting** too**Running**, you can get hello input URL.</span></span>

    <span data-ttu-id="36a2f-176">Lorsque le canal de hello est en cours d’exécution, cliquez avec le bouton droit sur nom de la chaîne hello, naviguez vers le bas toohover sur **tooclipboard de copier l’URL entrée** , puis sélectionnez **URL entrée principale**.</span><span class="sxs-lookup"><span data-stu-id="36a2f-176">When hello channel is running, right click hello channel name, navigate down toohover over **Copy Input URL tooclipboard** and then select **Primary Input  URL**.</span></span>  

    ![Elemental](./media/media-services-elemental-live-encoder/media-services-elemental6.png)
2. <span data-ttu-id="36a2f-178">Coller ces informations dans hello **Destination primaire** champ hello élémentaire.</span><span class="sxs-lookup"><span data-stu-id="36a2f-178">Paste this information in hello **Primary Destination** field of hello Elemental.</span></span> <span data-ttu-id="36a2f-179">Tous les autres paramètres peuvent rester par défaut de hello.</span><span class="sxs-lookup"><span data-stu-id="36a2f-179">All other settings can remain hello default.</span></span>

    ![Elemental](./media/media-services-elemental-live-encoder/media-services-elemental14.png)

    <span data-ttu-id="36a2f-181">Pour assurer la redondance supplémentaire, répétez ces étapes avec hello secondaire URL d’entrée en créant un onglet séparé de « Sortie » pour la diffusion en continu UDP/TS.</span><span class="sxs-lookup"><span data-stu-id="36a2f-181">For extra redundancy, repeat these steps with hello Secondary Input URL by creating a separate "Output" tab for UDP/TS Streaming.</span></span>
3. <span data-ttu-id="36a2f-182">Cliquez sur **créer** (si un nouvel événement a été créé) ou **mise à jour** (si la modification d’un événement existant), puis continuez encodeur de hello toostart.</span><span class="sxs-lookup"><span data-stu-id="36a2f-182">Click **Create** (if a new event was created) or **Update** (if editing a pre-existing event) and then proceed toostart hello encoder.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="36a2f-183">Avant de cliquer sur **Démarrer** sur l’interface web Live élémentaire hello, vous **doit** vous assurer que le canal de hello est prêt.</span><span class="sxs-lookup"><span data-stu-id="36a2f-183">Before you click **Start** on hello Elemental Live web interface, you **must** ensure that hello Channel is ready.</span></span>
> <span data-ttu-id="36a2f-184">Assurez-vous également que pas tooleave hello canal dans un état prêt sans un événement pendant plus de 15 minutes >.</span><span class="sxs-lookup"><span data-stu-id="36a2f-184">Also, make sure not tooleave hello Channel in a ready state without an event for longer than > 15 minutes.</span></span>
>
>

<span data-ttu-id="36a2f-185">Une fois le flux de données hello s’exécute pendant 30 secondes, accédez toohello arrière AMSE outil et test de la lecture.</span><span class="sxs-lookup"><span data-stu-id="36a2f-185">After hello stream has been running for 30 seconds, navigate back toohello AMSE tool and test playback.</span></span>  

### <a name="test-playback"></a><span data-ttu-id="36a2f-186">Tester la lecture</span><span class="sxs-lookup"><span data-stu-id="36a2f-186">Test playback</span></span>

<span data-ttu-id="36a2f-187">Accédez outil AMSE toohello et cliquez avec le bouton droit sur toobe de canal hello testé.</span><span class="sxs-lookup"><span data-stu-id="36a2f-187">Navigate toohello AMSE tool, and right click hello channel toobe tested.</span></span> <span data-ttu-id="36a2f-188">À partir du menu de hello, placez le curseur sur **hello de lecture aperçu** et sélectionnez **avec Azure Media Player**.</span><span class="sxs-lookup"><span data-stu-id="36a2f-188">From hello menu, hover over **Playback hello Preview** and select **with Azure Media Player**.</span></span>  

    ![Elemental](./media/media-services-elemental-live-encoder/media-services-elemental8.png)

<span data-ttu-id="36a2f-189">Si le flux de données hello s’affiche dans le lecteur hello, encodeur de hello a été correctement configuré tooconnect tooAMS.</span><span class="sxs-lookup"><span data-stu-id="36a2f-189">If hello stream appears in hello player, then hello encoder has been properly configured tooconnect tooAMS.</span></span>

<span data-ttu-id="36a2f-190">Si une erreur est reçue, le canal de hello devez paramètres d’encodeur et de réinitialisation toobe ajustées.</span><span class="sxs-lookup"><span data-stu-id="36a2f-190">If an error is received, hello channel will need toobe reset and encoder settings adjusted.</span></span> <span data-ttu-id="36a2f-191">Consultez hello [dépannage](media-services-troubleshooting-live-streaming.md) rubrique pour obtenir des conseils.</span><span class="sxs-lookup"><span data-stu-id="36a2f-191">Please see hello [troubleshooting](media-services-troubleshooting-live-streaming.md) topic for guidance.</span></span>   

### <a name="create-a-program"></a><span data-ttu-id="36a2f-192">Créer un programme</span><span class="sxs-lookup"><span data-stu-id="36a2f-192">Create a program</span></span>
1. <span data-ttu-id="36a2f-193">Une fois que vous avez vérifié que la lecture fonctionne sur le canal, créez un programme.</span><span class="sxs-lookup"><span data-stu-id="36a2f-193">Once channel playback is confirmed, create a program.</span></span> <span data-ttu-id="36a2f-194">Sous hello **Live** onglet dans l’outil AMSE hello, cliquez avec le bouton droit dans la zone du programme hello et sélectionnez **créer un nouveau programme**.</span><span class="sxs-lookup"><span data-stu-id="36a2f-194">Under hello **Live** tab in hello AMSE tool, right click within hello program area and select **Create New Program**.</span></span>  

    ![Elemental](./media/media-services-elemental-live-encoder/media-services-elemental9.png)
2. <span data-ttu-id="36a2f-196">Nom de programme de hello et, si nécessaire, ajustez hello **longueur de fenêtre d’Archive** (heures de too4 les valeurs par défaut).</span><span class="sxs-lookup"><span data-stu-id="36a2f-196">Name hello program and, if needed, adjust hello **Archive Window Length** (which defaults too4 hours).</span></span> <span data-ttu-id="36a2f-197">Vous pouvez également spécifier un emplacement de stockage ou les conserver en tant que valeur par défaut hello.</span><span class="sxs-lookup"><span data-stu-id="36a2f-197">You can also specify a storage location or leave as hello default.</span></span>  
3. <span data-ttu-id="36a2f-198">Vérifiez hello **maintenant démarrer hello programme** boîte.</span><span class="sxs-lookup"><span data-stu-id="36a2f-198">Check hello **Start hello Program now** box.</span></span>
4. <span data-ttu-id="36a2f-199">Cliquez sur **Créer le programme**.</span><span class="sxs-lookup"><span data-stu-id="36a2f-199">Click **Create Program**.</span></span>  

    >[!NOTE]
    > <span data-ttu-id="36a2f-200">La création d’un programme prend moins de temps que la création d’un canal.</span><span class="sxs-lookup"><span data-stu-id="36a2f-200">Program creation takes less time than channel creation.</span></span>   
      
5. <span data-ttu-id="36a2f-201">Une fois l’exécution du programme hello, confirmer la lecture en cliquant avec le bouton droit sur un programme hello et en naviguant trop**lecture hello programmes** , puis en sélectionnant **avec Azure Media Player**.</span><span class="sxs-lookup"><span data-stu-id="36a2f-201">Once hello program is running, confirm playback by right clicking hello program and navigating too**Playback hello program(s)** and then selecting **with Azure Media Player**.</span></span>  
6. <span data-ttu-id="36a2f-202">Après confirmation, cliquez à nouveau programme de hello, puis sélectionnez **copier hello URL de sortie tooClipboard** (ou en extraire ces informations hello **informations et des paramètres du programme** option de menu de hello).</span><span class="sxs-lookup"><span data-stu-id="36a2f-202">Once confirmed, right click hello program again and select **Copy hello Output URL tooClipboard** (or retrieve this information from hello **Program information and settings** option from hello menu).</span></span>

<span data-ttu-id="36a2f-203">Hello flux est maintenant prêt toobe incorporé dans un lecteur ou public tooan distribuée pour live affichage.</span><span class="sxs-lookup"><span data-stu-id="36a2f-203">hello stream is now ready toobe embedded in a player, or distributed tooan audience for live viewing.</span></span>  

## <a name="troubleshooting"></a><span data-ttu-id="36a2f-204">Résolution des problèmes</span><span class="sxs-lookup"><span data-stu-id="36a2f-204">Troubleshooting</span></span>
<span data-ttu-id="36a2f-205">Consultez hello [dépannage](media-services-troubleshooting-live-streaming.md) rubrique pour obtenir des conseils.</span><span class="sxs-lookup"><span data-stu-id="36a2f-205">Please see hello [troubleshooting](media-services-troubleshooting-live-streaming.md) topic for guidance.</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="36a2f-206">Parcours d’apprentissage de Media Services</span><span class="sxs-lookup"><span data-stu-id="36a2f-206">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="36a2f-207">Fournir des commentaires</span><span class="sxs-lookup"><span data-stu-id="36a2f-207">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
