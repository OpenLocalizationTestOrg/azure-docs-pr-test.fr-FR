---
title: "aaaFailover en mode de récupération de Site | Documents Microsoft"
description: "Azure Site Recovery coordonne la réplication hello, le basculement et récupération des ordinateurs virtuels et des serveurs physiques. En savoir plus sur tooAzure de basculement ou un centre de données secondaire."
services: site-recovery
documentationcenter: 
author: prateek9us
manager: gauravd
editor: 
ms.assetid: 44813a48-c680-4581-a92e-cecc57cc3b1e
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 07/04/2017
ms.author: pratshar
ms.openlocfilehash: 7cacea829d78bb7de2b2d67402291b472b10f023
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="failover-in-site-recovery"></a>Basculement via Microsoft Azure Site Recovery
Cet article décrit comment toofailover les ordinateurs virtuels et des serveurs physiques protègent par Site Recovery.

## <a name="prerequisites"></a>Composants requis
1. Avant d’effectuer un basculement, effectuez une [test de basculement](site-recovery-test-failover-to-azure.md) tooensure que tout fonctionne comme prévu.
1. [Préparer hello réseau](site-recovery-network-design.md) à l’emplacement cible avant d’effectuer un basculement.  


## <a name="run-a-failover"></a>Exécuter un basculement
Cette procédure décrit comment toorun un basculement pour un [plan de récupération](site-recovery-create-recovery-plans.md). Vous pouvez également exécuter basculement hello pour un serveur physique ou un seul ordinateur virtuel à partir de hello **éléments répliqués** page


![Basculement](./media/site-recovery-failover/Failover.png)

1. Sélectionnez **Plans de récupération** > *nom_planrécupération*. Cliquez sur **Basculement**.
2. Sur hello **basculement** écran, sélectionnez un **Point de récupération** toofailover à. Vous pouvez utiliser une des options suivantes de hello :
    1.  **Dernière** (par défaut) : cette option traite tout d’abord toutes les données hello qui a été envoyé tooSite récupération service toocreate un point de récupération pour chaque ordinateur virtuel avant de les avoir basculé tooit. Cette option fournit hello plus bas RPO (Recovery Point Objective) en tant que hello virtuels créés après le basculement a toutes les données hello qui a été répliquées tooSite le service de récupération lorsque hello basculement a été déclenchée.
    1.  **Dernier traitement**: cette option bascule toutes les machines virtuelles hello plan toohello dernière récupération du point de récupération qui a déjà été traitée par le service de récupération de Site. Lorsque vous effectuez un test de basculement d’un ordinateur virtuel, la date et heure du dernier point de récupération traité hello est également affiché. Si vous effectuez le basculement d’un plan de récupération, vous pouvez atteindre l’ordinateur virtuel de tooindividual et observez **des Points de récupération la plus récente** vignette tooget ces informations. Aucun temps n’est consacré à tooprocess hello des données non traitées, cette option fournit une option de basculement faible RTO (objectif de temps de récupération).
    1.  **Dernière cohérentes au niveau application**: cette option bascule toutes les machines virtuelles hello plan toohello dernière application récupération cohérent du point de récupération qui a déjà été traitée par le service de récupération de Site. Lorsque vous effectuez un test de basculement d’un ordinateur virtuel, la date et heure du dernier point de récupération cohérents avec l’application hello est également affiché. Si vous effectuez le basculement d’un plan de récupération, vous pouvez atteindre l’ordinateur virtuel de tooindividual et observez **des Points de récupération la plus récente** vignette tooget ces informations.
    1.  **Latest multi-VM processed** (Dernier point multimachine virtuelle traité) : cette option est disponible uniquement pour les plans de récupération qui incluent au moins une machine virtuelle avec la cohérence multimachine virtuelle activée. Machines virtuelles qui font partie d’une réplication groupe basculement toohello dernière courantes multi-VM récupération cohérent du point. Autres machines virtuelles basculement tootheir dernier traité point de récupération.  
    1.  **Latest multi-VM app-consistent** (Dernier point d’application multimachine virtuelle cohérent) : cette option est disponible uniquement pour les plans de récupération qui incluent au moins une machine virtuelle avec la cohérence multimachine virtuelle activée. Machines virtuelles qui font partie d’une réplication de groupe basculement toohello commun multi-VM récupération cohérents avec les applications les plus récentes. Autres machines virtuelles basculement tootheir dernière cohérents avec les applications de points de récupération.
    1.  **Personnalisé**: Si vous effectuez un test de basculement d’un ordinateur virtuel, vous pouvez ensuite utiliser ce point de récupération particulier option toofailover tooa.

    > [!NOTE]
    > Hello option toochoose un point de récupération n’est disponible que lorsque vous basculez sur tooAzure.
    >
    >


1. Si certains des ordinateurs virtuels de hello dans le plan de récupération hello ont été basculés d’une exécution précédente et maintenant hello virtuels sont actifs sur les emplacements source et cible, vous pouvez utiliser **modifier la direction de** option direction hello toodecide le basculement hello doit se produire.
1. Si vous avez basculé tooAzure et le chiffrement des données est activé pour le cloud hello (s’applique uniquement lorsque vous avez protégé des ordinateurs virtuels Hyper-v à partir d’un serveur VMM), dans **clé de chiffrement** certificat hello select qui a été émis quand vous activé le chiffrement des données pendant l’installation sur le serveur VMM de hello.
1. Sélectionnez **arrêt de la machine avant de commencer le basculement** si vous souhaitez que la récupération de Site tooattempt toodo un arrêt des machines virtuelles source avant de déclencher hello basculement. Le basculement est effectué même en cas d’échec de l’arrêt.  

    > [!NOTE]
    > En cas d’ordinateurs virtuels Hyper-v, cette option essaie également toosynchronize hello des données locales qui n’a pas encore été envoyées toohello service avant de déclencher le basculement de hello.
    >
    >

1. Vous pouvez suivre la progression du basculement hello sur hello **travaux** page. Même si des erreurs se produisent pendant un basculement non planifié, le plan de récupération hello s’exécute jusqu'à ce qu’elle est terminée.
1. Après le basculement de hello, valider hello virtual machine en vous connectant à tooit. Si vous voulez toogo un autre point de récupération pour l’ordinateur virtuel de hello, vous pouvez ensuite utiliser **modifier le point de récupération** option.
1. Une fois que vous êtes satisfait de hello a échoué sur l’ordinateur virtuel, vous pouvez **valider** hello de basculement. Cette opération supprime tous les points de récupération hello disponibles avec le service de hello et **modifier le point de récupération** option ne seront plus disponible.

## <a name="planned-failover"></a>Basculement planifié
Outre la basculement,les machines virtuelles Hyper-V protégées à l’aide de Site Recovery prennent également en charge le **Basculement planifié**. Cette option de basculement évite toute perte de données. Lorsqu’un basculement planifié est déclenché, tout d’abord hello source d’ordinateurs virtuels sont arrêtés, les données de salutation n’a encore toobe synchronisé est synchronisé et ensuite un basculement est déclenché.

> [!NOTE]
> Lorsque vous machines virtuelles de basculement Hyper-v à partir d’un local tooanother de site local site, toocome toohello arrière locale principale vous avez toofirst **réplication inverse** site précédent tooprimary de machine virtuelle hello et puis déclenchez un basculement. Si l’ordinateur virtuel principal hello n’est pas disponible, puis avant de démarrer trop**réplication inverse** vous avez toorestore hello virtual machine à partir d’une sauvegarde.   
>
>

## <a name="failover-job"></a>Travail de basculement

![Basculement](./media/site-recovery-failover/FailoverJob.png)

Le déclenchement d’un basculement implique les étapes suivantes :

1. Vérification des conditions requises : cette étape s’assure que toutes les conditions requises pour le basculement sont satisfaites.
1. Basculement : Cette étape traite les données de hello et rend prêt afin qu’une machine virtuelle Azure peut être créée à partir d’elle. Si vous avez choisi **dernière** point de récupération, cette étape crée un point de récupération à partir des données hello qui a été envoyées toohello service.
1. Démarrer : Cette étape crée une machine virtuelle Azure à l’aide de données de hello traitées à l’étape précédente de hello.

> [!WARNING]
> **Ne pas annuler une en cours basculement**: avant de démarrer le basculement, la réplication pour la machine virtuelle de hello est arrêtée. Si vous **Annuler** un travail de progression, s’arrête le basculement mais la machine virtuelle de hello ne démarrera pas tooreplicate. Il n’est plus possible ensuite de démarrer à nouveau la réplication.
>
>

## <a name="time-taken-for-failover-tooazure"></a>Temps nécessaire pour le basculement tooAzure

Dans certains cas, le basculement d’ordinateurs virtuels nécessite une étape supplémentaire intermédiaire qui prend généralement environ 8 toocomplete de minutes too10. Il s’agit des cas suivants :

* Machines virtuelles VMware utilisant une version antérieure à la 9.8 pour le service de mobilité
* Serveurs physiques 
* Machines virtuelles VMware Linux
* Machines virtuelles Hyper-V protégées en tant que serveurs physiques
* Machines virtuelles où les pilotes suivants ne sont pas présents en tant que pilotes de démarrage 
    * storvsc 
    * vmbus 
    * storflt 
    * intelide 
    * atapi
* Machines virtuelles VMware qui n’ont pas de service DHCP activé, que vous utilisiez des adresses IP statiques ou DHCP

Bonjour tous les autres cas cette étape intermédiaire n’est pas obligatoire et durée hello pour le basculement hello est nettement plus faible. 





## <a name="using-scripts-in-failover"></a>Utilisation de scripts lors du basculement
Vous souhaiterez peut-être tooautomate certaines actions tout en effectuant un basculement. Vous pouvez utiliser des scripts ou [runbooks Azure automation](site-recovery-runbook-automation.md) dans [plans de récupération](site-recovery-create-recovery-plans.md) toodo qui.

## <a name="other-considerations"></a>Autres points à considérer
* **Lettre de lecteur** : tooretain lettre de lecteur hello sur des machines virtuelles après basculement, vous pouvez définir hello **stratégie SAN** pour hello virtual machine trop**OnlineAll**. [En savoir plus](https://support.microsoft.com/en-us/help/3031135/how-to-preserve-the-drive-letter-for-protected-virtual-machines-that-are-failed-over-or-migrated-to-azure).



## <a name="next-steps"></a>Étapes suivantes
Une fois que vous n’avez pas sur les ordinateurs virtuels et de centre de données local hello est disponible, vous devez [ **reprotéger** ](site-recovery-how-to-reprotect.md) les ordinateurs virtuels VMware sauvegarder le centre de données local toohello.

Utilisez [ **le basculement planifié** ](site-recovery-failback-from-azure-to-hyper-v.md) option trop**la restauration automatique** ordinateurs virtuels Hyper-v de nouveau tooon local Azure.

Si vous n’avez pas sur une Hyper-v virtual machine tooanother des données locales center géré par un centre de données principal de serveur et hello VMM est disponible, puis utilisez **la réplication inverse** option toostart hello réplication différé toohello Centre de données principal.
