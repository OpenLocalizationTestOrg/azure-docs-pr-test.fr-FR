---
title: cluster de ressources aaaManage pour Apache Spark sur Azure HDInsight | Documents Microsoft
description: "Découvrez comment gérer les ressources pour les clusters Spark sur Azure HDInsight pour de meilleures performances toouse."
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 9da7d4e3-458e-4296-a628-77b14643f7e4
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: nitinme
ms.openlocfilehash: e18682a24f77494db884105f9db03c0a350ddad6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-resources-for-apache-spark-cluster-on-azure-hdinsight"></a>Gérer les ressources du cluster Apache Spark dans Azure HDInsight 

Dans cet article, vous allez apprendre comment tooaccess les interfaces de hello, Ambari UI, l’interface utilisateur des fils et hello Spark historique serveur associé à votre cluster Spark. Vous découvrirez également comment tootune hello configuration du cluster pour des performances optimales.

**Configuration requise :**

Vous devez disposer de hello :

* Un abonnement Azure. Consultez la page [Obtention d’un essai gratuit d’Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).
* Un cluster Apache Spark sur HDInsight. Pour obtenir des instructions, consultez [Création de clusters Apache Spark dans Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).

## <a name="how-do-i-launch-hello-ambari-web-ui"></a>Comment lancer hello l’interface utilisateur de Ambari Web ?
1. À partir de hello [Azure Portal](https://portal.azure.com/), à partir du tableau d’accueil hello, cliquez sur la vignette hello pour votre cluster Spark (si vous avez épinglé il toohello tableau d’accueil). Vous pouvez également naviguer cluster tooyour sous **parcourir tous les** > **Clusters HDInsight**.
2. Dans le panneau de cluster Spark hello, cliquez sur **tableau de bord**. Lorsque vous y êtes invité, entrez les informations d’identification du admin de hello pour le cluster Spark de hello.

    ![Lancer Ambari](./media/hdinsight-apache-spark-resource-manager/hdinsight-launch-cluster-dashboard.png "Démarrer le gestionnaire de ressources")
3. Cela devrait s’ouvrir hello l’interface utilisateur de Ambari Web, comme indiqué ci-dessous.

    ![Interface utilisateur web Ambari](./media/hdinsight-apache-spark-resource-manager/ambari-web-ui.png "Interface utilisateur web Ambari")   

## <a name="how-do-i-launch-hello-spark-history-server"></a>Comment lancer hello Spark historique serveur ?
1. À partir de hello [Azure Portal](https://portal.azure.com/), à partir du tableau d’accueil hello, cliquez sur la vignette hello pour votre cluster Spark (si vous avez épinglé il toohello tableau d’accueil).
2. À partir de hello cluster panneau, sous **liens rapides**, cliquez sur **tableau de bord de Cluster**. Bonjour **tableau de bord de Cluster** panneau, cliquez sur **Spark historique Server**.

    ![Serveur d’historique Spark](./media/hdinsight-apache-spark-resource-manager/launch-history-server.png "Serveur d’historique Spark")

    Lorsque vous y êtes invité, entrez les informations d’identification du admin de hello pour le cluster Spark de hello.

## <a name="how-do-i-launch-hello-yarn-ui"></a>Comment lancer hello fils UI ?
Vous pouvez utiliser hello fils UI toomonitor applications en cours d’exécution sur le cluster de Spark hello.

1. Dans le panneau de cluster hello, cliquez sur **tableau de bord de Cluster**, puis cliquez sur **fils**.

    ![Lancer l’interface utilisateur Yarn](./media/hdinsight-apache-spark-resource-manager/launch-yarn-ui.png)

   > [!TIP]
   > Ou bien, vous pouvez également lancer hello l’interface utilisateur des fils de hello Ambari UI. toolaunch hello Ambari UI, à partir du Panneau de cluster hello, cliquez sur **tableau de bord de Cluster**, puis cliquez sur **tableau de bord de Cluster HDInsight**. À partir de hello Ambari UI, cliquez sur **fils**, cliquez sur **liens rapides**et cliquez sur Gestionnaire de ressources actif hello, puis cliquez sur **ResourceManager UI**.
   >
   >

## <a name="what-is-hello-optimum-cluster-configuration-toorun-spark-applications"></a>Nouveautés d’applications de Spark toorun hello cluster optimales configuration ?
paramètres de clé Hello trois qui peuvent être utilisés pour la configuration de Spark selon les spécifications de l’application sont `spark.executor.instances`, `spark.executor.cores`, et `spark.executor.memory`. Un exécuteur est un processus lancé pour une application Spark. Il s’exécute sur le nœud de travail hello et est responsable toocarry tâches hello pour une application hello. nombre d’exécuteurs hello exécuteur tailles et pour chaque cluster par défaut de Hello est calculé en fonction nombre de hello de nœuds de travail et la taille du nœud travail hello. Ils sont stockés dans `spark-defaults.conf` sur nœuds principaux d’un cluster hello.

trois paramètres de configuration Hello peuvent être configurées au niveau du cluster hello (pour toutes les applications qui s’exécutent sur le cluster de hello) ou peuvent être spécifiés pour chaque application également.

### <a name="change-hello-parameters-using-ambari-ui"></a>Modifier les paramètres de hello à l’aide de Ambari UI
1. À partir de hello Ambari UI, cliquez sur **Spark**, cliquez sur **configurations**, puis développez **personnalisé spark-defaults**.

    ![Définir des paramètres à l’aide d’Ambari](./media/hdinsight-apache-spark-resource-manager/set-parameters-using-ambari.png)
2. valeurs par défaut de Hello sont bonnes toohave 4 Spark aux applications d’exécuter simultanément sur le cluster de hello. Vous pouvez modifications ces valeurs à partir de l’interface utilisateur de hello, comme indiqué ci-dessous.

    ![Définir des paramètres à l’aide d’Ambari](./media/hdinsight-apache-spark-resource-manager/set-executor-parameters.png)
3. Cliquez sur **enregistrer** modifications de configuration toosave hello. En hello haut hello, vous serez invité toorestart tous hello les services affectés. Cliquez sur **Restart (Redémarrer)**.

    ![Redémarrer les services](./media/hdinsight-apache-spark-resource-manager/restart-services.png)

### <a name="change-hello-parameters-for-an-application-running-in-jupyter-notebook"></a>Modifier les paramètres d’une application en cours d’exécution dans un bloc-notes jupyter hello
Pour les applications en cours d’exécution dans un bloc-notes jupyter de hello, vous pouvez utiliser hello `%%configure` magique de modifications de configuration toomake hello. Dans l’idéal, vous devez apporter ces modifications devant l’application hello, avant d’exécuter la première cellule de code hello. Cela garantit que la configuration hello est appliqué toohello Livy session, lorsque celui-ci est créé. Si vous voulez que la configuration de hello toochange à un stade ultérieur dans l’application hello, vous devez utiliser hello `-f` paramètre. Toutefois, en procédant ainsi, tous les progrès Bonjour application seront perdue.

extrait de code Hello ci-dessous montre comment toochange hello configuration d’une application en cours d’exécution dans le bloc-notes.

    %%configure
    {"executorMemory": "3072M", "executorCores": 4, "numExecutors":10}

Paramètres de configuration doivent être passées comme une chaîne JSON et doivent être sur la ligne suivante de hello après magique de hello, comme indiqué dans l’exemple, la colonne hello.

### <a name="change-hello-parameters-for-an-application-submitted-using-spark-submit"></a>Modifier les paramètres d’une application soumise à l’aide de hello spark-submit
Commande suivante est un exemple de comment toochange hello pour une application de traitement par lots est envoyée à l’aide des paramètres de configuration `spark-submit`.

    spark-submit --class <hello application class tooexecute> --executor-memory 3072M --executor-cores 4 –-num-executors 10 <location of application jar file> <application parameters>

### <a name="change-hello-parameters-for-an-application-submitted-using-curl"></a>Modifier les paramètres de hello pour une demande envoyée à l’aide de cURL
Commande suivante est un exemple de comment toochange hello les paramètres de configuration pour une application de traitement par lots est soumise à l’aide de cURL.

    curl -k -v -H 'Content-Type: application/json' -X POST -d '{"file":"<location of application jar file>", "className":"<hello application class tooexecute>", "args":[<application parameters>], "numExecutors":10, "executorMemory":"2G", "executorCores":5' localhost:8998/batches

### <a name="how-do-i-change-these-parameters-on-a-spark-thrift-server"></a>Comment modifier ces paramètres sur un serveur Thrift Spark ?
Spark Thrift Server offre JDBC/ODBC accès tooa Spark cluster et est utilisé tooservice requêtes Spark SQL. Les outils tels que Power BI, Tableau, etc. utilisez ODBC protocole toocommunicate avec des requêtes de Spark SQL tooexecute Spark Thrift serveur comme une Application Spark. Lors de la création d’un cluster Spark, deux instances de hello Spark Thrift Server sont démarrés, un sur chaque nœud principal. Chaque serveur de Thrift Spark apparaît sous la forme d’une application Spark Bonjour fils UI.

Spark Thrift Server utilise l’allocation dynamique de l’exécuteur de nouvelles et par conséquent hello `spark.executor.instances` n’est pas utilisé. En revanche, Spark Thrift serveur utilise `spark.dynamicAllocation.minExecutors` et `spark.dynamicAllocation.maxExecutors` nombre d’exécuteur toospecify hello. paramètres de configuration de Hello `spark.executor.cores` et `spark.executor.memory` est toomodify hello exécuteur taille utilisée. Vous pouvez modifier ces paramètres comme indiqué ci-dessous.

* Développez hello **avancé spark-thrift-sparkconf** paramètres de catégorie tooupdate hello `spark.dynamicAllocation.minExecutors`, `spark.dynamicAllocation.maxExecutors`, et `spark.executor.memory`.

    ![Configurer le serveur Thrift Spark](./media/hdinsight-apache-spark-resource-manager/spark-thrift-server-1.png)    
* Développez hello **personnalisé spark-thrift-sparkconf** paramètre de catégorie tooupdate hello `spark.executor.cores`.

    ![Configurer le serveur Thrift Spark](./media/hdinsight-apache-spark-resource-manager/spark-thrift-server-2.png)

### <a name="how-do-i-change-hello-driver-memory-of-hello-spark-thrift-server"></a>Comment modifier les hello pilote de mémoire de hello Spark Thrift serveur ?
Spark Thrift Server pilote mémoire est configuré too25 de taille du nœud principal RAM hello, condition hello totale de mémoire RAM de nœud principal de hello est supérieur à 14 Go. Vous pouvez utiliser hello Ambari UI toochange hello pilote configuration de la mémoire, comme illustré ci-dessous.

* À partir de hello Ambari UI, cliquez sur **Spark**, cliquez sur **configurations**, développez **avancé spark-env**, puis indiquez la valeur hello pour **spark_thrift_cmd_opts**.

    ![Configurer la mémoire RAM du serveur Thrift Spark](./media/hdinsight-apache-spark-resource-manager/spark-thrift-server-ram.png)

## <a name="i-do-not-use-bi-with-spark-cluster-how-do-i-take-hello-resources-back"></a>Je n’utilise pas d’outils décisionnels avec le cluster Spark. Comment rétablir les ressources hello en ?
Étant donné que nous utilisons l’allocation dynamique Spark, hello uniquement les ressources qui sont consommés par le serveur de thrift hello ressources sont des formes de base hello deux applications. tooreclaim ces ressources, que vous devez arrêter hello Thrift Server services s’exécutant sur un cluster de hello.

1. À partir de hello Ambari UI, à partir du volet de gauche hello, cliquez sur **Spark**.
2. Dans la page suivante de hello, cliquez sur **Spark Thrift serveurs**.

    ![Redémarrer le serveur Thrift](./media/hdinsight-apache-spark-resource-manager/restart-thrift-server-1.png)
3. Vous devez voir les deux headnodes hello sur quel hello Spark Thrift Server est en cours d’exécution. Cliquez sur un des hello headnodes.

    ![Redémarrer le serveur Thrift](./media/hdinsight-apache-spark-resource-manager/restart-thrift-server-2.png)
4. page suivante de Hello répertorie tous les services de hello en cours d’exécution sur ce nœud principal. À partir de la liste de hello cliquez tooSpark suivant du bouton de liste déroulante hello Thrift serveur, puis cliquez sur **arrêter**.

    ![Redémarrer le serveur Thrift](./media/hdinsight-apache-spark-resource-manager/restart-thrift-server-3.png)
5. Répétez ces étapes sur hello autre nœud principal également.

## <a name="my-jupyter-notebooks-are-not-running-as-expected-how-can-i-restart-hello-service"></a>Mes blocs-notes Jupyter ne s’exécutent pas comme prévu. Comment puis-je redémarrer le service de hello ?
Lancez hello l’interface utilisateur de Ambari Web comme indiqué ci-dessus. Dans le volet de navigation gauche hello, cliquez sur **Notebook**, cliquez sur **Actions Service**, puis cliquez sur **redémarrer tous les**. Cela démarre hello Notebook service sur tous les hello headnodes.

    ![Restart Jupyter](./media/hdinsight-apache-spark-resource-manager/restart-jupyter.png "Restart Jupyter")

## <a name="how-do-i-know-if-i-am-running-out-of-resources"></a>Comment savoir si mes ressources sont épuisées ?
Lancez hello fils UI comme indiqué ci-dessus. Dans la table des métriques de Cluster sur l’écran hello, vérifiez les valeurs de **mémoire utilisée** et **mémoire totale** colonnes. Si les valeurs hello 2 sont très proches, il peut-être pas suffisamment ressources toostart hello prochaine application. Hello valable toohello **VCores utilisé** et **VCores Total** colonnes. En outre, dans la vue principale de hello, s’il existe une application séjourné dans **accepté** état et la passe ne pas par **en cours d’exécution** ni **n’a pas pu** d’état, cela peut également indiquer une qu’il ne reçoit pas suffisamment toostart de ressources.

    ![Resource Limit](./media/hdinsight-apache-spark-resource-manager/resource-limit.png "Resource Limit")

## <a name="how-do-i-kill-a-running-application-toofree-up-resource"></a>Comment mettre fin en cours d’exécution toofree application ressource ?
1. Bonjour fils UI, à partir du volet de gauche hello, cliquez sur **en cours d’exécution**. À partir de la liste de hello des applications en cours d’exécution, déterminez hello application toobe arrêtés, puis cliquez sur hello **ID**.

    ![Arrêter App1](./media/hdinsight-apache-spark-resource-manager/kill-app1.png "Arrêter App1")

2. Cliquez sur **arrêter l’Application** sur hello coin supérieur droit, puis cliquez sur **OK**.

    ![Arrêter App2](./media/hdinsight-apache-spark-resource-manager/kill-app2.png "Arrêter App2")

## <a name="see-also"></a>Voir aussi
* [Track and debug jobs running on an Apache Spark cluster in HDInsight (Suivi et débogage des tâches en cours d’exécution sur un cluster Apache Spark dans HDInsight)](hdinsight-apache-spark-job-debugging.md)

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
