---
title: "aaaRun un test de basculement pour le site secondaire de la tooa de réplication d’ordinateur virtuel Hyper-V avec Azure Site Recovery | Documents Microsoft"
description: "Décrit comment toorun un test de basculement pour un ordinateur virtuel Hyper-V réplication tooa System Center VMM secondaire du site avec Azure Site Recovery."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: a3fd11ce-65a1-4308-8435-45cf954353ef
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/30/2017
ms.author: raynew
ms.openlocfilehash: a60411541c2db001c573735bcb0d651f6618f295
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="step-10-run-a-test-failover-for-hyper-v-replication-tooa-secondary-site"></a>Étape 10 : Exécuter un test de basculement pour le site secondaire de tooa de réplication Hyper-V


Après avoir activé la réplication pour Hyper-V virtual machines virtuelles avec [Azure Site Recovery](site-recovery-overview.md), utilisez cette toorun article un test de basculement. Un test de basculement vérifie que la réplication fonctionne, sans affecter votre environnement de production. 


Après avoir lu cet article, validez les commentaires au bas de hello, ou sur hello [Forum sur Azure Recovery Services](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="before-you-start"></a>Avant de commencer

- Lorsque vous êtes déclenchement d’un test de basculement, vous pouvez spécifier le réplica hello réseau toowhich hello test que machines virtuelles se connectera. [En savoir plus](site-recovery-test-failover-vmm-to-vmm.md#network-options-in-site-recovery) sur les options de réseau hello.
- Nous vous recommandons de ne pas choisir un réseau que vous avez sélectionné lors du mappage réseau.
- instructions Hello dans cet article décrivent comment toofail sur une seule machine virtuelle. En savoir plus sur [création de plans de récupération](site-recovery-create-recovery-plans.md) si vous souhaitez toofail sur plusieurs machines virtuelles ensemble.
- En savoir plus sur les[limitations des tests de basculement](site-recovery-test-failover-vmm-to-vmm.md#things-to-note).
- adresse IP donnée tooa machine virtuelle pendant le test de basculement Hello est hello recevrait la même adresse IP que hello de machine virtuelle pour un basculement planifié ou non planifié (en supposant qu’adresse hello est disponible dans le réseau de basculement de test hello). Si l’adresse IP de hello n’est pas disponible dans le réseau de basculement de test hello, hello machine virtuelle reçoit une autre adresse IP qui est disponible dans le réseau de basculement de test hello.
- Si vous voulez toodo un test de basculement dans votre réseau de production, pour une validation complète de l’ordinateur de connectivité réseau de bout en bout, sachez que :
    - Hello de qu'ordinateur virtuel principal doit être arrêté lorsque vous effectuez un test de basculement hello. Sinon, deux machines virtuelles avec hello même identité sera exécuté dans hello même réseau à hello même temps. 
    - Si vous apportez des modifications tootest VM, ces modifications sont perdues lors du nettoyage hello test de basculement. Ces modifications ne sont pas répliquée toohello arrière d’ordinateurs virtuels principal.
    - Tester un un réseau de production prospects toodowntime pour vos charges de travail de production. Demander aux utilisateurs pas toouse application hello lors de l’extraction de récupération d’urgence hello est en cours d’exécution.  


## <a name="run-a-test-failover-for-a-vm"></a>Exécuter un test de basculement pour une machine virtuelle

1. toofail sur une seule machine virtuelle, dans **répliquées des éléments**, cliquez sur la machine virtuelle de hello > **Test de basculement**.
2. Dans **le Test de basculement**, spécifiez comment machines virtuelles de test sera connecté toonetworks après le basculement de test hello. 
3. Cliquez sur **OK** toobegin hello basculement. Suivre la progression sur hello **travaux** onglet.
5. Une fois le basculement terminé, vérifiez que le test hello démarrage des machines virtuelles avec succès.
6. Lorsque vous avez terminé, cliquez sur **basculement de test de nettoyage** sur le plan de récupération hello.
7. Dans **Notes**, enregistrer et enregistrer toutes les observations associées au basculement de test hello. Cette étape supprime hello ordinateurs virtuels et des réseaux qui ont été créés pendant le test de basculement.


## <a name="next-steps"></a>Étapes suivantes

Une fois que vous avez testé le déploiement de hello, en savoir plus sur les autres types de [basculement](site-recovery-failover.md).
