---
title: Utiliser le Kit de ressources Azure pour IntelliJ avec Hortonworks Sandbox | Microsoft Docs
description: "Découvrez comment utiliser HDInsight Tools dans le Kit de ressources Azure pour IntelliJ avec Hortonworks Sandbox."
keywords: "outils Hadoop, requête hive, intellij, hortonworks sandbox, kit de ressources azure pour intellij"
services: HDInsight
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: b587cc9b-a41a-49ac-998f-b54d6c0bdfe0
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/25/2017
ms.author: jgao
ms.openlocfilehash: c49f185db5a035f70a711bf309b973182d94a2b0
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="use-hdinsight-tools-for-intellij-with-hortonworks-sandbox"></a><span data-ttu-id="4b18a-104">Utiliser HDInsight Tools pour IntelliJ avec Hortonworks Sandbox</span><span class="sxs-lookup"><span data-stu-id="4b18a-104">Use HDInsight Tools for IntelliJ with Hortonworks Sandbox</span></span>

<span data-ttu-id="4b18a-105">Découvrez comment utiliser HDInsight Tools pour IntelliJ pour développer des applications Apache Scala et tester les applications sur [Hortonworks Sandbox](http://hortonworks.com/products/sandbox/) en cours d’exécution sur votre station de travail.</span><span class="sxs-lookup"><span data-stu-id="4b18a-105">Learn how to use HDInsight Tools for IntelliJ to develop Apache Scala applications and then test the applications on [Hortonworks Sandbox](http://hortonworks.com/products/sandbox/) running on your workstation.</span></span> 

<span data-ttu-id="4b18a-106">[IntelliJ IDEA](https://www.jetbrains.com/idea/) est un environnement de développement Java intégré (IDE) pour développer des logiciels.</span><span class="sxs-lookup"><span data-stu-id="4b18a-106">[IntelliJ IDEA](https://www.jetbrains.com/idea/) is a Java-integrated development environment (IDE) for developing computer software.</span></span> <span data-ttu-id="4b18a-107">Après avoir développé et testé vos applications sur Hortonworks Sandbox, vous pouvez les déplacer vers [Azure HDInsight](hdinsight-hadoop-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="4b18a-107">After you have developed and tested your applications on Hortonworks Sandbox, you can move them to [Azure HDInsight](hdinsight-hadoop-introduction.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4b18a-108">Composants requis</span><span class="sxs-lookup"><span data-stu-id="4b18a-108">Prerequisites</span></span>

<span data-ttu-id="4b18a-109">Avant de commencer ce didacticiel, vous devez disposer des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="4b18a-109">Before you begin this tutorial, you must have:</span></span>

- <span data-ttu-id="4b18a-110">Hortonworks Data Platform (HDP) 2.4 on Hortonworks Sandbox s’exécutant sur votre environnement local.</span><span class="sxs-lookup"><span data-stu-id="4b18a-110">Hortonworks Data Platform (HDP) 2.4 on Hortonworks Sandbox running on your local environment.</span></span> <span data-ttu-id="4b18a-111">Pour configurer HDP, consultez [Prise en main de l’écosystème Hadoop avec un bac à sable (sandbox) Hadoop sur une machine virtuelle](hdinsight-hadoop-emulator-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="4b18a-111">To configure HDP, see [Get started in the Hadoop ecosystem with a Hadoop sandbox on a virtual machine](hdinsight-hadoop-emulator-get-started.md).</span></span> 
    >[!NOTE]
    ><span data-ttu-id="4b18a-112">HDInsight Tools pour IntelliJ a seulement été testé avec HDP 2.4.</span><span class="sxs-lookup"><span data-stu-id="4b18a-112">HDInsight Tools for IntelliJ has been tested only with HDP 2.4.</span></span> <span data-ttu-id="4b18a-113">Pour obtenir HDP 2.4, développez **Hortonworks Sandbox Archive** sur le [site de téléchargement Hortonworks Sandbox](http://hortonworks.com/downloads/#sandbox).</span><span class="sxs-lookup"><span data-stu-id="4b18a-113">To get HDP 2.4, expand **Hortonworks Sandbox Archive** on the [Hortonworks Sandbox downloads site](http://hortonworks.com/downloads/#sandbox).</span></span>

- <span data-ttu-id="4b18a-114">[Kit de développeur Java (JDK) version 1.8 ou ultérieure](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).</span><span class="sxs-lookup"><span data-stu-id="4b18a-114">[Java Developer Kit (JDK) version 1.8 or later](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).</span></span> <span data-ttu-id="4b18a-115">JDK est requis par le Kit de ressources Azure pour IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="4b18a-115">JDK is required by the Azure Toolkit for IntelliJ.</span></span>

- <span data-ttu-id="4b18a-116">[Édition communautaire d’IntelliJ IDEA](https://www.jetbrains.com/idea/download) avec les plug-ins [Scala](https://plugins.jetbrains.com/idea/plugin/1347-scala) et [Kit de ressources Azure pour IntelliJ](../azure-toolkit-for-intellij.md).</span><span class="sxs-lookup"><span data-stu-id="4b18a-116">[IntelliJ IDEA community edition](https://www.jetbrains.com/idea/download) with the [Scala](https://plugins.jetbrains.com/idea/plugin/1347-scala) plug-in and the [Azure Toolkit for IntelliJ](../azure-toolkit-for-intellij.md) plug-in.</span></span> <span data-ttu-id="4b18a-117">HDInsight Tools pour IntelliJ est disponible dans le kit de ressources Azure pour IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="4b18a-117">HDInsight Tools for IntelliJ is available as a part of the Azure Toolkit for IntelliJ.</span></span> 

  <span data-ttu-id="4b18a-118">Pour installer les plug-ins, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="4b18a-118">To install the plug-ins, do the following:</span></span>

  1. <span data-ttu-id="4b18a-119">Ouvrez IntelliJ IDEA.</span><span class="sxs-lookup"><span data-stu-id="4b18a-119">Open IntelliJ IDEA.</span></span>
  2. <span data-ttu-id="4b18a-120">Sur l’écran d’**accueil**, sélectionnez **Configurer**, puis **Plug-ins**.</span><span class="sxs-lookup"><span data-stu-id="4b18a-120">On the **Welcome** screen, select **Configure**, and then select **Plugins**.</span></span>
  3. <span data-ttu-id="4b18a-121">Sélectionnez **Installer le plug-in JetBrains** dans le coin inférieur gauche.</span><span class="sxs-lookup"><span data-stu-id="4b18a-121">Select **Install JetBrains plugin** in the lower-left corner.</span></span>
  4. <span data-ttu-id="4b18a-122">Utilisez la fonction de recherche pour rechercher **Scala**, puis sélectionnez **Installer**.</span><span class="sxs-lookup"><span data-stu-id="4b18a-122">Use the search function to search for **Scala**, and then select **Install**.</span></span>
  5. <span data-ttu-id="4b18a-123">Sélectionnez **Redémarrer IntelliJ IDEA** pour terminer l’installation.</span><span class="sxs-lookup"><span data-stu-id="4b18a-123">Select **Restart IntelliJ IDEA** to complete the installation.</span></span>
  6. <span data-ttu-id="4b18a-124">Répétez les étapes 4 et 5 pour installer le **Kit de ressources Azure pour IntelliJ**.</span><span class="sxs-lookup"><span data-stu-id="4b18a-124">Repeat step 4 and 5 to install the **Azure Toolkit for IntelliJ**.</span></span> <span data-ttu-id="4b18a-125">Pour plus d’informations, consultez [Install the Azure Toolkit for IntelliJ](../azure-toolkit-for-intellij-installation.md)(Installer le Kit de ressources Azure pour IntelliJ).</span><span class="sxs-lookup"><span data-stu-id="4b18a-125">For more information, see [Install the Azure Toolkit for IntelliJ](../azure-toolkit-for-intellij-installation.md).</span></span>

## <a name="create-a-spark-scala-application"></a><span data-ttu-id="4b18a-126">Créer une application Spark Scala</span><span class="sxs-lookup"><span data-stu-id="4b18a-126">Create a Spark Scala application</span></span>

<span data-ttu-id="4b18a-127">Dans cette section, vous créez un exemple de projet Scala à l’aide d’IntelliJ IDEA.</span><span class="sxs-lookup"><span data-stu-id="4b18a-127">In this section, you create a sample Scala project by using IntelliJ IDEA.</span></span> <span data-ttu-id="4b18a-128">Dans la section suivante, vous lizr IntelliJ IDEA à Hortonworks Sandbox (émulateur) avant d’envoyer le projet.</span><span class="sxs-lookup"><span data-stu-id="4b18a-128">In the next section, you link IntelliJ IDEA to the Hortonworks Sandbox (emulator) before you submit the project.</span></span>

1. <span data-ttu-id="4b18a-129">Ouvrez IntelliJ IDEA à partir de votre station de travail.</span><span class="sxs-lookup"><span data-stu-id="4b18a-129">Open IntelliJ IDEA from your workstation.</span></span> <span data-ttu-id="4b18a-130">Dans la boîte de dialogue **Nouveau projet** , procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="4b18a-130">In the **New Project** dialog box, do the following:</span></span>

   <span data-ttu-id="4b18a-131">a.</span><span class="sxs-lookup"><span data-stu-id="4b18a-131">a.</span></span> <span data-ttu-id="4b18a-132">Sélectionnez **HDInsight** > **Spark sur HDInsight (Scala)**.</span><span class="sxs-lookup"><span data-stu-id="4b18a-132">Select **HDInsight** > **Spark on HDInsight (Scala)**.</span></span>

   <span data-ttu-id="4b18a-133">b.</span><span class="sxs-lookup"><span data-stu-id="4b18a-133">b.</span></span> <span data-ttu-id="4b18a-134">Dans la liste des **outils de génération**, sélectionnez l’une des options suivantes, en fonction de vos besoins :</span><span class="sxs-lookup"><span data-stu-id="4b18a-134">In the **Build tool** list, select either of the following, according to your need:</span></span>

    * <span data-ttu-id="4b18a-135">**Maven**, pour la prise en charge de l’Assistant de création de projets Scala</span><span class="sxs-lookup"><span data-stu-id="4b18a-135">**Maven**, for Scala project-creation wizard support</span></span>
    * <span data-ttu-id="4b18a-136">**SBT**, pour gérer les dépendances et la génération du projet Scala</span><span class="sxs-lookup"><span data-stu-id="4b18a-136">**SBT**, for managing the dependencies and building for the Scala project</span></span>

   ![Boîte de dialogue Nouveau projet](./media/hdinsight-tools-for-intellij-with-hortonworks-sandbox/intellij-create-scala-project.png)

2. <span data-ttu-id="4b18a-138">Sélectionnez **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="4b18a-138">Select **Next**.</span></span>

3. <span data-ttu-id="4b18a-139">Dans la boîte de dialogue **Nouveau projet** suivante, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="4b18a-139">In the next **New Project** dialog box, do the following:</span></span>

    ![Créer les propriétés du projet IntelliJ Scala](./media/hdinsight-tools-for-intellij-with-hortonworks-sandbox/intellij-create-scala-project-properties.png)

    <span data-ttu-id="4b18a-141">a.</span><span class="sxs-lookup"><span data-stu-id="4b18a-141">a.</span></span> <span data-ttu-id="4b18a-142">Dans la zone **Nom du projet**, entrez un nom de projet.</span><span class="sxs-lookup"><span data-stu-id="4b18a-142">In the **Project name** box, enter a project name.</span></span>

    <span data-ttu-id="4b18a-143">b.</span><span class="sxs-lookup"><span data-stu-id="4b18a-143">b.</span></span> <span data-ttu-id="4b18a-144">Dans la zone **Emplacement du projet**, entrez un emplacement de projet.</span><span class="sxs-lookup"><span data-stu-id="4b18a-144">In the **Project location** box, enter a project location.</span></span>

    <span data-ttu-id="4b18a-145">c.</span><span class="sxs-lookup"><span data-stu-id="4b18a-145">c.</span></span> <span data-ttu-id="4b18a-146">En regard de la liste déroulante **Kit de développement logiciel (SDK) de projet**, sélectionnez **Nouveau**, **JDK**, puis spécifiez le dossier Java JDK version 1.7 ou ultérieure.</span><span class="sxs-lookup"><span data-stu-id="4b18a-146">Next to the **Project SDK** drop-down list, select **New**, select **JDK**, and then specify the folder of Java JDK version 1.7 or later.</span></span> <span data-ttu-id="4b18a-147">Sélectionnez **Java 1.8** pour le cluster Spark 2.x, ou **Java 1.7** pour le cluster Spark 1.x.</span><span class="sxs-lookup"><span data-stu-id="4b18a-147">Select **Java 1.8** for the Spark 2.x cluster, or select **Java 1.7** for the Spark 1.x cluster.</span></span> <span data-ttu-id="4b18a-148">L’emplacement par défaut est C:\Program Files\Java\jdk1.8.x_xxx.</span><span class="sxs-lookup"><span data-stu-id="4b18a-148">The default location is C:\Program Files\Java\jdk1.8.x_xxx.</span></span>

    <span data-ttu-id="4b18a-149">d.</span><span class="sxs-lookup"><span data-stu-id="4b18a-149">d.</span></span> <span data-ttu-id="4b18a-150">Dans la liste déroulante **Version Spark**, l’assistant de création de projets Scala intègre la version correcte pour le kit de développement logiciel Spark et le kit de développement logiciel Scala.</span><span class="sxs-lookup"><span data-stu-id="4b18a-150">In the **Spark version** drop-down list, Scala project creation wizard integrates the proper version for Spark SDK and Scala SDK.</span></span> <span data-ttu-id="4b18a-151">Si la version du cluster spark est antérieure à la version 2.0, sélectionnez **Spark 1.x**.</span><span class="sxs-lookup"><span data-stu-id="4b18a-151">If the Spark cluster version is earlier than 2.0, select **Spark 1.x**.</span></span> <span data-ttu-id="4b18a-152">Sinon, sélectionnez **Spark 2.x**.</span><span class="sxs-lookup"><span data-stu-id="4b18a-152">Otherwise, select **Spark2.x**.</span></span> <span data-ttu-id="4b18a-153">La version utilisée dans cet exemple est Spark 1.6.2 (Scala 2.10.5).</span><span class="sxs-lookup"><span data-stu-id="4b18a-153">This example uses Spark 1.6.2 (Scala 2.10.5).</span></span> <span data-ttu-id="4b18a-154">Assurez-vous que vous utilisez le référentiel marqué Scala 2.10.x.</span><span class="sxs-lookup"><span data-stu-id="4b18a-154">Make sure that you are using the repository marked Scala 2.10.x.</span></span> <span data-ttu-id="4b18a-155">N’utilisez pas le référentiel marqué Scala 2.11.x.</span><span class="sxs-lookup"><span data-stu-id="4b18a-155">Do not use the repository marked Scala 2.11.x.</span></span>

4. <span data-ttu-id="4b18a-156">Sélectionnez **Terminer**.</span><span class="sxs-lookup"><span data-stu-id="4b18a-156">Select **Finish**.</span></span>

5. <span data-ttu-id="4b18a-157">Si la vue **Projet** n’est pas déjà ouverte, appuyez sur **Alt+1** pour l’ouvrir.</span><span class="sxs-lookup"><span data-stu-id="4b18a-157">If the **Project** view is not already open, press **Alt+1** to open it.</span></span>

6. <span data-ttu-id="4b18a-158">Dans l’**Explorateur de projets**, développez le projet, puis sélectionnez **src**.</span><span class="sxs-lookup"><span data-stu-id="4b18a-158">In **Project Explorer**, expand the project, and then select **src**.</span></span>

7. <span data-ttu-id="4b18a-159">Cliquez avec le bouton droit sur **src**, pointez sur **New** (Nouveau), puis sélectionnez **Scala class** (Classe Scala).</span><span class="sxs-lookup"><span data-stu-id="4b18a-159">Right-click **src**, point to **New**, and then select **Scala class**.</span></span>

8. <span data-ttu-id="4b18a-160">Entrez un nom dans la zone **Name**, et dans la zone **Kind** (Type), sélectionnez **Object** (Objet), puis **OK**.</span><span class="sxs-lookup"><span data-stu-id="4b18a-160">In the **Name** box, enter a name, in the **Kind** box, select **Object**, and then select **OK**.</span></span>

    ![Fenêtre Créer une classe Scala](./media/hdinsight-tools-for-intellij-with-hortonworks-sandbox/intellij-create-new-scala-class.png)

9. <span data-ttu-id="4b18a-162">Dans le fichier.scala, collez le code suivant :</span><span class="sxs-lookup"><span data-stu-id="4b18a-162">In the .scala file, paste the following code:</span></span>

        import java.util.Random
        import org.apache.spark.{SparkConf, SparkContext}
        import org.apache.spark.SparkContext._

        /**
        * Usage: GroupByTest [numMappers] [numKVPairs] [valSize] [numReducers]
        */
        object GroupByTest {
            def main(args: Array[String]) {
                val sparkConf = new SparkConf().setAppName("GroupBy Test")
                var numMappers = 3
                var numKVPairs = 10
                var valSize = 10
                var numReducers = 2

                val sc = new SparkContext(sparkConf)

                val pairs1 = sc.parallelize(0 until numMappers, numMappers).flatMap { p =>
                val ranGen = new Random
                var arr1 = new Array[(Int, Array[Byte])](numKVPairs)
                for (i <- 0 until numKVPairs) {
                    val byteArr = new Array[Byte](valSize)
                    ranGen.nextBytes(byteArr)
                    arr1(i) = (ranGen.nextInt(Int.MaxValue), byteArr)
                }
                arr1
                }.cache
                // Enforce that everything has been calculated and in cache
                pairs1.count

                println(pairs1.groupByKey(numReducers).count)
            }
        }

10. <span data-ttu-id="4b18a-163">Dans le menu **Générer**, sélectionnez **Générer un projet**.</span><span class="sxs-lookup"><span data-stu-id="4b18a-163">On the **Build** menu, select **Build project**.</span></span> <span data-ttu-id="4b18a-164">Vérifiez que la compilation a été terminée avec succès.</span><span class="sxs-lookup"><span data-stu-id="4b18a-164">Make sure that the compilation has been completed successfully.</span></span>


## <a name="link-to-the-hortonworks-sandbox"></a><span data-ttu-id="4b18a-165">Lien vers Hortonworks Sandbox</span><span class="sxs-lookup"><span data-stu-id="4b18a-165">Link to the Hortonworks Sandbox</span></span>

<span data-ttu-id="4b18a-166">Vous devez disposer d’une application IntelliJ existante avant de pouvoir établir un lien vers un Hortonworks Sandbox (émulateur).</span><span class="sxs-lookup"><span data-stu-id="4b18a-166">Before you can link to a Hortonworks Sandbox (emulator), you must have an existing IntelliJ application.</span></span>

<span data-ttu-id="4b18a-167">Pour établir un lien vers un émulateur, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="4b18a-167">To link to an emulator, do the following:</span></span>

1. <span data-ttu-id="4b18a-168">Ouvrez le projet dans IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="4b18a-168">Open the project in IntelliJ.</span></span>

2. <span data-ttu-id="4b18a-169">Dans le menu **Affichage**, sélectionnez **Fenêtres d’outil**, puis **Azure Explorer**.</span><span class="sxs-lookup"><span data-stu-id="4b18a-169">On the **View** menu, select **Tools Windows**, and then select **Azure Explorer**.</span></span>

3. <span data-ttu-id="4b18a-170">Développez **Azure**, cliquez avec le bouton droit sur **HDInsight**, puis sélectionnez **Lier un émulateur**.</span><span class="sxs-lookup"><span data-stu-id="4b18a-170">Expand **Azure**, right-click **HDInsight**, and then select **Link an Emulator**.</span></span>

4. <span data-ttu-id="4b18a-171">Dans la fenêtre **Link A New Emulator** (Lier un nouvel émulateur), saisissez le mot de passe que vous avez configuré pour le compte racine du Hortonworks Sandbox, puis entrez des valeurs semblables à celles de la capture d’écran ci-dessous et sélectionnez **OK**.</span><span class="sxs-lookup"><span data-stu-id="4b18a-171">In the **Link A New Emulator** window, enter the password that you've configured for the root account of the Hortonworks Sandbox, enter values similar to those in the following screenshot, and then select **OK**.</span></span> 

   ![Fenêtre « Link a New Emulator » (Lier un nouvel émulateur)](./media/hdinsight-tools-for-intellij-with-hortonworks-sandbox/intellij-link-an-emulator.png)

5. <span data-ttu-id="4b18a-173">Sélectionnez **Oui** pour configurer l’émulateur.</span><span class="sxs-lookup"><span data-stu-id="4b18a-173">To configure the emulator, select **Yes**.</span></span>

<span data-ttu-id="4b18a-174">Lorsque l’il est connecté avec succès, l’émulateur (Hortonworks Sandbox) est répertorié sous le nœud HDInsight.</span><span class="sxs-lookup"><span data-stu-id="4b18a-174">When the emulator is connected successfully, the emulator (Hortonworks Sandbox) is listed in the HDInsight node.</span></span>

## <a name="submit-the-spark-scala-application-to-the-hortonworks-sandbox"></a><span data-ttu-id="4b18a-175">Envoyer l’application Spark Scala au Hortonworks Sandbox</span><span class="sxs-lookup"><span data-stu-id="4b18a-175">Submit the Spark Scala application to the Hortonworks Sandbox</span></span>

<span data-ttu-id="4b18a-176">Après avoir lié IntelliJ IDEA à l’émulateur, vous pouvez envoyer votre projet.</span><span class="sxs-lookup"><span data-stu-id="4b18a-176">After you have linked IntelliJ IDEA to the emulator, you can submit your project.</span></span>

<span data-ttu-id="4b18a-177">Pour envoyer un projet à un émulateur, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="4b18a-177">To submit a project to an emulator, do the following:</span></span>

1. <span data-ttu-id="4b18a-178">Dans l’**Explorateur de projets**, cliquez avec le bouton droit sur le nom du projet et sélectionnez **Submit Spark Application to HDInsight** (Envoyer l’application Spark à HDInsight).</span><span class="sxs-lookup"><span data-stu-id="4b18a-178">In **Project Explorer**, right-click the project, and then select **Submit Spark application to HDInsight**.</span></span>

2. <span data-ttu-id="4b18a-179">Effectuez les actions suivantes :</span><span class="sxs-lookup"><span data-stu-id="4b18a-179">Do the following:</span></span>

    <span data-ttu-id="4b18a-180">a.</span><span class="sxs-lookup"><span data-stu-id="4b18a-180">a.</span></span> <span data-ttu-id="4b18a-181">Dans la liste déroulante **Cluster Spark (Linux uniquement)**, sélectionnez votre Hortonworks Sandbox local.</span><span class="sxs-lookup"><span data-stu-id="4b18a-181">In the **Spark cluster (Linux only)** drop-down list, select your local Hortonworks Sandbox.</span></span>

    <span data-ttu-id="4b18a-182">b.</span><span class="sxs-lookup"><span data-stu-id="4b18a-182">b.</span></span> <span data-ttu-id="4b18a-183">Dans la zone **Nom de la classe principale**, sélectionnez ou entrez le nom de la classe principale.</span><span class="sxs-lookup"><span data-stu-id="4b18a-183">In the **Main class name** box, choose or enter the main class name.</span></span> <span data-ttu-id="4b18a-184">Pour ce didacticiel, il s’agit de **GroupByTest**.</span><span class="sxs-lookup"><span data-stu-id="4b18a-184">For this tutorial, the name is **GroupByTest**.</span></span>

3. <span data-ttu-id="4b18a-185">Sélectionnez **Envoyer**.</span><span class="sxs-lookup"><span data-stu-id="4b18a-185">Select **Submit**.</span></span> <span data-ttu-id="4b18a-186">Les journaux d’envoi de travaux sont affichés dans la fenêtre d’outil d’envoi Spark.</span><span class="sxs-lookup"><span data-stu-id="4b18a-186">The job submission logs are shown in the Spark submission tool window.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4b18a-187">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="4b18a-187">Next steps</span></span>

- <span data-ttu-id="4b18a-188">Pour apprendre à créer des applications pour HDInsight à l’aide des outils HDInsight pour IntelliJ Spark, consultez [Utiliser HDInsight Tools dans le kit de ressources Azure pour IntelliJ afin de créer des applications Spark pour un cluster Linux HDInsight Spark](hdinsight-apache-spark-intellij-tool-plugin.md).</span><span class="sxs-lookup"><span data-stu-id="4b18a-188">To learn how to create Spark applications for HDInsight by using HDInsight Tools for IntelliJ, go to [Use HDInsight Tools in Azure Toolkit for IntelliJ to create Spark applications for HDInsight Spark Linux cluster](hdinsight-apache-spark-intellij-tool-plugin.md).</span></span>

- <span data-ttu-id="4b18a-189">Pour visionner une vidéo des outils HDInsight pour IntelliJ, consultez [Introduce HDInsight Tools for IntelliJ for Spark Development](https://www.youtube.com/watch?v=YTZzYVgut6c) (Présentation des outils HDInsight pour le développement d’IntelliJ pour Spark.</span><span class="sxs-lookup"><span data-stu-id="4b18a-189">To watch a video of HDInsight Tools for IntelliJ, go to [Introduce HDInsight Tools for IntelliJ for Spark Development](https://www.youtube.com/watch?v=YTZzYVgut6c).</span></span>

- <span data-ttu-id="4b18a-190">Pour apprendre à déboguer des applications Spark en utilisant le kit de ressources à distance sur HDInsight via SSH, consultez [Déboguer des applications Spark à distance sur un cluster HDInsight avec le kit de ressources Azure pour IntelliJ via SSH](hdinsight-apache-spark-intellij-tool-debug-remotely-through-ssh.md).</span><span class="sxs-lookup"><span data-stu-id="4b18a-190">To learn how to debug Spark applications by using the toolkit remotely on HDInsight through SSH, go to [Remotely debug Spark applications on an HDInsight cluster with Azure Toolkit for IntelliJ through SSH](hdinsight-apache-spark-intellij-tool-debug-remotely-through-ssh.md).</span></span>

- <span data-ttu-id="4b18a-191">Pour apprendre à déboguer des applications Spark en utilisant le kit de ressources à distance sur HDInsight via VPN, consultez [Utiliser HDInsight Tools dans le kit de ressources Azure pour IntelliJ pour déboguer des applications Spark à distance sur un cluster Linux Spark HDInsight](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md).</span><span class="sxs-lookup"><span data-stu-id="4b18a-191">To learn how to debug Spark applications by using the toolkit remotely on HDInsight through VPN, go to [Use HDInsight Tools in Azure Toolkit for IntelliJ to debug Spark applications remotely on HDInsight Spark Linux cluster](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md).</span></span>

- <span data-ttu-id="4b18a-192">Pour savoir comment utiliser les outils HDInsight pour Eclipse pour créer l’application Spark, consultez [Utiliser HDInsight Tools dans le kit de ressources Azure pour Eclipse pour créer des applications Spark](hdinsight-apache-spark-eclipse-tool-plugin.md).</span><span class="sxs-lookup"><span data-stu-id="4b18a-192">To learn how to use HDInsight Tools for Eclipse to create a Spark application, go to [Use HDInsight Tools in Azure Toolkit for Eclipse to create Spark applications](hdinsight-apache-spark-eclipse-tool-plugin.md).</span></span>

- <span data-ttu-id="4b18a-193">Pour visionner une vidéo de HDInsight Tools pour Eclipse, consultez [Use HDInsight Tool for Eclipse to create Spark applications](https://mix.office.com/watch/1rau2mopb6fha) (Utiliser HDInsight Tools pour Eclipse afin de créer des applications Spark).</span><span class="sxs-lookup"><span data-stu-id="4b18a-193">To watch a video of HDInsight Tools for Eclipse, go to [Use HDInsight Tool for Eclipse to create Spark applications](https://mix.office.com/watch/1rau2mopb6fha).</span></span>
