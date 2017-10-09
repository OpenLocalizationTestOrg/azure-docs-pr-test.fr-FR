---
title: aaaWhat est Apache Hive et HiveQL - Azure HDInsight | Documents Microsoft
description: "Apache Hive est un système d’entrepôt de données pour Hadoop. Vous pouvez interroger les données stockées dans la ruche à l’aide de HiveQL, tooTransact-SQL similaire. Dans ce document, vous devez savoir comment la ruche toouse et HiveQL avec Azure HDInsight."
keywords: "hiveql, quelle est la ruche, hadoop hiveql, comment toouse hive, découvrez hive, quelle est la ruche"
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 2c10f989-7636-41bf-b7f7-c4b67ec0814f
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/03/2017
ms.author: larryfr
ms.openlocfilehash: a2772312263895ff99b499898264c2e6d5e816e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-apache-hive-and-hiveql-on-azure-hdinsight"></a><span data-ttu-id="e2f2e-106">Présentation d’Apache Hive et HiveQL sur Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="e2f2e-106">What is Apache Hive and HiveQL on Azure HDInsight?</span></span>

<span data-ttu-id="e2f2e-107">[Apache Hive](http://hive.apache.org/) est un système d’entrepôt de données pour Hadoop.</span><span class="sxs-lookup"><span data-stu-id="e2f2e-107">[Apache Hive](http://hive.apache.org/) is a data warehouse system for Hadoop.</span></span> <span data-ttu-id="e2f2e-108">Hive permet la synthèse, l’interrogation et l’analyse des données.</span><span class="sxs-lookup"><span data-stu-id="e2f2e-108">Hive enables data summarization, querying, and analysis of data.</span></span> <span data-ttu-id="e2f2e-109">Requêtes Hive sont écrites dans HiveQL, qui est un tooSQL similaire de langage de requête.</span><span class="sxs-lookup"><span data-stu-id="e2f2e-109">Hive queries are written in HiveQL, which is a query language similar tooSQL.</span></span>

<span data-ttu-id="e2f2e-110">Ruche vous permet de tooproject structure sur des données en grande partie non structurées.</span><span class="sxs-lookup"><span data-stu-id="e2f2e-110">Hive allows you tooproject structure on largely unstructured data.</span></span> <span data-ttu-id="e2f2e-111">Après avoir défini la structure de hello, vous pouvez utiliser les données de salutation HiveQL tooquery sans avoir connaissance de Java ou MapReduce.</span><span class="sxs-lookup"><span data-stu-id="e2f2e-111">After you define hello structure, you can use HiveQL tooquery hello data without knowledge of Java or MapReduce.</span></span>

<span data-ttu-id="e2f2e-112">HDInsight fournit plusieurs types de cluster adaptés à des charges de travail spécifiques.</span><span class="sxs-lookup"><span data-stu-id="e2f2e-112">HDInsight provides several cluster types, which are tuned for specific workloads.</span></span> <span data-ttu-id="e2f2e-113">Hello cluster types suivants est souvent utilisée pour les requêtes Hive :</span><span class="sxs-lookup"><span data-stu-id="e2f2e-113">hello following cluster types are most often used for Hive queries:</span></span>

* <span data-ttu-id="e2f2e-114">__Ruche interactif__: cluster Hadoop de A qui fournit [faible latence analytiques de traitement (LLAP)](https://cwiki.apache.org/confluence/display/Hive/LLAP) temps de réponse de tooimprove de fonctionnalités des requêtes interactives.</span><span class="sxs-lookup"><span data-stu-id="e2f2e-114">__Interactive Hive__: A Hadoop cluster that provides [Low Latency Analytical Processing (LLAP)](https://cwiki.apache.org/confluence/display/Hive/LLAP) functionality tooimprove response times for interactive queries.</span></span> <span data-ttu-id="e2f2e-115">Pour plus d’informations, consultez hello [démarrer avec la ruche Interactive dans HDInsight](hdinsight-hadoop-use-interactive-hive.md) document.</span><span class="sxs-lookup"><span data-stu-id="e2f2e-115">For more information, see hello [Start with Interactive Hive in HDInsight](hdinsight-hadoop-use-interactive-hive.md) document.</span></span>

* <span data-ttu-id="e2f2e-116">__Hadoop__ : cluster Hadoop adapté aux charges de travail de traitement par lots.</span><span class="sxs-lookup"><span data-stu-id="e2f2e-116">__Hadoop__: A Hadoop cluster that is tuned for batch processing workloads.</span></span> <span data-ttu-id="e2f2e-117">Pour plus d’informations, consultez hello [démarrer avec Hadoop dans HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md) document.</span><span class="sxs-lookup"><span data-stu-id="e2f2e-117">For more information, see hello [Start with Hadoop in HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md) document.</span></span>

* <span data-ttu-id="e2f2e-118">__Spark__ : Apache Spark intègre une fonctionnalité permettant de travailler avec Hive.</span><span class="sxs-lookup"><span data-stu-id="e2f2e-118">__Spark__: Apache Spark has built-in functionality for working with Hive.</span></span> <span data-ttu-id="e2f2e-119">Pour plus d’informations, consultez hello [démarrer avec Spark sur HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md) document.</span><span class="sxs-lookup"><span data-stu-id="e2f2e-119">For more information, see hello [Start with Spark on HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md) document.</span></span>

* <span data-ttu-id="e2f2e-120">__HBase__: HiveQL peut être tooquery utilisé les données stockées dans HBase.</span><span class="sxs-lookup"><span data-stu-id="e2f2e-120">__HBase__: HiveQL can be used tooquery data stored in HBase.</span></span> <span data-ttu-id="e2f2e-121">Pour plus d’informations, consultez hello [démarrer avec HBase sur HDInsight](hdinsight-hbase-tutorial-get-started-linux.md) document.</span><span class="sxs-lookup"><span data-stu-id="e2f2e-121">For more information, see hello [Start with HBase on HDInsight](hdinsight-hbase-tutorial-get-started-linux.md) document.</span></span>

## <a name="how-toouse-hive"></a><span data-ttu-id="e2f2e-122">Comment la ruche toouse</span><span class="sxs-lookup"><span data-stu-id="e2f2e-122">How toouse Hive</span></span>

<span data-ttu-id="e2f2e-123">Utilisez hello suivant toodiscover table comment toouse Hive hdinsight :</span><span class="sxs-lookup"><span data-stu-id="e2f2e-123">Use hello following table toodiscover how toouse Hive with HDInsight:</span></span>

| <span data-ttu-id="e2f2e-124">**Utilisez cette méthode** si vous souhaitez...</span><span class="sxs-lookup"><span data-stu-id="e2f2e-124">**Use this method** if you want...</span></span> | <span data-ttu-id="e2f2e-125">... un interpréteur de commandes **interactif**</span><span class="sxs-lookup"><span data-stu-id="e2f2e-125">...an **interactive** shell</span></span> | <span data-ttu-id="e2f2e-126">... un traitement par **lots**</span><span class="sxs-lookup"><span data-stu-id="e2f2e-126">...**batch** processing</span></span> | <span data-ttu-id="e2f2e-127">...avec ce **système d’exploitation cluster**</span><span class="sxs-lookup"><span data-stu-id="e2f2e-127">...with this **cluster operating system**</span></span> | <span data-ttu-id="e2f2e-128">...depuis ce **système d’exploitation cluster**</span><span class="sxs-lookup"><span data-stu-id="e2f2e-128">...from this **client operating system**</span></span> |
|:--- |:---:|:---:|:--- |:--- |
| [<span data-ttu-id="e2f2e-129">Affichage Hive</span><span class="sxs-lookup"><span data-stu-id="e2f2e-129">Hive View</span></span>](hdinsight-hadoop-use-hive-ambari-view.md) |<span data-ttu-id="e2f2e-130">✔</span><span class="sxs-lookup"><span data-stu-id="e2f2e-130">✔</span></span> |<span data-ttu-id="e2f2e-131">✔</span><span class="sxs-lookup"><span data-stu-id="e2f2e-131">✔</span></span> |<span data-ttu-id="e2f2e-132">Linux</span><span class="sxs-lookup"><span data-stu-id="e2f2e-132">Linux</span></span> |<span data-ttu-id="e2f2e-133">N’importe lequel (basé sur le navigateur)</span><span class="sxs-lookup"><span data-stu-id="e2f2e-133">Any (browser based)</span></span> |
| [<span data-ttu-id="e2f2e-134">Client Beeline</span><span class="sxs-lookup"><span data-stu-id="e2f2e-134">Beeline client</span></span>](hdinsight-hadoop-use-hive-beeline.md) |<span data-ttu-id="e2f2e-135">✔</span><span class="sxs-lookup"><span data-stu-id="e2f2e-135">✔</span></span> |<span data-ttu-id="e2f2e-136">✔</span><span class="sxs-lookup"><span data-stu-id="e2f2e-136">✔</span></span> |<span data-ttu-id="e2f2e-137">Linux</span><span class="sxs-lookup"><span data-stu-id="e2f2e-137">Linux</span></span> |<span data-ttu-id="e2f2e-138">Linux, Unix, Mac OS X ou Windows</span><span class="sxs-lookup"><span data-stu-id="e2f2e-138">Linux, Unix, Mac OS X, or Windows</span></span> |
| [<span data-ttu-id="e2f2e-139">API REST</span><span class="sxs-lookup"><span data-stu-id="e2f2e-139">REST API</span></span>](hdinsight-hadoop-use-hive-curl.md) |&nbsp; |<span data-ttu-id="e2f2e-140">✔</span><span class="sxs-lookup"><span data-stu-id="e2f2e-140">✔</span></span> |<span data-ttu-id="e2f2e-141">Linux ou Windows*</span><span class="sxs-lookup"><span data-stu-id="e2f2e-141">Linux or Windows*</span></span> |<span data-ttu-id="e2f2e-142">Linux, Unix, Mac OS X ou Windows</span><span class="sxs-lookup"><span data-stu-id="e2f2e-142">Linux, Unix, Mac OS X, or Windows</span></span> |
| [<span data-ttu-id="e2f2e-143">Outils HDInsight pour Visual Studio</span><span class="sxs-lookup"><span data-stu-id="e2f2e-143">HDInsight tools for Visual Studio</span></span>](hdinsight-hadoop-use-hive-visual-studio.md) |&nbsp; |<span data-ttu-id="e2f2e-144">✔</span><span class="sxs-lookup"><span data-stu-id="e2f2e-144">✔</span></span> |<span data-ttu-id="e2f2e-145">Linux ou Windows*</span><span class="sxs-lookup"><span data-stu-id="e2f2e-145">Linux or Windows*</span></span> |<span data-ttu-id="e2f2e-146">Windows</span><span class="sxs-lookup"><span data-stu-id="e2f2e-146">Windows</span></span> |
| [<span data-ttu-id="e2f2e-147">Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="e2f2e-147">Windows PowerShell</span></span>](hdinsight-hadoop-use-hive-powershell.md) |&nbsp; |<span data-ttu-id="e2f2e-148">✔</span><span class="sxs-lookup"><span data-stu-id="e2f2e-148">✔</span></span> |<span data-ttu-id="e2f2e-149">Linux ou Windows*</span><span class="sxs-lookup"><span data-stu-id="e2f2e-149">Linux or Windows*</span></span> |<span data-ttu-id="e2f2e-150">Windows</span><span class="sxs-lookup"><span data-stu-id="e2f2e-150">Windows</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="e2f2e-151">\*Linux est hello seul système d’exploitation utilisé sur HDInsight version 3.4 ou supérieure.</span><span class="sxs-lookup"><span data-stu-id="e2f2e-151">\* Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="e2f2e-152">Pour plus d’informations, consultez [Suppression de HDInsight sous Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="e2f2e-152">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>
>
> <span data-ttu-id="e2f2e-153">Si vous utilisez un cluster HDInsight de basés sur Windows, vous pouvez utiliser hello [console de requête](hdinsight-hadoop-use-hive-query-console.md) depuis votre navigateur ou [Bureau à distance](hdinsight-hadoop-use-hive-remote-desktop.md) toorun des requêtes Hive.</span><span class="sxs-lookup"><span data-stu-id="e2f2e-153">If you are using a Windows-based HDInsight cluster, you can use hello [Query console](hdinsight-hadoop-use-hive-query-console.md) from your browser or [Remote Desktop](hdinsight-hadoop-use-hive-remote-desktop.md) toorun Hive queries.</span></span>

## <a name="hiveql-language-reference"></a><span data-ttu-id="e2f2e-154">Référence du langage HiveQL</span><span class="sxs-lookup"><span data-stu-id="e2f2e-154">HiveQL language reference</span></span>

<span data-ttu-id="e2f2e-155">Référence du langage HiveQL est disponible dans hello [manuel de langage (https://cwiki.apache.org/confluence/display/Hive/LanguageManual)](https://cwiki.apache.org/confluence/display/Hive/LanguageManual).</span><span class="sxs-lookup"><span data-stu-id="e2f2e-155">HiveQL language reference is available in hello [language manual (https://cwiki.apache.org/confluence/display/Hive/LanguageManual)](https://cwiki.apache.org/confluence/display/Hive/LanguageManual).</span></span>

## <a name="hive-and-data-structure"></a><span data-ttu-id="e2f2e-156">Hive et structure des données</span><span class="sxs-lookup"><span data-stu-id="e2f2e-156">Hive and data structure</span></span>

<span data-ttu-id="e2f2e-157">Ruche comprend des données semi-structurées et structuration de toowork avec.</span><span class="sxs-lookup"><span data-stu-id="e2f2e-157">Hive understands how toowork with structured and semi-structured data.</span></span> <span data-ttu-id="e2f2e-158">Par exemple, fichiers texte dans lequel les champs de hello sont délimités par des caractères spécifiques.</span><span class="sxs-lookup"><span data-stu-id="e2f2e-158">For example, text files where hello fields are delimited by specific characters.</span></span> <span data-ttu-id="e2f2e-159">Hello HiveQL instruction qui suit crée une table sur délimitées par un espace de données :</span><span class="sxs-lookup"><span data-stu-id="e2f2e-159">hello following HiveQL statement creates a table over space-delimited data:</span></span>

```hiveql
CREATE EXTERNAL TABLE log4jLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
ROW FORMAT DELIMITED FIELDS TERMINATED BY ' '
STORED AS TEXTFILE LOCATION '/example/data/';
```

<span data-ttu-id="e2f2e-160">Hive prend également en charge un **sérialiseur/ désérialiseur (SerDe)** personnalisé pour des données structurées de manière irrégulière ou complexes.</span><span class="sxs-lookup"><span data-stu-id="e2f2e-160">Hive also supports custom **serializer/deserializers (SerDe)** for complex or irregularly structured data.</span></span> <span data-ttu-id="e2f2e-161">Pour plus d’informations, consultez hello [comment toouse un SerDe JSON personnalisée avec HDInsight](http://blogs.msdn.com/b/bigdatasupport/archive/2014/06/18/how-to-use-a-custom-json-serde-with-microsoft-azure-hdinsight.aspx) document.</span><span class="sxs-lookup"><span data-stu-id="e2f2e-161">For more information, see hello [How toouse a custom JSON SerDe with HDInsight](http://blogs.msdn.com/b/bigdatasupport/archive/2014/06/18/how-to-use-a-custom-json-serde-with-microsoft-azure-hdinsight.aspx) document.</span></span>

<span data-ttu-id="e2f2e-162">Pour plus d’informations sur les formats de fichier pris en charge par la ruche, consultez hello [manuel de langage (https://cwiki.apache.org/confluence/display/Hive/LanguageManual)](https://cwiki.apache.org/confluence/display/Hive/LanguageManual)</span><span class="sxs-lookup"><span data-stu-id="e2f2e-162">For more information on file formats supported by Hive, see hello [Language manual (https://cwiki.apache.org/confluence/display/Hive/LanguageManual)](https://cwiki.apache.org/confluence/display/Hive/LanguageManual)</span></span>

## <a name="hive-internal-tables-vs-external-tables"></a><span data-ttu-id="e2f2e-163">Tables internes et externes Hive</span><span class="sxs-lookup"><span data-stu-id="e2f2e-163">Hive internal tables vs external tables</span></span>

<span data-ttu-id="e2f2e-164">Hive vous permet de créer deux types de tables :</span><span class="sxs-lookup"><span data-stu-id="e2f2e-164">There are two types of tables that you can create with Hive:</span></span>

* <span data-ttu-id="e2f2e-165">__Interne__: données sont stockées dans l’entrepôt de données Hive hello.</span><span class="sxs-lookup"><span data-stu-id="e2f2e-165">__Internal__: Data is stored in hello Hive data warehouse.</span></span> <span data-ttu-id="e2f2e-166">Hello l’entrepôt de données se trouve dans `/hive/warehouse/` sur le stockage par défaut hello pour le cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="e2f2e-166">hello data warehouse is located at `/hive/warehouse/` on hello default storage for hello cluster.</span></span>

    <span data-ttu-id="e2f2e-167">Utilisez des tables internes quand :</span><span class="sxs-lookup"><span data-stu-id="e2f2e-167">Use internal tables when:</span></span>

    * <span data-ttu-id="e2f2e-168">les données sont temporaires.</span><span class="sxs-lookup"><span data-stu-id="e2f2e-168">Data is temporary.</span></span>
    * <span data-ttu-id="e2f2e-169">Vous souhaitez ruche toomanage hello du cycle de vie de la table de hello et données.</span><span class="sxs-lookup"><span data-stu-id="e2f2e-169">You want Hive toomanage hello lifecycle of hello table and data.</span></span>

* <span data-ttu-id="e2f2e-170">__Externe__: les données sont stockées en dehors de l’entrepôt de données hello.</span><span class="sxs-lookup"><span data-stu-id="e2f2e-170">__External__: Data is stored outside hello data warehouse.</span></span> <span data-ttu-id="e2f2e-171">les données de salutation pouvant figurer sur n’importe quel stockage accessible par cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="e2f2e-171">hello data can be stored on any storage accessible by hello cluster.</span></span>

    <span data-ttu-id="e2f2e-172">Utilisez des tables externes quand :</span><span class="sxs-lookup"><span data-stu-id="e2f2e-172">Use external tables when:</span></span>

    * <span data-ttu-id="e2f2e-173">les données de salutation sont également utilisées en dehors de la ruche.</span><span class="sxs-lookup"><span data-stu-id="e2f2e-173">hello data is also used outside of Hive.</span></span> <span data-ttu-id="e2f2e-174">Par exemple, les fichiers de données hello sont mis à jour par un autre processus (qui ne verrouille pas les fichiers hello.)</span><span class="sxs-lookup"><span data-stu-id="e2f2e-174">For example, hello data files are updated by another process (that does not lock hello files.)</span></span>
    * <span data-ttu-id="e2f2e-175">Les données doivent tooremain Bonjour sous-jacent emplacement, même après la suppression de table de hello.</span><span class="sxs-lookup"><span data-stu-id="e2f2e-175">Data needs tooremain in hello underlying location, even after dropping hello table.</span></span>
    * <span data-ttu-id="e2f2e-176">Vous avez besoin d’un emplacement personnalisé, par exemple un compte de stockage non sélectionné par défaut.</span><span class="sxs-lookup"><span data-stu-id="e2f2e-176">You need a custom location, such as a non-default storage account.</span></span>
    * <span data-ttu-id="e2f2e-177">Un programme autre que ruche gère le format de données hello, l’emplacement, etc..</span><span class="sxs-lookup"><span data-stu-id="e2f2e-177">A program other than hive manages hello data format, location, etc.</span></span>

<span data-ttu-id="e2f2e-178">Pour plus d’informations, consultez hello [Hive interne et externe Tables Intro] [ cindygross-hive-tables] billet de blog.</span><span class="sxs-lookup"><span data-stu-id="e2f2e-178">For more information, see hello [Hive Internal and External Tables Intro][cindygross-hive-tables] blog post.</span></span>

## <a name="user-defined-functions-udf"></a><span data-ttu-id="e2f2e-179">Fonctions définies par l’utilisateur (UDF)</span><span class="sxs-lookup"><span data-stu-id="e2f2e-179">User-defined functions (UDF)</span></span>

<span data-ttu-id="e2f2e-180">Hive peut également être étendu via des **fonctions définies par l'utilisateur (UDF)**.</span><span class="sxs-lookup"><span data-stu-id="e2f2e-180">Hive can also be extended through **user-defined functions (UDF)**.</span></span> <span data-ttu-id="e2f2e-181">Un fichier UDF vous permet de tooimplement de fonctionnalité ou logique qui n’est pas facilement être modelée dans HiveQL.</span><span class="sxs-lookup"><span data-stu-id="e2f2e-181">A UDF allows you tooimplement functionality or logic that isn't easily modeled in HiveQL.</span></span> <span data-ttu-id="e2f2e-182">Pour obtenir un exemple d’utilisation des UDF avec Hive, consultez hello suivant des documents :</span><span class="sxs-lookup"><span data-stu-id="e2f2e-182">For an example of using UDFs with Hive, see hello following documents:</span></span>

* [<span data-ttu-id="e2f2e-183">Utiliser une fonction Java définie par l’utilisateur avec Hive</span><span class="sxs-lookup"><span data-stu-id="e2f2e-183">Use a Java user-defined function with Hive</span></span>](hdinsight-hadoop-hive-java-udf.md)

* [<span data-ttu-id="e2f2e-184">Utiliser une fonction Python définie par l’utilisateur avec Hive et Pig</span><span class="sxs-lookup"><span data-stu-id="e2f2e-184">Use a Python user-defined function with Hive and Pig</span></span>](hdinsight-python.md)

* [<span data-ttu-id="e2f2e-185">Utiliser une fonction C# définie par l’utilisateur avec Hive et Pig</span><span class="sxs-lookup"><span data-stu-id="e2f2e-185">Use a C# user-defined function with Hive and Pig</span></span>](hdinsight-hadoop-hive-pig-udf-dotnet-csharp.md)

* [<span data-ttu-id="e2f2e-186">Fonctionnement des tooHDInsight tooadd une ruche personnalisée défini par l’utilisateur</span><span class="sxs-lookup"><span data-stu-id="e2f2e-186">How tooadd a custom Hive user-defined function tooHDInsight</span></span>](http://blogs.msdn.com/b/bigdatasupport/archive/2014/01/14/how-to-add-custom-hive-udfs-to-hdinsight.aspx)

* [<span data-ttu-id="e2f2e-187">Une date/heure exemple ruche fonction définie par l’utilisateur tooconvert met en forme tooHive timestamp</span><span class="sxs-lookup"><span data-stu-id="e2f2e-187">An example Hive user-defined function tooconvert date/time formats tooHive timestamp</span></span>](https://github.com/Azure-Samples/hdinsight-java-hive-udf)

## <span data-ttu-id="e2f2e-188"><a id="data"></a>Exemple de données</span><span class="sxs-lookup"><span data-stu-id="e2f2e-188"><a id="data"></a>Example data</span></span>

<span data-ttu-id="e2f2e-189">Hive sur HDInsight est préchargé avec une table interne nommée `hivesampletable`.</span><span class="sxs-lookup"><span data-stu-id="e2f2e-189">Hive on HDInsight comes pre-loaded with an internal table named `hivesampletable`.</span></span> <span data-ttu-id="e2f2e-190">HDInsight fournit également des exemples de jeux de données pouvant être utilisés avec Hive.</span><span class="sxs-lookup"><span data-stu-id="e2f2e-190">HDInsight also provides example data sets that can be used with Hive.</span></span> <span data-ttu-id="e2f2e-191">Ces jeux de données sont stockées dans hello `/example/data` et `/HdiSamples` répertoires.</span><span class="sxs-lookup"><span data-stu-id="e2f2e-191">These data sets are stored in hello `/example/data` and `/HdiSamples` directories.</span></span> <span data-ttu-id="e2f2e-192">Ils existent dans le stockage par défaut hello pour votre cluster.</span><span class="sxs-lookup"><span data-stu-id="e2f2e-192">These directories exist in hello default storage for your cluster.</span></span>

## <span data-ttu-id="e2f2e-193"><a id="job"></a>Exemple de requête Hive</span><span class="sxs-lookup"><span data-stu-id="e2f2e-193"><a id="job"></a>Example Hive query</span></span>

<span data-ttu-id="e2f2e-194">Hello suivant des colonnes de projet instructions HiveQL sur hello `/example/data/sample.log` fichier :</span><span class="sxs-lookup"><span data-stu-id="e2f2e-194">hello following HiveQL statements project columns onto hello `/example/data/sample.log` file:</span></span>

    set hive.execution.engine=tez;
    DROP TABLE log4jLogs;
    CREATE EXTERNAL TABLE log4jLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
    ROW FORMAT DELIMITED FIELDS TERMINATED BY ' '
    STORED AS TEXTFILE LOCATION '/example/data/';
    SELECT t4 AS sev, COUNT(*) AS count FROM log4jLogs WHERE t4 = '[ERROR]' AND INPUT__FILE__NAME LIKE '%.log' GROUP BY t4;

<span data-ttu-id="e2f2e-195">Dans l’exemple précédent de hello, les instructions HiveQL hello effectuent hello suivant des actions :</span><span class="sxs-lookup"><span data-stu-id="e2f2e-195">In hello previous example, hello HiveQL statements perform hello following actions:</span></span>

* <span data-ttu-id="e2f2e-196">`set hive.execution.engine=tez;`: Jeux hello toouse du moteur d’exécution Tez.</span><span class="sxs-lookup"><span data-stu-id="e2f2e-196">`set hive.execution.engine=tez;`: Sets hello execution engine toouse Tez.</span></span> <span data-ttu-id="e2f2e-197">L’utilisation de Tez au lieu de MapReduce peut augmenter les performances de requête.</span><span class="sxs-lookup"><span data-stu-id="e2f2e-197">Using Tez instead of MapReduce can provide an increase in query performance.</span></span> <span data-ttu-id="e2f2e-198">Pour plus d’informations sur Tez, consultez hello [Tez d’Apache utilisation pour améliorer les performances](#usetez) section.</span><span class="sxs-lookup"><span data-stu-id="e2f2e-198">For more information on Tez, see hello [Use Apache Tez for improved performance](#usetez) section.</span></span>

    > [!NOTE]
    > <span data-ttu-id="e2f2e-199">Cette instruction est uniquement requise lorsque vous utilisez un cluster HDInsight sous Windows.</span><span class="sxs-lookup"><span data-stu-id="e2f2e-199">This statement is only required when using a Windows-based HDInsight cluster.</span></span> <span data-ttu-id="e2f2e-200">Tez est le moteur d’exécution par défaut hello pour HDInsight de basés sur Linux.</span><span class="sxs-lookup"><span data-stu-id="e2f2e-200">Tez is hello default execution engine for Linux-based HDInsight.</span></span>

* <span data-ttu-id="e2f2e-201">`DROP TABLE`: Si la table de hello existe déjà, supprimez-le.</span><span class="sxs-lookup"><span data-stu-id="e2f2e-201">`DROP TABLE`: If hello table already exists, delete it.</span></span>

* <span data-ttu-id="e2f2e-202">`CREATE EXTERNAL TABLE` : crée une table **externe** dans Hive.</span><span class="sxs-lookup"><span data-stu-id="e2f2e-202">`CREATE EXTERNAL TABLE`: Creates a new **external** table in Hive.</span></span> <span data-ttu-id="e2f2e-203">Les tables externes ne stockent la définition de table hello Hive.</span><span class="sxs-lookup"><span data-stu-id="e2f2e-203">External tables only store hello table definition in Hive.</span></span> <span data-ttu-id="e2f2e-204">les données de salutation reste dans l’emplacement d’origine de hello et au format d’origine de hello.</span><span class="sxs-lookup"><span data-stu-id="e2f2e-204">hello data is left in hello original location and in hello original format.</span></span>

* <span data-ttu-id="e2f2e-205">`ROW FORMAT`: Indique la ruche de mise en forme les données de salutation.</span><span class="sxs-lookup"><span data-stu-id="e2f2e-205">`ROW FORMAT`: Tells Hive how hello data is formatted.</span></span> <span data-ttu-id="e2f2e-206">Dans ce cas, les champs de hello dans chaque journal sont séparés par un espace.</span><span class="sxs-lookup"><span data-stu-id="e2f2e-206">In this case, hello fields in each log are separated by a space.</span></span>

* <span data-ttu-id="e2f2e-207">`STORED AS TEXTFILE LOCATION`: Indique ruche où hello les données sont stockées (hello `example/data` active) et qu’il est stocké sous forme de texte.</span><span class="sxs-lookup"><span data-stu-id="e2f2e-207">`STORED AS TEXTFILE LOCATION`: Tells Hive where hello data is stored (hello `example/data` directory) and that it is stored as text.</span></span> <span data-ttu-id="e2f2e-208">les données de salutation peuvent être dans un fichier ou réparties sur plusieurs fichiers dans le répertoire de hello.</span><span class="sxs-lookup"><span data-stu-id="e2f2e-208">hello data can be in one file or spread across multiple files within hello directory.</span></span>

* <span data-ttu-id="e2f2e-209">`SELECT`: Sélectionne un nombre de toutes les lignes où hello colonne **t4** contient la valeur de hello **[erreur]**.</span><span class="sxs-lookup"><span data-stu-id="e2f2e-209">`SELECT`: Selects a count of all rows where hello column **t4** contains hello value **[ERROR]**.</span></span> <span data-ttu-id="e2f2e-210">Cette instruction renvoie la valeur **3**, car trois lignes contiennent cette valeur.</span><span class="sxs-lookup"><span data-stu-id="e2f2e-210">This statement returns a value of **3** because there are three rows that contain this value.</span></span>

* <span data-ttu-id="e2f2e-211">`INPUT__FILE__NAME LIKE '%.log'`-Ruche tente de fichiers de tooall tooapply hello schéma dans le répertoire de hello.</span><span class="sxs-lookup"><span data-stu-id="e2f2e-211">`INPUT__FILE__NAME LIKE '%.log'` - Hive attempts tooapply hello schema tooall files in hello directory.</span></span> <span data-ttu-id="e2f2e-212">Dans ce cas, le répertoire de hello contient des fichiers qui ne correspondent pas hello schéma.</span><span class="sxs-lookup"><span data-stu-id="e2f2e-212">In this case, hello directory contains files that do not match hello schema.</span></span> <span data-ttu-id="e2f2e-213">données de garbage tooprevent dans les résultats de hello, cette instruction indique ruche que nous devons retourner uniquement les données à partir de fichiers se terminant par. journal.</span><span class="sxs-lookup"><span data-stu-id="e2f2e-213">tooprevent garbage data in hello results, this statement tells Hive that we should only return data from files ending in .log.</span></span>

> [!NOTE]
> <span data-ttu-id="e2f2e-214">Tables externes doivent être utilisées lorsque vous attendez hello toobe de données sous-jacent mis à jour par une source externe.</span><span class="sxs-lookup"><span data-stu-id="e2f2e-214">External tables should be used when you expect hello underlying data toobe updated by an external source.</span></span> <span data-ttu-id="e2f2e-215">Par exemple, un processus de chargement de données automatisé ou une opération MapReduce.</span><span class="sxs-lookup"><span data-stu-id="e2f2e-215">For example, an automated data upload process, or MapReduce operation.</span></span>
>
> <span data-ttu-id="e2f2e-216">Suppression d’une table externe est **pas** supprimer les données de salutation, elle supprime uniquement la définition de la table hello.</span><span class="sxs-lookup"><span data-stu-id="e2f2e-216">Dropping an external table does **not** delete hello data, it only deletes hello table definition.</span></span>

<span data-ttu-id="e2f2e-217">toocreate un **interne** table externe à la place, utilisez hello suivant HiveQL :</span><span class="sxs-lookup"><span data-stu-id="e2f2e-217">toocreate an **internal** table instead of external, use hello following HiveQL:</span></span>

    set hive.execution.engine=tez;
    CREATE TABLE IF NOT EXISTS errorLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
    STORED AS ORC;
    INSERT OVERWRITE TABLE errorLogs
    SELECT t1, t2, t3, t4, t5, t6, t7 FROM log4jLogs WHERE t4 = '[ERROR]';

<span data-ttu-id="e2f2e-218">Ces instructions effectuent hello suivant des actions :</span><span class="sxs-lookup"><span data-stu-id="e2f2e-218">These statements perform hello following actions:</span></span>

* <span data-ttu-id="e2f2e-219">`CREATE TABLE IF NOT EXISTS`: Si la table de hello n’existe pas, créez-le.</span><span class="sxs-lookup"><span data-stu-id="e2f2e-219">`CREATE TABLE IF NOT EXISTS`: If hello table does not exist, create it.</span></span> <span data-ttu-id="e2f2e-220">Étant donné que hello **externe** mot clé n’est pas utilisé, cette instruction crée une table interne.</span><span class="sxs-lookup"><span data-stu-id="e2f2e-220">Because hello **EXTERNAL** keyword is not used, this statement creates an internal table.</span></span> <span data-ttu-id="e2f2e-221">tableau de Hello est stocké dans l’entrepôt de données Hive hello et entièrement géré par ruche.</span><span class="sxs-lookup"><span data-stu-id="e2f2e-221">hello table is stored in hello Hive data warehouse and is managed completely by Hive.</span></span>

* <span data-ttu-id="e2f2e-222">`STORED AS ORC`: Stocke les données de hello dans format optimisé lignes en colonnes (ORC).</span><span class="sxs-lookup"><span data-stu-id="e2f2e-222">`STORED AS ORC`: Stores hello data in Optimized Row Columnar (ORC) format.</span></span> <span data-ttu-id="e2f2e-223">ORC est un format particulièrement efficace et optimisé pour le stockage de données Hive.</span><span class="sxs-lookup"><span data-stu-id="e2f2e-223">ORC is a highly optimized and efficient format for storing Hive data.</span></span>

* <span data-ttu-id="e2f2e-224">`INSERT OVERWRITE ... SELECT`: Sélectionne des lignes à partir de hello **log4jLogs** table qui contient **[erreur]**, et puis insertions hello des données dans hello **journaux d’erreurs de** table.</span><span class="sxs-lookup"><span data-stu-id="e2f2e-224">`INSERT OVERWRITE ... SELECT`: Selects rows from hello **log4jLogs** table that contains **[ERROR]**, and then inserts hello data into hello **errorLogs** table.</span></span>

> [!NOTE]
> <span data-ttu-id="e2f2e-225">Contrairement aux tables externes, la suppression d’une table interne supprime également les données sous-jacentes hello.</span><span class="sxs-lookup"><span data-stu-id="e2f2e-225">Unlike external tables, dropping an internal table also deletes hello underlying data.</span></span>

## <a name="improve-hive-query-performance"></a><span data-ttu-id="e2f2e-226">Améliorer les performances des requêtes Hive</span><span class="sxs-lookup"><span data-stu-id="e2f2e-226">Improve Hive query performance</span></span>

### <span data-ttu-id="e2f2e-227"><a id="usetez"></a>Apache Tez</span><span class="sxs-lookup"><span data-stu-id="e2f2e-227"><a id="usetez"></a>Apache Tez</span></span>

<span data-ttu-id="e2f2e-228">[Apache Tez](http://tez.apache.org) est une infrastructure qui permet à des applications utilisant beaucoup de données, tels que Hive, toorun beaucoup plus efficacement à l’échelle.</span><span class="sxs-lookup"><span data-stu-id="e2f2e-228">[Apache Tez](http://tez.apache.org) is a framework that allows data intensive applications, such as Hive, toorun much more efficiently at scale.</span></span> <span data-ttu-id="e2f2e-229">Tez est activé par défaut pour les clusters HDInsight basés sur Linux.</span><span class="sxs-lookup"><span data-stu-id="e2f2e-229">Tez is enabled by default for Linux-based HDInsight clusters.</span></span>

> [!NOTE]
> <span data-ttu-id="e2f2e-230">Tez est actuellement désactivé par défaut pour les clusters HDInsight basés sur Windows, et il doit être activé.</span><span class="sxs-lookup"><span data-stu-id="e2f2e-230">Tez is currently off by default for Windows-based HDInsight clusters and it must be enabled.</span></span> <span data-ttu-id="e2f2e-231">avantage tootake de Tez, hello valeur suivante doit être définie pour une requête Hive :</span><span class="sxs-lookup"><span data-stu-id="e2f2e-231">tootake advantage of Tez, hello following value must be set for a Hive query:</span></span>
>
> `set hive.execution.engine=tez;`
>
> <span data-ttu-id="e2f2e-232">Tez est moteur par défaut de hello pour les clusters HDInsight de basés sur Linux.</span><span class="sxs-lookup"><span data-stu-id="e2f2e-232">Tez is hello default engine for Linux-based HDInsight clusters.</span></span>

<span data-ttu-id="e2f2e-233">Hello [Hive sur les documents de conception Tez](https://cwiki.apache.org/confluence/display/Hive/Hive+on+Tez) contient des détails sur le choix d’implémentation hello et les configurations de paramétrage.</span><span class="sxs-lookup"><span data-stu-id="e2f2e-233">hello [Hive on Tez design documents](https://cwiki.apache.org/confluence/display/Hive/Hive+on+Tez) contains details about hello implementation choices and tuning configurations.</span></span>

<span data-ttu-id="e2f2e-234">tooaid dans les tâches de débogage exécuté à l’aide de Tez, HDInsight fournit hello suivant des interfaces utilisateur web qui vous permettre de tooview les détails des travaux de Tez :</span><span class="sxs-lookup"><span data-stu-id="e2f2e-234">tooaid in debugging jobs ran using Tez, HDInsight provides hello following web UIs that allow you tooview details of Tez jobs:</span></span>

* [<span data-ttu-id="e2f2e-235">Utilisez hello vue Ambari Tez sur HDInsight de basés sur Linux</span><span class="sxs-lookup"><span data-stu-id="e2f2e-235">Use hello Ambari Tez view on Linux-based HDInsight</span></span>](hdinsight-debug-ambari-tez-view.md)

* [<span data-ttu-id="e2f2e-236">Utilisez hello Tez UI sur HDInsight de basés sur Windows</span><span class="sxs-lookup"><span data-stu-id="e2f2e-236">Use hello Tez UI on Windows-based HDInsight</span></span>](hdinsight-debug-tez-ui.md)

### <a name="low-latency-analytical-processing-llap"></a><span data-ttu-id="e2f2e-237">Low Latency Analytical Processing (LLAP)</span><span class="sxs-lookup"><span data-stu-id="e2f2e-237">Low Latency Analytical Processing (LLAP)</span></span>

<span data-ttu-id="e2f2e-238">[LLAP](https://cwiki.apache.org/confluence/display/Hive/LLAP) (parfois appelé Live Long and Process) est une nouvelle fonctionnalité de Hive 2.0 qui permet la mise en cache en mémoire des requêtes.</span><span class="sxs-lookup"><span data-stu-id="e2f2e-238">[LLAP](https://cwiki.apache.org/confluence/display/Hive/LLAP) (sometimes known as Live Long and Process) is a new feature in Hive 2.0 that allows in-memory caching of queries.</span></span> <span data-ttu-id="e2f2e-239">LLAP effectue des requêtes Hive beaucoup plus rapides des trop[26 x plus rapide que la ruche 1.x dans certains cas](https://hortonworks.com/blog/announcing-apache-hive-2-1-25x-faster-queries-much/).</span><span class="sxs-lookup"><span data-stu-id="e2f2e-239">LLAP makes Hive queries much faster, up too[26x faster than Hive 1.x in some cases](https://hortonworks.com/blog/announcing-apache-hive-2-1-25x-faster-queries-much/).</span></span>

<span data-ttu-id="e2f2e-240">HDInsight fournit LLAP Bonjour Hive interactif de type de cluster.</span><span class="sxs-lookup"><span data-stu-id="e2f2e-240">HDInsight provides LLAP in hello Interactive Hive cluster type.</span></span> <span data-ttu-id="e2f2e-241">Pour plus d’informations, consultez hello [démarrer avec la ruche interactif](hdinsight-hadoop-use-interactive-hive.md) document.</span><span class="sxs-lookup"><span data-stu-id="e2f2e-241">For more information, see hello [Start with Interactive Hive](hdinsight-hadoop-use-interactive-hive.md) document.</span></span>

## <a name="hive-jobs-and-sql-server-integration-services"></a><span data-ttu-id="e2f2e-242">Tâches Hive et SQL Server Integration Services</span><span class="sxs-lookup"><span data-stu-id="e2f2e-242">Hive jobs and SQL Server Integration Services</span></span>

<span data-ttu-id="e2f2e-243">Vous pouvez utiliser SQL Server Integration Services (SSIS) toorun un travail Hive.</span><span class="sxs-lookup"><span data-stu-id="e2f2e-243">You can use SQL Server Integration Services (SSIS) toorun a Hive job.</span></span> <span data-ttu-id="e2f2e-244">Bonjour Azure Feature Pack pour SSIS fournit hello suivant des composants qui fonctionnent avec les tâches Hive dans HDInsight.</span><span class="sxs-lookup"><span data-stu-id="e2f2e-244">hello Azure Feature Pack for SSIS provides hello following components that work with Hive jobs on HDInsight.</span></span>

* <span data-ttu-id="e2f2e-245">[Tâche Hive d’Azure HDInsight][hivetask]</span><span class="sxs-lookup"><span data-stu-id="e2f2e-245">[Azure HDInsight Hive Task][hivetask]</span></span>

* <span data-ttu-id="e2f2e-246">[Gestionnaire de connexions d’abonnement Azure][connectionmanager]</span><span class="sxs-lookup"><span data-stu-id="e2f2e-246">[Azure Subscription Connection Manager][connectionmanager]</span></span>

<span data-ttu-id="e2f2e-247">En savoir plus sur hello Azure Feature Pack pour SSIS [ici][ssispack].</span><span class="sxs-lookup"><span data-stu-id="e2f2e-247">Learn more about hello Azure Feature Pack for SSIS [here][ssispack].</span></span>

## <span data-ttu-id="e2f2e-248"><a id="nextsteps"></a>Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="e2f2e-248"><a id="nextsteps"></a>Next steps</span></span>

<span data-ttu-id="e2f2e-249">Maintenant que vous savez quelle est la ruche et comment toouse avec Hadoop dans HDInsight, hello utilisation suivant lie tooexplore autres toowork manières avec Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="e2f2e-249">Now that you've learned what Hive is and how toouse it with Hadoop in HDInsight, use hello following links tooexplore other ways toowork with Azure HDInsight.</span></span>

* <span data-ttu-id="e2f2e-250">[Télécharger des données tooHDInsight][hdinsight-upload-data]</span><span class="sxs-lookup"><span data-stu-id="e2f2e-250">[Upload data tooHDInsight][hdinsight-upload-data]</span></span>
* <span data-ttu-id="e2f2e-251">[Utilisation de Pig avec HDInsight][hdinsight-use-pig]</span><span class="sxs-lookup"><span data-stu-id="e2f2e-251">[Use Pig with HDInsight][hdinsight-use-pig]</span></span>
* <span data-ttu-id="e2f2e-252">[Utilisation des tâches MapReduce avec HDInsight][hdinsight-use-mapreduce]</span><span class="sxs-lookup"><span data-stu-id="e2f2e-252">[Use MapReduce jobs with HDInsight][hdinsight-use-mapreduce]</span></span>

[hdinsight-sdk-documentation]: http://msdnstage.redmond.corp.microsoft.com/library/dn479185.aspx

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/

[apache-tez]: http://tez.apache.org
[apache-hive]: http://hive.apache.org/
[apache-log4j]: http://en.wikipedia.org/wiki/Log4j
[hive-on-tez-wiki]: https://cwiki.apache.org/confluence/display/Hive/Hive+on+Tez
[import-to-excel]: http://azure.microsoft.com/documentation/articles/hdinsight-connect-excel-power-query/
[hivetask]: http://msdn.microsoft.com/library/mt146771(v=sql.120).aspx
[connectionmanager]: http://msdn.microsoft.com/library/mt146773(v=sql.120).aspx
[ssispack]: http://msdn.microsoft.com/library/mt146770(v=sql.120).aspx

[hdinsight-use-pig]: hdinsight-use-pig.md
[hdinsight-use-oozie]: hdinsight-use-oozie.md
[hdinsight-analyze-flight-data]: hdinsight-analyze-flight-delay-data.md
[hdinsight-use-mapreduce]: hdinsight-use-mapreduce.md


[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md

[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md
[hdinsight-upload-data]: hdinsight-upload-data.md

[Powershell-install-configure]: /powershell/azureps-cmdlets-docs
[powershell-here-strings]: http://technet.microsoft.com/library/ee692792.aspx


[cindygross-hive-tables]: http://blogs.msdn.com/b/cindygross/archive/2013/02/06/hdinsight-hive-internal-and-external-tables-intro.aspx
