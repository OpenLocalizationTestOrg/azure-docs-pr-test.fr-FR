---
title: aaaInstall et utiliser Giraph sur HDInsight (Hadoop) - Azure | Documents Microsoft
description: "Découvrez comment les clusters tooinstall Giraph sur HDInsight de basés sur Linux à l’aide des Actions de Script. Actions de script permettent de toocustomize hello cluster lors de la création, par la modification de la configuration de cluster ou l’installation des services et les utilitaires."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 9fcac906-8f06-4002-9fe8-473e42f8fd0f
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: larryfr
ms.openlocfilehash: 0f195b65cebf5e24d1808ef33b95b4d362555521
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="install-giraph-on-hdinsight-hadoop-clusters-and-use-giraph-tooprocess-large-scale-graphs"></a>Installer Giraph sur les clusters HDInsight Hadoop et utiliser des graphiques de Giraph tooprocess à grande échelle

Découvrez comment tooinstall Apache Giraph sur un cluster HDInsight. fonctionnalité d’action de script Hello de HDInsight vous permet de toocustomize votre cluster en exécutant un script de l’interpréteur de commandes. Scripts peuvent être utilisés toocustomize clusters pendant et après la création du cluster.

> [!IMPORTANT]
> étapes de Hello dans ce document nécessitent un cluster HDInsight qui utilise Linux. Linux est hello seul système d’exploitation utilisé sur HDInsight version 3.4 ou supérieure. Pour plus d’informations, consultez [Suppression de HDInsight sous Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).

## <a name="whatis"></a>Présentation de Giraph

[Apache Giraph](http://giraph.apache.org/) vous permet de graphique tooperform traitement à l’aide de Hadoop et peut être utilisé avec Azure HDInsight. Les graphiques modélisent les relations entre les objets. Par exemple, les connexions entre des routeurs d’un réseau étendu hello comme hello Internet ou les relations entre les utilisateurs pouvant accéder à des réseaux sociaux. Le traitement du graphique vous permet de tooreason sur les relations hello entre les objets dans un graphique, telles que :

* identifier les amis potentiels en fonction de vos relations actuelles ;

* Identification hello la plus courte entre deux ordinateurs dans un réseau.

* Calcul de rang dans la page hello des pages Web.

> [!WARNING]
> Les composants fournis avec le cluster HDInsight de hello sont entièrement gérés - Support technique de Microsoft vous aide à tooisolate et résoudre les problèmes connexes toothese composants.
>
> Les composants personnalisés, tels que Giraph, réception efforcera toohelp vous toofurther hello de dépannage. Support technique de Microsoft soit en mesure de tooresolving hello. Si ce n’est pas le cas, vous devez consulter les communautés open source. Elles regorgent de connaissances approfondies sur cette technologie. Vous pouvez, par exemple, utiliser de nombreux sites de communauté, comme le [forum MSDN sur HDInsight](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=hdinsight), [http://stackoverflow.com](http://stackoverflow.com). En outre, les projets Apache ont des sites de projet sur [http://apache.org](http://apache.org). Par exemple : [Hadoop](http://hadoop.apache.org/).


## <a name="what-hello-script-does"></a>Le script hello effectue

Ce script effectue hello suivant des actions :

* Installe Giraph trop`/usr/hdp/current/giraph`

* Hello de copies `giraph-examples.jar` stockage de fichier toodefault (WASB) pour votre cluster :`/example/jars/giraph-examples.jar`

## <a name="install"></a>Installez Giraph à l’aide des actions de script

Un tooinstall de script d’exemple Giraph sur un cluster HDInsight est disponible à l’adresse hello l’emplacement suivant :

    https://hdiconfigactions.blob.core.windows.net/linuxgiraphconfigactionv01/giraph-installer-v01.sh

Cette section fournit des instructions sur la façon dont toouse hello exemple de script lors de la création du cluster de hello à l’aide de hello portail Azure.

> [!NOTE]
> Une action de script peut être appliquée à l’aide d’une des méthodes suivantes de hello :
> * Azure PowerShell
> * Hello CLI d’Azure
> * Hello HDInsight .NET SDK
> * Modèles Microsoft Azure Resource Manager
> 
> Vous pouvez également appliquer tooalready d’actions de script clusters en cours d’exécution. Pour plus d’informations, consultez la page [Personnaliser des clusters HDInsight à l’aide d’une action de script](hdinsight-hadoop-customize-cluster-linux.md).

1. Démarrer la création d’un cluster à l’aide des étapes hello dans [clusters basés sur Linux de créer de HDInsight](hdinsight-hadoop-create-linux-clusters-portal.md), mais n’effectuez pas la création.

2. Sur hello **Configuration facultative** panneau, sélectionnez **Actions de Script**et fournir hello informations suivantes :

   * **NOM**: entrez un nom convivial pour l’action de script hello.

   * **URI du SCRIPT** : https://hdiconfigactions.blob.core.windows.net/linuxgiraphconfigactionv01/giraph-installer-v01.sh

   * **HEAD** : cochez cette entrée.

   * **WORKER** : laissez cette entrée désactivée.

   * **ZOOKEEPER** : laissez cette entrée désactivée.

   * **PARAMETERS**: laissez ce champ vide.

3. En bas de hello Hello **Actions de Script**, utilisez hello **sélectionnez** configuration hello toosave du bouton. Enfin, utilisez hello **sélectionnez** bouton bas hello hello **Configuration facultative** informations de configuration facultatives panneau toosave hello.

4. Poursuivre la création de cluster de hello comme décrit dans [clusters basés sur Linux de créer de HDInsight](hdinsight-hadoop-create-linux-clusters-portal.md).

## <a name="usegiraph"></a>Utilisation de Giraph dans HDInsight

Une fois que le cluster de hello a été créé, utilisez hello étapes toorun hello SimpleShortestPathsComputation exemple inclus avec Giraph suivant. Cet exemple utilise basic de hello [Pregel](http://people.apache.org/~edwardyoon/documents/pregel.pdf) implémentation utilisée pour rechercher le chemin d’accès plus court de hello entre les objets dans un graphique.

1. Connecter le cluster HDInsight de toohello à l’aide de SSH :

    ```bash
    ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
    ```

    Pour en savoir plus, voir [Utilisation de SSH avec HDInsight (Hadoop) depuis Bash (l’interpréteur de commande) sur Windows 10, Linux, Unix ou OS X](hdinsight-hadoop-linux-use-ssh-unix.md).

2. Toocreate de commande suivant de hello d’utiliser un fichier nommé **tiny_graph.txt**:

    ```bash
    nano tiny_graph.txt
    ```

    Utilisez hello après le texte en tant que contenu hello de ce fichier :

    ```text
    [0,0,[[1,1],[3,3]]]
    [1,0,[[0,1],[2,2],[3,1]]]
    [2,0,[[1,2],[4,4]]]
    [3,0,[[0,3],[1,1],[4,4]]]
    [4,0,[[3,4],[2,4]]]
    ```

    Ces données décrivant une relation entre les objets dans un graphique orienté, à l’aide du format de hello `[source_id, source_value,[[dest_id], [edge_value],...]]`. Chaque ligne représente une relation entre un objet `source_id` et un ou plusieurs objets `dest_id`. Hello `edge_value` peut être considéré comme puissance de hello ou de distance de connexion hello entre `source_id` et `dest\_id`.

    Dessiner, à l’aide de valeur hello (ou les poids) en tant que distance hello entre des objets, les données de salutation peut se présenter comme hello suivant schéma :

    ![tiny_graph.txt drawn as circles with lines of varying distance between](./media/hdinsight-hadoop-giraph-install-linux/giraph-graph.png)

3. fichier de hello toosave, utilisez **Ctrl + X**, puis **Y**et enfin **entrée** nom de fichier tooaccept hello.

4. Utilisez hello suivant des données de salutation toostore dans le stockage principal pour votre cluster HDInsight :

    ```bash
    hdfs dfs -put tiny_graph.txt /example/data/tiny_graph.txt
    ```

5. Exécutez hello SimpleShortestPathsComputation exemple à l’aide de hello de commande suivante :

    ```bash
    yarn jar /usr/hdp/current/giraph/giraph-examples.jar org.apache.giraph.GiraphRunner org.apache.giraph.examples.SimpleShortestPathsComputation -ca mapred.job.tracker=headnodehost:9010 -vif org.apache.giraph.io.formats.JsonLongDoubleFloatDoubleVertexInputFormat -vip /example/data/tiny_graph.txt -vof org.apache.giraph.io.formats.IdWithValueTextOutputFormat -op /example/output/shortestpaths -w 2
    ```

    paramètres de Hello utilisés avec cette commande sont décrits dans hello tableau suivant :

   | Paramètre | Résultat |
   | --- | --- |
   | `jar` |fichier jar du Hello qui contient des exemples de hello. |
   | `org.apache.giraph.GiraphRunner` |classe Hello utilisé les exemples de hello toostart. |
   | `org.apache.giraph.examples.SimpleShortestPathsCoputation` |exemple Hello qui est utilisé. Dans cet exemple, il calcule hello plus court chemin entre ID 1 et tous les autres ID dans le graphique de hello. |
   | `-ca mapred.job.tracker` |nœud principal de Hello pour le cluster de hello. |
   | `-vif` |Hello toouse de format d’entrée pour les données d’entrée hello. |
   | `-vip` |fichier de données d’entrée Hello. |
   | `-vof` |format de sortie Hello. Dans cet exemple, l’ID et la valeur sous forme de texte brut. |
   | `-op` |emplacement de sortie Hello. |
   | `-w 2` |nombre de Hello de travailleurs toouse. Dans cet exemple, 2. |

    Pour plus d’informations sur ces et autres paramètres utilisés avec les exemples de Giraph, consultez hello [Giraph quickstart](http://giraph.apache.org/quick_start.html).

6. Une fois le travail de hello terminée, les résultats de hello sont stockés dans hello **/example/out/shotestpaths** active. Hello les noms de fichiers de sortie commencent par **partie-m -** et se terminer par un nombre indiquant hello tout d’abord, en second lieu, les fichiers etc.. Utilisez hello après la sortie de commande tooview hello :

    ```bash
    hdfs dfs -text /example/output/shortestpaths/*
    ```

    une sortie Hello doit apparaître toohello similaire après le texte :

        0    1.0
        4    5.0
        2    2.0
        1    0.0
        3    1.0

    Hello SimpleShortestPathComputation exemple est codé en dur toostart avec l’objet ID 1 et rechercher des objets de tooother hello plus courts chemin d’accès. sortie de Hello est au format hello de `destination_id` et `distance`. Hello `distance` est hello valeur (poids) des bords hello traversées entre l’objet ID 1 et ID hello cible.

    Visualiser ces données, vous pouvez vérifier les résultats hello par déplacement des chemins d’accès plus courts de hello entre l’ID 1 et tous les autres objets. Hello plus court chemin entre ID 1 et 4 de l’ID est 5. Cette valeur est la distance totale de hello entre <span style="color:orange">ID 1 et 3</span>, puis <span style="color:red">ID 3 et 4</span>.

    ![Drawing of objects as circles with shortest paths drawn between](./media/hdinsight-hadoop-giraph-install-linux/giraph-graph-out.png)

## <a name="next-steps"></a>Étapes suivantes

* [Installer et utiliser Hue sur les clusters HDInsight](hdinsight-hadoop-hue-linux.md).

* [Installation de Solr sur des clusters HDInsight](hdinsight-hadoop-solr-install-linux.md).
