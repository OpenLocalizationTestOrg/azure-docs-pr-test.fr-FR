---
title: "aaaHow est la réplication entre le travail de régions Azure dans Azure Site Recovery machine virtuelle Azure ?  | Microsoft Docs"
description: "Cet article fournit une vue d’ensemble des composants et architecture utilisée lors de la réplication des machines virtuelles Azure entre des régions Azure à l’aide du service d’Azure Site Recovery hello."
services: site-recovery
documentationcenter: 
author: sujayt
manager: rochakm
editor: 
ms.assetid: 
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 05/29/2017
ms.author: sujayt
ms.openlocfilehash: 01eda83e490821f8afc8a2973c18a19453a2e84a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-does-azure-vm-replication-work-in-site-recovery"></a>Comment la réplication de machine virtuelle Azure fonctionne-t-elle dans Site Recovery ?


Cet article décrit les composants hello et les processus impliqués dans la réplication et la récupération des machines virtuelles (VM) à partir d’une région tooanother à l’aide de hello [Azure Site Recovery](site-recovery-overview.md) service.

>[!NOTE]
>Réplication de machine virtuelle Azure avec hello service Site Recovery est actuellement en version préliminaire.

Valider les commentaires en bas de hello de cet article, ou poser des questions dans hello [Forum sur Azure Recovery Services](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

## <a name="architectural-components"></a>Composants architecturaux

Hello suivant schéma fournit une vue d’ensemble d’un environnement de machine virtuelle Azure dans une région spécifique (dans cet exemple, hello emplacement de l’est des États-Unis). Dans un environnement de machine virtuelle Azure :
- Les applications peuvent s’exécuter sur des machines équipées de disques réparties sur plusieurs comptes de stockage.
- Hello machines virtuelles peut être inclus dans un ou plusieurs sous-réseaux dans un réseau virtuel.

![environnement client](./media/site-recovery-azure-to-azure-architecture/source-environment.png)

En savoir plus sur les conditions préalables au déploiement de hello et les besoins en hello [matrice de prise en charge](site-recovery-support-matrix-azure-to-azure.md).

## <a name="replication-process"></a>Processus de réplication

### <a name="step-1"></a>Étape 1

Lorsque vous activez la réplication de machine virtuelle Azure Bonjour portail Azure, hello les ressources affichées Bonjour suivant de schéma et table sont automatiquement créées dans la région cible hello. Par défaut, les ressources sont créées en fonction des paramètres de la région source. Vous pouvez personnaliser les paramètres de cible de hello en fonction des besoins. [En savoir plus](site-recovery-replicate-azure-to-azure.md).

![Activer le processus de réplication, étape 1](./media/site-recovery-azure-to-azure-architecture/enable-replication-step-1.png)

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

   ![Activer le processus de réplication, étape 2](./media/site-recovery-azure-to-azure-architecture/enable-replication-step-2.png)

   >[!IMPORTANT]
   > Récupération de site n’a jamais besoin connectivité entrante toohello machine virtuelle. Hello machine virtuelle doit uniquement connectivité sortante tooSite récupération service URL/adresses IP Office 365 authentification URL/adresses IP et adresses de compte de stockage du cache. Pour plus d’informations, consultez hello [des conseils de mise en réseau pour la réplication des machines virtuelles](site-recovery-azure-to-azure-networking-guidance.md) l’article.

## <a name="continuous-replication-process"></a>Processus de réplication continue

Une fois que l’utilisation de la réplication continue, disque écritures sont immédiatement transférées compte de stockage de cache toohello. Récupération de site traite les données de hello et l’envoie toohello compte de stockage cible. Une fois le traitement des données de hello, points de récupération sont générées dans le compte de stockage cible hello quelques minutes.

## <a name="failover-process"></a>Processus de basculement

Lorsque vous démarrez un basculement, hello qu'ordinateurs virtuels sont créés dans le groupe de ressources cible hello, réseau virtuel cible, sous-réseau cible et hello ciblent à haute disponibilité. Lors d’un basculement, vous pouvez utiliser n’importe quel point de récupération.

![Processus de basculement](./media/site-recovery-azure-to-azure-architecture/failover.png)

## <a name="next-steps"></a>Étapes suivantes

- En savoir plus sur la [mise en réseau](site-recovery-azure-to-azure-networking-guidance.md) pour la réplication de machine virtuelle Azure.
- Suivez une procédure pas à pas trop[répliquer les machines virtuelles Azure.](site-recovery-azure-to-azure.md)
