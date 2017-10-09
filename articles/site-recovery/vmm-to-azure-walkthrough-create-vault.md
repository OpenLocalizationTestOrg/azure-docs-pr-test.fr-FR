---
title: "aaaSet d’un coffre pour tooAzure de réplication (avec System Center VMM) d’Hyper-V à l’aide d’Azure Site Recovery | Documents Microsoft"
description: "Résume les étapes hello vous devez tooset d’un coffre pour tooAzure de réplication (avec VMM) d’Hyper-V à l’aide d’Azure Site Recovery"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: b3cd6f03-c33c-406d-91d4-5cba69f79abd
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 07/23/2017
ms.author: raynew
ms.openlocfilehash: f2c90f3c8b0a48db1e57fefd9829d29cffff8d43
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="step-7-set-up-a-vault-for-hyper-v-replication"></a>Étape 7 : configurer un coffre pour la réplication Hyper-V

Cet article décrit comment configurer un coffre tooset et spécifier ce que vous souhaitez tooreplicate à partir de votre emplacement local, tooAzure à l’aide de hello [Azure Site Recovery](site-recovery-overview.md) service Bonjour portail Azure.


Ajouter des commentaires et questions bas hello de cet article, ou sur hello [Forum sur Azure Recovery Services](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

## <a name="create-a-recovery-services-vault"></a>Créer un coffre Recovery Services

[!INCLUDE [site-recovery-create-vault](../../includes/site-recovery-create-vault.md)]



## <a name="select-a-protection-goal"></a>Sélectionner un objectif de protection

Sélectionnez les éléments tooreplicate, et où vous souhaitez que tooreplicate à.

1. Cliquez sur **Coffres Recovery Services** > coffre.
2. Bonjour ressource Menu, cliquez sur **Site Recovery** > **préparer l’Infrastructure** > **objectif de Protection**.
3. Dans **objectif de Protection**, sélectionnez **tooAzure** > **Oui, avec Hyper-V**. Sélectionnez **Oui** tooconfirm vous n VMM. 

     ![Sélectionner des objectifs](./media/vmm-to-azure-walkthrough-create-vault/choose-goals.png)



## <a name="next-steps"></a>Étapes suivantes

Accédez trop[étape 8 : configurer la source et cible](vmm-to-azure-walkthrough-source-target.md)
