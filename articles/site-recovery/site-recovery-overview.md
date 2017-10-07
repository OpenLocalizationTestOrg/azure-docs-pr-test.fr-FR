---
title: "Azure Site Recovery n’est aaaWhat ? | Microsoft Docs"
description: "Fournit une vue d’ensemble de hello service Azure Site Recovery et résume les scénarios de déploiement."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: cfreeman
editor: 
ms.assetid: e9b97b00-0c92-4970-ae92-5166a4d43b68
ms.service: site-recovery
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/25/2017
ms.author: raynew
ms.openlocfilehash: da6755654b8036a03314ec836f014b64428d5518
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-site-recovery"></a>Qu’est-ce que Site Recovery ?

Bienvenue dans le service d’Azure Site Recovery toohello ! Cet article fournit une vue d’ensemble rapide du service de hello.

## <a name="business-continuity-and-disaster-recovery-bcdr-with-azure-recovery-services"></a>Continuité des activités et récupération d’urgence (BDCR) avec Azure Recovery Services

En tant qu’organisation, vous devez toofigure out comment vous allez tookeep sécurité de vos données et applications/les charges de travail en cours d’exécution lors de la planification et les interruptions non planifiées se produisent.

Services de récupération Azure contribuent stratégie BCDR tooyour :

- **Service Site Recovery** : ce service aide à assurer une continuité des activités en maintenant les applications en cours d’exécution sur des machines virtuelles et des serveurs physiques disponibles, en cas de panne du site. Récupération de site réplique des charges de travail en cours d’exécution sur des machines virtuelles et des serveurs physiques afin qu’ils restent disponibles dans un emplacement secondaire si le site principal de hello n’est pas disponible. Il récupère le site principal de charges de travail toohello quand il fonctionne et exécutez de nouveau.
- **Service de sauvegarde**: hello en outre, [Azure Backup](https://docs.microsoft.com/azure/backup/) service conserve vos données de par sa sauvegarde tooAzure.

Site Recovery peut gérer la réplication pour :

- Les machines virtuelles Azure qui répliquent des données entre des régions Azure.
- Local réplication tooAzure ou site secondaire de tooa de serveurs physiques et virtuels.


## <a name="what-does-site-recovery-provide"></a>À quoi sert Site Recovery ?

**Fonctionnalité** | **Détails**
--- | ---
**Déployer une solution BCDR simple** | À l’aide de la récupération de Site, vous pouvez configurer et gérer la réplication, le basculement et la restauration à partir d’un emplacement unique dans hello portail Azure.
**Répliquer des machines virtuelles Azure** | Vous pouvez configurer votre stratégie BCDR afin que les machines virtuelles Azure soient répliquées entre les régions Azure.
**Répliquer hors site des machines virtuelles locales** | Vous pouvez répliquer local machines virtuelles et tooAzure des serveurs physiques ou emplacement de site secondaire tooa. Réplication tooAzure élimine hello coût et la complexité de la gestion d’un centre de données secondaire.
**Répliquer n’importe quelle charge de travail** | Répliquez n’importe quelle charge de travail en cours d’exécution sur des machines virtuelles Azure, des machines virtuelles Hyper-V locales, des machines virtuelles VMware et des serveurs physiques Windows/Linux pris en charge.
**Maintenir les données durables et sécurisées** | Site Recovery orchestre la réplication sans intercepter les données d’une application. Données répliquées sont stockées dans le stockage Azure, avec une résilience de hello fournit. En cas de basculement, les machines virtuelles Azure sont créés en fonction des données de hello répliquée.
**Respecter les RTO et les RPO** | Maintenez les objectifs de délai de récupération (RTO) et les objectifs de point de récupération (RPO) au sein des limites fixées par l’organisation. Site Recovery fournit une réplication continue pour les machines virtuelles Azure et VMware. Les machines virtuelles Hyper-V bénéficient d’une fréquence de réplication de 30 secondes seulement. Vous pouvez réduire davantage les RTO en les ajoutant à l’intégration [Azure Traffic Manager](https://azure.microsoft.com/blog/reduce-rto-by-using-azure-traffic-manager-with-azure-site-recovery/).
**Maintenir la cohérence des applications en cas de basculement** | Vous pouvez configurer des points de récupération avec des captures instantanées cohérentes au niveau des applications. Ces captures récupèrent les données des disques, l’ensemble des données en mémoire et toutes les transactions en cours de traitement.
**Réaliser des tests sans interruption** | Vous pouvez facilement exécuter des basculements de test toosupport exercices de récupération d’urgence, sans affecter la réplication en cours.
**Exécuter des basculements flexibles** | Vous pouvez exécuter des basculements planifiés pour les interruptions attendues, sans perte de données, ou des basculements non planifiés avec une perte de données minimale (en fonction de la fréquence de réplication) pour les incidents inattendus. Vous pouvez facilement échouer tooyour arrière principal de site lorsqu’il est disponible.
**Créer des plans de récupération** | Vous pouvez personnaliser et séquencer le basculement et la récupération d’applications multiniveau sur plusieurs machines virtuelles avec des plans de récupération. Vous regroupez des machines dans des plans et ajoutez des scripts ainsi que des actions manuelles. Les plans de récupération peuvent être intégrés à des runbooks Azure Automation.
**Intégration aux technologies BCDR existantes** | Site Recovery s’intègre à d’autres technologies BCDR. Par exemple, vous pouvez utiliser la récupération de Site tooprotect hello SQL Server principal des charges de travail d’entreprise, y compris la prise en charge native de SQL Server AlwaysOn, basculement de hello toomanage des groupes de disponibilité.
**Intégrer la bibliothèque d’automation hello** | La bibliothèque Azure Automation diversifiée fournit des scripts spécifiques à l’application prêts pour la production, qui peuvent être téléchargés et intégrés au service Site Recovery.
**Gérer les paramètres réseau** | Site Recovery s’intègre à Azure pour permettre une gestion simple du réseau d’application, y compris la réservation d’adresses IP, la configuration des équilibrages de charges et l’intégration d’Azure Traffic Manager pour des commutations réseau efficaces.


## <a name="what-can-i-replicate"></a>Que puis-je répliquer ?

**Pris en charge** | **Détails**
--- | ---
**Que puis-je répliquer ?** | Machines virtuelles Azure entre régions Azure (préversion)<br/><br/>  Les ordinateurs virtuels VMware, des ordinateurs virtuels Hyper-V, des serveurs physiques (Windows et Linux) tooAzure local < br /<br/> Les ordinateurs virtuels VMware, des ordinateurs virtuels Hyper-V, site secondaire de serveurs physiques tooa sur site. Pour les ordinateurs virtuels Hyper-V, site secondaire de réplication tooa est uniquement pris en charge si les ordinateurs hôtes Hyper-V sont gérés par System Center VMM.
**Quelles sont les régions prises en charge pour Site Recovery ?** | [Régions prises en charge](https://azure.microsoft.com/regions/services/) |
**De quels systèmes d’exploitation ont besoin les machines répliquées ?** | [Exigences des machines virtuelles Azure](site-recovery-support-matrix-azure-to-azure.md#support-for-replicated-machine-os-versions)<br></br>[Exigences des machines virtuelles VMware](site-recovery-support-matrix-to-azure.md#support-for-replicated-machine-os-versions)<br/><br/> Pour les machines virtuelles Hyper-V, tous les [SE invités](https://technet.microsoft.com/windows-server-docs/compute/hyper-v/supported-windows-guest-operating-systems-for-hyper-v-on-windows) pris en charge par Azure et Hyper-V sont pris en charge.<br/><br/> [Exigences des serveurs physiques](site-recovery-support-matrix-to-azure.md#support-for-replicated-machine-os-versions)
**De quels serveurs/hôtes VMware ai-je besoin ?** | Les machines virtuelles VMware peuvent se trouver sur des [hôtes vSphere/serveurs vCenter](site-recovery-support-matrix-to-azure.md#support-for-datacenter-management-servers)
**Quelles charges de travail puis-je répliquer ?** | Vous pouvez répliquer toutes les charges de travail qui s’exécutent sur une machine de réplication prise en charge. En outre, équipe de récupération de Site hello effectuées spécifique à l’application de test pour un [nombre d’applications](site-recovery-workload.md#workload-summary).


## <a name="azure-portal-considerations"></a>Considérations relatives au portail Azure

* Récupération de site peut être déployée dans hello [portail Azure](https://portal.azure.com).
* Bonjour portail Azure classic, vous pouvez gérer le Site Recovery avec le modèle de gestion des services classique hello.
- portail classique de Hello doit uniquement avoir des déploiements de récupération de Site existants toomaintain utilisé. Impossible de créer des coffres dans le portail classique de hello.

## <a name="next-steps"></a>Étapes suivantes
* En savoir plus sur la [prise en charge de la charge de travail](site-recovery-workload.md)
* Prise en main [la réplication entre les régions Azure VM](site-recovery-azure-to-azure.md), [VMware réplication tooAzure](vmware-walkthrough-overview.md), ou [tooAzure de réplication Hyper-V](hyper-v-site-walkthrough-overview.md).
