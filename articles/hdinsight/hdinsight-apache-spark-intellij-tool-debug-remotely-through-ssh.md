---
title: "Kit de ressources Azure pour IntelliJ : déboguer des applications Spark à distance via SSH | Microsoft Docs"
description: "Obtenir des instructions sur la façon dont les clusters toouse outils HDInsight dans la boîte à outils Azure pour les applications de toodebug IntelliJ à distance sur HDInsight via SSH"
keywords: "déboguer à distance intellij, débogage à distance intellij, ssh, intellij, hdinsight, déboguer intellij, débogage"
services: hdinsight
documentationcenter: 
author: jejiang
manager: DJ
editor: Jenny Jiang
tags: azure-portal
ms.assetid: 
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: 
ms.devlang: 
ms.topic: article
ms.date: 08/24/2017
ms.author: Jenny Jiang
ms.openlocfilehash: bf3ab9d04c2ff9fcb6bbbdeefb11f55a12fbd845
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="debug-spark-applications-on-an-hdinsight-cluster-with-azure-toolkit-for-intellij-through-ssh"></a>Déboguez des applications Spark sur un cluster HDInsight avec le kit de ressources Azure pour IntelliJ via SSH

Cet article fournit des instructions sur la façon de toouse outils HDInsight dans la boîte à outils Azure pour les applications de toodebug IntelliJ à distance sur un cluster HDInsight. toodebug votre projet, vous pouvez également afficher hello [applications déboguer HDInsight Spark avec la boîte à outils Azure pour IntelliJ](https://channel9.msdn.com/Series/AzureDataLake/Debug-HDInsight-Spark-Applications-with-Azure-Toolkit-for-IntelliJ) vidéo.

**Configuration requise**

* **Outils HDInsight dans le kit de ressources Azure pour IntelliJ**. Cet outil fait partie du kit de ressources Azure pour IntelliJ. Pour plus d’informations, consultez [Installation du kit de ressources Azure pour IntelliJ](https://docs.microsoft.com/en-us/azure/azure-toolkit-for-intellij-installation).
* **Kit de ressources Azure pour IntelliJ**. Utilisez ces applications de Spark toocreate Kit de ressources pour un cluster HDInsight. Pour plus d’informations, suivez les instructions de hello dans [utilisez Azure Toolkit pour les applications de Spark IntelliJ toocreate pour un cluster HDInsight](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-apache-spark-intellij-tool-plugin).
* **Service HDInsight SSH avec gestion de nom d’utilisateur et de mot de passe**. Pour plus d’informations, consultez [connecter tooHDInsight (Hadoop) à l’aide de SSH](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-linux-use-ssh-unix) et [utiliser SSH tunneling tooaccess Ambari web de l’interface utilisateur, JobHistory, NameNode, Oozie et autres interfaces utilisateur web](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-linux-ambari-ssh-tunnel). 
 

## <a name="create-a-spark-scala-application-and-configure-it-for-remote-debugging"></a>Créer une application Spark Scala et la configurer pour le débogage à distance

1. Démarrez IntelliJ IDEA et créez un projet. Bonjour **nouveau projet** boîte de dialogue zone, hello suivant :

   a. Sélectionnez **HDInsight**. 

   b. Sélectionnez un modèle Java ou Scala en fonction de vos préférences. Sélectionnez entre hello options suivantes :

      - **Spark sur HDInsight (Scala)**

      - **Spark sur HDInsight (Java)**

      - **Spark sur exemple d’exécution de cluster HDInsight (Scala)**

      Cet exemple utilise un modèle **Spark sur exemple d’exécution de cluster HDInsight (Scala)**.

   c. Bonjour **outil de génération** , sélectionnez une des hello suivant, selon le besoin de tooyour :

      - **Maven**, pour la prise en charge de l’Assistant de création de projets Scala

      -  **SBT**, pour la gestion des dépendances de hello et la création de projet de Scala hello 

      ![Créer un projet de débogage](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-create-projectfor-debug-remotely.png)

   d. Sélectionnez **Suivant**.     
 
3. Bonjour suivant **nouveau projet** fenêtre, hello suivant :

   ![Sélectionnez hello Spark SDK](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-new-project.png)

   a. Entrez un nom de projet et un emplacement de projet.

   b. Bonjour **projet SDK** la liste déroulante, sélectionnez **Java 1.8** pour **nouvelles 2.x** de cluster ou sélectionnez **Java 1.7** pour **Spark 1. x** cluster.

   c. Bonjour **Spark Version** la liste déroulante, Assistant de création de projet Scala hello intègre version correcte de hello pour le Kit de développement logiciel Spark et Scala SDK. Si la version du cluster spark hello est antérieure à la version 2.0, sélectionnez **nouvelles 1.x**. Sinon, sélectionnez **Spark 2.x.** La version utilisée dans cet exemple est **Spark 2.0.2 (Scala 2.11.8)**.

   d. Sélectionnez **Terminer**.

4. Sélectionnez **src** > **principal** > **scala** tooopen votre code dans un projet de hello. Cet exemple utilise hello **SparkCore_wasbloTest** script.

5. tooaccess hello **modifier les Configurations** menu, icône hello select dans le coin supérieur droit de hello. Dans ce menu, vous pouvez créer ou modifier des configurations hello pour le débogage distant.

   ![Modifier les configurations](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-edit-configurations.png) 

6. Bonjour **Configurations d’exécution/débogage** boîte de dialogue, sélectionnez hello plus signe (**+**). Puis sélectionnez hello **soumettre un travail Spark** option.

   ![Ajouter une nouvelle configuration](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-add-new-Configuration.png)
7. Entrez les informations sur le **Nom**, le **Cluster Spark** et le **Nom principal de la classe**. Puis sélectionnez **Configuration avancée**. 

   ![Exécuter le débogage des configurations](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-run-debug-configurations.png)

8. Bonjour **Spark soumission Advanced Configuration** boîte de dialogue, sélectionnez **débogage distant d’activer les Spark**. Entrez le nom d’utilisateur de hello SSH, puis entrez un mot de passe ou utiliser un fichier de clé privée. configuration de hello toosave, sélectionnez **OK**.

   ![Activer le débogage à distance Spark](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-enable-spark-remote-debug.png)

9. configuration de Hello est désormais enregistrée avec nom hello fourni. Détails de configuration hello tooview, nom de la configuration sélectionnez hello. toomake change, sélectionnez **modifier les Configurations de**. 

10. Après avoir terminé les paramètres de configuration hello, vous pouvez exécuter des projets de hello sur un cluster distant de hello ou effectuer un débogage à distance.

## <a name="learn-how-tooperform-remote-debugging"></a>Découvrez comment tooperform le débogage distant
### <a name="scenario-1-perform-remote-run"></a>Scénario 1 : effectuer une exécution à distance

Dans cette section, nous vous indiquons comment toodebug exécuteurs et des pilotes.

    import org.apache.spark.{SparkConf, SparkContext}

    object LogQuery {
      val exampleApacheLogs = List(
        """10.10.10.10 - "FRED" [18/Jan/2013:17:56:07 +1100] "GET http://images.com/2013/Generic.jpg
          | HTTP/1.1" 304 315 "http://referall.com/" "Mozilla/4.0 (compatible; MSIE 7.0; Windows NT 5.1;
          | GTB7.4; .NET CLR 2.0.50727; .NET CLR 3.0.04506.30; .NET CLR 3.0.04506.648; .NET CLR
          | 3.5.21022; .NET CLR 3.0.4506.2152; .NET CLR 1.0.3705; .NET CLR 1.1.4322; .NET CLR
          | 3.5.30729; Release=ARP)" "UD-1" - "image/jpeg" "whatever" 0.350 "-" - "" 265 923 934 ""
          | 62.24.11.25 images.com 1358492167 - Whatup""".stripMargin.lines.mkString,
        """10.10.10.10 - "FRED" [18/Jan/2013:18:02:37 +1100] "GET http://images.com/2013/Generic.jpg
          | HTTP/1.1" 304 306 "http:/referall.com" "Mozilla/4.0 (compatible; MSIE 7.0; Windows NT 5.1;
          | GTB7.4; .NET CLR 2.0.50727; .NET CLR 3.0.04506.30; .NET CLR 3.0.04506.648; .NET CLR
          | 3.5.21022; .NET CLR 3.0.4506.2152; .NET CLR 1.0.3705; .NET CLR 1.1.4322; .NET CLR
          | 3.5.30729; Release=ARP)" "UD-1" - "image/jpeg" "whatever" 0.352 "-" - "" 256 977 988 ""
          | 0 73.23.2.15 images.com 1358492557 - Whatup""".stripMargin.lines.mkString
      )
      def main(args: Array[String]) {
        val sparkconf = new SparkConf().setAppName("Log Query")
        val sc = new SparkContext(sparkconf)
        val dataSet = sc.parallelize(exampleApacheLogs)
        // scalastyle:off
        val apacheLogRegex =
          """^([\d.]+) (\S+) (\S+) \[([\w\d:/]+\s[+\-]\d{4})\] "(.+?)" (\d{3}) ([\d\-]+) "([^"]+)" "([^"]+)".*""".r
        // scalastyle:on
        /** Tracks hello total query count and number of aggregate bytes for a particular group. */
        class Stats(val count: Int, val numBytes: Int) extends Serializable {
          def merge(other: Stats): Stats = new Stats(count + other.count, numBytes + other.numBytes)
          override def toString: String = "bytes=%s\tn=%s".format(numBytes, count)
        }
        def extractKey(line: String): (String, String, String) = {
          apacheLogRegex.findFirstIn(line) match {
            case Some(apacheLogRegex(ip, _, user, dateTime, query, status, bytes, referer, ua)) =>
              if (user != "\"-\"") (ip, user, query)
              else (null, null, null)
            case _ => (null, null, null)
          }
        }
        def extractStats(line: String): Stats = {
          apacheLogRegex.findFirstIn(line) match {
            case Some(apacheLogRegex(ip, _, user, dateTime, query, status, bytes, referer, ua)) =>
              new Stats(1, bytes.toInt)
            case _ => new Stats(1, 0)
          }
        }
        
        dataSet.map(line => (extractKey(line), extractStats(line)))
          .reduceByKey((a, b) => a.merge(b))
          .collect().foreach{
          case (user, query) => println("%s\t%s".format(user, query))}

        sc.stop()
      }
    }


1. Définir des points de saut, puis sélectionnez hello **déboguer** icône.

   ![Sélectionnez l’icône de débogage hello](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-debug-icon.png)

2. Lorsque l’exécution du programme hello atteint un point de rupture hello, vous voyez un **pilote** onglet et deux **exécuteur** onglets Bonjour **débogueur** volet. Sélectionnez hello **Resume programme** toocontinue icône exécuter le code hello, qui ensuite atteint le point d’arrêt suivant de hello et se concentre sur hello correspondant **exécuteur** onglet. Vous pouvez consulter les journaux d’exécution hello sur hello correspondant **Console** onglet.

   ![Onglet Débogage](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-debugger-tab.png)

### <a name="scenario-2-perform-remote-debugging-and-bug-fixing"></a>Scénario 2 : effectuer un débogage à distance et une résolution des bogues
Dans cette section, nous vous indiquons comment toodynamically mise à jour hello valeur de la variable à l’aide de hello IntelliJ fonctionnalité pour une solution simple de débogage. Bonjour exemple de code suivant, une exception est levée, car le fichier hello cible existe déjà.
  
        import org.apache.spark.SparkConf
        import org.apache.spark.SparkContext

        object SparkCore_WasbIOTest {
          def main(arg: Array[String]): Unit = {
            val conf = new SparkConf().setAppName("SparkCore_WasbIOTest")
            val sc = new SparkContext(conf)
            val rdd = sc.textFile("wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")

            // Find hello rows that have only one digit in hello sixth column.
            val rdd1 = rdd.filter(s => s.split(",")(6).length() == 1)

            try {
              var target = "wasb:///HVACout2_testdebug1";
              rdd1.saveAsTextFile(target);
            } catch {
              case ex: Exception => {
                throw ex;
              }
            }
          }
        }


#### <a name="tooperform-remote-debugging-and-bug-fixing"></a>débogage distant tooperform et résolution des bogues
1. Configurer les deux points de rupture, puis sélectionnez hello **déboguer** hello de toostart icône processus de débogage distant.

2. code de Hello s’arrête au premier point de rupture hello et paramètre hello et des informations sur les variables sont affichés dans hello **Variables** volet. 

3. Sélectionnez hello **Resume programme** toocontinue d’icône. code de Hello s’arrête au deuxième point de hello. exception de Hello est interceptée comme prévu.

  ![Lever l’erreur](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-throw-error.png) 

4. Sélectionnez hello **Resume programme** icône Nouveau. Hello **HDInsight Spark soumission** affiche une erreur « Échec de l’exécution de la tâche ».

  ![Soumission de l’erreur](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-error-submission.png) 

5. toodynamically mise à jour hello valeur de la variable à l’aide des fonctionnalités de débogage IntelliJ hello, sélectionnez **déboguer** à nouveau. Hello **Variables** volet s’affiche à nouveau. 

6. Cible de hello avec le bouton droit sur hello **déboguer** onglet, puis sélectionnez **définir la valeur**. Ensuite, entrez une nouvelle valeur pour la variable de hello. Puis sélectionnez **entrée** valeur hello de toosave. 

  ![Définir la valeur](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-set-value.png) 

7. Sélectionnez hello **Resume programme** programme de hello icône toocontinue toorun. Cette fois-ci, aucune exception n’est interceptée. Vous pouvez voir que ce projet hello s’exécute correctement, sans aucune exception.

  ![Déboguer sans exception](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-debug-without-exception.png)

## <a name="seealso"></a>Étapes suivantes
* [Vue d’ensemble : Apache Spark sur Azure HDInsight](hdinsight-apache-spark-overview.md)

### <a name="demo"></a>Démonstration
* Créez un projet Scala (vidéo) : [Créer des applications Scala Spark](https://channel9.msdn.com/Series/AzureDataLake/Create-Spark-Applications-with-the-Azure-Toolkit-for-IntelliJ)
* Débogage distant (vidéo) : [utilisation Azure Toolkit pour les applications de Spark IntelliJ toodebug à distance sur un cluster HDInsight](https://channel9.msdn.com/Series/AzureDataLake/Debug-HDInsight-Spark-Applications-with-Azure-Toolkit-for-IntelliJ)

### <a name="scenarios"></a>Scénarios
* [Spark avec BI : effectuez une analyse interactive des données à l’aide de Spark dans HDInsight avec des outils BI](hdinsight-apache-spark-use-bi-tools.md)
* [Spark avec Machine Learning : Spark utilisation dans tooanalyze HDInsight à l’aide des données HVAC de température de génération](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [Spark avec Machine Learning : Spark utilisation dans résultats de l’inspection alimentaires toopredict HDInsight](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [Diffusion en continu de Spark : Spark utilisation dans les applications de diffusion en continu en temps réel toobuild HDInsight](hdinsight-apache-spark-eventhub-streaming.md)
* [Analyse des journaux de site web à l’aide de Spark dans HDInsight](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a>Créer et exécuter des applications
* [Créer une application autonome avec Scala](hdinsight-apache-spark-create-standalone-application.md)
* [Exécuter des tâches à distance avec Livy sur un cluster Spark](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a>Outils et extensions
* [Utilisez la boîte à outils Azure pour les applications de Spark IntelliJ toocreate pour un cluster HDInsight](hdinsight-apache-spark-intellij-tool-plugin.md)
* [Utilisez la boîte à outils Azure pour les applications de Spark IntelliJ toodebug à distance via le VPN](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [Utiliser HDInsight Tools pour IntelliJ avec Hortonworks Sandbox](hdinsight-tools-for-intellij-with-hortonworks-sandbox.md)
* [Utilisez les outils HDInsight dans la boîte à outils Azure pour les applications de Spark toocreate Eclipse](hdinsight-apache-spark-eclipse-tool-plugin.md)
* [Utiliser des bloc-notes Zeppelin avec un cluster Spark sur HDInsight](hdinsight-apache-spark-zeppelin-notebook.md)
* [Cluster de noyaux disponibles pour le bloc-notes jupyter Bonjour Spark sur HDInsight](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [Utiliser des packages externes avec les blocs-notes Jupyter](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [Installer Notebook sur votre ordinateur et vous connecter tooan cluster HDInsight Spark](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a>Gestion des ressources
* [Gérer les ressources de cluster d’Apache Spark hello dans Azure HDInsight](hdinsight-apache-spark-resource-manager.md)
* [Track and debug jobs running on an Apache Spark cluster in HDInsight (Suivi et débogage des tâches en cours d’exécution sur un cluster Apache Spark dans HDInsight)](hdinsight-apache-spark-job-debugging.md)
