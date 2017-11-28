---
title: "aaaConfigure hello FMLE encodeur toosend un flux à débit binaire unique en continu | Documents Microsoft"
description: "Cette rubrique montre comment tooconfigure hello Flash Media en direct encodeur (FMLE) encodeur toosend un canaux tooAMS de flux à débit binaire unique qui est activés pour l’encodage live."
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
ms.openlocfilehash: 780d911c5186ec09c784264f9a0d0c3f8059d305
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-fmle-encoder-toosend-a-single-bitrate-live-stream"></a><span data-ttu-id="65b43-103">Utilisez hello FMLE encodeur toosend un flux à débit binaire unique en continu.</span><span class="sxs-lookup"><span data-stu-id="65b43-103">Use hello FMLE encoder toosend a single bitrate live stream</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="65b43-104">FMLE</span><span class="sxs-lookup"><span data-stu-id="65b43-104">FMLE</span></span>](media-services-configure-fmle-live-encoder.md)
> * [<span data-ttu-id="65b43-105">Elemental Live</span><span class="sxs-lookup"><span data-stu-id="65b43-105">Elemental Live</span></span>](media-services-configure-elemental-live-encoder.md)
> * [<span data-ttu-id="65b43-106">Tricaster</span><span class="sxs-lookup"><span data-stu-id="65b43-106">Tricaster</span></span>](media-services-configure-tricaster-live-encoder.md)
> * [<span data-ttu-id="65b43-107">Wirecast</span><span class="sxs-lookup"><span data-stu-id="65b43-107">Wirecast</span></span>](media-services-configure-wirecast-live-encoder.md)
>
>

<span data-ttu-id="65b43-108">Cette rubrique montre comment tooconfigure hello [Flash Media Encoder Live](http://www.adobe.com/products/flash-media-encoder.html) toosend d’encodeur (FMLE) tooAMS canaux activés pour l’encodage live de diffuser un débit binaire unique.</span><span class="sxs-lookup"><span data-stu-id="65b43-108">This topic shows how tooconfigure hello [Flash Media Live Encoder](http://www.adobe.com/products/flash-media-encoder.html) (FMLE) encoder toosend a single bitrate stream tooAMS channels that are enabled for live encoding.</span></span> <span data-ttu-id="65b43-109">Pour plus d’informations, consultez [utilisation de canaux est à activé tooPerform Live encodage avec Azure Media Services](media-services-manage-live-encoder-enabled-channels.md).</span><span class="sxs-lookup"><span data-stu-id="65b43-109">For more information, see [Working with Channels that are Enabled tooPerform Live Encoding with Azure Media Services](media-services-manage-live-encoder-enabled-channels.md).</span></span>

<span data-ttu-id="65b43-110">Ce didacticiel montre comment toomanage Azure Media Services (AMS) avec l’outil d’Azure Media Services Explorer (AMSE).</span><span class="sxs-lookup"><span data-stu-id="65b43-110">This tutorial shows how toomanage Azure Media Services (AMS) with Azure Media Services Explorer (AMSE) tool.</span></span> <span data-ttu-id="65b43-111">Cet outil est uniquement compatible avec les PC Windows.</span><span class="sxs-lookup"><span data-stu-id="65b43-111">This tool only runs on Windows PC.</span></span> <span data-ttu-id="65b43-112">Si vous êtes sur le Mac ou Linux, utilisez hello toocreate portail Azure [canaux](media-services-portal-creating-live-encoder-enabled-channel.md#create-a-channel) et [programmes](media-services-portal-creating-live-encoder-enabled-channel.md).</span><span class="sxs-lookup"><span data-stu-id="65b43-112">If you are on Mac or Linux, use hello Azure portal toocreate [channels](media-services-portal-creating-live-encoder-enabled-channel.md#create-a-channel) and [programs](media-services-portal-creating-live-encoder-enabled-channel.md).</span></span>

<span data-ttu-id="65b43-113">Notez que ce didacticiel décrit l’utilisation de AAC.</span><span class="sxs-lookup"><span data-stu-id="65b43-113">Note that this tutorial describes using AAC.</span></span> <span data-ttu-id="65b43-114">Cependant, FMLE ne prend pas en charge AAC par défaut.</span><span class="sxs-lookup"><span data-stu-id="65b43-114">However, FMLE doesn’t supports AAC by default.</span></span> <span data-ttu-id="65b43-115">Vous devez toopurchase un plug-in pour le codage AAC ce type de MainConcept : [plug-in AAC](http://www.mainconcept.com/products/plug-ins/plug-ins-for-adobe/aac-encoder-fmle.html)</span><span class="sxs-lookup"><span data-stu-id="65b43-115">You would need toopurchase a plugin for AAC encoding such as from MainConcept: [AAC plugin](http://www.mainconcept.com/products/plug-ins/plug-ins-for-adobe/aac-encoder-fmle.html)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="65b43-116">Composants requis</span><span class="sxs-lookup"><span data-stu-id="65b43-116">Prerequisites</span></span>
* [<span data-ttu-id="65b43-117">Créer un compte Azure Media Services</span><span class="sxs-lookup"><span data-stu-id="65b43-117">Create an Azure Media Services account</span></span>](media-services-portal-create-account.md)
* <span data-ttu-id="65b43-118">Vérifiez qu’un point de terminaison de streaming est en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="65b43-118">Ensure there is a Streaming Endpoint running.</span></span> <span data-ttu-id="65b43-119">Pour plus d’informations, consultez [Gestion des points de terminaison de diffusion en continu dans un compte Media Services](media-services-portal-manage-streaming-endpoints.md)</span><span class="sxs-lookup"><span data-stu-id="65b43-119">For more information, see [Manage Streaming Endpoints in a Media Services Account](media-services-portal-manage-streaming-endpoints.md)</span></span>
* <span data-ttu-id="65b43-120">Installer la version la plus récente de hello hello [AMSE](https://github.com/Azure/Azure-Media-Services-Explorer) outil.</span><span class="sxs-lookup"><span data-stu-id="65b43-120">Install hello latest version of hello [AMSE](https://github.com/Azure/Azure-Media-Services-Explorer) tool.</span></span>
* <span data-ttu-id="65b43-121">Lancer l’outil de hello et tooyour AMS compte de connexion.</span><span class="sxs-lookup"><span data-stu-id="65b43-121">Launch hello tool and connect tooyour AMS account.</span></span>

## <a name="tips"></a><span data-ttu-id="65b43-122">Conseils</span><span class="sxs-lookup"><span data-stu-id="65b43-122">Tips</span></span>
* <span data-ttu-id="65b43-123">Si possible, utilisez une connexion Internet câblée.</span><span class="sxs-lookup"><span data-stu-id="65b43-123">Whenever possible, use a hardwired internet connection.</span></span>
* <span data-ttu-id="65b43-124">Une règle empirique lors de la détermination de la bande passante est hello toodouble débits binaires de diffusion en continu.</span><span class="sxs-lookup"><span data-stu-id="65b43-124">A good rule of thumb when determining bandwidth requirements is toodouble hello streaming bitrates.</span></span> <span data-ttu-id="65b43-125">Alors que cela n’est pas obligatoire, il vous aide à atténuer l’impact hello de congestion du réseau.</span><span class="sxs-lookup"><span data-stu-id="65b43-125">While this is not a mandatory requirement, it will help mitigate hello impact of network congestion.</span></span>
* <span data-ttu-id="65b43-126">Lors de l’utilisation d’encodeurs logiciels, fermez tous les programmes inutiles.</span><span class="sxs-lookup"><span data-stu-id="65b43-126">When using software based encoders, close out any unnecessary programs.</span></span>

## <a name="create-a-channel"></a><span data-ttu-id="65b43-127">Créer un canal</span><span class="sxs-lookup"><span data-stu-id="65b43-127">Create a channel</span></span>
1. <span data-ttu-id="65b43-128">Dans l’outil AMSE hello, accédez à toohello **Live** onglet et cliquez avec le bouton droit dans la zone de canal hello.</span><span class="sxs-lookup"><span data-stu-id="65b43-128">In hello AMSE tool, navigate toohello **Live** tab, and right click within hello channel area.</span></span> <span data-ttu-id="65b43-129">Dans le menu qui s’affiche, sélectionnez **Créer un canal...**</span><span class="sxs-lookup"><span data-stu-id="65b43-129">Select **Create channel…**</span></span> <span data-ttu-id="65b43-130">à partir du menu de hello.</span><span class="sxs-lookup"><span data-stu-id="65b43-130">from hello menu.</span></span>

    ![FMLE](./media/media-services-fmle-live-encoder/media-services-fmle1.png)

2. <span data-ttu-id="65b43-132">Spécifiez un nom de canal, champ de description hello est facultatif.</span><span class="sxs-lookup"><span data-stu-id="65b43-132">Specify a channel name, hello description field is optional.</span></span> <span data-ttu-id="65b43-133">Sous paramètres de canal, sélectionnez **Standard** pour hello option d’encodage Live, avec hello entrée protocole défini trop**RTMP**.</span><span class="sxs-lookup"><span data-stu-id="65b43-133">Under Channel Settings, select **Standard** for hello Live Encoding option, with hello Input Protocol set too**RTMP**.</span></span> <span data-ttu-id="65b43-134">Vous pouvez laisser tous les autres paramètres inchangés.</span><span class="sxs-lookup"><span data-stu-id="65b43-134">You can leave all other settings as is.</span></span>

    <span data-ttu-id="65b43-135">Vérifiez que hello **début hello nouveau canal maintenant** est sélectionnée.</span><span class="sxs-lookup"><span data-stu-id="65b43-135">Make sure hello **Start hello new channel now** is selected.</span></span>

3. <span data-ttu-id="65b43-136">Cliquez sur **Créer un canal**.</span><span class="sxs-lookup"><span data-stu-id="65b43-136">Click **Create Channel**.</span></span>

   ![FMLE](./media/media-services-fmle-live-encoder/media-services-fmle2.png)

> [!NOTE]
> <span data-ttu-id="65b43-138">canal de Hello peut prendre jusqu'à 20 minutes toostart.</span><span class="sxs-lookup"><span data-stu-id="65b43-138">hello channel can take as long as 20 minutes toostart.</span></span>
>
>

<span data-ttu-id="65b43-139">Pendant le démarrage du canal de hello, vous pouvez [configurer l’encodeur de hello](media-services-configure-fmle-live-encoder.md#configure_fmle_rtmp).</span><span class="sxs-lookup"><span data-stu-id="65b43-139">While hello channel is starting you can [configure hello encoder](media-services-configure-fmle-live-encoder.md#configure_fmle_rtmp).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="65b43-140">Notez que la facturation commence dès que l’état du canal indique qu’il est prêt à être utilisé.</span><span class="sxs-lookup"><span data-stu-id="65b43-140">Note that billing starts as soon as Channel goes into a ready state.</span></span> <span data-ttu-id="65b43-141">Pour plus d’informations, consultez [États du canal](media-services-manage-live-encoder-enabled-channels.md#states).</span><span class="sxs-lookup"><span data-stu-id="65b43-141">For more information, see [Channel's states](media-services-manage-live-encoder-enabled-channels.md#states).</span></span>
>
>

## <span data-ttu-id="65b43-142"><a id=configure_fmle_rtmp></a>Configurer l’encodeur FMLE hello</span><span class="sxs-lookup"><span data-stu-id="65b43-142"><a id=configure_fmle_rtmp></a>Configure hello FMLE encoder</span></span>
<span data-ttu-id="65b43-143">Dans ce didacticiel hello des paramètres de sortie suivants sont utilisés.</span><span class="sxs-lookup"><span data-stu-id="65b43-143">In this tutorial hello following output settings are used.</span></span> <span data-ttu-id="65b43-144">Hello le reste de cette section décrit les étapes de configuration plus en détail.</span><span class="sxs-lookup"><span data-stu-id="65b43-144">hello rest of this section describes configuration steps in more detail.</span></span>

<span data-ttu-id="65b43-145">**Vidéo**:</span><span class="sxs-lookup"><span data-stu-id="65b43-145">**Video**:</span></span>

* <span data-ttu-id="65b43-146">Codec : H.264</span><span class="sxs-lookup"><span data-stu-id="65b43-146">Codec: H.264</span></span>
* <span data-ttu-id="65b43-147">Profil : Élevé (niveau 4.0)</span><span class="sxs-lookup"><span data-stu-id="65b43-147">Profile: High (Level 4.0)</span></span>
* <span data-ttu-id="65b43-148">Débit binaire : 5 000 kbit/s</span><span class="sxs-lookup"><span data-stu-id="65b43-148">Bitrate: 5000 kbps</span></span>
* <span data-ttu-id="65b43-149">Image clé : 2 secondes (60 secondes)</span><span class="sxs-lookup"><span data-stu-id="65b43-149">Keyframe: 2 seconds (60 seconds)</span></span>
* <span data-ttu-id="65b43-150">Fréquence d’images : 30</span><span class="sxs-lookup"><span data-stu-id="65b43-150">Frame Rate: 30</span></span>

<span data-ttu-id="65b43-151">**Audio**:</span><span class="sxs-lookup"><span data-stu-id="65b43-151">**Audio**:</span></span>

* <span data-ttu-id="65b43-152">Codec : AAC (LC)</span><span class="sxs-lookup"><span data-stu-id="65b43-152">Codec: AAC (LC)</span></span>
* <span data-ttu-id="65b43-153">Débit binaire : 192 kbit/s</span><span class="sxs-lookup"><span data-stu-id="65b43-153">Bitrate: 192 kbps</span></span>
* <span data-ttu-id="65b43-154">Taux d’échantillonnage : 44,1 kHz</span><span class="sxs-lookup"><span data-stu-id="65b43-154">Sample Rate: 44.1 kHz</span></span>

### <a name="configuration-steps"></a><span data-ttu-id="65b43-155">Configuration</span><span class="sxs-lookup"><span data-stu-id="65b43-155">Configuration steps</span></span>
1. <span data-ttu-id="65b43-156">Accédez toohello que Flash Media en direct l’encodeur (FMLE) de l’interface sur l’ordinateur hello utilisé.</span><span class="sxs-lookup"><span data-stu-id="65b43-156">Navigate toohello Flash Media Live Encoder’s (FMLE) interface on hello machine being used.</span></span>

    <span data-ttu-id="65b43-157">interface de Hello est une page principale de paramètres.</span><span class="sxs-lookup"><span data-stu-id="65b43-157">hello interface is one main page of settings.</span></span> <span data-ttu-id="65b43-158">Veuillez prendre note des recommandées suivantes de hello paramètres tooget main FMLE d’à l’aide de la diffusion en continu.</span><span class="sxs-lookup"><span data-stu-id="65b43-158">Please take note of hello following recommended settings tooget started with streaming using FMLE.</span></span>

   * <span data-ttu-id="65b43-159">Format : Fréquence d’images H.264 : 30,00</span><span class="sxs-lookup"><span data-stu-id="65b43-159">Format: H.264 Frame Rate: 30.00</span></span>
   * <span data-ttu-id="65b43-160">Taille d’entrée : 1280 x 720</span><span class="sxs-lookup"><span data-stu-id="65b43-160">Input Size: 1280 x 720</span></span>
   * <span data-ttu-id="65b43-161">Débit binaire : 5000 Kbit/s (cette valeur peut être ajustée en fonction des limitations du réseau)</span><span class="sxs-lookup"><span data-stu-id="65b43-161">Bit Rate: 5000 Kbps (Can be adjusted based on network limitations)</span></span>  

     ![FMLE](./media/media-services-fmle-live-encoder/media-services-fmle3.png)

     <span data-ttu-id="65b43-163">Lors de l’utilisation entrelacée sources, veuillez coche hello « Désentrelacer » option</span><span class="sxs-lookup"><span data-stu-id="65b43-163">When using interlaced sources, please checkmark hello “Deinterlace” option</span></span>
2. <span data-ttu-id="65b43-164">Sélectionnez hello clé icône suivant tooFormat, ces paramètres supplémentaires doivent être :</span><span class="sxs-lookup"><span data-stu-id="65b43-164">Select hello wrench icon next tooFormat, these additional settings should be:</span></span>

   * <span data-ttu-id="65b43-165">Profil : Principal</span><span class="sxs-lookup"><span data-stu-id="65b43-165">Profile: Main</span></span>
   * <span data-ttu-id="65b43-166">Niveau : 4.0</span><span class="sxs-lookup"><span data-stu-id="65b43-166">Level: 4.0</span></span>
   * <span data-ttu-id="65b43-167">Fréquence d’image clé : 2 secondes</span><span class="sxs-lookup"><span data-stu-id="65b43-167">Keyframe Frequency: 2 seconds</span></span>

     ![FMLE](./media/media-services-fmle-live-encoder/media-services-fmle4.png)
3. <span data-ttu-id="65b43-169">Définissez hello suivant paramètre audio important :</span><span class="sxs-lookup"><span data-stu-id="65b43-169">Set hello following important audio setting:</span></span>

   * <span data-ttu-id="65b43-170">Format : AAC</span><span class="sxs-lookup"><span data-stu-id="65b43-170">Format: AAC</span></span>
   * <span data-ttu-id="65b43-171">Taux d’échantillonnage : 44100 kHz</span><span class="sxs-lookup"><span data-stu-id="65b43-171">Sample Rate: 44100 Hz</span></span>
   * <span data-ttu-id="65b43-172">Débit binaire : 192 kbit/s</span><span class="sxs-lookup"><span data-stu-id="65b43-172">Bitrate: 192 Kbps</span></span>

     ![FMLE](./media/media-services-fmle-live-encoder/media-services-fmle5.png)
4. <span data-ttu-id="65b43-174">Obtenir les URL d’entrée du canal hello dans l’ordre tooassign il toohello FMLE **point de terminaison RTMP**.</span><span class="sxs-lookup"><span data-stu-id="65b43-174">Get hello channel's input URL in order tooassign it toohello FMLE's **RTMP Endpoint**.</span></span>

    <span data-ttu-id="65b43-175">Accédez outil AMSE toohello précédent et vérifier l’état d’achèvement canal hello.</span><span class="sxs-lookup"><span data-stu-id="65b43-175">Navigate back toohello AMSE tool, and check on hello channel completion status.</span></span> <span data-ttu-id="65b43-176">Une fois que l’état de hello a été modifié à partir de **départ** trop**en cours d’exécution**, vous pouvez obtenir les URL d’entrée hello.</span><span class="sxs-lookup"><span data-stu-id="65b43-176">Once hello State has changed from **Starting** too**Running**, you can get hello input URL.</span></span>

    <span data-ttu-id="65b43-177">Lorsque le canal de hello est en cours d’exécution, cliquez avec le bouton droit sur nom de la chaîne hello, naviguez vers le bas toohover sur **tooclipboard de copier l’URL entrée** , puis sélectionnez **URL entrée principale**.</span><span class="sxs-lookup"><span data-stu-id="65b43-177">When hello channel is running, right click hello channel name, navigate down toohover over **Copy Input URL tooclipboard** and then select **Primary Input  URL**.</span></span>  

    ![FMLE](./media/media-services-fmle-live-encoder/media-services-fmle6.png)
5. <span data-ttu-id="65b43-179">Coller ces informations dans hello **FMS URL** champ de la section de sortie hello et attribuer un nom de flux.</span><span class="sxs-lookup"><span data-stu-id="65b43-179">Paste this information in hello **FMS URL** field of hello output section, and assign a stream name.</span></span>

    ![FMLE](./media/media-services-fmle-live-encoder/media-services-fmle7.png)

    <span data-ttu-id="65b43-181">Pour assurer la redondance supplémentaire, répétez ces étapes avec hello secondaire URL d’entrée.</span><span class="sxs-lookup"><span data-stu-id="65b43-181">For extra redundancy, repeat these steps with hello Secondary Input URL.</span></span>
6. <span data-ttu-id="65b43-182">Sélectionnez **Connecter**.</span><span class="sxs-lookup"><span data-stu-id="65b43-182">Select **Connect**.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="65b43-183">Avant de cliquer sur **Connect**, vous **doit** vous assurer que le canal de hello est prêt.</span><span class="sxs-lookup"><span data-stu-id="65b43-183">Before you click **Connect**, you **must** ensure that hello Channel is ready.</span></span>
> <span data-ttu-id="65b43-184">Assurez-vous également que pas tooleave hello canal dans un état prêt sans une contribution d’entrée de flux pendant plus de 15 minutes >.</span><span class="sxs-lookup"><span data-stu-id="65b43-184">Also, make sure not tooleave hello Channel in a ready state without an input contribution feed for longer than > 15 minutes.</span></span>
>
>

## <a name="test-playback"></a><span data-ttu-id="65b43-185">Tester la lecture</span><span class="sxs-lookup"><span data-stu-id="65b43-185">Test playback</span></span>

<span data-ttu-id="65b43-186">Accédez outil AMSE toohello et cliquez avec le bouton droit sur toobe de canal hello testé.</span><span class="sxs-lookup"><span data-stu-id="65b43-186">Navigate toohello AMSE tool, and right click hello channel toobe tested.</span></span> <span data-ttu-id="65b43-187">À partir du menu de hello, placez le curseur sur **hello de lecture aperçu** et sélectionnez **avec Azure Media Player**.</span><span class="sxs-lookup"><span data-stu-id="65b43-187">From hello menu, hover over **Playback hello Preview** and select **with Azure Media Player**.</span></span>  

    ![fmle](./media/media-services-fmle-live-encoder/media-services-fmle8.png)

<span data-ttu-id="65b43-188">Si le flux de données hello s’affiche dans le lecteur hello, encodeur de hello a été correctement configuré tooconnect tooAMS.</span><span class="sxs-lookup"><span data-stu-id="65b43-188">If hello stream appears in hello player, then hello encoder has been properly configured tooconnect tooAMS.</span></span>

<span data-ttu-id="65b43-189">Si une erreur est reçue, le canal de hello devez paramètres d’encodeur et de réinitialisation toobe ajustées.</span><span class="sxs-lookup"><span data-stu-id="65b43-189">If an error is received, hello channel will need toobe reset and encoder settings adjusted.</span></span> <span data-ttu-id="65b43-190">Consultez hello [dépannage](media-services-troubleshooting-live-streaming.md) rubrique pour obtenir des conseils.</span><span class="sxs-lookup"><span data-stu-id="65b43-190">Please see hello [troubleshooting](media-services-troubleshooting-live-streaming.md) topic for guidance.</span></span>  

## <a name="create-a-program"></a><span data-ttu-id="65b43-191">Créer un programme</span><span class="sxs-lookup"><span data-stu-id="65b43-191">Create a program</span></span>
1. <span data-ttu-id="65b43-192">Une fois que vous avez vérifié que la lecture fonctionne sur le canal, créez un programme.</span><span class="sxs-lookup"><span data-stu-id="65b43-192">Once channel playback is confirmed, create a program.</span></span> <span data-ttu-id="65b43-193">Sous hello **Live** onglet dans l’outil AMSE hello, cliquez avec le bouton droit dans la zone du programme hello et sélectionnez **créer un nouveau programme**.</span><span class="sxs-lookup"><span data-stu-id="65b43-193">Under hello **Live** tab in hello AMSE tool, right click within hello program area and select **Create New Program**.</span></span>  

    ![FMLE](./media/media-services-fmle-live-encoder/media-services-fmle9.png)
2. <span data-ttu-id="65b43-195">Nom de programme de hello et, si nécessaire, ajustez hello **longueur de fenêtre d’Archive** (heures de too4 les valeurs par défaut).</span><span class="sxs-lookup"><span data-stu-id="65b43-195">Name hello program and, if needed, adjust hello **Archive Window Length** (which defaults too4 hours).</span></span> <span data-ttu-id="65b43-196">Vous pouvez également spécifier un emplacement de stockage ou les conserver en tant que valeur par défaut hello.</span><span class="sxs-lookup"><span data-stu-id="65b43-196">You can also specify a storage location or leave as hello default.</span></span>  
3. <span data-ttu-id="65b43-197">Vérifiez hello **maintenant démarrer hello programme** boîte.</span><span class="sxs-lookup"><span data-stu-id="65b43-197">Check hello **Start hello Program now** box.</span></span>
4. <span data-ttu-id="65b43-198">Cliquez sur **Créer le programme**.</span><span class="sxs-lookup"><span data-stu-id="65b43-198">Click **Create Program**.</span></span>  

    >[!NOTE]
    ><span data-ttu-id="65b43-199">La création d’un programme prend moins de temps que la création d’un canal.</span><span class="sxs-lookup"><span data-stu-id="65b43-199">Program creation takes less time than channel creation.</span></span>
        
5. <span data-ttu-id="65b43-200">Une fois l’exécution du programme hello, confirmer la lecture en cliquant avec le bouton droit sur un programme hello et en naviguant trop**lecture hello programmes** , puis en sélectionnant **avec Azure Media Player**.</span><span class="sxs-lookup"><span data-stu-id="65b43-200">Once hello program is running, confirm playback by right clicking hello program and navigating too**Playback hello program(s)** and then selecting **with Azure Media Player**.</span></span>  
6. <span data-ttu-id="65b43-201">Après confirmation, cliquez à nouveau programme de hello, puis sélectionnez **copier hello URL de sortie tooClipboard** (ou en extraire ces informations hello **informations et des paramètres du programme** option de menu de hello).</span><span class="sxs-lookup"><span data-stu-id="65b43-201">Once confirmed, right click hello program again and select **Copy hello Output URL tooClipboard** (or retrieve this information from hello **Program information and settings** option from hello menu).</span></span>

<span data-ttu-id="65b43-202">Hello flux est maintenant prêt toobe incorporé dans un lecteur ou public tooan distribuée pour live affichage.</span><span class="sxs-lookup"><span data-stu-id="65b43-202">hello stream is now ready toobe embedded in a player, or distributed tooan audience for live viewing.</span></span>  

## <a name="troubleshooting"></a><span data-ttu-id="65b43-203">Résolution des problèmes</span><span class="sxs-lookup"><span data-stu-id="65b43-203">Troubleshooting</span></span>
<span data-ttu-id="65b43-204">Consultez hello [dépannage](media-services-troubleshooting-live-streaming.md) rubrique pour obtenir des conseils.</span><span class="sxs-lookup"><span data-stu-id="65b43-204">Please see hello [troubleshooting](media-services-troubleshooting-live-streaming.md) topic for guidance.</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="65b43-205">Parcours d’apprentissage de Media Services</span><span class="sxs-lookup"><span data-stu-id="65b43-205">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="65b43-206">Fournir des commentaires</span><span class="sxs-lookup"><span data-stu-id="65b43-206">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
