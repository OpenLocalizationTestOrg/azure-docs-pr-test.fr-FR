---
title: "un volume StorSimple à partir de la sauvegarde d’aaaRestore | Documents Microsoft"
description: "Explique comment toouse hello StorSimple Manager service catalogue de sauvegarde page toorestore un volume StorSimple à partir d’un jeu de sauvegarde."
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: b979782e-3184-4465-ad5f-e4516a5885d2
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 08/17/2016
ms.author: alkohli
ms.openlocfilehash: e0efa74b14603be41af0cfc5400de3c39ab8824e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="restore-a-storsimple-volume-from-a-backup-set"></a>Restauration d’un volume StorSimple à partir d’un jeu de sauvegarde
[!INCLUDE [storsimple-version-selector-restore-from-backup](../../includes/storsimple-version-selector-restore-from-backup.md)]

## <a name="overview"></a>Vue d'ensemble
Hello **catalogue de sauvegarde** page affiche tous les jeux de sauvegarde hello qui sont créés lorsque des sauvegardes manuelles ou automatisées sont effectuées. Vous pouvez utiliser cette toolist page toutes les sauvegardes hello pour une stratégie de sauvegarde ou un volume, sélectionnez ou supprimer les sauvegardes, ou utiliser une sauvegarde toorestore ou cloner un volume.

 ![Page Catalogue de sauvegarde](./media/storsimple-restore-from-backup-set/HCS_BackupCatalog.png)

Ce didacticiel explique comment toouse hello **catalogue de sauvegarde** page toorestore un volume sur votre appareil à partir d’un jeu de sauvegarde.

## <a name="how-toouse-hello-backup-catalog"></a>Comment toouse hello catalogue de sauvegarde
Hello **catalogue de sauvegarde** page fournit une requête qui vous permet de toonarrow votre sélection du jeu de sauvegarde. Vous pouvez filtrer hello jeux de sauvegarde qui est récupérés en fonction de hello paramètres suivants :

* **APPAREIL** – périphérique hello sur quel hello jeu de sauvegarde a été créé.
* **Stratégie de sauvegarde** ou **volume** – hello stratégie de sauvegarde ou volume associé à ce jeu de sauvegarde.
* **À partir de** et **à** : hello plage de date et heure de création de jeu de sauvegarde hello.

Hello jeux de sauvegarde filtrés sont ensuite sous forme de tableau en fonction de hello suivant des attributs :

* **Nom** hello – nom de la stratégie de sauvegarde hello ou volume associé au jeu de sauvegarde hello.
* **Taille** – hello taille réelle du jeu de sauvegarde hello.
* **Créé sur** : date de hello et l’heure de création des sauvegardes de hello. 
* **Type** : les jeux de sauvegarde peuvent être des instantanés locaux ou des instantanés cloud. Un instantané local est une sauvegarde de toutes vos données de volume stockées localement sur le périphérique de hello, tandis qu’un instantané cloud fait référence sauvegarde toohello des données de volume résidant dans le cloud de hello. Les instantanés locaux offrent un accès plus rapide, alors que les instantanés cloud sont choisis pour la résilience des données.
* **Initié par** : les sauvegardes hello peuvent être lancées automatiquement en fonction de tooa planification ou manuellement par un utilisateur. (Vous pouvez utiliser les sauvegardes tooschedule stratégie de sauvegarde. Vous pouvez également utiliser hello **sauvegarde** option tootake une sauvegarde interactive.)

## <a name="how-toorestore-your-storsimple-volume-from-a-backup"></a>Comment toorestore votre volume StorSimple à partir d’une sauvegarde
Vous pouvez utiliser hello **catalogue de sauvegarde** page toorestore votre volume StorSimple à partir d’une sauvegarde spécifique. 

> [!WARNING]
> Restauration à partir d’une sauvegarde remplace les volumes existants hello à partir de la sauvegarde de hello. Cela peut entraîner une perte de hello de toutes les données écrites après que hello sauvegarde a été effectuée.
> 
> 

Avant de lancer une restauration sur un volume, vérifiez que le volume de hello est hors connexion. Vous devez tout d’abord les volumes hello tootake hors connexion sur l’ordinateur hôte de hello et puis hello appareil. Suivez les étapes de hello dans [mettre un volume hors connexion](storsimple-manage-volumes.md#take-a-volume-offline). Effectuer hello suivant les étapes toorestore un volume à partir d’un jeu de sauvegarde.

### <a name="toorestore-from-a-backup-set"></a>toorestore à partir d’un jeu de sauvegarde
1. Sur la page du service StorSimple Manager hello, cliquez sur hello **catalogue de sauvegarde** onglet.
   
    ![Catalogue de sauvegarde](./media/storsimple-restore-from-backup-set/HCS_Restore.png)
2. Sélectionnez un jeu de sauvegarde comme suit :
   
   1. Sélectionnez le périphérique approprié de hello.
   2. Dans la liste déroulante hello, choisissez que vous souhaitez tooselect la stratégie de sauvegarde ou volume hello pour la sauvegarde de hello.
   3. Spécifiez la plage de temps hello.
   4. Cliquez sur une icône de coche hello ![icône en forme de coche](./media/storsimple-restore-from-backup-set/HCS_CheckIcon.png) tooexecute cette requête.
      
      Hello sauvegardes associées de stratégie de sauvegarde ou volume hello sélectionné doivent apparaître dans la liste hello des jeux de sauvegarde.
3. Développez hello jeu de sauvegarde tooview hello associée des volumes. Ces volumes doivent être mis hors connexion sur l’hôte de hello et de périphérique avant de les restaurer. Suivez les étapes de hello dans [mettre un volume hors connexion](storsimple-manage-volumes.md#take-a-volume-offline).
   
   > [!IMPORTANT]
   > Assurez-vous que vous avez effectué des volumes hello hors connexion sur l’ordinateur hôte de hello tout d’abord, avant de mettre hors connexion les volumes hello sur le périphérique de hello. Si vous ne prenez pas les volumes hello hors connexion sur l’ordinateur hôte de hello, il pourrait endommager toodata corruption.
   > 
   > 
4. Sélectionnez un jeu de sauvegarde. Cliquez sur **restaurer** bas hello de page de hello.
5. Vous êtes invité à confirmer l’opération. 
   
    ![Page Confirmation](./media/storsimple-restore-from-backup-set/HCS_ConfirmRestore.png)
6. Passez en revue les informations de restauration hello et cliquez sur une icône de coche hello ![icône de coche](./media/storsimple-restore-from-backup-set/HCS_CheckIcon.png). Ceci lancera un travail de restauration que vous pouvez afficher en accédant à hello **travaux** page. 
7. Une fois la restauration de hello est terminée, vous pouvez vérifier que le contenu hello de vos volumes est remplacés par les volumes de sauvegarde de hello.

![Vidéo disponible](./media/storsimple-restore-from-backup-set/Video_icon.png)**Vidéo disponible**

toowatch une vidéo qui montre comment vous pouvez utiliser hello clone et restaurer les fonctionnalités dans les fichiers de StorSimple toorecover supprimé, cliquez sur [ici](https://azure.microsoft.com/documentation/videos/storsimple-recover-deleted-files-with-storsimple/).

## <a name="next-steps"></a>Étapes suivantes
* Découvrez comment trop[StorSimple de gérer les volumes](storsimple-manage-volumes.md).
* Découvrez comment trop[utilisez hello tooadminister du service StorSimple Manager de votre appareil StorSimple](storsimple-manager-service-administration.md).

