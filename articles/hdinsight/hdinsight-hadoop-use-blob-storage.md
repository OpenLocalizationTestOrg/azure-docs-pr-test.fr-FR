---
title: "aaaQuery des données à partir de HDFS compatible avec le stockage Azure - Azure HDInsight | Documents Microsoft"
description: "Découvrez comment tooquery les données de stockage Azure et d’Azure Data Lake Store toostore des résultats de votre analyse."
keywords: "stockage blob,hdfs,données structurées,données non structurées,data lake store,entrée Hadoop,sortie Hadoop,stockage hadoop,entrée hdfs,sortie hdfs,stockage hdfs, wasb azure"
services: hdinsight,storage
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 1d2e65f2-16de-449e-915f-3ffbc230f815
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/09/2017
ms.author: jgao
ms.openlocfilehash: 1032d60424b65e3c0c54a25c7c15970b017a788f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-storage-with-azure-hdinsight-clusters"></a>Utiliser le stockage Azure avec des clusters Azure HDInsight

tooanalyze des données dans le cluster HDInsight, vous pouvez stocker des données de hello dans le stockage Azure, Azure Data Lake Store ou les deux. Les deux options de stockage permettent de supprimer toosafely que des clusters HDInsight qui sont utilisés pour le calcul sans perdre de données utilisateur.

Hadoop prend en charge une notion hello par défaut du système de fichiers. système de fichiers par défaut Hello implique un schéma par défaut et une autorité. Il peut également être tooresolve utilisé des chemins d’accès relatifs. Au cours de hello processus de création du cluster HDInsight, vous pouvez spécifier un conteneur d’objets blob dans le stockage Azure en tant que système de fichiers par défaut hello ou avec HDInsight 3.5, vous pouvez sélectionner le stockage Azure ou Azure Data Lake Store en tant que système de fichiers par défaut hello à quelques exceptions près. Pour la prise en charge de hello de l’utilisation de Data Lake Store comme valeur par défaut hello et de stockage, consultez [disponibilités pour le cluster HDInsight](./hdinsight-hadoop-use-data-lake-store.md#availabilities-for-hdinsight-clusters).

Dans cet article, vous découvrez le fonctionnement du stockage Azure avec des clusters HDInsight. toolearn Data Lake Store fonctionnement avec les clusters HDInsight, consultez [utilisez Azure Data Lake Store avec Azure HDInsight clusters](hdinsight-hadoop-use-data-lake-store.md). Consultez la rubrique [Créer des clusters Hadoop dans HDInsight](hdinsight-hadoop-provision-linux-clusters.md) pour des informations sur la création d’un cluster HDInsight.

Le stockage Azure est une solution de stockage à la fois robuste et polyvalente qui s’intègre en toute transparence à HDInsight. HDInsight peut utiliser un conteneur d’objets blob dans le stockage Azure en tant que système de fichiers par défaut hello pour le cluster de hello. Via une interface (HDFS) de système de fichiers distribués Hadoop, ensemble de hello de composants dans HDInsight peut fonctionner directement sur les données structurées ou non structurées stockées en tant qu’objets BLOB.

> [!WARNING]
> Plusieurs options sont disponibles lors de la création d’un compte de stockage Azure. Hello tableau suivant fournit des informations sur les options sont prises en charge avec HDInsight :
> 
> | Type de compte de stockage | Niveau de stockage | Pris en charge avec HDInsight |
> | ------- | ------- | ------- |
> | Compte de stockage à usage général | Standard | __Oui__ |
> | &nbsp; | Premium | Non |
> | Compte de stockage d’objets blob | À chaud | Non |
> | &nbsp; | À froid | Non |

Nous vous déconseillons d’utiliser le conteneur d’objets blob hello par défaut pour le stockage des données d’entreprise. La suppression du conteneur d’objets blob par défaut hello après chaque tooreduce utilisez coût de stockage est une bonne pratique. Notez que le conteneur par défaut hello contient des applications et du système des journaux. Vérifiez les journaux hello tooretrieve vraiment avant de supprimer le conteneur de hello.

Le partage d’un conteneur d’objets blob sur plusieurs clusters n’est pas pris en charge.

## <a name="hdinsight-storage-architecture"></a>Architecture de stockage HDInsight
Hello suivant schéma fournit une vue abstraite de hello HDInsight architecture de stockage de l’utilisation du stockage Azure :

![Clusters Hadoop utilisent hello HDFS API tooaccess et stocker des données structurées et non structurées dans le stockage Blob. ] (./media/hdinsight-hadoop-use-blob-storage/HDI.WASB.Arch.png "L’Architecture de stockage de HDInsight")

HDInsight fournit le système de fichiers accès toohello distribué est localement attaché toohello les nœuds de calcul. Ce système de fichiers sont accessibles à l’aide de hello complet URI, par exemple :

    hdfs://<namenodehost>/<path>

En outre, HDInsight vous permet de tooaccess les données stockées dans le stockage Azure. syntaxe de Hello est :

    wasb[s]://<containername>@<accountname>.blob.core.windows.net/<path>

Voici des points à prendre en compte lorsque vous utilisez un compte de stockage Azure avec des clusters HDInsight.

* **Conteneurs dans des comptes de stockage hello qui sont connectés tooa cluster :** étant hello nom et une clé associés hello cluster lors de la création, vous avez les objets BLOB de toohello un accès complet dans ces conteneurs.

* **Conteneurs publics ou des objets BLOB publics dans les comptes de stockage qui ne sont pas connectés tooa cluster :** vous disposez des autorisations en lecture seule toohello des objets BLOB des conteneurs de hello.
  
  > [!NOTE]
  > Conteneurs publics autorisent tooget une liste de tous les objets BLOB qui sont disponibles dans le conteneur et d’obtenir les métadonnées de conteneur. Objets BLOB publics permettre de BLOB de hello tooaccess uniquement si vous connaissez l’URL exacte hello. Pour plus d’informations, consultez <a href="http://msdn.microsoft.com/library/windowsazure/dd179354.aspx">restreindre l’accès toocontainers et les objets BLOB</a>.
  > 
  > 
* **Les conteneurs privés dans des comptes de stockage qui ne sont pas connectés tooa cluster :** BLOB hello dans les conteneurs hello n’est pas accessible, sauf si vous définissez le compte de stockage hello lorsque vous envoyez des travaux de WebHCat hello. Une explication sera fournie plus loin dans cet article.

les comptes de stockage Hello qui sont définies dans le processus de création de hello et leurs clés sont stockées dans %HADOOP_HOME%/conf/core-site.xml sur les nœuds de cluster hello. comportement par défaut de Hello de HDInsight est définis dans le fichier de base-site.XML hello les comptes de stockage toouse hello. Vous pouvez modifier ce paramètre avec [Ambari](./hdinsight-hadoop-manage-ambari.md).

Plusieurs tâches WebHCat, notamment Hive, MapReduce, la diffusion en continu Hadoop et Pig, peuvent véhiculer avec elles une description des comptes de stockage et des métadonnées. (cela fonctionne actuellement pour Pig, pour les comptes de stockage, mais pas pour les métadonnées.) Pour plus d'informations, consultez la page [Utilisation d'un cluster HDInsight avec des comptes de stockage et des metastores secondaires](http://social.technet.microsoft.com/wiki/contents/articles/23256.using-an-hdinsight-cluster-with-alternate-storage-accounts-and-metastores.aspx).

Les objets blob peuvent être utilisés pour les données structurées et non structurées. Les conteneurs d’objets blob stockent des données en tant que paires clé/valeur et sans hiérarchie de répertoires. Toutefois, le caractère de barre oblique hello (/) peut être utilisé dans hello toomake nom de la clé il apparaît comme si un fichier est stocké dans une structure de répertoire. Par exemple, une clé d'objet blob peut être *input/log1.txt*. Ne réel *d’entrée* répertoire existe, mais en raison de la présence de toohello du caractère de barre oblique hello dans le nom de la clé hello, il semble hello un chemin d’accès de fichier.

## <a id="benefits"></a>Avantages du stockage Azure
Hello implicite de coût de performance de pas colocaliser des clusters de calcul et des ressources de stockage est atténuée par moyen hello clusters de calcul hello sont créés les ressources de compte de stockage toohello fermer à l’intérieur de hello région Azure, où le réseau à grande vitesse hello permet efficace pour les nœuds de calcul hello tooaccess hello des données dans le stockage Azure.

Il existe plusieurs avantages associés au stockage des données de salutation dans le stockage Azure au lieu de HDFS :

* **Partage et la réutilisation des données :** données hello dans HDFS se trouve à l’intérieur du cluster de calcul hello. Seules les applications hello qui ont accès toohello compute cluster permettre utiliser des données de hello en utilisant les API de HDFS. données de Hello dans le stockage Azure sont accessibles par le biais hello HDFS API ou hello [API REST de stockage Blob][blob-storage-restAPI]. Par conséquent, un ensemble plus important d’applications (y compris les autres clusters HDInsight) et les outils permettre être utilisé tooproduce et consommer des données de la hello.
* **L’archivage des données :** le stockage des données dans le stockage Azure permet de clusters HDInsight de hello utilisés pour toobe calcul supprimé en toute sécurité sans perdre de données utilisateur.
* **Coût de stockage de données :** le stockage des données dans DFS pour hello à long terme est plus coûteuse que le stockage des données de salutation dans le stockage Azure, car le coût de hello d’un cluster de calcul est supérieur à coût hello de stockage Azure. En outre, étant donné que les données de salutation n’ayant pas de toobe rechargé pour chaque génération de cluster de calcul, vous enregistrez également les coûts de chargement des données.
* **Montée en puissance parallèle élastique :** HDFS bien que vous fournit un système de fichiers de montée en charge, la montée en puissance hello est déterminée par le nombre de hello de nœuds que vous créez pour votre cluster. Modification de l’échelle de hello peut devenir un processus plus complexe que partie de confiance sur élastique hello mise à l’échelle les fonctionnalités que vous obtenez automatiquement dans le stockage Azure.
* **Géoréplication :** vous pouvez géo-répliquer votre stockage Azure. Bien que cela vous donne la redondance des données et récupération géographique, un emplacement géorépliqué de basculement toohello affecte sérieusement les performances de vos, et il peut entraîner des frais supplémentaires. Notre recommandation est toochoose hello géo-réplication avec soin et uniquement si la valeur de données de hello hello est la valeur hello coût supplémentaire.

Certaines tâches MapReduce et les packages peuvent créer des résultats intermédiaires que vous ne souhaitez pas vraiment toostore dans le stockage Azure. Dans ce cas, vous pouvez choisir les données hello toostore hello HDFS local. En fait, HDInsight utilise DFS pour plusieurs de ces résultats intermédiaires dans les tâches Hive et d'autres processus.

> [!NOTE]
> La plupart des commandes HDFS (par exemple <b>ls</b>, <b>copyFromLocal</b> et <b>mkdir</b>) fonctionnent toujours comme prévu. Hello uniquement les commandes qui sont spécifiques toohello HDFS implémentation native (qui est référencé tooas DFS) comme <b>fschk</b> et <b>dfsadmin</b>, afficher un comportement différent dans le stockage Azure.
> 
> 

## <a name="create-blob-containers"></a>Création de conteneurs d’objets blob
objets BLOB toouse, tout d’abord créer un [compte de stockage Azure][azure-storage-create]. Ce cadre, vous spécifiez une région Azure où le compte de stockage hello est créé. cluster de Hello et compte de stockage hello doivent être hébergés dans hello même région. Hello Hive le magasin de métadonnées SQL Server et SQL Server, base de données doit également se trouver dans le magasin de métadonnées Oozie hello même région.

Partout où il réside, chaque objet blob que vous créez appartient conteneur tooa dans votre compte de stockage Azure. Ce conteneur peut être un objet blob existant créé hors de HDInsight ou un conteneur créé pour un cluster HDInsight.

conteneur d’objets Blob par défaut Hello stocke les informations de cluster spécifiques telles que l’historique des travaux et des journaux. Ne partagez pas un conteneur d’objets blob par défaut avec plusieurs clusters HDInsight. Cela est susceptible d’endommager l’historique des travaux. Il est recommandé de toouse un conteneur différent pour chaque cluster et placer des données partagées sur un compte de stockage spécifié dans le déploiement de toutes les clusters au lieu du compte de stockage par défaut hello. Pour plus d'informations sur la configuration des comptes de stockage liés, consultez la rubrique [Création de clusters HDInsight][hdinsight-creation]. Toutefois, vous pouvez réutiliser un conteneur de stockage par défaut une fois le cluster de HDInsight hello d’origine a été supprimé. Pour des clusters HBase, vous pouvez réellement conserver les données et le schéma de la table HBase hello en créant un nouveau cluster HBase à l’aide du conteneur d’objets blob hello par défaut est utilisé par un cluster HBase qui a été supprimé.

[!INCLUDE [secure-transfer-enabled-storage-account](../../includes/hdinsight-secure-transfer.md)]

### <a name="use-hello-azure-portal"></a>Utilisez hello portail Azure
Lorsque vous créez un cluster HDInsight à partir de hello Portal, vous avez hello options (comme indiqué ci-dessous) tooprovide hello compte de stockage détails. Vous pouvez également spécifier si vous souhaitez un compte de stockage supplémentaires associées au cluster de hello et dans ce cas, choisissez Data Lake Store ou un autre objet blob de stockage Azure en tant qu’espace de stockage supplémentaire hello.

![source de données de création hadoop HDInsight](./media/hdinsight-hadoop-use-blob-storage/hdinsight.provision.data.source.png)

> [!WARNING]
> À l’aide d’un compte de stockage supplémentaire dans un emplacement autre que le cluster HDInsight de hello n’est pas pris en charge.


### <a name="use-azure-powershell"></a>Utilisation d'Azure PowerShell
Si vous [installé et configuré Azure PowerShell][powershell-install], vous pouvez utiliser hello suivant toocreate invite de PowerShell Azure hello un compte de stockage et un conteneur :

[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell.md)]

    $SubscriptionID = "<Your Azure Subscription ID>"
    $ResourceGroupName = "<New Azure Resource Group Name>"
    $Location = "EAST US 2"

    $StorageAccountName = "<New Azure Storage Account Name>"
    $containerName = "<New Azure Blob Container Name>"

    Add-AzureRmAccount
    Select-AzureRmSubscription -SubscriptionId $SubscriptionID

    # Create resource group
    New-AzureRmResourceGroup -name $ResourceGroupName -Location $Location

    # Create default storage account
    New-AzureRmStorageAccount -ResourceGroupName $ResourceGroupName -Name $StorageAccountName -Location $Location -Type Standard_LRS 

    # Create default blob containers
    $storageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -StorageAccountName $StorageAccountName)[0].Value
    $destContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey  
    New-AzureStorageContainer -Name $containerName -Context $destContext

### <a name="use-azure-cli"></a>Utiliser l’interface de ligne de commande Microsoft Azure

[!INCLUDE [use-latest-version](../../includes/hdinsight-use-latest-cli.md)]

Si vous avez [installé et configuré hello CLI d’Azure](../cli-install-nodejs.md), suivants de hello commande peut être compte de stockage tooa utilisé et le conteneur.

    azure storage account create <storageaccountname> --type LRS

> [!NOTE]
> Hello `--type` paramètre indique la manière dont le compte de stockage hello est répliquée. Pour plus d'informations, consultez [Réplication Azure Storage](../storage/storage-redundancy.md). N’utilisez pas le stockage redondant dans une zone (ZRS), car ZRS ne prend pas en charge les objets blob de pages, les fichiers, les tables ni les files d’attente.
> 
> 

Vous êtes toospecify demandées hello région que le compte de stockage hello est créé dans. Vous devez créer le compte de stockage hello Bonjour même région que vous prévoyez sur la création de votre cluster HDInsight.

Une fois que le compte de stockage hello est créé, utilisez hello suivant des clés de compte de stockage commande tooretrieve hello :

    azure storage account keys list <storageaccountname>

toocreate un conteneur, utilisez hello de commande suivante :

    azure storage container create <containername> --account-name <storageaccountname> --account-key <storageaccountkey>

## <a name="address-files-in-azure-storage"></a>Adressage des fichiers dans le stockage Azure
schéma d’URI Hello pour accéder aux fichiers dans le stockage Azure à partir de HDInsight est :

    wasb[s]://<BlobStorageContainerName>@<StorageAccountName>.blob.core.windows.net/<path>

schéma d’URI Hello fournit un accès non chiffrés (avec hello *wasb :* préfixe) et SSL chiffrée accès (avec *wasbs*). Nous vous recommandons d’utiliser *wasbs* dans la mesure du possible, même lorsque l’accès aux données qui réside à l’intérieur de hello même région dans Azure.

Hello &lt;BlobStorageContainerName&gt; identifie le nom de hello du conteneur d’objets blob hello dans le stockage Azure.
Hello &lt;StorageAccountName&gt; identifie le nom de compte de stockage Azure hello. Un nom de domaine complet (FQDN) est requis.

Si ni &lt;BlobStorageContainerName&gt; ni &lt;StorageAccountName&gt; a été spécifié, système de fichiers par défaut hello est utilisé. Pour les fichiers hello sur le système de fichiers par défaut hello, vous pouvez utiliser un chemin d’accès relatif ou un chemin d’accès absolu. Par exemple, hello *hadoop-mapreduce-Examples.jar* fichier fourni avec les clusters HDInsight peut être tooby référencé à l’aide de valeurs hello suivantes :

    wasb://mycontainer@myaccount.blob.core.windows.net/example/jars/hadoop-mapreduce-examples.jar
    wasb:///example/jars/hadoop-mapreduce-examples.jar
    /example/jars/hadoop-mapreduce-examples.jar

> [!NOTE]
> nom de fichier Hello est <i>hadoop-Examples.jar</i> dans les clusters HDInsight versions 2.1 et version 1.6.
> 
> 

Hello &lt;chemin d’accès&gt; est hello fichier ou répertoire HDFS chemin d’accès. Comme les conteneurs dans le stockage Azure constituent simplement un magasin de clé-valeur, il n’y a pas de système de fichiers hiérarchique. Une barre oblique (« / ») à l'intérieur d'une clé d'objet blob est interprétée comme un séparateur de répertoire. Par exemple, les nom d’objet blob hello pour *hadoop-mapreduce-Examples.jar* est :

    example/jars/hadoop-mapreduce-examples.jar

> [!NOTE]
> Lorsque vous travaillez avec des objets BLOB en dehors de HDInsight, la plupart des utilitaires ne pas reconnaître le format WASB hello et à la place attendent un format de chemin d’accès de base, telles que `example/jars/hadoop-mapreduce-examples.jar`.
> 
> 

## <a name="access-blobs"></a>Accéder aux objets BLOB 


### <a name="access-blobs-using-azure-powershell"></a> Utiliser Azure PowerShell
> [!NOTE]
> commandes Hello dans cette section fournissent un exemple de base de l’utilisation de PowerShell tooaccess données est stockées dans des objets BLOB. Pour obtenir un exemple plus complet qui est personnalisé pour travailler avec HDInsight, consultez hello [outils HDInsight](https://github.com/Blackmist/hdinsight-tools).
> 
> 

Utilisez hello suivant commande toolist hello blob applets de commande :

    Get-Command *blob*

![Liste des cmdlets PowerShell relatives aux objets blob.][img-hdi-powershell-blobcommands]

#### <a name="upload-files"></a>Charger des fichiers
Consultez [télécharger des données tooHDInsight][hdinsight-upload-data].

#### <a name="download-files"></a>Téléchargement de fichiers
Hello script suivant télécharge un bloc blob toohello le dossier actuel. Avant d’exécuter le script hello, modifiez hello tooa répertoire où vous disposez des autorisations en écriture.

    $resourceGroupName = "<AzureResourceGroupName>"
    $storageAccountName = "<AzureStorageAccountName>"   # hello storage account used for hello default file system specified at creation.
    $containerName = "<BlobStorageContainerName>"  # hello default file system container has hello same name as hello cluster.
    $blob = "example/data/sample.log" # hello name of hello blob toobe downloaded.

    # Use Add-AzureAccount if you haven't connected tooyour Azure subscription
    Login-AzureRmAccount 
    Select-AzureRmSubscription -SubscriptionID "<Your Azure Subscription ID>"

    Write-Host "Create a context object ... " -ForegroundColor Green
    $storageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -Name $storageAccountName)[0].Value
    $storageContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey  

    Write-Host "Download hello blob ..." -ForegroundColor Green
    Get-AzureStorageBlobContent -Container $ContainerName -Blob $blob -Context $storageContext -Force

    Write-Host "List hello downloaded file ..." -ForegroundColor Green
    cat "./$blob"

Fournir le nom de groupe de ressources hello et nom du cluster hello, vous pouvez utiliser hello suivant de code :

    $resourceGroupName = "<AzureResourceGroupName>"
    $clusterName = "<HDInsightClusterName>"
    $blob = "example/data/sample.log" # hello name of hello blob toobe downloaded.

    $cluster = Get-AzureRmHDInsightCluster -ResourceGroupName $resourceGroupName -ClusterName $clusterName
    $defaultStorageAccount = $cluster.DefaultStorageAccount -replace '.blob.core.windows.net'
    $defaultStorageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -Name $defaultStorageAccount)[0].Value
    $defaultStorageContainer = $cluster.DefaultStorageContainer
    $storageContext = New-AzureStorageContext -StorageAccountName $defaultStorageAccount -StorageAccountKey $defaultStorageAccountKey 

    Write-Host "Download hello blob ..." -ForegroundColor Green
    Get-AzureStorageBlobContent -Container $defaultStorageContainer -Blob $blob -Context $storageContext -Force


#### <a name="delete-files"></a>Supprimer des fichiers
    Remove-AzureStorageBlob -Container $containerName -Context $storageContext -blob $blob

#### <a name="list-files"></a>Énumérer des fichiers
    Get-AzureStorageBlob -Container $containerName -Context $storageContext -prefix "example/data/"

#### <a name="run-hive-queries-using-an-undefined-storage-account"></a>Exécution de requêtes Hive à l'aide d'un compte de stockage non défini
Cet exemple montre comment toolist un dossier à partir du compte de stockage qui n’est pas défini au cours de hello le processus de création.
$clusterName = "<HDInsightClusterName>"

    $undefinedStorageAccount = "<UnboundedStorageAccountUnderTheSameSubscription>"
    $undefinedContainer = "<UnboundedBlobContainerAssociatedWithTheStorageAccount>"

    $undefinedStorageKey = Get-AzureStorageKey $undefinedStorageAccount | %{ $_.Primary }

    Use-AzureRmHDInsightCluster $clusterName

    $defines = @{}
    $defines.Add("fs.azure.account.key.$undefinedStorageAccount.blob.core.windows.net", $undefinedStorageKey)

    Invoke-AzureRmHDInsightHiveJob -Defines $defines -Query "dfs -ls wasb://$undefinedContainer@$undefinedStorageAccount.blob.core.windows.net/;"

### <a name="use-azure-cli"></a>Utiliser l’interface de ligne de commande Microsoft Azure
Utilisez hello suivant de commandes toolist hello dépendant de l’objet blob de commandes :

    azure storage blob

**Exemple d’utilisation de le tooupload CLI d’Azure un fichier**

    azure storage blob upload <sourcefilename> <containername> <blobname> --account-name <storageaccountname> --account-key <storageaccountkey>

**Exemple d’utilisation de le toodownload CLI d’Azure un fichier**

    azure storage blob download <containername> <blobname> <destinationfilename> --account-name <storageaccountname> --account-key <storageaccountkey>

**Exemple d’utilisation de Azure CLI toodelete un fichier**

    azure storage blob delete <containername> <blobname> --account-name <storageaccountname> --account-key <storageaccountkey>

**Exemple d’utilisation de fichiers de toolist CLI d’Azure**

    azure storage blob list <containername> <blobname|prefix> --account-name <storageaccountname> --account-key <storageaccountkey>

## <a name="use-additional-storage-accounts"></a>Utiliser des comptes de stockage supplémentaires

Lors de la création d’un cluster HDInsight, vous permet de spécifier hello Azure Storage compte tooassociate avec lui. En outre toothis compte de stockage, vous pouvez ajouter plu les comptes de stockage à partir de hello même abonnement Azure ou différents abonnements Azure pendant le processus de création de hello ou après la création d’un cluster. Pour en savoir plus sur l'ajout de comptes de stockage supplémentaires, consultez la rubrique [Création de clusters HDInsight](hdinsight-hadoop-provision-linux-clusters.md).

> [!WARNING]
> À l’aide d’un compte de stockage supplémentaire dans un emplacement autre que le cluster HDInsight de hello n’est pas pris en charge.

## <a name="next-steps"></a>Étapes suivantes
Dans cet article, vous avez appris comment toouse HDFS compatible avec le stockage Azure avec HDInsight. Cela vous permet de toobuild évolutive et à long terme, l’archivage des solutions d’acquisition de données et l’utilisation de HDInsight toounlock hello plus d’informations à l’intérieur de stockée hello structurées et les données non structurées.

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
