---
title: "aaaLoad - Azure Data Lake Store tooSQL l’entrepôt de données | Documents Microsoft"
description: "Découvrez comment toouse PolyBase externe tables données tooload à partir d’Azure Data Lake Store dans Azure SQL Data Warehouse."
services: sql-data-warehouse
documentationcenter: NA
author: ckarst
manager: barbkess
editor: 
ms.assetid: 
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: loading
ms.date: 01/25/2017
ms.author: cakarst;barbkess
ms.openlocfilehash: 50ef23b3eba5f58bc9974095f84140dc5c11fa4b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="load-data-from-azure-data-lake-store-into-sql-data-warehouse"></a>Chargement de données Azure Data Lake Store dans SQL Data Warehouse
Ce document vous donne toutes les étapes que vous avez besoin de tooload vos propres données à partir de Azure données Lake Store (ADLS) dans l’entrepôt de données SQL à l’aide de PolyBase.
Lorsque vous êtes en mesure de toorun des requêtes ad hoc sur les données de hello stockées dans ADLS à l’aide des Tables externes hello, comme une meilleure pratique nous vous suggérons l’importation des données de hello en hello SQL Data Warehouse.
Durée estimée : 10 minutes, en supposant que vous avez conditions préalables de hello devez toocomplete.
Ce didacticiel vous apprendra à effectuer les opérations suivantes :

1. Créer tooload des objets de base de données externe à partir d’Azure Data Lake Store.
2. Se connecter tooan répertoire de magasin Azure Data Lake.
3. Charger des données dans Azure SQL Data Warehouse.

## <a name="before-you-begin"></a>Avant de commencer
toorun ce didacticiel, vous devez :

* Toouse Active Directory Application Azure pour l’authentification de Service. toocreate, suivez [l’authentification Active directory](https://docs.microsoft.com/azure/data-lake-store/data-lake-store-authenticate-using-active-directory)

>[!NOTE] 
> Vous devez hello client ID, clé et valeur de point de terminaison de jeton OAuth2.0 de votre tooyour de tooconnect d’Active Directory Application Azure Data Lake à partir de l’entrepôt de données SQL. Détails de tooget comment ces valeurs sont dans le lien hello ci-dessus.
>Remarque pour l’inscription Azure Active Directory Application servir hello ID de l’Application hello ID Client.

* SQL Server Management Studio ou SQL Server Data Tools, toodownload SSMS et connecter voir [requête SSMS](https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-query-ssms)

* Un entrepôt de données SQL Azure, suivez de toocreate un : https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-get-started-provision

* Un Azure Data Lake Store pour lequel le chiffrement est activé ou non. suivi d’un seul toocreate : https://docs.microsoft.com/azure/data-lake-store/data-lake-store-get-started-portal




## <a name="configure-hello-data-source"></a>Configurer la source de données hello
PolyBase utilise l’emplacement de T-SQL des objets externes toodefine hello et les attributs de données externes de hello. des objets externes Hello sont stockés dans la référence de l’entrepôt de données SQL et des données hello que th est stockées en externe.


###  <a name="create-a-credential"></a>Créer des informations d’identification
Stocker de votre Azure Data Lake tooaccess, vous devez toocreate une clé principale de base de données de tooencrypt votre secret d’identification utilisé dans l’étape suivante de hello.
Vous créez ensuite des informations d’identification d’une étendue de la base de données, ce qui stocke les hello principal des références de service définis dans AAD. Pour ceux qui ont utilisé PolyBase tooconnect tooWindows objets BLOB de stockage Azure, notez ces informations d’identification hello syntaxe est différente.
tooconnect tooAzure Data Lake Store, vous devez **premier** créer une Application Active Directory de Azure, créer une clé d’accès et accordez hello application accès toohello Azure Data Lake ressource. Instrucitons tooperform ces étapes sont situés [ici](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-authenticate-using-active-directory).

```sql
-- A: Create a Database Master Key.
-- Only necessary if one does not already exist.
-- Required tooencrypt hello credential secret in hello next step.
-- For more information on Master Key: https://msdn.microsoft.com/en-us/library/ms174382.aspx?f=255&MSPPError=-2147217396

CREATE MASTER KEY;


-- B: Create a database scoped credential
-- IDENTITY: Pass hello client id and OAuth 2.0 Token Endpoint taken from your Azure Active Directory Application
-- SECRET: Provide your AAD Application Service Principal key.
-- For more information on Create Database Scoped Credential: https://msdn.microsoft.com/en-us/library/mt270260.aspx

CREATE DATABASE SCOPED CREDENTIAL ADLCredential
WITH
    IDENTITY = '<client_id>@<OAuth_2.0_Token_EndPoint>',
    SECRET = '<key>'
;

-- It should look something like this:
CREATE DATABASE SCOPED CREDENTIAL ADLCredential
WITH
    IDENTITY = '536540b4-4239-45fe-b9a3-629f97591c0c@https://login.microsoftonline.com/42f988bf-85f1-41af-91ab-2d2cd011da47/oauth2/token',
    SECRET = 'BjdIlmtKp4Fpyh9hIvr8HJlUida/seM5kQ3EpLAmeDI='
;
```


### <a name="create-hello-external-data-source"></a>Créer la source de données externe hello
Utilisez cette [CREATE EXTERNAL DATA SOURCE] [ CREATE EXTERNAL DATA SOURCE] emplacement de hello toostore des données de hello et type hello de données de commande.
Vous trouverez hello ADL URI dans hello portail Azure et www.portal.azure.com.

```sql
-- C: Create an external data source
-- TYPE: HADOOP - PolyBase uses Hadoop APIs tooaccess data in Azure Data Lake Store.
-- LOCATION: Provide Azure Data Lake accountname and URI
-- CREDENTIAL: Provide hello credential created in hello previous step.

CREATE EXTERNAL DATA SOURCE AzureDataLakeStore
WITH (
    TYPE = HADOOP,
    LOCATION = 'adl://<AzureDataLake account_name>.azuredatalakestore.net',
    CREDENTIAL = ADLCredential
);
```



## <a name="configure-data-format"></a>Configurer le format des données
les données de salutation tooimport de ADLS, vous devez format de fichier externe toospecify hello. Cette commande a les options spécifiques au format toodescribe vos données.
Voici un exemple de format de fichier fréquemment utilisé, soit un fichier texte délimité par une barre verticale.
Consultez notre documentation T-SQL pour obtenir une liste complète [CREATE EXTERNAL FILE FORMAT][CREATE EXTERNAL FILE FORMAT]

```sql
-- D: Create an external file format
-- FIELD_TERMINATOR: Marks hello end of each field (column) in a delimited text file
-- STRING_DELIMITER: Specifies hello field terminator for data of type string in hello text-delimited file.
-- DATE_FORMAT: Specifies a custom format for all date and time data that might appear in a delimited text file.
-- Use_Type_Default: Store all Missing values as NULL

CREATE EXTERNAL FILE FORMAT TextFileFormat
WITH
(   FORMAT_TYPE = DELIMITEDTEXT
,    FORMAT_OPTIONS    (   FIELD_TERMINATOR = '|'
                    ,    STRING_DELIMITER = ''
                    ,    DATE_FORMAT         = 'yyyy-MM-dd HH:mm:ss.fff'
                    ,    USE_TYPE_DEFAULT = FALSE
                    )
);
```

## <a name="create-hello-external-tables"></a>Créer des tables externes hello
Maintenant que vous avez spécifié hello données source et formats de fichier, vous êtes prêt toocreate des tables externes hello. Les tables externes vous permettent d’interagir avec des données externes. PolyBase utilise tooread de parcours de répertoire récursive tous les fichiers dans tous les sous-répertoires du répertoire hello spécifié dans le paramètre d’emplacement hello. En outre, hello l’exemple suivant montre comment toocreate hello objet. Vous devez toocustomize hello instruction toowork avec données hello dans ADLS.

```sql
-- D: Create an External Table
-- LOCATION: Folder under hello ADLS root folder.
-- DATA_SOURCE: Specifies which Data Source Object toouse.
-- FILE_FORMAT: Specifies which File Format Object toouse
-- REJECT_TYPE: Specifies how you want toodeal with rejected rows. Either Value or percentage of hello total
-- REJECT_VALUE: Sets hello Reject value based on hello reject type.

-- DimProduct
CREATE EXTERNAL TABLE [dbo].[DimProduct_external] (
    [ProductKey] [int] NOT NULL,
    [ProductLabel] [nvarchar](255) NULL,
    [ProductName] [nvarchar](500) NULL
)
WITH
(
    LOCATION='/DimProduct/'
,   DATA_SOURCE = AzureDataLakeStore
,   FILE_FORMAT = TextFileFormat
,   REJECT_TYPE = VALUE
,   REJECT_VALUE = 0
)
;

```

## <a name="external-table-considerations"></a>Considérations relatives aux tables externes
Création d’une table externe est facile, mais il existe des nuances qui doivent toobe indiqué.

Le chargement de données avec PolyBase est fortement typé. Cela signifie que chaque ligne de données hello en cours ingérées doit satisfaire la définition de schéma de table hello.
Si une ligne donnée ne correspond pas à la définition de schéma hello, ligne de hello est rejetée à partir de la charge de hello.

Hello REJECT_TYPE et REJECT_VALUE permettent de toodefine le nombre de lignes ou le pourcentage de données de salutation doit être présent dans la table finale de hello.
Au cours du chargement, si la valeur de rejet hello est atteinte, le chargement de hello échoue. cause la plus courante de lignes rejetées Hello est une incompatibilité de définition de schéma.
Par exemple, si une colonne reçoit correctement schéma hello int lorsque les données de salutation dans le fichier de hello sont une chaîne, chaque ligne ne fonctionnera pas tooload.

Hello emplacement spécifie hello premier répertoire tooread des données à partir de.
Dans ce cas, s’il y avait sous-répertoires /DimProduct/ PolyBase seraient importer toutes les données hello dans les sous-répertoires hello.

## <a name="load-hello-data"></a>Charger des données hello
données tooload à partir d’Azure Data Lake Store utilisent hello [CREATE TABLE AS SELECT (Transact-SQL)] [ CREATE TABLE AS SELECT (Transact-SQL)] instruction. Utilise hello chargement avec SACT fortement typé que vous avez créé une table externe.

SACT crée une nouvelle table et le remplit avec des résultats d’une instruction select hello. SACT définit hello nouvelle table toohave hello les mêmes colonnes et types de données comme résultats hello Hello select (instruction). Si vous sélectionnez toutes les colonnes hello à partir d’une table externe, hello nouvelle table est un réplica de colonnes de hello et les types de données dans une table externe hello.

Dans cet exemple, nous créons une table de hachage distribuée appelée DimProduct à partir de notre table externe DimProduct_external.

```sql

CREATE TABLE [dbo].[DimProduct]
WITH (DISTRIBUTION = HASH([ProductKey]  ) )
AS
SELECT * FROM [dbo].[DimProduct_external]
OPTION (LABEL = 'CTAS : Load [dbo].[DimProduct]');
```


## <a name="optimize-columnstore-compression"></a>Optimiser la compression columnstore
Par défaut, SQL Data Warehouse stocke la table de hello en tant qu’un index cluster columnstore. Après un chargement, certains hello lignes de données ne peuvent pas être compressé au hello columnstore.  Cela peut être dû à diverses raisons. toolearn, voir [gérer les index columnstore][manage columnstore indexes].

performances des requêtes toooptimize et la compression de columnstore après un chargement, reconstruire hello table tooforce hello columnstore index toocompress toutes les lignes hello.

```sql

ALTER INDEX ALL ON [dbo].[DimProduct] REBUILD;

```

Pour plus d’informations sur la gestion des index columnstore, consultez hello [gérer les index columnstore] [ manage columnstore indexes] l’article.

## <a name="optimize-statistics"></a>Optimiser les statistiques
Il s’agit des statistiques de colonne unique toocreate meilleures immédiatement après un chargement. Les statistiques offrent plusieurs possibilités. Par exemple, si vous créez des statistiques de colonnes uniques sur toutes les colonnes qu’il peut prendre un toorebuild beaucoup de temps toutes les statistiques de hello. Si vous savez que certaines colonnes ne vont pas toobe dans les prédicats de requête, vous pouvez ignorer la création des statistiques sur les colonnes.

Si vous décidez de toocreate les statistiques de colonnes uniques sur chaque colonne de chaque table, vous pouvez utiliser les exemples de code de procédure stockée hello `prc_sqldw_create_stats` Bonjour [statistiques] [ statistics] l’article.

Bonjour à l’exemple suivant est un bon point de départ pour la création de statistiques. Il crée des statistiques de colonnes uniques sur chaque colonne de table de dimension hello et sur chaque colonne de jointure dans des tables de faits hello. Vous pouvez toujours ajouter des colonnes de table de faits unique ou plusieurs colonnes de statistiques tooother ultérieurement.


## <a name="achievement-unlocked"></a>Et voilà !
Vous avez correctement chargé les données dans Azure SQL Data Warehouse. Bon travail !

##<a name="next-steps"></a>Étapes suivantes
Le chargement des données est hello première étape toodeveloping une solution d’entrepôt de données à l’aide de l’entrepôt de données SQL. Découvrez nos ressources de développement dans les sections [Tables](https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-tables-overview) et [T-SQL](https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-develop-loops.md).


<!--Image references-->

<!--Article references-->
[Create a SQL Data Warehouse]: sql-data-warehouse-get-started-provision.md
[Load data into SQL Data Warehouse]: sql-data-warehouse-overview-load.md
[SQL Data Warehouse development overview]: sql-data-warehouse-overview-develop.md
[manage columnstore indexes]: sql-data-warehouse-tables-index.md
[Statistics]: sql-data-warehouse-tables-statistics.md
[CTAS]: sql-data-warehouse-develop-ctas.md
[label]: sql-data-warehouse-develop-label.md

<!--MSDN references-->
[CREATE EXTERNAL DATA SOURCE]: https://msdn.microsoft.com/library/dn935022.aspx
[CREATE EXTERNAL FILE FORMAT]: https://msdn.microsoft.com/library/dn935026.aspx
[CREATE TABLE AS SELECT (Transact-SQL)]: https://msdn.microsoft.com/library/mt204041.aspx
[sys.dm_pdw_exec_requests]: https://msdn.microsoft.com/library/mt203887.aspx
[REBUILD]: https://msdn.microsoft.com/library/ms188388.aspx

<!--Other Web references-->
[Microsoft Download Center]: http://www.microsoft.com/download/details.aspx?id=36433
[Load hello full Contoso Retail Data Warehouse]: https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/contoso-data-warehouse/readme.md
