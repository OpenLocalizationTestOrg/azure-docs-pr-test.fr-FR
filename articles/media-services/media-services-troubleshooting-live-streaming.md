---
title: "guide d’aaaTroubleshooting pour la diffusion en continu | Documents Microsoft"
description: "Cette rubrique fournit des suggestions sur comment tootroubleshoot live des problèmes de diffusion en continu."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 3a7f6c1d-ce57-4fa4-a7a6-edb526b3ffbf
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: juliako
ms.openlocfilehash: 8549bae947ff3b225ce624220d1e48b63f90208c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-guide-for-live-streaming"></a><span data-ttu-id="2a1f4-103">Guide de dépannage de la vidéo en flux continu</span><span class="sxs-lookup"><span data-stu-id="2a1f4-103">Troubleshooting guide for live streaming</span></span>
<span data-ttu-id="2a1f4-104">Cette rubrique offre des suggestions sur la façon de tootroubleshoot dynamique de certains problèmes de diffusion en continu.</span><span class="sxs-lookup"><span data-stu-id="2a1f4-104">This topic gives suggestions on how tootroubleshoot some live streaming problems.</span></span>

## <a name="issues-related-tooon-premises-encoders"></a><span data-ttu-id="2a1f4-105">Les problèmes liés à des encodeurs de tooon local</span><span class="sxs-lookup"><span data-stu-id="2a1f4-105">Issues related tooon-premises encoders</span></span>
<span data-ttu-id="2a1f4-106">Cette section fournit des suggestions de tootroubleshoot des problèmes connexes tooon local encodeurs qui sont configurés toosend un canaux tooAMS de flux à débit binaire unique qui est activés pour l’encodage live.</span><span class="sxs-lookup"><span data-stu-id="2a1f4-106">This section gives suggestions on how tootroubleshoot problems related tooon-premises encoders that are configured toosend a single bitrate stream tooAMS channels that are enabled for live encoding.</span></span>

### <a name="problem-would-like-toosee-logs"></a><span data-ttu-id="2a1f4-107">Problème : Aimeriez toosee journaux</span><span class="sxs-lookup"><span data-stu-id="2a1f4-107">Problem: Would like toosee logs</span></span>
* <span data-ttu-id="2a1f4-108">**Problème potentiel**: impossible de trouver des journaux de l’encodeur qui pourraient aider à déboguer des problèmes.</span><span class="sxs-lookup"><span data-stu-id="2a1f4-108">**Potential issue**: Can't find encoder logs that might help in debugging issues.</span></span>
  
  * <span data-ttu-id="2a1f4-109">**Telestream Wirecast** : les journaux se trouvent en général sous C:\Users\{nom_utilisateur}\AppData\Roaming\Wirecast\\</span><span class="sxs-lookup"><span data-stu-id="2a1f4-109">**Telestream Wirecast**: You can usually find logs under C:\Users\{username}\AppData\Roaming\Wirecast\\</span></span> 
  * <span data-ttu-id="2a1f4-110">**Live élémentaire**: vous trouverez a des liens toologs sur le portail de gestion hello.</span><span class="sxs-lookup"><span data-stu-id="2a1f4-110">**Elemental Live**: You can find has links toologs on hello management portal.</span></span> <span data-ttu-id="2a1f4-111">Cliquez sur **Statistiques**, puis **Journaux**.</span><span class="sxs-lookup"><span data-stu-id="2a1f4-111">Click on **Stats**, then **Logs**.</span></span> <span data-ttu-id="2a1f4-112">Sur hello **des fichiers journaux** page, vous verrez une liste de tous les journaux hello des éléments de l’événement en direct ; sélectionnez hello une correspondant à votre session actuelle.</span><span class="sxs-lookup"><span data-stu-id="2a1f4-112">On hello **Log Files** page, you will see a list of logs for all hello LiveEvent items; select hello one matching your current session.</span></span> 
  * <span data-ttu-id="2a1f4-113">**Flash Media Encoder de Live**: vous trouverez hello **répertoire du journal en cours...**  en naviguant toohello **journal de codage** onglet.</span><span class="sxs-lookup"><span data-stu-id="2a1f4-113">**Flash Media Live Encoder**: You can find hello **Log Directory...** by navigating toohello **Encoding Log** tab.</span></span>

### <a name="problem-there-is-no-option-for-outputting-a-progressive-stream"></a><span data-ttu-id="2a1f4-114">Problème : il n’existe aucune option pour générer un flux progressif</span><span class="sxs-lookup"><span data-stu-id="2a1f4-114">Problem: There is no option for outputting a progressive stream</span></span>
* <span data-ttu-id="2a1f4-115">**Problème potentiel**: encodeur hello utilisé ne désentrelacer automatiquement.</span><span class="sxs-lookup"><span data-stu-id="2a1f4-115">**Potential issue**: hello encoder being used doesn't automatically deinterlace.</span></span> 
  
    <span data-ttu-id="2a1f4-116">**Étapes de dépannage**: recherchez une option de désentrelacement dans l’interface d’encodeur hello.</span><span class="sxs-lookup"><span data-stu-id="2a1f4-116">**Troubleshooting steps**: Look for a de-interlacing option within hello encoder interface.</span></span> <span data-ttu-id="2a1f4-117">Une fois le désentrelacement activé, revérifiez les paramètres de sortie progressive.</span><span class="sxs-lookup"><span data-stu-id="2a1f4-117">Once de-interlacing is enabled, check again for progressive output settings.</span></span> 

### <a name="problem-tried-several-encoder-output-settings-and-still-unable-tooconnect"></a><span data-ttu-id="2a1f4-118">Problème : A tenté de plusieurs paramètres de sortie l’encodeur et tooconnect toujours pas.</span><span class="sxs-lookup"><span data-stu-id="2a1f4-118">Problem: Tried several encoder output settings and still unable tooconnect.</span></span>
* <span data-ttu-id="2a1f4-119">**Problème potentiel**: le canal d’encodage Azure n’a pas été réinitialisé correctement.</span><span class="sxs-lookup"><span data-stu-id="2a1f4-119">**Potential issue**: Azure encoding channel was not properly reset.</span></span> 
  
    <span data-ttu-id="2a1f4-120">**Étapes de dépannage**: Assurez-vous qu’encodeur de hello n’est plus repousse tooAMS, arrêter et réinitialiser le canal de hello.</span><span class="sxs-lookup"><span data-stu-id="2a1f4-120">**Troubleshooting steps**: Make sure hello encoder is no longer pushing tooAMS, stop and reset hello channel.</span></span> <span data-ttu-id="2a1f4-121">Une fois en cours d’exécution, essayez de connecter votre encodeur avec les nouveaux paramètres de hello.</span><span class="sxs-lookup"><span data-stu-id="2a1f4-121">Once running again, try connecting your encoder with hello new settings.</span></span> <span data-ttu-id="2a1f4-122">Si cela ne résout toujours pas de problème de hello, essayez de créer un nouveau canal entièrement, parfois, les canaux peuvent être endommagés après que plusieurs tentatives infructueuses.</span><span class="sxs-lookup"><span data-stu-id="2a1f4-122">If this still does not correct hello issue, try creating a new channel entirely, sometimes channels can become corrupt after several failed attempts.</span></span>  
* <span data-ttu-id="2a1f4-123">**Problème potentiel**: taille de GOP hello ou les paramètres de l’image clé ne sont pas optimaux.</span><span class="sxs-lookup"><span data-stu-id="2a1f4-123">**Potential issue**: hello GOP size or key frame settings are not optimal.</span></span> 
  
    <span data-ttu-id="2a1f4-124">**Étapes de dépannage**: la taille de GOP ou l’intervalle d’image clé recommandé(e) est de deux secondes.</span><span class="sxs-lookup"><span data-stu-id="2a1f4-124">**Troubleshooting steps**: Recommended GOP size or keyframe interval is 2 seconds.</span></span> <span data-ttu-id="2a1f4-125">Certains encodeurs calculent ce paramètre en nombre d’images, tandis que d’autres utilisent des secondes.</span><span class="sxs-lookup"><span data-stu-id="2a1f4-125">Some encoders calculate this setting in number of frames, while others use seconds.</span></span> <span data-ttu-id="2a1f4-126">Par exemple : lors de la sortie à 30 i/s, hello taille de GOP serait 60 frames, qui est équivalent too2 secondes.</span><span class="sxs-lookup"><span data-stu-id="2a1f4-126">For example: When outputting 30fps, hello GOP size would be 60 frames, which is equivalent too2 seconds.</span></span>  
* <span data-ttu-id="2a1f4-127">**Problème potentiel**: ports fermés bloquent les flux hello.</span><span class="sxs-lookup"><span data-stu-id="2a1f4-127">**Potential issue**: Closed ports are blocking hello stream.</span></span> 
  
    <span data-ttu-id="2a1f4-128">**Étapes de dépannage**: lors de la diffusion en continu via le protocole RTMP, vérifiez le pare-feu et/ou tooconfirm de paramètres de proxy que les ports de sortie 1935 et 1936 sont ouverts.</span><span class="sxs-lookup"><span data-stu-id="2a1f4-128">**Troubleshooting steps**: When streaming via RTMP, check firewall and/or proxy settings tooconfirm that outbound ports 1935 and 1936 are open.</span></span> <span data-ttu-id="2a1f4-129">Lorsque vous utilisez la diffusion en flux continu RTP, vérifiez que le port sortant 2010 est ouvert.</span><span class="sxs-lookup"><span data-stu-id="2a1f4-129">When using RTP streaming, confirm that outbound port 2010 is open.</span></span> 

### <a name="problem-when-configuring-hello-encoder-toostream-with-hello-rtp-protocol-there-is-no-place-tooenter-a-host-name"></a><span data-ttu-id="2a1f4-130">Problème : Lorsque vous configurez hello encodeur toostream hello protocole RTP, il n’est pas tooenter un nom d’hôte.</span><span class="sxs-lookup"><span data-stu-id="2a1f4-130">Problem: When configuring hello encoder toostream with hello RTP protocol, there is no place tooenter a host name.</span></span>
* <span data-ttu-id="2a1f4-131">**Problème potentiel**: les encodeurs de nombreux RTP ne permettent pas de noms d’hôte et une adresse IP doit toobe acquis.</span><span class="sxs-lookup"><span data-stu-id="2a1f4-131">**Potential issue**: Many RTP encoders do not allow for host names, and an IP address will need toobe acquired.</span></span>  
  
    <span data-ttu-id="2a1f4-132">**Étapes de dépannage**: toofind hello d’adresse IP, ouvrez une invite de commande sur n’importe quel ordinateur.</span><span class="sxs-lookup"><span data-stu-id="2a1f4-132">**Troubleshooting steps**: toofind hello IP address, open a command prompt on any computer.</span></span> <span data-ttu-id="2a1f4-133">toodo dans Windows, ouvrez hello Lanceur d’exécution (WIN + R) et tapez « cmd » tooopen.</span><span class="sxs-lookup"><span data-stu-id="2a1f4-133">toodo this in Windows, open hello Run launcher (WIN + R) and type “cmd” tooopen.</span></span>  
  
    <span data-ttu-id="2a1f4-134">Une fois que l’invite de commandes hello est ouvert, tapez « Ping [nom d’hôte de AMS] ».</span><span class="sxs-lookup"><span data-stu-id="2a1f4-134">Once hello command prompt is open, type "Ping [AMS Host Name]".</span></span> 
  
    <span data-ttu-id="2a1f4-135">nom d’hôte Hello peut être dérivée en omettant le numéro du port hello de hello Azure URL de réception, mise en évidence dans hello l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="2a1f4-135">hello host name can be derived by omitting hello port number from hello Azure Ingest URL, as highlighted in hello following example:</span></span> 
  
    <span data-ttu-id="2a1f4-136">rtp://test2-amstest009.rtp.channel.mediaservices.windows.net:2010/</span><span class="sxs-lookup"><span data-stu-id="2a1f4-136">rtp://test2-amstest009.rtp.channel.mediaservices.windows.net:2010/</span></span> 
  
    ![FMLE](./media/media-services-fmle-live-encoder/media-services-fmle10.png)

> [!NOTE]
> <span data-ttu-id="2a1f4-138">Si après avoir appliqué les étapes de dépannage hello que vous toujours ne peut pas diffuser en continu, envoyer un ticket de support à l’aide de hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="2a1f4-138">If after following hello troubleshooting steps you still cannot successfully stream, submit a support ticket using hello Azure portal.</span></span>
> 
> 

## <a name="media-services-learning-paths"></a><span data-ttu-id="2a1f4-139">Parcours d’apprentissage de Media Services</span><span class="sxs-lookup"><span data-stu-id="2a1f4-139">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="2a1f4-140">Fournir des commentaires</span><span class="sxs-lookup"><span data-stu-id="2a1f4-140">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

