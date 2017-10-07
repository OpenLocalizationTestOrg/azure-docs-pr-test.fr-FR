---
title: "aaaAzure Toolkit pour Eclipse - Scala de créer des applications pour HDInsight Spark | Documents Microsoft"
description: "Utilisez les outils HDInsight dans la boîte à outils Azure pour Eclipse toodevelop Spark d’applications écrites dans Scala et les envoyer tooan cluster HDInsight Spark, directement à partir de celles-ci hello IDE Eclipse."
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: f6c79550-5803-4e13-b541-e86c4abb420b
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/24/2017
ms.author: nitinme
ms.openlocfilehash: 3ab70857c1e81f591a1c7e29bc1706ec4899ff58
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-toolkit-for-eclipse-toocreate-spark-applications-for-an-hdinsight-cluster"></a>Utilisez la boîte à outils Azure pour les applications de Spark toocreate Eclipse pour un cluster HDInsight

Utilisez les outils HDInsight dans la boîte à outils Azure pour Eclipse toodevelop Spark d’applications écrites dans Scala et les envoyer cluster Azure HDInsight Spark tooan, directement à partir de hello IDE Eclipse. Vous pouvez utiliser les outils de HDInsight hello plug-in de différentes manières :

* toodevelop et envoi d’une application Scala Spark sur un cluster HDInsight Spark
* tooaccess vos ressources de cluster Azure HDInsight Spark
* toodevelop et exécuter une application Scala Spark localement

> [!IMPORTANT]
> Cet outil peut être toocreate utilisé et soumettre des applications uniquement pour un cluster HDInsight Spark sur Linux.
> 
> 

## <a name="prerequisites"></a>Composants requis

* Un cluster Apache Spark sur HDInsight. Pour obtenir des instructions, consultez [Création de clusters Apache Spark dans Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).
* Oracle Java Development Kit version 8, qui est utilisée pour l’exécution d’IDE Eclipse hello. Vous pouvez le télécharger depuis hello [site Web d’Oracle](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).
* IDE Eclipse. Cet article utilise Eclipse Neon. Vous pouvez l’installer à partir de hello [site Web d’Eclipse](https://www.eclipse.org/downloads/).   
* Kit de développement logiciel (SDK) Spark. Vous pouvez le télécharger à partir de [GitHub](http://go.microsoft.com/fwlink/?LinkID=723585&clcid=0x409).


## <a name="install-hdinsight-tools-in-azure-toolkit-for-eclipse-and-scala-plugin"></a>Installer les outils HDInsight dans la boîte à outils Azure pour Eclipse et plug-in Scala
### <a name="install-hdinsight-tools"></a>Installer HDInsight Tools
HDInsight Tools pour Eclipse est disponible dans le cadre du kit de ressources Azure pour Eclipse. Pour plus d’informations sur l’installation, voir [Installation du kit de ressources Azure pour Eclipse](../azure-toolkit-for-eclipse-installation.md).
### <a name="install-scala-plugin"></a>Installer le plug-in Scala
Lorsque vous ouvrez hello Intellij, hello outils HDInsight automatique détecte si vous avez installé le plug-in Scala ou non. Cliquez sur **OK** toocontinue et suivez tooinstall d’instructions hello en hello Eclipse Marketplace.

 ![Le plug-in Scala automatiquement installer](./media/hdinsight-apache-spark-eclipse-tool-plugin/auto-install-scala.png)

## <a name="sign-in-tooyour-azure-subscription"></a>Se connecter tooyour abonnement Azure
1. Démarrer hello IDE Eclipse et ouvrez l’Explorateur d’Azure. Sur hello **fenêtre** menu, cliquez sur **afficher la vue**, puis cliquez sur **autres**. Dans la boîte de dialogue hello qui s’ouvre, développez **Azure**, cliquez sur **Explorateur Azure**, puis cliquez sur **OK**.

    ![Boîte de dialogue Affichage](./media/hdinsight-apache-spark-eclipse-tool-plugin/view-explorer-1.png)
2. Avec le bouton hello **Azure** nœud, puis cliquez sur **connectez-vous**.
3. Bonjour **Azure Sign In** boîte de dialogue, choisissez la méthode d’authentification hello, cliquez sur **connecter**et entrez vos informations d’identification Azure.
   
    ![Boîte de dialogue Connexion à Azure](./media/hdinsight-apache-spark-eclipse-tool-plugin/view-explorer-2.png)
4. Une fois que vous êtes connecté, hello **sélectionnez les abonnements** boîte de dialogue propose toutes hello abonnements Azure associés aux informations d’identification hello. Cliquez sur **sélectionnez** boîte de dialogue tooclose hello.

    ![Boîte de dialogue Sélectionner des abonnements](./media/hdinsight-apache-spark-eclipse-tool-plugin/Select-Subscriptions.png)
5. Sur hello **Explorateur Azure** onglet, développez **HDInsight** hello toosee des clusters HDInsight Spark sous votre abonnement.
   
    ![Clusters HDInsight Spark dans l’Explorateur Azure](./media/hdinsight-apache-spark-eclipse-tool-plugin/view-explorer-3.png)
6. Vous pouvez développer davantage un nom du nœud toosee hello ressources de cluster (par exemple, les comptes de stockage) associé hello cluster.
   
    ![Développement d’un cluster nom toosee des ressources](./media/hdinsight-apache-spark-eclipse-tool-plugin/view-explorer-4.png)



## <a name="set-up-a-spark-scala-project-for-an-hdinsight-spark-cluster"></a>Configuration d’un projet Spark Scala pour un cluster HDInsight Spark

1. Dans l’espace de travail hello IDE Eclipse, cliquez sur **fichier**, cliquez sur **nouveau**, puis cliquez sur **projet**. 
2. Dans l’Assistant Nouveau projet de hello, développez **HDInsight**, sélectionnez **Spark sur HDInsight (Scala)**, puis cliquez sur **suivant**.

    ![En sélectionnant hello Spark sur HDInsight (Scala) projet](./media/hdinsight-apache-spark-eclipse-tool-plugin/create-hdi-scala-app-2.png)
3. automatique d’Assistant Création de Hello Scala projet détecte si vous avez installé le plug-in Scala ou non. Cliquez sur **OK** toocontinue télécharger le plug-in de hello Scala, puis suivez hello instructions toorestart Eclipse.

    ![vérification Scala](./media/hdinsight-apache-spark-eclipse-tool-plugin/auto-install-scala-2.png)
4. Bonjour **nouveau projet de Scala HDInsight** boîte de dialogue, fournissez hello valeurs suivantes, puis cliquez sur **suivant**:
   * Entrez un nom pour le projet de hello.
   * Bonjour **JRE** zone, assurez-vous que **utiliser un environnement d’exécution JRE** est défini trop**JavaSE-1.7** ou version ultérieure.
   * Assurez-vous que le Kit de développement logiciel Spark est toohello définir un emplacement où vous avez téléchargé hello Kit de développement logiciel. emplacement de téléchargement de lien toohello Hello est inclus dans hello [conditions préalables](#prerequisites) plus haut dans cet article. Vous pouvez également télécharger hello SDK à partir de hello lien inclus dans la boîte de dialogue hello.

    ![Boîte de dialogue New HDInsight Scala Project (Nouveau projet HDInsight Scala)](./media/hdinsight-apache-spark-eclipse-tool-plugin/create-hdi-scala-app-3.png)
5.  Dans la boîte de dialogue suivante hello, cliquez sur hello **bibliothèques** onglet et conserver les valeurs par défaut hello, puis cliquez sur **Terminer**. 
   
    ![Onglet Libraries (Bibliothèques)](./media/hdinsight-apache-spark-eclipse-tool-plugin/create-hdi-scala-app-4.png)
  
## <a name="create-a-scala-application-for-an-hdinsight-spark-cluster"></a>Créer une application Scala pour un cluster HDInsight Spark

1. Bonjour IDE Eclipse, à partir de l’Explorateur de Package, développez le projet hello que vous avez créé précédemment, cliquez sur **src**, pointez trop**nouveau**, puis cliquez sur **autres**.
2. Bonjour **sélectionner un Assistant** boîte de dialogue, développez **Scala Assistants**, cliquez sur **Scala objet**, puis cliquez sur **suivant**.
   
    ![Boîte de dialogue Select a wizard (Sélectionner un Assistant)](./media/hdinsight-apache-spark-eclipse-tool-plugin/create-scala-proj-1.png)
3. Bonjour **créer un nouveau fichier** boîte de dialogue, entrez un nom pour l’objet de hello, puis cliquez sur **Terminer**.
   
    ![Boîte de dialogue Create New File (Créer un fichier)](./media/hdinsight-apache-spark-eclipse-tool-plugin/create-scala-proj-2.png)
4. Collez hello suivant de code dans l’éditeur de texte hello :
   
        import org.apache.spark.SparkConf
        import org.apache.spark.SparkContext
   
        object MyClusterApp{
          def main (arg: Array[String]): Unit = {
            val conf = new SparkConf().setAppName("MyClusterApp")
            val sc = new SparkContext(conf)
   
            val rdd = sc.textFile("wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")
   
            //find hello rows that have only one digit in hello seventh column in hello CSV
            val rdd1 =  rdd.filter(s => s.split(",")(6).length() == 1)
   
            rdd1.saveAsTextFile("wasb:///HVACOut")
          }        
        }
5. Exécutez l’application hello sur un cluster HDInsight Spark :
   
   1. À partir de l’Explorateur de Package, cliquez sur le nom de projet hello et sélectionnez **tooHDInsight de soumettre une Application de Spark**.        
   2. Bonjour **Spark soumission** boîte de dialogue, fournissez hello valeurs suivantes, puis cliquez sur **Submit**:
      
      * Pour **nom de Cluster**, sélectionnez hello cluster HDInsight Spark sur lequel vous souhaitez toorun votre application.
      * Sélectionnez un artefact à partir de projets d’Eclipse hello ou sélectionnez-en un dans un disque dur. valeur par défaut de Hello dépend de l’élément hello avec le bouton droit dans l’Explorateur de package.
      * Bonjour **nom de la classe principale** dropdownlist, envoi Assistant affiche tous les noms des objets à partir de votre projet sélectionné. Sélectionnez ou entrez un que vous souhaitez toorun. Si vous sélectionnez un artefact à partir du disque dur, vous devez entrer le nom de la classe principale vous-même. 
      * Étant donné que le code de l’application hello dans cet exemple ne requièrent aucun argument de ligne de commande ni référencer des fichiers ou des fichiers JAR, vous pouvez laisser hello restant des zones de texte vides.
        
       ![Boîte de dialogue Spark Submission (Envoi Spark)](./media/hdinsight-apache-spark-eclipse-tool-plugin/create-scala-proj-3.png)
   3. Hello **Spark soumission** onglet doit commencer à afficher la progression de hello. Vous pouvez arrêter l’application hello en cliquant sur le bouton hello rouge Bonjour **Spark soumission** fenêtre. Vous pouvez également afficher les journaux hello pour cette application spécifique exécuté en cliquant sur icône du globe hello (indiquée par la zone bleue de hello dans l’image de hello).
      
       ![Fenêtre Spark Submission (Envoi Spark)](./media/hdinsight-apache-spark-eclipse-tool-plugin/create-scala-proj-4.png)

## <a name="access-and-manage-hdinsight-spark-clusters-by-using-hdinsight-tools-in-azure-toolkit-for-eclipse"></a>Accéder aux clusters HDInsight Spark et les gérer à l’aide de HDInsight Tools dans le kit de ressources Azure pour Eclipse
Vous pouvez effectuer diverses opérations à l’aide des outils HDInsight, y compris l’accès à la sortie des tâches hello.

### <a name="access-hello-job-view"></a>Affichage des travaux hello Access
1. Dans l’Explorateur d’Azure, développez **HDInsight**, développez le nom du cluster Spark hello, puis cliquez sur **travaux**. 

    ![Nœud Vue de la tâche](./media/hdinsight-apache-spark-intellij-tool-plugin/job-view-node.png)

2. Cliquez sur hello **travaux** nœud. Outils de HDInsight Hello détecte automatiquement si vous avez installé le plug-in clipse hello E (fx) ou non. Cliquez sur **OK** toocontinue et suivre des instructions hello tooinstall hello Eclipse Marketplace et redémarrer Eclipse.

    ![Installer E(fx)clipse](./media/hdinsight-apache-spark-eclipse-tool-plugin/auto-install-efxclipse.png)

3. Ouvrez hello vue des travaux à partir de hello **travaux** nœud. Dans le volet droit de hello, hello **Spark travail vue** onglet affiche toutes les applications hello qui ont été exécutées sur le cluster de hello. Cliquez sur nom hello application hello pour lequel vous souhaitez toosee plus de détails.

    ![Détails de l’application](./media/hdinsight-apache-spark-intellij-tool-plugin/view-job-logs.png)
4. Si vous pointez sur le graphique de travail hello, il affiche base informations du travail en cours d’exécution. En cliquant sur le graphique de travail hello montre le graphique des étapes hello et informations générés par chaque tâche.

    ![Détails des étapes du travail](./media/hdinsight-apache-spark-intellij-tool-plugin/Job-graph-stage-info.png)

5. Les journaux fréquemment utilisées, notamment les pilotes Stderr, Stdout de pilote et des informations de répertoire, sont répertoriées dans hello **journal** onglet.

    ![Détails des journaux](./media/hdinsight-apache-spark-intellij-tool-plugin/Job-log-info.png)
6. Vous pouvez également ouvrir hello historique de Spark UI et hello UI fils (au niveau de l’application hello) en cliquant sur le lien hypertexte respectifs de hello haut hello de fenêtre hello.

### <a name="access-hello-storage-container-for-hello-cluster"></a>Conteneur de stockage hello d’accès pour le cluster de hello
1. Dans l’Explorateur d’Azure, développez hello **HDInsight** toosee de nœud racine une liste de clusters HDInsight Spark qui sont disponibles.
2. Développez le compte de stockage hello cluster nom toosee hello et conteneur de stockage par défaut hello pour le cluster de hello.
   
    ![Compte de stockage et conteneur de stockage par défaut](./media/hdinsight-apache-spark-eclipse-tool-plugin/view-explorer-5.png)
3. Cliquez sur le nom de conteneur de stockage hello associé hello cluster. Dans le volet droit de hello, double-cliquez sur hello **HVACOut** dossier. Ouvrez un des hello **partie -** fichiers de sortie de hello toosee de l’application hello.

### <a name="access-hello-spark-history-server"></a>Serveur d’accès hello Spark historique
1. Dans l’Explorateur Azure, cliquez avec le bouton droit sur le nom de votre cluster Spark, puis sélectionnez **Open Spark History UI** (Ouvrir l’interface utilisateur de l’historique Spark). Lorsque vous y êtes invité, entrez les informations d’identification du admin de hello pour le cluster de hello. Vous devez avoir spécifié ces lors de la configuration de cluster de hello.
2. Dans le tableau de bord de serveur de hello Spark historique, vous utilisez toolook de nom d’application hello pour application hello que vous venez d’en cours d’exécution. Bonjour précédant le code, vous définir le nom de l’application hello en utilisant `val conf = new SparkConf().setAppName("MyClusterApp")`. Le nom de votre application Spark était donc **MyClusterApp**.

### <a name="start-hello-ambari-portal"></a>Démarrer le portail de Ambari hello
1. Dans l’Explorateur Azure, cliquez avec le bouton droit sur le nom de votre cluster Spark, puis sélectionnez **Open Cluster Management Portal (Ambari)** (Ouvrir le portail de gestion des clusters [Ambari]). 
2. Lorsque vous y êtes invité, entrez les informations d’identification du admin de hello pour le cluster de hello. Vous devez avoir spécifié ces lors de la configuration de cluster de hello.

### <a name="manage-azure-subscriptions"></a>Gérer les abonnements Azure
Par défaut, les outils HDInsight dans la boîte à outils Azure pour Eclipse répertorie les clusters de Spark de hello à partir de tous vos abonnements Azure. Si nécessaire, vous pouvez spécifier des abonnements hello pour lequel vous souhaitez le cluster de hello tooaccess. 

1. Dans l’Explorateur d’Azure, avec le bouton droit hello **Azure** nœud racine, puis cliquez sur **gérer les abonnements**. 
2. Dans la boîte de dialogue hello, désactivez les cases à cocher hello abonnement hello que vous ne souhaitez tooaccess, puis cliquez sur **fermer**. Vous pouvez également cliquer sur **se déconnecter** si vous souhaitez toosign dans votre abonnement Azure.

## <a name="run-a-spark-scala-application-locally"></a>Exécuter une application Spark Scala localement
Vous pouvez utiliser les outils HDInsight dans la boîte à outils Azure pour les applications de Spark Scala toorun Eclipse localement sur votre station de travail. En règle générale, ces applications n’ont besoin d’accéder aux ressources de toocluster tel qu’un conteneur de stockage, et vous pouvez exécuter et tester localement.

### <a name="prerequisite"></a>Configuration requise
Lorsque vous exécutez l’application hello locale Spark Scala sur un ordinateur Windows, vous pouvez obtenir une exception comme expliqué dans [SPARK-2356](https://issues.apache.org/jira/browse/SPARK-2356). Cette exception est liée à l’absence du fichier **WinUtils.exe** dans Windows. 

tooresolve cette erreur, vous devez [télécharger hello exécutable](http://public-repo-1.hortonworks.com/hdp-win-alpha/winutils.exe) tooa emplacement comme **C:\WinUtils\bin**. Vous devez ensuite ajouter la variable d’environnement hello **HADOOP_HOME** et la valeur hello de variable de hello trop**C\WinUtils**.

### <a name="run-a-local-spark-scala-application"></a>Exécuter une application Spark Scala locale
1. Démarrez Eclipse et créez un projet. Bonjour **nouveau projet** boîte de dialogue, vérifiez hello options suivantes, puis cliquez sur **suivant**.
   
   * Dans le volet gauche de hello, sélectionnez **HDInsight**.
   * Dans le volet droit de hello, sélectionnez **Spark sur HDInsight Local exécuter échantillon (Scala)**.

    ![Boîte de dialogue Nouveau projet](./media/hdinsight-apache-spark-eclipse-tool-plugin/hdi-spark-app-local-run.png)
2. Détails du projet tooprovide hello, suivez les étapes 3 à 6 de hello section antérieure [configurer un projet Spark Scala pour un cluster HDInsight Spark](#set-up-a-spark-scala-project-for-an-hdinsight-spark cluster).
3. modèle de Hello ajoute un exemple de code (**LogQuery**) sous hello **src** dossier que vous pouvez exécuter localement sur votre ordinateur.
   
    ![Emplacement de LogQuery](./media/hdinsight-apache-spark-eclipse-tool-plugin/local-app.png)
4. Avec le bouton hello **LogQuery** application, pointez trop**exécuter en tant que**, puis cliquez sur **1 Application Scala**. Vous verrez une sortie comme Bonjour **Console** onglet en bas de hello :
   
   ![Résultat de l’exécution locale de l’application Spark](./media/hdinsight-apache-spark-eclipse-tool-plugin/hdi-spark-app-local-run-result.png)

## <a name="faq"></a>Forum Aux Questions
toosubmit application tooAzure Data Lake Store, choisissez **Interactive** mode pendant le processus de hello signe dans Azure. Si vous sélectionnez le mode **automatique**, vous pouvez obtenir une erreur.

![Connexion interactive](./media/hdinsight-apache-spark-eclipse-tool-plugin/interactive-authentication.png)

À présent, nous l’avons résolue. Vous pouvez choisir un toosubmit Cluster lac de données Azure à votre application avec n’importe quelle méthode de connexion.

## <a name="feedback-and-known-issues"></a>Commentaires et problèmes connus
Pour l’instant, la visualisation directe des sorties Spark n’est pas prise en charge.

Si vous avez des suggestions ou les commentaires, ou si vous rencontrez des problèmes lors de l’utilisation de cet outil, vous pouvez toosend libre nous un e-mail à hdivstool@microsoft.com.

## <a name="seealso"></a>Voir aussi
* [Vue d’ensemble : Apache Spark sur Azure HDInsight](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a>Scénarios
* [Spark avec BI : effectuez une analyse interactive des données à l’aide de Spark dans HDInsight avec des outils BI](hdinsight-apache-spark-use-bi-tools.md)
* [Spark avec Machine Learning : utilisez Spark dans HDInsight pour l’analyse de la température des bâtiments à l’aide des données des systèmes HVAC](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [Spark avec Machine Learning : Spark utilisation dans résultats de l’inspection alimentaires toopredict HDInsight](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [Streaming Spark : Utiliser Spark dans HDInsight pour créer des applications de diffusion en continu en temps réel](hdinsight-apache-spark-eventhub-streaming.md)
* [Analyse des journaux de site web à l’aide de Spark dans HDInsight](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="creating-and-running-applications"></a>Création et exécution d’applications
* [Créer une application autonome avec Scala](hdinsight-apache-spark-create-standalone-application.md)
* [Exécuter des tâches à distance avec Livy sur un cluster Spark](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a>Outils et extensions
* [Utilisez la boîte à outils Azure pour IntelliJ toocreate et soumettre des applications de Spark Scala](hdinsight-apache-spark-intellij-tool-plugin.md)
* [Utilisez la boîte à outils Azure pour les applications de Spark IntelliJ toodebug à distance via le VPN](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [Utilisez la boîte à outils Azure pour les applications de Spark IntelliJ toodebug à distance via SSH](hdinsight-apache-spark-intellij-tool-debug-remotely-through-ssh.md)
* [Utiliser HDInsight Tools pour IntelliJ avec Hortonworks Sandbox](hdinsight-tools-for-intellij-with-hortonworks-sandbox.md)
* [Utiliser des bloc-notes Zeppelin avec un cluster Spark sur HDInsight](hdinsight-apache-spark-zeppelin-notebook.md)
* [Noyaux disponibles pour le bloc-notes Jupyter dans un cluster Spark pour HDInsight](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [Utiliser des packages externes avec les blocs-notes Jupyter](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [Installer Notebook sur votre ordinateur et vous connecter tooan cluster HDInsight Spark](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="managing-resources"></a>Gestion des ressources
* [Gérer les ressources de cluster d’Apache Spark hello dans Azure HDInsight](hdinsight-apache-spark-resource-manager.md)
* [Track and debug jobs running on an Apache Spark cluster in HDInsight (Suivi et débogage des tâches en cours d’exécution sur un cluster Apache Spark dans HDInsight)](hdinsight-apache-spark-job-debugging.md)

