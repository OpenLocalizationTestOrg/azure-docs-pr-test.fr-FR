---
title: "Configurer l’encodeur Elemental Live pour envoyer un flux live à débit binaire unique | Microsoft Docs"
description: "Cette rubrique explique comment configurer l’encodeur Elemental Live afin d’envoyer un flux à débit binaire unique à des canaux AMS activés pour l’encodage en temps réel."
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
ms.openlocfilehash: 668a3ab46a70c0ee25fa87031d27c0f4333ec89c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="use-the-elemental-live-encoder-to-send-a-single-bitrate-live-stream"></a><span data-ttu-id="cc0d8-103">Utiliser l’encodeur Elemental Live pour envoyer un flux live à débit binaire unique</span><span class="sxs-lookup"><span data-stu-id="cc0d8-103">Use the Elemental Live encoder to send a single bitrate live stream</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="cc0d8-104">Elemental Live</span><span class="sxs-lookup"><span data-stu-id="cc0d8-104">Elemental Live</span></span>](media-services-configure-elemental-live-encoder.md)
> * [<span data-ttu-id="cc0d8-105">Tricaster</span><span class="sxs-lookup"><span data-stu-id="cc0d8-105">Tricaster</span></span>](media-services-configure-tricaster-live-encoder.md)
> * [<span data-ttu-id="cc0d8-106">Wirecast</span><span class="sxs-lookup"><span data-stu-id="cc0d8-106">Wirecast</span></span>](media-services-configure-wirecast-live-encoder.md)
> * [<span data-ttu-id="cc0d8-107">FMLE</span><span class="sxs-lookup"><span data-stu-id="cc0d8-107">FMLE</span></span>](media-services-configure-fmle-live-encoder.md)
>
>

<span data-ttu-id="cc0d8-108">Cette rubrique explique comment configurer l’encodeur [Elemental Live](http://www.elementaltechnologies.com/products/elemental-live) afin d’envoyer un flux à débit binaire unique à des canaux AMS activés pour l’encodage en temps réel.</span><span class="sxs-lookup"><span data-stu-id="cc0d8-108">This topic shows how to configure the [Elemental Live](http://www.elementaltechnologies.com/products/elemental-live) encoder to send a single bitrate stream to AMS channels that are enabled for live encoding.</span></span>  <span data-ttu-id="cc0d8-109">Pour plus d’informations, consultez la rubrique [Utilisation de canaux activés pour effectuer un encodage en temps réel avec Azure Media Services](media-services-manage-live-encoder-enabled-channels.md).</span><span class="sxs-lookup"><span data-stu-id="cc0d8-109">For more information, see [Working with Channels that are Enabled to Perform Live Encoding with Azure Media Services](media-services-manage-live-encoder-enabled-channels.md).</span></span>

<span data-ttu-id="cc0d8-110">Ce didacticiel montre comment gérer Azure Media Services (AMS) avec l’outil Azure Media Services Explorer (AMSE).</span><span class="sxs-lookup"><span data-stu-id="cc0d8-110">This tutorial shows how to manage Azure Media Services (AMS) with Azure Media Services Explorer (AMSE) tool.</span></span> <span data-ttu-id="cc0d8-111">Cet outil est uniquement compatible avec les PC Windows.</span><span class="sxs-lookup"><span data-stu-id="cc0d8-111">This tool only runs on Windows PC.</span></span> <span data-ttu-id="cc0d8-112">Si vous êtes sous Mac ou Linux, utilisez le portail Azure pour créer des [canaux](media-services-portal-creating-live-encoder-enabled-channel.md#create-a-channel) et des [programmes](media-services-portal-creating-live-encoder-enabled-channel.md).</span><span class="sxs-lookup"><span data-stu-id="cc0d8-112">If you are on Mac or Linux, use the Azure portal to create [channels](media-services-portal-creating-live-encoder-enabled-channel.md#create-a-channel) and [programs](media-services-portal-creating-live-encoder-enabled-channel.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cc0d8-113">Conditions préalables</span><span class="sxs-lookup"><span data-stu-id="cc0d8-113">Prerequisites</span></span>
* <span data-ttu-id="cc0d8-114">Suppose une connaissance pratique de l’utilisation de l’interface web Elemental Live pour créer des événements en direct.</span><span class="sxs-lookup"><span data-stu-id="cc0d8-114">Must have a working knowledge of using Elemental Live web interface to create live events.</span></span>
* [<span data-ttu-id="cc0d8-115">Créer un compte Azure Media Services</span><span class="sxs-lookup"><span data-stu-id="cc0d8-115">Create an Azure Media Services account</span></span>](media-services-portal-create-account.md)
* <span data-ttu-id="cc0d8-116">Vérifiez qu’un point de terminaison de streaming est en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="cc0d8-116">Ensure there is a Streaming Endpoint running.</span></span> <span data-ttu-id="cc0d8-117">Pour plus d’informations, consultez la rubrique [Gestion des points de terminaison de diffusion en continu dans un compte Media Services](media-services-portal-manage-streaming-endpoints.md).</span><span class="sxs-lookup"><span data-stu-id="cc0d8-117">For more information, see [Manage Streaming Endpoints in a Media Services Account](media-services-portal-manage-streaming-endpoints.md).</span></span>
* <span data-ttu-id="cc0d8-118">Installez la dernière version de l’outil [AMSE](https://github.com/Azure/Azure-Media-Services-Explorer) .</span><span class="sxs-lookup"><span data-stu-id="cc0d8-118">Install the latest version of the [AMSE](https://github.com/Azure/Azure-Media-Services-Explorer) tool.</span></span>
* <span data-ttu-id="cc0d8-119">Lancez l’outil et connectez-vous à votre compte AMS.</span><span class="sxs-lookup"><span data-stu-id="cc0d8-119">Launch the tool and connect to your AMS account.</span></span>

## <a name="tips"></a><span data-ttu-id="cc0d8-120">Conseils</span><span class="sxs-lookup"><span data-stu-id="cc0d8-120">Tips</span></span>
* <span data-ttu-id="cc0d8-121">Si possible, utilisez une connexion Internet câblée.</span><span class="sxs-lookup"><span data-stu-id="cc0d8-121">Whenever possible, use a hardwired internet connection.</span></span>
* <span data-ttu-id="cc0d8-122">Une bonne règle pour déterminer les besoins en bande passante consiste à doubler les débits binaires de diffusion en continu.</span><span class="sxs-lookup"><span data-stu-id="cc0d8-122">A good rule of thumb when determining bandwidth requirements is to double the streaming bitrates.</span></span> <span data-ttu-id="cc0d8-123">Bien qu’il ne s’agisse pas d’une obligation, cela permet de réduire l’impact de l’encombrement du réseau.</span><span class="sxs-lookup"><span data-stu-id="cc0d8-123">While this is not a mandatory requirement, it will help mitigate the impact of network congestion.</span></span>
* <span data-ttu-id="cc0d8-124">Lors de l’utilisation d’encodeurs logiciels, fermez tous les programmes inutiles.</span><span class="sxs-lookup"><span data-stu-id="cc0d8-124">When using software based encoders, close out any unnecessary programs.</span></span>

## <a name="elemental-live-with-rtp-ingest"></a><span data-ttu-id="cc0d8-125">Elemental Live avec réception RTP</span><span class="sxs-lookup"><span data-stu-id="cc0d8-125">Elemental Live with RTP ingest</span></span>
<span data-ttu-id="cc0d8-126">Cette section explique comment configurer l’encodeur Elemental Live qui envoie un flux live à débit binaire unique via RTP.</span><span class="sxs-lookup"><span data-stu-id="cc0d8-126">This section shows how to configure the Elemental Live encoder that sends a single bitrate live stream over RTP.</span></span>  <span data-ttu-id="cc0d8-127">Pour plus d’informations, consultez la rubrique [Flux MPEG-TS via RTP](media-services-manage-live-encoder-enabled-channels.md#channel).</span><span class="sxs-lookup"><span data-stu-id="cc0d8-127">For more information, see [MPEG-TS stream over RTP](media-services-manage-live-encoder-enabled-channels.md#channel).</span></span>

### <a name="create-a-channel"></a><span data-ttu-id="cc0d8-128">Créer un canal</span><span class="sxs-lookup"><span data-stu-id="cc0d8-128">Create a channel</span></span>

1. <span data-ttu-id="cc0d8-129">Dans l’outil AMSE, accédez à l’onglet **Live** , puis cliquez avec le bouton droit dans la zone des canaux.</span><span class="sxs-lookup"><span data-stu-id="cc0d8-129">In the AMSE tool, navigate to the **Live** tab, and right click within the channel area.</span></span> <span data-ttu-id="cc0d8-130">Dans le menu qui s’affiche, sélectionnez **Créer un canal...**</span><span class="sxs-lookup"><span data-stu-id="cc0d8-130">Select **Create channel…**</span></span> <span data-ttu-id="cc0d8-131">.</span><span class="sxs-lookup"><span data-stu-id="cc0d8-131">from the menu.</span></span>

    ![Elemental](./media/media-services-elemental-live-encoder/media-services-elemental1.png)

2. <span data-ttu-id="cc0d8-133">Spécifiez un nom de canal (le champ Description est facultatif).</span><span class="sxs-lookup"><span data-stu-id="cc0d8-133">Specify a channel name, the description field is optional.</span></span> <span data-ttu-id="cc0d8-134">Sous Paramètres du canal, sélectionnez **Standard** pour l’option Live Encoding, avec le protocole d’entrée défini sur **RTP (MPEG-TS)**.</span><span class="sxs-lookup"><span data-stu-id="cc0d8-134">Under Channel Settings, select **Standard** for the Live Encoding option, with the Input Protocol set to **RTP (MPEG-TS)**.</span></span> <span data-ttu-id="cc0d8-135">Vous pouvez laisser tous les autres paramètres inchangés.</span><span class="sxs-lookup"><span data-stu-id="cc0d8-135">You can leave all other settings as is.</span></span>

    <span data-ttu-id="cc0d8-136">Vérifiez que l’option **Démarrer maintenant le nouveau canal** est sélectionnée.</span><span class="sxs-lookup"><span data-stu-id="cc0d8-136">Make sure the **Start the new channel now** is selected.</span></span>

3. <span data-ttu-id="cc0d8-137">Cliquez sur **Créer un canal**.</span><span class="sxs-lookup"><span data-stu-id="cc0d8-137">Click **Create Channel**.</span></span>

   ![Elemental](./media/media-services-elemental-live-encoder/media-services-elemental12.png)

> [!NOTE]
> <span data-ttu-id="cc0d8-139">Le démarrage du canal peut prendre jusqu’à 20 minutes.</span><span class="sxs-lookup"><span data-stu-id="cc0d8-139">The channel can take as long as 20 minutes to start.</span></span>
>
>

<span data-ttu-id="cc0d8-140">Pendant le démarrage du canal, vous pouvez [configurer l’encodeur](media-services-configure-elemental-live-encoder.md#configure_elemental_rtp).</span><span class="sxs-lookup"><span data-stu-id="cc0d8-140">While the channel is starting you can [configure the encoder](media-services-configure-elemental-live-encoder.md#configure_elemental_rtp).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="cc0d8-141">Notez que la facturation commence dès que l’état du canal indique qu’il est prêt à être utilisé.</span><span class="sxs-lookup"><span data-stu-id="cc0d8-141">Note that billing starts as soon as Channel goes into a ready state.</span></span> <span data-ttu-id="cc0d8-142">Pour plus d’informations, consultez [États du canal](media-services-manage-live-encoder-enabled-channels.md#states).</span><span class="sxs-lookup"><span data-stu-id="cc0d8-142">For more information, see [Channel's states](media-services-manage-live-encoder-enabled-channels.md#states).</span></span>
>
>

### <span data-ttu-id="cc0d8-143"><a id=configure_elemental_rtp></a>Configurer l’encodeur Elemental Live</span><span class="sxs-lookup"><span data-stu-id="cc0d8-143"><a id=configure_elemental_rtp></a>Configure the Elemental Live encoder</span></span>
<span data-ttu-id="cc0d8-144">Dans ce didacticiel, les paramètres de sortie ci-dessous sont utilisés.</span><span class="sxs-lookup"><span data-stu-id="cc0d8-144">In this tutorial the following output settings are used.</span></span> <span data-ttu-id="cc0d8-145">Le reste de cette section décrit la procédure de configuration plus en détail.</span><span class="sxs-lookup"><span data-stu-id="cc0d8-145">The rest of this section describes configuration steps in more detail.</span></span>

<span data-ttu-id="cc0d8-146">**Vidéo**:</span><span class="sxs-lookup"><span data-stu-id="cc0d8-146">**Video**:</span></span>

* <span data-ttu-id="cc0d8-147">Codec : H.264</span><span class="sxs-lookup"><span data-stu-id="cc0d8-147">Codec: H.264</span></span>
* <span data-ttu-id="cc0d8-148">Profil : Élevé (niveau 4.0)</span><span class="sxs-lookup"><span data-stu-id="cc0d8-148">Profile: High (Level 4.0)</span></span>
* <span data-ttu-id="cc0d8-149">Débit binaire : 5 000 kbit/s</span><span class="sxs-lookup"><span data-stu-id="cc0d8-149">Bitrate: 5000 kbps</span></span>
* <span data-ttu-id="cc0d8-150">Image clé : 2 secondes (60 secondes)</span><span class="sxs-lookup"><span data-stu-id="cc0d8-150">Keyframe: 2 seconds (60 seconds)</span></span>
* <span data-ttu-id="cc0d8-151">Fréquence d’images : 30</span><span class="sxs-lookup"><span data-stu-id="cc0d8-151">Frame Rate: 30</span></span>

<span data-ttu-id="cc0d8-152">**Audio**:</span><span class="sxs-lookup"><span data-stu-id="cc0d8-152">**Audio**:</span></span>

* <span data-ttu-id="cc0d8-153">Codec : AAC (LC)</span><span class="sxs-lookup"><span data-stu-id="cc0d8-153">Codec: AAC (LC)</span></span>
* <span data-ttu-id="cc0d8-154">Débit binaire : 192 kbit/s</span><span class="sxs-lookup"><span data-stu-id="cc0d8-154">Bitrate: 192 kbps</span></span>
* <span data-ttu-id="cc0d8-155">Taux d’échantillonnage : 44,1 kHz</span><span class="sxs-lookup"><span data-stu-id="cc0d8-155">Sample Rate: 44.1 kHz</span></span>

#### <a name="configuration-steps"></a><span data-ttu-id="cc0d8-156">Configuration</span><span class="sxs-lookup"><span data-stu-id="cc0d8-156">Configuration steps</span></span>
1. <span data-ttu-id="cc0d8-157">Accédez à l’interface web **Elemental Live** et configurez l’encodeur pour la diffusion en continu **UDP/TS**.</span><span class="sxs-lookup"><span data-stu-id="cc0d8-157">Navigate to the **Elemental Live** web interface, and set up the encoder for **UDP/TS** streaming.</span></span>
2. <span data-ttu-id="cc0d8-158">Une fois qu’un nouvel événement a été créé, faites défiler l’écran jusqu’aux groupes de sortie et ajoutez le groupe de sortie **UDP/TS** .</span><span class="sxs-lookup"><span data-stu-id="cc0d8-158">Once a new event is created, scroll down to the output groups and add the **UDP/TS** output group.</span></span>
3. <span data-ttu-id="cc0d8-159">Créez une nouvelle sortie en sélectionnant **New Stream**, puis en cliquant sur **Add Output**.</span><span class="sxs-lookup"><span data-stu-id="cc0d8-159">Create a new output by selecting **New Stream** and then clicking **Add Output**.</span></span>  

    ![Elemental](./media/media-services-elemental-live-encoder/media-services-elemental13.png)

   > [!NOTE]
   > <span data-ttu-id="cc0d8-161">Il est recommandé que le code horaire de l’événement Elemental soit défini sur Horloge système pour aider l’encodeur à se reconnecter en cas d’échec d’un flux.</span><span class="sxs-lookup"><span data-stu-id="cc0d8-161">It is recommended that the Elemental event has the timecode set to "System Clock" to help the encoder reconnect in the case of a stream failure.</span></span>
   >
   >
4. <span data-ttu-id="cc0d8-162">Maintenant que la sortie a été créée, cliquez sur **Add Stream**.</span><span class="sxs-lookup"><span data-stu-id="cc0d8-162">Now that the Output has been created, click **Add Stream**.</span></span> <span data-ttu-id="cc0d8-163">Vous pouvez à présent configurer les paramètres de sortie.</span><span class="sxs-lookup"><span data-stu-id="cc0d8-163">The output settings can now be configured.</span></span>
5. <span data-ttu-id="cc0d8-164">Faites défiler l’écran jusqu’au flux « Stream 1 » qui vient d’être créé, cliquez sur l’onglet **Video** à gauche et développez la section de paramètres **Advanced**.</span><span class="sxs-lookup"><span data-stu-id="cc0d8-164">Scroll down to the "Stream 1" that was just created, click the **Video** tab on the left and expand the **Advanced** settings section.</span></span>

    ![Elemental](./media/media-services-elemental-live-encoder/media-services-elemental4.png)

    <span data-ttu-id="cc0d8-166">Même si Elemental Live offre un large éventail de possibilités de personnalisation, les paramètres suivants sont recommandés pour commencer la diffusion en continu vers AMS.</span><span class="sxs-lookup"><span data-stu-id="cc0d8-166">While Elemental Live has a wide range of available customizing, the following settings are recommended for getting started with streaming to AMS.</span></span>

   * <span data-ttu-id="cc0d8-167">Resolution : 1280 x 720</span><span class="sxs-lookup"><span data-stu-id="cc0d8-167">Resolution: 1280 x 720</span></span>
   * <span data-ttu-id="cc0d8-168">Framerate : 30</span><span class="sxs-lookup"><span data-stu-id="cc0d8-168">Framerate: 30</span></span>
   * <span data-ttu-id="cc0d8-169">GOP Size : 60 frames</span><span class="sxs-lookup"><span data-stu-id="cc0d8-169">GOP Size: 60 frames</span></span>
   * <span data-ttu-id="cc0d8-170">Interlace Mode : Progressive</span><span class="sxs-lookup"><span data-stu-id="cc0d8-170">Interlace Mode: Progressive</span></span>
   * <span data-ttu-id="cc0d8-171">Bitrate : 5000000 bit/s (cette valeur peut être ajustée en fonction des limitations du réseau)</span><span class="sxs-lookup"><span data-stu-id="cc0d8-171">Bitrate: 5000000 bit/s (This can be adjusted based on network limitations)</span></span>

    ![Elemental](./media/media-services-elemental-live-encoder/media-services-elemental5.png)

1. <span data-ttu-id="cc0d8-173">Obtenez l’URL d’entrée du canal.</span><span class="sxs-lookup"><span data-stu-id="cc0d8-173">Get the channel's input URL.</span></span>

    <span data-ttu-id="cc0d8-174">Revenez à l’outil AMSE et vérifiez l’état d’achèvement du canal.</span><span class="sxs-lookup"><span data-stu-id="cc0d8-174">Navigate back to the AMSE tool, and check on the channel completion status.</span></span> <span data-ttu-id="cc0d8-175">Une fois que l’état est passé de **Démarrage** à **En cours d’exécution**, vous pouvez obtenir l’URL d’entrée.</span><span class="sxs-lookup"><span data-stu-id="cc0d8-175">Once the State has changed from **Starting** to **Running**, you can get the input URL.</span></span>

    <span data-ttu-id="cc0d8-176">Une fois le canal en cours d’exécution, cliquez avec le bouton droit sur le nom du canal, déplacez le pointeur vers le bas pour le placer sur **Copier l’URL entrée dans le Presse-papiers**, puis sélectionnez **URL d’entrée principale**.</span><span class="sxs-lookup"><span data-stu-id="cc0d8-176">When the channel is running, right click the channel name, navigate down to hover over **Copy Input URL to clipboard** and then select **Primary Input  URL**.</span></span>  

    ![Elemental](./media/media-services-elemental-live-encoder/media-services-elemental6.png)
2. <span data-ttu-id="cc0d8-178">Collez ces informations dans le champ **Primary Destination** d’Elemental.</span><span class="sxs-lookup"><span data-stu-id="cc0d8-178">Paste this information in the **Primary Destination** field of the Elemental.</span></span> <span data-ttu-id="cc0d8-179">Tous les autres paramètres peuvent rester inchangés.</span><span class="sxs-lookup"><span data-stu-id="cc0d8-179">All other settings can remain the default.</span></span>

    ![Elemental](./media/media-services-elemental-live-encoder/media-services-elemental14.png)

    <span data-ttu-id="cc0d8-181">Pour bénéficier d’une redondance supplémentaire, répétez ces étapes avec l’URL d’entrée secondaire en créant un onglet « Output » distinct pour la diffusion en continu UDP/TS.</span><span class="sxs-lookup"><span data-stu-id="cc0d8-181">For extra redundancy, repeat these steps with the Secondary Input URL by creating a separate "Output" tab for UDP/TS Streaming.</span></span>
3. <span data-ttu-id="cc0d8-182">Cliquez sur **Create** (si un événement a été créé) ou **Update** (en cas de modification d’un événement existant), puis procédez au démarrage de l’encodeur.</span><span class="sxs-lookup"><span data-stu-id="cc0d8-182">Click **Create** (if a new event was created) or **Update** (if editing a pre-existing event) and then proceed to start the encoder.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="cc0d8-183">Avant de cliquer sur **Start** dans l’interface web Elemental Live, vous **devez** vérifier que le canal est prêt.</span><span class="sxs-lookup"><span data-stu-id="cc0d8-183">Before you click **Start** on the Elemental Live web interface, you **must** ensure that the Channel is ready.</span></span>
> <span data-ttu-id="cc0d8-184">Veillez également à ne pas laisser le canal à l’état d’exécution sans événement pendant plus de 15 minutes.</span><span class="sxs-lookup"><span data-stu-id="cc0d8-184">Also, make sure not to leave the Channel in a ready state without an event for longer than > 15 minutes.</span></span>
>
>

<span data-ttu-id="cc0d8-185">Une fois que le flux a été exécuté pendant 30 secondes, revenez à l’outil AMSE et testez la lecture.</span><span class="sxs-lookup"><span data-stu-id="cc0d8-185">After the stream has been running for 30 seconds, navigate back to the AMSE tool and test playback.</span></span>  

### <a name="test-playback"></a><span data-ttu-id="cc0d8-186">Tester la lecture</span><span class="sxs-lookup"><span data-stu-id="cc0d8-186">Test playback</span></span>

<span data-ttu-id="cc0d8-187">Accédez à l’outil AMSE et cliquez avec le bouton droit sur le canal à tester.</span><span class="sxs-lookup"><span data-stu-id="cc0d8-187">Navigate to the AMSE tool, and right click the channel to be tested.</span></span> <span data-ttu-id="cc0d8-188">Dans le menu, placez le pointeur sur **Lire l’aperçu** et sélectionnez **avec Azure Media Player**.</span><span class="sxs-lookup"><span data-stu-id="cc0d8-188">From the menu, hover over **Playback the Preview** and select **with Azure Media Player**.</span></span>  

    ![Elemental](./media/media-services-elemental-live-encoder/media-services-elemental8.png)

<span data-ttu-id="cc0d8-189">Si le flux s’affiche dans le lecteur, cela signifie que l’encodeur a été correctement configuré pour se connecter à AMS.</span><span class="sxs-lookup"><span data-stu-id="cc0d8-189">If the stream appears in the player, then the encoder has been properly configured to connect to AMS.</span></span>

<span data-ttu-id="cc0d8-190">Si vous recevez une erreur, vous devrez réinitialiser le canal et ajuster les paramètres de l’encodeur.</span><span class="sxs-lookup"><span data-stu-id="cc0d8-190">If an error is received, the channel will need to be reset and encoder settings adjusted.</span></span> <span data-ttu-id="cc0d8-191">Pour obtenir des instructions détaillées, reportez-vous à la rubrique consacrée à la [résolution des problèmes](media-services-troubleshooting-live-streaming.md) .</span><span class="sxs-lookup"><span data-stu-id="cc0d8-191">Please see the [troubleshooting](media-services-troubleshooting-live-streaming.md) topic for guidance.</span></span>   

### <a name="create-a-program"></a><span data-ttu-id="cc0d8-192">Créer un programme</span><span class="sxs-lookup"><span data-stu-id="cc0d8-192">Create a program</span></span>
1. <span data-ttu-id="cc0d8-193">Une fois que vous avez vérifié que la lecture fonctionne sur le canal, créez un programme.</span><span class="sxs-lookup"><span data-stu-id="cc0d8-193">Once channel playback is confirmed, create a program.</span></span> <span data-ttu-id="cc0d8-194">Sous l’onglet **Live** de l’outil AMSE, cliquez avec le bouton droit dans la zone des programmes et sélectionnez **Créer un programme**.</span><span class="sxs-lookup"><span data-stu-id="cc0d8-194">Under the **Live** tab in the AMSE tool, right click within the program area and select **Create New Program**.</span></span>  

    ![Elemental](./media/media-services-elemental-live-encoder/media-services-elemental9.png)
2. <span data-ttu-id="cc0d8-196">Nommez le programme et, si nécessaire, ajustez la **longueur de la fenêtre d’archive** (qui est de 4 heures par défaut).</span><span class="sxs-lookup"><span data-stu-id="cc0d8-196">Name the program and, if needed, adjust the **Archive Window Length** (which defaults to 4 hours).</span></span> <span data-ttu-id="cc0d8-197">Vous pouvez également spécifier un emplacement de stockage ou conserver la valeur par défaut.</span><span class="sxs-lookup"><span data-stu-id="cc0d8-197">You can also specify a storage location or leave as the default.</span></span>  
3. <span data-ttu-id="cc0d8-198">Cochez la case **Démarrer le programme maintenant** .</span><span class="sxs-lookup"><span data-stu-id="cc0d8-198">Check the **Start the Program now** box.</span></span>
4. <span data-ttu-id="cc0d8-199">Cliquez sur **Créer le programme**.</span><span class="sxs-lookup"><span data-stu-id="cc0d8-199">Click **Create Program**.</span></span>  

    >[!NOTE]
    > <span data-ttu-id="cc0d8-200">La création d’un programme prend moins de temps que la création d’un canal.</span><span class="sxs-lookup"><span data-stu-id="cc0d8-200">Program creation takes less time than channel creation.</span></span>   
      
5. <span data-ttu-id="cc0d8-201">Une fois le programme en cours d’exécution, vérifiez que la lecture fonctionne. Pour ce faire, cliquez avec le bouton droit sur le programme, placez le pointeur sur **Lire le(s) programme(s)**, puis sélectionnez **avec Azure Media Player**.</span><span class="sxs-lookup"><span data-stu-id="cc0d8-201">Once the program is running, confirm playback by right clicking the program and navigating to **Playback the program(s)** and then selecting **with Azure Media Player**.</span></span>  
6. <span data-ttu-id="cc0d8-202">Après confirmation, cliquez à nouveau avec le bouton droit sur le programme et sélectionnez **Copier l’URL de sortie dans le Presse-papiers** (ou obtenez cette information à l’aide de l’option **Informations et paramètres du programme** du menu).</span><span class="sxs-lookup"><span data-stu-id="cc0d8-202">Once confirmed, right click the program again and select **Copy the Output URL to Clipboard** (or retrieve this information from the **Program information and settings** option from the menu).</span></span>

<span data-ttu-id="cc0d8-203">Le flux est maintenant prêt à être incorporé dans un lecteur ou distribué à une audience pour un affichage en direct.</span><span class="sxs-lookup"><span data-stu-id="cc0d8-203">The stream is now ready to be embedded in a player, or distributed to an audience for live viewing.</span></span>  

## <a name="troubleshooting"></a><span data-ttu-id="cc0d8-204">résolution des problèmes</span><span class="sxs-lookup"><span data-stu-id="cc0d8-204">Troubleshooting</span></span>
<span data-ttu-id="cc0d8-205">Pour obtenir des instructions détaillées, reportez-vous à la rubrique consacrée à la [résolution des problèmes](media-services-troubleshooting-live-streaming.md) .</span><span class="sxs-lookup"><span data-stu-id="cc0d8-205">Please see the [troubleshooting](media-services-troubleshooting-live-streaming.md) topic for guidance.</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="cc0d8-206">Parcours d’apprentissage de Media Services</span><span class="sxs-lookup"><span data-stu-id="cc0d8-206">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="cc0d8-207">Fournir des commentaires</span><span class="sxs-lookup"><span data-stu-id="cc0d8-207">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
