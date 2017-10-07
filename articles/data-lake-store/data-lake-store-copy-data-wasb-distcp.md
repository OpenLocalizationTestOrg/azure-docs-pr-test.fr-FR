---
title: "tooand de données aaaCopy de WASB dans Data Lake Store à l’aide de Distcp | Documents Microsoft"
description: "Utilisez Distcp outil toocopy données tooand à partir d’objets BLOB de stockage Azure tooData Lake Store"
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: ae2e9506-69dd-4b95-8759-4dadca37ea70
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/29/2017
ms.author: nitinme
ms.openlocfilehash: ec23410bbab0f82449a475412bc3b097c4a8fccd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-distcp-toocopy-data-between-azure-storage-blobs-and-data-lake-store"></a>Utiliser des données de toocopy Distcp entre les objets BLOB de stockage Azure et Data Lake Store
> [!div class="op_single_selector"]
> * [Utilisation de DistCp](data-lake-store-copy-data-wasb-distcp.md)
> * [Utilisation d’AdlCopy](data-lake-store-copy-data-azure-storage-blob.md)
>
>

Une fois que vous avez créé un cluster HDInsight accès tooa un compte Data Lake Store, vous pouvez utiliser les outils d’écosystème de Hadoop comme des données de toocopy Distcp **tooand de** un stockage de cluster HDInsight (WASB) dans un compte Data Lake Store. Cet article fournit des instructions sur la façon de tooachieve cela.

## <a name="prerequisites"></a>Composants requis
Avant de commencer cet article, vous devez disposer de hello :

* **Un abonnement Azure**. Consultez la page [Obtention d’un essai gratuit d’Azure](https://azure.microsoft.com/pricing/free-trial/).
* **Un compte Azure Data Lake Store**. Pour obtenir des instructions sur la façon de voir d’un seul, toocreate [prise en main Azure Data Lake Store](data-lake-store-get-started-portal.md)
* **Cluster HDInsight Azure** avec accès tooa compte Data Lake Store. Voir [Créer un cluster HDInsight avec Data Lake Store](data-lake-store-hdinsight-hadoop-use-portal.md). Assurez-vous que vous activez Bureau à distance de cluster de hello.

## <a name="do-you-learn-fast-with-videos"></a>Les vidéos vous permettent-elles d’apprendre rapidement ?
[Regardez cette vidéo](https://mix.office.com/watch/1liuojvdx6sie) sur la façon de toocopy des données entre les objets BLOB de stockage Azure et à l’aide de DistCp Data Lake Store.

## <a name="use-distcp-from-an-hdinsight-linux-cluster"></a>Utiliser Distcp à partir d’un cluster HDInsight Linux

Un cluster HDInsight est fourni avec l’utilitaire de Distcp hello, qui peut être utilisés toocopy des données à partir de sources différentes dans un cluster HDInsight. Si vous avez configuré le cluster HDInsight de hello toouse Data Lake Store en tant qu’un stockage supplémentaire, hello Distcp utilitaire peut être utilisé out of box toocopy des tooand de données à partir d’un compte Data Lake Store. Dans cette section, nous examiner comment toouse hello Distcp utilitaire.

1. À partir de votre bureau, utilisez SSH tooconnect toohello cluster. Consultez [Connect tooa HDInsight de basés sur Linux cluster](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md). Exécuter des commandes hello à partir de l’invite de commandes hello SSH.

2. Vérifiez si vous avez accès hello objets BLOB de stockage Azure (WASB). Exécutez hello de commande suivante :

        hdfs dfs –ls wasb://<container_name>@<storage_account_name>.blob.core.windows.net/

    Il doit fournir une liste du contenu dans l’objet blob de stockage hello.
3. De même, vérifiez si vous pouvez accéder à hello compte Data Lake Store à partir du cluster de hello. Exécutez hello de commande suivante :

        hdfs dfs -ls adl://<data_lake_store_account>.azuredatalakestore.net:443/

    Il doit fournir une liste de fichiers/dossiers Bonjour compte Data Lake Store.
4. Utilisez des données toocopy Distcp WASB tooa compte Data Lake Store.

        hadoop distcp wasb://<container_name>@<storage_account_name>.blob.core.windows.net/example/data/gutenberg adl://<data_lake_store_account>.azuredatalakestore.net:443/myfolder

    Cette copie contenu hello Hello **/exemple données/gutenberg/** dossier dans WASB trop**/myfolder** Bonjour compte Data Lake Store.
5. De même, utilisez des données toocopy Distcp tooWASB du compte Data Lake Store.

        hadoop distcp adl://<data_lake_store_account>.azuredatalakestore.net:443/myfolder wasb://<container_name>@<storage_account_name>.blob.core.windows.net/example/data/gutenberg

    Cette copie contenu hello du **/myfolder** Bonjour Data Lake Store compte trop**/exempledonnées/gutenberg/** dossier dans WASB.

## <a name="performance-considerations-while-using-distcp"></a>Considérations de performances lors de l’utilisation de DistCp

DistCp's la plus faible granularité est un fichier unique, définition hello maximal du nombre de copies simultanées est hello plus importantes paramètre toooptimize sur Data Lake Store. Cela est contrôlé en définissant le nombre de hello de mappeurs (am ») le paramètre de ligne de commande hello. Ce paramètre spécifie le nombre maximal de hello de mappeurs qui sera utilisé toocopy données. La valeur par défaut est 20.

**Exemple**

    hadoop distcp wasb://<container_name>@<storage_account_name>.blob.core.windows.net/example/data/gutenberg adl://<data_lake_store_account>.azuredatalakestore.net:443/myfolder -m 100

### <a name="how-do-i-determine-hello-number-of-mappers-toouse"></a>Comment déterminer le nombre de hello de mappeurs toouse ?

Voici quelques conseils à suivre.

* **Étape 1 : Déterminer la quantité totale de mémoire fils** -hello première étape consiste cluster toodetermine hello fils mémoire toohello disponible sur lequel vous exécutez la tâche de DistCp hello. Ces informations sont disponibles dans le portail de Ambari hello associé hello cluster. Accédez tooYARN et afficher hello configurations onglet toosee hello fils de mémoire. tooget hello fils mémoire totale, multiplication hello mémoire fils par nœud en nombre hello de nœuds dont vous disposez dans votre cluster.

* **Étape 2 : Calculer le nombre de hello de mappeurs** -hello valeur **m** est le quotient de toohello égal totale de mémoire fils divisée par la taille du conteneur fils de hello. Hello, les informations de taille de conteneur fils est disponible dans le portail de Ambari hello ainsi. Accédez tooYARN et vue Bonjour configurations onglet Bonjour taille du conteneur fils est affiché dans cette fenêtre. Hello tooarrive équation au nombre de hello de mappeurs (**m**) est

        m = (number of nodes * YARN memory for each node) / YARN container size

**Exemple**

Supposons que vous avez un 4 nœuds D14v2s dans un cluster de hello et que vous essayez de tootransfer 10 To de données à partir de 10 différents dossiers. Chacun des dossiers de hello contiennent différentes quantités de données et tailles de fichier hello dans chaque dossier sont différents.

* Mémoire totale de fils - de hello portail Ambari vous déterminez que hello mémoire des fils est 96 Go pour un nœud D14. Ainsi, la mémoire YARN totale pour un cluster à 4 nœuds est : 

        YARN memory = 4 * 96GB = 384GB

* Nombre de mappeurs - de hello portail Ambari vous déterminez que taille de conteneur fils hello est 3072 pour un nœud de cluster D14. Par conséquent, le nombre de mappeurs est :

        m = (4 nodes * 96GB) / 3072MB = 128 mappers

Si d’autres applications utilisent la mémoire, puis vous pouvez choisir tooonly utiliser une partie de la mémoire des fils de votre cluster pour DistCp.

### <a name="copying-large-datasets"></a>Copie de jeux de données volumineux

Lorsque la taille de hello de hello dataset toobe déplacées sont très volumineux (par exemple, > 1 To) ou si vous avez de nombreux dossiers, vous devez envisager d’utiliser plusieurs travaux DistCp. Il n’existe probablement aucun gain de performance, mais il distribuent les tâches de hello afin que si un travail échoue, il vous suffit toorestart cette tâche spécifique plutôt que de projet hello.

### <a name="limitations"></a>Limites

* DistCp essaie mappeurs toocreate qui ont des performances de toooptimize de taille. Augmenter le nombre hello de mappeurs pas toujours augmente les performances.

* DistCp est limité tooonly l’une mappeur par fichier. Par conséquent, vous ne devez pas avoir plus de mappeurs que de fichiers. Étant donné que DistCp affecter uniquement un mappeur tooa fichier, cela limite hello d’accès concurrentiel qui peut être utilisés toocopy des fichiers volumineux.

* Si vous avez un petit nombre de fichiers volumineux, vous devez fractionner les dans toogive de segments de fichier de 256 Mo vous plus de concurrence potentielle. 
 
* Si vous copiez à partir d’un compte de stockage d’objets Blob Azure, votre travail de copie peut être limité sur le côté de stockage d’objets blob hello. Cela sera dégrader les performances de hello de votre travail de copie. toolearn savoir plus sur les limites de hello de stockage d’objets Blob Azure, consultez les limites de stockage Azure à [abonnement Azure et limites de service](../azure-subscription-service-limits.md).

## <a name="see-also"></a>Voir aussi
* [Copier des données d’objets BLOB de stockage Azure tooData Lake Store](data-lake-store-copy-data-azure-storage-blob.md)
* [Sécuriser les données dans Data Lake Store](data-lake-store-secure-data.md)
* [Utiliser Azure Data Lake Analytics avec Data Lake Store](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [Utiliser Azure HDInsight avec Data Lake Store](data-lake-store-hdinsight-hadoop-use-portal.md)
