---
title: "aaaMonitoring & réglage des performances - base de données SQL Azure | Documents Microsoft"
description: "Conseils pour le réglage des performances dans Azure SQL Database par le biais de l’évaluation et de l’amélioration."
services: sql-database
documentationcenter: 
author: v-shysun
manager: felixwu
editor: 
keywords: "réglage des performances de sql, réglage des performances de base de données, conseils pour le réglage des performances de sql, réglage des performances de sql database"
ms.assetid: eb7b3f66-3b33-4e1b-84fb-424a928a6672
ms.service: sql-database
ms.custom: monitor & tune
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: v-shysun
ms.openlocfilehash: 9e196831902aa6ea841ef14caf5713e82ebfc62d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="monitoring-and-performance-tuning"></a>Surveillance et optimisation des performances

Base de données SQL Azure est gérée automatiquement et le service de données flexible dans lequel vous pouvez facilement surveiller l’utilisation, ajouter ou supprimer des ressources (processeur, mémoire, e/s), trouver des recommandations qui peuvent améliorer les performances de votre base de données ou base de données permettent d’adapter la charge de travail tooyour et optimiser automatiquement les performances.

Cet article fournit une vue d’ensemble des options de surveillance et d’optimisation des performances, disponibles dans Azure SQL Database.

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="monitoring-and-troubleshooting-database-performance"></a>Surveillance et résolution des problèmes de performances des bases de données

Permet de base de données SQL Azure vous tooeasily surveiller votre utilisation de base de données et identifiez les requêtes susceptibles de provoquer des problèmes de performances hello. Vous pouvez surveiller les performances des bases de données à l’aide du portail Azure ou des vues système. Vous avez hello options pour la surveillance et la résolution des problèmes de performances de la base de données suivantes :

1. Bonjour [portail Azure](https://portal.azure.com), cliquez sur **bases de données SQL**, sélectionnez hello de base de données et l’utiliser pour les ressources approche leur maximum hello analyse graphique toolook. Consommation de DTU est affichée par défaut. Cliquez sur **modifier** toochange hello plage de temps et les valeurs indiquées.
2. Utilisez [Query Performance Insight](sql-database-query-performance.md) requêtes hello tooidentify qui passent hello plus de ressources.
3. Vous pouvez utiliser des vues de gestion dynamique (DMV), événements étendus (`XEvents`), et hello du magasin de requêtes dans les paramètres de performances tooget SSMS en temps réel.

Consultez hello [rubrique Conseils de performances](sql-database-performance-guidance.md) toofind les techniques que vous pouvez utiliser tooimprove les performances de base de données SQL Azure si vous identifiez un problème lié à l’aide de ces rapports ou des vues.

> [!IMPORTANT] 
> Il est recommandé de toujours utiliser hello dernière version de Management Studio tooremain synchronisés avec les mises à jour tooMicrosoft Azure et base de données SQL. [Mettre à jour SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx).
>

## <a name="optimize-database-tooimprove-performance"></a>Optimiser les performances de tooimprove de base de données

Base de données SQL Azure vous permet de tooidentify opportunités tooimprove et optimiser les performances de requête sans modifier les ressources en examinant [recommandations de paramétrage des performances](sql-database-advisor.md). Des index manquants et des requêtes incorrectement optimisées sont souvent à l’origine de performances de base de données limitées. Vous pouvez appliquer ces performances de tooimprove recommandations paramétrage de votre charge de travail.
Vous pouvez également laisser de la base de données SQL Azure trop[optimiser automatiquement les performances de vos requêtes](sql-database-automatic-tuning.md) en appliquant toutes les identifiées recommandations et en vérifiant qu’elles améliorent les performances de la base de données. Vous pouvez utiliser hello suivant des performances de tooimprove options de votre base de données :

1. Utilisez [Assistant de base de données SQL](sql-database-advisor-portal.md) tooview des recommandations pour la création et la suppression des index, le paramétrage des requêtes et résolution des problèmes de schéma.
2. [Activez le réglage automatique](sql-database-automatic-tuning-enable.md) et laissez Azure SQL Database corriger automatiquement les problèmes de performances identifiés.

## <a name="improving-database-performance-with-more-resources"></a>Amélioration des performances de base de données avec davantage de ressources

Enfin, s’il n’y a aucun élément pouvant être actionnée qui peut améliorer les performances de votre base de données, vous pouvez modifier la quantité de hello de ressources disponibles dans la base de données SQL Azure. Vous pouvez affecter d’autres ressources en modifiant hello [niveau de service](sql-database-service-tiers.md) d’un système autonome de base de données ou d’augmenter les Edtu hello d’un pool élastique à tout moment.
1. Pour les bases de données autonomes, vous pouvez [modifier les niveaux de service](sql-database-service-tiers.md) performances de base de données à la demande tooimprove.
2. Pour plusieurs bases de données, envisagez d’utiliser [pools élastiques](sql-database-elastic-pool-guidance.md) tooscale ressources automatiquement.

## <a name="tune-and-refactor-application-or-database-code"></a>Régler et refactoriser le code d’une application ou d’une base de données

Vous pouvez modifier de façon optimale toomore de code d’application utilisent hello de base de données, modifier des index, forcer des plans ou utiliser des indicateurs toomanually adapter la charge de travail tooyour hello de base de données. Trouver des conseils et des conseils de réglage manuel et de réécrire le code hello Bonjour [rubrique Conseils de performances](sql-database-performance-guidance.md) l’article.


## <a name="next-steps"></a>Étapes suivantes

- tooenable automatique de paramétrage dans la base de données SQL Azure et de laisser automatique paramétrage fonctionnalité entièrement gérer votre charge de travail, consultez [activer le réglage automatique](sql-database-automatic-tuning-enable.md).
- paramétrage manuel toouse, vous pouvez passer en revue [recommandations dans le portail Azure de paramétrage](sql-database-advisor-portal.md) et appliquer manuellement hello celles qui améliorent les performances de vos requêtes.
- Modifier les ressources disponibles dans votre base de données en modifiant les [niveaux de service Azure SQL Database](sql-database-performance-guidance.md)