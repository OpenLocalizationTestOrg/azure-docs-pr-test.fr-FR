---
title: "aaaPolyBase dans le didacticiel sur l’entrepôt de données SQL | Documents Microsoft"
description: "Découvrez les nouveautés de PolyBase et comment toouse pour les scénarios d’entreposage de données."
services: sql-data-warehouse
documentationcenter: NA
author: ckarst
manager: jhubbard
editor: 
ms.assetid: 0a0103b4-ddd6-4d1e-87be-4965d6e99f3f
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: loading
ms.date: 03/01/2017
ms.author: cakarst;barbkess
ms.openlocfilehash: 3e680ec407c1d920dd59ea922b82c9208b5e9a84
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="load-data-with-polybase-in-sql-data-warehouse"></a>Télécharger des données avec PolyBase dans SQL Data Warehouse
> [!div class="op_single_selector"]
> * [Redgate](sql-data-warehouse-load-with-redgate.md)  
> * [Data Factory](sql-data-warehouse-get-started-load-with-azure-data-factory.md)  
> * [PolyBase](sql-data-warehouse-get-started-load-with-polybase.md)  
> * [BCP](sql-data-warehouse-load-with-bcp.md)
> 
> 

Ce didacticiel montre comment les données de tooload dans l’entrepôt de données SQL à l’aide de AzCopy et PolyBase. À la fin de ce didacticiel, vous saurez comment :

* Utiliser le stockage d’objets blob tooAzure AzCopy toocopy données
* Créer des objets de base de données les données de salutation toodefine
* Exécuter une requête T-SQL tooload des données hello

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Loading-data-with-PolyBase-in-Azure-SQL-Data-Warehouse/player]
> 
> 

## <a name="prerequisites"></a>Composants requis
toostep dans ce didacticiel, vous avez besoin

* Une base de données SQL Data Warehouse
* Un compte de stockage Azure de type stockage redondant local standard (LRS-Standard), stockage géo-redondant Standard (Standard-GRS) ou stockage géo-redondant avec accès en lecture Standard (Standard-RAGRS)
* L’utilitaire de ligne de commande AzCopy Téléchargez et installez hello [version la plus récente de AzCopy] [ latest version of AzCopy] qui est installé avec hello de stockage Microsoft Azure Tools.
  
    ![Outils Azure Storage](./media/sql-data-warehouse-get-started-load-with-polybase/install-azcopy.png)

## <a name="step-1-add-sample-data-tooazure-blob-storage"></a>Étape 1 : Ajouter le stockage d’objets blob tooAzure échantillon de données
Données de commandes tooload, nous devons tooput quelques exemples de données dans un stockage d’objets blob Azure. Lors de cette étape, nous allons remplir un objet blob Azure Storage avec des exemples de données. Une version ultérieure, nous allons utiliser PolyBase tooload ces exemples de données dans votre base de données SQL Data Warehouse.

### <a name="a-prepare-a-sample-text-file"></a>R : Préparer un exemple de fichier texte
tooprepare un exemple de fichier texte :

1. Ouvrez le bloc-notes, puis copiez hello après des lignes de données dans un nouveau fichier. Enregistrez ce répertoire temporaire local de tooyour sous % temp%\DimDate2.txt.

```
20150301,1,3
20150501,2,4
20151001,4,2
20150201,1,3
20151201,4,2
20150801,3,1
20150601,2,4
20151101,4,2
20150401,2,4
20150701,3,1
20150901,3,1
20150101,1,3
```

### <a name="b-find-your-blob-service-endpoint"></a>B. Recherchez votre point de terminaison de service blob
toofind votre point de terminaison de service blob :

1. Sélectionnez hello Azure Portal **Parcourir** > **comptes de stockage**.
2. Cliquez sur le compte de stockage hello souhaité toouse.
3. Dans le panneau de compte de stockage hello, cliquez sur objets BLOB
   
    ![Cliquer sur les objets blobs](./media/sql-data-warehouse-get-started-load-with-polybase/click-blobs.png)
4. Enregistrez votre URL de point de terminaison du service blob pour l’utiliser à une date ultérieure.
   
    ![Point de terminaison de service blob](./media/sql-data-warehouse-get-started-load-with-polybase/blob-service.png)

### <a name="c-find-your-azure-storage-key"></a>C. Rechercher votre clé de stockage Azure
toofind votre clé de stockage Azure :

1. À partir de hello portail Azure, sélectionnez **Parcourir** > **comptes de stockage**.
2. Cliquez sur le compte de stockage hello souhaité toouse.
3. Sélectionnez **Tous les paramètres** > **Clés d’accès**.
4. Cliquez sur hello copie boîte toocopy une du Presse-papiers toohello accès aux clés.
   
    ![Copier la clé de stockage Azure](./media/sql-data-warehouse-get-started-load-with-polybase/access-key.png)

### <a name="d-copy-hello-sample-file-tooazure-blob-storage"></a>D. Copiez le stockage d’objets blob hello exemple fichier tooAzure
toocopy votre stockage d’objets blob de données tooAzure :

1. Ouvrez une invite de commandes et modifiez le répertoire d’installation des répertoires toohello AzCopy. Cette commande modifie le répertoire d’installation par défaut toohello sur un client de Windows 64 bits.
   
    ```
    cd /d "%ProgramFiles(x86)%\Microsoft SDKs\Azure\AzCopy"
    ```
2. Exécutez hello suivant du fichier de commandes tooupload hello. Spécifiez l’URL du point de terminaison de votre service d’objets blobs pour <blob service endpoint URL> et votre clé de compte de stockage Azure pour <azure_storage_account_key>.
   
    ```
    .\AzCopy.exe /Source:C:\Temp\ /Dest:<blob service endpoint URL> /datacontainer/datedimension/ /DestKey:<azure_storage_account_key> /Pattern:DimDate2.txt
    ```

Voir aussi [prise en main de l’utilitaire de ligne de commande AzCopy de hello][Getting Started with hello AzCopy Command-Line Utility].

### <a name="e-explore-your-blob-storage-container"></a>E. Explorer votre conteneur de stockage d’objets blobs
fichier de hello toosee vous avez téléchargé tooblob stockage :

1. Retournez dans le panneau de service Blob tooyour.
2. Sous Conteneurs, double-cliquez sur **datacontainer**.
3. tooexplore hello chemin d’accès tooyour données, cliquez sur le dossier de hello **datedimension** et vous verrez votre fichier téléchargé **DimDate2.txt**.
4. tooview propriétés, cliquez sur **DimDate2.txt**.
5. Notez que dans le panneau des propriétés hello Blob, vous pouvez télécharger ou supprimer le fichier de hello.
   
    ![Afficher le stockage blob Azure](./media/sql-data-warehouse-get-started-load-with-polybase/view-blob.png)

## <a name="step-2-create-an-external-table-for-hello-sample-data"></a>Étape 2 : Créer une table externe de données d’exemple hello
Dans cette section, nous créons une table externe qui définit les données d’exemple hello.

PolyBase utilise les données tooaccess de tables externes dans le stockage blob Azure. Car les données de salutation ne sont pas stockées dans l’entrepôt de données SQL, PolyBase gère les données externes de l’authentification toohello à l’aide d’une information d’identification de l’étendue de base de données.

exemple Hello dans cette étape utilise ces toocreate d’instructions Transact-SQL une table externe.

* [Create Master Key (Transact-SQL)] [ Create Master Key (Transact-SQL)] secret de hello tooencrypt de votre base de données d’une étendue d’informations d’identification.
* [Création d’informations d’identification d’une étendue de base de données (Transact-SQL)] [ Create Database Scoped Credential (Transact-SQL)] toospecify les informations d’authentification pour votre compte de stockage Azure.
* [Créer la Source de données externe (Transact-SQL)] [ Create External Data Source (Transact-SQL)] emplacement de hello toospecify de votre stockage d’objets blob Azure.
* [Créer un Format de fichier externe (Transact-SQL)] [ Create External File Format (Transact-SQL)] format de hello toospecify de vos données.
* [Créer une Table externe (Transact-SQL)] [ Create External Table (Transact-SQL)] toospecify la définition de table hello et l’emplacement de hello des données.

Exécutez cette requête sur votre base de données SQL Data Warehouse. Il crée une table externe nommée DimDate2External dans le schéma dbo hello qui pointe toohello DimDate2.txt exemples de données dans le stockage d’objets blob Azure hello.

```sql
-- A: Create a master key.
-- Only necessary if one does not already exist.
-- Required tooencrypt hello credential secret in hello next step.

CREATE MASTER KEY;


-- B: Create a database scoped credential
-- IDENTITY: Provide any string, it is not used for authentication tooAzure storage.
-- SECRET: Provide your Azure storage account key.


CREATE DATABASE SCOPED CREDENTIAL AzureStorageCredential
WITH
    IDENTITY = 'user',
    SECRET = '<azure_storage_account_key>'
;


-- C: Create an external data source
-- TYPE: HADOOP - PolyBase uses Hadoop APIs tooaccess data in Azure blob storage.
-- LOCATION: Provide Azure storage account name and blob container name.
-- CREDENTIAL: Provide hello credential created in hello previous step.

CREATE EXTERNAL DATA SOURCE AzureStorage
WITH (
    TYPE = HADOOP,
    LOCATION = 'wasbs://<blob_container_name>@<azure_storage_account_name>.blob.core.windows.net',
    CREDENTIAL = AzureStorageCredential
);


-- D: Create an external file format
-- FORMAT_TYPE: Type of file format in Azure storage (supported: DELIMITEDTEXT, RCFILE, ORC, PARQUET).
-- FORMAT_OPTIONS: Specify field terminator, string delimiter, date format etc. for delimited text files.
-- Specify DATA_COMPRESSION method if data is compressed.

CREATE EXTERNAL FILE FORMAT TextFile
WITH (
    FORMAT_TYPE = DelimitedText,
    FORMAT_OPTIONS (FIELD_TERMINATOR = ',')
);


-- E: Create hello external table
-- Specify column names and data types. This needs toomatch hello data in hello sample file.
-- LOCATION: Specify path toofile or directory that contains hello data (relative toohello blob container).
-- toopoint tooall files under hello blob container, use LOCATION='.'

CREATE EXTERNAL TABLE dbo.DimDate2External (
    DateId INT NOT NULL,
    CalendarQuarter TINYINT NOT NULL,
    FiscalQuarter TINYINT NOT NULL
)
WITH (
    LOCATION='/datedimension/',
    DATA_SOURCE=AzureStorage,
    FILE_FORMAT=TextFile
);


-- Run a query on hello external table

SELECT count(*) FROM dbo.DimDate2External;

```


Dans l’Explorateur d’objets SQL Server dans Visual Studio, vous pouvez voir le format de fichier externe hello, source de données externe et hello DimDate2External table.

![Afficher les tables externes](./media/sql-data-warehouse-get-started-load-with-polybase/external-table.png)

## <a name="step-3-load-data-into-sql-data-warehouse"></a>Étape 3 : Charger des données dans SQL Data Warehouse
Une fois qu’une table externe hello est créée, vous pouvez charger des données de hello dans une nouvelle table ou insérer dans une table existante.

* les données de salutation tooload dans une nouvelle table, exécutez hello [CREATE TABLE AS SELECT (Transact-SQL)] [ CREATE TABLE AS SELECT (Transact-SQL)] instruction. nouvelle table de Hello aura colonnes hello nommées dans la requête de hello. types de données Hello de colonnes de hello correspondra à des types de données hello dans la définition de la table externe hello.
* les données de salutation tooload dans une table existante, utilisez hello [INSERT... SELECT (Transact-SQL)] [ INSERT...SELECT (Transact-SQL)] instruction.

```sql
-- Load hello data from Azure blob storage tooSQL Data Warehouse

CREATE TABLE dbo.DimDate2
WITH
(   
    CLUSTERED COLUMNSTORE INDEX,
    DISTRIBUTION = ROUND_ROBIN
)
AS
SELECT * FROM [dbo].[DimDate2External];
```

## <a name="step-4-create-statistics-on-your-newly-loaded-data"></a>Étape 4 : Créer des statistiques sur vos données nouvellement chargées
SQL Data Warehouse ne prend pas en charge les statistiques de création ou de mise à jour automatiques. Par conséquent, les performances de requête tooachieve, il est important de statistiques toocreate sur chaque colonne de chaque table après hello d’abord chargement. Il est également important tooupdate statistiques après des modifications importantes dans les données de salutation.

Cet exemple crée des statistiques de colonne unique sur la nouvelle table de DimDate2 hello.

```sql
CREATE STATISTICS [DateId] on [DimDate2] ([DateId]);
CREATE STATISTICS [CalendarQuarter] on [DimDate2] ([CalendarQuarter]);
CREATE STATISTICS [FiscalQuarter] on [DimDate2] ([FiscalQuarter]);
```

toolearn, voir [statistiques][Statistics].  

## <a name="next-steps"></a>Étapes suivantes
Consultez hello [guide de PolyBase] [ PolyBase guide] pour plus d’informations à connaître lorsque vous développez une solution qui utilise PolyBase.

<!--Image references-->


<!--Article references-->
[PolyBase in SQL Data Warehouse Tutorial]: ./sql-data-warehouse-get-started-load-with-polybase.md
[Load data with bcp]: ./sql-data-warehouse-load-with-bcp.md
[Statistics]: ./sql-data-warehouse-tables-statistics.md
[PolyBase guide]: ./sql-data-warehouse-load-polybase-guide.md
[Getting Started with hello AzCopy Command-Line Utility]:../storage/common/storage-use-azcopy.md
[latest version of AzCopy]:../storage/common/storage-use-azcopy.md

<!--External references-->
[supported source/sink]: https://msdn.microsoft.com/library/dn894007.aspx
[copy activity]: https://msdn.microsoft.com/library/dn835035.aspx
[SQL Server destination adapter]: https://msdn.microsoft.com/library/ms141095.aspx
[SSIS]: https://msdn.microsoft.com/library/ms141026.aspx


[CREATE EXTERNAL DATA SOURCE (Transact-SQL)]:https://msdn.microsoft.com/library/dn935022.aspx
[CREATE EXTERNAL FILE FORMAT (Transact-SQL)]:https://msdn.microsoft.com/library/dn935026.aspx
[CREATE EXTERNAL TABLE (Transact-SQL)]:https://msdn.microsoft.com/library/dn935021.aspx

[DROP EXTERNAL DATA SOURCE (Transact-SQL)]:https://msdn.microsoft.com/library/mt146367.aspx
[DROP EXTERNAL FILE FORMAT (Transact-SQL)]:https://msdn.microsoft.com/library/mt146379.aspx
[DROP EXTERNAL TABLE (Transact-SQL)]:https://msdn.microsoft.com/library/mt130698.aspx

[CREATE TABLE AS SELECT (Transact-SQL)]:https://msdn.microsoft.com/library/mt204041.aspx
[INSERT...SELECT (Transact-SQL)]:https://msdn.microsoft.com/library/ms174335.aspx
[CREATE MASTER KEY (Transact-SQL)]:https://msdn.microsoft.com/library/ms174382.aspx
[CREATE CREDENTIAL (Transact-SQL)]:https://msdn.microsoft.com/library/ms189522.aspx
[CREATE DATABASE SCOPED CREDENTIAL (Transact-SQL)]:https://msdn.microsoft.com/library/mt270260.aspx
[DROP CREDENTIAL (Transact-SQL)]:https://msdn.microsoft.com/library/ms189450.aspx
