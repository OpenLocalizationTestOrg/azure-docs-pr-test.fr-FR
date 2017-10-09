---
title: "aaaSet une stratégie de réplication pour tooAzure de réplication de serveur physique avec Azure Site Recovery | Documents Microsoft"
description: "Résume les étapes hello vous devez tooset une stratégie de réplication lors de la réplication locale stockage tooAzure de serveurs physiques à l’aide du service d’Azure Site Recovery hello"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: d7874bd8-6626-4668-9ec9-dbd2d26f8f81
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: d6bdeeffc24ffc8eaba24311f7c76452edb65648
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="step-8-set-up-a-replication-policy-for-physical-server-replication-tooazure"></a>Étape 8 : Définir une stratégie de réplication pour le serveur physique réplication tooAzure


Cet article décrit comment tooset une stratégie de réplication lorsque vous effectuez une réplication tooAzure de serveurs physiques Windows/Linux à l’aide de hello [Azure Site Recovery](site-recovery-overview.md) service Bonjour portail Azure.


Ajouter des commentaires et questions bas hello de cet article, ou sur hello [Forum sur Azure Recovery Services](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="configure-a-policy"></a>Configurer une stratégie

1. Cliquez sur **Infrastructure de Site Recovery** > **Stratégies de réplication** > **+Stratégie de réplication**.
2. Dans **Créer une stratégie de réplication**, indiquez le nom de la stratégie.
3. Dans **seuil RPO**, spécifiez la limite RPO hello. Cette valeur indique la fréquence à laquelle les points de récupération des données sont créés. Une alerte est générée lorsque la réplication continue dépasse cette limite.
4. Dans **rétention du point de récupération**, spécifiez la durée (en heures) est d’une fenêtre de rétention hello pour chaque point de récupération. Machines virtuelles répliquées peuvent être récupérées point tooany dans une fenêtre. Des too24 rétention d’heures est pris en charge pour les machines répliquées toopremium stockage et 72 heures pour le stockage standard.
5. Dans **Fréquence des captures instantanées de cohérence d’application**, spécifiez la fréquence de création des points de récupération contenant des captures instantanées cohérentes avec les applications (en minutes). Cliquez sur **OK** stratégie de hello toocreate.

    ![Stratégie de réplication](./media/physical-walkthrough-replication/gs-replication2.png)
8. Lorsque vous créez une nouvelle stratégie, il est automatiquement associé serveur de configuration hello. Par défaut, une stratégie de correspondance est automatiquement créée pour la restauration automatique. Par exemple, si hello stratégie de réplication est **rep-policy** stratégie de restauration automatique hello sera **rep-stratégie de la restauration automatique**. Cette stratégie n’est utilisée qu’à partir du moment où vous initiez une restauration automatique à partir d’Azure.

## <a name="next-steps"></a>Étapes suivantes

Accédez trop[étape 9 : installer le service de mobilité hello](physical-walkthrough-install-mobility.md)
