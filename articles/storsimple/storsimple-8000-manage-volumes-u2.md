---
title: les volumes StorSimple aaaManage (Update 3) | Documents Microsoft
description: "Explique comment tooadd, modifier, surveiller et supprimer des volumes StorSimple et tootake les hors connexion si nécessaire."
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 07/19/2017
ms.author: alkohli
ms.openlocfilehash: 6228c4486dd5a7887df670c4c4584c4edcdfc509
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-device-manager-service-toomanage-volumes-update-3-or-later"></a>Utiliser des volumes de toomanage service hello StorSimple le Gestionnaire de périphériques (Update 3 ou version ultérieure)

## <a name="overview"></a>Vue d'ensemble

Ce didacticiel explique comment toouse hello toocreate du service Gestionnaire de périphériques StorSimple et gestion des volumes sur les appareils hello StorSimple 8000 series exécutant Update 3 et versions ultérieures.

Hello service du Gestionnaire de périphériques StorSimple est une extension Bonjour portail Azure qui vous permet de gérer votre solution StorSimple à partir d’une seule interface web. Utiliser des volumes toomanage portail Azure hello sur tous vos appareils. Vous pouvez également créer et gérer des services StorSimple, gérer des appareils, des stratégies de sauvegarde et un catalogue de sauvegarde, et afficher des alertes.

## <a name="volume-types"></a>Types de volume

Les volumes StorSimple peuvent être les suivants :

* **Attaché localement volumes**: données de ces volumes restent sur l’appareil StorSimple local hello en permanence.
* **Niveaux de volumes**: données de ces volumes peuvent déborder toohello cloud.

Un volume d’archivage est un type de volume hiérarchisé. Hello supérieure la déduplication taille du segment utilisé pour les volumes d’archivage permet hello appareil tootransfer supérieure des segments de données toohello dans le cloud.

Si nécessaire, vous pouvez modifier le type de volume hello à partir de tootiered local ou de toolocal à plusieurs niveaux. Pour plus d’informations, consultez trop[modifier le type de volume hello](#change-the-volume-type).

### <a name="locally-pinned-volumes"></a>Volumes épinglés localement 

Les volumes attachés localement sont entièrement volumes pas de niveau de la toohello données dans le cloud, garantissant ainsi local garanties pour les données primaires, indépendamment de connectivité du cloud. Les données des volumes épinglés localement ne sont pas dédupliquées ni compressées, mais les instantanés des volumes épinglés localement sont dédupliqués. 

Les volumes épinglés localement sont totalement configurés. Vous devez donc disposer de suffisamment d’espace sur votre appareil lorsque vous les créez. Vous pouvez configurer les volumes attachés localement tooa la taille maximale de 8 To sur l’appareil de hello StorSimple 8100 et 20 To sur l’appareil de 8600 hello. StorSimple réserve hello local espace libre restant sur périphérique hello pour les instantanés, les métadonnées et le traitement des données. Vous pouvez augmenter la taille de hello d’un volume attaché localement toohello espace maximal disponible, mais vous ne pouvez pas réduire la taille hello d’un volume une fois créé.

Lorsque vous créez un volume attaché localement, l’espace disponible de hello pour la création de volumes à plusieurs niveaux est réduite. Hello inverse est également vrai : Si vous avez des volumes hiérarchisés existants, espace hello disponible pour une création localement épinglé volumes sera inférieur dans les limites maximales hello indiqués ci-dessus. Pour plus d’informations sur les volumes locaux, consultez toohello [Forum aux questions sur les volumes attachés localement](storsimple-8000-local-volume-faq.md).

### <a name="tiered-volumes"></a>Volumes hiérarchisés 

Volumes hiérarchisés sont des volumes alloués dans le hello fréquemment données auxquelles vous accédez restent local sur l’appareil de hello et moins de données fréquemment utilisées sont automatiquement hiérarchisé toohello cloud. Allocation dynamique est une technologie de virtualisation dans lequel le stockage disponible apparaît tooexceed des ressources physiques. Plutôt que de réserver suffisamment de stockage à l’avance, StorSimple utilise tooallocate provisionnement dynamique juste assez toomeet d’espace nécessaire en cours. nature évolutive de Hello de stockage cloud simplifie cette approche, car StorSimple peut augmenter ou diminuer les besoins changeants de toomeet de stockage cloud.

Si vous utilisez hello volume à plusieurs niveaux pour les données d’archivage, sélectionnez hello **utiliser ce volume pour les données d’archive moins fréquemment sollicitées** taille de segment de déduplication case à cocher toochange hello pour votre volume too512 Ko. Si vous ne sélectionnez pas de cette option, le volume de hiérarchisé correspondant hello utilisera une taille de segment de 64 Ko. Une plus grande taille de segment de la déduplication permet de transfert hello tooexpedite des appareils hello du cloud toohello de données d’archivage volumineux.


### <a name="provisioned-capacity"></a>Capacité allouée

Consultez toohello tableau pour une capacité déployée maximale pour chaque type d’appareil et le volume suivant. (Notez que les volumes épinglés localement ne sont pas disponibles sur un appareil virtuel.)

|  | Taille maximale de volume hiérarchisé | Taille maximale de volume épinglé localement |
| --- | --- | --- |
| **Appareils physiques** | | |
| 8100 |64 To |8 To |
| 8600 |64 To |20 To |
| **Appareils virtuels** | | |
| 8010 |30 To |N/A |
| 8020 |64 To |N/A |

## <a name="hello-volumes-blade"></a>Panneau de volumes Hello

Hello **Volumes** panneau vous permet de volumes de stockage hello toomanage qui sont configurés sur l’appareil Microsoft Azure StorSimple hello pour vos initiateurs (serveurs). Il affiche la liste hello des volumes sur hello StorSimple périphériques connectés tooyour service.

 ![Page volumes](./media/storsimple-8000-manage-volumes-u2/volumeslist.png)

Un volume est constitué d’une série d’attributs :

* **Nom de volume** – un nom descriptif qui doit être uniques et permet d’identifier le volume de hello. Ce nom est également utilisé dans les rapports d’analyse lorsque vous filtrez sur un volume particulier. Une fois que le volume de hello est créé, il ne peut pas être renommé.
* **État** : peut être en ligne ou hors connexion. Si un volume est hors connexion, il n’est pas visible tooinitiators (serveurs) autorisés accès toouse hello volume.
* **Capacité** – spécifie la quantité totale de hello de données qui peuvent être stockées à l’initiateur hello (serveur). Les volumes attachés localement sont entièrement approvisionnés et résident sur l’appareil StorSimple hello. Volumes hiérarchisés sont alloués dynamiquement et hello données dédupliquées. Avec des volumes alloués dynamiquement, votre appareil ne Préalloue pas la capacité de stockage physique en interne ou sur le cloud hello selon la capacité du volume tooconfigured. capacité du volume Hello est allouée et consommée à la demande.
* **Type** – indique si le volume de hello est **à plusieurs niveaux** (hello par défaut) ou **attaché localement**.

Suivez les instructions de hello dans cette hello didacticiel tooperform tâches suivantes :

* Ajout d’un volume 
* Modification d’un volume 
* Modifier le type de volume hello
* Suppression d’un volume 
* Mise hors connexion d’un volume 
* Analyse d’un volume 

## <a name="add-a-volume"></a>Ajout d’un volume

Vous [avez créé un volume](storsimple-8000-deployment-walkthrough-u2.md#step-6-create-a-volume) lors du déploiement de votre appareil de la gamme 8000 StorSimple. La procédure d’ajout d’un volume est similaire.

#### <a name="tooadd-a-volume"></a>tooadd un volume

1. À partir de hello tableau qui répertorie les périphériques hello Bonjour **périphériques** panneau, sélectionnez votre appareil. Cliquez sur **+ Ajouter un volume**.

    ![Ajouter un volume](./media/storsimple-8000-manage-volumes-u2/step5createvol1.png)

2. Bonjour **ajouter un volume** panneau :
   
    1. Hello **périphérique** est automatiquement renseigné avec votre appareil.

    2. À partir de la liste déroulante hello, sélectionnez le conteneur de volume hello où vous avez besoin d’un volume de tooadd.

    3.  Saisissez un **nom** pour le volume. Après la création de volume de hello, vous ne pouvez pas renommer volume de hello.

    4. Dans la liste déroulante hello, sélectionnez hello **Type** pour votre volume. Pour les charges de travail qui nécessitent des garanties locales, une faible latence et les meilleures performances possibles, sélectionnez un volume **épinglé localement** . Pour toutes les autres données, sélectionnez un volume **à plusieurs niveaux** . Si vous utilisez ce volume pour les données d’archivage, cochez la case **Utiliser ce volume pour des données d’archivage moins fréquemment sollicitées**.
      
       La configuration d’un volume à plusieurs niveaux est légère, et sa création peut être rapide. En sélectionnant **utiliser ce volume pour les données d’archive moins fréquemment sollicitées** pour le volume hiérarchisé ciblé pour la taille de segment de la déduplication des données d’archivage des modifications hello pour votre volume too512 Ko. Si ce champ n’est pas coché, volume de hiérarchisé correspondant hello utilise une taille de segment de 64 Ko. Une plus grande taille de segment de la déduplication permet de transfert hello tooexpedite des appareils hello du cloud toohello de données d’archivage volumineux.
       
       Un volume attaché localement est approvisionné et garantit que les données de salutation principal sur le volume de hello restent local toohello appareil et ne pas déborder toohello cloud.  Si vous créez un volume attaché localement, hello de vérification d’espace disponible sur les couches locales hello taille de volume de hello tooprovision Hello demandée. opération Hello de création d’un volume attaché localement peut impliquer le débordement des données existantes à partir de hello appareil toohello cloud et durée hello de volume de hello toocreate peut être longue. durée totale de Hello dépend hello taille du volume de hello configuré, la bande passante réseau disponible et données hello sur votre appareil.

    5. Spécifiez hello **capacité approvisionnée** pour votre volume. Prenez note de la capacité de hello est disponible selon le type de volume hello sélectionné. Hello spécifié la taille du volume ne doit pas dépasser espace hello.
      
       Vous pouvez configurer les volumes attachés localement des too8.5 To ou des volumes hiérarchisés jusqu'à to too200 sur l’appareil 8100 de hello. Sur l’appareil 8600 supérieure de hello, vous pouvez configurer les volumes attachés localement des too22.5 To ou des volumes hiérarchisés jusqu'à too500 to. Comme espace local sur le périphérique de hello hello requis toohost jeu de travail de volumes hiérarchisés, la création de volumes attachés localement affecte espace hello disponible pour l’approvisionnement des volumes hiérarchisés. Par conséquent, si vous créez un volume épinglé localement, l’espace disponible pour la création de volumes à plusieurs niveaux est réduit. De même, si vous créez un volume hiérarchisé, espace disponible de hello pour la création de volumes attachés localement est réduite.
      
       Si vous configurez un volume attaché localement de 8,5 To (taille maximale autorisée) sur votre appareil 8100, vous avez épuisé tout hello local l’espace disponible sur le périphérique de hello. Impossible de créer un volume à plusieurs niveaux à partir de ce point, car il n’existe aucun espace local sur hello appareil toohost hello plage de travail de hello à plusieurs niveaux de volume. Volumes hiérarchisés existants affectent également les espace hello disponible. Par exemple, si vous avez un appareil 8100 qui possède déjà des volumes à plusieurs niveaux de 106 To, seuls 4 To d’espace sont disponibles pour les volumes épinglés localement.

    6. Bonjour **connecté des ordinateurs hôtes** , cliquez sur la flèche de hello. 

        ![Hôtes connectés](./media/storsimple-8000-manage-volumes-u2/step5createvol2.png)

    7. Bonjour **connecté des ordinateurs hôtes** panneau, choisissez un ACR existant ou ajouter un nouvel ACR. Si vous choisissez un nouvel ACR, puis indiquez un **nom** pour votre ACR, indiquez hello **iSCSI Qualified Name** (IQN) de votre hôte Windows. Si vous n’avez pas hello IQN, passez trop[Get hello IQN d’un hôte Windows Server](#get-the-iqn-of-a-windows-server-host). Cliquez sur **Créer**. Création d’un volume avec hello spécifié les paramètres.

        ![Click Create](./media/storsimple-8000-manage-volumes-u2/step5createvol3.png)

Le nouveau volume est maintenant prêt toouse.

> [!NOTE]
> Si vous créez un volume attaché localement et ensuite créerez un autre localement épinglé volume immédiatement par la suite, les tâches de création de volume hello exécutent de manière séquentielle. première tâche de création de volume Hello doit se terminer avant le début du travail de la création du volume suivant hello.

## <a name="modify-a-volume"></a>Modification d’un volume

Modifier un volume lorsque vous devez tooexpand ou modification hello hôtes qui accèdent aux volumes de hello.

> [!IMPORTANT]
> * Si vous modifiez la taille du volume sur le périphérique de hello hello, taille du volume hello doit toobe modifiée sur hôte hello également.
> * les étapes de côté hôte Hello décrites ici sont pour Windows Server 2012 (2012 R2). Les procédures pour Linux ou d’autres systèmes d’exploitation sont différentes. Consultez les instructions de système d’exploitation hôte tooyour lors de la modification du volume hello sur un ordinateur hôte exécutant un autre système d’exploitation.

#### <a name="toomodify-a-volume"></a>toomodify un volume

1. Atteindre le service du Gestionnaire de périphériques StorSimple tooyour, puis cliquez sur **périphériques**. À partir de hello tableau qui répertorie les périphériques hello, sélectionnez hello que dispose d’un volume hello que vous avez l’intention de toomodify. Cliquez sur **Paramètres > Volumes**.

    ![Accédez tooVolumes panneau](./media/storsimple-8000-manage-volumes-u2/modifyvol2.png)

2. À partir de hello tabulaire liste des volumes, sélectionnez le volume hello et tooinvoke hello contexte menu contextuel. Sélectionnez **mettre hors connexion** volume de hello tootake vous allez modifier en mode hors connexion.

    ![Sélectionner le volume et le mettre hors connexion](./media/storsimple-8000-manage-volumes-u2/modifyvol4.png)

3. Bonjour **mettre hors connexion** panneau, examiner l’impact hello de mise hors connexion de volume de hello et cochez la case correspondante hello. Assurez-vous que le volume de hello correspondant sur l’ordinateur hôte de hello est tout d’abord hors connexion. Pour plus d’informations sur comment tootake un volume hors connexion sur un serveur hôte connecté tooStorSimple, consultez instructions spécifiques du système toooperating. Cliquez sur **Mettre hors connexion**.

    ![Passer en revue les répercussions de la mise hors connexion du volume](./media/storsimple-8000-manage-volumes-u2/modifyvol5.png)

4. Une fois que le volume de hello est hors connexion (comme indiqué par l’état du volume hello), sélectionnez le volume hello et tooinvoke hello contexte menu contextuel. Sélectionnez **Modifier le volume**.

    ![Sélectionner Modifier le volume](./media/storsimple-8000-manage-volumes-u2/modifyvol9.png)


5. Bonjour **modifier le volume** panneau, vous pouvez apporter hello modifications suivantes :
   
   1. Hello volume **nom** ne peut pas être modifié.
   2. Convertir hello **Type** à partir de tootiered attaché localement ou de toolocally hiérarchisé épinglé (consultez [modifier le type de volume hello](#change-the-volume-type) pour plus d’informations).
   3. Augmenter hello **capacité approvisionnée**. Hello **capacité approvisionnée** ne peut être augmentée. Vous ne pouvez pas réduire la taille d’un volume après sa création.
   4. Sous **connecté des ordinateurs hôtes**, vous pouvez modifier hello ACR. toomodify un ACR, hello doit être en mode hors connexion.

       ![Passer en revue les répercussions de la mise hors connexion du volume](./media/storsimple-8000-manage-volumes-u2/modifyvol11.png)

5. Cliquez sur **enregistrer** toosave vos modifications. Cliquez sur **Oui**lorsque vous êtes invité à confirmer l’opération. Hello portail Azure affiche un message de volume de mise à jour. Il affiche un message de réussite lorsque le volume de hello a été mis à jour avec succès.

    ![Passer en revue les répercussions de la mise hors connexion du volume](./media/storsimple-8000-manage-volumes-u2/modifyvol5.png)

7. Si vous développez un volume, effectuez hello sur votre ordinateur hôte Windows comme suit :
   
   1. Accédez trop**gestion de l’ordinateur** ->**gestion des disques**.
   2. Cliquez avec le bouton droit sur **Gestion des disques**, puis sélectionnez **Analyser les disques de nouveau**.
   3. Dans la liste de hello des disques, sélectionnez volume hello mis à jour, avec le bouton droit et sélectionnez **étendre le Volume**. l’Assistant étendre le Volume Hello démarre. Cliquez sur **Suivant**.
   4. Exécutez l’Assistant hello, en acceptant les valeurs par défaut de hello. Une fois hello Assistant terminé, volume de hello doit afficher hello augmenté taille.
      
      > [!NOTE]
      > Si vous développez un volume attaché localement, puis un autre localement épinglé volume immédiatement par la suite, travaux d’expansion hello volume exécutées de manière séquentielle. Hello volume d’expansion tâche doit se terminer avant le début du travail de hello suivant volume d’expansion.
      

## <a name="change-hello-volume-type"></a>Modifier le type de volume hello

Vous pouvez modifier le type de volume hello à partir de toolocally hiérarchisé épinglée ou de tootiered attaché localement. Toutefois, cette conversion ne doit pas être effectuée fréquemment.

### <a name="tiered-toolocal-volume-conversion-considerations"></a>Considérations sur la conversion volume hiérarchisé toolocal

Parmi les raisons de la conversion d’un volume de hiérarchisé toolocally épinglée sont :

* Assurance de la disponibilité et des performances des données locales.
* Élimination des latences du cloud et des problèmes de connexion au cloud.

En règle générale, ils sont petits volumes existants que vous souhaitez tooaccess fréquemment. Un volume épinglé localement est entièrement configuré lors de sa création. 

Si vous convertissez un volume de tooa attaché localement volume hiérarchisé, StorSimple vérifie que vous avez suffisamment d’espace sur votre appareil avant de démarrer la conversion de hello. Si vous disposez d’un manque d’espace, vous recevez une erreur et hello opération sera annulée. 

> [!NOTE]
> Avant de commencer une conversion de toolocally hiérarchisé épinglé, vérifiez que hello espace nécessaire de vos autres charges de travail. 

Conversion d’un volume hiérarchisé tooa attaché localement peut nuire aux performances de l’appareil. En outre, hello suivant facteurs peut-être augmenter hello durée de conversion de hello toocomplete :

* La bande passante est insuffisante.
* Il n’existe aucune sauvegarde actuelle.

effets de hello toominimize que ces facteurs peuvent avoir :

* Passez en revue vos stratégies de limitation de bande passante et assurez-vous qu’une bande passante dédiée de 40 Mbits/s est disponible.
* Planifier la conversion hello pendant les heures creuses.
* Prendre un instantané cloud avant de commencer la conversion de hello.

Si vous convertissez plusieurs volumes (prise en charge de différentes charges de travail), vous devez classer conversion de volume hello afin que les volumes de priorité plus élevées sont tout d’abord convertis. Par exemple, vous devez convertir des volumes hébergeant des machines virtuelles ou des volumes avec des charges de travail SQL avant de convertir des volumes avec des charges de travail à partage de fichiers.

### <a name="local-tootiered-volume-conversion-considerations"></a>Considérations de conversion de volume local tootiered

Vous souhaiterez peut-être toochange un tooa volume attaché localement à plusieurs niveaux volume si vous avez besoin d’espace supplémentaire tooprovision autres volumes. Lorsque vous convertissez tootiered de volume attaché localement de hello, hello une capacité disponible sur les appareils hello augmente en taille hello de la capacité de hello publié. Si des problèmes de connectivité empêchent hello la conversion d’un volume à partir de toohello de type local hello hiérarchisé type, hello volume local présentera de propriétés d’un volume hiérarchisé jusqu'à ce que la conversion de hello est terminée. Il s’agit, car certaines données peuvent avoir répandu toohello cloud. Ces données vidées continuent toooccupy d’espace local sur l’appareil hello qui ne peut pas être libérée tant que l’opération de hello est redémarrée et achevée.

> [!NOTE]
> La conversion d’un volume peut prendre un certain temps. Vous ne pouvez pas l’annuler une fois qu’elle a commencé. volume de Hello reste en ligne pendant la conversion de hello et vous pouvez effectuer des sauvegardes, mais vous ne pouvez pas développer ou restaurer le volume de hello lors de la conversion de hello est en cours.


#### <a name="toochange-hello-volume-type"></a>type de volume hello toochange

1. Atteindre le service du Gestionnaire de périphériques StorSimple tooyour, puis cliquez sur **périphériques**. À partir de hello tableau qui répertorie les périphériques hello, sélectionnez hello que dispose d’un volume hello que vous avez l’intention de toomodify. Cliquez sur **Paramètres > Volumes**.

    ![Accédez tooVolumes panneau](./media/storsimple-8000-manage-volumes-u2/modifyvol2.png)

3. À partir de hello tabulaire liste des volumes, sélectionnez le volume hello et tooinvoke hello contexte menu contextuel. Sélectionnez **Modifier**.

    ![Sélectionner Modifier dans le menu contextuel](./media/storsimple-8000-manage-volumes-u2/changevoltype2.png)

4. Sur hello **modifier le volume** panneau, modifier le type de volume hello en sélectionnant le nouveau type de hello de hello **Type** liste déroulante.
   
   * Si vous modifiez le type de hello trop**attaché localement**, StorSimple vérifiera toosee s’il existe une capacité suffisante.
   * Si vous modifiez le type de hello trop**à plusieurs niveaux** et ce volume sera utilisé pour les données d’archivage, sélectionnez hello **utiliser ce volume pour les données d’archive moins fréquemment sollicitées** case à cocher.
   * Si vous configurez un volume attaché localement comme à plusieurs niveaux ou _inversement_, hello message suivant s’affiche.
   
    ![Message de modification du type de volume](./media/storsimple-8000-manage-volumes-u2/changevoltype3.png)

7. Cliquez sur **enregistrer** modifications de hello toosave. Lorsque vous êtes invité à confirmer l’opération, cliquez sur **Oui** processus de conversion toostart hello. 

    ![Enregistrer et confirmer](./media/storsimple-8000-manage-volumes-u2/modifyvol11.png)

8. Hello portail Azure affiche une notification pour la création de tâche hello qui serait de mettre à jour le volume de hello. Cliquez sur l’état de hello toomonitor hello notification du travail de conversion de volume hello.

    ![Travail de conversion des volumes](./media/storsimple-8000-manage-volumes-u2/changevoltype5.png)

## <a name="take-a-volume-offline"></a>Mise hors connexion d’un volume

Vous devrez peut-être tootake un volume hors connexion lorsque vous envisagez de toomodify ou de supprimer le volume de hello. Lorsqu’un volume est hors connexion, il n’est pas disponible pour l’accès en lecture-écriture. Vous devez mettre le volume de hello hors connexion sur l’hôte de hello et de périphérique de hello.

#### <a name="tootake-a-volume-offline"></a>tootake un volume hors connexion

1. Assurez-vous que le volume hello en question n’est pas utilisé avant de mettre hors connexion.
2. Mettez d’abord volume hello hors connexion sur l’ordinateur hôte de hello. Cela élimine tout risque potentiel de corruption des données sur le volume de hello. Pour connaître la procédure, consultez instructions toohello de votre système d’exploitation hôte.
3. Une fois que l’hôte de hello est hors connexion, prenez volume de hello sur périphérique hello hors connexion en effectuant hello comme suit :
   
    1. Atteindre le service du Gestionnaire de périphériques StorSimple tooyour, puis cliquez sur **périphériques**. À partir de hello tableau qui répertorie les périphériques hello, sélectionnez hello que dispose d’un volume hello que vous avez l’intention de toomodify. Cliquez sur **Paramètres > Volumes**.

        ![Accédez tooVolumes panneau](./media/storsimple-8000-manage-volumes-u2/modifyvol2.png)

    2. À partir de hello tabulaire liste des volumes, sélectionnez le volume hello et tooinvoke hello contexte menu contextuel. Sélectionnez **mettre hors connexion** volume de hello tootake vous allez modifier en mode hors connexion.

        ![Sélectionner le volume et le mettre hors connexion](./media/storsimple-8000-manage-volumes-u2/modifyvol4.png)

3. Bonjour **mettre hors connexion** panneau, examiner l’impact hello de mise hors connexion de volume de hello et cochez la case correspondante hello. Cliquez sur **Mettre hors connexion**. 

    ![Passer en revue les répercussions de la mise hors connexion du volume](./media/storsimple-8000-manage-volumes-u2/modifyvol5.png)
      
      Vous êtes averti lorsque le volume de hello est hors connexion. état du volume Hello met également à jour tooOffline.
      
4. Une fois un volume est hors connexion, si vous sélectionnez le volume de hello et avec le bouton droit, **mettre en ligne** option est disponible dans le menu contextuel de hello.

> [!NOTE]
> Hello **mettre hors connexion** commande envoie un volume hello tootake toohello appareil hors connexion. Si les hôtes utilisent toujours le volume de hello, cela entraîne des connexions interrompues, mais mise hors connexion de volume de hello n’échouera pas.

## <a name="delete-a-volume"></a>Suppression d’un volume

> [!IMPORTANT]
> Vous pouvez supprimer un volume uniquement s’il est hors connexion.

Terminer hello suivant les étapes toodelete un volume.

#### <a name="toodelete-a-volume"></a>toodelete un volume

1. Atteindre le service du Gestionnaire de périphériques StorSimple tooyour, puis cliquez sur **périphériques**. À partir de hello tableau qui répertorie les périphériques hello, sélectionnez hello que dispose d’un volume hello que vous avez l’intention de toomodify. Cliquez sur **Paramètres > Volumes**.

    ![Accédez tooVolumes panneau](./media/storsimple-8000-manage-volumes-u2/modifyvol2.png)

3. Vérifier l’état de hello du volume de hello souhaité toodelete. Si le volume de hello souhaité toodelete n’est pas hors connexion, mettre hors connexion tout d’abord. Suivez les étapes de hello dans [mettre un volume hors connexion](#take-a-volume-offline).
4. Une fois que le volume de hello est hors connexion, sélectionnez le volume hello, tooinvoke hello contexte menu contextuel, puis sélectionnez **supprimer**.

    ![Sélectionner Supprimer dans le menu contextuel](./media/storsimple-8000-manage-volumes-u2/deletevol1.png)

5. Bonjour **supprimer** panneau, de révision et de case à cocher hello select par rapport à impact hello de la suppression d’un volume. Lorsque vous supprimez un volume, toutes les données hello qui réside sur le volume de hello est perdue. 

    ![Enregistrer et confirmer les modifications](./media/storsimple-8000-manage-volumes-u2/deletevol2.png)

6. Après la suppression des volumes de hello, liste tabulaire de hello des volumes met à jour la suppression tooindicate hello.

    ![Liste des volumes mise à jour](./media/storsimple-8000-manage-volumes-u2/deletevol3.png)
   
   > [!NOTE]
   > Si vous supprimez un volume attaché localement, espace hello disponible pour les nouveaux volumes ne peut pas être mis à jour immédiatement. Hello Service du Gestionnaire de périphériques StorSimple met à jour disponible d’espace local hello régulièrement. Nous vous suggérons de qu'attendre quelques minutes avant d’essayer de nouveau volume de toocreate hello.
   >
   > En outre, si vous supprimez un volume attaché localement, puis un autre localement épinglé volume immédiatement par la suite, les tâches de suppression du volume hello exécutent séquentiellement. tâche de suppression de volume premier Hello doit se terminer avant le début du travail de suppression de volume suivant hello.

## <a name="monitor-a-volume"></a>Analyse d’un volume

Surveillance du volume vous permet de toocollect I aux E/s statistiques pour un volume. Surveillance est activée par défaut pour hello 32 premiers volumes que vous créez. L’analyse des volumes supplémentaires est désactivée par défaut. 

> [!NOTE]
> L’analyse des volumes clonés est désactivée par défaut.


Effectuer hello suivant les étapes tooenable ou désactiver la surveillance d’un volume.

#### <a name="tooenable-or-disable-volume-monitoring"></a>tooenable ou désactiver la surveillance du volume

1. Atteindre le service du Gestionnaire de périphériques StorSimple tooyour, puis cliquez sur **périphériques**. À partir de hello tableau qui répertorie les périphériques hello, sélectionnez hello que dispose d’un volume hello que vous avez l’intention de toomodify. Cliquez sur **Paramètres > Volumes**.
2. À partir de hello tabulaire liste des volumes, sélectionnez le volume hello et tooinvoke hello contexte menu contextuel. Sélectionnez **Modifier**.
3. Bonjour **modifier le volume** panneau, pour **analyse** sélectionnez **activer** ou **désactiver** tooenable ou désactiver l’analyse.

    ![Désactiver l’analyse](./media/storsimple-8000-manage-volumes-u2/monitorvol1.png) 

4. Cliquez sur **Enregistrer** puis, lorsque vous êtes invité à confirmer l’opération, cliquez sur **Oui**. Hello portail Azure affiche une notification de mise à jour du volume de hello, puis un message de réussite, une fois la mise à jour avec succès de volume de hello.

## <a name="next-steps"></a>Étapes suivantes

* Découvrez comment trop[cloner un volume StorSimple](storsimple-8000-clone-volume-u2.md).
* Découvrez comment trop[utilisez hello tooadminister du service Gestionnaire de périphériques StorSimple votre appareil StorSimple](storsimple-8000-manager-service-administration.md).

