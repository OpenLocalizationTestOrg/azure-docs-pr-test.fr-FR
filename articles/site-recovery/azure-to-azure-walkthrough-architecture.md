---
title: "architecture de hello aaaReview pour la réplication de machines virtuelles Azure entre les régions Azure | Documents Microsoft"
description: "Cet article fournit une vue d’ensemble des composants et architecture utilisée lors de la réplication des machines virtuelles Azure entre les régions Azure à l’aide du service d’Azure Site Recovery hello."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 07/12/2017
ms.author: raynew
ms.openlocfilehash: 4caab4e7a764040f317201d1345c40c73f836d81
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="step-1-review-hello-architecture-for-azure-vm-replication-between-azure-regions"></a>Étape 1 : Passez en revue l’architecture hello pour la réplication de machine virtuelle Azure entre les régions Azure


Après avoir examiné hello [étapes](azure-to-azure-walkthrough-overview.md) pour ce déploiement, lisez cette composants de l’article toounderstand hello et les processus utilisés lors de la réplication et la récupération des machines virtuelles (VM) à partir d’une région Azure tooanother, à l’aide de [Azure Site Recovery](site-recovery-overview.md).

- Lorsque vous avez terminé l’article de hello, doit avoir une bonne compréhension du fonctionne de la région de tooanother de réplication de machine virtuelle Azure.
- Valider les commentaires en bas de hello de cet article, ou poser des questions dans hello [Forum sur Azure Recovery Services](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

>[!NOTE]
>Réplication de machine virtuelle Azure avec hello service Site Recovery est actuellement en version préliminaire.



## <a name="architectural-components"></a>Composants architecturaux

Hello suivant schéma fournit une vue d’ensemble d’un environnement de machine virtuelle Azure dans une région spécifique (dans cet exemple, hello emplacement de l’est des États-Unis). Dans un environnement de machine virtuelle Azure :
- Les applications peuvent s’exécuter sur des machines équipées de disques réparties sur plusieurs comptes de stockage.
- Hello machines virtuelles peut être inclus dans un ou plusieurs sous-réseaux dans un réseau virtuel.

![environnement client](./media/azure-to-azure-walkthrough-architecture/source-environment.png)

## <a name="replication-process"></a>Processus de réplication

### <a name="step-1"></a>Étape 1

Lorsque vous activez la réplication de machine virtuelle Azure Bonjour portail Azure, hello les ressources affichées Bonjour suivant de schéma et table sont automatiquement créées dans la région cible hello. Par défaut, les ressources sont créées en fonction des paramètres de la région source. Vous pouvez personnaliser les paramètres de cible de hello en fonction des besoins. [En savoir plus](site-recovery-replicate-azure-to-azure.md).

![Activer le processus de réplication, étape 1](./media/azure-to-azure-walkthrough-architecture/enable-replication-step-1.png)

**Ressource** | **Détails**
--- | ---
**Groupe de ressources cible** | Bonjour toowhich de groupe de ressources appartiennent des machines virtuelles répliquées après le basculement.
**Réseau virtuel cible** | Hello du réseau virtuel dans lequel les machines virtuelles répliquées sont situés après le basculement. Un mappage réseau est créé entre les réseaux virtuels source et cible, et inversement.
**Comptes Stockage de cache** | Avant que les modifications sur la source de que machines virtuelles sont répliquées toohello compte de stockage cible, elles sont suivies et envoyés le compte de stockage de cache toohello dans l’emplacement cible de hello. Cela garantit un impact minimal sur les applications de production en cours d’exécution sur la machine virtuelle de hello.
**Comptes de stockage cibles**  | Comptes de stockage de données de hello cibles emplacement toowhich hello est répliquée.
**Groupes à haute disponibilité cibles**  | Groupes à haute disponibilité dans le hello répliquée les machines virtuelles sont situés après le basculement.

### <a name="step-2"></a>Étape 2

Comme la réplication est activée, hello extension service mobilité de la récupération de Site est automatiquement installé sur hello machine virtuelle. suivant de Hello se produit :

1. Hello machine virtuelle est enregistré dans la récupération de Site.

2. La réplication continue est configurée pour hello machine virtuelle. Données écrit sur la machine virtuelle de hello disques sont en permanence transférés du compte de stockage de cache toohello dans l’emplacement source de hello.

   ![Activer le processus de réplication, étape 2](./media/azure-to-azure-walkthrough-architecture/enable-replication-step-2.png)

  
  Notez que Site Recovery n’a jamais besoin entrant connectivité toohello machine virtuelle. Uniquement sortant service de connectivité tooSite récupération les adresses URL/IP, les adresses URL/IP authentification Office 365 et adresses de compte de stockage du cache est nécessaire. 

## <a name="continuous-replication-process"></a>Processus de réplication continue

Une fois que l’utilisation de la réplication continue, disque écritures sont immédiatement transférées compte de stockage de cache toohello. Récupération de site traite les données de hello et l’envoie toohello compte de stockage cible. Une fois le traitement des données de hello, points de récupération sont générées dans le compte de stockage cible hello quelques minutes.

## <a name="failover-process"></a>Processus de basculement

Lorsque vous démarrez un basculement, hello qu'ordinateurs virtuels sont créés dans le groupe de ressources cible hello, réseau virtuel cible, sous-réseau cible et hello ciblent à haute disponibilité. Lors d’un basculement, vous pouvez utiliser n’importe quel point de récupération.

![Processus de basculement](./media/azure-to-azure-walkthrough-architecture/failover.png)

## <a name="next-steps"></a>Étapes suivantes

Accédez trop[étape 2 : vérifier les conditions préalables et restrictions](azure-to-azure-walkthrough-prerequisites.md)
