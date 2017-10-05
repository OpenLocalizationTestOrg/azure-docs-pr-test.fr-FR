---
title: "Charger de grandes quantités de données sur Data Lake Store à l’aide de méthodes hors connexion | Microsoft Docs"
description: "Utiliser l’outil AdlCopy pour copier les données d’objets blob Stockage Azure vers Data Lake Store"
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
ms.openlocfilehash: b469c0ebe9838a1ea986cff3043e3008941e9aa9
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="use-the-azure-importexport-service-for-offline-copy-of-data-to-data-lake-store"></a><span data-ttu-id="d6abd-103">Utiliser le service Azure Import/Export pour copier les données dans Data Lake Store hors connexion</span><span class="sxs-lookup"><span data-stu-id="d6abd-103">Use the Azure Import/Export service for offline copy of data to Data Lake Store</span></span>
<span data-ttu-id="d6abd-104">Dans cet article, vous allez découvrir comment copier de grands jeux de données (> 200 Go) dans un Azure Data Lake Store à l’aide de méthodes de copie hors connexion, comme le [service Azure Import/Export](../storage/common/storage-import-export-service.md).</span><span class="sxs-lookup"><span data-stu-id="d6abd-104">In this article, you'll learn how to copy huge data sets (>200 GB) into an Azure Data Lake Store by using offline copy methods, like the [Azure Import/Export service](../storage/common/storage-import-export-service.md).</span></span> <span data-ttu-id="d6abd-105">Plus précisément, la taille du fichier utilisé comme exemple dans cet article est de 339 420 860 416 octets ou environ 319 Go sur disque.</span><span class="sxs-lookup"><span data-stu-id="d6abd-105">Specifically, the file used as an example in this article is 339,420,860,416 bytes, or about 319 GB on disk.</span></span> <span data-ttu-id="d6abd-106">Appelons ce fichier 319GB.tsv.</span><span class="sxs-lookup"><span data-stu-id="d6abd-106">Let's call this file 319GB.tsv.</span></span>

<span data-ttu-id="d6abd-107">Le service Azure Import/Export vous aide à transférer de façon plus sécurisée des volumes importants de données vers Stockage Blob Azure en expédiant des disques durs vers un centre de données Azure.</span><span class="sxs-lookup"><span data-stu-id="d6abd-107">The Azure Import/Export service helps you to transfer large amounts of data more securely to Azure Blob storage by shipping hard disk drives to an Azure datacenter.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d6abd-108">Composants requis</span><span class="sxs-lookup"><span data-stu-id="d6abd-108">Prerequisites</span></span>
<span data-ttu-id="d6abd-109">Avant de commencer la lecture cet article, vous devez disposer des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="d6abd-109">Before you begin, you must have the following:</span></span>

* <span data-ttu-id="d6abd-110">**Un abonnement Azure**.</span><span class="sxs-lookup"><span data-stu-id="d6abd-110">**An Azure subscription**.</span></span> <span data-ttu-id="d6abd-111">Consultez [Obtenir une version d'évaluation gratuite d'Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="d6abd-111">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="d6abd-112">**Un compte de stockage Azure**.</span><span class="sxs-lookup"><span data-stu-id="d6abd-112">**An Azure storage account**.</span></span>
* <span data-ttu-id="d6abd-113">**Un compte Azure Data Lake Store**.</span><span class="sxs-lookup"><span data-stu-id="d6abd-113">**An Azure Data Lake Store account**.</span></span> <span data-ttu-id="d6abd-114">Pour savoir comment en créer un, consultez [Prise en main d'Azure Data Lake Store](data-lake-store-get-started-portal.md)</span><span class="sxs-lookup"><span data-stu-id="d6abd-114">For instructions on how to create one, see [Get started with Azure Data Lake Store](data-lake-store-get-started-portal.md)</span></span>

## <a name="preparing-the-data"></a><span data-ttu-id="d6abd-115">Préparation des données</span><span class="sxs-lookup"><span data-stu-id="d6abd-115">Preparing the data</span></span>
<span data-ttu-id="d6abd-116">Avant d’utiliser le service Import/Export, scindez le fichier de données à transférer **en copies de moins de 200 Go**.</span><span class="sxs-lookup"><span data-stu-id="d6abd-116">Before using the Import/Export service, break the data file to be transferred **into copies that are less than 200 GB** in size.</span></span> <span data-ttu-id="d6abd-117">L’outil d’importation ne fonctionne pas avec des fichiers de plus de 200 Go.</span><span class="sxs-lookup"><span data-stu-id="d6abd-117">The import tool does not work with files greater than 200 GB.</span></span> <span data-ttu-id="d6abd-118">Dans ce didacticiel, nous fractionnons le fichier en blocs de 100 Go.</span><span class="sxs-lookup"><span data-stu-id="d6abd-118">In this tutorial, we split the file into chunks of 100 GB each.</span></span> <span data-ttu-id="d6abd-119">Pour ce faire, utilisez [Cygwin](https://cygwin.com/install.html).</span><span class="sxs-lookup"><span data-stu-id="d6abd-119">You can do this by using [Cygwin](https://cygwin.com/install.html).</span></span> <span data-ttu-id="d6abd-120">Cygwin prend en charge les commandes Linux.</span><span class="sxs-lookup"><span data-stu-id="d6abd-120">Cygwin supports Linux commands.</span></span> <span data-ttu-id="d6abd-121">Dans ce cas, utilisez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="d6abd-121">In this case, use the following command:</span></span>

    split -b 100m 319GB.tsv

<span data-ttu-id="d6abd-122">L’opération split crée des fichiers portant les noms suivants.</span><span class="sxs-lookup"><span data-stu-id="d6abd-122">The split operation creates files with the following names.</span></span>

    319GB.tsv-part-aa

    319GB.tsv-part-ab

    319GB.tsv-part-ac

    319GB.tsv-part-ad

## <a name="get-disks-ready-with-data"></a><span data-ttu-id="d6abd-123">Préparer les disques avec les données</span><span class="sxs-lookup"><span data-stu-id="d6abd-123">Get disks ready with data</span></span>
<span data-ttu-id="d6abd-124">Suivez les instructions relatives à [l’utilisation du Service Azure Import/Export](../storage/common/storage-import-export-service.md) (sous la section **Préparation des lecteurs**) pour préparer vos disques durs.</span><span class="sxs-lookup"><span data-stu-id="d6abd-124">Follow the instructions in [Using the Azure Import/Export service](../storage/common/storage-import-export-service.md) (under the **Prepare your drives** section) to prepare your hard drives.</span></span> <span data-ttu-id="d6abd-125">Voici la séquence générale :</span><span class="sxs-lookup"><span data-stu-id="d6abd-125">Here's the overall sequence:</span></span>

1. <span data-ttu-id="d6abd-126">Procurez-vous un disque dur utilisable pour le service Import/Export Azure.</span><span class="sxs-lookup"><span data-stu-id="d6abd-126">Procure a hard disk that meets the requirement to be used for the Azure Import/Export service.</span></span>
2. <span data-ttu-id="d6abd-127">Identifiez un compte de stockage Azure où les données seront copiées une fois le disque expédié vers le centre de données Azure.</span><span class="sxs-lookup"><span data-stu-id="d6abd-127">Identify an Azure storage account where the data will be copied after it is shipped to the Azure datacenter.</span></span>
3. <span data-ttu-id="d6abd-128">Utilisez [l’outil Azure Import/Export](http://go.microsoft.com/fwlink/?LinkID=301900&clcid=0x409), qui est un utilitaire de ligne de commande.</span><span class="sxs-lookup"><span data-stu-id="d6abd-128">Use the [Azure Import/Export Tool](http://go.microsoft.com/fwlink/?LinkID=301900&clcid=0x409), a command-line utility.</span></span> <span data-ttu-id="d6abd-129">Voici un exemple d’extrait de code illustrant l’utilisation de l’outil.</span><span class="sxs-lookup"><span data-stu-id="d6abd-129">Here's a sample snippet that shows how to use the tool.</span></span>

    ````
    WAImportExport PrepImport /sk:<StorageAccountKey> /t: <TargetDriveLetter> /format /encrypt /logdir:e:\myexportimportjob\logdir /j:e:\myexportimportjob\journal1.jrn /id:myexportimportjob /srcdir:F:\demo\ExImContainer /dstdir:importcontainer/vf1/
    ````
    <span data-ttu-id="d6abd-130">Pour obtenir d’autres exemples d’extraits, consultez [Using the Azure Import/Export service](../storage/common/storage-import-export-service.md) (Utilisation du service Azure Import/Export).</span><span class="sxs-lookup"><span data-stu-id="d6abd-130">See [Using the Azure Import/Export service](../storage/common/storage-import-export-service.md) for more sample snippets.</span></span>
4. <span data-ttu-id="d6abd-131">La commande précédente crée un fichier journal à l’emplacement spécifié.</span><span class="sxs-lookup"><span data-stu-id="d6abd-131">The preceding command creates a journal file at the specified location.</span></span> <span data-ttu-id="d6abd-132">Utilisez ce fichier journal pour créer un travail d’importation à partir du [portail Azure Classic](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="d6abd-132">Use this journal file to create an import job from the [Azure classic portal](https://manage.windowsazure.com).</span></span>

## <a name="create-an-import-job"></a><span data-ttu-id="d6abd-133">Créer une tâche d’importation</span><span class="sxs-lookup"><span data-stu-id="d6abd-133">Create an import job</span></span>
<span data-ttu-id="d6abd-134">Vous pouvez maintenant créer un travail d’importation en suivant les instructions relatives à [l’utilisation du Service Azure Import/Export](../storage/common/storage-import-export-service.md) (sous la section **Création de la tâche d’importation**).</span><span class="sxs-lookup"><span data-stu-id="d6abd-134">You can now create an import job by using the instructions in [Using the Azure Import/Export service](../storage/common/storage-import-export-service.md) (under the **Create the Import job** section).</span></span> <span data-ttu-id="d6abd-135">Pour ce travail d’importation, entre autres détails, indiquez le fichier journal créé durant la préparation des lecteurs de disque.</span><span class="sxs-lookup"><span data-stu-id="d6abd-135">For this import job, with other details, also provide the journal file created while preparing the disk drives.</span></span>

## <a name="physically-ship-the-disks"></a><span data-ttu-id="d6abd-136">Expédier les disques physiquement</span><span class="sxs-lookup"><span data-stu-id="d6abd-136">Physically ship the disks</span></span>
<span data-ttu-id="d6abd-137">Vous pouvez désormais expédier physiquement les disques vers un centre de données Azure.</span><span class="sxs-lookup"><span data-stu-id="d6abd-137">You can now physically ship the disks to an Azure datacenter.</span></span> <span data-ttu-id="d6abd-138">Les données y seront copiées dans les objets blob Stockage Azure que vous avez fournis durant la création du travail d’importation.</span><span class="sxs-lookup"><span data-stu-id="d6abd-138">There, the data is copied over to the Azure Storage blobs you provided while creating the import job.</span></span> <span data-ttu-id="d6abd-139">En outre, pendant la création du travail, si vous avez choisi d’indiquer les informations de suivi plus tard, vous pouvez maintenant revenir à votre travail d’importation et mettre à jour le numéro de suivi.</span><span class="sxs-lookup"><span data-stu-id="d6abd-139">Also, while creating the job, if you opted to provide the tracking information later, you can now go back to your import job and update the tracking number.</span></span>

## <a name="copy-data-from-azure-storage-blobs-to-azure-data-lake-store"></a><span data-ttu-id="d6abd-140">Copier des données d’objets blob Stockage Azure vers Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="d6abd-140">Copy data from Azure Storage blobs to Azure Data Lake Store</span></span>
<span data-ttu-id="d6abd-141">Une fois que l’état du travail d’importation indique que celui-ci est terminé, vous pouvez vérifier si les données sont disponibles dans les objets blob Stockage Azure que vous aviez spécifiés.</span><span class="sxs-lookup"><span data-stu-id="d6abd-141">After the status of the import job shows that it's completed, you can verify whether the data is available in the Azure Storage blobs you had specified.</span></span> <span data-ttu-id="d6abd-142">Vous pouvez ensuite utiliser différentes méthodes pour déplacer ces données depuis les objets blob vers Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="d6abd-142">You can then use a variety of methods to move that data from the blobs to Azure Data Lake Store.</span></span> <span data-ttu-id="d6abd-143">Pour connaître toutes les options disponibles pour le chargement de données, consultez [Réception de données dans Data Lake Store](data-lake-store-data-scenarios.md#ingest-data-into-data-lake-store).</span><span class="sxs-lookup"><span data-stu-id="d6abd-143">For all the available options for uploading data, see [Ingesting data into Data Lake Store](data-lake-store-data-scenarios.md#ingest-data-into-data-lake-store).</span></span>

<span data-ttu-id="d6abd-144">Dans cette section, nous vous fournissons les définitions JSON grâce auxquelles vous pouvez créer un pipeline Azure Data Factory en vue de copier les données.</span><span class="sxs-lookup"><span data-stu-id="d6abd-144">In this section, we provide you with the JSON definitions that you can use to create an Azure Data Factory pipeline for copying data.</span></span> <span data-ttu-id="d6abd-145">Vous pouvez utiliser ces définitions JSON à partir du [portail Azure](../data-factory/data-factory-copy-activity-tutorial-using-azure-portal.md), de [Visual Studio](../data-factory/data-factory-copy-activity-tutorial-using-visual-studio.md) ou de [Azure PowerShell](../data-factory/data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="d6abd-145">You can use these JSON definitions from the [Azure portal](../data-factory/data-factory-copy-activity-tutorial-using-azure-portal.md), or [Visual Studio](../data-factory/data-factory-copy-activity-tutorial-using-visual-studio.md), or [Azure PowerShell](../data-factory/data-factory-copy-activity-tutorial-using-powershell.md).</span></span>

### <a name="source-linked-service-azure-storage-blob"></a><span data-ttu-id="d6abd-146">Service lié source (objet blob Stockage Azure)</span><span class="sxs-lookup"><span data-stu-id="d6abd-146">Source linked service (Azure Storage blob)</span></span>
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

### <a name="target-linked-service-azure-data-lake-store"></a><span data-ttu-id="d6abd-147">Service lié cible (Azure Data Lake Store)</span><span class="sxs-lookup"><span data-stu-id="d6abd-147">Target linked service (Azure Data Lake Store)</span></span>
````
{
    "name": "AzureDataLakeStoreLinkedService",
    "properties": {
        "type": "AzureDataLakeStore",
        "description": "",
        "typeProperties": {
            "authorization": "<Click 'Authorize' to allow this data factory and the activities it runs to access this Data Lake Store with your access rights>",
            "dataLakeStoreUri": "https://<adls_account_name>.azuredatalakestore.net/webhdfs/v1",
            "sessionId": "<OAuth session id from the OAuth authorization session. Each session id is unique and may only be used once>"
        }
    }
}
````
### <a name="input-data-set"></a><span data-ttu-id="d6abd-148">Jeu de données d’entrée</span><span class="sxs-lookup"><span data-stu-id="d6abd-148">Input data set</span></span>
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
### <a name="output-data-set"></a><span data-ttu-id="d6abd-149">Jeu de données de sortie</span><span class="sxs-lookup"><span data-stu-id="d6abd-149">Output data set</span></span>
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
### <a name="pipeline-copy-activity"></a><span data-ttu-id="d6abd-150">Pipeline (activité de copie)</span><span class="sxs-lookup"><span data-stu-id="d6abd-150">Pipeline (copy activity)</span></span>
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
<span data-ttu-id="d6abd-151">Pour plus d’informations, consultez [Move data from Azure Storage blob to Azure Data Lake Store using Azure Data Factory](../data-factory/data-factory-azure-datalake-connector.md) (Déplacer des données à partir d’un objet blob Stockage Azure vers Azure Data Lake Store à l’aide d’Azure Data Factory).</span><span class="sxs-lookup"><span data-stu-id="d6abd-151">For more information, see [Move data from Azure Storage blob to Azure Data Lake Store using Azure Data Factory](../data-factory/data-factory-azure-datalake-connector.md).</span></span>

## <a name="reconstruct-the-data-files-in-azure-data-lake-store"></a><span data-ttu-id="d6abd-152">Reconstruire les fichiers de données dans Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="d6abd-152">Reconstruct the data files in Azure Data Lake Store</span></span>
<span data-ttu-id="d6abd-153">Nous avons commencé avec un fichier de 319 Go, que nous avons scindé en fichiers de plus petite taille afin de pouvoir le transférer à l’aide du service Azure Import/Export.</span><span class="sxs-lookup"><span data-stu-id="d6abd-153">We started with a file that was 319 GB, and broke it down into files of smaller size so that it could be transferred by using the Azure Import/Export service.</span></span> <span data-ttu-id="d6abd-154">Les données se trouvant désormais dans Azure Data Lake Store, nous pouvons reconstruire le fichier à sa taille d’origine.</span><span class="sxs-lookup"><span data-stu-id="d6abd-154">Now that the data is in Azure Data Lake Store, we can reconstruct the file to its original size.</span></span> <span data-ttu-id="d6abd-155">Pour ce faire, vous pouvez utiliser l’applet de commande Azure PowerShell suivante.</span><span class="sxs-lookup"><span data-stu-id="d6abd-155">You can use the following Azure PowerShell cmldts to do so.</span></span>

````
# Login to our account
Login-AzureRmAccount

# List your subscriptions
Get-AzureRmSubscription

# Switch to the subscription you want to work with
Set-AzureRmContext –SubscriptionId
Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.DataLakeStore"

# Join  the files
Join-AzureRmDataLakeStoreItem -AccountName "<adls_account_name" -Paths "/importeddatafeb8job/319GB.tsv-part-aa","/importeddatafeb8job/319GB.tsv-part-ab", "/importeddatafeb8job/319GB.tsv-part-ac", "/importeddatafeb8job/319GB.tsv-part-ad" -Destination "/importeddatafeb8job/MergedFile.csv”
````

## <a name="next-steps"></a><span data-ttu-id="d6abd-156">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="d6abd-156">Next steps</span></span>
* [<span data-ttu-id="d6abd-157">Sécuriser les données dans Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="d6abd-157">Secure data in Data Lake Store</span></span>](data-lake-store-secure-data.md)
* [<span data-ttu-id="d6abd-158">Utiliser Azure Data Lake Analytics avec Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="d6abd-158">Use Azure Data Lake Analytics with Data Lake Store</span></span>](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [<span data-ttu-id="d6abd-159">Utiliser Azure HDInsight avec Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="d6abd-159">Use Azure HDInsight with Data Lake Store</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)
