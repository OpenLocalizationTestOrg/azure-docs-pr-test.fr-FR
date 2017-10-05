---
title: "Kit de ressources Azure pour IntelliJ : déboguer des applications Spark à distance via SSH | Microsoft Docs"
description: "Obtenez des instructions étape par étape sur la façon d’utiliser HDInsight Tools dans le kit de ressources Azure pour IntelliJ pour déboguer des applications à distance sur des clusters HDInsight via SSH"
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
ms.openlocfilehash: 19053e31d6eb097bc91a04ef9c6af5772aaa16da
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="debug-spark-applications-on-an-hdinsight-cluster-with-azure-toolkit-for-intellij-through-ssh"></a><span data-ttu-id="fe714-104">Déboguez des applications Spark sur un cluster HDInsight avec le kit de ressources Azure pour IntelliJ via SSH</span><span class="sxs-lookup"><span data-stu-id="fe714-104">Debug Spark applications on an HDInsight cluster with Azure Toolkit for IntelliJ through SSH</span></span>

<span data-ttu-id="fe714-105">Cet article propose des instructions étape par étape sur la façon d’utiliser HDInsight Tools dans le kit de ressources Azure pour IntelliJ pour déboguer des applications à distance sur un cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="fe714-105">This article provides step-by-step guidance on how to use HDInsight Tools in Azure Toolkit for IntelliJ to debug applications remotely on an HDInsight cluster.</span></span> <span data-ttu-id="fe714-106">Pour déboguer votre projet, vous pouvez également regarder la vidéo [Debug HDInsight Spark applications with Azure Toolkit for IntelliJ](https://channel9.msdn.com/Series/AzureDataLake/Debug-HDInsight-Spark-Applications-with-Azure-Toolkit-for-IntelliJ) (Déboguer des applications HDInsight Spark avec le kit de ressources Azure pour IntelliJ).</span><span class="sxs-lookup"><span data-stu-id="fe714-106">To debug your project, you can also view the [Debug HDInsight Spark applications with Azure Toolkit for IntelliJ](https://channel9.msdn.com/Series/AzureDataLake/Debug-HDInsight-Spark-Applications-with-Azure-Toolkit-for-IntelliJ) video.</span></span>

<span data-ttu-id="fe714-107">**Configuration requise**</span><span class="sxs-lookup"><span data-stu-id="fe714-107">**Prerequisites**</span></span>

* <span data-ttu-id="fe714-108">**Outils HDInsight dans le kit de ressources Azure pour IntelliJ**.</span><span class="sxs-lookup"><span data-stu-id="fe714-108">**HDInsight Tools in Azure Toolkit for IntelliJ**.</span></span> <span data-ttu-id="fe714-109">Cet outil fait partie du kit de ressources Azure pour IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="fe714-109">This tool is part of Azure Toolkit for IntelliJ.</span></span> <span data-ttu-id="fe714-110">Pour plus d’informations, consultez [Installation du kit de ressources Azure pour IntelliJ](https://docs.microsoft.com/en-us/azure/azure-toolkit-for-intellij-installation).</span><span class="sxs-lookup"><span data-stu-id="fe714-110">For more information, see [Install Azure Toolkit for IntelliJ](https://docs.microsoft.com/en-us/azure/azure-toolkit-for-intellij-installation).</span></span>
* <span data-ttu-id="fe714-111">**Kit de ressources Azure pour IntelliJ**.</span><span class="sxs-lookup"><span data-stu-id="fe714-111">**Azure Toolkit for IntelliJ**.</span></span> <span data-ttu-id="fe714-112">Utilisez ce kit de ressources pour créer des applications Spark pour un cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="fe714-112">Use this toolkit to create Spark applications for an HDInsight cluster.</span></span> <span data-ttu-id="fe714-113">Pour plus d’informations, veuillez suivre les instructions de la rubrique [Utiliser le kit de ressources Azure pour IntelliJ pour créer des applications Spark pour un cluster HDInsight](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-apache-spark-intellij-tool-plugin).</span><span class="sxs-lookup"><span data-stu-id="fe714-113">For more information, follow the instructions in [Use Azure Toolkit for IntelliJ to create Spark applications for an HDInsight cluster](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-apache-spark-intellij-tool-plugin).</span></span>
* <span data-ttu-id="fe714-114">**Service HDInsight SSH avec gestion de nom d’utilisateur et de mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="fe714-114">**HDInsight SSH service with username and password management**.</span></span> <span data-ttu-id="fe714-115">Pour plus d’informations consultez la rubrique [Connexion à HDInsight (Hadoop) à l’aide de SSH](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-linux-use-ssh-unix) et [Utiliser le tunneling SSH pour accéder à l’IU web Ambari, JobHistory, NameNode, Oozie et à d’autres IU web](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-linux-ambari-ssh-tunnel).</span><span class="sxs-lookup"><span data-stu-id="fe714-115">For more information, see [Connect to HDInsight (Hadoop) by using SSH](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-linux-use-ssh-unix) and [Use SSH tunneling to access Ambari web UI, JobHistory, NameNode, Oozie, and other web UIs](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-linux-ambari-ssh-tunnel).</span></span> 
 

## <a name="create-a-spark-scala-application-and-configure-it-for-remote-debugging"></a><span data-ttu-id="fe714-116">Créer une application Spark Scala et la configurer pour le débogage à distance</span><span class="sxs-lookup"><span data-stu-id="fe714-116">Create a Spark Scala application and configure it for remote debugging</span></span>

1. <span data-ttu-id="fe714-117">Démarrez IntelliJ IDEA et créez un projet.</span><span class="sxs-lookup"><span data-stu-id="fe714-117">Start IntelliJ IDEA, and then create a project.</span></span> <span data-ttu-id="fe714-118">Dans la boîte de dialogue **Nouveau projet** , procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="fe714-118">In the **New Project** dialog box, do the following:</span></span>

   <span data-ttu-id="fe714-119">a.</span><span class="sxs-lookup"><span data-stu-id="fe714-119">a.</span></span> <span data-ttu-id="fe714-120">Sélectionnez **HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="fe714-120">Select **HDInsight**.</span></span> 

   <span data-ttu-id="fe714-121">b.</span><span class="sxs-lookup"><span data-stu-id="fe714-121">b.</span></span> <span data-ttu-id="fe714-122">Sélectionnez un modèle Java ou Scala en fonction de vos préférences.</span><span class="sxs-lookup"><span data-stu-id="fe714-122">Select a Java or Scala template based on your preference.</span></span> <span data-ttu-id="fe714-123">Sélectionnez entre les options suivantes :</span><span class="sxs-lookup"><span data-stu-id="fe714-123">Select between the following options:</span></span>

      - <span data-ttu-id="fe714-124">**Spark sur HDInsight (Scala)**</span><span class="sxs-lookup"><span data-stu-id="fe714-124">**Spark on HDInsight (Scala)**</span></span>

      - <span data-ttu-id="fe714-125">**Spark sur HDInsight (Java)**</span><span class="sxs-lookup"><span data-stu-id="fe714-125">**Spark on HDInsight (Java)**</span></span>

      - <span data-ttu-id="fe714-126">**Spark sur exemple d’exécution de cluster HDInsight (Scala)**</span><span class="sxs-lookup"><span data-stu-id="fe714-126">**Spark on HDInsight Cluster Run Sample (Scala)**</span></span>

      <span data-ttu-id="fe714-127">Cet exemple utilise un modèle **Spark sur exemple d’exécution de cluster HDInsight (Scala)**.</span><span class="sxs-lookup"><span data-stu-id="fe714-127">This example uses a **Spark on HDInsight Cluster Run Sample (Scala)** template.</span></span>

   <span data-ttu-id="fe714-128">c.</span><span class="sxs-lookup"><span data-stu-id="fe714-128">c.</span></span> <span data-ttu-id="fe714-129">Dans la liste des **outils de génération**, sélectionnez l’une des options suivantes, en fonction de vos besoins :</span><span class="sxs-lookup"><span data-stu-id="fe714-129">In the **Build tool** list, select either of the following, according to your need:</span></span>

      - <span data-ttu-id="fe714-130">**Maven**, pour la prise en charge de l’Assistant de création de projets Scala</span><span class="sxs-lookup"><span data-stu-id="fe714-130">**Maven**, for Scala project-creation wizard support</span></span>

      -  <span data-ttu-id="fe714-131">**SBT**, pour gérer les dépendances et la génération du projet Scala</span><span class="sxs-lookup"><span data-stu-id="fe714-131">**SBT**, for managing the dependencies and building for the Scala project</span></span> 

      ![Créer un projet de débogage](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-create-projectfor-debug-remotely.png)

   <span data-ttu-id="fe714-133">d.</span><span class="sxs-lookup"><span data-stu-id="fe714-133">d.</span></span> <span data-ttu-id="fe714-134">Sélectionnez **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="fe714-134">Select **Next**.</span></span>     
 
3. <span data-ttu-id="fe714-135">Dans la fenêtre **Nouveau projet** qui s’ouvre, effectuez les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="fe714-135">In the next **New Project** window, do the following:</span></span>

   ![Sélectionner le SDK Spark](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-new-project.png)

   <span data-ttu-id="fe714-137">a.</span><span class="sxs-lookup"><span data-stu-id="fe714-137">a.</span></span> <span data-ttu-id="fe714-138">Entrez un nom de projet et un emplacement de projet.</span><span class="sxs-lookup"><span data-stu-id="fe714-138">Enter a project name and project location.</span></span>

   <span data-ttu-id="fe714-139">b.</span><span class="sxs-lookup"><span data-stu-id="fe714-139">b.</span></span> <span data-ttu-id="fe714-140">Dans la liste déroulante **Kit de développement logiciel (SDK) de projet**, sélectionnez **Java 1.8** pour le cluster **Spark 2.x** ou **Java 1.7** pour le cluster **Spark 1.x**.</span><span class="sxs-lookup"><span data-stu-id="fe714-140">In the **Project SDK** drop-down list, select **Java 1.8** for **Spark 2.x** cluster or select **Java 1.7** for **Spark 1.x** cluster.</span></span>

   <span data-ttu-id="fe714-141">c.</span><span class="sxs-lookup"><span data-stu-id="fe714-141">c.</span></span> <span data-ttu-id="fe714-142">Dans la liste déroulante **Version Spark**, l’assistant de création de projets Scala intègre la version correcte pour le SDK Spark et le SDK Scala.</span><span class="sxs-lookup"><span data-stu-id="fe714-142">In the **Spark Version** drop-down list, the Scala project creation wizard integrates the correct version for Spark SDK and Scala SDK.</span></span> <span data-ttu-id="fe714-143">Si la version du cluster spark est antérieure à la version 2.0, sélectionnez **Spark 1.x**.</span><span class="sxs-lookup"><span data-stu-id="fe714-143">If the spark cluster version is earlier than 2.0, select **Spark 1.x**.</span></span> <span data-ttu-id="fe714-144">Sinon, sélectionnez **Spark 2.x.**</span><span class="sxs-lookup"><span data-stu-id="fe714-144">Otherwise, select **Spark 2.x.**</span></span> <span data-ttu-id="fe714-145">La version utilisée dans cet exemple est **Spark 2.0.2 (Scala 2.11.8)**.</span><span class="sxs-lookup"><span data-stu-id="fe714-145">This example uses **Spark 2.0.2 (Scala 2.11.8)**.</span></span>

   <span data-ttu-id="fe714-146">d.</span><span class="sxs-lookup"><span data-stu-id="fe714-146">d.</span></span> <span data-ttu-id="fe714-147">Sélectionnez **Terminer**.</span><span class="sxs-lookup"><span data-stu-id="fe714-147">Select **Finish**.</span></span>

4. <span data-ttu-id="fe714-148">Sélectionnez **src** > **principal** > **scala** pour ouvrir votre code dans le projet.</span><span class="sxs-lookup"><span data-stu-id="fe714-148">Select **src** > **main** > **scala** to open your code in the project.</span></span> <span data-ttu-id="fe714-149">Cet exemple utilise le script **SparkCore_wasbloTest**.</span><span class="sxs-lookup"><span data-stu-id="fe714-149">This example uses the **SparkCore_wasbloTest** script.</span></span>

5. <span data-ttu-id="fe714-150">Pour accéder au menu **Modifier les configurations**, sélectionnez l’icône dans le coin supérieur droit.</span><span class="sxs-lookup"><span data-stu-id="fe714-150">To access the **Edit Configurations** menu, select the icon in the upper-right corner.</span></span> <span data-ttu-id="fe714-151">Dans ce menu, vous pouvez créer ou modifier les configurations pour le débogage à distance.</span><span class="sxs-lookup"><span data-stu-id="fe714-151">From this menu, you can create or edit the configurations for remote debugging.</span></span>

   ![Modifier les configurations](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-edit-configurations.png) 

6. <span data-ttu-id="fe714-153">Dans la boîte de dialogue **Run/Debug Configurations** (Exécuter/Déboguer les configurations) sélectionnez le signe plus (**+**).</span><span class="sxs-lookup"><span data-stu-id="fe714-153">In the **Run/Debug Configurations** dialog box, select the plus sign (**+**).</span></span> <span data-ttu-id="fe714-154">Puis sélectionnez l’option **Soumettre un travail Spark**.</span><span class="sxs-lookup"><span data-stu-id="fe714-154">Then select the **Submit Spark Job** option.</span></span>

   ![Ajouter une nouvelle configuration](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-add-new-Configuration.png)
7. <span data-ttu-id="fe714-156">Entrez les informations sur le **Nom**, le **Cluster Spark** et le **Nom principal de la classe**.</span><span class="sxs-lookup"><span data-stu-id="fe714-156">Enter information for **Name**, **Spark cluster**, and **Main class name**.</span></span> <span data-ttu-id="fe714-157">Puis sélectionnez **Configuration avancée**.</span><span class="sxs-lookup"><span data-stu-id="fe714-157">Then select **Advanced configuration**.</span></span> 

   ![Exécuter le débogage des configurations](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-run-debug-configurations.png)

8. <span data-ttu-id="fe714-159">Dans la boîte de dialogue **Configuration avancée des soumissions Spark**, sélectionnez **Activer le débogage à distance Spark**.</span><span class="sxs-lookup"><span data-stu-id="fe714-159">In the **Spark Submission Advanced Configuration** dialog box, select **Enable Spark remote debug**.</span></span> <span data-ttu-id="fe714-160">Entrez le nom d’utilisateur SSH, puis entrez un mot de passe ou utilisez un fichier de clé privée.</span><span class="sxs-lookup"><span data-stu-id="fe714-160">Enter the SSH username, and then enter a password or use a private key file.</span></span> <span data-ttu-id="fe714-161">Pour enregistrer la configuration, sélectionnez **OK**.</span><span class="sxs-lookup"><span data-stu-id="fe714-161">To save the configuration, select **OK**.</span></span>

   ![Activer le débogage à distance Spark](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-enable-spark-remote-debug.png)

9. <span data-ttu-id="fe714-163">La configuration est maintenant enregistrée avec le nom fourni.</span><span class="sxs-lookup"><span data-stu-id="fe714-163">The configuration is now saved with the name you provided.</span></span> <span data-ttu-id="fe714-164">Pour afficher les détails de configuration, sélectionnez le nom de configuration.</span><span class="sxs-lookup"><span data-stu-id="fe714-164">To view the configuration details, select the configuration name.</span></span> <span data-ttu-id="fe714-165">Pour apporter des modifications, sélectionnez **Modifier les configurations**.</span><span class="sxs-lookup"><span data-stu-id="fe714-165">To make changes, select **Edit Configurations**.</span></span> 

10. <span data-ttu-id="fe714-166">Une fois le paramétrage des configurations terminé, vous pouvez exécuter le projet sur le cluster à distance ou effectuer un débogage à distance.</span><span class="sxs-lookup"><span data-stu-id="fe714-166">After you complete the configurations settings, you can run the project against the remote cluster or perform remote debugging.</span></span>

## <a name="learn-how-to-perform-remote-debugging"></a><span data-ttu-id="fe714-167">Apprendre à effectuer un débogage à distance</span><span class="sxs-lookup"><span data-stu-id="fe714-167">Learn how to perform remote debugging</span></span>
### <a name="scenario-1-perform-remote-run"></a><span data-ttu-id="fe714-168">Scénario 1 : effectuer une exécution à distance</span><span class="sxs-lookup"><span data-stu-id="fe714-168">Scenario 1: Perform remote run</span></span>

<span data-ttu-id="fe714-169">Dans cette section, nous vous montrons comment déboguer des pilotes et des exécuteurs.</span><span class="sxs-lookup"><span data-stu-id="fe714-169">In this section, we show you how to debug drivers and executors.</span></span>

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
        /** Tracks the total query count and number of aggregate bytes for a particular group. */
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


1. <span data-ttu-id="fe714-170">Configurez des points de rupture, puis sélectionnez l’icône **Déboguer**.</span><span class="sxs-lookup"><span data-stu-id="fe714-170">Set up breaking points, and then select the **Debug** icon.</span></span>

   ![Sélectionner l’icône de débogage](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-debug-icon.png)

2. <span data-ttu-id="fe714-172">Quand l’exécution du programme atteint le point de rupture, un onglet **Pilote** et deux onglets **Exécuteur** s’affichent dans le volet **Débogueur**.</span><span class="sxs-lookup"><span data-stu-id="fe714-172">When the program execution reaches the breaking point, you see a **Driver** tab and two **Executor** tabs in the **Debugger** pane.</span></span> <span data-ttu-id="fe714-173">Sélectionnez l’icône **Reprendre le programme** pour continuer à exécuter le code ; le point de rupture suivant est alors atteint et l’onglet **Exécuteur** correspondant est sélectionné. Vous pouvez consulter les journaux d’exécution sous l’onglet **Console** correspondant.</span><span class="sxs-lookup"><span data-stu-id="fe714-173">Select the **Resume Program** icon to continue running the code, which then reaches the next breakpoint and focuses on the corresponding **Executor** tab. You can review the execution logs on the corresponding **Console** tab.</span></span>

   ![Onglet Débogage](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-debugger-tab.png)

### <a name="scenario-2-perform-remote-debugging-and-bug-fixing"></a><span data-ttu-id="fe714-175">Scénario 2 : effectuer un débogage à distance et une résolution des bogues</span><span class="sxs-lookup"><span data-stu-id="fe714-175">Scenario 2: Perform remote debugging and bug fixing</span></span>
<span data-ttu-id="fe714-176">Dans cette section, nous vous indiquons comment mettre à jour dynamiquement la valeur de la variable à l’aide de la fonctionnalité de débogage IntelliJ pour une résolution simple.</span><span class="sxs-lookup"><span data-stu-id="fe714-176">In this section, we show you how to dynamically update the variable value by using the IntelliJ debugging capability for a simple fix.</span></span> <span data-ttu-id="fe714-177">Dans l’exemple de code suivant, une exception est levée car le fichier cible existe déjà.</span><span class="sxs-lookup"><span data-stu-id="fe714-177">In the following code example, an exception is thrown because the target file already exists.</span></span>
  
        import org.apache.spark.SparkConf
        import org.apache.spark.SparkContext

        object SparkCore_WasbIOTest {
          def main(arg: Array[String]): Unit = {
            val conf = new SparkConf().setAppName("SparkCore_WasbIOTest")
            val sc = new SparkContext(conf)
            val rdd = sc.textFile("wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")

            // Find the rows that have only one digit in the sixth column.
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


#### <a name="to-perform-remote-debugging-and-bug-fixing"></a><span data-ttu-id="fe714-178">Pour effectuer un débogage à distance et une résolution des bogues</span><span class="sxs-lookup"><span data-stu-id="fe714-178">To perform remote debugging and bug fixing</span></span>
1. <span data-ttu-id="fe714-179">Configurez deux points de rupture, puis sélectionnez l’icône **Déboguer** pour démarrer le processus de débogage à distance.</span><span class="sxs-lookup"><span data-stu-id="fe714-179">Set up two breaking points, and then select the **Debug** icon to start the remote debugging process.</span></span>

2. <span data-ttu-id="fe714-180">Le code s’arrête au premier point de rupture et les informations sur les paramètres et les variables s’affichent dans le volet **Variable**.</span><span class="sxs-lookup"><span data-stu-id="fe714-180">The code stops at the first breaking point, and the parameter and variable information are shown in the **Variables** pane.</span></span> 

3. <span data-ttu-id="fe714-181">Sélectionnez l’icône **Reprendre le programme** pour continuer.</span><span class="sxs-lookup"><span data-stu-id="fe714-181">Select the **Resume Program** icon to continue.</span></span> <span data-ttu-id="fe714-182">Le code s’arrête au deuxième point.</span><span class="sxs-lookup"><span data-stu-id="fe714-182">The code stops at the second point.</span></span> <span data-ttu-id="fe714-183">L’exception est interceptée comme prévu.</span><span class="sxs-lookup"><span data-stu-id="fe714-183">The exception is caught as expected.</span></span>

  ![Lever l’erreur](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-throw-error.png) 

4. <span data-ttu-id="fe714-185">Resélectionnez l’icône **Reprendre le programme**.</span><span class="sxs-lookup"><span data-stu-id="fe714-185">Select the **Resume Program** icon again.</span></span> <span data-ttu-id="fe714-186">La fenêtre **Soumission HDInsight Spark** affiche une erreur d’exécution de tâche.</span><span class="sxs-lookup"><span data-stu-id="fe714-186">The **HDInsight Spark Submission** window displays a "job run failed" error.</span></span>

  ![Soumission de l’erreur](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-error-submission.png) 

5. <span data-ttu-id="fe714-188">Pour mettre à jour dynamiquement la valeur de la variable à l’aide de la fonctionnalité de débogage IntelliJ, resélectionnez **Déboguer**.</span><span class="sxs-lookup"><span data-stu-id="fe714-188">To dynamically update the variable value by using the IntelliJ debugging capability, select **Debug** again.</span></span> <span data-ttu-id="fe714-189">Le volet **Variables** réapparaît.</span><span class="sxs-lookup"><span data-stu-id="fe714-189">The **Variables** pane appears again.</span></span> 

6. <span data-ttu-id="fe714-190">Cliquez avec le bouton droit de la cible de l’onglet **Déboguer**, puis sélectionnez **Définir la valeur**.</span><span class="sxs-lookup"><span data-stu-id="fe714-190">Right-click the target on the **Debug** tab, and then select **Set Value**.</span></span> <span data-ttu-id="fe714-191">Ensuite, entrez une nouvelle valeur pour la variable.</span><span class="sxs-lookup"><span data-stu-id="fe714-191">Next, enter a new value for the variable.</span></span> <span data-ttu-id="fe714-192">Puis sélectionnez **Entrer** pour enregistrer la valeur.</span><span class="sxs-lookup"><span data-stu-id="fe714-192">Then select **Enter** to save the value.</span></span> 

  ![Définir la valeur](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-set-value.png) 

7. <span data-ttu-id="fe714-194">Sélectionnez l’icône **Reprendre le programme** pour continuer à exécuter le programme.</span><span class="sxs-lookup"><span data-stu-id="fe714-194">Select the **Resume Program** icon to continue to run the program.</span></span> <span data-ttu-id="fe714-195">Cette fois-ci, aucune exception n’est interceptée.</span><span class="sxs-lookup"><span data-stu-id="fe714-195">This time, no exception is caught.</span></span> <span data-ttu-id="fe714-196">Vous pouvez voir que le projet s’exécute correctement sans aucune exception.</span><span class="sxs-lookup"><span data-stu-id="fe714-196">You can see that the project runs successfully without any exceptions.</span></span>

  ![Déboguer sans exception](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-debug-without-exception.png)

## <span data-ttu-id="fe714-198"><a name="seealso"></a>Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="fe714-198"><a name="seealso"></a>Next steps</span></span>
* [<span data-ttu-id="fe714-199">Vue d’ensemble : Apache Spark sur Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="fe714-199">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="demo"></a><span data-ttu-id="fe714-200">Démonstration</span><span class="sxs-lookup"><span data-stu-id="fe714-200">Demo</span></span>
* <span data-ttu-id="fe714-201">Créez un projet Scala (vidéo) : [Créer des applications Scala Spark](https://channel9.msdn.com/Series/AzureDataLake/Create-Spark-Applications-with-the-Azure-Toolkit-for-IntelliJ)</span><span class="sxs-lookup"><span data-stu-id="fe714-201">Create Scala project (video): [Create Spark Scala Applications](https://channel9.msdn.com/Series/AzureDataLake/Create-Spark-Applications-with-the-Azure-Toolkit-for-IntelliJ)</span></span>
* <span data-ttu-id="fe714-202">Débogage à distance (vidéo) : [Utiliser le kit de ressources Azure pour IntelliJ afin de déboguer des applications Spark à distance sur un cluster HDInsight](https://channel9.msdn.com/Series/AzureDataLake/Debug-HDInsight-Spark-Applications-with-Azure-Toolkit-for-IntelliJ)</span><span class="sxs-lookup"><span data-stu-id="fe714-202">Remote debug (video): [Use Azure Toolkit for IntelliJ to debug Spark applications remotely on an HDInsight cluster](https://channel9.msdn.com/Series/AzureDataLake/Debug-HDInsight-Spark-Applications-with-Azure-Toolkit-for-IntelliJ)</span></span>

### <a name="scenarios"></a><span data-ttu-id="fe714-203">Scénarios</span><span class="sxs-lookup"><span data-stu-id="fe714-203">Scenarios</span></span>
* [<span data-ttu-id="fe714-204">Spark avec BI : effectuez une analyse interactive des données à l’aide de Spark dans HDInsight avec des outils BI</span><span class="sxs-lookup"><span data-stu-id="fe714-204">Spark with BI: Perform interactive data analysis by using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="fe714-205">Spark avec Machine Learning : Utiliser Spark dans HDInsight pour l’analyse de la température de bâtiments à l’aide de données HVAC</span><span class="sxs-lookup"><span data-stu-id="fe714-205">Spark with Machine Learning: Use Spark in HDInsight to analyze building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="fe714-206">Spark avec Machine Learning : Utiliser Spark dans HDInsight pour prédire les résultats de l’inspection des aliments</span><span class="sxs-lookup"><span data-stu-id="fe714-206">Spark with Machine Learning: Use Spark in HDInsight to predict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="fe714-207">Streaming Spark : Utiliser Spark dans HDInsight pour créer des applications de diffusion en continu en temps réel</span><span class="sxs-lookup"><span data-stu-id="fe714-207">Spark Streaming: Use Spark in HDInsight to build real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)
* [<span data-ttu-id="fe714-208">Analyse des journaux de site web à l’aide de Spark dans HDInsight</span><span class="sxs-lookup"><span data-stu-id="fe714-208">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a><span data-ttu-id="fe714-209">Créer et exécuter des applications</span><span class="sxs-lookup"><span data-stu-id="fe714-209">Create and run applications</span></span>
* [<span data-ttu-id="fe714-210">Créer une application autonome avec Scala</span><span class="sxs-lookup"><span data-stu-id="fe714-210">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="fe714-211">Exécuter des tâches à distance avec Livy sur un cluster Spark</span><span class="sxs-lookup"><span data-stu-id="fe714-211">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="fe714-212">Outils et extensions</span><span class="sxs-lookup"><span data-stu-id="fe714-212">Tools and extensions</span></span>
* [<span data-ttu-id="fe714-213">Utiliser le kit de ressources Azure pour IntelliJ afin de créer des applications Spark pour un cluster HDInsight</span><span class="sxs-lookup"><span data-stu-id="fe714-213">Use Azure Toolkit for IntelliJ to create Spark applications for an HDInsight cluster</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="fe714-214">Utiliser le kit de ressources Azure pour IntelliJ pour déboguer des applications Spark à distance via VPN</span><span class="sxs-lookup"><span data-stu-id="fe714-214">Use Azure Toolkit for IntelliJ to debug Spark applications remotely through VPN</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="fe714-215">Utiliser HDInsight Tools pour IntelliJ avec Hortonworks Sandbox</span><span class="sxs-lookup"><span data-stu-id="fe714-215">Use HDInsight Tools for IntelliJ with Hortonworks Sandbox</span></span>](hdinsight-tools-for-intellij-with-hortonworks-sandbox.md)
* [<span data-ttu-id="fe714-216">Utiliser HDInsight Tools dans le kit de ressources Azure pour Eclipse pour créer des applications Spark</span><span class="sxs-lookup"><span data-stu-id="fe714-216">Use HDInsight Tools in Azure Toolkit for Eclipse to create Spark applications</span></span>](hdinsight-apache-spark-eclipse-tool-plugin.md)
* [<span data-ttu-id="fe714-217">Utiliser des bloc-notes Zeppelin avec un cluster Spark sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="fe714-217">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="fe714-218">Noyaux disponibles pour le bloc-notes Jupyter dans le cluster Spark pour HDInsight</span><span class="sxs-lookup"><span data-stu-id="fe714-218">Kernels available for Jupyter notebook in the Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="fe714-219">Utiliser des packages externes avec les blocs-notes Jupyter</span><span class="sxs-lookup"><span data-stu-id="fe714-219">Use external packages with Jupyter notebooks</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="fe714-220">Install Jupyter on your computer and connect to an HDInsight Spark cluster (Installer Jupyter sur un ordinateur et se connecter au cluster Spark sur HDInsight)</span><span class="sxs-lookup"><span data-stu-id="fe714-220">Install Jupyter on your computer and connect to an HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a><span data-ttu-id="fe714-221">Gestion des ressources</span><span class="sxs-lookup"><span data-stu-id="fe714-221">Manage resources</span></span>
* [<span data-ttu-id="fe714-222">Gérer les ressources du cluster Apache Spark dans Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="fe714-222">Manage resources for the Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="fe714-223">Suivi et débogage des tâches en cours d’exécution sur un cluster Apache Spark dans HDInsight</span><span class="sxs-lookup"><span data-stu-id="fe714-223">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)
