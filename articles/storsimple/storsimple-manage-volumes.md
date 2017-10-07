---
title: aaaManage vos volumes StorSimple | Documents Microsoft
description: "Explique comment tooadd, modifier, surveiller et supprimer des volumes StorSimple et tootake les hors connexion si nécessaire."
services: storsimple
documentationcenter: NA
author: SharS
manager: carmonm
editor: 
ms.assetid: ccabd859-590c-4568-a81d-6ff38f125be3
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 05/11/2016
ms.author: v-sharos
ms.openlocfilehash: 8dc646261ee2ad8f2b80291518716f4de55b63f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-manager-service-toomanage-volumes"></a>Utiliser les volumes toomanage hello StorSimple Manager
[!INCLUDE [storsimple-version-selector-manage-volumes](../../includes/storsimple-version-selector-manage-volumes.md)]

## <a name="overview"></a>Vue d'ensemble
Ce didacticiel explique comment toouse hello toocreate du service StorSimple Manager et gestion des volumes sur l’appareil StorSimple hello et un appareil virtuel StorSimple.

Hello service StorSimple Manager est une extension de hello portail classique Azure qui vous permet de gérer votre solution StorSimple à partir d’une seule interface web. Dans des volumes plus toomanaging, vous pourrez utiliser toocreate de service StorSimple Manager hello et gérer les services StorSimple, afficher et gérer des appareils, afficher les alertes et afficher et gérer les stratégies de sauvegarde et de catalogue de sauvegarde hello.

> [!NOTE]
> Azure StorSimple peut créer uniquement des volumes alloués dynamiquement. Vous ne pouvez pas créer de volumes entièrement ou partiellement alloués sur un système Azure StorSimple.
> 
> Allocation dynamique est une technologie de virtualisation dans lequel le stockage disponible apparaît tooexceed des ressources physiques. Plutôt que de réserver suffisamment de stockage à l’avance, Azure StorSimple utilise tooallocate provisionnement dynamique juste assez toomeet d’espace nécessaire en cours. Cette approche facilite la nature évolutive de Hello de stockage cloud, car Azure StorSimple peut augmenter ou diminuer les besoins changeants de toomeet de stockage cloud.
> 
> 

## <a name="hello-volumes-page"></a>page de Volumes Hello
Hello **Volumes** page vous permet de volumes de stockage hello toomanage qui sont configurés sur l’appareil Microsoft Azure StorSimple hello pour vos initiateurs (serveurs). Il affiche la liste hello des volumes sur votre appareil StorSimple.

 ![Page volumes](./media/storsimple-manage-volumes/HCS_VolumesPage.png)

Un volume est constitué d’une série d’attributs :

* **Nom** – un nom descriptif qui doit être uniques et permet d’identifier le volume de hello. Ce nom est également utilisé dans les rapports d’analyse lorsque vous filtrez sur un volume particulier.
* **État** : peut être en ligne ou hors connexion. Si un volume est hors connexion, il n’est pas visible tooinitiators (serveurs) autorisés accès toouse hello volume.
* **Capacité** – spécifie la taille hello volume est perçue par l’initiateur hello (serveur). La capacité indique la quantité totale de hello de données qui peuvent être stockées à l’initiateur hello (serveur). Les volumes sont alloués dynamiquement et les données dédupliquées. Cela implique que votre appareil ne Préalloue pas la capacité de stockage physique en interne ou sur le cloud hello selon la capacité du volume tooconfigured. capacité du volume Hello est allouée et consommée à la demande.
* **Type** – type de volume hello peut être à plusieurs niveaux ou d’archivage (un sous-type de multi-niveau)
* **Accès** – spécifie les initiateurs hello (serveurs) autorisés accès toothis volume. Les initiateurs qui ne sont pas membres de l’enregistrement de contrôle d’accès (ACR) qui est associé au volume de hello ne voient pas de volume de hello.
* **Analyse** : indique si un volume est ou non en cours d’analyse. Par défaut, l’analyse est activée au moment de la création du volume. Toutefois, elle est désactivée pour un volume cloné. tooenable d’analyse pour un volume, suivez les instructions de hello dans le moniteur d’un volume.

les tâches les plus courantes Hello associés à un volume sont :

* Ajout d’un volume
* Modification d’un volume
* Suppression d’un volume
* Mise hors connexion d’un volume
* Analyse d’un volume

## <a name="add-a-volume"></a>Ajout d’un volume
Vous [avez créé un volume](storsimple-deployment-walkthrough-u1.md#step-6-create-a-volume) lors du déploiement de votre solution StorSimple. La procédure d’ajout d’un volume est similaire.

### <a name="tooadd-a-volume"></a>tooadd un volume
1. Sur hello **périphériques** page, sélectionnez le périphérique de hello, double-cliquez dessus, puis cliquez sur hello **conteneurs de volumes** onglet.
2. Sélectionnez un conteneur de volume et cliquez sur la flèche hello dans hello correspondant ligne tooaccess hello volumes associés hello conteneur.
3. Cliquez sur **ajouter** bas hello de page de hello. Assistant Ajout d’un volume de Hello démarre.
   
     ![Assistant Ajout de volume, paramètres de base](./media/storsimple-manage-volumes/AddVolume1.png)
4. Bonjour Assistant Ajout d’un volume, sous **les paramètres de base**, hello suivant :
   
   1. Saisissez un **nom** pour le volume.
   2. Spécifiez hello **capacité approvisionnée** pour votre volume en Go ou to. capacité de Hello doit être comprise entre 1 et 64 To pour un périphérique physique. capacité maximale Hello qui peut être configurée pour un volume sur un périphérique virtuel StorSimple est de 30 To.
   3. Sélectionnez hello **Type d’utilisation** pour votre volume. Si vous utilisez hello volume à plusieurs niveaux pour les données d’archivage, en sélectionnant hello **utiliser ce volume pour les données d’archive moins fréquemment sollicitées** case à cocher modifie la taille de segment de la déduplication de hello pour votre volume too512 Ko. Si vous ne sélectionnez pas de cette option, le volume de hiérarchisé correspondant hello utilisera une taille de segment de 64 Ko. Une plus grande taille de segment de la déduplication permet de transfert hello tooexpedite des appareils hello du cloud toohello de données d’archivage volumineux. (Les volumes hiérarchisés ont été précédemment appelés volumes principales).
   4. Cliquez sur la flèche hello ![icône de flèche](./media/storsimple-manage-volumes/HCS_ArrowIcon.png)toogo toohello **des paramètres supplémentaires** page.
      
        ![Assistant Ajout de volume, paramètres avancés](./media/storsimple-manage-volumes/AddVolume2.png)
5. Sous **Paramètres supplémentaires**, ajoutez un enregistrement de contrôle d’accès (ACR) :
   
   1. Sélectionnez un enregistrement de contrôle d’accès (ACR) à partir de la liste déroulante de hello. Vous pouvez également ajouter un nouvel enregistrement de contrôle d’accès. ACR déterminent quels hôtes peuvent accéder à vos volumes par correspondance hello hôte IQN associé à celui répertorié dans l’enregistrement de hello.
   2. Nous vous recommandons d’activer une sauvegarde par défaut en sélectionnant hello **activer une sauvegarde par défaut pour ce volume** case à cocher.
   3. Cliquez sur une icône de coche hello ![Icône en forme de coche](./media/storsimple-manage-volumes/HCS_CheckIcon.png) volume de hello toocreate avec hello spécifié les paramètres.

Le nouveau volume est maintenant prêt toouse.

## <a name="modify-a-volume"></a>Modification d’un volume
Modifier un volume lorsque vous devez tooexpand ou modification hello hôtes qui accèdent aux volumes de hello.

> [!IMPORTANT]
> * Si vous modifiez la taille du volume sur le périphérique de hello hello, taille du volume hello doit toobe modifiée sur hôte hello également.
> * les étapes de côté hôte Hello décrites ici sont pour Windows Server 2012 (2012 R2). Les procédures pour Linux ou d’autres systèmes d’exploitation sont différentes. Consultez les instructions de système d’exploitation hôte tooyour lors de la modification du volume hello sur un ordinateur hôte exécutant un autre système d’exploitation.
> 
> 

### <a name="toomodify-a-volume"></a>toomodify un volume
1. Sur hello **périphériques** page, sélectionnez le périphérique de hello, double-cliquez dessus, puis cliquez sur hello **conteneur de volumes** onglet. Cette page répertorie dans un format tabulaire de tous les conteneurs de volumes hello qui sont associés au périphérique de hello.
2. Sélectionnez un conteneur de volume et cliquez dessus de la liste de hello toodisplay de tous les volumes hello conteneur hello.
3. Sur hello **Volumes** page, sélectionnez un volume, cliquez sur **modifier**.
4. Bonjour Assistant Modification de volume, sous **les paramètres de base**, vous pouvez effectuer les suivant hello :
   
   * Modifier hello **nom** et **Type** si vous souhaitez toomodify un volume d’archive tooan volume hiérarchisé en sélectionnant hello **utiliser ce volume pour les données d’archive moins fréquemment sollicitées** taille de segment de déduplication case à cocher toochange hello pour votre volume too512 Ko.
   * Augmenter hello **capacité approvisionnée**. Hello **capacité approvisionnée** ne peut être augmentée. Vous ne pouvez pas réduire la taille d’un volume après sa création.
     
     > [!NOTE]
     > Vous ne pouvez pas modifier le conteneur de volume hello après que qu’elle est affectée tooa volume.
     > 
     > 
5. Sous **des paramètres supplémentaires**, vous pouvez effectuer les suivant hello :
   
   * Modifier hello ACR, sous réserve que hello volume est hors connexion. Si le volume de hello est en ligne, vous devez tootake il premier hors connexion. Consultez étapes toohello dans [mettre un volume hors connexion](#take-a-volume-offline) toomodifying préalable hello ACR.
   * Modifier la liste hello d’ACR après que hello volume est hors connexion.
     
     > [!NOTE]
     > Vous ne pouvez pas modifier hello **activer une sauvegarde par défaut pour ce volume** option pour le volume de hello.
     > 
     > 
6. Enregistrez vos modifications en cliquant sur une icône de coche hello ![icône-coche](./media/storsimple-manage-volumes/HCS_CheckIcon.png). Hello portail Azure classic affiche un message de volume de mise à jour. Il affiche un message de réussite lorsque le volume de hello a été mis à jour avec succès.
7. Si vous développez un volume, effectuez hello sur votre ordinateur hôte Windows comme suit :
   
   1. Accédez trop**gestion de l’ordinateur** ->**gestion des disques**.
   2. Cliquez avec le bouton droit sur **Gestion des disques**, puis sélectionnez **Analyser les disques de nouveau**.
   3. Dans la liste de hello des disques, sélectionnez volume hello mis à jour, avec le bouton droit et sélectionnez **étendre le Volume**. l’Assistant étendre le Volume Hello démarre. Cliquez sur **Suivant**.
   4. Exécutez l’Assistant hello, en acceptant les valeurs par défaut de hello. Une fois hello Assistant terminé, volume de hello doit afficher hello augmenté taille.

![Vidéo disponible](./media/storsimple-manage-volumes/Video_icon.png)**Vidéo disponible**

toowatch une vidéo qui montre comment tooexpand un volume, cliquez sur [ici](https://azure.microsoft.com/documentation/videos/expand-a-storsimple-volume/).

## <a name="take-a-volume-offline"></a>Mise hors connexion d’un volume
Vous devrez peut-être tootake un volume hors connexion lors de la planification toomodify ou supprimer il. Lorsqu’un volume est hors connexion, il n’est pas disponible pour l’accès en lecture-écriture. Vous devez tootake hello volume hors connexion sur l’ordinateur hôte de hello, ainsi que sur les appareils hello. Effectuer hello suivant les étapes tootake un volume hors connexion.

### <a name="tootake-a-volume-offline"></a>tootake un volume hors connexion
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

### <a name="toodelete-a-volume"></a>toodelete un volume
1. Sur hello **périphériques** page, sélectionnez le périphérique de hello, double-cliquez dessus, puis cliquez sur hello **conteneurs de volumes** onglet.
2. Sélectionnez le conteneur de volumes hello a hello volume de toodelete. Cliquez sur Bonjour volume conteneur tooaccess Bonjour **Volumes** page.
3. Tous les volumes de hello sont associés à ce conteneur sont affichés dans un format tabulaire. Vérifier l’état de hello du volume de hello souhaité toodelete. Si hello volume de toodelete n’est pas hors connexion, des étapes il hello hors connexion de tout d’abord, suivant [mettre un volume hors connexion](#take-a-volume-offline).
4. Une fois le volume de hello est hors connexion, cliquez sur **supprimer** bas hello de page de hello.
5. Cliquez sur **Oui**lorsque vous êtes invité à confirmer l’opération. volume de Hello va être supprimée et hello **Volumes** page affiche la liste hello mis à jour des volumes hello conteneur.

## <a name="monitor-a-volume"></a>Analyse d’un volume
Surveillance du volume vous permet de toocollect I aux E/s statistiques pour un volume. Surveillance est activée par défaut pour hello 32 premiers volumes que vous créez. L’analyse des volumes supplémentaires est désactivée par défaut. L’analyse des volumes clonés est également désactivée par défaut.

Effectuer hello suivant les étapes tooenable ou désactiver la surveillance d’un volume.

### <a name="tooenable-or-disable-volume-monitoring"></a>tooenable ou désactiver la surveillance du volume
1. Sur hello **périphériques** page, sélectionnez le périphérique de hello, double-cliquez dessus, puis cliquez sur hello **conteneurs de volumes** onglet.
2. Sélectionnez conteneur de volumes hello dans le hello volume réside, puis cliquez sur Bonjour volume conteneur tooaccess Bonjour **Volumes** page.
3. Tous les volumes de hello sont associés à ce conteneur sont répertoriés dans l’affichage sous forme de tableau de hello. Cliquez sur et sélectionnez le volume de hello ou un clone du volume.
4. Au bas de hello de page de hello, cliquez sur **modifier**.
5. Dans l’Assistant Modifier le Volume de hello, sous **les paramètres de base**, sélectionnez **activer** ou **désactiver** de hello **analyse** liste déroulante.
   
    ![Modifier un volume, paramètres de base](./media/storsimple-manage-volumes/HCS_MonitorVolumeM.png)

## <a name="next-steps"></a>Étapes suivantes
* Découvrez comment trop[cloner un volume StorSimple](storsimple-clone-volume.md).
* Découvrez comment trop[utilisez hello tooadminister du service StorSimple Manager de votre appareil StorSimple](storsimple-manager-service-administration.md).

