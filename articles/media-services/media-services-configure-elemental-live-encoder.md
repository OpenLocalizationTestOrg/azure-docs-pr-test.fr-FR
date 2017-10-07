---
title: "aaaConfigure hello toosend d’encodeur Live élémentaire un flux à débit binaire unique en continu | Documents Microsoft"
description: "Cette rubrique montre comment tooconfigure hello toosend d’encodeur Live élémentaire un canaux tooAMS de flux à débit binaire unique qui est activés pour l’encodage live."
services: media-services
documentationcenter: 
author: cenkdin
manager: cfowler
editor: 
ms.assetid: 9c6bf6a9-6273-4fdd-9477-f0e565280b5b
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: ne
ms.topic: article
ms.date: 01/05/2017
ms.author: cenkd;anilmur;juliako
ms.openlocfilehash: 9a5de6189bfb123768a9da038b8c8db69cf85e91
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-elemental-live-encoder-toosend-a-single-bitrate-live-stream"></a>Utilisez hello Live élémentaire encodeur toosend un flux à débit binaire unique en continu.
> [!div class="op_single_selector"]
> * [Elemental Live](media-services-configure-elemental-live-encoder.md)
> * [Tricaster](media-services-configure-tricaster-live-encoder.md)
> * [Wirecast](media-services-configure-wirecast-live-encoder.md)
> * [FMLE](media-services-configure-fmle-live-encoder.md)
>
>

Cette rubrique montre comment tooconfigure hello [Live élémentaire](http://www.elementaltechnologies.com/products/elemental-live) encodeur toosend canaux tooAMS qui sont activés pour l’encodage live de diffuser un débit binaire unique.  Pour plus d’informations, consultez [utilisation de canaux est à activé tooPerform Live encodage avec Azure Media Services](media-services-manage-live-encoder-enabled-channels.md).

Ce didacticiel montre comment toomanage Azure Media Services (AMS) avec l’outil d’Azure Media Services Explorer (AMSE). Cet outil est uniquement compatible avec les PC Windows. Si vous êtes sur le Mac ou Linux, utilisez hello toocreate portail Azure [canaux](media-services-portal-creating-live-encoder-enabled-channel.md#create-a-channel) et [programmes](media-services-portal-creating-live-encoder-enabled-channel.md).

## <a name="prerequisites"></a>Composants requis
* Doit avoir une connaissance pratique de l’utilisation de Live élémentaire web interface toocreate événements en direct.
* [Créer un compte Azure Media Services](media-services-portal-create-account.md)
* Vérifiez qu’un point de terminaison de streaming est en cours d’exécution. Pour plus d’informations, consultez la rubrique [Gestion des points de terminaison de diffusion en continu dans un compte Media Services](media-services-portal-manage-streaming-endpoints.md).
* Installer la version la plus récente de hello hello [AMSE](https://github.com/Azure/Azure-Media-Services-Explorer) outil.
* Lancer l’outil de hello et tooyour AMS compte de connexion.

## <a name="tips"></a>Conseils
* Si possible, utilisez une connexion Internet câblée.
* Une règle empirique lors de la détermination de la bande passante est hello toodouble débits binaires de diffusion en continu. Alors que cela n’est pas obligatoire, il vous aide à atténuer l’impact hello de congestion du réseau.
* Lors de l’utilisation d’encodeurs logiciels, fermez tous les programmes inutiles.

## <a name="elemental-live-with-rtp-ingest"></a>Elemental Live avec réception RTP
Cette section montre comment encoder de Live élémentaire tooconfigure hello qui envoie un débit binaire unique flux dynamique sur RTP.  Pour plus d’informations, consultez la rubrique [Flux MPEG-TS via RTP](media-services-manage-live-encoder-enabled-channels.md#channel).

### <a name="create-a-channel"></a>Créer un canal

1. Dans l’outil AMSE hello, accédez à toohello **Live** onglet et cliquez avec le bouton droit dans la zone de canal hello. Dans le menu qui s’affiche, sélectionnez **Créer un canal...** à partir du menu de hello.

    ![Elemental](./media/media-services-elemental-live-encoder/media-services-elemental1.png)

2. Spécifiez un nom de canal, champ de description hello est facultatif. Sous paramètres de canal, sélectionnez **Standard** pour hello option d’encodage Live, avec hello entrée protocole défini trop**RTP (MPEG-TS)**. Vous pouvez laisser tous les autres paramètres inchangés.

    Vérifiez que hello **début hello nouveau canal maintenant** est sélectionnée.

3. Cliquez sur **Créer un canal**.

   ![Elemental](./media/media-services-elemental-live-encoder/media-services-elemental12.png)

> [!NOTE]
> canal de Hello peut prendre jusqu'à 20 minutes toostart.
>
>

Pendant le démarrage du canal de hello, vous pouvez [configurer l’encodeur de hello](media-services-configure-elemental-live-encoder.md#configure_elemental_rtp).

> [!IMPORTANT]
> Notez que la facturation commence dès que l’état du canal indique qu’il est prêt à être utilisé. Pour plus d’informations, consultez [États du canal](media-services-manage-live-encoder-enabled-channels.md#states).
>
>

### <a id=configure_elemental_rtp></a>Configurer l’encodeur Live élémentaire de hello
Dans ce didacticiel hello des paramètres de sortie suivants sont utilisés. Hello le reste de cette section décrit les étapes de configuration plus en détail.

**Vidéo**:

* Codec : H.264
* Profil : Élevé (niveau 4.0)
* Débit binaire : 5 000 kbit/s
* Image clé : 2 secondes (60 secondes)
* Fréquence d’images : 30

**Audio**:

* Codec : AAC (LC)
* Débit binaire : 192 kbit/s
* Taux d’échantillonnage : 44,1 kHz

#### <a name="configuration-steps"></a>Configuration
1. Accédez toohello **Live élémentaire** interface web et configurer encodeur hello pour **UDP/TS** de diffusion en continu.
2. Une fois qu’un nouvel événement est créé, faites défiler la liste des groupes de sorties toohello et ajouter hello **UDP/TS** le groupe de sorties.
3. Créez une nouvelle sortie en sélectionnant **New Stream**, puis en cliquant sur **Add Output**.  

    ![Elemental](./media/media-services-elemental-live-encoder/media-services-elemental13.png)

   > [!NOTE]
   > Il est recommandé que l’événement élémentaire hello a timecode hello défini trop encodeur de « L’horloge système » toohelp hello reconnecter dans les cas de hello d’une erreur de flux de données.
   >
   >
4. Maintenant que hello sortie a été créée, cliquez sur **d’ajouter un flux**. paramètres de sortie Hello peuvent maintenant être configurés.
5. Faites défiler la liste toohello « Stream 1 » qui vient d’être créé, cliquez sur hello **vidéo** onglet hello gauche et développez hello **avancé** section de paramètres.

    ![Elemental](./media/media-services-elemental-live-encoder/media-services-elemental4.png)

    Alors que Live élémentaire a une grande variété de personnalisation disponibles, hello paramètres suivants sont recommandés pour la mise en route de tooAMS de diffusion en continu.

   * Resolution : 1280 x 720
   * Framerate : 30
   * GOP Size : 60 frames
   * Interlace Mode : Progressive
   * Bitrate : 5000000 bit/s (cette valeur peut être ajustée en fonction des limitations du réseau)

    ![Elemental](./media/media-services-elemental-live-encoder/media-services-elemental5.png)

1. Obtient les URL d’entrée du canal hello.

    Accédez outil AMSE toohello précédent et vérifier l’état d’achèvement canal hello. Une fois que l’état de hello a été modifié à partir de **départ** trop**en cours d’exécution**, vous pouvez obtenir les URL d’entrée hello.

    Lorsque le canal de hello est en cours d’exécution, cliquez avec le bouton droit sur nom de la chaîne hello, naviguez vers le bas toohover sur **tooclipboard de copier l’URL entrée** , puis sélectionnez **URL entrée principale**.  

    ![Elemental](./media/media-services-elemental-live-encoder/media-services-elemental6.png)
2. Coller ces informations dans hello **Destination primaire** champ hello élémentaire. Tous les autres paramètres peuvent rester par défaut de hello.

    ![Elemental](./media/media-services-elemental-live-encoder/media-services-elemental14.png)

    Pour assurer la redondance supplémentaire, répétez ces étapes avec hello secondaire URL d’entrée en créant un onglet séparé de « Sortie » pour la diffusion en continu UDP/TS.
3. Cliquez sur **créer** (si un nouvel événement a été créé) ou **mise à jour** (si la modification d’un événement existant), puis continuez encodeur de hello toostart.

> [!IMPORTANT]
> Avant de cliquer sur **Démarrer** sur l’interface web Live élémentaire hello, vous **doit** vous assurer que le canal de hello est prêt.
> Assurez-vous également que pas tooleave hello canal dans un état prêt sans un événement pendant plus de 15 minutes >.
>
>

Une fois le flux de données hello s’exécute pendant 30 secondes, accédez toohello arrière AMSE outil et test de la lecture.  

### <a name="test-playback"></a>Tester la lecture

Accédez outil AMSE toohello et cliquez avec le bouton droit sur toobe de canal hello testé. À partir du menu de hello, placez le curseur sur **hello de lecture aperçu** et sélectionnez **avec Azure Media Player**.  

    ![Elemental](./media/media-services-elemental-live-encoder/media-services-elemental8.png)

Si le flux de données hello s’affiche dans le lecteur hello, encodeur de hello a été correctement configuré tooconnect tooAMS.

Si une erreur est reçue, le canal de hello devez paramètres d’encodeur et de réinitialisation toobe ajustées. Consultez hello [dépannage](media-services-troubleshooting-live-streaming.md) rubrique pour obtenir des conseils.   

### <a name="create-a-program"></a>Créer un programme
1. Une fois que vous avez vérifié que la lecture fonctionne sur le canal, créez un programme. Sous hello **Live** onglet dans l’outil AMSE hello, cliquez avec le bouton droit dans la zone du programme hello et sélectionnez **créer un nouveau programme**.  

    ![Elemental](./media/media-services-elemental-live-encoder/media-services-elemental9.png)
2. Nom de programme de hello et, si nécessaire, ajustez hello **longueur de fenêtre d’Archive** (heures de too4 les valeurs par défaut). Vous pouvez également spécifier un emplacement de stockage ou les conserver en tant que valeur par défaut hello.  
3. Vérifiez hello **maintenant démarrer hello programme** boîte.
4. Cliquez sur **Créer le programme**.  

    >[!NOTE]
    > La création d’un programme prend moins de temps que la création d’un canal.   
      
5. Une fois l’exécution du programme hello, confirmer la lecture en cliquant avec le bouton droit sur un programme hello et en naviguant trop**lecture hello programmes** , puis en sélectionnant **avec Azure Media Player**.  
6. Après confirmation, cliquez à nouveau programme de hello, puis sélectionnez **copier hello URL de sortie tooClipboard** (ou en extraire ces informations hello **informations et des paramètres du programme** option de menu de hello).

Hello flux est maintenant prêt toobe incorporé dans un lecteur ou public tooan distribuée pour live affichage.  

## <a name="troubleshooting"></a>Résolution des problèmes
Consultez hello [dépannage](media-services-troubleshooting-live-streaming.md) rubrique pour obtenir des conseils.

## <a name="media-services-learning-paths"></a>Parcours d’apprentissage de Media Services
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fournir des commentaires
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
