---
title: "les stratégies de sauvegarde de gestionnaire d’instantanés aaaStorSimple | Documents Microsoft"
description: "Décrit comment toouse hello StorSimple Snapshot Manager MMC enfichable toocreate et gérer des stratégies de sauvegarde hello qui contrôlent les sauvegardes planifiées."
services: storsimple
documentationcenter: NA
author: SharS
manager: timlt
editor: 
ms.assetid: 04415d0b-42f0-4737-8afa-257fb2dbe5d0
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 06/05/2017
ms.author: v-sharos
ms.openlocfilehash: c2ae75a8d0568090add6018da18de73eb56e6590
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-storsimple-snapshot-manager-toocreate-and-manage-backup-policies"></a>Utilisez le Gestionnaire d’instantanés StorSimple toocreate et gérer des stratégies de sauvegarde
## <a name="overview"></a>Vue d'ensemble
Une stratégie de sauvegarde crée une planification de sauvegarde des données de volume local ou dans le cloud de hello. Lorsque vous créez une stratégie de sauvegarde, vous pouvez également spécifier une stratégie de rétention. (Vous pouvez conserver un maximum de 64 instantanés). Pour plus d'informations sur les stratégies de sauvegarde, consultez la page [Types de sauvegarde](storsimple-what-is-snapshot-manager.md#backup-types-and-backup-policies) dans [Gamme StorSimple 8000 : une solution de cloud hybride](storsimple-overview.md).

Ce didacticiel explique comment :

* Créer une stratégie de sauvegarde
* Modifier une stratégie de sauvegarde
* Supprimer une stratégie de sauvegarde

## <a name="create-a-backup-policy"></a>Créer une stratégie de sauvegarde
Utilisez hello suivant la procédure toocreate une stratégie de sauvegarde.

#### <a name="toocreate-a-backup-policy"></a>toocreate une stratégie de sauvegarde
1. Cliquez sur icône du bureau de hello toostart Gestionnaire d’instantanés StorSimple.
2. Bonjour **étendue** volet, avec le bouton droit **stratégies de sauvegarde**, puis cliquez sur **créer une stratégie de sauvegarde**.

    ![Créer une stratégie de sauvegarde](./media/storsimple-snapshot-manager-manage-backup-policies/HCS_SSM_Create_BU_policy.png)

    Hello **créer une stratégie** boîte de dialogue s’affiche.

    ![Créer une stratégie - onglet Général](./media/storsimple-snapshot-manager-manage-backup-policies/HCS_SSM_Create_policy_general.png)
3. Sur hello **général** onglet, hello complète informations suivantes :

   1. Bonjour **nom** zone de texte, tapez un nom pour la stratégie de hello.
   2. Bonjour **groupe de volumes** zone de texte, le nom de groupe de volumes hello associé hello stratégie hello de type.
   3. Sélectionnez **Instantané local** ou **Instantané cloud**.
   4. Sélectionnez nombre hello de captures instantanées tooretain. Si vous sélectionnez **tous les**, 64 instantanés à conserver (hello maximale).
4. Cliquez sur hello **planification** onglet.

    ![Créer une stratégie - onglet Planification](./media/storsimple-snapshot-manager-manage-backup-policies/HCS_SSM_Create_policy_schedule.png)
5. Sur hello **planification** onglet, hello complète informations suivantes :

   1. Cliquez sur hello **activer** sauvegarde suivante de case à cocher tooschedule hello.
   2. Sous **Paramètres**, sélectionnez **Une fois**, **Quotidienne**, **Hebdomadaire** ou **Mensuelle**.
   3. Bonjour **Démarrer** zone de texte, cliquez sur icône du calendrier hello et sélectionnez une date de début.
   4. Sous **Paramètres avancés**, vous pouvez définir des planifications répétées facultatives et une date de fin.
   5. Cliquez sur **OK**.

Après avoir créé une stratégie de sauvegarde, hello informations suivantes s’affiche dans hello **résultats** volet :

* **Nom** hello – nom de la stratégie de sauvegarde.
* **Type** : instantané local ou instantané cloud.
* **Groupe de volumes** : hello associé hello stratégie de groupe de volumes.
* **Rétention** hello – nombre d’instantanés conservés ; hello maximale est 64.
* **Créé** – date hello que cette stratégie a été créée.
* **Activé** : indique si la stratégie de hello est actuellement en vigueur : **True** indique qu’il est appliqué. **False** indique qu’il n’est pas en vigueur.

## <a name="edit-a-backup-policy"></a>Modifier une stratégie de sauvegarde
Utilisez hello suivant la procédure tooedit une stratégie de sauvegarde existante.

#### <a name="tooedit-a-backup-policy"></a>tooedit une stratégie de sauvegarde
1. Cliquez sur icône du bureau de hello toostart Gestionnaire d’instantanés StorSimple.
2. Bonjour **étendue** volet, cliquez sur hello **stratégies de sauvegarde** nœud. Toutes les stratégies de sauvegarde hello apparaissent dans hello **résultats** volet.
3. Cliquez sur stratégie hello que vous souhaitez tooedit, puis cliquez sur **modifier**.

    ![Modifier une stratégie de sauvegarde](./media/storsimple-snapshot-manager-manage-backup-policies/HCS_SSM_Edit_BU_policy.png)
4. Hello lorsque **créer une stratégie de** fenêtre s’affiche, entrez vos modifications, puis cliquez sur **OK**.

## <a name="delete-a-backup-policy"></a>Supprimer une stratégie de sauvegarde
Utilisez hello suivant la procédure toodelete une stratégie de sauvegarde.

#### <a name="toodelete-a-backup-policy"></a>toodelete une stratégie de sauvegarde
1. Cliquez sur icône du bureau de hello toostart Gestionnaire d’instantanés StorSimple.
2. Bonjour **étendue** volet, cliquez sur hello **stratégies de sauvegarde** nœud. Toutes les stratégies de sauvegarde hello apparaissent dans hello **résultats** volet.
3. Cliquez sur la stratégie de sauvegarde hello que vous souhaitez toodelete, puis cliquez sur **supprimer**.
4. Lorsque le message de confirmation hello s’affiche, cliquez sur **Oui**.

    ![Confirmation de la suppression de la stratégie de sauvegarde](./media/storsimple-snapshot-manager-manage-backup-policies/HCS_SSM_Delete_BU_policy.png)

## <a name="next-steps"></a>Étapes suivantes
* Découvrez comment trop[utiliser le Gestionnaire d’instantanés StorSimple tooadminister votre solution StorSimple](storsimple-snapshot-manager-admin.md).
* Découvrez comment trop[utiliser le Gestionnaire d’instantanés StorSimple tooview et gérer des travaux de sauvegarde](storsimple-snapshot-manager-manage-backup-jobs.md).
