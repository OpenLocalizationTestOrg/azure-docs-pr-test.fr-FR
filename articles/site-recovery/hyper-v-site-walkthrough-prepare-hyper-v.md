---
title: "aaaPrepare Hyper-V héberge (sans System Center VMM) pour la réplication tooAzure | Documents Microsoft"
description: "Décrit comment tooprepare Hyper-V héberge pour tooAzure de réplication à l’aide d’Azure Site Recovery"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 0f204e24-8d78-4076-95c5-8137d1be9c01
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/22/2017
ms.author: raynew
ms.openlocfilehash: 714b229d5efbd66a9844bd09e36ac3f69919a6bb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="step-6-prepare-hyper-v-hosts-for-replication-tooazure"></a>Étape 6 : Préparer les ordinateurs hôtes Hyper-V pour la réplication tooAzure

Suivez les instructions dans cette tooprepare article hello local toointeract d’ordinateurs hôtes Hyper-V avec Azure Site Recovery.

Après avoir lu cet article, validez les commentaires en bas de hello ou poser des questions techniques sur hello [Forum sur Azure Recovery Services](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="prepare-hosts"></a>Préparer des ordinateurs hôtes

- Assurez-vous que les hôtes Hyper-V de hello respectent hello [conditions préalables](site-recovery-prereq.md#disaster-recovery-of-hyper-v-vms-to-azure-no-vmm).
- Assurez-vous que les hôtes de hello peuvent accéder à des URL de hello requis :

    [!INCLUDE [site-recovery-URLS](../../includes/site-recovery-URLS.md)]
    
- Si vous avez des règles de pare-feu basé sur l’adresse IP, assurez-vous qu’ils autorisent un tooAzure de communication.
- Autoriser hello [plages d’adresses IP Azure Datacenter](https://www.microsoft.com/download/confirmation.aspx?id=41653)et hello port HTTPS (443).
- Autoriser les plages d’adresses IP pour hello région Azure de votre abonnement et ouest des États-Unis (utilisé pour la gestion d’identité et contrôle d’accès).

Pendant le déploiement de la récupération de Site, vous ajoutez les hôtes Hyper-V qui contiennent des machines virtuelles que vous souhaitez tooreplicate tooa Hyper-V site. Bonjour fournisseur Site Recovery et l’agent Recovery Services sont installés sur chaque ordinateur hôte. site de Hello Hyper-V est enregistré dans hello de coffre Recovery Services.

## <a name="next-steps"></a>Étapes suivantes

Accédez trop[étape 7 : créer un coffre](hyper-v-site-walkthrough-create-vault.md)

