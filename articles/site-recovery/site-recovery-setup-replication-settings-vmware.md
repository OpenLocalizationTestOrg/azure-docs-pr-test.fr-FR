---
title: "aaaSet des paramètres de réplication pour Azure Site Recovery | Documents Microsoft"
description: "Décrit comment la réplication tooorchestrate toodeploy Site Recovery, le basculement et récupération des ordinateurs virtuels Hyper-V dans VMM nuages tooAzure."
services: site-recovery
documentationcenter: 
author: sujayt
manager: rochakm
editor: rayne-wiselman
ms.assetid: 8e7d868e-00f3-4e8b-9a9e-f23365abf6ac
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 06/05/2017
ms.author: sutalasi
ms.openlocfilehash: 618e92e42411732a2a1bb75c5e5ea8a433cd7d58
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-replication-policy-for-vmware-tooazure"></a>Gérer la stratégie de réplication pour VMware tooAzure


## <a name="create-a-replication-policy"></a>Créer une stratégie de réplication

1. Sélectionnez **Gérer** > **Infrastructure Site Recovery**.
2. Sélectionnez **Stratégies de réplication** sous **Pour les machines VMware et physiques**.
3. Sélectionnez **+Stratégie de réplication**.

    ![Créer une stratégie de réplication](./media/site-recovery-setup-replication-settings-vmware/createpolicy.png)

4. Entrez le nom de la stratégie hello.

5. Dans **seuil RPO**, spécifiez la limite RPO hello. Des alertes sont générées lorsque la réplication continue dépasse cette limite.
6. Dans **rétention du point de récupération**, spécifier (en heures) hello de durée de conservation hello pour chaque point de récupération. Les ordinateurs protégés peuvent être récupérées point tooany dans une fenêtre de rétention.

    > [!NOTE]
    > Les heures too24 de rétention sont pris en charge pour les machines répliquées toopremium stockage. Les heures too72 de rétention sont pris en charge pour les machines répliquées toostandard stockage.

    > [!NOTE]
    > Une stratégie de réplication pour la restauration automatique est automatiquement créée.

7. Dans **Fréquence des captures instantanées cohérentes au niveau de l’application**, spécifiez la fréquence de création des points de récupération qui contiennent des captures instantanées cohérentes au niveau de l’application (en minutes).

8. Cliquez sur **OK**. stratégie de Hello doit être créée dans les 30 secondes too60.

![Génération d’une stratégie de réplication](./media/site-recovery-setup-replication-settings-vmware/Creating-Policy.png)

## <a name="associate-a-configuration-server-with-a-replication-policy"></a>Associer un serveur de configuration à une stratégie de réplication
1. Choisissez toowhich de stratégie de réplication hello tooassociate hello configuration serveur.
2. Cliquez sur **Associer**.
![Associer un serveur de configuration](./media/site-recovery-setup-replication-settings-vmware/Associate-CS-1.PNG)

3. Sélectionnez le serveur de configuration hello de liste hello des serveurs.
4. Cliquez sur **OK**. serveur de configuration Hello doit être associé dans un seul tootwo minutes.

![Association du serveur de configuration](./media/site-recovery-setup-replication-settings-vmware/Associate-CS-2.png)

## <a name="edit-a-replication-policy"></a>Modifier une stratégie de réplication
1. Choisissez la stratégie de réplication hello pour lequel vous souhaitez tooedit les paramètres de réplication.
![Modifier la stratégie de réplication](./media/site-recovery-setup-replication-settings-vmware/Select-Policy.png)

2. Cliquez sur **Edit Settings**.
![Modifier les paramètres de la stratégie de réplication](./media/site-recovery-setup-replication-settings-vmware/Edit-Policy.png)

3. Modifier les paramètres de hello selon vos besoins.
4. Cliquez sur **Enregistrer**. stratégie de Hello doit être enregistré dans les deux minutes toofive, selon le nombre de machines virtuelles sont à l’aide de la stratégie de réplication.

![Enregistrer la stratégie de réplication](./media/site-recovery-setup-replication-settings-vmware/Save-Policy.png)

## <a name="dissociate-a-configuration-server-from-a-replication-policy"></a>Dissocier un serveur de configuration d’une stratégie de réplication
1. Choisissez toowhich de stratégie de réplication hello tooassociate hello configuration serveur.
2. Cliquez sur **Dissocier**.
3. Sélectionnez le serveur de configuration hello de liste hello des serveurs.
4. Cliquez sur **OK**. serveur de configuration Hello doit être dissocié en un seul tootwo minutes.

    > [!NOTE]
    > Vous ne pouvez pas dissocier un serveur de configuration s’il existe au moins un élément répliqué à l’aide de la stratégie de hello. Assurez-vous qu’aucun élément répliquées à l’aide de la stratégie de hello avant de vous dissocier le serveur de configuration hello.

## <a name="delete-a-replication-policy"></a>Supprimer une stratégie de réplication

1. Choisissez la stratégie de réplication hello que vous souhaitez toodelete.
2. Cliquez sur **Supprimer**. stratégie de Hello doit être supprimée en 30 secondes too60.

    > [!NOTE]
    > Vous ne pouvez pas supprimer une stratégie de réplication s’il a tooit de serveur associé au moins une configuration. Assurez-vous qu’aucun élément répliquées à l’aide de la stratégie de hello et supprimez que tous les hello associées des serveurs de configuration avant de supprimer la stratégie de hello.
