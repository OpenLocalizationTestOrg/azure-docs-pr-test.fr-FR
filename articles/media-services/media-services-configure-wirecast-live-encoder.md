---
title: "Configurer l’encodeur Telestream Wirecast pour envoyer un flux en direct à débit binaire unique | Microsoft Docs"
description: "Cette rubrique explique comment configurer l’encodeur en direct Wirecast afin d’envoyer un flux à débit binaire unique à des canaux AMS activés pour l’encodage en temps réel. "
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 0d2f1e81-51a6-4ca9-894a-6dfa51ce4c70
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: ne
ms.topic: article
ms.date: 01/05/2017
ms.author: juliako;cenkdin;anilmur
ms.openlocfilehash: c4df14f24650ce431dfb31cc774cab6d3cf3aef0
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="use-the-wirecast-encoder-to-send-a-single-bitrate-live-stream"></a><span data-ttu-id="995a1-103">Utiliser l’encodeur Wirecast pour envoyer un flux en direct à débit binaire unique</span><span class="sxs-lookup"><span data-stu-id="995a1-103">Use the Wirecast encoder to send a single bitrate live stream</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="995a1-104">Wirecast</span><span class="sxs-lookup"><span data-stu-id="995a1-104">Wirecast</span></span>](media-services-configure-wirecast-live-encoder.md)
> * [<span data-ttu-id="995a1-105">Elemental Live</span><span class="sxs-lookup"><span data-stu-id="995a1-105">Elemental Live</span></span>](media-services-configure-elemental-live-encoder.md)
> * [<span data-ttu-id="995a1-106">Tricaster</span><span class="sxs-lookup"><span data-stu-id="995a1-106">Tricaster</span></span>](media-services-configure-tricaster-live-encoder.md)
> * [<span data-ttu-id="995a1-107">FMLE</span><span class="sxs-lookup"><span data-stu-id="995a1-107">FMLE</span></span>](media-services-configure-fmle-live-encoder.md)
>
>

<span data-ttu-id="995a1-108">Cette rubrique explique comment configurer l’encodeur en direct [Telestream Wirecast](http://www.telestream.net/wirecast/overview.htm) afin d’envoyer un flux à débit binaire unique à des canaux AMS activés pour l’encodage en temps réel.</span><span class="sxs-lookup"><span data-stu-id="995a1-108">This topic shows how to configure the [Telestream Wirecast](http://www.telestream.net/wirecast/overview.htm) live encoder to send a single bitrate stream to AMS channels that are enabled for live encoding.</span></span>  <span data-ttu-id="995a1-109">Pour plus d’informations, consultez [Utilisation de canaux activés pour effectuer un encodage en temps réel avec Azure Media Services](media-services-manage-live-encoder-enabled-channels.md).</span><span class="sxs-lookup"><span data-stu-id="995a1-109">For more information, see [Working with Channels that are Enabled to Perform Live Encoding with Azure Media Services](media-services-manage-live-encoder-enabled-channels.md).</span></span>

<span data-ttu-id="995a1-110">Ce didacticiel montre comment gérer Azure Media Services (AMS) avec l’outil Azure Media Services Explorer (AMSE).</span><span class="sxs-lookup"><span data-stu-id="995a1-110">This tutorial shows how to manage Azure Media Services (AMS) with Azure Media Services Explorer (AMSE) tool.</span></span> <span data-ttu-id="995a1-111">Cet outil est uniquement compatible avec les PC Windows.</span><span class="sxs-lookup"><span data-stu-id="995a1-111">This tool only runs on Windows PC.</span></span> <span data-ttu-id="995a1-112">Si vous êtes sous Mac ou Linux, utilisez le portail Azure pour créer des [canaux](media-services-portal-creating-live-encoder-enabled-channel.md#create-a-channel) et des [programmes](media-services-portal-creating-live-encoder-enabled-channel.md).</span><span class="sxs-lookup"><span data-stu-id="995a1-112">If you are on Mac or Linux, use the Azure portal to create [channels](media-services-portal-creating-live-encoder-enabled-channel.md#create-a-channel) and [programs](media-services-portal-creating-live-encoder-enabled-channel.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="995a1-113">Conditions préalables</span><span class="sxs-lookup"><span data-stu-id="995a1-113">Prerequisites</span></span>
* [<span data-ttu-id="995a1-114">Créer un compte Azure Media Services</span><span class="sxs-lookup"><span data-stu-id="995a1-114">Create an Azure Media Services account</span></span>](media-services-portal-create-account.md)
* <span data-ttu-id="995a1-115">Vérifiez qu’un point de terminaison de streaming est en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="995a1-115">Ensure there is a Streaming Endpoint running.</span></span> <span data-ttu-id="995a1-116">Pour plus d’informations, consultez [Gestion des points de terminaison de diffusion en continu dans un compte Media Services](media-services-portal-manage-streaming-endpoints.md)</span><span class="sxs-lookup"><span data-stu-id="995a1-116">For more information, see [Manage Streaming Endpoints in a Media Services Account](media-services-portal-manage-streaming-endpoints.md)</span></span>
* <span data-ttu-id="995a1-117">Installez la dernière version de l’outil [AMSE](https://github.com/Azure/Azure-Media-Services-Explorer) .</span><span class="sxs-lookup"><span data-stu-id="995a1-117">Install the latest version of the [AMSE](https://github.com/Azure/Azure-Media-Services-Explorer) tool.</span></span>
* <span data-ttu-id="995a1-118">Lancez l’outil et connectez-vous à votre compte AMS.</span><span class="sxs-lookup"><span data-stu-id="995a1-118">Launch the tool and connect to your AMS account.</span></span>

## <a name="tips"></a><span data-ttu-id="995a1-119">Conseils</span><span class="sxs-lookup"><span data-stu-id="995a1-119">Tips</span></span>
* <span data-ttu-id="995a1-120">Si possible, utilisez une connexion Internet câblée.</span><span class="sxs-lookup"><span data-stu-id="995a1-120">Whenever possible, use a hardwired internet connection.</span></span>
* <span data-ttu-id="995a1-121">Une bonne règle pour déterminer les besoins en bande passante consiste à doubler les débits binaires de diffusion en continu.</span><span class="sxs-lookup"><span data-stu-id="995a1-121">A good rule of thumb when determining bandwidth requirements is to double the streaming bitrates.</span></span> <span data-ttu-id="995a1-122">Bien qu’il ne s’agisse pas d’une obligation, cela permet de réduire l’impact de l’encombrement du réseau.</span><span class="sxs-lookup"><span data-stu-id="995a1-122">While this is not a mandatory requirement, it will help mitigate the impact of network congestion.</span></span>
* <span data-ttu-id="995a1-123">Lors de l’utilisation d’encodeurs logiciels, fermez tous les programmes inutiles.</span><span class="sxs-lookup"><span data-stu-id="995a1-123">When using software based encoders, close out any unnecessary programs.</span></span>

## <a name="create-a-channel"></a><span data-ttu-id="995a1-124">Créer un canal</span><span class="sxs-lookup"><span data-stu-id="995a1-124">Create a channel</span></span>
1. <span data-ttu-id="995a1-125">Dans l’outil AMSE, accédez à l’onglet **Live** , puis cliquez avec le bouton droit dans la zone des canaux.</span><span class="sxs-lookup"><span data-stu-id="995a1-125">In the AMSE tool, navigate to the **Live** tab, and right click within the channel area.</span></span> <span data-ttu-id="995a1-126">Dans le menu qui s’affiche, sélectionnez **Créer un canal...**</span><span class="sxs-lookup"><span data-stu-id="995a1-126">Select **Create channel…**</span></span> <span data-ttu-id="995a1-127">.</span><span class="sxs-lookup"><span data-stu-id="995a1-127">from the menu.</span></span>

    ![Wirecast](./media/media-services-wirecast-live-encoder/media-services-wirecast1.png)

2. <span data-ttu-id="995a1-129">Spécifiez un nom de canal (le champ Description est facultatif).</span><span class="sxs-lookup"><span data-stu-id="995a1-129">Specify a channel name, the description field is optional.</span></span> <span data-ttu-id="995a1-130">Sous Paramètres du canal, sélectionnez **Standard** pour l’option Live Encoding, avec le protocole d’entrée défini sur **RTPM**.</span><span class="sxs-lookup"><span data-stu-id="995a1-130">Under Channel Settings, select **Standard** for the Live Encoding option, with the Input Protocol set to **RTMP**.</span></span> <span data-ttu-id="995a1-131">Vous pouvez laisser tous les autres paramètres inchangés.</span><span class="sxs-lookup"><span data-stu-id="995a1-131">You can leave all other settings as is.</span></span>

    <span data-ttu-id="995a1-132">Vérifiez que l’option **Démarrer maintenant le nouveau canal** est sélectionnée.</span><span class="sxs-lookup"><span data-stu-id="995a1-132">Make sure the **Start the new channel now** is selected.</span></span>

3. <span data-ttu-id="995a1-133">Cliquez sur **Créer un canal**.</span><span class="sxs-lookup"><span data-stu-id="995a1-133">Click **Create Channel**.</span></span>

   ![Wirecast](./media/media-services-wirecast-live-encoder/media-services-wirecast2.png)

> [!NOTE]
> <span data-ttu-id="995a1-135">Le démarrage du canal peut prendre jusqu’à 20 minutes.</span><span class="sxs-lookup"><span data-stu-id="995a1-135">The channel can take as long as 20 minutes to start.</span></span>
>
>

<span data-ttu-id="995a1-136">Pendant le démarrage du canal, vous pouvez [configurer l’encodeur](media-services-configure-wirecast-live-encoder.md#configure_wirecast_rtmp).</span><span class="sxs-lookup"><span data-stu-id="995a1-136">While the channel is starting you can [configure the encoder](media-services-configure-wirecast-live-encoder.md#configure_wirecast_rtmp).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="995a1-137">Notez que la facturation commence dès que l’état du canal indique qu’il est prêt à être utilisé.</span><span class="sxs-lookup"><span data-stu-id="995a1-137">Note that billing starts as soon as Channel goes into a ready state.</span></span> <span data-ttu-id="995a1-138">Pour plus d’informations, consultez [États du canal](media-services-manage-live-encoder-enabled-channels.md#states).</span><span class="sxs-lookup"><span data-stu-id="995a1-138">For more information, see [Channel's states](media-services-manage-live-encoder-enabled-channels.md#states).</span></span>
>
>

## <span data-ttu-id="995a1-139"><a id=configure_wirecast_rtmp></a>Configurer l’encodeur Telestream Wirecast</span><span class="sxs-lookup"><span data-stu-id="995a1-139"><a id=configure_wirecast_rtmp></a>Configure the Telestream Wirecast encoder</span></span>
<span data-ttu-id="995a1-140">Dans ce didacticiel, les paramètres de sortie ci-dessous sont utilisés.</span><span class="sxs-lookup"><span data-stu-id="995a1-140">In this tutorial the following output settings are used.</span></span> <span data-ttu-id="995a1-141">Le reste de cette section décrit la procédure de configuration plus en détail.</span><span class="sxs-lookup"><span data-stu-id="995a1-141">The rest of this section describes configuration steps in more detail.</span></span>

<span data-ttu-id="995a1-142">**Vidéo**:</span><span class="sxs-lookup"><span data-stu-id="995a1-142">**Video**:</span></span>

* <span data-ttu-id="995a1-143">Codec : H.264</span><span class="sxs-lookup"><span data-stu-id="995a1-143">Codec: H.264</span></span>
* <span data-ttu-id="995a1-144">Profil : Élevé (niveau 4.0)</span><span class="sxs-lookup"><span data-stu-id="995a1-144">Profile: High (Level 4.0)</span></span>
* <span data-ttu-id="995a1-145">Débit binaire : 5 000 kbit/s</span><span class="sxs-lookup"><span data-stu-id="995a1-145">Bitrate: 5000 kbps</span></span>
* <span data-ttu-id="995a1-146">Image clé : 2 secondes (60 secondes)</span><span class="sxs-lookup"><span data-stu-id="995a1-146">Keyframe: 2 seconds (60 seconds)</span></span>
* <span data-ttu-id="995a1-147">Fréquence d’images : 30</span><span class="sxs-lookup"><span data-stu-id="995a1-147">Frame Rate: 30</span></span>

<span data-ttu-id="995a1-148">**Audio**:</span><span class="sxs-lookup"><span data-stu-id="995a1-148">**Audio**:</span></span>

* <span data-ttu-id="995a1-149">Codec : AAC (LC)</span><span class="sxs-lookup"><span data-stu-id="995a1-149">Codec: AAC (LC)</span></span>
* <span data-ttu-id="995a1-150">Débit binaire : 192 kbit/s</span><span class="sxs-lookup"><span data-stu-id="995a1-150">Bitrate: 192 kbps</span></span>
* <span data-ttu-id="995a1-151">Taux d’échantillonnage : 44,1 kHz</span><span class="sxs-lookup"><span data-stu-id="995a1-151">Sample Rate: 44.1 kHz</span></span>

### <a name="configuration-steps"></a><span data-ttu-id="995a1-152">Configuration</span><span class="sxs-lookup"><span data-stu-id="995a1-152">Configuration steps</span></span>
1. <span data-ttu-id="995a1-153">Ouvrez l’application Telestream Wirecast sur votre ordinateur et configurez le streaming RTMP.</span><span class="sxs-lookup"><span data-stu-id="995a1-153">Open the Telestream Wirecast application on the machine being used, and set up for RTMP streaming.</span></span>
2. <span data-ttu-id="995a1-154">Configurez la sortie en accédant à l’onglet **Sortie** et en sélectionnant **Paramètres de sortie...**.</span><span class="sxs-lookup"><span data-stu-id="995a1-154">Configure the output by navigating to the **Output** tab and selecting **Output Settings…**.</span></span>

    <span data-ttu-id="995a1-155">Vérifiez que le champ **Destination de sortie** est défini sur **Serveur RTMP**.</span><span class="sxs-lookup"><span data-stu-id="995a1-155">Make sure the **Output Destination** is set to **RTMP Server**.</span></span>
3. <span data-ttu-id="995a1-156">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="995a1-156">Click **OK**.</span></span>
4. <span data-ttu-id="995a1-157">Sur la page de paramètres, définissez le champ **Destination** sur **Azure Media Services**.</span><span class="sxs-lookup"><span data-stu-id="995a1-157">On the settings page, set the **Destination** field to be **Azure Media Services**.</span></span>

    <span data-ttu-id="995a1-158">Le profil d’encodage est prédéfini sur **Azure H.264 720 p 16:9 (1280 x 720)**.</span><span class="sxs-lookup"><span data-stu-id="995a1-158">The Encoding profile is pre-selected to **Azure H.264 720p 16:9 (1280x720)**.</span></span> <span data-ttu-id="995a1-159">Pour personnaliser ces paramètres, sélectionnez l’icône en forme d’engrenage à droite de la liste déroulante, puis sélectionnez **Nouvelle prédéfinition**.</span><span class="sxs-lookup"><span data-stu-id="995a1-159">To customize these settings, select the gear icon to the right of the drop down, and then choose **New Preset**.</span></span>

    ![Wirecast](./media/media-services-wirecast-live-encoder/media-services-wirecast3.png)
5. <span data-ttu-id="995a1-161">Configurez les présélections de l’encodeur.</span><span class="sxs-lookup"><span data-stu-id="995a1-161">Configure encoder presets.</span></span>

    <span data-ttu-id="995a1-162">Nommez la présélection et vérifiez les paramètres recommandés suivants :</span><span class="sxs-lookup"><span data-stu-id="995a1-162">Name the preset, and check for the following recommended settings:</span></span>

    <span data-ttu-id="995a1-163">**Vidéo**</span><span class="sxs-lookup"><span data-stu-id="995a1-163">**Video**</span></span>

   * <span data-ttu-id="995a1-164">Encodeur : MainConcept H.264</span><span class="sxs-lookup"><span data-stu-id="995a1-164">Encoder: MainConcept H.264</span></span>
   * <span data-ttu-id="995a1-165">Images par seconde : 30</span><span class="sxs-lookup"><span data-stu-id="995a1-165">Frames per Second: 30</span></span>
   * <span data-ttu-id="995a1-166">Débit binaire moyen : 5 000 Kbit/s (cette valeur peut être ajustée en fonction des limitations du réseau)</span><span class="sxs-lookup"><span data-stu-id="995a1-166">Average bit rate: 5000 kbits/sec (Can be adjusted based on network limitations)</span></span>
   * <span data-ttu-id="995a1-167">Profil : Principal</span><span class="sxs-lookup"><span data-stu-id="995a1-167">Profile: Main</span></span>
   * <span data-ttu-id="995a1-168">Trame-clé toutes les : 60 images</span><span class="sxs-lookup"><span data-stu-id="995a1-168">Key frame every: 60 frames</span></span>

    <span data-ttu-id="995a1-169">**Audio**</span><span class="sxs-lookup"><span data-stu-id="995a1-169">**Audio**</span></span>

   * <span data-ttu-id="995a1-170">Vitesse de transmission cible : 192 kbit/s</span><span class="sxs-lookup"><span data-stu-id="995a1-170">Target bit rate: 192 kbits/sec</span></span>
   * <span data-ttu-id="995a1-171">Taux d’échantillonnage : 44 100 kHz</span><span class="sxs-lookup"><span data-stu-id="995a1-171">Sample Rate: 44.100 kHz</span></span>

     ![Wirecast](./media/media-services-wirecast-live-encoder/media-services-wirecast4.png)
6. <span data-ttu-id="995a1-173">Appuyez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="995a1-173">Press **Save**.</span></span>

    <span data-ttu-id="995a1-174">Vous pouvez maintenant sélectionner le profil créé dans le champ Encodage.</span><span class="sxs-lookup"><span data-stu-id="995a1-174">The Encoding field now has the newly created profile available for selection.</span></span>

    <span data-ttu-id="995a1-175">Assurez-vous que ce nouveau profil est sélectionné.</span><span class="sxs-lookup"><span data-stu-id="995a1-175">Make sure the new profile is selected.</span></span>
7. <span data-ttu-id="995a1-176">Récupérez l’URL d’entrée du canal pour l’affecter au **Point de terminaison RTMP**Wirecast.</span><span class="sxs-lookup"><span data-stu-id="995a1-176">Get the channel's input URL in order to assign it to the Wirecast **RTMP Endpoint**.</span></span>

    <span data-ttu-id="995a1-177">Revenez à l’outil AMSE et vérifiez l’état d’achèvement du canal.</span><span class="sxs-lookup"><span data-stu-id="995a1-177">Navigate back to the AMSE tool, and check on the channel completion status.</span></span> <span data-ttu-id="995a1-178">Une fois que l’état est passé de **Démarrage** à **En cours d’exécution**, vous pouvez obtenir l’URL d’entrée.</span><span class="sxs-lookup"><span data-stu-id="995a1-178">Once the State has changed from **Starting** to **Running**, you can get the input URL.</span></span>

    <span data-ttu-id="995a1-179">Une fois le canal en cours d’exécution, cliquez avec le bouton droit sur le nom du canal, déplacez le pointeur vers le bas pour le placer sur **Copier l’URL entrée dans le Presse-papiers**, puis sélectionnez **URL d’entrée principale**.</span><span class="sxs-lookup"><span data-stu-id="995a1-179">When the channel is running, right click the channel name, navigate down to hover over **Copy Input URL to clipboard** and then select **Primary Input  URL**.</span></span>  

    ![Wirecast](./media/media-services-wirecast-live-encoder/media-services-wirecast6.png)
8. <span data-ttu-id="995a1-181">Dans la fenêtre **Paramètres de sortie** de Wirecast, collez ces informations dans le champ **Adresse** de la section de sortie et indiquez un nom de flux.</span><span class="sxs-lookup"><span data-stu-id="995a1-181">In the Wirecast **Output Settings** window, paste this information in the **Address** field of the output section, and assign a stream name.</span></span>

    ![Wirecast](./media/media-services-wirecast-live-encoder/media-services-wirecast5.png)

1. <span data-ttu-id="995a1-183">Sélectionnez **OK**.</span><span class="sxs-lookup"><span data-stu-id="995a1-183">Select **OK**.</span></span>
2. <span data-ttu-id="995a1-184">Sur l’écran principal de **Wirecast**, vérifiez que les sources d’entrée audio et vidéo sont prêtes, puis appuyez sur **Flux** dans le coin supérieur gauche.</span><span class="sxs-lookup"><span data-stu-id="995a1-184">On the main **Wirecast** screen, confirm input sources for video and audio are ready and then hit **Stream** in the top left hand corner.</span></span>

   ![Wirecast](./media/media-services-wirecast-live-encoder/media-services-wirecast7.png)

> [!IMPORTANT]
> <span data-ttu-id="995a1-186">Avant de cliquer sur **Flux**, vous **devez** vérifier que le canal est prêt.</span><span class="sxs-lookup"><span data-stu-id="995a1-186">Before you click **Stream**, you **must** ensure that the Channel is ready.</span></span>
> <span data-ttu-id="995a1-187">Veillez également à ne pas laisser le canal à l’état d’exécution sans un flux de contribution d’entrée pendant plus de 15 minutes.</span><span class="sxs-lookup"><span data-stu-id="995a1-187">Also, make sure not to leave the Channel in a ready state without an input contribution feed for longer than > 15 minutes.</span></span>
>
>

## <a name="test-playback"></a><span data-ttu-id="995a1-188">Tester la lecture</span><span class="sxs-lookup"><span data-stu-id="995a1-188">Test playback</span></span>

<span data-ttu-id="995a1-189">Accédez à l’outil AMSE et cliquez avec le bouton droit sur le canal à tester.</span><span class="sxs-lookup"><span data-stu-id="995a1-189">Navigate to the AMSE tool, and right click the channel to be tested.</span></span> <span data-ttu-id="995a1-190">Dans le menu, placez le pointeur sur **Lire l’aperçu** et sélectionnez **avec Azure Media Player**.</span><span class="sxs-lookup"><span data-stu-id="995a1-190">From the menu, hover over **Playback the Preview** and select **with Azure Media Player**.</span></span>  

    ![wirecast](./media/media-services-wirecast-live-encoder/media-services-wirecast8.png)

<span data-ttu-id="995a1-191">Si le flux s’affiche dans le lecteur, cela signifie que l’encodeur a été correctement configuré pour se connecter à AMS.</span><span class="sxs-lookup"><span data-stu-id="995a1-191">If the stream appears in the player, then the encoder has been properly configured to connect to AMS.</span></span>

<span data-ttu-id="995a1-192">Si vous recevez une erreur, vous devrez réinitialiser le canal et ajuster les paramètres de l’encodeur.</span><span class="sxs-lookup"><span data-stu-id="995a1-192">If an error is received, the channel will need to be reset and encoder settings adjusted.</span></span> <span data-ttu-id="995a1-193">Pour obtenir des instructions détaillées, reportez-vous à la rubrique consacrée à la [résolution des problèmes](media-services-troubleshooting-live-streaming.md) .</span><span class="sxs-lookup"><span data-stu-id="995a1-193">Please see the [troubleshooting](media-services-troubleshooting-live-streaming.md) topic for guidance.</span></span>  

## <a name="create-a-program"></a><span data-ttu-id="995a1-194">Créer un programme</span><span class="sxs-lookup"><span data-stu-id="995a1-194">Create a program</span></span>
1. <span data-ttu-id="995a1-195">Une fois que vous avez vérifié que la lecture fonctionne sur le canal, créez un programme.</span><span class="sxs-lookup"><span data-stu-id="995a1-195">Once channel playback is confirmed, create a program.</span></span> <span data-ttu-id="995a1-196">Sous l’onglet **Live** de l’outil AMSE, cliquez avec le bouton droit dans la zone des programmes et sélectionnez **Créer un programme**.</span><span class="sxs-lookup"><span data-stu-id="995a1-196">Under the **Live** tab in the AMSE tool, right click within the program area and select **Create New Program**.</span></span>  

    ![Wirecast](./media/media-services-wirecast-live-encoder/media-services-wirecast9.png)
2. <span data-ttu-id="995a1-198">Nommez le programme et, si nécessaire, ajustez la **longueur de la fenêtre d’archive** (qui est de 4 heures par défaut).</span><span class="sxs-lookup"><span data-stu-id="995a1-198">Name the program and, if needed, adjust the **Archive Window Length** (which defaults to 4 hours).</span></span> <span data-ttu-id="995a1-199">Vous pouvez également spécifier un emplacement de stockage ou conserver la valeur par défaut.</span><span class="sxs-lookup"><span data-stu-id="995a1-199">You can also specify a storage location or leave as the default.</span></span>  
3. <span data-ttu-id="995a1-200">Cochez la case **Démarrer le programme maintenant** .</span><span class="sxs-lookup"><span data-stu-id="995a1-200">Check the **Start the Program now** box.</span></span>
4. <span data-ttu-id="995a1-201">Cliquez sur **Créer le programme**.</span><span class="sxs-lookup"><span data-stu-id="995a1-201">Click **Create Program**.</span></span>  

   >[!NOTE]
   ><span data-ttu-id="995a1-202">La création d’un programme prend moins de temps que la création d’un canal.</span><span class="sxs-lookup"><span data-stu-id="995a1-202">Program creation takes less time than channel creation.</span></span>
       
5. <span data-ttu-id="995a1-203">Une fois le programme en cours d’exécution, vérifiez que la lecture fonctionne. Pour ce faire, cliquez avec le bouton droit sur le programme, placez le pointeur sur **Lire le(s) programme(s)**, puis sélectionnez **avec Azure Media Player**.</span><span class="sxs-lookup"><span data-stu-id="995a1-203">Once the program is running, confirm playback by right clicking the program and navigating to **Playback the program(s)** and then selecting **with Azure Media Player**.</span></span>  
6. <span data-ttu-id="995a1-204">Après confirmation, cliquez à nouveau avec le bouton droit sur le programme et sélectionnez **Copier l’URL de sortie dans le Presse-papiers** (ou obtenez cette information à l’aide de l’option **Informations et paramètres du programme** du menu).</span><span class="sxs-lookup"><span data-stu-id="995a1-204">Once confirmed, right click the program again and select **Copy the Output URL to Clipboard** (or retrieve this information from the **Program information and settings** option from the menu).</span></span>

<span data-ttu-id="995a1-205">Le flux est maintenant prêt à être incorporé dans un lecteur ou distribué à une audience pour un affichage en direct.</span><span class="sxs-lookup"><span data-stu-id="995a1-205">The stream is now ready to be embedded in a player, or distributed to an audience for live viewing.</span></span>  

## <a name="troubleshooting"></a><span data-ttu-id="995a1-206">résolution des problèmes</span><span class="sxs-lookup"><span data-stu-id="995a1-206">Troubleshooting</span></span>
<span data-ttu-id="995a1-207">Pour obtenir des instructions détaillées, reportez-vous à la rubrique consacrée à la [résolution des problèmes](media-services-troubleshooting-live-streaming.md) .</span><span class="sxs-lookup"><span data-stu-id="995a1-207">Please see the [troubleshooting](media-services-troubleshooting-live-streaming.md) topic for guidance.</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="995a1-208">Parcours d’apprentissage de Media Services</span><span class="sxs-lookup"><span data-stu-id="995a1-208">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="995a1-209">Fournir des commentaires</span><span class="sxs-lookup"><span data-stu-id="995a1-209">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
