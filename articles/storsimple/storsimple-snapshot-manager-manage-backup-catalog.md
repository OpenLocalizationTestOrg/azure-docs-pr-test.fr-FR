---
title: "catalogue de sauvegarde de gestionnaire d’instantanés aaaStorSimple | Documents Microsoft"
description: "Décrit comment toouse hello StorSimple Snapshot Manager MMC enfichable tooview et gérer le catalogue de sauvegarde hello."
services: storsimple
documentationcenter: NA
author: SharS
manager: timlt
editor: 
ms.assetid: 6abdbfd2-22ce-45a5-aa15-38fae4c8f4ec
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 06/05/2017
ms.author: v-sharos
ms.openlocfilehash: 173410095bcec7948d780d7fc258d2e3670bde8c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-storsimple-snapshot-manager-toomanage-hello-backup-catalog"></a>Catalogue de sauvegarde de gestionnaire d’instantanés StorSimple utilisation toomanage hello

## <a name="overview"></a>Vue d'ensemble
Hello la principale fonction de gestionnaire d’instantanés StorSimple est tooallow vous toocreate cohérents avec l’application sauvegarde de copie de volumes StorSimple sous forme de hello d’instantanés. Les instantanés sont ensuite répertoriés dans un fichier XML appelé *catalogue de sauvegarde*. catalogue de sauvegarde Hello organise les instantanés par groupe de volumes, puis par instantané local ou instantané cloud.

Ce didacticiel décrit comment vous pouvez utiliser hello **catalogue de sauvegarde** hello toocomplete de nœud tâches suivantes :

* Restaurer un volume
* Cloner un volume ou un groupe de volumes
* Supprimer une sauvegarde
* Récupérer un fichier
* Restaurer la base de données du Gestionnaire d’instantanés Storsimple hello

Vous pouvez afficher le catalogue de sauvegarde hello en développant hello **catalogue de sauvegarde** nœud Bonjour **étendue** volet, puis en développant un groupe de volumes hello.

* Si vous cliquez sur le nom de groupe de volumes hello, hello **résultats** volet affiche le nombre hello d’instantanés locaux et les instantanés cloud disponibles pour le groupe de volumes hello. 
* Si vous cliquez sur **instantané Local** ou **instantané Cloud**, hello **résultats** volet affiche hello suivant des informations sur chaque instantané de sauvegarde (selon votre **Vue** paramètres) :
  
  * **Nom** – hello temps hello instantané a été pris.
  * **Type** : indique s’il s’agit d’un instantané local ou d’un instantané cloud.
  * **Propriétaire** – propriétaire du contenu hello. 
  * **Disponible** : indique si l’instantané de hello n’est actuellement disponible. **True** indique qu’un instantané hello est disponible et peut être restauré. **False** indique qu’un instantané hello n’est plus disponible. 
  * **Importé** : indique si la sauvegarde de hello a été importée. **True** indique que la sauvegarde hello a été importée à partir de hello service au niveau de l’appareil hello hello a été configuré dans le gestionnaire StorSimple Snapshot ; le Gestionnaire de périphériques StorSimple **False** indique qu’il n’a pas été importé, mais a été créé par gestionnaire d’instantanés StorSimple. (Vous pouvez facilement identifier un groupe de volumes importés, car un suffixe est ajouté qui identifie le périphérique hello à partir de laquelle le groupe de volumes hello a été importé.)
    
    ![Catalogue de sauvegarde](./media/storsimple-snapshot-manager-manage-backup-catalog/HCS_SSM_Backup_catalog.png)
* Si vous développez **instantané Local** ou **instantané Cloud**, puis cliquez sur un nom d’instantané individuel, hello **résultats** volet affiche hello suivant informations hello instantané que vous avez sélectionné :
  
  * **Nom** – hello volume identifié par la lettre de lecteur. 
  * **Nom local** – nom local de hello du lecteur hello (si disponible). 
  * **APPAREIL** hello – nom de l’appareil hello sur quel hello volume réside. 
  * **Disponible** : indique si l’instantané de hello n’est actuellement disponible. **True** indique qu’un instantané hello est disponible et peut être restauré. **False** indique qu’un instantané hello n’est plus disponible. 

## <a name="restore-a-volume"></a>Restaurer un volume
Utilisez hello suivant la procédure toorestore un volume à partir de la sauvegarde.

#### <a name="prerequisites"></a>Composants requis
Si vous ne le n'avez pas déjà fait, créez un volume et un groupe de volumes, puis supprimez les volumes hello. Par défaut, le Gestionnaire d’instantanés StorSimple sauvegarde un volume avant d’autoriser la toobe supprimé. Cette précaution peut éviter les pertes de données si le volume de hello est supprimé par inadvertance ou si les données de salutation doivent toobe récupérée pour une raison quelconque. 

Gestionnaire d’instantanés StorSimple affiche hello message suivant lors de la création de sauvegarde de secours hello.

![Message automatique d’instantané](./media/storsimple-snapshot-manager-manage-backup-catalog/HCS_SSM_Automatic_snap.png) 

> [!IMPORTANT]
> Vous ne pouvez pas supprimer un volume qui fait partie d’un groupe de volumes. option de suppression Hello n’est pas disponible. <br>
> 
> 

#### <a name="toorestore-a-volume"></a>toorestore un volume
1. Cliquez sur icône du bureau de hello toostart Gestionnaire d’instantanés StorSimple. 
2. Bonjour **étendue** volet, développez hello **catalogue de sauvegarde** nœud, développez un groupe de volumes, puis cliquez sur **instantanés locaux** ou **instantanés de Cloud**. Une liste d’instantanés de sauvegarde s’affiche dans hello **résultats** volet.
3. Sauvegarde de hello de recherche que vous souhaitez toorestore, avec le bouton droit, puis cliquez sur **restaurer**.
   
    ![Restaurer le catalogue de sauvegarde](./media/storsimple-snapshot-manager-manage-backup-catalog/HCS_SSM_Restore_BU_catalog.png) 
4. Sur la page de confirmation hello, examinez les détails de hello, tapez **confirmer**, puis cliquez sur **OK**. Gestionnaire d’instantanés StorSimple utilise un volume de hello toorestore sauvegarde hello.
   
    ![Message de confirmation de la restauration](./media/storsimple-snapshot-manager-manage-backup-catalog/HCS_SSM_Restore_volume_msg.png) 
5. Vous pouvez surveiller action de restauration hello en cours d’exécution. Bonjour **étendue** volet, développez hello **travaux** nœud, puis cliquez sur **en cours d’exécution**. Détails de la tâche Hello apparaissent dans hello **résultats** volet. Lorsque le travail de restauration hello est terminé, détails de la tâche hello sont transférée toohello **dernières 24 heures** liste.

## <a name="clone-a-volume-or-volume-group"></a>Cloner un volume ou un groupe de volumes
Utilisez hello suivant la procédure toocreate un double (clone) d’un volume ou un groupe de volumes.

#### <a name="tooclone-a-volume-or-volume-group"></a>tooclone un volume ou un groupe de volumes
1. Cliquez sur icône du bureau de hello toostart Gestionnaire d’instantanés StorSimple.
2. Bonjour **étendue** volet, développez hello **catalogue de sauvegarde** nœud, développez un groupe de volumes, puis cliquez sur **instantanés Cloud**. Liste des sauvegardes s’affiche dans hello **résultats** volet.
3. Trouver le volume de hello ou un groupe de volumes que vous voulez tooclone, volume de hello avec le bouton droit ou nom de groupe de volume, puis cliquez sur **Clone**. Hello **cloner un instantané Cloud** boîte de dialogue s’affiche.
   
    ![Cloner un instantané cloud](./media/storsimple-snapshot-manager-manage-backup-catalog/HCS_SSM_Clone.png) 
4. Hello complète **cloner un instantané Cloud** boîte de dialogue comme suit : 
   
   1. Bonjour **nom** zone de texte, tapez un nom pour hello cloner le volume. Ce nom apparaîtra dans hello **Volumes** nœud. 
   2. (Facultatif) sélectionnez **lecteur**, puis sélectionnez une lettre de lecteur à partir de la liste déroulante de hello.
   3. (Facultatif) sélectionnez **dossier (NTFS)**et tapez un chemin d’accès du dossier ou cliquez sur Parcourir et sélectionnez un emplacement pour le dossier de hello. 
   4. Cliquez sur **Créer**.
5. Hello, processus de clonage terminée, vous devez initialiser hello cloné volume. Démarrez le Gestionnaire de serveur, puis l’outil Gestion des disques. Pour obtenir des instructions détaillées, consultez la section [Monter les volumes](storsimple-snapshot-manager-manage-volumes.md#mount-volumes). Une fois qu’il est initialisé, hello volume sera répertorié sous hello **Volumes** nœud Bonjour **étendue** volet. Si vous ne voyez pas de volume hello répertorié, actualiser la liste hello des volumes (clic droit hello **Volumes** nœud, puis cliquez sur **Actualiser**).

## <a name="delete-a-backup"></a>Supprimer une sauvegarde
Utilisez hello suivant la procédure toodelete un instantané à partir du catalogue de sauvegarde hello. 

> [!NOTE]
> Suppression d’un instantané supprime hello associées hello instantané des données sauvegardée. Toutefois, les processus hello de nettoyage des données à partir du cloud de hello peuvent prendre un certain temps.<br>


#### <a name="toodelete-a-backup"></a>toodelete une sauvegarde
1. Cliquez sur icône du bureau de hello toostart Gestionnaire d’instantanés StorSimple.
2. Bonjour **étendue** volet, développez hello **catalogue de sauvegarde** nœud, développez un groupe de volumes, puis cliquez sur **instantanés locaux** ou **instantanés de Cloud**. Une liste d’instantanés s’affiche dans hello **résultats** volet.
3. Instantané d’hello avec le bouton droit vous souhaitez toodelete, puis cliquez sur **supprimer**.
4. Lorsque le message de confirmation hello s’affiche, cliquez sur **OK**.

## <a name="recover-a-file"></a>Récupérer un fichier
Si un fichier est supprimé par erreur un volume, vous pouvez récupérer le fichier de hello en récupérant un instantané antérieur à la suppression hello, à l’aide de hello instantané toocreate un clone du volume de hello, puis copiez le fichier hello hello volume d’origine du toohello volume cloné.

#### <a name="prerequisites"></a>Composants requis
Avant de commencer, assurez-vous que vous disposez d’une sauvegarde actuelle de groupe de volumes hello. Ensuite, supprimez un fichier stocké sur l’un des volumes hello dans ce groupe de volumes. Enfin, utilisez hello suivant de fichier de hello supprimé toorestore étapes à partir de votre sauvegarde. 

#### <a name="toorecover-a-deleted-file"></a>toorecover un fichier supprimé
1. Cliquez sur icône du Gestionnaire d’instantanés StorSimple hello sur votre bureau. fenêtre de console du Gestionnaire d’instantanés StorSimple Hello s’affiche. 
2. Bonjour **étendue** volet, développez hello **catalogue de sauvegarde** nœud et parcourir tooa instantané qui contient le fichier de hello supprimé. En règle générale, vous devez sélectionner un instantané qui a été créé avant la suppression hello.
3. Volume de hello de recherche que vous souhaitez tooclone, avec le bouton droit, puis cliquez sur **Clone**. Hello **cloner un instantané Cloud** boîte de dialogue s’affiche.
   
    ![Cloner un instantané cloud](./media/storsimple-snapshot-manager-manage-backup-catalog/HCS_SSM_Clone.png) 
4. Hello complète **cloner un instantané Cloud** boîte de dialogue comme suit : 
   
   1. Bonjour **nom** zone de texte, tapez un nom pour hello cloner le volume. Ce nom apparaîtra dans hello **Volumes** nœud. 
   2. (Facultatif) Sélectionnez **lecteur**, puis sélectionnez une lettre de lecteur à partir de la liste déroulante de hello. 
   3. (Facultatif) Sélectionnez **dossier (NTFS)**et tapez un chemin d’accès du dossier ou cliquez sur **Parcourir** et sélectionnez un emplacement pour le dossier de hello. 
   4. Cliquez sur **Créer**. 
5. Hello, processus de clonage terminée, vous devez initialiser hello cloné volume. Démarrez le Gestionnaire de serveur, puis l’outil Gestion des disques. Pour obtenir des instructions détaillées, consultez la section [Monter les volumes](storsimple-snapshot-manager-manage-volumes.md#mount-volumes). Une fois qu’il est initialisé, hello volume sera répertorié sous hello **Volumes** nœud Bonjour **étendue** volet. 
   
    Si vous ne voyez pas de volume hello répertorié, actualiser la liste hello des volumes (clic droit hello **Volumes** nœud, puis cliquez sur **Actualiser**).
6. Dossier NTFS hello ouvert qui contient le volume de hello cloné, développez hello **Volumes** nœud et le volume de hello puis ouvrez cloné. Trouver hello fichier que vous voulez toorecover, copiez volume principal de toohello.
7. Après avoir restauré le fichier de hello, vous pouvez supprimer le dossier NTFS hello qui contient le volume de hello cloné.

## <a name="restore-hello-storsimple-snapshot-manager-database"></a>Restaurer la base de données du Gestionnaire d’instantanés StorSimple hello
Vous devez sauvegarder régulièrement d’une base de données du Gestionnaire d’instantanés StorSimple hello sur l’ordinateur hôte hello. Si un incident se produit, ou l’ordinateur hôte hello échoue pour une raison quelconque, restaurez-la à partir de la sauvegarde de hello. Sauvegarde de base de données création hello est un processus manuel.

#### <a name="tooback-up-and-restore-hello-database"></a>tooback haut et la base de données de restauration hello
1. Arrêter hello Service de gestion StorSimple de Microsoft :
   
   1. Démarrez le Gestionnaire de serveur.
   2. Tableau de bord du Gestionnaire de serveur hello, sur hello **outils** menu, sélectionnez **Services**.
   3. Sur hello **Services** fenêtre, sélectionnez hello **Microsoft StorSimple Management Service**.
   4. Bonjour avec le bouton droit volet, sous **Microsoft StorSimple Management Service**, cliquez sur **arrêter le service de hello**.
2. Sur l’ordinateur hôte hello, accédez à tooC:\ProgramData\Microsoft\StorSimple\BACatalog. 
   
   > [!NOTE]
   > ProgramData est un dossier masqué.
   > 
   > 
3. Rechercher le fichier XML de catalogue hello, copier le fichier hello et stocker hello copier dans un emplacement sûr ou dans le cloud de hello. Si hello hôte échoue, vous pouvez utiliser ce fichier de sauvegarde toohelp recover hello stratégies de sauvegarde que vous avez créé dans Gestionnaire d’instantanés StorSimple.
   
    ![Fichier de catalogue de sauvegarde Azure StorSimple](./media/storsimple-snapshot-manager-manage-backup-catalog/HCS_SSM_bacatalog.png)
4. Redémarrez hello Service de gestion StorSimple de Microsoft : 
   
   1. Tableau de bord du Gestionnaire de serveur hello, sur hello **outils** menu, sélectionnez **Services**.
   2. Sur hello **Services** fenêtre, sélectionnez hello **Microsoft StorSimple Management Service**.
   3. Bonjour avec le bouton droit volet, sous **Microsoft StorSimple Management Service**, cliquez sur **redémarrer hello service**.
5. Sur l’ordinateur hôte hello, accédez à tooC:\ProgramData\Microsoft\StorSimple\BACatalog. 
6. Supprimer le fichier XML de catalogue hello et remplacez-la par la version de sauvegarde hello que vous avez créé. 
7. Cliquez sur hello bureau Gestionnaire d’instantanés StorSimple icône toostart Gestionnaire d’instantanés StorSimple. 

## <a name="next-steps"></a>Étapes suivantes
* En savoir plus sur [à l’aide du Gestionnaire d’instantanés StorSimple tooadminister votre solution StorSimple](storsimple-snapshot-manager-admin.md).
* En savoir plus sur [les tâches et les flux de travail du Gestionnaire d’instantanés StorSimple](storsimple-snapshot-manager-admin.md#storsimple-snapshot-manager-tasks-and-workflows).

