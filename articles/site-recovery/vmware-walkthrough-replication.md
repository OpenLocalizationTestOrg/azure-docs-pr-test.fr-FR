---
title: "aaaSet une stratégie de réplication pour tooAzure de réplication VMware VM avec Azure Site Recovery | Documents Microsoft"
description: "Résume les étapes hello vous devez tooset une stratégie de réplication lors de la réplication des ordinateurs virtuels VMware tooAzure stockage"
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
ms.openlocfilehash: 12870f3f98a4dd412221b817581403cd4bf7a76d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="step-9-set-up-a-replication-policy-for-vmware-vm-replication-tooazure"></a>Étape 9 : Configurer une stratégie de réplication pour VMware VM réplication tooAzure


Cet article décrit comment tooset une stratégie de réplication lorsque vous effectuez une réplication tooAzure les ordinateurs virtuels VMware à l’aide de hello [Azure Site Recovery](site-recovery-overview.md) service Bonjour portail Azure.


Ajouter des commentaires et questions bas hello de cet article, ou sur hello [Forum sur Azure Recovery Services](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="configure-a-policy"></a>Configurer une stratégie

Visionnez une courte vidéo de présentation avant de commencer :
> [!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/VMware-to-Azure-with-ASR-Video2-vCenter-Server-Discovery-and-Replication-Policy/player]

1. toocreate une stratégie de réplication, cliquez sur **infrastructure de Site Recovery** > **stratégies de réplication** > **+ la stratégie de réplication**.
2. Dans **Créer une stratégie de réplication**, indiquez le nom de la stratégie.
3. Dans **seuil RPO**, spécifiez la limite RPO hello. Cette valeur spécifie la fréquence à laquelle les points de récupération des données sont créés. Une alerte est générée lorsque la réplication continue dépasse cette limite.
4. Dans **rétention du point de récupération**, spécifiez la durée (en heures) est d’une fenêtre de rétention hello pour chaque point de récupération. Machines virtuelles répliquées peuvent être récupérées point tooany dans une fenêtre. Des too24 rétention d’heures est pris en charge pour les machines répliquées toopremium stockage et 72 heures pour le stockage standard.
5. Dans **Fréquence des captures instantanées de cohérence d’application**, spécifiez la fréquence de création des points de récupération contenant des captures instantanées cohérentes avec les applications (en minutes). Cliquez sur **OK** stratégie de hello toocreate.

    ![Stratégie de réplication](./media/vmware-walkthrough-replication/gs-replication2.png)
8. Lorsque vous créez une nouvelle stratégie, il est automatiquement associé serveur de configuration hello. Par défaut, une stratégie de correspondance est automatiquement créée pour la restauration automatique. Par exemple, si hello stratégie de réplication est **rep-policy** stratégie de restauration automatique hello sera **rep-stratégie de la restauration automatique**. Cette stratégie n’est utilisée qu’à partir du moment où vous initiez une restauration automatique à partir d’Azure.

## <a name="next-steps"></a>Étapes suivantes

Accédez trop[étape 10 : installer le service de mobilité hello](vmware-walkthrough-install-mobility.md)
