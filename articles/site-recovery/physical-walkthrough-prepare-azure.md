---
title: "tooreplicate de ressources Azure aaaPrepare local tooAzure serveurs physiques à l’aide d’Azure Site Recovery | Documents Microsoft"
description: "Décrit ce que vous devez en place dans Azure avant de pouvoir répliquer tooAzure de serveurs locaux, à l’aide du service d’Azure Site Recovery hello"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 4e320d9b-8bb8-46bb-ba21-77c5d16748ac
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/25/2017
ms.author: raynew
ms.openlocfilehash: b1d008dac278bc7797188a3c9c15f2a3b5fe12d7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="step-5-prepare-azure-resources-for-physical-server-replication-tooazure"></a>Étape 5 : Préparer les ressources Azure pour tooAzure de réplication de serveur physique


Utilisez les instructions de hello dans cette tooprepare article Azure ressources afin que vous pouvez répliquer tooAzure de serveurs locaux à l’aide de hello [Azure Site Recovery](site-recovery-overview.md) service.

Ajouter des commentaires et questions bas hello de cet article, ou sur hello [Forum sur Azure Recovery Services](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

## <a name="before-you-start"></a>Avant de commencer

Vérifiez que vous avez lu hello [conditions préalables](physical-walkthrough-prerequisites.md).

## <a name="set-up-an-azure-account"></a>Configurer un compte Azure

- Procurez-vous un [compte Microsoft Azure](http://azure.microsoft.com/).
- Vous pouvez commencer par une version d’ [essai gratuit](https://azure.microsoft.com/pricing/free-trial/).
- Vérifiez les régions hello pris en charge pour la récupération de Site, sous **disponibilité géographique** dans [détails de la tarification de Azure Site Recovery](https://azure.microsoft.com/pricing/details/site-recovery/).
- En savoir plus sur [Site Recovery tarification](site-recovery-faq.md#pricing)et obtenir hello [tarification](https://azure.microsoft.com/pricing/details/site-recovery/).



## <a name="set-up-an-azure-network"></a>Configurer un réseau Azure

- Configurez un réseau Azure Les machines virtuelles Azure sont placées dans ce réseau une fois créées après le basculement.
- Récupération de site Bonjour portail Azure peut utiliser des réseaux définis dans [le Gestionnaire de ressources](../resource-manager-deployment-model.md), ou en mode classique.
- réseau de Hello doivent se trouver dans hello Services de récupération de la même région que hello coffre.
- Prenez connaissance de la [tarification des réseaux virtuels](https://azure.microsoft.com/pricing/details/virtual-network/).
- Découvrez la [connectivité de la machine virtuelle Azure](physical-walkthrough-network.md) après le basculement.


## <a name="set-up-an-azure-storage-account"></a>Configurer un compte de stockage Azure

- Récupération de site réplique un stockage local serveurs tooAzure. Machines virtuelles Azure sont créés à partir du stockage de hello après que le basculement se produit.
- Configurer un [compte de stockage Azure](../storage/common/storage-create-storage-account.md#create-a-storage-account) pour les données répliquées.
- Récupération de site Bonjour portail Azure peut utiliser des comptes de stockage configurés dans le Gestionnaire de ressources, ou en mode classique.
- compte de stockage Hello peut être standard ou [premium](../storage/common/storage-premium-storage.md).
- Si vous configurez un compte premium, vous aurez également besoin d’un compte standard supplémentaire pour les données de journal.


## <a name="next-steps"></a>Étapes suivantes

Accédez trop[étape 6 : configurer un coffre](physical-walkthrough-create-vault.md)
