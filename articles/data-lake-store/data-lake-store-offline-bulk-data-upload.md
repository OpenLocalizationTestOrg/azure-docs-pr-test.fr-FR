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
# <a name="use-hello-azure-importexport-service-for-offline-copy-of-data-toodata-lake-store"></a>Utiliser le service d’importation/exportation Azure hello pour une copie hors connexion tooData Lake du magasin de données
Dans cet article, vous allez apprendre comment les données volumineuses toocopy définit (> 200 Go) dans un Azure Data Lake Store à l’aide des méthodes de copie en mode hors connexion, comme hello [service Azure Import/Export](../storage/common/storage-import-export-service.md). Plus précisément, fichier hello utilisé comme un exemple dans cet article est 339,420,860,416 octets, ou environ 319 Go sur le disque. Appelons ce fichier 319GB.tsv.

Hello service Azure Import/Export vous permet de tootransfer de grandes quantités de données plus en toute sécurité tooAzure stockage d’objets Blob par disque dur de livraison lecteurs tooan centre de données Azure.

## <a name="prerequisites"></a>Composants requis
Avant de commencer, vous devez disposer de hello :

* **Un abonnement Azure**. Consultez [Obtenir une version d'évaluation gratuite d'Azure](https://azure.microsoft.com/pricing/free-trial/).
* **Un compte de stockage Azure**.
* **Un compte Azure Data Lake Store**. Pour obtenir des instructions sur la façon de voir d’un seul, toocreate [prise en main Azure Data Lake Store](data-lake-store-get-started-portal.md)

## <a name="preparing-hello-data"></a>Préparation des données hello
Avant d’utiliser le service d’importation/exportation hello, toobe de fichier saut hello données transférées **dans les copies de moins de 200 Go** taille. outil d’importation Hello ne fonctionne pas avec les fichiers de plus de 200 Go. Dans ce didacticiel, nous fractionnez le fichier en hello en segments de 100 Go. Pour ce faire, utilisez [Cygwin](https://cygwin.com/install.html). Cygwin prend en charge les commandes Linux. Dans ce cas, utilisez hello de commande suivante :

    split -b 100m 319GB.tsv

opération de fractionnement Hello crée des fichiers avec hello nom.

    319GB.tsv-part-aa

    319GB.tsv-part-ab

    319GB.tsv-part-ac

    319GB.tsv-part-ad

## <a name="get-disks-ready-with-data"></a>Préparer les disques avec les données
Suivez les instructions de hello dans [à l’aide du service d’importation/exportation Azure hello](../storage/common/storage-import-export-service.md) (sous hello **préparer vos lecteurs** section) tooprepare vos disques durs. Voici hello séquence :

1. Fournissez un disque dur qui répond aux hello exigence toobe est utilisé pour hello service Azure Import/Export.
2. Identifiez un compte de stockage Azure dans lequel les données de salutation seront copiées lorsqu’elle est expédiée toohello centre de données Azure.
3. Hello d’utilisation [outil d’importation/exportation Azure](http://go.microsoft.com/fwlink/?LinkID=301900&clcid=0x409), un utilitaire de ligne de commande. Voici un extrait de l’exemple qui montre comment toouse hello outil.

    ````
    WAImportExport PrepImport /sk:<StorageAccountKey> /t: <TargetDriveLetter> /format /encrypt /logdir:e:\myexportimportjob\logdir /j:e:\myexportimportjob\journal1.jrn /id:myexportimportjob /srcdir:F:\demo\ExImContainer /dstdir:importcontainer/vf1/
    ````
    Consultez [à l’aide du service d’importation/exportation Azure hello](../storage/common/storage-import-export-service.md) pour plus d’exemples d’extraits.
4. Hello commande précédente crée un journal de l’emplacement de fichier à hello spécifié. Utilisez cette toocreate de fichier journal un travail d’importation à partir de hello [portail Azure classic](https://manage.windowsazure.com).

## <a name="create-an-import-job"></a>Créer une tâche d’importation
Vous pouvez maintenant créer un travail d’importation à l’aide d’instructions hello dans [à l’aide du service d’importation/exportation Azure hello](../storage/common/storage-import-export-service.md) (sous hello **travail d’importation hello créer** section). Pour ce travail d’importation, avec d’autres détails, fournissent également les fichiers de journal hello créé lors de la préparation des lecteurs de disque hello.

## <a name="physically-ship-hello-disks"></a>Physiquement expédier les disques de hello
Vous pouvez expédier maintenant physiquement de hello disques tooan centre de données Azure. Là, les données de salutation sont copiées sur des objets BLOB de stockage Azure toohello que vous avez fourni lors de la création du travail d’importation hello. En outre, lors de la création de tâche de hello, si vous avez choisi hello tooprovide suivi des informations de version ultérieure, vous pouvez maintenant revenir numéro de suivi du hello de travail et la mise à jour d’importation tooyour.

## <a name="copy-data-from-azure-storage-blobs-tooazure-data-lake-store"></a>Copier des données depuis le stockage Azure BLOB tooAzure Data Lake Store
Après l’état hello Hello travail d’importation montre qu’il est terminé, vous pouvez vérifier si les données de salutation sont disponibles dans des objets BLOB de stockage Azure hello que vous aviez spécifié. Vous pouvez ensuite utiliser les diverses toomove de méthodes que les données à partir de hello BLOB tooAzure Data Lake Store. Pour tous les hello les options disponibles pour le téléchargement des données, consultez [réception de données dans Data Lake Store](data-lake-store-data-scenarios.md#ingest-data-into-data-lake-store).

Dans cette section, nous vous fournir les définitions de JSON hello que vous pouvez utiliser toocreate un pipeline Azure Data Factory pour copier des données. Vous pouvez utiliser les définitions de JSON à partir de hello [portail Azure](../data-factory/data-factory-copy-activity-tutorial-using-azure-portal.md), ou [Visual Studio](../data-factory/data-factory-copy-activity-tutorial-using-visual-studio.md), ou [Azure PowerShell](../data-factory/data-factory-copy-activity-tutorial-using-powershell.md).

### <a name="source-linked-service-azure-storage-blob"></a>Service lié source (objet blob Stockage Azure)
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

### <a name="target-linked-service-azure-data-lake-store"></a>Service lié cible (Azure Data Lake Store)
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
### <a name="input-data-set"></a>Jeu de données d’entrée
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
### <a name="output-data-set"></a>Jeu de données de sortie
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
### <a name="pipeline-copy-activity"></a>Pipeline (activité de copie)
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
Pour plus d’informations, consultez [déplacer des données depuis le stockage Azure blob tooAzure Data Lake Store à l’aide d’Azure Data Factory](../data-factory/data-factory-azure-datalake-connector.md).

## <a name="reconstruct-hello-data-files-in-azure-data-lake-store"></a>Reconstruire les fichiers de données hello dans Azure Data Lake Store
Nous avons commencé avec un fichier qui a été 319 Go et tirez-en dans des fichiers de plus petite taille afin qu’il peut être transféré à l’aide du service d’importation/exportation Azure hello. Maintenant que les données de salutation sont dans Azure Data Lake Store, nous pouvons reconstruire la taille d’origine du tooits fichier hello. Vous pouvez utiliser hello suivant Azure PowerShell cmldts toodo donc.

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

## <a name="next-steps"></a>Étapes suivantes
* [Sécuriser les données dans Data Lake Store](data-lake-store-secure-data.md)
* [Utiliser Azure Data Lake Analytics avec Data Lake Store](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [Utiliser Azure HDInsight avec Data Lake Store](data-lake-store-hdinsight-hadoop-use-portal.md)
