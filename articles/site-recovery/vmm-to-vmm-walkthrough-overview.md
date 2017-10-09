---
title: aaaReplicate des ordinateurs virtuels Hyper-V tooa secondaire deux sites VMM avec Azure Site Recovery | Documents Microsoft
description: "Fournit une vue d’ensemble pour la réplication de site VMM secondaire tooa ordinateurs virtuels Hyper-V à l’aide de hello portail Azure."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: jwhit
editor: 
ms.assetid: 476ca82a-8f5c-4498-9dcf-e1011d60ed59
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: raynew
ms.openlocfilehash: 90e44bfc2237dfa7646fb2b7b1e533a7f6d83c50
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-hyper-v-virtual-machines-in-vmm-clouds-tooa-secondary-vmm-site"></a>Réplication d’ordinateurs virtuels Hyper-V dans le site VMM secondaire VMM clouds tooa

> [!div class="op_single_selector"]
> * [Portail Azure](site-recovery-vmm-to-vmm.md)
> * [Portail classique](site-recovery-vmm-to-vmm-classic.md)
> * [PowerShell - Resource Manager](site-recovery-vmm-to-vmm-powershell-resource-manager.md)
>
>

Cet article fournit une vue d’ensemble de hello étapes requises tooreplicate local Hyper-V virtual machines virtuelles gérées dans des clouds System Center Virtual Machine Manager (VMM), emplacement de VMM secondaire tooa, à l’aide de [Azure Site Recovery](site-recovery-overview.md)Bonjour portail Azure.

Après avoir lu cet article, validez les commentaires au bas de hello, ou sur hello [Forum sur Azure Recovery Services](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="step-1-review-hello-scenario-architecture"></a>Étape 1 : Passez en revue l’architecture du scénario de hello

Avant de commencer le déploiement, examen de l’architecture du scénario hello et assurez-vous que vous comprenez tous les composants de hello, vous devez toodeploy.

Accédez trop[étape 1 : examen de l’architecture de hello](vmm-to-vmm-walkthrough-architecture.md).

## <a name="step-2-review-prerequisites-and-limitations"></a>Étape 2 : Vérifier les conditions préalables et les limitations

Assurez-vous que vous comprenez les limitations et les conditions préalables au déploiement de hello.

**Conditions préalables Azure**: vous avez besoin d’un abonnement Microsoft Azure et Azure Recovery Services coffre, tooorchestrate et gérer la réplication.
**Serveurs VMM et hôtes Hyper-V locaux** : assurez-vous que les serveurs VMM et les hôtes Hyper-V sont conformes et préparés pour le déploiement Site Recovery.

Accédez trop[étape 2 : vérifier les conditions préalables et limitations](vmm-to-vmm-walkthrough-prerequisites.md).

## <a name="step-3-plan-networking"></a>Étape 3 : Planifier la mise en réseau

Vous devez toodo certains tooensure que vous pouvez configurer le mappage réseau entre les réseaux de VM de VMM lorsque vous déployez le scénario de hello de planification d’un réseau.

Accédez trop[étape 3 : planifier la mise en réseau](vmm-to-vmm-walkthrough-network.md).


## <a name="step-4-prepare-vmm-and-hyper-v"></a>Étape 4 : Préparer VMM et Hyper-V

Préparer les serveurs VMM hello et hôtes Hyper-V pour le déploiement de la récupération de Site.

Accédez trop[étape 4 : préparer les serveurs locaux](vmm-to-vmm-walkthrough-vmm-hyper-v.md).

## <a name="step-5-set-up-a-vault"></a>Étape 5 : Configurer un coffre

Configurez un coffre Recovery Services. coffre de Hello contient les paramètres de configuration et orchestre la réplication.

[Étape 5 : Configurer un coffre](vmm-to-vmm-walkthrough-create-vault.md)

## <a name="step-6-set-up-source-and-target-settings"></a>Étape 6 : Configurer les paramètres de la source et de la cible

Configurez les emplacements de VMM réplication source et cible des hello. Ajouter hello VMM serveurs toohello coffre-fort et télécharger les fichiers d’installation hello pour les composants de Site Recovery. Exécutez le programme d’installation du fournisseur Azure Site Recovery sur le serveur VMM de hello. Le programme d’installation installe hello fournisseur sur le serveur VMM de hello et les enregistre sur le serveur hello dans le coffre de hello. Vous installez hello Microsoft Recovery Services agent sur chaque hôte Hyper-V.

Accédez trop[étape 6 : configurer les paramètres source et cible hello](vmm-to-vmm-walkthrough-source-target.md).

## <a name="step-7-configure-network-mapping"></a>Étape 7 : Configuration du mappage réseau

Mappez les réseaux VMM VM dans les emplacements source et cible hello. Après le basculement, les machines virtuelles sont créées dans le réseau cible de hello ce réseau d’ordinateurs virtuels maps toohello source dans le hello source d’ordinateur virtuel Hyper-V se trouve.

Accédez trop[étape 7 : configurer le mappage réseau](vmm-to-vmm-walkthrough-network-mapping.md).


## <a name="step-8-set-up-a-replication-policy"></a>Étape 8 : Configurer une stratégie de réplication

Spécifiez comment les machines virtuelles seront répliquées entre les emplacements VMM.

Accédez trop[étape 8 : définir une stratégie de réplication](vmm-to-vmm-walkthrough-replication.md).


## <a name="step-9-enable-replication-for-vms"></a>Étape 9 : Activer la réplication des machines virtuelles

Sélectionnez hello machines virtuelles tooreplicate. Activation d’une machine virtuelle pour le site secondaire toohello de la réplication initiale hello réplication déclencheurs, suivie de la réplication delta en cours.

Accédez trop[étape 9 : activer la réplication](vmm-to-vmm-walkthrough-enable-replication.md).


## <a name="step-10-run-a-test-failover"></a>Étape 10 : Exécuter un test de basculement

Exécutez un toomake de basculement de test que tout fonctionne comme prévu.

Accédez trop[étape 10 : exécuter un test de basculement](vmm-to-vmm-walkthrough-test-failover.md).
