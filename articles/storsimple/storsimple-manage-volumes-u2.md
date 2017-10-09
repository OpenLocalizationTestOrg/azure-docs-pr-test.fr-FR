---
title: aaaManage vos volumes StorSimple (U2) | Documents Microsoft
description: "Explique comment tooadd, modifier, surveiller et supprimer des volumes StorSimple et tootake les hors connexion si nécessaire."
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: 57896932-0aa5-4805-970c-d13403ae7551
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 10/28/2016
ms.author: alkohli
ms.openlocfilehash: 8b64f1d92023646cdf881882854d9bc5d7334a10
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-manager-service-toomanage-volumes-update-2"></a>Utiliser des volumes de toomanage hello StorSimple Manager service (Update 2)
[!INCLUDE [storsimple-version-selector-manage-volumes](../../includes/storsimple-version-selector-manage-volumes.md)]

## <a name="overview"></a>Vue d'ensemble
Ce didacticiel explique comment toouse hello toocreate du service StorSimple Manager et gestion des volumes sur l’appareil StorSimple hello et un appareil virtuel StorSimple Update 2 est installé.

Hello service StorSimple Manager est une extension Bonjour portail classique Azure qui vous permet de gérer votre solution StorSimple à partir d’une seule interface web. Dans des volumes plus toomanaging, vous pourrez utiliser toocreate de service StorSimple Manager hello et gérer les services StorSimple, afficher et gérer des appareils, afficher les alertes et afficher et gérer les stratégies de sauvegarde et de catalogue de sauvegarde hello.

## <a name="volume-types"></a>Types de volume
Les volumes StorSimple peuvent être les suivants :

* **Attaché localement volumes**: données de ces volumes restent sur l’appareil StorSimple local hello en permanence.
* **Niveaux de volumes**: données de ces volumes peuvent déborder toohello cloud.

Un volume d’archivage est un type de volume hiérarchisé. Hello supérieure la déduplication taille du segment utilisé pour les volumes d’archivage permet hello appareil tootransfer supérieure des segments de données toohello dans le cloud. 

Si nécessaire, vous pouvez modifier le type de volume hello à partir de tootiered local ou de toolocal à plusieurs niveaux. Pour plus d’informations, consultez trop[modifier le type de volume hello](#change-the-volume-type).

### <a name="locally-pinned-volumes"></a>Volumes épinglés localement 
Les volumes attachés localement sont entièrement volumes pas de niveau de la toohello données dans le cloud, garantissant ainsi local garanties pour les données primaires, indépendamment de connectivité du cloud. Les données des volumes épinglés localement ne sont pas dédupliquées ni compressées, mais les instantanés des volumes épinglés localement sont dédupliqués. 

Les volumes épinglés localement sont totalement configurés. Vous devez donc disposer de suffisamment d’espace sur votre appareil lorsque vous les créez. Vous pouvez configurer les volumes attachés localement tooa la taille maximale de 8 To sur l’appareil de hello StorSimple 8100 et 20 To sur l’appareil de 8600 hello. StorSimple réserve hello local espace libre restant sur périphérique hello pour les instantanés, les métadonnées et le traitement des données. Vous pouvez augmenter la taille de hello d’un volume attaché localement toohello espace maximal disponible, mais vous ne pouvez pas réduire la taille hello d’un volume une fois créé.

Lorsque vous créez un volume attaché localement, l’espace disponible de hello pour la création de volumes à plusieurs niveaux est réduite. Hello inverse est également vrai : Si vous avez des volumes hiérarchisés existants, espace hello disponible pour une création localement épinglé volumes sera inférieur dans les limites maximales hello indiqués ci-dessus. Pour plus d’informations sur les volumes locaux, consultez toohello [Forum aux questions sur les volumes attachés localement](storsimple-local-volume-faq.md).   

### <a name="tiered-volumes"></a>Volumes hiérarchisés 
Volumes hiérarchisés sont des volumes alloués dans le hello fréquemment données auxquelles vous accédez restent local sur l’appareil de hello et moins de données fréquemment utilisées sont automatiquement hiérarchisé toohello cloud. Allocation dynamique est une technologie de virtualisation dans lequel le stockage disponible apparaît tooexceed des ressources physiques. Plutôt que de réserver suffisamment de stockage à l’avance, StorSimple utilise tooallocate provisionnement dynamique juste assez toomeet d’espace nécessaire en cours. nature évolutive de Hello de stockage cloud simplifie cette approche, car StorSimple peut augmenter ou diminuer les besoins changeants de toomeet de stockage cloud.

Si vous utilisez hello volume à plusieurs niveaux pour les données d’archivage, en sélectionnant hello **utiliser ce volume pour les données d’archive moins fréquemment sollicitées** case à cocher modifie la taille de segment de la déduplication de hello pour votre volume too512 Ko. Si vous ne sélectionnez pas de cette option, le volume de hiérarchisé correspondant hello utilisera une taille de segment de 64 Ko. Une plus grande taille de segment de la déduplication permet de transfert hello tooexpedite des appareils hello du cloud toohello de données d’archivage volumineux.

> [!NOTE]
> Archivage volumes créés avec une version 2 mise à jour avant de StorSimple seront importées comme hiérarchisé hello archivage la case à cocher.
> 
> 

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

## <a name="hello-volumes-page"></a>page de Volumes Hello
Hello **Volumes** page vous permet de volumes de stockage hello toomanage qui sont configurés sur l’appareil Microsoft Azure StorSimple hello pour vos initiateurs (serveurs). Il affiche la liste hello des volumes sur votre appareil StorSimple.

 ![Page volumes](./media/storsimple-manage-volumes-u2/VolumePage.png)

Un volume est constitué d’une série d’attributs :

* **Nom de volume** – un nom descriptif qui doit être uniques et permet d’identifier le volume de hello. Ce nom est également utilisé dans les rapports d’analyse lorsque vous filtrez sur un volume particulier.
* **État** : peut être en ligne ou hors connexion. Si un volume est hors connexion, il n’est pas visible tooinitiators (serveurs) autorisés accès toouse hello volume.
* **Capacité** – spécifie la quantité totale de hello de données qui peuvent être stockées à l’initiateur hello (serveur). Les volumes attachés localement sont entièrement approvisionnés et résident sur l’appareil StorSimple hello. Volumes hiérarchisés sont alloués dynamiquement et hello données dédupliquées. Avec des volumes alloués dynamiquement, votre appareil ne Préalloue pas la capacité de stockage physique en interne ou sur le cloud hello selon la capacité du volume tooconfigured. capacité du volume Hello est allouée et consommée à la demande.
* **Type** – indique si le volume de hello est **à plusieurs niveaux** (hello par défaut) ou **attaché localement**.
* **Sauvegarde** – indique si une stratégie de sauvegarde par défaut existe pour le volume de hello.
* **Accès** – spécifie les initiateurs hello (serveurs) autorisés accès toothis volume. Les initiateurs qui ne sont pas membres de l’enregistrement de contrôle d’accès (ACR) qui est associé au volume de hello ne voient pas de volume de hello.
* **Analyse** : indique si un volume est ou non en cours d’analyse. Par défaut, l’analyse est activée au moment de la création du volume. Toutefois, elle est désactivée pour un volume cloné. tooenable d’analyse pour un volume, suivez les instructions de hello dans [surveiller un volume](#monitor-a-volume). 

Suivez les instructions de hello dans cette hello didacticiel tooperform tâches suivantes :

* Ajout d’un volume 
* Modification d’un volume 
* Modifier le type de volume hello
* Suppression d’un volume 
* Mise hors connexion d’un volume 
* Analyse d’un volume 

## <a name="add-a-volume"></a>Ajout d’un volume
Vous [avez créé un volume](storsimple-deployment-walkthrough-u2.md#step-6-create-a-volume) lors du déploiement de votre solution StorSimple. La procédure d’ajout d’un volume est similaire.

#### <a name="tooadd-a-volume"></a>tooadd un volume
1. Sur hello **périphériques** page, sélectionnez le périphérique de hello, double-cliquez dessus, puis cliquez sur hello **conteneurs de volumes** onglet.
2. Sélectionnez un conteneur de volume à partir de la liste de hello et double-cliquez dessus tooaccess hello volumes associés hello conteneur.
3. Cliquez sur **ajouter** bas hello de page de hello. Assistant Ajout d’un volume de Hello démarre.
   
     ![Assistant Ajout de volume, paramètres de base](./media/storsimple-manage-volumes-u2/TieredVolEx.png)
4. Bonjour Assistant Ajout d’un volume, sous **les paramètres de base**, hello suivant :
   
   1. Saisissez un **nom** pour le volume.
   2. Sélectionnez un **Type d’utilisation** à partir de la liste déroulante de hello. Pour les charges de travail nécessitant des toobe de données disponible localement sur le périphérique de hello en permanence, sélectionnez **attaché localement**. Pour tous les autres types de données, sélectionnez **Hiérarchisé**. (**à plusieurs niveaux** est la valeur par défaut hello.)
   3. Si vous avez sélectionné **à plusieurs niveaux** à l’étape 2, vous pouvez sélectionner hello **utiliser ce volume pour les données d’archive moins fréquemment sollicitées** case tooconfigure un volume d’archive.
   4. Entrez hello **capacité approvisionnée** pour votre volume en Go ou to. Consultez la section [Capacité allouée](#provisioned-capacity) pour connaître les tailles maximales pour chaque type d’appareil et de volume. Examinez hello **capacité disponible** toodetermine la capacité de stockage est réellement disponible sur votre appareil.
5. Cliquez sur la flèche hello![Icône en forme de flèche](./media/storsimple-manage-volumes-u2/HCS_ArrowIcon.png). Si vous configurez un volume attaché localement, hello message suivant s’affiche.
   
    ![Message de modification du type de volume](./media/storsimple-manage-volumes-u2/LocalVolEx.png)
6. Cliquez sur la flèche hello ![icône de flèche](./media/storsimple-manage-volumes-u2/HCS_ArrowIcon.png)nouveau toogo toohello **des paramètres supplémentaires** page.
   
    ![Assistant Ajout de volume, paramètres avancés](./media/storsimple-manage-volumes-u2/AddVolume2.png)<br>
7. Sous **Paramètres supplémentaires**, ajoutez un enregistrement de contrôle d’accès (ACR) :
   
   1. Sélectionnez un enregistrement de contrôle d’accès (ACR) à partir de la liste déroulante de hello. Vous pouvez également ajouter un nouvel enregistrement de contrôle d’accès. ACR déterminent quels hôtes peuvent accéder à vos volumes par correspondance hello hôte IQN associé à celui répertorié dans l’enregistrement de hello. Si vous ne spécifiez pas un ACR, vous verrez hello message suivant.
      
        ![Spécifier l’ACR](./media/storsimple-manage-volumes-u2/SpecifyACR.png)
   2. Nous vous recommandons de sélectionner hello **activer une sauvegarde par défaut pour ce volume** case à cocher.
   3. Cliquez sur une icône de coche hello ![Icône en forme de coche](./media/storsimple-manage-volumes-u2/HCS_CheckIcon.png) volume de hello toocreate avec hello spécifié les paramètres.

Le nouveau volume est maintenant prêt toouse.

> [!NOTE]
> Si vous créez un volume attaché localement et ensuite créerez un autre localement épinglé volume immédiatement par la suite, les tâches de création de volume hello exécutent de manière séquentielle. première tâche de création de volume Hello doit se terminer avant le début du travail de la création du volume suivant hello.
> 
> 

## <a name="modify-a-volume"></a>Modification d’un volume
Modifier un volume lorsque vous devez tooexpand ou modification hello hôtes qui accèdent aux volumes de hello.

> [!IMPORTANT]
> * Si vous modifiez la taille du volume sur le périphérique de hello hello, taille du volume hello doit toobe modifiée sur hôte hello également. 
> * les étapes de côté hôte Hello décrites ici sont pour Windows Server 2012 (2012 R2). Les procédures pour Linux ou d’autres systèmes d’exploitation sont différentes. Consultez les instructions de système d’exploitation hôte tooyour lors de la modification du volume hello sur un ordinateur hôte exécutant un autre système d’exploitation. 
> 
> 

#### <a name="toomodify-a-volume"></a>toomodify un volume
1. Sur hello **périphériques** page, sélectionnez le périphérique de hello, double-cliquez dessus, puis cliquez sur hello **conteneurs de volumes** onglet.
2. Sélectionnez un conteneur de volume à partir de la liste de hello et double-cliquez dessus tooview des volumes hello associés hello conteneur.
3. Sélectionnez un volume et en hello en bas de page de hello, cliquez sur **modifier**. Assistant Modification de volume Hello démarre.
4. Bonjour Assistant Modification de volume, sous **les paramètres de base**, vous pouvez effectuer les suivant hello :
   
   * Modifier hello **nom**.
   * Convertir hello **Type d’utilisation** à partir de tootiered attaché localement ou de toolocally hiérarchisé épinglé (consultez [modifier le type de volume hello](#change-the-volume-type) pour plus d’informations).
   * Augmenter hello **capacité approvisionnée**. Hello **capacité approvisionnée** ne peut être augmentée. Vous ne pouvez pas réduire la taille d’un volume après sa création.
5. Sous **des paramètres supplémentaires**, vous pouvez modifier hello ACR, sous réserve que hello volume est hors connexion. Si le volume de hello est en ligne, vous devez tootake il premier hors connexion. Consultez étapes toohello dans [mettre un volume hors connexion](#take-a-volume-offline) toomodifying préalable hello ACR.
   
   > [!NOTE]
   > Vous ne pouvez pas modifier hello **activer une sauvegarde par défaut** option pour le volume de hello.
   > 
   > 
6. Enregistrez vos modifications en cliquant sur une icône de coche hello ![icône-coche](./media/storsimple-manage-volumes-u2/HCS_CheckIcon.png). Hello portail Azure classic affiche un message de volume de mise à jour. Il affiche un message de réussite lorsque le volume de hello a été mis à jour avec succès.
7. Si vous développez un volume, effectuez hello sur votre ordinateur hôte Windows comme suit :
   
   1. Accédez trop**gestion de l’ordinateur** ->**gestion des disques**.
   2. Cliquez avec le bouton droit sur **Gestion des disques**, puis sélectionnez **Analyser les disques de nouveau**.
   3. Dans la liste de hello des disques, sélectionnez volume hello mis à jour, avec le bouton droit et sélectionnez **étendre le Volume**. l’Assistant étendre le Volume Hello démarre. Cliquez sur **Suivant**.
   4. Exécutez l’Assistant hello, en acceptant les valeurs par défaut de hello. Une fois hello Assistant terminé, volume de hello doit afficher hello augmenté taille.
      
      > [!NOTE]
      > Si vous développez un volume attaché localement, puis un autre localement épinglé volume immédiatement par la suite, travaux d’expansion hello volume exécutées de manière séquentielle. Hello volume d’expansion tâche doit se terminer avant le début du travail de hello suivant volume d’expansion.
      > 
      > 

![Vidéo disponible](./media/storsimple-manage-volumes-u2/Video_icon.png)**Vidéo disponible**

toowatch une vidéo qui montre comment tooexpand un volume, cliquez sur [ici](https://azure.microsoft.com/documentation/videos/expand-a-storsimple-volume/).

## <a name="change-hello-volume-type"></a>Modifier le type de volume hello
Vous pouvez modifier le type de volume hello à partir de toolocally hiérarchisé épinglée ou de tootiered attaché localement. Toutefois, cette conversion ne doit pas être effectuée fréquemment. Parmi les raisons de la conversion d’un volume de hiérarchisé toolocally épinglée sont :

* Assurance de la disponibilité et des performances des données locales.
* Élimination des latences du cloud et des problèmes de connexion au cloud.

En règle générale, ils sont petits volumes existants que vous souhaitez tooaccess fréquemment. Un volume épinglé localement est entièrement configuré lors de sa création. Si vous convertissez un volume de tooa attaché localement volume hiérarchisé, StorSimple vérifie que vous avez suffisamment d’espace sur votre appareil avant de démarrer la conversion de hello. Si vous disposez d’un manque d’espace, vous recevez une erreur et hello opération sera annulée. 

> [!NOTE]
> Avant de commencer une conversion de toolocally hiérarchisé épinglé, vérifiez que hello espace nécessaire de vos autres charges de travail. 
> 
> 

Vous souhaiterez peut-être toochange un tooa volume attaché localement à plusieurs niveaux volume si vous avez besoin d’espace supplémentaire tooprovision autres volumes. Lorsque vous convertissez tootiered de volume attaché localement de hello, hello une capacité disponible sur les appareils hello augmente en taille hello de la capacité de hello publié. Si des problèmes de connectivité empêchent hello la conversion d’un volume à partir de toohello de type local hello hiérarchisé type, hello volume local présentera de propriétés d’un volume hiérarchisé jusqu'à ce que la conversion de hello est terminée. Il s’agit, car certaines données peuvent avoir répandu toohello cloud. Ces données vidées continue toooccupy d’espace local sur l’appareil hello qui ne peut pas être libérée tant que l’opération de hello est redémarrée et achevée.

> [!NOTE]
> La conversion d’un volume peut prendre un certain temps. Vous ne pouvez pas l’annuler une fois qu’elle a commencé. volume de Hello reste en ligne pendant la conversion de hello et vous pouvez effectuer des sauvegardes, mais vous ne pouvez pas développer ou restaurer le volume de hello lors de la conversion de hello est en cours.  
> 
> 

Conversion d’un volume hiérarchisé tooa attaché localement peut nuire aux performances de l’appareil. En outre, hello suivant facteurs peut-être augmenter hello durée de conversion de hello toocomplete :

* La bande passante est insuffisante.
* Il n’existe aucune sauvegarde actuelle.

effets de hello toominimize que ces facteurs peuvent avoir :

* Passez en revue vos stratégies de limitation de bande passante et assurez-vous qu’une bande passante dédiée de 40 Mbits/s est disponible.
* Planifier la conversion hello pendant les heures creuses.
* Prendre un instantané cloud avant de commencer la conversion de hello.

Si vous convertissez plusieurs volumes (prise en charge de différentes charges de travail), vous devez classer conversion de volume hello afin que les volumes de priorité plus élevées sont tout d’abord convertis. Par exemple, vous devez convertir des volumes hébergeant des machines virtuelles ou des volumes avec des charges de travail SQL avant de convertir des volumes avec des charges de travail à partage de fichiers.

#### <a name="toochange-hello-volume-type"></a>type de volume hello toochange
1. Sur hello **périphériques** page, sélectionnez le périphérique de hello, double-cliquez dessus, puis cliquez sur hello **conteneurs de volumes** onglet.
2. Sélectionnez un conteneur de volume à partir de la liste de hello et double-cliquez dessus tooview des volumes hello associés hello conteneur.
3. Sélectionnez un volume et en hello en bas de page de hello, cliquez sur **modifier**. Assistant Modification de volume Hello démarre.
4. Sur hello **les paramètres de base** , changez le type d’utilisation hello en sélectionnant le nouveau type de hello de hello **Type d’utilisation** liste déroulante.
   
   * Si vous modifiez le type de hello trop**attaché localement**, StorSimple vérifiera toosee s’il existe une capacité suffisante.
   * Si vous modifiez le type de hello trop**à plusieurs niveaux** et ce volume sera utilisé pour les données d’archivage, sélectionnez hello **utiliser ce volume pour les données d’archive moins fréquemment sollicitées** case à cocher.
     
       ![Case à cocher Archiver](./media/storsimple-manage-volumes-u2/ModifyTieredVolEx.png)
5. Cliquez sur la flèche hello ![icône de flèche](./media/storsimple-manage-volumes-u2/HCS_ArrowIcon.png) toogo toohello **des paramètres supplémentaires** page. Si vous configurez un volume attaché localement, hello message suivant s’affiche.
   
    ![Message de modification du type de volume](./media/storsimple-manage-volumes-u2/ModifyLocalVolEx.png)
6. Cliquez sur la flèche hello ![Icône en forme de flèche](./media/storsimple-manage-volumes-u2/HCS_ArrowIcon.png) nouveau toocontinue.
7. Cliquez sur une icône de coche hello ![Icône en forme de coche](./media/storsimple-manage-volumes-u2/HCS_CheckIcon.png) processus de conversion toostart hello. Hello portail Azure affiche un message de volume de mise à jour. Il affiche un message de réussite lorsque le volume de hello a été mis à jour avec succès.

## <a name="take-a-volume-offline"></a>Mise hors connexion d’un volume
Vous devrez peut-être tootake un volume hors connexion lors de la planification toomodify ou supprimer il. Lorsqu’un volume est hors connexion, il n’est pas disponible pour l’accès en lecture-écriture. Vous devez tootake hello volume hors connexion sur l’ordinateur hôte de hello, ainsi que sur les appareils hello. 

#### <a name="tootake-a-volume-offline"></a>tootake un volume hors connexion
1. Assurez-vous que le volume hello en question n’est pas utilisé avant de mettre hors connexion.
2. Mettez d’abord volume hello hors connexion sur l’ordinateur hôte de hello. Cela élimine tout risque potentiel de corruption des données sur le volume de hello. Pour connaître la procédure, consultez instructions toohello de votre système d’exploitation hôte.
3. Une fois que l’hôte de hello est hors connexion, prenez volume de hello sur périphérique hello hors connexion en effectuant hello comme suit :
   
   1. Sur hello **périphériques** page, sélectionnez le périphérique de hello, double-cliquez dessus, puis cliquez sur hello **conteneurs de volumes** hello d’onglet **conteneurs de volumes** onglet listes dans un format tabulaire toutes les conteneurs de volumes Hello qui sont associés au périphérique de hello.
   2. Sélectionnez un conteneur de volume et cliquez dessus de la liste de hello toodisplay de tous les volumes hello conteneur hello.
   3. Sélectionnez un volume, cliquez sur **Mettre hors connexion**.
   4. Cliquez sur **Oui**lorsque vous êtes invité à confirmer l’opération. Hello volume doit maintenant être hors connexion.
      
      Une fois un volume hors connexion, hello **mettre en ligne** option est disponible.

> [!NOTE]
> Hello **mettre hors connexion** commande envoie un volume hello tootake toohello appareil hors connexion. Si les hôtes utilisent toujours le volume de hello, cela entraîne des connexions interrompues, mais mise hors connexion de volume de hello n’échouera pas. 
> 
> 

## <a name="delete-a-volume"></a>Suppression d’un volume
> [!IMPORTANT]
> Vous pouvez supprimer un volume uniquement s’il est hors connexion.
> 
> 

Terminer hello suivant les étapes toodelete un volume.

#### <a name="toodelete-a-volume"></a>toodelete un volume
1. Sur hello **périphériques** page, sélectionnez le périphérique de hello, double-cliquez dessus, puis cliquez sur hello **conteneurs de volumes** onglet.
2. Sélectionnez le conteneur de volumes hello a hello volume de toodelete. Cliquez sur Bonjour volume conteneur tooaccess Bonjour **Volumes** page.
3. Tous les volumes de hello sont associés à ce conteneur sont affichés dans un format tabulaire. Vérifier l’état de hello du volume de hello souhaité toodelete. Si hello volume de toodelete n’est pas hors connexion, des étapes il hello hors connexion de tout d’abord, suivant [mettre un volume hors connexion](#take-a-volume-offline).
4. Une fois le volume de hello est hors connexion, cliquez sur **supprimer** bas hello de page de hello.
5. Cliquez sur **Oui**lorsque vous êtes invité à confirmer l’opération. volume de Hello va être supprimée et hello **Volumes** page affiche la liste hello mis à jour des volumes hello conteneur.
   
   > [!NOTE]
   > Si vous supprimez un volume attaché localement, espace hello disponible pour les nouveaux volumes ne peut pas être mis à jour immédiatement. Hello Service StorSimple Manager met à jour disponible d’espace local hello régulièrement. Nous vous suggérons de qu'attendre quelques minutes avant d’essayer de nouveau volume de toocreate hello.<br> En outre, si vous supprimez un volume attaché localement, puis un autre localement épinglé volume immédiatement par la suite, les tâches de suppression du volume hello exécutent séquentiellement. tâche de suppression de volume premier Hello doit se terminer avant le début du travail de suppression de volume suivant hello.
   > 
   > 

## <a name="monitor-a-volume"></a>Analyse d’un volume
Surveillance du volume vous permet de toocollect I aux E/s statistiques pour un volume. Surveillance est activée par défaut pour hello 32 premiers volumes que vous créez. L’analyse des volumes supplémentaires est désactivée par défaut. L’analyse des volumes clonés est également désactivée par défaut.

Effectuer hello suivant les étapes tooenable ou désactiver la surveillance d’un volume.

#### <a name="tooenable-or-disable-volume-monitoring"></a>tooenable ou désactiver la surveillance du volume
1. Sur hello **périphériques** page, sélectionnez le périphérique de hello, double-cliquez dessus, puis cliquez sur hello **conteneurs de volumes** onglet.
2. Sélectionnez conteneur de volumes hello dans le hello volume réside, puis cliquez sur Bonjour volume conteneur tooaccess Bonjour **Volumes** page.
3. Tous les volumes de hello sont associés à ce conteneur sont répertoriés dans l’affichage sous forme de tableau de hello. Cliquez sur et sélectionnez le volume de hello ou un clone du volume.
4. Au bas de hello de page de hello, cliquez sur **modifier**.
5. Dans l’Assistant Modifier le Volume de hello, sous **les paramètres de base**, sélectionnez **activer** ou **désactiver** de hello **analyse** liste déroulante.

## <a name="next-steps"></a>Étapes suivantes
* Découvrez comment trop[cloner un volume StorSimple](storsimple-clone-volume.md).
* Découvrez comment trop[utilisez hello tooadminister du service StorSimple Manager de votre appareil StorSimple](storsimple-manager-service-administration.md).

