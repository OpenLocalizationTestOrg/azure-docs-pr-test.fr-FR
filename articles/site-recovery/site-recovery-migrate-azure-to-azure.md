---
title: "machines virtuelles Azure IaaS d’aaaMigrate entre les régions Azure | Documents Microsoft"
description: "Utilisez Azure IaaS Azure Site Recovery toomigrate virtuels à partir d’une région Azure tooanother."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: jwhit
editor: tysonn
ms.assetid: 8a29e0d9-0010-4739-972f-02b8bdf360f6
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/14/2017
ms.author: raynew
ms.openlocfilehash: c84dc77716b8d19969eab60707ed1332ca39b893
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-azure-iaas-virtual-machines-between-azure-regions-with-azure-site-recovery"></a>Migrer des machines virtuelles IaaS Azure entre différentes régions Azure avec Azure Site Recovery
## <a name="overview"></a>Vue d'ensemble
Récupération de Site de tooAzure Bienvenue ! Utilisez cet article si vous souhaitez que les machines virtuelles Azure de toomigrate entre les régions Azure. Avant de commencer, notez les points suivants :

* Azure dispose de deux modèles de déploiement différents pour créer et utiliser des ressources : Azure Resource Manager et classique. Azure a également deux portails : hello portail classique Azure qui prend en charge le modèle de déploiement classique hello et hello portail Azure avec prise en charge pour les deux modèles de déploiement. les étapes de base Hello pour la migration sont hello même si vous configurez la récupération de Site dans le Gestionnaire de ressources ou standard. Hello toutefois les instructions de l’interface utilisateur et des captures d’écran dans cet article sont pertinentes pour hello portail Azure.
* **Actuellement vous pouvez uniquement migrer d’une région tooanother. Vous pouvez basculer des machines virtuelles à partir d’une région Azure tooanother, mais vous ne pouvez pas restaurer les à nouveau.**

Valider des commentaires ou des questions au bas de hello de cet article, ou sur hello [Forum sur Azure Recovery Services](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

## <a name="prerequisites"></a>Composants requis
Voici ce dont vous avez besoin pour ce déploiement :

* **Machines virtuelles IaaS**: hello des machines virtuelles que vous souhaitez toomigrate. Vous migrez ces machines virtuelles en les traitant comme des machines physiques.

## <a name="deployment-steps"></a>Étapes du déploiement
Cette section décrit les étapes de déploiement hello dans le nouveau portail de Azure hello.

1. [Créer un coffre](site-recovery-vmware-to-azure.md).
2. [Activer la réplication](site-recovery-vmware-to-azure.md). Activer la réplication pour hello machines virtuelles, vous souhaitez toomigrate, choisissez Azure en tant que source. 
3. [ Exécuter un basculement non planifié](site-recovery-failover.md). Une fois la réplication initiale terminée, vous pouvez exécuter un basculement non planifié à partir d’une région Azure tooanother. Si vous le souhaitez, vous pouvez créer un plan de récupération et exécuter un basculement non planifié, toomigrate plusieurs ordinateurs virtuels entre les régions. [Découvrez d’autres informations](site-recovery-create-recovery-plans.md) sur les plans de récupération.

## <a name="next-steps"></a>Étapes suivantes
Découvrez les autres scénarios de réplication dans [Qu’est-ce que le service Azure Site Recovery ?](site-recovery-overview.md)
