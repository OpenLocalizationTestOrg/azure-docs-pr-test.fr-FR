---
title: "aaaManage de calcul power dans l’entrepôt de données SQL Azure (aperçu) | Documents Microsoft"
description: "Capacités de montée en puissance des performances dans Azure SQL Data Warehouse. Montée en puissance parallèle en ajustant les Dwu ou suspendre et reprendre les coûts toosave de ressources de calcul."
services: sql-data-warehouse
documentationcenter: NA
author: hirokib
manager: johnmac
editor: 
ms.assetid: e13a82b0-abfe-429f-ac3c-f2b6789a70c6
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: manage
ms.date: 03/22/2017
ms.author: elbutter
ms.openlocfilehash: 1ffbe8d694ac181eaeb6f585a2cee87a570ed7d5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-compute-power-in-azure-sql-data-warehouse-overview"></a>Gestion de la puissance de calcul dans Azure SQL Data Warehouse (Vue d’ensemble)
> [!div class="op_single_selector"]
> * [Vue d'ensemble](sql-data-warehouse-manage-compute-overview.md)
> * [Portail](sql-data-warehouse-manage-compute-portal.md)
> * [PowerShell](sql-data-warehouse-manage-compute-powershell.md)
> * [REST](sql-data-warehouse-manage-compute-rest-api.md)
> * [TSQL](sql-data-warehouse-manage-compute-tsql.md)
>
>

architecture Hello de SQL Data Warehouse sépare le stockage et calcul, ce qui permet de chaque tooscale indépendamment. Par conséquent, le calcul peut être les demandes de performances toomeet à l’échelle indépendante de la quantité de hello de données. Une conséquence naturelle de cette architecture est la séparation de la [facturation][billed] du calcul et du stockage. 

Cette présentation décrit comment monter en charge fonctionne avec SQL Data Warehouse et comment tooutilize hello suspendre, reprendre et des fonctionnalités de mise à l’échelle de l’entrepôt de données SQL. Consultez hello [unités (Dwu) de l’entrepôt de données] [ data warehouse units (DWUs)] toolearn page Comment Dwu et les performances sont liés. 

## <a name="how-compute-management-operations-work-in-sql-data-warehouse"></a>Fonctionnement des opérations de gestion du calcul dans SQL Data Warehouse
architecture Hello pour SQL Data Warehouse se compose d’un nœud de contrôle, le calcul des nœuds et une couche de stockage hello réparties sur les 60 distributions. 

Pendant une session active normale dans l’entrepôt de données SQL, nœud de tête de votre système gère les métadonnées hello et contient l’optimiseur de requête hello distribué. Sous ce nœud principal, se trouvent les nœuds de calcul et la couche de stockage. Pour une 400 DWU, votre système a un nœud principal, quatre nœuds de calcul et couche de stockage hello, consistant à 60 distributions. 

Lorsque vous subir une échelle ou interrompez l’opération, système de hello tout d’abord supprime toutes les requêtes entrantes et restaure les transactions tooensure un état cohérent. La mise à l’échelle intervient uniquement une fois la restauration des transactions effectuée. Pour une opération de montée en puissance parallèle, les dispositions de système de hello hello du nombre de nœuds de calcul supplémentaire souhaité et commence ensuite le rattachement de couche de stockage toohello hello calcul nœuds. Pour une opération de réduction, hello nœuds inutiles sont publiées et autres nœuds de calcul hello eux-mêmes rattachement toohello le nombre approprié de distributions. Pour une opération de pause, toutes les calcul nœuds sont publiées et votre système est soumises à une variété de tooleave des opérations de métadonnées de votre système final dans un état stable.

| DWU  | \# de nœuds de calcul | \# de distributions par nœud |
| ---- | ------------------ | ---------------------------- |
| 100  | 1                  | 60                           |
| 200  | 2                  | 30                           |
| 300  | 3                  | 20                           |
| 400  | 4                  | 15                           |
| 500  | 5                  | 12                           |
| 600  | 6                  | 10                           |
| 1 000 | 10                 | 6                            |
| 1 200 | 12                 | 5                            |
| 1 500 | 15                 | 4                            |
| 2000 | 20                 | 3                            |
| 3000 | 30                 | 2                            |
| 6000 | 60                 | 1                            |

trois fonctions principales Hello pour la gestion de compute sont :

1. Suspendre
2. Reprendre
3. Mettre à l'échelle

Chacune de ces opérations peut-être prendre plusieurs minutes toocomplete. Si vous êtes mise à l’échelle, suspension/reprise automatiquement, vous souhaiterez tooensure de logique de tooimplement que certaines opérations ont été effectuées avant de procéder à une autre action. 

Vérification de l’état de base de données hello via différents points de terminaison vous permettra de toocorrectly implémenter l’automatisation de ces opérations. portail de Hello fournira une notification à la fin d’un état actuel de bases de données opération et hello mais n’autorise pas de vérification de la programmation de l’état. 

>  [!NOTE]
>
>  La fonctionnalité de gestion du calcul n’existe pas sur tous les points de terminaison.
>
>  

|              | Suspendre/Reprendre | Scale | Vérifier l’état de la base de données |
| ------------ | ------------ | ----- | -------------------- |
| Portail Azure | Oui          | Oui   | **Non**               |
| PowerShell   | Oui          | Oui   | Oui                  |
| API REST     | Oui          | Oui   | Oui                  |
| T-SQL        | **Non**       | Oui   | Oui                  |



<a name="scale-compute-bk"></a>

## <a name="scale-compute"></a>Mise à l’échelle des ressources de calcul

Les performances dans SQL Data Warehouse se mesurent en [Data Warehouse Units (DWU)][data warehouse units (DWUs)] qui sont une unité abstraite de ressources de calcul (processeur, mémoire et bande passante d’E/S). Un utilisateur qui souhaite tooscale les performances de leur système pouvez le faire par différents moyens, par exemple via le portail de hello, T-SQL et les API REST. 

### <a name="how-do-i-scale-compute"></a>Comment mettre à l’échelle les ressources de calcul ?
La puissance de calcul est gérée pour vous SQL Data Warehouse en modifiant la valeur dwu hello. Les performances augmentent [de manière linéaire][linearly] à mesure que vous ajoutez des DWU pour certaines opérations.  Nous proposons des offres DWU qui vous garantissent une évolution notable de vos performances lorsque vous effectuez une montée ou une descente en puissance de votre système. 

tooadjust Dwu, vous pouvez utiliser une de ces méthodes individuelles.

* [Mise à l’échelle de la puissance de calcul avec le portail Azure][Scale compute power with Azure portal]
* [Mise à l’échelle de la puissance de calcul avec PowerShell][Scale compute power with PowerShell]
* [Mise à l’échelle de la puissance de calcul avec les API REST][Scale compute power with REST APIs]
* [Mise à l’échelle de la puissance de calcul avec TSQL][Scale compute power with TSQL]

### <a name="how-many-dwus-should-i-use"></a>Combien d’unités DWU dois-je utiliser ?

toounderstand votre valeur DWU idéale est, essayez d’et vers le bas jusqu'à la mise à l’échelle et des requêtes en cours d’exécution après le chargement de vos données. La mise à l’échelle étant rapide, vous pouvez essayer plusieurs niveaux de performances en une heure ou moins. 

> [!Note] 
> Entrepôt de données SQL est conçu tooprocess de grandes quantités de données. toosee ses fonctionnalités trues pour la mise à l’échelle, surtout au plus grand Dwu, que vous souhaitez toouse un jeu de données volumineux qui approche ou dépasse 1 To.

Recommandations relatives à la recherche hello meilleures DWU de votre charge de travail :

1. Si vous disposez d’un entrepôt de données en développement, commencez par sélectionner un niveau de performances utilisant un nombre réduit d’unités DWU.  DW400 ou DW200 est un bon point de départ.
2. Surveiller les performances de votre application, en observant nombre hello de Dwu sélectionné par rapport performances toohello que vous observez.
3. Déterminez la quantité accélérer ou ralentir les performances pour vous tooreach hello niveau de performance optimal pour les besoins de votre par en supposant que l’échelle linéaire.
4. Augmentez ou diminuez le nombre de hello Dwu dans toohow proportion beaucoup plus rapide ou plus lent vous voulez tooperform de votre charge de travail. 
5. Continuez à effectuer des ajustements jusqu’à ce que vous atteigniez le niveau de performances requis par vos activités.

> [!NOTE]
>
> Performances des requêtes augmentent avec plus de parallélisation uniquement si le travail de hello peut être répartis entre les nœuds de calcul. Si vous trouvez que la mise à l’échelle ne change pas les performances, consultez nos articles toocheck si vos données sont distribuées inégalement ou si vous introduisez une grande quantité de déplacement des données de réglage des performances. 

### <a name="when-should-i-scale-dwus"></a>Quand dois-je mettre les unités DWU à l’échelle ?
Mise à l’échelle Dwu modifie hello scénarios importants suivants :

1. Modification linéaire des performances du système hello pour les analyses, les agrégations et les instructions de SACT
2. Nombre de hello croissant de lecteurs et writers lors du chargement avec PolyBase
3. Nombre maximal de requêtes simultanées et d’emplacements concurrentiels

Quand tooscale Dwu :

1. Avant d’exécuter une opération de chargement ou de transformation de données importante, vous pouvez augmenter le nombre d’unités DWU afin que vos données soient disponibles plus rapidement.
2. Pendant les heures de pointe, l’échelle tooaccommodate plus grand nombre de requêtes simultanées. 

<a name="pause-compute-bk"></a>

## <a name="pause-compute"></a>Suspension du calcul
[!INCLUDE [SQL Data Warehouse pause description](../../includes/sql-data-warehouse-pause-description.md)]

toopause une base de données, utilisez une de ces méthodes individuelles.

* [Suspension du calcul avec le portail Azure][Pause compute with Azure portal]
* [Suspension du calcul avec PowerShell][Pause compute with PowerShell]
* [Suspension du calcul avec des API REST][Pause compute with REST APIs]

<a name="resume-compute-bk"></a>

## <a name="resume-compute"></a>Reprise du calcul
[!INCLUDE [SQL Data Warehouse resume description](../../includes/sql-data-warehouse-resume-description.md)]

tooresume une base de données, utilisez une de ces méthodes individuelles.

* [Reprise du calcul avec le portail Azure][Resume compute with Azure portal]
* [Reprise du calcul avec PowerShell][Resume compute with PowerShell]
* [Reprise du calcul avec des API REST][Resume compute with REST APIs]

<a name="check-compute-bk"></a>

## <a name="check-database-state"></a>Vérifier l’état de base de données 

tooresume une base de données, utilisez une de ces méthodes individuelles.

- [Vérifier l’état de la base de données avec T-SQL][Check database state with T-SQL]
- [Vérifier l’état de la base de données avec PowerShell][Check database state with PowerShell]
- [Vérifier l’état de la base de données avec les API REST][Check database state with REST APIs]

## <a name="permissions"></a>Autorisations

Base de données de mise à l’échelle hello nécessite des autorisations de hello décrites dans [ALTER DATABASE][ALTER DATABASE].  Suspendre et reprendre nécessitent hello [SQL DB collaborateur] [ SQL DB Contributor] autorisation, spécifiquement Microsoft.Sql/servers/databases/action.

<a name="next-steps-bk"></a>

## <a name="next-steps"></a>Étapes suivantes
Consultez toohello suivant toohelp articles vous comprenez certains concepts de performance clés supplémentaires :

* [Gestion des charges de travail et d’accès concurrentiel][Workload and concurrency management]
* [Vue d’ensemble de conception de table][Table design overview]
* [Distribution de tables][Table distribution]
* [Indexation de table][Table indexing]
* [Partitionnement de tables][Table partitioning]
* [Statistiques de table][Table statistics]
* [Meilleures pratiques][Best practices]

<!--Image reference-->

<!--Article references-->
[data warehouse units (DWUs)]: ./sql-data-warehouse-overview-what-is.md#predictable-and-scalable-performance-with-data-warehouse-units
[billed]: https://azure.microsoft.com/en-us/pricing/details/sql-data-warehouse/
[linearly]: ./sql-data-warehouse-overview-what-is.md#predictable-and-scalable-performance-with-data-warehouse-units
[Scale compute power with Azure portal]: ./sql-data-warehouse-manage-compute-portal.md#scale-compute-power
[Scale compute power with PowerShell]: ./sql-data-warehouse-manage-compute-powershell.md#scale-compute-bk
[Scale compute power with REST APIs]: ./sql-data-warehouse-manage-compute-rest-api.md#scale-compute-bk
[Scale compute power with TSQL]: ./sql-data-warehouse-manage-compute-tsql.md#scale-compute-bk

[capacity limits]: ./sql-data-warehouse-service-capacity-limits.md

[Pause compute with Azure portal]:  ./sql-data-warehouse-manage-compute-portal.md#pause-compute-bk
[Pause compute with PowerShell]: ./sql-data-warehouse-manage-compute-powershell.md#pause-compute-bk
[Pause compute with REST APIs]: ./sql-data-warehouse-manage-compute-rest-api.md#pause-compute-bk

[Resume compute with Azure portal]:  ./sql-data-warehouse-manage-compute-portal.md#resume-compute-bk
[Resume compute with PowerShell]: ./sql-data-warehouse-manage-compute-powershell.md#resume-compute-bk
[Resume compute with REST APIs]: ./sql-data-warehouse-manage-compute-rest-api.md#resume-compute-bk

[Check database state with T-SQL]: ./sql-data-warehouse-manage-compute-tsql.md#check-database-state-and-operation-progress
[Check database state with PowerShell]: ./sql-data-warehouse-manage-compute-powershell.md#check-database-state
[Check database state with REST APIs]: ./sql-data-warehouse-manage-compute-rest-api.md#check-database-state

[Workload and concurrency management]: ./sql-data-warehouse-develop-concurrency.md
[Table design overview]: ./sql-data-warehouse-tables-overview.md
[Table distribution]: ./sql-data-warehouse-tables-distribute.md
[Table indexing]: ./sql-data-warehouse-tables-index.md
[Table partitioning]: ./sql-data-warehouse-tables-partition.md
[Table statistics]: ./sql-data-warehouse-tables-statistics.md
[Best practices]: ./sql-data-warehouse-best-practices.md
[development overview]: ./sql-data-warehouse-overview-develop.md

[SQL DB Contributor]: ../active-directory/role-based-access-built-in-roles.md#sql-db-contributor

<!--MSDN references-->
[ALTER DATABASE]: https://msdn.microsoft.com/library/mt204042.aspx

<!--Other Web references-->
[Azure portal]: http://portal.azure.com/
