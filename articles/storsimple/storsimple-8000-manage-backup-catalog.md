---
title: aaaManage votre catalogue de sauvegarde StorSimple | Documents Microsoft
description: "Explique comment toouse hello toolist de page pour le Gestionnaire de périphériques StorSimple service catalogue de sauvegarde, sélectionnez et supprimer des jeux de sauvegarde."
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
ms.date: 06/29/2017
ms.author: alkohli
ms.openlocfilehash: e464609e74409a06a198790719abd82ed03c03d9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-device-manager-service-toomanage-your-backup-catalog"></a>Utilisez hello le Gestionnaire de périphériques StorSimple service toomanage votre catalogue de sauvegarde
## <a name="overview"></a>Vue d'ensemble
Hello service du Gestionnaire de périphériques StorSimple **catalogue de sauvegarde** panneau affiche tous les jeux de sauvegarde hello qui sont créés lorsque les sauvegardes manuelles ou planifiées sont effectuées. Vous pouvez utiliser cette toolist page toutes les sauvegardes hello pour une stratégie de sauvegarde ou un volume, sélectionnez ou supprimer les sauvegardes, ou utiliser une sauvegarde toorestore ou cloner un volume.

Ce didacticiel explique comment toolist, select et supprimer une jeu de sauvegarde. toolearn comment toorestore votre périphérique de sauvegarde, accédez trop[restaurer votre appareil à partir d’un jeu de sauvegarde](storsimple-8000-restore-from-backup-set-u2.md). toolearn comment tooclone un volume, accédez trop[cloner un volume StorSimple](storsimple-8000-clone-volume-u2.md).

![Catalogue de sauvegarde](./media/storsimple-8000-manage-backup-catalog/bucatalog.png) 

Hello **catalogue de sauvegarde** panneau fournit un toonarrow requête votre sélection du jeu de sauvegarde. Vous pouvez filtrer les jeux de sauvegarde hello qui est récupérés, en fonction de hello paramètres suivants :

* **APPAREIL** – périphérique hello sur quel hello jeu de sauvegarde a été créé.
* **Stratégie de sauvegarde ou Volume** – hello stratégie de sauvegarde ou volume associé à ce jeu de sauvegarde.
* **Depuis et vers** : hello plage de date et heure de création de jeu de sauvegarde hello.

Hello jeux de sauvegarde filtrés sont ensuite sous forme de tableau en fonction de hello suivant des attributs :

* **Nom** hello – nom de la stratégie de sauvegarde hello ou volume associé au jeu de sauvegarde hello.
* **Taille** – hello taille réelle du jeu de sauvegarde hello.
* **Créé le** : date de hello et l’heure de création des sauvegardes de hello. 
* **Type** : les jeux de sauvegarde peuvent être des instantanés locaux ou des instantanés cloud. Un instantané local est une sauvegarde de toutes vos données de volume stockées localement sur le périphérique de hello, tandis qu’un instantané cloud fait référence sauvegarde toohello des données de volume résidant dans le cloud de hello. Les instantanés locaux offrent un accès plus rapide, alors que les instantanés cloud sont choisis pour la résilience des données.
* **Initié par** : les sauvegardes hello peuvent être initiées automatiquement par une planification ou manuellement par un utilisateur. Vous pouvez utiliser une sauvegarde de tooschedule de stratégie de sauvegarde. Vous pouvez également utiliser hello **sauvegarde** option tootake une sauvegarde manuelle.

## <a name="list-backup-sets-for-a-backup-policy"></a>Répertorier les jeux de sauvegarde pour une stratégie de sauvegarde
Les étapes suivantes de hello complète toolist toutes les sauvegardes de hello pour une stratégie de sauvegarde.

#### <a name="toolist-backup-sets"></a>jeux de sauvegarde toolist
1. Atteindre le service du Gestionnaire de périphériques StorSimple tooyour et cliquez sur **catalogue de sauvegarde**.

2. Filtrage des sélections de hello comme suit :
   
   1. Spécifiez la plage de temps hello.
   2. Sélectionnez le périphérique approprié de hello.
   3. Filtrer par **stratégie de sauvegarde** tooview hello sauvegardes hello correspondantes.
   3. Dans la liste déroulante de stratégie de sauvegarde hello, choisissez **tous les** tooview tous hello hello sélectionné des sauvegardes appareil.
   4. Cliquez sur **appliquer** tooexecute cette requête.
      
      les sauvegardes de Hello associées de stratégie de sauvegarde hello sélectionné doivent apparaître dans la liste hello des jeux de sauvegarde.

      ![Accédez toobackup catalogue](./media/storsimple-8000-manage-backup-catalog/bucatalog1.png)

## <a name="select-a-backup-set"></a>Sélectionner un jeu de sauvegarde
Hello complet suivant les étapes tooselect une sauvegarde définis pour une stratégie de sauvegarde ou volume.

#### <a name="tooselect-a-backup-set"></a>tooselect un jeu de sauvegarde
1. Atteindre le service du Gestionnaire de périphériques StorSimple tooyour et cliquez sur **catalogue de sauvegarde**.
2. Filtrage des sélections de hello comme suit :
   
   1. Spécifiez la plage de temps hello. 
   2. Sélectionnez le périphérique approprié de hello. 
   3. Filtrer par la stratégie de sauvegarde ou de volume pour la sauvegarde hello que vous souhaitez tooselect.
   4. Cliquez sur **appliquer** tooexecute cette requête.
      
      Hello sauvegardes associées de stratégie de sauvegarde ou volume hello sélectionné doivent apparaître dans la liste hello des jeux de sauvegarde.

      ![Accédez toobackup catalogue](./media/storsimple-8000-manage-backup-catalog/bucatalog1.png)

3. Sélectionnez un jeu de sauvegarde et développez-le. Vous pouvez maintenant voir les jeux de sauvegarde hello ventilées par volumes hello qu’il contient. Hello **restaurer** et **supprimer** options sont disponibles via le menu contextuel de hello (clic droit) pour le jeu de sauvegarde hello. Vous pouvez effectuer une de ces actions sur un jeu de sauvegarde hello que vous avez sélectionné.

    ![Accédez toobackup catalogue](./media/storsimple-8000-manage-backup-catalog/bucatalog2.png)

## <a name="delete-a-backup-set"></a>Supprimer un jeu de sauvegarde
Suppression d’une sauvegarde lorsque vous ne souhaitez plus des données hello tooretain associées. Effectuer hello suivant les étapes toodelete un jeu de sauvegarde.

#### <a name="toodelete-a-backup-set"></a>toodelete un jeu de sauvegarde
 Atteindre le service du Gestionnaire de périphériques StorSimple tooyour et cliquez sur **catalogue de sauvegarde**.
2. Filtrage des sélections de hello comme suit :
   
   1. Spécifiez la plage de temps hello. 
   2. Sélectionnez le périphérique approprié de hello. 
   3. Filtrer par la stratégie de sauvegarde ou de volume pour la sauvegarde hello que vous souhaitez tooselect.
   4. Cliquez sur **appliquer** tooexecute cette requête.
      
      Hello sauvegardes associées de stratégie de sauvegarde ou volume hello sélectionné doivent apparaître dans la liste hello des jeux de sauvegarde.

      ![Accédez toobackup catalogue](./media/storsimple-8000-manage-backup-catalog/bucatalog1.png)

3. Sélectionnez un jeu de sauvegarde et développez-le. Vous pouvez maintenant voir les jeux de sauvegarde hello ventilées par volumes hello qu’il contient. Hello **restaurer** et **supprimer** options sont disponibles via le menu contextuel de hello (clic droit) pour le jeu de sauvegarde hello. Cliquez sur le jeu de sauvegarde hello sélectionné et à partir du menu contextuel de hello, sélectionnez **supprimer**.

    ![Accédez toobackup catalogue](./media/storsimple-8000-manage-backup-catalog/bucatalog3.png)

4. Lorsque vous êtes invité à confirmer l’opération, passez en revue les informations hello affiché, puis cliquez sur **supprimer**. sauvegarde sélectionnée de Hello est supprimé définitivement.

    ![Accédez toobackup catalogue](./media/storsimple-8000-manage-backup-catalog/bucatalog4.png)  

5. Vous êtes averti lorsqu’une suppression de hello est en cours d’exécution et lorsqu’il a terminé avec succès. Après que la suppression de hello s’effectue, actualiser la requête hello sur cette page. jeu de sauvegarde Hello supprimé n’apparaît plus dans liste hello des jeux de sauvegarde.

    ![Accédez toobackup catalogue](./media/storsimple-8000-manage-backup-catalog/bucatalog7.png)

## <a name="next-steps"></a>Étapes suivantes
* Découvrez comment trop[utilisez hello toorestore du catalogue de sauvegarde de votre appareil à partir d’un jeu de sauvegarde](storsimple-8000-restore-from-backup-set-u2.md).
* Découvrez comment trop[utilisez hello tooadminister du service Gestionnaire de périphériques StorSimple votre appareil StorSimple](storsimple-8000-manager-service-administration.md).

