---
title: aaaCreate Scala application toorun sur les clusters de Spark - Azure HDInsight | Documents Microsoft
description: "Créez une application Spark écrite en Scala avec Apache Maven comme archétype Maven existant et système de build hello pour Scala fournie par IntelliJ idée."
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: b2467a40-a340-4b80-bb00-f2c3339db57b
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/25/2017
ms.author: nitinme
ms.openlocfilehash: b25291b60921021486f55d78b4832a070a54d163
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-scala-maven-application-toorun-on-apache-spark-cluster-on-hdinsight"></a>Créer un toorun d’application Scala Maven sur cluster Apache Spark sur HDInsight

Découvrez comment toocreate une application de Spark écrite en Scala avec Maven IntelliJ idée. article de Hello utilise Apache Maven hello système de génération et commence par archétype Maven existant pour Scala fournie par IntelliJ idée.  Création d’une application de Scala dans IntelliJ idée implique hello comme suit :

* Utilisez Maven en tant que système de génération hello.
* Mettre à jour les dépendances de modules de modèle d’objet projet (POM) fichier tooresolve Spark.
* Écrire votre application dans Scala.
* Générer un fichier jar qui peut être soumis tooHDInsight Spark clusters.
* Exécuter l’application hello sur cluster Spark à l’aide de Livy.

> [!NOTE]
> HDInsight fournit également un idée de IntelliJ plug-in outil tooease hello processus de création et envoi d’applications tooan cluster HDInsight Spark sur Linux. Pour plus d’informations, consultez [utilisez HDInsight outils plug-in pour IntelliJ idée toocreate et soumettre des applications de Spark](hdinsight-apache-spark-intellij-tool-plugin.md).
> 
> 

## <a name="prerequisites"></a>Composants requis

* Un abonnement Azure. Consultez la page [Obtention d’un essai gratuit d’Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).
* Un cluster Apache Spark sur HDInsight. Pour obtenir des instructions, consultez [Création de clusters Apache Spark dans Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).
* Kit de développement logiciel (SDK) Oracle Java. Vous pouvez l’installer à partir d’ [ici](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).
* IDE Java. Cet article utilise IntelliJ IDEA 15.0.1. Vous pouvez l’installer à partir d’ [ici](https://www.jetbrains.com/idea/download/).

## <a name="install-scala-plugin-for-intellij-idea"></a>Installer le plug-in Scala pour IntelliJ IDEA
Si les installation IntelliJ idée ne s’invite pas pas pour l’activation du plug-in Scala, lancez IntelliJ idée et accéder à hello suivant le plug-in hello étapes tooinstall :

1. Démarrez IntelliJ IDEA, puis à partir de l’écran d’accueil, cliquez sur **Configurer**, puis sur **Plug-ins**.
   
    ![Activer le plug-in Scala](./media/hdinsight-apache-spark-create-standalone-application/enable-scala-plugin.png)
2. Dans l’écran suivant de hello, cliquez sur **plug-in de l’installation de JetBrains** à partir de l’angle inférieur gauche hello. Bonjour **parcourir les plug-ins JetBrains** boîte de dialogue qui s’ouvre, recherchez Scala, puis **installer**.
   
    ![Installer le plug-in Scala](./media/hdinsight-apache-spark-create-standalone-application/install-scala-plugin.png)
3. Une fois que le plug-in hello s’installe correctement, cliquez sur hello **bouton de redémarrer une idée de IntelliJ** toorestart hello IDE.

## <a name="create-a-standalone-scala-project"></a>Créer un programme Scala autonome
1. Lancez IntelliJ IDEA et créez un nouveau projet. Dans la boîte de dialogue Nouveau projet hello, rendre hello des options suivantes, puis cliquez sur **suivant**.
   
    ![Créer un projet Maven](./media/hdinsight-apache-spark-create-standalone-application/create-maven-project.png)
   
   * Sélectionnez **Maven** en tant que type de projet hello.
   * Spécifiez un **projet SDK**. Cliquez sur Nouveau et accédez répertoire d’installation de Java toohello généralement `C:\Program Files\Java\jdk1.8.0_66`.
   * Sélectionnez hello **à partir d’un archétype** option.
   * Dans la liste hello d’archetypes, sélectionnez **org.scala tools.archetypes:scala archétype simple**. Cela créer une structure de répertoire correct hello et télécharger le programme Scala toowrite hello requis par défaut dépendances.
2. Indiquez les valeurs appropriées pour **GroupId**, **ArtifactId** et **Version**. Cliquez sur **Suivant**.
3. Dans hello boîte de dialogue suivante où vous spécifiez le répertoire de base Maven et d’autres paramètres de l’utilisateur, acceptez les valeurs par défaut hello et cliquez sur **suivant**.
4. Dans la dernière boîte de dialogue hello, spécifiez un nom de projet et un emplacement, puis **Terminer**.
5. Supprimer hello **MySpec.Scala** de fichiers au **src\test\scala\com\microsoft\spark\example**. Il est inutile cela pour l’application hello.
6. Si nécessaire, renommez les fichiers de code source et de test par défaut hello. À partir du volet de gauche hello Bonjour IntelliJ idée, accédez trop**src\main\scala\com.microsoft.spark.example**. Avec le bouton droit **App.scala**, cliquez sur **refactoriser**, cliquez sur Renommer un fichier et dans la boîte de dialogue hello, indiquez hello nouveau nom pour l’application hello et puis cliquez sur **refactoriser**.
   
    ![Renommer les fichiers](./media/hdinsight-apache-spark-create-standalone-application/rename-scala-files.png)  
7. Dans les étapes suivantes hello, vous mettrez à jour les dépendances hello pom.xml toodefine hello hello Spark Scala application. Pour ces dépendances toobe téléchargé et résolus automatiquement, que vous devez configurer Maven en conséquence.
   
    ![Configurer Maven pour les téléchargements automatiques](./media/hdinsight-apache-spark-create-standalone-application/configure-maven.png)
   
   1. À partir de hello **fichier** menu, cliquez sur **paramètres**.
   2. Bonjour **paramètres** boîte de dialogue, accédez trop**déploiement de la Build, l’exécution,** > **outils de génération** > **Maven**  >  **Importation**.
   3. L’option hello trop**automatiquement les projets Maven d’importation**.
   4. Cliquez sur **Appliquer**, puis sur **OK**.
8. Mettre à jour hello Scala source fichier tooinclude votre code d’application. Ouvrez et remplacez hello existants dans exemple de code hello suivant de code et enregistrer les modifications de hello. Ce code lit les données de salutation hello HVAC.csv (disponible sur tous les clusters HDInsight Spark), récupère les lignes hello qui ont uniquement un chiffre dans la sixième colonne de hello et écrit la sortie de hello trop**/HVACOut** sous stockage de la valeur par défaut hello conteneur pour un cluster de hello.
   
        package com.microsoft.spark.example
   
        import org.apache.spark.SparkConf
        import org.apache.spark.SparkContext
   
        /**
          * Test IO toowasb
          */
        object WasbIOTest {
          def main (arg: Array[String]): Unit = {
            val conf = new SparkConf().setAppName("WASBIOTest")
            val sc = new SparkContext(conf)
   
            val rdd = sc.textFile("wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")
   
            //find hello rows which have only one digit in hello 7th column in hello CSV
            val rdd1 = rdd.filter(s => s.split(",")(6).length() == 1)
   
            rdd1.saveAsTextFile("wasb:///HVACout")
          }
        }
9. Mettre à jour hello pom.xml.
   
   1. Dans `<project>\<properties>` ajoutez hello qui suit :
      
          <scala.version>2.10.4</scala.version>
          <scala.compat.version>2.10.4</scala.compat.version>
          <scala.binary.version>2.10</scala.binary.version>
   2. Dans `<project>\<dependencies>` ajoutez hello qui suit :
      
           <dependency>
             <groupId>org.apache.spark</groupId>
             <artifactId>spark-core_${scala.binary.version}</artifactId>
             <version>1.4.1</version>
           </dependency>
      
      Enregistrer les modifications toopom.xml.
10. Création du fichier .jar hello. IntelliJ IDEA permet de créer le fichier JAR en tant qu’artefact d'un projet. Effectuer hello comme suit.
    
    1. À partir de hello **fichier** menu, cliquez sur **Structure de projet**.
    2. Bonjour **Structure de projet** boîte de dialogue, cliquez sur **artefacts** puis hello plus de symbole. Dans la boîte de dialogue contextuelle hello, cliquez sur **JAR**, puis cliquez sur **à partir de modules avec des dépendances**.
       
        ![Créer un fichier jar](./media/hdinsight-apache-spark-create-standalone-application/create-jar-1.png)
    3. Bonjour **créer JAR à partir de Modules** boîte de dialogue, cliquez sur les points de suspension hello (![points de suspension](./media/hdinsight-apache-spark-create-standalone-application/ellipsis.png) ) par rapport à hello **principale classe**.
    4. Bonjour **sélection de la classe principale** boîte de dialogue, la classe hello sélectionnez s’affiche par défaut, puis cliquez sur **OK**.
       
        ![Créer un fichier jar](./media/hdinsight-apache-spark-create-standalone-application/create-jar-2.png)
    5. Bonjour **créer JAR à partir de Modules** boîte de dialogue zone, assurez-vous que cette option hello trop**extraire toohello cible JAR** est sélectionné, puis cliquez sur **OK**. Cela crée un fichier JAR contenant toutes les dépendances.
       
        ![Créer un fichier jar](./media/hdinsight-apache-spark-create-standalone-application/create-jar-3.png)
    6. onglet Disposition de sortie Hello répertorie tous les fichiers JAR hello qui sont inclus dans le cadre du projet de Maven hello. Vous pouvez sélectionner et hello supprimer ceux sur lesquels hello Scala application ne possède pas de dépendance directe. Pour l’application hello, nous allons créer ici, vous pouvez supprimer tout sauf hello dernière (**SparkSimpleApp compilation sortie**). Sélectionnez hello JAR toodelete, puis cliquez sur hello **supprimer** icône.
       
        ![Créer un fichier jar](./media/hdinsight-apache-spark-create-standalone-application/delete-output-jars.png)
       
        Assurez-vous que **Build sur Vérifiez** à cocher est activée, ce qui garantit que ce fichier jar hello est créé chaque fois que projet de hello est généré ou mis à jour. Cliquez sur **Appliquer**, puis sur **OK**.
    7. Dans la barre de menus de hello, cliquez sur **générer**, puis cliquez sur **créer le projet**. Vous pouvez également cliquer sur **des artefacts de Build** jar de hello toocreate. Hello jar de sortie est créé sous **\out\artifacts**.
       
        ![Créer un fichier jar](./media/hdinsight-apache-spark-create-standalone-application/output.png)

## <a name="run-hello-application-on-hello-spark-cluster"></a>Exécutez l’application hello sur cluster Spark de hello
application de hello toorun sur le cluster de hello, vous devez procéder comme suit de hello :

* **Copie hello application jar toohello stockage Azure d’objets blob** associé hello cluster. Vous pouvez utiliser [ **AzCopy**](../storage/common/storage-use-azcopy.md), par conséquent, utilitaire, toodo une commande de ligne. Il existe de nombreux autres clients ainsi que vous pouvez utiliser les données tooupload. Pour en savoir plus à leur sujet, consultez [Téléchargement de données pour les travaux Hadoop dans HDInsight](hdinsight-upload-data.md).
* **Utiliser Livy toosubmit un travail de l’application à distance** cluster Spark de toohello. Clusters Spark sur HDInsight inclut Livy qui expose des autres points de terminaison tooremotely envoyer des travaux de Spark. Pour plus d’informations, consultez [Envoi de travaux Spark à distance en utilisant Livy avec les clusters Spark sur HDInsight](hdinsight-apache-spark-livy-rest-interface.md).

## <a name="next-step"></a>Étape suivante

Dans cet article vous avez appris comment toocreate une application de scala Spark. Avance toohello suivant l’article toolearn comment toorun cette application sur un HDInsight Spark de cluster à l’aide de Livy.

> [!div class="nextstepaction"]
>[Exécution de travaux à distance avec Livy sur un cluster Spark](hdinsight-apache-spark-livy-rest-interface.md)

