---
title: "la réplication pour les ordinateurs virtuels Hyper-V en répliquant tooAzure (sans System Center VMM) avec Azure Site Recovery aaaEnable | Documents Microsoft"
description: "Résume les étapes hello vous devez tooenable réplication tooAzure pour des ordinateurs virtuels Hyper-V à l’aide du service d’Azure Site Recovery hello"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: bd31ef01-69f1-4591-a519-e42510a6e2f4
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/21/2017
ms.author: raynew
ms.openlocfilehash: 1589cb7aa1fe954e075cb7bf1f4a4ec199ed3ec7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="step-10-enable-replication-for-hyper-v-vms-replicating-tooazure"></a>Étape 10 : Activer la réplication pour les ordinateurs virtuels Hyper-V en réplication tooAzure


Cet article décrit comment la réplication pour tooenable locaux virtuels Hyper-V (ne pas gérés par System Center VMM) tooAzure, à l’aide de hello [Azure Site Recovery](site-recovery-overview.md) service Bonjour portail Azure.

Ajouter des commentaires et questions bas hello de cet article, ou sur hello [Forum sur Azure Recovery Services](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).




## <a name="before-you-start"></a>Avant de commencer

Avant de commencer, assurez-vous que votre compte d’utilisateur Azure a hello requis [autorisations](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines) tooenable la réplication d’un nouveau tooAzure d’ordinateur virtuel.

## <a name="exclude-disks-from-replication"></a>Exclure les disques de la réplication

Par défaut, tous les disques d’une machine sont répliqués. Vous pouvez exclure des disques de la réplication. Par exemple, vous pouvez tooreplicate les disques avec les données temporaires ou des données a actualisé chaque fois qu’un ordinateur ou redémarrage de l’application (par exemple pagefile.sys ou tempdb de SQL Server). [En savoir plus](site-recovery-exclude-disk.md)


## <a name="replicate-vms"></a>Répliquer des machines virtuelles

Activez la réplication des machines virtuelles comme suit :          

1. Cliquez sur **Répliquer l’application** > **Source**. Après avoir configuré la réplication pour hello la première fois, vous pouvez cliquer sur **+ répliquer** tooenable la réplication pour des ordinateurs supplémentaires.

    ![Activer la réplication](./media/hyper-v-site-walkthrough-enable-replication/enable-replication.png)
2. Dans **Source**, sélectionnez les sites hello Hyper-V. Cliquez ensuite sur **OK**.
3. Dans **cible**, sélectionnez l’abonnement de coffre hello et hello basculement modèle toouse dans Azure (classique ou ressource management) après le basculement.
4. Sélectionnez le compte de stockage hello souhaité toouse. Si vous n’avez pas un compte que vous souhaitez toouse, vous pouvez [créer un](#set-up-an-azure-storage-account). Cliquez ensuite sur **OK**.
5. Sélectionnez hello toowhich réseau et le sous-réseau Azure machines virtuelles Azure se connecte lorsqu’elles sont créées avec basculement.

    - tooapply hello paramètres tooall ordinateurs du réseau vous activez pour la réplication, sélectionnez **configurer maintenant pour les ordinateurs sélectionnés**.
    - Sélectionnez **configurer ultérieurement** tooselect hello réseau Azure par ordinateur.
    - Si vous n’avez pas un réseau de toouse, vous pouvez [créer un](#set-up-an-azure-network). Sélectionnez un sous-réseau, le cas échéant. Cliquez ensuite sur **OK**.

   ![Activer la réplication](./media/hyper-v-site-walkthrough-enable-replication/enable-replication11.png)

6. Dans **virtuels** > **sélectionner des machines virtuelles**, cliquez sur et sélectionnez chaque ordinateur que vous souhaitez tooreplicate. Vous pouvez uniquement sélectionner les machines pour lesquelles la réplication peut être activée. Cliquez ensuite sur **OK**.

    ![Activer la réplication](./media/hyper-v-site-walkthrough-enable-replication/enable-replication5-for-exclude-disk.png)

7. Dans **propriétés** > **configurer les propriétés**, sélectionnez le système d’exploitation de hello pour les machines virtuelles hello sélectionné et hello disque de système d’exploitation.
8. Vérifiez que ce nom de machine virtuelle Azure hello (nom de la cible) est conforme à [spécifications de la machine virtuelle Azure](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).
9. Par défaut, tous les disques hello Hello machine virtuelle sont sélectionnés pour la réplication. Disques effacer tooexclude les.
10. Cliquez sur **OK** toosave modifications. Vous pouvez opter pour une définition ultérieure des propriétés.

    ![Activer la réplication](./media/hyper-v-site-walkthrough-enable-replication/enable-replication6-with-exclude-disk.png)

11. Dans **les paramètres de réplication** > **configurer les paramètres de réplication**, sélectionnez hello réplication stratégie tooapply pour hello protégé des machines virtuelles. Cliquez ensuite sur **OK**. Vous pouvez modifier la stratégie de réplication hello dans **stratégies de réplication** > nom de la stratégie > **modifier les paramètres**. Les modifications que vous appliquez seront utilisées pour les nouvelles machines et les machines dont la réplication est déjà en cours.


   ![Activer la réplication](./media/hyper-v-site-walkthrough-enable-replication/enable-replication7.png)

Vous pouvez suivre la progression de hello **activer la Protection** de la tâche dans **travaux** > **les tâches de récupération de Site**. Après avoir hello **finaliser la Protection** s’exécute la tâche machine de hello est prête pour le basculement.


## <a name="next-steps"></a>Étapes suivantes


Accédez trop[étape 11 : exécuter un test de basculement](hyper-v-site-walkthrough-test-failover.md)
