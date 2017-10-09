---
title: "architecture de hello aaaReview pour le site secondaire tooa réplication Hyper-V avec Azure Site Recovery | Documents Microsoft"
description: "Cet article fournit une vue d’ensemble de l’architecture de hello pour répliquer des ordinateurs virtuels Hyper-V tooa secondaire System Center VMM site local avec Azure Site Recovery."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 07099161-4cc7-4f32-8eb9-2a71bbf0750b
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/30/2017
ms.author: raynew
ms.openlocfilehash: 0de4b4e8601116c73e6fd710597ce4e561884368
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="step-1-review-hello-architecture-for-hyper-v-replication-tooa-secondary-site"></a>Étape 1 : Passez en revue l’architecture hello pour le site secondaire de tooa de réplication Hyper-V

Cet article décrit les composants hello et processus impliqués lors de la réplication locale Hyper-V, machines virtuelles (VM) dans des clouds System Center Virtual Machine Manager (VMM), à l’aide de hello le site VMM secondaire tooa [Azure Site Recovery](site-recovery-overview.md)service Bonjour portail Azure.

Valider les commentaires en bas de hello de cet article ou Bonjour [Forum sur Azure Recovery Services](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).



## <a name="architectural-components"></a>Composants architecturaux

Voici ce que vous avez besoin pour la réplication de site VMM secondaire de machines virtuelles Hyper-V tooa.

**Composant** | **Emplacement** | **Détails**
--- | --- | ---
**Microsoft Azure** | Abonnement dans Azure. | Vous créez un coffre Recovery Services Bonjour abonnement Azure, tooorchestrate et gérez la réplication entre les emplacements de VMM.
**Serveur VMM** | Vous avez besoin d’un emplacement VMM principal et secondaire. | Nous vous recommandons d’un serveur VMM dans le site principal de hello et un site secondaire de hello 
**Serveur Hyper-V** |  Serveurs d’hôte Hyper-V un ou plusieurs dans des clouds VMM principaux et secondaires hello. | Données sont répliquées entre hello serveurs principaux et secondaires Hyper-V hôte via hello LAN ou VPN, à l’aide de l’authentification Kerberos ou le certificat.  
**Machines virtuelles Hyper-V** | Sur le serveur hôte Hyper-V. | serveur hôte de Hello source doit avoir au moins une machine virtuelle que vous souhaitez tooreplicate.

## <a name="replication-process"></a>Processus de réplication

1. Vous définir hello compte Azure, créez un coffre Recovery Services et ce que vous souhaitez tooreplicate.
2. Vous configurez hello source et cible paramètres de réplication, notamment l’installation hello fournisseur Azure Site Recovery sur les serveurs VMM et l’agent de Microsoft Azure Recovery Services hello sur chaque ordinateur hôte Hyper-V.
3. Vous créez une stratégie de réplication pour la source de hello cloud VMM. stratégie de Hello est appliqué tooall machines virtuelles situées sur des ordinateurs hôtes dans le cloud de hello.
4. Activation de la réplication pour chaque VMM et la réplication initiale d’une machine virtuelle a lieu conformément aux paramètres que vous choisissez hello.
5. À l’issue de la réplication initiale, la réplication des modifications delta commence. Les modifications qui font l’objet d’un suivi sont conservées dans un fichier .hrl.


![Tooon-site local](./media/vmm-to-vmm-walkthrough-architecture/arch-onprem-onprem.png)

## <a name="failover-and-failback-process"></a>Processus de basculement et de restauration automatique

1. Vous pouvez effectuer un [basculement](site-recovery-failover.md) planifié ou non planifié entre des sites locaux. Si vous exécutez un basculement planifié, alors que les machines virtuelles source sont arrêtés tooensure aucune perte de données.
2. Vous pouvez basculer d’un seul ordinateur, ou créer [plans de récupération](site-recovery-create-recovery-plans.md) basculement tooorchestrate de plusieurs ordinateurs.
4. Si vous effectuez un basculement non planifié tooa site secondaire une fois que les machines de basculement hello dans l’emplacement secondaire de hello ne sont pas activés pour la réplication ou de protection. Si vous avez exécuté un basculement planifié, après le basculement de hello, dans l’emplacement secondaire de hello, les ordinateurs sont protégés.
5. Ensuite, vous validez hello basculement toostart accès hello la charge de travail à partir de l’ordinateur virtuel de réplication hello.
6. Lorsque votre site principal est à nouveau disponible, vous lancez tooreplicate la réplication inverse de hello toohello de site secondaire principal. La réplication inverse place les ordinateurs virtuels de hello dans un état protégé, mais hello de centre de données secondaire est toujours un emplacement Directory hello.
7. site principal de hello toomake dans un emplacement Directory hello là encore, vous initiez un basculement planifié à partir de tooprimary secondaire, suivie de la réplication inverse un autre.



## <a name="next-steps"></a>Étapes suivantes

Accédez trop[étape 2 : passez en revue les conditions préalables de hello et limitations](vmm-to-vmm-walkthrough-prerequisites.md).
