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
# <a name="troubleshooting-guide-for-live-streaming"></a>Guide de dépannage de la vidéo en flux continu
Cette rubrique offre des suggestions sur la façon de tootroubleshoot dynamique de certains problèmes de diffusion en continu.

## <a name="issues-related-tooon-premises-encoders"></a>Les problèmes liés à des encodeurs de tooon local
Cette section fournit des suggestions de tootroubleshoot des problèmes connexes tooon local encodeurs qui sont configurés toosend un canaux tooAMS de flux à débit binaire unique qui est activés pour l’encodage live.

### <a name="problem-would-like-toosee-logs"></a>Problème : Aimeriez toosee journaux
* **Problème potentiel**: impossible de trouver des journaux de l’encodeur qui pourraient aider à déboguer des problèmes.
  
  * **Telestream Wirecast** : les journaux se trouvent en général sous C:\Users\{nom_utilisateur}\AppData\Roaming\Wirecast\ 
  * **Live élémentaire**: vous trouverez a des liens toologs sur le portail de gestion hello. Cliquez sur **Statistiques**, puis **Journaux**. Sur hello **des fichiers journaux** page, vous verrez une liste de tous les journaux hello des éléments de l’événement en direct ; sélectionnez hello une correspondant à votre session actuelle. 
  * **Flash Media Encoder de Live**: vous trouverez hello **répertoire du journal en cours...**  en naviguant toohello **journal de codage** onglet.

### <a name="problem-there-is-no-option-for-outputting-a-progressive-stream"></a>Problème : il n’existe aucune option pour générer un flux progressif
* **Problème potentiel**: encodeur hello utilisé ne désentrelacer automatiquement. 
  
    **Étapes de dépannage**: recherchez une option de désentrelacement dans l’interface d’encodeur hello. Une fois le désentrelacement activé, revérifiez les paramètres de sortie progressive. 

### <a name="problem-tried-several-encoder-output-settings-and-still-unable-tooconnect"></a>Problème : A tenté de plusieurs paramètres de sortie l’encodeur et tooconnect toujours pas.
* **Problème potentiel**: le canal d’encodage Azure n’a pas été réinitialisé correctement. 
  
    **Étapes de dépannage**: Assurez-vous qu’encodeur de hello n’est plus repousse tooAMS, arrêter et réinitialiser le canal de hello. Une fois en cours d’exécution, essayez de connecter votre encodeur avec les nouveaux paramètres de hello. Si cela ne résout toujours pas de problème de hello, essayez de créer un nouveau canal entièrement, parfois, les canaux peuvent être endommagés après que plusieurs tentatives infructueuses.  
* **Problème potentiel**: taille de GOP hello ou les paramètres de l’image clé ne sont pas optimaux. 
  
    **Étapes de dépannage**: la taille de GOP ou l’intervalle d’image clé recommandé(e) est de deux secondes. Certains encodeurs calculent ce paramètre en nombre d’images, tandis que d’autres utilisent des secondes. Par exemple : lors de la sortie à 30 i/s, hello taille de GOP serait 60 frames, qui est équivalent too2 secondes.  
* **Problème potentiel**: ports fermés bloquent les flux hello. 
  
    **Étapes de dépannage**: lors de la diffusion en continu via le protocole RTMP, vérifiez le pare-feu et/ou tooconfirm de paramètres de proxy que les ports de sortie 1935 et 1936 sont ouverts. Lorsque vous utilisez la diffusion en flux continu RTP, vérifiez que le port sortant 2010 est ouvert. 

### <a name="problem-when-configuring-hello-encoder-toostream-with-hello-rtp-protocol-there-is-no-place-tooenter-a-host-name"></a>Problème : Lorsque vous configurez hello encodeur toostream hello protocole RTP, il n’est pas tooenter un nom d’hôte.
* **Problème potentiel**: les encodeurs de nombreux RTP ne permettent pas de noms d’hôte et une adresse IP doit toobe acquis.  
  
    **Étapes de dépannage**: toofind hello d’adresse IP, ouvrez une invite de commande sur n’importe quel ordinateur. toodo dans Windows, ouvrez hello Lanceur d’exécution (WIN + R) et tapez « cmd » tooopen.  
  
    Une fois que l’invite de commandes hello est ouvert, tapez « Ping [nom d’hôte de AMS] ». 
  
    nom d’hôte Hello peut être dérivée en omettant le numéro du port hello de hello Azure URL de réception, mise en évidence dans hello l’exemple suivant : 
  
    rtp://test2-amstest009.rtp.channel.mediaservices.windows.net:2010/ 
  
    ![FMLE](./media/media-services-fmle-live-encoder/media-services-fmle10.png)

> [!NOTE]
> Si après avoir appliqué les étapes de dépannage hello que vous toujours ne peut pas diffuser en continu, envoyer un ticket de support à l’aide de hello portail Azure.
> 
> 

## <a name="media-services-learning-paths"></a>Parcours d’apprentissage de Media Services
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fournir des commentaires
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

