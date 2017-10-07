---
title: "aaaSet une stratégie de réplication pour tooAzure de réplication d’ordinateur virtuel d’Hyper-V (avec VMM) avec Azure Site Recovery | Documents Microsoft"
description: "Décrit comment tooset une stratégie de réplication pour tooAzure de réplication d’ordinateur virtuel d’Hyper-V (avec VMM) avec Azure Site Recovery"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: ee808b20-324b-4198-b831-edb65b95e8b7
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/23/2017
ms.author: raynew
ms.openlocfilehash: e1579fde559ca34eca19a01e740fec28a0df2f9e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="step-10-set-up-a-replication-policy-for-hyper-v-vm-replication-with-vmm-tooazure"></a>Étape 10 : Définir une stratégie de réplication pour tooAzure de réplication (avec VMM) d’un ordinateur virtuel Hyper-V


Après avoir configuré [le mappage réseau](vmm-to-azure-walkthrough-network-mapping.md), utilisez cette tooconfigure article une stratégie de réplication T\tooreplicate locaux virtuels Hyper-V gérés dans tooAzure des clouds System Center Virtual Machine Manager (VMM), à l’aide de hello [ Azure Site Recovery](site-recovery-overview.md) service Bonjour portail Azure.

Après avoir lu cet article, validez les commentaires au bas de hello, ou sur hello [Forum sur Azure Recovery Services](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).



## <a name="create-a-policy"></a>Création d’une stratégie

1. toocreate une stratégie de réplication, cliquez sur **Prepare infrastructure** > **les paramètres de réplication** > **+ créer et associer**.

    ![Réseau](./media/vmm-to-azure-walkthrough-replication/gs-replication.png)
2. Dans **Créer et associer une stratégie**, indiquez le nom de la stratégie.
3. Dans **fréquence de copie**, spécifiez la fréquence à laquelle vous souhaitez tooreplicate d’éventuelles données delta après la réplication initiale de hello (toutes les 30 secondes, 5 ou 15 minutes).

    > [!NOTE]
    >  Une fréquence de deuxième 30 n’est pas pris en charge lors de la réplication de stockage de toopremium. limitation de Hello est déterminée par le nombre de hello d’instantanés par l’objet blob (100) pris en charge par le stockage premium. [En savoir plus](../storage/common/storage-premium-storage.md#snapshots-and-copy-blob)

4. Dans **rétention du point de récupération**, spécifiez, en heures, la durée de conservation hello sera être pour chaque point de récupération. Les ordinateurs protégés peuvent être récupérées point tooany dans une fenêtre.
5. Dans **Fréquence des captures instantanées cohérentes de l’application**, spécifiez la fréquence de création des points de récupération contenant des instantanés cohérents au niveau des applications (entre 1 et 12 heures). Hyper-V utilise deux types de captures instantanées, un instantané standard qui fournit un instantané incrémentiel de la machine virtuelle hello et un instantané cohérent de l’application qui prend un instantané de point-à-temps hello des données d’application à l’intérieur de machine virtuelle de hello. Instantanés cohérents au niveau de l’application utilisent tooensure Volume Shadow Copy Service (VSS) que les applications sont dans un état cohérent lors de l’instantané hello. Notez que si vous activez les instantanés cohérents au niveau de l’application, il affecte les performances de hello des applications s’exécutant sur des machines virtuelles sources. Assurez-vous que la valeur hello que vous définissez est inférieur au nombre de hello de points de récupération supplémentaires que vous configurez.
6. Dans **heure de début de la réplication initiale**, indiquer quand toostart hello la réplication initiale. la réplication Hello se produit sur votre bande passante internet, vous pouvez donc tooschedule il en dehors des heures occupés.
7. Dans **chiffrer les données stockées sur Azure**, spécifiez si tooencrypt données reste dans le stockage Azure. Cliquez ensuite sur **OK**.

    ![Stratégie de réplication](./media/vmm-to-azure-walkthrough-replication/gs-replication2.png)
8. Lorsque vous créez une nouvelle stratégie, il est automatiquement associé hello cloud VMM. Cliquez sur **OK**. Vous pouvez associer clouds VMM supplémentaires (et hello machines virtuelles dans les) cette stratégie de réplication dans **réplication** > nom de la stratégie > **associer le Cloud VMM**.

    ![Stratégie de réplication](./media/vmm-to-azure-walkthrough-replication/policy-associate.png)



## <a name="next-steps"></a>Étapes suivantes

Accédez trop[étape 11 : activer la réplication](vmm-to-azure-walkthrough-enable-replication.md)
