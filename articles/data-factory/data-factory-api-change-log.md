---
title: "aaaData Factory - journal de modification de l’API .NET | Documents Microsoft"
description: "Décrit les modifications avec rupture, les ajouts de fonctionnalités, des correctifs de bogues etc.... dans une version spécifique de l’API .NET pour hello Azure Data Factory."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 8208271b-7f4c-4214-b665-d2ff503c4470
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/05/2017
ms.author: spelluru
ms.openlocfilehash: 1d44b45c3dc8f9d483d1f1cef7068edacc610932
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-data-factory---net-api-change-log"></a>Azure Data Factory : Journal des modifications de l’API .NET
Cet article fournit des informations sur les modifications tooAzure SDK de fabrique de données dans une version spécifique. Vous trouverez le dernier package NuGet de hello pour Azure Data Factory [ici](https://www.nuget.org/packages/Microsoft.Azure.Management.DataFactories)

## <a name="version-4110"></a>Version 4.11.0
Ajouts de fonctionnalités :

* Hello des types de services liés suivants ont été ajoutés :
  * [OnPremisesMongoDbLinkedService](https://msdn.microsoft.com/library/mt765129.aspx)
  * [AmazonRedshiftLinkedService](https://msdn.microsoft.com/library/mt765121.aspx)
  * [AwsAccessKeyLinkedService](https://msdn.microsoft.com/library/mt765144.aspx)
* Hello, les types de jeu de données suivants ont été ajouté :
  * [MongoDbCollectionDataset](https://msdn.microsoft.com/library/mt765145.aspx)
  * [AmazonS3Dataset](https://msdn.microsoft.com/library/mt765112.aspx)
* suivant de Hello copie source types ont été ajoutés :
  * [MongoDbSource](https://msdn.microsoft.com/library/mt765123.aspx)

## <a name="version-4100"></a>Version 4.10.0
* Hello propriétés facultatives suivantes ont été ajoutée tooTextFormat :
  * [SkipLineCount](https://msdn.microsoft.com/library/azure/microsoft.azure.management.datafactories.models.textformat.skiplinecount.aspx)
  * [FirstRowAsHeader](https://msdn.microsoft.com/library/azure/microsoft.azure.management.datafactories.models.textformat.firstrowasheader.aspx)
  * [TreatEmptyAsNull](https://msdn.microsoft.com/library/azure/microsoft.azure.management.datafactories.models.textformat.treatemptyasnull.aspx)
* Hello des types de services liés suivants ont été ajoutés :
  * [OnPremisesCassandraLinkedService](https://msdn.microsoft.com/library/azure/microsoft.azure.management.datafactories.models.onpremisescassandralinkedservice.aspx)
  * [SalesforceLinkedService](https://msdn.microsoft.com/library/azure/microsoft.azure.management.datafactories.models.salesforcelinkedservice.aspx)
* Hello, les types de jeu de données suivants ont été ajouté :
  * [OnPremisesCassandraTableDataset](https://msdn.microsoft.com/library/azure/microsoft.azure.management.datafactories.models.onpremisescassandratabledataset.aspx)
* suivant de Hello copie source types ont été ajoutés :
  * [CassandraSource](https://msdn.microsoft.com/library/azure/microsoft.azure.management.datafactories.models.cassandrasource.aspx)
* Ajouter [WebServiceInputs](https://msdn.microsoft.com/library/azure/microsoft.azure.management.datafactories.models.azuremlbatchexecutionactivity.webserviceinputs.aspx) tooAzureMLBatchExecutionActivity de propriété
  * Activer le passage de plusieurs entrées de service web expérience d’Azure Machine Learning tooan

## <a name="version-491"></a>Version 4.9.1
### <a name="bug-fix"></a>Résolution de bogue
* L’authentification basée sur des API Web pour [WebLinkedService](https://msdn.microsoft.com/library/azure/microsoft.azure.management.datafactories.models.weblinkedservice.authenticationtype.aspx)est déconseillée.

## <a name="version-490"></a>Version 4.9.0
### <a name="feature-additions"></a>Ajouts de fonctionnalités
* Ajouter [EnableStaging](https://msdn.microsoft.com/library/mt767916.aspx) et [StagingSettings](https://msdn.microsoft.com/library/mt767918.aspx) tooCopyActivity de propriétés. Consultez [intermédiaire copie](data-factory-copy-activity-performance.md#staged-copy) pour plus d’informations sur la fonctionnalité de hello.

### <a name="bug-fix"></a>Résolution de bogue
* Introduction d’une surcharge de méthode [ActivityWindowOperationExtensions.List](https://msdn.microsoft.com/library/mt767915.aspx), qui nécessite une instance de [ActivityWindowsByActivityListParameters](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.activitywindowsbyactivitylistparameters.aspx).
* Marquage de [WriteBatchSize](https://msdn.microsoft.com/library/dn884293.aspx) et [WriteBatchTimeout](https://msdn.microsoft.com/library/dn884245.aspx) comme facultatifs dans CopySink.

## <a name="version-480"></a>Version 4.8.0
### <a name="feature-additions"></a>Ajouts de fonctionnalités
* Hello propriétés facultatives suivantes ont été ajoutée tooCopy activité tooenable réglage des performances de la copie de type :
  * [ParallelCopies](https://msdn.microsoft.com/library/mt767910.aspx)
  * [CloudDataMovementUnits](https://msdn.microsoft.com/library/mt767912.aspx)

## <a name="version-470"></a>Version 4.7.0
### <a name="feature-additions"></a>Ajouts de fonctionnalités
* Ajouter le nouveau type StorageFormat [OrcFormat](https://msdn.microsoft.com/library/mt723391.aspx) toocopy les fichiers de type ligne optimisé (ORC) sous forme de colonnes.
* Ajouter [AllowPolyBase](https://msdn.microsoft.com/library/mt723396.aspx) et PolyBaseSettings propriétés tooSqlDWSink.
  * Permet d’utiliser de hello de données de toocopy PolyBase dans SQL Data Warehouse.

## <a name="version-461"></a>Version 4.6.1
### <a name="bug-fixes"></a>Résolution des bogues
* Résout les requêtes HTTP pour les listes de fenêtres d’activité.
  * Supprime le nom de groupe de ressources hello et nom de fabrique de données hello à partir de la charge utile de demande hello.

## <a name="version-460"></a>Version 4.6.0
### <a name="feature-additions"></a>Ajouts de fonctionnalités
* Hello propriétés suivantes ont été ajoutées trop[PipelineProperties](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.pipelineproperties_properties.aspx):
  * [PipelineMode](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.pipelineproperties.pipelinemode.aspx)
  * [ExpirationTime](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.pipelineproperties.expirationtime.aspx)
  * [Groupes de données](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.pipelineproperties.datasets.aspx)
* Hello propriétés suivantes ont été ajoutées trop[PipelineRuntimeInfo](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.common.models.pipelineruntimeinfo.aspx):
  * [PipelineState](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.common.models.pipelineruntimeinfo.pipelinestate.aspx)
* Ajout de nouvelles [StorageFormat](https://msdn.microsoft.com/library/azure/microsoft.azure.management.datafactories.models.storageformat.aspx) type [JsonFormat](https://msdn.microsoft.com/library/azure/microsoft.azure.management.datafactories.models.jsonformat.aspx) toodefine de jeux de données dont les données sont au format JSON de type.

## <a name="version-450"></a>Version 4.5.0
### <a name="feature-additions"></a>Ajouts de fonctionnalités
* Ajout d’une [liste des opérations pour la fenêtre d’activité](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.activitywindowoperationsextensions.aspx).
  * Ajout de méthodes tooretrieve activité windows avec des filtres basés sur des types d’entités hello (autrement dit, les fabriques de données, des datasets, pipelines et activités).
* Hello des types de services liés suivants ont été ajoutés :
  * [ODataLinkedService](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.odatalinkedservice.aspx), [WebLinkedService](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.weblinkedservice.aspx)
* Hello, les types de jeu de données suivants ont été ajouté :
  * [ODataResourceDataset](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.odataresourcedataset.aspx), [WebTableDataset](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.webtabledataset.aspx)
* suivant de Hello copie source types ont été ajoutés :     
  * [WebSource](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.websource.aspx)

## <a name="version-440"></a>Version 4.4.0
### <a name="feature-additions"></a>Ajouts de fonctionnalités
* Hello type de service lié suivant a été ajouté en tant que sources de données et récepteurs pour les activités de copie :
  * [AzureStorageSasLinkedService](https://msdn.microsoft.com/library/azure/microsoft.azure.management.datafactories.models.azurestoragesaslinkedservice.aspx). Consultez la section [Service lié SAP Azure Storage](data-factory-azure-blob-connector.md#azure-storage-sas-linked-service) pour obtenir des informations conceptuelles et des exemples.

## <a name="version-430"></a>Version 4.3.0
### <a name="feature-additions"></a>Ajouts de fonctionnalités
* Hello suivants vous n avez encore les types de service lié été ajouté en tant que sources de données pour les activités de copie :
  * [HdfsLinkedService](https://msdn.microsoft.com/library/azure/microsoft.azure.management.datafactories.models.hdfslinkedservice.aspx). Consultez la section [Déplacer des données de HDFS à l’aide de Data Factory](data-factory-hdfs-connector.md) pour obtenir des informations conceptuelles et des exemples.
  * [OnPremisesOdbcLinkedService](https://msdn.microsoft.com/library/azure/microsoft.azure.management.datafactories.models.onpremisesodbclinkedservice.aspx). Consultez la section [Transfert de données à partir de magasins de données ODBC à l’aide d’Azure Data Factory](data-factory-odbc-connector.md) pour obtenir des informations conceptuelles et des exemples.

## <a name="version-420"></a>Version 4.2.0
### <a name="feature-additions"></a>Ajouts de fonctionnalités
* Hello, suivant le type d’activité a été ajoutée : [AzureMLUpdateResourceActivity](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuremlupdateresourceactivity.aspx). Pour plus d’informations sur l’activité de hello, consultez [les modèles de mise à jour Azure ML à l’aide de hello activité des ressources de mise à jour](data-factory-azure-ml-batch-execution-activity.md).
* Une nouvelle propriété facultatif [updateResourceEndpoint](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuremllinkedservice.updateresourceendpoint.aspx) a été ajouté toohello [AzureMLLinkedService classe](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuremllinkedservice.aspx).
* [LongRunningOperationInitialTimeout](https://msdn.microsoft.com/library/azure/microsoft.azure.management.datafactories.datafactorymanagementclient.longrunningoperationinitialtimeout.aspx) et [LongRunningOperationRetryTimeout](https://msdn.microsoft.com/library/azure/microsoft.azure.management.datafactories.datafactorymanagementclient.longrunningoperationretrytimeout.aspx) propriétés ont été ajoutées toohello [DataFactoryManagementClient](https://msdn.microsoft.com/library/azure/microsoft.azure.management.datafactories.datafactorymanagementclient.aspx) classe.
* Autoriser la configuration des délais d’attente hello pour le client appelle toohello service Data Factory.

## <a name="version-410"></a>Version 4.1.0
### <a name="feature-additions"></a>Ajouts de fonctionnalités
* Hello des types de services liés suivants ont été ajoutés :
  * [AzureDataLakeStoreLinkedService](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakestorelinkedservice.aspx)
  * [AzureDataLakeAnalyticsLinkedService](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakeanalyticslinkedservice.aspx)
* Hello, les types d’activité suivants ont été ajouté :
  * [DataLakeAnalyticsUSQLActivity](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.datalakeanalyticsusqlactivity.aspx)
* Hello, les types de jeu de données suivants ont été ajouté :
  * [AzureDataLakeStoreDataset](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakestoredataset.aspx)
* Hello les types source et le récepteur suivants pour l’activité de copie ont été ajoutées :
  * [AzureDataLakeStoreSource](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakestoresource.aspx)
  * [AzureDataLakeStoreSink](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakestoresink.aspx)

## <a name="version-401"></a>Version 4.0.1
### <a name="breaking-changes"></a>Dernières modifications
Hello classes suivantes ont été renommée. nouveaux noms de Hello ont les noms d’origine hello de classes avant de version 4.0.0.

| Nom dans 4.0.0 | Nom dans 4.0.1 |
|:--- |:--- |
| AzureSqlDataWarehouseDataset |[AzureSqlDataWarehouseTableDataset](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuresqldatawarehousetabledataset.aspx) |
| AzureSqlDataset |[AzureSqlTableDataset](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuresqltabledataset.aspx) |
| AzureDataset |[AzureTableDataset](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuretabledataset.aspx) |
| OracleDataset |[OracleTableDataset](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.oracletabledataset.aspx) |
| RelationalDataset |[RelationalTableDataset](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.relationaltabledataset.aspx) |
| SqlServerDataset |[SqlServerTableDataset](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.sqlservertabledataset.aspx) |

## <a name="version-400"></a>Version 4.0.0
### <a name="breaking-changes"></a>Dernières modifications
* Hello suivant classes/interfaces ont été renommée.

| Ancien nom | Nouveau nom |
|:--- |:--- |
| ITableOperations |[IDatasetOperations](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.idatasetoperations.aspx) |
| Table |[Dataset](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.dataset.aspx) |
| TableProperties |[DatasetProperties](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.datasetproperties.aspx) |
| TableTypeProprerties |[DatasetTypeProperties](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.datasettypeproperties.aspx) |
| TableCreateOrUpdateParameters |[DatasetCreateOrUpdateParameters](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.datasetcreateorupdateparameters.aspx) |
| TableCreateOrUpdateResponse |[DatasetCreateOrUpdateResponse](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.datasetcreateorupdateresponse.aspx) |
| TableGetResponse |[DatasetGetResponse](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.datasetgetresponse.aspx) |
| TableListResponse |[DatasetListResponse](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.datasetlistresponse.aspx) |
| CreateOrUpdateWithRawJsonContentParameters |[DatasetCreateOrUpdateWithRawJsonContentParameters](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.datasetcreateorupdatewithrawjsoncontentparameters.aspx) |

* Hello **liste** méthodes retournent des résultats paginés maintenant. Si la réponse de hello contient un vide **NextLink** propriété, hello client application a besoin de page suivante de toocontinue extraction hello jusqu'à ce que toutes les pages sont retournées.  Voici un exemple :

    ```csharp
    PipelineListResponse response = client.Pipelines.List("ResourceGroupName", "DataFactoryName");
    var pipelines = new List<Pipeline>(response.Pipelines);

    string nextLink = response.NextLink;
    while (!string.IsNullOrEmpty(nextLink))
    {
        PipelineListResponse nextResponse = client.Pipelines.ListNext(nextLink);
        pipelines.AddRange(nextResponse.Pipelines);

        nextLink = nextResponse.NextLink;
    }
    ```
* **Liste** pipeline API retourne uniquement hello résumé d’un pipeline au lieu de tous les détails. Par exemple, les activités d’un résumé de pipeline ne contiennent que le nom et le type.

### <a name="feature-additions"></a>Ajouts de fonctionnalités
* Hello [SqlDWSink](https://msdn.microsoft.com/library/azure/microsoft.azure.management.datafactories.models.sqldwsink.aspx) classe prend en charge deux nouvelles propriétés, **SliceIdentifierColumnName** et **SqlWriterCleanupScript**, toosupport idempotent copie tooAzure de données SQL Entrepôt. Consultez hello [Azure SQL Data Warehouse](data-factory-azure-sql-data-warehouse-connector.md) article pour plus d’informations sur ces propriétés.
* Nous prennent désormais en charge l’exécution de procédure stockée avec des sources de base de données SQL Azure et Azure SQL Data Warehouse dans le cadre de l’activité de copie de hello. Hello [SqlSource](https://msdn.microsoft.com/library/azure/microsoft.azure.management.datafactories.models.sqlsource.aspx) et [SqlDWSource](https://msdn.microsoft.com/library/azure/microsoft.azure.management.datafactories.models.sqldwsource.aspx) classes ont hello propriétés suivantes : **SqlReaderStoredProcedureName** et **StoredProcedureParameters** . Consultez hello [base de données SQL Azure](data-factory-azure-sql-connector.md#sqlsource) et [Azure SQL Data Warehouse](data-factory-azure-sql-data-warehouse-connector.md#sqldwsource) articles sur Azure.com pour plus d’informations sur ces propriétés.  
