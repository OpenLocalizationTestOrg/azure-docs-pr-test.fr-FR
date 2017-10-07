---
title: "aaaReport sur les bases de données à grande échelle cloud (partitionnement horizontal) | Documents Microsoft"
description: "Comment toouse franchissent les requêtes de base de données de base de données"
services: sql-database
documentationcenter: 
manager: jhubbard
author: MladjoA
ms.assetid: c81ef5e3-41e9-4fd2-8631-868f2e168147
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/23/2016
ms.author: mlandzic
ms.openlocfilehash: e34f398f8d408cffd91a70fc2cfbda73daec3550
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="report-across-scaled-out-cloud-databases-preview"></a>Créer des rapports sur des bases de données cloud avec montée en charge (version préliminaire)
Vous pouvez créer des rapports tirés de plusieurs bases de données SQL Azure à partir d’un point de connexion unique par le biais d’une [requête élastique](sql-database-elastic-query-overview.md). bases de données Hello doivent être partitionnées horizontalement (également appelé « partitionnée »).

Si vous avez une base de données existante, consultez [existant de la migration des bases de données bases de données tooscaled](sql-database-elastic-convert-to-use-elastic-tools.md).

les objets SQL toounderstand hello nécessaires tooquery, consultez [interroger plusieurs bases de données partitionnées horizontalement](sql-database-elastic-query-horizontal-partitioning.md).

## <a name="prerequisites"></a>Composants requis
Téléchargez et exécutez hello [mise en route avec l’exemple des outils de base de données élastique](sql-database-elastic-scale-get-started.md).

## <a name="create-a-shard-map-manager-using-hello-sample-app"></a>Créer une carte de partitions manager à l’aide de hello, exemple d’application
Ici vous allez créer une carte de partitions manager ainsi que plusieurs partitions, suivie de l’insertion de données dans les partitions hello. Si vous vous trouvez tooalready contiennent le programme d’installation de partitions avec des données partitionnées, vous pouvez ignorer hello comme suit et déplacer la section suivante de toohello.

1. Générez et exécutez hello **prise en main des outils de base de données élastique** exemple d’application. Hello comme suit avant l’étape 7 de la section de hello [télécharger et exécuter l’exemple d’application hello](sql-database-elastic-scale-get-started.md#download-and-run-the-sample-app). Extrémité hello de l’étape 7, vous verrez hello après l’invite de commandes :

    ![invite de commande][1]
2. Dans la fenêtre de commande hello, tapez « 1 » et appuyez sur **entrée**. Cela crée le Gestionnaire de carte de partitions hello et ajoute le serveur de toohello deux partitions. Tapez « 3 », puis appuyez sur **entrée**; Répétez l’action de hello quatre fois. Cela permet d’insérer des lignes d’exemples de données dans vos partitions.
3. Hello [portail Azure](https://portal.azure.com) doivent s’afficher trois nouvelles bases de données dans votre serveur :

   ![Confirmation Visual Studio][2]

   À ce stade, les requêtes de bases de données croisées sont pris en charge via les bibliothèques clientes hello élastique de base de données. Par exemple, utilisez l’option 4 dans la fenêtre de commande hello. Hello les résultats d’une requête de plusieurs partition sont toujours un **UNION ALL** de résultats hello à partir de toutes les partitions.

   Dans la section suivante de hello, nous créer un point de terminaison de base de données exemple qui prend en charge l’interrogation plus riche de données de hello entre les partitions.

## <a name="create-an-elastic-query-database"></a>Créez une base de données de requête élastique
1. Ouvrez hello [portail Azure](https://portal.azure.com) et connectez-vous.
2. Créer une nouvelle base de données SQL Azure Bonjour même serveur que votre programme d’installation de la partition. Nom de la base de données hello « ElasticDBQuery ».

    ![Portail Azure et tarification][3]

    > [!NOTE]
    > Vous pouvez utiliser une base de données existante. Si vous pouvez le faire, il ne doit pas être une des partitions hello que vous aimeriez tooexecute vos requêtes sur. Cette base de données sera utilisé pour la création d’objets de métadonnées pour une requête de base de données élastique hello.
    >

## <a name="create-database-objects"></a>Créez des objets de base de données
### <a name="database-scoped-master-key-and-credentials"></a>Clé principale et informations d’identification de la base de données
Il s’agit de gestionnaire de carte de partitions toohello tooconnect utilisés et les partitions hello :

1. Ouvrez SQL Server Management Studio ou SQL Server Data Tools dans Visual Studio.
2. Se connecter tooElasticDBQuery de base de données et exécutez hello suivant de commandes T-SQL :

        CREATE MASTER KEY ENCRYPTION BY PASSWORD = '<password>';

        CREATE DATABASE SCOPED CREDENTIAL ElasticDBQueryCred
        WITH IDENTITY = '<username>',
        SECRET = '<password>';

    « username » et « password » doit être hello même en tant qu’informations de connexion utilisées à l’étape 6 de [télécharger et exécuter l’exemple d’application hello](sql-database-elastic-scale-get-started.md#download-and-run-the-sample-app) dans [prise en main des outils de base de données élastique](sql-database-elastic-scale-get-started.md).

### <a name="external-data-sources"></a>Sources de données externes
toocreate source de données externe, exécutez hello suivant de commande de base de données ElasticDBQuery hello :

    CREATE EXTERNAL DATA SOURCE MyElasticDBQueryDataSrc WITH
      (TYPE = SHARD_MAP_MANAGER,
      LOCATION = '<server_name>.database.windows.net',
      DATABASE_NAME = 'ElasticScaleStarterKit_ShardMapManagerDb',
      CREDENTIAL = ElasticDBQueryCred,
       SHARD_MAP_NAME = 'CustomerIDShardMap'
    ) ;

 « CustomerIDShardMap » est le nom hello de carte de partitions hello, si vous avez créé carte de partitions et de carte de partitions hello manager à l’aide des exemples d’outils hello élastique de base de données. Toutefois, si vous avez utilisé votre installation personnalisée pour cet exemple, il doit être nom de mappage de partitions hello choisis dans votre application.

### <a name="external-tables"></a>Tables externes
Créer une table externe qui correspond à celui de la table de clients de hello sur les partitions hello en exécutant la commande suivante sur la base de données ElasticDBQuery de hello :

    CREATE EXTERNAL TABLE [dbo].[Customers]
    ( [CustomerId] [int] NOT NULL,
      [Name] [nvarchar](256) NOT NULL,
      [RegionId] [int] NOT NULL)
    WITH
    ( DATA_SOURCE = MyElasticDBQueryDataSrc,
      DISTRIBUTION = SHARDED([CustomerId])
    ) ;

## <a name="execute-a-sample-elastic-database-t-sql-query"></a>Exécutez un exemple de requête T-SQL de base de données élastique
Après avoir défini vos tables externes et votre source de données externe, vous pouvez utiliser l’ensemble T-SQL sur vos tables externes.

Exécutez cette requête sur la base de données ElasticDBQuery hello :

    select count(CustomerId) from [dbo].[Customers]

Vous remarquerez cette requête hello regroupe les résultats à partir de toutes les partitions hello et donne hello suivant de sortie :

![Détails des résultats][4]

## <a name="import-elastic-database-query-results-tooexcel"></a>Importer tooExcel de résultats de requête de base de données élastique
 Vous pouvez importer les résultats hello à partir d’un fichier Excel de tooan requête.

1. Lancez Excel 2013.
2. Accédez toohello **données** ruban.
3. Cliquez sur **À partir d’autres sources** et sur **À partir de SQL Server**.

   ![Importation au format Excel à partir d’autres sources][5]
4. Bonjour **Assistant connexion de données** tapez hello des informations d’identification nom et la connexion de serveur. Cliquez ensuite sur **Suivant**.
5. Dans la boîte de dialogue hello **base de données hello Select qui contient les données hello**, sélectionnez hello **ElasticDBQuery** base de données.
6. Sélectionnez hello **clients** de table dans la vue de liste hello et cliquez sur **suivant**. Puis, cliquez sur **Terminer**.
7. Bonjour **importer des données** formulaire sous **Choisissez comment vous voulez que tooview ces données dans votre classeur**, sélectionnez **Table** et cliquez sur **OK**.

Tous les hello des lignes à partir de **clients** table, stockée dans des partitions différentes remplir la feuille de calcul Excel hello.

Vous pouvez maintenant utiliser les fonctions de visualisation de données puissantes d’Excel. Vous pouvez utiliser de chaîne de connexion hello avec le nom de votre serveur, nom de la base de données et que vous les informations d’identification tooconnect votre BI et données intégration outils toohello requête élastique de base de données. Assurez-vous que SQL Server est pris en charge comme source de données pour votre outil. Vous pouvez consulter la base de données de requête élastique toohello et des tables externes comme toute autre base de données SQL Server et des tables SQL Server que vous devez vous connecter toowith votre outil.

### <a name="cost"></a>Coût
Il n’existe aucun frais supplémentaire pour à l’aide de la fonctionnalité de requête de base de données élastique hello.

Pour plus d’informations sur la tarification, consultez la page [Tarification - Base de données SQL](https://azure.microsoft.com/pricing/details/sql-database/).

## <a name="next-steps"></a>Étapes suivantes

* Pour une présentation des requêtes élastiques, consultez [Présentation des requêtes élastiques](sql-database-elastic-query-overview.md).
* Pour le didacticiel sur le partitionnement vertical, consultez [Prise en main des requêtes de bases de données croisées (partitionnement vertical)](sql-database-elastic-query-getting-started-vertical.md).
* Pour la syntaxe et des exemples de requêtes pour des données partitionnées verticalement, consultez [Requêtes sur des données partitionnées verticalement](sql-database-elastic-query-vertical-partitioning.md)
* Pour la syntaxe et des exemples de requêtes pour des données partitionnées horizontalement, consultez [Requêtes sur des données partitionnées horizontalement](sql-database-elastic-query-horizontal-partitioning.md)
* Consultez [sp\_execute \_remote](https://msdn.microsoft.com/library/mt703714) pour une procédure stockée qui exécute une instruction Transact-SQL sur une seule base de données Azure SQL distante ou un ensemble de bases de données servant de partitions dans un schéma de partitionnement horizontal.


<!--Image references-->
[1]: ./media/sql-database-elastic-query-getting-started/cmd-prompt.png
[2]: ./media/sql-database-elastic-query-getting-started/portal.png
[3]: ./media/sql-database-elastic-query-getting-started/tiers.png
[4]: ./media/sql-database-elastic-query-getting-started/details.png
[5]: ./media/sql-database-elastic-query-getting-started/exel-sources.png
<!--anchors-->
