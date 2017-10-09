---
title: "site secondaire tooa réplication aaaEnable Hyper-V avec Azure Site Recovery | Documents Microsoft"
description: "Décrit comment la réplication pour les ordinateurs virtuels Hyper-V en répliquant tooa tooenable System Center VMM secondaire du site avec Azure Site Recovery."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: d8782d14-9fef-4396-8912-ff945efc851b
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/30/2017
ms.author: raynew
ms.openlocfilehash: b4484e0118cb23f343187fe867d9795d30926baf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="step-9-enable-replication-tooa-secondary-site-for-hyper-v-vms"></a>Étape 9 : Activer le site secondaire tooa de réplication pour les ordinateurs virtuels Hyper-V


Après avoir configuré une stratégie de réplication, utiliser ce site secondaire System Center Virtual Machine Manager (VMM) article tooenable réplication tooa pour local Hyper-V virtuels (VM), à l’aide de [Azure Site Recovery](site-recovery-overview.md).

Après avoir lu cet article, validez les commentaires au bas de hello, ou sur hello [Forum sur Azure Recovery Services](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).



## <a name="select-vms-tooreplicate"></a>Sélectionnez tooreplicate de machines virtuelles

1. Cliquez sur **Étape 2 : Répliquer l’application** > **Source**. 

    ![Activer la réplication](./media/vmm-to-vmm-walkthrough-enable-replication/enable-replication1.png)

2. Dans **Source**, sélectionnez le serveur VMM de hello et hello cloud dans quel hello hôtes Hyper-V que vous souhaitez tooreplicate sont situés. Cliquez ensuite sur **OK**.

    ![Activer la réplication](./media/vmm-to-vmm-walkthrough-enable-replication/enable-replication2.png)
3. Dans **cible**, vérifiez que le serveur VMM secondaire de hello et cloud.
4. Dans **virtuels**, sélectionnez hello machines virtuelles tooprotect à partir de la liste de hello.

    ![Activer la protection pour les machines virtuelles](./media/vmm-to-vmm-walkthrough-enable-replication/enable-replication5.png)

Vous pouvez suivre la progression de hello **activer la Protection** action dans **travaux** > **les tâches de récupération de Site**. Après avoir hello **finaliser la Protection** tâche se termine, hello la réplication initiale est terminée et ordinateur virtuel de hello est prêt pour le basculement.

Notez les points suivants :

- Vous pouvez également activer la protection des machines virtuelles dans la console VMM hello. Cliquez sur **activer la Protection** de barre d’outils hello dans les propriétés d’une machine virtuelle hello > **Azure Site Recovery** onglet.
- Une fois que vous avez activé la réplication, vous pouvez afficher les propriétés d’hello VM dans **répliquées des éléments**. Sur hello **Essentials** tableau de bord, vous pouvez voir des informations sur la stratégie de réplication hello pour hello machine virtuelle et son état. Cliquez sur **Propriétés** pour obtenir plus de détails.

## <a name="onboard-existing-vms"></a>Intégrer des machines virtuelles existantes

Si vous avez des machines virtuelles existantes dans VMM qui sont répliquées à l’aide du réplica Hyper-V, vous pouvez les intégrer à la réplication Azure Site Recovery comme suit :

1. Assurez-vous que ce serveur hello Hyper-V héberge hello que machine virtuelle existante se trouve dans un cloud principal hello, et ce serveur d’Hyper-V hello hébergement hello ordinateur virtuel se trouve dans le cloud secondaire de hello.
2. Assurez-vous que la stratégie de réplication est configurée pour un cloud VMM principal hello.
3. Activer la réplication pour l’ordinateur virtuel principal hello. Azure Site Recovery et VMM s’assurer que hello même hôte de réplica et de la machine virtuelle est détectée et Azure Site Recovery réutilise et spécifié les paramètres de réplication de rétablir la connexion à l’aide de hello.


## <a name="next-steps"></a>Étapes suivantes

Accédez trop[étape 10 : exécuter un test de basculement](vmm-to-vmm-walkthrough-test-failover.md).
