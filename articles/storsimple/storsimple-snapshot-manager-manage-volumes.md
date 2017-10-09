---
title: "aaaStorSimple Gestionnaire d’instantanés et les volumes | Documents Microsoft"
description: "Décrit comment toouse hello StorSimple Snapshot Manager MMC enfichable tooview et gérer les volumes et sauvegardes de tooconfigure."
services: storsimple
documentationcenter: NA
author: SharS
manager: carmonm
editor: 
ms.assetid: 78896323-e57c-431e-bbe2-0cbde1cf43a2
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 04/18/2016
ms.author: v-sharos
ms.openlocfilehash: b8ce102d082b7c773d667a9d3ec747be9e1d3064
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-storsimple-snapshot-manager-tooview-and-manage-volumes"></a>Utilisez le Gestionnaire d’instantanés StorSimple tooview et gestion des volumes
## <a name="overview"></a>Vue d'ensemble
Vous pouvez utiliser le Gestionnaire d’instantanés StorSimple de hello **Volumes** nœud (sur hello **étendue** volet) tooselect volumes et afficher des informations à leur sujet. les volumes de Hello sont présentés en tant que lecteurs qui correspondent toohello les volumes montés par hello hôte. Hello **Volumes** nœud affiche les volumes locaux et les types de volumes qui sont prises en charge par StorSimple, notamment les volumes détectés via l’utilisation de hello d’iSCSI et un appareil. 

Pour plus d’informations sur les volumes pris en charge, accédez trop[prise en charge de plusieurs types de volume](storsimple-what-is-snapshot-manager.md#support-for-multiple-volume-types).

![Liste des volumes dans le volet Résultats](./media/storsimple-snapshot-manager-manage-volumes/HCS_SSM_Volume_node.png)

Hello **Volumes** nœud vous permet également de rescanner ou de supprimer des volumes une fois le Gestionnaire d’instantanés StorSimple les détecte. 

Ce didacticiel vous explique comment monter, initialiser et formater les volumes, puis utiliser le Gestionnaire d’instantanés StorSimple pour :

* Afficher des informations sur les volumes 
* Supprimer des volumes
* Relancer l’analyse des volumes 
* Configurer un volume de base et le sauvegarder
* Configurer un volume dynamique mis en miroir et le sauvegarder

> [!NOTE]
> Tous les hello **Volume** nœud actions sont également disponibles dans hello **Actions** volet.
> 
> 

## <a name="mount-volumes"></a>Monter les volumes
Hello d’utilisation suivant la procédure toomount, initialiser et formater les volumes StorSimple. Cette procédure utilise la gestion des disques, un utilitaire système de gestion des disques durs et les volumes correspondants hello ou des partitions. Pour plus d’informations sur la gestion des disques, consultez trop[gestion des disques](https://technet.microsoft.com/library/cc770943.aspx) sur le site Web de Microsoft TechNet hello.

#### <a name="toomount-volumes"></a>volumes toomount
1. Sur votre ordinateur hôte, démarrez l’initiateur iSCSI Microsoft hello.
2. Indiquez une des adresses IP portail cible de hello hello interface ou adresse IP de détection et connecter toohello appareil. Une fois hello est connecté, les volumes de hello seront accessibles tooyour Windows system. Pour plus d’informations sur l’utilisation de l’initiateur iSCSI Microsoft hello, accédez toohello section « Périphérique cible iSCSI connexion tooan » [installation et configuration de Microsoft iSCSI Initiator][1].
3. Utiliser les hello suivant options toostart gestion des disques :
   
   * Tapez Diskmgmt.msc Bonjour **exécuter** boîte.
   * Démarrez le Gestionnaire de serveur, développez hello **stockage** nœud et sélectionnez **gestion des disques**.
   * Démarrer **outils d’administration**, développez hello **gestion de l’ordinateur** nœud et sélectionnez **gestion des disques**. 
     
     > [!NOTE]
     > Vous devez utiliser toorun de privilèges d’administrateur gestion des disques.
     > 
     > 
4. Prenez hello ou les volumes en ligne :
   
   1. Dans Gestion des disques, cliquez avec le bouton droit sur un volume marqué **Hors connexion**.
   2. Cliquez sur **Réactiver le disque**. Hello, il doit être marqué **Online** une fois le disque de hello est réactivé.
5. Initialiser l’ou les volumes hello :
   
   1. Cliquez sur les volumes hello découverts.
   2. Dans le menu de hello, sélectionnez **initialiser le disque**.
   3. Bonjour **initialiser le disque** boîte de dialogue, les disques de hello select que vous souhaitez tooinitialize, puis cliquez sur **OK**.
6. Formatez les volumes simples :
   
   1. Cliquez sur un volume que vous souhaitez tooformat.
   2. Dans le menu de hello, sélectionnez **nouveau Volume Simple**.
   3. Utilisez le volume hello tooformat hello nouveau Volume Simple Assistant :
      
      * Spécifiez la taille du volume hello.
      * Fournissez une lettre de lecteur.
      * Sélectionnez le système de fichiers NTFS hello.
      * Spécifiez une taille d’unité d’allocation 64 Ko.
      * Effectuez un formatage rapide.
7. Formatez des volumes à plusieurs partitions. Pour obtenir des instructions, consultez toohello section « Partitions et Volumes » [mise en œuvre la gestion de disque](https://msdn.microsoft.com/library/dd163556.aspx).

## <a name="view-information-about-your-volumes"></a>Afficher les informations sur les volumes
Utilisez hello suivant la procédure tooview informations local et les volumes Azure StorSimple.

#### <a name="tooview-volume-information"></a>informations sur le volume tooview
1. Cliquez sur icône du bureau de hello toostart Gestionnaire d’instantanés StorSimple. 
2. Bonjour **étendue** volet, cliquez sur hello **Volumes** nœud. Une liste des volumes locaux et montés, y compris tous les volumes Azure StorSimple, apparaît dans hello **résultats** volet. Hello colonnes Bonjour **résultats** volet sont configurables. (Clic droit hello **Volumes** nœud, sélectionnez **vue**, puis sélectionnez **Ajout/Suppression de colonnes**.)
   
    ![Configurer des colonnes de hello](./media/storsimple-snapshot-manager-manage-volumes/HCS_SSM_View_volumes.png)
   
   | Colonne de résultats | Description |
   |:--- |:--- |
   |  Nom |Hello **nom** colonne contient hello lecteur lettre attribuée tooeach découverts volume. |
   |  Appareil |Hello **périphérique** colonne contient l’adresse hello de l’ordinateur hôte hello appareil toohello connecté. |
   |  Nom de volume d’appareil |Hello **nom de Volume de périphérique** colonne contient le nom hello hello appareil volume toowhich Hello sélectionné volume appartient. Il s’agit de nom de volume hello défini dans hello portail Azure pour ce volume spécifique. |
   |  Chemins d’accès |Hello **des chemins d’accès** colonne affiche le volume de toohello hello accès chemin d’accès. Il s’agit de hello lecteur lettre ou point de montage à quels hello volume est accessible sur l’ordinateur hôte hello. |

## <a name="delete-a-volume"></a>Suppression d’un volume
Utilisez hello suivant procédure toodelete un volume à partir de gestionnaire d’instantanés StorSimple.

> [!NOTE]
> Vous ne pouvez pas supprimer un volume qui fait partie d’un groupe de volumes. (option de suppression hello n’est pas disponible pour les volumes qui sont membres d’un groupe de volumes). Vous devez supprimer le volume hello toodelete hello volume entier groupe.

#### <a name="toodelete-a-volume"></a>toodelete un volume
1. Cliquez sur icône du bureau de hello toostart Gestionnaire d’instantanés StorSimple.
2. Bonjour **étendue** volet, cliquez sur hello **Volumes** nœud. 
3. Bonjour **résultats** volet, le volume de hello avec le bouton que vous souhaitez toodelete.
4. Cliquez sur hello, **supprimer**. 
   
    ![Suppression d’un volume](./media/storsimple-snapshot-manager-manage-volumes/HCS_SSM_Delete_volume.png) 
5. Hello **supprimer le Volume** boîte de dialogue s’affiche. Type **confirmer** dans hello de zone de texte, puis cliquez sur **OK**.
6. Par défaut, le Gestionnaire d’instantanés StorSimple sauvegarde un volume avant de le supprimer. Cette précaution peut vous protéger contre la perte de données si hello suppression non intentionnelle. Gestionnaire d’instantanés StorSimple affiche un **instantané automatique** message de progression durant la sauvegarde de volume de hello. 
   
    ![Message automatique d’instantané](./media/storsimple-snapshot-manager-manage-volumes/HCS_SSM_Automatic_snap.png) 

## <a name="rescan-volumes"></a>Relancer l’analyse des volumes
Utilisez hello suivant la procédure toorescan hello volumes connectés tooStorSimple Gestionnaire d’instantanés.

#### <a name="toorescan-hello-volumes"></a>volumes de hello toorescan
1. Cliquez sur icône du bureau de hello toostart Gestionnaire d’instantanés StorSimple.
2. Bonjour **étendue** volet, avec le bouton droit **Volumes**, puis cliquez sur **rescanner les volumes**.
   
    ![Relancer l’analyse des volumes](./media/storsimple-snapshot-manager-manage-volumes/HCS_SSM_Rescan_volumes.png)
   
    Cette procédure synchronise liste des volumes hello avec Gestionnaire d’instantanés StorSimple. Toutes les modifications, telles que les nouveaux volumes ou de suppression de volumes, apparaîtront dans les résultats de hello.

## <a name="configure-and-back-up-a-basic-volume"></a>Configurer et sauvegarder un volume de base
Utilisez hello suivant la procédure tooconfigure une sauvegarde d’un volume de base, puis lancez immédiatement une sauvegarde ou créer une stratégie pour les sauvegardes planifiées.

### <a name="prerequisites"></a>Composants requis
Avant de commencer :

* Assurez-vous que l’appareil StorSimple hello et l’ordinateur hôte sont correctement configurés. Pour plus d’informations, consultez trop[déployer l’appareil StorSimple local](storsimple-deployment-walkthrough-u2.md).
* Installez et configurez le Gestionnaire d’instantanés StorSimple. Pour plus d’informations, consultez trop[déployer le Gestionnaire d’instantanés StorSimple](storsimple-snapshot-manager-deployment.md).

#### <a name="tooconfigure-backup-of-a-basic-volume"></a>sauvegarde tooconfigure d’un volume de base
1. Créer un volume de base sur l’appareil StorSimple hello.
2. Monter, initialiser et formater le volume de hello comme décrit dans [monter des volumes](#mount-volumes). 
3. Cliquez sur icône du Gestionnaire d’instantanés StorSimple hello sur votre bureau. fenêtre du Gestionnaire d’instantanés StorSimple Hello s’affiche. 
4. Bonjour **étendue** volet, avec le bouton hello **Volumes** nœud et sélectionnez **rescanner les volumes**. Lors de l’analyse de hello terminée, une liste des volumes doit apparaître dans hello **résultats** volet. 
5. Bonjour **résultats** volet, cliquez sur hello volume, puis sélectionnez **créer un groupe de volumes**. 
   
    ![Créer un groupe de volumes](./media/storsimple-snapshot-manager-manage-volumes/HCS_SSM_Create_volume_group.png) 
6. Bonjour **créer un groupe de volumes** boîte de dialogue, tapez un nom pour le groupe de volumes hello, affecter des volumes tooit, puis cliquez sur **OK**.
7. Bonjour **étendue** volet, développez hello **groupes de volumes** nœud. nouveau groupe de volumes Hello doit apparaître sous hello **groupes de volumes** nœud. 
8. Cliquez sur le nom de groupe de volumes hello.
   
   * toostart un travail de sauvegarde interactif (à la demande), cliquez sur **créer une sauvegarde**. 
   * tooschedule une sauvegarde automatique, cliquez sur **créer une stratégie de sauvegarde**. Sur hello **général** , sélectionnez un groupe de volumes à partir de la liste de hello. Sur hello **planification** , entrez les détails de la planification hello. Quand vous avez terminé, cliquez sur **OK**. 
9. tooconfirm qui hello du travail de sauvegarde a démarré, développez hello **travaux** nœud Bonjour **étendue** volet, puis cliquez sur hello **en cours d’exécution** nœud. liste de Hello de travaux en cours d’exécution s’affiche dans hello **résultats** volet. 

## <a name="configure-and-back-up-a-dynamic-mirrored-volume"></a>Configurer et sauvegarder un volume dynamique mis en miroir
Hello terminée après la sauvegarde de tooconfigure étapes d’un volume en miroir dynamique :

* Étape 1 : Toocreate utiliser la gestion des disques d’un volume en miroir dynamique. 
* Étape 2 : Sauvegarde de gestionnaire d’instantanés StorSimple utilisation tooconfigure.

### <a name="prerequisites"></a>Composants requis
Avant de commencer :

* Assurez-vous que l’appareil StorSimple hello et l’ordinateur hôte sont correctement configurés. Pour plus d’informations, consultez trop[déployer l’appareil StorSimple local](storsimple-8000-deployment-walkthrough-u2.md).
* Installez et configurez le Gestionnaire d’instantanés StorSimple. Pour plus d’informations, consultez trop[déployer le Gestionnaire d’instantanés StorSimple](storsimple-snapshot-manager-deployment.md).
* Configurez deux volumes sur l’appareil StorSimple hello. (Dans les exemples hello, sont les volumes disponibles hello **Disk 1** et **Disk 2**.) 

### <a name="step-1-use-disk-management-toocreate-a-dynamic-mirrored-volume"></a>Étape 1 : Utiliser la gestion des disques toocreate un volume en miroir dynamique
Gestion des disques est un utilitaire système de gestion des disques durs et les volumes hello ou partitions qu’ils contiennent. Pour plus d’informations sur la gestion des disques, consultez trop[gestion des disques](https://technet.microsoft.com/library/cc770943.aspx) sur le site Web de Microsoft TechNet hello.

#### <a name="toocreate-a-dynamic-mirrored-volume"></a>toocreate un volume en miroir dynamique
1. Utiliser les hello suivant options toostart gestion des disques : 
   
   * Ouvrez hello **exécuter** , tapez **Diskmgmt.msc**, puis appuyez sur ENTRÉE.
   * Démarrez le Gestionnaire de serveur, développez hello **stockage** nœud et sélectionnez **gestion des disques**. 
   * Démarrer **outils d’administration**, développez hello **gestion de l’ordinateur** nœud et sélectionnez **gestion des disques**. 
2. Assurez-vous que vous disposez de deux volumes disponibles sur l’appareil StorSimple hello. (Dans l’exemple de hello, sont les volumes disponibles hello **Disk 1** et **Disk 2**.) 
3. Dans la fenêtre de gestion des disques hello, dans la colonne de droite hello du volet inférieur de hello, cliquez sur **Disk 1** et sélectionnez **nouveau Volume en miroir**. 
   
    ![Nouveau volume en miroir](./media/storsimple-snapshot-manager-manage-volumes/HCS_SSM_New_mirrored_volume.png) 
4. Sur hello **nouveau Volume en miroir** page de l’Assistant, cliquez sur **suivant**.
5. Sur hello **sélectionner les disques** , sélectionnez **Disk 2** Bonjour **sélectionnés** volet, cliquez sur **ajouter**, puis cliquez sur **suivant**. 
6. Sur hello **attribuer une lettre de lecteur ou chemin d’accès** page, acceptez les valeurs par défaut hello et puis cliquez sur **suivant**. 
7. Sur hello **Format Volume** page hello **taille d’unité d’Allocation** boîte, sélectionnez **64K**. Sélectionnez hello **effectuer un formatage rapide** case à cocher, puis cliquez sur **suivant**. 
8. Sur hello **fin hello nouveau Volume en miroir** page, passez en revue vos paramètres, puis cliquez sur **Terminer**. 
9. Un message apparaît tooindicate qui hello disque de base sera converti tooa un disque dynamique. Cliquez sur **Oui**.
   
    ![Message de conversion de disque dynamique](./media/storsimple-snapshot-manager-manage-volumes/HCS_SSM_Disk_management_msg.png) 
10. Dans Gestion des disques, vérifiez que Disque 1 et Disque 2 sont affichés comme des volumes en miroir dynamiques. (**Dynamique** doit apparaître dans la colonne d’état hello, et couleur de barre de capacité hello doit modifier toored, ce qui indique un volume en miroir.) 
    
    ![Disques dynamiques mis en miroir du composant Gestion des disques](./media/storsimple-snapshot-manager-manage-volumes/HCS_SSM_Verify_dynamic_disks_2.png) 

### <a name="step-2-use-storsimple-snapshot-manager-tooconfigure-backup"></a>Étape 2 : Gestionnaire d’instantanés StorSimple utilisation tooconfigure sauvegarde
Utilisez hello suivant la procédure tooconfigure un volume en miroir dynamique, puis lancez immédiatement une sauvegarde ou créer une stratégie pour les sauvegardes planifiées.

#### <a name="tooconfigure-backup-of-a-dynamic-mirrored-volume"></a>sauvegarde tooconfigure d’un volume en miroir dynamique
1. Cliquez sur icône du Gestionnaire d’instantanés StorSimple hello sur votre bureau. fenêtre du Gestionnaire d’instantanés StorSimple Hello s’affiche. 
2. Bonjour **étendue** volet, avec le bouton hello **Volumes** nœud et sélectionnez **rescanner les volumes**. Lors de l’analyse de hello terminée, une liste des volumes doit apparaître dans hello **résultats** volet. volume de mise en miroir dynamique Hello est répertorié comme un volume unique. 
3. Bonjour **résultats** volet, cliquez sur le volume en miroir dynamique de hello, puis cliquez sur **créer un groupe de volumes**. 
4. Bonjour **créer un groupe de volumes** boîte de dialogue, tapez un nom pour le groupe de volumes hello, affectez hello volume en miroir dynamique toothis groupe, puis cliquez sur **OK**. 
5. Bonjour **étendue** volet, développez hello **groupes de volumes** nœud. nouveau groupe de volumes Hello doit apparaître sous hello **groupes de volumes** nœud. 
6. Cliquez sur le nom de groupe de volumes hello. 
   
   * toostart un travail de sauvegarde interactif (à la demande), cliquez sur **créer une sauvegarde**. 
   * tooschedule une sauvegarde automatique, cliquez sur **créer une stratégie de sauvegarde**. Sur hello **général** page, le groupe de volumes hello select à partir de la liste de hello. Sur hello **planification** , entrez les détails de la planification hello. Quand vous avez terminé, cliquez sur **OK**. 
7. Vous pouvez surveiller le travail de sauvegarde hello en cours d’exécution. Bonjour **étendue** volet, développez hello **travaux** nœud, puis cliquez sur **en cours d’exécution**, détails de la tâche hello apparaissent dans hello **résultats** volet. Lors de la tâche de sauvegarde hello est terminée, les détails de hello sont transférée toohello **dernières 24** heures de travail de liste. 

## <a name="next-steps"></a>Étapes suivantes
* Découvrez comment trop[utiliser le Gestionnaire d’instantanés StorSimple tooadminister votre solution StorSimple](storsimple-snapshot-manager-admin.md).
* Découvrez comment trop[utiliser le Gestionnaire d’instantanés StorSimple toocreate et gérer des groupes de volumes](storsimple-snapshot-manager-manage-volume-groups.md).

<!--Reference links-->
[1]: https://msdn.microsoft.com/library/ee338480(v=ws.10).aspx
