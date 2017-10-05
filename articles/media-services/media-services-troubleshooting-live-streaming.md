---
title: "Guide de dépannage de la vidéo en flux continu | Microsoft Docs"
description: "Cette rubrique fournit des suggestions sur la façon de résoudre les problèmes de vidéo en flux continu."
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
ms.openlocfilehash: fa91baf7c494941fccf0e6ca38b930f3c2a521ce
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="troubleshooting-guide-for-live-streaming"></a><span data-ttu-id="0dc58-103">Guide de dépannage de la vidéo en flux continu</span><span class="sxs-lookup"><span data-stu-id="0dc58-103">Troubleshooting guide for live streaming</span></span>
<span data-ttu-id="0dc58-104">Cette rubrique fournit des suggestions sur la façon de résoudre certains problèmes de vidéo en flux continu.</span><span class="sxs-lookup"><span data-stu-id="0dc58-104">This topic gives suggestions on how to troubleshoot some live streaming problems.</span></span>

## <a name="issues-related-to-on-premises-encoders"></a><span data-ttu-id="0dc58-105">Problèmes liés aux encodeurs locaux</span><span class="sxs-lookup"><span data-stu-id="0dc58-105">Issues related to on-premises encoders</span></span>
<span data-ttu-id="0dc58-106">Cette section fournit des suggestions sur la façon de résoudre les problèmes liés aux encodeurs locaux qui sont configurés pour envoyer un flux à débit binaire unique à des canaux AMS activés pour l’encodage live.</span><span class="sxs-lookup"><span data-stu-id="0dc58-106">This section gives suggestions on how to troubleshoot problems related to on-premises encoders that are configured to send a single bitrate stream to AMS channels that are enabled for live encoding.</span></span>

### <a name="problem-would-like-to-see-logs"></a><span data-ttu-id="0dc58-107">Problème : vous aimeriez voir les journaux</span><span class="sxs-lookup"><span data-stu-id="0dc58-107">Problem: Would like to see logs</span></span>
* <span data-ttu-id="0dc58-108">**Problème potentiel**: impossible de trouver des journaux de l’encodeur qui pourraient aider à déboguer des problèmes.</span><span class="sxs-lookup"><span data-stu-id="0dc58-108">**Potential issue**: Can't find encoder logs that might help in debugging issues.</span></span>
  
  * <span data-ttu-id="0dc58-109">**Telestream Wirecast** : les journaux se trouvent en général sous C:\Users\{nom_utilisateur}\AppData\Roaming\Wirecast\\</span><span class="sxs-lookup"><span data-stu-id="0dc58-109">**Telestream Wirecast**: You can usually find logs under C:\Users\{username}\AppData\Roaming\Wirecast\\</span></span> 
  * <span data-ttu-id="0dc58-110">**Elemental Live** : vous pouvez trouver des liens vers les journaux sur le portail de gestion.</span><span class="sxs-lookup"><span data-stu-id="0dc58-110">**Elemental Live**: You can find has links to logs on the management portal.</span></span> <span data-ttu-id="0dc58-111">Cliquez sur **Statistiques**, puis **Journaux**.</span><span class="sxs-lookup"><span data-stu-id="0dc58-111">Click on **Stats**, then **Logs**.</span></span> <span data-ttu-id="0dc58-112">Dans la page **Fichiers journaux**, vous trouvez une liste des journaux pour tous les éléments LiveEvent. Sélectionnez celui qui correspond à votre session active.</span><span class="sxs-lookup"><span data-stu-id="0dc58-112">On the **Log Files** page, you will see a list of logs for all the LiveEvent items; select the one matching your current session.</span></span> 
  * <span data-ttu-id="0dc58-113">**Flash Media Live Encoder** : vous pouvez trouver le **Répertoire des journaux...** en accédant à l’onglet **Journal d’encodage**.</span><span class="sxs-lookup"><span data-stu-id="0dc58-113">**Flash Media Live Encoder**: You can find the **Log Directory...** by navigating to the **Encoding Log** tab.</span></span>

### <a name="problem-there-is-no-option-for-outputting-a-progressive-stream"></a><span data-ttu-id="0dc58-114">Problème : il n’existe aucune option pour générer un flux progressif</span><span class="sxs-lookup"><span data-stu-id="0dc58-114">Problem: There is no option for outputting a progressive stream</span></span>
* <span data-ttu-id="0dc58-115">**Problème potentiel**: l’encodeur utilisé n’effectue pas de désentrelacement automatique.</span><span class="sxs-lookup"><span data-stu-id="0dc58-115">**Potential issue**: The encoder being used doesn't automatically deinterlace.</span></span> 
  
    <span data-ttu-id="0dc58-116">**Étapes de dépannage**: recherchez une option de désentrelacement dans l’interface de l’encodeur.</span><span class="sxs-lookup"><span data-stu-id="0dc58-116">**Troubleshooting steps**: Look for a de-interlacing option within the encoder interface.</span></span> <span data-ttu-id="0dc58-117">Une fois le désentrelacement activé, revérifiez les paramètres de sortie progressive.</span><span class="sxs-lookup"><span data-stu-id="0dc58-117">Once de-interlacing is enabled, check again for progressive output settings.</span></span> 

### <a name="problem-tried-several-encoder-output-settings-and-still-unable-to-connect"></a><span data-ttu-id="0dc58-118">Problème : vous avez essayé plusieurs paramètres de sortie d’encodeur et la connexion échoue encore.</span><span class="sxs-lookup"><span data-stu-id="0dc58-118">Problem: Tried several encoder output settings and still unable to connect.</span></span>
* <span data-ttu-id="0dc58-119">**Problème potentiel**: le canal d’encodage Azure n’a pas été réinitialisé correctement.</span><span class="sxs-lookup"><span data-stu-id="0dc58-119">**Potential issue**: Azure encoding channel was not properly reset.</span></span> 
  
    <span data-ttu-id="0dc58-120">**Étapes de dépannage** : vérifiez que l’encodeur ne transmet plus les données à AMS, arrêtez puis réinitialisez le canal.</span><span class="sxs-lookup"><span data-stu-id="0dc58-120">**Troubleshooting steps**: Make sure the encoder is no longer pushing to AMS, stop and reset the channel.</span></span> <span data-ttu-id="0dc58-121">Une fois le canal redémarré, essayez de connecter votre encodeur avec les nouveaux paramètres.</span><span class="sxs-lookup"><span data-stu-id="0dc58-121">Once running again, try connecting your encoder with the new settings.</span></span> <span data-ttu-id="0dc58-122">Si cela ne résout toujours pas le problème, essayez de créer un canal. Parfois, les canaux peuvent être endommagés après plusieurs tentatives infructueuses.</span><span class="sxs-lookup"><span data-stu-id="0dc58-122">If this still does not correct the issue, try creating a new channel entirely, sometimes channels can become corrupt after several failed attempts.</span></span>  
* <span data-ttu-id="0dc58-123">**Problème potentiel**: la taille de GOP ou les paramètres d’image clé ne sont pas optimaux.</span><span class="sxs-lookup"><span data-stu-id="0dc58-123">**Potential issue**: The GOP size or key frame settings are not optimal.</span></span> 
  
    <span data-ttu-id="0dc58-124">**Étapes de dépannage**: la taille de GOP ou l’intervalle d’image clé recommandé(e) est de deux secondes.</span><span class="sxs-lookup"><span data-stu-id="0dc58-124">**Troubleshooting steps**: Recommended GOP size or keyframe interval is 2 seconds.</span></span> <span data-ttu-id="0dc58-125">Certains encodeurs calculent ce paramètre en nombre d’images, tandis que d’autres utilisent des secondes.</span><span class="sxs-lookup"><span data-stu-id="0dc58-125">Some encoders calculate this setting in number of frames, while others use seconds.</span></span> <span data-ttu-id="0dc58-126">Par exemple : lors de la sortie de 30 i/s, la taille de GOP serait de 60 images, ce qui équivaut à deux secondes.</span><span class="sxs-lookup"><span data-stu-id="0dc58-126">For example: When outputting 30fps, the GOP size would be 60 frames, which is equivalent to 2 seconds.</span></span>  
* <span data-ttu-id="0dc58-127">**Problème potentiel**: des ports fermés bloquent le flux de données.</span><span class="sxs-lookup"><span data-stu-id="0dc58-127">**Potential issue**: Closed ports are blocking the stream.</span></span> 
  
    <span data-ttu-id="0dc58-128">**Étapes de dépannage**: lors de la diffusion en flux continu via RTMP, vérifiez les paramètres de pare-feu et/ou de proxy pour confirmer que les ports sortants 1935 et 1936 sont ouverts.</span><span class="sxs-lookup"><span data-stu-id="0dc58-128">**Troubleshooting steps**: When streaming via RTMP, check firewall and/or proxy settings to confirm that outbound ports 1935 and 1936 are open.</span></span> <span data-ttu-id="0dc58-129">Lorsque vous utilisez la diffusion en flux continu RTP, vérifiez que le port sortant 2010 est ouvert.</span><span class="sxs-lookup"><span data-stu-id="0dc58-129">When using RTP streaming, confirm that outbound port 2010 is open.</span></span> 

### <a name="problem-when-configuring-the-encoder-to-stream-with-the-rtp-protocol-there-is-no-place-to-enter-a-host-name"></a><span data-ttu-id="0dc58-130">Problème : lors de la configuration de l’encodeur pour la diffusion avec le protocole RTP, il n’y a aucun emplacement où entrer un nom d’hôte.</span><span class="sxs-lookup"><span data-stu-id="0dc58-130">Problem: When configuring the encoder to stream with the RTP protocol, there is no place to enter a host name.</span></span>
* <span data-ttu-id="0dc58-131">**Problème potentiel**: de nombreux encodeurs RTP n’autorisent pas les noms d’hôtes et une adresse IP doit être acquise.</span><span class="sxs-lookup"><span data-stu-id="0dc58-131">**Potential issue**: Many RTP encoders do not allow for host names, and an IP address will need to be acquired.</span></span>  
  
    <span data-ttu-id="0dc58-132">**Étapes de dépannage**: pour trouver l’adresse IP, ouvrez une invite de commandes sur n’importe quel ordinateur.</span><span class="sxs-lookup"><span data-stu-id="0dc58-132">**Troubleshooting steps**: To find the IP address, open a command prompt on any computer.</span></span> <span data-ttu-id="0dc58-133">Pour ce faire, dans Windows, ouvrez le lanceur Exécuter (touche Windows + R) et tapez « cmd ».</span><span class="sxs-lookup"><span data-stu-id="0dc58-133">To do this in Windows, open the Run launcher (WIN + R) and type “cmd” to open.</span></span>  
  
    <span data-ttu-id="0dc58-134">Une fois l’invite de commandes ouverte, tapez « Ping [nom_hôte_AMS] ».</span><span class="sxs-lookup"><span data-stu-id="0dc58-134">Once the command prompt is open, type "Ping [AMS Host Name]".</span></span> 
  
    <span data-ttu-id="0dc58-135">Vous pouvez obtenir le nom d’hôte en omettant le numéro de port de l’URL de réception Azure, comme illustré dans l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="0dc58-135">The host name can be derived by omitting the port number from the Azure Ingest URL, as highlighted in the following example:</span></span> 
  
    <span data-ttu-id="0dc58-136">rtp://test2-amstest009.rtp.channel.mediaservices.windows.net:2010/</span><span class="sxs-lookup"><span data-stu-id="0dc58-136">rtp://test2-amstest009.rtp.channel.mediaservices.windows.net:2010/</span></span> 
  
    ![FMLE](./media/media-services-fmle-live-encoder/media-services-fmle10.png)

> [!NOTE]
> <span data-ttu-id="0dc58-138">Si, après avoir suivi la procédure de dépannage, vous ne pouvez toujours pas diffuser en continu avec succès, envoyez un ticket de support en utilisant le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="0dc58-138">If after following the troubleshooting steps you still cannot successfully stream, submit a support ticket using the Azure portal.</span></span>
> 
> 

## <a name="media-services-learning-paths"></a><span data-ttu-id="0dc58-139">Parcours d’apprentissage de Media Services</span><span class="sxs-lookup"><span data-stu-id="0dc58-139">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="0dc58-140">Fournir des commentaires</span><span class="sxs-lookup"><span data-stu-id="0dc58-140">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

