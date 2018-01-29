---
title: "Copier de façon incrémentielle des données en utilisant Change Tracking et Azure Data Factory | Microsoft Docs"
description: "Dans ce didacticiel, vous allez créer un pipeline Azure Data Factory qui copie de façon incrémentielle des données delta de plusieurs tables d’une base de données SQL Server locale dans une base de données Azure SQL. "
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: spelluru
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 01/22/2018
ms.author: jingwang
ms.openlocfilehash: d2cf578d6328e6e53d1081b9ab4de3ad262390df
ms.sourcegitcommit: 9cc3d9b9c36e4c973dd9c9028361af1ec5d29910
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/23/2018
---
# <a name="incrementally-load-data-from-azure-sql-database-to-azure-blob-storage-using-change-tracking-information"></a>Charger de façon incrémentielle des données d’Azure SQL Database dans le stockage Blob Azure à l’aide de la technologie de suivi des modifications 
Dans ce didacticiel, vous allez créer une fabrique de données Azure avec un pipeline qui charge des données delta basées sur des informations de **suivi des modifications** dans la base de données Azure SQL source vers un stockage Blob Azure.  

Dans ce didacticiel, vous allez effectuer les étapes suivantes :

> [!div class="checklist"]
> * Préparer le magasin de données source
> * Créer une fabrique de données.
> * créez des services liés. 
> * Créez des jeux de données source, récepteur et de suivi des modifications.
> * Créer, exécuter et surveiller le pipeline de copie complète
> * Ajouter ou mettre à jour des données dans la table source
> * Créer, exécuter et surveiller le pipeline de copie incrémentielle

> [!NOTE]
> Cet article s’applique à la version 2 de Data Factory, actuellement en préversion. Si vous utilisez la version 1 du service Data Factory, qui est généralement disponible, consultez la [documentation Data Factory version 1](v1/data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).

## <a name="overview"></a>Vue d’ensemble
Dans une solution d’intégration de données, le chargement incrémentiel de données après des chargements de données initiaux est un scénario largement utilisé. Dans certains cas, les données modifiées pendant une période dans votre magasin de données source peuvent être facilement découpées (par exemple, LastModifyTime, CreationTime). Dans certains cas, il n’existe pas de manière explicite pour identifier les données delta depuis le dernier traitement des données. La technologie Change Tracking prise en charge par les magasins de données tels qu’Azure SQL Database et SQL Server peut être utilisée pour identifier les données delta.  Ce didacticiel explique comment utiliser Azure Data Factory version 2 pour utiliser la technologie Change Tracking SQL afin de charger de façon incrémentielle des données delta d’Azure SQL Database dans le stockage blob Azure.  Pour des informations plus concrètes sur la technologie Change Tracking SQL, consultez [Change Tracking dans SQL Server](/sql/relational-databases/track-changes/about-change-tracking-sql-server). 

## <a name="end-to-end-workflow"></a>Workflow de bout en bout
Voici les étapes de workflow de bout en bout classiques pour charger de façon incrémentielle des données à l’aide de la technologie Change Tracking.

> [!NOTE]
> Azure SQL Database et SQL Server prennent en charge la technologie Change Tracking. Ce didacticiel utilise la Azure SQL Database comme magasin de données source. Vous pouvez également utiliser un SQL Server local. 

1. **Chargement initial de données d’historique** (exécuter une fois) :
    1. Activez la technologie Change Tracking dans la base de données Azure SQL source.
    2. Obtenez la valeur initiale de SYS_CHANGE_VERSION dans la base de données Azure SQL comme ligne de base pour la capture des données modifiées.
    3. Chargez les données complètes de la base de données Azure SQL vers un compte de stockage blob Azure. 
2. **Chargement incrémentiel de données delta selon une planification** (exécuter périodiquement après le chargement initial des données) :
    1. Obtenez les valeurs SYS_CHANGE_VERSION anciennes et nouvelles.
    3. Chargez les données delta en associant les clés primaires des lignes modifiées (entre deux valeurs SYS_CHANGE_VERSION) de **sys.change_tracking_tables** avec des données dans la **table source**, puis déplacez les données delta vers la destination.
    4. Mettez à jour SYS_CHANGE_VERSION pour le chargement delta suivant.

## <a name="high-level-solution"></a>Solution générale
Dans ce didacticiel, vous créez deux pipelines qui effectuent les deux opérations suivantes :  

1. **Chargement initial :** vous créez un pipeline avec une activité de copie qui copie l’ensemble des données du magasin de données source (Azure SQL Database) dans le magasin de données de destination (stockage blob Azure).

    ![Chargement complet des données](media/tutorial-incremental-copy-change-tracking-feature-powershell/full-load-flow-diagram.png)
1.  **Chargement incrémentiel :** vous créez un pipeline avec les activités suivantes, et vous l’exécutez régulièrement. 
    1. Créez **deux activités de recherche** pour obtenir les valeurs SYS_CHANGE_VERSION anciennes et nouvelles dans Azure SQL Database et les transmettre à l’activité de copie.
    2. Créez **une activité de copie** pour copier les données insérées/mises à jour/supprimées entre deux valeurs SYS_CHANGE_VERSION d’Azure SQL Database dans un stockage blob Azure.
    3. Créez **une activité de procédure stockée** pour mettre à jour la valeur de SYS_CHANGE_VERSION pour la prochaine exécution du pipeline.

    ![Diagramme de flux de chargement incrémentiel](media/tutorial-incremental-copy-change-tracking-feature-powershell/incremental-load-flow-diagram.png)


Si vous n’avez pas d’abonnement Azure, créez un compte [gratuit](https://azure.microsoft.com/free/) avant de commencer.

## <a name="prerequisites"></a>configuration requise
* Azure PowerShell. Installez les modules Azure PowerShell les plus récents en suivant les instructions décrites dans [Comment installer et configurer Azure PowerShell](/powershell/azure/install-azurerm-ps).
* **Base de données SQL Azure**. Vous utilisez la base de données comme magasin de données **sources**. Si vous n’avez pas de base de données Azure SQL Database, consultez l’article [Création d’une base de données Azure SQL](../sql-database/sql-database-get-started-portal.md) pour savoir comme en créer une.
* **Compte Stockage Azure**. Vous utilisez le stockage Blob comme magasin de données **récepteur**. Si vous n’avez pas de compte de stockage Azure, consultez l’article [Créer un compte de stockage](../storage/common/storage-create-storage-account.md#create-a-storage-account) pour savoir comment en créer un. Créez un conteneur sous le nom **adftutorial**. 

### <a name="create-a-data-source-table-in-your-azure-sql-database"></a>Créer une table de source de données dans votre base de données Azure SQL Database
1. Lancez **SQL Server Management Studio** et connectez-vous à votre serveur Azure SQL. 
2. Dans l’**Explorateur de serveurs**, cliquez avec le bouton droit sur votre **base de données** et choisissez **Nouvelle requête**.
3. Exécutez la commande SQL suivante sur votre base de données Azure SQL Database pour créer une table sous le nom `data_source_table` comme magasin de la source de données.  
    
    ```sql
    create table data_source_table
    (
        PersonID int NOT NULL,
        Name varchar(255),
        Age int
        PRIMARY KEY (PersonID)
    );

    INSERT INTO data_source_table
        (PersonID, Name, Age)
    VALUES
        (1, 'aaaa', 21),
        (2, 'bbbb', 24),
        (3, 'cccc', 20),
        (4, 'dddd', 26),
        (5, 'eeee', 22);

    ```
4. Activez le mécanisme **Change Tracking** sur votre base de données et la table source (data_source_table) en exécutant la requête SQL suivante : 

    > [!NOTE]
    > - Remplacez &lt;le nom de votre base de données&gt; par le nom de votre base de données Azure SQL contenant la data_source_table. 
    > - Dans cet exemple, les données modifiées sont conservées pendant deux jours. Si vous chargez les données modifiées tous les trois jours ou plus, certaines données modifiées ne sont pas incluses.  Vous devez remplacer la valeur de CHANGE_RETENTION par un plus grand nombre. Assurez-vous également que votre période pour charger les données modifiées est de moins de deux jours. Pour plus d’informations, consultez [Activer le suivi des modifications pour une base de données](/sql/relational-databases/track-changes/enable-and-disable-change-tracking-sql-server#enable-change-tracking-for-a-database)
 
    ```sql
    ALTER DATABASE <your database name>
    SET CHANGE_TRACKING = ON  
    (CHANGE_RETENTION = 2 DAYS, AUTO_CLEANUP = ON)  
  
    ALTER TABLE data_source_table
    ENABLE CHANGE_TRACKING  
    WITH (TRACK_COLUMNS_UPDATED = ON)
    ```
5. Créez une nouvelle table et stockez la ChangeTracking_version avec une valeur par défaut en exécutant la requête suivante : 

    ```sql
    create table table_store_ChangeTracking_version
    (
        TableName varchar(255),
        SYS_CHANGE_VERSION BIGINT,
    );

    DECLARE @ChangeTracking_version BIGINT
    SET @ChangeTracking_version = CHANGE_TRACKING_CURRENT_VERSION();  

    INSERT INTO table_store_ChangeTracking_version
    VALUES ('data_source_table', @ChangeTracking_version)
    ```
    
    > [!NOTE]
    > Si les données ne sont pas modifiées une fois que vous avez activé le suivi des modifications pour SQL Database, la valeur de la version de suivi des modifications est 0.
6. Exécutez la requête suivante pour créer une procédure stockée dans votre base de données Azure SQL. Le pipeline appelle cette procédure stockée pour mettre à jour la version de suivi des modifications dans la table que vous avez créée à l’étape précédente. 

    ```sql
    CREATE PROCEDURE Update_ChangeTracking_Version @CurrentTrackingVersion BIGINT, @TableName varchar(50)
    AS
    
    BEGIN
    
        UPDATE table_store_ChangeTracking_version
        SET [SYS_CHANGE_VERSION] = @CurrentTrackingVersion
    WHERE [TableName] = @TableName
    
    END    
    ```

### <a name="azure-powershell"></a>Azure PowerShell
Installez les modules Azure PowerShell les plus récents en suivant les instructions décrites dans [Comment installer et configurer Azure PowerShell](/powershell/azure/install-azurerm-ps).

## <a name="create-a-data-factory"></a>Créer une fabrique de données
1. Définissez une variable pour le nom du groupe de ressources que vous utiliserez ultérieurement dans les commandes PowerShell. Copiez le texte de commande suivant dans PowerShell, spécifiez un nom pour le [groupe de ressources Azure](../azure-resource-manager/resource-group-overview.md) entre des guillemets doubles, puis exécutez la commande. Par exemple : `"adfrg"`. 
   
     ```powershell
    $resourceGroupName = "ADFTutorialResourceGroup";
    ```

    Si le groupe de ressources existe déjà, vous pouvez ne pas le remplacer. Affectez une valeur différente à la variable `$resourceGroupName` et exécutez à nouveau la commande
2. Définissez une variable pour l’emplacement de la fabrique de données : 

    ```powershell
    $location = "East US"
    ```
3. Pour créer le groupe de ressources Azure, exécutez la commande suivante : 

    ```powershell
    New-AzureRmResourceGroup $resourceGroupName $location
    ``` 
    Si le groupe de ressources existe déjà, vous pouvez ne pas le remplacer. Affectez une valeur différente à la variable `$resourceGroupName` et exécutez à nouveau la commande. 
3. Définissez une variable pour le nom de la fabrique de données. 

    > [!IMPORTANT]
    >  Mettez à jour le nom de la fabrique de données afin qu’il soit globalement unique.  

    ```powershell
    $dataFactoryName = "IncCopyChgTrackingDF";
    ```
5. Pour créer la fabrique de données, exécutez l’applet de commande **Set-AzureRmDataFactoryV2** suivante : 
    
    ```powershell       
    Set-AzureRmDataFactoryV2 -ResourceGroupName $resourceGroupName -Location $location -Name $dataFactoryName 
    ```

Notez les points suivants :

* Le nom de la fabrique de données Azure doit être un nom global unique. Si vous recevez l’erreur suivante, changez le nom, puis réessayez.

    ```
    The specified Data Factory name 'ADFIncCopyChangeTrackingTestFactory' is already in use. Data Factory names must be globally unique.
    ```
* Pour créer des instances de fabrique de données, le compte d’utilisateur que vous utilisez pour vous connecter à Azure doit être un membre des rôles **contributeur** ou **propriétaire**, ou un **administrateur** de l’abonnement Azure.
* À l’heure actuelle, Data Factory version 2 vous permet de créer des fabriques de données uniquement dans les régions Est des États-Unis, Est des États-Unis 2 et Europe de l’Ouest. Les magasins de données (Stockage Azure, Azure SQL Database, etc.) et les services de calcul (HDInsight, etc.) utilisés par la fabrique de données peuvent se trouver dans d’autres régions.


## <a name="create-linked-services"></a>Créez des services liés
Vous allez créer des services liés dans une fabrique de données pour lier vos magasins de données et vos services de calcul à la fabrique de données. Dans cette section, vous allez créer des services liés à votre compte de stockage Azure et à la base de données Azure SQL Database. 

### <a name="create-azure-storage-linked-service"></a>Créer un service lié Stockage Azure.
Dans cette étape, vous liez votre compte Stockage Azure à la fabrique de données.

1. Créez un fichier JSON sous le nom **AzureStorageLinkedService.json** dans le dossier **C:\ADFTutorials\IncCopyChangeTrackingTutorial** avec le contenu suivant : (créez le dossier s’il n’existe pas déjà.). Remplacez `<accountName>`, `<accountKey>` par le nom et la clé de votre compte de stockage Azure avant d’enregistrer le fichier.

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
2. Dans **Azure PowerShell**, basculez vers le dossier **C:\ADFTutorials\IncCopyChgTrackingTutorial**.
3. Exécutez l’applet de commande **Set-AzureRmDataFactoryV2LinkedService** pour créer le service lié **AzureStorageLinkedService**. Dans l’exemple suivant, vous passez les valeurs des paramètres **ResourceGroupName** et **DataFactoryName**. 

    ```powershell
    Set-AzureRmDataFactoryV2LinkedService -DataFactoryName $dataFactoryName -ResourceGroupName $resourceGroupName -Name "AzureStorageLinkedService" -File ".\AzureStorageLinkedService.json"
    ```

    Voici l'exemple de sortie :

    ```json
    LinkedServiceName : AzureStorageLinkedService
    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : IncCopyChgTrackingDF
    Properties        : Microsoft.Azure.Management.DataFactory.Models.AzureStorageLinkedService
    ```

### <a name="create-azure-sql-database-linked-service"></a>Créez le service lié Azure SQL Database.
Dans cette étape, vous liez votre base de données Azure SQL à la fabrique de données.

1. Créez un fichier JSON sous le nom **AzureSQLDatabaseLinkedService.json** dans le dossier **C:\ADFTutorials\IncCopyChangeTrackingTutorial** avec le contenu suivant : Remplacez **&lt;server&gt; &lt;database name&gt;, &lt;user id&gt; et &lt;password&gt;** par le nom de votre serveur Azure SQL, le nom de votre base de données, ID utilisateur et mot de passe avant d’enregistrer le fichier. 

    ```json
    {
        "name": "AzureSQLDatabaseLinkedService",
        "properties": {
            "type": "AzureSqlDatabase",
            "typeProperties": {
                "connectionString": {
                    "value": "Server = tcp:<server>.database.windows.net,1433;Initial Catalog=<database name>; Persist Security Info=False; User ID=<user name>; Password=<password>; MultipleActiveResultSets = False; Encrypt = True; TrustServerCertificate = False; Connection Timeout = 30;",
                    "type": "SecureString"
                }
            }
        }
    }
    ```
2. Dans **Azure PowerShell**, exécutez l’applet de commande **Set-AzureRmDataFactoryV2LinkedService** pour créer le service lié : **AzureSQLDatabaseLinkedService**. 

    ```powershell
    Set-AzureRmDataFactoryV2LinkedService -DataFactoryName $dataFactoryName -ResourceGroupName $resourceGroupName -Name "AzureSQLDatabaseLinkedService" -File ".\AzureSQLDatabaseLinkedService.json"
    ```

    Voici l'exemple de sortie :

    ```json
    LinkedServiceName : AzureSQLDatabaseLinkedService
    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : IncCopyChgTrackingDF
    Properties        : Microsoft.Azure.Management.DataFactory.Models.AzureSqlDatabaseLinkedService
    ```

## <a name="create-datasets"></a>Créez les jeux de données
Dans cette étape, vous créez des jeux de données pour représenter la source de données et la destination de données. et l’emplacement pour stocker SYS_CHANGE_VERSION.

### <a name="create-a-source-dataset"></a>Créer un jeu de données source
Dans cette étape, vous créez un jeu de données pour représenter les données source. 

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

2.  Exécutez l’applet de commande Set-AzureRmDataFactoryV2Dataset pour créer le jeu de données SourceDataset.
    
    ```powershell
    Set-AzureRmDataFactoryV2Dataset -DataFactoryName $dataFactoryName -ResourceGroupName $resourceGroupName -Name "SourceDataset" -File ".\SourceDataset.json"
    ```

    Voici l’exemple de sortie de l’applet de commande :
    
    ```json
    DatasetName       : SourceDataset
    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : IncCopyChgTrackingDF
    Structure         :
    Properties        : Microsoft.Azure.Management.DataFactory.Models.AzureSqlTableDataset
    ```

### <a name="create-a-sink-dataset"></a>Créer un jeu de données récepteur
Dans cette étape, vous créez un jeu de données pour représenter les données copiées à partir du magasin de données source. 

1. Créez un fichier JSON sous le nom SinkDataset.json dans le même dossier avec le contenu suivant : 

    ```json
    {
        "name": "SinkDataset",
        "properties": {
            "type": "AzureBlob",
            "typeProperties": {
                "folderPath": "adftutorial/incchgtracking",
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

    Vous créez le conteneur adftutorial dans votre stockage blob Azure dans le cadre des prérequis. Créez le conteneur s’il n’existe pas (ou) attribuez-lui le nom d’un conteneur existant. Dans ce didacticiel, le nom du fichier de sortie est généré dynamiquement en utilisant l’expression : @CONCAT('Incremental-', pipeline().RunId, '.txt').
2.  Exécutez l’applet de commande Set-AzureRmDataFactoryV2Dataset pour créer le jeu de données SinkDataset.
    
    ```powershell
    Set-AzureRmDataFactoryV2Dataset -DataFactoryName $dataFactoryName -ResourceGroupName $resourceGroupName -Name "SinkDataset" -File ".\SinkDataset.json"
    ```

    Voici l’exemple de sortie de l’applet de commande :
    
    ```json
    DatasetName       : SinkDataset
    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : IncCopyChgTrackingDF
    Structure         :
    Properties        : Microsoft.Azure.Management.DataFactory.Models.AzureBlobDataset
    ```

### <a name="create-a-change-tracking-dataset"></a>Créer un jeu de données de suivi des modifications
Dans cette étape, vous créez un jeu de données pour stocker la version de suivi des modifications.  

1. Créez un fichier JSON sous le nom ChangeTrackingDataset.json dans le même dossier avec le contenu suivant : 

    ```json
    {
        "name": " ChangeTrackingDataset",
        "properties": {
            "type": "AzureSqlTable",
            "typeProperties": {
                "tableName": "table_store_ChangeTracking_version"
            },
            "linkedServiceName": {
                "referenceName": "AzureSQLDatabaseLinkedService",
                "type": "LinkedServiceReference"
            }
        }
    }
    ```

    Vous créez la table table_store_ChangeTracking_version dans le cadre des prérequis.
2.  Exécutez l’applet de commande Set-AzureRmDataFactoryV2Dataset pour créer le jeu de données WatermarkDataset.
    
    ```powershell
    Set-AzureRmDataFactoryV2Dataset -DataFactoryName $dataFactoryName -ResourceGroupName $resourceGroupName -Name "ChangeTrackingDataset" -File ".\ChangeTrackingDataset.json"
    ```

    Voici l’exemple de sortie de l’applet de commande :
    
    ```json
    DatasetName       : ChangeTrackingDataset
    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : IncCopyChgTrackingDF
    Structure         :
    Properties        : Microsoft.Azure.Management.DataFactory.Models.AzureSqlTableDataset
    ```

## <a name="create-a-pipeline-for-the-full-copy"></a>Créer un pipeline pour la copie complète
Dans cette étape, vous créez un pipeline avec une activité de copie qui copie l’ensemble des données du magasin de données source (Azure SQL Database) dans le magasin de données de destination (stockage Blob Azure).

1. Créez un fichier JSON sous le nom FullCopyPipeline.json dans le même dossier avec le contenu suivant : 

    ```json
    {
        "name": "FullCopyPipeline",
        "properties": {
            "activities": [{
                "name": "FullCopyActivity",
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "SqlSource"
                    },
                    "sink": {
                        "type": "BlobSink"
                    }
                },
    
                "inputs": [{
                    "referenceName": "SourceDataset",
                    "type": "DatasetReference"
                }],
                "outputs": [{
                    "referenceName": "SinkDataset",
                    "type": "DatasetReference"
                }]
            }]
        }
    }
    ```
2. Exécutez l’applet de commande Set-AzureRmDataFactoryV2Pipeline pour créer le pipeline : FullCopyPipeline.
    
   ```powershell
    Set-AzureRmDataFactoryV2Pipeline -DataFactoryName $dataFactoryName -ResourceGroupName $resourceGroupName -Name "FullCopyPipeline" -File ".\FullCopyPipeline.json"
   ``` 

   Voici l'exemple de sortie : 

   ```json
    PipelineName      : FullCopyPipeline
    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : IncCopyChgTrackingDF
    Activities        : {FullCopyActivity}
    Parameters        :
   ```
 
### <a name="run-the-full-copy-pipeline"></a>Exécuter le pipeline de copie complète
Exécutez le pipeline **FullCopyPipeline** en utilisant l’applet de commande **Invoke-AzureRmDataFactoryV2Pipeline**. 

```powershell
Invoke-AzureRmDataFactoryV2Pipeline -PipelineName "FullCopyPipeline" -ResourceGroup $resourceGroupName -dataFactoryName $dataFactoryName        
``` 

### <a name="monitor-the-full-copy-pipeline"></a>Surveiller le pipeline de copie complète

1. Connectez-vous au [portail Azure](https://portal.azure.com).
2. Cliquez sur **Plus de services**, effectuez une recherche avec le mot clé `data factories`, puis sélectionnez **Fabriques de données**. 

    ![Menu Fabriques de données](media\tutorial-incremental-copy-change-tracking-feature-powershell\monitor-data-factories-menu-1.png)
3. Recherchez **votre fabrique de données** dans la liste des fabriques de données et sélectionnez-la pour ouvrir la page de la fabrique de données. 

    ![Rechercher votre fabrique de données](media\tutorial-incremental-copy-change-tracking-feature-powershell\monitor-search-data-factory-2.png)
4. Sur la page Fabrique de données, cliquez sur la vignette **Surveiller et gérer**. 

    ![Vignette Surveiller et gérer](media\tutorial-incremental-copy-change-tracking-feature-powershell\monitor-monitor-manage-tile-3.png)    
5. L’**application d’intégration des données** démarre dans un onglet séparé. Vous pouvez voir toutes les **exécutions de pipeline** et leurs états. Notez que dans l’exemple suivant, l’état d’exécution de pipeline est **Réussite**. Vous pouvez vérifier les paramètres transmis au pipeline en cliquant sur le lien dans la colonne **Paramètres**. Si une erreur s’est produite, vous voyez un lien dans la colonne **Erreur**. Cliquez sur le lien dans la colonne **Actions**. 

    ![Exécutions de pipeline](media\tutorial-incremental-copy-change-tracking-feature-powershell\monitor-pipeline-runs-4.png)    
6. Lorsque vous cliquez sur le lien dans la colonne **Actions**, la page suivante affiche toutes les **exécutions d’activité** du pipeline. 

    ![Exécutions d’activités](media\tutorial-incremental-copy-change-tracking-feature-powershell\monitor-activity-runs-5.png)
7. Pour revenir à la vue **Exécutions de pipeline**, cliquez sur **Pipelines** comme illustré dans l’image. 


### <a name="review-the-results"></a>Passer en revue les résultats.
Vous voyez un fichier nommé `incremental-<GUID>.txt` dans le dossier `incchgtracking` du conteneur `adftutorial`. 

![Fichier de sortie d’une copie complète](media\tutorial-incremental-copy-change-tracking-feature-powershell\full-copy-output-file.png)

Le fichier doit contenir les données de la base de données Azure SQL :

```
1,aaaa,21
2,bbbb,24
3,cccc,20
4,dddd,26
5,eeee,22
```

## <a name="add-more-data-to-the-source-table"></a>Ajouter plus de données à la table source

Exécutez la requête suivante par rapport à la base de données Azure SQL pour ajouter une ligne et mettre à jour une ligne. 

```sql
INSERT INTO data_source_table
(PersonID, Name, Age)
VALUES
(6, 'new','50');


UPDATE data_source_table
SET [Age] = '10', [name]='update' where [PersonID] = 1

``` 

## <a name="create-a-pipeline-for-the-delta-copy"></a>Créer un pipeline pour la copie delta
Dans cette étape, vous créez un pipeline avec les activités suivantes, et vous l’exécutez régulièrement. Les **activités de recherche** obtiennent les valeurs SYS_CHANGE_VERSION anciennes et nouvelles dans Azure SQL Database et les transmettent à l’activité de copie. L’**activité de copie** copie les données insérées/mises à jour/supprimées entre deux valeurs SYS_CHANGE_VERSION d’Azure SQL Database dans un stockage blob Azure. L’**activité de procédure stockée** met à jour la valeur de SYS_CHANGE_VERSION pour la prochaine exécution du pipeline.

1. Créez un fichier JSON sous le nom IncrementalCopyPipeline.json dans le même dossier avec le contenu suivant : 

    ```json
    {
            "name": "IncrementalCopyPipeline",
            "properties": {
                "activities": [
                {
                        "name": "LookupLastChangeTrackingVersionActivity",
                        "type": "Lookup",
                        "typeProperties": {
                        "source": {
                            "type": "SqlSource",
                            "sqlReaderQuery": "select * from table_store_ChangeTracking_version"
                            },
        
                            "dataset": {
                            "referenceName": "ChangeTrackingDataset",
                            "type": "DatasetReference"
                            }
                        }
                    },
                    {
                        "name": "LookupCurrentChangeTrackingVersionActivity",
                        "type": "Lookup",
                        "typeProperties": {
                            "source": {
                                "type": "SqlSource",
                                "sqlReaderQuery": "SELECT CHANGE_TRACKING_CURRENT_VERSION() as CurrentChangeTrackingVersion"
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
                                "sqlReaderQuery": "select data_source_table.PersonID,data_source_table.Name,data_source_table.Age, CT.SYS_CHANGE_VERSION, SYS_CHANGE_OPERATION from data_source_table RIGHT OUTER JOIN CHANGETABLE(CHANGES data_source_table, @{activity('LookupLastChangeTrackingVersionActivity').output.firstRow.SYS_CHANGE_VERSION}) as CT on data_source_table.PersonID = CT.PersonID where CT.SYS_CHANGE_VERSION <= @{activity('LookupCurrentChangeTrackingVersionActivity').output.firstRow.CurrentChangeTrackingVersion}"
                            },
                            "sink": {
                                "type": "BlobSink"
                            }
                        },
                        "dependsOn": [
                            {
                                "activity": "LookupLastChangeTrackingVersionActivity",
                                "dependencyConditions": [
                                    "Succeeded"
                                ]
                            },
                            {
                                "activity": "LookupCurrentChangeTrackingVersionActivity",
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
                        "name": "StoredProceduretoUpdateChangeTrackingActivity",
                        "type": "SqlServerStoredProcedure",
                        "typeProperties": {
    
                            "storedProcedureName": "Update_ChangeTracking_Version",
                            "storedProcedureParameters": {
                            "CurrentTrackingVersion": {"value": "@{activity('LookupCurrentChangeTrackingVersionActivity').output.firstRow.CurrentChangeTrackingVersion}", "type": "INT64" },
                                "TableName":  { "value":"@{activity('LookupLastChangeTrackingVersionActivity').output.firstRow.TableName}", "type":"String"}
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
                ]
        
            }
    }
    
    ```
2. Exécutez l’applet de commande Set-AzureRmDataFactoryV2Pipeline pour créer le pipeline : FullCopyPipeline.
    
   ```powershell
    Set-AzureRmDataFactoryV2Pipeline -DataFactoryName $dataFactoryName -ResourceGroupName $resourceGroupName -Name "IncrementalCopyPipeline" -File ".\IncrementalCopyPipeline.json"
   ``` 

   Voici l'exemple de sortie : 

   ```json
    PipelineName      : IncrementalCopyPipeline
    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : IncCopyChgTrackingDF
    Activities        : {LookupLastChangeTrackingVersionActivity, LookupCurrentChangeTrackingVersionActivity, IncrementalCopyActivity, StoredProceduretoUpdateChangeTrackingActivity}
    Parameters        :
   ```

### <a name="run-the-incremental-copy-pipeline"></a>Exécuter le pipeline de copie incrémentielle
Exécutez le pipeline **IncrementalCopyPipeline** en utilisant l’applet de commande **Invoke-AzureRmDataFactoryV2Pipeline**. 

```powershell
Invoke-AzureRmDataFactoryV2Pipeline -PipelineName "IncrementalCopyPipeline" -ResourceGroup $resourceGroupName -dataFactoryName $dataFactoryName     
``` 


### <a name="monitor-the-incremental-copy-pipeline"></a>Surveiller le pipeline de copie incrémentielle
1. Dans l’**Application d’intégration de données**, actualisez la vue **Exécutions de pipeline**. Vérifiez que IncrementalCopyPipeline apparaît dans la liste. Cliquez sur le lien dans la colonne **Actions**.  

    ![Exécutions de pipeline](media\tutorial-incremental-copy-change-tracking-feature-powershell\monitor-pipeline-runs-6.png)    
2. Lorsque vous cliquez sur le lien dans la colonne **Actions**, la page suivante affiche toutes les **exécutions d’activité** du pipeline. 

    ![Exécutions d’activités](media\tutorial-incremental-copy-change-tracking-feature-powershell\monitor-activity-runs-7.png)
3. Pour revenir à la vue **Exécutions de pipeline**, cliquez sur **Pipelines** comme illustré dans l’image. 

### <a name="review-the-results"></a>Passer en revue les résultats.
Vous voyez le second fichier dans le dossier `incchgtracking` du conteneur `adftutorial`. 

![Fichier de sortie de la copie incrémentielle](media\tutorial-incremental-copy-change-tracking-feature-powershell\incremental-copy-output-file.png)

Le fichier ne doit contenir que les données delta de la base de données Azure SQL. L’enregistrement avec `U` correspond à la ligne mise à jour dans la base de données et `I` à la ligne ajoutée. 

```
1,update,10,2,U
6,new,50,1,I
```
Les trois premières colonnes correspondent aux données modifiées de data_source_table. Les deux dernières colonnes correspondent aux métadonnées de la table système de suivi des modifications. La quatrième colonne correspond à SYS_CHANGE_VERSION de chaque ligne modifiée. La cinquième colonne correspond à l’opération : U = mise à jour, I = insertion.  Pour plus d’informations sur le suivi des modifications, consultez [CHANGETABLE](/sql/relational-databases/system-functions/changetable-transact-sql). 

```
==================================================================
PersonID Name    Age    SYS_CHANGE_VERSION    SYS_CHANGE_OPERATION
==================================================================
1        update  10     2                     U
6        new     50     1                     I
```

    
## <a name="next-steps"></a>étapes suivantes
Passez au didacticiel suivant pour en savoir plus sur la transformation des données en utilisant un cluster Spark sur Azure :

> [!div class="nextstepaction"]
>[Transformer des données en utilisant un cluster Spark dans le cloud](tutorial-transform-data-spark-powershell.md)



