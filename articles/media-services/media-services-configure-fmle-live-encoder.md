---
title: "Configurer l’encodeur FMLE pour envoyer un flux live à débit binaire unique | Microsoft Docs"
description: "Cette rubrique explique comment configurer l’encodeur Flash Media Live Encoder (FMLE) afin d’envoyer un flux à débit binaire unique à des canaux AMS activés pour l’encodage en temps réel."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 3113f333-517a-47a1-a1b3-57e200c6b2a2
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: ne
ms.topic: article
ms.date: 01/05/2017
ms.author: juliako;cenkdin;anilmur
ms.openlocfilehash: e831048f34ecf6e89595adc4bfd58b5977e04bdb
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="use-the-fmle-encoder-to-send-a-single-bitrate-live-stream"></a><span data-ttu-id="9bec6-103">Utiliser l’encodeur FMLE pour envoyer un flux en direct à débit binaire unique</span><span class="sxs-lookup"><span data-stu-id="9bec6-103">Use the FMLE encoder to send a single bitrate live stream</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="9bec6-104">FMLE</span><span class="sxs-lookup"><span data-stu-id="9bec6-104">FMLE</span></span>](media-services-configure-fmle-live-encoder.md)
> * [<span data-ttu-id="9bec6-105">Elemental Live</span><span class="sxs-lookup"><span data-stu-id="9bec6-105">Elemental Live</span></span>](media-services-configure-elemental-live-encoder.md)
> * [<span data-ttu-id="9bec6-106">Tricaster</span><span class="sxs-lookup"><span data-stu-id="9bec6-106">Tricaster</span></span>](media-services-configure-tricaster-live-encoder.md)
> * [<span data-ttu-id="9bec6-107">Wirecast</span><span class="sxs-lookup"><span data-stu-id="9bec6-107">Wirecast</span></span>](media-services-configure-wirecast-live-encoder.md)
>
>

<span data-ttu-id="9bec6-108">Cette rubrique explique comment configurer l’encodeur [Flash Media Live Encoder](http://www.adobe.com/products/flash-media-encoder.html) (FMLE) afin d’envoyer un flux à débit binaire unique à des canaux AMS activés pour l’encodage en temps réel.</span><span class="sxs-lookup"><span data-stu-id="9bec6-108">This topic shows how to configure the [Flash Media Live Encoder](http://www.adobe.com/products/flash-media-encoder.html) (FMLE) encoder to send a single bitrate stream to AMS channels that are enabled for live encoding.</span></span> <span data-ttu-id="9bec6-109">Pour plus d’informations, consultez [Utilisation de canaux activés pour effectuer un encodage en temps réel avec Azure Media Services](media-services-manage-live-encoder-enabled-channels.md).</span><span class="sxs-lookup"><span data-stu-id="9bec6-109">For more information, see [Working with Channels that are Enabled to Perform Live Encoding with Azure Media Services](media-services-manage-live-encoder-enabled-channels.md).</span></span>

<span data-ttu-id="9bec6-110">Ce didacticiel montre comment gérer Azure Media Services (AMS) avec l’outil Azure Media Services Explorer (AMSE).</span><span class="sxs-lookup"><span data-stu-id="9bec6-110">This tutorial shows how to manage Azure Media Services (AMS) with Azure Media Services Explorer (AMSE) tool.</span></span> <span data-ttu-id="9bec6-111">Cet outil est uniquement compatible avec les PC Windows.</span><span class="sxs-lookup"><span data-stu-id="9bec6-111">This tool only runs on Windows PC.</span></span> <span data-ttu-id="9bec6-112">Si vous êtes sous Mac ou Linux, utilisez le portail Azure pour créer des [canaux](media-services-portal-creating-live-encoder-enabled-channel.md#create-a-channel) et des [programmes](media-services-portal-creating-live-encoder-enabled-channel.md).</span><span class="sxs-lookup"><span data-stu-id="9bec6-112">If you are on Mac or Linux, use the Azure portal to create [channels](media-services-portal-creating-live-encoder-enabled-channel.md#create-a-channel) and [programs](media-services-portal-creating-live-encoder-enabled-channel.md).</span></span>

<span data-ttu-id="9bec6-113">Notez que ce didacticiel décrit l’utilisation de AAC.</span><span class="sxs-lookup"><span data-stu-id="9bec6-113">Note that this tutorial describes using AAC.</span></span> <span data-ttu-id="9bec6-114">Cependant, FMLE ne prend pas en charge AAC par défaut.</span><span class="sxs-lookup"><span data-stu-id="9bec6-114">However, FMLE doesn’t supports AAC by default.</span></span> <span data-ttu-id="9bec6-115">Vous devez acheter un plug-in pour l’encodage AAC, comme par exemple, le [plug-in AAC de MainConcept](http://www.mainconcept.com/products/plug-ins/plug-ins-for-adobe/aac-encoder-fmle.html)</span><span class="sxs-lookup"><span data-stu-id="9bec6-115">You would need to purchase a plugin for AAC encoding such as from MainConcept: [AAC plugin](http://www.mainconcept.com/products/plug-ins/plug-ins-for-adobe/aac-encoder-fmle.html)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9bec6-116">Conditions préalables</span><span class="sxs-lookup"><span data-stu-id="9bec6-116">Prerequisites</span></span>
* [<span data-ttu-id="9bec6-117">Créer un compte Azure Media Services</span><span class="sxs-lookup"><span data-stu-id="9bec6-117">Create an Azure Media Services account</span></span>](media-services-portal-create-account.md)
* <span data-ttu-id="9bec6-118">Vérifiez qu’un point de terminaison de streaming est en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="9bec6-118">Ensure there is a Streaming Endpoint running.</span></span> <span data-ttu-id="9bec6-119">Pour plus d’informations, consultez [Gestion des points de terminaison de diffusion en continu dans un compte Media Services](media-services-portal-manage-streaming-endpoints.md)</span><span class="sxs-lookup"><span data-stu-id="9bec6-119">For more information, see [Manage Streaming Endpoints in a Media Services Account](media-services-portal-manage-streaming-endpoints.md)</span></span>
* <span data-ttu-id="9bec6-120">Installez la dernière version de l’outil [AMSE](https://github.com/Azure/Azure-Media-Services-Explorer) .</span><span class="sxs-lookup"><span data-stu-id="9bec6-120">Install the latest version of the [AMSE](https://github.com/Azure/Azure-Media-Services-Explorer) tool.</span></span>
* <span data-ttu-id="9bec6-121">Lancez l’outil et connectez-vous à votre compte AMS.</span><span class="sxs-lookup"><span data-stu-id="9bec6-121">Launch the tool and connect to your AMS account.</span></span>

## <a name="tips"></a><span data-ttu-id="9bec6-122">Conseils</span><span class="sxs-lookup"><span data-stu-id="9bec6-122">Tips</span></span>
* <span data-ttu-id="9bec6-123">Si possible, utilisez une connexion Internet câblée.</span><span class="sxs-lookup"><span data-stu-id="9bec6-123">Whenever possible, use a hardwired internet connection.</span></span>
* <span data-ttu-id="9bec6-124">Une bonne règle pour déterminer les besoins en bande passante consiste à doubler les débits binaires de diffusion en continu.</span><span class="sxs-lookup"><span data-stu-id="9bec6-124">A good rule of thumb when determining bandwidth requirements is to double the streaming bitrates.</span></span> <span data-ttu-id="9bec6-125">Bien qu’il ne s’agisse pas d’une obligation, cela permet de réduire l’impact de l’encombrement du réseau.</span><span class="sxs-lookup"><span data-stu-id="9bec6-125">While this is not a mandatory requirement, it will help mitigate the impact of network congestion.</span></span>
* <span data-ttu-id="9bec6-126">Lors de l’utilisation d’encodeurs logiciels, fermez tous les programmes inutiles.</span><span class="sxs-lookup"><span data-stu-id="9bec6-126">When using software based encoders, close out any unnecessary programs.</span></span>

## <a name="create-a-channel"></a><span data-ttu-id="9bec6-127">Créer un canal</span><span class="sxs-lookup"><span data-stu-id="9bec6-127">Create a channel</span></span>
1. <span data-ttu-id="9bec6-128">Dans l’outil AMSE, accédez à l’onglet **Live** , puis cliquez avec le bouton droit dans la zone des canaux.</span><span class="sxs-lookup"><span data-stu-id="9bec6-128">In the AMSE tool, navigate to the **Live** tab, and right click within the channel area.</span></span> <span data-ttu-id="9bec6-129">Dans le menu qui s’affiche, sélectionnez **Créer un canal...**</span><span class="sxs-lookup"><span data-stu-id="9bec6-129">Select **Create channel…**</span></span> <span data-ttu-id="9bec6-130">.</span><span class="sxs-lookup"><span data-stu-id="9bec6-130">from the menu.</span></span>

    ![FMLE](./media/media-services-fmle-live-encoder/media-services-fmle1.png)

2. <span data-ttu-id="9bec6-132">Spécifiez un nom de canal (le champ Description est facultatif).</span><span class="sxs-lookup"><span data-stu-id="9bec6-132">Specify a channel name, the description field is optional.</span></span> <span data-ttu-id="9bec6-133">Sous Paramètres du canal, sélectionnez **Standard** pour l’option Live Encoding, avec le protocole d’entrée défini sur **RTPM**.</span><span class="sxs-lookup"><span data-stu-id="9bec6-133">Under Channel Settings, select **Standard** for the Live Encoding option, with the Input Protocol set to **RTMP**.</span></span> <span data-ttu-id="9bec6-134">Vous pouvez laisser tous les autres paramètres inchangés.</span><span class="sxs-lookup"><span data-stu-id="9bec6-134">You can leave all other settings as is.</span></span>

    <span data-ttu-id="9bec6-135">Vérifiez que l’option **Démarrer maintenant le nouveau canal** est sélectionnée.</span><span class="sxs-lookup"><span data-stu-id="9bec6-135">Make sure the **Start the new channel now** is selected.</span></span>

3. <span data-ttu-id="9bec6-136">Cliquez sur **Créer un canal**.</span><span class="sxs-lookup"><span data-stu-id="9bec6-136">Click **Create Channel**.</span></span>

   ![FMLE](./media/media-services-fmle-live-encoder/media-services-fmle2.png)

> [!NOTE]
> <span data-ttu-id="9bec6-138">Le démarrage du canal peut prendre jusqu’à 20 minutes.</span><span class="sxs-lookup"><span data-stu-id="9bec6-138">The channel can take as long as 20 minutes to start.</span></span>
>
>

<span data-ttu-id="9bec6-139">Pendant le démarrage du canal, vous pouvez [configurer l’encodeur](media-services-configure-fmle-live-encoder.md#configure_fmle_rtmp).</span><span class="sxs-lookup"><span data-stu-id="9bec6-139">While the channel is starting you can [configure the encoder](media-services-configure-fmle-live-encoder.md#configure_fmle_rtmp).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9bec6-140">Notez que la facturation commence dès que l’état du canal indique qu’il est prêt à être utilisé.</span><span class="sxs-lookup"><span data-stu-id="9bec6-140">Note that billing starts as soon as Channel goes into a ready state.</span></span> <span data-ttu-id="9bec6-141">Pour plus d’informations, consultez [États du canal](media-services-manage-live-encoder-enabled-channels.md#states).</span><span class="sxs-lookup"><span data-stu-id="9bec6-141">For more information, see [Channel's states](media-services-manage-live-encoder-enabled-channels.md#states).</span></span>
>
>

## <span data-ttu-id="9bec6-142"><a id=configure_fmle_rtmp></a>Configurer l’encodeur FMLE</span><span class="sxs-lookup"><span data-stu-id="9bec6-142"><a id=configure_fmle_rtmp></a>Configure the FMLE encoder</span></span>
<span data-ttu-id="9bec6-143">Dans ce didacticiel, les paramètres de sortie ci-dessous sont utilisés.</span><span class="sxs-lookup"><span data-stu-id="9bec6-143">In this tutorial the following output settings are used.</span></span> <span data-ttu-id="9bec6-144">Le reste de cette section décrit la procédure de configuration plus en détail.</span><span class="sxs-lookup"><span data-stu-id="9bec6-144">The rest of this section describes configuration steps in more detail.</span></span>

<span data-ttu-id="9bec6-145">**Vidéo**:</span><span class="sxs-lookup"><span data-stu-id="9bec6-145">**Video**:</span></span>

* <span data-ttu-id="9bec6-146">Codec : H.264</span><span class="sxs-lookup"><span data-stu-id="9bec6-146">Codec: H.264</span></span>
* <span data-ttu-id="9bec6-147">Profil : Élevé (niveau 4.0)</span><span class="sxs-lookup"><span data-stu-id="9bec6-147">Profile: High (Level 4.0)</span></span>
* <span data-ttu-id="9bec6-148">Débit binaire : 5 000 kbit/s</span><span class="sxs-lookup"><span data-stu-id="9bec6-148">Bitrate: 5000 kbps</span></span>
* <span data-ttu-id="9bec6-149">Image clé : 2 secondes (60 secondes)</span><span class="sxs-lookup"><span data-stu-id="9bec6-149">Keyframe: 2 seconds (60 seconds)</span></span>
* <span data-ttu-id="9bec6-150">Fréquence d’images : 30</span><span class="sxs-lookup"><span data-stu-id="9bec6-150">Frame Rate: 30</span></span>

<span data-ttu-id="9bec6-151">**Audio**:</span><span class="sxs-lookup"><span data-stu-id="9bec6-151">**Audio**:</span></span>

* <span data-ttu-id="9bec6-152">Codec : AAC (LC)</span><span class="sxs-lookup"><span data-stu-id="9bec6-152">Codec: AAC (LC)</span></span>
* <span data-ttu-id="9bec6-153">Débit binaire : 192 kbit/s</span><span class="sxs-lookup"><span data-stu-id="9bec6-153">Bitrate: 192 kbps</span></span>
* <span data-ttu-id="9bec6-154">Taux d’échantillonnage : 44,1 kHz</span><span class="sxs-lookup"><span data-stu-id="9bec6-154">Sample Rate: 44.1 kHz</span></span>

### <a name="configuration-steps"></a><span data-ttu-id="9bec6-155">Configuration</span><span class="sxs-lookup"><span data-stu-id="9bec6-155">Configuration steps</span></span>
1. <span data-ttu-id="9bec6-156">Accédez à l’interface de l’encodeur FMLE sur la machine en cours d’utilisation.</span><span class="sxs-lookup"><span data-stu-id="9bec6-156">Navigate to the Flash Media Live Encoder’s (FMLE) interface on the machine being used.</span></span>

    <span data-ttu-id="9bec6-157">L’interface correspond à une page principale de paramètres.</span><span class="sxs-lookup"><span data-stu-id="9bec6-157">The interface is one main page of settings.</span></span> <span data-ttu-id="9bec6-158">Veuillez prendre note des paramètres recommandés suivants pour utiliser le streaming à l’aide de FMLE.</span><span class="sxs-lookup"><span data-stu-id="9bec6-158">Please take note of the following recommended settings to get started with streaming using FMLE.</span></span>

   * <span data-ttu-id="9bec6-159">Format : Fréquence d’images H.264 : 30,00</span><span class="sxs-lookup"><span data-stu-id="9bec6-159">Format: H.264 Frame Rate: 30.00</span></span>
   * <span data-ttu-id="9bec6-160">Taille d’entrée : 1280 x 720</span><span class="sxs-lookup"><span data-stu-id="9bec6-160">Input Size: 1280 x 720</span></span>
   * <span data-ttu-id="9bec6-161">Débit binaire : 5000 Kbit/s (cette valeur peut être ajustée en fonction des limitations du réseau)</span><span class="sxs-lookup"><span data-stu-id="9bec6-161">Bit Rate: 5000 Kbps (Can be adjusted based on network limitations)</span></span>  

     ![FMLE](./media/media-services-fmle-live-encoder/media-services-fmle3.png)

     <span data-ttu-id="9bec6-163">Lors de l’utilisation de sources entrelacées, veuillez cocher l’option « Désentrelacement ».</span><span class="sxs-lookup"><span data-stu-id="9bec6-163">When using interlaced sources, please checkmark the “Deinterlace” option</span></span>
2. <span data-ttu-id="9bec6-164">Sélectionnez l’icône en forme de clé en regard de Format. Elle doit mener vers les paramètres supplémentaires suivants :</span><span class="sxs-lookup"><span data-stu-id="9bec6-164">Select the wrench icon next to Format, these additional settings should be:</span></span>

   * <span data-ttu-id="9bec6-165">Profil : Principal</span><span class="sxs-lookup"><span data-stu-id="9bec6-165">Profile: Main</span></span>
   * <span data-ttu-id="9bec6-166">Niveau : 4.0</span><span class="sxs-lookup"><span data-stu-id="9bec6-166">Level: 4.0</span></span>
   * <span data-ttu-id="9bec6-167">Fréquence d’image clé : 2 secondes</span><span class="sxs-lookup"><span data-stu-id="9bec6-167">Keyframe Frequency: 2 seconds</span></span>

     ![FMLE](./media/media-services-fmle-live-encoder/media-services-fmle4.png)
3. <span data-ttu-id="9bec6-169">Définissez le paramètre audio important suivant :</span><span class="sxs-lookup"><span data-stu-id="9bec6-169">Set the following important audio setting:</span></span>

   * <span data-ttu-id="9bec6-170">Format : AAC</span><span class="sxs-lookup"><span data-stu-id="9bec6-170">Format: AAC</span></span>
   * <span data-ttu-id="9bec6-171">Taux d’échantillonnage : 44100 kHz</span><span class="sxs-lookup"><span data-stu-id="9bec6-171">Sample Rate: 44100 Hz</span></span>
   * <span data-ttu-id="9bec6-172">Débit binaire : 192 kbit/s</span><span class="sxs-lookup"><span data-stu-id="9bec6-172">Bitrate: 192 Kbps</span></span>

     ![FMLE](./media/media-services-fmle-live-encoder/media-services-fmle5.png)
4. <span data-ttu-id="9bec6-174">Récupérez l’URL d’entrée du canal pour l’affecter au **Point de terminaison RTMP**FMLE.</span><span class="sxs-lookup"><span data-stu-id="9bec6-174">Get the channel's input URL in order to assign it to the FMLE's **RTMP Endpoint**.</span></span>

    <span data-ttu-id="9bec6-175">Revenez à l’outil AMSE et vérifiez l’état d’achèvement du canal.</span><span class="sxs-lookup"><span data-stu-id="9bec6-175">Navigate back to the AMSE tool, and check on the channel completion status.</span></span> <span data-ttu-id="9bec6-176">Une fois que l’état est passé de **Démarrage** à **En cours d’exécution**, vous pouvez obtenir l’URL d’entrée.</span><span class="sxs-lookup"><span data-stu-id="9bec6-176">Once the State has changed from **Starting** to **Running**, you can get the input URL.</span></span>

    <span data-ttu-id="9bec6-177">Une fois le canal en cours d’exécution, cliquez avec le bouton droit sur le nom du canal, déplacez le pointeur vers le bas pour le placer sur **Copier l’URL entrée dans le Presse-papiers**, puis sélectionnez **URL d’entrée principale**.</span><span class="sxs-lookup"><span data-stu-id="9bec6-177">When the channel is running, right click the channel name, navigate down to hover over **Copy Input URL to clipboard** and then select **Primary Input  URL**.</span></span>  

    ![fmle](./media/media-services-fmle-live-encoder/media-services-fmle6.png)
5. <span data-ttu-id="9bec6-179">Collez ces informations dans le champ **URL FMS** de la section de sortie et attribuez un nom de flux.</span><span class="sxs-lookup"><span data-stu-id="9bec6-179">Paste this information in the **FMS URL** field of the output section, and assign a stream name.</span></span>

    ![FMLE](./media/media-services-fmle-live-encoder/media-services-fmle7.png)

    <span data-ttu-id="9bec6-181">Pour une redondance supplémentaire, répétez ces étapes avec l’URL d’entrée secondaire.</span><span class="sxs-lookup"><span data-stu-id="9bec6-181">For extra redundancy, repeat these steps with the Secondary Input URL.</span></span>
6. <span data-ttu-id="9bec6-182">Sélectionnez **Connecter**.</span><span class="sxs-lookup"><span data-stu-id="9bec6-182">Select **Connect**.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9bec6-183">Avant de cliquer sur **Connecter**, vous **devez** vérifier que le canal est prêt.</span><span class="sxs-lookup"><span data-stu-id="9bec6-183">Before you click **Connect**, you **must** ensure that the Channel is ready.</span></span>
> <span data-ttu-id="9bec6-184">Veillez également à ne pas laisser le canal à l’état d’exécution sans un flux de contribution d’entrée pendant plus de 15 minutes.</span><span class="sxs-lookup"><span data-stu-id="9bec6-184">Also, make sure not to leave the Channel in a ready state without an input contribution feed for longer than > 15 minutes.</span></span>
>
>

## <a name="test-playback"></a><span data-ttu-id="9bec6-185">Tester la lecture</span><span class="sxs-lookup"><span data-stu-id="9bec6-185">Test playback</span></span>

<span data-ttu-id="9bec6-186">Accédez à l’outil AMSE et cliquez avec le bouton droit sur le canal à tester.</span><span class="sxs-lookup"><span data-stu-id="9bec6-186">Navigate to the AMSE tool, and right click the channel to be tested.</span></span> <span data-ttu-id="9bec6-187">Dans le menu, placez le pointeur sur **Lire l’aperçu** et sélectionnez **avec Azure Media Player**.</span><span class="sxs-lookup"><span data-stu-id="9bec6-187">From the menu, hover over **Playback the Preview** and select **with Azure Media Player**.</span></span>  

    ![fmle](./media/media-services-fmle-live-encoder/media-services-fmle8.png)

<span data-ttu-id="9bec6-188">Si le flux s’affiche dans le lecteur, cela signifie que l’encodeur a été correctement configuré pour se connecter à AMS.</span><span class="sxs-lookup"><span data-stu-id="9bec6-188">If the stream appears in the player, then the encoder has been properly configured to connect to AMS.</span></span>

<span data-ttu-id="9bec6-189">Si vous recevez une erreur, vous devrez réinitialiser le canal et ajuster les paramètres de l’encodeur.</span><span class="sxs-lookup"><span data-stu-id="9bec6-189">If an error is received, the channel will need to be reset and encoder settings adjusted.</span></span> <span data-ttu-id="9bec6-190">Pour obtenir des instructions détaillées, reportez-vous à la rubrique consacrée à la [résolution des problèmes](media-services-troubleshooting-live-streaming.md) .</span><span class="sxs-lookup"><span data-stu-id="9bec6-190">Please see the [troubleshooting](media-services-troubleshooting-live-streaming.md) topic for guidance.</span></span>  

## <a name="create-a-program"></a><span data-ttu-id="9bec6-191">Créer un programme</span><span class="sxs-lookup"><span data-stu-id="9bec6-191">Create a program</span></span>
1. <span data-ttu-id="9bec6-192">Une fois que vous avez vérifié que la lecture fonctionne sur le canal, créez un programme.</span><span class="sxs-lookup"><span data-stu-id="9bec6-192">Once channel playback is confirmed, create a program.</span></span> <span data-ttu-id="9bec6-193">Sous l’onglet **Live** de l’outil AMSE, cliquez avec le bouton droit dans la zone des programmes et sélectionnez **Créer un programme**.</span><span class="sxs-lookup"><span data-stu-id="9bec6-193">Under the **Live** tab in the AMSE tool, right click within the program area and select **Create New Program**.</span></span>  

    ![FMLE](./media/media-services-fmle-live-encoder/media-services-fmle9.png)
2. <span data-ttu-id="9bec6-195">Nommez le programme et, si nécessaire, ajustez la **longueur de la fenêtre d’archive** (qui est de 4 heures par défaut).</span><span class="sxs-lookup"><span data-stu-id="9bec6-195">Name the program and, if needed, adjust the **Archive Window Length** (which defaults to 4 hours).</span></span> <span data-ttu-id="9bec6-196">Vous pouvez également spécifier un emplacement de stockage ou conserver la valeur par défaut.</span><span class="sxs-lookup"><span data-stu-id="9bec6-196">You can also specify a storage location or leave as the default.</span></span>  
3. <span data-ttu-id="9bec6-197">Cochez la case **Démarrer le programme maintenant** .</span><span class="sxs-lookup"><span data-stu-id="9bec6-197">Check the **Start the Program now** box.</span></span>
4. <span data-ttu-id="9bec6-198">Cliquez sur **Créer le programme**.</span><span class="sxs-lookup"><span data-stu-id="9bec6-198">Click **Create Program**.</span></span>  

    >[!NOTE]
    ><span data-ttu-id="9bec6-199">La création d’un programme prend moins de temps que la création d’un canal.</span><span class="sxs-lookup"><span data-stu-id="9bec6-199">Program creation takes less time than channel creation.</span></span>
        
5. <span data-ttu-id="9bec6-200">Une fois le programme en cours d’exécution, vérifiez que la lecture fonctionne. Pour ce faire, cliquez avec le bouton droit sur le programme, placez le pointeur sur **Lire le(s) programme(s)**, puis sélectionnez **avec Azure Media Player**.</span><span class="sxs-lookup"><span data-stu-id="9bec6-200">Once the program is running, confirm playback by right clicking the program and navigating to **Playback the program(s)** and then selecting **with Azure Media Player**.</span></span>  
6. <span data-ttu-id="9bec6-201">Après confirmation, cliquez à nouveau avec le bouton droit sur le programme et sélectionnez **Copier l’URL de sortie dans le Presse-papiers** (ou obtenez cette information à l’aide de l’option **Informations et paramètres du programme** du menu).</span><span class="sxs-lookup"><span data-stu-id="9bec6-201">Once confirmed, right click the program again and select **Copy the Output URL to Clipboard** (or retrieve this information from the **Program information and settings** option from the menu).</span></span>

<span data-ttu-id="9bec6-202">Le flux est maintenant prêt à être incorporé dans un lecteur ou distribué à une audience pour un affichage en direct.</span><span class="sxs-lookup"><span data-stu-id="9bec6-202">The stream is now ready to be embedded in a player, or distributed to an audience for live viewing.</span></span>  

## <a name="troubleshooting"></a><span data-ttu-id="9bec6-203">résolution des problèmes</span><span class="sxs-lookup"><span data-stu-id="9bec6-203">Troubleshooting</span></span>
<span data-ttu-id="9bec6-204">Pour obtenir des instructions détaillées, reportez-vous à la rubrique consacrée à la [résolution des problèmes](media-services-troubleshooting-live-streaming.md) .</span><span class="sxs-lookup"><span data-stu-id="9bec6-204">Please see the [troubleshooting](media-services-troubleshooting-live-streaming.md) topic for guidance.</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="9bec6-205">Parcours d’apprentissage de Media Services</span><span class="sxs-lookup"><span data-stu-id="9bec6-205">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="9bec6-206">Fournir des commentaires</span><span class="sxs-lookup"><span data-stu-id="9bec6-206">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
