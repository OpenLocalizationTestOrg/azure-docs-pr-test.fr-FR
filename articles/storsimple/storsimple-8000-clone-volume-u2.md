---
title: "aaaClone un volume sur la série StorSimple 8000 | Documents Microsoft"
description: "Décrit l’utilisation et les types de clone différents hello et explique comment vous pouvez utiliser un tooclone de jeu de sauvegarde un volume individuel sur un appareil de série StorSimple 8000."
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
ms.workload: TBD
ms.date: 07/26/2017
ms.author: alkohli
ms.openlocfilehash: 4f7e1f62f17c7b2bd72820a00a5ab87b7e192332
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-device-manager-service-in-azure-portal-tooclone-a-volume"></a>Utiliser le service du Gestionnaire de périphériques StorSimple hello dans tooclone portail Azure un volume

## <a name="overview"></a>Vue d'ensemble

Ce didacticiel décrit comment vous pouvez utiliser un jeu de sauvegarde de tooclone un volume individuel via hello **catalogue de sauvegarde** panneau. Elle explique également la différence de hello *temporaire* et *permanente* clone. Guide de Hello dans ce didacticiel s’applique appareil de série hello StorSimple 8000 tooall en cours d’exécution mise à jour 3 ou version ultérieure.

Hello service du Gestionnaire de périphériques StorSimple **catalogue de sauvegarde** panneau affiche tous les jeux de sauvegarde hello qui sont créés lorsque des sauvegardes manuelles ou automatisées sont effectuées. Vous pouvez ensuite sélectionner un volume dans un tooclone de jeu de sauvegarde.

 ![Liste des jeux de sauvegarde](./media/storsimple-8000-clone-volume-u2/bucatalog.png)

## <a name="considerations-for-cloning-a-volume"></a>Remarques relatives au clonage d’un volume

Prendre en compte les informations suivantes lors du clonage d’un volume de hello.

- Un clone comporte dans hello même façon qu’un volume normal. Toute opération qui est possible sur un volume est disponible pour les clones hello.

- La surveillance et la sauvegarde par défaut sont automatiquement désactivées sur un volume cloné. Vous devez tooconfigure un volume cloné pour toutes les sauvegardes.

- Un volume épinglé localement est cloné comme un volume à plusieurs niveaux. Si vous avez besoin de hello toobe volume cloné attaché localement, vous pouvez convertir ce volume hello tooa attaché localement après que l’opération de clonage hello est terminée avec succès. Pour plus d’informations sur la conversion d’un tooa volume hiérarchisé localement épinglé volume, accédez trop[modifier le type de volume hello](storsimple-8000-manage-volumes-u2.md#change-the-volume-type).

- Si vous essayez tooconvert qu'un volume cloné à partir de plusieurs niveaux toolocally épinglé immédiatement après le clonage (lorsqu’il est toujours un clone temporaire), conversion de hello échoue avec hello message d’erreur suivant :

    `Unable toomodify hello usage type for volume {0}. This can happen if hello volume being modified is a transient clone and hasn’t been made permanent. Take a cloud snapshot of this volume and then retry hello modify operation.`

    Cette erreur se produit uniquement si vous effectuez un clonage sur tooa autre appareil. Vous pouvez convertir correctement les toolocally de volume hello épinglé si vous convertissez d’abord clone permanent de hello clone temporaire tooa. Prendre un instantané de cloud de hello clone temporaire tooconvert il clone permanent de tooa.

## <a name="create-a-clone-of-a-volume"></a>Création du clone d’un volume

Vous pouvez créer un clone d’hello même périphérique, un autre périphérique ou même un dispositif de cloud à l’aide d’une variable locale ou dans le cloud instantané.

procédure de Hello ci-dessous décrit comment toocreate un clone à partir de hello catalogue de sauvegarde.  Un clone de l’autre méthode tooinitiate est toogo trop**Volumes**un volume, puis cliquez sur le menu contextuel de hello tooinvoke et sélectionnez **Clone**.

Effectuer hello suivant étapes toocreate un clone du volume de votre catalogue de sauvegarde hello.

#### <a name="tooclone-a-volume"></a>tooclone un volume

1. Atteindre le service du Gestionnaire de périphériques StorSimple tooyour, puis cliquez sur **catalogue de sauvegarde**.

2. Sélectionnez un jeu de sauvegarde comme suit :
   
   1. Sélectionnez le périphérique approprié de hello.
   2. Dans la liste déroulante hello, choisissez que vous souhaitez tooselect la stratégie de sauvegarde ou volume hello pour la sauvegarde de hello.
   3. Spécifiez la plage de temps hello.
   4. Cliquez sur **appliquer** tooexecute cette requête.

    Hello sauvegardes associées de stratégie de sauvegarde ou volume hello sélectionné doivent apparaître dans la liste hello des jeux de sauvegarde.
   
    ![Liste des jeux de sauvegarde](./media/storsimple-8000-clone-volume-u2/bucatalog.png)
     
3. Développez hello jeu de sauvegarde tooview hello associée des volumes. Ces volumes doivent être mis hors connexion sur l’hôte de hello et de périphérique avant de les restaurer. Accès aux volumes hello sur hello **Volumes** Panneau de votre appareil, puis hello de suivre les étapes [mettre un volume hors connexion](storsimple-8000-manage-volumes-u2.md#take-a-volume-offline) tootake hors connexion.
   
   > [!IMPORTANT]
   > Assurez-vous que vous avez effectué des volumes hello hors connexion sur l’ordinateur hôte de hello tout d’abord, avant de mettre hors connexion les volumes hello sur le périphérique de hello. Si vous ne prenez pas les volumes hello hors connexion sur l’ordinateur hôte de hello, il pourrait endommager toodata corruption.
   
4. Accédez arrière toohello **catalogue de sauvegarde** et sélectionnez un volume dans un jeu de sauvegarde. Avec le bouton droit et, dans le menu contextuel de hello, sélectionnez **Clone**.

   ![Liste des jeux de sauvegarde](./media/storsimple-8000-clone-volume-u2/clonevol3b.png) 

3. Bonjour **Clone** panneau, hello comme suit :
   
    1. Identifiez un appareil cible. Il s’agit d’emplacement hello où clone de hello sera créé. Vous pouvez choisir hello même appareil ou spécifiez un autre périphérique.

      > [!NOTE]
      > Assurez-vous que la capacité hello requise pour le clone de hello est inférieure à capacité hello disponible sur l’appareil cible de hello.
       
    2. Indiquez un nom de volume unique pour votre clone. nom de Hello doit contenir entre 3 et 127 caractères.
      
        > [!NOTE]
        > Hello **Clone Volume en tant que** champ sera **à plusieurs niveaux** même si vous effectuez un clonage un volume attaché localement. Vous ne pouvez pas modifier ce paramètre ; Toutefois, si vous avez besoin de hello toobe volume cloné attaché localement, ainsi, vous pouvez convertir ce volume hello tooa attaché localement après avoir créé les clone hello. Pour plus d’informations sur la conversion d’un tooa volume hiérarchisé localement épinglé volume, accédez trop[modifier le type de volume hello](storsimple-8000-manage-volumes-u2.md#change-the-volume-type).
          
    3. Sous **connecté des ordinateurs hôtes**, spécifiez un enregistrement de contrôle d’accès (ACR) pour le clone de hello. Vous pouvez ajouter un nouvel ACR ou choisissez dans la liste existante de hello. Hello ACR déterminera les hôtes peuvent accéder à ce clone.
      
        ![Liste des jeux de sauvegarde](./media/storsimple-8000-clone-volume-u2/clonevol3a.png) 

    4. Cliquez sur **Clone** opération hello de toocomplete.

4. Un travail de clonage est initialisé, et vous êtes averti lorsque hello clone est correctement créé. Cliquez sur la notification de travail hello ou accédez trop**travaux** travail de clonage panneau toomonitor hello.

    ![Liste des jeux de sauvegarde](./media/storsimple-8000-clone-volume-u2/clonevol5.png)

7. Une fois le travail de clonage hello est terminée, accédez tooyour appareil, puis **Volumes**. Dans la liste de hello des volumes, vous devez voir clone hello qui vient d’être créé dans hello même conteneur de volume disposant de volumes source hello.

    ![Liste des jeux de sauvegarde](./media/storsimple-8000-clone-volume-u2/clonevol6.png)

Un clone créé de cette manière est un clone temporaire. Pour plus d’informations sur les types de clone, consultez la page [Clones temporaires et permanents](#transient-vs-permanent-clones).


## <a name="transient-vs-permanent-clones"></a>Clones temporaires et permanents
Clones temporaires sont créés uniquement lorsque vous clonez tooanother appareil. Vous pouvez cloner un volume spécifique à partir d’un jeu de sauvegarde tooa autre périphérique géré par hello StorSimple le Gestionnaire de périphériques. clone temporaire de Hello possède des références toohello données dans le volume d’origine de hello et utilise ce tooread de données et d’écriture localement sur l’appareil cible de hello.

Une fois que vous prenez un instantané cloud d’un clone temporaire, clone qui en résulte de hello est un *permanente* clone. Pendant ce processus, une copie des données de hello est créée sur le cloud de hello hello toocopy temps que ces données sont déterminées par la taille de hello de données de hello et hello latences Azure (il s’agit d’une copie de Azure pour Azure). Ce processus peut prendre des jours tooweeks. clone temporaire de Hello devient un clone permanent et n’a pas les références toohello données d’origine volume qui il a été cloné à partir de.

## <a name="scenarios-for-transient-and-permanent-clones"></a>Scénarios pour les clones temporaires et permanents
Hello les sections suivantes décrire des exemples de situations dans lequel les clones permanents et temporaires peuvent être utilisés.

### <a name="item-level-recovery-with-a-transient-clone"></a>Récupération au niveau de l’élément avec un clone temporaire
Vous devez toorecover un fichier de présentation Microsoft PowerPoint un ans. Votre administrateur informatique identifie la sauvegarde spécifique de hello à ce stade, et puis filtres hello volume. Hello administrateur puis clone hello volume, localise hello fichier que vous recherchez et il fournit tooyou. Dans ce scénario, un clone temporaire est utilisé.

### <a name="testing-in-hello-production-environment-with-a-permanent-clone"></a>Les tests dans un environnement de production hello avec un clone permanent
Vous devez tooverify un bogue de test dans un environnement de production hello. Vous créez un clone du volume de hello dans l’environnement de production hello et prenez un instantané cloud de cette toocreate de cloner un volume cloné indépendant. Dans ce scénario, un clone permanent est utilisé.

## <a name="next-steps"></a>Étapes suivantes
* Découvrez comment trop[restaurer un volume StorSimple à partir d’un jeu de sauvegarde](storsimple-8000-restore-from-backup-set-u2.md).
* Découvrez comment trop[utilisez hello tooadminister du service Gestionnaire de périphériques StorSimple votre appareil StorSimple](storsimple-8000-manager-service-administration.md).

