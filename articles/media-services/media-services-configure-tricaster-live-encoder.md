---
title: "aaaConfigure hello NewTek TriCaster encodeur toosend un flux à débit binaire unique en continu | Documents Microsoft"
description: "Cette rubrique montre comment tooconfigure hello Tricaster live encodeur toosend un canaux tooAMS de flux à débit binaire unique qui est activés pour l’encodage live."
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
ms.openlocfilehash: 57dcf62a6a76b04e69f147a738be78ccb3c3ecdc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-newtek-tricaster-encoder-toosend-a-single-bitrate-live-stream"></a><span data-ttu-id="11424-103">Utilisez hello NewTek TriCaster encodeur toosend un flux à débit binaire unique en continu.</span><span class="sxs-lookup"><span data-stu-id="11424-103">Use hello NewTek TriCaster encoder toosend a single bitrate live stream</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="11424-104">Tricaster</span><span class="sxs-lookup"><span data-stu-id="11424-104">Tricaster</span></span>](media-services-configure-tricaster-live-encoder.md)
> * [<span data-ttu-id="11424-105">Elemental Live</span><span class="sxs-lookup"><span data-stu-id="11424-105">Elemental Live</span></span>](media-services-configure-elemental-live-encoder.md)
> * [<span data-ttu-id="11424-106">Wirecast</span><span class="sxs-lookup"><span data-stu-id="11424-106">Wirecast</span></span>](media-services-configure-wirecast-live-encoder.md)
> * [<span data-ttu-id="11424-107">FMLE</span><span class="sxs-lookup"><span data-stu-id="11424-107">FMLE</span></span>](media-services-configure-fmle-live-encoder.md)
>
>

<span data-ttu-id="11424-108">Cette rubrique montre comment tooconfigure hello [NewTek TriCaster](http://newtek.com/products/tricaster-40.html) live encodeur toosend un canaux tooAMS de flux à débit binaire unique qui est activés pour l’encodage live.</span><span class="sxs-lookup"><span data-stu-id="11424-108">This topic shows how tooconfigure hello [NewTek TriCaster](http://newtek.com/products/tricaster-40.html) live encoder toosend a single bitrate stream tooAMS channels that are enabled for live encoding.</span></span> <span data-ttu-id="11424-109">Pour plus d’informations, consultez [utilisation de canaux est à activé tooPerform Live encodage avec Azure Media Services](media-services-manage-live-encoder-enabled-channels.md).</span><span class="sxs-lookup"><span data-stu-id="11424-109">For more information, see [Working with Channels that are Enabled tooPerform Live Encoding with Azure Media Services](media-services-manage-live-encoder-enabled-channels.md).</span></span>

<span data-ttu-id="11424-110">Ce didacticiel montre comment toomanage Azure Media Services (AMS) avec l’outil d’Azure Media Services Explorer (AMSE).</span><span class="sxs-lookup"><span data-stu-id="11424-110">This tutorial shows how toomanage Azure Media Services (AMS) with Azure Media Services Explorer (AMSE) tool.</span></span> <span data-ttu-id="11424-111">Cet outil est uniquement compatible avec les PC Windows.</span><span class="sxs-lookup"><span data-stu-id="11424-111">This tool only runs on Windows PC.</span></span> <span data-ttu-id="11424-112">Si vous êtes sur le Mac ou Linux, utilisez hello toocreate portail Azure [canaux](media-services-portal-creating-live-encoder-enabled-channel.md#create-a-channel) et [programmes](media-services-portal-creating-live-encoder-enabled-channel.md).</span><span class="sxs-lookup"><span data-stu-id="11424-112">If you are on Mac or Linux, use hello Azure portal toocreate [channels](media-services-portal-creating-live-encoder-enabled-channel.md#create-a-channel) and [programs](media-services-portal-creating-live-encoder-enabled-channel.md).</span></span>

> [!NOTE]
> <span data-ttu-id="11424-113">Lors d’envoi dans une contribution à l’aide de Tricaster flux tooAMS canaux activés pour l’encodage live, il peut y avoir des problèmes de vidéo et audio dans votre événement en direct si vous utilisez certaines fonctionnalités de Tricaster, tels que rapide Couper entre les flux ou de basculement à partir de plus .</span><span class="sxs-lookup"><span data-stu-id="11424-113">When using Tricaster for sending in a contribution feed tooAMS channels that are enabled for live encoding, there can be video/audio glitches in your live event if you use certain features of Tricaster, such as rapid cutting between feeds, or switching to/from slates.</span></span> <span data-ttu-id="11424-114">Hello AMS équipe travaille sur la résolution de ces problèmes, en attendant, il est déconseillé de toouse ces fonctionnalités.</span><span class="sxs-lookup"><span data-stu-id="11424-114">hello AMS team is working on fixing these issues, until then, it is not recommend toouse these features.</span></span>
>
>

## <a name="prerequisites"></a><span data-ttu-id="11424-115">Composants requis</span><span class="sxs-lookup"><span data-stu-id="11424-115">Prerequisites</span></span>
* [<span data-ttu-id="11424-116">Créer un compte Azure Media Services</span><span class="sxs-lookup"><span data-stu-id="11424-116">Create an Azure Media Services account</span></span>](media-services-portal-create-account.md)
* <span data-ttu-id="11424-117">Vérifiez qu’un point de terminaison de streaming est en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="11424-117">Ensure there is a Streaming Endpoint running.</span></span> <span data-ttu-id="11424-118">Pour plus d’informations, consultez [Gestion des points de terminaison de diffusion en continu dans un compte Media Services](media-services-portal-manage-streaming-endpoints.md)</span><span class="sxs-lookup"><span data-stu-id="11424-118">For more information, see [Manage Streaming Endpoints in a Media Services Account](media-services-portal-manage-streaming-endpoints.md)</span></span>
* <span data-ttu-id="11424-119">Installer la version la plus récente de hello hello [AMSE](https://github.com/Azure/Azure-Media-Services-Explorer) outil.</span><span class="sxs-lookup"><span data-stu-id="11424-119">Install hello latest version of hello [AMSE](https://github.com/Azure/Azure-Media-Services-Explorer) tool.</span></span>
* <span data-ttu-id="11424-120">Lancer l’outil de hello et tooyour AMS compte de connexion.</span><span class="sxs-lookup"><span data-stu-id="11424-120">Launch hello tool and connect tooyour AMS account.</span></span>

## <a name="tips"></a><span data-ttu-id="11424-121">Conseils</span><span class="sxs-lookup"><span data-stu-id="11424-121">Tips</span></span>
* <span data-ttu-id="11424-122">Si possible, utilisez une connexion Internet câblée.</span><span class="sxs-lookup"><span data-stu-id="11424-122">Whenever possible, use a hardwired internet connection.</span></span>
* <span data-ttu-id="11424-123">Une règle empirique lors de la détermination de la bande passante est hello toodouble débits binaires de diffusion en continu.</span><span class="sxs-lookup"><span data-stu-id="11424-123">A good rule of thumb when determining bandwidth requirements is toodouble hello streaming bitrates.</span></span> <span data-ttu-id="11424-124">Alors que cela n’est pas obligatoire, il vous aide à atténuer l’impact hello de congestion du réseau.</span><span class="sxs-lookup"><span data-stu-id="11424-124">While this is not a mandatory requirement, it will help mitigate hello impact of network congestion.</span></span>
* <span data-ttu-id="11424-125">Lors de l’utilisation d’encodeurs logiciels, fermez tous les programmes inutiles.</span><span class="sxs-lookup"><span data-stu-id="11424-125">When using software based encoders, close out any unnecessary programs.</span></span>

## <a name="create-a-channel"></a><span data-ttu-id="11424-126">Créer un canal</span><span class="sxs-lookup"><span data-stu-id="11424-126">Create a channel</span></span>
1. <span data-ttu-id="11424-127">Dans l’outil AMSE hello, accédez à toohello **Live** onglet et cliquez avec le bouton droit dans la zone de canal hello.</span><span class="sxs-lookup"><span data-stu-id="11424-127">In hello AMSE tool, navigate toohello **Live** tab, and right click within hello channel area.</span></span> <span data-ttu-id="11424-128">Dans le menu qui s’affiche, sélectionnez **Créer un canal...**</span><span class="sxs-lookup"><span data-stu-id="11424-128">Select **Create channel…**</span></span> <span data-ttu-id="11424-129">à partir du menu de hello.</span><span class="sxs-lookup"><span data-stu-id="11424-129">from hello menu.</span></span>

    ![Tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster1.png)

2. <span data-ttu-id="11424-131">Spécifiez un nom de canal, champ de description hello est facultatif.</span><span class="sxs-lookup"><span data-stu-id="11424-131">Specify a channel name, hello description field is optional.</span></span> <span data-ttu-id="11424-132">Sous paramètres de canal, sélectionnez **Standard** pour hello option d’encodage Live, avec hello entrée protocole défini trop**RTMP**.</span><span class="sxs-lookup"><span data-stu-id="11424-132">Under Channel Settings, select **Standard** for hello Live Encoding option, with hello Input Protocol set too**RTMP**.</span></span> <span data-ttu-id="11424-133">Vous pouvez laisser tous les autres paramètres inchangés.</span><span class="sxs-lookup"><span data-stu-id="11424-133">You can leave all other settings as is.</span></span>

    <span data-ttu-id="11424-134">Vérifiez que hello **début hello nouveau canal maintenant** est sélectionnée.</span><span class="sxs-lookup"><span data-stu-id="11424-134">Make sure hello **Start hello new channel now** is selected.</span></span>

3. <span data-ttu-id="11424-135">Cliquez sur **Créer un canal**.</span><span class="sxs-lookup"><span data-stu-id="11424-135">Click **Create Channel**.</span></span>

   ![Tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster2.png)

> [!NOTE]
> <span data-ttu-id="11424-137">canal de Hello peut prendre jusqu'à 20 minutes toostart.</span><span class="sxs-lookup"><span data-stu-id="11424-137">hello channel can take as long as 20 minutes toostart.</span></span>
>
>

<span data-ttu-id="11424-138">Pendant le démarrage du canal de hello, vous pouvez [configurer l’encodeur de hello](media-services-configure-tricaster-live-encoder.md#configure_tricaster_rtmp).</span><span class="sxs-lookup"><span data-stu-id="11424-138">While hello channel is starting you can [configure hello encoder](media-services-configure-tricaster-live-encoder.md#configure_tricaster_rtmp).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="11424-139">Notez que la facturation commence dès que l’état du canal indique qu’il est prêt à être utilisé.</span><span class="sxs-lookup"><span data-stu-id="11424-139">Note that billing starts as soon as Channel goes into a ready state.</span></span> <span data-ttu-id="11424-140">Pour plus d’informations, consultez [États du canal](media-services-manage-live-encoder-enabled-channels.md#states).</span><span class="sxs-lookup"><span data-stu-id="11424-140">For more information, see [Channel's states](media-services-manage-live-encoder-enabled-channels.md#states).</span></span>
>
>

## <span data-ttu-id="11424-141"><a id=configure_tricaster_rtmp></a>Configurer hello NewTek TriCaster encodeur</span><span class="sxs-lookup"><span data-stu-id="11424-141"><a id=configure_tricaster_rtmp></a>Configure hello NewTek TriCaster encoder</span></span>
<span data-ttu-id="11424-142">Dans ce didacticiel hello des paramètres de sortie suivants sont utilisés.</span><span class="sxs-lookup"><span data-stu-id="11424-142">In this tutorial hello following output settings are used.</span></span> <span data-ttu-id="11424-143">Hello le reste de cette section décrit les étapes de configuration plus en détail.</span><span class="sxs-lookup"><span data-stu-id="11424-143">hello rest of this section describes configuration steps in more detail.</span></span>

<span data-ttu-id="11424-144">**Vidéo**:</span><span class="sxs-lookup"><span data-stu-id="11424-144">**Video**:</span></span>

* <span data-ttu-id="11424-145">Codec : H.264</span><span class="sxs-lookup"><span data-stu-id="11424-145">Codec: H.264</span></span>
* <span data-ttu-id="11424-146">Profil : Élevé (niveau 4.0)</span><span class="sxs-lookup"><span data-stu-id="11424-146">Profile: High (Level 4.0)</span></span>
* <span data-ttu-id="11424-147">Débit binaire : 5 000 kbit/s</span><span class="sxs-lookup"><span data-stu-id="11424-147">Bitrate: 5000 kbps</span></span>
* <span data-ttu-id="11424-148">Image clé : 2 secondes (60 secondes)</span><span class="sxs-lookup"><span data-stu-id="11424-148">Keyframe: 2 seconds (60 seconds)</span></span>
* <span data-ttu-id="11424-149">Fréquence d’images : 30</span><span class="sxs-lookup"><span data-stu-id="11424-149">Frame Rate: 30</span></span>

<span data-ttu-id="11424-150">**Audio**:</span><span class="sxs-lookup"><span data-stu-id="11424-150">**Audio**:</span></span>

* <span data-ttu-id="11424-151">Codec : AAC (LC)</span><span class="sxs-lookup"><span data-stu-id="11424-151">Codec: AAC (LC)</span></span>
* <span data-ttu-id="11424-152">Débit binaire : 192 kbit/s</span><span class="sxs-lookup"><span data-stu-id="11424-152">Bitrate: 192 kbps</span></span>
* <span data-ttu-id="11424-153">Taux d’échantillonnage : 44,1 kHz</span><span class="sxs-lookup"><span data-stu-id="11424-153">Sample Rate: 44.1 kHz</span></span>

### <a name="configuration-steps"></a><span data-ttu-id="11424-154">Configuration</span><span class="sxs-lookup"><span data-stu-id="11424-154">Configuration steps</span></span>
1. <span data-ttu-id="11424-155">Créez un projet **NewTek TriCaster** en fonction de la source d’entrée vidéo utilisée.</span><span class="sxs-lookup"><span data-stu-id="11424-155">Create a new **NewTek TriCaster** project depending on what video input source is being used.</span></span>
2. <span data-ttu-id="11424-156">Une fois dans ce projet, recherche hello **flux** bouton, puis cliquez sur hello ENGRENAGE icône tooit tooaccess hello flux configuration menu suivant.</span><span class="sxs-lookup"><span data-stu-id="11424-156">Once within that project, find hello **Stream** button, and click hello gear icon next tooit tooaccess hello stream configuration menu.</span></span>

    ![Tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster3.png)
3. <span data-ttu-id="11424-158">Une fois hello menu ouvert, cliquez sur **nouveau** sous le titre de connexion hello.</span><span class="sxs-lookup"><span data-stu-id="11424-158">Once hello menu has opened, click **New** under hello Connection heading.</span></span> <span data-ttu-id="11424-159">Lorsque vous y êtes invité pour le type de connexion hello, sélectionnez **Adobe Flash**.</span><span class="sxs-lookup"><span data-stu-id="11424-159">When prompted for hello connection type, select **Adobe Flash**.</span></span>

    ![Tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster4.png)
4. <span data-ttu-id="11424-161">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="11424-161">Click **OK**.</span></span>
5. <span data-ttu-id="11424-162">Un profil FMLE peut maintenant être importé en cliquant sur la flèche sous déroulante hello **profil Streaming** et la navigation trop**Parcourir**.</span><span class="sxs-lookup"><span data-stu-id="11424-162">An FMLE profile can now be imported by clicking hello drop down arrow under **Streaming Profile** and navigating too**Browse**.</span></span>

    ![Tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster5.png)
6. <span data-ttu-id="11424-164">Accédez toowhere hello configuré FMLE profil a été enregistré.</span><span class="sxs-lookup"><span data-stu-id="11424-164">Navigate toowhere hello configured FMLE profile was saved.</span></span>
7. <span data-ttu-id="11424-165">Sélectionnez-le, puis appuyez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="11424-165">Select it, and press **OK**.</span></span>

    <span data-ttu-id="11424-166">Une fois le profil de hello est téléchargé, passez toohello prochaine étape.</span><span class="sxs-lookup"><span data-stu-id="11424-166">Once hello profile is uploaded, proceed toohello next step.</span></span>
8. <span data-ttu-id="11424-167">Obtenir les URL d’entrée du canal hello dans l’ordre tooassign il toohello Tricaster **point de terminaison RTMP**.</span><span class="sxs-lookup"><span data-stu-id="11424-167">Get hello channel's input URL in order tooassign it toohello Tricaster **RTMP Endpoint**.</span></span>

    <span data-ttu-id="11424-168">Accédez outil AMSE toohello précédent et vérifier l’état d’achèvement canal hello.</span><span class="sxs-lookup"><span data-stu-id="11424-168">Navigate back toohello AMSE tool, and check on hello channel completion status.</span></span> <span data-ttu-id="11424-169">Une fois que l’état de hello a été modifié à partir de **départ** trop**en cours d’exécution**, vous pouvez obtenir les URL d’entrée hello.</span><span class="sxs-lookup"><span data-stu-id="11424-169">Once hello State has changed from **Starting** too**Running**, you can get hello input URL.</span></span>

    <span data-ttu-id="11424-170">Lorsque le canal de hello est en cours d’exécution, cliquez avec le bouton droit sur nom de la chaîne hello, naviguez vers le bas toohover sur **tooclipboard de copier l’URL entrée** , puis sélectionnez **URL entrée principale**.</span><span class="sxs-lookup"><span data-stu-id="11424-170">When hello channel is running, right click hello channel name, navigate down toohover over **Copy Input URL tooclipboard** and then select **Primary Input  URL**.</span></span>  

    ![Tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster6.png)
9. <span data-ttu-id="11424-172">Coller ces informations dans hello **emplacement** champ sous **Flash Server** dans le projet de Tricaster hello.</span><span class="sxs-lookup"><span data-stu-id="11424-172">Paste this information in hello **Location** field under **Flash Server** within hello Tricaster project.</span></span> <span data-ttu-id="11424-173">Également attribuer un nom de flux Bonjour **ID de flux** champ.</span><span class="sxs-lookup"><span data-stu-id="11424-173">Also assign a stream name in hello **Stream ID** field.</span></span>

    <span data-ttu-id="11424-174">Si les informations de flux de données a été ajoutées à profil FMLE toohello, il peut également être importée toothis section en cliquant sur **importer les paramètres**, toohello enregistré FMLE profil en cliquant sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="11424-174">If stream information was added toohello FMLE profile, it can also be imported toothis section by clicking **Import Settings**, navigating toohello saved FMLE profile and clicking **OK**.</span></span> <span data-ttu-id="11424-175">les champs Flash Server appropriés Hello doivent remplir avec des informations de hello à partir de FMLE.</span><span class="sxs-lookup"><span data-stu-id="11424-175">hello relevant Flash Server fields should populate with hello information from FMLE.</span></span>

    ![Tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster7.png)
10. <span data-ttu-id="11424-177">Lorsque vous avez terminé, cliquez sur **OK** bas hello écran hello.</span><span class="sxs-lookup"><span data-stu-id="11424-177">When finished, click **OK** at hello bottom of hello screen.</span></span> <span data-ttu-id="11424-178">Lorsque les entrées audio et vidéo en hello Tricaster sont prêtes, commencez tooAMS de diffusion en continu en cliquant sur hello **flux** bouton.</span><span class="sxs-lookup"><span data-stu-id="11424-178">When video and audio inputs into hello Tricaster are ready, begin streaming tooAMS by clicking hello **Stream** button.</span></span>

     ![Tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster11.png)

> [!IMPORTANT]
> <span data-ttu-id="11424-180">Avant de cliquer sur **flux**, vous **doit** vous assurer que le canal de hello est prêt.</span><span class="sxs-lookup"><span data-stu-id="11424-180">Before you click **Stream**, you **must** ensure that hello Channel is ready.</span></span>
> <span data-ttu-id="11424-181">Assurez-vous également que pas tooleave hello canal dans un état prêt sans une contribution d’entrée de flux pendant plus de 15 minutes >.</span><span class="sxs-lookup"><span data-stu-id="11424-181">Also, make sure not tooleave hello Channel in a ready state without an input contribution feed for longer than > 15 minutes.</span></span>
>
>

## <a name="test-playback"></a><span data-ttu-id="11424-182">Tester la lecture</span><span class="sxs-lookup"><span data-stu-id="11424-182">Test playback</span></span>
<span data-ttu-id="11424-183">Accédez outil AMSE toohello et cliquez avec le bouton droit sur toobe de canal hello testé.</span><span class="sxs-lookup"><span data-stu-id="11424-183">Navigate toohello AMSE tool, and right click hello channel toobe tested.</span></span> <span data-ttu-id="11424-184">À partir du menu de hello, placez le curseur sur **hello de lecture aperçu** et sélectionnez **avec Azure Media Player**.</span><span class="sxs-lookup"><span data-stu-id="11424-184">From hello menu, hover over **Playback hello Preview** and select **with Azure Media Player**.</span></span>  

    ![tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster8.png)

<span data-ttu-id="11424-185">Si le flux de données hello s’affiche dans le lecteur hello, encodeur de hello a été correctement configuré tooconnect tooAMS.</span><span class="sxs-lookup"><span data-stu-id="11424-185">If hello stream appears in hello player, then hello encoder has been properly configured tooconnect tooAMS.</span></span>

<span data-ttu-id="11424-186">Si une erreur est reçue, le canal de hello devez paramètres d’encodeur et de réinitialisation toobe ajustées.</span><span class="sxs-lookup"><span data-stu-id="11424-186">If an error is received, hello channel will need toobe reset and encoder settings adjusted.</span></span> <span data-ttu-id="11424-187">Consultez hello [dépannage](media-services-troubleshooting-live-streaming.md) rubrique pour obtenir des conseils.</span><span class="sxs-lookup"><span data-stu-id="11424-187">Please see hello [troubleshooting](media-services-troubleshooting-live-streaming.md) topic for guidance.</span></span>  

## <a name="create-a-program"></a><span data-ttu-id="11424-188">Créer un programme</span><span class="sxs-lookup"><span data-stu-id="11424-188">Create a program</span></span>
1. <span data-ttu-id="11424-189">Une fois que vous avez vérifié que la lecture fonctionne sur le canal, créez un programme.</span><span class="sxs-lookup"><span data-stu-id="11424-189">Once channel playback is confirmed, create a program.</span></span> <span data-ttu-id="11424-190">Sous hello **Live** onglet dans l’outil AMSE hello, cliquez avec le bouton droit dans la zone du programme hello et sélectionnez **créer un nouveau programme**.</span><span class="sxs-lookup"><span data-stu-id="11424-190">Under hello **Live** tab in hello AMSE tool, right click within hello program area and select **Create New Program**.</span></span>  

    ![Tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster9.png)
2. <span data-ttu-id="11424-192">Nom de programme de hello et, si nécessaire, ajustez hello **longueur de fenêtre d’Archive** (heures de too4 les valeurs par défaut).</span><span class="sxs-lookup"><span data-stu-id="11424-192">Name hello program and, if needed, adjust hello **Archive Window Length** (which defaults too4 hours).</span></span> <span data-ttu-id="11424-193">Vous pouvez également spécifier un emplacement de stockage ou les conserver en tant que valeur par défaut hello.</span><span class="sxs-lookup"><span data-stu-id="11424-193">You can also specify a storage location or leave as hello default.</span></span>  
3. <span data-ttu-id="11424-194">Vérifiez hello **maintenant démarrer hello programme** boîte.</span><span class="sxs-lookup"><span data-stu-id="11424-194">Check hello **Start hello Program now** box.</span></span>
4. <span data-ttu-id="11424-195">Cliquez sur **Créer le programme**.</span><span class="sxs-lookup"><span data-stu-id="11424-195">Click **Create Program**.</span></span>  

    >[!NOTE]
    ><span data-ttu-id="11424-196">La création d’un programme prend moins de temps que la création d’un canal.</span><span class="sxs-lookup"><span data-stu-id="11424-196">Program creation takes less time than channel creation.</span></span>
        
5. <span data-ttu-id="11424-197">Une fois l’exécution du programme hello, confirmer la lecture en cliquant avec le bouton droit sur un programme hello et en naviguant trop**lecture hello programmes** , puis en sélectionnant **avec Azure Media Player**.</span><span class="sxs-lookup"><span data-stu-id="11424-197">Once hello program is running, confirm playback by right clicking hello program and navigating too**Playback hello program(s)** and then selecting **with Azure Media Player**.</span></span>  
6. <span data-ttu-id="11424-198">Après confirmation, cliquez à nouveau programme de hello, puis sélectionnez **copier hello URL de sortie tooClipboard** (ou en extraire ces informations hello **informations et des paramètres du programme** option de menu de hello).</span><span class="sxs-lookup"><span data-stu-id="11424-198">Once confirmed, right click hello program again and select **Copy hello Output URL tooClipboard** (or retrieve this information from hello **Program information and settings** option from hello menu).</span></span>

<span data-ttu-id="11424-199">Hello flux est maintenant prêt toobe incorporé dans un lecteur ou public tooan distribuée pour live affichage.</span><span class="sxs-lookup"><span data-stu-id="11424-199">hello stream is now ready toobe embedded in a player, or distributed tooan audience for live viewing.</span></span>  

## <a name="troubleshooting"></a><span data-ttu-id="11424-200">Résolution des problèmes</span><span class="sxs-lookup"><span data-stu-id="11424-200">Troubleshooting</span></span>
<span data-ttu-id="11424-201">Consultez hello [dépannage](media-services-troubleshooting-live-streaming.md) rubrique pour obtenir des conseils.</span><span class="sxs-lookup"><span data-stu-id="11424-201">Please see hello [troubleshooting](media-services-troubleshooting-live-streaming.md) topic for guidance.</span></span>

## <a name="next-step"></a><span data-ttu-id="11424-202">Étape suivante</span><span class="sxs-lookup"><span data-stu-id="11424-202">Next step</span></span>
<span data-ttu-id="11424-203">Consultez les parcours d’apprentissage de Media Services.</span><span class="sxs-lookup"><span data-stu-id="11424-203">Review Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="11424-204">Fournir des commentaires</span><span class="sxs-lookup"><span data-stu-id="11424-204">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
