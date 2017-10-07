---
title: aaaClone votre volume StorSimple | Documents Microsoft
description: "Décrit les types de clone différents hello et à quel moment toouse et explique comment vous pouvez utiliser un jeu de sauvegarde de tooclone un volume individuel."
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: b5d615f2-02a7-4222-9867-6c0385ce748c
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 08/17/2016
ms.author: alkohli
ms.openlocfilehash: e98d28db1abeb515ba78ab5860e7c5eba0dfcbb5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-manager-service-tooclone-a-volume"></a>Utilisez hello StorSimple Manager service tooclone un volume
[!INCLUDE [storsimple-version-selector-clone-volume](../../includes/storsimple-version-selector-clone-volume.md)]

## <a name="overview"></a>Vue d'ensemble
Hello service StorSimple Manager **catalogue de sauvegarde** page affiche tous les jeux de sauvegarde hello qui sont créés lorsque des sauvegardes manuelles ou automatisées sont effectuées. Vous pouvez utiliser cette toolist page toutes les sauvegardes hello pour une stratégie de sauvegarde ou un volume, sélectionnez ou supprimer les sauvegardes, ou utiliser une sauvegarde toorestore ou cloner un volume.

![Page Catalogue de sauvegarde](./media/storsimple-clone-volume/HCS_BackupCatalog.png)  

Ce didacticiel explique comment vous pouvez utiliser un jeu de sauvegarde de tooclone un volume individuel. Elle explique également la différence de hello *temporaire* et *permanente* clone. 

## <a name="create-a-clone-of-a-volume"></a>Création du clone d’un volume
Vous pouvez créer un clone sur hello même périphérique, un autre périphérique ou même un ordinateur virtuel à l’aide d’une variable locale ou un instantané cloud.

#### <a name="tooclone-a-volume"></a>tooclone un volume
1. Sur la page du service StorSimple Manager hello, cliquez sur hello **catalogue de sauvegarde** onglet et sélectionnez un jeu de sauvegarde.
2. Développez hello jeu de sauvegarde tooview hello associée des volumes. Cliquez sur et sélectionnez un volume à partir du jeu de sauvegarde hello.
   
     ![Clonage d’un volume](./media/storsimple-clone-volume/HCS_Clone.png) 
3. Cliquez sur **Clone** toobegin le clonage du volume de hello sélectionné.
4. Dans l’Assistant clonage de volumes de hello, sous **spécifier le nom et l’emplacement**:
   
   1. Identifiez un appareil cible. Il s’agit d’emplacement hello où clone de hello sera créé. Vous pouvez choisir hello même appareil ou spécifiez un autre périphérique. Si vous choisissez un volume associé aux autres fournisseurs de services cloud hello (pas Azure), liste déroulante répertorie pour l’appareil cible de hello affiche uniquement les périphériques physiques. Vous ne pouvez pas cloner un volume associé à d’autres fournisseurs de services cloud sur un appareil virtuel.
      
      > [!NOTE]
      > Assurez-vous que la capacité hello requise pour le clone de hello est inférieure à capacité hello disponible sur l’appareil cible de hello.
      > 
      > 
   2. Indiquez un nom de volume unique pour votre clone. nom de Hello doit contenir entre 3 et 127 caractères.
   3. Cliquez sur la flèche hello ![icône-flèche](./media/storsimple-clone-volume/HCS_ArrowIcon.png) page suivante du toohello tooproceed.
5. Sous **Spécifier des hôtes qui peuvent utiliser ce volume**:
   
   1. Spécifiez un enregistrement de contrôle d’accès (ACR) pour le clone de hello. Vous pouvez ajouter un nouvel ACR ou choisissez dans la liste existante de hello.
   2. Cliquez sur une icône de coche hello ![icône-coche](./media/storsimple-clone-volume/HCS_CheckIcon.png)opération toocomplete hello.
6. Un travail de clonage sera lancé et vous serez averti lorsque hello clone est correctement créé. Cliquez sur **afficher le travail** toomonitor travail de clonage hello sur hello **travaux** page.
7. Après avoir hello travail de clonage est terminée :
   
   1. Accédez toohello **périphériques** page et sélectionnez hello **conteneurs de volumes** onglet. 
   2. Sélectionnez le conteneur de volume hello associé au volume source hello que vous avez cloné. Dans la liste de hello des volumes, vous devez voir clone hello qui vient d’être créé.

> [!NOTE]
> La surveillance et la sauvegarde par défaut sont automatiquement désactivées sur un volume cloné.
> 
> 

Un clone créé de cette manière est un clone temporaire. Pour plus d’informations sur les types de clone, consultez la page [Clones temporaires et permanents](#transient-vs-permanent-clones).

Ce clone est désormais un volume normal et toutes les opérations possibles sur un volume seront disponibles pour le clone de hello. Vous devez tooconfigure ce volume pour toutes les sauvegardes.

## <a name="transient-vs-permanent-clones"></a>Clones temporaires et permanents
Clones permanents et temporaires sont créés uniquement lorsque vous clonez sur tooa autre appareil. Vous pouvez cloner un volume spécifique à partir d’un jeu de sauvegarde tooa autre appareil. Un clone créé de cette manière est un clone *temporaire* . clone temporaire de Hello aura le volume d’origine de références toohello et utilisera ce tooread volume lors de l’écriture en local. 

Une fois que vous prenez un instantané cloud d’un clone temporaire, clone qui en résulte de hello sera un *permanente* clone. clone permanent de Hello est indépendant et n’a pas un volume d’origine de toohello références qui il a été cloné à partir de.  

## <a name="scenarios-for-transient-and-permanent-clones"></a>Scénarios pour les clones temporaires et permanents
Hello les sections suivantes décrire des exemples de situations dans lequel les clones permanents et temporaires peuvent être utilisés.

### <a name="item-level-recovery-with-a-transient-clone"></a>Récupération au niveau de l’élément avec un clone temporaire
Vous devez toorecover un fichier de présentation Microsoft PowerPoint un ans. Votre administrateur informatique identifie la sauvegarde spécifique de hello à cette période, et puis filtres hello volume. Hello administrateur puis clone hello volume, localise hello fichier que vous recherchez et il fournit tooyou. Dans ce scénario, un clone temporaire est utilisé. 

![Vidéo disponible](./media/storsimple-clone-volume/Video_icon.png)**Vidéo disponible**

toowatch une vidéo qui montre comment vous pouvez utiliser hello clone et restaurer les fonctionnalités dans les fichiers de StorSimple toorecover supprimé, cliquez sur [ici](https://azure.microsoft.com/documentation/videos/storsimple-recover-deleted-files-with-storsimple/).

### <a name="testing-in-hello-production-environment-with-a-permanent-clone"></a>Les tests dans un environnement de production hello avec un clone permanent
Vous devez tooverify un bogue de test dans un environnement de production hello. Vous créez un clone du volume de hello dans l’environnement de production hello en prenant un instantané cloud de ce clone. Hello volume cloné est désormais indépendant. Dans ce scénario, un clone permanent est utilisé.

## <a name="next-steps"></a>Étapes suivantes
* Découvrez comment trop[restaurer un volume StorSimple à partir d’un jeu de sauvegarde](storsimple-restore-from-backup-set.md).
* Découvrez comment trop[utilisez hello tooadminister du service StorSimple Manager de votre appareil StorSimple](storsimple-manager-service-administration.md).

