---
title: "conditions préalables de hello aaaReview pour la réplication de tooAzure Hyper-V (sans System Center VMM) à l’aide d’Azure Site Recovery | Documents Microsoft"
description: "Décrit les conditions requises de hello pour configurer la réplication, le basculement et la récupération de tooAzure d’ordinateurs virtuels Hyper-V local avec Azure Site Recovery"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 7ef3fb46-52f5-4c8a-b1a1-658c2305762a
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/21/2017
ms.author: raynew
ms.openlocfilehash: 3eefc3b7e3982ec6c413c1db7f7784863f9c701d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="step-2-review-hello-prerequisites-for-hyper-v-without-vmm-tooazure-replication"></a>Étape 2 : Passez en revue les conditions préalables de hello pour la réplication Hyper-V (sans VMM) tooAzure

conditions préalables de Hello sont résumées dans le tableau de hello.


**Configuration requise** | **Détails** 
--- | --- 
**Microsoft Azure** | Découvrez la [configuration requise pour Azure](site-recovery-prereq.md#azure-requirements).
**Serveurs locaux** | [En savoir plus](site-recovery-prereq.md#disaster-recovery-of-hyper-v-vms-to-azure-no-vmm) sur la configuration requise pour les ordinateurs hôtes Hyper-V de hello localement.
**Machines virtuelles Hyper-V en local** | Machines virtuelles que vous souhaitez tooreplicate doit être en cours d’exécution un [prise en charge du système d’exploitation](site-recovery-support-matrix-to-azure.md#support-for-replicated-machine-os-versions)et être conformes avec [conditions préalables Azure](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).
**URL Azure** | Hôtes Hyper-V doivent accéder aux URL de toothese :<br/><br/> [!INCLUDE [site-recovery-URLS](../../includes/site-recovery-URLS.md)]<br/><br/> Si vous avez des règles de pare-feu basé sur l’adresse IP, assurez-vous qu’ils autorisent un tooAzure de communication.<br/></br> Autoriser hello [plages d’adresses IP Azure Datacenter](https://www.microsoft.com/download/confirmation.aspx?id=41653)et hello port HTTPS (443).<br/></br> Autoriser les plages d’adresses IP pour hello région Azure de votre abonnement et ouest des États-Unis (utilisé pour la gestion d’identité et contrôle d’accès).



## <a name="next-steps"></a>Étapes suivantes

- Si vous effectuez un déploiement complet, passez trop[étape 3 : planifier la capacité](hyper-v-site-walkthrough-capacity.md)
- Si vous effectuez un déploiement de test simple, passez trop[étape 4 : planifier la mise en réseau](hyper-v-site-walkthrough-network.md).
