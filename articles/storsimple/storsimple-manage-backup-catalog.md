---
title: aaaManage votre catalogue de sauvegarde StorSimple | Documents Microsoft
description: "Explique comment toouse toolist de page de catalogue de sauvegarde de service StorSimple Manager hello, sélectionner et supprimer des jeux de sauvegarde pour un volume."
services: storsimple
documentationcenter: NA
author: SharS
manager: carmonm
editor: 
ms.assetid: ad81bee9-fe43-40b3-a384-b15fb274ecd9
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 04/28/2016
ms.author: v-sharos
ms.openlocfilehash: 14f565c174a10da2c9e2f934a533a5e493f77226
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-manager-service-toomanage-your-backup-catalog"></a>Utilisez hello StorSimple Manager service toomanage votre catalogue de sauvegarde
## <a name="overview"></a>Vue d'ensemble
Hello service StorSimple Manager **catalogue de sauvegarde** page affiche tous les jeux de sauvegarde hello qui sont créés lorsque les sauvegardes manuelles ou planifiées sont effectuées. Vous pouvez utiliser cette toolist page toutes les sauvegardes hello pour une stratégie de sauvegarde ou un volume, sélectionnez ou supprimer les sauvegardes, ou utiliser une sauvegarde toorestore ou cloner un volume.

Ce didacticiel explique comment toolist, select et supprimer une jeu de sauvegarde. toolearn comment toorestore votre périphérique de sauvegarde, accédez trop[restaurer votre appareil à partir d’un jeu de sauvegarde](storsimple-restore-from-backup-set.md). toolearn comment tooclone un volume, accédez trop[cloner un volume StorSimple](storsimple-clone-volume.md).

![Catalogue de sauvegarde](./media/storsimple-manage-backup-catalog/backupcatalog.png) 

Hello **catalogue de sauvegarde** page fournit un toonarrow requête votre sélection du jeu de sauvegarde. Vous pouvez filtrer les jeux de sauvegarde hello qui est récupérés, en fonction de hello paramètres suivants :

* **APPAREIL** – périphérique hello sur quel hello jeu de sauvegarde a été créé.
* **Stratégie de sauvegarde ou Volume** – hello stratégie de sauvegarde ou volume associé à ce jeu de sauvegarde.
* **Depuis et vers** : hello plage de date et heure de création de jeu de sauvegarde hello.

Hello jeux de sauvegarde filtrés sont ensuite sous forme de tableau en fonction de hello suivant des attributs :

* **Nom** hello – nom de la stratégie de sauvegarde hello ou volume associé au jeu de sauvegarde hello.
* **Taille** – hello taille réelle du jeu de sauvegarde hello.
* **Créé le** : date de hello et l’heure de création des sauvegardes de hello. 
* **Type** : les jeux de sauvegarde peuvent être des instantanés locaux ou des instantanés cloud. Un instantané local est une sauvegarde de toutes vos données de volume stockées localement sur le périphérique de hello, tandis qu’un instantané cloud fait référence sauvegarde toohello des données de volume résidant dans le cloud de hello. Les instantanés locaux offrent un accès plus rapide, alors que les instantanés cloud sont choisis pour la résilience des données.
* **Initié par** : les sauvegardes hello peuvent être initiées automatiquement par une planification ou manuellement par un utilisateur. Vous pouvez utiliser une sauvegarde de tooschedule de stratégie de sauvegarde. Vous pouvez également utiliser hello **sauvegarde** option tootake une sauvegarde manuelle.

## <a name="list-backup-sets-for-a-volume"></a>Répertorier les jeux de sauvegarde pour un volume
Les étapes suivantes de hello complète toolist toutes les sauvegardes de hello pour un volume.

#### <a name="toolist-backup-sets"></a>jeux de sauvegarde toolist
1. Sur la page du service StorSimple Manager hello, cliquez sur hello **catalogue de sauvegarde** onglet.
2. Filtrage des sélections de hello comme suit :
   
   1. Sélectionnez le périphérique approprié de hello.
   2. Dans la liste déroulante hello, choisissez un volume de tooview les sauvegardes hello correspondantes hello.
   3. Spécifiez la plage de temps hello.
   4. Cliquez sur une icône de coche hello ![Icône en forme de coche](./media/storsimple-manage-backup-catalog/HCS_CheckIcon.png) tooexecute cette requête.
      
      sauvegardes Hello associés au volume de hello sélectionné doivent apparaître dans la liste hello des jeux de sauvegarde.

## <a name="select-a-backup-set"></a>Sélectionner un jeu de sauvegarde
Hello complet suivant les étapes tooselect une sauvegarde définis pour une stratégie de sauvegarde ou volume.

#### <a name="tooselect-a-backup-set"></a>tooselect un jeu de sauvegarde
1. Sur la page du service StorSimple Manager hello, cliquez sur hello **catalogue de sauvegarde** onglet.
2. Filtrage des sélections de hello comme suit :
   
   1. Sélectionnez le périphérique approprié de hello.
   2. Dans la liste déroulante hello, choisissez que vous souhaitez tooselect la stratégie de sauvegarde ou volume hello pour la sauvegarde de hello.
   3. Spécifiez la plage de temps hello.
   4. Cliquez sur une icône de coche hello ![Icône en forme de coche](./media/storsimple-manage-backup-catalog/HCS_CheckIcon.png) tooexecute cette requête.
      
      Hello sauvegardes associées de stratégie de sauvegarde ou volume hello sélectionné doivent apparaître dans la liste hello des jeux de sauvegarde.
3. Sélectionnez un jeu de sauvegarde et développez-le. Hello **restaurer** et **supprimer** options s’affichent en bas de hello de page de hello. Vous pouvez effectuer une de ces actions sur un jeu de sauvegarde hello que vous avez sélectionné.

## <a name="delete-a-backup-set"></a>Supprimer un jeu de sauvegarde
Suppression d’une sauvegarde lorsque vous ne souhaitez plus des données hello tooretain associées. Effectuer hello suivant les étapes toodelete un jeu de sauvegarde.

#### <a name="toodelete-a-backup-set"></a>toodelete un jeu de sauvegarde
1. Sur la page du service StorSimple Manager hello, cliquez sur hello **onglet du catalogue de sauvegarde**.
2. Filtrage des sélections de hello comme suit :
   
   1. Sélectionnez le périphérique approprié de hello.
   2. Dans la liste déroulante hello, choisissez que vous souhaitez tooselect la stratégie de sauvegarde ou volume hello pour la sauvegarde de hello.
   3. Spécifiez la plage de temps hello.
   4. Cliquez sur une icône de coche hello ![Icône en forme de coche](./media/storsimple-manage-backup-catalog/HCS_CheckIcon.png) tooexecute cette requête.
      
      Hello sauvegardes associées de stratégie de sauvegarde ou volume hello sélectionné doivent apparaître dans la liste hello des jeux de sauvegarde.
3. Sélectionnez un jeu de sauvegarde et développez-le. Hello **restaurer** et **supprimer** options s’affichent en bas de hello de page de hello. Cliquez sur **Supprimer**.
4. Vous êtes averti lorsqu’une suppression de hello est en cours d’exécution et lorsqu’il a terminé avec succès. Après que la suppression de hello s’effectue, actualiser la requête hello sur cette page. jeu de sauvegarde Hello supprimé n’apparaît plus dans liste hello des jeux de sauvegarde.

## <a name="next-steps"></a>Étapes suivantes
* Découvrez comment trop[utilisez hello toorestore du catalogue de sauvegarde de votre appareil à partir d’un jeu de sauvegarde](storsimple-restore-from-backup-set.md).
* Découvrez comment trop[utilisez hello tooadminister du service StorSimple Manager de votre appareil StorSimple](storsimple-manager-service-administration.md).

