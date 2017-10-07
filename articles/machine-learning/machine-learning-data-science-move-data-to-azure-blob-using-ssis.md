---
title: "tooor de données aaaMove à partir du stockage d’objets Blob Azure à l’aide de connecteurs SSIS | Documents Microsoft"
description: "Déplacer les données tooor à partir du stockage d’objets Blob Azure à l’aide de connecteurs SSIS."
services: machine-learning,storage
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 96a1b5fb-34d1-4b9b-8d99-2bb8289e0398
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev
ms.openlocfilehash: 15068af1c69f11e74e109ee5ae2b9f1a674ea388
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-tooor-from-azure-blob-storage-using-ssis-connectors"></a>Déplacer les données tooor de stockage d’objets Blob Azure à l’aide de connecteurs SSIS
Hello [SQL Server Integration Services Feature Pack pour Azure](https://msdn.microsoft.com/library/mt146770.aspx) fournit des composants tooconnect tooAzure, transférer des données entre des sources de données Azure et locales et traiter les données stockées dans Azure.

[!INCLUDE [blob-storage-tool-selector](../../includes/machine-learning-blob-storage-tool-selector.md)]

Une fois que les clients ont déplacé des données locales dans le cloud de hello, ils peuvent y accéder à partir de n’importe quel service Azure tooleverage hello toute la puissance de la suite de hello de technologies Azure. Il peut être utilisé, par exemple, dans Machine Learning ou sur un cluster HDInsight.

Il s’agit généralement être la première étape de hello pour hello [SQL](machine-learning-data-science-process-sql-walkthrough.md) et [HDInsight](machine-learning-data-science-process-hive-walkthrough.md) procédures pas à pas.

Pour en savoir plus sur les scénarios canoniques qui utiliser SSIS tooaccomplish entreprise doit communes dans les scénarios d’intégration hybride données, consultez [faire plus avec SQL Server Integration Services Feature Pack pour Azure](http://blogs.msdn.com/b/ssis/archive/2015/06/25/doing-more-with-sql-server-integration-services-feature-pack-for-azure.aspx) blog.

> [!NOTE]
> Pour un stockage d’objets blob tooAzure présentation complète, consultez trop[principes de base Azure Blob](../storage/blobs/storage-dotnet-how-to-use-blobs.md) et trop[Service d’objets Blob Azure](https://msdn.microsoft.com/library/azure/dd179376.aspx).
> 
> 

## <a name="prerequisites"></a>Composants requis
tâches de hello tooperform décrit dans cet article, vous devez disposer un abonnement Azure et configurer un compte de stockage Azure. Vous devez connaître votre stockage Azure compte compte et le nom de clé tooupload ou télécharger des données.

* tooset d’un **abonnement Azure**, consultez [version d’évaluation d’un mois gratuite](https://azure.microsoft.com/pricing/free-trial/).
* Pour obtenir des instructions sur la création d’ **un compte de stockage** et obtenir des informations sur le compte et la clé, consultez la section [À propos des comptes de stockage Azure](../storage/common/storage-create-storage-account.md).

toouse hello **connecteurs SSIS**, vous devez télécharger :

* **SQL Server 2014 ou 2016 Standard (ou version ultérieure)**: l’installation inclut SQL Server Integration Services.
* **Microsoft SQL Server 2014 ou 2016 Integration Services Feature Pack pour Azure**: ils peuvent être téléchargés, respectivement, à partir de hello [SQL Server 2014 Integration Services](http://www.microsoft.com/download/details.aspx?id=47366) et [intégration de SQL Server 2016 Services](https://www.microsoft.com/download/details.aspx?id=49492) pages.

> [!NOTE]
> SSIS est installé avec SQL Server, mais n’est pas inclus dans la version Express hello. Pour plus d'informations sur les applications incluses dans les différentes éditions de SQL Server, consultez [Éditions de SQL Server](http://www.microsoft.com/en-us/server-cloud/products/sql-server-editions/)
> 
> 

Pour les supports de formation sur SSIS, consultez la [formation pratique SSIS](http://www.microsoft.com/download/details.aspx?id=20766)

Pour plus d’informations sur la façon de tooget à distance à l’exécution à l’aide de SISS toobuild simple extraction, transformation et les packages de chargement (ETL), consultez [didacticiel SSIS : création d’un Package ETL Simple](https://msdn.microsoft.com/library/ms169917.aspx).

## <a name="download-nyc-taxi-dataset"></a>Télécharger l’ensemble de données Taxi NYC
Hello exemple décrit ici utiliser un jeu de données disponible publiquement--hello [NYC Taxi allers-retours](http://www.andresmh.com/nyctaxitrips/) jeu de données. Hello dataset se compose des trajets de taxi environ 173 millions dans NYC dans l’année hello 2013. Il existe deux types de données : les données détaillées relatives aux voyages et celles relatives aux tarifs des courses. Comme il existe un fichier par élément pour chaque mois, nous avons 24 fichiers, chacun d’eux d’un volume de 2 Go avant compression.

## <a name="upload-data-tooazure-blob-storage"></a>Télécharger le stockage d’objets blob de données tooAzure
données toomove à l’aide de hello SSIS du feature pack à partir du stockage d’objets blob tooAzure local, nous utilisons une instance de hello [ **tâche de chargement d’objets Blob Azure**](https://msdn.microsoft.com/library/mt146776.aspx), illustrée ici :

![configure-data-science-vm](./media/machine-learning-data-science-move-data-to-azure-blob-using-ssis/ssis-azure-blob-upload-task.png)

paramètres Hello hello utilise des tâches sont décrites ici :

| Champ | Description |
| --- | --- |
| **AzureStorageConnection** |Spécifie un gestionnaire de connexions de stockage Azure existant ou crée un nouveau qui fait référence le compte de stockage Azure tooan qui pointe de fichiers d’objets blob toowhere hello sont hébergés. |
| **BlobContainer** |Spécifie le nom hello du conteneur d’objets blob hello qui contiennent les fichiers hello téléchargé comme objet BLOB. |
| **BlobDirectory** |Spécifie le répertoire d’objets blob hello où hello du fichier téléchargé est stocké en tant qu’objet blob de blocs. répertoire d’objets blob Hello est une structure hiérarchique virtuelle. Si l’objet blob de hello existe déjà, il a ia remplacé. |
| **LocalDirectory** |Spécifie le répertoire local hello contenant hello toobe de fichiers téléchargé. |
| **FileName** |Spécifie un nom filtrer tooselect les fichiers avec le modèle de nom spécifié hello. Par exemple, MySheet\*.xls\* inclut des fichiers tels que MySheet001.xls et MySheetABC.xlsx |
| **TimeRangeFrom/TimeRangeTo** |Spécifie une plage de temps pour appliquer un filtre. Les fichiers modifiés après *TimeRangeFrom* et avant *TimeRangeTo* sont inclus. |

> [!NOTE]
> Hello **AzureStorageConnection** informations d’identification doivent toobe correct et hello **BlobContainer** doit exister avant la tentative de transfert de hello.
> 
> 

## <a name="download-data-from-azure-blob-storage"></a>Télécharger les données depuis le stockage d’objets blobs Azure
données toodownload à partir d’objets blob Azure tooon local de stockage avec SSIS, utilisez une instance de hello [tâche de chargement d’objets Blob Azure](https://msdn.microsoft.com/library/mt146779.aspx).

## <a name="more-advanced-ssis-azure-scenarios"></a>Scénarios SSIS-Azure plus élaborés
pack de fonctionnalités Hello SSIS permet plus complexe toobe flux géré par les tâches d’empaquetage ensemble. Par exemple, hello blob pourraient de flux de données directement dans un cluster HDInsight, dont la sortie peut être téléchargée tooa arrière blob et stockage local tooon. SSIS peut exécuter des tâches Hive et Pig sur un cluster HDInsight à l’aide de connecteurs SSIS supplémentaires :

* toorun du cluster avec SSIS, utilisez un script Hive sur un Azure HDInsight [tâche Hive](https://msdn.microsoft.com/library/mt146771.aspx).
* toorun du cluster avec SSIS, utilisez un script Pig sur un Azure HDInsight [tâche Pig Azure HDInsight](https://msdn.microsoft.com/library/mt146781.aspx).

