---
title: "tooinstall d’Action de Script aaaUse Solr sur le cluster Hadoop - Azure | Documents Microsoft"
description: "Découvrez comment toocustomize HDInsight cluster avec Solr à l’aide d’Action de Script."
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: b1e6f338-8ac1-4b38-bbb5-2f7388b9de3b
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/05/2016
ms.author: nitinme
ROBOTS: NOINDEX
ms.openlocfilehash: 022ba56b7499390a91bfe869e5069893e56b6503
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="install-and-use-solr-on-windows-based-hdinsight-clusters"></a>Installer et utiliser Solr sur les clusters HDInsight Windows

Découvrez comment toocustomize HDInsight de basés sur Windows en cluster avec Solr à l’aide d’Action de Script et toouse Solr toosearch données.

> [!IMPORTANT]
> les étapes dans ce travail seul document avec des clusters HDInsight de basés sur Windows Hello. HDInsight est uniquement disponible sur Windows pour les versions antérieures à HDInsight 3.4. Linux est hello seul système d’exploitation utilisé sur HDInsight version 3.4 ou supérieure. Pour plus d’informations, consultez [Suppression de HDInsight sous Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement). Pour plus d’informations sur l’utilisation de Solr avec un cluster Linux, consultez [Installation et utilisation de Solr sur des clusters HDInsight Hadoop (Linux)](hdinsight-hadoop-solr-install-linux.md).


Vous pouvez installer Solr sur n’importe quel type de cluster (Hadoop, Storm, HBase, Spark) sur Azure HDInsight à l’aide d’une *action de script*. Un tooinstall de script d’exemple Solr sur un cluster HDInsight est disponible à partir d’un objet blob de stockage de Azure en lecture seule à [https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1).

exemple de script Hello fonctionne uniquement avec la version 3.1 du cluster HDInsight. Pour plus d’informations sur les versions des clusters HDInsight, consultez la page [Versions des clusters HDInsight](hdinsight-component-versioning.md).

exemple de script Hello utilisé dans cette rubrique crée un cluster basé sur Windows de Solr avec une configuration spécifique. Si vous souhaitez que le cluster de Solr hello tooconfigure avec différents regroupements, partitions, schémas, les réplicas, etc., vous devez modifier le script de hello et les fichiers binaires de Solr en conséquence.

**Articles connexes**

* [Installer et utiliser Solr sur des clusters HDInsight Hadoop (Linux)](hdinsight-hadoop-solr-install-linux.md)
* [Créer des clusters Hadoop dans HDInsight](hdinsight-provision-clusters.md): informations générales sur la création de clusters HDInsight.
* [Personnaliser un cluster HDInsight à l’aide d’une action de script][hdinsight-cluster-customize] : informations générales sur la personnalisation de clusters HDInsight à l’aide d’actions de script.
* [Développer des scripts d’action de script pour HDInsight](hdinsight-hadoop-script-actions.md).

## <a name="what-is-solr"></a>Présentation de Solr
<a href="http://lucene.apache.org/solr/features.html" target="_blank">Apache Solr</a> est une plateforme de recherche d’entreprise qui permet d’effectuer de puissantes opérations de recherche en texte intégral sur des données. Tandis que Hadoop permet de stocker et gérer des quantités importantes de données, Apache Solr fournit les fonctionnalités de recherche hello tooquickly extraire des données hello.

## <a name="install-solr-using-portal"></a>Installer Solr à l’aide du portail
1. Démarrer la création d’un cluster à l’aide de hello **création personnalisée** option, comme décrit dans [Hadoop de créer des clusters dans HDInsight](hdinsight-provision-clusters.md).
2. Sur hello **Actions de Script** page de l’Assistant de hello, cliquez sur **ajouter une action de script** tooprovide des détails sur l’action de script hello, comme indiqué ci-dessous :

    ![Utilisez l’Action de Script toocustomize un cluster](./media/hdinsight-hadoop-solr-install/hdi-script-action-solr.png "toocustomize d’Action de Script d’utiliser un cluster")

    <table border='1'>
        <tr><th>Propriété</th><th>Valeur</th></tr>
        <tr><td>Nom</td>
            <td>Spécifiez un nom pour l’action de script hello. Par exemple, <b>Installation Solr</b>.</td></tr>
        <tr><td>URI du script</td>
            <td>Spécifier le script de toohello d’identificateur de ressource uniforme (URI) hello qui est appelée toocustomize hello cluster. Par exemple, <i>https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1</i></td></tr>
        <tr><td>Type de nœud</td>
            <td>Spécifiez les nœuds hello sur lequel le script de personnalisation hello est exécuté. Vous avez le choix entre <b>Tous les nœuds</b>, <b>Nœuds principaux uniquement</b> et <b>Nœuds de travail uniquement</b>.
        <tr><td>Paramètres</td>
            <td>Spécifiez des paramètres de hello, si requis par le script de hello. Hello script tooinstall Solr ne nécessite pas de paramètres, donc vous laissez ce champ vide.</td></tr>
    </table>

    Vous pouvez ajouter plusieurs tooinstall d’action de script de plusieurs composants sur le cluster de hello. Après avoir ajouté les scripts hello, cliquez sur toostart de coche hello création hello cluster.

## <a name="use-solr"></a>Utiliser Solr
Vous devez commencer par indexer Solr avec quelques fichiers de données. Vous pouvez ensuite utiliser des requêtes de recherche toorun Solr sur les données de salutation indexée. Effectuez hello suivant les étapes toouse Solr dans un cluster HDInsight :

1. **Utilisez tooremote du protocole RDP (Remote Desktop) dans le cluster HDInsight de hello avec Solr installé**. À partir de hello portail Azure, activer le Bureau à distance pour cluster hello que vous avez créé avec le cluster de hello installé et ensuite à distance dans Solr. Pour obtenir des instructions, consultez [connecter clusters tooHDInsight à l’aide du protocole RDP](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp).
2. **Indexez Solr en téléchargeant des fichiers de données**. Lorsque vous indexez Solr, vous placez les documents que vous devrez peut-être toosearch sur. tooindex Solr, tooremote RDP d’utilisation dans un cluster de hello, accédez toohello bureau, ouvrez la ligne de commande Hadoop hello et accédez trop**C:\apps\dist\solr-4.7.2\example\exampledocs**. Exécutez hello de commande suivante :

        java -jar post.jar solr.xml monitor.xml

    Vous verrez hello suivant de sortie de console de hello :

        POSTing file solr.xml
        POSTing file monitor.xml
        2 files indexed.
        COMMITting Solr index changes toohttp://localhost:8983/solr/update..
        Time spent: 0:00:01.624

    utilitaire de post.jar Hello indexe Solr avec deux exemples de documents, **solr.xml** et **monitor.xml**. utilitaire de post.jar Hello et de documents hello sont disponibles avec l’installation de Solr.
3. **Utilisez hello Solr du tableau de bord toosearch dans hello les documents indexés**. Dans toohello de session RDP hello HDInsight de cluster, ouvrez Internet Explorer et lancer le tableau de bord hello Solr à **http://headnodehost:8983/solr / #/**. À partir du volet de gauche hello, à partir de hello **Core sélecteur** liste déroulante, sélectionnez **collection1**, dans ce cas, cliquez sur **requête**. En tant qu’exemple, tooselect et retourner tous les documents hello dans Solr, fournissent hello valeurs suivantes :

   * Bonjour **q** texte, entrez  **\*:**\*. Cela renvoie tous les documents de hello sont indexées de Solr. Si vous souhaitez toosearch une chaîne spécifique au sein de documents de hello, vous pouvez entrer ici cette chaîne.
   * Bonjour **wt** zone de texte, le format de sortie hello select. La valeur par défaut est **json**. Cliquez sur **Exécuter la requête**.

     ![Utilisez l’Action de Script toocustomize un cluster](./media/hdinsight-hadoop-solr-install/hdi-solr-dashboard-query.png "exécuter une requête sur un tableau de bord Solr")

     sortie de Hello retourne hello deux documents que nous avons utilisés pour l’indexation de Solr. sortie de Hello ressemble au suivant de hello :

           "response": {
               "numFound": 2,
               "start": 0,
               "maxScore": 1,
               "docs": [
                 {
                   "id": "SOLR1000",
                   "name": "Solr, hello Enterprise Search Server",
                   "manu": "Apache Software Foundation",
                   "cat": [
                     "software",
                     "search"
                   ],
                   "features": [
                     "Advanced Full-Text Search Capabilities using Lucene",
                     "Optimized for High Volume Web Traffic",
                     "Standards Based Open Interfaces - XML and HTTP",
                     "Comprehensive HTML Administration Interfaces",
                     "Scalability - Efficient Replication tooother Solr Search Servers",
                     "Flexible and Adaptable with XML configuration and Schema",
                     "Good unicode support: héllo (hello with an accent over hello e)"
                   ],
                   "price": 0,
                   "price_c": "0,USD",
                   "popularity": 10,
                   "inStock": true,
                   "incubationdate_dt": "2006-01-17T00:00:00Z",
                   "_version_": 1486960636996878300
                 },
                 {
                   "id": "3007WFP",
                   "name": "Dell Widescreen UltraSharp 3007WFP",
                   "manu": "Dell, Inc.",
                   "manu_id_s": "dell",
                   "cat": [
                     "electronics and computer1"
                   ],
                   "features": [
                     "30\" TFT active matrix LCD, 2560 x 1600, .25mm dot pitch, 700:1 contrast"
                   ],
                   "includes": "USB cable",
                   "weight": 401.6,
                   "price": 2199,
                   "price_c": "2199,USD",
                   "popularity": 6,
                   "inStock": true,
                   "store": "43.17614,-90.57341",
                   "_version_": 1486960637584081000
                 }
               ]
             }
4. **Recommandé : Hello sauvegarder les données indexées de Solr tooAzure stockage d’objets Blob associé au cluster HDInsight de hello**. Comme une bonne pratique, sauvegardez les données hello indexé à partir des nœuds de cluster hello Solr vers un stockage d’objets Blob Azure. Effectuez hello suivant les étapes toodo ainsi :

   1. À partir de la session RDP de hello, ouvrez Internet Explorer et toohello point suivant l’URL :

           http://localhost:8983/solr/replication?command=backup

       La réponse doit ressembler à ceci :

           <?xml version="1.0" encoding="UTF-8"?>
           <response>
             <lst name="responseHeader">
               <int name="status">0</int>
               <int name="QTime">9</int>
             </lst>
             <str name="status">OK</str>
           </response>
   2. Dans la session à distance de hello, accédez trop {SOLR_HOME}\{Collection} \data. Pour cluster hello créé via un script d’exemple hello, cela doit être **C:\apps\dist\solr-4.7.2\example\solr\collection1\data**. À cet emplacement, vous devez voir un dossier de capture instantanée créé avec un nom similaire trop**instantané.* horodatage***.
   3. Code postal du dossier de capture instantanée hello et téléchargez-le tooAzure stockage d’objets Blob. À partir de la ligne de commande Hadoop hello, accédez à emplacement toohello du dossier de capture instantanée hello à l’aide de hello de commande suivante :

             hadoop fs -CopyFromLocal snapshot._timestamp_.zip /example/data

       Cette commande copie hello trop/exemple/captures instantanées/sous le conteneur hello au sein de la valeur par défaut de hello stockage compte associé hello cluster.

## <a name="install-solr-using-aure-powershell"></a>Installer Solr à l’aide d’Azure PowerShell
Consultez [Personnalisation de clusters HDInsight à l’aide d’une action de script](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell).  exemple Hello illustre comment tooinstall Spark à l’aide d’Azure PowerShell. Vous devez toocustomize hello script toouse [https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1).

## <a name="install-solr-using-net-sdk"></a>Installer Solr à l’aide du Kit de développement logiciel (SDK) .NET
Consultez [Personnalisation de clusters HDInsight à l’aide d’une action de script](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell). exemple Hello illustre comment tooinstall Spark à l’aide de hello du SDK .NET. Vous devez toocustomize hello script toouse [https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1).

## <a name="see-also"></a>Voir aussi
* [Installer et utiliser Solr sur des clusters HDInsight Hadoop (Linux)](hdinsight-hadoop-solr-install-linux.md)
* [Créer des clusters Hadoop dans HDInsight](hdinsight-provision-clusters.md): informations générales sur la création de clusters HDInsight.
* [Personnaliser un cluster HDInsight à l’aide d’une action de script][hdinsight-cluster-customize] : informations générales sur la personnalisation de clusters HDInsight à l’aide d’actions de script.
* [Développer des scripts d’action de script pour HDInsight](hdinsight-hadoop-script-actions.md).
* [Installer et utiliser Spark sur les clusters HDInsight][hdinsight-install-spark] : exemple d’action de script sur l’installation de Spark.
* [Installer R sur les clusters HDInsight][hdinsight-install-r] : exemple d’action de script sur l’installation de R.
* [Installer Giraph sur les clusters HDInsight](hdinsight-hadoop-giraph-install.md): exemple d’action de script sur l’installation de Giraph.

[powershell-install-configure]: /powershell/azureps-cmdlets-docs
[hdinsight-provision]: hdinsight-provision-clusters.md
[hdinsight-install-r]: hdinsight-hadoop-r-scripts.md
[hdinsight-install-spark]: hdinsight-hadoop-spark-install.md
[hdinsight-cluster-customize]: hdinsight-hadoop-customize-cluster.md
