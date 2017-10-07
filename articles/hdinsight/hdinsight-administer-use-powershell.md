---
title: les clusters aaaManage Hadoop dans HDInsight avec PowerShell - Azure | Documents Microsoft
description: "Découvrez comment tooperform administration tâches pour hello clusters Hadoop dans HDInsight à l’aide d’Azure PowerShell."
services: hdinsight
editor: cgronlun
manager: jhubbard
tags: azure-portal
author: mumian
documentationcenter: 
ms.assetid: bfdfa754-18e5-4ef9-b0d6-2dbdcebc0283
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ms.openlocfilehash: 3df082d752fa8c703db82a54b82b740290af6729
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-hadoop-clusters-in-hdinsight-by-using-azure-powershell"></a>Gestion des clusters Hadoop dans HDInsight au moyen d’Azure PowerShell
[!INCLUDE [selector](../../includes/hdinsight-portal-management-selector.md)]

Azure PowerShell est un environnement de script puissant que vous pouvez utiliser toocontrol et automatiser le déploiement de hello et la gestion de vos charges de travail dans Azure. Dans cet article, vous allez apprendre comment utilisent des clusters Hadoop de toomanage dans Azure HDInsight à l’aide d’une console Azure PowerShell locale via hello de Windows PowerShell. Pour la liste hello Hello applets de commande HDInsight PowerShell, consultez [référence d’applet de commande HDInsight][hdinsight-powershell-reference].

**Configuration requise**

Avant de commencer cet article, vous devez disposer de hello :

* **Un abonnement Azure**. Consultez la page [Obtention d’un essai gratuit d’Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).

## <a name="install-azure-powershell"></a>Installation d'Azure PowerShell
[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell.md)]

Si vous avez installé Azure PowerShell version 0.9x, vous devez le désinstaller avant d’installer une version plus récente.

version de hello toocheck de hello installé PowerShell :

    Get-Module *azure*

toouninstall hello ancienne version, exécuter des programmes et fonctionnalités dans le panneau de configuration hello.

## <a name="create-clusters"></a>Créer des clusters
Consultez la page [Créer des clusters basés sur Linux dans HDInsight à l’aide d’Azure PowerShell](hdinsight-hadoop-create-linux-clusters-azure-powershell.md)

## <a name="list-clusters"></a>Énumérer les clusters
Utilisez hello suivant toolist de commande tous les clusters dans l’abonnement actif de hello :

    Get-AzureRmHDInsightCluster

## <a name="show-cluster"></a>Afficher le cluster
Utilisez hello les détails de tooshow de commande d’un cluster spécifique dans l’abonnement actif de hello suivants :

    Get-AzureRmHDInsightCluster -ClusterName <Cluster Name>

## <a name="delete-clusters"></a>Suppression des clusters
Utilisez hello suivant commande toodelete un cluster :

    Remove-AzureRmHDInsightCluster -ClusterName <Cluster Name>

Vous pouvez également supprimer un cluster en supprimant le groupe de ressources hello contient hello cluster. Notez cette opération supprimera toutes les ressources hello groupe hello, y compris le compte de stockage par défaut hello.

    Remove-AzureRmResourceGroup -Name <Resource Group Name>

## <a name="scale-clusters"></a>Mise à l’échelle des clusters
cluster Hello fonctionnalité de mise à l’échelle permet un nombre de hello toochange de nœuds de travail utilisé par un cluster qui s’exécute dans Azure HDInsight sans avoir toore-créer le cluster de hello.

> [!NOTE]
> Seuls les clusters ayant la version 3.1.3 de HDInsight ou une version ultérieure sont pris en charge. Si vous ne savez pas de version hello de votre cluster, vous pouvez vérifier la page de propriétés hello.  Voir [Énumération et affichage des clusters](hdinsight-administer-use-portal-linux.md#list-and-show-clusters).
>
>

impact Hello modifiant nombre hello de nœuds de données pour chaque type de cluster pris en charge par HDInsight :

* Hadoop

    Vous pouvez augmenter de façon transparente nombre hello de nœuds de travail dans un cluster Hadoop qui est en cours d’exécution sans impact sur toutes les tâches en attente ou en cours d’exécution. Nouvelles tâches peuvent également être soumises pendant que l’opération de hello est en cours. Échecs dans une opération de mise à l’échelle sont correctement gérés afin que hello cluster est toujours conservé dans un état fonctionnel.

    Lorsqu’un cluster Hadoop est réduite en réduisant le nombre de hello de nœuds de données, certains services hello dans un cluster de hello sont redémarrés. Ainsi, en cours d’exécution et en attente de toofail de travaux à l’achèvement de hello Hello opération de mise à l’échelle. Vous pouvez, toutefois, renvoyer des tâches de hello une fois l’opération hello est terminée.
* HBase

    Vous pouvez accéder en toute transparence ajouter ou supprimer le cluster de nœuds tooyour HBase pendant son exécution. Serveurs régionaux sont équilibrés automatiquement après quelques minutes d’achèvement hello opération de mise à l’échelle. Toutefois, vous pouvez équilibrer manuellement les serveurs régionaux hello en vous connectant à un nœud principal de toohello du cluster et hello en cours d’exécution suivant des commandes dans une fenêtre d’invite de commandes :

        >pushd %HBASE_HOME%\bin
        >hbase shell
        >balancer
* Storm

    Vous pouvez accéder en toute transparence ajouter ou supprimer le cluster de données nœuds tooyour Storm pendant son exécution. Mais après la réussite de l’opération de mise à l’échelle de hello, vous devrez topologie de hello toorebalance.

    Cela peut se faire de deux façons à l’aide de :

  * l'interface utilisateur Web de Storm
  * l’outil d’interface de ligne de commande (CLI)

    Reportez-vous toohello [documentation d’Apache Storm](http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html) pour plus d’informations.

    interface utilisateur web de Storm Hello est disponible sur le cluster HDInsight de hello :

    ![HDInsight storm mise à l’échelle rééquilibrage](./media/hdinsight-administer-use-management-portal/hdinsight.portal.scale.cluster.png)

    Voici un exemple comment toouse hello CLI commande topologie de Storm toorebalance hello :

        ## Reconfigure hello topology "mytopology" toouse 5 worker processes,
        ## hello spout "blue-spout" toouse 3 executors, and
        ## hello bolt "yellow-bolt" toouse 10 executors
        $ storm rebalance mytopology -n 5 -e blue-spout=3 -e yellow-bolt=10

hello toochange taille du cluster Hadoop en utilisant Azure PowerShell, exécutez hello de commande suivante à partir d’un ordinateur client :

    Set-AzureRmHDInsightClusterSize -ClusterName <Cluster Name> -TargetInstanceCount <NewSize>


## <a name="grantrevoke-access"></a>Octroyer/Révoquer l’accès
Clusters HDInsight ont hello suivant (tous ces services ont des points de terminaison RESTful) des services web HTTP :

* ODBC
* JDBC
* Ambari
* Oozie
* Templeton

Par défaut, l'accès à ces services est octroyé. Vous pouvez révoquer ou octroyer l’accès de hello. toorevoke :

    Revoke-AzureRmHDInsightHttpServicesAccess -ClusterName <Cluster Name>

toogrant :

    $clusterName = "<HDInsight Cluster Name>"

    # Credential option 1
    $hadoopUserName = "admin"
    $hadoopUserPassword = "<Enter hello Password>"
    $hadoopUserPW = ConvertTo-SecureString -String $hadoopUserPassword -AsPlainText -Force
    $credential = New-Object System.Management.Automation.PSCredential($hadoopUserName,$hadoopUserPW)

    # Credential option 2
    #$credential = Get-Credential -Message "Enter hello HTTP username and password:" -UserName "admin"

    Grant-AzureRmHDInsightHttpServicesAccess -ClusterName $clusterName -HttpCredential $credential

> [!NOTE]
> Par attribution/révocation de l’accès hello, vous allez réinitialiser le mot de passe et le nom d’utilisateur de cluster de hello.
>
>

Peut également être cela via le portail de hello. Consultez [HDInsight de gérer à l’aide de hello portail Azure][hdinsight-admin-portal].

## <a name="update-http-user-credentials"></a>Mettre à jour les informations d’identification de l’utilisateur HTTP
Il est même hello procédure en tant que [Grant/revoke HTTP accès](#grant/revoke-access). Si le cluster de hello a été accordée hello accès HTTP, vous devez d’abord la révoquer.  Et accorder l’accès hello avec nouvelles informations d’identification utilisateur HTTP.

## <a name="find-hello-default-storage-account"></a>Recherchez le compte de stockage par défaut hello
Hello Powershell script suivant montre comment les tooget hello nom de compte de stockage par défaut et hello clé de compte de stockage par défaut pour un cluster.

    $clusterName = "<HDInsight Cluster Name>"

    $cluster = Get-AzureRmHDInsightCluster -ClusterName $clusterName
    $resourceGroupName = $cluster.ResourceGroup
    $defaultStorageAccountName = ($cluster.DefaultStorageAccount).Replace(".blob.core.windows.net", "")
    $defaultBlobContainerName = $cluster.DefaultStorageContainer
    $defaultStorageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -Name $defaultStorageAccountName)[0].Value
    $defaultStorageAccountContext = New-AzureStorageContext -StorageAccountName $defaultStorageAccountName -StorageAccountKey $defaultStorageAccountKey

## <a name="find-hello-resource-group"></a>Recherchez le groupe de ressources hello
En mode de gestionnaire de ressources hello, chaque cluster HDInsight appartient le groupe de ressources Azure tooan.  groupe de ressources toofind hello :

    $clusterName = "<HDInsight Cluster Name>"

    $cluster = Get-AzureRmHDInsightCluster -ClusterName $clusterName
    $resourceGroupName = $cluster.ResourceGroup


## <a name="submit-jobs"></a>Soumettre les travaux
**tâches MapReduce toosubmit**

Consultez [Exécution des exemples Hadoop MapReduce dans HDInsight basé sur Windows](hdinsight-run-samples.md)

**travaux de ruche toosubmit**

Consultez [Exécution de requêtes Hive avec PowerShell](hdinsight-hadoop-use-hive-powershell.md).

**travaux de Pig toosubmit**

Consultez [Exécution de tâches Pig avec PowerShell](hdinsight-hadoop-use-pig-powershell.md).

**travaux de Sqoop toosubmit**

Consultez l'article [Utilisation de Sqoop avec HDInsight](hdinsight-use-sqoop.md).

**travaux de Oozie toosubmit**

Consultez [Oozie utilisation avec Hadoop toodefine et exécuter un flux de travail dans HDInsight](hdinsight-use-oozie.md).

## <a name="upload-data-tooazure-blob-storage"></a>Télécharger le stockage d’objets Blob de données tooAzure
Consultez [télécharger des données tooHDInsight][hdinsight-upload-data].

## <a name="see-also"></a>Voir aussi
* [Documentation de référence des applets de commande HDInsight][hdinsight-powershell-reference]
* [Administrer HDInsight à l’aide de hello portail Azure][hdinsight-admin-portal]
* [Administration de HDInsight à l’aide de l’interface de ligne de commande][hdinsight-admin-cli]
* [Création de clusters HDInsight][hdinsight-provision]
* [Télécharger des données tooHDInsight][hdinsight-upload-data]
* [Envoi de tâches Hadoop par programme][hdinsight-submit-jobs]
* [Prise en main d’Azure HDInsight][hdinsight-get-started]

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/

[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md
[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-provision-custom-options]: hdinsight-hadoop-provision-linux-clusters.md#configuration
[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md

[hdinsight-admin-cli]: hdinsight-administer-use-command-line.md
[hdinsight-admin-portal]: hdinsight-administer-use-management-portal.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md
[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-mapreduce]: hdinsight-use-mapreduce.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-flight]: hdinsight-analyze-flight-delay-data.md

[hdinsight-powershell-reference]: https://msdn.microsoft.com/library/dn858087.aspx

[powershell-install-configure]: /powershell/azureps-cmdlets-docs

[image-hdi-ps-provision]: ./media/hdinsight-administer-use-powershell/HDI.PS.Provision.png
