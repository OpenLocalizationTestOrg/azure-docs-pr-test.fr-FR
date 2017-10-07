---
title: "tooAzure d’ordinateurs virtuels Hyper-V aaaReplicate avec Azure Site Recovery | Documents Microsoft"
description: "Décrit comment la réplication tooorchestrate, le basculement et récupération de local Hyper-V VM tooAzure"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: efddd986-bc13-4a1d-932d-5484cdc7ad8d
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/21/2017
ms.author: raynew
ms.openlocfilehash: ab9cd14149ef32a416428d0f4327aa18b042e9c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-hyper-v-virtual-machines-without-vmm-tooazure"></a>Répliquer tooAzure d’ordinateurs virtuels (sans VMM) Hyper-V 

> [!div class="op_single_selector"]
> * [Portail Azure](site-recovery-hyper-v-site-to-azure.md)
> * [Portail Azure Classic](site-recovery-hyper-v-site-to-azure-classic.md)
> * [PowerShell - Resource Manager](site-recovery-deploy-with-powershell-resource-manager.md)
>
>

Cet article fournit une vue d’ensemble de hello étapes requises tooreplicate local Hyper-V virtual machines tooAzure, à l’aide de hello [Azure Site Recovery](site-recovery-overview.md) Bonjour portail Azure. Dans ce déploiement, les machines virtuelles Hyper-V ne sont pas gérées par System Center Virtual Machine Manager (VMM).


Après avoir lu cet article, validez les commentaires en bas de hello ou poser des questions techniques sur hello [Forum sur Azure Recovery Services](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="step-1-review-architecture-and-prerequisites"></a>Étape 1 : vérifier l’architecture et les conditions préalables.

Avant de commencer le déploiement, consultez architecture du scénario hello et assurez-vous que vous comprenez tous les composants hello vous devez toodeploy

Accédez trop[étape 1 : examen de l’architecture de hello](hyper-v-site-walkthrough-architecture.md)


## <a name="step-2-review-prerequisites"></a>Étape 2 : Vérifier les conditions préalables

Vérifiez que vous disposez des prérequis de hello en place pour chaque composant de déploiement :

- **Conditions préalables Azure** : vous avez besoin d’un compte Microsoft Azure, d’un réseau Azure et de comptes de stockage.
- **Conditions préalables pour les machines virtuelles Hyper-V locales** : assurez-vous que les hôtes Hyper-V sont préparés pour le déploiement Site Recovery.
- **Répliquer les machines virtuelles**: machines virtuelles que vous souhaitez tooreplicate devez toocomply aux exigences d’Azure.

Accédez trop[étape 2 : vérifier les conditions préalables et restrictions](hyper-v-site-walkthrough-prerequisites.md)

## <a name="step-3-plan-capacity"></a>Étape 3 : planifier la capacité

Si vous effectuez un déploiement complet, vous devez toofigure à quelles ressources de réplication que vous avez besoin. Il existe deux de toohelp disponibles des outils pour cela. Accédez tooStep 2. Si vous effectuez une rapide configurer tootest hello environnement, vous pouvez ignorer cette étape.

Accédez trop[étape 3 : planifier la capacité](hyper-v-site-walkthrough-capacity.md)

## <a name="step-4-plan-networking"></a>Étape 4 : Planifier la mise en réseau

Vous devez toodo certains planification tooensure que les machines virtuelles Azure sont toonetworks connectés après que le basculement se produit, et que qu’ils ont hello droite des adresses IP d’un réseau.

Accédez trop[étape 4 : planifier la mise en réseau](hyper-v-site-walkthrough-network.md)

##  <a name="step-5-prepare-azure-resources"></a>Étape 5 : Préparer les ressources Azure

Configurez les réseaux et le stockage Azure avant de commencer. Vous pouvez le faire pendant le déploiement, mais nous vous recommandons de vous en occuper avant de commencer.

Accédez trop[étape 5 : préparer le Azure](hyper-v-site-walkthrough-prepare-azure.md)


## <a name="step-6-prepare-hyper-v"></a>Étape 6 : préparer Hyper-V

Assurez-vous que les serveurs Hyper-V remplissent les exigences liées au déploiement Site Recovery.

Accédez trop[étape 6 : préparation de Hyper-V](hyper-v-site-walkthrough-prepare-hyper-v.md)

## <a name="step-7-set-up-a-vault"></a>Étape 7 : configurer un coffre

Vous devez tooset d’un tooorchestrate du coffre Recovery Services et gérez la réplication. Lorsque vous configurez le coffre de hello, vous spécifiez ce que vous voulez tooreplicate, et où vous souhaitez que tooreplicate à.

Accédez trop[étape 7 : créer un coffre](hyper-v-site-walkthrough-create-vault.md)

## <a name="step-8-configure-source-and-target-settings"></a>Étape 8 : configurer les paramètres de source et de cible

Configurer la source de hello et la cible qui est utilisée pour la réplication. Configuration des paramètres de la source comprend l’ajout d’Hyper-V héberge tooa Hyper-V site, l’installation hello fournisseur Site Recovery et l’agent Recovery Services sur chaque ordinateur hôte Hyper-V et l’enregistrement de site de hello Bonjour de coffre Recovery Services.

Accédez trop[étape 8 : configurer hello source et cible](hyper-v-site-walkthrough-source-target.md)

## <a name="step-9-set-up-a-replication-policy"></a>Étape 9 : configurer une stratégie de réplication

Vous définissez des paramètres de réplication de stratégie toospecify pour les ordinateurs virtuels Hyper-V dans le coffre hello.

Accédez trop[étape 9 : configurer une stratégie de réplication](hyper-v-site-walkthrough-replication.md)


## <a name="step-10-enable-replication"></a>Étape 10 : Activer la réplication

Après avoir configuré une stratégie de réplication en place, après l’activation, la réplication initiale de hello machine virtuelle se produit.

Accédez trop[étape 10 : activer la réplication](hyper-v-site-walkthrough-enable-replication.md)

## <a name="step-11-run-a-test-failover"></a>Étape 11 : Exécuter un test de basculement

Une fois la réplication initiale se termine, et la réplication delta est en cours d’exécution, vous pouvez exécuter un toomake de basculement de test que tout fonctionne comme prévu.

Accédez trop[étape 11 : exécuter un test de basculement](hyper-v-site-walkthrough-test-failover.md)
