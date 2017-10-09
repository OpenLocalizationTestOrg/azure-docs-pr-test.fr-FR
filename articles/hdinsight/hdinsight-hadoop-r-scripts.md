---
title: aaaUse R dans les clusters HDInsight toocustomize - Azure | Documents Microsoft
description: "Découvrez comment tooinstall R à l’aide de Script Action et l’utilisation de R sur les clusters HDInsight."
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: be851270-afa5-4af0-a69e-2d343a4deeb7
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ROBOTS: NOINDEX
ms.openlocfilehash: bf5adf2e18dc43a743b29fd1567fad731b9c3ab7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="install-and-use-r-on-hdinsight-hadoop-clusters"></a>Installation et utilisation de R sur des clusters HDInsight Hadoop

Découvrez comment toocustomize Windows basé sur le cluster HDInsight porte R à l’aide d’Action de Script, et comment les clusters toouse R sur HDInsight. Hello [HDInsight offre](https://azure.microsoft.com/pricing/details/hdinsight/) inclut un serveur R dans le cadre de votre cluster HDInsight. Cela permet à des scripts R toouse MapReduce et Spark toorun distribué des calculs. Pour plus d’informations, consultez la section [Prise en main de R Server sur HDInsight](hdinsight-hadoop-r-server-get-started.md). Pour plus d’informations sur l’utilisation de R avec un cluster Linux, consultez [Installation et utilisation de R sur des clusters HDInsight Hadoop (Linux)](hdinsight-hadoop-r-scripts-linux.md).

Vous pouvez installer R sur n’importe quel type de cluster (Hadoop, Storm, HBase, Spark) sur Azure HDInsight à l’aide d’une *action de script*. Un tooinstall de script d’exemple R sur un cluster HDInsight est disponible à partir d’un objet blob de stockage de Azure en lecture seule à [https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1](https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1).

**Articles connexes**

* [Installation et utilisation de R sur des clusters HDInsight Hadoop (Linux)](hdinsight-hadoop-r-scripts-linux.md)
* [Créer des clusters Hadoop dans HDInsight](hdinsight-hadoop-provision-linux-clusters.md): informations générales sur la création de clusters HDInsight
* [Personnaliser un cluster HDInsight à l’aide d’une action de script][hdinsight-cluster-customize] : informations générales sur la personnalisation de clusters HDInsight à l’aide d’actions de script
* [Développer des scripts d’action de script pour HDInsight](hdinsight-hadoop-script-actions.md)

## <a name="what-is-r"></a>Qu'est-ce que R ?
Hello <a href="http://www.r-project.org/" target="_blank">R Project pour calculer des statistiques</a> est un langage open source et un environnement de calcul de statistiques. R intègre des centaines de fonctions statistiques et possède son propre langage de programmation qui regroupe des aspects de la programmation fonctionnelle et de la programmation orientée objet. Il offre également des fonctionnalités graphiques étendues. R est un environnement de programmation préféré hello pour professionnel plus les statisticiens et scientifiques dans un large éventail de champs.

R est compatible avec le stockage d'objets Blob Azure (WASB), ce qui permet aux données stockées à cet emplacement d'être traitées avec R sur HDInsight.  

## <a name="install-r"></a>Installation de R
A [exemple de script](https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1) tooinstall R sur un cluster HDInsight est disponible à partir d’un blob en lecture seule dans le stockage Azure. Cette section fournit des instructions sur comment toouse hello exemple de script lors de la création de cluster hello à l’aide de hello portail Azure.

> [!NOTE]
> exemple de script Hello a été introduite avec la version 3.1 du cluster HDInsight. Pour plus d’informations sur les versions des clusters HDInsight, consultez la page [Versions des clusters HDInsight](hdinsight-component-versioning.md).
>
>

1. Lorsque vous créez un cluster HDInsight à partir de hello portail, cliquez sur **Configuration facultative**, puis cliquez sur **Actions de Script**.
2. Sur hello **Actions de Script** , entrez hello valeurs suivantes :

    ![Utilisez l’Action de Script toocustomize un cluster](./media/hdinsight-hadoop-r-scripts/hdi-r-script-action.png "toocustomize d’Action de Script d’utiliser un cluster")

    <table border='1'>
        <tr><th>Propriété</th><th>Valeur</th></tr>
        <tr><td>Nom</td>
            <td>Spécifiez un nom pour l’action de script hello, par exemple, <b>R d’installer</b>.</td></tr>
        <tr><td>URI du script</td>
            <td>Spécifiez hello URI toohello script qui est appelée toocustomize cluster de hello, par exemple, <i>https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1</i></td></tr>
        <tr><td>Type de nœud</td>
            <td>Spécifiez les nœuds hello sur lequel le script de personnalisation hello est exécuté. Vous avez le choix entre <b>Tous les nœuds</b>, <b>Nœuds principaux uniquement</b> et <b>Nœuds de travail uniquement</b>.
        <tr><td>Paramètres</td>
            <td>Spécifiez des paramètres de hello, si requis par le script de hello. Toutefois, hello script tooinstall R ne nécessite pas de paramètres, donc vous laissez ce champ vide.</td></tr>
    </table>

    Vous pouvez ajouter plusieurs tooinstall d’action de script de plusieurs composants sur le cluster de hello. Après avoir ajouté les scripts hello, cliquez sur hello toostart de case à cocher créer le cluster de hello.

Vous pouvez également utiliser hello tooinstall de script R sur HDInsight à l’aide d’Azure PowerShell ou hello HDInsight .NET SDK. Vous trouverez des instructions relatives à ces procédures dans la suite de cet article.

## <a name="run-r-scripts"></a>Exécuter des scripts R
Cette section décrit comment script toorun R sur hello Hadoop cluster hdinsight.

1. **Établir un cluster de toohello de connexion Bureau à distance**: à partir du portail de hello, activer le Bureau à distance pour cluster hello vous avez créé avec R installé et connectez-vous toohello cluster. Pour obtenir des instructions, consultez [connecter clusters tooHDInsight à l’aide du protocole RDP](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp).
2. **Console de hello ouvrir R**: installation de hello R place une console toohello R de lien sur le bureau hello de nœud principal de hello. Cliquez sur cette console de hello R tooopen.
3. **Exécuter le script de hello R**: script de hello R peut être exécuté directement à partir de la console de hello R en les collant, en sélectionnant et en appuyant sur ENTRÉE. Voici un script d’exemple simple qui génère des too100 des numéros 1 hello et puis de les multiplie par 2.

        library(rmr2)
        library(rhdfs)
        ints = to.dfs(1:100)
        calc = mapreduce(input = ints, map = function(k, v) cbind(v, 2*v))
        from.dfs(calc)

Hello deux premières lignes appel hello RHadoop bibliothèques qui sont installés avec R. hello dernière ligne imprime hello résultats toohello console. sortie de Hello doit ressembler à ceci :

    [1,]  1 2
    [2,]  2 4
    .
    .
    .
    [98,]  98 196
    [99,]  99 198
    [100,] 100 200


## <a name="install-r-using-aure-powershell"></a>Installation de R en cas d'utilisation d'Azure PowerShell
Consultez [Personnalisation de clusters HDInsight à l’aide d’une action de script](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell).  exemple Hello illustre comment tooinstall Spark à l’aide d’Azure PowerShell. Vous devez toocustomize hello script toouse [https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1](https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1).

## <a name="install-r-using-net-sdk"></a>Installation de R à l'aide du Kit de développement logiciel (SDK) .NET
Consultez [Personnalisation de clusters HDInsight à l’aide d’une action de script](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell). exemple Hello illustre comment tooinstall Spark à l’aide de hello du SDK .NET. Vous devez toocustomize hello script toouse [https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1](https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps11).

## <a name="see-also"></a>Voir aussi
* [Installation et utilisation de R sur des clusters HDInsight Hadoop (Linux)](hdinsight-hadoop-r-scripts-linux.md)
* [Créer des clusters Hadoop dans HDInsight](hdinsight-hadoop-provision-linux-clusters.md): informations générales sur la création de clusters HDInsight
* [Personnaliser un cluster HDInsight à l’aide d’une action de script][hdinsight-cluster-customize] : informations générales sur la personnalisation de clusters HDInsight à l’aide d’actions de script
* [Développer des scripts d’action de script pour HDInsight](hdinsight-hadoop-script-actions.md)
* [Installer et utiliser Spark sur les clusters HDInsight][hdinsight-install-spark] : exemple d’action de script sur l’installation de Spark
* [Installer Giraph sur les clusters HDInsight](hdinsight-hadoop-giraph-install.md): exemple d’action de script sur l’installation de Giraph
* [Installation de Solr sur les clusters HDInsight](hdinsight-hadoop-solr-install-linux.md): exemple d’action de script sur l'installation de Solr.

[powershell-install-configure]: /powershell/azureps-cmdlets-docs
[hdinsight-provision]: ../hdinsight-provision-clusters/
[hdinsight-cluster-customize]: hdinsight-hadoop-customize-cluster-linux.md
[hdinsight-install-spark]: hdinsight-apache-spark-jupyter-spark-sql.md
