---
title: "Créer une application Scala à exécuter sur des clusters Spark - HDInsight Azure | Microsoft Docs"
description: "Créez une application Spark écrite en Scala avec Apache Maven comme système de génération et un archétype Maven existant pour Scala fourni par IntelliJ IDEA."
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
ms.openlocfilehash: 95dba08744357f8800b05e3d4b892e3a363d5985
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="create-a-scala-maven-application-to-run-on-apache-spark-cluster-on-hdinsight"></a><span data-ttu-id="b99b4-103">Créer une application Scala Maven à exécuter sur un cluster Apache Spark sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="b99b4-103">Create a Scala Maven application to run on Apache Spark cluster on HDInsight</span></span>

<span data-ttu-id="b99b4-104">Découvrez comment créer une application Spark écrite en Scala à l’aide de Maven avec IntelliJ IDEA.</span><span class="sxs-lookup"><span data-stu-id="b99b4-104">Learn how to create a Spark application written in Scala using Maven with IntelliJ IDEA.</span></span> <span data-ttu-id="b99b4-105">Dans cet article, Apache Maven est utilisé comme système de génération. Le document présente dans un premier temps un archétype Maven existant pour Scala fourni par IntelliJ IDEA.</span><span class="sxs-lookup"><span data-stu-id="b99b4-105">The article uses Apache Maven as the build system and starts with an existing Maven archetype for Scala provided by IntelliJ IDEA.</span></span>  <span data-ttu-id="b99b4-106">La création d’une application Scala avec IntelliJ IDEA implique les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="b99b4-106">Creating a Scala application in IntelliJ IDEA involves the following steps:</span></span>

* <span data-ttu-id="b99b4-107">Utiliser Maven en tant que le système de génération.</span><span class="sxs-lookup"><span data-stu-id="b99b4-107">Use Maven as the build system.</span></span>
* <span data-ttu-id="b99b4-108">Mettre à jour le fichier de modèle objet du projet (POM) pour résoudre les dépendances de module Spark.</span><span class="sxs-lookup"><span data-stu-id="b99b4-108">Update Project Object Model (POM) file to resolve Spark module dependencies.</span></span>
* <span data-ttu-id="b99b4-109">Écrire votre application dans Scala.</span><span class="sxs-lookup"><span data-stu-id="b99b4-109">Write your application in Scala.</span></span>
* <span data-ttu-id="b99b4-110">Générer un fichier jar qui peut être soumis à des clusters HDInsight Spark.</span><span class="sxs-lookup"><span data-stu-id="b99b4-110">Generate a jar file that can be submitted to HDInsight Spark clusters.</span></span>
* <span data-ttu-id="b99b4-111">Exécuter l’application à distance sur le cluster Spark à l’aide de Livy.</span><span class="sxs-lookup"><span data-stu-id="b99b4-111">Run the application on Spark cluster using Livy.</span></span>

> [!NOTE]
> <span data-ttu-id="b99b4-112">HDInsight propose également un outil de plug-in IntelliJ IDEA pour faciliter le processus de création et d’envoi des applications à un cluster HDInsight Spark sous Linux.</span><span class="sxs-lookup"><span data-stu-id="b99b4-112">HDInsight also provides an IntelliJ IDEA plugin tool to ease the process of creating and submitting applications to an HDInsight Spark cluster on Linux.</span></span> <span data-ttu-id="b99b4-113">Pour plus d’informations, consultez [Utiliser le plug-in Outils HDInsight pour IntelliJ IDEA afin de créer et d’envoyer des applications Spark](hdinsight-apache-spark-intellij-tool-plugin.md).</span><span class="sxs-lookup"><span data-stu-id="b99b4-113">For more information, see [Use HDInsight Tools Plugin for IntelliJ IDEA to create and submit Spark applications](hdinsight-apache-spark-intellij-tool-plugin.md).</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="b99b4-114">Composants requis</span><span class="sxs-lookup"><span data-stu-id="b99b4-114">Prerequisites</span></span>

* <span data-ttu-id="b99b4-115">Un abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="b99b4-115">An Azure subscription.</span></span> <span data-ttu-id="b99b4-116">Consultez la page [Obtention d’un essai gratuit d’Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="b99b4-116">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="b99b4-117">Un cluster Apache Spark sur HDInsight.</span><span class="sxs-lookup"><span data-stu-id="b99b4-117">An Apache Spark cluster on HDInsight.</span></span> <span data-ttu-id="b99b4-118">Pour obtenir des instructions, consultez [Création de clusters Apache Spark dans Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="b99b4-118">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>
* <span data-ttu-id="b99b4-119">Kit de développement logiciel (SDK) Oracle Java.</span><span class="sxs-lookup"><span data-stu-id="b99b4-119">Oracle Java Development kit.</span></span> <span data-ttu-id="b99b4-120">Vous pouvez l’installer à partir d’ [ici](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).</span><span class="sxs-lookup"><span data-stu-id="b99b4-120">You can install it from [here](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).</span></span>
* <span data-ttu-id="b99b4-121">IDE Java.</span><span class="sxs-lookup"><span data-stu-id="b99b4-121">A Java IDE.</span></span> <span data-ttu-id="b99b4-122">Cet article utilise IntelliJ IDEA 15.0.1.</span><span class="sxs-lookup"><span data-stu-id="b99b4-122">This article uses IntelliJ IDEA 15.0.1.</span></span> <span data-ttu-id="b99b4-123">Vous pouvez l’installer à partir d’ [ici](https://www.jetbrains.com/idea/download/).</span><span class="sxs-lookup"><span data-stu-id="b99b4-123">You can install it from [here](https://www.jetbrains.com/idea/download/).</span></span>

## <a name="install-scala-plugin-for-intellij-idea"></a><span data-ttu-id="b99b4-124">Installer le plug-in Scala pour IntelliJ IDEA</span><span class="sxs-lookup"><span data-stu-id="b99b4-124">Install Scala plugin for IntelliJ IDEA</span></span>
<span data-ttu-id="b99b4-125">Si l’installation d’IntelliJ IDEA ne vous invite pas à activer le plug-in Scala, lancez IntelliJ IDEA et parcourez les étapes suivantes pour installer le plug-in :</span><span class="sxs-lookup"><span data-stu-id="b99b4-125">If IntelliJ IDEA installation did not not prompt for enabling Scala plugin, launch IntelliJ IDEA and go through the following steps to install the plugin:</span></span>

1. <span data-ttu-id="b99b4-126">Démarrez IntelliJ IDEA, puis à partir de l’écran d’accueil, cliquez sur **Configurer**, puis sur **Plug-ins**.</span><span class="sxs-lookup"><span data-stu-id="b99b4-126">Start IntelliJ IDEA and from welcome screen click **Configure** and then click **Plugins**.</span></span>
   
    ![Activer le plug-in Scala](./media/hdinsight-apache-spark-create-standalone-application/enable-scala-plugin.png)
2. <span data-ttu-id="b99b4-128">Dans l'écran suivant, cliquez sur **Installer le plug-in JetBrains** dans le coin inférieur gauche.</span><span class="sxs-lookup"><span data-stu-id="b99b4-128">In the next screen, click **Install JetBrains plugin** from the lower left corner.</span></span> <span data-ttu-id="b99b4-129">Dans la boîte de dialogue **Parcourir les plug-ins JetBrains** qui s’ouvre, recherchez Scala, puis cliquez sur **Installer**.</span><span class="sxs-lookup"><span data-stu-id="b99b4-129">In the **Browse JetBrains Plugins** dialog box that opens, search for Scala and then click **Install**.</span></span>
   
    ![Installer le plug-in Scala](./media/hdinsight-apache-spark-create-standalone-application/install-scala-plugin.png)
3. <span data-ttu-id="b99b4-131">Une fois que le plug-in est correctement installé, cliquez sur bouton **Redémarrer IntelliJ IDEA** pour redémarrer l'IDE.</span><span class="sxs-lookup"><span data-stu-id="b99b4-131">After the plugin installs successfully, click the **Restart IntelliJ IDEA button** to restart the IDE.</span></span>

## <a name="create-a-standalone-scala-project"></a><span data-ttu-id="b99b4-132">Créer un programme Scala autonome</span><span class="sxs-lookup"><span data-stu-id="b99b4-132">Create a standalone Scala project</span></span>
1. <span data-ttu-id="b99b4-133">Lancez IntelliJ IDEA et créez un nouveau projet.</span><span class="sxs-lookup"><span data-stu-id="b99b4-133">Launch IntelliJ IDEA and create a new project.</span></span> <span data-ttu-id="b99b4-134">Dans la boîte de dialogue Nouveau projet, choisissez les options suivantes, puis cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="b99b4-134">In the new project dialog box, make the following choices, and then click **Next**.</span></span>
   
    ![Créer un projet Maven](./media/hdinsight-apache-spark-create-standalone-application/create-maven-project.png)
   
   * <span data-ttu-id="b99b4-136">Sélectionnez **Maven** comme type de projet.</span><span class="sxs-lookup"><span data-stu-id="b99b4-136">Select **Maven** as the project type.</span></span>
   * <span data-ttu-id="b99b4-137">Spécifiez un **projet SDK**.</span><span class="sxs-lookup"><span data-stu-id="b99b4-137">Specify a **Project SDK**.</span></span> <span data-ttu-id="b99b4-138">Cliquez sur Nouveau, puis accédez au répertoire d'installation Java, généralement `C:\Program Files\Java\jdk1.8.0_66`.</span><span class="sxs-lookup"><span data-stu-id="b99b4-138">Click New and navigate to the Java installation directory, typically `C:\Program Files\Java\jdk1.8.0_66`.</span></span>
   * <span data-ttu-id="b99b4-139">Sélectionnez l’option **Créer à partir d'un archétype** .</span><span class="sxs-lookup"><span data-stu-id="b99b4-139">Select the **Create from archetype** option.</span></span>
   * <span data-ttu-id="b99b4-140">Dans la liste des archétypes, sélectionnez **org.scala-tools.archetypes:scala-archetype-simple**.</span><span class="sxs-lookup"><span data-stu-id="b99b4-140">From the list of archetypes, select **org.scala-tools.archetypes:scala-archetype-simple**.</span></span> <span data-ttu-id="b99b4-141">Cela créera la structure de répertoire appropriée et téléchargera les dépendances requises par défaut pour écrire le programme Scala.</span><span class="sxs-lookup"><span data-stu-id="b99b4-141">This will create the right directory structure and download the required default dependencies to write Scala program.</span></span>
2. <span data-ttu-id="b99b4-142">Indiquez les valeurs appropriées pour **GroupId**, **ArtifactId** et **Version**.</span><span class="sxs-lookup"><span data-stu-id="b99b4-142">Provide relevant values for **GroupId**, **ArtifactId**, and **Version**.</span></span> <span data-ttu-id="b99b4-143">Cliquez sur **Next**.</span><span class="sxs-lookup"><span data-stu-id="b99b4-143">Click **Next**.</span></span>
3. <span data-ttu-id="b99b4-144">Dans la boîte de dialogue suivante, où vous spécifiez le répertoire de base Maven et d'autres paramètres utilisateur, acceptez les valeurs par défaut et cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="b99b4-144">In the next dialog box, where you specify Maven home directory and other user settings, accept the defaults and click **Next**.</span></span>
4. <span data-ttu-id="b99b4-145">Dans la dernière boîte de dialogue, spécifiez un nom de projet et un emplacement, puis cliquez sur **Terminer**.</span><span class="sxs-lookup"><span data-stu-id="b99b4-145">In the last dialog box, specify a project name and location and then click **Finish**.</span></span>
5. <span data-ttu-id="b99b4-146">Supprimez le fichier **MySpec.Scala** dans **src\test\scala\com\microsoft\spark\example**.</span><span class="sxs-lookup"><span data-stu-id="b99b4-146">Delete the **MySpec.Scala** file at **src\test\scala\com\microsoft\spark\example**.</span></span> <span data-ttu-id="b99b4-147">Ce fichier est inutile pour l'application.</span><span class="sxs-lookup"><span data-stu-id="b99b4-147">You do not need this for the application.</span></span>
6. <span data-ttu-id="b99b4-148">Si nécessaire, renommez les fichiers source et de test nommés par défaut.</span><span class="sxs-lookup"><span data-stu-id="b99b4-148">If required, rename the default source and test files.</span></span> <span data-ttu-id="b99b4-149">Dans le volet gauche d’IntelliJ IDEA, accédez à **src\main\scala\com.microsoft.spark.example**.</span><span class="sxs-lookup"><span data-stu-id="b99b4-149">From the left pane in the IntelliJ IDEA, navigate to **src\main\scala\com.microsoft.spark.example**.</span></span> <span data-ttu-id="b99b4-150">Cliquez avec le bouton droit sur **App.scala**, puis cliquez sur **Refactoriser** et sur Renommer un fichier. Dans la boîte de dialogue, indiquez le nouveau nom de l’application, puis cliquez sur **Refactoriser**.</span><span class="sxs-lookup"><span data-stu-id="b99b4-150">Right-click **App.scala**, click **Refactor**, click Rename file, and in the dialog box, provide the new name for the application and then click **Refactor**.</span></span>
   
    ![Renommer les fichiers](./media/hdinsight-apache-spark-create-standalone-application/rename-scala-files.png)  
7. <span data-ttu-id="b99b4-152">Dans les étapes suivantes, vous allez mettre à jour le fichier pom.xml pour définir les dépendances de l'application Spark Scala.</span><span class="sxs-lookup"><span data-stu-id="b99b4-152">In the subsequent steps, you will update the pom.xml to define the dependencies for the Spark Scala application.</span></span> <span data-ttu-id="b99b4-153">Ces dépendances sont téléchargées et résolues automatiquement, c’est pourquoi vous devez configurer Maven en conséquence.</span><span class="sxs-lookup"><span data-stu-id="b99b4-153">For those dependencies to be downloaded and resolved automatically, you must configure Maven accordingly.</span></span>
   
    ![Configurer Maven pour les téléchargements automatiques](./media/hdinsight-apache-spark-create-standalone-application/configure-maven.png)
   
   1. <span data-ttu-id="b99b4-155">Dans le menu **Fichier**, cliquez sur **Paramètres**.</span><span class="sxs-lookup"><span data-stu-id="b99b4-155">From the **File** menu, click **Settings**.</span></span>
   2. <span data-ttu-id="b99b4-156">Dans la boîte de dialogue **Paramètres**, accédez à **Génération, exécution, déploiement** > **Outils de génération** > **Maven** > **Importation**.</span><span class="sxs-lookup"><span data-stu-id="b99b4-156">In the **Settings** dialog box, navigate to **Build, Execution, Deployment** > **Build Tools** > **Maven** > **Importing**.</span></span>
   3. <span data-ttu-id="b99b4-157">Sélectionnez l'option **Importer les projets Maven automatiquement**.</span><span class="sxs-lookup"><span data-stu-id="b99b4-157">Select the option to **Import Maven projects automatically**.</span></span>
   4. <span data-ttu-id="b99b4-158">Cliquez sur **Appliquer**, puis sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="b99b4-158">Click **Apply**, and then click **OK**.</span></span>
8. <span data-ttu-id="b99b4-159">Mettez à jour le fichier source Scala pour inclure le code de votre application.</span><span class="sxs-lookup"><span data-stu-id="b99b4-159">Update the Scala source file to include your application code.</span></span> <span data-ttu-id="b99b4-160">Ouvrez et remplacez le code existant par le code suivant et enregistrez les modifications.</span><span class="sxs-lookup"><span data-stu-id="b99b4-160">Open and replace the existing sample code with the following code and save the changes.</span></span> <span data-ttu-id="b99b4-161">Ce code lit les données du fichier HVAC.csv (disponible sur tous les clusters HDInsight Spark), récupère les lignes qui contiennent uniquement un chiffre dans la sixième colonne et écrit la sortie dans **/HVACOut** , sous le conteneur de stockage par défaut du cluster.</span><span class="sxs-lookup"><span data-stu-id="b99b4-161">This code reads the data from the HVAC.csv (available on all HDInsight Spark clusters), retrieves the rows that only have one digit in the sixth column, and writes the output to **/HVACOut** under the default storage container for the cluster.</span></span>
   
        package com.microsoft.spark.example
   
        import org.apache.spark.SparkConf
        import org.apache.spark.SparkContext
   
        /**
          * Test IO to wasb
          */
        object WasbIOTest {
          def main (arg: Array[String]): Unit = {
            val conf = new SparkConf().setAppName("WASBIOTest")
            val sc = new SparkContext(conf)
   
            val rdd = sc.textFile("wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")
   
            //find the rows which have only one digit in the 7th column in the CSV
            val rdd1 = rdd.filter(s => s.split(",")(6).length() == 1)
   
            rdd1.saveAsTextFile("wasb:///HVACout")
          }
        }
9. <span data-ttu-id="b99b4-162">Mettez à jour le fichier pom.xml.</span><span class="sxs-lookup"><span data-stu-id="b99b4-162">Update the pom.xml.</span></span>
   
   1. <span data-ttu-id="b99b4-163">Ajoutez le bloc de code suivant à `<project>\<properties>` :</span><span class="sxs-lookup"><span data-stu-id="b99b4-163">Within `<project>\<properties>` add the following:</span></span>
      
          <scala.version>2.10.4</scala.version>
          <scala.compat.version>2.10.4</scala.compat.version>
          <scala.binary.version>2.10</scala.binary.version>
   2. <span data-ttu-id="b99b4-164">Ajoutez le bloc de code suivant à `<project>\<dependencies>` :</span><span class="sxs-lookup"><span data-stu-id="b99b4-164">Within `<project>\<dependencies>` add the following:</span></span>
      
           <dependency>
             <groupId>org.apache.spark</groupId>
             <artifactId>spark-core_${scala.binary.version}</artifactId>
             <version>1.4.1</version>
           </dependency>
      
      <span data-ttu-id="b99b4-165">Enregistrez les modifications apportées au fichier pom.xml.</span><span class="sxs-lookup"><span data-stu-id="b99b4-165">Save changes to pom.xml.</span></span>
10. <span data-ttu-id="b99b4-166">Créez le fichier .jar</span><span class="sxs-lookup"><span data-stu-id="b99b4-166">Create the .jar file.</span></span> <span data-ttu-id="b99b4-167">IntelliJ IDEA permet de créer le fichier JAR en tant qu’artefact d'un projet.</span><span class="sxs-lookup"><span data-stu-id="b99b4-167">IntelliJ IDEA enables creation of JAR as an artifact of a project.</span></span> <span data-ttu-id="b99b4-168">Procédez comme suit.</span><span class="sxs-lookup"><span data-stu-id="b99b4-168">Perform the following steps.</span></span>
    
    1. <span data-ttu-id="b99b4-169">Dans le menu **Fichier**, cliquez sur **Structure de projet**.</span><span class="sxs-lookup"><span data-stu-id="b99b4-169">From the **File** menu, click **Project Structure**.</span></span>
    2. <span data-ttu-id="b99b4-170">Dans la boîte de dialogue **Structure de projet**, cliquez sur **Artefacts**, puis sur le signe plus.</span><span class="sxs-lookup"><span data-stu-id="b99b4-170">In the **Project Structure** dialog box, click **Artifacts** and then click the plus symbol.</span></span> <span data-ttu-id="b99b4-171">Dans la boîte de dialogue contextuelle, cliquez sur **JAR**, puis sur **À partir de modules ayant des dépendances**.</span><span class="sxs-lookup"><span data-stu-id="b99b4-171">From the pop-up dialog box, click **JAR**, and then click **From modules with dependencies**.</span></span>
       
        ![Créer un fichier jar](./media/hdinsight-apache-spark-create-standalone-application/create-jar-1.png)
    3. <span data-ttu-id="b99b4-173">Dans la boîte de dialogue **Créer un fichier JAR à partir de modules**, cliquez sur le bouton de sélection (![ellipse](./media/hdinsight-apache-spark-create-standalone-application/ellipsis.png)) en regard de **Classe principale**.</span><span class="sxs-lookup"><span data-stu-id="b99b4-173">In the **Create JAR from Modules** dialog box, click the ellipsis (![ellipsis](./media/hdinsight-apache-spark-create-standalone-application/ellipsis.png) ) against the **Main Class**.</span></span>
    4. <span data-ttu-id="b99b4-174">Dans la boîte de dialogue **Sélectionner une classe principale**, sélectionnez la classe qui s’affiche par défaut, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="b99b4-174">In the **Select Main Class** dialog box, select the class that appears by default and then click **OK**.</span></span>
       
        ![Créer un fichier jar](./media/hdinsight-apache-spark-create-standalone-application/create-jar-2.png)
    5. <span data-ttu-id="b99b4-176">Dans la boîte de dialogue **Create JAR from Modules** (Créer un fichier JAR à partir de modules), assurez-vous que l’option **Extract to the target JAR** (Extraire vers le fichier JAR cible) est activée, puis cliquez sur **OK** (OK).</span><span class="sxs-lookup"><span data-stu-id="b99b4-176">In the **Create JAR from Modules** dialog box, make sure that the option to **extract to the target JAR** is selected, and then click **OK**.</span></span> <span data-ttu-id="b99b4-177">Cela crée un fichier JAR contenant toutes les dépendances.</span><span class="sxs-lookup"><span data-stu-id="b99b4-177">This creates a single JAR with all dependencies.</span></span>
       
        ![Créer un fichier jar](./media/hdinsight-apache-spark-create-standalone-application/create-jar-3.png)
    6. <span data-ttu-id="b99b4-179">L’onglet Disposition de la sortie répertorie tous les fichiers JAR inclus dans le cadre du projet Maven.</span><span class="sxs-lookup"><span data-stu-id="b99b4-179">The output layout tab lists all the jars that are included as part of the Maven project.</span></span> <span data-ttu-id="b99b4-180">Vous pouvez sélectionner et supprimer ceux sur lesquels l’application Scala n’a aucune dépendance directe.</span><span class="sxs-lookup"><span data-stu-id="b99b4-180">You can select and delete the ones on which the Scala application has no direct dependency.</span></span> <span data-ttu-id="b99b4-181">Pour l’application que nous créons ici, vous pouvez tous les supprimer sauf le dernier (**SparkSimpleApp compile output**).</span><span class="sxs-lookup"><span data-stu-id="b99b4-181">For the application we are creating here, you can remove all but the last one (**SparkSimpleApp compile output**).</span></span> <span data-ttu-id="b99b4-182">Sélectionnez les fichiers JAR à supprimer, puis cliquez sur l’icône **Delete** .</span><span class="sxs-lookup"><span data-stu-id="b99b4-182">Select the jars to delete and then click the **Delete** icon.</span></span>
       
        ![Créer un fichier jar](./media/hdinsight-apache-spark-create-standalone-application/delete-output-jars.png)
       
        <span data-ttu-id="b99b4-184">Assurez-vous que la case à cocher **Générer à la création** est activée, ce qui garantit la création du fichier JAR à chaque génération ou mise à jour du projet.</span><span class="sxs-lookup"><span data-stu-id="b99b4-184">Make sure **Build on make** box is selected, which ensures that the jar is created every time the project is built or updated.</span></span> <span data-ttu-id="b99b4-185">Cliquez sur **Appliquer**, puis sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="b99b4-185">Click **Apply** and then **OK**.</span></span>
    7. <span data-ttu-id="b99b4-186">Dans la barre de menus, cliquez sur **Générer**, puis sur **Créer le projet**.</span><span class="sxs-lookup"><span data-stu-id="b99b4-186">From the menu bar, click **Build**, and then click **Make Project**.</span></span> <span data-ttu-id="b99b4-187">Vous pouvez également cliquer sur **Générer les artefacts** pour créer le fichier JAR.</span><span class="sxs-lookup"><span data-stu-id="b99b4-187">You can also click **Build Artifacts** to create the jar.</span></span> <span data-ttu-id="b99b4-188">Le fichier JAR de sortie est créé sous **\out\artifacts**.</span><span class="sxs-lookup"><span data-stu-id="b99b4-188">The output jar is created under **\out\artifacts**.</span></span>
       
        ![Créer un fichier jar](./media/hdinsight-apache-spark-create-standalone-application/output.png)

## <a name="run-the-application-on-the-spark-cluster"></a><span data-ttu-id="b99b4-190">Exécuter l’application sur le cluster Spark</span><span class="sxs-lookup"><span data-stu-id="b99b4-190">Run the application on the Spark cluster</span></span>
<span data-ttu-id="b99b4-191">Pour exécuter l'application sur le cluster, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="b99b4-191">To run the application on the cluster, you must do the following:</span></span>

* <span data-ttu-id="b99b4-192">**Copiez le fichier JAR d'application sur l'objet blob Azure Storage** associé au cluster.</span><span class="sxs-lookup"><span data-stu-id="b99b4-192">**Copy the application jar to the Azure storage blob** associated with the cluster.</span></span> <span data-ttu-id="b99b4-193">Pour ce faire, vous pouvez utiliser l’utilitaire de ligne de commande [**AzCopy**](../storage/common/storage-use-azcopy.md).</span><span class="sxs-lookup"><span data-stu-id="b99b4-193">You can use [**AzCopy**](../storage/common/storage-use-azcopy.md), a command line utility, to do so.</span></span> <span data-ttu-id="b99b4-194">De nombreux autres clients permettent également de télécharger des données.</span><span class="sxs-lookup"><span data-stu-id="b99b4-194">There are a lot of other clients as well that you can use to upload data.</span></span> <span data-ttu-id="b99b4-195">Pour en savoir plus à leur sujet, consultez [Téléchargement de données pour les travaux Hadoop dans HDInsight](hdinsight-upload-data.md).</span><span class="sxs-lookup"><span data-stu-id="b99b4-195">You can find more about them at [Upload data for Hadoop jobs in HDInsight](hdinsight-upload-data.md).</span></span>
* <span data-ttu-id="b99b4-196">**Utilisez Livy pour soumettre une tâche de l'application à distance** au cluster Spark.</span><span class="sxs-lookup"><span data-stu-id="b99b4-196">**Use Livy to submit an application job remotely** to the Spark cluster.</span></span> <span data-ttu-id="b99b4-197">Les clusters Spark sur HDInsight incluent Livy qui expose des points de terminaison REST permettant d’envoyer à distance des travaux Spark.</span><span class="sxs-lookup"><span data-stu-id="b99b4-197">Spark clusters on HDInsight includes Livy that exposes REST endpoints to remotely submit Spark jobs.</span></span> <span data-ttu-id="b99b4-198">Pour plus d’informations, consultez [Envoi de travaux Spark à distance en utilisant Livy avec les clusters Spark sur HDInsight](hdinsight-apache-spark-livy-rest-interface.md).</span><span class="sxs-lookup"><span data-stu-id="b99b4-198">For more information, see [Submit Spark jobs remotely using Livy with Spark clusters on HDInsight](hdinsight-apache-spark-livy-rest-interface.md).</span></span>

## <a name="next-step"></a><span data-ttu-id="b99b4-199">Étape suivante</span><span class="sxs-lookup"><span data-stu-id="b99b4-199">Next step</span></span>

<span data-ttu-id="b99b4-200">Dans cet article, vous avez appris comment créer une application Spark Scala.</span><span class="sxs-lookup"><span data-stu-id="b99b4-200">In this article you learned how to create a Spark scala application.</span></span> <span data-ttu-id="b99b4-201">Passez à l’article suivant pour savoir comment exécuter cette application sur un cluster HDInsight Spark en utilisant Livy.</span><span class="sxs-lookup"><span data-stu-id="b99b4-201">Advance to the next article to learn how to run this application on an HDInsight Spark cluster using Livy.</span></span>

> [!div class="nextstepaction"]
>[<span data-ttu-id="b99b4-202">Exécuter des tâches à distance avec Livy sur un cluster Spark</span><span class="sxs-lookup"><span data-stu-id="b99b4-202">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

