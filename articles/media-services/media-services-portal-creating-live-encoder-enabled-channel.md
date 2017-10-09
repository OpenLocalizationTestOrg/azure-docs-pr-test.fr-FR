---
title: "aaaHow tooperform diffusion en continu à l’aide de flux de débits toocreate Azure Media Services avec hello portail Azure | Documents Microsoft"
description: "Parcours ce didacticiel vous guide dans les étapes de hello de création d’un canal qui reçoit un flux en direct à vitesse de transmission unique et qu’elle l’encode les flux de débits binaires toomulti à l’aide de hello portail Azure."
services: media-services
documentationcenter: 
author: anilmur
manager: cfowler
editor: 
ms.assetid: 504f74c2-3103-42a0-897b-9ff52f279e23
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/09/2017
ms.author: juliako
ms.openlocfilehash: 963a25b8ba4683a2ce34d9fb0e19499874b4707c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooperform-live-streaming-using-azure-media-services-toocreate-multi-bitrate-streams-with-hello-azure-portal"></a>Comment tooperform diffusion en continu à l’aide de débits toocreate d’Azure Media Services diffuse en continu avec hello portail Azure
> [!div class="op_single_selector"]
> * [Portail](media-services-portal-creating-live-encoder-enabled-channel.md)
> * [.NET](media-services-dotnet-creating-live-encoder-enabled-channel.md)
> * [API REST](https://docs.microsoft.com/rest/api/media/operations/channel)
> 
> 

Ce didacticiel vous guide tout au long des étapes hello de création d’un **canal** qui reçoit un flux en direct à vitesse de transmission unique et qu’elle l’encode les flux de débits binaires toomulti.

> [!NOTE]
> Pour plus d’informations conceptuelles tooChannels connexes qui sont activés pour l’encodage live, consultez [en continu à l’aide de flux de débits Azure Media Services toocreate](media-services-manage-live-encoder-enabled-channels.md).
> 
> 

## <a name="common-live-streaming-scenario"></a>Scénario courant de diffusion dynamique en continu
Hello Voici les étapes générales nécessaires à la création d’applications de diffusion en continu dynamiques communes.

> [!NOTE]
> Actuellement, hello maximum recommandé de durée d’un événement en direct est de 8 heures. Si vous avez besoin d’un canal de toorun pour de longues périodes, contactez amslived Microsoft.com.
> 
> 

1. Connecter un ordinateur de tooa caméra vidéo. Lancer et configurer un encodeur dynamique local qui peut afficher un flux à débit binaire unique dans un des hello suivant protocoles : RTMP, diffusion en continu lisse ou RTP (MPEG-TS). Pour plus d’informations, voir [Prise en charge RTMP et encodeurs dynamiques dans Azure Media Services](http://go.microsoft.com/fwlink/?LinkId=532824).
   
    Cette étape peut également être effectuée après la création du canal.
2. Créez et démarrez un canal. 
3. URL de réception récupérer hello canal. 
   
    URL de réception Hello est utilisé par hello encodeur en temps réel toosend hello flux toohello canal.
4. Récupérer l’URL d’aperçu hello canal. 
   
    Utilisez cette tooverify URL que votre canal reçoit correctement les flux live hello.
5. Créez un événement/programme (ce qui crée également un élément multimédia). 
6. Publier les événements hello (ce qui créeront un localisateur OnDemand pour un composant associé de hello).    
7. Démarrer l’événement hello lorsque vous êtes prêt toostart diffusion et l’archivage.
8. Si vous le souhaitez, encodeur en direct de hello peut être signalé toostart une publication. publication de Hello est insérée dans le flux de sortie hello.
9. Arrêter les événements hello chaque fois que vous souhaitez toostop de diffusion en continu et l’archivage des événements de hello.
10. Supprimer un événement de hello (et éventuellement supprimer actif de hello).   

## <a name="in-this-tutorial"></a>Dans ce didacticiel
Dans ce didacticiel, hello portail Azure est hello utilisé tooaccomplish tâches suivantes : 

1. Créer un canal qui est activé tooperform encodage dynamique.
2. Get hello URL de réception dans l’ordre toosupply il toolive encodeur. encodeur en direct de Hello utilisera ce flux de données URL tooingest hello en hello canal.
3. Créer un événement/programme (et un élément multimédia).
4. Publier l’élément multimédia de hello et obtenir l’URL de diffusion en continu.  
5. Lire votre contenu.
6. Nettoyage.

## <a name="prerequisites"></a>Composants requis
Hello Voici didacticiel de hello toocomplete requis.

* toocomplete ce didacticiel, vous avez besoin d’un compte Azure. Si vous ne possédez pas de compte, vous pouvez créer un compte d'évaluation gratuit en quelques minutes. 
  Pour plus d'informations, consultez la page [Version d'évaluation gratuite d'Azure](https://azure.microsoft.com/pricing/free-trial/).
* Un compte Media Services. toocreate un compte Media Services, consultez [créer un compte](media-services-portal-create-account.md).
* Une webcam et un encodeur capable d’envoyer un flux dynamique à débit binaire unique.

## <a name="create-a-channel"></a>Créer un canal
1. Bonjour [portail Azure](https://portal.azure.com/), sélectionnez le service de média, puis cliquez sur le nom de votre compte Media Services.
2. Sélectionnez **Vidéo en flux continu**.
3. Sélectionnez **Création personnalisée**. Cette option vous permet de créer un canal activé pour l’encodage live.
   
    ![Créer un CANAL](./media/media-services-portal-creating-live-encoder-enabled-channel/media-services-create-channel.png)
4. Cliquez sur **Paramètres**.
   
   1. Choisissez hello **encodage Live** type de canal. Ce type spécifie que vous souhaitez toocreate un canal qui est activé pour l’encodage live. Que signifie hello entrant à débit binaire unique flux est envoyé toohello canal et codée en un flux de débits à l’aide des paramètres de l’encodeur dynamique spécifié. Pour plus d’informations, consultez [en continu à l’aide de flux de débits Azure Media Services toocreate](media-services-manage-live-encoder-enabled-channels.md). Cliquez sur OK.
   2. Indiquez le nom d’un canal.
   3. Cliquez sur OK bas hello écran hello.
5. Sélectionnez hello **réception** onglet.
   
   1. Sur cette page, vous pouvez sélectionner un protocole de diffusion en continu. Pourquoi **encodage Live** sont de type de canal, les options de protocole valide :
      
      * MP4 fragmenté (Smooth Streaming) à débit binaire unique
      * RTMP à débit binaire unique
      * RTP (MPEG-TS) : flux de transport MPEG-2 via RTP.
        
        Pour obtenir une explication détaillée sur chaque protocole, consultez [en continu à l’aide de flux de débits Azure Media Services toocreate](media-services-manage-live-encoder-enabled-channels.md).
        
        Vous ne pouvez pas modifier option protocole hello hello canal ou ses événements/programmes associés sont en cours d’exécution. Si vous avez besoin d’autres protocoles, vous devez créer des canaux distincts pour chaque protocole de diffusion.  
   2. Vous pouvez appliquer des restrictions d’adresse IP sur hello de réception. 
      
       Vous pouvez définir hello IP adresses qui sont autorisées à tooingest un canal toothis vidéo. Les adresses IP autorisées peuvent être spécifiées en tant qu’adresses IP uniques (par exemple, '10.0.0.1'), une plage d’adresses IP utilisant une adresse IP et un masque de sous-réseau CIDR (par exemple, '10.0.0.1/22'), ou une plage d’adresses IP utilisant une adresse IP et un masque de sous-réseau décimal séparé par des points (par exemple, '10.0.0.1(255.255.252.0)').
      
       Si aucune adresse IP n’est spécifiée et qu’il n’existe pas de définition de règle, alors aucune adresse IP n’est autorisée. tooallow n’importe quelle adresse IP, créez une règle et définissez 0.0.0.0/0.
6. Sur hello **aperçu** onglet, appliquer des restrictions d’adresse IP sur la version préliminaire de hello.
7. Sur hello **codage** onglet, spécifiez la valeur prédéfinie d’encodage hello. 
   
    Actuellement, hello uniquement système prédéfini, vous pouvez sélectionner est **par défaut 720p**. toospecify personnalisé prédéfinies, ouvrez un ticket de support Microsoft. Ensuite, entrez le nom hello Hello présélection créée pour vous. 

> [!NOTE]
> Actuellement, le démarrage du canal hello peut prendre jusqu'à too30 minutes. Réinitialisation du canal peut prendre jusqu'à too5 minutes.
> 
> 

Une fois que vous avez créé le canal de hello, vous pouvez cliquer sur le canal de hello et sélectionnez **paramètres** où vous pouvez afficher vos configurations de canaux. 

Pour plus d’informations, consultez [en continu à l’aide de flux de débits Azure Media Services toocreate](media-services-manage-live-encoder-enabled-channels.md).

## <a name="get-ingest-urls"></a>Obtenir les URL de réception
Une fois que le canal de hello est créé, vous pouvez obtenir les URL que vous fournirez un encodeur en temps réel de toohello d’ingestion. encodeur de Hello utilise ces tooinput URL un flux en direct.

![ingesturls](./media/media-services-portal-creating-live-encoder-enabled-channel/media-services-ingest-urls.png)

## <a name="create-and-manage-events"></a>Créer et gérer des événements
### <a name="overview"></a>Vue d'ensemble
Un canal est associé à des événements/des programmes qui vous permettent de la publication toocontrol hello et stockage des segments dans un flux en direct. Les canaux gèrent des événements/programmes. Hello relation de canal et le programme est très similaire tootraditional média, où un canal possède un flux constant de contenu et un programme est événements étendue toosome a expiré sur le canal.

Vous pouvez spécifier le nombre de hello d’heures que vous souhaitez tooretain hello enregistrée contenu pour l’événement de hello en définissant un hello **fenêtre d’Archive** longueur. Cette valeur peut être définie à partir d’un minimum de 5 minutes tooa 25 heures maximum. Longueur de fenêtre d’archive détermine également hello durée maximale pendant laquelle les clients peuvent effectuer des recherches dans le temps à partir de la position de diffusion en continu hello actuel. Les événements peuvent s’exécuter sur la durée spécifiée hello, mais le contenu qui se trouve derrière la longueur de la fenêtre hello est ignoré en continu. La valeur de cette propriété détermine également la durée pendant laquelle hello client manifestes peuvent atteindre.

Chaque événement est associé à un élément multimédia. événement de hello toopublish vous devez créer un localisateur OnDemand pour hello associés actif. Ce localisateur activera toobuild une URL de diffusion en continu que vous pouvez fournir tooyour clients.

Un canal prend en charge jusqu'à toothree qui s’exécutent simultanément des événements, vous pouvez créer plusieurs archives de hello même flux entrant. Cela vous permet de toopublish et archivage de différentes parties d’un événement en fonction des besoins. Par exemple, vos exigences d’entreprise est tooarchive 6 heures d’un événement, mais toobroadcast uniquement les 10 dernières minutes. tooaccomplish, vous devez toocreate deux qui s’exécutent simultanément événement. Un événement a la valeur tooarchive d’événement de hello les 6 heures, mais les programme hello ne sont pas publié. Hello autre événement est ensemble tooarchive pendant 10 minutes et ce programme est publié.

Vous ne devez pas réutiliser de programmes existants pour de nouveaux événements. Créez et lancez plutôt un nouveau programme pour chaque événement.

Démarrage d’un événement/programme lorsque vous êtes prêt toostart diffusion et l’archivage. Arrêter les événements hello chaque fois que vous souhaitez toostop de diffusion en continu et l’archivage des événements de hello. 

contenu de toodelete archivé, arrêter et supprimer un événement de hello et supprimez actif associé de hello. Un élément multimédia ne peut pas être supprimé s’il est utilisé par l’événement de hello ; événement de Hello doit d’abord être supprimée. 

Même après l’arrêt et de supprimer un événement de hello, hello les utilisateurs serait en mesure de toostream votre contenu archivé comme une vidéo à la demande, pour tant que vous ne supprimez pas l’élément multimédia de hello.

Si vous souhaitez hello tooretain archivé le contenu, mais n’est pas le disponible pour la diffusion en continu, supprimez hello localisateur de diffusion en continu.

### <a name="createstartstop-events"></a>Créer/Démarrer/Arrêter des événements
Une fois que vous avez hello flux transitent par le canal de hello commencer hello de diffusion en continu d’événements en créant un élément multimédia, le programme et le localisateur de diffusion en continu. Cela archiver les flux hello et rendre tooviewers disponible via le point de terminaison de diffusion en continu de hello. 

>[!NOTE]
>Création de votre compte AMS un **par défaut** point de terminaison de diffusion en continu est ajoutée tooyour compte Bonjour **arrêté** état. toostart de diffusion en continu de votre contenu et profitez de l’empaquetage dynamique et chiffrement dynamique, hello de point de terminaison de diffusion en continu à partir de laquelle vous souhaitez que le contenu toostream a toobe Bonjour **en cours d’exécution** état. 

Il existe deux événements de toostart façons : 

1. À partir de hello **canal** page, appuyez sur **événement Live** tooadd un nouvel événement.
   
    Spécifiez le nom de l’événement, le nom de l’élément multimédia, la fenêtre d’archivage et l’option de chiffrement.
   
    ![createprogram](./media/media-services-portal-creating-live-encoder-enabled-channel/media-services-create-program.png)
   
    Si vous avez laissé **publier maintenant de cet événement en direct** activée, hello d’événement hello URL de publication est créée.
   
    Vous pouvez appuyer sur **Démarrer**, chaque fois que vous êtes l’événement de hello toostream prêt.
   
    Une fois que vous démarrez les événements hello, vous pouvez appuyer sur **espion** toostart lecture de contenu de hello.
2. Vous pouvez également utiliser un raccourci et le Presse **Go Live** bouton sur hello **canal** page. Un élément multimédia, un programme et un localisateur de diffusion en continu par défaut sont alors créés.
   
    l’événement Hello est appelé **par défaut** et de la fenêtre d’archive hello a la valeur too8 heures.

Vous pouvez regarder hello des événement publié depuis hello **direct** page. 

Si vous cliquez sur **Off Air**(Hors antenne), tous les événements en direct sont arrêtés. 

## <a name="watch-hello-event"></a>Événement de hello espion
événement de hello toowatch, cliquez sur **espion** hello Azure hello portail ou de copie URL de diffusion en continu et utilisez un lecteur de votre choix. 

![Date de création](./media/media-services-portal-creating-live-encoder-enabled-channel/media-services-play-event.png)

Événement en direct convertit automatiquement le contenu de la demande tooon des événements lors de l’arrêt.

## <a name="clean-up"></a>Nettoyer
Si vous avez terminé de diffusion en continu d’événements et que vous souhaitez tooclean les ressources hello configurés précédemment, suivez hello suivant la procédure.

* Arrêtez les envoi push de flux de données hello à partir de l’encodeur de hello.
* Arrêter le canal de hello. Une fois que le canal de hello est arrêté, il ne mobilise pas tous les frais. Lorsque vous devez toostart il à nouveau, il aura hello même URL de réception afin de vous n’aurez pas tooreconfigure votre encodeur.
* Vous pouvez arrêter votre point de terminaison de diffusion en continu, sauf si vous souhaitez archiver de hello toocontinue tooprovide de votre événement en direct comme un flux à la demande. Si le canal de hello est arrêté, il ne mobilise pas tous les frais.

## <a name="view-archived-content"></a>Afficher le contenu archivé
Même après l’arrêt et de supprimer un événement de hello, hello les utilisateurs serait en mesure de toostream votre contenu archivé comme une vidéo à la demande, pour tant que vous ne supprimez pas l’élément multimédia de hello. Un élément multimédia ne peut pas être supprimé s’il est utilisé par un événement ; événement de Hello doit d’abord être supprimée. 

sélectionner de vos éléments multimédias, toomanage **paramètre** et cliquez sur **actifs**.

![Éléments multimédias](./media/media-services-portal-creating-live-encoder-enabled-channel/media-services-assets.png)

## <a name="considerations"></a>Considérations
* Actuellement, hello maximum recommandé de durée d’un événement en direct est de 8 heures. Si vous avez besoin d’un canal de toorun pour de longues périodes, contactez amslived Microsoft.com.
* Vérifiez que hello de diffusion en continu de point de terminaison à partir de laquelle vous souhaitez toostream votre contenu est Bonjour **en cours d’exécution** état.

## <a name="next-step"></a>Étape suivante
Consultez les parcours d’apprentissage de Media Services.

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fournir des commentaires
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

