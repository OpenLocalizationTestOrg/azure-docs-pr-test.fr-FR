---
title: "flux aaaLive avec des encodeurs locaux à l’aide de hello portail Azure | Documents Microsoft"
description: "Ce didacticiel vous guide tout au long des étapes de hello de création d’un canal qui est configuré pour une livraison directe."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 6f4acd95-cc64-4dd9-9e2d-8734707de326
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/09/2017
ms.author: juliako
ms.openlocfilehash: 1fb341e022f66f33903e13e07d3e84c0216cad77
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooperform-live-streaming-with-on-premises-encoders-using-hello-azure-portal"></a>Comment tooperform diffusion en continu avec local encodeurs à l’aide de hello portail Azure
> [!div class="op_single_selector"]
> * [Portail](media-services-portal-live-passthrough-get-started.md)
> * [.NET](media-services-dotnet-live-encode-with-onpremises-encoders.md)
> * [REST](https://docs.microsoft.com/rest/api/media/operations/channel)
> 
> 

Ce didacticiel vous guide tout au long des étapes hello de l’utilisation de hello toocreate portail Azure un **canal** qui est configuré pour une livraison directe. 

## <a name="prerequisites"></a>Composants requis
Hello Voici didacticiel de hello toocomplete requis :

* Un compte Azure. Pour plus d'informations, consultez la page [Version d'évaluation gratuite d'Azure](https://azure.microsoft.com/pricing/free-trial/). 
* Un compte Media Services. toocreate un compte Media Services, consultez [comment tooCreate un compte Media Services](media-services-portal-create-account.md).
* Une webcam. Par exemple, un [encodeur Telestream Wirecast](http://www.telestream.net/wirecast/overview.htm).

Il est fortement recommandé hello tooreview suivant des articles :

* [Prise en charge RTMP et encodeurs dynamiques dans Azure Media Services.](https://azure.microsoft.com/blog/2014/09/18/azure-media-services-rtmp-support-and-live-encoders/)
* [Vue d’ensemble de la vidéo en flux continu à l’aide d’Azure Media Services](media-services-manage-channels-overview.md)
* [Streaming en direct avec des encodeurs en local qui créent des flux multidébits](media-services-live-streaming-with-onprem-encoders.md)

## <a id="scenario"></a>Scénario courant de streaming en direct
Hello étapes suivantes décrivent les tâches impliquées dans la création d’applications de diffusion en continu live courants qui utilisent des canaux qui sont configurés pour la remise pass-through. Ce didacticiel montre comment toocreate et gérer un canal direct et les événements en direct.

>[!NOTE]
>Vérifiez que hello point de terminaison à partir de laquelle vous souhaitez toostream contenu de diffusion en continu est Bonjour **en cours d’exécution** état. 
    
1. Connecter un ordinateur de tooa caméra vidéo. Lancez et configurez un encodeur dynamique local qui produit un flux à débit binaire multiple au format MP4 fragmenté ou RTMP. Pour plus d’informations, voir [Prise en charge RTMP et encodeurs dynamiques dans Azure Media Services](http://go.microsoft.com/fwlink/?LinkId=532824).
   
    Cette étape peut également être effectuée après la création du canal.
2. Créez et démarrez un canal direct.
3. URL de réception récupérer hello canal. 
   
    URL de réception Hello est utilisé par hello encodeur en temps réel toosend hello flux toohello canal.
4. Récupérer l’URL d’aperçu hello canal. 
   
    Utilisez cette tooverify URL que votre canal reçoit correctement les flux live hello.
5. Créez un événement/programme en direct. 
   
    Lors de l’aide de hello portail Azure, création d’un événement en direct crée également un élément multimédia. 

6. Démarrez hello événement/programme lorsque vous êtes prêt toostart diffusion et l’archivage.
7. Si vous le souhaitez, encodeur en direct de hello peut être signalé toostart une publication. publication de Hello est insérée dans le flux de sortie hello.
8. Arrêter/programme hello d’événement chaque fois que vous souhaitez toostop de diffusion en continu et l’archivage des événements de hello.
9. Supprimer hello événement/programme (et éventuellement supprimer actif de hello).     

> [!IMPORTANT]
> Passez en revue [la diffusion en continu en direct avec les encodeurs locaux qui créent des flux de débits](media-services-live-streaming-with-onprem-encoders.md) toolearn sur les concepts et les considérations liées à la diffusion en continu toolive avec les canaux directs et les encodeurs locaux.
> 
> 

## <a name="tooview-notifications-and-errors"></a>erreurs et les notifications de tooview
Si vous souhaitez que les notifications de tooview et les erreurs générées par hello portail Azure, cliquez sur l’icône de Notification hello.

![Notifications](./media/media-services-portal-passthrough-get-started/media-services-notifications.png)

## <a name="create-and-start-pass-through-channels-and-events"></a>Créer et démarrer des canaux directs et des événements
Un canal est associé à des événements/des programmes qui vous permettent de la publication toocontrol hello et stockage des segments dans un flux en direct. Les canaux gèrent des événements. 

Vous pouvez spécifier le nombre de hello d’heures que vous voulez tooretain hello enregistrée contenu pour le programme de hello en définissant un hello **fenêtre d’Archive** longueur. Cette valeur peut être définie à partir d’un minimum de 5 minutes tooa 25 heures maximum. Longueur de fenêtre d’archive détermine également hello durée maximale pendant laquelle les clients peuvent effectuer des recherches dans le temps à partir de la position de diffusion en continu hello actuel. Les événements peuvent s’exécuter sur la durée spécifiée hello, mais le contenu qui se trouve derrière la longueur de la fenêtre hello est ignoré en continu. La valeur de cette propriété détermine également la durée pendant laquelle hello client manifestes peuvent atteindre.

Chaque événement est associé à un élément multimédia. événement de hello toopublish, vous devez créer un localisateur OnDemand pour un composant de hello associé. Ce localisateur permet toobuild une URL de diffusion en continu que vous pouvez fournir tooyour clients.

Un canal prend en charge jusqu'à toothree qui s’exécutent simultanément des événements, vous pouvez créer plusieurs archives de hello même flux entrant. Cela vous permet de toopublish et archivage de différentes parties d’un événement en fonction des besoins. Par exemple, vos exigences d’entreprise est tooarchive 6 heures d’un programme, mais toobroadcast uniquement les 10 dernières minutes. tooaccomplish, vous devez toocreate deux des programmes qui s’exécutent simultanément. Un programme a la valeur tooarchive d’événement de hello les 6 heures, mais les programme hello ne sont pas publié. Hello autre programme est ensemble tooarchive pendant 10 minutes et ce programme est publié.

Vous ne devez pas réutiliser d’événements en direct existants. Créez et lancez plutôt un nouvel événement pour chaque événement.

Démarrer l’événement hello lorsque vous êtes prêt toostart diffusion et l’archivage. Arrêter le programme de hello chaque fois que vous souhaitez toostop de diffusion en continu et l’archivage des événements de hello. 

contenu de toodelete archivé, arrêter et supprimer un événement de hello et supprimez actif associé de hello. Un élément multimédia ne peut pas être supprimé s’il est utilisé par un événement ; événement de Hello doit d’abord être supprimée. 

Même après l’arrêt et de supprimer un événement de hello, hello les utilisateurs serait en mesure de toostream votre contenu archivé comme une vidéo à la demande, pour tant que vous ne supprimez pas l’élément multimédia de hello.

Si vous souhaitez hello tooretain archivé le contenu, mais n’est pas le disponible pour la diffusion en continu, supprimez hello localisateur de diffusion en continu.

### <a name="toouse-hello-portal-toocreate-a-channel"></a>toouse hello toocreate portail un canal
Cette section montre comment toouse hello **création rapide** option toocreate un canal direct.

Pour plus d’informations sur les canaux directs, consultez [Streaming en direct avec des encodeurs locaux qui créent des flux multidébits](media-services-live-streaming-with-onprem-encoders.md).

1. Bonjour [portail Azure](https://portal.azure.com/), sélectionnez votre compte Azure Media Services.
2. Bonjour **paramètres** fenêtre, cliquez sur **diffusion en continu**. 
   
    ![Prise en main](./media/media-services-portal-passthrough-get-started/media-services-getting-started.png)
   
    Hello **continu** fenêtre s’affiche.
3. Cliquez sur **création rapide** toocreate un canal direct avec hello RTMP protocole de réception.
   
    Hello **créer un nouveau canal** fenêtre s’affiche.
4. Donnez un nom à nouveau canal de hello et cliquez sur **créer**. 
   
    Cela crée un canal direct avec hello protocole de réception RTMP.

## <a name="create-events"></a>Créer des événements
1. Sélectionnez un toowhich de canal que vous voulez tooadd un événement.
2. Appuyez sur le bouton **Événement réel** .

![Événement](./media/media-services-portal-passthrough-get-started/media-services-create-events.png)

## <a name="get-ingest-urls"></a>Obtenir les URL de réception
Une fois que le canal de hello est créé, vous pouvez obtenir les URL que vous fournirez un encodeur en temps réel de toohello d’ingestion. encodeur de Hello utilise ces tooinput URL un flux en direct.

![Date de création](./media/media-services-portal-passthrough-get-started/media-services-channel-created.png)

## <a name="watch-hello-event"></a>Événement de hello espion
événement de hello toowatch, cliquez sur **espion** hello Azure hello portail ou de copie URL de diffusion en continu et utilisez un lecteur de votre choix. 

![Date de création](./media/media-services-portal-passthrough-get-started/media-services-default-event.png)

Événement en direct obtiennent automatiquement le contenu de la demande tooon converti lors de l’arrêt.

## <a name="clean-up"></a>Nettoyer
Pour plus d’informations sur les canaux directs, consultez [Streaming en direct avec des encodeurs locaux qui créent des flux multidébits](media-services-live-streaming-with-onprem-encoders.md).

* Un canal peut être arrêté uniquement lorsque tous les événements de programmes sur un canal de hello ont été arrêtés.  Une fois que le canal de hello est arrêtée, elle n’entraîne pas de tous les frais. Lorsque vous devez toostart il à nouveau, il aura hello même URL de réception afin de vous n’aurez pas tooreconfigure votre encodeur.
* Un canal peut être supprimé uniquement lorsque tous les événements en direct sur le canal de hello ont été supprimés.

## <a name="view-archived-content"></a>Afficher le contenu archivé
Même après l’arrêt et de supprimer un événement de hello, hello les utilisateurs serait en mesure de toostream votre contenu archivé comme une vidéo à la demande, pour tant que vous ne supprimez pas l’élément multimédia de hello. Un élément multimédia ne peut pas être supprimé s’il est utilisé par un événement ; événement de Hello doit d’abord être supprimée. 

sélectionner de vos éléments multimédias, toomanage **paramètre** et cliquez sur **actifs**.

![Éléments multimédias](./media/media-services-portal-passthrough-get-started/media-services-assets.png)

## <a name="next-step"></a>Étape suivante
Consultez les parcours d’apprentissage de Media Services.

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fournir des commentaires
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

