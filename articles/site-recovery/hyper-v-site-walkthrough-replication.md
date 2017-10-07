---
title: "aaaSet une stratégie de réplication pour tooAzure de réplication (sans System Center VMM) d’un ordinateur virtuel Hyper-V avec Azure Site Recovery | Documents Microsoft"
description: "Résume les étapes hello vous devez tooset une stratégie de réplication lors de la réplication des ordinateurs virtuels Hyper-V tooAzure stockage"
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 1777e0eb-accb-42b5-a747-11272e131a52
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/22/2017
ms.author: raynew
ms.openlocfilehash: 4bd7161f4a0f015da0ecf595fbc6861ede5d68b0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="step-9-set-up-a-replication-policy-for-hyper-v-vm-replication-tooazure"></a>Étape 9 : Configurer une stratégie de réplication pour tooAzure de réplication de machine virtuelle Hyper-V

Cet article décrit comment tooset une stratégie de réplication lorsque vous effectuez une réplication tooAzure d’ordinateurs virtuels Hyper-V (sans System Center VMM) à l’aide de hello [Azure Site Recovery](site-recovery-overview.md) service Bonjour portail Azure.


Ajouter des commentaires et questions bas hello de cet article, ou sur hello [Forum sur Azure Recovery Services](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

## <a name="about-snapshots"></a>Informations concernant les instantanés

Hyper-V utilise deux types de captures instantanées, un instantané standard qui fournit un instantané incrémentiel de la machine virtuelle hello et un instantané cohérent de l’application qui prend un instantané de point-à-temps hello des données d’application à l’intérieur de machine virtuelle de hello.
    - Instantanés cohérents au niveau de l’application utilisent tooensure Volume Shadow Copy Service (VSS) que les applications sont dans un état cohérent lors de l’instantané hello.
    - Si vous activez les instantanés cohérents au niveau de l’application, il affecte les performances de hello des applications exécutées sur des machines virtuelles sources. Assurez-vous que la valeur hello que vous définissez est inférieur au nombre de hello de points de récupération supplémentaires que vous configurez.

## <a name="set-up-a-replication-policy"></a>Configurer une stratégie de réplication

1. toocreate une stratégie de réplication, cliquez sur **Prepare infrastructure** > **les paramètres de réplication** > **+ créer et associer**.

    ![Réseau](./media/hyper-v-site-walkthrough-replication/gs-replication.png)
2. Dans **Créer et associer une stratégie**, indiquez le nom de la stratégie.
3. Dans **fréquence de copie**, spécifiez la fréquence à laquelle vous souhaitez tooreplicate d’éventuelles données delta après la réplication initiale de hello (toutes les 30 secondes, 5 ou 15 minutes).

    > [!NOTE]
    > Une fréquence de deuxième 30 n’est pas pris en charge lors de la réplication de stockage de toopremium. limitation de Hello est déterminée par le nombre de hello d’instantanés par l’objet blob (100) pris en charge par le stockage premium. [En savoir plus](../storage/common/storage-premium-storage.md#snapshots-and-copy-blob).

4. Dans **rétention du point de récupération**, spécifiez combien d’heures de conservation hello est pour chaque point de récupération. Machines virtuelles peuvent être récupérée point tooany dans une fenêtre.
5. Dans **Fréquence des captures instantanées cohérentes de l’application**, spécifiez la fréquence de création des points de récupération contenant des instantanés cohérents au niveau des applications (entre 1 et 12 heures).
6. Dans **heure de début de la réplication initiale**, spécifiez quand toostart hello la réplication initiale. la réplication Hello se produit sur votre bande passante internet, vous pouvez donc tooschedule il en dehors des heures occupés. Cliquez ensuite sur **OK**.

    ![Stratégie de réplication](./media/hyper-v-site-walkthrough-replication/gs-replication2.png)

Lorsque vous créez une nouvelle stratégie, il est automatiquement associé site Hyper-V de hello. Vous pouvez associer un site Hyper-V (et hello machines virtuelles qu’il contient) à plusieurs stratégies de réplication dans **réplication** > nom de la stratégie > **associer le Site Hyper-V**.



## <a name="next-steps"></a>Étapes suivantes

Accédez trop[étape 10 : activer la réplication](hyper-v-site-walkthrough-enable-replication.md)
