---
title: "action aaaScript - packages d’installation de Python avec Notebook sur Azure HDInsight | Documents Microsoft"
description: "Obtenir des instructions détaillées sur comment toouse script action tooconfigure Notebook ordinateurs portables avec HDInsight Spark clusters toouse des packages python externe."
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
ms.openlocfilehash: 54db79e67995dee7ca00abff979f7d74ae5ab9cd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-script-action-tooinstall-external-python-packages-for-jupyter-notebooks-in-apache-spark-clusters-on-hdinsight"></a>Utiliser les packages de Python externes Action de Script tooinstall pour les ordinateurs portables Notebook dans les clusters Apache Spark sur HDInsight
> [!div class="op_single_selector"]
> * [À l’aide de la commande magique de cellule](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
> * [À l’aide d’une action de script](hdinsight-apache-spark-python-package-installation.md)
>
>

Découvrez comment toouse Actions de Script tooconfigure un cluster Apache Spark sur HDInsight (Linux) toouse externe, conçu par la Communauté **python** packages qui ne sont pas inclus l’emploi dans le cluster de hello.

> [!NOTE]
> Vous pouvez également configurer un bloc-notes jupyter à l’aide de `%%configure` magique toouse les packages externes. Pour obtenir des instructions, consultez [Utilisation de packages externes avec les blocs-notes Jupyter dans des clusters Apache Spark sur HDInsight](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md).
> 
> 

Vous pouvez rechercher hello [index du package](https://pypi.python.org/pypi) pour la liste complète des packages disponibles hello. Vous pouvez également obtenir une liste des packages disponibles à partir d’autres sources. Par exemple, vous pouvez installer les packages mis à disposition via [Anaconda](https://docs.continuum.io/anaconda/pkg-docs) ou [conda-forge](https://conda-forge.github.io/feedstocks.html).

Dans cet article, vous allez apprendre comment tooinstall hello [TensorFlow](https://www.tensorflow.org/) à l’aide du Script Actoin sur votre cluster et l’utiliser via un bloc-notes jupyter de hello.

## <a name="prerequisites"></a>Composants requis
Vous devez disposer de hello :

* Un abonnement Azure. Consultez la page [Obtention d’un essai gratuit d’Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).
* Un cluster Apache Spark sur HDInsight. Pour obtenir des instructions, consultez [Création de clusters Apache Spark dans Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).

   > [!NOTE]
   > Si vous n’avez pas encore de cluster Spark sur HDInsight Linux, vous pouvez exécuter des actions de script lors de la création du cluster. Consultez la documentation de hello sur [comment toouse personnalisées actions de script](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux).
   > 
   > 

## <a name="use-external-packages-with-jupyter-notebooks"></a>Utiliser des packages externes avec les blocs-notes Jupyter

1. À partir de hello [Azure Portal](https://portal.azure.com/), à partir du tableau d’accueil hello, cliquez sur la vignette hello pour votre cluster Spark (si vous avez épinglé il toohello tableau d’accueil). Vous pouvez également naviguer cluster tooyour sous **parcourir tous les** > **Clusters HDInsight**.   

2. Dans le panneau de cluster Spark hello, cliquez sur **Actions de Script** sous **utilisation**. Exécuter l’action personnalisée hello qui installe TensorFlow nœuds principaux d’hello et nœuds de travail hello. script d’interpréteur de commandes Hello peut être référencée à partir de : https://hdiconfigactions.blob.core.windows.net/linuxtensorflow/tensorflowinstall.sh visite documentation hello [comment toouse personnalisées actions de script](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux).

   > [!NOTE]
   > Il existe deux python installations en cluster de hello. Spark utilisera l’installation de python Anaconda hello située `/usr/bin/anaconda/bin`. Référencez cette installation dans vos actions personnalisées via `/usr/bin/anaconda/bin/pip` et `/usr/bin/anaconda/bin/conda`.
   > 
   > 

3. Ouvrez un bloc-notes PySpark Jupyter

    ![Créer un bloc-notes Jupyter](./media/hdinsight-apache-spark-python-package-installation/hdinsight-spark-create-notebook.png "Créer un bloc-notes Jupyter")

4. Un nouvel ordinateur portable est créé et ouvert avec le nom hello Untitled.pynb. Cliquez sur le nom du bloc-notes hello haut hello et entrez un nom convivial.

    ![Fournissez un nom pour l’ordinateur portable de hello](./media/hdinsight-apache-spark-python-package-installation/hdinsight-spark-name-notebook.png "fournir un nom d’ordinateur portable de hello")

5. Vous allez maintenant `import tensorflow` et exécuter un exemple hello world. 

    Code toocopy :

        import tensorflow as tf
        hello = tf.constant('Hello, TensorFlow!')
        sess = tf.Session()
        print(sess.run(hello))

    résultat de Hello doit ressembler à ceci :
    
    ![Exécution de code TensorFlow](./media/hdinsight-apache-spark-python-package-installation/execution.png "Exécuter le code TensorFlow")



## <a name="seealso"></a>Voir aussi
* [Vue d’ensemble : Apache Spark sur Azure HDInsight](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a>Scénarios
* [Spark avec BI : effectuez une analyse interactive des données à l’aide de Spark dans HDInsight avec des outils BI](hdinsight-apache-spark-use-bi-tools.md)
* [Spark avec Machine Learning : utilisez Spark dans HDInsight pour l’analyse de la température des bâtiments à l’aide des données des systèmes HVAC](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [Spark avec Machine Learning : Spark utilisation dans résultats de l’inspection alimentaires toopredict HDInsight](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [Streaming Spark : Utiliser Spark dans HDInsight pour créer des applications de diffusion en continu en temps réel](hdinsight-apache-spark-eventhub-streaming.md)
* [Analyse des journaux de site web à l’aide de Spark dans HDInsight](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a>Créer et exécuter des applications
* [Créer une application autonome avec Scala](hdinsight-apache-spark-create-standalone-application.md)
* [Exécuter des tâches à distance avec Livy sur un cluster Spark](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a>Outils et extensions
* [Utilisation de packages externes avec les blocs-notes Jupyter dans des clusters Apache Spark sur HDInsight](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [Utiliser le plug-in des outils HDInsight pour IntelliJ idée toocreate et soumettre des applications de Spark Scala](hdinsight-apache-spark-intellij-tool-plugin.md)
* [Utiliser des plug-in des outils HDInsight pour les applications de Spark toodebug IntelliJ idée à distance](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [Utiliser des bloc-notes Zeppelin avec un cluster Spark sur HDInsight](hdinsight-apache-spark-zeppelin-notebook.md)
* [Noyaux disponibles pour le bloc-notes Jupyter dans un cluster Spark pour HDInsight](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [Installer Notebook sur votre ordinateur et vous connecter tooan cluster HDInsight Spark](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a>Gestion des ressources
* [Gérer les ressources de cluster d’Apache Spark hello dans Azure HDInsight](hdinsight-apache-spark-resource-manager.md)
* [Track and debug jobs running on an Apache Spark cluster in HDInsight (Suivi et débogage des tâches en cours d’exécution sur un cluster Apache Spark dans HDInsight)](hdinsight-apache-spark-job-debugging.md)
