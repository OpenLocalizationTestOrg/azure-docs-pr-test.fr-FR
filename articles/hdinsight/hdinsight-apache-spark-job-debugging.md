---
title: "aaaDebug Apache Spark des travaux en cours d’exécution sur Azure HDInsight | Documents Microsoft"
description: "Utiliser l’interface utilisateur des fils Spark UI, tâches et Spark historique server tootrack et de débogage en cours d’exécution sur un cluster Spark dans Azure HDInsight"
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 59af05a7-2bd9-44b0-b55f-2438d294198b
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: nitinme
ms.openlocfilehash: 33d352a5773920735aa4e5e8532b78122f381377
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="debug-apache-spark-jobs-running-on-azure-hdinsight"></a>Déboguer des travaux Apache Spark en cours d’exécution sur Azure HDInsight

Dans cet article, vous allez apprendre comment tootrack et débogage et des travaux en cours d’exécution sur des clusters HDInsight à l’aide de hello fils UI, interface utilisateur Spark et hello du serveur de l’historique de Spark. Pour cet article, nous allons commencer un travail Spark à l’aide d’un ordinateur portable disponible avec le cluster Spark de hello, **apprentissage : l’analyse prédictive sur les données d’inspection de produits alimentaires à l’aide de MLLib**. Vous pouvez utiliser les étapes de hello ci-dessous tootrack une application que vous avez envoyé à l’aide de n’importe quel autre approche, par exemple, **spark-submit**.

## <a name="prerequisites"></a>Composants requis
Vous devez disposer de hello :

* Un abonnement Azure. Consultez la page [Obtention d’un essai gratuit d’Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).
* Un cluster Apache Spark sur HDInsight. Pour obtenir des instructions, consultez [Création de clusters Apache Spark dans Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).
* Démarrez bloc-notes de hello, en cours d’exécution  **[apprentissage : l’analyse prédictive sur les données d’inspection de produits alimentaires à l’aide de MLLib](hdinsight-apache-spark-machine-learning-mllib-ipython.md)**. Pour obtenir des instructions sur la façon de toorun ce bloc-notes, suivez hello lien.  

## <a name="track-an-application-in-hello-yarn-ui"></a>Effectuer le suivi d’une application Bonjour fils UI
1. Lancez hello fils UI. Dans le panneau de cluster hello, cliquez sur **tableau de bord de Cluster**, puis cliquez sur **fils**.
   
    ![Lancer l’interface utilisateur Yarn](./media/hdinsight-apache-spark-job-debugging/launch-yarn-ui.png)
   
   > [!TIP]
   > Ou bien, vous pouvez également lancer hello l’interface utilisateur des fils de hello Ambari UI. toolaunch hello Ambari UI, à partir du Panneau de cluster hello, cliquez sur **tableau de bord de Cluster**, puis cliquez sur **tableau de bord de Cluster HDInsight**. À partir de hello Ambari UI, cliquez sur **fils**, cliquez sur **liens rapides**et cliquez sur Gestionnaire de ressources actif hello, puis cliquez sur **ResourceManager UI**.    
   > 
   > 
2. Étant donné que vous avez démarré la tâche de Spark hello Notebook portables, application hello a le nom de hello **remotesparkmagics** (il s’agit de nom hello pour toutes les applications qui sont démarrées à partir d’ordinateurs portables de hello). Cliquez sur ID de l’application hello contre tooget de nom d’application hello plus d’informations sur la tâche de hello. Cette opération lance le mode d’application hello.
   
    ![Rechercher l’ID d’application Spark](./media/hdinsight-apache-spark-job-debugging/find-application-id.png)
   
    Pour de telles applications lancées à partir d’ordinateurs portables de hello Notebook, état de hello est toujours **en cours d’exécution** jusqu'à ce que vous quittiez bloc-notes de hello.
3. Vue d’application hello, vous pouvez descendre davantage toofind conteneurs hello associé hello hello journaux des applications et (stdout/stderr). Vous pouvez également lancer hello Spark UI en cliquant sur hello liaison correspondante toohello **URL de suivi**, comme illustré ci-dessous. 
   
    ![Télécharger les journaux de conteneur](./media/hdinsight-apache-spark-job-debugging/download-container-logs.png)

## <a name="track-an-application-in-hello-spark-ui"></a>Effectuer le suivi d’une application Bonjour Spark UI
Bonjour Spark UI, vous pouvez descendre dans les travaux de Spark hello qui est générées par l’application hello lancée précédemment.

1. toolaunch hello Spark UI, à partir de la vue d’application hello, cliquez sur le lien hello contre hello **URL de suivi**, comme illustré dans la capture d’écran hello ci-dessus. Vous pouvez voir tous les travaux de Spark hello qui sont lancées par l’application hello en cours d’exécution dans un bloc-notes jupyter de hello.
   
    ![Afficher les travaux Spark](./media/hdinsight-apache-spark-job-debugging/view-spark-jobs.png)
2. Cliquez sur hello **exécuteurs** toosee les informations de traitement et de stockage pour chaque exécuteur de l’onglet. Vous pouvez également récupérer la pile des appels hello en cliquant sur hello **de threads de vidage** lien.
   
    ![Afficher les exécuteurs Spark](./media/hdinsight-apache-spark-job-debugging/view-spark-executors.png)
3. Cliquez sur hello **étapes** onglet étapes de hello toosee associés application hello.
   
    ![Afficher les étapes Spark](./media/hdinsight-apache-spark-job-debugging/view-spark-stages.png)
   
    Chaque étape peut comporter plusieurs tâches dont vous pouvez afficher les statistiques d’exécution, comme illustré ci-dessous.
   
    ![Afficher les étapes Spark](./media/hdinsight-apache-spark-job-debugging/view-spark-stages-details.png) 
4. À partir de la page de détails de l’étape hello, vous pouvez lancer visualisation de DAG. Développez hello **DAG visualisation** lier en hello haut hello, comme indiqué ci-dessous.
   
    ![Afficher la visualisation DAG des étapes Spark](./media/hdinsight-apache-spark-job-debugging/view-spark-stages-dag-visualization.png)
   
    DAG ou Direct Aclyic graphique représente hello différentes étapes application hello. Chaque zone bleue dans le graphique de hello représente une opération de Spark appelée à partir de l’application hello.
5. À partir de la page de détails de l’étape hello, vous pouvez également lancer d’affichage de la chronologie application hello. Développez hello **événement chronologie** lier en hello haut hello, comme indiqué ci-dessous.
   
    ![Afficher la chronologie d’événement des étapes Spark](./media/hdinsight-apache-spark-job-debugging/view-spark-stages-event-timeline.png)
   
    Cela affiche les événements de Spark hello sous forme de hello d’une chronologie. affichage de la chronologie Hello est disponible à trois niveaux, sur les travaux, au sein d’un travail et d’une étape. image Hello ci-dessus capture chronologie hello pour une étape donnée.
   
   > [!TIP]
   > Si vous sélectionnez hello **activer le zoom avant** case à cocher, vous pouvez faire défiler gauche et droite sur l’affichage de la chronologie hello.
   > 
   > 
6. Autres onglets de hello Spark UI fournissent des informations utiles sur l’instance de Spark hello également.
   
   * Onglet stockage - si votre application crée une RDDs, vous trouverez plus d’informations sur celles figurant dans l’onglet de stockage hello.
   * Onglet environnement - cet onglet fournit de nombreuses informations utiles sur votre instance de Spark telles que hello 
     * version de Scala ;
     * Répertoire de journal des événements associé au cluster de hello
     * Nombre de cœurs de l’exécuteur de l’application hello
     * etc.

## <a name="find-information-about-completed-jobs-using-hello-spark-history-server"></a>Rechercher des informations sur les travaux terminés à l’aide de hello Spark historique serveur
Une fois qu’une tâche est terminée, hello plus d’informations sur les travaux hello sont conservés dans hello Spark historique serveur.

1. toolaunch hello Spark Server de l’historique, à partir du Panneau de cluster hello, cliquez sur **tableau de bord de Cluster**, puis cliquez sur **Spark historique Server**.
   
    ![Lancer le serveur d’historique Spark](./media/hdinsight-apache-spark-job-debugging/launch-spark-history-server.png)
   
   > [!TIP]
   > Ou bien, vous pouvez également lancer hello l’interface utilisateur du serveur Spark historique à partir de hello Ambari UI. toolaunch hello Ambari UI, à partir du Panneau de cluster hello, cliquez sur **tableau de bord de Cluster**, puis cliquez sur **tableau de bord de Cluster HDInsight**. À partir de hello Ambari UI, cliquez sur **Spark**, cliquez sur **liens rapides**, puis cliquez sur **l’interface utilisateur du serveur Spark historique**.
   > 
   > 
2. Vous verrez toutes les applications hello terminée répertoriées. Cliquez sur un toodrill de ID d’application vers le bas dans une application pour plus d’informations.
   
    ![Lancer le serveur d’historique Spark](./media/hdinsight-apache-spark-job-debugging/view-completed-applications.png)

## <a name="see-also"></a>Voir aussi
*  [Gérer les ressources de cluster d’Apache Spark hello dans Azure HDInsight](hdinsight-apache-spark-resource-manager.md)

### <a name="for-data-analysts"></a>Pour les analystes de données

* [Spark avec Machine Learning : utilisez Spark dans HDInsight pour l’analyse de la température des bâtiments à l’aide des données des systèmes HVAC](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [Spark avec Machine Learning : Spark utilisation dans résultats de l’inspection alimentaires toopredict HDInsight](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [Analyse des journaux de site web à l’aide de Spark dans HDInsight](hdinsight-apache-spark-custom-library-website-log-analysis.md)
* [Application Insight telemetry data analysis using Spark in HDInsight (Analyse des données de télémétrie Application Insight à l’aide de Spark dans HDInsight)](hdinsight-spark-analyze-application-insight-logs.md)
* [Utiliser Caffe sur Azure HDInsight Spark pour une formation approfondie échelonnée](hdinsight-deep-learning-caffe-spark.md)

### <a name="for-spark-developers"></a>Pour les développeurs Spark

* [Créer une application autonome avec Scala](hdinsight-apache-spark-create-standalone-application.md)
* [Exécution de travaux à distance avec Livy sur un cluster Spark](hdinsight-apache-spark-livy-rest-interface.md)
* [Utiliser le plug-in des outils HDInsight pour IntelliJ idée toocreate et soumettre des applications de Spark Scala](hdinsight-apache-spark-intellij-tool-plugin.md)
* [Streaming Spark : Utiliser Spark dans HDInsight pour créer des applications de diffusion en continu en temps réel](hdinsight-apache-spark-eventhub-streaming.md)
* [Utiliser des plug-in des outils HDInsight pour les applications de Spark toodebug IntelliJ idée à distance](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [Utiliser des bloc-notes Zeppelin avec un cluster Spark sur HDInsight](hdinsight-apache-spark-zeppelin-notebook.md)
* [Noyaux disponibles pour le bloc-notes Jupyter dans un cluster Spark pour HDInsight](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [Utiliser des packages externes avec les blocs-notes Jupyter](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [Installer Notebook sur votre ordinateur et vous connecter tooan cluster HDInsight Spark](hdinsight-apache-spark-jupyter-notebook-install-locally.md)


