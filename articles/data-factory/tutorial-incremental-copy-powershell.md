---
title: "Copier de façon incrémentielle des données en utilisant Azure Data Factory | Microsoft Docs"
description: "Dans ce didacticiel, vous allez créer un pipeline Azure Data Factory qui copie de façon incrémentielle les données d’une base de données Azure SQL Database dans un stockage Blob Azure."
services: data-factory
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: spelluru
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/10/2017
ms.author: shlo
ms.openlocfilehash: 91b632b6d2c2917acf17e9d89c1b5a4b0f8b1c33
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/11/2017
---
# <a name="incrementally-load-data-from-azure-sql-database-to-azure-blob-storage"></a>Charger de façon incrémentielle les données d’une base de données Azure SQL Database dans un stockage Blob Azure
Azure Data Factory est un service d’intégration de données basé sur le cloud qui vous permet de créer des flux de travail orientés données dans le cloud pour orchestrer et automatiser le déplacement et la transformation des données. Grâce à Azure Data Factory, vous pouvez créer et planifier des flux de travail orientés données (appelés pipelines) capables d’ingérer des données provenant de différents magasins de données, de traiter/transformer les données à l’aide de services de calcul comme Azure HDInsight Hadoop, Spark, Azure Data Lake Analytics et Azure Machine Learning, et de publier des données de sortie dans des magasins de données tels qu’Azure SQL Data Warehouse pour que des applications décisionnelles (BI) puissent les utiliser. 

En matière d’intégration de données, l’un des scénarios très répandu est celui qui consiste à charger les données de façon incrémentielle et périodique pour actualiser le résultat de l’analyse après les chargements de données et l’analyse de départ. Dans ce didacticiel, vous allez pour l’essentiel charger uniquement des enregistrements nouveaux ou mis à jour dans des récepteurs de données à partir de sources de données. Cette solution s’avère plus efficace que les chargements complets, surtout en présence de jeux de données volumineux.    

Vous pouvez utiliser Data Factory pour créer des solutions de limite supérieure en vue de charger les données de façon incrémentielle à l’aide des activités de recherche, de copie et de procédure stockée dans un pipeline.  

Dans ce didacticiel, vous allez effectuer les étapes suivantes :

> [!div class="checklist"]
> * Préparer le magasin de données pour y stocker la valeur de limite.   
> * Créer une fabrique de données.
> * créez des services liés. 
> * Créer des jeux de données source, récepteur et limite.
> * Créer un pipeline.
> * Exécuter le pipeline.
> * Surveiller l’exécution du pipeline. 

## <a name="overview"></a>Vue d'ensemble
Voici le diagramme général de la solution : 

![Chargement incrémentiel de données](media\tutorial-Incrementally-load-data-from-azure-sql-to-blob\incrementally-load.png)

Voici les étapes importantes à suivre pour créer cette solution : 

1. **Sélectionner la colonne de limite**.
    Sélectionnez une colonne dans le magasin de données sources, qui peut servir à découper les enregistrements nouveaux ou mis à jour pour chaque exécution. Normalement, les données contenues dans cette colonne sélectionnée (par exemple, last_modify_time ou ID) continuent de croître à mesure que des lignes sont créées ou mises à jour. La valeur maximale de cette colonne est utilisée comme limite.
2. **Préparer un magasin de données pour stocker la valeur de limite**.   
    Dans ce didacticiel, la valeur de limite est stockée dans une base de données Azure SQL Database.
3. **Créer un pipeline avec le flux de travail suivant :** 
    
    Le pipeline de cette solution compte les activités suivantes :
  
    1. Créez deux activités de **recherche**. Servez-vous de la première activité de recherche pour récupérer la dernière valeur de limite. Servez-vous de la deuxième activité de recherche pour récupérer la nouvelle valeur de limite. Ces valeurs de limite sont passées à l’activité de copie. 
    2. Créez une **activité de copie** qui copie les lignes du magasin de données sources dont la valeur de la colonne est supérieure à l’ancienne valeur et inférieure à la nouvelle. Elle copie ensuite les données delta du magasin de données sources dans un stockage Blob sous la forme d’un nouveau fichier. 
    3. Créez une **activité de procédure stockée** qui met à jour la valeur de limite pour le pipeline s’exécutant la prochaine fois. 


Si vous n’avez pas d’abonnement Azure, créez un compte [gratuit](https://azure.microsoft.com/free/) avant de commencer.

## <a name="prerequisites"></a>Composants requis
* **Base de données SQL Azure**. Vous utilisez la base de données comme magasin de données **sources**. Si vous n’avez pas de base de données Azure SQL Database, consultez l’article [Création d’une base de données Azure SQL](../sql-database/sql-database-get-started-portal.md) pour savoir comme en créer une.
* **Compte Stockage Azure**. Vous utilisez le stockage Blob comme magasin de données **récepteur**. Si vous n’avez pas de compte de stockage Azure, consultez l’article [Créer un compte de stockage](../storage/common/storage-create-storage-account.md#create-a-storage-account) pour savoir comment en créer un. Créez un conteneur sous le nom **adftutorial**. 
* **Azure PowerShell**. Suivez les instructions de la page [Installation et configuration d’Azure PowerShell](/powershell/azure/install-azurerm-ps).

### <a name="create-a-data-source-table-in-your-azure-sql-database"></a>Créer une table de source de données dans votre base de données Azure SQL Database
1. Ouvrez **SQL Server Management Studio** puis, dans l’**Explorateur de serveurs**, cliquez avec le bouton droit sur la base de données et choisissez **Nouvelle requête**.
2. Exécutez la commande SQL suivante sur votre base de données Azure SQL Database pour créer une table sous le nom `data_source_table` comme magasin de la source de données.  
    
    ```sql
    create table data_source_table
    (
        PersonID int,
        Name varchar(255),
        LastModifytime datetime
    );

    INSERT INTO data_source_table
    (PersonID, Name, LastModifytime)
    VALUES
    (1, 'aaaa','9/1/2017 12:56:00 AM'),
    (2, 'bbbb','9/2/2017 5:23:00 AM'),
    (3, 'cccc','9/3/2017 2:36:00 AM'),
    (4, 'dddd','9/4/2017 3:21:00 AM'),
    (5, 'eeee','9/5/2017 8:06:00 AM');
    ```
    Dans ce didacticiel, vous utilisez **LastModifytime** comme colonne de **limite**.  Les données contenues dans le magasin de la source de données sont indiquées dans le tableau suivant :

    ```
    PersonID | Name | LastModifytime
    -------- | ---- | --------------
    1 | aaaa | 2017-09-01 00:56:00.000
    2 | bbbb | 2017-09-02 05:23:00.000
    3 | cccc | 2017-09-03 02:36:00.000
    4 | dddd | 2017-09-04 03:21:00.000
    5 | eeee | 2017-09-05 08:06:00.000
    ```

### <a name="create-another-table-in-sql-database-to-store-the-high-watermark-value"></a>Créer une autre table dans la base de données SQL pour stocker la valeur de limite supérieure
1. Exécutez la commande SQL suivante sur votre base de données Azure SQL Database pour créer une table sous le nom `watermarktable` pour stocker la valeur de limite.  
    
    ```sql
    create table watermarktable
    (
    
    TableName varchar(255),
    WatermarkValue datetime,
    );
    ```
3. Définissez la **valeur** par défaut de la limite supérieure avec le nom de table du magasin de données sources.  (Dans ce didacticiel, le nom de table est **data_source_table**)

    ```sql
    INSERT INTO watermarktable
    VALUES ('data_source_table','1/1/2010 12:00:00 AM')    
    ```
4. Passez en revue les données de la table `watermarktable`.
    
    ```sql
    Select * from watermarktable
    ```
    Output: 

    ```
    TableName  | WatermarkValue
    ----------  | --------------
    data_source_table | 2010-01-01 00:00:00.000
    ```

### <a name="create-a-stored-procedure-in-azure-sql-database"></a>Créer une procédure stockée dans la base de données Azure SQL Database 

Exécutez la commande suivante pour créer une procédure stockée dans votre base de données Azure SQL Database.

```sql
CREATE PROCEDURE sp_write_watermark @LastModifiedtime datetime, @TableName varchar(50)
AS

BEGIN
    
    UPDATE watermarktable
    SET [WatermarkValue] = @LastModifiedtime 
WHERE [TableName] = @TableName
    
END
```

## <a name="create-a-data-factory"></a>Créer une fabrique de données

1. Lancez **PowerShell**. Conservez Azure PowerShell ouvert jusqu’à la fin de ce didacticiel. Si vous fermez puis rouvrez Azure PowerShell, vous devez réexécuter ces commandes.

    Exécutez la commande suivante, puis saisissez le nom d’utilisateur et le mot de passe que vous avez utilisés pour la connexion au portail Azure :
        
    ```powershell
    Login-AzureRmAccount
    ```        
    Exécutez la commande suivante pour afficher tous les abonnements de ce compte :

    ```powershell
    Get-AzureRmSubscription
    ```
    Exécutez la commande suivante pour sélectionner l’abonnement que vous souhaitez utiliser. Remplacez **SubscriptionId** par l’ID de votre abonnement Azure :

    ```powershell
    Select-AzureRmSubscription -SubscriptionId "<SubscriptionId>"       
    ```
2. Exécutez l’applet de commande **Set-AzureRmDataFactoryV2** pour créer une fabrique de données. Avant d’exécuter la commande, remplacez les espaces réservés par vos propres valeurs.

    ```powershell
    Set-AzureRmDataFactoryV2 -ResourceGroupName "<your resource group to create the factory>" -Location "East US" -Name "<specify the name of data factory to create. It must be globally unique.>" 
    ```

    Notez les points suivants :

    * Le nom de la fabrique de données Azure doit être un nom global unique. Si vous recevez l’erreur suivante, changez le nom, puis réessayez.

        ```
        The specified Data Factory name '<data factory name>' is already in use. Data Factory names must be globally unique.
        ```

    * Pour créer des instances de fabrique de données, vous devez avoir le statut d’administrateur/collaborateur de l’abonnement Azure.
    * Actuellement, Data Factory V2 vous permet de créer une fabrique de données uniquement dans la région Est des États-Unis. Les magasins de données (Stockage Azure, Azure SQL Database, etc.) et les services de calcul (HDInsight, etc.) utilisés par la fabrique de données peuvent se trouver dans d’autres régions.


## <a name="create-linked-services"></a>Créez des services liés
Vous allez créer des services liés dans une fabrique de données pour lier vos magasins de données et vos services de calcul à la fabrique de données. Dans cette section, vous allez créer des services liés à votre compte de stockage Azure et à la base de données Azure SQL Database. 

### <a name="create-azure-storage-linked-service"></a>Créer un service lié Stockage Azure.
1. Créez un fichier JSON sous le nom **AzureStorageLinkedService.json** dans le dossier **C:\ADF** avec le contenu suivant : (créez le dossier ADF s’il n’existe pas déjà). Remplacez `<accountName>`, `<accountKey>` par le nom et la clé de votre compte de stockage Azure avant d’enregistrer le fichier.

    ```json
    {
        "name": "AzureStorageLinkedService",
        "properties": {
            "type": "AzureStorage",
            "typeProperties": {
                "connectionString": {
                    "value": "DefaultEndpointsProtocol=https;AccountName=<accountName>;AccountKey=<accountKey>",
                    "type": "SecureString"
                }
            }
        }
    }
    ```
2. Dans **Azure PowerShell**, accédez au dossier **ADF**.
3. Exécutez l’applet de commande **Set-AzureRmDataFactoryV2LinkedService** pour créer le service lié **AzureStorageLinkedService**. Dans l’exemple suivant, vous passez les valeurs des paramètres **ResourceGroupName** et **DataFactoryName**. 

    ```powershell
    Set-AzureRmDataFactoryV2LinkedService -DataFactoryName $dataFactoryName -ResourceGroupName $resourceGroupName -Name "AzureStorageLinkedService" -File ".\AzureStorageLinkedService.json"
    ```

    Voici l'exemple de sortie :

    ```json
    LinkedServiceName : AzureStorageLinkedService
    ResourceGroupName : <resourceGroupName>
    DataFactoryName   : <dataFactoryName>
    Properties        : Microsoft.Azure.Management.DataFactory.Models.AzureStorageLinkedService
    ```

### <a name="create-azure-sql-database-linked-service"></a>Créez le service lié Azure SQL Database.
1. Créez un fichier JSON sous le nom **AzureSQLDatabaseLinkedService.json** dans le dossier **C:\ADF** avec le contenu suivant : (créez le dossier ADF s’il n’existe pas déjà). Avant d’enregistrer le fichier, remplacez **&lt;server&gt;, &lt;user id&gt; et &lt;password&gt;**  par le nom de votre serveur SQL Azure, l’ID utilisateur et le mot de passe. 

    ```json
    {
        "name": "AzureSQLDatabaseLinkedService",
        "properties": {
            "type": "AzureSqlDatabase",
            "typeProperties": {
                "connectionString": {
                    "value": "Server = tcp:<server>.database.windows.net,1433;Initial Catalog=<database name>; Persist Security Info=False; User ID=<user name> ; Password=<password>; MultipleActiveResultSets = False; Encrypt = True; TrustServerCertificate = False; Connection Timeout = 30;",
                    "type": "SecureString"
                }
            }
        }
    }
    ```
2. Dans **Azure PowerShell**, accédez au dossier **ADF**.
3. Exécutez l’applet de commande **Set-AzureRmDataFactoryV2LinkedService** pour créer le service lié **AzureSQLDatabaseLinkedService**. 

    ```powershell
    Set-AzureRmDataFactoryV2LinkedService -DataFactoryName $dataFactoryName -ResourceGroupName $resourceGroupName -Name "AzureSQLDatabaseLinkedService" -File ".\AzureSQLDatabaseLinkedService.json"
    ```

    Voici l'exemple de sortie :

    ```json
    LinkedServiceName : AzureSQLDatabaseLinkedService
    ResourceGroupName : ADF
    DataFactoryName   : incrementalloadingADF
    Properties        : Microsoft.Azure.Management.DataFactory.Models.AzureSqlDatabaseLinkedService
    ProvisioningState :
    ```

## <a name="create-datasets"></a>Créez les jeux de données
Dans cette étape, vous allez créer des jeux de données pour représenter les données sources et de réception. 

### <a name="create-a-source-dataset"></a>Créer un jeu de données source

1. Créez un fichier JSON sous le nom SourceDataset.json dans le même dossier avec le contenu suivant : 

    ```json
    {
        "name": "SourceDataset",
        "properties": {
            "type": "AzureSqlTable",
            "typeProperties": {
                "tableName": "data_source_table"
            },
            "linkedServiceName": {
                "referenceName": "AzureSQLDatabaseLinkedService",
                "type": "LinkedServiceReference"
            }
        }
    }
   
    ```
    Dans ce didacticiel, nous utilisons le nom de table **data_source_table**. Remplacez-le si vous utilisez une table de nom différent. 
2.  Exécutez l’applet de commande Set-AzureRmDataFactoryV2Dataset pour créer le jeu de données SourceDataset.
    
    ```powershell
    Set-AzureRmDataFactoryV2Dataset -DataFactoryName $dataFactoryName -ResourceGroupName $resourceGroupName -Name "SourceDataset" -File ".\SourceDataset.json"
    ```

    Voici l’exemple de sortie de l’applet de commande :
    
    ```json
    DatasetName       : SourceDataset
    ResourceGroupName : ADF
    DataFactoryName   : incrementalloadingADF
    Structure         :
    Properties        : Microsoft.Azure.Management.DataFactory.Models.AzureSqlTableDataset
    ```

### <a name="create-a-sink-dataset"></a>Créer un jeu de données récepteur

1. Créez un fichier JSON sous le nom SinkDataset.json dans le même dossier avec le contenu suivant : 

    ```json
    {
        "name": "SinkDataset",
        "properties": {
            "type": "AzureBlob",
            "typeProperties": {
                "folderPath": "adftutorial/incrementalcopy",
                "fileName": "@CONCAT('Incremental-', pipeline().RunId, '.txt')", 
                "format": {
                    "type": "TextFormat"
                }
            },
            "linkedServiceName": {
                "referenceName": "AzureStorageLinkedService",
                "type": "LinkedServiceReference"
            }
        }
    }   
    ```

    > [!IMPORTANT]
    > Cet extrait de code suppose que vous disposez d’un conteneur d’objets blob nommé **adftutorial** dans le stockage Blob Azure. Créez le conteneur s’il n’existe pas (ou) attribuez-lui le nom d’un conteneur existant. Le dossier de sortie `incrementalcopy` est automatiquement créé s’il n’existe pas dans le conteneur. Dans ce didacticiel, le nom de fichier est généré dynamiquement en utilisant l’expression : `@CONCAT('Incremental-', pipeline().RunId, '.txt')`.
2.  Exécutez l’applet de commande Set-AzureRmDataFactoryV2Dataset pour créer le jeu de données SinkDataset.
    
    ```powershell
    Set-AzureRmDataFactoryV2Dataset -DataFactoryName $dataFactoryName -ResourceGroupName $resourceGroupName -Name "SinkDataset" -File ".\SinkDataset.json"
    ```

    Voici l’exemple de sortie de l’applet de commande :
    
    ```json
    DatasetName       : SinkDataset
    ResourceGroupName : ADF
    DataFactoryName   : incrementalloadingADF
    Structure         :
    Properties        : Microsoft.Azure.Management.DataFactory.Models.AzureBlobDataset    
    ```

## <a name="create-a-dataset-for-watermark"></a>Créer un jeu de données pour la limite
Dans cette étape, vous allez créer un jeu de données pour stocker une valeur de limite supérieure. 

1. Créez un fichier JSON sous le nom WatermarkDataset.json dans le même dossier avec le contenu suivant : 

    ```json
    {
        "name": " WatermarkDataset ",
        "properties": {
            "type": "AzureSqlTable",
            "typeProperties": {
                "tableName": "watermarktable"
            },
            "linkedServiceName": {
                "referenceName": "AzureSQLDatabaseLinkedService",
                "type": "LinkedServiceReference"
            }
        }
    }    
    ```
2.  Exécutez l’applet de commande Set-AzureRmDataFactoryV2Dataset pour créer le jeu de données WatermarkDataset.
    
    ```powershell
    Set-AzureRmDataFactoryV2Dataset -DataFactoryName $dataFactoryName -ResourceGroupName $resourceGroupName -Name "WatermarkDataset" -File ".\WatermarkDataset.json"
    ```

    Voici l’exemple de sortie de l’applet de commande :
    
    ```json
    DatasetName       : WatermarkDataset
    ResourceGroupName : ADF
    DataFactoryName   : incrementalloadingADF
    Structure         :
    Properties        : Microsoft.Azure.Management.DataFactory.Models.AzureSqlTableDataset    
    ```

## <a name="create-a-pipeline"></a>Créer un pipeline
Dans ce didacticiel, vous allez créer un pipeline avec deux activités de recherche, une activité de copie et une activité de procédure stockée chaînées dans le même pipeline. 


1. Créez un fichier JSON sous le nom IncrementalCopyPipeline.json dans le même dossier avec le contenu suivant. 

    ```json
    {
        "name": "IncrementalCopyPipeline",
        "properties": {
            "activities": [
                {
                    "name": "LookupOldWaterMarkActivity",
                    "type": "Lookup",
                    "typeProperties": {
                        "source": {
                        "type": "SqlSource",
                        "sqlReaderQuery": "select * from watermarktable"
                        },
    
                        "dataset": {
                        "referenceName": "WatermarkDataset",
                        "type": "DatasetReference"
                        }
                    }
                },
                {
                    "name": "LookupNewWaterMarkActivity",
                    "type": "Lookup",
                    "typeProperties": {
                        "source": {
                            "type": "SqlSource",
                            "sqlReaderQuery": "select MAX(LastModifytime) as NewWatermarkvalue from data_source_table"
                        },
    
                        "dataset": {
                        "referenceName": "SourceDataset",
                        "type": "DatasetReference"
                        }
                    }
                },
                
                {
                    "name": "IncrementalCopyActivity",
                    "type": "Copy",
                    "typeProperties": {
                        "source": {
                            "type": "SqlSource",
                            "sqlReaderQuery": "select * from data_source_table where LastModifytime > '@{activity('LookupOldWaterMarkActivity').output.firstRow.WatermarkValue}' and LastModifytime <= '@{activity('LookupNewWaterMarkActivity').output.firstRow.NewWatermarkvalue}'"
                        },
                        "sink": {
                            "type": "BlobSink"
                        }
                    },
                    "dependsOn": [
                        {
                            "activity": "LookupNewWaterMarkActivity",
                            "dependencyConditions": [
                                "Succeeded"
                            ]
                        },
                        {
                            "activity": "LookupOldWaterMarkActivity",
                            "dependencyConditions": [
                                "Succeeded"
                            ]
                        }
                    ],
    
                    "inputs": [
                        {
                            "referenceName": "SourceDataset",
                            "type": "DatasetReference"
                        }
                    ],
                    "outputs": [
                        {
                            "referenceName": "SinkDataset",
                            "type": "DatasetReference"
                        }
                    ]
                },
    
                {
                    "name": "StoredProceduretoWriteWatermarkActivity",
                    "type": "SqlServerStoredProcedure",
                    "typeProperties": {
    
                        "storedProcedureName": "sp_write_watermark",
                        "storedProcedureParameters": {
                            "LastModifiedtime": {"value": "@{activity('LookupNewWaterMarkActivity').output.firstRow.NewWatermarkvalue}", "type": "datetime" },
                            "TableName":  { "value":"@{activity('LookupOldWaterMarkActivity').output.firstRow.TableName}", "type":"String"}
                        }
                    },
    
                    "linkedServiceName": {
                        "referenceName": "AzureSQLDatabaseLinkedService",
                        "type": "LinkedServiceReference"
                    },
    
                    "dependsOn": [
                        {
                            "activity": "IncrementalCopyActivity",
                            "dependencyConditions": [
                                "Succeeded"
                            ]
                        }
                    ]
                }
            ],
            
        }
    }
    ```json

    If you are using a source table with a name different from the one used in the tutorial (**data_source_table**), replace **data_source_table** in the sqlReaderQuery with the name of your source table. 
    

2. Run the Set-AzureRmDataFactoryV2Pipeline cmdlet to create the pipeline: IncrementalCopyPipeline.
    
   ```powershell
   Set-AzureRmDataFactoryV2Pipeline -DataFactoryName $dataFactoryName -ResourceGroupName $resourceGroupName -Name "IncrementalCopyPipeline" -File ".\IncrementalCopyPipeline.json"
   ``` 

   Voici l'exemple de sortie : 

   ```json
    PipelineName      : IncrementalCopyPipeline
    ResourceGroupName : ADF
    DataFactoryName   : incrementalloadingADF
    Activities        : {LookupOldWaterMarkActivity, LookupNewWaterMarkActivity, IncrementalCopyActivity, StoredProceduretoWriteWatermarkActivity}
    Parameters        :
   ```
 
## <a name="run-the-pipeline"></a>Exécuter le pipeline

1. Exécutez le pipeline **IncrementalCopyPipeline** en utilisant l’applet de commande **Invoke-AzureRmDataFactoryV2Pipeline**. Remplacez les espaces réservés par votre propre groupe de ressources et votre propre nom de fabrique de données.

    ```powershell
    $RunId = Invoke-AzureRmDataFactoryV2Pipeline -PipelineName "IncrementalCopyPipeline" -ResourceGroup "<your resource group>" -dataFactoryName "<your data factory name>"
    ``` 
2. Vérifiez l’état du pipeline en exécutant l’applet de commande Get-AzureRmDataFactoryV2ActivityRun jusqu’à ce que toutes les activités soient en cours d’exécution. Remplacez les espaces réservés des paramètres RunStartedAfter et RunStartedBefore par les dates qui vous conviennent.  Dans ce didacticiel, nous utilisons RunStartedAfter-« 2017/09/14 » - RunStartedBefore « 2017/09/15 »

    ```powershell
    Get-AzureRmDataFactoryV2ActivityRun -DataFactoryName $dataFactoryName -ResourceGroupName $resourceGroupName -PipelineRunId $RunId -RunStartedAfter "<start time>" -RunStartedBefore "<end time>"
    ```

    Voici l'exemple de sortie :
 
    ```json
    ResourceGroupName : ADF
    DataFactoryName   : incrementalloadingADF
    ActivityName      : LookupNewWaterMarkActivity
    PipelineRunId     : d4bf3ce2-5d60-43f3-9318-923155f61037
    PipelineName      : IncrementalCopyPipeline
    Input             : {source, dataset}
    Output            : {NewWatermarkvalue}
    LinkedServiceName :
    ActivityRunStart  : 9/14/2017 7:42:42 AM
    ActivityRunEnd    : 9/14/2017 7:42:50 AM
    DurationInMs      : 7777
    Status            : Succeeded
    Error             : {errorCode, message, failureType, target}
    
    ResourceGroupName : ADF
    DataFactoryName   : incrementalloadingADF
    ActivityName      : LookupOldWaterMarkActivity
    PipelineRunId     : d4bf3ce2-5d60-43f3-9318-923155f61037
    PipelineName      : IncrementalCopyPipeline
    Input             : {source, dataset}
    Output            : {TableName, WatermarkValue}
    LinkedServiceName :
    ActivityRunStart  : 9/14/2017 7:42:42 AM
    ActivityRunEnd    : 9/14/2017 7:43:07 AM
    DurationInMs      : 25437
    Status            : Succeeded
    Error             : {errorCode, message, failureType, target}
    
    ResourceGroupName : ADF
    DataFactoryName   : incrementalloadingADF
    ActivityName      : IncrementalCopyActivity
    PipelineRunId     : d4bf3ce2-5d60-43f3-9318-923155f61037
    PipelineName      : IncrementalCopyPipeline
    Input             : {source, sink}
    Output            : {dataRead, dataWritten, rowsCopied, copyDuration...}
    LinkedServiceName :
    ActivityRunStart  : 9/14/2017 7:43:10 AM
    ActivityRunEnd    : 9/14/2017 7:43:29 AM
    DurationInMs      : 19769
    Status            : Succeeded
    Error             : {errorCode, message, failureType, target}
    
    ResourceGroupName : ADF
    DataFactoryName   : incrementalloadingADF
    ActivityName      : StoredProceduretoWriteWatermarkActivity
    PipelineRunId     : d4bf3ce2-5d60-43f3-9318-923155f61037
    PipelineName      : IncrementalCopyPipeline
    Input             : {storedProcedureName, storedProcedureParameters}
    Output            : {}
    LinkedServiceName :
    ActivityRunStart  : 9/14/2017 7:43:32 AM
    ActivityRunEnd    : 9/14/2017 7:43:47 AM
    DurationInMs      : 14467
    Status            : Succeeded
    Error             : {errorCode, message, failureType, target}

    ```

## <a name="review-the-results"></a>Passer en revue les résultats.

1. Dans le stockage Blob Azure (magasin récepteur), vous devez vérifier que les données ont bien été copiées dans le fichier défini dans SinkDataset.  Dans le didacticiel actuel, le nom de fichier est `Incremental- d4bf3ce2-5d60-43f3-9318-923155f61037.txt`.  Ouvrez le fichier. Vous constatez alors que les enregistrements du fichier sont les mêmes que les données contenues dans la base de données Azure SQL Database.

    ```
    1,aaaa,2017-09-01 00:56:00.0000000
    2,bbbb,2017-09-02 05:23:00.0000000
    3,cccc,2017-09-03 02:36:00.0000000
    4,dddd,2017-09-04 03:21:00.0000000
    5,eeee,2017-09-05 08:06:00.0000000
    ``` 
2. Vérifiez la valeur la plus récente de `watermarktable` ; vous constatez que la valeur de limite a été mise à jour.

    ```sql
    Select * from watermarktable
    ```
    
    Voici l'exemple de sortie :
 
    TableName | WatermarkValue
    --------- | --------------
    data_source_table   2017-09-05  8:06:00.000

### <a name="insert-data-into-data-source-store-to-verify-delta-data-loading"></a>Insérer des données dans le magasin de la source de données pour vérifier le chargement des données delta

1. Insérez de nouvelles données dans la base de données Azure SQL Database (magasin de la source de données) :

    ```sql
    INSERT INTO data_source_table
    VALUES (6, 'newdata','9/6/2017 2:23:00 AM')
    
    INSERT INTO data_source_table
    VALUES (7, 'newdata','9/7/2017 9:01:00 AM')
    ``` 

    Les données mises à jour dans la base de données Azure SQL Database apparaissent comme suit :

    ```
    PersonID | Name | LastModifytime
    -------- | ---- | --------------
    1 | aaaa | 2017-09-01 00:56:00.000
    2 | bbbb | 2017-09-02 05:23:00.000
    3 | cccc | 2017-09-03 02:36:00.000
    4 | dddd | 2017-09-04 03:21:00.000
    5 | eeee | 2017-09-05 08:06:00.000
    6 | newdata | 2017-09-06 02:23:00.000
    7 | newdata | 2017-09-07 09:01:00.000
    ```
2. Exécutez à nouveau le pipeline **IncrementalCopyPipeline** en utilisant l’applet de commande **Invoke-AzureRmDataFactoryV2Pipeline**. Remplacez les espaces réservés par votre propre groupe de ressources et votre propre nom de fabrique de données.

    ```powershell
    $RunId = Invoke-AzureRmDataFactoryV2Pipeline -PipelineName "IncrementalCopyPipeline" -ResourceGroup "<your resource group>" -dataFactoryName "<your data factory name>"
    ```
3. Vérifiez l’état du pipeline en exécutant l’applet de commande **Get-AzureRmDataFactoryV2ActivityRun** jusqu’à ce que toutes les activités soient en cours d’exécution. Remplacez les espaces réservés des paramètres RunStartedAfter et RunStartedBefore par les dates qui vous conviennent.  Dans ce didacticiel, nous utilisons RunStartedAfter-« 2017/09/14 » - RunStartedBefore « 2017/09/15 »

    ```powershell
    Get-AzureRmDataFactoryV2ActivityRun -DataFactoryName $dataFactoryName -ResourceGroupName $resourceGroupName -PipelineRunId $RunId -RunStartedAfter "<start time>" -RunStartedBefore "<end time>"
    ```

    Voici l'exemple de sortie :
 
    ```json
    ResourceGroupName : ADF
    DataFactoryName   : incrementalloadingADF
    ActivityName      : LookupNewWaterMarkActivity
    PipelineRunId     : 2fc90ab8-d42c-4583-aa64-755dba9925d7
    PipelineName      : IncrementalCopyPipeline
    Input             : {source, dataset}
    Output            : {NewWatermarkvalue}
    LinkedServiceName :
    ActivityRunStart  : 9/14/2017 8:52:26 AM
    ActivityRunEnd    : 9/14/2017 8:52:58 AM
    DurationInMs      : 31758
    Status            : Succeeded
    Error             : {errorCode, message, failureType, target}
    
    ResourceGroupName : ADF
    DataFactoryName   : incrementalloadingADF
    ActivityName      : LookupOldWaterMarkActivity
    PipelineRunId     : 2fc90ab8-d42c-4583-aa64-755dba9925d7
    PipelineName      : IncrementalCopyPipeline
    Input             : {source, dataset}
    Output            : {TableName, WatermarkValue}
    LinkedServiceName :
    ActivityRunStart  : 9/14/2017 8:52:26 AM
    ActivityRunEnd    : 9/14/2017 8:52:52 AM
    DurationInMs      : 25497
    Status            : Succeeded
    Error             : {errorCode, message, failureType, target}
    
    ResourceGroupName : ADF
    DataFactoryName   : incrementalloadingADF
    ActivityName      : IncrementalCopyActivity
    PipelineRunId     : 2fc90ab8-d42c-4583-aa64-755dba9925d7
    PipelineName      : IncrementalCopyPipeline
    Input             : {source, sink}
    Output            : {dataRead, dataWritten, rowsCopied, copyDuration...}
    LinkedServiceName :
    ActivityRunStart  : 9/14/2017 8:53:00 AM
    ActivityRunEnd    : 9/14/2017 8:53:20 AM
    DurationInMs      : 20194
    Status            : Succeeded
    Error             : {errorCode, message, failureType, target}
    
    ResourceGroupName : ADF
    DataFactoryName   : incrementalloadingADF
    ActivityName      : StoredProceduretoWriteWatermarkActivity
    PipelineRunId     : 2fc90ab8-d42c-4583-aa64-755dba9925d7
    PipelineName      : IncrementalCopyPipeline
    Input             : {storedProcedureName, storedProcedureParameters}
    Output            : {}
    LinkedServiceName :
    ActivityRunStart  : 9/14/2017 8:53:23 AM
    ActivityRunEnd    : 9/14/2017 8:53:41 AM
    DurationInMs      : 18502
    Status            : Succeeded
    Error             : {errorCode, message, failureType, target}

    ```
4.  Un autre fichier doit avoir été créé dans le stockage Blob Azure. Dans ce didacticiel, le nom du nouveau fichier est `Incremental-2fc90ab8-d42c-4583-aa64-755dba9925d7.txt`.  Ouvrez ce fichier. Vous constatez alors qu’il contient des enregistrements à 2 lignes :
5.  Vérifiez la valeur la plus récente de `watermarktable` ; vous constatez que la valeur de limite a été de nouveau mise à jour.

    ```sql
    Select * from watermarktable
    ```
    Exemple de sortie : 
    
    TableName | WatermarkValue
    --------- | ---------------
    data_source_table | 2017-09-07 09:01:00.000

     
## <a name="next-steps"></a>Étapes suivantes
Dans ce didacticiel, vous avez effectué les étapes suivantes : 

> [!div class="checklist"]
> * Définition d’une colonne de **limite** et stockage de celle-ci dans la base de données Azure SQL Database.  
> * Créer une fabrique de données.
> * Création de services liés pour SQL Database et le stockage Blob. 
> * Création de jeux de données source et récepteur.
> * Créer un pipeline.
> * Exécuter le pipeline.
> * Surveiller l’exécution du pipeline. 

Passez au didacticiel suivant pour en savoir plus sur la transformation des données en utilisant un cluster Spark sur Azure :

> [!div class="nextstepaction"]
>[Transformer des données en utilisant un cluster Spark dans le cloud](tutorial-transform-data-spark-powershell.md)



