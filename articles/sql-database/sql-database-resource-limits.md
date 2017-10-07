---
title: "aaaAzure limites de ressources de base de données SQL | Documents Microsoft"
description: "Cette page décrit certaines limites de ressources courantes pour une base de données SQL Azure."
services: sql-database
documentationcenter: na
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: 884e519f-23bb-4b73-a718-00658629646a
ms.service: sql-database
ms.custom: DBs & servers
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 07/12/2017
ms.author: carlrab
ms.openlocfilehash: 3e7be4fdc74e802d37274690531caaf138bcedb0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-sql-database-resource-limits"></a>Limites de ressources de base de données SQL Azure
## <a name="overview"></a>Vue d'ensemble
Base de données SQL Azure gère la base de données de hello ressources tooa disponible à l’aide de deux mécanismes différents : **gouvernance de ressources** et **mise en œuvre des limites**. Cette rubrique décrit ces deux domaines principaux de la gestion des ressources.

## <a name="resource-governance"></a>Gouvernance des ressources
Un des objectifs des niveaux de service Basique, Standard, Premium et Premium RS hello hello est toobehave de la base de données SQL Azure comme si la base de données hello s’exécute sur son propre ordinateur, isolé des autres bases de données. La gouvernance des ressources émule ce comportement. Si hello agrégée l’utilisation des ressources atteint hello maximale disponible du processeur, mémoire, e/s du journal et base de données toohello attribué de ressources d’e/s de données, la gouvernance de ressources des requêtes de files d’attente de l’exécution et assigner des ressources toohello en file d’attente des requêtes en tant qu’ils libérer.

En tant que sur un ordinateur dédié, en utilisant tous les résultats de ressources disponibles dans l’exécution des requêtes, en cours d’exécution qui peut entraîner des délais d’attente de commande sur le client de hello. Applications avec une logique agressive de nouvelle tentative et applications qui s’exécutent des requêtes sur la base de données de hello avec une fréquence élevée peuvent rencontrer des messages d’erreur lors de la tentative de tooexecute nouvelles requêtes lors de la limite de hello de demandes simultanées a été atteinte.

### <a name="recommendations"></a>Recommandations :
Surveiller l’utilisation des ressources hello et temps de réponse moyens hello de requêtes lorsque approchent de leur utilisation maximale de hello d’une base de données. Si vous rencontrez des latences de requête supérieures, généralement, trois options s’offrent à vous :

1. Réduisez nombre de hello d’entrant demandes toohello de base de données tooprevent délai d’expiration et hello accumulation de demandes.
2. Affecter une base de données du toohello au niveau de performance supérieur.
3. Optimiser les requêtes tooreduce hello l’utilisation des ressources de chaque requête. Pour plus d’informations, consultez hello section compréhension de requêtes dans l’article de conseils pour les performances de base de données SQL Azure hello.

## <a name="enforcement-of-limits"></a>Application de limites
Les ressources autres que le processeur, la mémoire, les E/S de journal et les E/S de données sont appliquées en refusant les nouvelles demandes lorsque les limites sont atteintes. Lorsqu’une base de données atteint la limite de taille maximale de hello configuré, les insertions et les mises à jour qui augmentent la taille de données échouent, interrompre sélectionne et les suppressions toowork. Les clients reçoivent un [message d’erreur](sql-database-develop-error-messages.md) en fonction de la limite de hello qui a été atteint.

Par exemple, nombre de hello de base de données SQL de connexions tooa et nombre de hello de demandes simultanées qui peuvent être traités sont limitées. Base de données SQL permet de nombre hello de connexions toohello de base de données toobe supérieur au nombre de hello demandes simultanées toosupport du regroupement de connexions. Alors que le nombre de hello de connexions disponibles peut être facilement contrôlé par l’application hello, hello de demandes parallèles est souvent tooestimate plus difficile de fois et toocontrol. En particulier pendant les pics de charge lors de l’application hello envoie un trop grand nombre de demandes ou de base de données hello atteint ses limites de ressources et démarre accumuler les threads de travail en raison de toolonger des requêtes en cours d’exécution, les erreurs peuvent se produire.

## <a name="service-tiers-and-performance-levels"></a>Niveaux de service et niveaux de performances
Il existe des niveaux de service et de performances à la fois pour les pools élastiques et pour les bases de données uniques.

### <a name="single-databases"></a>Bases de données uniques
Pour une base de données, les limites de hello d’une base de données sont définies par hello de base de données service couche et niveau de performance. Hello tableau suivant décrit les caractéristiques de hello des bases de données Basic, Standard, Premium et Premium RS à différents niveaux de performances.

[!INCLUDE [SQL DB service tiers table](../../includes/sql-database-service-tiers-table.md)]

> [!IMPORTANT]
> Les clients qui utilisent des niveaux de performance P11 et P15 peuvent utiliser jusqu'à to too4 de stockage inclus sans frais supplémentaires. Cette option de 4 To est actuellement disponible dans hello suivant régions : nous East2, ouest des États-Unis, nous Gov Virginie, Europe de l’ouest, Allemagne Central, Asie du Sud, l’est du Japon, est de l’Australie, Canada Central et est du Canada.
>

### <a name="elastic-pools"></a>Pools élastiques
[Pools élastiques](sql-database-elastic-pool.md) partager des ressources entre les bases de données dans le pool de hello. Hello tableau suivant décrit les caractéristiques de hello de base, Standard, Premium et Premium RS pools élastiques.

[!INCLUDE [SQL DB service tiers table for elastic databases](../../includes/sql-database-service-tiers-table-elastic-pools.md)]

Pour une définition d’étendue de chaque ressource répertorié dans les tableaux précédents hello, consultez les descriptions de hello dans [les limites et les fonctionnalités de niveau de Service](sql-database-performance-guidance.md#service-tier-capabilities-and-limits). Pour obtenir une présentation des niveaux de service, consultez [Niveaux de service et de performance de Base de données SQL Azure](sql-database-service-tiers.md).

## <a name="other-sql-database-limits"></a>Autres limites de SQL Database
| Domaine | Limite | Description |
| --- | --- | --- |
| Bases de données utilisant l’exportation automatique par abonnement |10 |Exportation automatique vous permet de toocreate une planification personnalisée pour sauvegarder vos bases de données SQL. Aperçu de Hello de cette fonction se termine le 1er mars 2017.  |
| Bases de données par serveur |Des too5000 |Les too5000 les bases de données sont autorisées par serveur. |
| DTU par serveur |45000 |45 000 DTU sont autorisés par serveur pour l’approvisionnement des bases de données autonomes et des pools élastiques. Nombre total de Hello de bases de données autonomes et partagées autorisées par serveur est limité uniquement par le nombre de hello du serveur dtu.  

> [!IMPORTANT]
> La fonctionnalité Automatiser l’exportation Azure SQL Database est maintenant disponible en version préliminaire et sera supprimée le 1er mars 2017. Depuis le 1er décembre 2016, vous ne pourra plus être exportation tooconfigure en mesure d’automatisée sur toute base de données SQL. Tous vos travaux d’exportation automatisée existant continuera toowork jusqu’au 1er mars 2017. Après le 1er décembre 2016, vous pouvez utiliser [rétention de sauvegarde à long terme](sql-database-long-term-retention.md) ou [Azure Automation](../automation/automation-intro.md) bases de données SQL tooarchive régulièrement à l’aide de PowerShell périodiquement en fonction du calendrier tooa de votre choix. Pour un exemple de script, vous pouvez télécharger hello [exemple de script à partir de GitHub](https://github.com/Microsoft/sql-server-samples/tree/master/samples/manage/azure-automation-automated-export).
>


## <a name="resources"></a>Ressources
[Abonnement Azure et limites, quotas et contraintes du service](../azure-subscription-service-limits.md)

[Niveaux de service et niveaux de performances de la base de données SQL Azure](sql-database-service-tiers.md)

[Messages d'erreur pour les programmes clients SQL Database](sql-database-develop-error-messages.md)
