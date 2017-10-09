---
title: aaaMicrosoft cognitifs Toolkit avec Azure HDInsight Spark pour en savoir plus approfondie | Documents Microsoft
description: "Apprenez comment un apprentissage Microsoft cognitifs Toolkit approfondie de modèle d’apprentissage peut être appliqué tooa le jeu de données à l’aide de hello Spark Python API dans un cluster Azure HDInsight Spark."
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: nitinme
ms.openlocfilehash: c296d4697f16d4ef6a958fdb55289807d745ea40
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-microsoft-cognitive-toolkit-deep-learning-model-with-azure-hdinsight-spark-cluster"></a>Utiliser le modèle de formation approfondie Microsoft Cognitive Toolkit avec un cluster Azure HDInsight Spark

Dans cet article, vous hello comme suit.

1. Exécuter un script personnalisé de tooinstall Microsoft cognitifs Toolkit sur un cluster Azure HDInsight Spark.

2. Télécharger un toosee de cluster Notebook bloc-notes toohello Spark comment tooapply un formé Microsoft cognitifs Toolkit approfondie d’apprentissage toofiles de modèle dans un compte de stockage d’objets Blob Azure à l’aide de hello [Spark Python API (PySpark)](https://spark.apache.org/docs/0.9.0/python-programming-guide.html)

## <a name="prerequisites"></a>Composants requis

* **Un abonnement Azure**. Avant de commencer ce didacticiel, vous devez disposer d’un abonnement Azure. Voir [Créez votre compte Azure gratuit](https://azure.microsoft.com/free).

* **Cluster Azure HDInsight Spark**. Pour cet article, créez un cluster Spark 2.0. Pour obtenir des instructions, consultez la page [Créer un cluster Apache Spark dans Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).

## <a name="how-does-this-solution-flow"></a>Comment fonctionne cette solution ?

Cette solution est divisée entre cet article et un bloc-notes Jupyter que vous chargez dans le cadre de ce didacticiel. Dans cet article, vous effectuez hello comme suit :

* Exécuter une action de script sur un cluster HDInsight Spark tooinstall des packages Microsoft cognitifs Toolkit et Python.
* Télécharger un bloc-notes jupyter hello qui s’exécute hello solution toohello cluster HDInsight Spark.

Hello les étapes suivantes sont décrites dans le bloc-notes jupyter de hello.

- Charger des exemples d’images dans un RDD (Spark Resilient Distributed Dataset)
   - Charger des modules et prédéfinir des paramètres
   - Télécharger hello le jeu de données localement sur le cluster Spark de hello
   - Convertir le jeu de données de hello dans un RDD
- Images de hello de score à l’aide d’un modèle de boîte à outils cognitifs formé
   - Télécharger le cluster Spark toohello hello formé Toolkit cognitifs modèle
   - Définir toobe fonctions utilisée par les nœuds de travail
   - Images de score hello sur les nœuds de travail
   - Évaluer la précision du modèle


## <a name="install-microsoft-cognitive-toolkit"></a>Installer Microsoft Cognitive Toolkit

Vous pouvez installer Microsoft Cognitive Toolkit sur un cluster Spark avec une action de script. Action de script utilise des composants de tooinstall de scripts personnalisés sur le cluster hello qui ne sont pas disponibles par défaut. Vous pouvez utiliser le script personnalisé hello hello portail Azure, à l’aide du Kit de développement logiciel HDInsight .NET ou à l’aide d’Azure PowerShell. Vous pouvez également utiliser hello script tooinstall hello toolkit soit dans le cadre de la création du cluster, ou une fois le cluster de hello est en cours d’exécution. 

Dans cet article, nous utilisons hello tooinstall portail hello toolkit, une fois hello cluster a été créé. Pour autres façons toorun hello personnalisé de script, consultez [HDInsight de personnaliser des clusters à l’aide de Script Action](hdinsight-hadoop-customize-cluster-linux.md).

### <a name="using-hello-azure-portal"></a>À l’aide de hello portail Azure

Pour savoir comment toouse hello Azure Portal toorun de script action, consultez [HDInsight de personnaliser des clusters à l’aide de Script Action](hdinsight-hadoop-customize-cluster-linux.md#use-a-script-action-during-cluster-creation). Vérifiez que vous fournissez hello suivant entrées tooinstall Microsoft cognitifs Toolkit.

* Fournissez une valeur pour le nom de l’action script hello.

* Dans **URI de script bash**, entrez `https://raw.githubusercontent.com/Azure-Samples/hdinsight-pyspark-cntk-integration/master/cntk-install.sh`.

* Assurez-vous que vous exécutez les script hello uniquement sur hello noeuds head et de travail et effacer tous les hello autres cases à cocher.

* Cliquez sur **Créer**.

## <a name="upload-hello-jupyter-notebook-tooazure-hdinsight-spark-cluster"></a>Télécharger hello Notebook bloc-notes tooAzure cluster HDInsight Spark

toouse hello Microsoft cognitifs Toolkit avec un cluster Azure HDInsight Spark de hello, vous devez charger bloc-notes jupyter de hello **CNTK_model_scoring_on_Spark_walkthrough.ipynb** cluster Azure HDInsight Spark de toohello. Ce bloc-notes est disponible sur GitHub à l’adresse [https://github.com/Azure-Samples/hdinsight-pyspark-cntk-integration](https://github.com/Azure-Samples/hdinsight-pyspark-cntk-integration).

1. Référentiel de clone hello GitHub [https://github.com/Azure-Samples/hdinsight-pyspark-cntk-integration](https://github.com/Azure-Samples/hdinsight-pyspark-cntk-integration). Pour obtenir des instructions tooclone, consultez [clonage d’un référentiel](https://help.github.com/articles/cloning-a-repository/).

2. À partir de hello portail Azure, ouvrez le panneau de cluster Spark hello que vous déjà configurée, cliquez sur **tableau de bord de Cluster**, puis cliquez sur **bloc-notes jupyter**.

    Vous pouvez également lancer bloc-notes jupyter de hello en accédant toohello URL `https://<clustername>.azurehdinsight.net/jupyter/`. Remplacez \<nom_cluster > avec le nom hello de votre cluster HDInsight.

3. Dans le bloc-notes jupyter de hello, cliquez sur **télécharger** hello en haut à droite et puis accédez emplacement toohello où vous avez cloné le référentiel GitHub de hello.

    ![Télécharger Notebook bloc-notes tooAzure cluster HDInsight Spark](./media/hdinsight-apache-spark-microsoft-cognitive-toolkit/hdinsight-microsoft-cognitive-toolkit-load-jupyter-notebook.png "Notebook de télécharger bloc-notes tooAzure cluster HDInsight Spark")

4. Cliquez à nouveau sur **Charger**.

5. Une fois que le bloc-notes de hello est téléchargé, cliquez sur nom hello de l’ordinateur portable de hello et suivez les instructions de hello dans Bloc-notes hello lui-même sur tooload hello du jeu de données et effectuer le didacticiel de hello.

## <a name="see-also"></a>Voir aussi
* [Vue d’ensemble : Apache Spark sur Azure HDInsight](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a>Scénarios
* [Spark avec BI : effectuez une analyse interactive des données à l’aide de Spark dans HDInsight avec des outils BI](hdinsight-apache-spark-use-bi-tools.md)
* [Spark avec Machine Learning : utilisez Spark dans HDInsight pour l’analyse de la température des bâtiments à l’aide des données des systèmes HVAC](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [Spark avec Machine Learning : Spark utilisation dans résultats de l’inspection alimentaires toopredict HDInsight](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [Streaming Spark : Utiliser Spark dans HDInsight pour créer des applications de diffusion en continu en temps réel](hdinsight-apache-spark-eventhub-streaming.md)
* [Analyse des journaux de site web à l’aide de Spark dans HDInsight](hdinsight-apache-spark-custom-library-website-log-analysis.md)
* [Application Insight telemetry data analysis using Spark in HDInsight (Analyse des données de télémétrie Application Insight à l’aide de Spark dans HDInsight)](hdinsight-spark-analyze-application-insight-logs.md)

### <a name="create-and-run-applications"></a>Créer et exécuter des applications
* [Créer une application autonome avec Scala](hdinsight-apache-spark-create-standalone-application.md)
* [Exécuter des tâches à distance avec Livy sur un cluster Spark](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a>Outils et extensions
* [Utiliser le plug-in des outils HDInsight pour IntelliJ idée toocreate et soumettre des applications de Spark Scala](hdinsight-apache-spark-intellij-tool-plugin.md)
* [Utiliser des plug-in des outils HDInsight pour les applications de Spark toodebug IntelliJ idée à distance](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [Utiliser des bloc-notes Zeppelin avec un cluster Spark sur HDInsight](hdinsight-apache-spark-zeppelin-notebook.md)
* [Noyaux disponibles pour le bloc-notes Jupyter dans un cluster Spark pour HDInsight](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [Utiliser des packages externes avec les blocs-notes Jupyter](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [Installer Notebook sur votre ordinateur et vous connecter tooan cluster HDInsight Spark](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a>Gestion des ressources
* [Gérer les ressources de cluster d’Apache Spark hello dans Azure HDInsight](hdinsight-apache-spark-resource-manager.md)
* [Track and debug jobs running on an Apache Spark cluster in HDInsight (Suivi et débogage des tâches en cours d’exécution sur un cluster Apache Spark dans HDInsight)](hdinsight-apache-spark-job-debugging.md)

[hdinsight-versions]: hdinsight-component-versioning.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[azure-create-storageaccount]:../storage/common/storage-create-storage-account.md
