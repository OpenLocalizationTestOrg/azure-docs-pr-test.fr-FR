---
title: aaaUse Data Lake Store avec Hadoop dans HDInsight de Azure | Documents Microsoft
description: "Découvrez comment tooquery des données à partir d’Azure Data Lake Store et toostore des résultats de votre analyse."
keywords: "stockage d’objets blob, hdfs, données structurées, données non structurées, data lake store"
services: hdinsight,storage
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/03/2017
ms.author: jgao
ms.openlocfilehash: 89633218a37a2fe05043e05d61199dcc0252d7f0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-data-lake-store-with-azure-hdinsight-clusters"></a>Utiliser Data Lake Store avec des clusters Azure HDInsight

tooanalyze des données dans le cluster HDInsight, vous pouvez stocker les données de salutation soit dans [Azure Storage](../storage/common/storage-introduction.md), [Azure Data Lake Store](../data-lake-store/data-lake-store-overview.md), ou les deux. Les deux options de stockage permettent de supprimer toosafely que des clusters HDInsight qui sont utilisés pour le calcul sans perdre de données utilisateur.

Dans cet article, vous découvrez le fonctionnement de Data Lake Store avec des clusters HDInsight. toolearn comment le stockage Azure fonctionne avec les clusters HDInsight, consultez [utiliser le stockage Azure avec Azure HDInsight clusters](hdinsight-hadoop-use-blob-storage.md). Consultez la rubrique [Créer des clusters Hadoop dans HDInsight](hdinsight-hadoop-provision-linux-clusters.md) pour des informations sur la création d’un cluster HDInsight.

> [!NOTE]
> Data Lake Store est toujours accessible par le biais d’un canal sécurisé, donc il y a aucun nom de schéma de système de fichiers `adls`. Vous utilisez toujours `adl`.
> 
> 

## <a name="availabilities-for-hdinsight-clusters"></a>Disponibilités pour les clusters HDInsight

Hadoop prend en charge une notion hello par défaut du système de fichiers. système de fichiers par défaut Hello implique un schéma par défaut et une autorité. Il peut également être tooresolve utilisé des chemins d’accès relatifs. Pendant le processus de création de cluster HDInsight de hello, vous pouvez spécifier un conteneur d’objets blob dans le stockage Azure en tant que système de fichiers par défaut hello ou avec HDInsight 3.5 et les versions plus récentes, vous pouvez sélectionner le stockage Azure ou Azure Data Lake Store en tant que système de fichiers par défaut hello avec un quelques exceptions près. 

Les clusters HDInsight peuvent utiliser Data Lake Store de deux manières :

* En tant que stockage par défaut de hello
* Comme stockage supplémentaire, avec Azure Storage Blob comme stockage par défaut.

À partir de maintenant, seules certaines hello HDInsight cluster prise en charge des types/versions à l’aide de Data Lake Store comme stockage par défaut et les comptes de stockage supplémentaires :

| Type de cluster HDInsight | Data Lake Store comme stockage par défaut | Data Lake Store comme stockage supplémentaire| Remarques |
|------------------------|------------------------------------|---------------------------------------|------|
| HDInsight version 3.6 | Oui | Oui | |
| HDInsight version 3.5 | Oui | Oui | À l’exception de hello de HBase|
| HDInsight version 3.4 | Non | Oui | |
| HDInsight version 3.3 | Non | Non | |
| HDInsight version 3.2 | Non | Oui | |
| HDInsight Premium (couche)| Non | Non | |
| Storm | | |Vous pouvez utiliser les données de toowrite Data Lake Store à partir d’une topologie Storm. Vous pouvez également vous en servir pour stocker des données de référence qui peuvent ensuite être lues par une topologie Storm.|

À l’aide de Data Lake Store en tant qu’un compte de stockage supplémentaires ne pas affecter les performances ou hello capacité tooread ou d’écriture tooAzure stockage de cluster de hello.


## <a name="use-data-lake-store-as-default-storage"></a>Utiliser Data Lake Store comme stockage par défaut

Lorsque HDInsight est déployé avec Data Lake Store en tant que stockage par défaut, fichiers hello cluster sont stockés dans Data Lake Store Bonjour à l’emplacement suivant :

    adl://mydatalakestore/<cluster_root_path>/

où `<cluster_root_path>` hello désigne un dossier que vous créez dans Data Lake Store. En spécifiant un chemin d’accès racine pour chaque cluster, vous pouvez utiliser hello même compte Data Lake Store pour plusieurs clusters. Par conséquent, vous pouvez avoir une configuration dans laquelle :

* Cluster1 peut utiliser le chemin d’accès de hello`adl://mydatalakestore/cluster1storage`
* Cluster2 peut utiliser le chemin d’accès de hello`adl://mydatalakestore/cluster2storage`

Notez que les deux hello clusters utilisez hello même compte Data Lake Store **mydatalakestore**. Chaque cluster a accès tooits propre système de fichiers racine Data Lake Store. Hello expérience de déploiement du portail Azure en particulier vous invite toouse un nom de dossier comme **/clusters/\<nom_cluster >** pour le chemin d’accès racine de hello.

toouse en mesure de toobe un Data Lake Store en tant que stockage par défaut, vous devez accorder hello service principal l’accès toohello suivant des chemins d’accès :

- racine de compte Data Lake Store Hello.  Par exemple : adl://mydatalakestore/.
- dossier Hello pour tous les dossiers de cluster.  Par exemple : adl://mydatalakestore/clusters.
- dossier Hello pour le cluster de hello.  Par exemple : adl://mydatalakestore/clusters/cluster1storage.

Pour plus d’informations sur la création du principal de service et l’octroi de l’accès, consultez [Configure Data Lake store access](#configure-data-lake-store-access) (Configurer l’accès à Data Lake Store).


## <a name="use-data-lake-store-as-additional-storage"></a>Utiliser Data Lake Store comme stockage supplémentaire

Vous pouvez utiliser Data Lake Store en tant que stockage supplémentaire pour le cluster hello. Dans ce cas, du stockage par défaut hello cluster peut être un objet Blob de stockage Azure ou un compte Data Lake Store. Si vous exécutez les tâches HDInsight sur des données de hello stockées dans Data Lake Store en tant que stockage supplémentaire, vous devez utiliser des fichiers de toohello hello chemin qualifié complet. Par exemple :

    adl://mydatalakestore.azuredatalakestore.net/<file_path>

Notez qu’il existe aucune **cluster_root_path** dans l’URL de hello maintenant. C’est parce que Data Lake Store n’est pas un stockage par défaut dans ce cas vous devez toodo fournissent des fichiers de toohello hello chemin d’accès.

toouse en mesure de toobe un Data Lake Store en tant que stockage supplémentaire, vous devez uniquement toogrant hello service principal toohello chemins d’accès où sont stockés vos fichiers.  Par exemple :

    adl://mydatalakestore.azuredatalakestore.net/<file_path>

Pour plus d’informations sur la création du principal de service et l’octroi de l’accès, consultez [Configurer l’accès à Data Lake Store](#configure-data-lake-store-access).


## <a name="use-more-than-one-data-lake-store-accounts"></a>Utiliser plusieurs comptes Data Lake Store

Ajout d’un compte Data Lake Store comme supplémentaires et Data Lake Store plusieurs comptes sont effectuées en offrant une autorisation de cluster HDInsight hello sur les données de comptes Data Lake Store d’une ou plusieurs. Consultez [Configurer l’accès à Data Lake Store](#configure-data-lake-store-access).

## <a name="configure-data-lake-store-access"></a>Configurer l’accès aux données Data Lake Store

tooconfigure accès au magasin de LAC de données à partir de votre cluster HDInsight, vous devez disposer d’un principal du service Azure Active directory (Azure AD). Vous pouvez créer un principal de service uniquement si vous être administrateur Azure AD. principal du service Hello doit être créée avec un certificat. Pour plus d’informations, consultez [Configurer l’accès à Data Lake Store](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md#configure-data-lake-store-access), et [Create service principal with self-signed-certificate](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-self-signed-certificate) (Créer un principal du service avec un certificat auto-signé).

> [!NOTE]
> Si vous vous apprêtez toouse Azure Data Lake Store en tant que stockage supplémentaire pour le cluster HDInsight, nous vous recommandons vivement de procéder ainsi lorsque vous créez le cluster de hello comme décrit dans cet article. Ajout d’Azure Data Lake Store en tant que stockage supplémentaire tooan cluster HDInsight existant est un processus complexe et susceptible d’engendrer des tooerrors.
>

## <a name="access-files-from-hello-cluster"></a>Accéder aux fichiers à partir du cluster de hello

Il existe plusieurs méthodes que vous pouvez accéder à des fichiers hello Data Lake Store à partir d’un cluster HDInsight.

* **À l’aide du nom qualifié complet de hello**. Avec cette approche, vous fournissez le fichier de toohello hello chemin d’accès complet que vous souhaitez tooaccess.

        adl://mydatalakestore.azuredatalakestore.net/<cluster_root_path>/<file_path>

* **À l’aide du format de chemin d’accès raccourcie hello**. Avec cette approche, vous remplacez le chemin d’accès de hello jusqu'à la racine du cluster toohello avec adl : / / /. Par conséquent, dans l’exemple hello ci-dessus, vous pouvez remplacer `adl://mydatalakestore.azuredatalakestore.net/<cluster_root_path>/` avec `adl:///`.

        adl:///<file path>

* **À l’aide du chemin d’accès relatif de hello**. Avec cette approche, vous ne fournissez hello relatif au chemin toohello fichier que vous souhaitez tooaccess. Par exemple, si le fichier toohello hello chemin d’accès complet est :

        adl://mydatalakestore.azuredatalakestore.net/<cluster_root_path>/example/data/sample.log

    Vous pouvez accéder à hello même fichier exemple.log à l’aide de ce chemin d’accès relatif à la place.

        /example/data/sample.log

## <a name="create-hdinsight-clusters-with-access-toodata-lake-store"></a>Créer des clusters HDInsight avec accès tooData Lake Store

Utilisez hello suivant les liens pour obtenir des instructions détaillées sur comment toocreate des clusters HDInsight avec accès tooData Lake Store.

* [Utilisation du portail](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md)
* [Utilisation de PowerShell (avec Data Lake Store en tant que stockage par défaut)](../data-lake-store/data-lake-store-hdinsight-hadoop-use-powershell-for-default-storage.md)
* [Utilisation de PowerShell (avec Data Lake Store en tant que stockage supplémentaire)](../data-lake-store/data-lake-store-hdinsight-hadoop-use-powershell.md)
* [Utilisation de modèles Azure](../data-lake-store/data-lake-store-hdinsight-hadoop-use-resource-manager-template.md)


## <a name="next-steps"></a>Étapes suivantes
Dans cet article, vous avez appris comment toouse HDFS compatibles avec Azure Data Lake Store avec HDInsight. Cela vous permet de toobuild évolutive et à long terme, l’archivage des solutions d’acquisition de données et l’utilisation de HDInsight toounlock hello plus d’informations à l’intérieur de stockée hello structurées et les données non structurées.

Pour plus d'informations, consultez les pages suivantes :

* [Prise en main d’Azure HDInsight][hdinsight-get-started]
* [Prise en main d’Azure Data Lake Store](../data-lake-store/data-lake-store-get-started-portal.md)
* [Télécharger des données tooHDInsight][hdinsight-upload-data]
* [Utilisation de Hive avec HDInsight][hdinsight-use-hive]
* [Utilisation de Pig avec HDInsight][hdinsight-use-pig]
* [Utiliser des Signatures d’accès partagé Azure Storage toorestrict accès toodata avec HDInsight][hdinsight-use-sas]

[hdinsight-use-sas]: hdinsight-storage-sharedaccesssignature-permissions.md
[powershell-install]: /powershell/azureps-cmdlets-docs
[hdinsight-creation]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-pig]: hdinsight-use-pig.md

[blob-storage-restAPI]: http://msdn.microsoft.com/library/windowsazure/dd135733.aspx
[azure-storage-create]:../storage/common/storage-create-storage-account.md

[img-hdi-powershell-blobcommands]: ./media/hdinsight-hadoop-use-blob-storage/HDI.PowerShell.BlobCommands.png
[img-hdi-quick-create]: ./media/hdinsight-hadoop-use-blob-storage/HDI.QuickCreateCluster.png
[img-hdi-custom-create-storage-account]: ./media/hdinsight-hadoop-use-blob-storage/HDI.CustomCreateStorageAccount.png  
