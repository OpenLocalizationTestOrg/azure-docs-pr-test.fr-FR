---
title: aaaReplicate des ordinateurs virtuels Hyper-V dans VMM nuages tooAzure avec Azure Site Recovery | Documents Microsoft
description: "Fournit une vue d’ensemble pour répliquer des ordinateurs virtuels Hyper-V dans VMM tooAzure de nuages à l’aide du service d’Azure Site Recovery hello"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 8e7d868e-00f3-4e8b-9a9e-f23365abf6ac
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/14/2017
ms.author: raynew
ms.openlocfilehash: d6f729a49cc86ea07bebc4d7266fd7b58b3998f7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-hyper-v-virtual-machines-in-vmm-clouds-tooazure-using-site-recovery-in-hello-azure-portal"></a>Répliquer les machines virtuelles Hyper-V dans VMM tooAzure de nuages à l’aide de la récupération de Site Bonjour portail Azure
> [!div class="op_single_selector"]
> * [Portail Azure](site-recovery-vmm-to-azure.md)
> * [Portail Azure Classic](site-recovery-vmm-to-azure-classic.md)
> * [PowerShell Resource Manager](site-recovery-vmm-to-azure-powershell-resource-manager.md)
> * [PowerShell Classic](site-recovery-deploy-with-powershell.md)


Cet article fournit une vue d’ensemble de tooreplicate requis des étapes de hello local Hyper-V virtual machines virtuelles gérées dans System Center Virtual Machine Manager (VMM) clouds tooAzure, à l’aide de hello [Azure Site Recovery](site-recovery-overview.md) service dans Hello portail Azure.

Après avoir lu cet article, validez les commentaires au bas de hello, ou sur hello [Forum sur Azure Recovery Services](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="step-1-review-hello-scenario-architecture"></a>Étape 1 : Passez en revue l’architecture du scénario de hello

Avant de commencer le déploiement, examen de l’architecture du scénario hello et assurez-vous que vous comprenez tous les composants de hello, vous devez toodeploy.

Accédez trop[étape 1 : examen de l’architecture de hello](vmm-to-azure-walkthrough-architecture.md)

## <a name="step-2-review-prerequisites-and-limitations"></a>Étape 2 : Vérifier les conditions préalables et les limitations

Assurez-vous que vous comprenez les limitations et les conditions préalables au déploiement de hello.

**Conditions préalables Azure** : vous avez besoin d’un compte Microsoft Azure, d’un réseau Azure et de comptes de stockage.
**Serveurs VMM et hôtes Hyper-V locaux** : assurez-vous que les serveurs VMM et les hôtes Hyper-V sont conformes et préparés pour le déploiement Site Recovery.
**Répliquer les machines virtuelles**: Vérifiez que vous voulez tooreplicate de machines virtuelles sont conformes aux exigences d’Azure.

Accédez trop[étape 2 : vérifier les conditions préalables et restrictions](vmm-to-azure-walkthrough-prerequisites.md)

## <a name="step-3-plan-capacity"></a>Étape 3 : planifier la capacité

Si vous effectuez un déploiement complet, vous devez toofigure à quelles ressources de réplication que vous avez besoin. Il existe deux de toohelp disponibles des outils pour cela. Si vous effectuez une rapide configurer tootest hello environnement, vous pouvez ignorer cette étape.

Accédez trop[étape 3 : planifier la capacité](vmm-to-azure-walkthrough-capacity.md)

## <a name="step-4-plan-networking"></a>Étape 4 : Planifier la mise en réseau

Vous devez toodo certains tooensure que vous pouvez configurer le mappage réseau lorsque vous déployez le scénario de hello, de planification d’un réseau que les machines virtuelles Azure sera tooAzure connecté les réseaux virtuels après le basculement se produit et qu’ils sont attribués IP approprié répondant.

Accédez trop[étape 4 : planifier la mise en réseau](vmm-to-azure-walkthrough-network.md)


## <a name="step-5-prepare-azure-resources"></a>Étape 5 : Préparer les ressources Azure

Configurez un compte Azure, des réseaux et du stockage. Vous pouvez le faire pendant le déploiement, mais nous vous recommandons de vous en occuper avant de commencer.

Accédez trop[étape 5 : préparer le Azure](vmm-to-azure-walkthrough-prepare-azure.md)

## <a name="step-6-prepare-vmm-and-hyper-v"></a>Étape 6 : Préparer VMM et Hyper-V

Préparer les serveurs VMM hello local et les hôtes Hyper-V pour le déploiement de la récupération de Site.

Accédez trop[étape 6 : préparer les serveurs locaux](vmm-to-azure-walkthrough-vmm-hyper-v.md)

## <a name="step-7-set-up-a-vault"></a>Étape 7 : configurer un coffre

Configurez un coffre Recovery Services. coffre de Hello contient les paramètres de configuration et orchestre la réplication.

[Étape 7 : Configurer un coffre](vmm-to-azure-walkthrough-create-vault.md)

## <a name="step-8-configure-source-and-target-settings"></a>Étape 8 : configurer les paramètres de source et de cible

Configurez les emplacements de hello source et cible de réplication. Ajouter hello VMM serveur toohello dans l’archivage et télécharger des fichiers d’installation hello pour les composants de Site Recovery. Exécutez le programme d’installation du fournisseur Azure Site Recovery sur le serveur VMM de hello. Le programme d’installation installe hello fournisseur sur le serveur VMM de hello et les enregistre sur le serveur hello dans le coffre de hello. Vous installez hello Microsoft Recovery Services agent sur chaque hôte Hyper-V.

Accédez trop[étape 8 : configurer les paramètres source et cible](vmm-to-azure-walkthrough-source-target.md)

## <a name="step-9-configure-network-mapping"></a>Étape 9 : Configurer le mappage réseau

Mappage des locaux des réseaux virtuels VMM VM réseaux tooAzure. Après le basculement, les machines virtuelles Azure sont créés dans hello réseau Azure mappé toohello réseau d’ordinateurs virtuels en local dans le hello Hyper-V source se trouve.

Accédez trop[étape 9 : configurer le mappage réseau](vmm-to-azure-walkthrough-network-mapping.md)


## <a name="step-10-set-up-a-replication-policy"></a>Étape 10 : Configurer une stratégie de réplication

Spécifiez comment les machines virtuelles de local sera répliquée tooAzure.

Accédez trop[étape 10 : définir une stratégie de réplication](vmm-to-azure-walkthrough-replication.md)


## <a name="step-11-enable-replication-for-vms"></a>Étape 11 : Activer la réplication des machines virtuelles

Sélectionnez hello machines virtuelles tooreplicate. Activation d’une machine virtuelle pour la réplication déclencheurs hello la réplication initiale tooAzure, suivie de la réplication delta en cours.

Accédez trop[étape 11 : activer la réplication](vmm-to-azure-walkthrough-enable-replication.md)


## <a name="step-12-run-a-test-failover"></a>Étape 12 : exécuter un test de basculement

Exécutez un toomake de basculement de test que tout fonctionne comme prévu.

Accédez trop[étape 12 : exécuter un test de basculement](vmm-to-azure-walkthrough-test-failover.md)


