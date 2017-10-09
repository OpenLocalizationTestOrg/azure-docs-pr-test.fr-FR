---
title: "toouse aaaHow le traitement par lot des performances de l’application tooimprove base de données SQL Azure"
description: "Hello rubrique constitue une preuve que le traitement par lot de base de données operations considérablement imroves hello vitesse et l’évolutivité de vos applications de base de données SQL Azure. Bien que ces techniques de traitement par lot de travail pour une base de données SQL Server, hello se concentre sur l’article de hello sur Azure."
services: sql-database
documentationcenter: na
author: stevestein
manager: jhubbard
editor: 
ms.assetid: 563862ca-c65a-46f6-975d-10df7ff6aa9c
ms.service: sql-database
ms.custom: develop apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 07/12/2016
ms.author: sstein
ms.openlocfilehash: 124b203ee69c595f0813852ff09ef9ec6841233a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-batching-tooimprove-sql-database-application-performance"></a>Comment toouse le traitement par lot des performances des applications de base de données SQL tooimprove
Le traitement par lot des opérations tooAzure de la base de données SQL considérablement améliore les performances de hello et de l’évolutivité de vos applications. Dans l’ordre toounderstand hello d’avantages hello première partie de cet article traite des résultats de test qui comparent des demandes séquentielles et par lot tooa base de données SQL. Hello reste de l’article de hello montre des techniques de hello, scénarios et considérations toohelp toouse de traitement par lot avec succès dans vos applications Azure.

## <a name="why-is-batching-important-for-sql-database"></a>Pourquoi le traitement par lots est-il important pour une base de données SQL ?
Le traitement par lot des appels tooa le service distant est une stratégie connue pour améliorer les performances et l’évolutivité. Il existe des fixes traitement des coûts des interactions de tooany avec un service distant, telles que la sérialisation, le transfert de réseau et la désérialisation. L’empaquetage de plusieurs transactions distinctes dans un seul lot contribue à réduire ces coûts.

Dans ce document, nous souhaitons tooexamine différents scénarios et les stratégies de traitement par lot de base de données SQL. Bien que ces stratégies soient également importantes pour les applications locales qui utilisent SQL Server, il existe plusieurs raisons pour mettre en surbrillance utilisez hello du traitement par lot pour la base de données SQL :

* Est potentiellement plus grande latence du réseau l’accès à la base de données SQL, en particulier si vous accédez à base de données SQL à partir de l’extérieur hello même centre de données Microsoft Azure.
* caractéristiques d’architecture mutualisée Hello signifie que de base de données SQL qui hello l’efficacité des données de hello toohello de corrélation de couche d’accès évolutivité globale de la base de données hello. Base de données SQL doit empêcher un locataire/utilisateur de monopoliser détriment de toohello de ressources de base de données d’autres clients. Dans toousage réponse dépassant les quotas prédéfinis, base de données SQL réduit le débit ou répond avec les exceptions de limitation. L’efficacité, telles que le traitement par lot, activez vous toodo plus de travail sur la base de données SQL avant d’atteindre ces limites. 
* Le traitement par lots est également efficace pour les architectures qui utilisent plusieurs bases de données (partitionnement). Hello efficacité de votre interaction avec chaque unité de base de données est toujours un facteur clé dans votre évolutivité globale. 

Un des avantages de hello d’à l’aide de la base de données SQL est que vous n’avez pas les serveurs hello toomanage cette base de données hôte hello. Toutefois, cette infrastructure managée signifie également que vous avez toothink différemment sur les optimisations de la base de données. Vous ne pouvez plus chercher infrastructure de matériel ou de réseau la base de données des hello tooimprove. Ces environnements sont directement contrôlés par Microsoft Azure. Hello principal de la zone que vous pouvez contrôler est la façon dont votre application interagit avec la base de données SQL. Le traitement par lots constitue l’une de ces optimisations. 

Hello première partie du livre de hello examine différentes techniques de traitement par lot pour les applications .NET qui utilisent la base de données SQL. Hello deux dernières sections couvrent des instructions de traitement par lot et des scénarios.

## <a name="batching-strategies"></a>Stratégies de traitement par lots
### <a name="note-about-timing-results-in-this-topic"></a>Remarque relative aux résultats de minutage fournis dans cette rubrique
> [!NOTE]
> Résultats ne sont pas des points de référence, mais sont destinées à tooshow **performances relatives**. Les minutages reposent sur une moyenne calculée à partir d’au moins 10 séries de tests. Les opérations consistent en des insertions dans une table vide. Ces tests ont été mesurés pre-V12, et ils ne correspondent pas nécessairement toothroughput que vous pouvez rencontrer dans une base de données V12 à l’aide de nouveau hello [niveaux de service](sql-database-service-tiers.md). avantage relatif de Hello Hello technique de traitement par lot doit être similaire.
> 
> 

### <a name="transactions"></a>Transactions
Il semble étrange toobegin une revue du traitement par lots en traitant des transactions. Mais utilisez hello des transactions côté client a un effet de traitement par lot côté serveur subtil qui améliore les performances. Et les transactions peuvent être ajoutées avec seulement quelques lignes de code, afin de fournir des performances des opérations séquentielles tooimprove rapidement.

Envisagez de hello suivant de code c# qui contient une séquence d’insertion et mettre à jour des opérations sur une table simple.

    List<string> dbOperations = new List<string>();
    dbOperations.Add("update MyTable set mytext = 'updated text' where id = 1");
    dbOperations.Add("update MyTable set mytext = 'updated text' where id = 2");
    dbOperations.Add("update MyTable set mytext = 'updated text' where id = 3");
    dbOperations.Add("insert MyTable values ('new value',1)");
    dbOperations.Add("insert MyTable values ('new value',2)");
    dbOperations.Add("insert MyTable values ('new value',3)");

Hello suivant de manière séquentielle code ADO.NET effectue ces opérations.

    using (SqlConnection connection = new SqlConnection(CloudConfigurationManager.GetSetting("Sql.ConnectionString")))
    {
        conn.Open();

        foreach(string commandString in dbOperations)
        {
            SqlCommand cmd = new SqlCommand(commandString, conn);
            cmd.ExecuteNonQuery();                   
        }
    }

Hello meilleures toooptimize de façon à ce code est tooimplement une forme de traitement côté client de ces appels. Mais il existe une méthode simple tooincrease hello des performances de ce code en encapsulant simplement la séquence hello d’appels dans une transaction. Voici hello même code qui utilise une transaction.

    using (SqlConnection connection = new SqlConnection(CloudConfigurationManager.GetSetting("Sql.ConnectionString")))
    {
        conn.Open();
        SqlTransaction transaction = conn.BeginTransaction();

        foreach (string commandString in dbOperations)
        {
            SqlCommand cmd = new SqlCommand(commandString, conn, transaction);
            cmd.ExecuteNonQuery();
        }

        transaction.Commit();
    }

Les transactions sont en fait utilisées dans ces deux exemples. Dans le premier exemple de hello, chaque appel individuel est une transaction implicite. Dans le deuxième exemple de hello, une transaction explicite encapsule tous les appels hello. Par documentation hello pour hello [journal des transactions à écriture anticipée](https://msdn.microsoft.com/library/ms186259.aspx), les enregistrements de journal sont vidées toohello disque lors de la validation de la transaction hello. Par conséquent, en incluant davantage d’appels dans une transaction, hello journal des transactions toohello écriture peut retarder jusqu'à hello transaction est validée. En effet, vous activez le traitement par lot pour le journal des transactions du serveur toohello hello écritures.

Hello tableau suivant montre des résultats des tests ad hoc. effectuer les tests de Hello hello que même séquentiel insère avec et sans transactions. Pour plus de perspective, hello premier ensemble de tests a été exécuté à distance à partir d’une base de données portable toohello dans Microsoft Azure. Hello deuxième ensemble de tests a été exécuté à partir d’un service cloud et de la base de données qui résidaient dans hello même centre de données Microsoft Azure (ouest des États-Unis). Hello tableau suivant affiche hello durée en millisecondes des insertions séquentielles avec et sans transactions.

**Local tooAzure**:

| Opérations | Sans transaction (ms) | Avec transaction (ms) |
| --- | --- | --- |
| 1 |130 |402 |
| 10 |1 208 |1 226 |
| 100 |12 662 |10 395 |
| 1 000 |128 852 |102 917 |

**Azure tooAzure (même centre de données)**:

| Opérations | Sans transaction (ms) | Avec transaction (ms) |
| --- | --- | --- |
| 1 |21 |26 |
| 10 |220 |56 |
| 100 |2 145 |341 |
| 1 000 |21 479 |2 756 |

> [!NOTE]
> Les résultats ne représentent pas des valeurs de référence. Consultez hello [Remarque à propos des résultats du minutage dans cette rubrique](#note-about-timing-results-in-this-topic).
> 
> 

Selon les résultats des tests précédents hello, une seule opération d’habillage dans une transaction réellement réduit les performances. Mais lorsque vous augmentez le nombre de hello d’opérations dans une transaction unique, amélioration des performances hello devient plus marquée. différence de performances Hello est également plus apparente lorsque toutes les opérations se produisent dans le centre de données de Microsoft Azure hello. Hello de l’utilisation de la base de données SQL à partir du centre de données de Microsoft Azure hello en dehors de la latence accrue masque en partie le gain de performances hello de l’utilisation de transactions.

Bien que l’utilisation de hello des transactions peut accroître les performances, continuer trop[observer les meilleures pratiques pour les connexions et transactions](https://msdn.microsoft.com/library/ms187484.aspx). Conserver la transaction hello autant que la connexion de base de données hello possible et fermer après la fin du travail de hello. Bonjour à l’aide de la déclaration dans l’exemple précédent de hello garantit que hello est déconnecté lors de la fin du bloc de code suivant hello.

Hello précédente montre que vous pouvez ajouter un code ADO.NET tooany transaction locale avec deux lignes. Les transactions offrent un moyen rapide de performances de hello tooimprove du code qui effectue séquentiel insérer, mettre à jour et les opérations de suppression. Toutefois, pour des performances accrues de hello, pensez à hello code supplémentaire tootake parti du traitement par lots côté client, telles que des paramètres table.

Pour plus d’informations sur les transactions dans ADO.NET, consultez [Transactions locales dans ADO.NET](https://docs.microsoft.com/dotnet/framework/data/adonet/local-transactions).

### <a name="table-valued-parameters"></a>Paramètres table
Les paramètres table prennent en charge les types de tables définis par l’utilisateur en tant que paramètres dans les instructions Transact-SQL, en tant que procédures stockées et en tant que fonctions. Cette technique de traitement par lot côté client vous permet de toosend plusieurs lignes de données dans le paramètre de table hello. Paramètres table toouse, d’abord définir un type de table. Hello instruction Transact-SQL suivante crée un type de table nommé **MyTableType**.

    CREATE TYPE MyTableType AS TABLE 
    ( mytext TEXT,
      num INT );


Dans le code, vous créez un **DataTable** avec hello exactement les mêmes noms et types hello du type de table. Transférez ce **DataTable** dans un paramètre via une requête texte ou un appel de procédure stockée. Hello exemple suivant illustre cette technique :

    using (SqlConnection connection = new SqlConnection(CloudConfigurationManager.GetSetting("Sql.ConnectionString")))
    {
        connection.Open();

        DataTable table = new DataTable();
        // Add columns and rows. hello following is a simple example.
        table.Columns.Add("mytext", typeof(string));
        table.Columns.Add("num", typeof(int));    
        for (var i = 0; i < 10; i++)
        {
            table.Rows.Add(DateTime.Now.ToString(), DateTime.Now.Millisecond);
        }

        SqlCommand cmd = new SqlCommand(
            "INSERT INTO MyTable(mytext, num) SELECT mytext, num FROM @TestTvp",
            connection);

        cmd.Parameters.Add(
            new SqlParameter()
            {
                ParameterName = "@TestTvp",
                SqlDbType = SqlDbType.Structured,
                TypeName = "MyTableType",
                Value = table,
            });

        cmd.ExecuteNonQuery();
    }

Dans l’exemple précédent de hello, hello **SqlCommand** objet insère des lignes à partir d’un paramètre table,  **@TestTvp** . Hello précédemment créé **DataTable** objet reçoit le paramètre toothis avec hello **SqlCommand.Parameters.Add** (méthode). Traitement par lot insertions hello dans un appellent considérablement augmente hello des performances sur les insertions séquentielles.

tooimprove hello exemple précédent, utilisez une procédure stockée au lieu d’une commande de texte. Hello commande de Transact-SQL suivante crée une procédure stockée qui accepte hello **SimpleTestTableType** paramètre table.

    CREATE PROCEDURE [dbo].[sp_InsertRows] 
    @TestTvp as MyTableType READONLY
    AS
    BEGIN
    INSERT INTO MyTable(mytext, num) 
    SELECT mytext, num FROM @TestTvp
    END
    GO

Puis modifiez hello **SqlCommand** déclaration dans hello précédent code exemple toohello suivant de l’objet.

    SqlCommand cmd = new SqlCommand("sp_InsertRows", connection);
    cmd.CommandType = CommandType.StoredProcedure;

Dans la plupart des cas, les paramètres table présentent des performances équivalentes ou supérieures à celles des autres techniques de traitement par lots. Les paramètres table sont souvent préférables car ils apportent davantage de flexibilité que les autres options. Par exemple, les autres techniques, telles que de copie en bloc SQL, n’autorisent insertion hello de nouvelles lignes. Mais avec des paramètres table, vous pouvez utiliser la logique de toodetermine de procédure stockée hello les lignes qui sont mises à jour et d’insertions. type de table Hello peut également être modifié toocontain une colonne « Opération » qui indique si hello spécifiée ligne doit être inséré, mis à jour ou supprimée.

Hello tableau suivant indique les résultats des tests ad hoc pour une utilisation hello de paramètres table en millisecondes.

| Opérations | On-Premises tooAzure (ms) | Azure (même centre de données) |
| --- | --- | --- |
| 1 |124 |32 |
| 10 |131 |25 |
| 100 |338 |51 |
| 1 000 |2 615 |382 |
| 10000 |23 830 |3 586 |

> [!NOTE]
> Les résultats ne représentent pas des valeurs de référence. Consultez hello [Remarque à propos des résultats du minutage dans cette rubrique](#note-about-timing-results-in-this-topic).
> 
> 

le gain de performances Hello du traitement par lot est visible immédiatement. Dans le test séquentiel précédent de hello, 1000 opérations a nécessité 129 secondes hello en dehors de centre de données et 21 secondes dans le centre de données hello. Cependant, avec les paramètres table, les opérations de 1000 uniquement 2,6 secondes en dehors du centre de données hello et 0,4 seconde dans le centre de données hello.

Pour plus d’informations sur les paramètres table, consultez [Paramètres table](https://msdn.microsoft.com/library/bb510489.aspx).

### <a name="sql-bulk-copy"></a>Copie en bloc SQL
Copie en bloc SQL est une autre façon tooinsert grandes quantités de données dans une base de données cible. Applications .NET peuvent utiliser hello **SqlBulkCopy** opérations d’insertion en bloc tooperform de classe. **SqlBulkCopy** est similaire dans l’outil de ligne de commande de fonction toohello, **Bcp.exe**, ou instruction Transact-SQL, de hello **BULK INSERT**. Hello exemple de code suivant montre comment les lignes dans la source de hello hello de copie toobulk **DataTable**, table, table de destination toohello dans SQL Server, MyTable.

    using (SqlConnection connection = new SqlConnection(CloudConfigurationManager.GetSetting("Sql.ConnectionString")))
    {
        connection.Open();

        using (SqlBulkCopy bulkCopy = new SqlBulkCopy(connection))
        {
            bulkCopy.DestinationTableName = "MyTable";
            bulkCopy.ColumnMappings.Add("mytext", "mytext");
            bulkCopy.ColumnMappings.Add("num", "num");
            bulkCopy.WriteToServer(table);
        }
    }

Il existe quelques cas où la copie en bloc est préférable à l’utilisation des paramètres table. Consultez le tableau de comparaison hello de paramètres table et les opérations BULK INSERT dans la rubrique de hello [paramètres table](https://msdn.microsoft.com/library/bb510489.aspx).

Hello résultats des tests ad hoc suivants montrent les performances de hello du traitement par lot avec **SqlBulkCopy** en millisecondes.

| Opérations | On-Premises tooAzure (ms) | Azure (même centre de données) |
| --- | --- | --- |
| 1 |433 |57 |
| 10 |441 |32 |
| 100 |636 |53 |
| 1 000 |2 535 |341 |
| 10000 |21 605 |2 737 |

> [!NOTE]
> Les résultats ne représentent pas des valeurs de référence. Consultez hello [Remarque à propos des résultats du minutage dans cette rubrique](#note-about-timing-results-in-this-topic).
> 
> 

Dans le traitement par lots plus petits, les paramètres table hello utilisez obtenu les meilleures performances hello **SqlBulkCopy** classe. Toutefois, **SqlBulkCopy** effectuée 12-31 % plus rapide que les paramètres table pour les tests hello de 1 000 et 10 000 lignes. Comme les paramètres table, **SqlBulkCopy** est une bonne option pour les insertions traitées par lot, en particulier lors de la comparaison toohello les performances des opérations de non-batch.

Pour plus d’informations sur la copie en bloc dans ADO.NET, consultez [Opérations de copie en bloc dans SQL Server](https://msdn.microsoft.com/library/7ek5da1a.aspx).

### <a name="multiple-row-parameterized-insert-statements"></a>Instructions INSERT paramétrables sur plusieurs lignes
Pour les lots de petite taille consiste tooconstruct un grand paramétrables instruction INSERT qui insère plusieurs lignes. Hello, exemple de code suivant illustre cette technique.

    using (SqlConnection connection = new SqlConnection(CloudConfigurationManager.GetSetting("Sql.ConnectionString")))
    {
        connection.Open();

        string insertCommand = "INSERT INTO [MyTable] ( mytext, num ) " +
            "VALUES (@p1, @p2), (@p3, @p4), (@p5, @p6), (@p7, @p8), (@p9, @p10)";

        SqlCommand cmd = new SqlCommand(insertCommand, connection);

        for (int i = 1; i <= 10; i += 2)
        {
            cmd.Parameters.Add(new SqlParameter("@p" + i.ToString(), "test"));
            cmd.Parameters.Add(new SqlParameter("@p" + (i+1).ToString(), i));
        }

        cmd.ExecuteNonQuery();
    }


Cet exemple est destiné le concept de base tooshow hello. Un scénario plus réaliste effectuerait une boucle simultanément via la chaîne de requête hello requis entités tooconstruct hello et paramètres de commande hello. Vous êtes limité total tooa 2100 des paramètres de requête, cela limite le nombre total de hello de lignes qui peuvent être traitées de cette manière.

Hello suivant ad-hoc résultats afficher hello les performances des tests de ce type d’instruction d’insertion en millisecondes.

| Opérations | Paramètres table (ms) | Instruction INSERT unique (ms) |
| --- | --- | --- |
| 1 |32 |20 |
| 10 |30 |25 |
| 100 |33 |51 |

> [!NOTE]
> Les résultats ne représentent pas des valeurs de référence. Consultez hello [Remarque à propos des résultats du minutage dans cette rubrique](#note-about-timing-results-in-this-topic).
> 
> 

Cette approche peut être légèrement plus rapide pour les lots comportant moins de 100 lignes. Bien que l’amélioration de hello est petite, cette technique est une autre option qui peut fonctionner dans votre scénario d’application spécifique.

### <a name="dataadapter"></a>DataAdapter
Hello **DataAdapter** classe vous permet de toomodify un **DataSet** de l’objet, puis soumettez les modifications hello en tant qu’opérations INSERT, UPDATE et DELETE. Si vous utilisez hello **DataAdapter** de cette manière, il est important de toonote qui séparent les appels sont effectués pour chaque opération distincte. tooimprove des performances, utilisez hello **UpdateBatchSize** nombre toohello de propriété d’opérations qui doivent être traités par lot à la fois. Pour plus d’informations, consultez [Exécution de traitements par lots à l’aide de DataAdapters](https://msdn.microsoft.com/library/aadf8fk2.aspx).

### <a name="entity-framework"></a>Entity Framework
Entity Framework ne prend pas actuellement en charge le traitement par lots. Différents développeurs de la Communauté de hello ont tenté de solutions de contournement toodemonstrate comme remplacement hello **SaveChanges** (méthode). Mais hello solutions sont généralement complexes et adaptées toohello application et le modèle de données. projet de codeplex Entity Framework Hello possède actuellement une page de discussion sur cette demande de fonctionnalité. tooview cette discussion, consultez [2 août 2012 - Notes de réunion conception](http://entityframework.codeplex.com/wikipage?title=Design%20Meeting%20Notes%20-%20August%202%2c%202012).

### <a name="xml"></a>XML
Par souci d’exhaustivité, nous pensons qu’il est important tootalk à propos de XML en tant qu’une stratégie de traitement par lot. Toutefois, utilisez hello XML a aucun avantage par rapport autres méthodes et plusieurs inconvénients. approche de Hello est tootable table des paramètres similaires, mais un fichier XML ou une chaîne est passée de procédure stockée de tooa au lieu d’une table définie par l’utilisateur. procédure stockée Hello analyse les commandes de hello dans la procédure stockée hello.

Il existe plusieurs inconvénients toothis approche :

* L’utilisation de XML peut s’avérer fastidieuse et sujette aux erreurs.
* Analyse hello XML sur la base de données hello peut être gourmande en ressources processeur.
* Dans la plupart des cas, cette méthode est plus lente que celle des paramètres table.

Pour ces raisons, utilisation de la hello de XML pour les requêtes de traitement par lots n’est pas recommandée.

## <a name="batching-considerations"></a>Remarques relatives au traitement par lots
Hello les sections suivantes fournit plus d’informations pour une utilisation hello du traitement par lots dans les applications de base de données SQL.

### <a name="tradeoffs"></a>Compromis
En fonction de votre architecture, le traitement par lots peut vous obliger à faire un compromis entre performances et résilience. Par exemple, considérez le scénario hello où votre rôle rencontre une défaillance inattendue. Si vous perdez une ligne de données, l’impact de hello est inférieure à impact hello de perdre un grand lot de lignes non envoyées. Il existe un risque plus élevé lorsque le tampon de lignes avant de les envoyer toohello de base de données dans une fenêtre de temps spécifié.

En raison de ce compromis, évaluez le type hello des opérations de ce lot vous. Optez pour une approche plus agressive (lots plus volumineux et intervalles plus longs) pour les données moins critiques.

### <a name="batch-size"></a>Taille du lot
Dans nos tests, il a été généralement aucun avantage toobreaking grands lots en plus petits. En fait, cette sous-division s’est souvent traduite par des performances plus lentes que celles obtenues avec l’envoi d’un seul lot plus volumineux. Par exemple, considérez un scénario où vous souhaitez tooinsert 1000 lignes. Hello tableau suivant montre combien il prend les paramètres table toouse tooinsert 1000 lignes lorsqu’ils sont divisés en lots plus petits.

| Taille du lot | Itérations | Paramètres table (ms) |
| --- | --- | --- |
| 1 000 |1 |347 |
| 500 |2 |355 |
| 100 |10 |465 |
| 50 |20 |630 |

> [!NOTE]
> Les résultats ne représentent pas des valeurs de référence. Consultez hello [Remarque à propos des résultats du minutage dans cette rubrique](#note-about-timing-results-in-this-topic).
> 
> 

Vous pouvez voir que des performances optimales hello pour 1 000 lignes soient toosubmit les tous en même temps. Dans d’autres tests (non illustrés ici) s’est un toobreak de gain de performances un lot de 10 000 lignes et deux lots de 5 000 lignes. Mais le schéma de la table hello pour ces tests est relativement simple, vous devez réaliser des tests sur vos données et spécifiques tooverify des tailles de lot ces conclusions.

Un autre facteur tooconsider est que si le lot total de hello devient trop volumineux, base de données SQL peut limiter et refuser le traitement par lots de toocommit hello. Pour de meilleurs résultats de hello, test toodetermine de votre scénario spécifique, s’il existe une taille de lot idéale. Rendre la taille de lot hello configurable au runtime tooenable rapides réglages basés sur les performances ou des erreurs.

Enfin, équilibrez taille hello du lot de hello hello les risques associés au traitement par lot. Si des erreurs temporaires ou hello rôle échoue, envisagez les conséquences hello d’une nouvelle tentative d’opération de hello ou de perte de données hello dans un lot de hello.

### <a name="parallel-processing"></a>Traitement en parallèle
Que se passe-t-il si vous a duré approche hello de réduction de la taille de lot hello mais utilisé plusieurs threads tooexecute hello travail ? Là encore, nos tests ont montré que plusieurs petits lots multithreads produisaient de moins bonnes performances que celles obtenues avec un seul lot plus volumineux. Hello test suivant tente de tooinsert 1000 lignes dans un ou plusieurs traitements parallèles. Il montre comment un plus grand nombre de lots simultanés affecte les performances.

| Taille de lot [itérations] | Deux threads (ms) | Quatre threads (ms) | Six threads (ms) |
| --- | --- | --- | --- |
| 1 000 [1] |277 |315 |266 |
| 500 [2] |548 |278 |256 |
| 250 [4] |405 |329 |265 |
| 100 [10] |488 |439 |391 |

> [!NOTE]
> Les résultats ne représentent pas des valeurs de référence. Consultez hello [Remarque à propos des résultats du minutage dans cette rubrique](#note-about-timing-results-in-this-topic).
> 
> 

Il existe plusieurs raisons potentielles à une dégradation des performances hello tooparallelism échéance :

* Exécution de plusieurs appels réseau simultanés au lieu d’un seul.
* Plusieurs opérations sur une seule table peuvent entraîner une contention et un blocage.
* Surcharges associées multithreading.
* dépenses Hello d’ouvrir plusieurs connexions compense avantage hello du traitement parallèle.

Si vous ciblez différentes tables ou bases de données, il est possible toosee des performances gain avec cette stratégie. Le partitionnement ou les fédérations de bases de données constitue un scénario possible pour une telle approche. Partitionnement utilise plusieurs bases de données et les itinéraires différents tooeach de données. Si chaque petit lot est tooa autre base de données, puis en effectuant les opérations hello en parallèle peut être plus efficace. Toutefois, gain de performances hello n’est pas assez important toouse comme base hello pour un partitionnement de base de données arbre de décision toouse dans votre solution.

Dans certains modèles, l’exécution parallèle de lots plus petits peut entraîner une amélioration du débit des demandes dans un système sous charge. Dans ce cas, même s’il est plus rapide tooprocess un seul grand traitement, le traitement de plusieurs lots en parallèle peut être plus efficace.

Si vous n’utilisez pas l’exécution en parallèle, envisagez le nombre maximal de contrôle hello de threads de travail. Un plus petit nombre peut réduire la contention et accélérer la durée d’exécution. Envisagez également de charge supplémentaire hello sur la base de données cible hello dans les connexions et transactions.

### <a name="related-performance-factors"></a>Facteurs de performances associés
Les conseils classiques sur les performances de base de données s’appliquent également au traitement par lots. Par exemple, les performances d’insertion sont réduites pour les tables qui ont une grande clé primaire ou de nombreux index non ordonnés en clusters.

Si les paramètres table utilisent une procédure stockée, vous pouvez utiliser la commande hello **SET NOCOUNT ON** au début de hello de procédure de hello. Cette instruction supprime le retour hello du nombre de hello de lignes hello affectée dans la procédure de hello. Toutefois, dans nos tests, hello utilisation de **SET NOCOUNT ON** n’avait aucun effet ou une diminution des performances. Hello procédure stockée de test était simple avec un seul **insérer** du paramètre de table hello. Il est possible que les procédures stockées plus complexes puissent bénéficier de cette instruction. Mais ne supposez pas que l’ajout **SET NOCOUNT ON** tooyour stockée procédure automatiquement améliore les performances. toounderstand hello effet, testez votre procédure stockée avec et sans hello **SET NOCOUNT ON** instruction.

## <a name="batching-scenarios"></a>Scénarios de traitement par lots
Hello sections suivantes décrivent comment les paramètres table toouse dans trois scénarios d’application. premier scénario de Hello montre comment la mémoire tampon et le traitement par lots peuvent collaborer. deuxième scénario de Hello améliore les performances en effectuant les opérations maître / détails dans un appel de procédure stockée unique. Hello scénario final montre comment les paramètres table toouse dans une opération « UPSERT ».

### <a name="buffering"></a>Mise en mémoire tampon
Bien que certains scénarios apparaissent comme des candidats évidents pour le traitement par lots, il existe de nombreux scénarios qui peuvent tirer parti des avantages d’un traitement par lots différé. Toutefois, également le traitement différé a un plus grand risque que les données de salutation sont perdues au cours de l’événement hello d’une défaillance inattendue. Il est important toounderstand ce risque et prendre en compte les conséquences hello.

Par exemple, considérez une application web qui effectue le suivi de l’historique de navigation hello de chaque utilisateur. Sur chaque demande de page, application hello peut rendre une base de données appel toorecord hello page Affichage de l’utilisateur. Mais les performances et évolutivité supérieures peuvent être obtenues en mise en mémoire tampon des opérations de navigation des utilisateurs hello et en envoyant cette base de données toohello de données dans des lots. Vous pouvez déclencher la mise à jour de la base de données hello par temps écoulé et/ou taille de mémoire tampon. Par exemple, une règle peut spécifier que ce lot hello doit être traité après 20 secondes ou lorsque la mémoire tampon de hello atteint 1 000 éléments.

code Hello suivant utilise [Extensions réactives - Rx](https://msdn.microsoft.com/data/gg577609) tooprocess mis en mémoire tampon les événements déclenchés par une classe d’analyse. Hello lorsque les remplissages de la mémoire tampon ou un délai d’attente est atteint, lot hello de données utilisateur est envoyé de la base de données toohello avec un paramètre table.

Bonjour les détails de la navigation NavHistoryData classe modèles hello utilisateur suivants. Il contient des informations de base comme identificateur d’utilisateur hello, hello URL accessible et hello temps d’accès.

    public class NavHistoryData
    {
        public NavHistoryData(int userId, string url, DateTime accessTime)
        { UserId = userId; URL = url; AccessTime = accessTime; }
        public int UserId { get; set; }
        public string URL { get; set; }
        public DateTime AccessTime { get; set; }
    }

Hello NavHistoryDataMonitor classe est responsable de la mise en mémoire tampon de base de données de navigation données toohello hello utilisateur. Elle contient une méthode appelée RecordUserNavigationEntry qui répond en déclenchant un événement **OnAdded** . Hello de code suivant montre la logique du constructeur hello qui utilise Rx toocreate une collection observable selon les événements hello. Elle s’abonne ensuite toothis les collection observable avec la méthode de tampon hello. surcharge de Hello Spécifie que cette mémoire tampon hello doit être envoyée à toutes les 20 secondes ou 1 000 entrées.

    public NavHistoryDataMonitor()
    {
        var observableData =
            Observable.FromEventPattern<NavHistoryDataEventArgs>(this, "OnAdded");

        observableData.Buffer(TimeSpan.FromSeconds(20), 1000).Subscribe(Handler);           
    }

Hello Gestionnaire convertit tous les éléments de hello mis en mémoire tampon en un type de table incluse, mais cette procédure tooa stocké de type ce lot hello de processus. Hello de code suivant montre définition complète de hello pour hello NavHistoryDataEventArgs et classes de NavHistoryDataMonitor hello.

    public class NavHistoryDataEventArgs : System.EventArgs
    {
        public NavHistoryDataEventArgs(NavHistoryData data) { Data = data; }
        public NavHistoryData Data { get; set; }
    }

    public class NavHistoryDataMonitor
    {
        public event EventHandler<NavHistoryDataEventArgs> OnAdded;

        public NavHistoryDataMonitor()
        {
            var observableData =
                Observable.FromEventPattern<NavHistoryDataEventArgs>(this, "OnAdded");

            observableData.Buffer(TimeSpan.FromSeconds(20), 1000).Subscribe(Handler);           
        }

        public void RecordUserNavigationEntry(NavHistoryData data)
        {    
            if (OnAdded != null)
                OnAdded(this, new NavHistoryDataEventArgs(data));
        }

        protected void Handler(IList<EventPattern<NavHistoryDataEventArgs>> items)
        {
            DataTable navHistoryBatch = new DataTable("NavigationHistoryBatch");
            navHistoryBatch.Columns.Add("UserId", typeof(int));
            navHistoryBatch.Columns.Add("URL", typeof(string));
            navHistoryBatch.Columns.Add("AccessTime", typeof(DateTime));
            foreach (EventPattern<NavHistoryDataEventArgs> item in items)
            {
                NavHistoryData data = item.EventArgs.Data;
                navHistoryBatch.Rows.Add(data.UserId, data.URL, data.AccessTime);
            }

            using (SqlConnection connection = new SqlConnection(CloudConfigurationManager.GetSetting("Sql.ConnectionString")))
            {
                connection.Open();

                SqlCommand cmd = new SqlCommand("sp_RecordUserNavigation", connection);
                cmd.CommandType = CommandType.StoredProcedure;

                cmd.Parameters.Add(
                    new SqlParameter()
                    {
                        ParameterName = "@NavHistoryBatch",
                        SqlDbType = SqlDbType.Structured,
                        TypeName = "NavigationHistoryTableType",
                        Value = navHistoryBatch,
                    });

                cmd.ExecuteNonQuery();
            }
        }
    }

toouse cette classe mise en mémoire tampon, l’application hello crée un objet NavHistoryDataMonitor statique. Chaque fois un utilisateur accède à une page, application hello appelle la méthode de NavHistoryDataMonitor.RecordUserNavigationEntry hello. Hello logique de mise en mémoire tampon déroule tootake administration de l’envoi de ces bases de données de toohello entrées par lots.

### <a name="master-detail"></a>Maître/détail
Les paramètres table sont utiles pour les scénarios INSERT simples. Toutefois, il peut être plus difficiles insertions toobatch qui impliquent, et plusieurs tables. scénario de « maître/détail » Hello est un bon exemple. table principale de Hello identifie l’entité principale de hello. Une ou plusieurs tables de détails stockent des données sur les entités hello. Dans ce scénario, les relations de clé étrangères appliquent la relation de hello de détails tooa seule entité principale. Imaginez une version simplifiée d’une table PurchaseOrder et de sa table OrderDetail associée. Hello suivant Transact-SQL crée la table de PurchaseOrder hello avec quatre colonnes : OrderID, OrderDate, CustomerID et état.

    CREATE TABLE [dbo].[PurchaseOrder](
    [OrderID] [int] IDENTITY(1,1) NOT NULL,
    [OrderDate] [datetime] NOT NULL,
    [CustomerID] [int] NOT NULL,
    [Status] [nvarchar](50) NOT NULL,
     CONSTRAINT [PrimaryKey_PurchaseOrder] 
    PRIMARY KEY CLUSTERED ( [OrderID] ASC ))

Chaque commande contient un ou plusieurs achats de produits. Ces informations sont capturées dans la table PurchaseOrderDetail de hello. Hello suivant Transact-SQL crée la table PurchaseOrderDetail de hello avec cinq colonnes : OrderID, OrderDetailID, ProductID, UnitPrice et OrderQty.

    CREATE TABLE [dbo].[PurchaseOrderDetail](
    [OrderID] [int] NOT NULL,
    [OrderDetailID] [int] IDENTITY(1,1) NOT NULL,
    [ProductID] [int] NOT NULL,
    [UnitPrice] [money] NULL,
    [OrderQty] [smallint] NULL,
     CONSTRAINT [PrimaryKey_PurchaseOrderDetail] PRIMARY KEY CLUSTERED 
    ( [OrderID] ASC, [OrderDetailID] ASC ))

colonne de OrderID Hello dans la table PurchaseOrderDetail de hello doit faire référence à une commande à partir de la table de PurchaseOrder hello. Hello définition d’une clé étrangère applique cette contrainte.

    ALTER TABLE [dbo].[PurchaseOrderDetail]  WITH CHECK ADD 
    CONSTRAINT [FK_OrderID_PurchaseOrder] FOREIGN KEY([OrderID])
    REFERENCES [dbo].[PurchaseOrder] ([OrderID])

Dans l’ordre toouse les paramètres table, vous devez disposer d’un type de table défini par l’utilisateur pour chaque table cible.

    CREATE TYPE PurchaseOrderTableType AS TABLE 
    ( OrderID INT,
      OrderDate DATETIME,
      CustomerID INT,
      Status NVARCHAR(50) );
    GO

    CREATE TYPE PurchaseOrderDetailTableType AS TABLE 
    ( OrderID INT,
      ProductID INT,
      UnitPrice MONEY,
      OrderQty SMALLINT );
    GO

Vous devez ensuite définir ensuite une procédure stockée qui accepte les tables de ces types. Cette procédure permet à un lot d’application toolocally un ensemble de commandes et les détails de la commande dans un seul appel. Hello Transact-SQL suivant fournit déclaration de procédure stockée complète hello pour cet exemple de bon de commande.

    CREATE PROCEDURE sp_InsertOrdersBatch (
    @orders as PurchaseOrderTableType READONLY,
    @details as PurchaseOrderDetailTableType READONLY )
    AS
    SET NOCOUNT ON;

    -- Table that connects hello order identifiers in hello @orders
    -- table with hello actual order identifiers in hello PurchaseOrder table
    DECLARE @IdentityLink AS TABLE ( 
    SubmittedKey int, 
    ActualKey int, 
    RowNumber int identity(1,1)
    );

          -- Add new orders toohello PurchaseOrder table, storing hello actual
    -- order identifiers in hello @IdentityLink table   
    INSERT INTO PurchaseOrder ([OrderDate], [CustomerID], [Status])
    OUTPUT inserted.OrderID INTO @IdentityLink (ActualKey)
    SELECT [OrderDate], [CustomerID], [Status] FROM @orders ORDER BY OrderID;

    -- Match hello passed-in order identifiers with hello actual identifiers
    -- and complete hello @IdentityLink table for use with inserting hello details
    WITH OrderedRows As (
    SELECT OrderID, ROW_NUMBER () OVER (ORDER BY OrderID) As RowNumber 
    FROM @orders
    )
    UPDATE @IdentityLink SET SubmittedKey = M.OrderID
    FROM @IdentityLink L JOIN OrderedRows M ON L.RowNumber = M.RowNumber;

    -- Insert hello order details into hello PurchaseOrderDetail table, 
          -- using hello actual order identifiers of hello master table, PurchaseOrder
    INSERT INTO PurchaseOrderDetail (
    [OrderID],
    [ProductID],
    [UnitPrice],
    [OrderQty] )
    SELECT L.ActualKey, D.ProductID, D.UnitPrice, D.OrderQty
    FROM @details D
    JOIN @IdentityLink L ON L.SubmittedKey = D.OrderID;
    GO

Dans cet exemple, hello définies localement @IdentityLink table stocke les valeurs OrderID réels hello à partir des lignes de hello qui vient d’être inséré. Ces identificateurs de commande sont différents des valeurs de OrderID temporaires hello Bonjour @orders et @details paramètres table. Pour cette raison, hello @IdentityLink table connecte ensuite les valeurs OrderID hello de hello @orders toohello réel OrderID valeurs de paramètre pour les nouvelles lignes de hello dans la table de PurchaseOrder hello. Après cette étape, hello @IdentityLink table facilitent l’insertion détails de la commande hello avec hello OrderID réelle qui satisfait à la contrainte de clé étrangère hello.

Cette procédure stockée peut être utilisée à partir d’un code ou d’autres appels Transact-SQL. Consultez la section de paramètres table hello de ce document pour obtenir un exemple de code. Hello Transact-SQL de suivant montre comment toocall hello sp_InsertOrdersBatch.

    declare @orders as PurchaseOrderTableType
    declare @details as PurchaseOrderDetailTableType

    INSERT @orders 
    ([OrderID], [OrderDate], [CustomerID], [Status])
    VALUES(1, '1/1/2013', 1125, 'Complete'),
    (2, '1/13/2013', 348, 'Processing'),
    (3, '1/12/2013', 2504, 'Shipped')

    INSERT @details
    ([OrderID], [ProductID], [UnitPrice], [OrderQty])
    VALUES(1, 10, $11.50, 1),
    (1, 12, $1.58, 1),
    (2, 23, $2.57, 2),
    (3, 4, $10.00, 1)

    exec sp_InsertOrdersBatch @orders, @details

Cette solution permet à chaque toouse lot un ensemble de valeurs OrderID qui commencent à 1. Ces valeurs OrderID temporaires décrivent les relations hello dans un lot de hello, mais les valeurs OrderID réelles hello sont déterminées lors de l’opération d’insertion hello hello. Vous pouvez exécuter hello mêmes instructions dans l’exemple précédent de hello à plusieurs reprises et générer des commandes uniques dans la base de données hello. Vous devez donc penser à ajouter plus de code ou de logique de base de données pour éviter les doublons lorsque vous utilisez cette technique de traitement par lots.

Cet exemple montre que les opérations de base de données encore plus complexes, telles que les opérations maître/détail, peuvent être traitées par lots à l’aide des paramètres table.

### <a name="upsert"></a>Opération UPSERT
Un autre scénario de traitement par lots implique la mise à jour simultanée de lignes existantes et l’insertion de nouvelles lignes. Cette opération est parfois désignée tooas une opération « UPSERT » (update + insert). Plutôt que d’effectuer des appels distincts tooINSERT et mise à jour, instruction de fusion hello est mieux adapté toothis tâche. Hello instruction MERGE peut effectuer les deux insérer et mettre à jour des opérations dans un seul appel.

Paramètres table peuvent servir hello fusion instruction tooperform mises à jour et insertions. Par exemple, supposons une table d’employé simplifiée qui contient hello suivant colonnes : EmployeeID, FirstName, LastName, SocialSecurityNumber :

    CREATE TABLE [dbo].[Employee](
    [EmployeeID] [int] IDENTITY(1,1) NOT NULL,
    [FirstName] [nvarchar](50) NOT NULL,
    [LastName] [nvarchar](50) NOT NULL,
    [SocialSecurityNumber] [nvarchar](50) NOT NULL,
     CONSTRAINT [PrimaryKey_Employee] PRIMARY KEY CLUSTERED 
    ([EmployeeID] ASC ))

Dans cet exemple, vous pouvez utiliser des faits hello que hello SocialSecurityNumber est unique tooperform une fusion de plusieurs employés. Tout d’abord, créez les type de table défini par l’utilisateur de hello :

    CREATE TYPE EmployeeTableType AS TABLE 
    ( Employee_ID INT,
      FirstName NVARCHAR(50),
      LastName NVARCHAR(50),
      SocialSecurityNumber NVARCHAR(50) );
    GO

Ensuite, créez une procédure stockée ou écrire du code qui utilise hello mise à jour de fusion instruction tooperform hello et insert. Hello exemple suivant utilise hello instruction MERGE sur un paramètre table, @employees, de type EmployeeTableType. Hello contenu Hello @employees table ne sont pas affichés ici.

    MERGE Employee AS target
    USING (SELECT [FirstName], [LastName], [SocialSecurityNumber] FROM @employees) 
    AS source ([FirstName], [LastName], [SocialSecurityNumber])
    ON (target.[SocialSecurityNumber] = source.[SocialSecurityNumber])
    WHEN MATCHED THEN 
    UPDATE SET
    target.FirstName = source.FirstName, 
    target.LastName = source.LastName
    WHEN NOT MATCHED THEN
       INSERT ([FirstName], [LastName], [SocialSecurityNumber])
       VALUES (source.[FirstName], source.[LastName], source.[SocialSecurityNumber]);

Pour plus d’informations, consultez la documentation de hello et des exemples pour l’instruction de fusion hello. Bien que hello même travail puisse être effectué dans en plusieurs étapes stockées appel de procédure avec les opérations INSERT et UPDATE distinctes, hello instruction MERGE est plus efficace. Code de base de données peut également construire des appels Transact-SQL qui utilisent l’instruction MERGE de hello directement sans avoir recours à deux appels de base de données pour INSERT et UPDATE.

## <a name="recommendation-summary"></a>Résumé des recommandations
Hello liste suivante fournit un résumé de hello le traitement par lot les recommandations décrites dans cette rubrique :

* Utilisez la mise en mémoire tampon et de traitement par lot des performances de hello tooincrease et l’évolutivité des applications de base de données SQL.
* Comprendre les compromis de hello entre le traitement par lot/mise en mémoire tampon et la résilience. Lors d’une défaillance de rôle, risque hello de perdre un lot non traité de données critiques peut-être dépasser le gain de performances hello du traitement par lot.
* Tentative de tookeep de base de données de tous les appels toohello au sein d’une latence tooreduce de centre de données unique.
* Si vous choisissez une technique de traitement par lot, les paramètres table offrent une souplesse et des performances optimales hello.
* Pourquoi plus rapide insérer les performances, suivez ces recommandations générales, mais votre scénario de test :
  * Pour moins de 100 lignes, utilisez une seule commande INSERT paramétrable.
  * Pour moins de 1 000 lignes, utilisez des paramètres table.
  * Au-delà de 1 000 lignes, utilisez SqlBulkCopy.
* Pour mettre à jour et les opérations de suppression, utiliser des paramètres table avec logique de la procédure stockée qui détermine le bon fonctionnement de hello sur chaque ligne de paramètre de table hello.
* Conseils relatifs à la taille de lot :
  * Utilisez hello plus grandes tailles de lot qui ont un sens pour votre application et les besoins de l’entreprise.
  * Le gain de performances de hello solde de grands lots avec des risques de hello de défaillances temporaires ou catastrophiques. Quelle est la conséquence de hello de nouvelles tentatives ou de perte de données hello dans un lot de hello ? 
  * Test hello plus grand lot taille tooverify que base de données SQL ne rejette pas.
  * Créer des paramètres de configuration qui contrôle le traitement par lot, telles que la taille de lot hello ou de la fenêtre de temps de mise en mémoire tampon hello. Ces paramètres garantissent la flexibilité. Vous pouvez modifier hello le traitement par lot de comportement en production sans redéployer le service de cloud computing hello.
* Évitez l’exécution parallèle de lots qui s’exécutent sur une seule table dans une base de données unique. Si vous choisissez toodivide un lot unique sur plusieurs threads de travail, exécutez les tests toodetermine hello nombre idéal de threads. Après un seuil non spécifié, un plus grand nombre de threads aura pour effet de diminuer les performances au lieu de les augmenter.
* Envisagez la mise en mémoire tampon sur la taille et l’heure comme un moyen d’implémenter le traitement par lot pour d’autres scénarios.

## <a name="next-steps"></a>Étapes suivantes
Cet article consacré à la conception de base de données et les techniques de codage liées toobatching peut améliorer vos performances de l’application et l’évolutivité. Mais cet aspect ne représente qu’un facteur parmi d’autres dans votre stratégie globale. Pour plus de performances tooimprove de méthodes et de l’évolutivité, consultez [Guide des performances de base de données SQL Azure pour les bases de données uniques](sql-database-performance-guidance.md) et [considérations de prix et de performances pour un pool élastique](sql-database-elastic-pool-guidance.md).

