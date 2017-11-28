---
title: "aaaConfigure hello toosend d’encodeur Telestream Wirecast un flux à débit binaire unique en continu | Documents Microsoft"
description: "Cette rubrique montre comment tooconfigure hello Wirecast live encodeur toosend un canaux tooAMS de flux à débit binaire unique qui est activés pour l’encodage live. "
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
ms.openlocfilehash: e373f6c08232c652e65db584ded409c405d8cffe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-wirecast-encoder-toosend-a-single-bitrate-live-stream"></a><span data-ttu-id="21d4c-103">Utilisez hello Wirecast encodeur toosend un flux à débit binaire unique en continu.</span><span class="sxs-lookup"><span data-stu-id="21d4c-103">Use hello Wirecast encoder toosend a single bitrate live stream</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="21d4c-104">Wirecast</span><span class="sxs-lookup"><span data-stu-id="21d4c-104">Wirecast</span></span>](media-services-configure-wirecast-live-encoder.md)
> * [<span data-ttu-id="21d4c-105">Elemental Live</span><span class="sxs-lookup"><span data-stu-id="21d4c-105">Elemental Live</span></span>](media-services-configure-elemental-live-encoder.md)
> * [<span data-ttu-id="21d4c-106">Tricaster</span><span class="sxs-lookup"><span data-stu-id="21d4c-106">Tricaster</span></span>](media-services-configure-tricaster-live-encoder.md)
> * [<span data-ttu-id="21d4c-107">FMLE</span><span class="sxs-lookup"><span data-stu-id="21d4c-107">FMLE</span></span>](media-services-configure-fmle-live-encoder.md)
>
>

<span data-ttu-id="21d4c-108">Cette rubrique montre comment tooconfigure hello [Telestream Wirecast](http://www.telestream.net/wirecast/overview.htm) live encodeur toosend un canaux tooAMS de flux à débit binaire unique qui est activés pour l’encodage live.</span><span class="sxs-lookup"><span data-stu-id="21d4c-108">This topic shows how tooconfigure hello [Telestream Wirecast](http://www.telestream.net/wirecast/overview.htm) live encoder toosend a single bitrate stream tooAMS channels that are enabled for live encoding.</span></span>  <span data-ttu-id="21d4c-109">Pour plus d’informations, consultez [utilisation de canaux est à activé tooPerform Live encodage avec Azure Media Services](media-services-manage-live-encoder-enabled-channels.md).</span><span class="sxs-lookup"><span data-stu-id="21d4c-109">For more information, see [Working with Channels that are Enabled tooPerform Live Encoding with Azure Media Services](media-services-manage-live-encoder-enabled-channels.md).</span></span>

<span data-ttu-id="21d4c-110">Ce didacticiel montre comment toomanage Azure Media Services (AMS) avec l’outil d’Azure Media Services Explorer (AMSE).</span><span class="sxs-lookup"><span data-stu-id="21d4c-110">This tutorial shows how toomanage Azure Media Services (AMS) with Azure Media Services Explorer (AMSE) tool.</span></span> <span data-ttu-id="21d4c-111">Cet outil est uniquement compatible avec les PC Windows.</span><span class="sxs-lookup"><span data-stu-id="21d4c-111">This tool only runs on Windows PC.</span></span> <span data-ttu-id="21d4c-112">Si vous êtes sur le Mac ou Linux, utilisez hello toocreate portail Azure [canaux](media-services-portal-creating-live-encoder-enabled-channel.md#create-a-channel) et [programmes](media-services-portal-creating-live-encoder-enabled-channel.md).</span><span class="sxs-lookup"><span data-stu-id="21d4c-112">If you are on Mac or Linux, use hello Azure portal toocreate [channels](media-services-portal-creating-live-encoder-enabled-channel.md#create-a-channel) and [programs](media-services-portal-creating-live-encoder-enabled-channel.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="21d4c-113">Composants requis</span><span class="sxs-lookup"><span data-stu-id="21d4c-113">Prerequisites</span></span>
* [<span data-ttu-id="21d4c-114">Créer un compte Azure Media Services</span><span class="sxs-lookup"><span data-stu-id="21d4c-114">Create an Azure Media Services account</span></span>](media-services-portal-create-account.md)
* <span data-ttu-id="21d4c-115">Vérifiez qu’un point de terminaison de streaming est en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="21d4c-115">Ensure there is a Streaming Endpoint running.</span></span> <span data-ttu-id="21d4c-116">Pour plus d’informations, consultez [Gestion des points de terminaison de diffusion en continu dans un compte Media Services](media-services-portal-manage-streaming-endpoints.md)</span><span class="sxs-lookup"><span data-stu-id="21d4c-116">For more information, see [Manage Streaming Endpoints in a Media Services Account](media-services-portal-manage-streaming-endpoints.md)</span></span>
* <span data-ttu-id="21d4c-117">Installer la version la plus récente de hello hello [AMSE](https://github.com/Azure/Azure-Media-Services-Explorer) outil.</span><span class="sxs-lookup"><span data-stu-id="21d4c-117">Install hello latest version of hello [AMSE](https://github.com/Azure/Azure-Media-Services-Explorer) tool.</span></span>
* <span data-ttu-id="21d4c-118">Lancer l’outil de hello et tooyour AMS compte de connexion.</span><span class="sxs-lookup"><span data-stu-id="21d4c-118">Launch hello tool and connect tooyour AMS account.</span></span>

## <a name="tips"></a><span data-ttu-id="21d4c-119">Conseils</span><span class="sxs-lookup"><span data-stu-id="21d4c-119">Tips</span></span>
* <span data-ttu-id="21d4c-120">Si possible, utilisez une connexion Internet câblée.</span><span class="sxs-lookup"><span data-stu-id="21d4c-120">Whenever possible, use a hardwired internet connection.</span></span>
* <span data-ttu-id="21d4c-121">Une règle empirique lors de la détermination de la bande passante est hello toodouble débits binaires de diffusion en continu.</span><span class="sxs-lookup"><span data-stu-id="21d4c-121">A good rule of thumb when determining bandwidth requirements is toodouble hello streaming bitrates.</span></span> <span data-ttu-id="21d4c-122">Alors que cela n’est pas obligatoire, il vous aide à atténuer l’impact hello de congestion du réseau.</span><span class="sxs-lookup"><span data-stu-id="21d4c-122">While this is not a mandatory requirement, it will help mitigate hello impact of network congestion.</span></span>
* <span data-ttu-id="21d4c-123">Lors de l’utilisation d’encodeurs logiciels, fermez tous les programmes inutiles.</span><span class="sxs-lookup"><span data-stu-id="21d4c-123">When using software based encoders, close out any unnecessary programs.</span></span>

## <a name="create-a-channel"></a><span data-ttu-id="21d4c-124">Créer un canal</span><span class="sxs-lookup"><span data-stu-id="21d4c-124">Create a channel</span></span>
1. <span data-ttu-id="21d4c-125">Dans l’outil AMSE hello, accédez à toohello **Live** onglet et cliquez avec le bouton droit dans la zone de canal hello.</span><span class="sxs-lookup"><span data-stu-id="21d4c-125">In hello AMSE tool, navigate toohello **Live** tab, and right click within hello channel area.</span></span> <span data-ttu-id="21d4c-126">Dans le menu qui s’affiche, sélectionnez **Créer un canal...**</span><span class="sxs-lookup"><span data-stu-id="21d4c-126">Select **Create channel…**</span></span> <span data-ttu-id="21d4c-127">à partir du menu de hello.</span><span class="sxs-lookup"><span data-stu-id="21d4c-127">from hello menu.</span></span>

    ![Wirecast](./media/media-services-wirecast-live-encoder/media-services-wirecast1.png)

2. <span data-ttu-id="21d4c-129">Spécifiez un nom de canal, champ de description hello est facultatif.</span><span class="sxs-lookup"><span data-stu-id="21d4c-129">Specify a channel name, hello description field is optional.</span></span> <span data-ttu-id="21d4c-130">Sous paramètres de canal, sélectionnez **Standard** pour hello option d’encodage Live, avec hello entrée protocole défini trop**RTMP**.</span><span class="sxs-lookup"><span data-stu-id="21d4c-130">Under Channel Settings, select **Standard** for hello Live Encoding option, with hello Input Protocol set too**RTMP**.</span></span> <span data-ttu-id="21d4c-131">Vous pouvez laisser tous les autres paramètres inchangés.</span><span class="sxs-lookup"><span data-stu-id="21d4c-131">You can leave all other settings as is.</span></span>

    <span data-ttu-id="21d4c-132">Vérifiez que hello **début hello nouveau canal maintenant** est sélectionnée.</span><span class="sxs-lookup"><span data-stu-id="21d4c-132">Make sure hello **Start hello new channel now** is selected.</span></span>

3. <span data-ttu-id="21d4c-133">Cliquez sur **Créer un canal**.</span><span class="sxs-lookup"><span data-stu-id="21d4c-133">Click **Create Channel**.</span></span>

   ![Wirecast](./media/media-services-wirecast-live-encoder/media-services-wirecast2.png)

> [!NOTE]
> <span data-ttu-id="21d4c-135">canal de Hello peut prendre jusqu'à 20 minutes toostart.</span><span class="sxs-lookup"><span data-stu-id="21d4c-135">hello channel can take as long as 20 minutes toostart.</span></span>
>
>

<span data-ttu-id="21d4c-136">Pendant le démarrage du canal de hello, vous pouvez [configurer l’encodeur de hello](media-services-configure-wirecast-live-encoder.md#configure_wirecast_rtmp).</span><span class="sxs-lookup"><span data-stu-id="21d4c-136">While hello channel is starting you can [configure hello encoder](media-services-configure-wirecast-live-encoder.md#configure_wirecast_rtmp).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="21d4c-137">Notez que la facturation commence dès que l’état du canal indique qu’il est prêt à être utilisé.</span><span class="sxs-lookup"><span data-stu-id="21d4c-137">Note that billing starts as soon as Channel goes into a ready state.</span></span> <span data-ttu-id="21d4c-138">Pour plus d’informations, consultez [États du canal](media-services-manage-live-encoder-enabled-channels.md#states).</span><span class="sxs-lookup"><span data-stu-id="21d4c-138">For more information, see [Channel's states](media-services-manage-live-encoder-enabled-channels.md#states).</span></span>
>
>

## <span data-ttu-id="21d4c-139"><a id=configure_wirecast_rtmp></a>Configurer hello encodeur Telestream Wirecast</span><span class="sxs-lookup"><span data-stu-id="21d4c-139"><a id=configure_wirecast_rtmp></a>Configure hello Telestream Wirecast encoder</span></span>
<span data-ttu-id="21d4c-140">Dans ce didacticiel hello des paramètres de sortie suivants sont utilisés.</span><span class="sxs-lookup"><span data-stu-id="21d4c-140">In this tutorial hello following output settings are used.</span></span> <span data-ttu-id="21d4c-141">Hello le reste de cette section décrit les étapes de configuration plus en détail.</span><span class="sxs-lookup"><span data-stu-id="21d4c-141">hello rest of this section describes configuration steps in more detail.</span></span>

<span data-ttu-id="21d4c-142">**Vidéo**:</span><span class="sxs-lookup"><span data-stu-id="21d4c-142">**Video**:</span></span>

* <span data-ttu-id="21d4c-143">Codec : H.264</span><span class="sxs-lookup"><span data-stu-id="21d4c-143">Codec: H.264</span></span>
* <span data-ttu-id="21d4c-144">Profil : Élevé (niveau 4.0)</span><span class="sxs-lookup"><span data-stu-id="21d4c-144">Profile: High (Level 4.0)</span></span>
* <span data-ttu-id="21d4c-145">Débit binaire : 5 000 kbit/s</span><span class="sxs-lookup"><span data-stu-id="21d4c-145">Bitrate: 5000 kbps</span></span>
* <span data-ttu-id="21d4c-146">Image clé : 2 secondes (60 secondes)</span><span class="sxs-lookup"><span data-stu-id="21d4c-146">Keyframe: 2 seconds (60 seconds)</span></span>
* <span data-ttu-id="21d4c-147">Fréquence d’images : 30</span><span class="sxs-lookup"><span data-stu-id="21d4c-147">Frame Rate: 30</span></span>

<span data-ttu-id="21d4c-148">**Audio**:</span><span class="sxs-lookup"><span data-stu-id="21d4c-148">**Audio**:</span></span>

* <span data-ttu-id="21d4c-149">Codec : AAC (LC)</span><span class="sxs-lookup"><span data-stu-id="21d4c-149">Codec: AAC (LC)</span></span>
* <span data-ttu-id="21d4c-150">Débit binaire : 192 kbit/s</span><span class="sxs-lookup"><span data-stu-id="21d4c-150">Bitrate: 192 kbps</span></span>
* <span data-ttu-id="21d4c-151">Taux d’échantillonnage : 44,1 kHz</span><span class="sxs-lookup"><span data-stu-id="21d4c-151">Sample Rate: 44.1 kHz</span></span>

### <a name="configuration-steps"></a><span data-ttu-id="21d4c-152">Configuration</span><span class="sxs-lookup"><span data-stu-id="21d4c-152">Configuration steps</span></span>
1. <span data-ttu-id="21d4c-153">Ouvrez l’application de Telestream Wirecast de hello sur la machine hello utilisé et configuré pour la diffusion en continu du contenu RTMP.</span><span class="sxs-lookup"><span data-stu-id="21d4c-153">Open hello Telestream Wirecast application on hello machine being used, and set up for RTMP streaming.</span></span>
2. <span data-ttu-id="21d4c-154">Configurer la sortie de hello en naviguant toohello **sortie** onglet et en sélectionnant **les paramètres de sortie...** .</span><span class="sxs-lookup"><span data-stu-id="21d4c-154">Configure hello output by navigating toohello **Output** tab and selecting **Output Settings…**.</span></span>

    <span data-ttu-id="21d4c-155">Vérifiez que hello **Destination de sortie** est défini trop**serveur RTMP**.</span><span class="sxs-lookup"><span data-stu-id="21d4c-155">Make sure hello **Output Destination** is set too**RTMP Server**.</span></span>
3. <span data-ttu-id="21d4c-156">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="21d4c-156">Click **OK**.</span></span>
4. <span data-ttu-id="21d4c-157">Sur la page de paramètres hello, définissez hello **Destination** champ toobe **Azure Media Services**.</span><span class="sxs-lookup"><span data-stu-id="21d4c-157">On hello settings page, set hello **Destination** field toobe **Azure Media Services**.</span></span>

    <span data-ttu-id="21d4c-158">Hello profil d’encodage est présélectionnée trop**Azure H.264 720 p 16:9 (1280 x 720)**.</span><span class="sxs-lookup"><span data-stu-id="21d4c-158">hello Encoding profile is pre-selected too**Azure H.264 720p 16:9 (1280x720)**.</span></span> <span data-ttu-id="21d4c-159">toocustomize ces paramètres, sélectionnez hello ENGRENAGE icône toohello à droite de hello liste déroulante, puis choisissez **prédéfini nouvelle**.</span><span class="sxs-lookup"><span data-stu-id="21d4c-159">toocustomize these settings, select hello gear icon toohello right of hello drop down, and then choose **New Preset**.</span></span>

    ![Wirecast](./media/media-services-wirecast-live-encoder/media-services-wirecast3.png)
5. <span data-ttu-id="21d4c-161">Configurez les présélections de l’encodeur.</span><span class="sxs-lookup"><span data-stu-id="21d4c-161">Configure encoder presets.</span></span>

    <span data-ttu-id="21d4c-162">Nom Bonjour prédéfini et vérifier les paramètres recommandés de hello suivants :</span><span class="sxs-lookup"><span data-stu-id="21d4c-162">Name hello preset, and check for hello following recommended settings:</span></span>

    <span data-ttu-id="21d4c-163">**Vidéo**</span><span class="sxs-lookup"><span data-stu-id="21d4c-163">**Video**</span></span>

   * <span data-ttu-id="21d4c-164">Encodeur : MainConcept H.264</span><span class="sxs-lookup"><span data-stu-id="21d4c-164">Encoder: MainConcept H.264</span></span>
   * <span data-ttu-id="21d4c-165">Images par seconde : 30</span><span class="sxs-lookup"><span data-stu-id="21d4c-165">Frames per Second: 30</span></span>
   * <span data-ttu-id="21d4c-166">Débit binaire moyen : 5 000 Kbit/s (cette valeur peut être ajustée en fonction des limitations du réseau)</span><span class="sxs-lookup"><span data-stu-id="21d4c-166">Average bit rate: 5000 kbits/sec (Can be adjusted based on network limitations)</span></span>
   * <span data-ttu-id="21d4c-167">Profil : Principal</span><span class="sxs-lookup"><span data-stu-id="21d4c-167">Profile: Main</span></span>
   * <span data-ttu-id="21d4c-168">Trame-clé toutes les : 60 images</span><span class="sxs-lookup"><span data-stu-id="21d4c-168">Key frame every: 60 frames</span></span>

    <span data-ttu-id="21d4c-169">**Audio**</span><span class="sxs-lookup"><span data-stu-id="21d4c-169">**Audio**</span></span>

   * <span data-ttu-id="21d4c-170">Vitesse de transmission cible : 192 kbit/s</span><span class="sxs-lookup"><span data-stu-id="21d4c-170">Target bit rate: 192 kbits/sec</span></span>
   * <span data-ttu-id="21d4c-171">Taux d’échantillonnage : 44 100 kHz</span><span class="sxs-lookup"><span data-stu-id="21d4c-171">Sample Rate: 44.100 kHz</span></span>

     ![Wirecast](./media/media-services-wirecast-live-encoder/media-services-wirecast4.png)
6. <span data-ttu-id="21d4c-173">Appuyez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="21d4c-173">Press **Save**.</span></span>

    <span data-ttu-id="21d4c-174">champ de codage Hello a maintenant profil hello nouvellement créé disponible pour la sélection.</span><span class="sxs-lookup"><span data-stu-id="21d4c-174">hello Encoding field now has hello newly created profile available for selection.</span></span>

    <span data-ttu-id="21d4c-175">Vérifiez que hello nouveau profil est sélectionné.</span><span class="sxs-lookup"><span data-stu-id="21d4c-175">Make sure hello new profile is selected.</span></span>
7. <span data-ttu-id="21d4c-176">Obtenir les URL d’entrée du canal hello dans l’ordre tooassign il toohello Wirecast **point de terminaison RTMP**.</span><span class="sxs-lookup"><span data-stu-id="21d4c-176">Get hello channel's input URL in order tooassign it toohello Wirecast **RTMP Endpoint**.</span></span>

    <span data-ttu-id="21d4c-177">Accédez outil AMSE toohello précédent et vérifier l’état d’achèvement canal hello.</span><span class="sxs-lookup"><span data-stu-id="21d4c-177">Navigate back toohello AMSE tool, and check on hello channel completion status.</span></span> <span data-ttu-id="21d4c-178">Une fois que l’état de hello a été modifié à partir de **départ** trop**en cours d’exécution**, vous pouvez obtenir les URL d’entrée hello.</span><span class="sxs-lookup"><span data-stu-id="21d4c-178">Once hello State has changed from **Starting** too**Running**, you can get hello input URL.</span></span>

    <span data-ttu-id="21d4c-179">Lorsque le canal de hello est en cours d’exécution, cliquez avec le bouton droit sur nom de la chaîne hello, naviguez vers le bas toohover sur **tooclipboard de copier l’URL entrée** , puis sélectionnez **URL entrée principale**.</span><span class="sxs-lookup"><span data-stu-id="21d4c-179">When hello channel is running, right click hello channel name, navigate down toohover over **Copy Input URL tooclipboard** and then select **Primary Input  URL**.</span></span>  

    ![Wirecast](./media/media-services-wirecast-live-encoder/media-services-wirecast6.png)
8. <span data-ttu-id="21d4c-181">Bonjour Wirecast **les paramètres de sortie** fenêtre, coller ces informations dans hello **adresse** champ de la section de sortie hello et attribuer un nom de flux.</span><span class="sxs-lookup"><span data-stu-id="21d4c-181">In hello Wirecast **Output Settings** window, paste this information in hello **Address** field of hello output section, and assign a stream name.</span></span>

    ![Wirecast](./media/media-services-wirecast-live-encoder/media-services-wirecast5.png)

1. <span data-ttu-id="21d4c-183">Sélectionnez **OK**.</span><span class="sxs-lookup"><span data-stu-id="21d4c-183">Select **OK**.</span></span>
2. <span data-ttu-id="21d4c-184">Sur hello principal **Wirecast** , vérifiez que les sources d’entrée audio et vidéo sont prêts, puis appuyez sur **flux** dans l’angle supérieur gauche de hello.</span><span class="sxs-lookup"><span data-stu-id="21d4c-184">On hello main **Wirecast** screen, confirm input sources for video and audio are ready and then hit **Stream** in hello top left hand corner.</span></span>

   ![Wirecast](./media/media-services-wirecast-live-encoder/media-services-wirecast7.png)

> [!IMPORTANT]
> <span data-ttu-id="21d4c-186">Avant de cliquer sur **flux**, vous **doit** vous assurer que le canal de hello est prêt.</span><span class="sxs-lookup"><span data-stu-id="21d4c-186">Before you click **Stream**, you **must** ensure that hello Channel is ready.</span></span>
> <span data-ttu-id="21d4c-187">Assurez-vous également que pas tooleave hello canal dans un état prêt sans une contribution d’entrée de flux pendant plus de 15 minutes >.</span><span class="sxs-lookup"><span data-stu-id="21d4c-187">Also, make sure not tooleave hello Channel in a ready state without an input contribution feed for longer than > 15 minutes.</span></span>
>
>

## <a name="test-playback"></a><span data-ttu-id="21d4c-188">Tester la lecture</span><span class="sxs-lookup"><span data-stu-id="21d4c-188">Test playback</span></span>

<span data-ttu-id="21d4c-189">Accédez outil AMSE toohello et cliquez avec le bouton droit sur toobe de canal hello testé.</span><span class="sxs-lookup"><span data-stu-id="21d4c-189">Navigate toohello AMSE tool, and right click hello channel toobe tested.</span></span> <span data-ttu-id="21d4c-190">À partir du menu de hello, placez le curseur sur **hello de lecture aperçu** et sélectionnez **avec Azure Media Player**.</span><span class="sxs-lookup"><span data-stu-id="21d4c-190">From hello menu, hover over **Playback hello Preview** and select **with Azure Media Player**.</span></span>  

    ![wirecast](./media/media-services-wirecast-live-encoder/media-services-wirecast8.png)

<span data-ttu-id="21d4c-191">Si le flux de données hello s’affiche dans le lecteur hello, encodeur de hello a été correctement configuré tooconnect tooAMS.</span><span class="sxs-lookup"><span data-stu-id="21d4c-191">If hello stream appears in hello player, then hello encoder has been properly configured tooconnect tooAMS.</span></span>

<span data-ttu-id="21d4c-192">Si une erreur est reçue, le canal de hello devez paramètres d’encodeur et de réinitialisation toobe ajustées.</span><span class="sxs-lookup"><span data-stu-id="21d4c-192">If an error is received, hello channel will need toobe reset and encoder settings adjusted.</span></span> <span data-ttu-id="21d4c-193">Consultez hello [dépannage](media-services-troubleshooting-live-streaming.md) rubrique pour obtenir des conseils.</span><span class="sxs-lookup"><span data-stu-id="21d4c-193">Please see hello [troubleshooting](media-services-troubleshooting-live-streaming.md) topic for guidance.</span></span>  

## <a name="create-a-program"></a><span data-ttu-id="21d4c-194">Créer un programme</span><span class="sxs-lookup"><span data-stu-id="21d4c-194">Create a program</span></span>
1. <span data-ttu-id="21d4c-195">Une fois que vous avez vérifié que la lecture fonctionne sur le canal, créez un programme.</span><span class="sxs-lookup"><span data-stu-id="21d4c-195">Once channel playback is confirmed, create a program.</span></span> <span data-ttu-id="21d4c-196">Sous hello **Live** onglet dans l’outil AMSE hello, cliquez avec le bouton droit dans la zone du programme hello et sélectionnez **créer un nouveau programme**.</span><span class="sxs-lookup"><span data-stu-id="21d4c-196">Under hello **Live** tab in hello AMSE tool, right click within hello program area and select **Create New Program**.</span></span>  

    ![Wirecast](./media/media-services-wirecast-live-encoder/media-services-wirecast9.png)
2. <span data-ttu-id="21d4c-198">Nom de programme de hello et, si nécessaire, ajustez hello **longueur de fenêtre d’Archive** (heures de too4 les valeurs par défaut).</span><span class="sxs-lookup"><span data-stu-id="21d4c-198">Name hello program and, if needed, adjust hello **Archive Window Length** (which defaults too4 hours).</span></span> <span data-ttu-id="21d4c-199">Vous pouvez également spécifier un emplacement de stockage ou les conserver en tant que valeur par défaut hello.</span><span class="sxs-lookup"><span data-stu-id="21d4c-199">You can also specify a storage location or leave as hello default.</span></span>  
3. <span data-ttu-id="21d4c-200">Vérifiez hello **maintenant démarrer hello programme** boîte.</span><span class="sxs-lookup"><span data-stu-id="21d4c-200">Check hello **Start hello Program now** box.</span></span>
4. <span data-ttu-id="21d4c-201">Cliquez sur **Créer le programme**.</span><span class="sxs-lookup"><span data-stu-id="21d4c-201">Click **Create Program**.</span></span>  

   >[!NOTE]
   ><span data-ttu-id="21d4c-202">La création d’un programme prend moins de temps que la création d’un canal.</span><span class="sxs-lookup"><span data-stu-id="21d4c-202">Program creation takes less time than channel creation.</span></span>
       
5. <span data-ttu-id="21d4c-203">Une fois l’exécution du programme hello, confirmer la lecture en cliquant avec le bouton droit sur un programme hello et en naviguant trop**lecture hello programmes** , puis en sélectionnant **avec Azure Media Player**.</span><span class="sxs-lookup"><span data-stu-id="21d4c-203">Once hello program is running, confirm playback by right clicking hello program and navigating too**Playback hello program(s)** and then selecting **with Azure Media Player**.</span></span>  
6. <span data-ttu-id="21d4c-204">Après confirmation, cliquez à nouveau programme de hello, puis sélectionnez **copier hello URL de sortie tooClipboard** (ou en extraire ces informations hello **informations et des paramètres du programme** option de menu de hello).</span><span class="sxs-lookup"><span data-stu-id="21d4c-204">Once confirmed, right click hello program again and select **Copy hello Output URL tooClipboard** (or retrieve this information from hello **Program information and settings** option from hello menu).</span></span>

<span data-ttu-id="21d4c-205">Hello flux est maintenant prêt toobe incorporé dans un lecteur ou public tooan distribuée pour live affichage.</span><span class="sxs-lookup"><span data-stu-id="21d4c-205">hello stream is now ready toobe embedded in a player, or distributed tooan audience for live viewing.</span></span>  

## <a name="troubleshooting"></a><span data-ttu-id="21d4c-206">Résolution des problèmes</span><span class="sxs-lookup"><span data-stu-id="21d4c-206">Troubleshooting</span></span>
<span data-ttu-id="21d4c-207">Consultez hello [dépannage](media-services-troubleshooting-live-streaming.md) rubrique pour obtenir des conseils.</span><span class="sxs-lookup"><span data-stu-id="21d4c-207">Please see hello [troubleshooting](media-services-troubleshooting-live-streaming.md) topic for guidance.</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="21d4c-208">Parcours d’apprentissage de Media Services</span><span class="sxs-lookup"><span data-stu-id="21d4c-208">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="21d4c-209">Fournir des commentaires</span><span class="sxs-lookup"><span data-stu-id="21d4c-209">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
