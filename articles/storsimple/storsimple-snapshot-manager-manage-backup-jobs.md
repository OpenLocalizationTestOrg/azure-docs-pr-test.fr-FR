---
title: "les travaux de sauvegarde de gestionnaire d’instantanés aaaStorSimple | Documents Microsoft"
description: "Décrit comment toouse hello StorSimple Snapshot Manager MMC enfichable tooview et gérer des travaux de sauvegarde planifiées, en cours d’exécution et terminées."
services: storsimple
documentationcenter: NA
author: SharS
manager: timlt
editor: 
ms.assetid: bf4dcff6-c819-4766-b9d9-9922831cb200
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 06/05/2017
ms.author: v-sharos
ms.openlocfilehash: 3dba0a2aa527d17d67130f537bcdce5722b05a76
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-storsimple-snapshot-manager-tooview-and-manage-backup-jobs"></a>Utilisez le Gestionnaire d’instantanés StorSimple tooview et gérer des travaux de sauvegarde

## <a name="overview"></a>Vue d'ensemble
Hello **travaux** nœud Bonjour **étendue** volet affiche hello **planifiée**, **dernières 24 heures**, et **en cours d’exécution**les tâches que vous avez lancées de façon interactive ou par une stratégie configurée de sauvegarde. 

Ce didacticiel explique comment vous pouvez utiliser hello **travaux** informations sur les nœuds toodisplay sur les travaux de sauvegarde planifiées, récentes et en cours d’exécution. (hello la liste des tâches et les informations correspondantes s’affiche dans hello **résultats** volet.) Vous pouvez également cliquer avec le bouton droit sur une tâche répertoriée et afficher un menu contextuel présentant les actions disponibles.

## <a name="view-scheduled-jobs"></a>Afficher les tâches planifiées
Hello utilisation suivant la procédure tooview des travaux de sauvegarde planifiés.

#### <a name="tooview-scheduled-jobs"></a>travaux de tooview planifié
1. Cliquez sur icône du bureau de hello toostart Gestionnaire d’instantanés StorSimple. 
2. Bonjour **étendue** volet, développez hello **travaux** nœud, puis cliquez sur **planifiée**. Hello informations suivantes s’affichent dans hello **résultats** volet :
   
   * **Nom** hello – nom de l’instantané programmé de hello
   * **Prochaine exécution** : hello date et heure de capture instantanée planifiée suivante, hello
   * **La dernière exécution** : hello date et heure d’instantané hello planifiée le plus récent
     
     > [!NOTE]
     > Pour les instantanés uniquement à usage unique, hello **prochaine exécution** et **dernière exécution** sera même hello.
     
     ![Tâches de sauvegarde planifiées](./media/storsimple-snapshot-manager-manage-backup-jobs/HCS_SSM_Jobs_scheduled.png) 
3. tooperform des actions supplémentaires sur une tâche spécifique, cliquez sur le nom de travail de hello Bonjour **résultats** volet et sélectionnez des options de menu hello.

## <a name="view-recent-jobs"></a>Afficher les tâches récentes
Utilisez hello après procédure tooview sauvegarde et restauration des travaux qui ont été effectués dans hello des dernières 24 heures.

#### <a name="tooview-recent-jobs"></a>travaux récents tooview
1. Cliquez sur icône du bureau de hello toostart Gestionnaire d’instantanés StorSimple.
2. Bonjour **étendue** volet, développez hello **travaux** nœud, puis cliquez sur **dernières 24 heures**. Hello **résultats** volet affiche les tâches de sauvegarde pour hello des dernières 24 heures (maximum tooa 64 travaux). Hello informations suivantes s’affichent dans hello **résultats** volet, en fonction de hello **vue** options que vous spécifiez :
   
   * **Nom** hello – nom de l’instantané programmé de hello.
   * **Démarré** : date de hello et l’heure de début de l’instantané d’hello.
   * **Arrêté** – date de hello et l’heure instantané d’hello terminée ou a été arrêté.
   * **Écoulé** – durée hello entre hello **démarré** et **arrêté** fois.
   * **État** – hello état du travail de hello viennent de se terminer. **Réussite** indique que la sauvegarde hello a été créée avec succès. **Échec de** indique que le travail hello ne s’est pas exécuté correctement.
   * **Informations** : hello raison de l’échec de hello.
   * **Octets traités (Mo)** – quantité hello de données à partir du groupe de volumes hello qui a été traité (en Mo). 
     
     ![Travaux exécutés hello des dernières 24 heures](./media/storsimple-snapshot-manager-manage-backup-jobs/HCS_SSM_Jobs_Last_24_hours.png) 
3. tooperform des actions supplémentaires sur une tâche spécifique, cliquez sur le nom de travail de hello Bonjour **résultats** volet et sélectionnez des options de menu hello.
   
    ![Supprimer un travail](./media/storsimple-snapshot-manager-manage-backup-catalog/HCS_SSM_Delete_backup.png)

## <a name="view-currently-running-jobs"></a>Afficher les tâches en cours d’exécution
Utilisez hello suivant travaux tooview procédure en cours d’exécution.

#### <a name="tooview-currently-running-jobs"></a>tooview travaux en cours d’exécution
1. Cliquez sur icône du bureau de hello toostart Gestionnaire d’instantanés StorSimple.
2. Bonjour **étendue** volet, développez hello **travaux** nœud, puis cliquez sur **en cours d’exécution**. En fonction de hello **vue** options que vous spécifiez, hello informations suivantes s’affichent dans hello **résultats** volet :
   
   * **Nom** hello – nom de l’instantané programmé de hello.
   * **Démarré** : date de hello et l’heure de début de l’instantané d’hello.
   * **Point de contrôle** – hello action en cours de sauvegarde de hello.
   * **État** – hello pourcentage d’achèvement.
   * **Écoulé** – hello durée écoulée depuis le début de la sauvegarde hello. 
   * **Débit moyen (Mo)** – taux total d’octets de toothat de traitement des données de temps total nécessaire pour le traitement (Mo).
   * **Octets traités (Mo)** : nombre total d’octets de données traités (en Mo).
   * **Octets écrits (Mo)** : nombre total d’octets de données écrits (en Mo). Il inclut les données de salutation ainsi que les métadonnées de hello et n’est donc généralement supérieur à hello octets traités.
     
     ![Tâches en cours d’exécution](./media/storsimple-snapshot-manager-manage-backup-jobs/HCS_SSM_Jobs_running.png)
3. tooperform des actions supplémentaires sur une tâche spécifique, cliquez sur le nom de travail de hello Bonjour **résultats** volet et sélectionnez des options de menu hello.

## <a name="next-steps"></a>Étapes suivantes
* Découvrez comment trop[utiliser le Gestionnaire d’instantanés StorSimple tooadminister votre solution StorSimple](storsimple-snapshot-manager-admin.md).
* Découvrez comment trop[utiliser le catalogue de sauvegarde de gestionnaire d’instantanés StorSimple toomanage hello](storsimple-snapshot-manager-manage-backup-catalog.md).

