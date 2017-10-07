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
# <a name="use-azure-toolkit-for-intellij-toocreate-spark-applications-for-an-hdinsight-cluster"></a><span data-ttu-id="7c395-103">Utilisez la boîte à outils Azure pour les applications de Spark IntelliJ toocreate pour un cluster HDInsight</span><span class="sxs-lookup"><span data-stu-id="7c395-103">Use Azure Toolkit for IntelliJ toocreate Spark applications for an HDInsight cluster</span></span>

<span data-ttu-id="7c395-104">Utilisez hello boîte à outils Azure pour les applications de Spark toodevelop plug-in IntelliJ écrites dans Scala, puis les envoyer tooan cluster HDInsight Spark directement à partir de l’environnement de développement intégré IntelliJ hello (IDE).</span><span class="sxs-lookup"><span data-stu-id="7c395-104">Use hello Azure Toolkit for IntelliJ plug-in toodevelop Spark applications written in Scala, and then submit them tooan HDInsight Spark cluster directly from hello IntelliJ integrated development environment (IDE).</span></span> <span data-ttu-id="7c395-105">Vous pouvez utiliser hello plug-in de plusieurs façons :</span><span class="sxs-lookup"><span data-stu-id="7c395-105">You can use hello plug-in in a few ways:</span></span>

* <span data-ttu-id="7c395-106">Développer et soumettre une application Scala Spark sur un cluster HDInsight Spark.</span><span class="sxs-lookup"><span data-stu-id="7c395-106">Develop and submit a Scala Spark application on an HDInsight Spark cluster.</span></span>
* <span data-ttu-id="7c395-107">Accéder à vos ressources de cluster Azure HDInsight Spark.</span><span class="sxs-lookup"><span data-stu-id="7c395-107">Access your Azure HDInsight Spark cluster resources.</span></span>
* <span data-ttu-id="7c395-108">Développer et exécuter une application Scala Spark localement.</span><span class="sxs-lookup"><span data-stu-id="7c395-108">Develop and run a Scala Spark application locally.</span></span>

<span data-ttu-id="7c395-109">toocreate votre projet, le hello de vue [créer des Applications de Spark avec hello Azure Toolkit pour IntelliJ](https://channel9.msdn.com/Series/AzureDataLake/Create-Spark-Applications-with-the-Azure-Toolkit-for-IntelliJ) vidéo.</span><span class="sxs-lookup"><span data-stu-id="7c395-109">toocreate your project, view hello [Create Spark Applications with hello Azure Toolkit for IntelliJ](https://channel9.msdn.com/Series/AzureDataLake/Create-Spark-Applications-with-the-Azure-Toolkit-for-IntelliJ) video.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7c395-110">Vous pouvez utiliser ce plug-in toocreate et soumettre des applications uniquement pour un cluster HDInsight Spark sur Linux.</span><span class="sxs-lookup"><span data-stu-id="7c395-110">You can use this plug-in toocreate and submit applications only for an HDInsight Spark cluster on Linux.</span></span>
> 

## <a name="prerequisites"></a><span data-ttu-id="7c395-111">Composants requis</span><span class="sxs-lookup"><span data-stu-id="7c395-111">Prerequisites</span></span>

- <span data-ttu-id="7c395-112">Un cluster Apache Spark sur HDInsight Linux.</span><span class="sxs-lookup"><span data-stu-id="7c395-112">An Apache Spark cluster on HDInsight Linux.</span></span> <span data-ttu-id="7c395-113">Pour obtenir des instructions, consultez [Création de clusters Apache Spark dans Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="7c395-113">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>
- <span data-ttu-id="7c395-114">Kit de développement logiciel (SDK) Oracle Java.</span><span class="sxs-lookup"><span data-stu-id="7c395-114">Oracle Java Development Kit.</span></span> <span data-ttu-id="7c395-115">Vous pouvez l’installer à partir de hello [site Web d’Oracle](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).</span><span class="sxs-lookup"><span data-stu-id="7c395-115">You can install it from hello [Oracle website](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).</span></span>
- <span data-ttu-id="7c395-116">IntelliJ IDEA.</span><span class="sxs-lookup"><span data-stu-id="7c395-116">IntelliJ IDEA.</span></span> <span data-ttu-id="7c395-117">Cet article utilise la version 2017.1.</span><span class="sxs-lookup"><span data-stu-id="7c395-117">This article uses version 2017.1.</span></span> <span data-ttu-id="7c395-118">Vous pouvez l’installer à partir de hello [site Web de JetBrains](https://www.jetbrains.com/idea/download/).</span><span class="sxs-lookup"><span data-stu-id="7c395-118">You can install it from hello [JetBrains website](https://www.jetbrains.com/idea/download/).</span></span>

## <a name="install-azure-toolkit-for-intellij"></a><span data-ttu-id="7c395-119">Installer le kit de ressources Azure pour IntelliJ</span><span class="sxs-lookup"><span data-stu-id="7c395-119">Install Azure Toolkit for IntelliJ</span></span>
<span data-ttu-id="7c395-120">Pour plus d’informations, consultez [Installation du kit de ressources Azure pour IntelliJ](../azure-toolkit-for-intellij-installation.md).</span><span class="sxs-lookup"><span data-stu-id="7c395-120">For installation instructions, see [Install Azure Toolkit for IntelliJ](../azure-toolkit-for-intellij-installation.md).</span></span>

## <a name="sign-in-tooyour-azure-subscription"></a><span data-ttu-id="7c395-121">Se connecter tooyour abonnement Azure</span><span class="sxs-lookup"><span data-stu-id="7c395-121">Sign in tooyour Azure subscription</span></span>

1. <span data-ttu-id="7c395-122">Démarrez hello IntelliJ IDE et ouvrez l’Explorateur d’Azure.</span><span class="sxs-lookup"><span data-stu-id="7c395-122">Start hello IntelliJ IDE, and open Azure Explorer.</span></span> <span data-ttu-id="7c395-123">Sur hello **vue** menu, sélectionnez **fenêtres Outil**, puis sélectionnez **Explorateur Azure**.</span><span class="sxs-lookup"><span data-stu-id="7c395-123">On hello **View** menu, select **Tool Windows**, and then select **Azure Explorer**.</span></span>
       
   ![lien d’Explorateur Azure Hello](./media/hdinsight-apache-spark-intellij-tool-plugin/show-azure-explorer.png)

2. <span data-ttu-id="7c395-125">Avec le bouton hello **Azure** nœud et sélectionnez **connexion**.</span><span class="sxs-lookup"><span data-stu-id="7c395-125">Right-click hello **Azure** node, and then select **Sign In**.</span></span>

3. <span data-ttu-id="7c395-126">Bonjour **Azure Sign In** boîte de dialogue, sélectionnez **connecter**, puis entrez vos informations d’identification Azure.</span><span class="sxs-lookup"><span data-stu-id="7c395-126">In hello **Azure Sign In** dialog box, select **Sign in**, and then enter your Azure credentials.</span></span>

    ![Bonjour Azure boîte de dialogue Connexion](./media/hdinsight-apache-spark-intellij-tool-plugin/view-explorer-2.png)

4. <span data-ttu-id="7c395-128">Une fois que vous êtes connecté, hello **sélectionnez les abonnements** boîte de dialogue propose toutes hello abonnements Azure qui sont associées aux hello des informations d’identification.</span><span class="sxs-lookup"><span data-stu-id="7c395-128">After you're signed in, hello **Select Subscriptions** dialog box lists all hello Azure subscriptions that are associated with hello credentials.</span></span> <span data-ttu-id="7c395-129">Sélectionnez hello **sélectionnez** bouton.</span><span class="sxs-lookup"><span data-stu-id="7c395-129">Select hello **Select** button.</span></span>

    ![boîte de dialogue Sélectionnez les abonnements Hello](./media/hdinsight-apache-spark-intellij-tool-plugin/Select-Subscriptions.png)

5. <span data-ttu-id="7c395-131">Sur hello **Explorateur Azure** onglet, développez **HDInsight** hello tooview des clusters HDInsight Spark qui se trouvent dans votre abonnement.</span><span class="sxs-lookup"><span data-stu-id="7c395-131">On hello **Azure Explorer** tab, expand **HDInsight** tooview hello HDInsight Spark clusters that are in your subscription.</span></span>
   
    ![Clusters HDInsight Spark dans l’Explorateur Azure](./media/hdinsight-apache-spark-intellij-tool-plugin/view-explorer-3.png)

6. <span data-ttu-id="7c395-133">tooview hello ressources (par exemple, les comptes de stockage) qui sont associés au cluster de hello, vous pouvez développer davantage un nœud de nom de cluster.</span><span class="sxs-lookup"><span data-stu-id="7c395-133">tooview hello resources (for example, storage accounts) that are associated with hello cluster, you can further expand a cluster-name node.</span></span>
   
    ![Nœud de nom de cluster développé](./media/hdinsight-apache-spark-intellij-tool-plugin/view-explorer-4.png)

## <a name="run-a-spark-scala-application-on-an-hdinsight-spark-cluster"></a><span data-ttu-id="7c395-135">Exécuter une application Scala Spark sur un cluster HDInsight Spark</span><span class="sxs-lookup"><span data-stu-id="7c395-135">Run a Spark Scala application on an HDInsight Spark cluster</span></span>

1. <span data-ttu-id="7c395-136">Démarrez IntelliJ IDEA et créez un projet.</span><span class="sxs-lookup"><span data-stu-id="7c395-136">Start IntelliJ IDEA, and then create a project.</span></span> <span data-ttu-id="7c395-137">Bonjour **nouveau projet** boîte de dialogue zone, hello suivant :</span><span class="sxs-lookup"><span data-stu-id="7c395-137">In hello **New Project** dialog box, do hello following:</span></span> 

   <span data-ttu-id="7c395-138">a.</span><span class="sxs-lookup"><span data-stu-id="7c395-138">a.</span></span> <span data-ttu-id="7c395-139">Sélectionnez **HDInsight** > **Spark sur HDInsight (Scala)**.</span><span class="sxs-lookup"><span data-stu-id="7c395-139">Select **HDInsight** > **Spark on HDInsight (Scala)**.</span></span>

   <span data-ttu-id="7c395-140">b.</span><span class="sxs-lookup"><span data-stu-id="7c395-140">b.</span></span> <span data-ttu-id="7c395-141">Bonjour **outil de génération** , sélectionnez une des hello suivant, selon le besoin de tooyour :</span><span class="sxs-lookup"><span data-stu-id="7c395-141">In hello **Build tool** list, select either of hello following, according tooyour need:</span></span>

      * <span data-ttu-id="7c395-142">**Maven**, pour la prise en charge de l’Assistant de création de projets Scala</span><span class="sxs-lookup"><span data-stu-id="7c395-142">**Maven**, for Scala project-creation wizard support</span></span>
      * <span data-ttu-id="7c395-143">**SBT**, pour la gestion des dépendances de hello et la création de projet de Scala hello</span><span class="sxs-lookup"><span data-stu-id="7c395-143">**SBT**, for managing hello dependencies and building for hello Scala project</span></span>

    ![boîte de dialogue Nouveau projet Hello](./media/hdinsight-apache-spark-intellij-tool-plugin/create-hdi-scala-app.png)

2. <span data-ttu-id="7c395-145">Sélectionnez **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="7c395-145">Select **Next**.</span></span>

3. <span data-ttu-id="7c395-146">Assistant de création de projets Scala Hello détecte automatiquement si vous avez installé hello Scala plug-in.</span><span class="sxs-lookup"><span data-stu-id="7c395-146">hello Scala project-creation wizard automatically detects whether you've installed hello Scala plug-in.</span></span> <span data-ttu-id="7c395-147">Sélectionnez **Installer**.</span><span class="sxs-lookup"><span data-stu-id="7c395-147">Select **Install**.</span></span>

   ![Vérification de l’installation du plug-in Scala](./media/hdinsight-apache-spark-intellij-tool-plugin/Scala-Plugin-check-Reminder.PNG) 

4. <span data-ttu-id="7c395-149">hello de toodownload Scala plug-in, sélectionnez **OK**.</span><span class="sxs-lookup"><span data-stu-id="7c395-149">toodownload hello Scala plug-in, select **OK**.</span></span> <span data-ttu-id="7c395-150">Suivez les instructions de hello toorestart IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="7c395-150">Follow hello instructions toorestart IntelliJ.</span></span> 

   ![boîte de dialogue installation Hello Scala plug-in](./media/hdinsight-apache-spark-intellij-tool-plugin/Choose-Scala-Plugin.PNG)

5. <span data-ttu-id="7c395-152">Bonjour **nouveau projet** fenêtre, hello suivant :</span><span class="sxs-lookup"><span data-stu-id="7c395-152">In hello **New Project** window, do hello following:</span></span>  

    ![En sélectionnant hello Spark SDK](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-new-project.png)

   <span data-ttu-id="7c395-154">a.</span><span class="sxs-lookup"><span data-stu-id="7c395-154">a.</span></span> <span data-ttu-id="7c395-155">Entrez un nom de projet et un emplacement.</span><span class="sxs-lookup"><span data-stu-id="7c395-155">Enter a project name and location.</span></span>

   <span data-ttu-id="7c395-156">b.</span><span class="sxs-lookup"><span data-stu-id="7c395-156">b.</span></span> <span data-ttu-id="7c395-157">Bonjour **projet SDK** la liste déroulante, sélectionnez **Java 1.8** pour le cluster de hello Spark 2.x, ou sélectionnez **Java 1.7** pour le cluster de hello Spark 1.x.</span><span class="sxs-lookup"><span data-stu-id="7c395-157">In hello **Project SDK** drop-down list, select **Java 1.8** for hello Spark 2.x cluster, or select **Java 1.7** for hello Spark 1.x cluster.</span></span>

   <span data-ttu-id="7c395-158">c.</span><span class="sxs-lookup"><span data-stu-id="7c395-158">c.</span></span> <span data-ttu-id="7c395-159">Bonjour **version de Spark** la liste déroulante, Assistant de création de projet Scala intègre version correcte de hello pour le Kit de développement logiciel Spark et Scala SDK.</span><span class="sxs-lookup"><span data-stu-id="7c395-159">In hello **Spark version** drop-down list, Scala project creation wizard integrates hello proper version for Spark SDK and Scala SDK.</span></span> <span data-ttu-id="7c395-160">Si la version du cluster Spark hello est antérieure à la version 2.0, sélectionnez **nouvelles 1.x**.</span><span class="sxs-lookup"><span data-stu-id="7c395-160">If hello Spark cluster version is earlier than 2.0, select **Spark 1.x**.</span></span> <span data-ttu-id="7c395-161">Sinon, sélectionnez **Spark 2.x**.</span><span class="sxs-lookup"><span data-stu-id="7c395-161">Otherwise, select **Spark2.x**.</span></span> <span data-ttu-id="7c395-162">La version utilisée dans cet exemple est **Spark 2.0.2 (Scala 2.11.8)**.</span><span class="sxs-lookup"><span data-stu-id="7c395-162">This example uses **Spark 2.0.2 (Scala 2.11.8)**.</span></span>

6. <span data-ttu-id="7c395-163">Sélectionnez **Terminer**.</span><span class="sxs-lookup"><span data-stu-id="7c395-163">Select **Finish**.</span></span>

7. <span data-ttu-id="7c395-164">projet de Spark Hello crée automatiquement un artefact pour vous.</span><span class="sxs-lookup"><span data-stu-id="7c395-164">hello Spark project automatically creates an artifact for you.</span></span> <span data-ttu-id="7c395-165">artefact de hello tooview, hello suivant :</span><span class="sxs-lookup"><span data-stu-id="7c395-165">tooview hello artifact, do hello following:</span></span>

   <span data-ttu-id="7c395-166">a.</span><span class="sxs-lookup"><span data-stu-id="7c395-166">a.</span></span> <span data-ttu-id="7c395-167">Sur hello **fichier** menu, sélectionnez **Structure de projet**.</span><span class="sxs-lookup"><span data-stu-id="7c395-167">On hello **File** menu, select **Project Structure**.</span></span>

   <span data-ttu-id="7c395-168">b.</span><span class="sxs-lookup"><span data-stu-id="7c395-168">b.</span></span> <span data-ttu-id="7c395-169">Bonjour **Structure de projet** boîte de dialogue, sélectionnez **artefacts** tooview hello par défaut artefact qui est créé.</span><span class="sxs-lookup"><span data-stu-id="7c395-169">In hello **Project Structure** dialog box, select **Artifacts** tooview hello default artifact that is created.</span></span> <span data-ttu-id="7c395-170">Vous pouvez également créer vos propres artefact en sélectionnant le signe plus hello (**+**).</span><span class="sxs-lookup"><span data-stu-id="7c395-170">You can also create your own artifact by selecting hello plus sign (**+**).</span></span>

      ![Informations d’artefact dans la boîte de dialogue hello](./media/hdinsight-apache-spark-intellij-tool-plugin/default-artifact.png)
      
8. <span data-ttu-id="7c395-172">Ajoutez votre code source d’application de manière hello suivante :</span><span class="sxs-lookup"><span data-stu-id="7c395-172">Add your application source code by doing hello following:</span></span>

   <span data-ttu-id="7c395-173">a.</span><span class="sxs-lookup"><span data-stu-id="7c395-173">a.</span></span> <span data-ttu-id="7c395-174">Dans l’Explorateur de projets, cliquez sur **src**, pointez trop**nouveau**, puis sélectionnez **Scala classe**.</span><span class="sxs-lookup"><span data-stu-id="7c395-174">In Project Explorer, right-click **src**, point too**New**, and then select **Scala Class**.</span></span>
      
      ![Commandes pour la création d’une classe Scala à partir de l’Explorateur de projets](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-spark-scala-code.png)

   <span data-ttu-id="7c395-176">b.</span><span class="sxs-lookup"><span data-stu-id="7c395-176">b.</span></span> <span data-ttu-id="7c395-177">Bonjour **créer une nouvelle classe Scala** boîte de dialogue zone, fournissez un nom, sélectionnez **objet** Bonjour **type** zone, puis sélectionnez **OK**.</span><span class="sxs-lookup"><span data-stu-id="7c395-177">In hello **Create New Scala Class** dialog box, provide a name, select **Object** in hello **Kind** box, and then select **OK**.</span></span>
      
      ![Boîte de dialogue Créer une classe Scala](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-spark-scala-code-object.png)

   <span data-ttu-id="7c395-179">c.</span><span class="sxs-lookup"><span data-stu-id="7c395-179">c.</span></span> <span data-ttu-id="7c395-180">Bonjour **MyClusterApp.scala** file, collez hello suivant de code.</span><span class="sxs-lookup"><span data-stu-id="7c395-180">In hello **MyClusterApp.scala** file, paste hello following code.</span></span> <span data-ttu-id="7c395-181">Hello code lit les données de salutation HVAC.csv (disponible sur tous les clusters HDInsight Spark), récupère les lignes hello qui ont un seul chiffre dans la colonne de septième hello dans un fichier CSV hello et écrit la sortie de hello trop**/HVACOut** sous la valeur par défaut de hello conteneur de stockage pour le cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="7c395-181">hello code reads hello data from HVAC.csv (available on all HDInsight Spark clusters), retrieves hello rows that have only one digit in hello seventh column in hello CSV file, and writes hello output too**/HVACOut** under hello default storage container for hello cluster.</span></span>

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

9. <span data-ttu-id="7c395-182">Exécutez l’application hello sur un cluster HDInsight Spark en procédant comme suit de hello :</span><span class="sxs-lookup"><span data-stu-id="7c395-182">Run hello application on an HDInsight Spark cluster by doing hello following:</span></span>

   <span data-ttu-id="7c395-183">a.</span><span class="sxs-lookup"><span data-stu-id="7c395-183">a.</span></span> <span data-ttu-id="7c395-184">Dans l’Explorateur de projets, cliquez sur le nom de projet hello et sélectionnez **tooHDInsight de soumettre une Application de Spark**.</span><span class="sxs-lookup"><span data-stu-id="7c395-184">In Project Explorer, right-click hello project name, and then select **Submit Spark Application tooHDInsight**.</span></span>
      
      ![Hello commande tooHDInsight de soumettre une Application de Spark](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-submit-spark-app-1.png)

   <span data-ttu-id="7c395-186">b.</span><span class="sxs-lookup"><span data-stu-id="7c395-186">b.</span></span> <span data-ttu-id="7c395-187">Vous est demandée tooenter vos informations d’identification de l’abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="7c395-187">You are prompted tooenter your Azure subscription credentials.</span></span> <span data-ttu-id="7c395-188">Bonjour **Spark soumission** boîte de dialogue, fournissez hello valeurs suivantes, puis sélectionnez **Submit**.</span><span class="sxs-lookup"><span data-stu-id="7c395-188">In hello **Spark Submission** dialog box, provide hello following values, and then select **Submit**.</span></span>
      
      * <span data-ttu-id="7c395-189">Pour **au service de clusters (Linux uniquement)**, sélectionnez hello cluster HDInsight Spark sur lequel vous souhaitez toorun votre application.</span><span class="sxs-lookup"><span data-stu-id="7c395-189">For **Spark clusters (Linux only)**, select hello HDInsight Spark cluster on which you want toorun your application.</span></span>

      * <span data-ttu-id="7c395-190">Sélectionnez un artefact de projet de IntelliJ hello ou sélectionnez-en un dans le disque dur de hello.</span><span class="sxs-lookup"><span data-stu-id="7c395-190">Select an artifact from hello IntelliJ project, or select one from hello hard drive.</span></span>

      * <span data-ttu-id="7c395-191">Bonjour **nom de la classe principale** zone, les points de suspension hello select (**...** ), sélectionnez la classe principale hello dans votre code source d’application, puis sélectionnez **OK**.</span><span class="sxs-lookup"><span data-stu-id="7c395-191">In hello **Main class name** box, select hello ellipsis (**...**), select hello main class in your application source code, and then select **OK**.</span></span>

        ![boîte de dialogue de sélection de la classe principale Hello](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-submit-spark-app-3.png)

      * <span data-ttu-id="7c395-193">Car le code de l’application hello dans cet exemple ne pas nécessitent des arguments de ligne de commande ou référencer des fichiers ou des fichiers JAR, vous pouvez laisser hello restant zones vides.</span><span class="sxs-lookup"><span data-stu-id="7c395-193">Because hello application code in this example does not require command-line arguments or reference JARs or files, you can leave hello remaining boxes empty.</span></span> <span data-ttu-id="7c395-194">Après avoir fourni toutes les informations de hello, boîte de dialogue hello doit ressembler à hello suivant l’image.</span><span class="sxs-lookup"><span data-stu-id="7c395-194">After you provide all hello information, hello dialog box should resemble hello following image.</span></span>
        
        ![boîte de dialogue de soumission de Spark Hello](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-submit-spark-app-2.png)

   <span data-ttu-id="7c395-196">c.</span><span class="sxs-lookup"><span data-stu-id="7c395-196">c.</span></span> <span data-ttu-id="7c395-197">Hello **Spark soumission** onglet en bas de hello de fenêtre hello doit commencer à afficher la progression de hello.</span><span class="sxs-lookup"><span data-stu-id="7c395-197">hello **Spark Submission** tab at hello bottom of hello window should start displaying hello progress.</span></span> <span data-ttu-id="7c395-198">Vous pouvez également arrêter l’application hello en sélectionnant le bouton de hello rouge Bonjour **Spark soumission** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="7c395-198">You can also stop hello application by selecting hello red button in hello **Spark Submission** window.</span></span>
      
      ![fenêtre de soumission de Spark Hello](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-spark-app-result.png)
      
      <span data-ttu-id="7c395-200">toolearn tooaccess hello sortie des tâches, voir hello « accès et de gérer les clusters HDInsight Spark à l’aide de la boîte à outils Azure pour IntelliJ » plus loin dans cet article.</span><span class="sxs-lookup"><span data-stu-id="7c395-200">toolearn how tooaccess hello job output, see hello "Access and manage HDInsight Spark clusters by using Azure Toolkit for IntelliJ" section later in this article.</span></span>

## <a name="run-or-debug-a-spark-scala-application-on-an-hdinsight-spark-cluster"></a><span data-ttu-id="7c395-201">Exécuter ou déboguer comme une application Scala Spark sur un cluster HDInsight Spark</span><span class="sxs-lookup"><span data-stu-id="7c395-201">Run or debug a Spark Scala application on an HDInsight Spark cluster</span></span>
<span data-ttu-id="7c395-202">Nous recommandons également d’un autre moyen de l’envoi de cluster de toohello application hello Spark.</span><span class="sxs-lookup"><span data-stu-id="7c395-202">We also recommend another way of submitting hello Spark application toohello cluster.</span></span> <span data-ttu-id="7c395-203">Vous pouvez le faire en définissant des paramètres de hello Bonjour **configurations d’exécution/débogage** IDE.</span><span class="sxs-lookup"><span data-stu-id="7c395-203">You can do so by setting hello parameters in hello **Run/Debug configurations** IDE.</span></span> <span data-ttu-id="7c395-204">Pour obtenir des instructions, reportez-vous à la rubrique [Déboguer des applications Spark à distance sur un cluster HDInsight avec le kit de ressources Azure pour IntelliJ via SSH](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-apache-spark-intellij-tool-debug-remotely-through-ssh).</span><span class="sxs-lookup"><span data-stu-id="7c395-204">For more information, see [Remotely debug Spark applications on an HDInsight cluster with Azure Toolkit for IntelliJ through SSH](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-apache-spark-intellij-tool-debug-remotely-through-ssh).</span></span>

## <a name="access-and-manage-hdinsight-spark-clusters-by-using-azure-toolkit-for-intellij"></a><span data-ttu-id="7c395-205">Accéder aux clusters HDInsight Spark et les gérer à l’aide du kit de ressources Azure pour IntelliJ</span><span class="sxs-lookup"><span data-stu-id="7c395-205">Access and manage HDInsight Spark clusters by using Azure Toolkit for IntelliJ</span></span>
<span data-ttu-id="7c395-206">Vous pouvez effectuer diverses opérations à l’aide du kit de ressources Azure pour IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="7c395-206">You can perform various operations by using Azure Toolkit for IntelliJ.</span></span>

### <a name="access-hello-job-view"></a><span data-ttu-id="7c395-207">Affichage des travaux hello Access</span><span class="sxs-lookup"><span data-stu-id="7c395-207">Access hello job view</span></span>
1. <span data-ttu-id="7c395-208">Dans l’Explorateur d’Azure, développez **HDInsight**, développez le nom du cluster Spark hello, puis sélectionnez **travaux**.</span><span class="sxs-lookup"><span data-stu-id="7c395-208">In Azure Explorer, expand **HDInsight**, expand hello Spark cluster name, and then select **Jobs**.</span></span>  

    ![Nœud Vue de la tâche](./media/hdinsight-apache-spark-intellij-tool-plugin/job-view-node.png)

2. <span data-ttu-id="7c395-210">Dans le volet droit de hello, hello **Spark travail vue** onglet affiche toutes les applications hello qui ont été exécutées sur le cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="7c395-210">In hello right pane, hello **Spark Job View** tab displays all hello applications that were run on hello cluster.</span></span> <span data-ttu-id="7c395-211">Sélectionnez le nom hello d’application hello pour lequel vous souhaitez toosee plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="7c395-211">Select hello name of hello application for which you want toosee more details.</span></span>

    ![Détails de l’application](./media/hdinsight-apache-spark-intellij-tool-plugin/view-job-logs.png)

3. <span data-ttu-id="7c395-213">toodisplay en cours d’exécution travail informations de base, pointez sur le graphique de travail hello.</span><span class="sxs-lookup"><span data-stu-id="7c395-213">toodisplay basic running job information, hover over hello job graph.</span></span> <span data-ttu-id="7c395-214">graphique de phases tooview hello et informations que chaque tâche génère, sélectionnez un nœud sur le graphique de travail hello.</span><span class="sxs-lookup"><span data-stu-id="7c395-214">tooview hello stages graph and information that every job generates, select a node on hello job graph.</span></span>

    ![Détails des étapes du travail](./media/hdinsight-apache-spark-intellij-tool-plugin/Job-graph-stage-info.png)

4. <span data-ttu-id="7c395-216">tooview utilisé fréquemment les journaux, tels que *pilote Stderr*, *pilote Stdout*, et *des informations de répertoire*, sélectionnez hello **journal** onglet.</span><span class="sxs-lookup"><span data-stu-id="7c395-216">tooview frequently used logs, such as *Driver Stderr*, *Driver Stdout*, and *Directory Info*, select hello **Log** tab.</span></span>

    ![Détails des journaux](./media/hdinsight-apache-spark-intellij-tool-plugin/Job-log-info.png)

5. <span data-ttu-id="7c395-218">Vous pouvez également afficher hello historique de Spark UI et hello UI fils (au niveau de l’application hello) en sélectionnant un lien en haut de hello de fenêtre hello.</span><span class="sxs-lookup"><span data-stu-id="7c395-218">You can also view hello Spark history UI and hello YARN UI (at hello application level) by selecting a link at hello top of hello window.</span></span>

### <a name="access-hello-spark-history-server"></a><span data-ttu-id="7c395-219">Serveur d’accès hello Spark historique</span><span class="sxs-lookup"><span data-stu-id="7c395-219">Access hello Spark history server</span></span>
1. <span data-ttu-id="7c395-220">Dans Azure Explorer, développez **HDInsight**, cliquez avec le bouton droit sur le nom de votre cluster Spark et sélectionnez **Open Spark History UI** (Ouvrir l’interface utilisateur de l’historique Spark).</span><span class="sxs-lookup"><span data-stu-id="7c395-220">In Azure Explorer, expand **HDInsight**, right-click your Spark cluster name, and then select **Open Spark History UI**.</span></span> 

2. <span data-ttu-id="7c395-221">Lorsque vous y êtes invité, entrez les informations d’identification administrateur du cluster hello que vous avez spécifié lorsque vous configurez le cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="7c395-221">When you're prompted, enter hello cluster's admin credentials, which you specified when you set up hello cluster.</span></span>

3. <span data-ttu-id="7c395-222">Tableau de bord de serveur hello Spark historique, vous pouvez utiliser toolook de nom d’application hello pour application hello que vous venez d’en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="7c395-222">On hello Spark history server dashboard, you can use hello application name toolook for hello application that you just finished running.</span></span> <span data-ttu-id="7c395-223">Bonjour précédant le code, vous définir le nom de l’application hello en utilisant `val conf = new SparkConf().setAppName("MyClusterApp")`.</span><span class="sxs-lookup"><span data-stu-id="7c395-223">In hello preceding code, you set hello application name by using `val conf = new SparkConf().setAppName("MyClusterApp")`.</span></span> <span data-ttu-id="7c395-224">Par conséquent, le nom de votre application Spark est **MyClusterApp**.</span><span class="sxs-lookup"><span data-stu-id="7c395-224">Therefore, your Spark application name is **MyClusterApp**.</span></span>

### <a name="start-hello-ambari-portal"></a><span data-ttu-id="7c395-225">Démarrer le portail de Ambari hello</span><span class="sxs-lookup"><span data-stu-id="7c395-225">Start hello Ambari portal</span></span>
1. <span data-ttu-id="7c395-226">Dans Azure Explorer, développez **HDInsight**, cliquez avec le bouton droit sur le nom de votre cluster Spark et sélectionnez **Open Cluster Management Portal (Ambari)** (Ouvrir le portail de gestion des clusters (Ambari)).</span><span class="sxs-lookup"><span data-stu-id="7c395-226">In Azure Explorer, expand **HDInsight**, right-click your Spark cluster name, and then select **Open Cluster Management Portal (Ambari)**.</span></span> 

2. <span data-ttu-id="7c395-227">Lorsque vous y êtes invité, entrez les informations d’identification du admin de hello pour le cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="7c395-227">When you're prompted, enter hello admin credentials for hello cluster.</span></span> <span data-ttu-id="7c395-228">Vous avez spécifié ces informations d’identification au cours du processus d’installation de cluster hello.</span><span class="sxs-lookup"><span data-stu-id="7c395-228">You specified these credentials during hello cluster setup process.</span></span>

### <a name="manage-azure-subscriptions"></a><span data-ttu-id="7c395-229">Gérer les abonnements Azure</span><span class="sxs-lookup"><span data-stu-id="7c395-229">Manage Azure subscriptions</span></span>
<span data-ttu-id="7c395-230">Par défaut, Azure Toolkit pour IntelliJ répertorie les clusters de Spark hello à partir de tous vos abonnements Azure.</span><span class="sxs-lookup"><span data-stu-id="7c395-230">By default, Azure Toolkit for IntelliJ lists hello Spark clusters from all your Azure subscriptions.</span></span> <span data-ttu-id="7c395-231">Si nécessaire, vous pouvez spécifier des abonnements hello que vous souhaitez tooaccess.</span><span class="sxs-lookup"><span data-stu-id="7c395-231">If necessary, you can specify hello subscriptions that you want tooaccess.</span></span> 

1. <span data-ttu-id="7c395-232">Dans l’Explorateur d’Azure, avec le bouton droit hello **Azure** nœud racine, puis sélectionnez **gérer les abonnements**.</span><span class="sxs-lookup"><span data-stu-id="7c395-232">In Azure Explorer, right-click hello **Azure** root node, and then select **Manage Subscriptions**.</span></span> 

2. <span data-ttu-id="7c395-233">Dans la boîte de dialogue hello, désactivez hello cases à cocher suivants toohello abonnements que vous ne souhaitez tooaccess, puis sélectionnez **fermer**.</span><span class="sxs-lookup"><span data-stu-id="7c395-233">In hello dialog box, clear hello check boxes next toohello subscriptions that you don't want tooaccess, and then select **Close**.</span></span> <span data-ttu-id="7c395-234">Vous pouvez également sélectionner **se déconnecter** si vous souhaitez toosign dans votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="7c395-234">You can also select **Sign Out** if you want toosign out of your Azure subscription.</span></span>

## <a name="run-a-spark-scala-application-locally"></a><span data-ttu-id="7c395-235">Exécuter une application Spark Scala localement</span><span class="sxs-lookup"><span data-stu-id="7c395-235">Run a Spark Scala application locally</span></span>
<span data-ttu-id="7c395-236">Vous pouvez utiliser boîte à outils Azure pour les applications de Spark Scala IntelliJ toorun localement sur votre station de travail.</span><span class="sxs-lookup"><span data-stu-id="7c395-236">You can use Azure Toolkit for IntelliJ toorun Spark Scala applications locally on your workstation.</span></span> <span data-ttu-id="7c395-237">Hello applications généralement ne doivent accéder à des ressources de toocluster, telles que les conteneurs de stockage, et vous pouvez exécuter et tester localement.</span><span class="sxs-lookup"><span data-stu-id="7c395-237">hello applications usually don't need access toocluster resources, such as storage containers, and you can run and test them locally.</span></span>

### <a name="prerequisite"></a><span data-ttu-id="7c395-238">Configuration requise</span><span class="sxs-lookup"><span data-stu-id="7c395-238">Prerequisite</span></span>
<span data-ttu-id="7c395-239">Lorsque vous exécutez l’application hello locale Spark Scala sur un ordinateur Windows, vous pouvez obtenir une exception, comme expliqué dans [SPARK-2356](https://issues.apache.org/jira/browse/SPARK-2356).</span><span class="sxs-lookup"><span data-stu-id="7c395-239">While you're running hello local Spark Scala application on a Windows computer, you might get an exception, as explained in [SPARK-2356](https://issues.apache.org/jira/browse/SPARK-2356).</span></span> <span data-ttu-id="7c395-240">exception de Hello se produit parce que WinUtils.exe est manquant sur Windows.</span><span class="sxs-lookup"><span data-stu-id="7c395-240">hello exception occurs because WinUtils.exe is missing on Windows.</span></span> 

<span data-ttu-id="7c395-241">tooresolve cette erreur, [télécharger hello exécutable](http://public-repo-1.hortonworks.com/hdp-win-alpha/winutils.exe) emplacement tooa comme **C:\WinUtils\bin**.</span><span class="sxs-lookup"><span data-stu-id="7c395-241">tooresolve this error, [download hello executable](http://public-repo-1.hortonworks.com/hdp-win-alpha/winutils.exe) tooa location such as **C:\WinUtils\bin**.</span></span> <span data-ttu-id="7c395-242">Ensuite, ajoutez la variable d’environnement hello **HADOOP_HOME**et la valeur hello de variable de hello trop**C\WinUtils**.</span><span class="sxs-lookup"><span data-stu-id="7c395-242">Then, add hello environment variable **HADOOP_HOME**, and set hello value of hello variable too**C\WinUtils**.</span></span>

### <a name="run-a-local-spark-scala-application"></a><span data-ttu-id="7c395-243">Exécuter une application Spark Scala locale</span><span class="sxs-lookup"><span data-stu-id="7c395-243">Run a local Spark Scala application</span></span>
1. <span data-ttu-id="7c395-244">Démarrez IntelliJ IDEA et créez un projet.</span><span class="sxs-lookup"><span data-stu-id="7c395-244">Start IntelliJ IDEA, and create a project.</span></span> 

2. <span data-ttu-id="7c395-245">Bonjour **nouveau projet** boîte de dialogue zone, hello suivant :</span><span class="sxs-lookup"><span data-stu-id="7c395-245">In hello **New Project** dialog box, do hello following:</span></span>
   
    <span data-ttu-id="7c395-246">a.</span><span class="sxs-lookup"><span data-stu-id="7c395-246">a.</span></span> <span data-ttu-id="7c395-247">Sélectionnez **HDInsight** > **Spark on HDInsight Local Run Sample (Scala)** (Exemple d’exécution locale de Spark sur HDInsight [Scala]).</span><span class="sxs-lookup"><span data-stu-id="7c395-247">Select **HDInsight** > **Spark on HDInsight Local Run Sample (Scala)**.</span></span>

    <span data-ttu-id="7c395-248">b.</span><span class="sxs-lookup"><span data-stu-id="7c395-248">b.</span></span> <span data-ttu-id="7c395-249">Bonjour **outil de génération** , sélectionnez une des hello suivant, selon le besoin de tooyour :</span><span class="sxs-lookup"><span data-stu-id="7c395-249">In hello **Build tool** list, select either of hello following, according tooyour need:</span></span>

      * <span data-ttu-id="7c395-250">**Maven**, pour la prise en charge de l’Assistant de création de projets Scala</span><span class="sxs-lookup"><span data-stu-id="7c395-250">**Maven**, for Scala project-creation wizard support</span></span>
      * <span data-ttu-id="7c395-251">**SBT**, pour la gestion des dépendances de hello et la création de projet de Scala hello</span><span class="sxs-lookup"><span data-stu-id="7c395-251">**SBT**, for managing hello dependencies and building for hello Scala project</span></span>

    ![boîte de dialogue Nouveau projet Hello](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-spark-app-local-run.png)

3. <span data-ttu-id="7c395-253">Sélectionnez **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="7c395-253">Select **Next**.</span></span>
 
4. <span data-ttu-id="7c395-254">Dans la fenêtre suivante de hello, procédez comme hello suivant :</span><span class="sxs-lookup"><span data-stu-id="7c395-254">In hello next window, do hello following:</span></span>
   
    <span data-ttu-id="7c395-255">a.</span><span class="sxs-lookup"><span data-stu-id="7c395-255">a.</span></span> <span data-ttu-id="7c395-256">Entrez un nom de projet et un emplacement.</span><span class="sxs-lookup"><span data-stu-id="7c395-256">Enter a project name and location.</span></span>

    <span data-ttu-id="7c395-257">b.</span><span class="sxs-lookup"><span data-stu-id="7c395-257">b.</span></span> <span data-ttu-id="7c395-258">Bonjour **projet SDK** liste déroulante, sélectionnez une version de Java est postérieure à la version 1.7.</span><span class="sxs-lookup"><span data-stu-id="7c395-258">In hello **Project SDK** drop-down list, select a Java version that's later than version 1.7.</span></span>

    <span data-ttu-id="7c395-259">c.</span><span class="sxs-lookup"><span data-stu-id="7c395-259">c.</span></span> <span data-ttu-id="7c395-260">Bonjour **Spark Version** liste déroulante, sélectionnez hello version de Scala que toouse : Scala 2.11.x pour Spark 2.0 ou Scala 2.10.x pour Spark 1.6.</span><span class="sxs-lookup"><span data-stu-id="7c395-260">In hello **Spark Version** drop-down list, select hello version of Scala that you want toouse: Scala 2.11.x for Spark 2.0 or Scala 2.10.x for Spark 1.6.</span></span>

    ![boîte de dialogue Nouveau projet Hello](./media/hdinsight-apache-spark-intellij-tool-plugin/Create-local-project.PNG)

5. <span data-ttu-id="7c395-262">Sélectionnez **Terminer**.</span><span class="sxs-lookup"><span data-stu-id="7c395-262">Select **Finish**.</span></span>

6. <span data-ttu-id="7c395-263">modèle de Hello ajoute un exemple de code (**LogQuery**) sous hello **src** dossier que vous pouvez exécuter localement sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="7c395-263">hello template adds a sample code (**LogQuery**) under hello **src** folder that you can run locally on your computer.</span></span>
   
    ![Emplacement de LogQuery](./media/hdinsight-apache-spark-intellij-tool-plugin/local-app.png)

7. <span data-ttu-id="7c395-265">Avec le bouton hello **LogQuery** application et sélectionnez **exécuter 'LogQuery'**.</span><span class="sxs-lookup"><span data-stu-id="7c395-265">Right-click hello **LogQuery** application, and then select **Run 'LogQuery'**.</span></span> <span data-ttu-id="7c395-266">Sur hello **exécuter** onglet en bas de hello, vous voyez une sortie semblable à hello suivante :</span><span class="sxs-lookup"><span data-stu-id="7c395-266">On hello **Run** tab at hello bottom, you see an output like hello following:</span></span>
   
   ![Résultat de l’exécution locale de l’application Spark](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-spark-app-local-run-result.png)

## <a name="convert-existing-intellij-idea-applications-toouse-azure-toolkit-for-intellij"></a><span data-ttu-id="7c395-268">Convertir toouse d’applications existant IntelliJ idée boîte à outils Azure pour IntelliJ</span><span class="sxs-lookup"><span data-stu-id="7c395-268">Convert existing IntelliJ IDEA applications toouse Azure Toolkit for IntelliJ</span></span>
<span data-ttu-id="7c395-269">Vous pouvez convertir hello Spark Scala les applications existantes que vous avez créé dans l’idée de IntelliJ toobe compatible avec la boîte à outils Azure pour IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="7c395-269">You can convert hello existing Spark Scala applications that you created in IntelliJ IDEA toobe compatible with Azure Toolkit for IntelliJ.</span></span> <span data-ttu-id="7c395-270">Vous pouvez ensuite utiliser hello toosubmit plug-in hello applications tooan cluster HDInsight Spark.</span><span class="sxs-lookup"><span data-stu-id="7c395-270">You can then use hello plug-in toosubmit hello applications tooan HDInsight Spark cluster.</span></span>

1. <span data-ttu-id="7c395-271">Pour une application Spark Scala existante qui a été créée via IntelliJ idée, ouvrez le fichier de .iml associé de hello.</span><span class="sxs-lookup"><span data-stu-id="7c395-271">For an existing Spark Scala application that was created through IntelliJ IDEA, open hello associated .iml file.</span></span>

2. <span data-ttu-id="7c395-272">À la racine de hello niveau est un **module** élément hello suivante :</span><span class="sxs-lookup"><span data-stu-id="7c395-272">At hello root level is a **module** element like hello following:</span></span>
   
        <module org.jetbrains.idea.maven.project.MavenProjectsManager.isMavenModule="true" type="JAVA_MODULE" version="4">

   <span data-ttu-id="7c395-273">Modifier hello élément tooadd `UniqueKey="HDInsightTool"` ainsi que hello **module** élément ressemble à hello suivantes :</span><span class="sxs-lookup"><span data-stu-id="7c395-273">Edit hello element tooadd `UniqueKey="HDInsightTool"` so that hello **module** element looks like hello following:</span></span>
   
        <module org.jetbrains.idea.maven.project.MavenProjectsManager.isMavenModule="true" type="JAVA_MODULE" version="4" UniqueKey="HDInsightTool">

3. <span data-ttu-id="7c395-274">Enregistrer les modifications de hello.</span><span class="sxs-lookup"><span data-stu-id="7c395-274">Save hello changes.</span></span> <span data-ttu-id="7c395-275">Votre application doit maintenant être compatible avec le kit de ressources Azure pour IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="7c395-275">Your application should now be compatible with Azure Toolkit for IntelliJ.</span></span> <span data-ttu-id="7c395-276">Vous pouvez le tester en double-cliquant sur le nom du projet hello dans l’Explorateur de projets.</span><span class="sxs-lookup"><span data-stu-id="7c395-276">You can test it by right-clicking hello project name in Project Explorer.</span></span> <span data-ttu-id="7c395-277">menu contextuel de Hello a maintenant l’option de hello **tooHDInsight de soumettre une Application de Spark**.</span><span class="sxs-lookup"><span data-stu-id="7c395-277">hello pop-up menu now has hello option **Submit Spark Application tooHDInsight**.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="7c395-278">Résolution des problèmes</span><span class="sxs-lookup"><span data-stu-id="7c395-278">Troubleshooting</span></span>

### <a name="error-in-local-run-please-use-a-larger-heap-size"></a><span data-ttu-id="7c395-279">Erreur dans l’exécution locale : *Please use a larger heap size* (Veuillez utiliser un tas de plus grande taille)</span><span class="sxs-lookup"><span data-stu-id="7c395-279">Error in local run: *Please use a larger heap size*</span></span>
<span data-ttu-id="7c395-280">Dans la version 1.6 Spark, si vous utilisez un kit de développement Java 32 bits pendant l’exécution locale, vous pouvez rencontrer hello les erreurs suivantes :</span><span class="sxs-lookup"><span data-stu-id="7c395-280">In Spark 1.6, if you're using a 32-bit Java SDK during local run, you might encounter hello following errors:</span></span>

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

<span data-ttu-id="7c395-281">Ces erreurs se produisent, car la taille du tas de hello n’est pas assez grande pour Spark toorun.</span><span class="sxs-lookup"><span data-stu-id="7c395-281">These errors happen because hello heap size is not large enough for Spark toorun.</span></span> <span data-ttu-id="7c395-282">Spark nécessite au moins 471 Mo.</span><span class="sxs-lookup"><span data-stu-id="7c395-282">Spark requires at least 471 MB.</span></span> <span data-ttu-id="7c395-283">(Pour plus d’informations, voir [SPARK-12081](https://issues.apache.org/jira/browse/SPARK-12081).) Une solution simple est toouse un kit de développement Java 64 bits.</span><span class="sxs-lookup"><span data-stu-id="7c395-283">(For more information, see [SPARK-12081](https://issues.apache.org/jira/browse/SPARK-12081).) One simple solution is toouse a 64-bit Java SDK.</span></span> <span data-ttu-id="7c395-284">Vous pouvez également modifier les paramètres de JVM hello dans IntelliJ en ajoutant hello options suivantes :</span><span class="sxs-lookup"><span data-stu-id="7c395-284">You can also change hello JVM settings in IntelliJ by adding hello following options:</span></span>

    -Xms128m -Xmx512m -XX:MaxPermSize=300m -ea

![Ajout d’options toohello « Options de la machine virtuelle » zone IntelliJ](./media/hdinsight-apache-spark-intellij-tool-plugin/change-heap-size.png)

## <a name="faq"></a><span data-ttu-id="7c395-286">Forum Aux Questions</span><span class="sxs-lookup"><span data-stu-id="7c395-286">FAQ</span></span>
<span data-ttu-id="7c395-287">toosubmit application tooAzure Data Lake Store, choisissez **Interactive** mode pendant le processus de hello signe dans Azure.</span><span class="sxs-lookup"><span data-stu-id="7c395-287">toosubmit an application tooAzure Data Lake Store, choose **Interactive** mode during hello Azure sign-in process.</span></span> <span data-ttu-id="7c395-288">Si vous sélectionnez le mode **automatique**, vous pouvez obtenir une erreur.</span><span class="sxs-lookup"><span data-stu-id="7c395-288">If you select **Automated** mode, you can get an error.</span></span>

![Connexion interactive](./media/hdinsight-apache-spark-intellij-tool-plugin/interative-signin.png)

<span data-ttu-id="7c395-290">À présent, nous l’avons résolue.</span><span class="sxs-lookup"><span data-stu-id="7c395-290">Now, we resolved it.</span></span> <span data-ttu-id="7c395-291">Vous pouvez choisir un toosubmit Cluster lac de données Azure à votre application avec n’importe quelle méthode de connexion.</span><span class="sxs-lookup"><span data-stu-id="7c395-291">You can choose an Azure Data Lake Cluster toosubmit your application with any sign-in method.</span></span>

## <a name="feedback-and-known-issues"></a><span data-ttu-id="7c395-292">Commentaires et problèmes connus</span><span class="sxs-lookup"><span data-stu-id="7c395-292">Feedback and known issues</span></span>
<span data-ttu-id="7c395-293">Pour l’instant, la visualisation directe des sorties Spark n’est pas prise en charge.</span><span class="sxs-lookup"><span data-stu-id="7c395-293">Currently, viewing Spark outputs directly is not supported.</span></span>

<span data-ttu-id="7c395-294">Si vous avez des suggestions ou des commentaires, ou que vous rencontrez des problèmes lors de l’utilisation de ce plug-in, envoyez-nous un e-mail à l’adresse hdivstool@microsoft.com.</span><span class="sxs-lookup"><span data-stu-id="7c395-294">If you have any suggestions or feedback, or if you encounter any problems when you use this plug-in, email us at hdivstool@microsoft.com.</span></span>

## <span data-ttu-id="7c395-295"><a name="seealso"></a>Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="7c395-295"><a name="seealso"></a>Next steps</span></span>
* [<span data-ttu-id="7c395-296">Vue d’ensemble : Apache Spark sur Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="7c395-296">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="demo"></a><span data-ttu-id="7c395-297">Démonstration</span><span class="sxs-lookup"><span data-stu-id="7c395-297">Demo</span></span>
* <span data-ttu-id="7c395-298">Créez un projet Scala (vidéo) : [Créer des applications Scala Spark](https://channel9.msdn.com/Series/AzureDataLake/Create-Spark-Applications-with-the-Azure-Toolkit-for-IntelliJ)</span><span class="sxs-lookup"><span data-stu-id="7c395-298">Create Scala project (video): [Create Spark Scala Applications](https://channel9.msdn.com/Series/AzureDataLake/Create-Spark-Applications-with-the-Azure-Toolkit-for-IntelliJ)</span></span>
* <span data-ttu-id="7c395-299">Débogage distant (vidéo) : [utilisation Azure Toolkit pour les applications de Spark IntelliJ toodebug à distance sur un HDInsight Cluster](https://channel9.msdn.com/Series/AzureDataLake/Debug-HDInsight-Spark-Applications-with-Azure-Toolkit-for-IntelliJ)</span><span class="sxs-lookup"><span data-stu-id="7c395-299">Remote debug (video): [Use Azure Toolkit for IntelliJ toodebug Spark applications remotely on HDInsight Cluster](https://channel9.msdn.com/Series/AzureDataLake/Debug-HDInsight-Spark-Applications-with-Azure-Toolkit-for-IntelliJ)</span></span>

### <a name="scenarios"></a><span data-ttu-id="7c395-300">Scénarios</span><span class="sxs-lookup"><span data-stu-id="7c395-300">Scenarios</span></span>
* [<span data-ttu-id="7c395-301">Spark avec BI : effectuez une analyse interactive des données à l’aide de Spark dans HDInsight avec des outils BI</span><span class="sxs-lookup"><span data-stu-id="7c395-301">Spark with BI: Perform interactive data analysis by using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="7c395-302">Spark avec Machine Learning : Spark utilisation dans tooanalyze HDInsight à l’aide des données HVAC de température de génération</span><span class="sxs-lookup"><span data-stu-id="7c395-302">Spark with Machine Learning: Use Spark in HDInsight tooanalyze building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="7c395-303">Spark avec Machine Learning : Spark utilisation dans résultats de l’inspection alimentaires toopredict HDInsight</span><span class="sxs-lookup"><span data-stu-id="7c395-303">Spark with Machine Learning: Use Spark in HDInsight toopredict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="7c395-304">Diffusion en continu de Spark : Spark utilisation dans les applications de diffusion en continu en temps réel toobuild HDInsight</span><span class="sxs-lookup"><span data-stu-id="7c395-304">Spark Streaming: Use Spark in HDInsight toobuild real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)
* [<span data-ttu-id="7c395-305">Analyse des journaux de site web à l’aide de Spark dans HDInsight</span><span class="sxs-lookup"><span data-stu-id="7c395-305">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="creating-and-running-applications"></a><span data-ttu-id="7c395-306">Création et exécution d’applications</span><span class="sxs-lookup"><span data-stu-id="7c395-306">Creating and running applications</span></span>
* [<span data-ttu-id="7c395-307">Créer une application autonome avec Scala</span><span class="sxs-lookup"><span data-stu-id="7c395-307">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="7c395-308">Exécuter des tâches à distance avec Livy sur un cluster Spark</span><span class="sxs-lookup"><span data-stu-id="7c395-308">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="7c395-309">Outils et extensions</span><span class="sxs-lookup"><span data-stu-id="7c395-309">Tools and extensions</span></span>
* [<span data-ttu-id="7c395-310">Utilisez la boîte à outils Azure pour les applications de Spark IntelliJ toodebug à distance via le VPN</span><span class="sxs-lookup"><span data-stu-id="7c395-310">Use Azure Toolkit for IntelliJ toodebug Spark applications remotely through VPN</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="7c395-311">Utilisez la boîte à outils Azure pour les applications de Spark IntelliJ toodebug à distance via SSH</span><span class="sxs-lookup"><span data-stu-id="7c395-311">Use Azure Toolkit for IntelliJ toodebug Spark applications remotely through SSH</span></span>](hdinsight-apache-spark-intellij-tool-debug-remotely-through-ssh.md)
* [<span data-ttu-id="7c395-312">Utiliser HDInsight Tools pour IntelliJ avec Hortonworks Sandbox</span><span class="sxs-lookup"><span data-stu-id="7c395-312">Use HDInsight Tools for IntelliJ with Hortonworks Sandbox</span></span>](hdinsight-tools-for-intellij-with-hortonworks-sandbox.md)
* [<span data-ttu-id="7c395-313">Utilisez les outils HDInsight dans la boîte à outils Azure pour les applications de Spark toocreate Eclipse</span><span class="sxs-lookup"><span data-stu-id="7c395-313">Use HDInsight Tools in Azure Toolkit for Eclipse toocreate Spark applications</span></span>](hdinsight-apache-spark-eclipse-tool-plugin.md)
* [<span data-ttu-id="7c395-314">Utiliser des bloc-notes Zeppelin avec un cluster Spark sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="7c395-314">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="7c395-315">Noyaux disponibles pour le bloc-notes Jupyter dans un cluster Spark pour HDInsight</span><span class="sxs-lookup"><span data-stu-id="7c395-315">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="7c395-316">Utiliser des packages externes avec les blocs-notes Jupyter</span><span class="sxs-lookup"><span data-stu-id="7c395-316">Use external packages with Jupyter notebooks</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="7c395-317">Installer Notebook sur votre ordinateur et vous connecter tooan cluster HDInsight Spark</span><span class="sxs-lookup"><span data-stu-id="7c395-317">Install Jupyter on your computer and connect tooan HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="managing-resources"></a><span data-ttu-id="7c395-318">Gestion des ressources</span><span class="sxs-lookup"><span data-stu-id="7c395-318">Managing resources</span></span>
* [<span data-ttu-id="7c395-319">Gérer les ressources de cluster d’Apache Spark hello dans Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="7c395-319">Manage resources for hello Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="7c395-320">Track and debug jobs running on an Apache Spark cluster in HDInsight (Suivi et débogage des tâches en cours d’exécution sur un cluster Apache Spark dans HDInsight)</span><span class="sxs-lookup"><span data-stu-id="7c395-320">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)

