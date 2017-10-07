---
title: "réseaux aaaMap pour le site secondaire de la tooa de réplication d’ordinateur virtuel Hyper-V avec Azure Site Recovery | Documents Microsoft"
description: "Décrit comment les réseaux toomap lors de la réplication des ordinateurs virtuels Hyper-V tooa site VMM secondaire avec Azure Site Recovery."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 461b7c1c-ef61-4005-aeec-2324e727a3d0
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/30/2017
ms.author: raynew
ms.openlocfilehash: d4f621df4ce08ae055bc6809daea0b71b76754ad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="step-7-map-networks-for-hyper-v-vm-replication-tooa-secondary-site"></a>Étape 7 : Mapper les réseaux pour le site secondaire de machine virtuelle Hyper-V réplication tooa


Après avoir configuré [paramètres source et cible](vmm-to-vmm-walkthrough-source-target.md) pour répliquer le site de System Center Virtual Machine Manager (VMM) secondaire Hyper-V machines virtuelles (VM) tooa, utiliser ce mappage article tooconfigure réseau virtuel Hyper-V tooa de réplication de machine (VM) secondaire du site, à l’aide de [Azure Site Recovery](site-recovery-overview.md).

Après avoir lu cet article, validez les commentaires au bas de hello, ou sur hello [Forum sur Azure Recovery Services](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="before-you-start"></a>Avant de commencer

- En savoir plus sur le [mappage réseau](vmm-to-vmm-walkthrough-network.md#network-mapping-overview) avant de démarrer.
- Vérifiez que les ordinateurs virtuels sur les serveurs VMM sont connectés tooa réseau d’ordinateurs virtuels.

## <a name="configure-network-mapping"></a>Configurer le mappage réseau

1. Dans **Mappage réseau** > **Mappages réseau**, cliquez sur **+Mappage réseau**.
2. Dans **ajouter le mappage réseau** , sélectionnez la source de hello et serveurs VMM cible. réseaux d’ordinateurs virtuels Hello associés aux serveurs VMM de hello sont récupérés.
3. Dans **réseau Source**, sélectionnez réseau hello toouse à partir de la liste de hello des réseaux d’ordinateurs virtuels associé avec le serveur VMM principal de hello.
4. Dans **réseau cible**, sélectionnez réseau hello toouse sur le serveur VMM secondaire de hello. Cliquez ensuite sur **OK**.

    ![Mappage réseau](./media/vmm-to-vmm-walkthrough-network-mapping/network-mapping2.png)

Voici le processus exécuté lorsque le mappage réseau démarre :

* Les ordinateurs virtuels réplica existants qui correspondent le réseau d’ordinateurs virtuels toohello source sera réseau d’ordinateurs virtuels connectés toohello cible.
* Nouveaux ordinateurs virtuels qui sont le réseau d’ordinateurs virtuels connectés toohello source sera connecté toohello réseau cible après la réplication.
* Si vous modifiez un mappage existant avec un nouveau réseau, les machines virtuelles de réplication sera connectées à l’aide de nouveaux paramètres de hello.
* Si le réseau cible de hello possède plusieurs sous-réseaux et d’un de ces sous-réseaux a hello trouve du même nom que le sous-réseau sur lequel hello source virtual machine, puis hello ordinateur virtuel sera connecté toothat cible sous-réseau après le basculement. S’il n’existe aucun sous-réseau cible avec un nom correspondant, ordinateur virtuel de hello sera connecté toohello premier sous-réseau de réseau de hello.



## <a name="next-steps"></a>Étapes suivantes

Accédez trop[étape 8 : configurer une stratégie de réplication](vmm-to-vmm-walkthrough-replication.md).
