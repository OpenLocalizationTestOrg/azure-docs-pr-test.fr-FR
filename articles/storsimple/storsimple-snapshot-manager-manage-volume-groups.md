---
title: "groupes de volumes Gestionnaire d’instantanés aaaStorSimple | Documents Microsoft"
description: "Décrit comment toouse hello StorSimple Snapshot Manager MMC enfichable toocreate et gérer des groupes de volumes."
services: storsimple
documentationcenter: NA
author: SharS
manager: carmonm
editor: 
ms.assetid: 7a232414-6a28-4b81-bd7b-cf61e28b33d7
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 06/05/2017
ms.author: v-sharos
ms.openlocfilehash: f7830b62761db7aa5139456b555b6168fb6a85de
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-storsimple-snapshot-manager-toocreate-and-manage-volume-groups"></a>Utilisez le Gestionnaire d’instantanés StorSimple toocreate et gérer des groupes de volumes
## <a name="overview"></a>Vue d'ensemble
Vous pouvez utiliser hello **groupes de volumes** nœud sur hello **étendue** groupes toovolume du volet tooassign volumes, afficher des informations sur un groupe de volumes, planifiez des sauvegardes et modifier des groupes de volumes.

Groupes de volumes sont des pools de tooensure de volumes associés utilisés que les sauvegardes sont cohérentes avec les applications. Pour plus d’informations, consultez les sections [Volumes et groupes de volumes](storsimple-what-is-snapshot-manager.md#volumes-and-volume-groups) et [Intégration avec le service VSS de Windows](storsimple-what-is-snapshot-manager.md#integration-with-windows-volume-shadow-copy-service).

> [!IMPORTANT]
> * Tous les volumes d’un groupe de volumes doivent provenir d’un fournisseur de services cloud unique.
> * Lorsque vous configurez des groupes de volumes, ne mélangez pas les volumes partagés de cluster (CSV) non-CSV dans hello même groupe de volumes. Gestionnaire d’instantanés StorSimple ne prend pas en charge un mélange de volumes partagés de cluster et non-CSV dans hello même instantané.

![Nœud de groupes de volumes](./media/storsimple-snapshot-manager-manage-volume-groups/HCS_SSM_Volume_groups.png)

**Figure 1 : Nœud Groupes de volumes du Gestionnaire d’instantanés StorSimple** 

Ce didacticiel vous explique comment utiliser le Gestionnaire d’instantanés StorSimple pour :

* Afficher des informations sur vos groupes de volumes
* Créer un groupe de volumes
* Sauvegarder un groupe de volumes
* Modifier un groupe de volumes
* Supprimer un groupe de volumes

Toutes ces actions sont également disponibles sur hello **Actions** volet.

## <a name="view-volume-groups"></a>Afficher les groupes de volumes
Si vous cliquez sur hello **groupes de volumes** nœud, hello **résultats** volet affiche hello suivant des informations sur chaque groupe de volumes, en fonction des sélections de colonne hello vous apporter. (hello colonnes Bonjour **résultats** volet sont configurables. Avec le bouton hello **Volumes** nœud, sélectionnez **vue**, puis sélectionnez **Ajout/Suppression de colonnes**.)

| Colonne de résultats | Description |
|:--- |:--- |
| Nom |Hello **nom** colonne contient le nom de hello du groupe de volumes hello. |
| Application |Hello **Applications** colonne indique le nombre de hello d’enregistreurs VSS actuellement installés et en cours d’exécution hello hôte Windows. |
| Sélectionné |Hello **sélectionnés** colonne indique le nombre de hello de volumes qui sont contenus dans le groupe de volumes hello. Zéro (0) indique qu’aucune application n’est associée à des volumes dans le groupe de volumes hello hello. |
| Volumes importés |Hello **importé** colonne indique le nombre de hello de volumes importés. Lorsque la valeur trop**True**, cette colonne indique qu’un groupe de volumes ont été importé à partir de hello portail Azure et qu’il a été créé pas de gestionnaire d’instantanés StorSimple. |

> [!NOTE]
> Groupes de volumes StorSimple Snapshot Manager sont également affichées sur hello **stratégies de sauvegarde** onglet Bonjour portail Azure.
> 
> 

## <a name="create-a-volume-group"></a>Créer un groupe de volumes
Utilisez hello suivant la procédure toocreate un groupe de volumes.

#### <a name="toocreate-a-volume-group"></a>toocreate un groupe de volumes
1. Cliquez sur icône du bureau de hello toostart Gestionnaire d’instantanés StorSimple.
2. Bonjour **étendue** volet, avec le bouton droit **groupes de volumes**, puis cliquez sur **créer un groupe de volumes**.
   
    ![Créer un groupe de volumes](./media/storsimple-snapshot-manager-manage-volume-groups/HCS_SSM_Create_volume_group.png)
   
    Hello **créer un groupe de volumes** boîte de dialogue s’affiche.
   
    ![Boîte de dialogue Créer un groupe de volumes](./media/storsimple-snapshot-manager-manage-volume-groups/HCS_SSM_CreateVolumeGroup_dialog.png)
3. Entrez hello informations suivantes :
   
   1. Bonjour **nom** , tapez un nom unique pour le nouveau groupe de volumes hello.
   2. Bonjour **Applications** zone, sélectionnez les applications associées aux volumes hello que vous allez ajouter un groupe de volumes toohello.
      
       Hello **Applications** listes case à cocher uniquement les applications qui utilisent des volumes StorSimple et sont dotées d’enregistreurs VSS sont activées. Un enregistreur VSS est activé uniquement si tous les hello volumes que l’enregistreur hello connaît sont des volumes StorSimple. Si les Applications hello est vide, aucune des applications qui utilisent des volumes StorSimple d’Azure et sont prise en charge des enregistreurs VSS ne sont installées. (Actuellement, Azure StorSimple prend en charge Microsoft Exchange et SQL Server.) Pour plus d’informations sur les enregistreurs VSS, consultez la page [Intégration avec le service VSS de Windows](storsimple-what-is-snapshot-manager.md#integration-with-windows-volume-shadow-copy-service).
      
       Si vous sélectionnez une application, l’ensemble des volumes associés sont automatiquement sélectionnés. À l’inverse, si vous sélectionnez les volumes associés à une application spécifique, application hello est sélectionnée automatiquement dans hello **Applications** boîte. 
   3. Bonjour **Volumes** , sélectionnez le groupe de volumes StorSimple volumes tooadd toohello. 
      
      * Vous pouvez inclure des volumes à une ou plusieurs partitions. (Les volumes à plusieurs partitions peuvent être des disques dynamiques ou des disques de base avec plusieurs partitions.) Un volume contenant plusieurs partitions est traité comme une unité unique. Par conséquent, si vous ajoutez seul groupe de volumes tooa hello partitions, hello toutes les autres partitions sont automatiquement ajoutés toothat volume groupe au hello même temps. Après avoir ajouté un groupe de volumes plusieurs partition volume tooa, hello plusieurs volumes de partition continue toobe traité comme une unité unique.
      * Vous pouvez créer des groupes de volumes vides en affectant ne pas de n’importe quel toothem de volumes. 
      * Ne mélangez pas les volumes partagés de cluster (CSV) non-CSV dans hello même groupe de volumes. Gestionnaire d’instantanés StorSimple ne prend pas en charge un mélange de volumes partagés de cluster et non-volumes partagés de cluster dans hello même instantané.
4. Cliquez sur **OK** groupe de volumes toosave hello.

## <a name="back-up-a-volume-group"></a>Sauvegarder un groupe de volumes
Utilisez hello suivant tooback procédure d’un groupe de volumes.

#### <a name="tooback-up-a-volume-group"></a>tooback d’un groupe de volumes
1. Cliquez sur icône du bureau de hello toostart Gestionnaire d’instantanés StorSimple.
2. Bonjour **étendue** volet, développez hello **groupes de volumes** nœud, cliquez sur un nom de groupe de volumes, puis cliquez sur **créer une sauvegarde**.
   
    ![Sauvegarde immédiate d’un groupe de volumes](./media/storsimple-snapshot-manager-manage-volume-groups/HCS_SSM_Take_backup.png)
3. Bonjour **créer une sauvegarde** boîte de dialogue, sélectionnez **instantané Local** ou **instantané Cloud**, puis cliquez sur **créer**.
   
    ![Boîte de dialogue Démarrer la sauvegarde](./media/storsimple-snapshot-manager-manage-volume-groups/HCS_SSM_TakeBackup_dialog.png)
4. tooconfirm hello sauvegarde est en cours d’exécution, développez hello **travaux** nœud, puis cliquez sur **en cours d’exécution**. sauvegarde de Hello doit être répertorié.
5. hello tooview terminé d’instantané, développez hello **catalogue de sauvegarde** nœud, développez le nom de groupe de volumes hello, puis cliquez sur **instantané Local** ou **instantané Cloud**. sauvegarde de Hello s’afficheront si elle est terminée correctement.

## <a name="edit-a-volume-group"></a>Modifier un groupe de volumes
Utilisez hello suivant la procédure tooedit un groupe de volumes.

#### <a name="tooedit-a-volume-group"></a>tooedit un groupe de volumes
1. Cliquez sur icône du bureau de hello toostart Gestionnaire d’instantanés StorSimple.
2. Bonjour **étendue** volet, développez hello **groupes de volumes** nœud, cliquez sur un nom de groupe de volumes, puis cliquez sur **modifier**.
3. Hello ** créer un groupe de volumes ** boîte de dialogue s’affiche. Vous pouvez modifier hello **nom**, **Applications**, et **Volumes** entrées.
4. Cliquez sur **OK** toosave vos modifications.

## <a name="delete-a-volume-group"></a>Supprimer un groupe de volumes
Utilisez hello suivant la procédure toodelete un groupe de volumes. 

> [!WARNING]
> Cette opération supprime également toutes les sauvegardes hello associés à un groupe de volumes hello.
> 
> 

#### <a name="toodelete-a-volume-group"></a>toodelete un groupe de volumes
1. Cliquez sur icône du bureau de hello toostart Gestionnaire d’instantanés StorSimple.
2. Bonjour **étendue** volet, développez hello **groupes de volumes** nœud, cliquez sur un nom de groupe de volumes, puis cliquez sur **supprimer**.
3. Hello **supprimer un groupe de volumes** boîte de dialogue s’affiche. Type **confirmer** dans hello de zone de texte, puis cliquez sur **OK**.
   
    groupe de volumes Hello supprimé n’est plus répertorié dans liste hello hello **résultats** volet et toutes les sauvegardes qui sont associés à ce groupe de volumes sont supprimés à partir du catalogue de sauvegarde hello.

## <a name="next-steps"></a>Étapes suivantes
* Découvrez comment trop[utiliser le Gestionnaire d’instantanés StorSimple tooadminister votre solution StorSimple](storsimple-snapshot-manager-admin.md).
* Découvrez comment trop[utiliser le Gestionnaire d’instantanés StorSimple toocreate et gérer des stratégies de sauvegarde](storsimple-snapshot-manager-manage-backup-policies.md).

