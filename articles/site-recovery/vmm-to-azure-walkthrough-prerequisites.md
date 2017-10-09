---
title: "conditions préalables de hello aaaReview pour Hyper-V tooAzure la réplication (avec System Center VMM) à l’aide d’Azure Site Recovery | Documents Microsoft"
description: "Décrit les conditions requises de hello pour configurer la réplication, le basculement et récupération d’ordinateurs virtuels Hyper-V de localement dans tooAzure de clouds VMM, avec Azure Site Recovery"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: a1c30fd5-c979-473c-af44-4f725ad3e3ba
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/24/2017
ms.author: raynew
ms.openlocfilehash: de13a2d80b1a9a5d968a180d559f661ab11e70c7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="step-2-review-hello-prerequisites-for-hyper-v-with-vmm-tooazure-replication"></a>Étape 2 : Passez en revue les conditions préalables de hello pour la réplication Hyper-V (avec VMM) tooAzure

Une fois que vous avez consulté hello [architecture du scénario](vmm-to-azure-walkthrough-architecture.md), lisez cet article de toomake vous devez bien comprendre les conditions préalables au déploiement de hello. 

## <a name="prerequisites-and-limitations"></a>Conditions préalables et limitations

**Prérequis** | **Détails**
--- | ---
**Compte Azure** | Vous avez besoin d’un [compte Microsoft Azure](http://azure.microsoft.com/).
**Stockage Azure** | Vous avez besoin d’un stockage Azure compte toostore répliquée de données.<br/><br/> compte de stockage Hello doit être Bonjour Azure Recovery Services de la même région que hello coffre.<br/><br/>Vous pouvez utiliser le [stockage géoredondant](../storage/common/storage-redundancy.md#geo-redundant-storage) ou le stockage localement redondant. Nous vous recommandons d’utiliser le stockage géo-redondant. Avec un stockage géo-redondant, les données sont résilientes si une panne régionale se produit, ou si la région primaire hello ne peut pas être récupérée.<br/><br/> Vous pouvez utiliser un compte de stockage Azure standard ou Azure [Premium](../storage/common/storage-premium-storage.md). Le stockage Premium peut héberger des charges de travail nécessitant beaucoup d’E/S et est généralement utilisé pour les machines virtuelles nécessitant des performances d’E/S élevées et une faible latence. Si vous utilisez un stockage Premium pour les données répliquées, il vous faut également un compte de stockage standard. Un compte de stockage standard stocke les journaux de réplication qui capturent des données de site tooon les changements en cours.
**Réseau Azure** | Vous avez besoin une [réseau Azure](../virtual-network/virtual-network-get-started-vnet-subnet.md), toowhich machines virtuelles Azure se connecter après le basculement. réseau Azure Hello doit être Bonjour Services de récupération de la même région que hello coffre.
**Serveurs VMM locaux** | Vous avez besoin d’un ou plusieurs serveurs VMM exécutant System Center 2012 R2 ou une version ultérieure.<br/><br/> Chaque serveur VMM doit disposer d’un ou de plusieurs clouds privés. Chaque cloud nécessite un ou la plupart des groupes hôte.<br/><br/> serveur VMM de Hello nécessite un accès internet.
**Hyper-V local** | Serveurs de l’hôte Hyper-V doivent exécuter au moins Windows Server 2012 R2 avec le rôle hello Hyper-V activé ou Microsoft Hyper-V Server 2012 R2. dernières mises à jour de Hello doivent être installés.<br/><br/> hôte Hyper-V de Hello doit se trouver dans un groupe d’hôtes VMM (situé dans un cloud VMM).<br/><br/> Un hôte doit avoir une ou plusieurs machines virtuelles que tooreplicated.<br/><br/> Ordinateurs hôtes Hyper-V doivent être connecté toohello internet pour la réplication tooAzure, directement ou avec un proxy. Serveurs Hyper-V doivent avoir des correctifs hello décrites dans l’article [2961977](https://support.microsoft.com/kb/2961977).
**Machines virtuelles Hyper-V en local** | Machines virtuelles que vous souhaitez tooreplicate doit être en cours d’exécution un [prise en charge du système d’exploitation](site-recovery-support-matrix-to-azure.md#support-for-replicated-machine-os-versions)et être conformes avec [conditions préalables Azure](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements). nom d’ordinateur virtuel Hello peut être modifié une fois la réplication est activée. 




## <a name="next-steps"></a>Étapes suivantes

Accédez trop[étape 3 : planifier la capacité](vmm-to-azure-walkthrough-capacity.md)
