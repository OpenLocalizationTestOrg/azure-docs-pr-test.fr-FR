---
title: "aaaInstall et l’utilisation des clusters Giraph sur Hadoop dans HDInsight - Azure | Documents Microsoft"
description: "Découvrez comment toocustomize HDInsight de cluster avec Giraph et toouse Giraph."
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 77a1d0e0-55de-4e61-98a0-060914fb7ca0
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/05/2016
ms.author: nitinme
ROBOTS: NOINDEX
ms.openlocfilehash: bd473faca9d3c87c29d7566a18fc94211c50f059
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="install-and-use-giraph-on-windows-based-hdinsight-clusters"></a>Installer et utiliser Giraph sur les clusters HDInsight Windows

Découvrez comment toocustomize Windows basé sur le cluster HDInsight porte Giraph utilisant l’Action de Script et graphiques de toouse Giraph tooprocess à grande échelle. Pour plus d’informations sur l’utilisation de Giraph avec un cluster Linux, consultez [Installation de Giraph sur des clusters HDInsight Hadoop (Linux)](hdinsight-hadoop-giraph-install-linux.md).

> [!IMPORTANT]
> les étapes dans ce travail seul document avec des clusters HDInsight de basés sur Windows Hello. HDInsight est uniquement disponible sur Windows pour les versions antérieures à HDInsight 3.4. Linux est hello seul système d’exploitation utilisé sur HDInsight version 3.4 ou supérieure. Pour plus d’informations, consultez [Suppression de HDInsight sous Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement). Pour plus d’informations sur la façon de tooinstall Giraph sur un cluster HDInsight de basés sur Linux, consultez [Giraph d’installer sur les clusters HDInsight Hadoop (Linux)](hdinsight-hadoop-giraph-install-linux.md).


Vous pouvez installer Giraph sur n’importe quel type de cluster (Hadoop, Storm, HBase, Spark) sur Azure HDInsight à l’aide d’une *action de script*. Un tooinstall de script d’exemple Giraph sur un cluster HDInsight est disponible à partir d’un objet blob de stockage de Azure en lecture seule à [https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1). exemple de script Hello fonctionne uniquement avec la version 3.1 du cluster HDInsight. Pour plus d’informations sur les versions des clusters HDInsight, consultez la page [Versions des clusters HDInsight](hdinsight-component-versioning.md).

**Articles connexes**

* [Installer Giraph sur des clusters HDInsight Hadoop (Linux)](hdinsight-hadoop-giraph-install-linux.md)
* [Créer des clusters Hadoop dans HDInsight](hdinsight-provision-clusters.md): informations générales sur la création de clusters HDInsight.
* [Personnaliser un cluster HDInsight à l’aide d’une action de script][hdinsight-cluster-customize] : informations générales sur la personnalisation de clusters HDInsight à l’aide d’actions de script.
* [Développer des scripts d’action de script pour HDInsight](hdinsight-hadoop-script-actions.md).

## <a name="what-is-giraph"></a>Présentation de Giraph
<a href="http://giraph.apache.org/" target="_blank">Apache Giraph</a> vous permet de graphique tooperform traitement à l’aide de Hadoop et peut être utilisé avec Azure HDInsight. Graphiques de modéliser des relations entre les objets, tels que les connexions hello entre des routeurs d’un réseau de grande taille comme hello Internet, ou des relations entre des utilisateurs sur les réseaux sociaux (parfois désignée tooas un graphique social). Le traitement du graphique vous permet de tooreason sur les relations hello entre les objets dans un graphique, telles que :

* identifier les amis potentiels en fonction de vos relations actuelles ;
* Identification hello la plus courte entre deux ordinateurs dans un réseau.
* Calcul de rang dans la page hello des pages Web.

## <a name="install-giraph-using-portal"></a>Installation de Giraph à l'aide du portail
1. Démarrer la création d’un cluster à l’aide de hello **création personnalisée** option, comme décrit dans [Hadoop de créer des clusters dans HDInsight](hdinsight-provision-clusters.md).
2. Sur hello **Actions de Script** page de l’Assistant de hello, cliquez sur **ajouter une action de script** tooprovide des détails sur l’action de script hello, comme indiqué ci-dessous :

    ![Utilisez l’Action de Script toocustomize un cluster](./media/hdinsight-hadoop-giraph-install/hdi-script-action-giraph.png "toocustomize d’Action de Script d’utiliser un cluster")

    <table border='1'>
        <tr><th>Propriété</th><th>Valeur</th></tr>
        <tr><td>Nom</td>
            <td>Spécifiez un nom pour l’action de script hello. Par exemple, <b>Installation Giraph</b>.</td></tr>
        <tr><td>URI du script</td>
            <td>Spécifier le script de toohello d’identificateur de ressource uniforme (URI) hello qui est appelée toocustomize hello cluster. Par exemple, <i>https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1</i></td></tr>
        <tr><td>Type de nœud</td>
            <td>Spécifiez les nœuds hello sur lequel le script de personnalisation hello est exécuté. Vous avez le choix entre <b>Tous les nœuds</b>, <b>Nœuds principaux uniquement</b> et <b>Nœuds de travail uniquement</b>.
        <tr><td>Paramètres</td>
            <td>Spécifiez des paramètres de hello, si requis par le script de hello. Hello script tooinstall Giraph ne nécessite pas de paramètres, donc vous laissez ce champ vide.</td></tr>
    </table>

    Vous pouvez ajouter plusieurs tooinstall d’action de script de plusieurs composants sur le cluster de hello. Après avoir ajouté les scripts hello, cliquez sur toostart de coche hello création hello cluster.

## <a name="use-giraph"></a>Utiliser Giraph
Nous utilisons basic de hello hello SimpleShortestPathsComputation exemple toodemonstrate <a href = "http://people.apache.org/~edwardyoon/documents/pregel.pdf">Pregel</a> implémentation utilisée pour rechercher le chemin d’accès plus court de hello entre les objets dans un graphique. Utilisez hello suivant les étapes tooupload hello exemple hello et les données exemple jar, exécuter une tâche à l’aide de hello SimpleShortestPathsComputation exemple, puis afficher les résultats hello.

1. Télécharger un tooAzure de fichier de données exemple stockage d’objets Blob. Sur votre poste de travail local, créez un nouveau fichier nommé **tiny_graph.txt**. Elle doit contenir hello lignes suivantes :

        [0,0,[[1,1],[3,3]]]
        [1,0,[[0,1],[2,2],[3,1]]]
        [2,0,[[1,2],[4,4]]]
        [3,0,[[0,3],[1,1],[4,4]]]
        [4,0,[[3,4],[2,4]]]

    Téléchargez hello tiny_graph.txt fichier toohello stockage principal pour votre cluster HDInsight. Pour obtenir des instructions sur la façon de tooupload de données, consultez [télécharger des données pour les travaux Hadoop dans HDInsight](hdinsight-upload-data.md).

    Ces données décrivant une relation entre les objets dans un graphique orienté, à l’aide du format de hello [source\_id, source\_valeur, [[destination\_id], [edge\_valeur],...]]. Chaque ligne représente une relation entre un objet **source\_id** et un ou plusieurs objets **dest\_id**. Hello **bord\_valeur** (ou poids) peut être considéré comme puissance de hello ou de distance de connexion hello entre **source_id** et **dest\_id**.

    Dessiner, à l’aide de valeur de hello (ou poids) en tant que la distance entre les objets hello, hello au-dessus de données peut se présenter comme suit :

    ![tiny_graph.txt drawn as circles with lines of varying distance between](./media/hdinsight-hadoop-giraph-install/giraph-graph.png)
2. Exécutez hello SimpleShortestPathsComputation exemple. Utilisez hello suivant toorun hello exemple Azure PowerShell applets de commande à l’aide du fichier de tiny_graph.txt hello en tant qu’entrée.

    > [!IMPORTANT]
    > La prise en charge de la gestion des ressources HDInsight par Azure PowerShell à l’aide d’Azure Service Manager est **déconseillée** ; elle a été supprimée le 1er janvier 2017. étapes de Hello dans ce document Utilisez hello nouvelles applets de commande HDInsight qui fonctionnent avec Azure Resource Manager.
    >
    > Suivez les étapes de hello dans [installer et configurer Azure PowerShell](/powershell/azureps-cmdlets-docs) tooinstall hello dernière version d’Azure PowerShell. Si vous avez des scripts qui toobe besoin modifié toouse hello nouvelles applets de commande qui fonctionnent avec Azure Resource Manager, consultez [des outils de migration tooAzure développement basé sur le Gestionnaire de ressources pour les clusters HDInsight](hdinsight-hadoop-development-using-azure-resource-manager.md) pour plus d’informations.

    ```powershell
    $clusterName = "clustername"
    # Giraph examples jar
    $jarFile = "wasb:///example/jars/giraph-examples.jar"
    # Arguments for this job
    $jobArguments = "org.apache.giraph.examples.SimpleShortestPathsComputation",
                    "-ca", "mapred.job.tracker=headnodehost:9010",
                    "-vif", "org.apache.giraph.io.formats.JsonLongDoubleFloatDoubleVertexInputFormat",
                    "-vip", "wasb:///example/data/tiny_graph.txt",
                    "-vof", "org.apache.giraph.io.formats.IdWithValueTextOutputFormat",
                    "-op",  "wasb:///example/output/shortestpaths",
                    "-w", "2"
    # Create hello definition
    $jobDefinition = New-AzureHDInsightMapReduceJobDefinition
        -JarFile $jarFile
        -ClassName "org.apache.giraph.GiraphRunner"
        -Arguments $jobArguments

    # Run hello job, write output toohello Azure PowerShell window
    $job = Start-AzureHDInsightJob -Cluster $clusterName -JobDefinition $jobDefinition
    Write-Host "Wait for hello job toocomplete ..." -ForegroundColor Green
    Wait-AzureHDInsightJob -Job $job
    Write-Host "STDERR"
    Get-AzureHDInsightJobOutput -Cluster $clusterName -JobId $job.JobId -StandardError
    Write-Host "Display hello standard output ..." -ForegroundColor Green
    Get-AzureHDInsightJobOutput -Cluster $clusterName -JobId $job.JobId -StandardOutput
    ```

    Bonjour exemple ci-dessus, remplacez **clustername** avec nom hello de votre cluster HDInsight qui a Giraph installé.
3. Afficher les résultats hello. Une fois terminé, les travaux hello hello résultats seront stockés dans deux fichiers de sortie Bonjour **wasb : / / / exemple/out/shotestpaths** dossier. fichiers de Hello sont appelés **partie-m-00001** et **partie-m-00002**. Effectuez hello suivant les étapes toodownload et vue hello la sortie :

    ```powershell
    $subscriptionName = "<SubscriptionName>"       # Azure subscription name
    $storageAccountName = "<StorageAccountName>"   # Azure Storage account name
    $containerName = "<ContainerName>"             # Blob storage container name

    # Select hello current subscription
    Select-AzureSubscription $subscriptionName

    # Create hello Storage account context object
    $storageAccountKey = Get-AzureStorageKey $storageAccountName | %{ $_.Primary }
    $storageContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey

    # Download hello job output toohello workstation
    Get-AzureStorageBlobContent -Container $containerName -Blob example/output/shortestpaths/part-m-00001 -Context $storageContext -Force
    Get-AzureStorageBlobContent -Container $containerName -Blob example/output/shortestpaths/part-m-00002 -Context $storageContext -Force
    ```

    Cela créera hello **exemple/sortie/shortestpaths** structure du répertoire dans le répertoire en cours de hello sur votre station de travail et les fichiers toothat emplacement de téléchargement hello deux sortie.

    Hello d’utilisation **Cat** contenu de hello toodisplay applet de commande des fichiers de hello :

        Cat example/output/shortestpaths/part*

    une sortie Hello doit apparaître comme toohello suivantes :

        0    1.0
        4    5.0
        2    2.0
        1    0.0
        3    1.0

    Hello SimpleShortestPathComputation exemple est codé en dur toostart avec l’objet ID 1 et rechercher des objets de tooother hello plus courts chemin d’accès. Afin de la sortie de hello doit être lu comme `destination_id distance`, où la distance est hello (ou valeur poids) des bords hello traversées entre l’objet ID 1 et ID hello cible.

    Cette visualisation, vous pouvez vérifier les résultats hello par déplacement des chemins d’accès plus courts de hello entre l’ID 1 et tous les autres objets. Notez que hello chemin le plus court entre les ID 1 et 4 de l’ID est 5. Il s’agit hello total séparant <span style="color:orange">ID 1 et 3</span>, puis <span style="color:red">ID 3 et 4</span>.

    ![Drawing of objects as circles with shortest paths drawn between](./media/hdinsight-hadoop-giraph-install/giraph-graph-out.png)

## <a name="install-giraph-using-aure-powershell"></a>Installation de Giraph à l'aide d’Azure PowerShell
Consultez [Personnalisation de clusters HDInsight à l’aide d’une action de script](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell).  exemple Hello illustre comment tooinstall Spark à l’aide d’Azure PowerShell. Vous devez toocustomize hello script toouse [https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1).

## <a name="install-giraph-using-net-sdk"></a>Installation de Giraph à l'aide de .NET SDK
Consultez [Personnalisation de clusters HDInsight à l’aide d’une action de script](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell). exemple Hello illustre comment tooinstall Spark à l’aide de hello du SDK .NET. Vous devez toocustomize hello script toouse [https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1).

## <a name="see-also"></a>Voir aussi
* [Installer Giraph sur des clusters HDInsight Hadoop (Linux)](hdinsight-hadoop-giraph-install-linux.md)
* [Créer des clusters Hadoop dans HDInsight](hdinsight-provision-clusters.md): informations générales sur la création de clusters HDInsight.
* [Personnaliser un cluster HDInsight à l’aide d’une action de script][hdinsight-cluster-customize] : informations générales sur la personnalisation de clusters HDInsight à l’aide d’actions de script.
* [Développer des scripts d’action de script pour HDInsight](hdinsight-hadoop-script-actions.md).
* [Installer et utiliser Spark sur les clusters HDInsight][hdinsight-install-spark] : exemple d’action de script sur l’installation de Spark.
* [Installer R sur les clusters HDInsight][hdinsight-install-r] : exemple d’action de script sur l’installation de R.
* [Installation de Solr sur les clusters HDInsight](hdinsight-hadoop-solr-install.md): exemple d’action de script sur l'installation de Solr.

[tools]: https://github.com/Blackmist/hdinsight-tools
[aps]: http://azure.microsoft.com/documentation/articles/install-configure-powershell/

[powershell-install]: /powershell/azureps-cmdlets-docs
[hdinsight-provision]: hdinsight-provision-clusters.md
[hdinsight-install-r]: hdinsight-hadoop-r-scripts.md
[hdinsight-install-spark]: hdinsight-hadoop-spark-install.md
[hdinsight-cluster-customize]: hdinsight-hadoop-customize-cluster.md
