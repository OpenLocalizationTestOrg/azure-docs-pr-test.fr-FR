---
title: "aaaUpload grandes quantités de données dans Data Lake Store à l’aide de méthodes hors connexion | Documents Microsoft"
description: "Hello d’utilisation toocopy données de l’outil AdlCopy depuis le stockage Azure BLOB tooData Lake Store"
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 45321f6a-179f-4ee4-b8aa-efa7745b8eb6
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: 42ef75142a26ebfab05d89614782a54c244c4bcb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-azure-importexport-service-for-offline-copy-of-data-toodata-lake-store"></a><span data-ttu-id="ff8c3-103">Utiliser le service d’importation/exportation Azure hello pour une copie hors connexion tooData Lake du magasin de données</span><span class="sxs-lookup"><span data-stu-id="ff8c3-103">Use hello Azure Import/Export service for offline copy of data tooData Lake Store</span></span>
<span data-ttu-id="ff8c3-104">Dans cet article, vous allez apprendre comment les données volumineuses toocopy définit (> 200 Go) dans un Azure Data Lake Store à l’aide des méthodes de copie en mode hors connexion, comme hello [service Azure Import/Export](../storage/common/storage-import-export-service.md).</span><span class="sxs-lookup"><span data-stu-id="ff8c3-104">In this article, you'll learn how toocopy huge data sets (>200 GB) into an Azure Data Lake Store by using offline copy methods, like hello [Azure Import/Export service](../storage/common/storage-import-export-service.md).</span></span> <span data-ttu-id="ff8c3-105">Plus précisément, fichier hello utilisé comme un exemple dans cet article est 339,420,860,416 octets, ou environ 319 Go sur le disque.</span><span class="sxs-lookup"><span data-stu-id="ff8c3-105">Specifically, hello file used as an example in this article is 339,420,860,416 bytes, or about 319 GB on disk.</span></span> <span data-ttu-id="ff8c3-106">Appelons ce fichier 319GB.tsv.</span><span class="sxs-lookup"><span data-stu-id="ff8c3-106">Let's call this file 319GB.tsv.</span></span>

<span data-ttu-id="ff8c3-107">Hello service Azure Import/Export vous permet de tootransfer de grandes quantités de données plus en toute sécurité tooAzure stockage d’objets Blob par disque dur de livraison lecteurs tooan centre de données Azure.</span><span class="sxs-lookup"><span data-stu-id="ff8c3-107">hello Azure Import/Export service helps you tootransfer large amounts of data more securely tooAzure Blob storage by shipping hard disk drives tooan Azure datacenter.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ff8c3-108">Composants requis</span><span class="sxs-lookup"><span data-stu-id="ff8c3-108">Prerequisites</span></span>
<span data-ttu-id="ff8c3-109">Avant de commencer, vous devez disposer de hello :</span><span class="sxs-lookup"><span data-stu-id="ff8c3-109">Before you begin, you must have hello following:</span></span>

* <span data-ttu-id="ff8c3-110">**Un abonnement Azure**.</span><span class="sxs-lookup"><span data-stu-id="ff8c3-110">**An Azure subscription**.</span></span> <span data-ttu-id="ff8c3-111">Consultez [Obtenir une version d'évaluation gratuite d'Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ff8c3-111">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="ff8c3-112">**Un compte de stockage Azure**.</span><span class="sxs-lookup"><span data-stu-id="ff8c3-112">**An Azure storage account**.</span></span>
* <span data-ttu-id="ff8c3-113">**Un compte Azure Data Lake Store**.</span><span class="sxs-lookup"><span data-stu-id="ff8c3-113">**An Azure Data Lake Store account**.</span></span> <span data-ttu-id="ff8c3-114">Pour obtenir des instructions sur la façon de voir d’un seul, toocreate [prise en main Azure Data Lake Store](data-lake-store-get-started-portal.md)</span><span class="sxs-lookup"><span data-stu-id="ff8c3-114">For instructions on how toocreate one, see [Get started with Azure Data Lake Store](data-lake-store-get-started-portal.md)</span></span>

## <a name="preparing-hello-data"></a><span data-ttu-id="ff8c3-115">Préparation des données hello</span><span class="sxs-lookup"><span data-stu-id="ff8c3-115">Preparing hello data</span></span>
<span data-ttu-id="ff8c3-116">Avant d’utiliser le service d’importation/exportation hello, toobe de fichier saut hello données transférées **dans les copies de moins de 200 Go** taille.</span><span class="sxs-lookup"><span data-stu-id="ff8c3-116">Before using hello Import/Export service, break hello data file toobe transferred **into copies that are less than 200 GB** in size.</span></span> <span data-ttu-id="ff8c3-117">outil d’importation Hello ne fonctionne pas avec les fichiers de plus de 200 Go.</span><span class="sxs-lookup"><span data-stu-id="ff8c3-117">hello import tool does not work with files greater than 200 GB.</span></span> <span data-ttu-id="ff8c3-118">Dans ce didacticiel, nous fractionnez le fichier en hello en segments de 100 Go.</span><span class="sxs-lookup"><span data-stu-id="ff8c3-118">In this tutorial, we split hello file into chunks of 100 GB each.</span></span> <span data-ttu-id="ff8c3-119">Pour ce faire, utilisez [Cygwin](https://cygwin.com/install.html).</span><span class="sxs-lookup"><span data-stu-id="ff8c3-119">You can do this by using [Cygwin](https://cygwin.com/install.html).</span></span> <span data-ttu-id="ff8c3-120">Cygwin prend en charge les commandes Linux.</span><span class="sxs-lookup"><span data-stu-id="ff8c3-120">Cygwin supports Linux commands.</span></span> <span data-ttu-id="ff8c3-121">Dans ce cas, utilisez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="ff8c3-121">In this case, use hello following command:</span></span>

    split -b 100m 319GB.tsv

<span data-ttu-id="ff8c3-122">opération de fractionnement Hello crée des fichiers avec hello nom.</span><span class="sxs-lookup"><span data-stu-id="ff8c3-122">hello split operation creates files with hello following names.</span></span>

    319GB.tsv-part-aa

    319GB.tsv-part-ab

    319GB.tsv-part-ac

    319GB.tsv-part-ad

## <a name="get-disks-ready-with-data"></a><span data-ttu-id="ff8c3-123">Préparer les disques avec les données</span><span class="sxs-lookup"><span data-stu-id="ff8c3-123">Get disks ready with data</span></span>
<span data-ttu-id="ff8c3-124">Suivez les instructions de hello dans [à l’aide du service d’importation/exportation Azure hello](../storage/common/storage-import-export-service.md) (sous hello **préparer vos lecteurs** section) tooprepare vos disques durs.</span><span class="sxs-lookup"><span data-stu-id="ff8c3-124">Follow hello instructions in [Using hello Azure Import/Export service](../storage/common/storage-import-export-service.md) (under hello **Prepare your drives** section) tooprepare your hard drives.</span></span> <span data-ttu-id="ff8c3-125">Voici hello séquence :</span><span class="sxs-lookup"><span data-stu-id="ff8c3-125">Here's hello overall sequence:</span></span>

1. <span data-ttu-id="ff8c3-126">Fournissez un disque dur qui répond aux hello exigence toobe est utilisé pour hello service Azure Import/Export.</span><span class="sxs-lookup"><span data-stu-id="ff8c3-126">Procure a hard disk that meets hello requirement toobe used for hello Azure Import/Export service.</span></span>
2. <span data-ttu-id="ff8c3-127">Identifiez un compte de stockage Azure dans lequel les données de salutation seront copiées lorsqu’elle est expédiée toohello centre de données Azure.</span><span class="sxs-lookup"><span data-stu-id="ff8c3-127">Identify an Azure storage account where hello data will be copied after it is shipped toohello Azure datacenter.</span></span>
3. <span data-ttu-id="ff8c3-128">Hello d’utilisation [outil d’importation/exportation Azure](http://go.microsoft.com/fwlink/?LinkID=301900&clcid=0x409), un utilitaire de ligne de commande.</span><span class="sxs-lookup"><span data-stu-id="ff8c3-128">Use hello [Azure Import/Export Tool](http://go.microsoft.com/fwlink/?LinkID=301900&clcid=0x409), a command-line utility.</span></span> <span data-ttu-id="ff8c3-129">Voici un extrait de l’exemple qui montre comment toouse hello outil.</span><span class="sxs-lookup"><span data-stu-id="ff8c3-129">Here's a sample snippet that shows how toouse hello tool.</span></span>

    ````
    WAImportExport PrepImport /sk:<StorageAccountKey> /t: <TargetDriveLetter> /format /encrypt /logdir:e:\myexportimportjob\logdir /j:e:\myexportimportjob\journal1.jrn /id:myexportimportjob /srcdir:F:\demo\ExImContainer /dstdir:importcontainer/vf1/
    ````
    <span data-ttu-id="ff8c3-130">Consultez [à l’aide du service d’importation/exportation Azure hello](../storage/common/storage-import-export-service.md) pour plus d’exemples d’extraits.</span><span class="sxs-lookup"><span data-stu-id="ff8c3-130">See [Using hello Azure Import/Export service](../storage/common/storage-import-export-service.md) for more sample snippets.</span></span>
4. <span data-ttu-id="ff8c3-131">Hello commande précédente crée un journal de l’emplacement de fichier à hello spécifié.</span><span class="sxs-lookup"><span data-stu-id="ff8c3-131">hello preceding command creates a journal file at hello specified location.</span></span> <span data-ttu-id="ff8c3-132">Utilisez cette toocreate de fichier journal un travail d’importation à partir de hello [portail Azure classic](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="ff8c3-132">Use this journal file toocreate an import job from hello [Azure classic portal](https://manage.windowsazure.com).</span></span>

## <a name="create-an-import-job"></a><span data-ttu-id="ff8c3-133">Créer une tâche d’importation</span><span class="sxs-lookup"><span data-stu-id="ff8c3-133">Create an import job</span></span>
<span data-ttu-id="ff8c3-134">Vous pouvez maintenant créer un travail d’importation à l’aide d’instructions hello dans [à l’aide du service d’importation/exportation Azure hello](../storage/common/storage-import-export-service.md) (sous hello **travail d’importation hello créer** section).</span><span class="sxs-lookup"><span data-stu-id="ff8c3-134">You can now create an import job by using hello instructions in [Using hello Azure Import/Export service](../storage/common/storage-import-export-service.md) (under hello **Create hello Import job** section).</span></span> <span data-ttu-id="ff8c3-135">Pour ce travail d’importation, avec d’autres détails, fournissent également les fichiers de journal hello créé lors de la préparation des lecteurs de disque hello.</span><span class="sxs-lookup"><span data-stu-id="ff8c3-135">For this import job, with other details, also provide hello journal file created while preparing hello disk drives.</span></span>

## <a name="physically-ship-hello-disks"></a><span data-ttu-id="ff8c3-136">Physiquement expédier les disques de hello</span><span class="sxs-lookup"><span data-stu-id="ff8c3-136">Physically ship hello disks</span></span>
<span data-ttu-id="ff8c3-137">Vous pouvez expédier maintenant physiquement de hello disques tooan centre de données Azure.</span><span class="sxs-lookup"><span data-stu-id="ff8c3-137">You can now physically ship hello disks tooan Azure datacenter.</span></span> <span data-ttu-id="ff8c3-138">Là, les données de salutation sont copiées sur des objets BLOB de stockage Azure toohello que vous avez fourni lors de la création du travail d’importation hello.</span><span class="sxs-lookup"><span data-stu-id="ff8c3-138">There, hello data is copied over toohello Azure Storage blobs you provided while creating hello import job.</span></span> <span data-ttu-id="ff8c3-139">En outre, lors de la création de tâche de hello, si vous avez choisi hello tooprovide suivi des informations de version ultérieure, vous pouvez maintenant revenir numéro de suivi du hello de travail et la mise à jour d’importation tooyour.</span><span class="sxs-lookup"><span data-stu-id="ff8c3-139">Also, while creating hello job, if you opted tooprovide hello tracking information later, you can now go back tooyour import job and update hello tracking number.</span></span>

## <a name="copy-data-from-azure-storage-blobs-tooazure-data-lake-store"></a><span data-ttu-id="ff8c3-140">Copier des données depuis le stockage Azure BLOB tooAzure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="ff8c3-140">Copy data from Azure Storage blobs tooAzure Data Lake Store</span></span>
<span data-ttu-id="ff8c3-141">Après l’état hello Hello travail d’importation montre qu’il est terminé, vous pouvez vérifier si les données de salutation sont disponibles dans des objets BLOB de stockage Azure hello que vous aviez spécifié.</span><span class="sxs-lookup"><span data-stu-id="ff8c3-141">After hello status of hello import job shows that it's completed, you can verify whether hello data is available in hello Azure Storage blobs you had specified.</span></span> <span data-ttu-id="ff8c3-142">Vous pouvez ensuite utiliser les diverses toomove de méthodes que les données à partir de hello BLOB tooAzure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="ff8c3-142">You can then use a variety of methods toomove that data from hello blobs tooAzure Data Lake Store.</span></span> <span data-ttu-id="ff8c3-143">Pour tous les hello les options disponibles pour le téléchargement des données, consultez [réception de données dans Data Lake Store](data-lake-store-data-scenarios.md#ingest-data-into-data-lake-store).</span><span class="sxs-lookup"><span data-stu-id="ff8c3-143">For all hello available options for uploading data, see [Ingesting data into Data Lake Store](data-lake-store-data-scenarios.md#ingest-data-into-data-lake-store).</span></span>

<span data-ttu-id="ff8c3-144">Dans cette section, nous vous fournir les définitions de JSON hello que vous pouvez utiliser toocreate un pipeline Azure Data Factory pour copier des données.</span><span class="sxs-lookup"><span data-stu-id="ff8c3-144">In this section, we provide you with hello JSON definitions that you can use toocreate an Azure Data Factory pipeline for copying data.</span></span> <span data-ttu-id="ff8c3-145">Vous pouvez utiliser les définitions de JSON à partir de hello [portail Azure](../data-factory/data-factory-copy-activity-tutorial-using-azure-portal.md), ou [Visual Studio](../data-factory/data-factory-copy-activity-tutorial-using-visual-studio.md), ou [Azure PowerShell](../data-factory/data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="ff8c3-145">You can use these JSON definitions from hello [Azure portal](../data-factory/data-factory-copy-activity-tutorial-using-azure-portal.md), or [Visual Studio](../data-factory/data-factory-copy-activity-tutorial-using-visual-studio.md), or [Azure PowerShell](../data-factory/data-factory-copy-activity-tutorial-using-powershell.md).</span></span>

### <a name="source-linked-service-azure-storage-blob"></a><span data-ttu-id="ff8c3-146">Service lié source (objet blob Stockage Azure)</span><span class="sxs-lookup"><span data-stu-id="ff8c3-146">Source linked service (Azure Storage blob)</span></span>
````
{
    "name": "AzureStorageLinkedService",
    "properties": {
        "type": "AzureStorage",
        "description": "",
        "typeProperties": {
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
        }
    }
}
````

### <a name="target-linked-service-azure-data-lake-store"></a><span data-ttu-id="ff8c3-147">Service lié cible (Azure Data Lake Store)</span><span class="sxs-lookup"><span data-stu-id="ff8c3-147">Target linked service (Azure Data Lake Store)</span></span>
````
{
    "name": "AzureDataLakeStoreLinkedService",
    "properties": {
        "type": "AzureDataLakeStore",
        "description": "",
        "typeProperties": {
            "authorization": "<Click 'Authorize' tooallow this data factory and hello activities it runs tooaccess this Data Lake Store with your access rights>",
            "dataLakeStoreUri": "https://<adls_account_name>.azuredatalakestore.net/webhdfs/v1",
            "sessionId": "<OAuth session id from hello OAuth authorization session. Each session id is unique and may only be used once>"
        }
    }
}
````
### <a name="input-data-set"></a><span data-ttu-id="ff8c3-148">Jeu de données d’entrée</span><span class="sxs-lookup"><span data-stu-id="ff8c3-148">Input data set</span></span>
````
{
    "name": "InputDataSet",
    "properties": {
        "published": false,
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "importcontainer/vf1/"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {}
    }
}
````
### <a name="output-data-set"></a><span data-ttu-id="ff8c3-149">Jeu de données de sortie</span><span class="sxs-lookup"><span data-stu-id="ff8c3-149">Output data set</span></span>
````
{
"name": "OutputDataSet",
"properties": {
  "published": false,
  "type": "AzureDataLakeStore",
  "linkedServiceName": "AzureDataLakeStoreLinkedService",
  "typeProperties": {
    "folderPath": "/importeddatafeb8job/"
    },
  "availability": {
    "frequency": "Hour",
    "interval": 1
    }
  }
}
````
### <a name="pipeline-copy-activity"></a><span data-ttu-id="ff8c3-150">Pipeline (activité de copie)</span><span class="sxs-lookup"><span data-stu-id="ff8c3-150">Pipeline (copy activity)</span></span>
````
{
    "name": "CopyImportedData",
    "properties": {
        "description": "Pipeline with copy activity",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "BlobSource"
                    },
                    "sink": {
                        "type": "AzureDataLakeStoreSink",
                        "copyBehavior": "PreserveHierarchy",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "InputDataSet"
                    }
                ],
                "outputs": [
                    {
                        "name": "OutputDataSet"
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
                "name": "AzureBlobtoDataLake",
                "description": "Copy Activity"
            }
        ],
        "start": "2016-02-08T22:00:00Z",
        "end": "2016-02-08T23:00:00Z",
        "isPaused": false,
        "pipelineMode": "Scheduled"
    }
}
````
<span data-ttu-id="ff8c3-151">Pour plus d’informations, consultez [déplacer des données depuis le stockage Azure blob tooAzure Data Lake Store à l’aide d’Azure Data Factory](../data-factory/data-factory-azure-datalake-connector.md).</span><span class="sxs-lookup"><span data-stu-id="ff8c3-151">For more information, see [Move data from Azure Storage blob tooAzure Data Lake Store using Azure Data Factory](../data-factory/data-factory-azure-datalake-connector.md).</span></span>

## <a name="reconstruct-hello-data-files-in-azure-data-lake-store"></a><span data-ttu-id="ff8c3-152">Reconstruire les fichiers de données hello dans Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="ff8c3-152">Reconstruct hello data files in Azure Data Lake Store</span></span>
<span data-ttu-id="ff8c3-153">Nous avons commencé avec un fichier qui a été 319 Go et tirez-en dans des fichiers de plus petite taille afin qu’il peut être transféré à l’aide du service d’importation/exportation Azure hello.</span><span class="sxs-lookup"><span data-stu-id="ff8c3-153">We started with a file that was 319 GB, and broke it down into files of smaller size so that it could be transferred by using hello Azure Import/Export service.</span></span> <span data-ttu-id="ff8c3-154">Maintenant que les données de salutation sont dans Azure Data Lake Store, nous pouvons reconstruire la taille d’origine du tooits fichier hello.</span><span class="sxs-lookup"><span data-stu-id="ff8c3-154">Now that hello data is in Azure Data Lake Store, we can reconstruct hello file tooits original size.</span></span> <span data-ttu-id="ff8c3-155">Vous pouvez utiliser hello suivant Azure PowerShell cmldts toodo donc.</span><span class="sxs-lookup"><span data-stu-id="ff8c3-155">You can use hello following Azure PowerShell cmldts toodo so.</span></span>

````
# Login tooour account
Login-AzureRmAccount

# List your subscriptions
Get-AzureRmSubscription

# Switch toohello subscription you want toowork with
Set-AzureRmContext –SubscriptionId
Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.DataLakeStore"

# Join  hello files
Join-AzureRmDataLakeStoreItem -AccountName "<adls_account_name" -Paths "/importeddatafeb8job/319GB.tsv-part-aa","/importeddatafeb8job/319GB.tsv-part-ab", "/importeddatafeb8job/319GB.tsv-part-ac", "/importeddatafeb8job/319GB.tsv-part-ad" -Destination "/importeddatafeb8job/MergedFile.csv”
````

## <a name="next-steps"></a><span data-ttu-id="ff8c3-156">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="ff8c3-156">Next steps</span></span>
* [<span data-ttu-id="ff8c3-157">Sécuriser les données dans Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="ff8c3-157">Secure data in Data Lake Store</span></span>](data-lake-store-secure-data.md)
* [<span data-ttu-id="ff8c3-158">Utiliser Azure Data Lake Analytics avec Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="ff8c3-158">Use Azure Data Lake Analytics with Data Lake Store</span></span>](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [<span data-ttu-id="ff8c3-159">Utiliser Azure HDInsight avec Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="ff8c3-159">Use Azure HDInsight with Data Lake Store</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)
