---
title: pratiques aaaBest pour Azure SQL Data Warehouse | Documents Microsoft
description: "Recommandations et meilleures pratiques que vous devez connaître pour développer des solutions pour Azure SQL Data Warehouse. Elles vous aideront à réussir."
services: sql-data-warehouse
documentationcenter: NA
author: shivaniguptamsft
manager: jhubbard
editor: 
ms.assetid: 7b698cad-b152-4d33-97f5-5155dfa60f79
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: performance
ms.date: 10/31/2016
ms.author: shigu;barbkess
ms.openlocfilehash: 1f42908fc03e1ca52278a6853d1afe9543d648b7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="best-practices-for-azure-sql-data-warehouse"></a>Meilleures pratiques pour Azure SQL Data Warehouse
Cet article est une collection de nombreuses pratiques recommandées qui vous permettra de tooachieve des performances optimales de votre entrepôt de données SQL Azure.  Certains des concepts hello dans cet article sont tooexplain simple et de base, autres concepts sont plus avancées et nous scratch simplement la surface de hello dans cet article.  Hello cet article vise toogive vous certains horaires des instructions et tooraise base de toofocus est essentiel que vous générez votre entrepôt de données.  Chaque section présente tooa concept et point puis toomore détaillée articles notion hello garde de manière plus approfondie.

Si vous êtes novice avec Azure SQL Data Warehouse, ne laissez pas cet article vous submerger.  séquence de Hello des rubriques de hello est principalement par ordre de hello d’importance.  Si vous démarrez en se concentrant sur hello tout d’abord quelques concepts, vous serez en bonne voie.  Dès que vous vous sentirez plus à l’aise avec SQL Data Warehouse, vous pourrez revenir consulter d’autres concepts.  Peu de long pour tout toomake sens.

## <a name="reduce-cost-with-pause-and-scale"></a>Réduire les coûts avec les opérations de suspension et de mise à l’échelle
Une fonctionnalité clé de l’entrepôt de données SQL est hello capacité toopause lorsque vous n’utilisez pas, ce qui arrête la facturation hello des ressources de calcul.  Une autre fonctionnalité de clé est ressources de tooscale possibilité hello.  Suspension et la mise à l’échelle est possible via hello portail Azure ou de commandes PowerShell.  Vous familiariser avec ces fonctionnalités car elle peuvent réduire considérablement les coûts hello de votre entrepôt de données lorsqu’il n’est pas en cours d’utilisation.  Si vous souhaitez toujours votre entrepôt de données accessible, vous souhaiterez tooconsider il mise à l’échelle vers le bas toohello plus petite taille, un DW100 plutôt que de la suspension.

Voir aussi [Interrompre des ressources de calcul][Pause compute resources], [Reprendre des ressources de calcul][Resume compute resources], [Mettre à l’échelle des ressources de calcul].

## <a name="drain-transactions-before-pausing-or-scaling"></a>Vider les transactions avant la suspension ou la mise à l’échelle
Lorsque vous suspendez ou mettre à l’échelle de votre entrepôt de données SQL, coulisses hello que vos requêtes sont annulées lorsque vous lancez hello suspendre ou mettre à l’échelle de demande.  L’annulation d’une requête SELECT simple est une opération rapide et n’a quasiment aucun impact toohello temps toopause ou mettre à l’échelle de votre instance.  Toutefois, des requêtes transactionnelles, modifiez votre structure de données ou hello des données de hello, peut-être pas en mesure de toostop rapidement.  **Par définition, les requêtes transactionnelles doivent être terminées dans leur intégralité ou annuler leurs modifications.**  Annulant hello le travail effectué par une requête transactionnelle peut prendre longtemps, ou même plus, les modifications d’origine hello hello requête a été appliquer.  Par exemple, si vous annulez une requête qui a été suppression de lignes et a déjà été exécuté pendant une heure, il pourrait prendre hello système une heure tooinsert hello différé les lignes qui ont été supprimés.  Si vous exécutez la pause ou la mise à l’échelle pendant que les transactions sont en cours, votre pause ou la mise à l’échelle peut sembler tootake beaucoup de temps a, car la suspension et la mise à l’échelle les toowait pour hello rollback toocomplete avant de pouvoir procéder.

Voir aussi [Transactions][Understanding transactions], [Optimisation des transactions][Optimizing transactions]

## <a name="maintain-statistics"></a>Mettre à jour les statistiques
Contrairement à SQL Server, qui détecte et crée ou met à jour les statistiques automatiquement dans les colonnes, SQL Data Warehouse nécessite une maintenance manuelle des statistiques.  Pendant que nous envisagez toochange cela Bonjour futur, pour maintenant vous pouvez toomaintain votre tooensure des statistiques qui hello SQL Data Warehouse plans sont optimisées.  plans de Hello créés par l’optimiseur de hello ne sont pas aussi bien que les statistiques disponibles hello.  **Les statistiques échantillonnées sur chaque colonne est un moyen simple de tooget début de la création des statistiques.**  Il est tout aussi important tooupdate statistiques comme des modifications importantes produisent tooyour données.  Une méthode plus classique est peut-être tooupdate vos statistiques tous les jours ou après chaque charge.  Il existe toujours un compromis entre performances et hello coût toocreate et mise à jour des statistiques. Si vous trouvez que cela prend trop de temps toomaintain toutes vos statistiques, vous souhaiterez peut-être toobe tootry plus sélective sur les colonnes qui possèdent des statistiques ou les colonnes doive souvent mises à jour.  Par exemple, vous pourriez tooupdate des colonnes de date, où les nouvelles valeurs peuvent être ajouté, quotidienne. **Vous bénéficierez hello plus avantageux en ayant des statistiques sur des colonnes impliquées dans les jointures, les colonnes utilisées dans hello où clause et colonnes trouvent dans GROUP BY.**

Voir aussi [Gestion des statistiques sur les tables][Manage table statistics], [CREATE STATISTICS][CREATE STATISTICS], [UPDATE STATISTICS][UPDATE STATISTICS]

## <a name="group-insert-statements-into-batches"></a>Regrouper des instructions INSERT dans des lots
Une charge unique tooa petite table avec une instruction INSERT ou même un rechargement périodique d’une recherche peut effectuer parfaitement à vos besoins à l’aide d’une instruction comme `INSERT INTO MyLookup VALUES (1, 'Type 1')`.  Toutefois, si vous devez tooload des milliers, voire des millions de lignes journée hello, vous constaterez que les insertions de singleton ne peut pas suivre.  Au lieu de cela, développer vos processus afin qu’ils écrivent tooa fichier et un autre processus arrive régulièrement et charge de ce fichier.

Voir aussi [INSERT][INSERT]

## <a name="use-polybase-tooload-and-export-data-quickly"></a>Utilisez PolyBase tooload et exporter des données rapidement
SQL Data Warehouse prend en charge le chargement et l’exportation de données via plusieurs outils dont Azure Data Factory, PolyBase et BCP.  Pour les petits volumes de données où les performances ne sont pas essentielles, n’importe quel outil peut suffire à vos besoins.  Toutefois, lorsque vous chargez ou exportation de grands volumes de données ou des performances rapides sont nécessaire, PolyBase est hello meilleur choix.  PolyBase est conçue tooleverage hello MPP (massivement le traitement parallèle) architecture de l’entrepôt de données SQL et par conséquent, charge et exporter des grandeurs importantes de données plus rapidement que n’importe quel autre outil.  Les charges PolyBase peuvent être exécutées à l’aide de CTAS ou d’INSERT INTO.  **À l’aide de SACT permet de minimiser la journalisation des transactions et tooload de manière plus rapide hello vos données.**  Azure Data Factory prend également en charge les charges PolyBase.  PolyBase prend en charge une variété de formats de fichiers, y compris les fichiers Gzip.  **débit de toomaximize lors de l’utilisation de gzip fichiers texte, saut au moins 60 parallélisme toomaximize de fichiers de votre charge.**  Pour un débit total plus rapide, envisagez le chargement simultané des données.

Consultez aussi [Chargement de données][Load data], [Guide d’utilisation de PolyBase][Guide for using PolyBase], [Modèles et stratégies de chargement Azure SQL Data Warehouse][Azure SQL Data Warehouse loading patterns and strategies], [Téléchargement de données avec Azure Data Factory][Load Data with Azure Data Factory], [Déplacer des données à l’aide d’Azure Data Factory][Move data with Azure Data Factory], [CREATE EXTERNAL FILE FORMAT][CREATE EXTERNAL FILE FORMAT], [Create table as select (CTAS)][Create table as select (CTAS)]

## <a name="load-then-query-external-tables"></a>Charger, puis interroger les tables externes
Polybase, également connu sous le nom des tables externes, peut être hello plus rapide des tooload données, il n’est pas optimal pour les requêtes. Les tables SQL Data Warehouse Polybase ne prennent actuellement en charge que les fichiers d’objets blob Azure. Aucune ressource de calcul ne se charge de la sauvegarde de ces fichiers.  Par conséquent, l’entrepôt de données SQL ne peut pas déléguer ce travail et par conséquent doit lire un fichier entier de hello en le chargeant tootempdb données de commandes tooread hello.  Si vous avez plusieurs requêtes demandera ces données, il est donc une meilleure tooload ces données qu’une seule fois et utilisent des requêtes de table locale de hello.

Voir aussi [Guide d’utilisation de PolyBase][Guide for using PolyBase]

## <a name="hash-distribute-large-tables"></a>Hacher et distribuer de grandes tables
Par défaut, les tables sont distribuées par tourniquet (Round Robin).  Cela facilite pour tooget les utilisateurs en main la création de tables sans avoir toodecide comment leurs tables doivent être distribués.  Les tables distribuées par tourniquet (Round Robin) peuvent offrir des performances suffisantes pour certaines charges de travail, mais souvent la sélection d’une colonne de distribution s’avérera plus efficace.  Hello exemple le plus courant lorsqu’une table distribuée par une colonne sera surpassent présent une table de tourniquet (Round Robin) est lorsque deux grandes tables de faits sont joints.  Par exemple, si vous avez une table orders, qui est distribuée par order_id, et une table de transactions, qui est également distribuée par order_id, lorsque vous joignez votre table de transactions de commandes table tooyour sur order_id, cette requête est une requête directe, ce qui signifie que éliminer les opérations de déplacement de données.  Moins d’étapes signifie une requête plus rapide.  Moins de déplacement des données permet également d’obtenir des requêtes plus rapides.  Cette explication simplement Survoler hello. Lors du chargement d’une table distribuée, veillez à ce que vos données entrantes ne sont pas triées sur la clé de répartition hello car cela risque de ralentir votre charge.  Consultez hello ci-dessous de liens pour beaucoup plus de détails sur la sélection d’une colonne de distribution peut améliorer les performances et la manière toodefine une table distribuée dans la clause WITH de hello de votre instruction de créer des TABLES.

Voir aussi [Vue d’ensemble des tables][Table overview], [Distribution de tables][Table distribution], [Sélection d’une distribution de tables][Selecting table distribution], [CREATE TABLE][CREATE TABLE], [CREATE TABLE AS SELECT][CREATE TABLE AS SELECT]

## <a name="do-not-over-partition"></a>Ne pas créer trop de partitions
Bien que le partitionnement des données peut être très efficace pour mettre à jour vos données grâce au basculement de partitions ou à l’optimisation des analyses avec élimination de partition, avoir un trop grand nombre de partitions peut ralentir vos requêtes.  Souvent une stratégie de partitionnement à granularité élevée qui peut fonctionner correctement sur SQL Server peut poser des problèmes sur SQL Data Warehouse.  Ces trop nombreuses partitions peut également réduire l’efficacité des index columnstore en cluster hello si chaque partition possède moins de 1 million de lignes.  N’oubliez pas que coulisses de hello, SQL Data Warehouse partitionne vos données pour vous en 60 bases de données, donc si vous créez une table avec 100 partitions, cela entraîne en fait 6000 partitions.  Chaque charge de travail étant différents conseils hello est tooexperiment avec le partitionnement toosee mieux adaptée à votre charge de travail.  Envisagez d’abaisser le niveau de granularité à un niveau inférieur à celui qui a fonctionné pour vous dans SQL Server.  Par exemple, utilisez plutôt des partitions hebdomadaires ou mensuelles plutôt que des partitions quotidiennes.

Voir aussi [Partitionnement de table][Table partitioning]

## <a name="minimize-transaction-sizes"></a>Minimiser la taille des transactions
Les instructions INSERT, UPDATE et DELETE s’exécutent dans une transaction, et en cas d’échec elles doivent être restaurées.  hello toominimize potentiel pour une restauration long, réduire des tailles de transaction chaque fois que possible.  Pour ce faire, vous pouvez diviser les instructions INSERT, UPDATE et DELETE en plusieurs parties.  Par exemple, si vous disposez d’une instruction INSERT qui attendent tootake 1 heure, si possible, décomposent hello INSERT en 4 parties, qui seront exécutera dans les 15 minutes.  Tirer parti des cas spéciaux une journalisation minimale, telles que SACT, TRUNCATE, DROP TABLE ou INSERT tooempty tables, risque de restauration tooreduce.  Restaurations de tooeliminate un autre moyen est toouse métadonnées que les opérations comme le basculement de partition pour la gestion des données.  Par exemple, plutôt que d’exécuter un toodelete d’instruction de suppression de toutes les lignes dans une table où hello order_date était en octobre 2001, vous pouvez partitionner vos données mensuelles et puis extraire une partition de hello avec des données pour une partition vide à partir d’une autre table (voir ALTER Exemples TABLE).  Pour les tables non partitionnés envisagez à l’aide d’une SACT toowrite hello données tookeep dans une table plutôt que de l’utilisation de DELETE.  Si un SACT prend hello même intervalle de temps, il s’agit d’un toorun opération beaucoup plus sûre car elle a la journalisation des transactions très peu et peut être annulé rapidement si nécessaire.

Voir aussi [Transactions][Understanding transactions], [Optimisation des transactions][Optimizing transactions], [Partitionnement de table][Table partitioning], [TRUNCATE TABLE][TRUNCATE TABLE], [ALTER TABLE][ALTER TABLE], [Create table as select (CTAS)][Create table as select (CTAS)]

## <a name="use-hello-smallest-possible-column-size"></a>Utilisez la plus petite taille de colonne possibles hello
Lorsque vous définissez votre commande DDL, à l’aide de hello plus petit type de données qui prend en charge vos données améliore les performances de requête.  Ceci est particulièrement important pour les colonnes CHAR et VARCHAR.  Si la valeur la plus longue hello dans une colonne est de 25 caractères, puis définissez la colonne en tant que VARCHAR(25).  Évitez de définir toutes les colonnes tooa élevée par défaut de caractères.  En outre, définissez des colonnes VARCHAR lorsque cela suffit, au lieu d’utiliser NVARCHAR.

Voir aussi [Vue d’ensemble des tables][Table overview], [Types de données des tables][Table data types], [CREATE TABLE][CREATE TABLE]

## <a name="use-temporary-heap-tables-for-transient-data"></a>Utiliser des tables de segments de mémoire temporaires pour les données temporaires
Lorsque vous sont temporairement lancement des données sur SQL Data Warehouse, vous découvrirez peut-être qu’à l’aide d’une table de segment de mémoire effectue hello processus global plus rapidement.  Si vous chargez toostage uniquement de données il avant d’exécuter d’autres transformations, le chargement hello table tooheap de la table sera beaucoup plus rapide que le chargement de hello données tooa en cluster de table columnstore.  En outre, le chargement des données tooa table temporaire est également chargés beaucoup plus rapidement que le chargement d’un stockage de toopermanent de table.  Tables temporaires commencent par un « # » et sont accessibles uniquement par session hello qui l’a créé, afin qu’ils ne peuvent fonctionner dans certains scénarios limités.   Tables de segment de mémoire sont définis dans la clause WITH de hello d’une instruction CREATE TABLE.  Si vous utilisez une table temporaire, n’oubliez pas la toocreate des statistiques sur la table temporaire trop.

Voir aussi [Tables temporaires][Temporary tables], [CREATE TABLE][CREATE TABLE], [CREATE TABLE AS SELECT][CREATE TABLE AS SELECT]

## <a name="optimize-clustered-columnstore-tables"></a>Optimiser les tables columnstore en clusters
Index columnstore cluster constituent l’une des méthodes plus efficaces de hello que vous pouvez stocker vos données dans l’entrepôt de données SQL Azure.  Par défaut, les tables dans SQL Data Warehouse sont créées en tant que ColumnStore en cluster.  tooget hello meilleures performances pour les requêtes sur les tables columnstore, ayant la qualité de la bonne segment sont important.  Lors de l’écriture des lignes dans les tables toocolumnstore sollicitation de la mémoire, qualité de segment columnstore risquent d’en pâtir.  La qualité du segment peut être mesurée par le nombre de lignes dans un groupe de lignes compressé.  Consultez hello [Causes de columnstore une mauvaise qualité d’index] [ Causes of poor columnstore index quality] Bonjour [index de Table] [ Table indexes] sur l’article pour obtenir des instructions étape par étape détection et améliorer la qualité de segment pour les tables columnstore en cluster.  Étant donné que les segments de columnstore de haute qualité est important, il est une bonne idée toouse utilisateurs les ID qui se trouvent dans la classe de ressource moyenne ou grande hello pour charger les données.  Bonjour moins Dwu vous utilisez, hello plus grande hello classe de ressource souhaité tooyour tooassign chargement utilisateur.

Étant donné que les tables columnstore généralement ne sera pas transmettre des données à un segment columnstore compressée jusqu'à ce qu’il existe plus de 1 million de lignes par table et chaque table de l’entrepôt de données SQL est partitionnée en 60 tables, en règle générale, les tables columnstore ne tireront une requête sauf si la table de hello a plus de 60 millions de lignes.  Pour les tables avec moins de 60 millions de lignes, peut ne pas se toohave de n’importe quel sens un index columnstore.  Mais cela ne peut pas nuire non plus.  En outre, si vous partitionnez vos données, puis vous pouvez tooconsider que chaque partition aura besoin toobenefit de lignes de 1 million de toohave à partir d’un index cluster columnstore.  Si une table a 100 partitions, vous devez toobenefit de lignes toohave au moins 6 milliards d’un magasin de colonnes en cluster (60 distributions * 100 partitions * 1 million de lignes).  Si votre table ne possède pas de 6 milliards de lignes dans cet exemple, réduisez le nombre hello de partitions ou envisagez d’utiliser une table de segment de mémoire à la place.  Il peut également être utile que vous testiez toosee si améliorer les performances peuvent être obtenues avec une table de segment de mémoire avec les index secondaires, plutôt qu’une table columnstore.  Les tables columnstore ne gèrent pas encore les index secondaires.

Lorsque vous interrogez une table columnstore, les requêtes sont exécutées plus rapidement si vous sélectionnez uniquement les colonnes hello que nécessaires.  

Voir aussi [Index de table][Table indexes], [Guide des index columnstore][Columnstore indexes guide], [Reconstruction des index columnstore][Rebuilding columnstore indexes]

## <a name="use-larger-resource-class-tooimprove-query-performance"></a>Utilisez la plus grande classe tooimprove requête des performances des ressources
SQL Data Warehouse utilise des groupes de ressources comme une tooqueries de mémoire de façon tooallocate.  En dehors de la zone de hello, tous les utilisateurs sont affectés de classe de ressource le plus petit toohello qui accorde à 100 Mo de mémoire par la distribution.  Dans la mesure où il existe toujours des 60 distributions et chaque point de distribution a un minimum de 100 Mo, mémoire totale du large hello système allocation est 6 000 Mo, ou simplement sous 6 Go.  Certaines requêtes, telles que les jointures de grandes ou charges tooclustered columnstore tables, l’avantage d’allocations de mémoire supérieure.  Certaines requêtes, comme les analyses pures, ne tireront aucun avantage.  Côté hello retourner, utilisant des classes de ressources supérieure a un impact sur concurrence, : vous devrez tootake cela en considération avant de passer tous les de votre classe de ressources volumineux tooa les utilisateurs.

Voir aussi [Gestion de la concurrence et des charges de travail][Concurrency and workload management]

## <a name="use-smaller-resource-class-tooincrease-concurrency"></a>Utiliser la classe de ressource plus petits tooIncrease d’accès concurrentiel
Si vous constatez que les requêtes utilisateur semblent toohave un long délai, il peut s’agir que vos utilisateurs sont en cours d’exécution dans les classes de ressources plus volumineux et consomment un grand nombre d’emplacements d’accès concurrentiel à l’origine des autres tooqueue requêtes des.  toosee si les requêtes des utilisateurs sont en attente, exécutez `SELECT * FROM sys.dm_pdw_waits` toosee si toutes les lignes sont retournées.

Voir aussi [Gestion de la concurrence et des charges de travail][Concurrency and workload management], [sys.dm_pdw_waits][sys.dm_pdw_waits]

## <a name="use-dmvs-toomonitor-and-optimize-your-queries"></a>Utilisez les vues de gestion dynamique toomonitor et optimiser vos requêtes
SQL Data Warehouse a plusieurs vues de gestion dynamique qui peuvent être utilisé toomonitor l’exécution des requêtes.  Hello analyse article ci-dessous décrit des instructions détaillées sur la façon dont toolook détails hello d’une exécution de requête.  tooquickly des requêtes de recherche dans ces vues DMV, option d’étiquette hello vos requêtes peuvent aider à.

Voir aussi [Surveiller votre charge de travail à l’aide de vues de gestion dynamique][Monitor your workload using DMVs], [LABEL][LABEL], [OPTION][OPTION], [sys.dm_exec_sessions][sys.dm_exec_sessions], [sys.dm_pdw_exec_requests][sys.dm_pdw_exec_requests], [sys.dm_pdw_request_steps][sys.dm_pdw_request_steps], [sys.dm_pdw_sql_requests][sys.dm_pdw_sql_requests], [sys.dm_pdw_dms_workers], [DBCC PDW_SHOWEXECUTIONPLAN][DBCC PDW_SHOWEXECUTIONPLAN], [sys.dm_pdw_waits][sys.dm_pdw_waits]

## <a name="other-resources"></a>Autres ressources
Consultez également notre article [Dépannage][Troubleshooting] concernant les problèmes courants et leurs solutions.

Si vous ne trouvez pas ce que vous recherchiez dans cet article, essayez d’utiliser hello « Recherche des documents » sur le côté gauche de hello de cette page de toosearch tous les de documents Azure SQL Data Warehouse de salutation.  Hello [Forum MSDN l’entrepôt de données de SQL Azure] [ Azure SQL Data Warehouse MSDN Forum] a été créer comme emplacement pour vous tooask questions tooother utilisateurs et toohello groupe de produits de l’entrepôt de données SQL.  Nous suivons activement cette tooensure forum que vos questions sont traitées par un autre utilisateur ou de nous.  Si vous préférez tooask vos questions sur la pile de dépassement de capacité, nous avons également un [Azure entrepôt pile de dépassement de capacité Forum de données SQL][Azure SQL Data Warehouse Stack Overflow Forum].

Enfin, utilisez hello [commentaires de l’entrepôt de données de SQL Azure] [ Azure SQL Data Warehouse Feedback] toomake fonctionnalité demande de page.  L’ajout de vos demandes ou la confirmation des autres demandes nous permet vraiment de hiérarchiser les fonctions.

<!--Image references-->

<!--Article references-->
[Create a support ticket]: ./sql-data-warehouse-get-started-create-support-ticket.md
[Concurrency and workload management]: ./sql-data-warehouse-develop-concurrency.md
[Create table as select (CTAS)]: ./sql-data-warehouse-develop-ctas.md
[Table overview]: ./sql-data-warehouse-tables-overview.md
[Table data types]: ./sql-data-warehouse-tables-data-types.md
[Table distribution]: ./sql-data-warehouse-tables-distribute.md
[Table indexes]: ./sql-data-warehouse-tables-index.md
[Causes of poor columnstore index quality]: ./sql-data-warehouse-tables-index.md#causes-of-poor-columnstore-index-quality
[Rebuilding columnstore indexes]: ./sql-data-warehouse-tables-index.md#rebuilding-indexes-to-improve-segment-quality
[Table partitioning]: ./sql-data-warehouse-tables-partition.md
[Manage table statistics]: ./sql-data-warehouse-tables-statistics.md
[Temporary tables]: ./sql-data-warehouse-tables-temporary.md
[Guide for using PolyBase]: ./sql-data-warehouse-load-polybase-guide.md
[Load data]: ./sql-data-warehouse-overview-load.md
[Move data with Azure Data Factory]: ../data-factory/data-factory-azure-sql-data-warehouse-connector.md
[Load data with Azure Data Factory]: ./sql-data-warehouse-get-started-load-with-azure-data-factory.md
[Load data with bcp]: ./sql-data-warehouse-load-with-bcp.md
[Load data with PolyBase]: ./sql-data-warehouse-get-started-load-with-polybase.md
[Monitor your workload using DMVs]: ./sql-data-warehouse-manage-monitor.md
[Pause compute resources]: ./sql-data-warehouse-manage-compute-overview.md#pause-compute-bk
[Resume compute resources]: ./sql-data-warehouse-manage-compute-overview.md#resume-compute-bk
[Mettre à l’échelle des ressources de calcul]: ./sql-data-warehouse-manage-compute-overview.md#scale-compute
[Understanding transactions]: ./sql-data-warehouse-develop-transactions.md
[Optimizing transactions]: ./sql-data-warehouse-develop-best-practices-transactions.md
[Troubleshooting]: ./sql-data-warehouse-troubleshoot.md
[LABEL]: ./sql-data-warehouse-develop-label.md

<!--MSDN references-->
[ALTER TABLE]: https://msdn.microsoft.com/library/ms190273.aspx
[CREATE EXTERNAL FILE FORMAT]: https://msdn.microsoft.com/library/dn935026.aspx
[CREATE STATISTICS]: https://msdn.microsoft.com/library/ms188038.aspx
[CREATE TABLE]: https://msdn.microsoft.com/library/mt203953.aspx
[CREATE TABLE AS SELECT]: https://msdn.microsoft.com/library/mt204041.aspx
[DBCC PDW_SHOWEXECUTIONPLAN]: https://msdn.microsoft.com/library/mt204017.aspx
[INSERT]: https://msdn.microsoft.com/library/ms174335.aspx
[OPTION]: https://msdn.microsoft.com/library/ms190322.aspx
[TRUNCATE TABLE]: https://msdn.microsoft.com/library/ms177570.aspx
[UPDATE STATISTICS]: https://msdn.microsoft.com/library/ms187348.aspx
[sys.dm_exec_sessions]: https://msdn.microsoft.com/library/ms176013.aspx
[sys.dm_pdw_exec_requests]: https://msdn.microsoft.com/library/mt203887.aspx
[sys.dm_pdw_request_steps]: https://msdn.microsoft.com/library/mt203913.aspx
[sys.dm_pdw_sql_requests]: https://msdn.microsoft.com/library/mt203889.aspx
[sys.dm_pdw_dms_workers]: https://msdn.microsoft.com/library/mt203878.aspx
[sys.dm_pdw_waits]: https://msdn.microsoft.com/library/mt203893.aspx
[Columnstore indexes guide]: https://msdn.microsoft.com/library/gg492088.aspx

<!--Other Web references-->
[Selecting table distribution]: https://blogs.msdn.microsoft.com/sqlcat/2015/08/11/choosing-hash-distributed-table-vs-round-robin-distributed-table-in-azure-sql-dw-service/
[Azure SQL Data Warehouse Feedback]: https://feedback.azure.com/forums/307516-sql-data-warehouse
[Azure SQL Data Warehouse MSDN Forum]: https://social.msdn.microsoft.com/Forums/sqlserver/home?forum=AzureSQLDataWarehouse
[Azure SQL Data Warehouse Stack Overflow Forum]:  http://stackoverflow.com/questions/tagged/azure-sqldw
[Azure SQL Data Warehouse loading patterns and strategies]: https://blogs.msdn.microsoft.com/sqlcat/2016/02/06/azure-sql-data-warehouse-loading-patterns-and-strategies
