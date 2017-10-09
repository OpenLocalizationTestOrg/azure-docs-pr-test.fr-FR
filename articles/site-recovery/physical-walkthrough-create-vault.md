---
title: "aaaSet d’un coffre pour tooAzure de réplication de serveur physique à l’aide d’Azure Site Recovery | Documents Microsoft"
description: "Résume les étapes hello tooset d’un tooAzure de serveurs physiques tooreplicate coffre à l’aide d’Azure Site Recovery"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: d99f2605-f417-4995-be77-5323136b814f
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: 988928e3ece31116823f132cc39223fe44443468
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="step-6-set-up-a-vault-for-physical-server-replication-tooazure"></a>Étape 6 : Configurer un coffre pour tooAzure de réplication de serveur physique


Cet article décrit comment tooset d’un coffre. Vous créez le coffre hello et spécifier ce que vous souhaitez tooreplicate à partir de votre tooAzure emplacement local, à l’aide de hello [Azure Site Recovery](site-recovery-overview.md) service Bonjour portail Azure.


Ajouter des commentaires et questions bas hello de cet article, ou sur hello [Forum sur Azure Recovery Services](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).




## <a name="create-a-recovery-services-vault"></a>Créer un coffre Recovery Services

[!INCLUDE [site-recovery-create-vault](../../includes/site-recovery-create-vault.md)]

## <a name="select-a-protection-goal"></a>Sélectionner un objectif de protection

Sélectionnez les éléments tooreplicate, et où vous souhaitez que tooreplicate à.

1. Cliquez sur **Coffres Recovery Services** > coffre.
2. Bonjour ressource Menu, cliquez sur **Site Recovery** > **préparer l’Infrastructure** > **objectif de Protection**.
3. Dans **objectif de Protection**, sélectionnez **tooAzure** > **non virtualisé,**.


## <a name="next-steps"></a>Étapes suivantes

Accédez trop[étape 7 : configurer la source et cible](physical-walkthrough-source-target.md)
