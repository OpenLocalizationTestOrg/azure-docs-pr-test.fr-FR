---
title: "tooAzure d’ordinateurs virtuels VMware aaaReplicate avec Azure Site Recovery | Documents Microsoft"
description: "Fournit une vue d’ensemble des étapes de hello pour répliquer les charges de travail en cours d’exécution sur les ordinateurs virtuels VMware tooAzure"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: dab98aa5-9c41-4475-b7dc-2e07ab1cfd18
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: 7104f67a3635b916048dcb61bca770c89f0c77fc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-vmware-vms-tooazure-with-site-recovery"></a>Répliquer tooAzure les ordinateurs virtuels VMware avec Site Recovery

Cet article fournit une vue d’ensemble de hello étapes tooreplicate requis local VMware virtual machines tooAzure, à l’aide de hello [Azure Site Recovery](site-recovery-overview.md) service Bonjour portail Azure.


![Processus de déploiement](./media/vmware-walkthrough-overview/vmware-to-azure-process.png)

**Figure 1 : Résumé du processus de déploiement**

## <a name="step-1-review-architecture-and-prerequisites"></a>Étape 1 : vérifier l’architecture et les conditions préalables.

Avant de commencer le déploiement, consultez architecture du scénario hello et assurez-vous que vous comprenez tous les composants hello vous devez toodeploy

Accédez trop[étape 1 : examen de l’architecture de hello](vmware-walkthrough-architecture.md)


## <a name="step-2-review-prerequisites"></a>Étape 2 : Vérifier les conditions préalables

Vérifiez que vous disposez des prérequis de hello en place pour chaque composant de déploiement :

- **Conditions préalables Azure** : vous avez besoin d’un compte Microsoft Azure, d’un réseau Azure et de comptes de stockage.
- **Composants Site Recovery locaux** : vous avez besoin d’une machine exécutant les composants Site Recovery locaux.
- **Conditions préalables de VMware local**: vous devez tooset des comptes afin que la récupération de Site peut accéder aux serveurs VMware et les machines virtuelles.
- **Répliquer les machines virtuelles**: machines virtuelles vous toocomply besoin de tooreplicate aux exigences d’Azure et souhaitez composant du service mobilité hello installé.

Accédez trop[étape 2 : passez en revue les conditions préalables et restrictions](vmware-walkthrough-prerequisites.md)

## <a name="step-3-plan-capacity"></a>Étape 3 : planifier la capacité

Si vous effectuez un déploiement complet, vous devez toofigure à quelles ressources de réplication que vous avez besoin. Il existe deux de toohelp disponibles des outils pour cela. Accédez tooStep 2. Si vous effectuez une rapide configurer tootest hello environnement, vous pouvez ignorer cette étape.

Accédez trop[étape 3 : planifier la capacité](vmware-walkthrough-capacity.md)

## <a name="step-4-plan-networking"></a>Étape 4 : Planifier la mise en réseau

Vous devez toodo certains planification tooensure que les machines virtuelles Azure sont toonetworks connectés après que le basculement se produit, et que qu’ils ont hello droite des adresses IP d’un réseau.

Accédez trop[étape 4 : planifier la mise en réseau](vmware-walkthrough-network.md)

##  <a name="step-5-prepare-azure-resources"></a>Étape 5 : Préparer les ressources Azure

Configurez les réseaux et le stockage Azure avant de commencer. Vous pouvez le faire pendant le déploiement, mais nous vous recommandons de vous en occuper avant de commencer.

Accédez trop[étape 5 : préparer le Azure](vmware-walkthrough-prepare-azure.md)


## <a name="step-6-prepare-vmware"></a>Étape 6 : préparer VMware

Vous devez tooset des comptes de la récupération de Site utilisera pour :

- Tooautomatically de serveurs de virtualisation de VMware accès détecter les ordinateurs virtuels.
- Accéder au service de mobilité des machines virtuelles tooinstall hello. Chaque ordinateur virtuel que vous souhaitez tooreplicate agent doit être hello mobilité service installé avant que vous pouvez activer la réplication.

Accédez trop[étape 6 : préparation de VMware](vmware-walkthrough-prepare-vmware.md)

## <a name="step-7-set-up-a-vault"></a>Étape 7 : configurer un coffre

Vous devez tooset d’un tooorchestrate du coffre Recovery Services et gérez la réplication. Lorsque vous configurez le coffre de hello, vous spécifiez ce que vous voulez tooreplicate, et où vous souhaitez que tooreplicate à.

Accédez trop[étape 7 : configurer un coffre](vmware-walkthrough-create-vault.md)

## <a name="step-8-configure-source-and-target-settings"></a>Étape 8 : configurer les paramètres de source et de cible

Configurer la source de hello et la cible qui est utilisée pour la réplication. Configuration des paramètres de la source inclut exécutant le programme d’installation unifiée tooinstall composants de Site Recovery hello locaux.

Accédez trop[étape 8 : configurer hello source et cible](vmware-walkthrough-source-target.md)

## <a name="step-9-set-up-a-replication-policy"></a>Étape 9 : configurer une stratégie de réplication

Vous définissez des paramètres de réplication toospecify de stratégie pour les ordinateurs virtuels VMware dans le coffre hello.

Accédez trop[étape 9 : configurer une stratégie de réplication](vmware-walkthrough-replication.md)

## <a name="step-10-install-hello-mobility-service"></a>Étape 10 : Installer le service de mobilité hello

Hello service mobilité doit être installé sur chaque machine virtuelle, vous souhaitez tooreplicate. Il existe quelques façons tooset, configuration du service d’installation push ou pull hello.

Accédez trop[étape 10 : installer le service de mobilité hello](vmware-walkthrough-install-mobility.md)

## <a name="step-11-enable-replication"></a>Étape 11 : activer la réplication

Vous pouvez activer la réplication après que hello service mobilité est en cours d’exécution sur une machine virtuelle. Après l’activation, la réplication initiale de hello machine virtuelle se produit.

Accédez trop[étape 11 : activer la réplication](vmware-walkthrough-enable-replication.md)

## <a name="step-12-run-a-test-failover"></a>Étape 12 : exécuter un test de basculement

Une fois la réplication initiale se termine, et la réplication delta est en cours d’exécution, vous pouvez exécuter un toomake de basculement de test que tout fonctionne comme prévu.

Accédez trop[étape 12 : exécuter un test de basculement](vmware-walkthrough-test-failover.md)
