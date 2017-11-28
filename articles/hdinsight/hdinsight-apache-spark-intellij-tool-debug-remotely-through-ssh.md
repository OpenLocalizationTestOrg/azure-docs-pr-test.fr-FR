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
# <a name="debug-spark-applications-on-an-hdinsight-cluster-with-azure-toolkit-for-intellij-through-ssh"></a><span data-ttu-id="2c45f-104">Déboguez des applications Spark sur un cluster HDInsight avec le kit de ressources Azure pour IntelliJ via SSH</span><span class="sxs-lookup"><span data-stu-id="2c45f-104">Debug Spark applications on an HDInsight cluster with Azure Toolkit for IntelliJ through SSH</span></span>

<span data-ttu-id="2c45f-105">Cet article fournit des instructions sur la façon de toouse outils HDInsight dans la boîte à outils Azure pour les applications de toodebug IntelliJ à distance sur un cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="2c45f-105">This article provides step-by-step guidance on how toouse HDInsight Tools in Azure Toolkit for IntelliJ toodebug applications remotely on an HDInsight cluster.</span></span> <span data-ttu-id="2c45f-106">toodebug votre projet, vous pouvez également afficher hello [applications déboguer HDInsight Spark avec la boîte à outils Azure pour IntelliJ](https://channel9.msdn.com/Series/AzureDataLake/Debug-HDInsight-Spark-Applications-with-Azure-Toolkit-for-IntelliJ) vidéo.</span><span class="sxs-lookup"><span data-stu-id="2c45f-106">toodebug your project, you can also view hello [Debug HDInsight Spark applications with Azure Toolkit for IntelliJ](https://channel9.msdn.com/Series/AzureDataLake/Debug-HDInsight-Spark-Applications-with-Azure-Toolkit-for-IntelliJ) video.</span></span>

<span data-ttu-id="2c45f-107">**Configuration requise**</span><span class="sxs-lookup"><span data-stu-id="2c45f-107">**Prerequisites**</span></span>

* <span data-ttu-id="2c45f-108">**Outils HDInsight dans le kit de ressources Azure pour IntelliJ**.</span><span class="sxs-lookup"><span data-stu-id="2c45f-108">**HDInsight Tools in Azure Toolkit for IntelliJ**.</span></span> <span data-ttu-id="2c45f-109">Cet outil fait partie du kit de ressources Azure pour IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="2c45f-109">This tool is part of Azure Toolkit for IntelliJ.</span></span> <span data-ttu-id="2c45f-110">Pour plus d’informations, consultez [Installation du kit de ressources Azure pour IntelliJ](https://docs.microsoft.com/en-us/azure/azure-toolkit-for-intellij-installation).</span><span class="sxs-lookup"><span data-stu-id="2c45f-110">For more information, see [Install Azure Toolkit for IntelliJ](https://docs.microsoft.com/en-us/azure/azure-toolkit-for-intellij-installation).</span></span>
* <span data-ttu-id="2c45f-111">**Kit de ressources Azure pour IntelliJ**.</span><span class="sxs-lookup"><span data-stu-id="2c45f-111">**Azure Toolkit for IntelliJ**.</span></span> <span data-ttu-id="2c45f-112">Utilisez ces applications de Spark toocreate Kit de ressources pour un cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="2c45f-112">Use this toolkit toocreate Spark applications for an HDInsight cluster.</span></span> <span data-ttu-id="2c45f-113">Pour plus d’informations, suivez les instructions de hello dans [utilisez Azure Toolkit pour les applications de Spark IntelliJ toocreate pour un cluster HDInsight](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-apache-spark-intellij-tool-plugin).</span><span class="sxs-lookup"><span data-stu-id="2c45f-113">For more information, follow hello instructions in [Use Azure Toolkit for IntelliJ toocreate Spark applications for an HDInsight cluster](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-apache-spark-intellij-tool-plugin).</span></span>
* <span data-ttu-id="2c45f-114">**Service HDInsight SSH avec gestion de nom d’utilisateur et de mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="2c45f-114">**HDInsight SSH service with username and password management**.</span></span> <span data-ttu-id="2c45f-115">Pour plus d’informations, consultez [connecter tooHDInsight (Hadoop) à l’aide de SSH](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-linux-use-ssh-unix) et [utiliser SSH tunneling tooaccess Ambari web de l’interface utilisateur, JobHistory, NameNode, Oozie et autres interfaces utilisateur web](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-linux-ambari-ssh-tunnel).</span><span class="sxs-lookup"><span data-stu-id="2c45f-115">For more information, see [Connect tooHDInsight (Hadoop) by using SSH](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-linux-use-ssh-unix) and [Use SSH tunneling tooaccess Ambari web UI, JobHistory, NameNode, Oozie, and other web UIs](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-linux-ambari-ssh-tunnel).</span></span> 
 

## <a name="create-a-spark-scala-application-and-configure-it-for-remote-debugging"></a><span data-ttu-id="2c45f-116">Créer une application Spark Scala et la configurer pour le débogage à distance</span><span class="sxs-lookup"><span data-stu-id="2c45f-116">Create a Spark Scala application and configure it for remote debugging</span></span>

1. <span data-ttu-id="2c45f-117">Démarrez IntelliJ IDEA et créez un projet.</span><span class="sxs-lookup"><span data-stu-id="2c45f-117">Start IntelliJ IDEA, and then create a project.</span></span> <span data-ttu-id="2c45f-118">Bonjour **nouveau projet** boîte de dialogue zone, hello suivant :</span><span class="sxs-lookup"><span data-stu-id="2c45f-118">In hello **New Project** dialog box, do hello following:</span></span>

   <span data-ttu-id="2c45f-119">a.</span><span class="sxs-lookup"><span data-stu-id="2c45f-119">a.</span></span> <span data-ttu-id="2c45f-120">Sélectionnez **HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="2c45f-120">Select **HDInsight**.</span></span> 

   <span data-ttu-id="2c45f-121">b.</span><span class="sxs-lookup"><span data-stu-id="2c45f-121">b.</span></span> <span data-ttu-id="2c45f-122">Sélectionnez un modèle Java ou Scala en fonction de vos préférences.</span><span class="sxs-lookup"><span data-stu-id="2c45f-122">Select a Java or Scala template based on your preference.</span></span> <span data-ttu-id="2c45f-123">Sélectionnez entre hello options suivantes :</span><span class="sxs-lookup"><span data-stu-id="2c45f-123">Select between hello following options:</span></span>

      - <span data-ttu-id="2c45f-124">**Spark sur HDInsight (Scala)**</span><span class="sxs-lookup"><span data-stu-id="2c45f-124">**Spark on HDInsight (Scala)**</span></span>

      - <span data-ttu-id="2c45f-125">**Spark sur HDInsight (Java)**</span><span class="sxs-lookup"><span data-stu-id="2c45f-125">**Spark on HDInsight (Java)**</span></span>

      - <span data-ttu-id="2c45f-126">**Spark sur exemple d’exécution de cluster HDInsight (Scala)**</span><span class="sxs-lookup"><span data-stu-id="2c45f-126">**Spark on HDInsight Cluster Run Sample (Scala)**</span></span>

      <span data-ttu-id="2c45f-127">Cet exemple utilise un modèle **Spark sur exemple d’exécution de cluster HDInsight (Scala)**.</span><span class="sxs-lookup"><span data-stu-id="2c45f-127">This example uses a **Spark on HDInsight Cluster Run Sample (Scala)** template.</span></span>

   <span data-ttu-id="2c45f-128">c.</span><span class="sxs-lookup"><span data-stu-id="2c45f-128">c.</span></span> <span data-ttu-id="2c45f-129">Bonjour **outil de génération** , sélectionnez une des hello suivant, selon le besoin de tooyour :</span><span class="sxs-lookup"><span data-stu-id="2c45f-129">In hello **Build tool** list, select either of hello following, according tooyour need:</span></span>

      - <span data-ttu-id="2c45f-130">**Maven**, pour la prise en charge de l’Assistant de création de projets Scala</span><span class="sxs-lookup"><span data-stu-id="2c45f-130">**Maven**, for Scala project-creation wizard support</span></span>

      -  <span data-ttu-id="2c45f-131">**SBT**, pour la gestion des dépendances de hello et la création de projet de Scala hello</span><span class="sxs-lookup"><span data-stu-id="2c45f-131">**SBT**, for managing hello dependencies and building for hello Scala project</span></span> 

      ![Créer un projet de débogage](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-create-projectfor-debug-remotely.png)

   <span data-ttu-id="2c45f-133">d.</span><span class="sxs-lookup"><span data-stu-id="2c45f-133">d.</span></span> <span data-ttu-id="2c45f-134">Sélectionnez **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="2c45f-134">Select **Next**.</span></span>     
 
3. <span data-ttu-id="2c45f-135">Bonjour suivant **nouveau projet** fenêtre, hello suivant :</span><span class="sxs-lookup"><span data-stu-id="2c45f-135">In hello next **New Project** window, do hello following:</span></span>

   ![Sélectionnez hello Spark SDK](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-new-project.png)

   <span data-ttu-id="2c45f-137">a.</span><span class="sxs-lookup"><span data-stu-id="2c45f-137">a.</span></span> <span data-ttu-id="2c45f-138">Entrez un nom de projet et un emplacement de projet.</span><span class="sxs-lookup"><span data-stu-id="2c45f-138">Enter a project name and project location.</span></span>

   <span data-ttu-id="2c45f-139">b.</span><span class="sxs-lookup"><span data-stu-id="2c45f-139">b.</span></span> <span data-ttu-id="2c45f-140">Bonjour **projet SDK** la liste déroulante, sélectionnez **Java 1.8** pour **nouvelles 2.x** de cluster ou sélectionnez **Java 1.7** pour **Spark 1. x** cluster.</span><span class="sxs-lookup"><span data-stu-id="2c45f-140">In hello **Project SDK** drop-down list, select **Java 1.8** for **Spark 2.x** cluster or select **Java 1.7** for **Spark 1.x** cluster.</span></span>

   <span data-ttu-id="2c45f-141">c.</span><span class="sxs-lookup"><span data-stu-id="2c45f-141">c.</span></span> <span data-ttu-id="2c45f-142">Bonjour **Spark Version** la liste déroulante, Assistant de création de projet Scala hello intègre version correcte de hello pour le Kit de développement logiciel Spark et Scala SDK.</span><span class="sxs-lookup"><span data-stu-id="2c45f-142">In hello **Spark Version** drop-down list, hello Scala project creation wizard integrates hello correct version for Spark SDK and Scala SDK.</span></span> <span data-ttu-id="2c45f-143">Si la version du cluster spark hello est antérieure à la version 2.0, sélectionnez **nouvelles 1.x**.</span><span class="sxs-lookup"><span data-stu-id="2c45f-143">If hello spark cluster version is earlier than 2.0, select **Spark 1.x**.</span></span> <span data-ttu-id="2c45f-144">Sinon, sélectionnez **Spark 2.x.**</span><span class="sxs-lookup"><span data-stu-id="2c45f-144">Otherwise, select **Spark 2.x.**</span></span> <span data-ttu-id="2c45f-145">La version utilisée dans cet exemple est **Spark 2.0.2 (Scala 2.11.8)**.</span><span class="sxs-lookup"><span data-stu-id="2c45f-145">This example uses **Spark 2.0.2 (Scala 2.11.8)**.</span></span>

   <span data-ttu-id="2c45f-146">d.</span><span class="sxs-lookup"><span data-stu-id="2c45f-146">d.</span></span> <span data-ttu-id="2c45f-147">Sélectionnez **Terminer**.</span><span class="sxs-lookup"><span data-stu-id="2c45f-147">Select **Finish**.</span></span>

4. <span data-ttu-id="2c45f-148">Sélectionnez **src** > **principal** > **scala** tooopen votre code dans un projet de hello.</span><span class="sxs-lookup"><span data-stu-id="2c45f-148">Select **src** > **main** > **scala** tooopen your code in hello project.</span></span> <span data-ttu-id="2c45f-149">Cet exemple utilise hello **SparkCore_wasbloTest** script.</span><span class="sxs-lookup"><span data-stu-id="2c45f-149">This example uses hello **SparkCore_wasbloTest** script.</span></span>

5. <span data-ttu-id="2c45f-150">tooaccess hello **modifier les Configurations** menu, icône hello select dans le coin supérieur droit de hello.</span><span class="sxs-lookup"><span data-stu-id="2c45f-150">tooaccess hello **Edit Configurations** menu, select hello icon in hello upper-right corner.</span></span> <span data-ttu-id="2c45f-151">Dans ce menu, vous pouvez créer ou modifier des configurations hello pour le débogage distant.</span><span class="sxs-lookup"><span data-stu-id="2c45f-151">From this menu, you can create or edit hello configurations for remote debugging.</span></span>

   ![Modifier les configurations](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-edit-configurations.png) 

6. <span data-ttu-id="2c45f-153">Bonjour **Configurations d’exécution/débogage** boîte de dialogue, sélectionnez hello plus signe (**+**).</span><span class="sxs-lookup"><span data-stu-id="2c45f-153">In hello **Run/Debug Configurations** dialog box, select hello plus sign (**+**).</span></span> <span data-ttu-id="2c45f-154">Puis sélectionnez hello **soumettre un travail Spark** option.</span><span class="sxs-lookup"><span data-stu-id="2c45f-154">Then select hello **Submit Spark Job** option.</span></span>

   ![Ajouter une nouvelle configuration](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-add-new-Configuration.png)
7. <span data-ttu-id="2c45f-156">Entrez les informations sur le **Nom**, le **Cluster Spark** et le **Nom principal de la classe**.</span><span class="sxs-lookup"><span data-stu-id="2c45f-156">Enter information for **Name**, **Spark cluster**, and **Main class name**.</span></span> <span data-ttu-id="2c45f-157">Puis sélectionnez **Configuration avancée**.</span><span class="sxs-lookup"><span data-stu-id="2c45f-157">Then select **Advanced configuration**.</span></span> 

   ![Exécuter le débogage des configurations](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-run-debug-configurations.png)

8. <span data-ttu-id="2c45f-159">Bonjour **Spark soumission Advanced Configuration** boîte de dialogue, sélectionnez **débogage distant d’activer les Spark**.</span><span class="sxs-lookup"><span data-stu-id="2c45f-159">In hello **Spark Submission Advanced Configuration** dialog box, select **Enable Spark remote debug**.</span></span> <span data-ttu-id="2c45f-160">Entrez le nom d’utilisateur de hello SSH, puis entrez un mot de passe ou utiliser un fichier de clé privée.</span><span class="sxs-lookup"><span data-stu-id="2c45f-160">Enter hello SSH username, and then enter a password or use a private key file.</span></span> <span data-ttu-id="2c45f-161">configuration de hello toosave, sélectionnez **OK**.</span><span class="sxs-lookup"><span data-stu-id="2c45f-161">toosave hello configuration, select **OK**.</span></span>

   ![Activer le débogage à distance Spark](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-enable-spark-remote-debug.png)

9. <span data-ttu-id="2c45f-163">configuration de Hello est désormais enregistrée avec nom hello fourni.</span><span class="sxs-lookup"><span data-stu-id="2c45f-163">hello configuration is now saved with hello name you provided.</span></span> <span data-ttu-id="2c45f-164">Détails de configuration hello tooview, nom de la configuration sélectionnez hello.</span><span class="sxs-lookup"><span data-stu-id="2c45f-164">tooview hello configuration details, select hello configuration name.</span></span> <span data-ttu-id="2c45f-165">toomake change, sélectionnez **modifier les Configurations de**.</span><span class="sxs-lookup"><span data-stu-id="2c45f-165">toomake changes, select **Edit Configurations**.</span></span> 

10. <span data-ttu-id="2c45f-166">Après avoir terminé les paramètres de configuration hello, vous pouvez exécuter des projets de hello sur un cluster distant de hello ou effectuer un débogage à distance.</span><span class="sxs-lookup"><span data-stu-id="2c45f-166">After you complete hello configurations settings, you can run hello project against hello remote cluster or perform remote debugging.</span></span>

## <a name="learn-how-tooperform-remote-debugging"></a><span data-ttu-id="2c45f-167">Découvrez comment tooperform le débogage distant</span><span class="sxs-lookup"><span data-stu-id="2c45f-167">Learn how tooperform remote debugging</span></span>
### <a name="scenario-1-perform-remote-run"></a><span data-ttu-id="2c45f-168">Scénario 1 : effectuer une exécution à distance</span><span class="sxs-lookup"><span data-stu-id="2c45f-168">Scenario 1: Perform remote run</span></span>

<span data-ttu-id="2c45f-169">Dans cette section, nous vous indiquons comment toodebug exécuteurs et des pilotes.</span><span class="sxs-lookup"><span data-stu-id="2c45f-169">In this section, we show you how toodebug drivers and executors.</span></span>

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


1. <span data-ttu-id="2c45f-170">Définir des points de saut, puis sélectionnez hello **déboguer** icône.</span><span class="sxs-lookup"><span data-stu-id="2c45f-170">Set up breaking points, and then select hello **Debug** icon.</span></span>

   ![Sélectionnez l’icône de débogage hello](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-debug-icon.png)

2. <span data-ttu-id="2c45f-172">Lorsque l’exécution du programme hello atteint un point de rupture hello, vous voyez un **pilote** onglet et deux **exécuteur** onglets Bonjour **débogueur** volet.</span><span class="sxs-lookup"><span data-stu-id="2c45f-172">When hello program execution reaches hello breaking point, you see a **Driver** tab and two **Executor** tabs in hello **Debugger** pane.</span></span> <span data-ttu-id="2c45f-173">Sélectionnez hello **Resume programme** toocontinue icône exécuter le code hello, qui ensuite atteint le point d’arrêt suivant de hello et se concentre sur hello correspondant **exécuteur** onglet. Vous pouvez consulter les journaux d’exécution hello sur hello correspondant **Console** onglet.</span><span class="sxs-lookup"><span data-stu-id="2c45f-173">Select hello **Resume Program** icon toocontinue running hello code, which then reaches hello next breakpoint and focuses on hello corresponding **Executor** tab. You can review hello execution logs on hello corresponding **Console** tab.</span></span>

   ![Onglet Débogage](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-debugger-tab.png)

### <a name="scenario-2-perform-remote-debugging-and-bug-fixing"></a><span data-ttu-id="2c45f-175">Scénario 2 : effectuer un débogage à distance et une résolution des bogues</span><span class="sxs-lookup"><span data-stu-id="2c45f-175">Scenario 2: Perform remote debugging and bug fixing</span></span>
<span data-ttu-id="2c45f-176">Dans cette section, nous vous indiquons comment toodynamically mise à jour hello valeur de la variable à l’aide de hello IntelliJ fonctionnalité pour une solution simple de débogage.</span><span class="sxs-lookup"><span data-stu-id="2c45f-176">In this section, we show you how toodynamically update hello variable value by using hello IntelliJ debugging capability for a simple fix.</span></span> <span data-ttu-id="2c45f-177">Bonjour exemple de code suivant, une exception est levée, car le fichier hello cible existe déjà.</span><span class="sxs-lookup"><span data-stu-id="2c45f-177">In hello following code example, an exception is thrown because hello target file already exists.</span></span>
  
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


#### <a name="tooperform-remote-debugging-and-bug-fixing"></a><span data-ttu-id="2c45f-178">débogage distant tooperform et résolution des bogues</span><span class="sxs-lookup"><span data-stu-id="2c45f-178">tooperform remote debugging and bug fixing</span></span>
1. <span data-ttu-id="2c45f-179">Configurer les deux points de rupture, puis sélectionnez hello **déboguer** hello de toostart icône processus de débogage distant.</span><span class="sxs-lookup"><span data-stu-id="2c45f-179">Set up two breaking points, and then select hello **Debug** icon toostart hello remote debugging process.</span></span>

2. <span data-ttu-id="2c45f-180">code de Hello s’arrête au premier point de rupture hello et paramètre hello et des informations sur les variables sont affichés dans hello **Variables** volet.</span><span class="sxs-lookup"><span data-stu-id="2c45f-180">hello code stops at hello first breaking point, and hello parameter and variable information are shown in hello **Variables** pane.</span></span> 

3. <span data-ttu-id="2c45f-181">Sélectionnez hello **Resume programme** toocontinue d’icône.</span><span class="sxs-lookup"><span data-stu-id="2c45f-181">Select hello **Resume Program** icon toocontinue.</span></span> <span data-ttu-id="2c45f-182">code de Hello s’arrête au deuxième point de hello.</span><span class="sxs-lookup"><span data-stu-id="2c45f-182">hello code stops at hello second point.</span></span> <span data-ttu-id="2c45f-183">exception de Hello est interceptée comme prévu.</span><span class="sxs-lookup"><span data-stu-id="2c45f-183">hello exception is caught as expected.</span></span>

  ![Lever l’erreur](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-throw-error.png) 

4. <span data-ttu-id="2c45f-185">Sélectionnez hello **Resume programme** icône Nouveau.</span><span class="sxs-lookup"><span data-stu-id="2c45f-185">Select hello **Resume Program** icon again.</span></span> <span data-ttu-id="2c45f-186">Hello **HDInsight Spark soumission** affiche une erreur « Échec de l’exécution de la tâche ».</span><span class="sxs-lookup"><span data-stu-id="2c45f-186">hello **HDInsight Spark Submission** window displays a "job run failed" error.</span></span>

  ![Soumission de l’erreur](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-error-submission.png) 

5. <span data-ttu-id="2c45f-188">toodynamically mise à jour hello valeur de la variable à l’aide des fonctionnalités de débogage IntelliJ hello, sélectionnez **déboguer** à nouveau.</span><span class="sxs-lookup"><span data-stu-id="2c45f-188">toodynamically update hello variable value by using hello IntelliJ debugging capability, select **Debug** again.</span></span> <span data-ttu-id="2c45f-189">Hello **Variables** volet s’affiche à nouveau.</span><span class="sxs-lookup"><span data-stu-id="2c45f-189">hello **Variables** pane appears again.</span></span> 

6. <span data-ttu-id="2c45f-190">Cible de hello avec le bouton droit sur hello **déboguer** onglet, puis sélectionnez **définir la valeur**.</span><span class="sxs-lookup"><span data-stu-id="2c45f-190">Right-click hello target on hello **Debug** tab, and then select **Set Value**.</span></span> <span data-ttu-id="2c45f-191">Ensuite, entrez une nouvelle valeur pour la variable de hello.</span><span class="sxs-lookup"><span data-stu-id="2c45f-191">Next, enter a new value for hello variable.</span></span> <span data-ttu-id="2c45f-192">Puis sélectionnez **entrée** valeur hello de toosave.</span><span class="sxs-lookup"><span data-stu-id="2c45f-192">Then select **Enter** toosave hello value.</span></span> 

  ![Définir la valeur](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-set-value.png) 

7. <span data-ttu-id="2c45f-194">Sélectionnez hello **Resume programme** programme de hello icône toocontinue toorun.</span><span class="sxs-lookup"><span data-stu-id="2c45f-194">Select hello **Resume Program** icon toocontinue toorun hello program.</span></span> <span data-ttu-id="2c45f-195">Cette fois-ci, aucune exception n’est interceptée.</span><span class="sxs-lookup"><span data-stu-id="2c45f-195">This time, no exception is caught.</span></span> <span data-ttu-id="2c45f-196">Vous pouvez voir que ce projet hello s’exécute correctement, sans aucune exception.</span><span class="sxs-lookup"><span data-stu-id="2c45f-196">You can see that hello project runs successfully without any exceptions.</span></span>

  ![Déboguer sans exception](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-debug-without-exception.png)

## <span data-ttu-id="2c45f-198"><a name="seealso"></a>Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="2c45f-198"><a name="seealso"></a>Next steps</span></span>
* [<span data-ttu-id="2c45f-199">Vue d’ensemble : Apache Spark sur Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="2c45f-199">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="demo"></a><span data-ttu-id="2c45f-200">Démonstration</span><span class="sxs-lookup"><span data-stu-id="2c45f-200">Demo</span></span>
* <span data-ttu-id="2c45f-201">Créez un projet Scala (vidéo) : [Créer des applications Scala Spark](https://channel9.msdn.com/Series/AzureDataLake/Create-Spark-Applications-with-the-Azure-Toolkit-for-IntelliJ)</span><span class="sxs-lookup"><span data-stu-id="2c45f-201">Create Scala project (video): [Create Spark Scala Applications](https://channel9.msdn.com/Series/AzureDataLake/Create-Spark-Applications-with-the-Azure-Toolkit-for-IntelliJ)</span></span>
* <span data-ttu-id="2c45f-202">Débogage distant (vidéo) : [utilisation Azure Toolkit pour les applications de Spark IntelliJ toodebug à distance sur un cluster HDInsight](https://channel9.msdn.com/Series/AzureDataLake/Debug-HDInsight-Spark-Applications-with-Azure-Toolkit-for-IntelliJ)</span><span class="sxs-lookup"><span data-stu-id="2c45f-202">Remote debug (video): [Use Azure Toolkit for IntelliJ toodebug Spark applications remotely on an HDInsight cluster](https://channel9.msdn.com/Series/AzureDataLake/Debug-HDInsight-Spark-Applications-with-Azure-Toolkit-for-IntelliJ)</span></span>

### <a name="scenarios"></a><span data-ttu-id="2c45f-203">Scénarios</span><span class="sxs-lookup"><span data-stu-id="2c45f-203">Scenarios</span></span>
* [<span data-ttu-id="2c45f-204">Spark avec BI : effectuez une analyse interactive des données à l’aide de Spark dans HDInsight avec des outils BI</span><span class="sxs-lookup"><span data-stu-id="2c45f-204">Spark with BI: Perform interactive data analysis by using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="2c45f-205">Spark avec Machine Learning : Spark utilisation dans tooanalyze HDInsight à l’aide des données HVAC de température de génération</span><span class="sxs-lookup"><span data-stu-id="2c45f-205">Spark with Machine Learning: Use Spark in HDInsight tooanalyze building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="2c45f-206">Spark avec Machine Learning : Spark utilisation dans résultats de l’inspection alimentaires toopredict HDInsight</span><span class="sxs-lookup"><span data-stu-id="2c45f-206">Spark with Machine Learning: Use Spark in HDInsight toopredict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="2c45f-207">Diffusion en continu de Spark : Spark utilisation dans les applications de diffusion en continu en temps réel toobuild HDInsight</span><span class="sxs-lookup"><span data-stu-id="2c45f-207">Spark Streaming: Use Spark in HDInsight toobuild real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)
* [<span data-ttu-id="2c45f-208">Analyse des journaux de site web à l’aide de Spark dans HDInsight</span><span class="sxs-lookup"><span data-stu-id="2c45f-208">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a><span data-ttu-id="2c45f-209">Créer et exécuter des applications</span><span class="sxs-lookup"><span data-stu-id="2c45f-209">Create and run applications</span></span>
* [<span data-ttu-id="2c45f-210">Créer une application autonome avec Scala</span><span class="sxs-lookup"><span data-stu-id="2c45f-210">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="2c45f-211">Exécuter des tâches à distance avec Livy sur un cluster Spark</span><span class="sxs-lookup"><span data-stu-id="2c45f-211">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="2c45f-212">Outils et extensions</span><span class="sxs-lookup"><span data-stu-id="2c45f-212">Tools and extensions</span></span>
* [<span data-ttu-id="2c45f-213">Utilisez la boîte à outils Azure pour les applications de Spark IntelliJ toocreate pour un cluster HDInsight</span><span class="sxs-lookup"><span data-stu-id="2c45f-213">Use Azure Toolkit for IntelliJ toocreate Spark applications for an HDInsight cluster</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="2c45f-214">Utilisez la boîte à outils Azure pour les applications de Spark IntelliJ toodebug à distance via le VPN</span><span class="sxs-lookup"><span data-stu-id="2c45f-214">Use Azure Toolkit for IntelliJ toodebug Spark applications remotely through VPN</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="2c45f-215">Utiliser HDInsight Tools pour IntelliJ avec Hortonworks Sandbox</span><span class="sxs-lookup"><span data-stu-id="2c45f-215">Use HDInsight Tools for IntelliJ with Hortonworks Sandbox</span></span>](hdinsight-tools-for-intellij-with-hortonworks-sandbox.md)
* [<span data-ttu-id="2c45f-216">Utilisez les outils HDInsight dans la boîte à outils Azure pour les applications de Spark toocreate Eclipse</span><span class="sxs-lookup"><span data-stu-id="2c45f-216">Use HDInsight Tools in Azure Toolkit for Eclipse toocreate Spark applications</span></span>](hdinsight-apache-spark-eclipse-tool-plugin.md)
* [<span data-ttu-id="2c45f-217">Utiliser des bloc-notes Zeppelin avec un cluster Spark sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="2c45f-217">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="2c45f-218">Cluster de noyaux disponibles pour le bloc-notes jupyter Bonjour Spark sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="2c45f-218">Kernels available for Jupyter notebook in hello Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="2c45f-219">Utiliser des packages externes avec les blocs-notes Jupyter</span><span class="sxs-lookup"><span data-stu-id="2c45f-219">Use external packages with Jupyter notebooks</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="2c45f-220">Installer Notebook sur votre ordinateur et vous connecter tooan cluster HDInsight Spark</span><span class="sxs-lookup"><span data-stu-id="2c45f-220">Install Jupyter on your computer and connect tooan HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a><span data-ttu-id="2c45f-221">Gestion des ressources</span><span class="sxs-lookup"><span data-stu-id="2c45f-221">Manage resources</span></span>
* [<span data-ttu-id="2c45f-222">Gérer les ressources de cluster d’Apache Spark hello dans Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="2c45f-222">Manage resources for hello Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="2c45f-223">Track and debug jobs running on an Apache Spark cluster in HDInsight (Suivi et débogage des tâches en cours d’exécution sur un cluster Apache Spark dans HDInsight)</span><span class="sxs-lookup"><span data-stu-id="2c45f-223">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)
