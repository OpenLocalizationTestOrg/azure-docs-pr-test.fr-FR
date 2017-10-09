---
title: "tooAzure de réplication aaaEnable pour les ordinateurs virtuels Hyper-V dans VMM clouds avec Azure Site Recovery | Documents Microsoft"
description: "Décrit comment des clouds tooAzure de réplication tooenable pour les ordinateurs virtuels Hyper-V dans VMM, par hello service Azure Site Recovery"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 89a2c4fc-7e03-4a86-a2c0-52831ccebc1a
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/23/2017
ms.author: raynew
ms.openlocfilehash: 1a39bf65490c59a89a5e891184cadfacc2adee6d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="step-11-enable-replication-tooazure-for-hyper-v-vms-in-vmm-clouds"></a>Étape 11 : Activer la réplication tooAzure pour des ordinateurs virtuels Hyper-V dans les clouds VMM

Une fois que vous avez configuré une stratégie de réplication, utilisez cet article tooenable la réplication pour local Hyper-V virtual machines virtuelles gérée dans des clouds de System Center Virtual Machine Manager (VMM)), tooAzure, à l’aide de hello [Azure Site Recovery](site-recovery-overview.md)service Bonjour portail Azure.

Ajouter des commentaires et questions bas hello de cet article, ou sur hello [Forum sur Azure Recovery Services](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="before-you-start"></a>Avant de commencer

Assurez-vous que votre compte Azure a hello correct [autorisations](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines)toocreate machines virtuelles Azure. [En savoir plus](../active-directory/role-based-access-built-in-roles.md) sur le contrôle d’accès en fonction du rôle dans Azure.

## <a name="exclude-disks-from-replication"></a>Exclure les disques de la réplication

Par défaut, tous les disques d’une machine sont répliqués. Vous pouvez exclure des disques de la réplication. Par exemple, vous pouvez tooreplicate les disques avec les données temporaires ou des données a actualisé chaque fois qu’un ordinateur ou redémarrage de l’application (par exemple pagefile.sys ou tempdb de SQL Server). [En savoir plus](site-recovery-exclude-disk.md)

## <a name="replicate-vms"></a>Répliquer des machines virtuelles

Activez la réplication des machines virtuelles comme suit :  

1. Cliquez sur **Étape 2 : Répliquer l’application** > **Source**. Une fois que vous avez activé la réplication pour hello première fois, cliquez sur **+ répliquer** dans la réplication de tooenable hello coffre pour des ordinateurs supplémentaires.

    ![Activer la réplication](./media/vmm-to-azure-walkthrough-enable-replication/enable-replication1.png)
2. Bonjour **Source** panneau serveur VMM de select hello et nuage de hello dans quel hello Hyper-V se trouvent les hôtes. Cliquez ensuite sur **OK**.

    ![Activer la réplication](./media/vmm-to-azure-walkthrough-enable-replication/enable-replication-source.png)
3. Dans **cible**hello compte de stockage que vous utilisez pour les données répliquées et sélectionnez l’abonnement hello, modèle de déploiement après le basculement.

    ![Activer la réplication](./media/vmm-to-azure-walkthrough-enable-replication/enable-replication-target.png)
4. Sélectionnez le compte de stockage hello souhaité toouse. Si vous souhaitez toouse un compte de stockage différentes que celles que vous avez, vous pouvez [créer un](#set-up-an-azure-storage-account). Si vous utilisez un compte de stockage premium pour les données répliquées, vous devez tooselect une journaux de réplication de stockage standard supplémentaire compte toostore qui capturent les changements en cours tooon local data.toocreate un compte de stockage à l’aide du modèle de gestionnaire de ressources hello Cliquez sur **nouvel**. Si vous voulez toocreate un compte de stockage à l’aide du modèle classique de hello, cela [Bonjour Azure portal](../storage/common/storage-create-storage-account.md). Cliquez ensuite sur **OK**.
5. Sélectionnez hello toowhich réseau et le sous-réseau Azure machines virtuelles Azure se connecte lorsqu’elles sont créées après le basculement. Sélectionnez **configurer maintenant pour les machines sélectionnées**, tooapply hello réseau paramètre tooall machines que vous sélectionnez pour la protection. Sélectionnez **configurer ultérieurement**, tooselect hello réseau Azure par ordinateur. Si vous souhaitez toouse un réseau différents de ceux, vous pouvez [créer un](#set-up-an-azure-network). un réseau à l’aide de toocreate hello modèle, cliquez sur le Gestionnaire de ressources **nouvel**. Si vous voulez toocreate un réseau en utilisant le modèle classique de hello, cela [Bonjour Azure portal](../virtual-network/virtual-networks-create-vnet-classic-pportal.md). Sélectionnez un sous-réseau, le cas échéant. Cliquez ensuite sur **OK**.
6. Dans **virtuels** > **sélectionner des machines virtuelles**, cliquez sur et sélectionnez chaque ordinateur que vous souhaitez tooreplicate. Vous pouvez uniquement sélectionner les machines pour lesquelles la réplication peut être activée. Cliquez ensuite sur **OK**.

    ![Activer la réplication](./media/vmm-to-azure-walkthrough-enable-replication/enable-replication5.png)

7. Dans **propriétés** > **configurer les propriétés**, sélectionnez le système d’exploitation de hello pour les machines virtuelles hello sélectionné et hello disque de système d’exploitation.

    - Vérifiez que ce nom de machine virtuelle Azure hello (nom de la cible) est conforme à [spécifications de la machine virtuelle Azure](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).   
    - Par défaut, tous les disques hello Hello machine virtuelle sont sélectionnés pour la réplication, mais vous pouvez désactiver les disques tooexclude les.

        - Vous souhaiterez peut-être la bande passante de tooexclude disques tooreduce la réplication. Par exemple, vous pouvez tooreplicate les disques avec les données temporaires, ou les données qui a actualisé chaque fois qu’un ordinateur ou applications redémarre (comme pagefile.sys ou Microsoft SQL Server tempdb). Vous pouvez exclure les disque hello de la réplication en désélectionnant disque de hello.
        - Vous ne pouvez exclure que des disques de base. Vous ne pouvez pas exclure de disques de système d’exploitation.
        - Nous vous recommandons de ne pas exclure de disques dynamiques. Site Recovery ne peut pas déterminer si un disque dur virtuel à l’intérieur d’une machine virtuelle invitée est un disque de base ou dynamique. Si tous les disques de volume dynamique dépendants ne sont pas exclus, disque protégé hello apparaît comme un disque en panne lorsque hello machine virtuelle bascule et données hello sur ce disque ne seront pas accessibles.
        - Une fois la réplication activée, vous ne pouvez pas ajouter ni supprimer de disques pour la réplication. Si vous souhaitez tooadd ou excluez un disque, votre besoin d’une protection de toodisable pour hello machine virtuelle, puis réactivez-la.
        - Les disques que vous créez manuellement dans Azure ne sont pas restaurés automatiquement. Par exemple, si vous échouer trois disques et créez deux directement dans la machine virtuelle Azure, uniquement hello trois disques qui ont été basculés va échouer à partir tooHyper-V Azure. Vous ne pouvez inclure les disques créés manuellement dans la restauration automatique, ou dans la réplication inverse depuis tooAzure d’Hyper-V.
        - Si vous excluez un disque que nécessaire pour un toooperate de l’application, vous devez après basculement tooAzure toocreate manuellement dans Azure, ainsi que hello répliquées application peut s’exécuter. Vous pouvez également intégrer Azure automation dans un plan de récupération, disque de hello toocreate pendant le basculement de l’ordinateur de hello.

    Cliquez sur **OK** toosave modifications. Vous pouvez opter pour une définition ultérieure des propriétés.

    ![Activer la réplication](./media/vmm-to-azure-walkthrough-enable-replication/enable-replication6-with-exclude-disk.png)

8. Dans **les paramètres de réplication** > **configurer les paramètres de réplication**, sélectionnez hello réplication stratégie tooapply pour hello protégé des machines virtuelles. Cliquez ensuite sur **OK**. Vous pouvez modifier la stratégie de réplication hello dans **stratégies de réplication** > nom de la stratégie > **modifier les paramètres**. Les modifications appliquées sont utilisées pour les nouvelles machines et celles dont la réplication est en cours.

   ![Activer la réplication](./media/vmm-to-azure-walkthrough-enable-replication/enable-replication7.png)

Vous pouvez suivre la progression de hello **activer la Protection** de la tâche dans **travaux** > **les tâches de récupération de Site**. Après avoir hello **finaliser la Protection** travail s’exécute, l’ordinateur de hello est prêt pour le basculement.



## <a name="next-steps"></a>Étapes suivantes

Accédez trop[étape 12 : exécuter un test de basculement](vmm-to-azure-walkthrough-test-failover.md)
