---
title: "tooreplicate de ressources Azure aaaPrepare local tooAzure les ordinateurs virtuels VMware à l’aide d’Azure Site Recovery | Documents Microsoft"
description: "Décrit ce que vous avez besoin en place dans Azure avant de commencer la réplication tooAzure d’ordinateurs virtuels VMware local à l’aide d’Azure Site Recovery"
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
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: ac72fff0593783add789408ecfeb1812d70108b9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="step-5-prepare-azure-resources-for-vmware-replication-tooazure"></a>Étape 5 : Préparer les ressources Azure pour VMWare réplication tooAzure


Utilisez les instructions de hello dans cette tooprepare article Azure ressources afin que vous pouvez répliquer tooAzure d’ordinateurs locaux à l’aide de hello [Azure Site Recovery](site-recovery-overview.md) service.

Ajouter des commentaires et questions bas hello de cet article, ou sur hello [Forum sur Azure Recovery Services](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

## <a name="before-you-start"></a>Avant de commencer

Vérifiez que vous avez lu hello [conditions préalables](vmware-walkthrough-prerequisites.md)

## <a name="set-up-an-azure-account"></a>Configurer un compte Azure

- Procurez-vous un [compte Microsoft Azure](http://azure.microsoft.com/).
- Vous pouvez commencer par une version d’ [essai gratuit](https://azure.microsoft.com/pricing/free-trial/).
- Vérifiez les régions hello pris en charge pour la récupération de Site, sous géographique disponibilité dans [détails de la tarification de Azure Site Recovery](https://azure.microsoft.com/pricing/details/site-recovery/).
- En savoir plus sur [Site Recovery tarification](site-recovery-faq.md#pricing)et obtenir hello [tarification](https://azure.microsoft.com/pricing/details/site-recovery/).



## <a name="set-up-an-azure-network"></a>Configurer un réseau Azure

- Configurez un réseau Azure Les machines virtuelles Azure sont placées dans ce réseau une fois créées après le basculement.
- Récupération de site Bonjour portail Azure peut utiliser des réseaux définis dans [le Gestionnaire de ressources](../resource-manager-deployment-model.md), ou en mode classique.
- réseau de Hello doivent se trouver dans hello Services de récupération de la même région que hello coffre
- Prenez connaissance de la [tarification des réseaux virtuels](https://azure.microsoft.com/pricing/details/virtual-network/).
- Découvrez la [connectivité de la machine virtuelle Azure](site-recovery-network-design.md) après le basculement.


## <a name="set-up-an-azure-storage-account"></a>Configurer un compte de stockage Azure

- Récupération de site réplique le stockage de tooAzure d’ordinateurs locaux. Machines virtuelles Azure sont créés à partir du stockage de hello après que le basculement se produit.
- Configurer un [compte de stockage Azure](../storage/common/storage-create-storage-account.md#create-a-storage-account) pour les données répliquées.
- Récupération de site Bonjour portail Azure peut utiliser des comptes de stockage configurés dans le Gestionnaire de ressources, ou en mode classique.
- compte de stockage Hello peut être standard ou [premium](../storage/common/storage-premium-storage.md).
- Si vous configurez un compte premium, vous aurez également besoin d’un compte standard supplémentaire pour les données de journal.


## <a name="next-steps"></a>Étapes suivantes

Accédez trop[étape 6 : VMware de préparer les ressources](vmware-walkthrough-prepare-vmware.md)
