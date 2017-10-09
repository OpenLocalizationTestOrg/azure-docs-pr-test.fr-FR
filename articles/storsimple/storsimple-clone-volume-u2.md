---
title: "aaaClone volume de série StorSimple 8000 | Documents Microsoft"
description: "Décrit les types de clone différents hello et à quel moment toouse et explique comment vous pouvez utiliser un jeu de sauvegarde de tooclone un volume individuel."
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: 070ac53e-7388-4c48-b8a5-8ed7f9108b2c
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 07/26/2017
ms.author: alkohli
ms.openlocfilehash: f457625d2e3aa173f7ccf26984e1902a64e33b5e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-manager-service-tooclone-a-volume-update-2"></a>Utilisez hello StorSimple Manager service tooclone un volume (Update 2)
[!INCLUDE [storsimple-version-selector-clone-volume](../../includes/storsimple-version-selector-clone-volume.md)]

## <a name="overview"></a>Vue d'ensemble
Hello service StorSimple Manager **catalogue de sauvegarde** page affiche tous les jeux de sauvegarde hello qui sont créés lorsque des sauvegardes manuelles ou automatisées sont effectuées. Vous pouvez utiliser cette toolist page toutes les sauvegardes hello pour une stratégie de sauvegarde ou un volume, sélectionnez ou supprimer les sauvegardes, ou utiliser une sauvegarde toorestore ou cloner un volume.

![Page Catalogue de sauvegarde](./media/storsimple-clone-volume-u2/backupCatalog.png)  

Ce didacticiel explique comment vous pouvez utiliser un jeu de sauvegarde de tooclone un volume individuel. Elle explique également la différence de hello *temporaire* et *permanente* clone.

> [!NOTE]
> Un volume épinglé localement sera cloné comme un volume à plusieurs niveaux. Si vous avez besoin de hello toobe volume cloné attaché localement, vous pouvez convertir ce volume hello tooa attaché localement après que l’opération de clonage hello est terminée avec succès. Pour plus d’informations sur la conversion d’un tooa volume hiérarchisé localement épinglé volume, accédez trop[modifier le type de volume hello](storsimple-manage-volumes-u2.md#change-the-volume-type).
> 
> Si vous essayez tooconvert qu'un volume cloné à partir de plusieurs niveaux toolocally épinglé immédiatement après le clonage (lorsqu’il est toujours un clone temporaire), conversion de hello échoue avec hello message d’erreur suivant :
> 
> `Unable toomodify hello usage type for volume {0}. This can happen if hello volume being modified is a transient clone and hasn’t been made permanent. Take a cloud snapshot of this volume and then retry hello modify operation.` 
> 
> Cette erreur se produit uniquement si vous effectuez un clonage sur tooa autre appareil. Vous pouvez convertir correctement les toolocally de volume hello épinglé si vous convertissez d’abord clone permanent de hello clone temporaire tooa. tooconvert hello clone temporaire tooa permanente cloner, prenez un instantané cloud de celui-ci.
> 
> 

## <a name="create-a-clone-of-a-volume"></a>Création du clone d’un volume
Vous pouvez créer un clone d’hello même périphérique, un autre appareil ou même une machine virtuelle à l’aide d’une variable locale ou dans le cloud instantané.

#### <a name="tooclone-a-volume"></a>tooclone un volume
1. Sur la page du service StorSimple Manager hello, cliquez sur hello **catalogue de sauvegarde** onglet et sélectionnez un jeu de sauvegarde.
2. Développez hello jeu de sauvegarde tooview hello associée des volumes. Cliquez sur et sélectionnez un volume à partir du jeu de sauvegarde hello.
   
     ![Clonage d’un volume](./media/storsimple-clone-volume-u2/CloneVol.png) 
3. Cliquez sur **Clone** toobegin le clonage du volume de hello sélectionné.
4. Dans l’Assistant clonage de volumes de hello, sous **spécifier le nom et l’emplacement**:
   
   1. Identifiez un appareil cible. Il s’agit d’emplacement hello où clone de hello sera créé. Vous pouvez choisir hello même appareil ou spécifiez un autre périphérique. Si vous choisissez un volume associé aux autres fournisseurs de services cloud hello (pas Azure), liste déroulante répertorie pour l’appareil cible de hello affiche uniquement les périphériques physiques. Vous ne pouvez pas cloner un volume associé à d’autres fournisseurs de services cloud sur un appareil virtuel.
      
      > [!NOTE]
      > Assurez-vous que la capacité hello requise pour le clone de hello est inférieure à capacité hello disponible sur l’appareil cible de hello.
      > 
      > 
   2. Indiquez un nom de volume unique pour votre clone. nom de Hello doit contenir entre 3 et 127 caractères. 
      
      > [!NOTE]
      > Hello **Clone Volume en tant que** champ sera **à plusieurs niveaux** même si vous effectuez un clonage un volume attaché localement. Vous ne pouvez pas modifier ce paramètre ; Toutefois, si vous avez besoin de hello toobe volume cloné attaché localement, ainsi, vous pouvez convertir ce volume hello tooa attaché localement après avoir créé les clone hello. Pour plus d’informations sur la conversion d’un tooa volume hiérarchisé localement épinglé volume, accédez trop[modifier le type de volume hello](storsimple-manage-volumes-u2.md#change-the-volume-type).
      > 
      > 
      
        ![Assistant de clonage 1](./media/storsimple-clone-volume-u2/clone1.png) 
   3. Cliquez sur la flèche hello ![icône-flèche](./media/storsimple-clone-volume-u2/HCS_ArrowIcon.png) page suivante du toohello tooproceed.
5. Sous **Spécifier des hôtes qui peuvent utiliser ce volume**:
   
   1. Spécifiez un enregistrement de contrôle d’accès (ACR) pour le clone de hello. Vous pouvez ajouter un nouvel ACR ou choisissez dans la liste existante de hello.
      
        ![Assistant de clonage 2](./media/storsimple-clone-volume-u2/clone2.png) 
   2. Cliquez sur une icône de coche hello ![icône-coche](./media/storsimple-clone-volume-u2/HCS_CheckIcon.png)opération toocomplete hello.
6. Un travail de clonage sera lancé et vous serez averti lorsque hello clone est correctement créé. Cliquez sur **afficher le travail** toomonitor travail de clonage hello sur hello **travaux** page. Vous verrez hello message suivant lors de la tâche de clone hello est terminée :
   
    ![Message de clone](./media/storsimple-clone-volume-u2/CloneMsg.png) 
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
Clones temporaires sont créés uniquement lorsque vous clonez tooa autre appareil. Vous pouvez cloner un volume spécifique à partir d’un jeu de sauvegarde tooa autre périphérique géré par hello StorSimple Manager. clone temporaire de Hello sera ont des références toohello données dans le volume d’origine de hello et utilise ce tooread de données et écrire localement sur l’appareil cible de hello. 

Une fois que vous prenez un instantané cloud d’un clone temporaire, clone qui en résulte de hello sera un *permanente* clone. Pendant ce processus, une copie des données de hello est créée sur le cloud de hello hello toocopy temps que ces données sont déterminées par la taille de hello de données de hello et hello latences Azure (il s’agit d’une copie de Azure pour Azure). Ce processus peut prendre des jours tooweeks. clone temporaire de Hello devient un clone permanent de cette façon et n’a pas les références toohello données d’origine volume qui il a été cloné à partir de. 

## <a name="scenarios-for-transient-and-permanent-clones"></a>Scénarios pour les clones temporaires et permanents
Hello les sections suivantes décrire des exemples de situations dans lequel les clones permanents et temporaires peuvent être utilisés.

### <a name="item-level-recovery-with-a-transient-clone"></a>Récupération au niveau de l’élément avec un clone temporaire
Vous devez toorecover un fichier de présentation Microsoft PowerPoint un ans. Votre administrateur informatique identifie la sauvegarde spécifique de hello à cette période, et puis filtres hello volume. Hello administrateur puis clone hello volume, localise hello fichier que vous recherchez et il fournit tooyou. Dans ce scénario, un clone temporaire est utilisé. 

![Vidéo disponible](./media/storsimple-clone-volume-u2/Video_icon.png)**Vidéo disponible**

toowatch une vidéo qui montre comment vous pouvez utiliser hello clone et restaurer les fonctionnalités dans les fichiers de StorSimple toorecover supprimé, cliquez sur [ici](https://azure.microsoft.com/documentation/videos/storsimple-recover-deleted-files-with-storsimple/).

### <a name="testing-in-hello-production-environment-with-a-permanent-clone"></a>Les tests dans un environnement de production hello avec un clone permanent
Vous devez tooverify un bogue de test dans un environnement de production hello. Vous créez un clone du volume de hello dans l’environnement de production hello et prenez un instantané cloud de cette toocreate de cloner un volume cloné indépendant. Dans ce scénario, un clone permanent est utilisé.  

## <a name="next-steps"></a>Étapes suivantes
* Découvrez comment trop[restaurer un volume StorSimple à partir d’un jeu de sauvegarde](storsimple-restore-from-backup-set-u2.md).
* Découvrez comment trop[utilisez hello tooadminister du service StorSimple Manager de votre appareil StorSimple](storsimple-manager-service-administration.md).

