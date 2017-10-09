---
title: "aaaPrepare System Center VMM pour Hyper-V réplication tooAzure | Documents Microsoft"
description: "Décrit comment serveur de System Center VMM tooprepare pour tooAzure de réplication Hyper-V, à l’aide d’Azure Site Recovery"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: afcd81ae-d192-4013-a0af-3dac45b3c7e9
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 07/23/2017
ms.author: raynew
ms.openlocfilehash: 773b06afaf7d3eea1fe64f050bf3970943cf466a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="step-6-prepare-vmm-servers-and-hyper-v-hosts-for-hyper-v-replication-tooazure"></a>Étape 6 : Préparer les serveurs VMM et des ordinateurs hôtes Hyper-V pour tooAzure de réplication Hyper-V

Après avoir configuré [composants Azure](vmm-to-azure-walkthrough-prepare-azure.md) pour le déploiement de hello, utilisez les instructions de hello dans cet article tooprepare par VMM serveurs locaux et de toointeract des ordinateurs hôtes Hyper-V avec Azure Site Recovery.

Après avoir lu cet article, validez les commentaires en bas de hello ou poser des questions techniques sur hello [Forum sur Azure Recovery Services](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="prepare-vmm-servers"></a>Préparer les serveurs VMM

- Vous devez au moins un serveur VMM qui répondent aux exigences de prise en charge hello pour la réplication de Site Recovery (site-recovery-support-matrix-to-azure.md#support-for-datacenter-management-servers).
- Vérifiez que vous avez préparé serveur VMM de hello pour [le mappage réseau](vmm-to-azure-walkthrough-network.md#network-mapping-for-replication-to-azure).
- Assurez-vous que le serveur VMM hello peut accéder à ces URL

    [!INCLUDE [site-recovery-URLS](../../includes/site-recovery-URLS.md)]
    
- Si vous avez des règles de pare-feu basé sur l’adresse IP, assurez-vous qu’ils autorisent un tooAzure de communication.
- Autoriser hello [plages d’adresses IP Azure Datacenter](https://www.microsoft.com/download/confirmation.aspx?id=41653)et hello port HTTPS (443).
- Autoriser les plages d’adresses IP pour hello région Azure de votre abonnement et ouest des États-Unis (utilisé pour la gestion d’identité et contrôle d’accès).

Pendant le déploiement de la récupération de Site, vous téléchargez hello fournisseur Site Recovery et l’installer sur chaque serveur VMM. serveur VMM de Hello est inscrit dans hello de coffre Recovery Services.




## <a name="next-steps"></a>Étapes suivantes

Accédez trop[étape 7 : créer un coffre](vmm-to-azure-walkthrough-create-vault.md)

