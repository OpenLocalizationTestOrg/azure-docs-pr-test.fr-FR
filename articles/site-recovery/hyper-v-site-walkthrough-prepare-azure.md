---
title: "aaaPrepare ressources Azure tooreplicate machines virtuelles de Hyper-V (sans System Center VMM) tooAzure à l’aide d’Azure Site Recovery | Documents Microsoft"
description: "Décrit ce que vous avez besoin en place dans Azure avant de commencer la réplication tooAzure des ordinateurs virtuels Hyper-V (sans VMM) à l’aide d’Azure Site Recovery"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 28fa722c-675e-4637-98eb-7ccbf3806d69
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/21/2017
ms.author: raynew
ms.openlocfilehash: f659e300c39253b0eaf7218bee9d39b11682edb1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="step-5-prepare-azure-resources-for-hyper-v-replication-tooazure"></a>Étape 5 : Préparer les ressources Azure pour tooAzure de réplication Hyper-V

Utilisez les instructions hello dans cette tooprepare article Azure ressources afin que vous pouvez répliquer local machines virtuelles de Hyper-V (sans System Center VMM) tooAzure à l’aide de hello [Azure Site Recovery](site-recovery-overview.md) service.

Après avoir lu cet article, validez les commentaires en bas de hello ou poser des questions techniques sur hello [Forum sur Azure Recovery Services](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

## <a name="before-you-start"></a>Avant de commencer

Vérifiez que vous avez lu hello [conditions préalables](hyper-v-site-walkthrough-prerequisites.md)

## <a name="set-up-an-azure-account"></a>Configurer un compte Azure

- Procurez-vous un [compte Microsoft Azure](http://azure.microsoft.com/).
- Vous pouvez commencer par une version d’ [essai gratuit](https://azure.microsoft.com/pricing/free-trial/).
- Vérifiez les régions hello pris en charge pour la récupération de Site, sous géographique disponibilité dans [détails de la tarification de Azure Site Recovery](https://azure.microsoft.com/pricing/details/site-recovery/).
- En savoir plus sur [Site Recovery tarification](site-recovery-faq.md#pricing)et obtenir hello [tarification](https://azure.microsoft.com/pricing/details/site-recovery/).


## <a name="set-up-an-azure-network"></a>Configurer un réseau Azure

- Configurez un réseau Azure Les machines virtuelles Azure sont placées dans ce réseau une fois créées après le basculement.
- réseau de Hello doivent se trouver dans hello Services de récupération de la même région que hello coffre
- Récupération de site Bonjour portail Azure peut utiliser des réseaux définis dans [le Gestionnaire de ressources](../resource-manager-deployment-model.md), ou en mode classique.
- Nous vous recommandons de configurer un réseau avant de commencer. Si vous ne le faites pas, vous devez toodo il durant le déploiement de la récupération de Site.
- Prenez connaissance de la [tarification des réseaux virtuels](https://azure.microsoft.com/pricing/details/virtual-network/).


## <a name="set-up-an-azure-storage-account"></a>Configurer un compte de stockage Azure

- Récupération de site réplique le stockage de tooAzure d’ordinateurs locaux. Machines virtuelles Azure sont créés à partir du stockage de hello après que le basculement se produit.
- Configurer un standard/premium [compte de stockage Azure](../storage/common/storage-create-storage-account.md#create-a-storage-account) toohold répliquées tooAzure.
- [Stockage Premium](../storage/common/storage-premium-storage.md) est généralement utilisé pour les ordinateurs virtuels qui nécessitent un manière cohérente hautes performances d’e/s et à faible latence toohost e/s intensives les charges de travail.
- Si vous voulez toouse un toostore de compte premium des données répliquées, vous devez également un journaux de réplication de compte de stockage standard toostore que capture en cours devient tooon locale, les données.
- Selon le modèle de ressource hello souhaitées toouse de basculement des machines virtuelles Azure, vous devez définir un compte dans [mode Resource Manager](../storage/common/storage-create-storage-account.md), ou [en mode classique](../storage/common/storage-create-storage-account.md).
- Nous vous recommandons de configurer un compte de stockage avant de commencer. Si vous ne vous devez toodo il durant le déploiement de la récupération de Site. Hello doivent être dans hello Services de récupération de la même région que hello coffre.
- Vous ne pouvez pas déplacer des comptes de stockage utilisé par la récupération de Site entre les groupes de ressources de hello même abonnement, ou entre différents abonnements.


## <a name="next-steps"></a>Étapes suivantes

Accédez trop[étape 6 : ressources Hyper-V préparer](hyper-v-site-walkthrough-prepare-hyper-v.md)
