---
title: "vue d’ensemble de requête élastique de base de données SQL aaaAzure | Documents Microsoft"
description: "Vue d’ensemble de la fonctionnalité de requête élastique hello"
services: sql-database
documentationcenter: 
manager: jhubbard
author: MladjoA
ms.assetid: a8bf0e2c-bc74-44d0-9b1e-bcc9a6aa2e33
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/27/2016
ms.author: mlandzic
ms.openlocfilehash: db17f551882cfcae0da67fdda12708baeb6db81c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-sql-database-elastic-query-overview-preview"></a>Vue d’ensemble de la requête élastique Azure SQL Database (version préliminaire)
fonctionnalité de requête élastique Hello (en version préliminaire) vous permet de toorun une requête Transact-SQL qui s’étend sur plusieurs bases de données dans la base de données SQL Azure. Il vous permet de requêtes de bases de données croisées tooperform tooaccess des tables distantes et tooquery d’Outils (Excel, Power BI, Tableau, etc.) de Microsoft et tiers tooconnect entre les couches de données avec plusieurs bases de données. À l’aide de cette fonctionnalité, vous pouvez mettre à l’échelle des niveaux de données toolarge de requêtes dans la base de données SQL et visualiser les résultats de hello dans les rapports de business intelligence (BI).


## <a name="why-use-elastic-queries"></a>Pourquoi utiliser les requêtes élastiques ?

**Azure SQL Database**

Interrogez plusieurs bases de données SQL Azure entièrement dans T-SQL. Il est ainsi possible d’interroger en lecture seule des bases de données distantes. Cela permet une locale à l’aide des noms de trois et quatre parties ou de serveur lié tooSQL DB les applications toomigrate clients SQL Server.

**Disponible au niveau standard**

Requête élastique est pris en charge sur le niveau de performances Standard hello dans le niveau de performances plus toohello Premium. Consultez les section hello sur les limites d’aperçu ci-dessous sur les limitations de performances pour les niveaux de performances inférieurs.

**Bases de données push tooremote**

Requêtes élastiques peuvent désormais distribuer les paramètres toohello distants bases de données SQL pour l’exécution.

**Exécution d’une procédure stockée**

Exécutez des appels de procédures stockées ou de fonctions distantes avec [sp\_execute \_remote](https://msdn.microsoft.com/library/mt703714).

**Flexibilité**

Tables externes dont la requête élastique peuvent maintenant faire référence à des tables de tooremote avec un schéma différent ou le nom de la table.

## <a name="elastic-query-scenarios"></a>Scénarios de requête élastique

Hello vise toofacilitate interrogation des scénarios où plusieurs bases de données contribuent les lignes en un seul résultat global. requête de Hello peut soit être composée en hello utilisateur ou l’application directement ou indirectement via des outils qui sont connectés toohello de base de données. Ceci est particulièrement utile lors de la création de rapports, à l’aide des outils commerciaux d’intégration BI ou de données, ou toute application qui ne peut pas être modifiée. Une requête élastique, vous pouvez interroger sur plusieurs bases de données à l’aide d’expérience de connectivité de SQL Server familière hello dans des outils tels que Excel, Power BI, Tableau ou Cognos.
Une requête élastique permet un accès facile tooan ensemble de la collection de bases de données via des requêtes émises par SQL Server Management Studio ou Visual Studio et facilite l’interrogation des bases de données croisées d’Entity Framework ou d’autres environnements ORM. La figure 1 illustre un scénario où un existant cloud des applications (qui utilise hello [bibliothèque cliente de base de données élastique](sql-database-elastic-database-client-library.md)) s’appuie sur une montée en charge de données de couche, et une requête élastique est utilisée pour les rapports des bases de données croisées.

**Figure 1** Requête élastique utilisée sur la couche de données mise à l’échelle

![Requête élastique utilisée sur la couche de données mise à l’échelle][1]

Scénarios de client pour une requête élastique sont caractérisent par hello suivant topologies :

* **Le partitionnement vertical - requêtes de bases de données croisées** (topologie 1) : les données de salutation sont partitionnées verticalement entre plusieurs bases de données dans une couche de données. En règle générale, les différents ensembles de tables résident sur des bases de données différentes. Cela signifie que ce schéma hello est différent sur les différentes bases de données. Par exemple, toutes les tables d’inventaire se trouvent sur une base de données alors que toutes les tables liées à la comptabilité se trouvent dans une seconde base de données. Cas d’utilisation courants avec cette topologie nécessitent un tooquery entre ou rapports toocompile dans des tables dans plusieurs bases de données.
* **Partitionnement horizontal - partitionnement** (topologie 2) : les données sont partitionnées horizontalement les lignes toodistribute entre une montée en puissance parallèle de données de niveau. Avec cette approche, le schéma de hello est identique sur toutes les bases de données participantes. Cette approche est également appelée « partitionnement ». Partitionnement peut être effectué et gérés à l’aide des bibliothèques d’outils de base de données élastique hello (1) ou (2) partitionnement automatique. Une requête élastique est utilisé des rapports tooquery ou de la compilation sur plusieurs partitions.

> [!NOTE]
> Requête élastique fonctionne mieux pour les scénarios de création de rapports occasionnelles où la plupart du traitement de hello peut être effectuée sur la couche de données hello. Pour les charges de travail de création de rapports intensive ou les scénarios d’entreposage de données avec des requêtes plus complexes, pensez à utiliser [Azure SQL Data Warehouse](https://azure.microsoft.com/services/sql-data-warehouse/).
>  

## <a name="vertical-partitioning---cross-database-queries"></a>Le partitionnement vertical - requêtes de bases de données croisées

toobegin de codage, consultez [mise en route de la requête de bases de données croisées (partitionnement vertical)](sql-database-elastic-query-getting-started-vertical.md).

Une requête élastique peut être des données de toomake utilisé situées dans la base de données disponible tooother SQL bases de données SQL. Cela permet des requêtes à partir d’un tootables toorefer de base de données dans n’importe quel autre SQL base de données distante. première étape de Hello est toodefine une source de données externe pour chaque base de données distante. source de données externe Hello est défini dans la base de données locale hello à partir de laquelle vous souhaitez tootables d’accès toogain situé sur la base de données distante hello. Aucune modification n’est nécessaire sur la base de données distante hello. Pour verticales partitionnement scénarios classiques où les bases de données différentes ont des schémas différents, élastiques vous pouvez tooimplement utilisé cas d’utilisation courants tels que d’accéder à des données tooreference et interrogation des bases de données croisées.

> [!IMPORTANT]
> Vous devez posséder l’autorisation ALTER ANY EXTERNAL DATA SOURCE. Cette autorisation est incluse avec l’autorisation ALTER DATABASE hello. Les autorisations ALTER ANY EXTERNAL DATA SOURCE sont toohello nécessaires toorefer source de données sous-jacente.
>

**Données de référence**: topologie de hello est utilisé pour la gestion des données de référence. Dans la figure hello ci-dessous, deux tables (T1 et T2) avec les données de référence sont conservées sur une base de données dédié. À l’aide d’une requête élastique, vous pouvez désormais accéder aux tables T1 et T2 à distance à partir d’autres bases de données, comme indiqué dans la figure hello. Utilisez Topologie 1 si les tables de référence sont des requêtes de petite taille ou distantes se trouvant dans la table de référence et ayant des prédicats sélectifs.

**Figure 2** partitionnement Vertical - l’à l’aide de données de référence de requête élastique tooquery

![Partitionnement vertical - l’à l’aide de données de référence de requête élastique tooquery][3]

**Interrogation des bases de données croisées**: les requêtes élastiques permettent d’utiliser des cas nécessitant l’interrogation de plusieurs bases de données SQL. La figure 3 représente quatre bases de données différentes : Gestion de la relation client (CRM), Inventaire, Ressources humaines (RH) et Produits. Les requêtes effectuées dans une des bases de données hello également besoin d’accès tooone ou tous les hello autres bases de données. À l’aide d’une requête élastique, vous pouvez configurer votre base de données pour ce cas en exécutant des instructions DDL simples quelques sur chacun des quatre bases de données hello. Après cette configuration à usage unique, table distante de l’accès tooa est aussi simple que vous faites référence tooa des tables locales à partir de vos requêtes T-SQL ou de vos outils BI. Cette approche est recommandée si les requêtes distantes hello ne retournent pas de résultats volumineux.

**Figure 3** partitionnement Vertical - l’à l’aide de la requête élastique tooquery entre les différentes bases de données

![Partitionnement vertical - l’à l’aide de la requête élastique tooquery entre les différentes bases de données][4]

requêtes de base de données élastique pour des scénarios de partitionnement verticales qui requièrent la table de tooa access situés sur des bases de données SQL à distance avec hello même configurer Hello suit schéma :

* [CREATE MASTER KEY](https://msdn.microsoft.com/library/ms174382.aspx) mymasterkey
* [CREATE DATABASE SCOPED CREDENTIAL](https://msdn.microsoft.com/library/mt270260.aspx) mycredential
* [CREATE/DROP EXTERNAL DATA SOURCE](https://msdn.microsoft.com/library/dn935022.aspx) mydatasource de **RDBMS**
* [CREATE/DROP EXTERNAL TABLE](https://msdn.microsoft.com/library/dn935021.aspx) mytable

Après l’exécution des instructions DDL de hello, vous pouvez accéder table distante de hello « mytable » comme s’il s’agissait d’une table locale. Base de données SQL Azure ouvre automatiquement une base de données du toohello de connexion à distance, traite votre demande sur la base de données distante hello et retourne des résultats hello.

## <a name="horizontal-partitioning---sharding"></a>Partitionnement horizontal - partitionnement
Requiert de couche données à l’aide de tooperform requête élastique confondues tâches partitionnée, c'est-à-dire horizontalement partitionnée, un [carte de partitions de base de données élastique](sql-database-elastic-scale-shard-map-management.md) bases de données toorepresent hello de couche de données hello. En règle générale, uniquement un mappage de partition unique est utilisé dans ce scénario, et une base de données dédié avec des fonctions de requête élastique (nœud principal) sert de point d’entrée hello pour les requêtes de rapport. Cette base de données dédiée uniquement doit carte de partitions toohello accès. La figure 4 illustre cette topologie et sa configuration avec la carte de base de données et les partitions de la requête élastique hello. bases de données Hello dans la couche de données hello peuvent être de toute base de données SQL Azure version ou édition. Pour plus d’informations sur la bibliothèque cliente de base de données élastique hello et en créant des cartes de partitions, consultez [gestion de carte de partitions](sql-database-elastic-scale-shard-map-management.md).

**Figure 4** partitionnement horizontal : utilisation d’une requête élastique pour les rapports sur les couches de données partitionnées

![partitionnement horizontal : utilisation d’une requête élastique pour les rapports sur les couches de données partitionnées][5]

> [!NOTE]
> Requête base de données élastique (nœud principal) peut être la base de données distincte, ou il peut être hello même cette carte de partitions hello hôtes de la base de données. Configuration que vous choisissez, assurez-vous que ce niveau de service et les performances de cette base de données est suffisamment élevée toohandle hello attendu/demandes de connexion.

Hello suit configure des requêtes de base de données élastique pour horizontales partitionnement des scénarios qui requièrent l’ensemble de tooa d’accès de la table qui sont trouvent sur (généralement) plusieurs SQL bases de données distantes :

* [CREATE MASTER KEY](https://msdn.microsoft.com/library/ms174382.aspx) mymasterkey
* [CREATE DATABASE SCOPED CREDENTIAL](https://msdn.microsoft.com/library/mt270260.aspx) mycredential
* Créer un [carte de partitions](sql-database-elastic-scale-shard-map-management.md) représentant votre couche de données à l’aide de la bibliothèque cliente de base de données élastique hello.   
* [CREATE/DROP EXTERNAL DATA SOURCE](https://msdn.microsoft.com/library/dn935022.aspx) mydatasource de type **SHARD_MAP_MANAGER**
* [CREATE/DROP EXTERNAL TABLE](https://msdn.microsoft.com/library/dn935021.aspx) mytable

Une fois que vous avez effectué ces étapes, vous pouvez accéder à table partitionnée horizontalement de hello « mytable » comme s’il s’agissait d’une table locale. Base de données SQL Azure automatiquement ouvre plusieurs connexions parallèles toohello bases de données où les tables de hello sont stockées physiquement, traite les demandes de hello sur les bases de données distantes hello et retourne les résultats de hello.
Plus d’informations sur les étapes de hello requis pour le scénario de partitionnement horizontal hello se trouvent dans [élastique requête pour le partitionnement horizontal](sql-database-elastic-query-horizontal-partitioning.md).

toobegin de codage, consultez [mise en route de la requête élastique pour le partitionnement horizontal (partitionnement)](sql-database-elastic-query-getting-started.md).

## <a name="t-sql-querying"></a>Requêtes T-SQL
Une fois que vous avez défini vos sources de données externes et des tables externes, vous pouvez utiliser SQL Server connexion chaînes tooconnect toohello bases de données normales où vous avez défini vos tables externes. Vous pouvez ensuite exécuter des instructions T-SQL sur des tables externes sur cette connexion avec les limitations de hello décrites ci-dessous. Vous trouverez plus d’informations et des exemples de requêtes T-SQL dans les rubriques de la documentation hello pour [partitionnement horizontal](sql-database-elastic-query-horizontal-partitioning.md) et [le partitionnement vertical](sql-database-elastic-query-vertical-partitioning.md).

## <a name="connectivity-for-tools"></a>Connectivité des outils
Vous pouvez utiliser tooconnect de chaînes de connexion SQL Server standard pour vos applications et BI ou données toodatabases outils intégration qui ont des tables externes. Assurez-vous que SQL Server est pris en charge comme source de données pour votre outil. Une fois connecté, consultez toohello requête élastique de base de données et hello tables externes dans cette base de données comme vous le feriez avec toute autre base de données SQL Server que vous vous connectez à toowith votre outil.

> [!IMPORTANT]
> L’authentification à l’aide d’Azure Active Directory avec des requêtes élastiques n’est pas prise en charge actuellement.
> 
> 

## <a name="cost"></a>Coût
Requête élastique est inclus dans le coût de hello des bases de données de base de données SQL Azure. Notez que les topologies où se trouvent vos bases de données à distance dans un autre centre de données que hello du point de terminaison de requête élastique sont pris en charge, mais la sortie de données à partir de bases de données distantes sont facturés regular [taux Azure](https://azure.microsoft.com/pricing/details/data-transfers/).

## <a name="preview-limitations"></a>Limitations de la version préliminaire
* Votre première requête élastique en cours d’exécution peuvent occuper tooa quelques minutes sur le niveau de performances Standard hello. Ce temps est une fonctionnalité de requête élastique de hello tooload nécessaires ; améliore les performances de chargement avec les niveaux de performance supérieurs.
* La rédaction de script de sources de données externes ou de tables externes à partir de SSMS ou SSDT n’est pas encore prise en charge.
* L’importation/exportation de base de données de SQL ne prend pas en charge les tables et sources de données externes. Si vous devez toouse Import/Export, supprimer ces objets avant l’exportation et puis de les recréer après l’importation.
* Requête élastique prend actuellement en charge uniquement les tables de tooexternal d’accès en lecture seule. Vous pouvez toutefois utiliser toutes les fonctionnalités T-SQL sur la base de données hello où une table externe hello est définie. Cela peut être utile pour, par exemple, conserver les résultats temporaires, par exemple, sélectionnez < column_list > dans < local_table > ou toodefine des procédures stockées sur hello requête élastique de base de données qui font référence à des tables de tooexternal.
* À l’exception de nvarchar (max), les types métier ne sont pas pris en charge dans les définitions de table externes. Comme solution de contournement, vous pouvez créer une vue sur hello à distance de base de données qui effectue un cast de type LOB de hello en nvarchar (max), définissez votre table externe sur vue hello au lieu de la table de base hello et puis effectuer un cast vers le type LOB d’origine de hello dans vos requêtes.
* Les statistiques des colonnes via les tables externes ne sont pas prises en charge actuellement. Statistiques des tables sont prises en charge, mais doivent toobe créée manuellement.

## <a name="feedback"></a>Commentaires
Veuillez partager des commentaires sur votre expérience avec les requêtes élastiques avec nous sur Disqus ci-dessous, les forums MSDN hello, ou sur Stackoverflow. Nous sommes intéressés par tous les types de commentaires sur service hello (erreurs, les bords, les écarts de fonctionnalité).

## <a name="next-steps"></a>Étapes suivantes

* Pour le didacticiel sur le partitionnement vertical, consultez [Prise en main des requêtes de bases de données croisées (partitionnement vertical)](sql-database-elastic-query-getting-started-vertical.md).
* Pour la syntaxe et des exemples de requêtes pour des données partitionnées verticalement, consultez [Requêtes sur des données partitionnées verticalement](sql-database-elastic-query-vertical-partitioning.md)
* Pour commencer le didacticiel sur le partitionnement horizontal (sharding), consultez [Prise en main des requêtes élastiques pour le partitionnement horizontal (sharding)](sql-database-elastic-query-getting-started.md).
* Pour la syntaxe et des exemples de requêtes pour des données partitionnées horizontalement, consultez [Requêtes sur des données partitionnées horizontalement](sql-database-elastic-query-horizontal-partitioning.md)
* Consultez [sp\_execute \_remote](https://msdn.microsoft.com/library/mt703714) pour une procédure stockée qui exécute une instruction Transact-SQL sur une seule base de données Azure SQL distante ou un ensemble de bases de données servant de partitions dans un schéma de partitionnement horizontal.

<!--Image references-->
[1]: ./media/sql-database-elastic-query-overview/overview.png
[2]: ./media/sql-database-elastic-query-overview/topology1.png
[3]: ./media/sql-database-elastic-query-overview/vertpartrrefdata.png
[4]: ./media/sql-database-elastic-query-overview/verticalpartitioning.png
[5]: ./media/sql-database-elastic-query-overview/horizontalpartitioning.png

<!--anchors-->
