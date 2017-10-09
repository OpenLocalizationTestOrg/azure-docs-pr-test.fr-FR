---
title: aaaReplicate physique local tooAzure serveurs avec Azure Site Recovery | Documents Microsoft
description: "Fournit une vue d’ensemble des étapes de hello pour répliquer les charges de travail en cours d’exécution sur tooAzure de serveurs physiques locaux Windows/Linux avec hello service Azure Site Recovery."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 20122f01-929a-4675-b85b-a9b99d2618bc
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: f801b9544072d4029ec06cc1abfd4ff370e852e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-physical-servers-tooazure-with-site-recovery"></a>Répliquer tooAzure serveurs physiques avec Site Recovery

Cet article fournit une vue d’ensemble de hello étapes requises tooreplicate local Windows/Linux serveurs physiques tooAzure, à l’aide de hello [Azure Site Recovery](site-recovery-overview.md) service Bonjour portail Azure.


## <a name="step-1-review-architecture-and-prerequisites"></a>Étape 1 : vérifier l’architecture et les conditions préalables.

Avant de commencer le déploiement, consultez architecture du scénario hello et assurez-vous que vous comprenez tous les composants hello vous devez tooset le déploiement de hello.

Accédez trop[étape 1 : examen de l’architecture de hello](physical-walkthrough-architecture.md)


## <a name="step-2-review-prerequisites"></a>Étape 2 : Vérifier les conditions préalables

Vérifiez que vous disposez des prérequis de hello en place pour chaque composant de déploiement :

- **Conditions préalables Azure** : vous avez besoin d’un compte Microsoft Azure, d’un réseau Azure et de comptes de stockage.
- **Composants Site Recovery locaux** : vous avez besoin d’une machine exécutant les composants Site Recovery locaux.
- **Machines répliquées**: serveurs tooreplicate doivent toocomply avec locaux et les conditions requises pour Azure.

Accédez trop[étape 2 : passez en revue les conditions préalables et restrictions](physical-walkthrough-prerequisites.md)

## <a name="step-3-plan-capacity"></a>Étape 3 : planifier la capacité

Si vous effectuez un déploiement complet, vous devez toofigure à quelles ressources de réplication que vous avez besoin. Si vous effectuez une rapide configurer tootest hello environnement, vous pouvez ignorer cette étape.

Accédez trop[étape 3 : planifier la capacité](physical-walkthrough-capacity.md)

## <a name="step-4-plan-networking"></a>Étape 4 : Planifier la mise en réseau

Vous devez toodo certains planification tooensure que les machines virtuelles Azure sont toonetworks connectés après que le basculement se produit, et que qu’ils ont hello droite des adresses IP d’un réseau.

Accédez trop[étape 4 : planifier la mise en réseau](physical-walkthrough-network.md)

##  <a name="step-5-prepare-azure-resources"></a>Étape 5 : Préparer les ressources Azure

Configurez les réseaux et le stockage Azure avant de commencer. 

Accédez trop[étape 5 : préparer le Azure](physical-walkthrough-prepare-azure.md)


## <a name="step-6-set-up-a-vault"></a>Étape 6 : Configurer un coffre

Vous configurez un tooorchestrate du coffre Recovery Services et gérez la réplication. Lorsque vous configurez le coffre de hello, vous spécifiez ce que vous voulez tooreplicate, et où vous souhaitez que tooreplicate à.

Accédez trop[étape 6 : configurer un coffre](physical-walkthrough-create-vault.md)

## <a name="step-7-configure-source-and-target-settings"></a>Étape 7 : Configurer les paramètres de source et de cible

Configurer les paramètres de source de hello et cibles de site (Azure). Paramètres de la source inclut exécutant le programme d’installation unifiée tooinstall composants de Site Recovery hello locaux.

Accédez trop[étape 7 : configurer hello source et cible](physical-walkthrough-source-target.md)

## <a name="step-8-set-up-a-replication-policy"></a>Étape 8 : Configurer une stratégie de réplication

Vous configurez une stratégie toospecify physiques doivent répliquer les serveurs.

Accédez trop[étape 8 : définir une stratégie de réplication](physical-walkthrough-replication.md)

## <a name="step-9-install-hello-mobility-service"></a>Étape 9 : Installer le service de mobilité hello

Hello service mobilité doit être installé sur chaque serveur, vous souhaitez tooreplicate. Il existe quelques façons tooset, configuration du service hello, avec l’installation push ou pull.

Accédez trop[étape 9 : installer le service de mobilité hello](physical-walkthrough-install-mobility.md)

## <a name="step-10-enable-replication"></a>Étape 10 : Activer la réplication

Une fois hello service mobilité est en cours d’exécution sur un serveur, vous pouvez activer la réplication. Après l’activation, la réplication initiale de hello machine virtuelle se produit.

Accédez trop[étape 10 : activer la réplication](physical-walkthrough-enable-replication.md)

## <a name="step-11-run-a-test-failover"></a>Étape 11 : Exécuter un test de basculement

Une fois la réplication initiale est terminée et la réplication delta est en cours d’exécution, vous pouvez exécuter un toomake de basculement de test que tout fonctionne comme prévu.

Accédez trop[étape 11 : exécuter un test de basculement](physical-walkthrough-test-failover.md)

