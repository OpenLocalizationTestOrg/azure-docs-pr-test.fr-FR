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
# <a name="create-a-scala-maven-application-toorun-on-apache-spark-cluster-on-hdinsight"></a><span data-ttu-id="d3053-103">Créer un toorun d’application Scala Maven sur cluster Apache Spark sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="d3053-103">Create a Scala Maven application toorun on Apache Spark cluster on HDInsight</span></span>

<span data-ttu-id="d3053-104">Découvrez comment toocreate une application de Spark écrite en Scala avec Maven IntelliJ idée.</span><span class="sxs-lookup"><span data-stu-id="d3053-104">Learn how toocreate a Spark application written in Scala using Maven with IntelliJ IDEA.</span></span> <span data-ttu-id="d3053-105">article de Hello utilise Apache Maven hello système de génération et commence par archétype Maven existant pour Scala fournie par IntelliJ idée.</span><span class="sxs-lookup"><span data-stu-id="d3053-105">hello article uses Apache Maven as hello build system and starts with an existing Maven archetype for Scala provided by IntelliJ IDEA.</span></span>  <span data-ttu-id="d3053-106">Création d’une application de Scala dans IntelliJ idée implique hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="d3053-106">Creating a Scala application in IntelliJ IDEA involves hello following steps:</span></span>

* <span data-ttu-id="d3053-107">Utilisez Maven en tant que système de génération hello.</span><span class="sxs-lookup"><span data-stu-id="d3053-107">Use Maven as hello build system.</span></span>
* <span data-ttu-id="d3053-108">Mettre à jour les dépendances de modules de modèle d’objet projet (POM) fichier tooresolve Spark.</span><span class="sxs-lookup"><span data-stu-id="d3053-108">Update Project Object Model (POM) file tooresolve Spark module dependencies.</span></span>
* <span data-ttu-id="d3053-109">Écrire votre application dans Scala.</span><span class="sxs-lookup"><span data-stu-id="d3053-109">Write your application in Scala.</span></span>
* <span data-ttu-id="d3053-110">Générer un fichier jar qui peut être soumis tooHDInsight Spark clusters.</span><span class="sxs-lookup"><span data-stu-id="d3053-110">Generate a jar file that can be submitted tooHDInsight Spark clusters.</span></span>
* <span data-ttu-id="d3053-111">Exécuter l’application hello sur cluster Spark à l’aide de Livy.</span><span class="sxs-lookup"><span data-stu-id="d3053-111">Run hello application on Spark cluster using Livy.</span></span>

> [!NOTE]
> <span data-ttu-id="d3053-112">HDInsight fournit également un idée de IntelliJ plug-in outil tooease hello processus de création et envoi d’applications tooan cluster HDInsight Spark sur Linux.</span><span class="sxs-lookup"><span data-stu-id="d3053-112">HDInsight also provides an IntelliJ IDEA plugin tool tooease hello process of creating and submitting applications tooan HDInsight Spark cluster on Linux.</span></span> <span data-ttu-id="d3053-113">Pour plus d’informations, consultez [utilisez HDInsight outils plug-in pour IntelliJ idée toocreate et soumettre des applications de Spark](hdinsight-apache-spark-intellij-tool-plugin.md).</span><span class="sxs-lookup"><span data-stu-id="d3053-113">For more information, see [Use HDInsight Tools Plugin for IntelliJ IDEA toocreate and submit Spark applications](hdinsight-apache-spark-intellij-tool-plugin.md).</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="d3053-114">Composants requis</span><span class="sxs-lookup"><span data-stu-id="d3053-114">Prerequisites</span></span>

* <span data-ttu-id="d3053-115">Un abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="d3053-115">An Azure subscription.</span></span> <span data-ttu-id="d3053-116">Consultez la page [Obtention d’un essai gratuit d’Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="d3053-116">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="d3053-117">Un cluster Apache Spark sur HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d3053-117">An Apache Spark cluster on HDInsight.</span></span> <span data-ttu-id="d3053-118">Pour obtenir des instructions, consultez [Création de clusters Apache Spark dans Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="d3053-118">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>
* <span data-ttu-id="d3053-119">Kit de développement logiciel (SDK) Oracle Java.</span><span class="sxs-lookup"><span data-stu-id="d3053-119">Oracle Java Development kit.</span></span> <span data-ttu-id="d3053-120">Vous pouvez l’installer à partir d’ [ici](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).</span><span class="sxs-lookup"><span data-stu-id="d3053-120">You can install it from [here](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).</span></span>
* <span data-ttu-id="d3053-121">IDE Java.</span><span class="sxs-lookup"><span data-stu-id="d3053-121">A Java IDE.</span></span> <span data-ttu-id="d3053-122">Cet article utilise IntelliJ IDEA 15.0.1.</span><span class="sxs-lookup"><span data-stu-id="d3053-122">This article uses IntelliJ IDEA 15.0.1.</span></span> <span data-ttu-id="d3053-123">Vous pouvez l’installer à partir d’ [ici](https://www.jetbrains.com/idea/download/).</span><span class="sxs-lookup"><span data-stu-id="d3053-123">You can install it from [here](https://www.jetbrains.com/idea/download/).</span></span>

## <a name="install-scala-plugin-for-intellij-idea"></a><span data-ttu-id="d3053-124">Installer le plug-in Scala pour IntelliJ IDEA</span><span class="sxs-lookup"><span data-stu-id="d3053-124">Install Scala plugin for IntelliJ IDEA</span></span>
<span data-ttu-id="d3053-125">Si les installation IntelliJ idée ne s’invite pas pas pour l’activation du plug-in Scala, lancez IntelliJ idée et accéder à hello suivant le plug-in hello étapes tooinstall :</span><span class="sxs-lookup"><span data-stu-id="d3053-125">If IntelliJ IDEA installation did not not prompt for enabling Scala plugin, launch IntelliJ IDEA and go through hello following steps tooinstall hello plugin:</span></span>

1. <span data-ttu-id="d3053-126">Démarrez IntelliJ IDEA, puis à partir de l’écran d’accueil, cliquez sur **Configurer**, puis sur **Plug-ins**.</span><span class="sxs-lookup"><span data-stu-id="d3053-126">Start IntelliJ IDEA and from welcome screen click **Configure** and then click **Plugins**.</span></span>
   
    ![Activer le plug-in Scala](./media/hdinsight-apache-spark-create-standalone-application/enable-scala-plugin.png)
2. <span data-ttu-id="d3053-128">Dans l’écran suivant de hello, cliquez sur **plug-in de l’installation de JetBrains** à partir de l’angle inférieur gauche hello.</span><span class="sxs-lookup"><span data-stu-id="d3053-128">In hello next screen, click **Install JetBrains plugin** from hello lower left corner.</span></span> <span data-ttu-id="d3053-129">Bonjour **parcourir les plug-ins JetBrains** boîte de dialogue qui s’ouvre, recherchez Scala, puis **installer**.</span><span class="sxs-lookup"><span data-stu-id="d3053-129">In hello **Browse JetBrains Plugins** dialog box that opens, search for Scala and then click **Install**.</span></span>
   
    ![Installer le plug-in Scala](./media/hdinsight-apache-spark-create-standalone-application/install-scala-plugin.png)
3. <span data-ttu-id="d3053-131">Une fois que le plug-in hello s’installe correctement, cliquez sur hello **bouton de redémarrer une idée de IntelliJ** toorestart hello IDE.</span><span class="sxs-lookup"><span data-stu-id="d3053-131">After hello plugin installs successfully, click hello **Restart IntelliJ IDEA button** toorestart hello IDE.</span></span>

## <a name="create-a-standalone-scala-project"></a><span data-ttu-id="d3053-132">Créer un programme Scala autonome</span><span class="sxs-lookup"><span data-stu-id="d3053-132">Create a standalone Scala project</span></span>
1. <span data-ttu-id="d3053-133">Lancez IntelliJ IDEA et créez un nouveau projet.</span><span class="sxs-lookup"><span data-stu-id="d3053-133">Launch IntelliJ IDEA and create a new project.</span></span> <span data-ttu-id="d3053-134">Dans la boîte de dialogue Nouveau projet hello, rendre hello des options suivantes, puis cliquez sur **suivant**.</span><span class="sxs-lookup"><span data-stu-id="d3053-134">In hello new project dialog box, make hello following choices, and then click **Next**.</span></span>
   
    ![Créer un projet Maven](./media/hdinsight-apache-spark-create-standalone-application/create-maven-project.png)
   
   * <span data-ttu-id="d3053-136">Sélectionnez **Maven** en tant que type de projet hello.</span><span class="sxs-lookup"><span data-stu-id="d3053-136">Select **Maven** as hello project type.</span></span>
   * <span data-ttu-id="d3053-137">Spécifiez un **projet SDK**.</span><span class="sxs-lookup"><span data-stu-id="d3053-137">Specify a **Project SDK**.</span></span> <span data-ttu-id="d3053-138">Cliquez sur Nouveau et accédez répertoire d’installation de Java toohello généralement `C:\Program Files\Java\jdk1.8.0_66`.</span><span class="sxs-lookup"><span data-stu-id="d3053-138">Click New and navigate toohello Java installation directory, typically `C:\Program Files\Java\jdk1.8.0_66`.</span></span>
   * <span data-ttu-id="d3053-139">Sélectionnez hello **à partir d’un archétype** option.</span><span class="sxs-lookup"><span data-stu-id="d3053-139">Select hello **Create from archetype** option.</span></span>
   * <span data-ttu-id="d3053-140">Dans la liste hello d’archetypes, sélectionnez **org.scala tools.archetypes:scala archétype simple**.</span><span class="sxs-lookup"><span data-stu-id="d3053-140">From hello list of archetypes, select **org.scala-tools.archetypes:scala-archetype-simple**.</span></span> <span data-ttu-id="d3053-141">Cela créer une structure de répertoire correct hello et télécharger le programme Scala toowrite hello requis par défaut dépendances.</span><span class="sxs-lookup"><span data-stu-id="d3053-141">This will create hello right directory structure and download hello required default dependencies toowrite Scala program.</span></span>
2. <span data-ttu-id="d3053-142">Indiquez les valeurs appropriées pour **GroupId**, **ArtifactId** et **Version**.</span><span class="sxs-lookup"><span data-stu-id="d3053-142">Provide relevant values for **GroupId**, **ArtifactId**, and **Version**.</span></span> <span data-ttu-id="d3053-143">Cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="d3053-143">Click **Next**.</span></span>
3. <span data-ttu-id="d3053-144">Dans hello boîte de dialogue suivante où vous spécifiez le répertoire de base Maven et d’autres paramètres de l’utilisateur, acceptez les valeurs par défaut hello et cliquez sur **suivant**.</span><span class="sxs-lookup"><span data-stu-id="d3053-144">In hello next dialog box, where you specify Maven home directory and other user settings, accept hello defaults and click **Next**.</span></span>
4. <span data-ttu-id="d3053-145">Dans la dernière boîte de dialogue hello, spécifiez un nom de projet et un emplacement, puis **Terminer**.</span><span class="sxs-lookup"><span data-stu-id="d3053-145">In hello last dialog box, specify a project name and location and then click **Finish**.</span></span>
5. <span data-ttu-id="d3053-146">Supprimer hello **MySpec.Scala** de fichiers au **src\test\scala\com\microsoft\spark\example**.</span><span class="sxs-lookup"><span data-stu-id="d3053-146">Delete hello **MySpec.Scala** file at **src\test\scala\com\microsoft\spark\example**.</span></span> <span data-ttu-id="d3053-147">Il est inutile cela pour l’application hello.</span><span class="sxs-lookup"><span data-stu-id="d3053-147">You do not need this for hello application.</span></span>
6. <span data-ttu-id="d3053-148">Si nécessaire, renommez les fichiers de code source et de test par défaut hello.</span><span class="sxs-lookup"><span data-stu-id="d3053-148">If required, rename hello default source and test files.</span></span> <span data-ttu-id="d3053-149">À partir du volet de gauche hello Bonjour IntelliJ idée, accédez trop**src\main\scala\com.microsoft.spark.example**.</span><span class="sxs-lookup"><span data-stu-id="d3053-149">From hello left pane in hello IntelliJ IDEA, navigate too**src\main\scala\com.microsoft.spark.example**.</span></span> <span data-ttu-id="d3053-150">Avec le bouton droit **App.scala**, cliquez sur **refactoriser**, cliquez sur Renommer un fichier et dans la boîte de dialogue hello, indiquez hello nouveau nom pour l’application hello et puis cliquez sur **refactoriser**.</span><span class="sxs-lookup"><span data-stu-id="d3053-150">Right-click **App.scala**, click **Refactor**, click Rename file, and in hello dialog box, provide hello new name for hello application and then click **Refactor**.</span></span>
   
    ![Renommer les fichiers](./media/hdinsight-apache-spark-create-standalone-application/rename-scala-files.png)  
7. <span data-ttu-id="d3053-152">Dans les étapes suivantes hello, vous mettrez à jour les dépendances hello pom.xml toodefine hello hello Spark Scala application.</span><span class="sxs-lookup"><span data-stu-id="d3053-152">In hello subsequent steps, you will update hello pom.xml toodefine hello dependencies for hello Spark Scala application.</span></span> <span data-ttu-id="d3053-153">Pour ces dépendances toobe téléchargé et résolus automatiquement, que vous devez configurer Maven en conséquence.</span><span class="sxs-lookup"><span data-stu-id="d3053-153">For those dependencies toobe downloaded and resolved automatically, you must configure Maven accordingly.</span></span>
   
    ![Configurer Maven pour les téléchargements automatiques](./media/hdinsight-apache-spark-create-standalone-application/configure-maven.png)
   
   1. <span data-ttu-id="d3053-155">À partir de hello **fichier** menu, cliquez sur **paramètres**.</span><span class="sxs-lookup"><span data-stu-id="d3053-155">From hello **File** menu, click **Settings**.</span></span>
   2. <span data-ttu-id="d3053-156">Bonjour **paramètres** boîte de dialogue, accédez trop**déploiement de la Build, l’exécution,** > **outils de génération** > **Maven**  >  **Importation**.</span><span class="sxs-lookup"><span data-stu-id="d3053-156">In hello **Settings** dialog box, navigate too**Build, Execution, Deployment** > **Build Tools** > **Maven** > **Importing**.</span></span>
   3. <span data-ttu-id="d3053-157">L’option hello trop**automatiquement les projets Maven d’importation**.</span><span class="sxs-lookup"><span data-stu-id="d3053-157">Select hello option too**Import Maven projects automatically**.</span></span>
   4. <span data-ttu-id="d3053-158">Cliquez sur **Appliquer**, puis sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="d3053-158">Click **Apply**, and then click **OK**.</span></span>
8. <span data-ttu-id="d3053-159">Mettre à jour hello Scala source fichier tooinclude votre code d’application.</span><span class="sxs-lookup"><span data-stu-id="d3053-159">Update hello Scala source file tooinclude your application code.</span></span> <span data-ttu-id="d3053-160">Ouvrez et remplacez hello existants dans exemple de code hello suivant de code et enregistrer les modifications de hello.</span><span class="sxs-lookup"><span data-stu-id="d3053-160">Open and replace hello existing sample code with hello following code and save hello changes.</span></span> <span data-ttu-id="d3053-161">Ce code lit les données de salutation hello HVAC.csv (disponible sur tous les clusters HDInsight Spark), récupère les lignes hello qui ont uniquement un chiffre dans la sixième colonne de hello et écrit la sortie de hello trop**/HVACOut** sous stockage de la valeur par défaut hello conteneur pour un cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="d3053-161">This code reads hello data from hello HVAC.csv (available on all HDInsight Spark clusters), retrieves hello rows that only have one digit in hello sixth column, and writes hello output too**/HVACOut** under hello default storage container for hello cluster.</span></span>
   
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
9. <span data-ttu-id="d3053-162">Mettre à jour hello pom.xml.</span><span class="sxs-lookup"><span data-stu-id="d3053-162">Update hello pom.xml.</span></span>
   
   1. <span data-ttu-id="d3053-163">Dans `<project>\<properties>` ajoutez hello qui suit :</span><span class="sxs-lookup"><span data-stu-id="d3053-163">Within `<project>\<properties>` add hello following:</span></span>
      
          <scala.version>2.10.4</scala.version>
          <scala.compat.version>2.10.4</scala.compat.version>
          <scala.binary.version>2.10</scala.binary.version>
   2. <span data-ttu-id="d3053-164">Dans `<project>\<dependencies>` ajoutez hello qui suit :</span><span class="sxs-lookup"><span data-stu-id="d3053-164">Within `<project>\<dependencies>` add hello following:</span></span>
      
           <dependency>
             <groupId>org.apache.spark</groupId>
             <artifactId>spark-core_${scala.binary.version}</artifactId>
             <version>1.4.1</version>
           </dependency>
      
      <span data-ttu-id="d3053-165">Enregistrer les modifications toopom.xml.</span><span class="sxs-lookup"><span data-stu-id="d3053-165">Save changes toopom.xml.</span></span>
10. <span data-ttu-id="d3053-166">Création du fichier .jar hello.</span><span class="sxs-lookup"><span data-stu-id="d3053-166">Create hello .jar file.</span></span> <span data-ttu-id="d3053-167">IntelliJ IDEA permet de créer le fichier JAR en tant qu’artefact d'un projet.</span><span class="sxs-lookup"><span data-stu-id="d3053-167">IntelliJ IDEA enables creation of JAR as an artifact of a project.</span></span> <span data-ttu-id="d3053-168">Effectuer hello comme suit.</span><span class="sxs-lookup"><span data-stu-id="d3053-168">Perform hello following steps.</span></span>
    
    1. <span data-ttu-id="d3053-169">À partir de hello **fichier** menu, cliquez sur **Structure de projet**.</span><span class="sxs-lookup"><span data-stu-id="d3053-169">From hello **File** menu, click **Project Structure**.</span></span>
    2. <span data-ttu-id="d3053-170">Bonjour **Structure de projet** boîte de dialogue, cliquez sur **artefacts** puis hello plus de symbole.</span><span class="sxs-lookup"><span data-stu-id="d3053-170">In hello **Project Structure** dialog box, click **Artifacts** and then click hello plus symbol.</span></span> <span data-ttu-id="d3053-171">Dans la boîte de dialogue contextuelle hello, cliquez sur **JAR**, puis cliquez sur **à partir de modules avec des dépendances**.</span><span class="sxs-lookup"><span data-stu-id="d3053-171">From hello pop-up dialog box, click **JAR**, and then click **From modules with dependencies**.</span></span>
       
        ![Créer un fichier jar](./media/hdinsight-apache-spark-create-standalone-application/create-jar-1.png)
    3. <span data-ttu-id="d3053-173">Bonjour **créer JAR à partir de Modules** boîte de dialogue, cliquez sur les points de suspension hello (![points de suspension](./media/hdinsight-apache-spark-create-standalone-application/ellipsis.png) ) par rapport à hello **principale classe**.</span><span class="sxs-lookup"><span data-stu-id="d3053-173">In hello **Create JAR from Modules** dialog box, click hello ellipsis (![ellipsis](./media/hdinsight-apache-spark-create-standalone-application/ellipsis.png) ) against hello **Main Class**.</span></span>
    4. <span data-ttu-id="d3053-174">Bonjour **sélection de la classe principale** boîte de dialogue, la classe hello sélectionnez s’affiche par défaut, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="d3053-174">In hello **Select Main Class** dialog box, select hello class that appears by default and then click **OK**.</span></span>
       
        ![Créer un fichier jar](./media/hdinsight-apache-spark-create-standalone-application/create-jar-2.png)
    5. <span data-ttu-id="d3053-176">Bonjour **créer JAR à partir de Modules** boîte de dialogue zone, assurez-vous que cette option hello trop**extraire toohello cible JAR** est sélectionné, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="d3053-176">In hello **Create JAR from Modules** dialog box, make sure that hello option too**extract toohello target JAR** is selected, and then click **OK**.</span></span> <span data-ttu-id="d3053-177">Cela crée un fichier JAR contenant toutes les dépendances.</span><span class="sxs-lookup"><span data-stu-id="d3053-177">This creates a single JAR with all dependencies.</span></span>
       
        ![Créer un fichier jar](./media/hdinsight-apache-spark-create-standalone-application/create-jar-3.png)
    6. <span data-ttu-id="d3053-179">onglet Disposition de sortie Hello répertorie tous les fichiers JAR hello qui sont inclus dans le cadre du projet de Maven hello.</span><span class="sxs-lookup"><span data-stu-id="d3053-179">hello output layout tab lists all hello jars that are included as part of hello Maven project.</span></span> <span data-ttu-id="d3053-180">Vous pouvez sélectionner et hello supprimer ceux sur lesquels hello Scala application ne possède pas de dépendance directe.</span><span class="sxs-lookup"><span data-stu-id="d3053-180">You can select and delete hello ones on which hello Scala application has no direct dependency.</span></span> <span data-ttu-id="d3053-181">Pour l’application hello, nous allons créer ici, vous pouvez supprimer tout sauf hello dernière (**SparkSimpleApp compilation sortie**).</span><span class="sxs-lookup"><span data-stu-id="d3053-181">For hello application we are creating here, you can remove all but hello last one (**SparkSimpleApp compile output**).</span></span> <span data-ttu-id="d3053-182">Sélectionnez hello JAR toodelete, puis cliquez sur hello **supprimer** icône.</span><span class="sxs-lookup"><span data-stu-id="d3053-182">Select hello jars toodelete and then click hello **Delete** icon.</span></span>
       
        ![Créer un fichier jar](./media/hdinsight-apache-spark-create-standalone-application/delete-output-jars.png)
       
        <span data-ttu-id="d3053-184">Assurez-vous que **Build sur Vérifiez** à cocher est activée, ce qui garantit que ce fichier jar hello est créé chaque fois que projet de hello est généré ou mis à jour.</span><span class="sxs-lookup"><span data-stu-id="d3053-184">Make sure **Build on make** box is selected, which ensures that hello jar is created every time hello project is built or updated.</span></span> <span data-ttu-id="d3053-185">Cliquez sur **Appliquer**, puis sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="d3053-185">Click **Apply** and then **OK**.</span></span>
    7. <span data-ttu-id="d3053-186">Dans la barre de menus de hello, cliquez sur **générer**, puis cliquez sur **créer le projet**.</span><span class="sxs-lookup"><span data-stu-id="d3053-186">From hello menu bar, click **Build**, and then click **Make Project**.</span></span> <span data-ttu-id="d3053-187">Vous pouvez également cliquer sur **des artefacts de Build** jar de hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="d3053-187">You can also click **Build Artifacts** toocreate hello jar.</span></span> <span data-ttu-id="d3053-188">Hello jar de sortie est créé sous **\out\artifacts**.</span><span class="sxs-lookup"><span data-stu-id="d3053-188">hello output jar is created under **\out\artifacts**.</span></span>
       
        ![Créer un fichier jar](./media/hdinsight-apache-spark-create-standalone-application/output.png)

## <a name="run-hello-application-on-hello-spark-cluster"></a><span data-ttu-id="d3053-190">Exécutez l’application hello sur cluster Spark de hello</span><span class="sxs-lookup"><span data-stu-id="d3053-190">Run hello application on hello Spark cluster</span></span>
<span data-ttu-id="d3053-191">application de hello toorun sur le cluster de hello, vous devez procéder comme suit de hello :</span><span class="sxs-lookup"><span data-stu-id="d3053-191">toorun hello application on hello cluster, you must do hello following:</span></span>

* <span data-ttu-id="d3053-192">**Copie hello application jar toohello stockage Azure d’objets blob** associé hello cluster.</span><span class="sxs-lookup"><span data-stu-id="d3053-192">**Copy hello application jar toohello Azure storage blob** associated with hello cluster.</span></span> <span data-ttu-id="d3053-193">Vous pouvez utiliser [ **AzCopy**](../storage/common/storage-use-azcopy.md), par conséquent, utilitaire, toodo une commande de ligne.</span><span class="sxs-lookup"><span data-stu-id="d3053-193">You can use [**AzCopy**](../storage/common/storage-use-azcopy.md), a command line utility, toodo so.</span></span> <span data-ttu-id="d3053-194">Il existe de nombreux autres clients ainsi que vous pouvez utiliser les données tooupload.</span><span class="sxs-lookup"><span data-stu-id="d3053-194">There are a lot of other clients as well that you can use tooupload data.</span></span> <span data-ttu-id="d3053-195">Pour en savoir plus à leur sujet, consultez [Téléchargement de données pour les travaux Hadoop dans HDInsight](hdinsight-upload-data.md).</span><span class="sxs-lookup"><span data-stu-id="d3053-195">You can find more about them at [Upload data for Hadoop jobs in HDInsight](hdinsight-upload-data.md).</span></span>
* <span data-ttu-id="d3053-196">**Utiliser Livy toosubmit un travail de l’application à distance** cluster Spark de toohello.</span><span class="sxs-lookup"><span data-stu-id="d3053-196">**Use Livy toosubmit an application job remotely** toohello Spark cluster.</span></span> <span data-ttu-id="d3053-197">Clusters Spark sur HDInsight inclut Livy qui expose des autres points de terminaison tooremotely envoyer des travaux de Spark.</span><span class="sxs-lookup"><span data-stu-id="d3053-197">Spark clusters on HDInsight includes Livy that exposes REST endpoints tooremotely submit Spark jobs.</span></span> <span data-ttu-id="d3053-198">Pour plus d’informations, consultez [Envoi de travaux Spark à distance en utilisant Livy avec les clusters Spark sur HDInsight](hdinsight-apache-spark-livy-rest-interface.md).</span><span class="sxs-lookup"><span data-stu-id="d3053-198">For more information, see [Submit Spark jobs remotely using Livy with Spark clusters on HDInsight](hdinsight-apache-spark-livy-rest-interface.md).</span></span>

## <a name="next-step"></a><span data-ttu-id="d3053-199">Étape suivante</span><span class="sxs-lookup"><span data-stu-id="d3053-199">Next step</span></span>

<span data-ttu-id="d3053-200">Dans cet article vous avez appris comment toocreate une application de scala Spark.</span><span class="sxs-lookup"><span data-stu-id="d3053-200">In this article you learned how toocreate a Spark scala application.</span></span> <span data-ttu-id="d3053-201">Avance toohello suivant l’article toolearn comment toorun cette application sur un HDInsight Spark de cluster à l’aide de Livy.</span><span class="sxs-lookup"><span data-stu-id="d3053-201">Advance toohello next article toolearn how toorun this application on an HDInsight Spark cluster using Livy.</span></span>

> [!div class="nextstepaction"]
>[<span data-ttu-id="d3053-202">Exécution de travaux à distance avec Livy sur un cluster Spark</span><span class="sxs-lookup"><span data-stu-id="d3053-202">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

