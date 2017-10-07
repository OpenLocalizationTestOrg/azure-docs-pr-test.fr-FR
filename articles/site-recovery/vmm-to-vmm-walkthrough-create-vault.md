---
title: "aaaCreate un coffre pour le site secondaire tooa réplication Hyper-V avec Azure Site Recovery | Documents Microsoft"
description: "Décrit comment toocreate un coffre lors de la réplication des ordinateurs virtuels Hyper-V tooa System Center VMM secondaire du site avec Azure Site Recovery."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: ff65dbfb-cb26-410e-ab48-76971625db08
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/30/2017
ms.author: raynew
ms.openlocfilehash: 96ee09cbf2376a5089b9efa09dc7ab3fb7d472cb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="step-5-create-a-vault-for-hyper-v-replication-tooa-secondary-site"></a>Étape 5 : Créer un coffre pour le site secondaire de tooa de réplication Hyper-V

Après avoir préparé local [les serveurs System Center Virtual Machine Manager (VMM) et les hôtes/clusters Hyper-V](vmm-to-vmm-walkthrough-vmm-hyper-v.md) pour Hyper-V réplication tooa site secondaire à l’aide [Azure Site Recovery](site-recovery-overview.md), vous pouvez créer un Scénario de réplication Sélectionnez hello et coffre Recovery Services.

Après avoir lu cet article, validez les commentaires au bas de hello, ou sur hello [Forum sur Azure Recovery Services](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="create-a-recovery-services-vault"></a>Créer un coffre Recovery Services

[!INCLUDE [site-recovery-create-vault](../../includes/site-recovery-create-vault.md)]


## <a name="choose-a-protection-goal"></a>Choisir un objectif en matière de protection

Sélectionnez ce que vous souhaitez tooreplicate, et où tooreplicate à.

1. Cliquez sur **Site Recovery** > **Étape 1 : Préparez l’infrastructure** > **Objectif de protection**.
2. Sélectionnez **toorecovery site**, puis sélectionnez **Oui, avec Hyper-V**.
3. Sélectionnez **Oui** tooindicate que vous utilisez des hôtes VMM toomanage hello Hyper-V.
4. Sélectionnez **Oui** si vous avez un serveur VMM secondaire. Si vous déployez la réplication entre des clouds sur un seul serveur VMM, cliquez sur **Non**. Cliquez ensuite sur **OK**.

    ![Sélectionner des objectifs](./media/vmm-to-vmm-walkthrough-create-vault/choose-goals.png)



## <a name="next-steps"></a>Étapes suivantes

Accédez trop[étape 6 : configurer la source de réplication hello et cible](vmm-to-vmm-walkthrough-source-target.md).
