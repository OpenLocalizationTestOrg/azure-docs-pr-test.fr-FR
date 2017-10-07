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
# <a name="use-hello-wirecast-encoder-toosend-a-single-bitrate-live-stream"></a>Utilisez hello Wirecast encodeur toosend un flux à débit binaire unique en continu.
> [!div class="op_single_selector"]
> * [Wirecast](media-services-configure-wirecast-live-encoder.md)
> * [Elemental Live](media-services-configure-elemental-live-encoder.md)
> * [Tricaster](media-services-configure-tricaster-live-encoder.md)
> * [FMLE](media-services-configure-fmle-live-encoder.md)
>
>

Cette rubrique montre comment tooconfigure hello [Telestream Wirecast](http://www.telestream.net/wirecast/overview.htm) live encodeur toosend un canaux tooAMS de flux à débit binaire unique qui est activés pour l’encodage live.  Pour plus d’informations, consultez [utilisation de canaux est à activé tooPerform Live encodage avec Azure Media Services](media-services-manage-live-encoder-enabled-channels.md).

Ce didacticiel montre comment toomanage Azure Media Services (AMS) avec l’outil d’Azure Media Services Explorer (AMSE). Cet outil est uniquement compatible avec les PC Windows. Si vous êtes sur le Mac ou Linux, utilisez hello toocreate portail Azure [canaux](media-services-portal-creating-live-encoder-enabled-channel.md#create-a-channel) et [programmes](media-services-portal-creating-live-encoder-enabled-channel.md).

## <a name="prerequisites"></a>Composants requis
* [Créer un compte Azure Media Services](media-services-portal-create-account.md)
* Vérifiez qu’un point de terminaison de streaming est en cours d’exécution. Pour plus d’informations, consultez [Gestion des points de terminaison de diffusion en continu dans un compte Media Services](media-services-portal-manage-streaming-endpoints.md)
* Installer la version la plus récente de hello hello [AMSE](https://github.com/Azure/Azure-Media-Services-Explorer) outil.
* Lancer l’outil de hello et tooyour AMS compte de connexion.

## <a name="tips"></a>Conseils
* Si possible, utilisez une connexion Internet câblée.
* Une règle empirique lors de la détermination de la bande passante est hello toodouble débits binaires de diffusion en continu. Alors que cela n’est pas obligatoire, il vous aide à atténuer l’impact hello de congestion du réseau.
* Lors de l’utilisation d’encodeurs logiciels, fermez tous les programmes inutiles.

## <a name="create-a-channel"></a>Créer un canal
1. Dans l’outil AMSE hello, accédez à toohello **Live** onglet et cliquez avec le bouton droit dans la zone de canal hello. Dans le menu qui s’affiche, sélectionnez **Créer un canal...** à partir du menu de hello.

    ![Wirecast](./media/media-services-wirecast-live-encoder/media-services-wirecast1.png)

2. Spécifiez un nom de canal, champ de description hello est facultatif. Sous paramètres de canal, sélectionnez **Standard** pour hello option d’encodage Live, avec hello entrée protocole défini trop**RTMP**. Vous pouvez laisser tous les autres paramètres inchangés.

    Vérifiez que hello **début hello nouveau canal maintenant** est sélectionnée.

3. Cliquez sur **Créer un canal**.

   ![Wirecast](./media/media-services-wirecast-live-encoder/media-services-wirecast2.png)

> [!NOTE]
> canal de Hello peut prendre jusqu'à 20 minutes toostart.
>
>

Pendant le démarrage du canal de hello, vous pouvez [configurer l’encodeur de hello](media-services-configure-wirecast-live-encoder.md#configure_wirecast_rtmp).

> [!IMPORTANT]
> Notez que la facturation commence dès que l’état du canal indique qu’il est prêt à être utilisé. Pour plus d’informations, consultez [États du canal](media-services-manage-live-encoder-enabled-channels.md#states).
>
>

## <a id=configure_wirecast_rtmp></a>Configurer hello encodeur Telestream Wirecast
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

### <a name="configuration-steps"></a>Configuration
1. Ouvrez l’application de Telestream Wirecast de hello sur la machine hello utilisé et configuré pour la diffusion en continu du contenu RTMP.
2. Configurer la sortie de hello en naviguant toohello **sortie** onglet et en sélectionnant **les paramètres de sortie...** .

    Vérifiez que hello **Destination de sortie** est défini trop**serveur RTMP**.
3. Cliquez sur **OK**.
4. Sur la page de paramètres hello, définissez hello **Destination** champ toobe **Azure Media Services**.

    Hello profil d’encodage est présélectionnée trop**Azure H.264 720 p 16:9 (1280 x 720)**. toocustomize ces paramètres, sélectionnez hello ENGRENAGE icône toohello à droite de hello liste déroulante, puis choisissez **prédéfini nouvelle**.

    ![Wirecast](./media/media-services-wirecast-live-encoder/media-services-wirecast3.png)
5. Configurez les présélections de l’encodeur.

    Nom Bonjour prédéfini et vérifier les paramètres recommandés de hello suivants :

    **Vidéo**

   * Encodeur : MainConcept H.264
   * Images par seconde : 30
   * Débit binaire moyen : 5 000 Kbit/s (cette valeur peut être ajustée en fonction des limitations du réseau)
   * Profil : Principal
   * Trame-clé toutes les : 60 images

    **Audio**

   * Vitesse de transmission cible : 192 kbit/s
   * Taux d’échantillonnage : 44 100 kHz

     ![Wirecast](./media/media-services-wirecast-live-encoder/media-services-wirecast4.png)
6. Appuyez sur **Enregistrer**.

    champ de codage Hello a maintenant profil hello nouvellement créé disponible pour la sélection.

    Vérifiez que hello nouveau profil est sélectionné.
7. Obtenir les URL d’entrée du canal hello dans l’ordre tooassign il toohello Wirecast **point de terminaison RTMP**.

    Accédez outil AMSE toohello précédent et vérifier l’état d’achèvement canal hello. Une fois que l’état de hello a été modifié à partir de **départ** trop**en cours d’exécution**, vous pouvez obtenir les URL d’entrée hello.

    Lorsque le canal de hello est en cours d’exécution, cliquez avec le bouton droit sur nom de la chaîne hello, naviguez vers le bas toohover sur **tooclipboard de copier l’URL entrée** , puis sélectionnez **URL entrée principale**.  

    ![Wirecast](./media/media-services-wirecast-live-encoder/media-services-wirecast6.png)
8. Bonjour Wirecast **les paramètres de sortie** fenêtre, coller ces informations dans hello **adresse** champ de la section de sortie hello et attribuer un nom de flux.

    ![Wirecast](./media/media-services-wirecast-live-encoder/media-services-wirecast5.png)

1. Sélectionnez **OK**.
2. Sur hello principal **Wirecast** , vérifiez que les sources d’entrée audio et vidéo sont prêts, puis appuyez sur **flux** dans l’angle supérieur gauche de hello.

   ![Wirecast](./media/media-services-wirecast-live-encoder/media-services-wirecast7.png)

> [!IMPORTANT]
> Avant de cliquer sur **flux**, vous **doit** vous assurer que le canal de hello est prêt.
> Assurez-vous également que pas tooleave hello canal dans un état prêt sans une contribution d’entrée de flux pendant plus de 15 minutes >.
>
>

## <a name="test-playback"></a>Tester la lecture

Accédez outil AMSE toohello et cliquez avec le bouton droit sur toobe de canal hello testé. À partir du menu de hello, placez le curseur sur **hello de lecture aperçu** et sélectionnez **avec Azure Media Player**.  

    ![wirecast](./media/media-services-wirecast-live-encoder/media-services-wirecast8.png)

Si le flux de données hello s’affiche dans le lecteur hello, encodeur de hello a été correctement configuré tooconnect tooAMS.

Si une erreur est reçue, le canal de hello devez paramètres d’encodeur et de réinitialisation toobe ajustées. Consultez hello [dépannage](media-services-troubleshooting-live-streaming.md) rubrique pour obtenir des conseils.  

## <a name="create-a-program"></a>Créer un programme
1. Une fois que vous avez vérifié que la lecture fonctionne sur le canal, créez un programme. Sous hello **Live** onglet dans l’outil AMSE hello, cliquez avec le bouton droit dans la zone du programme hello et sélectionnez **créer un nouveau programme**.  

    ![Wirecast](./media/media-services-wirecast-live-encoder/media-services-wirecast9.png)
2. Nom de programme de hello et, si nécessaire, ajustez hello **longueur de fenêtre d’Archive** (heures de too4 les valeurs par défaut). Vous pouvez également spécifier un emplacement de stockage ou les conserver en tant que valeur par défaut hello.  
3. Vérifiez hello **maintenant démarrer hello programme** boîte.
4. Cliquez sur **Créer le programme**.  

   >[!NOTE]
   >La création d’un programme prend moins de temps que la création d’un canal.
       
5. Une fois l’exécution du programme hello, confirmer la lecture en cliquant avec le bouton droit sur un programme hello et en naviguant trop**lecture hello programmes** , puis en sélectionnant **avec Azure Media Player**.  
6. Après confirmation, cliquez à nouveau programme de hello, puis sélectionnez **copier hello URL de sortie tooClipboard** (ou en extraire ces informations hello **informations et des paramètres du programme** option de menu de hello).

Hello flux est maintenant prêt toobe incorporé dans un lecteur ou public tooan distribuée pour live affichage.  

## <a name="troubleshooting"></a>Résolution des problèmes
Consultez hello [dépannage](media-services-troubleshooting-live-streaming.md) rubrique pour obtenir des conseils.

## <a name="media-services-learning-paths"></a>Parcours d’apprentissage de Media Services
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fournir des commentaires
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
