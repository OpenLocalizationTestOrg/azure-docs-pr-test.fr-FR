---
title: "gestion des aaaConcurrency et de la charge de travail dans l’entrepôt de données SQL | Documents Microsoft"
description: "Décrit la gestion de la concurrence et des charges de travail dans Azure SQL Data Warehouse pour le développement de solutions."
services: sql-data-warehouse
documentationcenter: NA
author: sqlmojo
manager: jhubbard
editor: 
ms.assetid: ef170f39-ae24-4b04-af76-53bb4c4d16d3
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: performance
ms.date: 08/23/2017
ms.author: joeyong;barbkess;kavithaj
ms.openlocfilehash: 7f7e77aa687760252aed16573b609817ed9111c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="concurrency-and-workload-management-in-sql-data-warehouse"></a>Gestion de la concurrence et des charges de travail dans SQL Data Warehouse
toodeliver des performances prévisibles à grande échelle, Microsoft Azure SQL Data Warehouse vous permet de contrôler les niveaux d’accès concurrentiel et les affectations de ressources mémoire et la priorité de l’UC. Cet article vous présente les concepts de toohello de gestion d’accès concurrentiel et la charge de travail, expliquant comment ces deux fonctionnalités ont été implémentées, et comment vous pouvez les contrôler dans votre entrepôt de données. Gestion de la charge de travail de l’entrepôt de données SQL est prévue toohelp prend en charge les environnements multi-utilisateurs. Elle n’est pas destinée aux charges de travail multilocataires.

## <a name="concurrency-limits"></a>Limites de concurrence
Entrepôt de données SQL permet les too1, 024 connexions simultanées. Les 1024 connexions peuvent soumettre des requêtes simultanément. Débit toooptimize, entrepôt de données SQL peut cependant, file d’attente certaines tooensure de requêtes que chaque requête reçoit une allocation de mémoire minimale. La mise en file d’attente se produit lors de l’exécution de la requête. Par les files d’attente des requêtes lors de la concurrence limite est atteinte, l’entrepôt de données SQL peut augmenter débit total en vous assurant que les requêtes actives obtiennent accès toocritically nécessaire de ressources mémoire.  

Les limites de concurrence sont régies par deux concepts : les *requêtes simultanées* et les *emplacements de concurrence*. Pour une requête tooexecute, il doit s’exécuter au sein de la limite de simultanéité des requêtes hello et de répartition des créneaux hello d’accès concurrentiel.

* Requêtes simultanées sont des requêtes hello l’exécution à hello même temps. Entrepôt de données SQL prend en charge les requêtes simultanées de too32 sur plus volumineux DWU hello.
* Les emplacements de concurrence sont alloués en fonction de la DWU. Chaque DWU100 fournit 4 emplacements de concurrence. Par exemple, une DW100 alloue 4 emplacements de concurrence et une DW1000 en alloue 40. Chaque requête consomme un ou plusieurs d’accès concurrentiel des emplacements dépendantes hello [classe de ressource](#resource-classes) de requête de hello. Les requêtes s’exécutant dans une classe de ressource smallrc hello consomment un emplacement d’accès concurrentiel. Les requêtes en cours d’exécution dans une classe de ressource supérieure consomment plusieurs emplacements de concurrence.

Hello tableau suivant décrit les limites de hello pour les requêtes simultanées et les emplacements d’accès concurrentiel à hello différentes tailles DWU.

### <a name="concurrency-limits"></a>Limites de concurrence
| DWU | Nombre maximal de requêtes simultanées | Emplacements de concurrence alloués |
|:--- |:---:|:---:|
| DW100 |4 |4 |
| DW200 |8 |8 |
| DW300 |12 |12 |
| DW400 |16 |16 |
| DW500 |20 |20 |
| DW600 |24 |24 |
| DW1000 |32 |40 |
| DW1200 |32 |48 |
| DW1500 |32 |60 |
| DW2000 |32 |80 |
| DW3000 |32 |120 |
| DW6000 |32 |240 |

Lorsque l’un de ces seuils est atteint, les nouvelles requêtes sont mises en file d’attente et exécutées sur la base du modèle premier entré, premier sorti.  Comme des requêtes est terminée et nombre de hello de requêtes et des emplacements tombe en dessous des limites de hello, les requêtes en file d’attente sont libérés. 

> [!NOTE]  
> *Sélectionnez* requêtes exécution exclusivement sur vues de gestion dynamiques (DMV) ou les vues de catalogue ne sont pas soumis à des limites d’accès concurrentiel de hello. Vous pouvez surveiller le système hello, quelle que soit le nombre de hello de requêtes s’exécutant sur ce dernier.
> 
> 

## <a name="resource-classes"></a>Classes de ressources
Les classes de ressources vous permettent de contrôler l’allocation de mémoire et les cycles de processeur tooa requête. Vous pouvez attribuer deux types d’utilisateur de tooa de classes de ressources sous forme de hello des rôles de base de données. Hello deux types de classes de ressources sont les suivantes :
1. Classes de ressources dynamiques (**smallrc, mediumrc, largerc, xlargerc**) allouer une quantité de mémoire en fonction de hello variable DWU actuelle. Cela signifie que lorsque vous faites évoluer tooa DWU plus grand, vos requêtes automatiquement obtenir davantage de mémoire. 
2. Classes de ressources statiques (**staticrc10, staticrc20, staticrc30, staticrc40, staticrc50, staticrc60, staticrc70, staticrc80**) allouer hello même quantité de mémoire, indépendamment du hello DWU actuelle (sous réserve que hello DWU lui-même dispose de suffisamment de mémoire). Cela signifie que sur les DWU volumineuses, vous pouvez exécuter davantage de requêtes simultanées dans chaque classe de ressources.

La quantité de mémoire allouée aux utilisateurs de **smallrc** et **staticrc10** étant inférieure, ils peuvent profiter d’une plus grande concurrence. En revanche, les utilisateurs affectés trop**xlargerc** ou **staticrc80** reçoivent de grandes quantités de mémoire, et par conséquent, moins de leurs requêtes peuvent s’exécuter simultanément.

Par défaut, chaque utilisateur est un membre de classe de ressource le plus petit hello, **smallrc**. Hello procédure `sp_addrolemember` est utilisé de classe de ressource tooincrease hello, et `sp_droprolemember` est utilisé de classe de ressource toodecrease hello. Par exemple, cette commande augmenterait classe de ressource hello de loaduser trop**largerc**:

```sql
EXEC sp_addrolemember 'largerc', 'loaduser'
```


### <a name="queries-that-do-not-honor-resource-classes"></a>Requêtes qui ne tiennent pas compte des classes de ressources

Certains types de requêtes ne bénéficient pas d’une allocation de mémoire supérieure. système de Hello ignore leur allocation de classe de ressource et toujours exécute ces requêtes dans la classe de ressource le plus petit hello à la place. Si ces requêtes s’exécutent toujours dans la classe de ressource le plus petit hello, ils peuvent exécuter lorsque les emplacements d’accès concurrentiel sont sous pression et elles ne consomment des emplacements plus que nécessaire. Consultez [Exceptions de classe de ressources](#query-exceptions-to-concurrency-limits) pour plus d’informations.

## <a name="details-on-resource-class-assignment"></a>Détails concernant l’affectation des classes de ressources


Voici quelques autres détails concernant la classe de ressources :

* *Modifier le rôle* l’autorisation est requise classe de ressource hello toochange d’un utilisateur.
* Bien que vous pouvez ajouter un tooone utilisateur ou plusieurs des classes de ressources hello plus élevés, les classes de ressources dynamiques sont prioritaires sur les classes de ressources statiques. Autrement dit, si un utilisateur est assigné tooboth **mediumrc**(dynamique) et **staticrc80**(statique), **mediumrc** est la classe de ressource hello est honoré.
 * Lorsqu’un utilisateur est affecté toomore que la classe d’une ressource dans un type de classe de ressource spécifique (plus d’une classe de ressource dynamique ou plus d’une classe de ressource statique), la classe de ressource la plus élevée hello est respecté. Autrement dit, si un utilisateur est assigné largerc et tooboth mediumrc, la classe de ressource supérieur hello (largerc) est respectée. Et si un utilisateur est assigné tooboth **staticrc20** et **statirc80**, **staticrc80** est honoré.
* classe de ressource Hello hello d’administration d’utilisateur du système ne peut pas être modifié.

Pour obtenir un exemple détaillé, consultez [Exemple de modification d’une classe de ressources utilisateur](#changing-user-resource-class-example).

## <a name="memory-allocation"></a>Allocation de mémoire
Il existe tooincreasing leurs avantages et inconvénients de classe de ressource d’un utilisateur. L’augmentation d’une classe de ressource pour un utilisateur donne leurs requêtes toomore mémoire, ce qui peut signifier que les requêtes s’exécutent plus rapidement.  Toutefois, les classes de ressources plus élevées également réduisent nombre hello de requêtes simultanées qui peuvent s’exécuter. Il s’agit de compromis hello allouer de grandes quantités de requête unique tooa de mémoire ou d’autoriser les autres requêtes, ce qui a également besoin d’allocations de mémoire, toorun simultanément. Si un utilisateur se voit accorder haute allocations de mémoire pour une requête, les autres utilisateurs n’auront pas accès toothat toorun mémoire même une requête.

Hello tableau suivant mappe la mémoire hello allouée tooeach distribution par classe DWU et des ressources.

### <a name="memory-allocations-per-distribution-for-dynamic-resource-classes-mb"></a>Allocations de mémoire par distribution pour les classes de ressources dynamiques (Mo)
| DWU | smallrc | mediumrc | largerc | xlargerc |
|:--- |:---:|:---:|:---:|:---:|
| DW100 |100 |100 |200 |400 |
| DW200 |100 |200 |400 |800 |
| DW300 |100 |200 |400 |800 |
| DW400 |100 |400 |800 |1 600 |
| DW500 |100 |400 |800 |1 600 |
| DW600 |100 |400 |800 |1 600 |
| DW1000 |100 |800 |1 600 |3 200 |
| DW1200 |100 |800 |1 600 |3 200 |
| DW1500 |100 |800 |1 600 |3 200 |
| DW2000 |100 |1 600 |3 200 |6 400 |
| DW3000 |100 |1 600 |3 200 |6 400 |
| DW6000 |100 |3 200 |6 400 |12 800 |

Hello tableau suivant mappe la mémoire hello allouée tooeach distribution par DWU et de la classe de ressource statique. Notez que les classes de ressources supérieurs hello ont leur mémoire réduit les limites de DWU globales toohonor hello.

### <a name="memory-allocations-per-distribution-for-static-resource-classes-mb"></a>Allocations de mémoire par distribution pour les classes de ressources statiques (Mo)
| DWU | staticrc10 | staticrc20 | staticrc30 | staticrc40 | staticrc50 | staticrc60 | staticrc70 | staticrc80 |
|:--- |:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| DW100 |100 |200 |400 |400 |400 |400 |400 |400 |
| DW200 |100 |200 |400 |800 |800 |800 |800 |800 |
| DW300 |100 |200 |400 |800 |800 |800 |800 |800 |
| DW400 |100 |200 |400 |800 |1 600 |1 600 |1 600 |1 600 |
| DW500 |100 |200 |400 |800 |1 600 |1 600 |1 600 |1 600 |
| DW600 |100 |200 |400 |800 |1 600 |1 600 |1 600 |1 600 |
| DW1000 |100 |200 |400 |800 |1 600 |3 200 |3 200 |3 200 |
| DW1200 |100 |200 |400 |800 |1 600 |3 200 |3 200 |3 200 |
| DW1500 |100 |200 |400 |800 |1 600 |3 200 |3 200 |3 200 |
| DW2000 |100 |200 |400 |800 |1 600 |3 200 |6 400 |6 400 |
| DW3000 |100 |200 |400 |800 |1 600 |3 200 |6 400 |6 400 |
| DW6000 |100 |200 |400 |800 |1 600 |3 200 |6 400 |12 800 |

À partir de hello tableau précédent, vous pouvez voir qu’une requête en cours d’exécution sur un DW2000 Bonjour **xlargerc** classe de ressource aurait accès too6, 400 Mo de mémoire dans chacune des bases de données distribuées hello 60.  Dans SQL Data Warehouse, il existe 60 distributions. Par conséquent, l’allocation de mémoire totale toocalculate hello pour une requête dans une classe de ressource donné, le hello au-dessus des valeurs doit être multipliée par 60.

### <a name="memory-allocations-system-wide-gb"></a>Allocations de mémoire à l’échelle du système (Go)
| DWU | smallrc | mediumrc | largerc | xlargerc |
|:--- |:---:|:---:|:---:|:---:|
| DW100 |6 |6 |12 |23 |
| DW200 |6 |12 |23 |47 |
| DW300 |6 |12 |23 |47 |
| DW400 |6 |23 |47 |94 |
| DW500 |6 |23 |47 |94 |
| DW600 |6 |23 |47 |94 |
| DW1000 |6 |47 |94 |188 |
| DW1200 |6 |47 |94 |188 |
| DW1500 |6 |47 |94 |188 |
| DW2000 |6 |94 |188 |375 |
| DW3000 |6 |94 |188 |375 |
| DW6000 |6 |188 |375 |750 |

À partir de cette table d’allocations de mémoire système, vous pouvez voir qu’une requête en cours d’exécution sur un DW2000 dans la classe de ressource xlargerc hello est allouée à un total de 375 Go de mémoire (distributions de 6 400 Mo * 60 / 1 024 tooconvert tooGB) sur l’intégralité de hello de votre entrepôt de données SQL.

Hello même calcul s’applique toostatic des classes de ressources.
 
## <a name="concurrency-slot-consumption"></a>Consommation des emplacements de concurrence  
SQL Data Warehouse accorde plus tooqueries de mémoire en cours d’exécution dans les classes de ressources plus élevées. La mémoire est une ressource fixe.  Par conséquent, hello davantage de mémoire allouée par requête, hello moins de requêtes simultanées peuvent exécuter. Hello tableau suivant réitère tous les concepts de précédente hello dans une seule vue qui affiche le nombre de hello d’emplacements d’accès concurrentiel disponibles par DWU et emplacements hello consommées par chaque classe de ressource.  

### <a name="allocation-and-consumption-of-concurrency-slots-for-dynamic-resource-classes"></a>Allocation et consommation des emplacements de concurrence pour les classes de ressources dynamiques  
| DWU | Nombre maximal de requêtes concurrentes | Emplacements de concurrence alloués | Emplacements utilisés par smallrc | Emplacements utilisés par mediumrc | Emplacements utilisés par largerc | Emplacements utilisés par xlargerc |
|:--- |:---:|:---:|:---:|:---:|:---:|:---:|
| DW100 |4 |4 |1 |1 |2 |4 |
| DW200 |8 |8 |1 |2 |4 |8 |
| DW300 |12 |12 |1 |2 |4 |8 |
| DW400 |16 |16 |1 |4 |8 |16 |
| DW500 |20 |20 |1 |4 |8 |16 |
| DW600 |24 |24 |1 |4 |8 |16 |
| DW1000 |32 |40 |1 |8 |16 |32 |
| DW1200 |32 |48 |1 |8 |16 |32 |
| DW1500 |32 |60 |1 |8 |16 |32 |
| DW2000 |32 |80 |1 |16 |32 |64 |
| DW3000 |32 |120 |1 |16 |32 |64 |
| DW6000 |32 |240 |1 |32 |64 |128 |

### <a name="allocation-and-consumption-of-concurrency-slots-for-static-resource-classes"></a>Allocation et consommation des emplacements de concurrence pour les classes de ressources statiques  
| DWU | Nombre maximal de requêtes concurrentes | Emplacements de concurrence alloués |staticrc10 | staticrc20 | staticrc30 | staticrc40 | staticrc50 | staticrc60 | staticrc70 | staticrc80 |
|:--- |:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| DW100 |4 |4 |1 |2 |4 |4 |4 |4 |4 |4 |
| DW200 |8 |8 |1 |2 |4 |8 |8 |8 |8 |8 |
| DW300 |12 |12 |1 |2 |4 |8 |8 |8 |8 |8 |
| DW400 |16 |16 |1 |2 |4 |8 |16 |16 |16 |16 |
| DW500 | 20| 20| 1| 2| 4| 8| 16| 16| 16| 16|
| DW600 | 24| 24| 1| 2| 4| 8| 16| 16| 16| 16|
| DW1000 | 32| 40| 1| 2| 4| 8| 16| 32| 32| 32|
| DW1200 | 32| 48| 1| 2| 4| 8| 16| 32| 32| 32|
| DW1500 | 32| 60| 1| 2| 4| 8| 16| 32| 32| 32|
| DW2000 | 32| 80| 1| 2| 4| 8| 16| 32| 64| 64|
| DW3000 | 32| 120| 1| 2| 4| 8| 16| 32| 64| 64|
| DW6000 | 32| 240| 1| 2| 4| 8| 16| 32| 64| 128|

À partir de ces tableaux, vous pouvez constater que SQL Data Warehouse s’exécutant comme DW1000 alloue au maximum 32 requêtes simultanées et un total de 40 emplacements de concurrence. Si tous les utilisateurs étaient en cours d’exécution dans smallrc, 32 requêtes simultanées seraient alors autorisées car chaque requête consommerait un emplacement de concurrence. Si tous les utilisateurs sur un DW1000 en cours d’exécution dans mediumrc, chaque requête est allouée 800 Mo par distribution pour une allocation de mémoire totale de 47 Go par la requête et concurrence serait limitée too5 utilisateurs (les emplacements d’accès concurrentiel 40 / 8 emplacements par mediumrc utilisateur).

## <a name="selecting-proper-resource-class"></a>Sélection d’une classe de ressources appropriée  
Une bonne pratique est la classe de ressource tooa toopermanently affecter les utilisateurs, plutôt que de la modification de leurs classes de ressources. Par exemple, tables de charge tooclustered columnstore créer des index de meilleure qualité lors de l’allocation de mémoire. tooensure que charges ont accès toohigher mémoire, créez un utilisateur en particulier pour charger les données et définitivement affecter cette classe de ressource utilisateur tooa plus élevée.
Il existe quelques meilleures toofollow pratiques ici. Comme nous l’avons vu précédemment, SQL DW prend en charge deux types de classes de ressources : les classes de ressources statiques et les classes de ressources dynamiques.
### <a name="loading-best-practices"></a>Bonnes pratiques de chargement
1.  Si les attentes de hello sont des charges régulières quantité de données, une classe de ressource statique est un bon choix. Ultérieurement, lors de la mise à l’échelle des tooget plus de puissance de calcul, de l’entrepôt de données hello pourront toorun plu interroge out-of-the-box, comme utilisateur de charge hello ne consomme pas plus de mémoire.
2.  Si les prévisions de hello sont des charges plus grandes dans certains cas, une classe de ressource dynamique est un bon choix. Ultérieurement, lors de la mise à l’échelle des tooget plus de puissance de calcul, hello charge utilisateur obtient plus mémoire out-of-the-box, par conséquent, ce qui permet hello charge tooperform plus rapidement.

Hello mémoire nécessaire tooprocess charges efficacement dépend hello nature du tableau hello chargé et quantité hello de traitement des données. Par exemple, le chargement des données dans les tables CCI requiert que certains groupes de lignes de mémoire toolet CCI atteint Optimalité. Pour plus d’informations, consultez les index Columnstore hello - Guide de chargement des données.

Comme meilleure pratique, nous vous recommandons de toouse au moins 200 Mo de mémoire pour les charges.

### <a name="querying-best-practices"></a>Bonnes pratiques de requête
Les exigences sur le plan des requêtes varient en fonction de leur complexité. Augmentation de la mémoire par requête ou d’accroître la simultanéité de hello sont les deux tooaugment de méthodes valides pour le débit global en fonction des besoins de requête hello.
1.  Si les prévisions de hello sont des requêtes régulières complexes (par exemple, toogenerate rapports quotidiens et hebdomadaires) et n’avez pas besoin d’avantage tootake de l’accès concurrentiel, une classe de ressource dynamique est un bon choix. Si le système de hello possède plusieurs tooprocess de données, mise à l’échelle de l’entrepôt de données hello par conséquent automatiquement fournira plus de mémoire toohello utilisateur exécutant la requête de hello.
2.  Si les prévisions de hello sont les modèles d’accès concurrentiel diurnes ou variable (par exemple si la base de données hello est interrogé via une interface utilisateur largement accessible web), une classe de ressource statique est un bon choix. Ultérieurement, lors de la mise à l’échelle toodata entrepôt, utilisateur hello associé à la classe de ressource statique hello est automatiquement être toorun en mesure de requêtes simultanées plus.

En sélectionnant accorder appropriée de la mémoire en fonction de la nécessité de hello de votre requête est non trivial, car il dépend de nombreux facteurs, tels que quantité hello de données interrogées, hello nature des schémas de table hello et différentes jointure, la sélection et les prédicats de groupe. À partir d’un point de vue général, allouez davantage de mémoire toocomplete de requêtes plus rapidement, mais elle réduit de manière hello d’accès concurrentiel global. Si la concurrence n’est pas un problème, une allocation excessive de mémoire n’est pas dommageable. ajuster les toofine débit, la tentative de différentes versions de classes de ressources peut être nécessaire.

Vous pouvez utiliser suivante hello stockées toofigure procédure out octroi d’accès concurrentiel et la mémoire par la classe de ressource à une donnée SLO et hello plus proche meilleures classe de ressource pour les opérations CCI nécessitant de mémoire sur la table CCI non partitionnée à une classe de ressource donné :

#### <a name="description"></a>Description :  
Voici l’objectif hello de cette procédure stockée :  
1. figure toohelp utilisateur out octroi d’accès concurrentiel et la mémoire par la classe de ressource à un objectif du contrat donné. Utilisateur doit tooprovide NULL pour le schéma et tablename pour ce comme indiqué dans l’exemple hello ci-dessous.  
2. l’utilisateur toohelp trouver hello meilleures ressources classe la plus proche pour hello mémoire intensed opérations CCI (charger, table de copie, reconstruire les index, etc.) non partitionnée table CCI à une classe de ressource donné. stockée Hello proc utilise toofind de schéma de table à l’allocation de mémoire requise hello pour cela.

#### <a name="dependencies--restrictions"></a>Dépendances et restrictions :
- Cette procédure stockée n’est pas conçue toocalculate mémoire requise pour les table cci partitionnée.    
- Cette procédure stockée ne prend pas d’exigence de mémoire en compte pour la partie SELECT de hello de INSERT/SACT-sélectionnez et il suppose toobe une instruction SELECT simple.
- Cette procédure stockée utilise une table temporaire pour ce peut être utilisé dans la session de hello où cette procédure stockée a été créée.    
- Cette procédure stockée dépend d’offres actuelles de hello (par exemple, configuration matérielle, DMS config) et si un des qui modifie ensuite cette procédure stockée ne fonctionnera pas correctement.  
- Cette procédure stockée dépend de la limite de concurrence offerte existante et si celle-ci change, cette procédure stockée ne fonctionnera pas correctement.  
- Cette procédure stockée dépend des offres de classes de ressources existantes et si celles-ci changent, cette procédure stockée ne fonctionnera pas correctement.  

>  [!NOTE]  
>  Si vous n’obtenez pas de sortie après l’exécution de la procédure stockée avec les paramètres fournis, il est possible que vous soyez confronté à l’un des deux cas suivants : <br />1. Un paramètre DW contient une valeur SLO non valide. <br />2. OU il n’existe aucune classe de ressources correspondante pour l’opération ICC si le nom de la table a été fourni. <br />Par exemple, à DW100, allocation de mémoire disponible la plus élevée est de 400 Mo et si le schéma de la table est large suffisamment toocross hello exigence de 400 Mo.
      
#### <a name="usage-example"></a>Exemple d’utilisation :
Syntaxe :  
`EXEC dbo.prc_workload_management_by_DWU @DWU VARCHAR(7), @SCHEMA_NAME VARCHAR(128), @TABLE_NAME VARCHAR(128)`  
1. @DWU:Vous devez attribuer un tooextract de paramètre NULL hello DWU actuelle à partir de la BD DW de hello ou fournir une prise en charge DWU sous forme de hello de 'DW100'
2. @SCHEMA_NAME:Fournissez un nom de schéma de table de hello
3. @TABLE_NAME:Fournissez un nom de table d’intérêt de hello

Exemples d’exécution de cette procédure stockée :  
```sql  
EXEC dbo.prc_workload_management_by_DWU 'DW2000', 'dbo', 'Table1';  
EXEC dbo.prc_workload_management_by_DWU NULL, 'dbo', 'Table1';  
EXEC dbo.prc_workload_management_by_DWU 'DW6000', NULL, NULL;  
EXEC dbo.prc_workload_management_by_DWU NULL, NULL, NULL;  
```

Table1 utilisé Bonjour exemples ci-dessus pourrait être créée comme indiqué ci-dessous :  
`CREATE TABLE Table1 (a int, b varchar(50), c decimal (18,10), d char(10), e varbinary(15), f float, g datetime, h date);`

#### <a name="heres-hello-stored-procedure-definition"></a>Voici la définition de la procédure stockée hello :
```sql  
-------------------------------------------------------------------------------
-- Dropping prc_workload_management_by_DWU procedure if it exists.
-------------------------------------------------------------------------------
IF EXISTS (SELECT * FROM sys.objects WHERE type = 'P' AND name = 'prc_workload_management_by_DWU')
DROP PROCEDURE dbo.prc_workload_management_by_DWU
GO

-------------------------------------------------------------------------------
-- Creating prc_workload_management_by_DWU.
-------------------------------------------------------------------------------
CREATE PROCEDURE dbo.prc_workload_management_by_DWU
(   @DWU VARCHAR(7),
      @SCHEMA_NAME VARCHAR(128),
       @TABLE_NAME VARCHAR(128)
)
AS
IF @DWU IS NULL
BEGIN
-- Selecting proper DWU for hello current DB if not specified.
SET @DWU = (
  SELECT 'DW'+CAST(COUNT(*)*100 AS VARCHAR(10))
  FROM sys.dm_pdw_nodes
  WHERE type = 'COMPUTE')
END

DECLARE @DWU_NUM INT
SET @DWU_NUM = CAST (SUBSTRING(@DWU, 3, LEN(@DWU)-2) AS INT)

-- Raise error if either schema name or table name is supplied but not both them supplied
--IF ((@SCHEMA_NAME IS NOT NULL AND @TABLE_NAME IS NULL) OR (@TABLE_NAME IS NULL AND @SCHEMA_NAME IS NOT NULL))
--     RAISEERROR('User need toosupply either both Schema Name and Table Name or none of them')
       
-- Dropping temp table if exists.
IF OBJECT_ID('tempdb..#ref') IS NOT NULL
BEGIN
  DROP TABLE #ref;
END

-- Creating ref. temptable (CTAS) toohold mapping info.
-- CREATE TABLE #ref
CREATE TABLE #ref
WITH (DISTRIBUTION = ROUND_ROBIN)
AS 
WITH
-- Creating concurrency slots mapping for various DWUs.
alloc
AS
(
  SELECT 'DW100' AS DWU, 4 AS max_queries, 4 AS max_slots, 1 AS slots_used_smallrc, 1 AS slots_used_mediumrc,
        2 AS slots_used_largerc, 4 AS slots_used_xlargerc, 1 AS slots_used_staticrc10, 2 AS slots_used_staticrc20,
        4 AS slots_used_staticrc30, 4 AS slots_used_staticrc40, 4 AS slots_used_staticrc50,
        4 AS slots_used_staticrc60, 4 AS slots_used_staticrc70, 4 AS slots_used_staticrc80
  UNION ALL
    SELECT 'DW200', 8, 8, 1, 2, 4, 8, 1, 2, 4, 8, 8, 8, 8, 8
  UNION ALL
    SELECT 'DW300', 12, 12, 1, 2, 4, 8, 1, 2, 4, 8, 8, 8, 8, 8
  UNION ALL
    SELECT 'DW400', 16, 16, 1, 4, 8, 16, 1, 2, 4, 8, 16, 16, 16, 16
  UNION ALL
     SELECT 'DW500', 20, 20, 1, 4, 8, 16, 1, 2, 4, 8, 16, 16, 16, 16
  UNION ALL
    SELECT 'DW600', 24, 24, 1, 4, 8, 16, 1, 2, 4, 8, 16, 16, 16, 16
  UNION ALL
    SELECT 'DW1000', 32, 40, 1, 8, 16, 32, 1, 2, 4, 8, 16, 32, 32, 32
  UNION ALL
    SELECT 'DW1200', 32, 48, 1, 8, 16, 32, 1, 2, 4, 8, 16, 32, 32, 32
  UNION ALL
    SELECT 'DW1500', 32, 60, 1, 8, 16, 32, 1, 2, 4, 8, 16, 32, 32, 32
  UNION ALL
    SELECT 'DW2000', 32, 80, 1, 16, 32, 64, 1, 2, 4, 8, 16, 32, 64, 64
  UNION ALL
   SELECT 'DW3000', 32, 120, 1, 16, 32, 64, 1, 2, 4, 8, 16, 32, 64, 64
  UNION ALL
    SELECT 'DW6000', 32, 240, 1, 32, 64, 128, 1, 2, 4, 8, 16, 32, 64, 128
)
-- Creating workload mapping tootheir corresponding slot consumption and default memory grant.
,map
AS
(
  SELECT 'SloDWGroupC00' AS wg_name,1 AS slots_used,100 AS tgt_mem_grant_MB
  UNION ALL
    SELECT 'SloDWGroupC01',2,200
  UNION ALL
    SELECT 'SloDWGroupC02',4,400
  UNION ALL
    SELECT 'SloDWGroupC03',8,800
  UNION ALL
    SELECT 'SloDWGroupC04',16,1600
  UNION ALL
    SELECT 'SloDWGroupC05',32,3200
  UNION ALL
    SELECT 'SloDWGroupC06',64,6400
  UNION ALL
    SELECT 'SloDWGroupC07',128,12800
)
-- Creating ref based on current / asked DWU.
, ref
AS
(
  SELECT  a1.*
  ,       m1.wg_name          AS wg_name_smallrc
  ,       m1.tgt_mem_grant_MB AS tgt_mem_grant_MB_smallrc
  ,       m2.wg_name          AS wg_name_mediumrc
  ,       m2.tgt_mem_grant_MB AS tgt_mem_grant_MB_mediumrc
  ,       m3.wg_name          AS wg_name_largerc
  ,       m3.tgt_mem_grant_MB AS tgt_mem_grant_MB_largerc
  ,       m4.wg_name          AS wg_name_xlargerc
  ,       m4.tgt_mem_grant_MB AS tgt_mem_grant_MB_xlargerc
  ,       m5.wg_name          AS wg_name_staticrc10
  ,       m5.tgt_mem_grant_MB AS tgt_mem_grant_MB_staticrc10
  ,       m6.wg_name          AS wg_name_staticrc20
  ,       m6.tgt_mem_grant_MB AS tgt_mem_grant_MB_staticrc20
  ,       m7.wg_name          AS wg_name_staticrc30
  ,       m7.tgt_mem_grant_MB AS tgt_mem_grant_MB_staticrc30
  ,       m8.wg_name          AS wg_name_staticrc40
  ,       m8.tgt_mem_grant_MB AS tgt_mem_grant_MB_staticrc40
  ,       m9.wg_name          AS wg_name_staticrc50
  ,       m9.tgt_mem_grant_MB AS tgt_mem_grant_MB_staticrc50
  ,       m10.wg_name          AS wg_name_staticrc60
  ,       m10.tgt_mem_grant_MB AS tgt_mem_grant_MB_staticrc60
  ,       m11.wg_name          AS wg_name_staticrc70
  ,       m11.tgt_mem_grant_MB AS tgt_mem_grant_MB_staticrc70
  ,       m12.wg_name          AS wg_name_staticrc80
  ,       m12.tgt_mem_grant_MB AS tgt_mem_grant_MB_staticrc80
  FROM alloc a1
  JOIN map   m1  ON a1.slots_used_smallrc     = m1.slots_used
  JOIN map   m2  ON a1.slots_used_mediumrc    = m2.slots_used
  JOIN map   m3  ON a1.slots_used_largerc     = m3.slots_used
  JOIN map   m4  ON a1.slots_used_xlargerc    = m4.slots_used
  JOIN map   m5  ON a1.slots_used_staticrc10    = m5.slots_used
  JOIN map   m6  ON a1.slots_used_staticrc20    = m6.slots_used
  JOIN map   m7  ON a1.slots_used_staticrc30    = m7.slots_used
  JOIN map   m8  ON a1.slots_used_staticrc40    = m8.slots_used
  JOIN map   m9  ON a1.slots_used_staticrc50    = m9.slots_used
  JOIN map   m10  ON a1.slots_used_staticrc60    = m10.slots_used
  JOIN map   m11  ON a1.slots_used_staticrc70    = m11.slots_used
  JOIN map   m12  ON a1.slots_used_staticrc80    = m12.slots_used
-- WHERE   a1.DWU = @DWU
  WHERE   a1.DWU = UPPER(@DWU)
)
SELECT  DWU
,       max_queries
,       max_slots
,       slots_used
,       wg_name
,       tgt_mem_grant_MB
,       up1 as rc
,       (ROW_NUMBER() OVER(PARTITION BY DWU ORDER BY DWU)) as rc_id
FROM
(
    SELECT  DWU
    ,       max_queries
    ,       max_slots
    ,       slots_used
    ,       wg_name
    ,       tgt_mem_grant_MB
    ,       REVERSE(SUBSTRING(REVERSE(wg_names),1,CHARINDEX('_',REVERSE(wg_names),1)-1)) as up1
    ,       REVERSE(SUBSTRING(REVERSE(tgt_mem_grant_MBs),1,CHARINDEX('_',REVERSE(tgt_mem_grant_MBs),1)-1)) as up2
    ,       REVERSE(SUBSTRING(REVERSE(slots_used_all),1,CHARINDEX('_',REVERSE(slots_used_all),1)-1)) as up3
    FROM    ref AS r1
    UNPIVOT
    (
        wg_name FOR wg_names IN (wg_name_smallrc,wg_name_mediumrc,wg_name_largerc,wg_name_xlargerc,
        wg_name_staticrc10, wg_name_staticrc20, wg_name_staticrc30, wg_name_staticrc40, wg_name_staticrc50,
        wg_name_staticrc60, wg_name_staticrc70, wg_name_staticrc80)
    ) AS r2
    UNPIVOT
    (
        tgt_mem_grant_MB FOR tgt_mem_grant_MBs IN (tgt_mem_grant_MB_smallrc,tgt_mem_grant_MB_mediumrc,
        tgt_mem_grant_MB_largerc,tgt_mem_grant_MB_xlargerc, tgt_mem_grant_MB_staticrc10, tgt_mem_grant_MB_staticrc20,
        tgt_mem_grant_MB_staticrc30, tgt_mem_grant_MB_staticrc40, tgt_mem_grant_MB_staticrc50,
        tgt_mem_grant_MB_staticrc60, tgt_mem_grant_MB_staticrc70, tgt_mem_grant_MB_staticrc80)
    ) AS r3
    UNPIVOT
    (
        slots_used FOR slots_used_all IN (slots_used_smallrc,slots_used_mediumrc,slots_used_largerc,
        slots_used_xlargerc, slots_used_staticrc10, slots_used_staticrc20, slots_used_staticrc30,
        slots_used_staticrc40, slots_used_staticrc50, slots_used_staticrc60, slots_used_staticrc70,
        slots_used_staticrc80)
    ) AS r4
) a
WHERE   up1 = up2
AND     up1 = up3
;
-- Getting current info about workload groups.
WITH  
dmv  
AS  
(
  SELECT
          rp.name                                           AS rp_name
  ,       rp.max_memory_kb*1.0/1048576                      AS rp_max_mem_GB
  ,       (rp.max_memory_kb*1.0/1024)
          *(request_max_memory_grant_percent/100)           AS max_memory_grant_MB
  ,       (rp.max_memory_kb*1.0/1048576)
          *(request_max_memory_grant_percent/100)           AS max_memory_grant_GB
  ,       wg.name                                           AS wg_name
  ,       wg.importance                                     AS importance
  ,       wg.request_max_memory_grant_percent               AS request_max_memory_grant_percent
  FROM    sys.dm_pdw_nodes_resource_governor_workload_groups wg
  JOIN    sys.dm_pdw_nodes_resource_governor_resource_pools rp    ON  wg.pdw_node_id  = rp.pdw_node_id
                                                                  AND wg.pool_id      = rp.pool_id
  WHERE   rp.name = 'SloDWPool'
  GROUP BY
          rp.name
  ,       rp.max_memory_kb
  ,       wg.name
  ,       wg.importance
  ,       wg.request_max_memory_grant_percent
)
-- Creating resource class name mapping.
,names
AS
(
  SELECT 'smallrc' as resource_class, 1 as rc_id
  UNION ALL
    SELECT 'mediumrc', 2
  UNION ALL
    SELECT 'largerc', 3
  UNION ALL
    SELECT 'xlargerc', 4
  UNION ALL
    SELECT 'staticrc10', 5
  UNION ALL
    SELECT 'staticrc20', 6
  UNION ALL
    SELECT 'staticrc30', 7
  UNION ALL
    SELECT 'staticrc40', 8
  UNION ALL
    SELECT 'staticrc50', 9
  UNION ALL
    SELECT 'staticrc60', 10
  UNION ALL
    SELECT 'staticrc70', 11
  UNION ALL
    SELECT 'staticrc80', 12
)
,base AS
(   SELECT  schema_name
    ,       table_name
    ,       SUM(column_count)                   AS column_count
    ,       ISNULL(SUM(short_string_column_count),0)   AS short_string_column_count
    ,       ISNULL(SUM(long_string_column_count),0)    AS long_string_column_count
    FROM    (   SELECT  sm.name                                             AS schema_name
                ,       tb.name                                             AS table_name
                ,       COUNT(co.column_id)                                 AS column_count
                           ,       CASE    WHEN co.system_type_id IN (36,43,106,108,165,167,173,175,231,239) 
                                AND  co.max_length <= 32 
                                THEN COUNT(co.column_id) 
                        END                                                 AS short_string_column_count
                ,       CASE    WHEN co.system_type_id IN (165,167,173,175,231,239) 
                                AND  co.max_length > 32 and co.max_length <=8000
                                THEN COUNT(co.column_id) 
                        END                                                 AS long_string_column_count
                FROM    sys.schemas AS sm
                JOIN    sys.tables  AS tb   on sm.[schema_id] = tb.[schema_id]
                JOIN    sys.columns AS co   ON tb.[object_id] = co.[object_id]
                           WHERE tb.name = @TABLE_NAME AND sm.name = @SCHEMA_NAME
                GROUP BY sm.name
                ,        tb.name
                ,        co.system_type_id
                ,        co.max_length            ) a
GROUP BY schema_name
,        table_name
)
, size AS
(
SELECT  schema_name
,       table_name
,       75497472                                            AS table_overhead

,       column_count*1048576*8                              AS column_size
,       short_string_column_count*1048576*32                       AS short_string_size,       (long_string_column_count*16777216) AS long_string_size
FROM    base
UNION
SELECT CASE WHEN COUNT(*) = 0 THEN 'EMPTY' END as schema_name
         ,CASE WHEN COUNT(*) = 0 THEN 'EMPTY' END as table_name
         ,CASE WHEN COUNT(*) = 0 THEN 0 END as table_overhead
         ,CASE WHEN COUNT(*) = 0 THEN 0 END as column_size
         ,CASE WHEN COUNT(*) = 0 THEN 0 END as short_string_size

,CASE WHEN COUNT(*) = 0 THEN 0 END as long_string_size
FROM   base
)
, load_multiplier as 
(
SELECT  CASE 
                     WHEN FLOOR(8 * (CAST (@DWU_NUM AS FLOAT)/6000)) > 0 THEN FLOOR(8 * (CAST (@DWU_NUM AS FLOAT)/6000)) 
                     ELSE 1 
              END AS multipliplication_factor
) 
       SELECT  r1.DWU
       , schema_name
       , table_name
       , rc.resource_class as closest_rc_in_increasing_order
       , max_queries_at_this_rc = CASE
             WHEN (r1.max_slots / r1.slots_used > r1.max_queries)
                  THEN r1.max_queries
             ELSE r1.max_slots / r1.slots_used
                  END
       , r1.max_slots as max_concurrency_slots
       , r1.slots_used as required_slots_for_the_rc
       , r1.tgt_mem_grant_MB  as rc_mem_grant_MB
       , CAST((table_overhead*1.0+column_size+short_string_size+long_string_size)*multipliplication_factor/1048576    AS DECIMAL(18,2)) AS est_mem_grant_required_for_cci_operation_MB       
       FROM    size, load_multiplier, #ref r1, names  rc
       WHERE r1.rc_id=rc.rc_id
                     AND CAST((table_overhead*1.0+column_size+short_string_size+long_string_size)*multipliplication_factor/1048576    AS DECIMAL(18,2)) < r1.tgt_mem_grant_MB
       ORDER BY ABS(CAST((table_overhead*1.0+column_size+short_string_size+long_string_size)*multipliplication_factor/1048576    AS DECIMAL(18,2)) - r1.tgt_mem_grant_MB)
GO
```

## <a name="query-importance"></a>Importance de la requête
SQL Data Warehouse implémente des classes de ressources à l’aide de groupes de charges de travail. Il existe un total de huit groupes de charges de travail qui contrôlent le comportement de hello de classes de ressources hello sur hello différentes tailles DWU. Pour n’importe quel DWU, SQL Data Warehouse utilise quatre groupes de charges de travail de huit hello. Cela est logique car chaque groupe de charge de travail est affecté tooone de quatre classes de ressources : smallrc, mediumrc, largerc, ou xlargerc. Bonjour importance de la présentation des groupes de charges de travail hello est que certains de ces groupes de charges de travail sont définis toohigher *importance*. L’importance est utilisée pour la planification du processeur. Les requêtes exécutées avec une importance élevée obtiennent trois fois plus de cycles processeur que celles exécutées avec une importance moyenne. Ainsi, les mappages d’emplacements de concurrence déterminent également la priorité du processeur. Quand une requête utilise 16 emplacements ou plus, elle s’exécute avec une importance élevée.

Hello tableau suivant montre les mappages d’importance hello pour chaque groupe de charges de travail.

### <a name="workload-group-mappings-tooconcurrency-slots-and-importance"></a>Importance et les emplacements de la charge de travail groupe mappages tooconcurrency
| Groupes de charges de travail | Mappage d’emplacement de concurrence | Mo / Distribution | Mappage d’importance |
|:--- |:---:|:---:|:--- |
| SloDWGroupC00 |1 |100 |Moyenne |
| SloDWGroupC01 |2 |200 |Moyenne |
| SloDWGroupC02 |4 |400 |Moyenne |
| SloDWGroupC03 |8 |800 |Moyenne |
| SloDWGroupC04 |16 |1 600 |Élevé |
| SloDWGroupC05 |32 |3 200 |Élevé |
| SloDWGroupC06 |64 |6 400 |Élevé |
| SloDWGroupC07 |128 |12 800 |Élevé |

À partir de hello **Allocation et la consommation d’emplacements de concurrence** graphique, vous pouvez constater qu’un DW500 utilise 1, 4, 8 ou les emplacements d’accès concurrentiel 16 pour smallrc, mediumrc, largerc et xlargerc, respectivement. Vous pouvez rechercher ces valeurs Bonjour précédant l’importance de hello toofind graphique pour chaque classe de ressource.

### <a name="dw500-mapping-of-resource-classes-tooimportance"></a>Mappage de DW500 de tooimportance de classes de ressources
| classe de ressources | Groupe de charges de travail | Emplacements de concurrence utilisés | Mo / Distribution | importance |
|:--- |:--- |:---:|:---:|:--- |
| smallrc |SloDWGroupC00 |1 |100 |Moyenne |
| mediumrc |SloDWGroupC02 |4 |400 |Moyenne |
| largerc |SloDWGroupC03 |8 |800 |Moyenne |
| xlargerc |SloDWGroupC04 |16 |1 600 |Élevé |
| staticrc10 |SloDWGroupC00 |1 |100 |Moyenne |
| staticrc20 |SloDWGroupC01 |2 |200 |Moyenne |
| staticrc30 |SloDWGroupC02 |4 |400 |Moyenne |
| staticrc40 |SloDWGroupC03 |8 |800 |Moyenne |
| staticrc50 |SloDWGroupC03 |16 |1 600 |Élevé |
| staticrc60 |SloDWGroupC03 |16 |1 600 |Élevé |
| staticrc70 |SloDWGroupC03 |16 |1 600 |Élevé |
| staticrc80 |SloDWGroupC03 |16 |1 600 |Élevé |

Vous pouvez utiliser hello suivant toolook de requête DMV différences hello dans l’allocation des ressources mémoire en détail à partir de la perspective hello du gouverneur de ressources hello ou tooanalyze actives et historiques d’utilisation des groupes de charges de travail hello lors du dépannage.

```sql
WITH rg
AS
(   SELECT  
     pn.name                        AS node_name
    ,pn.[type]                        AS node_type
    ,pn.pdw_node_id                    AS node_id
    ,rp.name                        AS pool_name
    ,rp.max_memory_kb*1.0/1024                AS pool_max_mem_MB
    ,wg.name                        AS group_name
    ,wg.importance                    AS group_importance
    ,wg.request_max_memory_grant_percent        AS group_request_max_memory_grant_pcnt
    ,wg.max_dop                        AS group_max_dop
    ,wg.effective_max_dop                AS group_effective_max_dop
    ,wg.total_request_count                AS group_total_request_count
    ,wg.total_queued_request_count            AS group_total_queued_request_count
    ,wg.active_request_count                AS group_active_request_count
    ,wg.queued_request_count                AS group_queued_request_count
    FROM    sys.dm_pdw_nodes_resource_governor_workload_groups wg
    JOIN    sys.dm_pdw_nodes_resource_governor_resource_pools rp    
            ON  wg.pdw_node_id  = rp.pdw_node_id
            AND wg.pool_id      = rp.pool_id
    JOIN    sys.dm_pdw_nodes pn
            ON    wg.pdw_node_id    = pn.pdw_node_id
    WHERE   wg.name like 'SloDWGroup%'
        AND     rp.name = 'SloDWPool'
)
SELECT    pool_name
,        pool_max_mem_MB
,        group_name
,        group_importance
,        (pool_max_mem_MB/100)*group_request_max_memory_grant_pcnt AS max_memory_grant_MB
,        node_name
,        node_type
,       group_total_request_count
,       group_total_queued_request_count
,       group_active_request_count
,       group_queued_request_count
FROM    rg
ORDER BY
    node_name
,    group_request_max_memory_grant_pcnt
,    group_importance
;
```

## <a name="queries-that-honor-concurrency-limits"></a>Requêtes qui honorent les limites de concurrence
La plupart des requêtes sont régies par des classes de ressource. Ces requêtes doivent tenir à l’intérieur de requêtes simultanées hello et seuils d’emplacement d’accès concurrentiel. Un utilisateur ne peut pas choisir tooexclude une requête à partir du modèle d’emplacement hello d’accès concurrentiel.

tooreiterate, hello classes de ressources d’honorer les instructions suivantes :

* INSERT-SELECT
* UPDATE
* SUPPRIMER
* SELECT (lors de l’interrogation des tables d’utilisateur)
* ALTER INDEX REBUILD
* ALTER INDEX REORGANIZE
* ALTER TABLE REBUILD
* CREATE INDEX
* CREATE CLUSTERED COLUMNSTORE INDEX
* CREATE TABLE AS SELECT (CTAS)
* Chargement de données
* Opérations de déplacement de données effectuées par hello Service de déplacement des données (DMS)

## <a name="query-exceptions-tooconcurrency-limits"></a>Requête exceptions tooconcurrency limites
Certaines requêtes ne tiennent pas compte des ressources de hello classe toowhich hello utilisateur est affecté. Ces exceptions toohello les limites d’accès concurrentiel sont effectuées lorsque hello des ressources nécessaires pour une commande particulière est faible, souvent parce que la commande hello est une opération de métadonnées. Hello ces exceptions vise tooavoid les allocations de mémoire supérieure pour les requêtes qui n’auront jamais besoin les. Dans ces cas, hello par défaut de la classe de ressource le plus petit (smallrc) est toujours utilisé, quelle que soit la classe attribué toohello utilisateur hello ressource réelle. Par exemple, `CREATE LOGIN` s’exécute toujours dans smallrc. Hello ressources requises toofulfill cette opération étant très faible, il n’effectue aucune requête de sens tooinclude hello dans le modèle d’emplacement hello d’accès concurrentiel.  Également ces requêtes ne sont pas limités par limite de hello 32 utilisateur d’accès concurrentiel, limite de la session toohello de 1 024 sessions peut exécuter un nombre illimité de ces requêtes.

suivant les instructions de Hello n’honorent pas ces classes de ressources :

* CREATE ou DROP TABLE
* ALTER TABLE ... SWITCH, SPLIT ou MERGE PARTITION
* ALTER INDEX DISABLE
* DROP INDEX
* CREATE, UPDATE ou DROP STATISTICS
* TRUNCATE TABLE
* ALTER AUTHORIZATION
* CREATE LOGIN
* CREATE, ALTER ou DROP USER
* CREATE, ALTER ou DROP PROCEDURE
* CREATE ou DROP VIEW
* INSERT VALUES
* SELECT à partir des affichages système et des DMV
* EXPLAIN
* DBCC

<!--
Removed as these two are not confirmed / supported under SQLDW
- CREATE REMOTE TABLE AS SELECT
- CREATE EXTERNAL TABLE AS SELECT
- REDISTRIBUTE
-->

##  <a name="changing-user-resource-class-example"></a> Exemple de modification d’une classe de ressources utilisateur
1. **Créer une connexion :** ouvrir une connexion tooyour **master** hello serveur SQL Server hébergeant la base de données de l’entrepôt de données SQL de base de données et exécutez hello suivant les commandes.
   
    ```sql
    CREATE LOGIN newperson WITH PASSWORD = 'mypassword';
    CREATE USER newperson for LOGIN newperson;
    ```
   
   > [!NOTE]
   > Il est une bonne idée de toocreate un utilisateur dans la base de données master hello pour les utilisateurs d’Azure SQL Data Warehouse. Création d’un utilisateur dans master permet une toologin d’utilisateur à l’aide des outils tels que SSMS sans spécifier un nom de base de données.  Cela leur permet également toouse hello objet explorer tooview toutes les bases de données sur un serveur SQL server.  Pour plus d’informations sur la création et la gestion des utilisateurs, consultez [Sécuriser une base de données dans SQL Data Warehouse][Secure a database in SQL Data Warehouse].
   > 
   > 
2. **Créer un utilisateur de l’entrepôt de données SQL :** ouvrir une connexion toohello **SQL Data Warehouse** de base de données et exécutez hello commande suivante.
   
    ```sql
    CREATE USER newperson FOR LOGIN newperson;
    ```
3. **Accorder des autorisations :** hello suivant accorde de l’exemple `CONTROL` sur hello **SQL Data Warehouse** base de données. `CONTROL`à hello au niveau de la base de données est hello équivalent db_owner dans SQL Server.
   
    ```sql
    GRANT CONTROL ON DATABASE::MySQLDW toonewperson;
    ```
4. **Augmenter la classe de ressource :** tooadd de requête suivante de hello d’utiliser un rôle de gestion de la charge de travail supérieure utilisateur tooa.
   
    ```sql
    EXEC sp_addrolemember 'largerc', 'newperson'
    ```
5. **Diminuer la classe de ressource :** tooremove de requête suivante de hello d’utiliser un utilisateur à partir d’un rôle de gestion de la charge de travail.
   
    ```sql
    EXEC sp_droprolemember 'largerc', 'newperson';
    ```
   
   > [!NOTE]
   > Il n’est pas possible de tooremove un utilisateur à partir de smallrc.
   > 
   > 

## <a name="queued-query-detection-and-other-dmvs"></a>Détection des requêtes en file d’attente et autres vues de gestion dynamique
Vous pouvez utiliser hello `sys.dm_pdw_exec_requests` requêtes DMV tooidentify qui sont en attente dans une file d’attente d’accès concurrentiel. Les requêtes en attente pour un emplacement de concurrence auront le statut **suspendu**.

```sql
SELECT      r.[request_id]                 AS Request_ID
        ,r.[status]                 AS Request_Status
        ,r.[submit_time]             AS Request_SubmitTime
        ,r.[start_time]                 AS Request_StartTime
        ,DATEDIFF(ms,[submit_time],[start_time]) AS Request_InitiateDuration_ms
        ,r.resource_class                         AS Request_resource_class
FROM    sys.dm_pdw_exec_requests r;
```

Vous pouvez afficher les rôles de gestion des charges de travail avec `sys.database_principals`.

```sql
SELECT  ro.[name]           AS [db_role_name]
FROM    sys.database_principals ro
WHERE   ro.[type_desc]      = 'DATABASE_ROLE'
AND     ro.[is_fixed_role]  = 0;
```

Hello suivant la requête indique quel rôle est affecté à chaque utilisateur.

```sql
SELECT     r.name AS role_principal_name
        ,m.name AS member_principal_name
FROM    sys.database_role_members rm
JOIN    sys.database_principals AS r            ON rm.role_principal_id        = r.principal_id
JOIN    sys.database_principals AS m            ON rm.member_principal_id    = m.principal_id
WHERE    r.name IN ('mediumrc','largerc', 'xlargerc');
```

SQL Data Warehouse a hello suivante de types d’attente :

* **LocalQueriesConcurrencyResourceType**: les requêtes qui se trouvent en dehors de l’infrastructure d’emplacement hello d’accès concurrentiel. Les requêtes DMV et les fonctions système telles que `SELECT @@VERSION` sont des exemples de requête locale.
* **UserConcurrencyResourceType**: les requêtes qui se trouvent à l’intérieur d’infrastructure d’emplacement hello d’accès concurrentiel. Les requêtes exécutées sur des tables d’utilisateurs finaux sont des exemples de requêtes qui doivent utiliser ce type de ressource.
* **DmsConcurrencyResourceType**: attentes résultant d’opérations de déplacement de données.
* **BackupConcurrencyResourceType**: cette attente indique qu’une base de données est en cours de sauvegarde. valeur maximale de Hello pour ce type de ressource est 1. Si plusieurs sauvegardes ont été demandés au hello simultanément, hello d’autres file d’attente.

Hello `sys.dm_pdw_waits` DMV peut être utilisé toosee les ressources auxquelles une demande en attente pour.

```sql
SELECT  w.[wait_id]
,       w.[session_id]
,       w.[type]            AS Wait_type
,       w.[object_type]
,       w.[object_name]
,       w.[request_id]
,       w.[request_time]
,       w.[acquire_time]
,       w.[state]
,       w.[priority]
,    SESSION_ID()            AS Current_session
,    s.[status]            AS Session_status
,    s.[login_name]
,    s.[query_count]
,    s.[client_id]
,    s.[sql_spid]
,    r.[command]            AS Request_command
,    r.[label]
,    r.[status]            AS Request_status
,    r.[submit_time]
,    r.[start_time]
,    r.[end_compile_time]
,    r.[end_time]
,    DATEDIFF(ms,r.[submit_time],r.[start_time])        AS Request_queue_time_ms
,    DATEDIFF(ms,r.[start_time],r.[end_compile_time])    AS Request_compile_time_ms
,    DATEDIFF(ms,r.[end_compile_time],r.[end_time])        AS Request_execution_time_ms
,    r.[total_elapsed_time]
FROM    sys.dm_pdw_waits w
JOIN    sys.dm_pdw_exec_sessions s  ON w.[session_id] = s.[session_id]
JOIN    sys.dm_pdw_exec_requests r  ON w.[request_id] = r.[request_id]
WHERE    w.[session_id] <> SESSION_ID();
```

Hello `sys.dm_pdw_resource_waits` DMV affiche uniquement les attentes de ressources hello consommées par une requête donnée. Temps d’attente de ressources mesure uniquement le temps de hello en attente de toobe de ressources fourni, comme toosignal opposé délai, qui est le temps de hello nécessaire pour hello sous-jacent serveurs tooschedule hello la requête SQL sur les UC hello.

```sql
SELECT  [session_id]
,       [type]
,       [object_type]
,       [object_name]
,       [request_id]
,       [request_time]
,       [acquire_time]
,       DATEDIFF(ms,[request_time],[acquire_time])  AS acquire_duration_ms
,       [concurrency_slots_used]                    AS concurrency_slots_reserved
,       [resource_class]
,       [wait_id]                                   AS queue_position
FROM    sys.dm_pdw_resource_waits
WHERE    [session_id] <> SESSION_ID();
```

Hello `sys.dm_pdw_wait_stats` DMV peut être utilisé pour l’analyse des tendances historiques d’attentes.

```sql
SELECT    w.[pdw_node_id]
,        w.[wait_name]
,        w.[max_wait_time]
,        w.[request_count]
,        w.[signal_time]
,        w.[completed_count]
,        w.[wait_time]
FROM    sys.dm_pdw_wait_stats w;
```

## <a name="next-steps"></a>Étapes suivantes
Pour plus d’informations sur la gestion de la sécurité et des utilisateurs de base de données, consultez [Sécuriser une base de données dans SQL Data Warehouse][Secure a database in SQL Data Warehouse]. Pour plus d’informations sur les classes de ressources la plus grande peut améliorer la qualité d’index cluster columnstore, consultez [la reconstruction de qualité de segment index tooimprove].

<!--Image references-->

<!--Article references-->
[Secure a database in SQL Data Warehouse]: ./sql-data-warehouse-overview-manage-security.md
[la reconstruction de qualité de segment index tooimprove]: ./sql-data-warehouse-tables-index.md#rebuilding-indexes-to-improve-segment-quality
[Secure a database in SQL Data Warehouse]: ./sql-data-warehouse-overview-manage-security.md

<!--MSDN references-->
[Managing Databases and Logins in Azure SQL Database]:https://msdn.microsoft.com/library/azure/ee336235.aspx

<!--Other Web references-->
