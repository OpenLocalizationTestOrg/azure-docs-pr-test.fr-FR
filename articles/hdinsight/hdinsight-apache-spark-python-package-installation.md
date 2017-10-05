---
title: "Action de script : Installer des packages Python avec Jupyter sur Azure HDInsight | Microsoft Docs"
description: "Cette section comporte des instructions détaillées expliquant comment utiliser une action de script pour configurer des blocs-notes Jupyter disponibles avec des clusters HDInsight Spark pour utiliser des packages Python externes."
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 21978b71-eb53-480b-a3d1-c5d428a7eb5b
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: nitinme
ms.openlocfilehash: 20cf384c96d4ff4eaf064c8880ad128d521fb9bf
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="use-script-action-to-install-external-python-packages-for-jupyter-notebooks-in-apache-spark-clusters-on-hdinsight"></a>Utilisation d’une action de script pour installer des packages externes Python avec les blocs-notes Jupyter dans des clusters Apache Spark sur HDInsight
> [!div class="op_single_selector"]
> * [À l’aide de la commande magique de cellule](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
> * [À l’aide d’une action de script](hdinsight-apache-spark-python-package-installation.md)
>
>

Découvrez comment utiliser les actions de script pour configurer un cluster Apache Spark sur HDInsight (Linux) pour utiliser des packages **python** externes bénéficiant de la contribution de la communauté, qui ne sont pas inclus dans le cluster.

> [!NOTE]
> Vous pouvez également configurer un bloc-notes Jupyter à l’aide de la commande magique `%%configure` pour utiliser les packages externes. Pour obtenir des instructions, consultez [Utilisation de packages externes avec les blocs-notes Jupyter dans des clusters Apache Spark sur HDInsight](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md).
> 
> 

Vous pouvez rechercher [l’index de package](https://pypi.python.org/pypi) pour obtenir la liste complète des packages disponibles. Vous pouvez également obtenir une liste des packages disponibles à partir d’autres sources. Par exemple, vous pouvez installer les packages mis à disposition via [Anaconda](https://docs.continuum.io/anaconda/pkg-docs) ou [conda-forge](https://conda-forge.github.io/feedstocks.html).

Dans cet article, vous allez apprendre à installer le package [TensorFlow](https://www.tensorflow.org/) à l’aide de l’action de script sur votre cluster et l’utiliser via le bloc-notes Jupyter.

## <a name="prerequisites"></a>Composants requis
Vous devez disposer des éléments suivants :

* Un abonnement Azure. Consultez la page [Obtention d’un essai gratuit d’Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).
* Un cluster Apache Spark sur HDInsight. Pour obtenir des instructions, consultez [Création de clusters Apache Spark dans Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).

   > [!NOTE]
   > Si vous n’avez pas encore de cluster Spark sur HDInsight Linux, vous pouvez exécuter des actions de script lors de la création du cluster. Consultez la documentation sur [Guide d’utilisation des actions de script personnalisées](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux).
   > 
   > 

## <a name="use-external-packages-with-jupyter-notebooks"></a>Utiliser des packages externes avec les blocs-notes Jupyter

1. Dans le tableau d’accueil du [portail Azure](https://portal.azure.com/), cliquez sur la vignette de votre cluster Spark (si vous l’avez épinglé au tableau d’accueil). Vous pouvez également accéder à votre cluster sous **Parcourir tout** > **Clusters HDInsight**.   

2. Dans le panneau de cluster Spark, cliquez sur **Actions de script** sous **Utilisation**. Exécutez l’action personnalisée qui installe TensorFlow sur les nœuds principaux et les nœuds de travail. Le script bash peut être référencé à partir de : https://hdiconfigactions.blob.core.windows.net/linuxtensorflow/tensorflowinstall.sh Consultez la documentation sur [Guide d’utilisation des actions de script personnalisées](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux).

   > [!NOTE]
   > Il existe deux installations de Python dans le cluster. Spark utilisera l’installation d’Anaconda Python située dans `/usr/bin/anaconda/bin`. Référencez cette installation dans vos actions personnalisées via `/usr/bin/anaconda/bin/pip` et `/usr/bin/anaconda/bin/conda`.
   > 
   > 

3. Ouvrez un bloc-notes PySpark Jupyter

    ![Créer un bloc-notes Jupyter](./media/hdinsight-apache-spark-python-package-installation/hdinsight-spark-create-notebook.png "Créer un bloc-notes Jupyter")

4. Un nouveau bloc-notes est créé et ouvert sous le nom Untitled.pynb. Cliquez sur le nom du bloc-notes en haut, puis entrez un nom convivial.

    ![Donnez un nom au bloc-notes](./media/hdinsight-apache-spark-python-package-installation/hdinsight-spark-name-notebook.png "Donnez un nom au bloc-notes")

5. Vous allez maintenant `import tensorflow` et exécuter un exemple hello world. 

    Code à copier :

        import tensorflow as tf
        hello = tf.constant('Hello, TensorFlow!')
        sess = tf.Session()
        print(sess.run(hello))

    Le résultat aura l’aspect suivant :
    
    ![Exécution de code TensorFlow](./media/hdinsight-apache-spark-python-package-installation/execution.png "Exécuter le code TensorFlow")



## <a name="seealso"></a>Voir aussi
* [Vue d’ensemble : Apache Spark sur Azure HDInsight](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a>Scénarios
* [Spark avec BI : effectuez une analyse interactive des données à l’aide de Spark dans HDInsight avec des outils BI](hdinsight-apache-spark-use-bi-tools.md)
* [Spark avec Machine Learning : Utiliser Spark dans HDInsight pour l’analyse de la température de bâtiments à l’aide de données HVAC](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [Spark avec Machine Learning : Utiliser Spark dans HDInsight pour prédire les résultats de l’inspection des aliments](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [Streaming Spark : Utiliser Spark dans HDInsight pour créer des applications de diffusion en continu en temps réel](hdinsight-apache-spark-eventhub-streaming.md)
* [Analyse des journaux de site web à l’aide de Spark dans HDInsight](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a>Créer et exécuter des applications
* [Créer une application autonome avec Scala](hdinsight-apache-spark-create-standalone-application.md)
* [Exécuter des tâches à distance avec Livy sur un cluster Spark](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a>Outils et extensions
* [Utilisation de packages externes avec les blocs-notes Jupyter dans des clusters Apache Spark sur HDInsight](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [Utilisation du plugin d’outils HDInsight pour IntelliJ IDEA pour créer et soumettre des applications Spark Scala](hdinsight-apache-spark-intellij-tool-plugin.md)
* [Use HDInsight Tools Plugin for IntelliJ IDEA to debug Spark applications remotely) (Utiliser le plug-in Outils HDInsight pour IntelliJ IDEA pour déboguer des applications Spark à distance)](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [Utiliser des bloc-notes Zeppelin avec un cluster Spark sur HDInsight](hdinsight-apache-spark-zeppelin-notebook.md)
* [Noyaux disponibles pour le bloc-notes Jupyter dans un cluster Spark pour HDInsight](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [Installer Jupyter sur un ordinateur et se connecter au cluster Spark sur HDInsight](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a>Gestion des ressources
* [Gérer les ressources du cluster Apache Spark dans Azure HDInsight](hdinsight-apache-spark-resource-manager.md)
* [Suivi et débogage des tâches en cours d’exécution sur un cluster Apache Spark dans HDInsight](hdinsight-apache-spark-job-debugging.md)
