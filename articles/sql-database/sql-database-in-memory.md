---
title: "technologies de base de données SQL en mémoire aaaAzure | Documents Microsoft"
description: "Les technologies de base de données SQL en mémoire Azure améliorer sensiblement les performances hello de transactionnelle et les charges de travail analytique. Découvrez comment parti tootake de ces technologies."
services: sql-database
documentationCenter: 
author: jodebrui
manager: jhubbard
editor: 
ms.assetid: 250ef341-90e5-492f-b075-b4750d237c05
ms.service: sql-database
ms.custom: develop databases
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/24/2017
ms.author: jodebrui
ms.openlocfilehash: 1bacd7297b2f9b018853088eabf2a2ee66a9cb43
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="optimize-performance-by-using-in-memory-technologies-in-sql-database"></a>Optimisation des performances à l’aide des technologies en mémoire dans SQL Database

À l’aide des technologies en mémoire dans Azure SQL Database, vous pouvez obtenir des améliorations des performances pour différentes charges de travail : transactionnelles (traitement transactionnel en ligne (OLTP)), analytiques (traitement analytique en ligne (OLAP)) et mixtes (traitement transactionnel/analytique hybride (HTAP)). Raison de hello plus efficace des requêtes et traitement des transactions, de technologies en mémoire vous aident également tooreduce coût. Vous n’avez généralement pas besoin hello tooupgrade tarification hello de base de données tooachieve des gains de performances. Dans certains cas, vous pouvez même peut-être réduire hello tarification et toujours voir les améliorations des performances avec les technologies en mémoire.

Voici deux exemples illustrant comment l’OLTP en mémoire ont aidé à toosignificantly améliorer les performances :

- À l’aide de l’OLTP en mémoire, [Solutions d’entreprise de Quorum a été toodouble en mesure de leur charge de travail tout en améliorant la dtu de 70 %](https://customers.microsoft.com/story/quorum-doubles-key-databases-workload-while-lowering-dtu-with-sql-database).
    - DTU signifie *unité de débit de base de données* et inclut une mesure de la consommation des ressources.
- Hello vidéo suivante montre une amélioration significative de la consommation des ressources avec une charge de travail d’exemple : [OLTP en mémoire dans la base de données de SQL Azure vidéo](https://channel9.msdn.com/Shows/Data-Exposed/In-Memory-OTLP-in-Azure-SQL-DB).
    - Pour plus d’informations, voir blog de hello : [OLTP en mémoire dans le billet de Blog de base de données SQL Azure](https://azure.microsoft.com/blog/in-memory-oltp-in-azure-sql-database/)

Technologies en mémoire sont disponibles dans toutes les bases de données de niveau Premium de hello, y compris les bases de données dans les pools élastiques Premium.

Hello vidéo suivante explique les gains de performances potentiels avec les technologies en mémoire dans la base de données SQL Azure. N’oubliez pas que les gains de performance hello que vous voyez toujours dépendent de nombreux facteurs, notamment la nature hello de charge de travail hello et des données, le modèle d’accès de base de données hello et ainsi de suite.

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Azure-SQL-Database-In-Memory-Technologies/player]
>
>

Base de données SQL Azure a hello suivant des technologies en mémoire :

- *L’OLTP en mémoire* augmente le débit et réduit la latence de traitement des transactions. Les scénarios qui bénéficient de l’OLTP en mémoire sont : le traitement de transactions haut débit, notamment les données commerciales et de jeux, l’ingestion de données d’événements ou d’appareils IoT, la mise en cache, le chargement de données, les tables temporaires et les scénarios de variables de table.
- *Index cluster columnstore* réduit l’encombrement de votre stockage (haut too10 fois) et d’améliorer les performances des requêtes de création de rapports et analytique. Vous pouvez l’utiliser avec les tables de faits dans votre toofit de mini-Data Warehouses données davantage de données dans votre base de données et améliorer les performances. En outre, vous pouvez utiliser avec les données d’historique dans tooarchive de votre base de données opérationnelle et être en mesure de tooquery des heures de too10 davantage de données.
- *Les index non cluster columnstore* pour HTAP aide vous toogain des informations en temps réel dans votre entreprise grâce à l’interrogation hello opérationnelle de base de données directement, sans hello besoin toorun une extraction coûteuse, la transformation et le processus de chargement (ETL) et attendre pour hello toobe de l’entrepôt de données remplie. Les index non cluster columnstore exécution est très rapide des requêtes de l’analytique sur la base de données OLTP hello, tout en réduisant l’impact de hello sur la charge de travail opérationnelle hello.
- Vous pouvez également avoir combinaison hello d’une table mémoire optimisée avec un index columnstore. Cette combinaison vous permet de tooperform très rapide traitement des transactions et trop*simultanément* analytique d’exécution des requêtes très rapidement sur hello même données.

Les index columnstore et OLTP en mémoire ont fait partie du produit de SQL Server hello depuis 2012 et 2014, respectivement. Base de données SQL Azure et de SQL Server partagent hello même implémentation des technologies en mémoire. À l’avenir, les nouvelles fonctionnalités pour ces technologies seront publiées dans Azure SQL Database avant d’être publiées dans SQL Server.

Cette rubrique décrit les aspects de l’OLTP et columnstore index tooAzure spécifique de la base de données SQL et comprend également des exemples :
- Vous verrez impact hello de ces technologies sur des limites de taille de stockage et des données.
- Vous verrez comment toomanage hello déplacement de bases de données qui utilisent ces technologies entre hello différent niveaux tarifaires.
- Vous verrez deux exemples qui illustrent l’utilisation de hello d’OLTP en mémoire, ainsi que les index columnstore dans la base de données SQL Azure.

Hello suivant des ressources pour plus d’informations, consultez.

Obtenir des informations détaillées sur les technologies hello :

- [Vue d’ensemble de l’OLTP en mémoire et les scénarios d’utilisation](https://msdn.microsoft.com/library/mt774593.aspx) (inclut des études de cas de références toocustomer et tooget informations démarré)
- [Documentation pour l’OLTP In-Memory](http://msdn.microsoft.com/library/dn133186.aspx)
- [Description des index columnstore](https://msdn.microsoft.com/library/gg492088.aspx)
- Traitement hybride transactionnel et analytique (HTAP), également appelé [analytique opérationnelle en temps réel](https://msdn.microsoft.com/library/dn817827.aspx)

Une introduction rapide sur OLTP en mémoire : [démarrage rapide 1 : Technologies d’OLTP en mémoire plus rapidement les performances de T-SQL](http://msdn.microsoft.com/library/mt694156.aspx) (un autre article toohelp mise en route)

Vidéos détaillées sur les technologies de hello :

- [OLTP en mémoire dans la base de données SQL Azure](https://channel9.msdn.com/Shows/Data-Exposed/In-Memory-OTLP-in-Azure-SQL-DB) (qui contient une démonstration de performances avantages et les étapes tooreproduce ces résultats vous-même)
- [Vidéos d’OLTP en mémoire : Ce qu’il est/comment et quand toouse il](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/10/03/in-memory-oltp-video-what-it-is-and-whenhow-to-use-it/)
- [Index Columnstore : vidéos d’analyse en mémoire d’Ignite 2016](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/10/04/columnstore-index-in-memory-analytics-i-e-columnstore-index-videos-from-ignite-2016/)

## <a name="storage-and-data-size"></a>Taille des données et du stockage

### <a name="data-size-and-storage-cap-for-in-memory-oltp"></a>Seuil de la taille des données et du stockage pour l’OLTP en mémoire

l’OLTP en mémoire inclut des tables optimisées en mémoire, qui sont utilisées pour stocker des données de l’utilisateur. Ces tables sont toofit requis dans la mémoire. Étant donné que vous gérez mémoire directement dans hello service de base de données SQL, nous avons concept hello d’un quota pour les données utilisateur. Cette idée est référencé tooas *stockage de l’OLTP en mémoire*.

Chaque niveau tarifaire de base de données autonome pris en charge et chaque niveau tarifaire de pool élastique inclut une certaine quantité de stockage OLTP en mémoire. Au moment de hello de l’écriture, vous obtenez un gigaoctet de stockage pour chaque 125 unités de transaction de base de données (Udbd) ou d’une base de données élastique unités de transaction (Edtu).

Hello [les niveaux de service de base de données SQL](sql-database-service-tiers.md) article a liste officielle de hello de stockage hello OLTP en mémoire est disponible pour chaque base de données autonome et pool élastique tarification pris en charge.

Hello suivant le nombre d’éléments vers votre plafond de stockage OLTP en mémoire :

- Lignes de données utilisateur actives dans des tables optimisées en mémoire et variables de table. Notez que les anciennes versions de ligne ne comptent pas vers l’extrémité de fin hello.
- Index de tables optimisées en mémoire.
- Coûts de fonctionnement des opérations ALTER TABLE.

Si vous avez atteint le plafond de hello, vous recevez une erreur de quota de sortie, et vous n’êtes plus en mesure de données de tooinsert ou de mise à jour. toomitigate cette erreur, supprimer des données ou augmenter hello tarification de base de données hello ou un pool.

Pour plus d’informations sur l’analyse de l’utilisation du stockage de l’OLTP en mémoire et de configuration des alertes quand vous atteignez presque cap de hello, consultez [stockage analyse en mémoire](sql-database-in-memory-oltp-monitoring.md).

#### <a name="about-elastic-pools"></a>À propos des pools élastiques

Avec les pools élastiques, hello stockage de l’OLTP en mémoire est partagé entre toutes les bases de données dans le pool de hello. Par conséquent, l’utilisation de hello dans une base de données peut éventuellement affecter les autres bases de données. Voici deux solutions :

- Configurez un Max-eDTU pour les bases de données qui est inférieur au nombre d’eDTU hello pour le pool hello dans sa globalité. Cette valeur maximale limite hello OLTP en mémoire l’utilisation du stockage, des bases de données dans le pool de hello, toohello taille qui correspond le nombre d’eDTU toohello.
- Configurez un nombre d’eDTU minimal supérieur à 0. Cette garantie minimale que chaque base de données dans le pool de hello a quantité hello du stockage OLTP en mémoire disponible qui correspond toohello configuré Min-eDTU.

### <a name="data-size-and-storage-for-columnstore-indexes"></a>Taille des données et stockage pour les index columnstore

Index ColumnStore ne sont pas requis toofit en mémoire. Par conséquent, hello limite sur la taille de hello des index de hello a la taille globale maximale de la base de données de hello, qui est décrit dans hello [les niveaux de service de base de données SQL](sql-database-service-tiers.md) l’article.

Lorsque vous utilisez des index columnstore en cluster, la compression en colonnes est utilisée pour le stockage de table de base hello. Cette compression peut réduire considérablement l’encombrement du stockage des données utilisateur, ce qui signifie que vous pouvez entrer davantage de données dans la base de données hello hello. Et la compression de hello peut être accrue encore plue avec [la compression d’archivage en colonnes](https://msdn.microsoft.com/library/cc280449.aspx#Using Columnstore and Columnstore Archive Compression). quantité de Hello de compression qui vous pouvez d’obtenir dépend de la nature hello de données de hello, mais la compression de 10 fois hello n’est pas rare.

Par exemple, si vous disposez d’une base de données avec une taille maximale de 1 téraoctet (To) et obtenir de compression de hello 10 fois à l’aide des index columnstore, vous pouvez inclure un total de 10 To de données utilisateur dans la base de données hello.

Lorsque vous utilisez des index columnstore non cluster, table de base hello est toujours stockée au format rowstore traditionnelle de hello. Par conséquent, les économies de stockage hello ne sont pas important qu’avec des index columnstore en cluster. Toutefois, si vous remplacez un nombre d’index non cluster traditionnels avec un index columnstore unique, vous pouvez toujours voir un économies globales dans un encombrement de stockage hello pour la table de hello.

## <a name="moving-databases-that-use-in-memory-technologies-between-pricing-tiers"></a>Déplacement de bases de données utilisant des technologies en mémoire entre différents niveaux tarifaires

Il ne sont jamais les incompatibilités ou autres problèmes lorsque vous mettez à niveau tooa supérieur tarification, telles que de tooPremium Standard. ressources et les fonctionnalités disponibles hello uniquement augmentent.

Mais hello déclassement tarification peut nuire à votre base de données. impact de Hello est particulièrement évident lorsque vous rétrogradez à partir de Premium tooStandard ou de base lorsque votre base de données contient des objets de l’OLTP en mémoire. Tables optimisées en mémoire et des index columnstore, ne sont pas disponibles après la rétrogradation de hello (même si elles restent visibles). Bonjour les mêmes considérations s’appliquent lorsque vous êtes réduisant hello tarification d’un pool élastique ou déplacement d’une base de données avec des technologies en mémoire, dans une norme ou base pool élastique.

### <a name="in-memory-oltp"></a>OLTP In-Memory.

*Rétrogradation tooBasic et Standard*: OLTP en mémoire n’est pas pris en charge dans les bases de données de niveau Standard ou Basic de hello. En outre, il n’est pas possible de toomove une base de données qui a des toohello d’objets OLTP en mémoire niveau Standard ou Basic.

Avant de la rétrogradation de base/tooStandard hello de base de données, supprimez toutes les tables optimisées en mémoire et les types de tables, ainsi que tous les modules T-SQL compilés en mode natif.

Il existe un toounderstand moyen par programmation si une base de données prend en charge OLTP en mémoire. Vous pouvez exécuter hello suivant la requête Transact-SQL :

```
SELECT DatabasePropertyEx(DB_NAME(), 'IsXTPSupported');
```

Si la requête de hello retourne **1**, OLTP en mémoire est prise en charge dans cette base de données.


*Rétrogradation de niveau Premium inférieur de tooa*: les données dans des tables optimisées en mémoire doivent tenir au sein du stockage hello OLTP en mémoire est associée à hello tarification de base de données hello ou qui est disponible dans le pool élastique de hello. Si vous essayez de hello toolower niveau tarifaire ou déplacez la base de données hello dans un pool qui n’a pas suffisamment stockage OLTP en mémoire disponible, hello échoue.

### <a name="columnstore-indexes"></a>Index Columnstore

*Rétrogradation tooBasic ou Standard*: Columnstore index sont pris en charge uniquement sur le niveau de tarification hello Premium et non sous hello niveaux Standard ou Basic. Lors de la rétrogradation de votre base de données tooStandard ou le Basic, l’index columnstore est plus disponible. système de Hello tient à jour l’index columnstore, mais il ne s’appuie sur les index hello. Si vous passez ensuite tooPremium précédent, l’index columnstore est immédiatement prêt toobe exploitée à nouveau.

Si vous avez un **cluster** index columnstore, ensemble de la table hello devient indisponible après la rétrogradation de la couche. Par conséquent, nous vous recommandons de supprimer l’ensemble *cluster* d’index columnstore avant de passer de votre base de données sous le niveau Premium de hello.

*Rétrogradation de niveau Premium inférieur de tooa*: cette rétrogradation réussit si la base de données entière hello s’intègre au sein de la taille maximale de la base de données de hello pour cible hello niveau tarifaire ou au sein du stockage disponible dans le pool élastique de hello hello. Aucun impact n’est spécifique à partir de l’index columnstore de hello.


<a id="install_oltp_manuallink" name="install_oltp_manuallink"></a>

&nbsp;

## <a name="1-install-hello-in-memory-oltp-sample"></a>1. Installer l’exemple d’OLTP en mémoire hello

Vous pouvez créer la base de données AdventureWorksLT hello en quelques clics dans hello [portail Azure](https://portal.azure.com/). Ensuite, hello étapes de cette section expliquent comment vous pouvez enrichir votre base de données AdventureWorksLT avec des objets OLTP en mémoire et illustre les performances.

Pour une démonstration plus simple mais intéressante des performances de l’OLTP en mémoire, consultez :

- Version : [in-memory-oltp-demo-v1.0](https://github.com/Microsoft/sql-server-samples/releases/tag/in-memory-oltp-demo-v1.0)
- Code source : [in-memory-oltp-demo-source-code](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/in-memory/ticket-reservations)

#### <a name="installation-steps"></a>Procédure d’installation :

1. Bonjour [portail Azure](https://portal.azure.com/), créez une base de données Premium sur un serveur. Ensemble hello **Source** base de données AdventureWorksLT toohello. Pour obtenir des instructions détaillées, consultez [Créer votre première base de données SQL Azure](sql-database-get-started-portal.md).

2. Se connecter toohello de base de données avec SQL Server Management Studio [(SSMS.exe)](http://msdn.microsoft.com/library/mt238290.aspx).

3. Hello de copie [script Transact-SQL de l’OLTP en mémoire](https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/in-memory/t-sql-scripts/sql_in-memory_oltp_sample.sql) tooyour Presse-papiers. Hello script T-SQL crée des objets en mémoire nécessaire hello hello AdventureWorksLT base de données exemple que vous avez créé à l’étape 1.

4. Collez le script T-SQL de hello dans SSMS, puis exécutez le script de hello. Hello `MEMORY_OPTIMIZED = ON` les instructions CREATE TABLE clause sont cruciales. Par exemple :


```
CREATE TABLE [SalesLT].[SalesOrderHeader_inmem](
    [SalesOrderID] int IDENTITY NOT NULL PRIMARY KEY NONCLUSTERED ...,
    ...
) WITH (MEMORY_OPTIMIZED = ON);
```


#### <a name="error-40536"></a>Erreur 40536


Si vous obtenez une erreur 40536 lorsque vous exécutez le script de hello T-SQL, exécutez hello suivant tooverify de script T-SQL si la base de données hello prend en charge en mémoire :


```
SELECT DatabasePropertyEx(DB_Name(), 'IsXTPSupported');
```


Un résultat de **0** signifie que la technologie en mémoire n’est pas prise en charge, et un résultat de **1** signifie qu’elle l’est. problème de hello toodiagnose, assurez-vous que cette base de données hello est au niveau de service Premium hello.


#### <a name="about-hello-created-memory-optimized-items"></a>À propos de hello créé des éléments de la mémoire optimisée

**Tables**: exemple hello contient hello optimisées en mémoire des tables suivantes :

- SalesLT.Product_inmem
- SalesLT.SalesOrderHeader_inmem
- SalesLT.SalesOrderDetail_inmem
- Demo.DemoSalesOrderHeaderSeed
- Demo.DemoSalesOrderDetailSeed


Vous pouvez inspecter les tables optimisées en mémoire via hello **l’Explorateur d’objets** dans SSMS. Cliquez avec le bouton droit sur **Tables** > **Filtre** > **Paramètres de filtre** > **Est à mémoire optimisée**. valeur de Hello est égal à 1.


Ou bien, vous pouvez interroger les vues de catalogue hello, telles que :


```
SELECT is_memory_optimized, name, type_desc, durability_desc
    FROM sys.tables
    WHERE is_memory_optimized = 1;
```


**Procédure stockée compilée en mode natif** : vous pouvez inspecter SalesLT.usp_InsertSalesOrder_inmem via une requête de vue de catalogue :


```
SELECT uses_native_compilation, OBJECT_NAME(object_id), definition
    FROM sys.sql_modules
    WHERE uses_native_compilation = 1;
```


&nbsp;

### <a name="run-hello-sample-oltp-workload"></a>Exécuter la charge de travail OLTP hello exemple

Hello la seule différence entre hello suivant deux *des procédures stockées* est que la première procédure de hello utilise les versions mémoire optimisées des tables de hello, hello lors de la deuxième procédure utilise les tables sur disque standard hello :

- SalesLT**.**usp_InsertSalesOrder**_inmem**
- SalesLT**.**usp_InsertSalesOrder**_ondisk**


Dans cette section, vous voyez comment toouse hello pratique **ostress.exe** utilitaire tooexecute hello deux procédures stockées à des niveaux stressants. Vous pouvez comparer la durée pour hello deux contraintes s’exécute toofinish.


Lorsque vous exécutez ostress.exe, nous recommandons que vous passez des valeurs de paramètre conçus pour les deux éléments suivants de hello :

- Exécuter un grand nombre de connexions simultanées, en utilisant -n100.
- Répéter chaque boucle de connexion une centaine de fois, en utilisant -r500.


Toutefois, vous pourriez toostart avec beaucoup plus petites valeurs telle que - tooensure n10 et - r 50 que tout fonctionne.


### <a name="script-for-ostressexe"></a>Script pour ostress.exe


Cette section affiche le script T-SQL hello qui est incorporé dans notre ligne de commande ostress.exe. script de Hello utilise des éléments qui ont été créés par hello script T-SQL que vous avez installé précédemment.


Hello script suivant insère un exemple de commande client avec cinq éléments de la ligne suivante hello optimisées en mémoire *tables*:

- SalesLT.SalesOrderHeader_inmem
- SalesLT.SalesOrderDetail_inmem


```
DECLARE
    @i int = 0,
    @od SalesLT.SalesOrderDetailType_inmem,
    @SalesOrderID int,
    @DueDate datetime2 = sysdatetime(),
    @CustomerID int = rand() * 8000,
    @BillToAddressID int = rand() * 10000,
    @ShipToAddressID int = rand() * 10000;

INSERT INTO @od
    SELECT OrderQty, ProductID
    FROM Demo.DemoSalesOrderDetailSeed
    WHERE OrderID= cast((rand()*60) as int);

WHILE (@i < 20)
begin;
    EXECUTE SalesLT.usp_InsertSalesOrder_inmem @SalesOrderID OUTPUT,
        @DueDate, @CustomerID, @BillToAddressID, @ShipToAddressID, @od;
    SET @i = @i + 1;
end
```


toomake hello *_ondisk* version de hello précédent script T-SQL pour ostress.exe, vous devez remplacer les deux occurrences de hello *_inmem* substring avec *_ondisk*. Ces remplacements affectent les noms de tables et procédures stockées hello.


### <a name="install-rml-utilities-and-ostress"></a>Installer les utilitaires RML et ostress


Dans l’idéal, vous devez prévoir toorun ostress.exe sur une machine virtuelle Azure (VM). Vous devez créer un [Azure VM](https://azure.microsoft.com/documentation/services/virtual-machines/) Bonjour même région géographique Azure où se trouve votre base de données AdventureWorksLT. Vous pouvez aussi exécuter ostress.exe sur votre ordinateur portable.


Hello machine virtuelle, ou sur tout ce qui hébergent vous choisissez, installez les utilitaires de langage de balisage de relecture (RML) hello. utilitaires de Hello incluent ostress.exe.

Pour plus d'informations, consultez les pages suivantes :
- Hello discussion ostress.exe dans [exemple de base de données pour OLTP en mémoire](http://msdn.microsoft.com/library/mt465764.aspx).
- [Exemple de base de données pour OLTP en mémoire](http://msdn.microsoft.com/library/mt465764.aspx).
- Hello [blog pour l’installation de ostress.exe](http://blogs.msdn.com/b/psssql/archive/2013/10/29/cumulative-update-2-to-the-rml-utilities-for-microsoft-sql-server-released.aspx).



<!--
dn511655.aspx is for SQL 2014,
[Extensions tooAdventureWorks tooDemonstrate In-Memory OLTP]
(http://msdn.microsoft.com/library/dn511655&#x28;v=sql.120&#x29;.aspx)

whereas for SQL 2016+
[Sample Database for In-Memory OLTP]
(http://msdn.microsoft.com/library/mt465764.aspx)
-->



### <a name="run-hello-inmem-stress-workload-first"></a>Exécutez hello *_inmem* tout d’abord une contrainte la charge de travail


Vous pouvez utiliser un *invite de commandes RML* fenêtre toorun notre ligne de commande ostress.exe. paramètres de ligne de commande Hello directe ostress à :

- Exécuter 100 connexions simultanément (-n100).
- Chaque connexion exécuter les script T-SQL de hello 50 fois (-r 50).


```
ostress.exe -n100 -r50 -S<servername>.database.windows.net -U<login> -P<password> -d<database> -q -Q"DECLARE @i int = 0, @od SalesLT.SalesOrderDetailType_inmem, @SalesOrderID int, @DueDate datetime2 = sysdatetime(), @CustomerID int = rand() * 8000, @BillToAddressID int = rand() * 10000, @ShipToAddressID int = rand()* 10000; INSERT INTO @od SELECT OrderQty, ProductID FROM Demo.DemoSalesOrderDetailSeed WHERE OrderID= cast((rand()*60) as int); WHILE (@i < 20) begin; EXECUTE SalesLT.usp_InsertSalesOrder_inmem @SalesOrderID OUTPUT, @DueDate, @CustomerID, @BillToAddressID, @ShipToAddressID, @od; set @i += 1; end"
```


hello toorun précédant la ligne de commande ostress.exe :


1. Réinitialiser le contenu des données de base de données hello en exécutant hello suivant de commande dans SSMS, toodelete toutes les données hello qui ont été insérées par les exécutions précédentes :

    ``` tsql
    EXECUTE Demo.usp_DemoReset;
    ```

2. Copier le texte hello Hello précédant tooyour du Presse-papiers de la ligne de commande ostress.exe.

3. Remplacez hello `<placeholders>` pour hello paramètres -S - U -P -d par hello corriger des valeurs réelles.

4. Exécutez la ligne de commande que vous avez modifiée dans la fenêtre de commande RML.


#### <a name="result-is-a-duration"></a>Il en résulte une durée


Une fois ostress.exe, il écrit hello durée d’exécution en tant que sa dernière ligne de sortie dans la fenêtre de RML Cmd hello. Par exemple, une série de tests plus courte a duré environ 1,5 minute :

`11/12/15 00:35:00.873 [0x000030A8] OSTRESS exiting normally, elapsed time: 00:01:31.867`


#### <a name="reset-edit-for-ondisk-then-rerun"></a>Réinitialisez, paramétrez *_ondisk*, puis procédez à une nouvelle exécution.


Après avoir résultant de hello hello *_inmem* exécuter, effectuer hello comme suit pour hello *_ondisk* exécuter :


1. Réinitialisation de la base de données hello en exécutant hello suivant de commande dans SSMS toodelete toutes les données hello ayant été insérées par hello précédente exécution :
```
EXECUTE Demo.usp_DemoReset;
```

2. Modifier tooreplace de ligne de commande hello ostress.exe tous les *_inmem* avec *_ondisk*.

3. Réexécutez ostress.exe pour hello deuxième fois et capturer les résultats de durée hello.

4. Là encore, réinitialisation hello base de données (pour la suppression de façon responsable qui peut être une grande quantité de données de test).


#### <a name="expected-comparison-results"></a>Résultats de la comparaison attendus

Nos tests en mémoire ont montré que les performances améliorées par **neuf fois** pour cette charge de travail très simplifiée avec ostress s’exécutant sur une machine virtuelle de Azure dans hello même région Azure en tant que base de données hello.

<a id="install_analytics_manuallink" name="install_analytics_manuallink"></a>

&nbsp;

## <a name="2-install-hello-in-memory-analytics-sample"></a>2. Installer hello en mémoire Analytique


Dans cette section, vous comparez hello e/s et les résultats des statistiques lorsque vous utilisez un index columnstore par rapport à un index b-tree traditionnel.


Pour l’analytique en temps réel sur une charge de travail OLTP, il est souvent de meilleures toouse un index non cluster. Pour plus d’informations, consultez [Index columnstore décrits](http://msdn.microsoft.com/library/gg492088.aspx).



### <a name="prepare-hello-columnstore-analytics-test"></a>Préparer hello columnstore analytique test


1. Utilisez hello toocreate portail Azure une nouvelle base de données AdventureWorksLT à partir de l’exemple hello.
 - Utilisez ce nom exact.
 - Choisissez un niveau de service Premium.

2. Hello de copie [sql_in-memory_analytics_sample](https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/in-memory/t-sql-scripts/sql_in-memory_analytics_sample.sql) tooyour Presse-papiers.
 - Hello script T-SQL crée des objets en mémoire nécessaire hello hello AdventureWorksLT base de données exemple que vous avez créé à l’étape 1.
 - script de Hello crée deux tables de faits et de la table de Dimension hello. tables de faits Hello sont renseignées avec 3,5 millions de lignes chacune.
 - script de Hello peut prendre 15 minutes toocomplete.

3. Collez le script T-SQL de hello dans SSMS, puis exécutez le script de hello. Hello **COLUMNSTORE** mot clé Bonjour **CREATE INDEX** instruction est cruciale, comme dans :<br/>`CREATE NONCLUSTERED COLUMNSTORE INDEX ...;`

4. Définir le niveau de toocompatibility AdventureWorksLT 130 :<br/>`ALTER DATABASE AdventureworksLT SET compatibility_level = 130;`

    Niveau 130 n’est pas fonctionnalités tooIn directement lié, en mémoire. Mais le niveau 130 offre généralement des performances de requêtes supérieures au niveau 120.


#### <a name="key-tables-and-columnstore-indexes"></a>Tables et index columnstore essentiels


- dbo. FactResellerSalesXL_CCI est une table qui possède un index cluster columnstore, qui bénéficie de la compression à hello avancé *données* niveau.

- dbo. FactResellerSalesXL_PageCompressed est une table qui comporte un équivalent index ordonné en clusters standard, qui est compressé uniquement au hello *page* niveau.


#### <a name="key-queries-toocompare-hello-columnstore-index"></a>Index de clé requêtes toocompare hello columnstore


Il n’y [plusieurs types de requêtes T-SQL que vous pouvez exécuter](https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/in-memory/t-sql-scripts/clustered_columnstore_sample_queries.sql) toosee des améliorations de performances. À l’étape 2 dans hello script T-SQL, payer paire de toothis attention de requêtes. Elles diffèrent uniquement d’une ligne :


- `FROM FactResellerSalesXL_PageCompressed a`
- `FROM FactResellerSalesXL_CCI a`


Un index cluster columnstore est Bonjour FactResellerSalesXL\_les table CCI.

Hello extrait de script T-SQL suivant imprime des statistiques pour les e/s et l’heure de la requête hello de chaque table.


```
/*********************************************************************
Step 2 -- Overview
-- Page Compressed BTree table v/s Columnstore table performance differences
-- Enable actual Query Plan in order toosee Plan differences when Executing
*/
-- Ensure Database is in 130 compatibility mode
ALTER DATABASE AdventureworksLT SET compatibility_level = 130
GO

-- Execute a typical query that joins hello Fact Table with dimension tables
-- Note this query will run on hello Page Compressed table, Note down hello time
SET STATISTICS IO ON
SET STATISTICS TIME ON
GO

SELECT c.Year
    ,e.ProductCategoryKey
    ,FirstName + ' ' + LastName AS FullName
    ,count(SalesOrderNumber) AS NumSales
    ,sum(SalesAmount) AS TotalSalesAmt
    ,Avg(SalesAmount) AS AvgSalesAmt
    ,count(DISTINCT SalesOrderNumber) AS NumOrders
    ,count(DISTINCT a.CustomerKey) AS CountCustomers
FROM FactResellerSalesXL_PageCompressed a
INNER JOIN DimProduct b ON b.ProductKey = a.ProductKey
INNER JOIN DimCustomer d ON d.CustomerKey = a.CustomerKey
Inner JOIN DimProductSubCategory e on e.ProductSubcategoryKey = b.ProductSubcategoryKey
INNER JOIN DimDate c ON c.DateKey = a.OrderDateKey
GROUP BY e.ProductCategoryKey,c.Year,d.CustomerKey,d.FirstName,d.LastName
GO
SET STATISTICS IO OFF
SET STATISTICS TIME OFF
GO


-- This is hello same Prior query on a table with a clustered columnstore index CCI
-- hello comparison numbers are even more dramatic hello larger hello table is (this is an 11 million row table only)
SET STATISTICS IO ON
SET STATISTICS TIME ON
GO
SELECT c.Year
    ,e.ProductCategoryKey
    ,FirstName + ' ' + LastName AS FullName
    ,count(SalesOrderNumber) AS NumSales
    ,sum(SalesAmount) AS TotalSalesAmt
    ,Avg(SalesAmount) AS AvgSalesAmt
    ,count(DISTINCT SalesOrderNumber) AS NumOrders
    ,count(DISTINCT a.CustomerKey) AS CountCustomers
FROM FactResellerSalesXL_CCI a
INNER JOIN DimProduct b ON b.ProductKey = a.ProductKey
INNER JOIN DimCustomer d ON d.CustomerKey = a.CustomerKey
Inner JOIN DimProductSubCategory e on e.ProductSubcategoryKey = b.ProductSubcategoryKey
INNER JOIN DimDate c ON c.DateKey = a.OrderDateKey
GROUP BY e.ProductCategoryKey,c.Year,d.CustomerKey,d.FirstName,d.LastName
GO

SET STATISTICS IO OFF
SET STATISTICS TIME OFF
GO
```

Dans une base de données avec un niveau de tarification hello P2, attendez-vous à neuf fois gain de performances hello pour cette requête à l’aide d’un index columnstore cluster hello par rapport à un index classique hello. Avec P15, vous pouvez vous attendre environ 57 fois hello les gains de performance à l’aide des index columnstore de hello.



## <a name="next-steps"></a>Étapes suivantes

- [Démarrage rapide 1 : Technologies OLTP en mémoire pour des performances T-SQL plus rapides](http://msdn.microsoft.com/library/mt694156.aspx)

- [Utiliser OLTP en mémoire dans une application SQL Azure existante](sql-database-in-memory-oltp-migration.md)

- [Surveiller le stockage OLTP en mémoire](sql-database-in-memory-oltp-monitoring.md) pour l’OLTP en mémoire


## <a name="additional-resources"></a>Ressources supplémentaires

#### <a name="deeper-information"></a>Informations supplémentaires

- [Découvrez comment le Quorum double la charge de travail de la base de données clé tout en réduisant les DTU de 70 %, grâce à l’OLTP en mémoire dans la SQL Database](https://customers.microsoft.com/story/quorum-doubles-key-databases-workload-while-lowering-dtu-with-sql-database)

- [Billet de blog OLTP en mémoire dans Azure SQL Database](https://azure.microsoft.com/blog/in-memory-oltp-in-azure-sql-database/)

- [En savoir plus sur In-Memory OLTP](http://msdn.microsoft.com/library/dn133186.aspx)

- [En savoir plus sur les index columnstore](https://msdn.microsoft.com/library/gg492088.aspx)

- [En savoir plus sur l’analytique opérationnelle en temps réel](http://msdn.microsoft.com/library/dn817827.aspx)

- Consultez [Modèles de charge de travail courants et considérations relatives à la migration](http://msdn.microsoft.com/library/dn673538.aspx) (qui décrit des modèles de charge de travail où l’OLTP en mémoire apporte généralement des gains de performances significatifs)

#### <a name="application-design"></a>Conception des applications

- [In-Memory OLTP (optimisation en mémoire)](http://msdn.microsoft.com/library/dn133186.aspx)

- [Utiliser OLTP en mémoire dans une application SQL Azure existante](sql-database-in-memory-oltp-migration.md)

#### <a name="tools"></a>Outils

- [Portail Azure](https://portal.azure.com/)

- [SQL Server Management Studio (SSMS)](https://msdn.microsoft.com/library/mt238290.aspx)

- [Outils SQL Server Data Tools (SSDT)](http://msdn.microsoft.com/library/mt204009.aspx)
