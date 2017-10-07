---
title: aaaUse Azure Toolkit pour IntelliJ avec Hortonworks Sandbox | Documents Microsoft
description: "En savoir plus toouse HDInsight outils dans la boîte à outils Azure pour IntelliJ avec Hortonworks Sandbox."
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
ms.openlocfilehash: 2bf97068a9cec99fcc7b4ff9469b91d8cbe2a8d8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hdinsight-tools-for-intellij-with-hortonworks-sandbox"></a><span data-ttu-id="6e1d8-104">Utiliser HDInsight Tools pour IntelliJ avec Hortonworks Sandbox</span><span class="sxs-lookup"><span data-stu-id="6e1d8-104">Use HDInsight Tools for IntelliJ with Hortonworks Sandbox</span></span>

<span data-ttu-id="6e1d8-105">Découvrez comment les outils de HDInsight toouse pour les applications Apache Scala IntelliJ toodevelop et puis effectuer des tests hello applications sur [Hortonworks Sandbox](http://hortonworks.com/products/sandbox/) en cours d’exécution sur votre station de travail.</span><span class="sxs-lookup"><span data-stu-id="6e1d8-105">Learn how toouse HDInsight Tools for IntelliJ toodevelop Apache Scala applications and then test hello applications on [Hortonworks Sandbox](http://hortonworks.com/products/sandbox/) running on your workstation.</span></span> 

<span data-ttu-id="6e1d8-106">[IntelliJ IDEA](https://www.jetbrains.com/idea/) est un environnement de développement Java intégré (IDE) pour développer des logiciels.</span><span class="sxs-lookup"><span data-stu-id="6e1d8-106">[IntelliJ IDEA](https://www.jetbrains.com/idea/) is a Java-integrated development environment (IDE) for developing computer software.</span></span> <span data-ttu-id="6e1d8-107">Après avoir développé et testé vos applications sur Hortonworks Sandbox, vous pouvez les déplacer trop[Azure HDInsight](hdinsight-hadoop-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="6e1d8-107">After you have developed and tested your applications on Hortonworks Sandbox, you can move them too[Azure HDInsight](hdinsight-hadoop-introduction.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6e1d8-108">Composants requis</span><span class="sxs-lookup"><span data-stu-id="6e1d8-108">Prerequisites</span></span>

<span data-ttu-id="6e1d8-109">Avant de commencer ce didacticiel, vous devez disposer des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="6e1d8-109">Before you begin this tutorial, you must have:</span></span>

- <span data-ttu-id="6e1d8-110">Hortonworks Data Platform (HDP) 2.4 on Hortonworks Sandbox s’exécutant sur votre environnement local.</span><span class="sxs-lookup"><span data-stu-id="6e1d8-110">Hortonworks Data Platform (HDP) 2.4 on Hortonworks Sandbox running on your local environment.</span></span> <span data-ttu-id="6e1d8-111">tooconfigure HDP, consultez [prise en main de l’écosystème de Hadoop hello avec un bac à sable Hadoop sur un ordinateur virtuel](hdinsight-hadoop-emulator-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="6e1d8-111">tooconfigure HDP, see [Get started in hello Hadoop ecosystem with a Hadoop sandbox on a virtual machine](hdinsight-hadoop-emulator-get-started.md).</span></span> 
    >[!NOTE]
    ><span data-ttu-id="6e1d8-112">HDInsight Tools pour IntelliJ a seulement été testé avec HDP 2.4.</span><span class="sxs-lookup"><span data-stu-id="6e1d8-112">HDInsight Tools for IntelliJ has been tested only with HDP 2.4.</span></span> <span data-ttu-id="6e1d8-113">tooget HDP 2.4, développez **Hortonworks Sandbox Archive** sur hello [Hortonworks Sandbox télécharge site](http://hortonworks.com/downloads/#sandbox).</span><span class="sxs-lookup"><span data-stu-id="6e1d8-113">tooget HDP 2.4, expand **Hortonworks Sandbox Archive** on hello [Hortonworks Sandbox downloads site](http://hortonworks.com/downloads/#sandbox).</span></span>

- <span data-ttu-id="6e1d8-114">[Kit de développeur Java (JDK) version 1.8 ou ultérieure](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).</span><span class="sxs-lookup"><span data-stu-id="6e1d8-114">[Java Developer Kit (JDK) version 1.8 or later](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).</span></span> <span data-ttu-id="6e1d8-115">JDK est requis par hello boîte à outils Azure pour IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="6e1d8-115">JDK is required by hello Azure Toolkit for IntelliJ.</span></span>

- <span data-ttu-id="6e1d8-116">[Édition de communauté IntelliJ idée](https://www.jetbrains.com/idea/download) avec hello [Scala](https://plugins.jetbrains.com/idea/plugin/1347-scala) plug-in et hello [Azure Toolkit pour IntelliJ](../azure-toolkit-for-intellij.md) plug-in.</span><span class="sxs-lookup"><span data-stu-id="6e1d8-116">[IntelliJ IDEA community edition](https://www.jetbrains.com/idea/download) with hello [Scala](https://plugins.jetbrains.com/idea/plugin/1347-scala) plug-in and hello [Azure Toolkit for IntelliJ](../azure-toolkit-for-intellij.md) plug-in.</span></span> <span data-ttu-id="6e1d8-117">Outils HDInsight pour IntelliJ est disponible dans le cadre de la boîte à outils Azure pour IntelliJ de hello.</span><span class="sxs-lookup"><span data-stu-id="6e1d8-117">HDInsight Tools for IntelliJ is available as a part of hello Azure Toolkit for IntelliJ.</span></span> 

  <span data-ttu-id="6e1d8-118">tooinstall hello plug-ins, hello suivant :</span><span class="sxs-lookup"><span data-stu-id="6e1d8-118">tooinstall hello plug-ins, do hello following:</span></span>

  1. <span data-ttu-id="6e1d8-119">Ouvrez IntelliJ IDEA.</span><span class="sxs-lookup"><span data-stu-id="6e1d8-119">Open IntelliJ IDEA.</span></span>
  2. <span data-ttu-id="6e1d8-120">Sur hello **Bienvenue** écran, sélectionnez **configurer**, puis sélectionnez **plug-ins**.</span><span class="sxs-lookup"><span data-stu-id="6e1d8-120">On hello **Welcome** screen, select **Configure**, and then select **Plugins**.</span></span>
  3. <span data-ttu-id="6e1d8-121">Sélectionnez **plug-in de l’installation de JetBrains** dans l’angle inférieur gauche de hello.</span><span class="sxs-lookup"><span data-stu-id="6e1d8-121">Select **Install JetBrains plugin** in hello lower-left corner.</span></span>
  4. <span data-ttu-id="6e1d8-122">Utilisez toosearch de fonction de recherche hello pour **Scala**, puis sélectionnez **installer**.</span><span class="sxs-lookup"><span data-stu-id="6e1d8-122">Use hello search function toosearch for **Scala**, and then select **Install**.</span></span>
  5. <span data-ttu-id="6e1d8-123">Sélectionnez **redémarrer une idée de IntelliJ** installation de hello toocomplete.</span><span class="sxs-lookup"><span data-stu-id="6e1d8-123">Select **Restart IntelliJ IDEA** toocomplete hello installation.</span></span>
  6. <span data-ttu-id="6e1d8-124">Hello de tooinstall Répétez l’étape 4 et 5 **Azure Toolkit pour IntelliJ**.</span><span class="sxs-lookup"><span data-stu-id="6e1d8-124">Repeat step 4 and 5 tooinstall hello **Azure Toolkit for IntelliJ**.</span></span> <span data-ttu-id="6e1d8-125">Pour plus d’informations, consultez [installation Bonjour Azure Toolkit pour IntelliJ](../azure-toolkit-for-intellij-installation.md).</span><span class="sxs-lookup"><span data-stu-id="6e1d8-125">For more information, see [Install hello Azure Toolkit for IntelliJ](../azure-toolkit-for-intellij-installation.md).</span></span>

## <a name="create-a-spark-scala-application"></a><span data-ttu-id="6e1d8-126">Créer une application Spark Scala</span><span class="sxs-lookup"><span data-stu-id="6e1d8-126">Create a Spark Scala application</span></span>

<span data-ttu-id="6e1d8-127">Dans cette section, vous créez un exemple de projet Scala à l’aide d’IntelliJ IDEA.</span><span class="sxs-lookup"><span data-stu-id="6e1d8-127">In this section, you create a sample Scala project by using IntelliJ IDEA.</span></span> <span data-ttu-id="6e1d8-128">Dans la section suivante de hello, vous liez IntelliJ idée toohello Hortonworks Sandbox (émulateur) avant d’envoyer le projet de hello.</span><span class="sxs-lookup"><span data-stu-id="6e1d8-128">In hello next section, you link IntelliJ IDEA toohello Hortonworks Sandbox (emulator) before you submit hello project.</span></span>

1. <span data-ttu-id="6e1d8-129">Ouvrez IntelliJ IDEA à partir de votre station de travail.</span><span class="sxs-lookup"><span data-stu-id="6e1d8-129">Open IntelliJ IDEA from your workstation.</span></span> <span data-ttu-id="6e1d8-130">Bonjour **nouveau projet** boîte de dialogue zone, hello suivant :</span><span class="sxs-lookup"><span data-stu-id="6e1d8-130">In hello **New Project** dialog box, do hello following:</span></span>

   <span data-ttu-id="6e1d8-131">a.</span><span class="sxs-lookup"><span data-stu-id="6e1d8-131">a.</span></span> <span data-ttu-id="6e1d8-132">Sélectionnez **HDInsight** > **Spark sur HDInsight (Scala)**.</span><span class="sxs-lookup"><span data-stu-id="6e1d8-132">Select **HDInsight** > **Spark on HDInsight (Scala)**.</span></span>

   <span data-ttu-id="6e1d8-133">b.</span><span class="sxs-lookup"><span data-stu-id="6e1d8-133">b.</span></span> <span data-ttu-id="6e1d8-134">Bonjour **outil de génération** , sélectionnez une des hello suivant, selon le besoin de tooyour :</span><span class="sxs-lookup"><span data-stu-id="6e1d8-134">In hello **Build tool** list, select either of hello following, according tooyour need:</span></span>

    * <span data-ttu-id="6e1d8-135">**Maven**, pour la prise en charge de l’Assistant de création de projets Scala</span><span class="sxs-lookup"><span data-stu-id="6e1d8-135">**Maven**, for Scala project-creation wizard support</span></span>
    * <span data-ttu-id="6e1d8-136">**SBT**, pour la gestion des dépendances de hello et la création de projet de Scala hello</span><span class="sxs-lookup"><span data-stu-id="6e1d8-136">**SBT**, for managing hello dependencies and building for hello Scala project</span></span>

   ![boîte de dialogue Nouveau projet Hello](./media/hdinsight-tools-for-intellij-with-hortonworks-sandbox/intellij-create-scala-project.png)

2. <span data-ttu-id="6e1d8-138">Sélectionnez **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="6e1d8-138">Select **Next**.</span></span>

3. <span data-ttu-id="6e1d8-139">Bonjour suivant **nouveau projet** boîte de dialogue zone, hello suivant :</span><span class="sxs-lookup"><span data-stu-id="6e1d8-139">In hello next **New Project** dialog box, do hello following:</span></span>

    ![Créer les propriétés du projet IntelliJ Scala](./media/hdinsight-tools-for-intellij-with-hortonworks-sandbox/intellij-create-scala-project-properties.png)

    <span data-ttu-id="6e1d8-141">a.</span><span class="sxs-lookup"><span data-stu-id="6e1d8-141">a.</span></span> <span data-ttu-id="6e1d8-142">Bonjour **nom du projet** , entrez un nom de projet.</span><span class="sxs-lookup"><span data-stu-id="6e1d8-142">In hello **Project name** box, enter a project name.</span></span>

    <span data-ttu-id="6e1d8-143">b.</span><span class="sxs-lookup"><span data-stu-id="6e1d8-143">b.</span></span> <span data-ttu-id="6e1d8-144">Bonjour **emplacement du projet** , entrez un emplacement de projet.</span><span class="sxs-lookup"><span data-stu-id="6e1d8-144">In hello **Project location** box, enter a project location.</span></span>

    <span data-ttu-id="6e1d8-145">c.</span><span class="sxs-lookup"><span data-stu-id="6e1d8-145">c.</span></span> <span data-ttu-id="6e1d8-146">Toohello suivant **projet SDK** la liste déroulante, sélectionnez **nouveau**, sélectionnez **JDK**, puis spécifiez le dossier hello de Java JDK version 1.7 ou ultérieure.</span><span class="sxs-lookup"><span data-stu-id="6e1d8-146">Next toohello **Project SDK** drop-down list, select **New**, select **JDK**, and then specify hello folder of Java JDK version 1.7 or later.</span></span> <span data-ttu-id="6e1d8-147">Sélectionnez **Java 1.8** pour le cluster de hello Spark 2.x, ou sélectionnez **Java 1.7** pour le cluster de hello Spark 1.x.</span><span class="sxs-lookup"><span data-stu-id="6e1d8-147">Select **Java 1.8** for hello Spark 2.x cluster, or select **Java 1.7** for hello Spark 1.x cluster.</span></span> <span data-ttu-id="6e1d8-148">Hello par défaut est C:\Program Files\Java\jdk1.8.x_xxx.</span><span class="sxs-lookup"><span data-stu-id="6e1d8-148">hello default location is C:\Program Files\Java\jdk1.8.x_xxx.</span></span>

    <span data-ttu-id="6e1d8-149">d.</span><span class="sxs-lookup"><span data-stu-id="6e1d8-149">d.</span></span> <span data-ttu-id="6e1d8-150">Bonjour **version de Spark** la liste déroulante, Assistant de création de projet Scala intègre version correcte de hello pour le Kit de développement logiciel Spark et Scala SDK.</span><span class="sxs-lookup"><span data-stu-id="6e1d8-150">In hello **Spark version** drop-down list, Scala project creation wizard integrates hello proper version for Spark SDK and Scala SDK.</span></span> <span data-ttu-id="6e1d8-151">Si la version du cluster Spark hello est antérieure à la version 2.0, sélectionnez **nouvelles 1.x**.</span><span class="sxs-lookup"><span data-stu-id="6e1d8-151">If hello Spark cluster version is earlier than 2.0, select **Spark 1.x**.</span></span> <span data-ttu-id="6e1d8-152">Sinon, sélectionnez **Spark 2.x**.</span><span class="sxs-lookup"><span data-stu-id="6e1d8-152">Otherwise, select **Spark2.x**.</span></span> <span data-ttu-id="6e1d8-153">La version utilisée dans cet exemple est Spark 1.6.2 (Scala 2.10.5).</span><span class="sxs-lookup"><span data-stu-id="6e1d8-153">This example uses Spark 1.6.2 (Scala 2.10.5).</span></span> <span data-ttu-id="6e1d8-154">Assurez-vous que vous utilisez référentiel hello marquée Scala 2.10.x.</span><span class="sxs-lookup"><span data-stu-id="6e1d8-154">Make sure that you are using hello repository marked Scala 2.10.x.</span></span> <span data-ttu-id="6e1d8-155">N’utilisez pas de référentiel hello marquée Scala 2.11.x.</span><span class="sxs-lookup"><span data-stu-id="6e1d8-155">Do not use hello repository marked Scala 2.11.x.</span></span>

4. <span data-ttu-id="6e1d8-156">Sélectionnez **Terminer**.</span><span class="sxs-lookup"><span data-stu-id="6e1d8-156">Select **Finish**.</span></span>

5. <span data-ttu-id="6e1d8-157">Si hello **projet** affichage n’est pas déjà ouvert, appuyez sur **Alt + 1** tooopen il.</span><span class="sxs-lookup"><span data-stu-id="6e1d8-157">If hello **Project** view is not already open, press **Alt+1** tooopen it.</span></span>

6. <span data-ttu-id="6e1d8-158">Dans **Explorateur de projets**, développez le projet de hello, puis sélectionnez **src**.</span><span class="sxs-lookup"><span data-stu-id="6e1d8-158">In **Project Explorer**, expand hello project, and then select **src**.</span></span>

7. <span data-ttu-id="6e1d8-159">Avec le bouton droit **src**, pointez trop**nouveau**, puis sélectionnez **Scala classe**.</span><span class="sxs-lookup"><span data-stu-id="6e1d8-159">Right-click **src**, point too**New**, and then select **Scala class**.</span></span>

8. <span data-ttu-id="6e1d8-160">Bonjour **nom** , entrez un nom, Bonjour **type** boîte, sélectionnez **objet**, puis sélectionnez **OK**.</span><span class="sxs-lookup"><span data-stu-id="6e1d8-160">In hello **Name** box, enter a name, in hello **Kind** box, select **Object**, and then select **OK**.</span></span>

    ![fenêtre Créer une nouvelle classe Scala de Hello](./media/hdinsight-tools-for-intellij-with-hortonworks-sandbox/intellij-create-new-scala-class.png)

9. <span data-ttu-id="6e1d8-162">Dans le fichier de .scala hello, collez hello suivant de code :</span><span class="sxs-lookup"><span data-stu-id="6e1d8-162">In hello .scala file, paste hello following code:</span></span>

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

10. <span data-ttu-id="6e1d8-163">Sur hello **générer** menu, sélectionnez **projet Build**.</span><span class="sxs-lookup"><span data-stu-id="6e1d8-163">On hello **Build** menu, select **Build project**.</span></span> <span data-ttu-id="6e1d8-164">Assurez-vous que la compilation hello est terminée avec succès.</span><span class="sxs-lookup"><span data-stu-id="6e1d8-164">Make sure that hello compilation has been completed successfully.</span></span>


## <a name="link-toohello-hortonworks-sandbox"></a><span data-ttu-id="6e1d8-165">Lien toohello Hortonworks Sandbox</span><span class="sxs-lookup"><span data-stu-id="6e1d8-165">Link toohello Hortonworks Sandbox</span></span>

<span data-ttu-id="6e1d8-166">Avant de pouvoir lier tooa Hortonworks Sandbox (émulateur), vous devez disposer d’une application IntelliJ existante.</span><span class="sxs-lookup"><span data-stu-id="6e1d8-166">Before you can link tooa Hortonworks Sandbox (emulator), you must have an existing IntelliJ application.</span></span>

<span data-ttu-id="6e1d8-167">émulateur de tooan toolink, hello suivant :</span><span class="sxs-lookup"><span data-stu-id="6e1d8-167">toolink tooan emulator, do hello following:</span></span>

1. <span data-ttu-id="6e1d8-168">Projet ouvert hello dans IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="6e1d8-168">Open hello project in IntelliJ.</span></span>

2. <span data-ttu-id="6e1d8-169">Sur hello **vue** menu, sélectionnez **outils Windows**, puis sélectionnez **Explorateur Azure**.</span><span class="sxs-lookup"><span data-stu-id="6e1d8-169">On hello **View** menu, select **Tools Windows**, and then select **Azure Explorer**.</span></span>

3. <span data-ttu-id="6e1d8-170">Développez **Azure**, cliquez avec le bouton droit sur **HDInsight**, puis sélectionnez **Lier un émulateur**.</span><span class="sxs-lookup"><span data-stu-id="6e1d8-170">Expand **Azure**, right-click **HDInsight**, and then select **Link an Emulator**.</span></span>

4. <span data-ttu-id="6e1d8-171">Bonjour **lien un nouvel émulateur** fenêtre, entrez un mot de passe hello vos configurés pour le compte de racine hello Hello bac à sable Hortonworks, entrez toothose similaire de valeurs Bonjour suivant capture d’écran, puis **OK** .</span><span class="sxs-lookup"><span data-stu-id="6e1d8-171">In hello **Link A New Emulator** window, enter hello password that you've configured for hello root account of hello Hortonworks Sandbox, enter values similar toothose in hello following screenshot, and then select **OK**.</span></span> 

   ![fenêtre de « Lier un nouvel émulateur » Hello](./media/hdinsight-tools-for-intellij-with-hortonworks-sandbox/intellij-link-an-emulator.png)

5. <span data-ttu-id="6e1d8-173">émulateur Windows hello tooconfigure, sélectionnez **Oui**.</span><span class="sxs-lookup"><span data-stu-id="6e1d8-173">tooconfigure hello emulator, select **Yes**.</span></span>

<span data-ttu-id="6e1d8-174">Lors de l’émulateur de hello est connecté avec succès, l’émulateur hello (Hortonworks Sandbox) est répertorié dans le nœud de HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="6e1d8-174">When hello emulator is connected successfully, hello emulator (Hortonworks Sandbox) is listed in hello HDInsight node.</span></span>

## <a name="submit-hello-spark-scala-application-toohello-hortonworks-sandbox"></a><span data-ttu-id="6e1d8-175">Soumettre hello Spark Scala application toohello Hortonworks Sandbox</span><span class="sxs-lookup"><span data-stu-id="6e1d8-175">Submit hello Spark Scala application toohello Hortonworks Sandbox</span></span>

<span data-ttu-id="6e1d8-176">Une fois que vous avez lié l’émulateur de toohello IntelliJ idée, vous pouvez soumettre votre projet.</span><span class="sxs-lookup"><span data-stu-id="6e1d8-176">After you have linked IntelliJ IDEA toohello emulator, you can submit your project.</span></span>

<span data-ttu-id="6e1d8-177">toosubmit un émulateur tooan du projet, procédez comme hello suivant :</span><span class="sxs-lookup"><span data-stu-id="6e1d8-177">toosubmit a project tooan emulator, do hello following:</span></span>

1. <span data-ttu-id="6e1d8-178">Dans **Explorateur de projets**, cliquez sur le projet de hello, puis sélectionnez **soumettre de Spark application tooHDInsight**.</span><span class="sxs-lookup"><span data-stu-id="6e1d8-178">In **Project Explorer**, right-click hello project, and then select **Submit Spark application tooHDInsight**.</span></span>

2. <span data-ttu-id="6e1d8-179">Hello suivant :</span><span class="sxs-lookup"><span data-stu-id="6e1d8-179">Do hello following:</span></span>

    <span data-ttu-id="6e1d8-180">a.</span><span class="sxs-lookup"><span data-stu-id="6e1d8-180">a.</span></span> <span data-ttu-id="6e1d8-181">Bonjour **le cluster Spark (Linux uniquement)** liste déroulante, sélectionnez votre bac à sable Hortonworks local.</span><span class="sxs-lookup"><span data-stu-id="6e1d8-181">In hello **Spark cluster (Linux only)** drop-down list, select your local Hortonworks Sandbox.</span></span>

    <span data-ttu-id="6e1d8-182">b.</span><span class="sxs-lookup"><span data-stu-id="6e1d8-182">b.</span></span> <span data-ttu-id="6e1d8-183">Bonjour **nom de la classe principale** zone, sélectionnez ou entrez le nom de la classe principale hello.</span><span class="sxs-lookup"><span data-stu-id="6e1d8-183">In hello **Main class name** box, choose or enter hello main class name.</span></span> <span data-ttu-id="6e1d8-184">Pour ce didacticiel, le nom de hello est **GroupByTest**.</span><span class="sxs-lookup"><span data-stu-id="6e1d8-184">For this tutorial, hello name is **GroupByTest**.</span></span>

3. <span data-ttu-id="6e1d8-185">Sélectionnez **Envoyer**.</span><span class="sxs-lookup"><span data-stu-id="6e1d8-185">Select **Submit**.</span></span> <span data-ttu-id="6e1d8-186">envoi des journaux de la tâche Hello sont affichés dans la fenêtre d’outil hello Spark soumission.</span><span class="sxs-lookup"><span data-stu-id="6e1d8-186">hello job submission logs are shown in hello Spark submission tool window.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6e1d8-187">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="6e1d8-187">Next steps</span></span>

- <span data-ttu-id="6e1d8-188">comment les applications de Spark toocreate pour HDInsight à l’aide des outils HDInsight pour IntelliJ, accédez trop de toolearn[utiliser les outils HDInsight dans la boîte à outils Azure pour les applications Spark cluster HDInsight Spark Linux IntelliJ toocreate](hdinsight-apache-spark-intellij-tool-plugin.md).</span><span class="sxs-lookup"><span data-stu-id="6e1d8-188">toolearn how toocreate Spark applications for HDInsight by using HDInsight Tools for IntelliJ, go too[Use HDInsight Tools in Azure Toolkit for IntelliJ toocreate Spark applications for HDInsight Spark Linux cluster](hdinsight-apache-spark-intellij-tool-plugin.md).</span></span>

- <span data-ttu-id="6e1d8-189">toowatch une vidéo d’outils HDInsight pour IntelliJ, accédez trop[présentent les outils HDInsight pour IntelliJ pour le développement de Spark](https://www.youtube.com/watch?v=YTZzYVgut6c).</span><span class="sxs-lookup"><span data-stu-id="6e1d8-189">toowatch a video of HDInsight Tools for IntelliJ, go too[Introduce HDInsight Tools for IntelliJ for Spark Development](https://www.youtube.com/watch?v=YTZzYVgut6c).</span></span>

- <span data-ttu-id="6e1d8-190">toolearn comment les applications de Spark toodebug à l’aide de hello boîte à outils à distance sur HDInsight via SSH, accédez trop[déboguer à distance Spark sur un cluster HDInsight avec la boîte à outils Azure pour IntelliJ via SSH](hdinsight-apache-spark-intellij-tool-debug-remotely-through-ssh.md).</span><span class="sxs-lookup"><span data-stu-id="6e1d8-190">toolearn how toodebug Spark applications by using hello toolkit remotely on HDInsight through SSH, go too[Remotely debug Spark applications on an HDInsight cluster with Azure Toolkit for IntelliJ through SSH](hdinsight-apache-spark-intellij-tool-debug-remotely-through-ssh.md).</span></span>

- <span data-ttu-id="6e1d8-191">toolearn comment les applications de Spark toodebug à l’aide de hello boîte à outils à distance sur HDInsight via VPN, accédez trop[utiliser les outils HDInsight dans la boîte à outils Azure pour les applications de Spark IntelliJ toodebug à distance sur le cluster HDInsight Spark Linux](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md).</span><span class="sxs-lookup"><span data-stu-id="6e1d8-191">toolearn how toodebug Spark applications by using hello toolkit remotely on HDInsight through VPN, go too[Use HDInsight Tools in Azure Toolkit for IntelliJ toodebug Spark applications remotely on HDInsight Spark Linux cluster](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md).</span></span>

- <span data-ttu-id="6e1d8-192">toolearn comment toouse outils HDInsight pour Eclipse toocreate une application Spark, accédez trop[utiliser les outils HDInsight dans la boîte à outils Azure pour les applications de Spark Eclipse toocreate](hdinsight-apache-spark-eclipse-tool-plugin.md).</span><span class="sxs-lookup"><span data-stu-id="6e1d8-192">toolearn how toouse HDInsight Tools for Eclipse toocreate a Spark application, go too[Use HDInsight Tools in Azure Toolkit for Eclipse toocreate Spark applications](hdinsight-apache-spark-eclipse-tool-plugin.md).</span></span>

- <span data-ttu-id="6e1d8-193">toowatch une vidéo d’outils HDInsight pour Eclipse, accédez trop[HDInsight utiliser un outil pour les applications de Spark Eclipse toocreate](https://mix.office.com/watch/1rau2mopb6fha).</span><span class="sxs-lookup"><span data-stu-id="6e1d8-193">toowatch a video of HDInsight Tools for Eclipse, go too[Use HDInsight Tool for Eclipse toocreate Spark applications](https://mix.office.com/watch/1rau2mopb6fha).</span></span>
