---
title: tooAzure aaaMigrate avec Site Recovery | Documents Microsoft
description: "Cet article fournit une vue d’ensemble de la migration de machines virtuelles et tooAzure des serveurs physiques avec Azure Site Recovery"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: jwhit
editor: 
ms.assetid: c413efcd-d750-4b22-b34b-15bcaa03934a
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 04/05/2017
ms.author: raynew
ms.openlocfilehash: 6e65deee337c5371d441812ddb820dc8bc233684
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-tooazure-with-site-recovery"></a>Migrer tooAzure avec Site Recovery

Lisez cet article pour une vue d’ensemble de l’utilisation de service d’Azure Site Recovery hello pour la migration des ordinateurs virtuels et des serveurs physiques.

Récupération de site est un service Azure qui contribue de stratégie de BCDR tooyour en orchestrant ces opérations de réplication des serveurs physiques locaux et de machines virtuelles toohello cloud (Azure) ou tooa de centre de données secondaire. En cas de pannes dans votre emplacement principal, vous basculez toohello emplacement secondaire tookeep applications et charges de travail disponibles. Vous ne parvenez pas emplacement principal d’arrière tooyour lorsqu’elle retourne les opérations de toonormal. Pour en savoir plus, consultez [Qu’est-ce que Site Recovery ?](site-recovery-overview.md) Vous pouvez également utiliser la récupération de Site toomigrate votre locales existantes tooexpedite tooAzure de charges de travail votre voyage du cloud et un dispo hello tableau des fonctionnalités Azure.

Pour une vue d’ensemble rapide de la migration de tooperform, reportez-vous toothis vidéo.
>[!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/ASRHowTo-Video2-Migrate-Virtual-Machines-to-Azure/player]

Cet article décrit le déploiement Bonjour [portail Azure](https://portal.azure.com). Hello [portail Azure classic](https://manage.windowsazure.com/) peut être utilisé toomaintain existant coffres de récupération de Site, mais vous ne pouvez pas créer des coffres.

Valider les commentaires en bas de hello de cet article. Poser des questions techniques sur hello [Forum sur Azure Recovery Services](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="what-do-we-mean-by-migration"></a>Quelle est notre définition de la migration ?

Vous pouvez déployer la récupération de Site pour la réplication des machines virtuelles de local et des serveurs physiques, tooAzure ou tooa site secondaire. Vous répliquez des machines, basculer les à partir du site principal de hello lors de pannes se produisent et échouent toohello arrière principal de site lorsqu’il récupère. Dans toothis de plus, vous pouvez utiliser des machines virtuelles toomigrate de récupération de Site et serveurs physiques tooAzure, afin que les utilisateurs puissent y accéder en tant que machines virtuelles Azure. Migration implique la réplication et le basculement de tooAzure du site principal hello et un mouvement d’effectuer la migration.

## <a name="what-can-site-recovery-migrate"></a>Que peut migrer Site Recovery ?

Vous pouvez :

- Migrer les charges de travail en cours d’exécution sur toorun de serveurs physiques, ordinateurs virtuels Hyper-V et les ordinateurs virtuels VMware localement sur des machines virtuelles Azure. Vous pouvez également effectuer une réplication complète et une restauration automatique dans ce scénario.
- Migrer des [machines virtuelles IaaS Azure](site-recovery-migrate-azure-to-azure.md) entre des régions Azure. Actuellement, seule la migration est prise en charge dans ce scénario, pas la restauration automatique.
- Migrer [instances AWS Windows](site-recovery-migrate-aws-to-azure.md) tooAzure machines virtuelles IaaS. Actuellement, seule la migration est prise en charge dans ce scénario, pas la restauration automatique.

## <a name="migrate-on-premises-vms-and-physical-servers"></a>Migrer des machines virtuelles et des serveurs physiques locaux

toomigrate locaux des ordinateurs virtuels Hyper-V, les ordinateurs virtuels VMware et des serveurs physiques, vous suivez hello presque les mêmes étapes que celles utilisées pour la réplication normale.

1. Configurez un coffre Recovery Services.
2. Configurer les serveurs d’administration hello requis (VMware, VMM, Hyper-V - selon ce que vous souhaitez toomigrate), ajoutez-les toohello coffre et spécifier les paramètres de réplication.
3. Activer la réplication pour hello ordinateurs que vous voulez toomigrate
4. Après la migration initiale de hello, exécutez un tooensure de basculement de test rapide que tout fonctionne comme il le devrait.
5. Après avoir vérifié que votre environnement de réplication fonctionne, vous utilisez un basculement planifié ou non en fonction de [ce qui est pris en charge](site-recovery-failover.md) pour votre scénario. Nous vous recommandons d’utiliser un basculement planifié dans la mesure du possible.
6. Pour la migration, vous ne devez toocommit un basculement, ou la supprimer. Au lieu de cela, vous sélectionnez hello **effectuer la Migration** option pour chaque ordinateur, vous souhaitez toomigrate.
     - Dans **répliquées des éléments**, avec le bouton droit hello machine virtuelle, puis cliquez sur **effectuer la Migration**. Cliquez sur **OK** toocomplete. Vous pouvez suivre la progression dans les propriétés de machine virtuelle hello, dans en surveillant le travail de Migration complète hello dans **les tâches de récupération de Site**.
     - Hello **effectuer la Migration** action pour exécuter des processus de migration hello, supprime la réplication pour l’ordinateur de hello et arrête la facturation de récupération de Site pour l’ordinateur de hello.

![completemigration](./media/site-recovery-hyper-v-site-to-azure/migrate.png)

## <a name="migrate-between-azure-regions"></a>Migrer entre des régions Azure

Vous pouvez migrer des machines virtuelles Azure entre des régions à l’aide de Site Recovery. Dans ce scénario, seule la migration est prise en charge. En d’autres termes, vous pouvez répliquer des machines virtuelles de Azure hello et basculer tooanother région, mais vous ne pouvez pas restaurer. Dans ce scénario, que vous configurez un coffre Recovery Services, déployer une réplication de toomanage de serveur de configuration local, ajoutez-le toohello coffre et spécifiez les paramètres de réplication. Vous activez la réplication pour les machines hello souhaité toomigrate et exécuter une rapide test de basculement. Ensuite, vous exécutez un basculement non planifié avec hello **effectuer la Migration** option.

## <a name="migrate-aws-tooazure"></a>Migrer AWS tooAzure

Vous pouvez migrer des instances AWS tooAzure machines virtuelles. Dans ce scénario, seule la migration est prise en charge. En d’autres termes, vous pouvez répliquer des instances AWS hello et basculer tooAzure, mais vous ne pouvez pas restaurer. Les instances AWS sont gérées dans hello même façon que les serveurs physiques à des fins de migration. Configurer un coffre Recovery Services, déployer une réplication de toomanage de serveur de configuration local, ajoutez-le toohello coffre et spécifier les paramètres de réplication. Vous activez la réplication pour les machines hello souhaité toomigrate et exécuter une rapide test de basculement. Ensuite, vous exécutez un basculement non planifié avec hello **effectuer la Migration** option.




## <a name="next-steps"></a>Étapes suivantes

- [Migrer les ordinateurs virtuels VMware tooAzure](site-recovery-vmware-to-azure.md)
- [Migrer des ordinateurs virtuels Hyper-V dans VMM clouds tooAzure](site-recovery-vmm-to-azure.md)
- [Migrer des ordinateurs virtuels Hyper-V sans tooAzure VMM](site-recovery-hyper-v-site-to-azure.md)
- [Migrate Azure VMs between Azure regions (Migrer des machines virtuelles Azure entre des régions Azure)](site-recovery-migrate-azure-to-azure.md)
- [Migrer AWS instances tooAzure](site-recovery-migrate-aws-to-azure.md)
- [Préparer les ordinateurs migrés tooenable réplication](site-recovery-azure-to-azure-after-migration.md) région tooanother pour les besoins de récupération d’urgence.
- Commencez à protéger vos charges de travail en [répliquant des machines virtuelles Azure.](site-recovery-azure-to-azure.md)
