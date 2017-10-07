---
redirect_url: /azure/sql-data-warehouse/sql-data-warehouse-load-with-data-factory
title: "données aaaLoad avec Azure Data Factory | Documents Microsoft"
description: "En savoir plus les données tooload avec Azure Data Factory"
services: sql-data-warehouse
documentationcenter: NA
author: twounder
manager: jhubbard
editor: 
tags: azure-sql-data-warehouse
ms.assetid: ac7ddaa7-a3a5-4e15-b3cf-c696d2d105df
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.date: 10/31/2016
ms.author: mausher;barbkess
ms.custom: loading
ms.openlocfilehash: 4186bd88d14be33f90130a41e8df06ce1d7cbab2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="load-data-with-azure-data-factory"></a>Téléchargement de données avec Azure Data Factory
> [!div class="op_single_selector"]
> * [Redgate](sql-data-warehouse-load-with-redgate.md)  
> * [Data Factory](sql-data-warehouse-get-started-load-with-azure-data-factory.md)  
> * [PolyBase](sql-data-warehouse-get-started-load-with-polybase.md)  
> * [BCP](sql-data-warehouse-load-with-bcp.md)  
> 
> 

Ce didacticiel vous montre comment toocreate un pipeline de données Azure Data Factory toomove tooAzure de l’objet Blob de stockage Azure SQL Data Warehouse. Avec hello, vous allez comme suit :

* Données d’exemple de configuration dans un objet blob Azure Storage.
* Connecter des ressources tooAzure Data Factory.
* Créer une pipeline des données de toomove à partir d’objets BLOB de stockage tooSQL l’entrepôt de données.

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Loading-Azure-SQL-Data-Warehouse-with-Azure-Data-Factory/player]
> 
> 

## <a name="before-you-begin"></a>Avant de commencer
toofamiliarize vous-même avec Azure Data Factory, consultez [Introduction tooAzure Data Factory][Introduction tooAzure Data Factory].

### <a name="create-or-identify-resources"></a>Créer ou identifier des ressources
Avant de commencer ce didacticiel, vous devez hello toohave suivant des ressources :

* **Objet Blob de stockage Azure**: ce didacticiel utilise l’objet Blob de stockage Azure en tant que source de données hello pour le pipeline d’Azure Data Factory hello et par conséquent, vous devez toohave une toostore disponible hello exemples de données. Si vous n’avez pas déjà, découvrez comment trop[créer un compte de stockage][Create a storage account].
* **SQL Data Warehouse**: ces didacticiel se déplace hello données à partir de l’objet Blob de stockage Azure trop SQL Data Warehouse et donc ont besoin toohave en ligne un entrepôt de données qui est chargé avec hello exemples de données AdventureWorksDW. Si vous n’avez pas déjà d’un entrepôt de données, découvrez comment trop[configurer un][Create a SQL Data Warehouse]. Si vous disposez d’un entrepôt de données mais que vous n’avez pas mettre en service avec les données d’exemple hello, vous pouvez [charger manuellement][Load sample data into SQL Data Warehouse].
* **Azure Data Factory**: Azure Data Factory se termine la charge réelle de hello et par conséquent, vous devez toohave une que vous pouvez utiliser le pipeline de déplacement des données toobuild hello. Si vous n’avez pas déjà, découvrez comment toocreate un à l’étape 1 de [prise en main Azure Data Factory (éditeur Data Factory)][Get started with Azure Data Factory (Data Factory Editor)].
* **AZCopy**: vous devez AZCopy toocopy hello exemples de données à partir de votre objet Blob de stockage Azure de tooyour client local. Pour obtenir des instructions d’installation, consultez hello [AZCopy documentation][AZCopy documentation].

## <a name="step-1-copy-sample-data-tooazure-storage-blob"></a>Étape 1 : Copie exemple tooAzure de données objet Blob de stockage
Une fois que toutes les parties hello prêt, vous êtes prêt toocopy exemple tooyour de données objet Blob de stockage Azure.

1. [Téléchargez les exemples de données][Download sample data]. Ces données ajoute trois ans de données de ventes tooyour exemples de données AdventureWorksDW.
2. Utilisez cette commande de toocopy AZCopy hello trois années de tooyour de données objet Blob de stockage Azure.
   
    ````
    AzCopy /Source:<Sample Data Location>  /Dest:https://<storage account>.blob.core.windows.net/<container name> /DestKey:<storage key> /Pattern:FactInternetSales.csv
    ````

## <a name="step-2-connect-resources-tooazure-data-factory"></a>Étape 2 : Connecter des ressources tooAzure Data Factory
Maintenant que les données de salutation sont en place, nous pouvons créer les données de salutation hello Azure Data Factory pipeline toomove depuis le stockage blob Azure dans SQL Data Warehouse.

tooget démarré, ouvrez hello [portail Azure] [ Azure portal] et sélectionnez votre data factory hello menu de gauche.

### <a name="step-21-create-linked-service"></a>Étape 2.1 : créer un service lié
Lier votre compte de stockage Azure et de la fabrique de données SQL Data Warehouse tooyour.  

1. Tout d’abord, commencer le processus d’inscription de hello en cliquant sur la section « Services liés » de hello votre fabrique de données et puis cliquez sur « Nouveau magasin de données. » Choisissez un tooregister nom votre stockage azure sous, sélectionnez Azure Storage, comme votre type, puis entrez votre nom de compte et votre clé de compte.
2. tooregister SQL Data Warehouse accédez toohello les section « Auteur et déployer », sélectionnez « Nouveau magasin de données », puis sur Azure SQL Data Warehouse. Copiez et collez ce modèle, puis renseignez vos informations.
   
    ```JSON
    {
        "name": "<Linked Service Name>",
        "properties": {
            "description": "",
            "type": "AzureSqlDW",
            "typeProperties": {
                 "connectionString": "Data Source=tcp:<server name>.database.windows.net,1433;Initial Catalog=<server name>;Integrated Security=False;User ID=<user>@<servername>;Password=<password>;Connect Timeout=30;Encrypt=True"
             }
        }
    }
    ```

### <a name="step-22-define-hello-dataset"></a>Étape 2.2 : Définir le jeu de données hello
Après que la création d’hello des services liés, il nous faudra toodefine hello des ensembles de données.  Ici, cela signifie que la définition de structure hello de données hello sont déplacées à partir de votre entrepôt de données de stockage tooyour.  Vous pouvez en savoir plus sur la création

1. Démarrer ce processus en naviguant dans la section « Auteur et déployer » de toohello votre fabrique de données.
2. Cliquez sur 'Nouveau jeu de données', 'Le stockage Blob Azure' toolink votre fabrique de données de stockage tooyour.  Vous pouvez utiliser hello ci-dessous script toodefine vos données dans le stockage d’objets Blob Azure :
   
    ```JSON
    {
        "name": "<Dataset Name>",
        "properties": {
            "type": "AzureBlob",
            "linkedServiceName": "<linked storage name>",
            "typeProperties": {
                "folderPath": "<containter name>",
                "fileName": "FactInternetSales.csv",
                "format": {
                "type": "TextFormat",
                "columnDelimiter": ",",
                "rowDelimiter": "\n"
                }
            },
            "external": true,
            "availability": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "externalData": {
                    "retryInterval": "00:01:00",
                    "retryTimeout": "00:10:00",
                    "maximumRetry": 3
                }
            }
        }
    }
    ```
3. Maintenant, nous allons définir notre jeu de données pour SQL Data Warehouse. Nous allons commencer Bonjour même manière, en cliquant sur « Nouveau jeu de données », puis sur Azure SQL Data Warehouse.
   
    ```JSON
    {
        "name": "DWDataset",
        "properties": {
            "type": "AzureSqlDWTable",
            "linkedServiceName": "AzureSqlDWLinkedService",
            "typeProperties": {
                "tableName": "FactInternetSales"
            },
            "availability": {
                "frequency": "Hour",
                "interval": 1
            }
        }
    }
    ```

## <a name="step-3-create-and-run-your-pipeline"></a>Étape 3 : créer et exécuter le pipeline
Enfin, nous configurer et exécuter le pipeline de hello dans Azure Data Factory.  Il s’agit d’opération hello qui se termine le déplacement des données réelles de hello.  Vous trouverez une vue complète des opérations hello que vous pouvez réaliser avec SQL Data Warehouse et Azure Data Factory [ici][Move data tooand from Azure SQL Data Warehouse using Azure Data Factory].

Bonjour section « Auteur et déployer », cliquez sur 'Plus les commandes', « Nouveau Pipeline ».  Après avoir créé le pipeline de hello, vous pouvez utiliser hello ci-dessous code tootransfer hello données tooyour data warehouse :

```JSON
{
    "name": "<Pipeline Name>",
    "properties": {
        "description": "<Description>",
        "activities": [
          {
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "BlobSource",
                    "skipHeaderLineCount": 1
                },
                "sink": {
                    "type": "SqlDWSink",
                    "writeBatchSize": 0,
                    "writeBatchTimeout": "00:00:10"
                }
            },
            "inputs": [
              {
                "name": "<Storage Dataset>"
              }
            ],
            "outputs": [
              {
                "name": "<Data Warehouse Dataset>"
              }
            ],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "Sample Copy",
            "description": "Copy Activity"
          }
        ],
        "start": "<Date YYYY-MM-DD>",
        "end": "<Date YYYY-MM-DD>",
        "isPaused": false
    }
}
```

## <a name="next-steps"></a>Étapes suivantes
toolearn plus, commencez par l’affichage :

* [Parcours d’apprentissage Azure Data Factory][Azure Data Factory learning path].
* [Azure SQL Data Warehouse Connector][Azure SQL Data Warehouse Connector]. Il s’agit de rubrique de référence de base hello pour l’utilisation d’Azure Data Factory et Azure SQL Data Warehouse.

Ces rubriques fournissent des informations détaillées sur Azure Data Factory. Elles présentent de base de données SQL Azure ou HDInsight, mais les informations de hello tooAzure SQL Data Warehouse s’appliquent également.

* [Didacticiel : Prise en main Azure Data Factory] [ Tutorial: Get started with Azure Data Factory] didacticiel de base hello pour le traitement des données avec Azure Data Factory. Dans ce didacticiel, vous créer votre premier pipeline qui utilise HDInsight tootransform et analyser les journaux web sur une base mensuelle. Notez que ce didacticiel ne couvre aucune activité de copie.
* [Didacticiel : Copier des données à partir de l’objet Blob de stockage Azure tooAzure base de données SQL][Tutorial: Copy data from Azure Storage Blob tooAzure SQL Database]. Dans ce didacticiel, vous créez un pipeline de données de toocopy Azure Data Factory à partir de l’objet Blob de stockage Azure tooAzure base de données SQL.

<!--Image references-->

<!--Article references-->
[AZCopy documentation]: ../storage/storage-use-azcopy.md
[Azure SQL Data Warehouse Connector]: ../data-factory/data-factory-azure-sql-data-warehouse-connector.md
[BCP]: sql-data-warehouse-load-with-bcp.md
[Create a SQL Data Warehouse]: sql-data-warehouse-get-started-provision.md
[Create a storage account]: ../storage/storage-create-storage-account.md#create-a-storage-account
[Data Factory]: sql-data-warehouse-get-started-load-with-azure-data-factory.md
[Get started with Azure Data Factory (Data Factory Editor)]: ../data-factory/data-factory-build-your-first-pipeline-using-editor.md
[Introduction tooAzure Data Factory]: ../data-factory/data-factory-introduction.md
[Load sample data into SQL Data Warehouse]: sql-data-warehouse-load-sample-databases.md
[Move data tooand from Azure SQL Data Warehouse using Azure Data Factory]: ../data-factory/data-factory-azure-sql-data-warehouse-connector.md
[PolyBase]: sql-data-warehouse-get-started-load-with-polybase.md
[Tutorial: Copy data from Azure Storage Blob tooAzure SQL Database]: ../data-factory/data-factory-copy-data-from-azure-blob-storage-to-sql-database.md
[Tutorial: Get started with Azure Data Factory]: ../data-factory/data-factory-build-your-first-pipeline.md

<!--MSDN references-->

<!--Other Web references-->
[Azure Data Factory learning path]: https://azure.microsoft.com/documentation/learning-paths/data-factory
[Azure portal]: https://portal.azure.com
[Download sample data]: https://migrhoststorage.blob.core.windows.net/adfsample/FactInternetSales.csv
