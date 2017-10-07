---
title: "le mappage réseau aaaConfigure pour répliquer des ordinateurs virtuels Hyper-V dans VMM nuages tooAzure avec Azure Site Recovery | Documents Microsoft"
description: "Décrit comment le mappage réseau tooconfigure lors de la réplication des ordinateurs virtuels Hyper-V dans VMM nuages tooAzure avec Azure Site Recovery"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: jwhit
editor: tysonn
ms.assetid: 8e7d868e-00f3-4e8b-9a9e-f23365abf6ac
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/23/2017
ms.author: raynew
ms.openlocfilehash: 081a9fdb0ffa4114099e9bcb9c1b1e43ad26ecbb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="step-9-configure-network-mapping-for-hyper-v-replication-with-vmm-tooazure"></a>Étape 9 : Configurer le mappage réseau pour tooAzure de réplication (avec VMM) Hyper-V

Après avoir configuré hello [les paramètres de réplication source et cible](vmm-to-azure-walkthrough-source-target.md), utilisez cette toomap de mappage de l’article tooconfigure réseau entre les réseaux d’ordinateurs virtuels VMM local et les réseaux Azure.

Ajouter des commentaires et questions bas hello de cet article, ou sur hello [Forum sur Azure Recovery Services](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

## <a name="before-you-start"></a>Avant de commencer

- En savoir plus sur le [mappage réseau](vmm-to-azure-walkthrough-network.md#network-mapping-for-replication-to-azure).
- [Préparez VMM pour le mappage réseau](vmm-to-azure-walkthrough-network.md#prepare-vmm-for-network-mapping). 
- Vérifiez que les ordinateurs virtuels sur le serveur VMM de hello sont connectés tooa réseau d’ordinateurs virtuels et que vous avez créé au moins un réseau virtuel Azure. Plusieurs réseaux d’ordinateurs virtuels peuvent être mappés tooa réseau Azure unique.

## <a name="configure-mapping"></a>Configuration du mappage

Configurez le mappage comme suit :

1. Dans **Infrastructure Site Recovery** > **réseau mappages** > **mappage réseau**, cliquez sur hello **+ mappage réseau**  icône.

    ![Mappage réseau](./media/vmm-to-azure-walkthrough-network-mapping/network-mapping1.png)
2. Dans **ajouter le mappage réseau**, sélectionnez serveur VMM source à hello, et **Azure** comme cible de hello.
3. Vérifiez l’abonnement de hello et le modèle de déploiement hello après le basculement.
4. Dans **réseau Source**, sélectionnez le réseau d’ordinateurs virtuels de hello source locale que vous souhaitez toomap à partir de la liste hello associé avec le serveur VMM de hello.
5. Dans **réseau cible**, sélectionnez hello réseau Azure dans le réplica de machines virtuelles Azure se trouve lorsqu’elles sont créées. Cliquez ensuite sur **OK**.

    ![Mappage réseau](./media/vmm-to-azure-walkthrough-network-mapping/network-mapping2.png)

Voici le processus exécuté lorsque le mappage réseau démarre :

* Machines virtuelles existantes sur le réseau d’ordinateurs virtuels hello source sont réseau cible de toohello connecté au commencement de mappage. Réseau d’ordinateurs virtuels source nouvelles machines virtuelles connectés toohello connectés toohello mappé réseau Azure lors de la réplication a lieu.
* Si vous modifiez un mappage réseau existant, les machines virtuelles de réplication se connecter à l’aide de nouveaux paramètres de hello.
* Si le réseau cible de hello possède plusieurs sous-réseaux, et un de ces sous-réseaux a hello le même nom que le sous-réseau sur lequel virtual machine de hello source se trouve, puis hello ordinateur virtuel se connecte le sous-réseau de toothat cible après le basculement.
* S’il n’existe aucun sous-réseau cible avec un nom correspondant, ordinateur virtuel de hello se connecte toohello premier sous-réseau de réseau de hello.



## <a name="next-steps"></a>Étapes suivantes

Accédez trop[étape 10 : créer une stratégie de réplication](vmm-to-azure-walkthrough-replication.md)
