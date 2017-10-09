---
title: "la réplication pour les machines virtuelles VMware en répliquant tooAzure avec Azure Site Recovery aaaEnable | Documents Microsoft"
description: "Résume les étapes hello vous devez tooenable réplication tooAzure pour les ordinateurs virtuels VMware à l’aide du service d’Azure Site Recovery hello"
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 519c5559-7032-4954-b8b5-f24f5242a954
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: 490782bbbfa3dd92c626d3985c75d771df53d566
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="step-11-enable-replication-for-vmware-virtual-machines-tooazure"></a>Étape 11 : Activer la réplication pour tooAzure des machines virtuelles VMware


Cet article décrit comment réplication tooenable pour VMware local virtual machines tooAzure, à l’aide de hello [Azure Site Recovery](site-recovery-overview.md) service Bonjour portail Azure.

Ajouter des commentaires et questions bas hello de cet article, ou sur hello [Forum sur Azure Recovery Services](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="before-you-start"></a>Avant de commencer

- Les ordinateurs virtuels VMware doit avoir hello [composant du service mobilité installé](vmware-walkthrough-install-mobility.md). -Si une machine virtuelle est préparée à l’installation push, serveur de processus hello installe automatiquement le service de mobilité hello lorsque vous activez la réplication.
- Votre compte d’utilisateur Azure a besoin spécifique [autorisations](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines) tooenable la réplication d’un tooAzure de machine virtuelle
- Lorsque vous ajoutez ou modifiez des machines virtuelles, il peut prendre too15 minutes ou plus pour effet de tootake de modifications et les tooappear dans le portail de hello.
- Vous pouvez vérifier l’heure de dernier découvert de hello pour les machines virtuelles dans **serveurs de Configuration** > **dernier Contact à**.
- tooadd machines virtuelles sans attendre la détection planifiée hello, serveur de configuration de mise en surbrillance hello (ne cliquez pas dessus), puis cliquez sur **Actualiser**.



## <a name="exclude-disks-from-replication"></a>Exclure les disques de la réplication

Par défaut, tous les disques d’une machine sont répliqués. Vous pouvez exclure des disques de la réplication. Par exemple, vous pouvez tooreplicate les disques avec les données temporaires ou des données a actualisé chaque fois qu’un ordinateur ou redémarrage de l’application (par exemple pagefile.sys ou tempdb de SQL Server). [En savoir plus](site-recovery-exclude-disk.md)

## <a name="replicate-vms"></a>Répliquer des machines virtuelles

Avant de commencer, visionnez une courte vidéo de présentation :

>[!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/VMware-to-Azure-with-ASR-Video3-Protect-VMware-Virtual-Machines/player]

1. Cliquez sur **Étape 2 : Répliquer l’application** > **Source**.
2. Dans **Source**, sélectionnez le serveur de configuration hello.
3. Dans **Type de machine**, sélectionnez **Machines virtuelles**.
4. Dans **vCenter/vSphere hyperviseur**, sélectionnez le serveur vCenter hello qui gère l’ordinateur hôte de vSphere hello ou sélectionner l’ordinateur hôte hello.
5. Sélectionnez le serveur de processus hello. Si vous n’avez pas créé de tous les serveurs de processus supplémentaire ce sera le serveur de configuration hello. Cliquez ensuite sur **OK**.

    ![Activer la réplication](./media/vmware-walkthrough-enable-replication/enable-replication2.png)

6. Dans **cible**hello du groupe de ressources dans lequel vous souhaitez hello toocreate a échoué sur des machines virtuelles et sélectionnez l’abonnement de hello. Choisir le modèle de déploiement hello que toouse dans Azure (classique ou ressource de gestion), hello basculé de machines virtuelles.


7. Sélectionnez le compte de stockage Azure hello que toouse souhaité pour répliquer les données. Si vous ne souhaitez pas toouse un compte que vous avez déjà configuré, vous pouvez créer un nouveau.

8. Sélectionnez hello toowhich réseau et le sous-réseau Azure machines virtuelles Azure se connecte lorsqu’elles sont créées après le basculement. Sélectionnez **configurer maintenant pour les machines sélectionnées**, tooapply hello réseau paramètre tooall machines que vous sélectionnez pour la protection. Sélectionnez **configurer ultérieurement** tooselect hello réseau Azure par ordinateur. Si vous ne souhaitez pas toouse un réseau existant, vous pouvez créer un.

    ![Activer la réplication](./media/vmware-walkthrough-enable-replication/enable-rep3.png)
9. Dans **virtuels** > **sélectionner des machines virtuelles**, cliquez sur et sélectionnez chaque ordinateur que vous souhaitez tooreplicate. Vous pouvez uniquement sélectionner les machines pour lesquelles la réplication peut être activée. Cliquez ensuite sur **OK**.

    ![Activer la réplication](./media/vmware-walkthrough-enable-replication/enable-replication5.png)
10. Dans **propriétés** > **configurer les propriétés**, sélectionnez compte hello qui sera utilisé par hello processus serveur tooautomatically installer le service de mobilité hello sur l’ordinateur de hello.
11. Par défaut, tous les disques sont répliqués. Cliquez sur **tous les disques** et effacer tous les disques que vous ne souhaitez pas tooreplicate. Cliquez ensuite sur **OK**. Vous pouvez configurer des propriétés de machine virtuelle supplémentaires ultérieurement.

    ![Activer la réplication](./media/vmware-walkthrough-enable-replication/enable-replication6.png)
11. Dans **les paramètres de réplication** > **configurer les paramètres de réplication**, vérifiez que hello correct de la stratégie de réplication est activée. Si vous modifiez une stratégie, les modifications seront appliquées tooreplicating machine et toonew machines.
12. Activer **la cohérence Multimachine virtuelle** si vous souhaitez toogather ordinateurs dans un groupe de réplication, spécifiez un nom pour le groupe de hello. Cliquez ensuite sur **OK**. Notez les points suivants :

    * Les machines des groupes de réplication sont répliquées ensemble et ont des points de récupération cohérents après incident et avec les applications lorsqu’elles basculent.
    * Nous vous recommandons de rassembler les machines virtuelles et les serveurs physiques afin qu’ils reflètent vos charges de travail. L’activation de la cohérence multimachine virtuelle peuvent affecter les performances de la charge de travail et doit être utilisé uniquement si les ordinateurs hello même charge de travail et que vous avez besoin de cohérence.

    ![Activer la réplication](./media/vmware-walkthrough-enable-replication/enable-replication7.png)
13. Cliquez sur **Activer la réplication**. Vous pouvez suivre la progression de hello **activer la Protection** de la tâche dans **paramètres** > **travaux** > **tâches de récupération de Site**. Après avoir hello **finaliser la Protection** s’exécute la tâche machine de hello est prête pour le basculement.

## <a name="next-steps"></a>Étapes suivantes

Accédez trop[étape 12 : exécuter un test de basculement](vmware-walkthrough-test-failover.md)
