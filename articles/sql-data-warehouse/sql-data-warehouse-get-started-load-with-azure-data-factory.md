---
redirect_url: /azure/sql-data-warehouse/sql-data-warehouse-load-with-data-factory
title: "Chargement de données Azure Data Factory | Microsoft Docs"
description: "Apprenez à charger des données avec Azure Data Factory"
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
ms.openlocfilehash: 0b01c77c916b616974545fc3da442e72e5336399
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="load-data-with-azure-data-factory"></a><span data-ttu-id="23abe-103">Téléchargement de données avec Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="23abe-103">Load Data with Azure Data Factory</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="23abe-104">Redgate</span><span class="sxs-lookup"><span data-stu-id="23abe-104">Redgate</span></span>](sql-data-warehouse-load-with-redgate.md)  
> * [<span data-ttu-id="23abe-105">Data Factory</span><span class="sxs-lookup"><span data-stu-id="23abe-105">Data Factory</span></span>](sql-data-warehouse-get-started-load-with-azure-data-factory.md)  
> * [<span data-ttu-id="23abe-106">PolyBase</span><span class="sxs-lookup"><span data-stu-id="23abe-106">PolyBase</span></span>](sql-data-warehouse-get-started-load-with-polybase.md)  
> * [<span data-ttu-id="23abe-107">BCP</span><span class="sxs-lookup"><span data-stu-id="23abe-107">BCP</span></span>](sql-data-warehouse-load-with-bcp.md)  
> 
> 

<span data-ttu-id="23abe-108">Ce didacticiel vous montre comment créer un pipeline dans Azure Data Factory pour déplacer des données des objets blobs Microsoft Azure Storage vers un entrepôt Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="23abe-108">This tutorial shows you how to create a pipeline in Azure Data Factory to move data from Azure Storage Blob to Azure SQL Data Warehouse.</span></span> <span data-ttu-id="23abe-109">Lors des opérations qui suivent, vous allez :</span><span class="sxs-lookup"><span data-stu-id="23abe-109">With the following steps you will:</span></span>

* <span data-ttu-id="23abe-110">Données d’exemple de configuration dans un objet blob Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="23abe-110">Set up sample data in an Azure Storage Blob.</span></span>
* <span data-ttu-id="23abe-111">Connectez des ressources à Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="23abe-111">Connect resources to Azure Data Factory.</span></span>
* <span data-ttu-id="23abe-112">Créer un pipeline pour déplacer des objets blobs de stockage vers SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="23abe-112">Create a pipeline to move data from Storage Blobs to SQL Data Warehouse.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Loading-Azure-SQL-Data-Warehouse-with-Azure-Data-Factory/player]
> 
> 

## <a name="before-you-begin"></a><span data-ttu-id="23abe-113">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="23abe-113">Before you begin</span></span>
<span data-ttu-id="23abe-114">Pour vous familiariser avec Azure Data Factory, consultez [Présentation d’Azure Data Factory][Introduction to Azure Data Factory].</span><span class="sxs-lookup"><span data-stu-id="23abe-114">To familiarize yourself with Azure Data Factory, see [Introduction to Azure Data Factory][Introduction to Azure Data Factory].</span></span>

### <a name="create-or-identify-resources"></a><span data-ttu-id="23abe-115">Créer ou identifier des ressources</span><span class="sxs-lookup"><span data-stu-id="23abe-115">Create or identify resources</span></span>
<span data-ttu-id="23abe-116">Avant de commencer ce didacticiel, vous devez disposer des ressources suivantes :</span><span class="sxs-lookup"><span data-stu-id="23abe-116">Before starting this tutorial, you need to have the following resources:</span></span>

* <span data-ttu-id="23abe-117">**Objet blob Azure Storage** : ce didacticiel utilise l’objet blob Azure Storage comme source de données pour le pipeline Azure Data Factory. Vous devez donc disposer d’un objet blob pour stocker les exemples de données.</span><span class="sxs-lookup"><span data-stu-id="23abe-117">**Azure Storage Blob**: This tutorial uses Azure Storage Blob as the data source for the Azure Data Factory pipeline, and so you need to have one available to store the sample data.</span></span> <span data-ttu-id="23abe-118">Si vous n’en avez pas, découvrez comment [créer un compte de stockage][Create a storage account].</span><span class="sxs-lookup"><span data-stu-id="23abe-118">If you don't have one already, learn how to [Create a storage account][Create a storage account].</span></span>
* <span data-ttu-id="23abe-119">**SQL Data Warehouse** : ce didacticiel déplace les données entre l’objet blob Azure Storage et l’entrepôt SQL Data Warehouse ; vous avez donc besoin de disposer d’un entrepôt de données en ligne contenant les exemples de données AdventureWorksDW.</span><span class="sxs-lookup"><span data-stu-id="23abe-119">**SQL Data Warehouse**: This tutorial moves the data from Azure Storage Blob to  SQL Data Warehouse and so need to have a data warehouse online that is loaded with the AdventureWorksDW sample data.</span></span> <span data-ttu-id="23abe-120">Si vous n’en avez pas, découvrez comment [approvisionner un entrepôt de données][Create a SQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="23abe-120">If you do not already have a data warehouse, learn how to [provision one][Create a SQL Data Warehouse].</span></span> <span data-ttu-id="23abe-121">Si vous disposez bien d’un entrepôt de données, mais que vous ne l’avez pas configuré avec les exemples de données, vous pouvez les [charger manuellement][Load sample data into SQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="23abe-121">If you have a data warehouse but didn't provision it with the sample data, you can [load it manually][Load sample data into SQL Data Warehouse].</span></span>
* <span data-ttu-id="23abe-122">**Azure Data Factory** : Azure Data Factory exécute la charge réelle, ce qui signifie que vous devez disposer d’une instance que vous utiliserez pour créer le pipeline de déplacement des données.</span><span class="sxs-lookup"><span data-stu-id="23abe-122">**Azure Data Factory**: Azure Data Factory completes the actual load and so you need to have one that you can use to build the data movement pipeline.</span></span> <span data-ttu-id="23abe-123">Si vous n’en possédez pas encore, apprenez à en créer une à l’étape 1 de la section [Didacticiel : Créer votre première fabrique de données Azure à l’aide du portail Azure][Get started with Azure Data Factory (Data Factory Editor)].</span><span class="sxs-lookup"><span data-stu-id="23abe-123">If you don't have one already, learn how to create one in Step 1 of [Get started with Azure Data Factory (Data Factory Editor)][Get started with Azure Data Factory (Data Factory Editor)].</span></span>
* <span data-ttu-id="23abe-124">**AZCopy**: vous avez besoin d’AZCopy pour copier les exemples de données de votre client local sur votre objet blob Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="23abe-124">**AZCopy**: You need AZCopy to copy the sample data from your local client to your Azure Storage Blob.</span></span> <span data-ttu-id="23abe-125">Pour obtenir des instructions d’installation, consultez la [documentation d’AZCopy][AZCopy documentation].</span><span class="sxs-lookup"><span data-stu-id="23abe-125">For install instructions, see the [AZCopy documentation][AZCopy documentation].</span></span>

## <a name="step-1-copy-sample-data-to-azure-storage-blob"></a><span data-ttu-id="23abe-126">Étape 1 : copier des exemples de données sur l’objet blob Azure Storage</span><span class="sxs-lookup"><span data-stu-id="23abe-126">Step 1: Copy sample data to Azure Storage Blob</span></span>
<span data-ttu-id="23abe-127">Une fois que tous les éléments sont prêts, vous pouvez copier les exemples de données sur votre objet blob Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="23abe-127">Once you have all the pieces ready, you are ready to copy sample data to your Azure Storage Blob.</span></span>

1. <span data-ttu-id="23abe-128">[Téléchargez les exemples de données][Download sample data].</span><span class="sxs-lookup"><span data-stu-id="23abe-128">[Download sample data][Download sample data].</span></span> <span data-ttu-id="23abe-129">Ces données ajoutent trois années de données de ventes à vos exemples de données AdventureWorksDW.</span><span class="sxs-lookup"><span data-stu-id="23abe-129">This data adds another three years of sales data to your AdventureWorksDW sample data.</span></span>
2. <span data-ttu-id="23abe-130">Utilisez cette commande AZCopy pour copier les trois années de données dans l’objet blob Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="23abe-130">Use this AZCopy command to copy the three years of data to your Azure Storage Blob.</span></span>
   
    ````
    AzCopy /Source:<Sample Data Location>  /Dest:https://<storage account>.blob.core.windows.net/<container name> /DestKey:<storage key> /Pattern:FactInternetSales.csv
    ````

## <a name="step-2-connect-resources-to-azure-data-factory"></a><span data-ttu-id="23abe-131">Étape 2 : connecter des ressources à Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="23abe-131">Step 2: Connect resources to Azure Data Factory</span></span>
<span data-ttu-id="23abe-132">Maintenant que les données sont en place, vous pouvez créer le pipeline Azure Data Factory pour déplacer les données entre le stockage d’objets blob Azure et l’entrepôt SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="23abe-132">Now that the data is in place we can create the Azure Data Factory pipeline to move the data from Azure blob storage into SQL Data Warehouse.</span></span>

<span data-ttu-id="23abe-133">Pour commencer, ouvrez le [portail Azure][Azure portal], puis sélectionnez votre fabrique de données dans le menu de gauche.</span><span class="sxs-lookup"><span data-stu-id="23abe-133">To get started, open the [Azure portal][Azure portal] and select your data factory from the left-hand menu.</span></span>

### <a name="step-21-create-linked-service"></a><span data-ttu-id="23abe-134">Étape 2.1 : créer un service lié</span><span class="sxs-lookup"><span data-stu-id="23abe-134">Step 2.1: Create Linked Service</span></span>
<span data-ttu-id="23abe-135">Liez votre compte de stockage Azure et SQL Data Warehouse à votre fabrique de données.</span><span class="sxs-lookup"><span data-stu-id="23abe-135">Link your Azure storage account and SQL Data Warehouse to your data factory.</span></span>  

1. <span data-ttu-id="23abe-136">Tout d’abord, commencez le processus d’inscription en cliquant sur la section « Services liés » de votre fabrique de données, puis sur « Nouveau magasin de données. »</span><span class="sxs-lookup"><span data-stu-id="23abe-136">First, begin the registration process by clicking the 'Linked Services' section of your data factory and then click 'New data store.'</span></span> <span data-ttu-id="23abe-137">Choisissez un nom sous lequel inscrire votre compte de stockage Azure, sélectionnez le stockage Azure en tant que type, puis saisissez votre nom de compte ainsi que votre clé de compte.</span><span class="sxs-lookup"><span data-stu-id="23abe-137">Choose a name to register your azure storage under, select Azure Storage as your type, and then enter your Account Name and Account Key.</span></span>
2. <span data-ttu-id="23abe-138">Pour enregistrer SQL Data Warehouse, accédez à la section « Créer et déployer », sélectionnez « Nouveau magasin de données », puis « Azure SQL Data Warehouse ».</span><span class="sxs-lookup"><span data-stu-id="23abe-138">To register SQL Data Warehouse navigate to the 'Author and Deploy' section, select 'New Data Store', and then 'Azure SQL Data Warehouse'.</span></span> <span data-ttu-id="23abe-139">Copiez et collez ce modèle, puis renseignez vos informations.</span><span class="sxs-lookup"><span data-stu-id="23abe-139">Copy and paste in this template, and then fill in your specific information.</span></span>
   
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

### <a name="step-22-define-the-dataset"></a><span data-ttu-id="23abe-140">Étape 2.2 : définir le jeu de données</span><span class="sxs-lookup"><span data-stu-id="23abe-140">Step 2.2: Define the dataset</span></span>
<span data-ttu-id="23abe-141">Après avoir créé les services liés, nous devrons définir les jeux de données.</span><span class="sxs-lookup"><span data-stu-id="23abe-141">After creating the linked services, we will have to define the data sets.</span></span>  <span data-ttu-id="23abe-142">Ici, cela signifie que nous devons définir la structure des données déplacées de votre espace de stockage vers votre entrepôt de données.</span><span class="sxs-lookup"><span data-stu-id="23abe-142">Here this means defining the structure of the data that is being moved from your storage to your data warehouse.</span></span>  <span data-ttu-id="23abe-143">Vous pouvez en savoir plus sur la création</span><span class="sxs-lookup"><span data-stu-id="23abe-143">You can read more about creating</span></span>

1. <span data-ttu-id="23abe-144">Lancez ce processus en accédant à la section « Créer et déployer » de votre fabrique de données.</span><span class="sxs-lookup"><span data-stu-id="23abe-144">Start this process by navigating to the 'Author and Deploy' section of your data factory.</span></span>
2. <span data-ttu-id="23abe-145">Cliquez sur « Nouveau dataset », puis sur « Stockage des objets blobs Azure » pour lier votre stockage à votre fabrique de données.</span><span class="sxs-lookup"><span data-stu-id="23abe-145">Click 'New dataset' and then 'Azure Blob storage' to link your storage to your data factory.</span></span>  <span data-ttu-id="23abe-146">Vous pouvez utiliser le script ci-dessous pour définir vos données dans le stockage des objets blobs Azure :</span><span class="sxs-lookup"><span data-stu-id="23abe-146">You can use the below script to define your data in Azure Blob storage:</span></span>
   
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
3. <span data-ttu-id="23abe-147">Maintenant, nous allons définir notre jeu de données pour SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="23abe-147">Now we define our dataset for SQL Data Warehouse.</span></span> <span data-ttu-id="23abe-148">Commencer de la même manière, en cliquant sur « Nouveau dataset », puis sur « Azure SQL Data Warehouse ».</span><span class="sxs-lookup"><span data-stu-id="23abe-148">We start in the same way, by clicking 'New dataset' and then 'Azure SQL Data Warehouse'.</span></span>
   
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

## <a name="step-3-create-and-run-your-pipeline"></a><span data-ttu-id="23abe-149">Étape 3 : créer et exécuter le pipeline</span><span class="sxs-lookup"><span data-stu-id="23abe-149">Step 3: Create and run your pipeline</span></span>
<span data-ttu-id="23abe-150">Enfin, nous allons configurer et exécuter le pipeline dans Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="23abe-150">Finally, we set up and run the pipeline in Azure Data Factory.</span></span>  <span data-ttu-id="23abe-151">Il s’agit de l’opération qui achève le déplacement effectif des données.</span><span class="sxs-lookup"><span data-stu-id="23abe-151">This is the operation that completes the actual data movement.</span></span>  <span data-ttu-id="23abe-152">Vous trouverez [ici][Move data to and from Azure SQL Data Warehouse using Azure Data Factory] une présentation complète des opérations que vous pouvez réaliser avec SQL Data Warehouse et Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="23abe-152">You can find a full view of the operations that you can complete with SQL Data Warehouse and Azure Data Factory [here][Move data to and from Azure SQL Data Warehouse using Azure Data Factory].</span></span>

<span data-ttu-id="23abe-153">Dans la section « Créer et déployer », cliquez sur « Autres commandes », puis sur « Nouveau Pipeline ».</span><span class="sxs-lookup"><span data-stu-id="23abe-153">In the 'Author and Deploy' section, click 'More Commands' and then 'New Pipeline'.</span></span>  <span data-ttu-id="23abe-154">Après avoir créé le pipeline, vous pouvez utiliser le code ci-dessous pour transférer les données vers votre entrepôt de données :</span><span class="sxs-lookup"><span data-stu-id="23abe-154">After you create the pipeline, you can use the below code to transfer the data to your data warehouse:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="23abe-155">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="23abe-155">Next steps</span></span>
<span data-ttu-id="23abe-156">Pour plus d’informations, consultez les articles suivants :</span><span class="sxs-lookup"><span data-stu-id="23abe-156">To learn more, start by viewing:</span></span>

* <span data-ttu-id="23abe-157">[Parcours d’apprentissage Azure Data Factory][Azure Data Factory learning path].</span><span class="sxs-lookup"><span data-stu-id="23abe-157">[Azure Data Factory learning path][Azure Data Factory learning path].</span></span>
* <span data-ttu-id="23abe-158">[Azure SQL Data Warehouse Connector][Azure SQL Data Warehouse Connector].</span><span class="sxs-lookup"><span data-stu-id="23abe-158">[Azure SQL Data Warehouse Connector][Azure SQL Data Warehouse Connector].</span></span> <span data-ttu-id="23abe-159">Il s’agit de la rubrique de référence pour l’utilisation d’Azure Data Factory avec Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="23abe-159">This is the core reference topic for using Azure Data Factory with Azure SQL Data Warehouse.</span></span>

<span data-ttu-id="23abe-160">Ces rubriques fournissent des informations détaillées sur Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="23abe-160">These topics provide detailed information about Azure Data Factory.</span></span> <span data-ttu-id="23abe-161">Elles décrivent la base de données SQL Azure et HDinsight, mais s’appliquent également à Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="23abe-161">They discuss Azure SQL Database or HDInsight, but the information also applies to Azure SQL Data Warehouse.</span></span>

* <span data-ttu-id="23abe-162">[Didacticiel : Créer votre première fabrique de données (vue d’ensemble)][Tutorial: Get started with Azure Data Factory] Ce didacticiel est consacré au traitement des données avec Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="23abe-162">[Tutorial: Get started with Azure Data Factory][Tutorial: Get started with Azure Data Factory] This is the core tutorial for processing data with Azure Data Factory.</span></span> <span data-ttu-id="23abe-163">Dans ce didacticiel, vous allez apprendre à créer votre premier pipeline qui fait appel à HDInsight pour transformer et analyser des journaux web tous les mois.</span><span class="sxs-lookup"><span data-stu-id="23abe-163">In this tutorial, you will build your first pipeline that uses HDInsight to transform and analyze web logs on a monthly basis.</span></span> <span data-ttu-id="23abe-164">Notez que ce didacticiel ne couvre aucune activité de copie.</span><span class="sxs-lookup"><span data-stu-id="23abe-164">Note, there is no copy activity in this tutorial.</span></span>
* <span data-ttu-id="23abe-165">[Didacticiel : Copie de données d’Azure Storage Blob vers une base de données Azure SQL Database][Tutorial: Copy data from Azure Storage Blob to Azure SQL Database].</span><span class="sxs-lookup"><span data-stu-id="23abe-165">[Tutorial: Copy data from Azure Storage Blob to Azure SQL Database][Tutorial: Copy data from Azure Storage Blob to Azure SQL Database].</span></span> <span data-ttu-id="23abe-166">Ce didacticiel crée un pipeline dans Azure Data Factory pour copier des données d’un objet blob Azure Storage dans une base de données SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="23abe-166">In this tutorial, you create a pipeline in Azure Data Factory to copy data from Azure Storage Blob to Azure SQL Database.</span></span>

<!--Image references-->

<!--Article references-->
[AZCopy documentation]: ../storage/storage-use-azcopy.md
[Azure SQL Data Warehouse Connector]: ../data-factory/data-factory-azure-sql-data-warehouse-connector.md
[BCP]: sql-data-warehouse-load-with-bcp.md
[Create a SQL Data Warehouse]: sql-data-warehouse-get-started-provision.md
[Create a storage account]: ../storage/storage-create-storage-account.md#create-a-storage-account
[Data Factory]: sql-data-warehouse-get-started-load-with-azure-data-factory.md
[Get started with Azure Data Factory (Data Factory Editor)]: ../data-factory/data-factory-build-your-first-pipeline-using-editor.md
[Introduction to Azure Data Factory]: ../data-factory/data-factory-introduction.md
[Load sample data into SQL Data Warehouse]: sql-data-warehouse-load-sample-databases.md
[Move data to and from Azure SQL Data Warehouse using Azure Data Factory]: ../data-factory/data-factory-azure-sql-data-warehouse-connector.md
[PolyBase]: sql-data-warehouse-get-started-load-with-polybase.md
[Tutorial: Copy data from Azure Storage Blob to Azure SQL Database]: ../data-factory/data-factory-copy-data-from-azure-blob-storage-to-sql-database.md
[Tutorial: Get started with Azure Data Factory]: ../data-factory/data-factory-build-your-first-pipeline.md

<!--MSDN references-->

<!--Other Web references-->
[Azure Data Factory learning path]: https://azure.microsoft.com/documentation/learning-paths/data-factory
[Azure portal]: https://portal.azure.com
[Download sample data]: https://migrhoststorage.blob.core.windows.net/adfsample/FactInternetSales.csv
