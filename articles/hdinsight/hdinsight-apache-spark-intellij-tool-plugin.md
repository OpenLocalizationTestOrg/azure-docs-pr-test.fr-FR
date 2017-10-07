---
title: "Kit de ressources Azure pour IntelliJ : créer des applications Spark pour un cluster HDInsight | Microsoft Docs"
description: "Utilisez hello boîte à outils Azure pour les applications de Spark toodevelop IntelliJ écrites dans Scala et les envoyer tooan cluster HDInsight Spark."
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 73304272-6c8b-482e-af7c-cd25d95dab4d
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/24/2017
ms.author: nitinme
ms.openlocfilehash: 22cce014bb848a54e198e77a50bf13448012310e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-toolkit-for-intellij-toocreate-spark-applications-for-an-hdinsight-cluster"></a>Utilisez la boîte à outils Azure pour les applications de Spark IntelliJ toocreate pour un cluster HDInsight

Utilisez hello boîte à outils Azure pour les applications de Spark toodevelop plug-in IntelliJ écrites dans Scala, puis les envoyer tooan cluster HDInsight Spark directement à partir de l’environnement de développement intégré IntelliJ hello (IDE). Vous pouvez utiliser hello plug-in de plusieurs façons :

* Développer et soumettre une application Scala Spark sur un cluster HDInsight Spark.
* Accéder à vos ressources de cluster Azure HDInsight Spark.
* Développer et exécuter une application Scala Spark localement.

toocreate votre projet, le hello de vue [créer des Applications de Spark avec hello Azure Toolkit pour IntelliJ](https://channel9.msdn.com/Series/AzureDataLake/Create-Spark-Applications-with-the-Azure-Toolkit-for-IntelliJ) vidéo.

> [!IMPORTANT]
> Vous pouvez utiliser ce plug-in toocreate et soumettre des applications uniquement pour un cluster HDInsight Spark sur Linux.
> 

## <a name="prerequisites"></a>Composants requis

- Un cluster Apache Spark sur HDInsight Linux. Pour obtenir des instructions, consultez [Création de clusters Apache Spark dans Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).
- Kit de développement logiciel (SDK) Oracle Java. Vous pouvez l’installer à partir de hello [site Web d’Oracle](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).
- IntelliJ IDEA. Cet article utilise la version 2017.1. Vous pouvez l’installer à partir de hello [site Web de JetBrains](https://www.jetbrains.com/idea/download/).

## <a name="install-azure-toolkit-for-intellij"></a>Installer le kit de ressources Azure pour IntelliJ
Pour plus d’informations, consultez [Installation du kit de ressources Azure pour IntelliJ](../azure-toolkit-for-intellij-installation.md).

## <a name="sign-in-tooyour-azure-subscription"></a>Se connecter tooyour abonnement Azure

1. Démarrez hello IntelliJ IDE et ouvrez l’Explorateur d’Azure. Sur hello **vue** menu, sélectionnez **fenêtres Outil**, puis sélectionnez **Explorateur Azure**.
       
   ![lien d’Explorateur Azure Hello](./media/hdinsight-apache-spark-intellij-tool-plugin/show-azure-explorer.png)

2. Avec le bouton hello **Azure** nœud et sélectionnez **connexion**.

3. Bonjour **Azure Sign In** boîte de dialogue, sélectionnez **connecter**, puis entrez vos informations d’identification Azure.

    ![Bonjour Azure boîte de dialogue Connexion](./media/hdinsight-apache-spark-intellij-tool-plugin/view-explorer-2.png)

4. Une fois que vous êtes connecté, hello **sélectionnez les abonnements** boîte de dialogue propose toutes hello abonnements Azure qui sont associées aux hello des informations d’identification. Sélectionnez hello **sélectionnez** bouton.

    ![boîte de dialogue Sélectionnez les abonnements Hello](./media/hdinsight-apache-spark-intellij-tool-plugin/Select-Subscriptions.png)

5. Sur hello **Explorateur Azure** onglet, développez **HDInsight** hello tooview des clusters HDInsight Spark qui se trouvent dans votre abonnement.
   
    ![Clusters HDInsight Spark dans l’Explorateur Azure](./media/hdinsight-apache-spark-intellij-tool-plugin/view-explorer-3.png)

6. tooview hello ressources (par exemple, les comptes de stockage) qui sont associés au cluster de hello, vous pouvez développer davantage un nœud de nom de cluster.
   
    ![Nœud de nom de cluster développé](./media/hdinsight-apache-spark-intellij-tool-plugin/view-explorer-4.png)

## <a name="run-a-spark-scala-application-on-an-hdinsight-spark-cluster"></a>Exécuter une application Scala Spark sur un cluster HDInsight Spark

1. Démarrez IntelliJ IDEA et créez un projet. Bonjour **nouveau projet** boîte de dialogue zone, hello suivant : 

   a. Sélectionnez **HDInsight** > **Spark sur HDInsight (Scala)**.

   b. Bonjour **outil de génération** , sélectionnez une des hello suivant, selon le besoin de tooyour :

      * **Maven**, pour la prise en charge de l’Assistant de création de projets Scala
      * **SBT**, pour la gestion des dépendances de hello et la création de projet de Scala hello

    ![boîte de dialogue Nouveau projet Hello](./media/hdinsight-apache-spark-intellij-tool-plugin/create-hdi-scala-app.png)

2. Sélectionnez **Suivant**.

3. Assistant de création de projets Scala Hello détecte automatiquement si vous avez installé hello Scala plug-in. Sélectionnez **Installer**.

   ![Vérification de l’installation du plug-in Scala](./media/hdinsight-apache-spark-intellij-tool-plugin/Scala-Plugin-check-Reminder.PNG) 

4. hello de toodownload Scala plug-in, sélectionnez **OK**. Suivez les instructions de hello toorestart IntelliJ. 

   ![boîte de dialogue installation Hello Scala plug-in](./media/hdinsight-apache-spark-intellij-tool-plugin/Choose-Scala-Plugin.PNG)

5. Bonjour **nouveau projet** fenêtre, hello suivant :  

    ![En sélectionnant hello Spark SDK](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-new-project.png)

   a. Entrez un nom de projet et un emplacement.

   b. Bonjour **projet SDK** la liste déroulante, sélectionnez **Java 1.8** pour le cluster de hello Spark 2.x, ou sélectionnez **Java 1.7** pour le cluster de hello Spark 1.x.

   c. Bonjour **version de Spark** la liste déroulante, Assistant de création de projet Scala intègre version correcte de hello pour le Kit de développement logiciel Spark et Scala SDK. Si la version du cluster Spark hello est antérieure à la version 2.0, sélectionnez **nouvelles 1.x**. Sinon, sélectionnez **Spark 2.x**. La version utilisée dans cet exemple est **Spark 2.0.2 (Scala 2.11.8)**.

6. Sélectionnez **Terminer**.

7. projet de Spark Hello crée automatiquement un artefact pour vous. artefact de hello tooview, hello suivant :

   a. Sur hello **fichier** menu, sélectionnez **Structure de projet**.

   b. Bonjour **Structure de projet** boîte de dialogue, sélectionnez **artefacts** tooview hello par défaut artefact qui est créé. Vous pouvez également créer vos propres artefact en sélectionnant le signe plus hello (**+**).

      ![Informations d’artefact dans la boîte de dialogue hello](./media/hdinsight-apache-spark-intellij-tool-plugin/default-artifact.png)
      
8. Ajoutez votre code source d’application de manière hello suivante :

   a. Dans l’Explorateur de projets, cliquez sur **src**, pointez trop**nouveau**, puis sélectionnez **Scala classe**.
      
      ![Commandes pour la création d’une classe Scala à partir de l’Explorateur de projets](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-spark-scala-code.png)

   b. Bonjour **créer une nouvelle classe Scala** boîte de dialogue zone, fournissez un nom, sélectionnez **objet** Bonjour **type** zone, puis sélectionnez **OK**.
      
      ![Boîte de dialogue Créer une classe Scala](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-spark-scala-code-object.png)

   c. Bonjour **MyClusterApp.scala** file, collez hello suivant de code. Hello code lit les données de salutation HVAC.csv (disponible sur tous les clusters HDInsight Spark), récupère les lignes hello qui ont un seul chiffre dans la colonne de septième hello dans un fichier CSV hello et écrit la sortie de hello trop**/HVACOut** sous la valeur par défaut de hello conteneur de stockage pour le cluster de hello.

        import org.apache.spark.SparkConf
        import org.apache.spark.SparkContext
    
        object MyClusterApp{
            def main (arg: Array[String]): Unit = {
            val conf = new SparkConf().setAppName("MyClusterApp")
            val sc = new SparkContext(conf)
    
            val rdd = sc.textFile("wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")
    
            //find hello rows that have only one digit in hello seventh column in hello CSV file
            val rdd1 =  rdd.filter(s => s.split(",")(6).length() == 1)
    
            rdd1.saveAsTextFile("wasb:///HVACOut")
            }
    
        }

9. Exécutez l’application hello sur un cluster HDInsight Spark en procédant comme suit de hello :

   a. Dans l’Explorateur de projets, cliquez sur le nom de projet hello et sélectionnez **tooHDInsight de soumettre une Application de Spark**.
      
      ![Hello commande tooHDInsight de soumettre une Application de Spark](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-submit-spark-app-1.png)

   b. Vous est demandée tooenter vos informations d’identification de l’abonnement Azure. Bonjour **Spark soumission** boîte de dialogue, fournissez hello valeurs suivantes, puis sélectionnez **Submit**.
      
      * Pour **au service de clusters (Linux uniquement)**, sélectionnez hello cluster HDInsight Spark sur lequel vous souhaitez toorun votre application.

      * Sélectionnez un artefact de projet de IntelliJ hello ou sélectionnez-en un dans le disque dur de hello.

      * Bonjour **nom de la classe principale** zone, les points de suspension hello select (**...** ), sélectionnez la classe principale hello dans votre code source d’application, puis sélectionnez **OK**.

        ![boîte de dialogue de sélection de la classe principale Hello](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-submit-spark-app-3.png)

      * Car le code de l’application hello dans cet exemple ne pas nécessitent des arguments de ligne de commande ou référencer des fichiers ou des fichiers JAR, vous pouvez laisser hello restant zones vides. Après avoir fourni toutes les informations de hello, boîte de dialogue hello doit ressembler à hello suivant l’image.
        
        ![boîte de dialogue de soumission de Spark Hello](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-submit-spark-app-2.png)

   c. Hello **Spark soumission** onglet en bas de hello de fenêtre hello doit commencer à afficher la progression de hello. Vous pouvez également arrêter l’application hello en sélectionnant le bouton de hello rouge Bonjour **Spark soumission** fenêtre.
      
      ![fenêtre de soumission de Spark Hello](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-spark-app-result.png)
      
      toolearn tooaccess hello sortie des tâches, voir hello « accès et de gérer les clusters HDInsight Spark à l’aide de la boîte à outils Azure pour IntelliJ » plus loin dans cet article.

## <a name="run-or-debug-a-spark-scala-application-on-an-hdinsight-spark-cluster"></a>Exécuter ou déboguer comme une application Scala Spark sur un cluster HDInsight Spark
Nous recommandons également d’un autre moyen de l’envoi de cluster de toohello application hello Spark. Vous pouvez le faire en définissant des paramètres de hello Bonjour **configurations d’exécution/débogage** IDE. Pour obtenir des instructions, reportez-vous à la rubrique [Déboguer des applications Spark à distance sur un cluster HDInsight avec le kit de ressources Azure pour IntelliJ via SSH](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-apache-spark-intellij-tool-debug-remotely-through-ssh).

## <a name="access-and-manage-hdinsight-spark-clusters-by-using-azure-toolkit-for-intellij"></a>Accéder aux clusters HDInsight Spark et les gérer à l’aide du kit de ressources Azure pour IntelliJ
Vous pouvez effectuer diverses opérations à l’aide du kit de ressources Azure pour IntelliJ.

### <a name="access-hello-job-view"></a>Affichage des travaux hello Access
1. Dans l’Explorateur d’Azure, développez **HDInsight**, développez le nom du cluster Spark hello, puis sélectionnez **travaux**.  

    ![Nœud Vue de la tâche](./media/hdinsight-apache-spark-intellij-tool-plugin/job-view-node.png)

2. Dans le volet droit de hello, hello **Spark travail vue** onglet affiche toutes les applications hello qui ont été exécutées sur le cluster de hello. Sélectionnez le nom hello d’application hello pour lequel vous souhaitez toosee plus d’informations.

    ![Détails de l’application](./media/hdinsight-apache-spark-intellij-tool-plugin/view-job-logs.png)

3. toodisplay en cours d’exécution travail informations de base, pointez sur le graphique de travail hello. graphique de phases tooview hello et informations que chaque tâche génère, sélectionnez un nœud sur le graphique de travail hello.

    ![Détails des étapes du travail](./media/hdinsight-apache-spark-intellij-tool-plugin/Job-graph-stage-info.png)

4. tooview utilisé fréquemment les journaux, tels que *pilote Stderr*, *pilote Stdout*, et *des informations de répertoire*, sélectionnez hello **journal** onglet.

    ![Détails des journaux](./media/hdinsight-apache-spark-intellij-tool-plugin/Job-log-info.png)

5. Vous pouvez également afficher hello historique de Spark UI et hello UI fils (au niveau de l’application hello) en sélectionnant un lien en haut de hello de fenêtre hello.

### <a name="access-hello-spark-history-server"></a>Serveur d’accès hello Spark historique
1. Dans Azure Explorer, développez **HDInsight**, cliquez avec le bouton droit sur le nom de votre cluster Spark et sélectionnez **Open Spark History UI** (Ouvrir l’interface utilisateur de l’historique Spark). 

2. Lorsque vous y êtes invité, entrez les informations d’identification administrateur du cluster hello que vous avez spécifié lorsque vous configurez le cluster de hello.

3. Tableau de bord de serveur hello Spark historique, vous pouvez utiliser toolook de nom d’application hello pour application hello que vous venez d’en cours d’exécution. Bonjour précédant le code, vous définir le nom de l’application hello en utilisant `val conf = new SparkConf().setAppName("MyClusterApp")`. Par conséquent, le nom de votre application Spark est **MyClusterApp**.

### <a name="start-hello-ambari-portal"></a>Démarrer le portail de Ambari hello
1. Dans Azure Explorer, développez **HDInsight**, cliquez avec le bouton droit sur le nom de votre cluster Spark et sélectionnez **Open Cluster Management Portal (Ambari)** (Ouvrir le portail de gestion des clusters (Ambari)). 

2. Lorsque vous y êtes invité, entrez les informations d’identification du admin de hello pour le cluster de hello. Vous avez spécifié ces informations d’identification au cours du processus d’installation de cluster hello.

### <a name="manage-azure-subscriptions"></a>Gérer les abonnements Azure
Par défaut, Azure Toolkit pour IntelliJ répertorie les clusters de Spark hello à partir de tous vos abonnements Azure. Si nécessaire, vous pouvez spécifier des abonnements hello que vous souhaitez tooaccess. 

1. Dans l’Explorateur d’Azure, avec le bouton droit hello **Azure** nœud racine, puis sélectionnez **gérer les abonnements**. 

2. Dans la boîte de dialogue hello, désactivez hello cases à cocher suivants toohello abonnements que vous ne souhaitez tooaccess, puis sélectionnez **fermer**. Vous pouvez également sélectionner **se déconnecter** si vous souhaitez toosign dans votre abonnement Azure.

## <a name="run-a-spark-scala-application-locally"></a>Exécuter une application Spark Scala localement
Vous pouvez utiliser boîte à outils Azure pour les applications de Spark Scala IntelliJ toorun localement sur votre station de travail. Hello applications généralement ne doivent accéder à des ressources de toocluster, telles que les conteneurs de stockage, et vous pouvez exécuter et tester localement.

### <a name="prerequisite"></a>Configuration requise
Lorsque vous exécutez l’application hello locale Spark Scala sur un ordinateur Windows, vous pouvez obtenir une exception, comme expliqué dans [SPARK-2356](https://issues.apache.org/jira/browse/SPARK-2356). exception de Hello se produit parce que WinUtils.exe est manquant sur Windows. 

tooresolve cette erreur, [télécharger hello exécutable](http://public-repo-1.hortonworks.com/hdp-win-alpha/winutils.exe) emplacement tooa comme **C:\WinUtils\bin**. Ensuite, ajoutez la variable d’environnement hello **HADOOP_HOME**et la valeur hello de variable de hello trop**C\WinUtils**.

### <a name="run-a-local-spark-scala-application"></a>Exécuter une application Spark Scala locale
1. Démarrez IntelliJ IDEA et créez un projet. 

2. Bonjour **nouveau projet** boîte de dialogue zone, hello suivant :
   
    a. Sélectionnez **HDInsight** > **Spark on HDInsight Local Run Sample (Scala)** (Exemple d’exécution locale de Spark sur HDInsight [Scala]).

    b. Bonjour **outil de génération** , sélectionnez une des hello suivant, selon le besoin de tooyour :

      * **Maven**, pour la prise en charge de l’Assistant de création de projets Scala
      * **SBT**, pour la gestion des dépendances de hello et la création de projet de Scala hello

    ![boîte de dialogue Nouveau projet Hello](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-spark-app-local-run.png)

3. Sélectionnez **Suivant**.
 
4. Dans la fenêtre suivante de hello, procédez comme hello suivant :
   
    a. Entrez un nom de projet et un emplacement.

    b. Bonjour **projet SDK** liste déroulante, sélectionnez une version de Java est postérieure à la version 1.7.

    c. Bonjour **Spark Version** liste déroulante, sélectionnez hello version de Scala que toouse : Scala 2.11.x pour Spark 2.0 ou Scala 2.10.x pour Spark 1.6.

    ![boîte de dialogue Nouveau projet Hello](./media/hdinsight-apache-spark-intellij-tool-plugin/Create-local-project.PNG)

5. Sélectionnez **Terminer**.

6. modèle de Hello ajoute un exemple de code (**LogQuery**) sous hello **src** dossier que vous pouvez exécuter localement sur votre ordinateur.
   
    ![Emplacement de LogQuery](./media/hdinsight-apache-spark-intellij-tool-plugin/local-app.png)

7. Avec le bouton hello **LogQuery** application et sélectionnez **exécuter 'LogQuery'**. Sur hello **exécuter** onglet en bas de hello, vous voyez une sortie semblable à hello suivante :
   
   ![Résultat de l’exécution locale de l’application Spark](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-spark-app-local-run-result.png)

## <a name="convert-existing-intellij-idea-applications-toouse-azure-toolkit-for-intellij"></a>Convertir toouse d’applications existant IntelliJ idée boîte à outils Azure pour IntelliJ
Vous pouvez convertir hello Spark Scala les applications existantes que vous avez créé dans l’idée de IntelliJ toobe compatible avec la boîte à outils Azure pour IntelliJ. Vous pouvez ensuite utiliser hello toosubmit plug-in hello applications tooan cluster HDInsight Spark.

1. Pour une application Spark Scala existante qui a été créée via IntelliJ idée, ouvrez le fichier de .iml associé de hello.

2. À la racine de hello niveau est un **module** élément hello suivante :
   
        <module org.jetbrains.idea.maven.project.MavenProjectsManager.isMavenModule="true" type="JAVA_MODULE" version="4">

   Modifier hello élément tooadd `UniqueKey="HDInsightTool"` ainsi que hello **module** élément ressemble à hello suivantes :
   
        <module org.jetbrains.idea.maven.project.MavenProjectsManager.isMavenModule="true" type="JAVA_MODULE" version="4" UniqueKey="HDInsightTool">

3. Enregistrer les modifications de hello. Votre application doit maintenant être compatible avec le kit de ressources Azure pour IntelliJ. Vous pouvez le tester en double-cliquant sur le nom du projet hello dans l’Explorateur de projets. menu contextuel de Hello a maintenant l’option de hello **tooHDInsight de soumettre une Application de Spark**.

## <a name="troubleshooting"></a>Résolution des problèmes

### <a name="error-in-local-run-please-use-a-larger-heap-size"></a>Erreur dans l’exécution locale : *Please use a larger heap size* (Veuillez utiliser un tas de plus grande taille)
Dans la version 1.6 Spark, si vous utilisez un kit de développement Java 32 bits pendant l’exécution locale, vous pouvez rencontrer hello les erreurs suivantes :

    Exception in thread "main" java.lang.IllegalArgumentException: System memory 259522560 must be at least 4.718592E8. Please use a larger heap size.
        at org.apache.spark.memory.UnifiedMemoryManager$.getMaxMemory(UnifiedMemoryManager.scala:193)
        at org.apache.spark.memory.UnifiedMemoryManager$.apply(UnifiedMemoryManager.scala:175)
        at org.apache.spark.SparkEnv$.create(SparkEnv.scala:354)
        at org.apache.spark.SparkEnv$.createDriverEnv(SparkEnv.scala:193)
        at org.apache.spark.SparkContext.createSparkEnv(SparkContext.scala:288)
        at org.apache.spark.SparkContext.<init>(SparkContext.scala:457)
        at LogQuery$.main(LogQuery.scala:53)
        at LogQuery.main(LogQuery.scala)
        at sun.reflect.NativeMethodAccessorImpl.invoke0(Native Method)
        at sun.reflect.NativeMethodAccessorImpl.invoke(NativeMethodAccessorImpl.java:57)
        at sun.reflect.DelegatingMethodAccessorImpl.invoke(DelegatingMethodAccessorImpl.java:43)
        at java.lang.reflect.Method.invoke(Method.java:606)
        at com.intellij.rt.execution.application.AppMain.main(AppMain.java:144)

Ces erreurs se produisent, car la taille du tas de hello n’est pas assez grande pour Spark toorun. Spark nécessite au moins 471 Mo. (Pour plus d’informations, voir [SPARK-12081](https://issues.apache.org/jira/browse/SPARK-12081).) Une solution simple est toouse un kit de développement Java 64 bits. Vous pouvez également modifier les paramètres de JVM hello dans IntelliJ en ajoutant hello options suivantes :

    -Xms128m -Xmx512m -XX:MaxPermSize=300m -ea

![Ajout d’options toohello « Options de la machine virtuelle » zone IntelliJ](./media/hdinsight-apache-spark-intellij-tool-plugin/change-heap-size.png)

## <a name="faq"></a>Forum Aux Questions
toosubmit application tooAzure Data Lake Store, choisissez **Interactive** mode pendant le processus de hello signe dans Azure. Si vous sélectionnez le mode **automatique**, vous pouvez obtenir une erreur.

![Connexion interactive](./media/hdinsight-apache-spark-intellij-tool-plugin/interative-signin.png)

À présent, nous l’avons résolue. Vous pouvez choisir un toosubmit Cluster lac de données Azure à votre application avec n’importe quelle méthode de connexion.

## <a name="feedback-and-known-issues"></a>Commentaires et problèmes connus
Pour l’instant, la visualisation directe des sorties Spark n’est pas prise en charge.

Si vous avez des suggestions ou des commentaires, ou que vous rencontrez des problèmes lors de l’utilisation de ce plug-in, envoyez-nous un e-mail à l’adresse hdivstool@microsoft.com.

## <a name="seealso"></a>Étapes suivantes
* [Vue d’ensemble : Apache Spark sur Azure HDInsight](hdinsight-apache-spark-overview.md)

### <a name="demo"></a>Démonstration
* Créez un projet Scala (vidéo) : [Créer des applications Scala Spark](https://channel9.msdn.com/Series/AzureDataLake/Create-Spark-Applications-with-the-Azure-Toolkit-for-IntelliJ)
* Débogage distant (vidéo) : [utilisation Azure Toolkit pour les applications de Spark IntelliJ toodebug à distance sur un HDInsight Cluster](https://channel9.msdn.com/Series/AzureDataLake/Debug-HDInsight-Spark-Applications-with-Azure-Toolkit-for-IntelliJ)

### <a name="scenarios"></a>Scénarios
* [Spark avec BI : effectuez une analyse interactive des données à l’aide de Spark dans HDInsight avec des outils BI](hdinsight-apache-spark-use-bi-tools.md)
* [Spark avec Machine Learning : Spark utilisation dans tooanalyze HDInsight à l’aide des données HVAC de température de génération](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [Spark avec Machine Learning : Spark utilisation dans résultats de l’inspection alimentaires toopredict HDInsight](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [Diffusion en continu de Spark : Spark utilisation dans les applications de diffusion en continu en temps réel toobuild HDInsight](hdinsight-apache-spark-eventhub-streaming.md)
* [Analyse des journaux de site web à l’aide de Spark dans HDInsight](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="creating-and-running-applications"></a>Création et exécution d’applications
* [Créer une application autonome avec Scala](hdinsight-apache-spark-create-standalone-application.md)
* [Exécuter des tâches à distance avec Livy sur un cluster Spark](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a>Outils et extensions
* [Utilisez la boîte à outils Azure pour les applications de Spark IntelliJ toodebug à distance via le VPN](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [Utilisez la boîte à outils Azure pour les applications de Spark IntelliJ toodebug à distance via SSH](hdinsight-apache-spark-intellij-tool-debug-remotely-through-ssh.md)
* [Utiliser HDInsight Tools pour IntelliJ avec Hortonworks Sandbox](hdinsight-tools-for-intellij-with-hortonworks-sandbox.md)
* [Utilisez les outils HDInsight dans la boîte à outils Azure pour les applications de Spark toocreate Eclipse](hdinsight-apache-spark-eclipse-tool-plugin.md)
* [Utiliser des bloc-notes Zeppelin avec un cluster Spark sur HDInsight](hdinsight-apache-spark-zeppelin-notebook.md)
* [Noyaux disponibles pour le bloc-notes Jupyter dans un cluster Spark pour HDInsight](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [Utiliser des packages externes avec les blocs-notes Jupyter](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [Installer Notebook sur votre ordinateur et vous connecter tooan cluster HDInsight Spark](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="managing-resources"></a>Gestion des ressources
* [Gérer les ressources de cluster d’Apache Spark hello dans Azure HDInsight](hdinsight-apache-spark-resource-manager.md)
* [Track and debug jobs running on an Apache Spark cluster in HDInsight (Suivi et débogage des tâches en cours d’exécution sur un cluster Apache Spark dans HDInsight)](hdinsight-apache-spark-job-debugging.md)

