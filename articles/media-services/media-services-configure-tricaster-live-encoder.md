---
title: "Configurer l’encodeur NewTek TriCaster pour envoyer un flux en direct à débit binaire unique | Microsoft Docs"
description: "Cette rubrique explique comment configurer l’encodeur en direct TriCaster afin d’envoyer un flux à débit binaire unique à des canaux AMS activés pour l’encodage en temps réel."
services: media-services
documentationcenter: 
author: cenkdin
manager: cfowler
editor: 
ms.assetid: 8973181a-3059-471a-a6bb-ccda7d3ff297
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: ne
ms.topic: article
ms.date: 01/05/2017
ms.author: juliako;cenkd;anilmur
ms.openlocfilehash: 42b012fb98bd0504c931ce391d63aecca8c3d311
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="use-the-newtek-tricaster-encoder-to-send-a-single-bitrate-live-stream"></a><span data-ttu-id="a1ef8-103">Utiliser l’encodeur NewTek TriCaster pour envoyer un flux en direct à débit binaire unique</span><span class="sxs-lookup"><span data-stu-id="a1ef8-103">Use the NewTek TriCaster encoder to send a single bitrate live stream</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="a1ef8-104">Tricaster</span><span class="sxs-lookup"><span data-stu-id="a1ef8-104">Tricaster</span></span>](media-services-configure-tricaster-live-encoder.md)
> * [<span data-ttu-id="a1ef8-105">Elemental Live</span><span class="sxs-lookup"><span data-stu-id="a1ef8-105">Elemental Live</span></span>](media-services-configure-elemental-live-encoder.md)
> * [<span data-ttu-id="a1ef8-106">Wirecast</span><span class="sxs-lookup"><span data-stu-id="a1ef8-106">Wirecast</span></span>](media-services-configure-wirecast-live-encoder.md)
> * [<span data-ttu-id="a1ef8-107">FMLE</span><span class="sxs-lookup"><span data-stu-id="a1ef8-107">FMLE</span></span>](media-services-configure-fmle-live-encoder.md)
>
>

<span data-ttu-id="a1ef8-108">Cette rubrique explique comment configurer l’encodeur en direct [NewTek TriCaster](http://newtek.com/products/tricaster-40.html) afin d’envoyer un flux à débit binaire unique à des canaux AMS activés pour l’encodage en temps réel.</span><span class="sxs-lookup"><span data-stu-id="a1ef8-108">This topic shows how to configure the [NewTek TriCaster](http://newtek.com/products/tricaster-40.html) live encoder to send a single bitrate stream to AMS channels that are enabled for live encoding.</span></span> <span data-ttu-id="a1ef8-109">Pour plus d’informations, consultez [Utilisation de canaux activés pour effectuer un encodage en temps réel avec Azure Media Services](media-services-manage-live-encoder-enabled-channels.md).</span><span class="sxs-lookup"><span data-stu-id="a1ef8-109">For more information, see [Working with Channels that are Enabled to Perform Live Encoding with Azure Media Services](media-services-manage-live-encoder-enabled-channels.md).</span></span>

<span data-ttu-id="a1ef8-110">Ce didacticiel montre comment gérer Azure Media Services (AMS) avec l’outil Azure Media Services Explorer (AMSE).</span><span class="sxs-lookup"><span data-stu-id="a1ef8-110">This tutorial shows how to manage Azure Media Services (AMS) with Azure Media Services Explorer (AMSE) tool.</span></span> <span data-ttu-id="a1ef8-111">Cet outil est uniquement compatible avec les PC Windows.</span><span class="sxs-lookup"><span data-stu-id="a1ef8-111">This tool only runs on Windows PC.</span></span> <span data-ttu-id="a1ef8-112">Si vous êtes sous Mac ou Linux, utilisez le portail Azure pour créer des [canaux](media-services-portal-creating-live-encoder-enabled-channel.md#create-a-channel) et des [programmes](media-services-portal-creating-live-encoder-enabled-channel.md).</span><span class="sxs-lookup"><span data-stu-id="a1ef8-112">If you are on Mac or Linux, use the Azure portal to create [channels](media-services-portal-creating-live-encoder-enabled-channel.md#create-a-channel) and [programs](media-services-portal-creating-live-encoder-enabled-channel.md).</span></span>

> [!NOTE]
> <span data-ttu-id="a1ef8-113">Pendant l’utilisation de Tricaster pour l’envoi dans un flux de contribution pour des canaux AMS activés pour l’encodage live, il peut y avoir des problèmes vidéo/audio dans votre événement en direct si vous utilisez certaines fonctionnalités de Tricaster, telles que le découpage rapide entre des flux ou le basculement de/vers les ardoises.</span><span class="sxs-lookup"><span data-stu-id="a1ef8-113">When using Tricaster for sending in a contribution feed to AMS channels that are enabled for live encoding, there can be video/audio glitches in your live event if you use certain features of Tricaster, such as rapid cutting between feeds, or switching to/from slates.</span></span> <span data-ttu-id="a1ef8-114">L’équipe AMS travaille à la résolution de ces problèmes. En attendant, il est déconseillé d’utiliser ces fonctionnalités.</span><span class="sxs-lookup"><span data-stu-id="a1ef8-114">The AMS team is working on fixing these issues, until then, it is not recommend to use these features.</span></span>
>
>

## <a name="prerequisites"></a><span data-ttu-id="a1ef8-115">Conditions préalables</span><span class="sxs-lookup"><span data-stu-id="a1ef8-115">Prerequisites</span></span>
* [<span data-ttu-id="a1ef8-116">Créer un compte Azure Media Services</span><span class="sxs-lookup"><span data-stu-id="a1ef8-116">Create an Azure Media Services account</span></span>](media-services-portal-create-account.md)
* <span data-ttu-id="a1ef8-117">Vérifiez qu’un point de terminaison de streaming est en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="a1ef8-117">Ensure there is a Streaming Endpoint running.</span></span> <span data-ttu-id="a1ef8-118">Pour plus d’informations, consultez [Gestion des points de terminaison de diffusion en continu dans un compte Media Services](media-services-portal-manage-streaming-endpoints.md)</span><span class="sxs-lookup"><span data-stu-id="a1ef8-118">For more information, see [Manage Streaming Endpoints in a Media Services Account](media-services-portal-manage-streaming-endpoints.md)</span></span>
* <span data-ttu-id="a1ef8-119">Installez la dernière version de l’outil [AMSE](https://github.com/Azure/Azure-Media-Services-Explorer) .</span><span class="sxs-lookup"><span data-stu-id="a1ef8-119">Install the latest version of the [AMSE](https://github.com/Azure/Azure-Media-Services-Explorer) tool.</span></span>
* <span data-ttu-id="a1ef8-120">Lancez l’outil et connectez-vous à votre compte AMS.</span><span class="sxs-lookup"><span data-stu-id="a1ef8-120">Launch the tool and connect to your AMS account.</span></span>

## <a name="tips"></a><span data-ttu-id="a1ef8-121">Conseils</span><span class="sxs-lookup"><span data-stu-id="a1ef8-121">Tips</span></span>
* <span data-ttu-id="a1ef8-122">Si possible, utilisez une connexion Internet câblée.</span><span class="sxs-lookup"><span data-stu-id="a1ef8-122">Whenever possible, use a hardwired internet connection.</span></span>
* <span data-ttu-id="a1ef8-123">Une bonne règle pour déterminer les besoins en bande passante consiste à doubler les débits binaires de diffusion en continu.</span><span class="sxs-lookup"><span data-stu-id="a1ef8-123">A good rule of thumb when determining bandwidth requirements is to double the streaming bitrates.</span></span> <span data-ttu-id="a1ef8-124">Bien qu’il ne s’agisse pas d’une obligation, cela permet de réduire l’impact de l’encombrement du réseau.</span><span class="sxs-lookup"><span data-stu-id="a1ef8-124">While this is not a mandatory requirement, it will help mitigate the impact of network congestion.</span></span>
* <span data-ttu-id="a1ef8-125">Lors de l’utilisation d’encodeurs logiciels, fermez tous les programmes inutiles.</span><span class="sxs-lookup"><span data-stu-id="a1ef8-125">When using software based encoders, close out any unnecessary programs.</span></span>

## <a name="create-a-channel"></a><span data-ttu-id="a1ef8-126">Créer un canal</span><span class="sxs-lookup"><span data-stu-id="a1ef8-126">Create a channel</span></span>
1. <span data-ttu-id="a1ef8-127">Dans l’outil AMSE, accédez à l’onglet **Live** , puis cliquez avec le bouton droit dans la zone des canaux.</span><span class="sxs-lookup"><span data-stu-id="a1ef8-127">In the AMSE tool, navigate to the **Live** tab, and right click within the channel area.</span></span> <span data-ttu-id="a1ef8-128">Dans le menu qui s’affiche, sélectionnez **Créer un canal...**</span><span class="sxs-lookup"><span data-stu-id="a1ef8-128">Select **Create channel…**</span></span> <span data-ttu-id="a1ef8-129">.</span><span class="sxs-lookup"><span data-stu-id="a1ef8-129">from the menu.</span></span>

    ![Tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster1.png)

2. <span data-ttu-id="a1ef8-131">Spécifiez un nom de canal (le champ Description est facultatif).</span><span class="sxs-lookup"><span data-stu-id="a1ef8-131">Specify a channel name, the description field is optional.</span></span> <span data-ttu-id="a1ef8-132">Sous Paramètres du canal, sélectionnez **Standard** pour l’option Live Encoding, avec le protocole d’entrée défini sur **RTPM**.</span><span class="sxs-lookup"><span data-stu-id="a1ef8-132">Under Channel Settings, select **Standard** for the Live Encoding option, with the Input Protocol set to **RTMP**.</span></span> <span data-ttu-id="a1ef8-133">Vous pouvez laisser tous les autres paramètres inchangés.</span><span class="sxs-lookup"><span data-stu-id="a1ef8-133">You can leave all other settings as is.</span></span>

    <span data-ttu-id="a1ef8-134">Vérifiez que l’option **Démarrer maintenant le nouveau canal** est sélectionnée.</span><span class="sxs-lookup"><span data-stu-id="a1ef8-134">Make sure the **Start the new channel now** is selected.</span></span>

3. <span data-ttu-id="a1ef8-135">Cliquez sur **Créer un canal**.</span><span class="sxs-lookup"><span data-stu-id="a1ef8-135">Click **Create Channel**.</span></span>

   ![Tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster2.png)

> [!NOTE]
> <span data-ttu-id="a1ef8-137">Le démarrage du canal peut prendre jusqu’à 20 minutes.</span><span class="sxs-lookup"><span data-stu-id="a1ef8-137">The channel can take as long as 20 minutes to start.</span></span>
>
>

<span data-ttu-id="a1ef8-138">Pendant le démarrage du canal, vous pouvez [configurer l’encodeur](media-services-configure-tricaster-live-encoder.md#configure_tricaster_rtmp).</span><span class="sxs-lookup"><span data-stu-id="a1ef8-138">While the channel is starting you can [configure the encoder](media-services-configure-tricaster-live-encoder.md#configure_tricaster_rtmp).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a1ef8-139">Notez que la facturation commence dès que l’état du canal indique qu’il est prêt à être utilisé.</span><span class="sxs-lookup"><span data-stu-id="a1ef8-139">Note that billing starts as soon as Channel goes into a ready state.</span></span> <span data-ttu-id="a1ef8-140">Pour plus d’informations, consultez [États du canal](media-services-manage-live-encoder-enabled-channels.md#states).</span><span class="sxs-lookup"><span data-stu-id="a1ef8-140">For more information, see [Channel's states](media-services-manage-live-encoder-enabled-channels.md#states).</span></span>
>
>

## <span data-ttu-id="a1ef8-141"><a id=configure_tricaster_rtmp></a>Configurer l’encodeur NewTek TriCaster</span><span class="sxs-lookup"><span data-stu-id="a1ef8-141"><a id=configure_tricaster_rtmp></a>Configure the NewTek TriCaster encoder</span></span>
<span data-ttu-id="a1ef8-142">Dans ce didacticiel, les paramètres de sortie ci-dessous sont utilisés.</span><span class="sxs-lookup"><span data-stu-id="a1ef8-142">In this tutorial the following output settings are used.</span></span> <span data-ttu-id="a1ef8-143">Le reste de cette section décrit la procédure de configuration plus en détail.</span><span class="sxs-lookup"><span data-stu-id="a1ef8-143">The rest of this section describes configuration steps in more detail.</span></span>

<span data-ttu-id="a1ef8-144">**Vidéo**:</span><span class="sxs-lookup"><span data-stu-id="a1ef8-144">**Video**:</span></span>

* <span data-ttu-id="a1ef8-145">Codec : H.264</span><span class="sxs-lookup"><span data-stu-id="a1ef8-145">Codec: H.264</span></span>
* <span data-ttu-id="a1ef8-146">Profil : Élevé (niveau 4.0)</span><span class="sxs-lookup"><span data-stu-id="a1ef8-146">Profile: High (Level 4.0)</span></span>
* <span data-ttu-id="a1ef8-147">Débit binaire : 5 000 kbit/s</span><span class="sxs-lookup"><span data-stu-id="a1ef8-147">Bitrate: 5000 kbps</span></span>
* <span data-ttu-id="a1ef8-148">Image clé : 2 secondes (60 secondes)</span><span class="sxs-lookup"><span data-stu-id="a1ef8-148">Keyframe: 2 seconds (60 seconds)</span></span>
* <span data-ttu-id="a1ef8-149">Fréquence d’images : 30</span><span class="sxs-lookup"><span data-stu-id="a1ef8-149">Frame Rate: 30</span></span>

<span data-ttu-id="a1ef8-150">**Audio**:</span><span class="sxs-lookup"><span data-stu-id="a1ef8-150">**Audio**:</span></span>

* <span data-ttu-id="a1ef8-151">Codec : AAC (LC)</span><span class="sxs-lookup"><span data-stu-id="a1ef8-151">Codec: AAC (LC)</span></span>
* <span data-ttu-id="a1ef8-152">Débit binaire : 192 kbit/s</span><span class="sxs-lookup"><span data-stu-id="a1ef8-152">Bitrate: 192 kbps</span></span>
* <span data-ttu-id="a1ef8-153">Taux d’échantillonnage : 44,1 kHz</span><span class="sxs-lookup"><span data-stu-id="a1ef8-153">Sample Rate: 44.1 kHz</span></span>

### <a name="configuration-steps"></a><span data-ttu-id="a1ef8-154">Configuration</span><span class="sxs-lookup"><span data-stu-id="a1ef8-154">Configuration steps</span></span>
1. <span data-ttu-id="a1ef8-155">Créez un projet **NewTek TriCaster** en fonction de la source d’entrée vidéo utilisée.</span><span class="sxs-lookup"><span data-stu-id="a1ef8-155">Create a new **NewTek TriCaster** project depending on what video input source is being used.</span></span>
2. <span data-ttu-id="a1ef8-156">Une fois dans ce projet, recherchez le bouton **Flux** , puis cliquez sur l’icône en forme d’engrenage pour accéder au menu de configuration du flux de données.</span><span class="sxs-lookup"><span data-stu-id="a1ef8-156">Once within that project, find the **Stream** button, and click the gear icon next to it to access the stream configuration menu.</span></span>

    ![Tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster3.png)
3. <span data-ttu-id="a1ef8-158">Une fois le menu ouvert, cliquez sur **Nouveau** sous le titre Connexion.</span><span class="sxs-lookup"><span data-stu-id="a1ef8-158">Once the menu has opened, click **New** under the Connection heading.</span></span> <span data-ttu-id="a1ef8-159">Lorsque vous êtes invité à saisir un type de connexion, sélectionnez **Adobe Flash**.</span><span class="sxs-lookup"><span data-stu-id="a1ef8-159">When prompted for the connection type, select **Adobe Flash**.</span></span>

    ![Tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster4.png)
4. <span data-ttu-id="a1ef8-161">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="a1ef8-161">Click **OK**.</span></span>
5. <span data-ttu-id="a1ef8-162">Vous pouvez à présent importer un profil FMLE en cliquant sur la flèche sous le menu déroulant **Profil Streaming** et en accédant à **Parcourir**.</span><span class="sxs-lookup"><span data-stu-id="a1ef8-162">An FMLE profile can now be imported by clicking the drop down arrow under **Streaming Profile** and navigating to **Browse**.</span></span>

    ![Tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster5.png)
6. <span data-ttu-id="a1ef8-164">Accédez à l’emplacement d’enregistrement de votre profil FMLE configuré.</span><span class="sxs-lookup"><span data-stu-id="a1ef8-164">Navigate to where the configured FMLE profile was saved.</span></span>
7. <span data-ttu-id="a1ef8-165">Sélectionnez-le, puis appuyez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="a1ef8-165">Select it, and press **OK**.</span></span>

    <span data-ttu-id="a1ef8-166">Lorsque le profil est téléchargé, passez à l’étape suivante.</span><span class="sxs-lookup"><span data-stu-id="a1ef8-166">Once the profile is uploaded, proceed to the next step.</span></span>
8. <span data-ttu-id="a1ef8-167">Récupérez l’URL d’entrée du canal pour l’affecter au **Point de terminaison RTMP**Tricaster.</span><span class="sxs-lookup"><span data-stu-id="a1ef8-167">Get the channel's input URL in order to assign it to the Tricaster **RTMP Endpoint**.</span></span>

    <span data-ttu-id="a1ef8-168">Revenez à l’outil AMSE et vérifiez l’état d’achèvement du canal.</span><span class="sxs-lookup"><span data-stu-id="a1ef8-168">Navigate back to the AMSE tool, and check on the channel completion status.</span></span> <span data-ttu-id="a1ef8-169">Une fois que l’état est passé de **Démarrage** à **En cours d’exécution**, vous pouvez obtenir l’URL d’entrée.</span><span class="sxs-lookup"><span data-stu-id="a1ef8-169">Once the State has changed from **Starting** to **Running**, you can get the input URL.</span></span>

    <span data-ttu-id="a1ef8-170">Une fois le canal en cours d’exécution, cliquez avec le bouton droit sur le nom du canal, déplacez le pointeur vers le bas pour le placer sur **Copier l’URL entrée dans le Presse-papiers**, puis sélectionnez **URL d’entrée principale**.</span><span class="sxs-lookup"><span data-stu-id="a1ef8-170">When the channel is running, right click the channel name, navigate down to hover over **Copy Input URL to clipboard** and then select **Primary Input  URL**.</span></span>  

    ![Tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster6.png)
9. <span data-ttu-id="a1ef8-172">Collez ces informations dans le champ **Emplacement** sous **Serveur Flash** dans le projet Tricaster.</span><span class="sxs-lookup"><span data-stu-id="a1ef8-172">Paste this information in the **Location** field under **Flash Server** within the Tricaster project.</span></span> <span data-ttu-id="a1ef8-173">Indiquez également un nom de flux dans le champ **ID de flux** .</span><span class="sxs-lookup"><span data-stu-id="a1ef8-173">Also assign a stream name in the **Stream ID** field.</span></span>

    <span data-ttu-id="a1ef8-174">Si des informations de flux de données ont été ajoutées au profil FMLE, vous pouvez également les importer dans cette section en cliquant sur **Importer les paramètres**, en accédant au profil FMLE enregistré et en cliquant sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="a1ef8-174">If stream information was added to the FMLE profile, it can also be imported to this section by clicking **Import Settings**, navigating to the saved FMLE profile and clicking **OK**.</span></span> <span data-ttu-id="a1ef8-175">Les champs Serveur Flash adéquats doivent être remplis par des informations de FMLE.</span><span class="sxs-lookup"><span data-stu-id="a1ef8-175">The relevant Flash Server fields should populate with the information from FMLE.</span></span>

    ![Tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster7.png)
10. <span data-ttu-id="a1ef8-177">Lorsque vous avez terminé, cliquez sur **OK** en bas de l’écran.</span><span class="sxs-lookup"><span data-stu-id="a1ef8-177">When finished, click **OK** at the bottom of the screen.</span></span> <span data-ttu-id="a1ef8-178">Lorsque les entrées audio et vidéo dans Tricaster sont prêtes, commencez le streaming vers AMS en cliquant sur le bouton **Flux** .</span><span class="sxs-lookup"><span data-stu-id="a1ef8-178">When video and audio inputs into the Tricaster are ready, begin streaming to AMS by clicking the **Stream** button.</span></span>

     ![Tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster11.png)

> [!IMPORTANT]
> <span data-ttu-id="a1ef8-180">Avant de cliquer sur **Flux**, vous **devez** vérifier que le canal est prêt.</span><span class="sxs-lookup"><span data-stu-id="a1ef8-180">Before you click **Stream**, you **must** ensure that the Channel is ready.</span></span>
> <span data-ttu-id="a1ef8-181">Veillez également à ne pas laisser le canal à l’état d’exécution sans un flux de contribution d’entrée pendant plus de 15 minutes.</span><span class="sxs-lookup"><span data-stu-id="a1ef8-181">Also, make sure not to leave the Channel in a ready state without an input contribution feed for longer than > 15 minutes.</span></span>
>
>

## <a name="test-playback"></a><span data-ttu-id="a1ef8-182">Tester la lecture</span><span class="sxs-lookup"><span data-stu-id="a1ef8-182">Test playback</span></span>
<span data-ttu-id="a1ef8-183">Accédez à l’outil AMSE et cliquez avec le bouton droit sur le canal à tester.</span><span class="sxs-lookup"><span data-stu-id="a1ef8-183">Navigate to the AMSE tool, and right click the channel to be tested.</span></span> <span data-ttu-id="a1ef8-184">Dans le menu, placez le pointeur sur **Lire l’aperçu** et sélectionnez **avec Azure Media Player**.</span><span class="sxs-lookup"><span data-stu-id="a1ef8-184">From the menu, hover over **Playback the Preview** and select **with Azure Media Player**.</span></span>  

    ![tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster8.png)

<span data-ttu-id="a1ef8-185">Si le flux s’affiche dans le lecteur, cela signifie que l’encodeur a été correctement configuré pour se connecter à AMS.</span><span class="sxs-lookup"><span data-stu-id="a1ef8-185">If the stream appears in the player, then the encoder has been properly configured to connect to AMS.</span></span>

<span data-ttu-id="a1ef8-186">Si vous recevez une erreur, vous devrez réinitialiser le canal et ajuster les paramètres de l’encodeur.</span><span class="sxs-lookup"><span data-stu-id="a1ef8-186">If an error is received, the channel will need to be reset and encoder settings adjusted.</span></span> <span data-ttu-id="a1ef8-187">Pour obtenir des instructions détaillées, reportez-vous à la rubrique consacrée à la [résolution des problèmes](media-services-troubleshooting-live-streaming.md) .</span><span class="sxs-lookup"><span data-stu-id="a1ef8-187">Please see the [troubleshooting](media-services-troubleshooting-live-streaming.md) topic for guidance.</span></span>  

## <a name="create-a-program"></a><span data-ttu-id="a1ef8-188">Créer un programme</span><span class="sxs-lookup"><span data-stu-id="a1ef8-188">Create a program</span></span>
1. <span data-ttu-id="a1ef8-189">Une fois que vous avez vérifié que la lecture fonctionne sur le canal, créez un programme.</span><span class="sxs-lookup"><span data-stu-id="a1ef8-189">Once channel playback is confirmed, create a program.</span></span> <span data-ttu-id="a1ef8-190">Sous l’onglet **Live** de l’outil AMSE, cliquez avec le bouton droit dans la zone des programmes et sélectionnez **Créer un programme**.</span><span class="sxs-lookup"><span data-stu-id="a1ef8-190">Under the **Live** tab in the AMSE tool, right click within the program area and select **Create New Program**.</span></span>  

    ![Tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster9.png)
2. <span data-ttu-id="a1ef8-192">Nommez le programme et, si nécessaire, ajustez la **longueur de la fenêtre d’archive** (qui est de 4 heures par défaut).</span><span class="sxs-lookup"><span data-stu-id="a1ef8-192">Name the program and, if needed, adjust the **Archive Window Length** (which defaults to 4 hours).</span></span> <span data-ttu-id="a1ef8-193">Vous pouvez également spécifier un emplacement de stockage ou conserver la valeur par défaut.</span><span class="sxs-lookup"><span data-stu-id="a1ef8-193">You can also specify a storage location or leave as the default.</span></span>  
3. <span data-ttu-id="a1ef8-194">Cochez la case **Démarrer le programme maintenant** .</span><span class="sxs-lookup"><span data-stu-id="a1ef8-194">Check the **Start the Program now** box.</span></span>
4. <span data-ttu-id="a1ef8-195">Cliquez sur **Créer le programme**.</span><span class="sxs-lookup"><span data-stu-id="a1ef8-195">Click **Create Program**.</span></span>  

    >[!NOTE]
    ><span data-ttu-id="a1ef8-196">La création d’un programme prend moins de temps que la création d’un canal.</span><span class="sxs-lookup"><span data-stu-id="a1ef8-196">Program creation takes less time than channel creation.</span></span>
        
5. <span data-ttu-id="a1ef8-197">Une fois le programme en cours d’exécution, vérifiez que la lecture fonctionne. Pour ce faire, cliquez avec le bouton droit sur le programme, placez le pointeur sur **Lire le(s) programme(s)**, puis sélectionnez **avec Azure Media Player**.</span><span class="sxs-lookup"><span data-stu-id="a1ef8-197">Once the program is running, confirm playback by right clicking the program and navigating to **Playback the program(s)** and then selecting **with Azure Media Player**.</span></span>  
6. <span data-ttu-id="a1ef8-198">Après confirmation, cliquez à nouveau avec le bouton droit sur le programme et sélectionnez **Copier l’URL de sortie dans le Presse-papiers** (ou obtenez cette information à l’aide de l’option **Informations et paramètres du programme** du menu).</span><span class="sxs-lookup"><span data-stu-id="a1ef8-198">Once confirmed, right click the program again and select **Copy the Output URL to Clipboard** (or retrieve this information from the **Program information and settings** option from the menu).</span></span>

<span data-ttu-id="a1ef8-199">Le flux est maintenant prêt à être incorporé dans un lecteur ou distribué à une audience pour un affichage en direct.</span><span class="sxs-lookup"><span data-stu-id="a1ef8-199">The stream is now ready to be embedded in a player, or distributed to an audience for live viewing.</span></span>  

## <a name="troubleshooting"></a><span data-ttu-id="a1ef8-200">résolution des problèmes</span><span class="sxs-lookup"><span data-stu-id="a1ef8-200">Troubleshooting</span></span>
<span data-ttu-id="a1ef8-201">Pour obtenir des instructions détaillées, reportez-vous à la rubrique consacrée à la [résolution des problèmes](media-services-troubleshooting-live-streaming.md) .</span><span class="sxs-lookup"><span data-stu-id="a1ef8-201">Please see the [troubleshooting](media-services-troubleshooting-live-streaming.md) topic for guidance.</span></span>

## <a name="next-step"></a><span data-ttu-id="a1ef8-202">Étape suivante</span><span class="sxs-lookup"><span data-stu-id="a1ef8-202">Next step</span></span>
<span data-ttu-id="a1ef8-203">Consultez les parcours d’apprentissage de Media Services.</span><span class="sxs-lookup"><span data-stu-id="a1ef8-203">Review Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="a1ef8-204">Fournir des commentaires</span><span class="sxs-lookup"><span data-stu-id="a1ef8-204">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
