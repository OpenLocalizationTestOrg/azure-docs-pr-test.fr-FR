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
# <a name="load-data-with-azure-data-factory"></a><span data-ttu-id="2e6c9-103">Téléchargement de données avec Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="2e6c9-103">Load Data with Azure Data Factory</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="2e6c9-104">Redgate</span><span class="sxs-lookup"><span data-stu-id="2e6c9-104">Redgate</span></span>](sql-data-warehouse-load-with-redgate.md)  
> * [<span data-ttu-id="2e6c9-105">Data Factory</span><span class="sxs-lookup"><span data-stu-id="2e6c9-105">Data Factory</span></span>](sql-data-warehouse-get-started-load-with-azure-data-factory.md)  
> * [<span data-ttu-id="2e6c9-106">PolyBase</span><span class="sxs-lookup"><span data-stu-id="2e6c9-106">PolyBase</span></span>](sql-data-warehouse-get-started-load-with-polybase.md)  
> * [<span data-ttu-id="2e6c9-107">BCP</span><span class="sxs-lookup"><span data-stu-id="2e6c9-107">BCP</span></span>](sql-data-warehouse-load-with-bcp.md)  
> 
> 

<span data-ttu-id="2e6c9-108">Ce didacticiel vous montre comment toocreate un pipeline de données Azure Data Factory toomove tooAzure de l’objet Blob de stockage Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="2e6c9-108">This tutorial shows you how toocreate a pipeline in Azure Data Factory toomove data from Azure Storage Blob tooAzure SQL Data Warehouse.</span></span> <span data-ttu-id="2e6c9-109">Avec hello, vous allez comme suit :</span><span class="sxs-lookup"><span data-stu-id="2e6c9-109">With hello following steps you will:</span></span>

* <span data-ttu-id="2e6c9-110">Données d’exemple de configuration dans un objet blob Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="2e6c9-110">Set up sample data in an Azure Storage Blob.</span></span>
* <span data-ttu-id="2e6c9-111">Connecter des ressources tooAzure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="2e6c9-111">Connect resources tooAzure Data Factory.</span></span>
* <span data-ttu-id="2e6c9-112">Créer une pipeline des données de toomove à partir d’objets BLOB de stockage tooSQL l’entrepôt de données.</span><span class="sxs-lookup"><span data-stu-id="2e6c9-112">Create a pipeline toomove data from Storage Blobs tooSQL Data Warehouse.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Loading-Azure-SQL-Data-Warehouse-with-Azure-Data-Factory/player]
> 
> 

## <a name="before-you-begin"></a><span data-ttu-id="2e6c9-113">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="2e6c9-113">Before you begin</span></span>
<span data-ttu-id="2e6c9-114">toofamiliarize vous-même avec Azure Data Factory, consultez [Introduction tooAzure Data Factory][Introduction tooAzure Data Factory].</span><span class="sxs-lookup"><span data-stu-id="2e6c9-114">toofamiliarize yourself with Azure Data Factory, see [Introduction tooAzure Data Factory][Introduction tooAzure Data Factory].</span></span>

### <a name="create-or-identify-resources"></a><span data-ttu-id="2e6c9-115">Créer ou identifier des ressources</span><span class="sxs-lookup"><span data-stu-id="2e6c9-115">Create or identify resources</span></span>
<span data-ttu-id="2e6c9-116">Avant de commencer ce didacticiel, vous devez hello toohave suivant des ressources :</span><span class="sxs-lookup"><span data-stu-id="2e6c9-116">Before starting this tutorial, you need toohave hello following resources:</span></span>

* <span data-ttu-id="2e6c9-117">**Objet Blob de stockage Azure**: ce didacticiel utilise l’objet Blob de stockage Azure en tant que source de données hello pour le pipeline d’Azure Data Factory hello et par conséquent, vous devez toohave une toostore disponible hello exemples de données.</span><span class="sxs-lookup"><span data-stu-id="2e6c9-117">**Azure Storage Blob**: This tutorial uses Azure Storage Blob as hello data source for hello Azure Data Factory pipeline, and so you need toohave one available toostore hello sample data.</span></span> <span data-ttu-id="2e6c9-118">Si vous n’avez pas déjà, découvrez comment trop[créer un compte de stockage][Create a storage account].</span><span class="sxs-lookup"><span data-stu-id="2e6c9-118">If you don't have one already, learn how too[Create a storage account][Create a storage account].</span></span>
* <span data-ttu-id="2e6c9-119">**SQL Data Warehouse**: ces didacticiel se déplace hello données à partir de l’objet Blob de stockage Azure trop SQL Data Warehouse et donc ont besoin toohave en ligne un entrepôt de données qui est chargé avec hello exemples de données AdventureWorksDW.</span><span class="sxs-lookup"><span data-stu-id="2e6c9-119">**SQL Data Warehouse**: This tutorial moves hello data from Azure Storage Blob too SQL Data Warehouse and so need toohave a data warehouse online that is loaded with hello AdventureWorksDW sample data.</span></span> <span data-ttu-id="2e6c9-120">Si vous n’avez pas déjà d’un entrepôt de données, découvrez comment trop[configurer un][Create a SQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="2e6c9-120">If you do not already have a data warehouse, learn how too[provision one][Create a SQL Data Warehouse].</span></span> <span data-ttu-id="2e6c9-121">Si vous disposez d’un entrepôt de données mais que vous n’avez pas mettre en service avec les données d’exemple hello, vous pouvez [charger manuellement][Load sample data into SQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="2e6c9-121">If you have a data warehouse but didn't provision it with hello sample data, you can [load it manually][Load sample data into SQL Data Warehouse].</span></span>
* <span data-ttu-id="2e6c9-122">**Azure Data Factory**: Azure Data Factory se termine la charge réelle de hello et par conséquent, vous devez toohave une que vous pouvez utiliser le pipeline de déplacement des données toobuild hello.</span><span class="sxs-lookup"><span data-stu-id="2e6c9-122">**Azure Data Factory**: Azure Data Factory completes hello actual load and so you need toohave one that you can use toobuild hello data movement pipeline.</span></span> <span data-ttu-id="2e6c9-123">Si vous n’avez pas déjà, découvrez comment toocreate un à l’étape 1 de [prise en main Azure Data Factory (éditeur Data Factory)][Get started with Azure Data Factory (Data Factory Editor)].</span><span class="sxs-lookup"><span data-stu-id="2e6c9-123">If you don't have one already, learn how toocreate one in Step 1 of [Get started with Azure Data Factory (Data Factory Editor)][Get started with Azure Data Factory (Data Factory Editor)].</span></span>
* <span data-ttu-id="2e6c9-124">**AZCopy**: vous devez AZCopy toocopy hello exemples de données à partir de votre objet Blob de stockage Azure de tooyour client local.</span><span class="sxs-lookup"><span data-stu-id="2e6c9-124">**AZCopy**: You need AZCopy toocopy hello sample data from your local client tooyour Azure Storage Blob.</span></span> <span data-ttu-id="2e6c9-125">Pour obtenir des instructions d’installation, consultez hello [AZCopy documentation][AZCopy documentation].</span><span class="sxs-lookup"><span data-stu-id="2e6c9-125">For install instructions, see hello [AZCopy documentation][AZCopy documentation].</span></span>

## <a name="step-1-copy-sample-data-tooazure-storage-blob"></a><span data-ttu-id="2e6c9-126">Étape 1 : Copie exemple tooAzure de données objet Blob de stockage</span><span class="sxs-lookup"><span data-stu-id="2e6c9-126">Step 1: Copy sample data tooAzure Storage Blob</span></span>
<span data-ttu-id="2e6c9-127">Une fois que toutes les parties hello prêt, vous êtes prêt toocopy exemple tooyour de données objet Blob de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="2e6c9-127">Once you have all hello pieces ready, you are ready toocopy sample data tooyour Azure Storage Blob.</span></span>

1. <span data-ttu-id="2e6c9-128">[Téléchargez les exemples de données][Download sample data].</span><span class="sxs-lookup"><span data-stu-id="2e6c9-128">[Download sample data][Download sample data].</span></span> <span data-ttu-id="2e6c9-129">Ces données ajoute trois ans de données de ventes tooyour exemples de données AdventureWorksDW.</span><span class="sxs-lookup"><span data-stu-id="2e6c9-129">This data adds another three years of sales data tooyour AdventureWorksDW sample data.</span></span>
2. <span data-ttu-id="2e6c9-130">Utilisez cette commande de toocopy AZCopy hello trois années de tooyour de données objet Blob de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="2e6c9-130">Use this AZCopy command toocopy hello three years of data tooyour Azure Storage Blob.</span></span>
   
    ````
    AzCopy /Source:<Sample Data Location>  /Dest:https://<storage account>.blob.core.windows.net/<container name> /DestKey:<storage key> /Pattern:FactInternetSales.csv
    ````

## <a name="step-2-connect-resources-tooazure-data-factory"></a><span data-ttu-id="2e6c9-131">Étape 2 : Connecter des ressources tooAzure Data Factory</span><span class="sxs-lookup"><span data-stu-id="2e6c9-131">Step 2: Connect resources tooAzure Data Factory</span></span>
<span data-ttu-id="2e6c9-132">Maintenant que les données de salutation sont en place, nous pouvons créer les données de salutation hello Azure Data Factory pipeline toomove depuis le stockage blob Azure dans SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="2e6c9-132">Now that hello data is in place we can create hello Azure Data Factory pipeline toomove hello data from Azure blob storage into SQL Data Warehouse.</span></span>

<span data-ttu-id="2e6c9-133">tooget démarré, ouvrez hello [portail Azure] [ Azure portal] et sélectionnez votre data factory hello menu de gauche.</span><span class="sxs-lookup"><span data-stu-id="2e6c9-133">tooget started, open hello [Azure portal][Azure portal] and select your data factory from hello left-hand menu.</span></span>

### <a name="step-21-create-linked-service"></a><span data-ttu-id="2e6c9-134">Étape 2.1 : créer un service lié</span><span class="sxs-lookup"><span data-stu-id="2e6c9-134">Step 2.1: Create Linked Service</span></span>
<span data-ttu-id="2e6c9-135">Lier votre compte de stockage Azure et de la fabrique de données SQL Data Warehouse tooyour.</span><span class="sxs-lookup"><span data-stu-id="2e6c9-135">Link your Azure storage account and SQL Data Warehouse tooyour data factory.</span></span>  

1. <span data-ttu-id="2e6c9-136">Tout d’abord, commencer le processus d’inscription de hello en cliquant sur la section « Services liés » de hello votre fabrique de données et puis cliquez sur « Nouveau magasin de données. »</span><span class="sxs-lookup"><span data-stu-id="2e6c9-136">First, begin hello registration process by clicking hello 'Linked Services' section of your data factory and then click 'New data store.'</span></span> <span data-ttu-id="2e6c9-137">Choisissez un tooregister nom votre stockage azure sous, sélectionnez Azure Storage, comme votre type, puis entrez votre nom de compte et votre clé de compte.</span><span class="sxs-lookup"><span data-stu-id="2e6c9-137">Choose a name tooregister your azure storage under, select Azure Storage as your type, and then enter your Account Name and Account Key.</span></span>
2. <span data-ttu-id="2e6c9-138">tooregister SQL Data Warehouse accédez toohello les section « Auteur et déployer », sélectionnez « Nouveau magasin de données », puis sur Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="2e6c9-138">tooregister SQL Data Warehouse navigate toohello 'Author and Deploy' section, select 'New Data Store', and then 'Azure SQL Data Warehouse'.</span></span> <span data-ttu-id="2e6c9-139">Copiez et collez ce modèle, puis renseignez vos informations.</span><span class="sxs-lookup"><span data-stu-id="2e6c9-139">Copy and paste in this template, and then fill in your specific information.</span></span>
   
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

### <a name="step-22-define-hello-dataset"></a><span data-ttu-id="2e6c9-140">Étape 2.2 : Définir le jeu de données hello</span><span class="sxs-lookup"><span data-stu-id="2e6c9-140">Step 2.2: Define hello dataset</span></span>
<span data-ttu-id="2e6c9-141">Après que la création d’hello des services liés, il nous faudra toodefine hello des ensembles de données.</span><span class="sxs-lookup"><span data-stu-id="2e6c9-141">After creating hello linked services, we will have toodefine hello data sets.</span></span>  <span data-ttu-id="2e6c9-142">Ici, cela signifie que la définition de structure hello de données hello sont déplacées à partir de votre entrepôt de données de stockage tooyour.</span><span class="sxs-lookup"><span data-stu-id="2e6c9-142">Here this means defining hello structure of hello data that is being moved from your storage tooyour data warehouse.</span></span>  <span data-ttu-id="2e6c9-143">Vous pouvez en savoir plus sur la création</span><span class="sxs-lookup"><span data-stu-id="2e6c9-143">You can read more about creating</span></span>

1. <span data-ttu-id="2e6c9-144">Démarrer ce processus en naviguant dans la section « Auteur et déployer » de toohello votre fabrique de données.</span><span class="sxs-lookup"><span data-stu-id="2e6c9-144">Start this process by navigating toohello 'Author and Deploy' section of your data factory.</span></span>
2. <span data-ttu-id="2e6c9-145">Cliquez sur 'Nouveau jeu de données', 'Le stockage Blob Azure' toolink votre fabrique de données de stockage tooyour.</span><span class="sxs-lookup"><span data-stu-id="2e6c9-145">Click 'New dataset' and then 'Azure Blob storage' toolink your storage tooyour data factory.</span></span>  <span data-ttu-id="2e6c9-146">Vous pouvez utiliser hello ci-dessous script toodefine vos données dans le stockage d’objets Blob Azure :</span><span class="sxs-lookup"><span data-stu-id="2e6c9-146">You can use hello below script toodefine your data in Azure Blob storage:</span></span>
   
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
3. <span data-ttu-id="2e6c9-147">Maintenant, nous allons définir notre jeu de données pour SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="2e6c9-147">Now we define our dataset for SQL Data Warehouse.</span></span> <span data-ttu-id="2e6c9-148">Nous allons commencer Bonjour même manière, en cliquant sur « Nouveau jeu de données », puis sur Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="2e6c9-148">We start in hello same way, by clicking 'New dataset' and then 'Azure SQL Data Warehouse'.</span></span>
   
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

## <a name="step-3-create-and-run-your-pipeline"></a><span data-ttu-id="2e6c9-149">Étape 3 : créer et exécuter le pipeline</span><span class="sxs-lookup"><span data-stu-id="2e6c9-149">Step 3: Create and run your pipeline</span></span>
<span data-ttu-id="2e6c9-150">Enfin, nous configurer et exécuter le pipeline de hello dans Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="2e6c9-150">Finally, we set up and run hello pipeline in Azure Data Factory.</span></span>  <span data-ttu-id="2e6c9-151">Il s’agit d’opération hello qui se termine le déplacement des données réelles de hello.</span><span class="sxs-lookup"><span data-stu-id="2e6c9-151">This is hello operation that completes hello actual data movement.</span></span>  <span data-ttu-id="2e6c9-152">Vous trouverez une vue complète des opérations hello que vous pouvez réaliser avec SQL Data Warehouse et Azure Data Factory [ici][Move data tooand from Azure SQL Data Warehouse using Azure Data Factory].</span><span class="sxs-lookup"><span data-stu-id="2e6c9-152">You can find a full view of hello operations that you can complete with SQL Data Warehouse and Azure Data Factory [here][Move data tooand from Azure SQL Data Warehouse using Azure Data Factory].</span></span>

<span data-ttu-id="2e6c9-153">Bonjour section « Auteur et déployer », cliquez sur 'Plus les commandes', « Nouveau Pipeline ».</span><span class="sxs-lookup"><span data-stu-id="2e6c9-153">In hello 'Author and Deploy' section, click 'More Commands' and then 'New Pipeline'.</span></span>  <span data-ttu-id="2e6c9-154">Après avoir créé le pipeline de hello, vous pouvez utiliser hello ci-dessous code tootransfer hello données tooyour data warehouse :</span><span class="sxs-lookup"><span data-stu-id="2e6c9-154">After you create hello pipeline, you can use hello below code tootransfer hello data tooyour data warehouse:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="2e6c9-155">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="2e6c9-155">Next steps</span></span>
<span data-ttu-id="2e6c9-156">toolearn plus, commencez par l’affichage :</span><span class="sxs-lookup"><span data-stu-id="2e6c9-156">toolearn more, start by viewing:</span></span>

* <span data-ttu-id="2e6c9-157">[Parcours d’apprentissage Azure Data Factory][Azure Data Factory learning path].</span><span class="sxs-lookup"><span data-stu-id="2e6c9-157">[Azure Data Factory learning path][Azure Data Factory learning path].</span></span>
* <span data-ttu-id="2e6c9-158">[Azure SQL Data Warehouse Connector][Azure SQL Data Warehouse Connector].</span><span class="sxs-lookup"><span data-stu-id="2e6c9-158">[Azure SQL Data Warehouse Connector][Azure SQL Data Warehouse Connector].</span></span> <span data-ttu-id="2e6c9-159">Il s’agit de rubrique de référence de base hello pour l’utilisation d’Azure Data Factory et Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="2e6c9-159">This is hello core reference topic for using Azure Data Factory with Azure SQL Data Warehouse.</span></span>

<span data-ttu-id="2e6c9-160">Ces rubriques fournissent des informations détaillées sur Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="2e6c9-160">These topics provide detailed information about Azure Data Factory.</span></span> <span data-ttu-id="2e6c9-161">Elles présentent de base de données SQL Azure ou HDInsight, mais les informations de hello tooAzure SQL Data Warehouse s’appliquent également.</span><span class="sxs-lookup"><span data-stu-id="2e6c9-161">They discuss Azure SQL Database or HDInsight, but hello information also applies tooAzure SQL Data Warehouse.</span></span>

* <span data-ttu-id="2e6c9-162">[Didacticiel : Prise en main Azure Data Factory] [ Tutorial: Get started with Azure Data Factory] didacticiel de base hello pour le traitement des données avec Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="2e6c9-162">[Tutorial: Get started with Azure Data Factory][Tutorial: Get started with Azure Data Factory] This is hello core tutorial for processing data with Azure Data Factory.</span></span> <span data-ttu-id="2e6c9-163">Dans ce didacticiel, vous créer votre premier pipeline qui utilise HDInsight tootransform et analyser les journaux web sur une base mensuelle.</span><span class="sxs-lookup"><span data-stu-id="2e6c9-163">In this tutorial, you will build your first pipeline that uses HDInsight tootransform and analyze web logs on a monthly basis.</span></span> <span data-ttu-id="2e6c9-164">Notez que ce didacticiel ne couvre aucune activité de copie.</span><span class="sxs-lookup"><span data-stu-id="2e6c9-164">Note, there is no copy activity in this tutorial.</span></span>
* <span data-ttu-id="2e6c9-165">[Didacticiel : Copier des données à partir de l’objet Blob de stockage Azure tooAzure base de données SQL][Tutorial: Copy data from Azure Storage Blob tooAzure SQL Database].</span><span class="sxs-lookup"><span data-stu-id="2e6c9-165">[Tutorial: Copy data from Azure Storage Blob tooAzure SQL Database][Tutorial: Copy data from Azure Storage Blob tooAzure SQL Database].</span></span> <span data-ttu-id="2e6c9-166">Dans ce didacticiel, vous créez un pipeline de données de toocopy Azure Data Factory à partir de l’objet Blob de stockage Azure tooAzure base de données SQL.</span><span class="sxs-lookup"><span data-stu-id="2e6c9-166">In this tutorial, you create a pipeline in Azure Data Factory toocopy data from Azure Storage Blob tooAzure SQL Database.</span></span>

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
