---
title: "Présentation d’Apache Hive et HiveQL - Azure HDInsight | Microsoft Docs"
description: "Apache Hive est un système d’entrepôt de données pour Hadoop. Vous pouvez interroger les données stockées dans Hive à l’aide de HiveQL, qui est similaire à Transact-SQL. Dans ce document, découvrez comment utiliser Hive et HiveQL avec Azure HDInsight."
keywords: "hiveql,présentation de hive,hadoop hiveql,utilisation de hive,découvrir hive,présentation de hive"
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
ms.openlocfilehash: 6b3ee17141f773bec07cf40e0b6d63363e9b5164
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="what-is-apache-hive-and-hiveql-on-azure-hdinsight"></a><span data-ttu-id="3ed1b-106">Présentation d’Apache Hive et HiveQL sur Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="3ed1b-106">What is Apache Hive and HiveQL on Azure HDInsight?</span></span>

<span data-ttu-id="3ed1b-107">[Apache Hive](http://hive.apache.org/) est un système d’entrepôt de données pour Hadoop.</span><span class="sxs-lookup"><span data-stu-id="3ed1b-107">[Apache Hive](http://hive.apache.org/) is a data warehouse system for Hadoop.</span></span> <span data-ttu-id="3ed1b-108">Hive permet la synthèse, l’interrogation et l’analyse des données.</span><span class="sxs-lookup"><span data-stu-id="3ed1b-108">Hive enables data summarization, querying, and analysis of data.</span></span> <span data-ttu-id="3ed1b-109">Les requêtes Hive sont écrites dans le langage HiveQL, qui est un langage de requête semblable à SQL.</span><span class="sxs-lookup"><span data-stu-id="3ed1b-109">Hive queries are written in HiveQL, which is a query language similar to SQL.</span></span>

<span data-ttu-id="3ed1b-110">Hive vous permet de concevoir une structure sur des données largement non structurées.</span><span class="sxs-lookup"><span data-stu-id="3ed1b-110">Hive allows you to project structure on largely unstructured data.</span></span> <span data-ttu-id="3ed1b-111">Une fois que vous avez défini la structure, vous pouvez utiliser HiveQL pour interroger les données sans connaître Java ou MapReduce.</span><span class="sxs-lookup"><span data-stu-id="3ed1b-111">After you define the structure, you can use HiveQL to query the data without knowledge of Java or MapReduce.</span></span>

<span data-ttu-id="3ed1b-112">HDInsight fournit plusieurs types de cluster adaptés à des charges de travail spécifiques.</span><span class="sxs-lookup"><span data-stu-id="3ed1b-112">HDInsight provides several cluster types, which are tuned for specific workloads.</span></span> <span data-ttu-id="3ed1b-113">Voici les types de cluster les plus souvent utilisés pour les requêtes Hive :</span><span class="sxs-lookup"><span data-stu-id="3ed1b-113">The following cluster types are most often used for Hive queries:</span></span>

* <span data-ttu-id="3ed1b-114">__Hive interactif__ : cluster Hadoop qui offre une fonctionnalité LLAP [(Low Latency Analytical Processing)](https://cwiki.apache.org/confluence/display/Hive/LLAP) afin d’améliorer les temps de réponse des requêtes interactives.</span><span class="sxs-lookup"><span data-stu-id="3ed1b-114">__Interactive Hive__: A Hadoop cluster that provides [Low Latency Analytical Processing (LLAP)](https://cwiki.apache.org/confluence/display/Hive/LLAP) functionality to improve response times for interactive queries.</span></span> <span data-ttu-id="3ed1b-115">Pour plus d’informations, consultez le document [Démarrer avec Hive interactif dans HDInsight](hdinsight-hadoop-use-interactive-hive.md).</span><span class="sxs-lookup"><span data-stu-id="3ed1b-115">For more information, see the [Start with Interactive Hive in HDInsight](hdinsight-hadoop-use-interactive-hive.md) document.</span></span>

* <span data-ttu-id="3ed1b-116">__Hadoop__ : cluster Hadoop adapté aux charges de travail de traitement par lots.</span><span class="sxs-lookup"><span data-stu-id="3ed1b-116">__Hadoop__: A Hadoop cluster that is tuned for batch processing workloads.</span></span> <span data-ttu-id="3ed1b-117">Pour plus d’informations, consultez le document [Démarrer avec Hadoop dans HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="3ed1b-117">For more information, see the [Start with Hadoop in HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md) document.</span></span>

* <span data-ttu-id="3ed1b-118">__Spark__ : Apache Spark intègre une fonctionnalité permettant de travailler avec Hive.</span><span class="sxs-lookup"><span data-stu-id="3ed1b-118">__Spark__: Apache Spark has built-in functionality for working with Hive.</span></span> <span data-ttu-id="3ed1b-119">Pour plus d’informations, consultez le document [Démarrer avec Spark dans HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="3ed1b-119">For more information, see the [Start with Spark on HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md) document.</span></span>

* <span data-ttu-id="3ed1b-120">__HBase__ : HiveQL peut être utilisé pour interroger les données stockées dans HBase.</span><span class="sxs-lookup"><span data-stu-id="3ed1b-120">__HBase__: HiveQL can be used to query data stored in HBase.</span></span> <span data-ttu-id="3ed1b-121">Pour plus d’informations, consultez le document [Démarrer avec HBase dans HDInsight](hdinsight-hbase-tutorial-get-started-linux.md).</span><span class="sxs-lookup"><span data-stu-id="3ed1b-121">For more information, see the [Start with HBase on HDInsight](hdinsight-hbase-tutorial-get-started-linux.md) document.</span></span>

## <a name="how-to-use-hive"></a><span data-ttu-id="3ed1b-122">Utilisation de Hive</span><span class="sxs-lookup"><span data-stu-id="3ed1b-122">How to use Hive</span></span>

<span data-ttu-id="3ed1b-123">Utilisez le tableau suivant pour découvrir comment utiliser Hive avec HDInsight :</span><span class="sxs-lookup"><span data-stu-id="3ed1b-123">Use the following table to discover how to use Hive with HDInsight:</span></span>

| <span data-ttu-id="3ed1b-124">**Utilisez cette méthode** si vous souhaitez...</span><span class="sxs-lookup"><span data-stu-id="3ed1b-124">**Use this method** if you want...</span></span> | <span data-ttu-id="3ed1b-125">... un interpréteur de commandes **interactif**</span><span class="sxs-lookup"><span data-stu-id="3ed1b-125">...an **interactive** shell</span></span> | <span data-ttu-id="3ed1b-126">... un traitement par **lots**</span><span class="sxs-lookup"><span data-stu-id="3ed1b-126">...**batch** processing</span></span> | <span data-ttu-id="3ed1b-127">...avec ce **système d’exploitation cluster**</span><span class="sxs-lookup"><span data-stu-id="3ed1b-127">...with this **cluster operating system**</span></span> | <span data-ttu-id="3ed1b-128">...depuis ce **système d’exploitation cluster**</span><span class="sxs-lookup"><span data-stu-id="3ed1b-128">...from this **client operating system**</span></span> |
|:--- |:---:|:---:|:--- |:--- |
| [<span data-ttu-id="3ed1b-129">Affichage Hive</span><span class="sxs-lookup"><span data-stu-id="3ed1b-129">Hive View</span></span>](hdinsight-hadoop-use-hive-ambari-view.md) |<span data-ttu-id="3ed1b-130">✔</span><span class="sxs-lookup"><span data-stu-id="3ed1b-130">✔</span></span> |<span data-ttu-id="3ed1b-131">✔</span><span class="sxs-lookup"><span data-stu-id="3ed1b-131">✔</span></span> |<span data-ttu-id="3ed1b-132">Linux</span><span class="sxs-lookup"><span data-stu-id="3ed1b-132">Linux</span></span> |<span data-ttu-id="3ed1b-133">N’importe lequel (basé sur le navigateur)</span><span class="sxs-lookup"><span data-stu-id="3ed1b-133">Any (browser based)</span></span> |
| [<span data-ttu-id="3ed1b-134">Client Beeline</span><span class="sxs-lookup"><span data-stu-id="3ed1b-134">Beeline client</span></span>](hdinsight-hadoop-use-hive-beeline.md) |<span data-ttu-id="3ed1b-135">✔</span><span class="sxs-lookup"><span data-stu-id="3ed1b-135">✔</span></span> |<span data-ttu-id="3ed1b-136">✔</span><span class="sxs-lookup"><span data-stu-id="3ed1b-136">✔</span></span> |<span data-ttu-id="3ed1b-137">Linux</span><span class="sxs-lookup"><span data-stu-id="3ed1b-137">Linux</span></span> |<span data-ttu-id="3ed1b-138">Linux, Unix, Mac OS X ou Windows</span><span class="sxs-lookup"><span data-stu-id="3ed1b-138">Linux, Unix, Mac OS X, or Windows</span></span> |
| [<span data-ttu-id="3ed1b-139">API REST</span><span class="sxs-lookup"><span data-stu-id="3ed1b-139">REST API</span></span>](hdinsight-hadoop-use-hive-curl.md) |&nbsp; |<span data-ttu-id="3ed1b-140">✔</span><span class="sxs-lookup"><span data-stu-id="3ed1b-140">✔</span></span> |<span data-ttu-id="3ed1b-141">Linux ou Windows*</span><span class="sxs-lookup"><span data-stu-id="3ed1b-141">Linux or Windows*</span></span> |<span data-ttu-id="3ed1b-142">Linux, Unix, Mac OS X ou Windows</span><span class="sxs-lookup"><span data-stu-id="3ed1b-142">Linux, Unix, Mac OS X, or Windows</span></span> |
| [<span data-ttu-id="3ed1b-143">Outils HDInsight pour Visual Studio</span><span class="sxs-lookup"><span data-stu-id="3ed1b-143">HDInsight tools for Visual Studio</span></span>](hdinsight-hadoop-use-hive-visual-studio.md) |&nbsp; |<span data-ttu-id="3ed1b-144">✔</span><span class="sxs-lookup"><span data-stu-id="3ed1b-144">✔</span></span> |<span data-ttu-id="3ed1b-145">Linux ou Windows*</span><span class="sxs-lookup"><span data-stu-id="3ed1b-145">Linux or Windows*</span></span> |<span data-ttu-id="3ed1b-146">Windows</span><span class="sxs-lookup"><span data-stu-id="3ed1b-146">Windows</span></span> |
| [<span data-ttu-id="3ed1b-147">Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="3ed1b-147">Windows PowerShell</span></span>](hdinsight-hadoop-use-hive-powershell.md) |&nbsp; |<span data-ttu-id="3ed1b-148">✔</span><span class="sxs-lookup"><span data-stu-id="3ed1b-148">✔</span></span> |<span data-ttu-id="3ed1b-149">Linux ou Windows*</span><span class="sxs-lookup"><span data-stu-id="3ed1b-149">Linux or Windows*</span></span> |<span data-ttu-id="3ed1b-150">Windows</span><span class="sxs-lookup"><span data-stu-id="3ed1b-150">Windows</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="3ed1b-151">\* Linux est le seul système d’exploitation utilisé sur HDInsight version 3.4 ou supérieure.</span><span class="sxs-lookup"><span data-stu-id="3ed1b-151">\* Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="3ed1b-152">Pour plus d’informations, consultez [Suppression de HDInsight sous Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="3ed1b-152">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>
>
> <span data-ttu-id="3ed1b-153">Si vous utilisez un cluster HDInsight basé sur Windows, vous pouvez utiliser la [console de requête](hdinsight-hadoop-use-hive-query-console.md) depuis votre navigateur ou [Bureau à distance](hdinsight-hadoop-use-hive-remote-desktop.md) pour exécuter des requêtes Hive.</span><span class="sxs-lookup"><span data-stu-id="3ed1b-153">If you are using a Windows-based HDInsight cluster, you can use the [Query console](hdinsight-hadoop-use-hive-query-console.md) from your browser or [Remote Desktop](hdinsight-hadoop-use-hive-remote-desktop.md) to run Hive queries.</span></span>

## <a name="hiveql-language-reference"></a><span data-ttu-id="3ed1b-154">Référence du langage HiveQL</span><span class="sxs-lookup"><span data-stu-id="3ed1b-154">HiveQL language reference</span></span>

<span data-ttu-id="3ed1b-155">La référence du langage HiveQL est disponible dans le [manuel (https://cwiki.apache.org/confluence/display/Hive/LanguageManual)](https://cwiki.apache.org/confluence/display/Hive/LanguageManual).</span><span class="sxs-lookup"><span data-stu-id="3ed1b-155">HiveQL language reference is available in the [language manual (https://cwiki.apache.org/confluence/display/Hive/LanguageManual)](https://cwiki.apache.org/confluence/display/Hive/LanguageManual).</span></span>

## <a name="hive-and-data-structure"></a><span data-ttu-id="3ed1b-156">Hive et structure des données</span><span class="sxs-lookup"><span data-stu-id="3ed1b-156">Hive and data structure</span></span>

<span data-ttu-id="3ed1b-157">Hive est capable de travailler avec des données structurées et semi-structurées.</span><span class="sxs-lookup"><span data-stu-id="3ed1b-157">Hive understands how to work with structured and semi-structured data.</span></span> <span data-ttu-id="3ed1b-158">Par exemple, les fichiers texte dans lesquels les champs sont délimités par des caractères spécifiques.</span><span class="sxs-lookup"><span data-stu-id="3ed1b-158">For example, text files where the fields are delimited by specific characters.</span></span> <span data-ttu-id="3ed1b-159">L’instruction HiveQL suivante crée une table à partir de données délimitées par des espaces :</span><span class="sxs-lookup"><span data-stu-id="3ed1b-159">The following HiveQL statement creates a table over space-delimited data:</span></span>

```hiveql
CREATE EXTERNAL TABLE log4jLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
ROW FORMAT DELIMITED FIELDS TERMINATED BY ' '
STORED AS TEXTFILE LOCATION '/example/data/';
```

<span data-ttu-id="3ed1b-160">Hive prend également en charge un **sérialiseur/ désérialiseur (SerDe)** personnalisé pour des données structurées de manière irrégulière ou complexes.</span><span class="sxs-lookup"><span data-stu-id="3ed1b-160">Hive also supports custom **serializer/deserializers (SerDe)** for complex or irregularly structured data.</span></span> <span data-ttu-id="3ed1b-161">Pour plus d’informations, consultez le document [Utilisation d’un SerDe JSON personnalisé avec HDInsight](http://blogs.msdn.com/b/bigdatasupport/archive/2014/06/18/how-to-use-a-custom-json-serde-with-microsoft-azure-hdinsight.aspx).</span><span class="sxs-lookup"><span data-stu-id="3ed1b-161">For more information, see the [How to use a custom JSON SerDe with HDInsight](http://blogs.msdn.com/b/bigdatasupport/archive/2014/06/18/how-to-use-a-custom-json-serde-with-microsoft-azure-hdinsight.aspx) document.</span></span>

<span data-ttu-id="3ed1b-162">Pour plus d’informations sur les formats de fichiers pris en charge par Hive, consultez le [manuel (https://cwiki.apache.org/confluence/display/Hive/LanguageManual)](https://cwiki.apache.org/confluence/display/Hive/LanguageManual)</span><span class="sxs-lookup"><span data-stu-id="3ed1b-162">For more information on file formats supported by Hive, see the [Language manual (https://cwiki.apache.org/confluence/display/Hive/LanguageManual)](https://cwiki.apache.org/confluence/display/Hive/LanguageManual)</span></span>

## <a name="hive-internal-tables-vs-external-tables"></a><span data-ttu-id="3ed1b-163">Tables internes et externes Hive</span><span class="sxs-lookup"><span data-stu-id="3ed1b-163">Hive internal tables vs external tables</span></span>

<span data-ttu-id="3ed1b-164">Hive vous permet de créer deux types de tables :</span><span class="sxs-lookup"><span data-stu-id="3ed1b-164">There are two types of tables that you can create with Hive:</span></span>

* <span data-ttu-id="3ed1b-165">__Interne__ : les données sont stockées dans l’entrepôt de données Hive.</span><span class="sxs-lookup"><span data-stu-id="3ed1b-165">__Internal__: Data is stored in the Hive data warehouse.</span></span> <span data-ttu-id="3ed1b-166">L’entrepôt de données se trouve dans `/hive/warehouse/` sur le stockage par défaut du cluster.</span><span class="sxs-lookup"><span data-stu-id="3ed1b-166">The data warehouse is located at `/hive/warehouse/` on the default storage for the cluster.</span></span>

    <span data-ttu-id="3ed1b-167">Utilisez des tables internes quand :</span><span class="sxs-lookup"><span data-stu-id="3ed1b-167">Use internal tables when:</span></span>

    * <span data-ttu-id="3ed1b-168">les données sont temporaires.</span><span class="sxs-lookup"><span data-stu-id="3ed1b-168">Data is temporary.</span></span>
    * <span data-ttu-id="3ed1b-169">Vous voulez que Hive gère le cycle de vie de la table et des données.</span><span class="sxs-lookup"><span data-stu-id="3ed1b-169">You want Hive to manage the lifecycle of the table and data.</span></span>

* <span data-ttu-id="3ed1b-170">__Externe__ : les données sont stockées en dehors de l’entrepôt de données.</span><span class="sxs-lookup"><span data-stu-id="3ed1b-170">__External__: Data is stored outside the data warehouse.</span></span> <span data-ttu-id="3ed1b-171">Les données peuvent être stockées sur tout stockage accessible par le cluster.</span><span class="sxs-lookup"><span data-stu-id="3ed1b-171">The data can be stored on any storage accessible by the cluster.</span></span>

    <span data-ttu-id="3ed1b-172">Utilisez des tables externes quand :</span><span class="sxs-lookup"><span data-stu-id="3ed1b-172">Use external tables when:</span></span>

    * <span data-ttu-id="3ed1b-173">Les données sont également utilisées en dehors de Hive.</span><span class="sxs-lookup"><span data-stu-id="3ed1b-173">The data is also used outside of Hive.</span></span> <span data-ttu-id="3ed1b-174">Par exemple, les fichiers de données sont mis à jour par un autre processus (qui ne verrouille pas les fichiers.)</span><span class="sxs-lookup"><span data-stu-id="3ed1b-174">For example, the data files are updated by another process (that does not lock the files.)</span></span>
    * <span data-ttu-id="3ed1b-175">Les données doivent rester dans l’emplacement sous-jacent, même après suppression de la table.</span><span class="sxs-lookup"><span data-stu-id="3ed1b-175">Data needs to remain in the underlying location, even after dropping the table.</span></span>
    * <span data-ttu-id="3ed1b-176">Vous avez besoin d’un emplacement personnalisé, par exemple un compte de stockage non sélectionné par défaut.</span><span class="sxs-lookup"><span data-stu-id="3ed1b-176">You need a custom location, such as a non-default storage account.</span></span>
    * <span data-ttu-id="3ed1b-177">Un programme autre que Hive gère le format de données, l’emplacement, etc.</span><span class="sxs-lookup"><span data-stu-id="3ed1b-177">A program other than hive manages the data format, location, etc.</span></span>

<span data-ttu-id="3ed1b-178">Pour plus d’informations, consultez le billet de blog [Introduction aux tables interne et externe Hive][cindygross-hive-tables].</span><span class="sxs-lookup"><span data-stu-id="3ed1b-178">For more information, see the [Hive Internal and External Tables Intro][cindygross-hive-tables] blog post.</span></span>

## <a name="user-defined-functions-udf"></a><span data-ttu-id="3ed1b-179">Fonctions définies par l’utilisateur (UDF)</span><span class="sxs-lookup"><span data-stu-id="3ed1b-179">User-defined functions (UDF)</span></span>

<span data-ttu-id="3ed1b-180">Hive peut également être étendu via des **fonctions définies par l'utilisateur (UDF)**.</span><span class="sxs-lookup"><span data-stu-id="3ed1b-180">Hive can also be extended through **user-defined functions (UDF)**.</span></span> <span data-ttu-id="3ed1b-181">Une fonction UDF vous permet d'implémenter une fonctionnalité ou une logique qui n'est pas facilement modelée en HiveQL.</span><span class="sxs-lookup"><span data-stu-id="3ed1b-181">A UDF allows you to implement functionality or logic that isn't easily modeled in HiveQL.</span></span> <span data-ttu-id="3ed1b-182">Pour obtenir un exemple d’utilisation des fonctions définies par l’utilisateur (UDF) avec Hive, consultez les documents suivants :</span><span class="sxs-lookup"><span data-stu-id="3ed1b-182">For an example of using UDFs with Hive, see the following documents:</span></span>

* [<span data-ttu-id="3ed1b-183">Utiliser une fonction Java définie par l’utilisateur avec Hive</span><span class="sxs-lookup"><span data-stu-id="3ed1b-183">Use a Java user-defined function with Hive</span></span>](hdinsight-hadoop-hive-java-udf.md)

* [<span data-ttu-id="3ed1b-184">Utiliser une fonction Python définie par l’utilisateur avec Hive et Pig</span><span class="sxs-lookup"><span data-stu-id="3ed1b-184">Use a Python user-defined function with Hive and Pig</span></span>](hdinsight-python.md)

* [<span data-ttu-id="3ed1b-185">Utiliser une fonction C# définie par l’utilisateur avec Hive et Pig</span><span class="sxs-lookup"><span data-stu-id="3ed1b-185">Use a C# user-defined function with Hive and Pig</span></span>](hdinsight-hadoop-hive-pig-udf-dotnet-csharp.md)

* [<span data-ttu-id="3ed1b-186">Guide pratique pour ajouter une fonction Hive définie par l’utilisateur à HDInsight</span><span class="sxs-lookup"><span data-stu-id="3ed1b-186">How to add a custom Hive user-defined function to HDInsight</span></span>](http://blogs.msdn.com/b/bigdatasupport/archive/2014/01/14/how-to-add-custom-hive-udfs-to-hdinsight.aspx)

* [<span data-ttu-id="3ed1b-187">Exemple de fonction Hive définie par l’utilisateur pour convertir les formats date/heure en horodatage Hive</span><span class="sxs-lookup"><span data-stu-id="3ed1b-187">An example Hive user-defined function to convert date/time formats to Hive timestamp</span></span>](https://github.com/Azure-Samples/hdinsight-java-hive-udf)

## <span data-ttu-id="3ed1b-188"><a id="data"></a>Exemple de données</span><span class="sxs-lookup"><span data-stu-id="3ed1b-188"><a id="data"></a>Example data</span></span>

<span data-ttu-id="3ed1b-189">Hive sur HDInsight est préchargé avec une table interne nommée `hivesampletable`.</span><span class="sxs-lookup"><span data-stu-id="3ed1b-189">Hive on HDInsight comes pre-loaded with an internal table named `hivesampletable`.</span></span> <span data-ttu-id="3ed1b-190">HDInsight fournit également des exemples de jeux de données pouvant être utilisés avec Hive.</span><span class="sxs-lookup"><span data-stu-id="3ed1b-190">HDInsight also provides example data sets that can be used with Hive.</span></span> <span data-ttu-id="3ed1b-191">Ces jeux de données sont stockés dans les répertoires `/example/data` et `/HdiSamples`.</span><span class="sxs-lookup"><span data-stu-id="3ed1b-191">These data sets are stored in the `/example/data` and `/HdiSamples` directories.</span></span> <span data-ttu-id="3ed1b-192">Ces répertoires sont disponibles dans le stockage par défaut de votre cluster.</span><span class="sxs-lookup"><span data-stu-id="3ed1b-192">These directories exist in the default storage for your cluster.</span></span>

## <span data-ttu-id="3ed1b-193"><a id="job"></a>Exemple de requête Hive</span><span class="sxs-lookup"><span data-stu-id="3ed1b-193"><a id="job"></a>Example Hive query</span></span>

<span data-ttu-id="3ed1b-194">Les instructions HiveQL suivantes projettent des colonnes sur le fichier `/example/data/sample.log` :</span><span class="sxs-lookup"><span data-stu-id="3ed1b-194">The following HiveQL statements project columns onto the `/example/data/sample.log` file:</span></span>

    set hive.execution.engine=tez;
    DROP TABLE log4jLogs;
    CREATE EXTERNAL TABLE log4jLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
    ROW FORMAT DELIMITED FIELDS TERMINATED BY ' '
    STORED AS TEXTFILE LOCATION '/example/data/';
    SELECT t4 AS sev, COUNT(*) AS count FROM log4jLogs WHERE t4 = '[ERROR]' AND INPUT__FILE__NAME LIKE '%.log' GROUP BY t4;

<span data-ttu-id="3ed1b-195">Dans l’exemple précédent, les instructions HiveQL effectuent les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="3ed1b-195">In the previous example, the HiveQL statements perform the following actions:</span></span>

* <span data-ttu-id="3ed1b-196">`set hive.execution.engine=tez;`: définit le moteur d’exécution pour utiliser Tez.</span><span class="sxs-lookup"><span data-stu-id="3ed1b-196">`set hive.execution.engine=tez;`: Sets the execution engine to use Tez.</span></span> <span data-ttu-id="3ed1b-197">L’utilisation de Tez au lieu de MapReduce peut augmenter les performances de requête.</span><span class="sxs-lookup"><span data-stu-id="3ed1b-197">Using Tez instead of MapReduce can provide an increase in query performance.</span></span> <span data-ttu-id="3ed1b-198">Pour plus d’informations sur Tez, consultez la section [Utilisation d’Apache Tez pour des performances améliorées](#usetez) .</span><span class="sxs-lookup"><span data-stu-id="3ed1b-198">For more information on Tez, see the [Use Apache Tez for improved performance](#usetez) section.</span></span>

    > [!NOTE]
    > <span data-ttu-id="3ed1b-199">Cette instruction est uniquement requise lorsque vous utilisez un cluster HDInsight sous Windows.</span><span class="sxs-lookup"><span data-stu-id="3ed1b-199">This statement is only required when using a Windows-based HDInsight cluster.</span></span> <span data-ttu-id="3ed1b-200">Tez est le moteur d’exécution par défaut pour HDInsight sous Linux.</span><span class="sxs-lookup"><span data-stu-id="3ed1b-200">Tez is the default execution engine for Linux-based HDInsight.</span></span>

* <span data-ttu-id="3ed1b-201">`DROP TABLE` : si la table existe déjà, supprimez-la.</span><span class="sxs-lookup"><span data-stu-id="3ed1b-201">`DROP TABLE`: If the table already exists, delete it.</span></span>

* <span data-ttu-id="3ed1b-202">`CREATE EXTERNAL TABLE` : crée une table **externe** dans Hive.</span><span class="sxs-lookup"><span data-stu-id="3ed1b-202">`CREATE EXTERNAL TABLE`: Creates a new **external** table in Hive.</span></span> <span data-ttu-id="3ed1b-203">Les tables externes stockent uniquement la définition de table dans Hive.</span><span class="sxs-lookup"><span data-stu-id="3ed1b-203">External tables only store the table definition in Hive.</span></span> <span data-ttu-id="3ed1b-204">Les données restent à l’emplacement d’origine, dans le format d’origine.</span><span class="sxs-lookup"><span data-stu-id="3ed1b-204">The data is left in the original location and in the original format.</span></span>

* <span data-ttu-id="3ed1b-205">`ROW FORMAT` : indique à Hive le mode de formatage des données.</span><span class="sxs-lookup"><span data-stu-id="3ed1b-205">`ROW FORMAT`: Tells Hive how the data is formatted.</span></span> <span data-ttu-id="3ed1b-206">Dans ce cas, les champs de chaque journal sont séparés par un espace.</span><span class="sxs-lookup"><span data-stu-id="3ed1b-206">In this case, the fields in each log are separated by a space.</span></span>

* <span data-ttu-id="3ed1b-207">`STORED AS TEXTFILE LOCATION` : indique à Hive où sont stockées les données (répertoire `example/data`) et qu'elles sont stockées sous forme de texte.</span><span class="sxs-lookup"><span data-stu-id="3ed1b-207">`STORED AS TEXTFILE LOCATION`: Tells Hive where the data is stored (the `example/data` directory) and that it is stored as text.</span></span> <span data-ttu-id="3ed1b-208">Les données peuvent être dans un seul fichier ou réparties sur plusieurs fichiers dans le répertoire.</span><span class="sxs-lookup"><span data-stu-id="3ed1b-208">The data can be in one file or spread across multiple files within the directory.</span></span>

* <span data-ttu-id="3ed1b-209">`SELECT` : sélectionne toutes les lignes où la colonne **t4** contient la valeur **[ERROR]**.</span><span class="sxs-lookup"><span data-stu-id="3ed1b-209">`SELECT`: Selects a count of all rows where the column **t4** contains the value **[ERROR]**.</span></span> <span data-ttu-id="3ed1b-210">Cette instruction renvoie la valeur **3**, car trois lignes contiennent cette valeur.</span><span class="sxs-lookup"><span data-stu-id="3ed1b-210">This statement returns a value of **3** because there are three rows that contain this value.</span></span>

* <span data-ttu-id="3ed1b-211">`INPUT__FILE__NAME LIKE '%.log'`- Hive tente d’appliquer le schéma à tous les fichiers dans le répertoire.</span><span class="sxs-lookup"><span data-stu-id="3ed1b-211">`INPUT__FILE__NAME LIKE '%.log'` - Hive attempts to apply the schema to all files in the directory.</span></span> <span data-ttu-id="3ed1b-212">Dans ce cas, le répertoire contient des fichiers qui ne correspondent pas au schéma.</span><span class="sxs-lookup"><span data-stu-id="3ed1b-212">In this case, the directory contains files that do not match the schema.</span></span> <span data-ttu-id="3ed1b-213">Pour éviter que des données incorrectes n’apparaissent dans les résultats, cette instruction indique à Hive de retourner uniquement des données provenant de fichiers se terminant par .log.</span><span class="sxs-lookup"><span data-stu-id="3ed1b-213">To prevent garbage data in the results, this statement tells Hive that we should only return data from files ending in .log.</span></span>

> [!NOTE]
> <span data-ttu-id="3ed1b-214">Les tables externes doivent être utilisées lorsque vous vous attendez à ce que les données sous-jacentes soient mises à jour par une source externe,</span><span class="sxs-lookup"><span data-stu-id="3ed1b-214">External tables should be used when you expect the underlying data to be updated by an external source.</span></span> <span data-ttu-id="3ed1b-215">Par exemple, un processus de chargement de données automatisé ou une opération MapReduce.</span><span class="sxs-lookup"><span data-stu-id="3ed1b-215">For example, an automated data upload process, or MapReduce operation.</span></span>
>
> <span data-ttu-id="3ed1b-216">La suppression d'une table externe ne supprime **pas** les données, mais seulement la définition de la table.</span><span class="sxs-lookup"><span data-stu-id="3ed1b-216">Dropping an external table does **not** delete the data, it only deletes the table definition.</span></span>

<span data-ttu-id="3ed1b-217">Pour créer une table **interne** plutôt qu’externe, utilisez le code HiveQL suivant :</span><span class="sxs-lookup"><span data-stu-id="3ed1b-217">To create an **internal** table instead of external, use the following HiveQL:</span></span>

    set hive.execution.engine=tez;
    CREATE TABLE IF NOT EXISTS errorLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
    STORED AS ORC;
    INSERT OVERWRITE TABLE errorLogs
    SELECT t1, t2, t3, t4, t5, t6, t7 FROM log4jLogs WHERE t4 = '[ERROR]';

<span data-ttu-id="3ed1b-218">Ces instructions effectuent les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="3ed1b-218">These statements perform the following actions:</span></span>

* <span data-ttu-id="3ed1b-219">`CREATE TABLE IF NOT EXISTS` : si la table n’existe pas, créez-la.</span><span class="sxs-lookup"><span data-stu-id="3ed1b-219">`CREATE TABLE IF NOT EXISTS`: If the table does not exist, create it.</span></span> <span data-ttu-id="3ed1b-220">Étant donné que le mot-clé **EXTERNAL** n’est pas utilisé, cette instruction crée une table interne.</span><span class="sxs-lookup"><span data-stu-id="3ed1b-220">Because the **EXTERNAL** keyword is not used, this statement creates an internal table.</span></span> <span data-ttu-id="3ed1b-221">La table est stockée dans l’entrepôt de données Hive et gérée intégralement par Hive.</span><span class="sxs-lookup"><span data-stu-id="3ed1b-221">The table is stored in the Hive data warehouse and is managed completely by Hive.</span></span>

* <span data-ttu-id="3ed1b-222">`STORED AS ORC` : stocke les données dans un format ORC (Optimized Row Columnar).</span><span class="sxs-lookup"><span data-stu-id="3ed1b-222">`STORED AS ORC`: Stores the data in Optimized Row Columnar (ORC) format.</span></span> <span data-ttu-id="3ed1b-223">ORC est un format particulièrement efficace et optimisé pour le stockage de données Hive.</span><span class="sxs-lookup"><span data-stu-id="3ed1b-223">ORC is a highly optimized and efficient format for storing Hive data.</span></span>

* <span data-ttu-id="3ed1b-224">`INSERT OVERWRITE ... SELECT` : sélectionne des lignes de la table **log4jLogs** qui contient **[ERROR]**, puis insère les données dans la table **errorLogs**.</span><span class="sxs-lookup"><span data-stu-id="3ed1b-224">`INSERT OVERWRITE ... SELECT`: Selects rows from the **log4jLogs** table that contains **[ERROR]**, and then inserts the data into the **errorLogs** table.</span></span>

> [!NOTE]
> <span data-ttu-id="3ed1b-225">Contrairement aux tables externes, la suppression d’une table interne entraîne également la suppression des données sous-jacentes.</span><span class="sxs-lookup"><span data-stu-id="3ed1b-225">Unlike external tables, dropping an internal table also deletes the underlying data.</span></span>

## <a name="improve-hive-query-performance"></a><span data-ttu-id="3ed1b-226">Améliorer les performances des requêtes Hive</span><span class="sxs-lookup"><span data-stu-id="3ed1b-226">Improve Hive query performance</span></span>

### <span data-ttu-id="3ed1b-227"><a id="usetez"></a>Apache Tez</span><span class="sxs-lookup"><span data-stu-id="3ed1b-227"><a id="usetez"></a>Apache Tez</span></span>

<span data-ttu-id="3ed1b-228">[Apache Tez](http://tez.apache.org) est une infrastructure qui permet une exécution à l'échelle beaucoup plus efficace pour les applications, telles que Hive, qui manipulent de grandes quantités de données.</span><span class="sxs-lookup"><span data-stu-id="3ed1b-228">[Apache Tez](http://tez.apache.org) is a framework that allows data intensive applications, such as Hive, to run much more efficiently at scale.</span></span> <span data-ttu-id="3ed1b-229">Tez est activé par défaut pour les clusters HDInsight basés sur Linux.</span><span class="sxs-lookup"><span data-stu-id="3ed1b-229">Tez is enabled by default for Linux-based HDInsight clusters.</span></span>

> [!NOTE]
> <span data-ttu-id="3ed1b-230">Tez est actuellement désactivé par défaut pour les clusters HDInsight basés sur Windows, et il doit être activé.</span><span class="sxs-lookup"><span data-stu-id="3ed1b-230">Tez is currently off by default for Windows-based HDInsight clusters and it must be enabled.</span></span> <span data-ttu-id="3ed1b-231">Pour pouvoir tirer parti de Tez, vous devez définir la valeur suivante pour une requête Hive :</span><span class="sxs-lookup"><span data-stu-id="3ed1b-231">To take advantage of Tez, the following value must be set for a Hive query:</span></span>
>
> `set hive.execution.engine=tez;`
>
> <span data-ttu-id="3ed1b-232">Tez est le moteur par défaut pour les clusters HDInsight sous Linux.</span><span class="sxs-lookup"><span data-stu-id="3ed1b-232">Tez is the default engine for Linux-based HDInsight clusters.</span></span>

<span data-ttu-id="3ed1b-233">Les [documents de conception Hive sur Tez](https://cwiki.apache.org/confluence/display/Hive/Hive+on+Tez) contiennent des informations détaillées sur les options d’implémentation et les configurations du réglage.</span><span class="sxs-lookup"><span data-stu-id="3ed1b-233">The [Hive on Tez design documents](https://cwiki.apache.org/confluence/display/Hive/Hive+on+Tez) contains details about the implementation choices and tuning configurations.</span></span>

<span data-ttu-id="3ed1b-234">Pour faciliter le débogage des tâches exécutées en utilisant Tez, HDInsight fournit les interfaces utilisateur web suivantes qui vous permettent d'afficher les détails des tâches Tez :</span><span class="sxs-lookup"><span data-stu-id="3ed1b-234">To aid in debugging jobs ran using Tez, HDInsight provides the following web UIs that allow you to view details of Tez jobs:</span></span>

* [<span data-ttu-id="3ed1b-235">Utilisez la vue Tez Ambari sur HDInsight Linux</span><span class="sxs-lookup"><span data-stu-id="3ed1b-235">Use the Ambari Tez view on Linux-based HDInsight</span></span>](hdinsight-debug-ambari-tez-view.md)

* [<span data-ttu-id="3ed1b-236">Utiliser l'interface utilisateur Tez sur HDInsight Windows</span><span class="sxs-lookup"><span data-stu-id="3ed1b-236">Use the Tez UI on Windows-based HDInsight</span></span>](hdinsight-debug-tez-ui.md)

### <a name="low-latency-analytical-processing-llap"></a><span data-ttu-id="3ed1b-237">Low Latency Analytical Processing (LLAP)</span><span class="sxs-lookup"><span data-stu-id="3ed1b-237">Low Latency Analytical Processing (LLAP)</span></span>

<span data-ttu-id="3ed1b-238">[LLAP](https://cwiki.apache.org/confluence/display/Hive/LLAP) (parfois appelé Live Long and Process) est une nouvelle fonctionnalité de Hive 2.0 qui permet la mise en cache en mémoire des requêtes.</span><span class="sxs-lookup"><span data-stu-id="3ed1b-238">[LLAP](https://cwiki.apache.org/confluence/display/Hive/LLAP) (sometimes known as Live Long and Process) is a new feature in Hive 2.0 that allows in-memory caching of queries.</span></span> <span data-ttu-id="3ed1b-239">LLAP accélère considérablement les requêtes Hive, avec dans certains cas des vitesses jusqu’à [26 fois plus rapides qu’avec Hive 1.x](https://hortonworks.com/blog/announcing-apache-hive-2-1-25x-faster-queries-much/).</span><span class="sxs-lookup"><span data-stu-id="3ed1b-239">LLAP makes Hive queries much faster, up to [26x faster than Hive 1.x in some cases](https://hortonworks.com/blog/announcing-apache-hive-2-1-25x-faster-queries-much/).</span></span>

<span data-ttu-id="3ed1b-240">HDInsight propose la fonctionnalité LLAP dans le cluster de type Hive interactif.</span><span class="sxs-lookup"><span data-stu-id="3ed1b-240">HDInsight provides LLAP in the Interactive Hive cluster type.</span></span> <span data-ttu-id="3ed1b-241">Pour plus d’informations, consultez le document [Démarrer avec Hive interactif](hdinsight-hadoop-use-interactive-hive.md).</span><span class="sxs-lookup"><span data-stu-id="3ed1b-241">For more information, see the [Start with Interactive Hive](hdinsight-hadoop-use-interactive-hive.md) document.</span></span>

## <a name="hive-jobs-and-sql-server-integration-services"></a><span data-ttu-id="3ed1b-242">Tâches Hive et SQL Server Integration Services</span><span class="sxs-lookup"><span data-stu-id="3ed1b-242">Hive jobs and SQL Server Integration Services</span></span>

<span data-ttu-id="3ed1b-243">Vous pouvez utiliser les services SQL Server Integration Services (SSIS) pour exécuter un travail Hive.</span><span class="sxs-lookup"><span data-stu-id="3ed1b-243">You can use SQL Server Integration Services (SSIS) to run a Hive job.</span></span> <span data-ttu-id="3ed1b-244">Le pack de fonctionnalités Azure pour SSIS fournit les composants suivants, compatibles avec les tâches Hive sur HDInsight.</span><span class="sxs-lookup"><span data-stu-id="3ed1b-244">The Azure Feature Pack for SSIS provides the following components that work with Hive jobs on HDInsight.</span></span>

* <span data-ttu-id="3ed1b-245">[Tâche Hive d’Azure HDInsight][hivetask]</span><span class="sxs-lookup"><span data-stu-id="3ed1b-245">[Azure HDInsight Hive Task][hivetask]</span></span>

* <span data-ttu-id="3ed1b-246">[Gestionnaire de connexions d’abonnement Azure][connectionmanager]</span><span class="sxs-lookup"><span data-stu-id="3ed1b-246">[Azure Subscription Connection Manager][connectionmanager]</span></span>

<span data-ttu-id="3ed1b-247">Pour en savoir plus sur le pack de fonctionnalités Azure pour SSIS, cliquez [ici][ssispack].</span><span class="sxs-lookup"><span data-stu-id="3ed1b-247">Learn more about the Azure Feature Pack for SSIS [here][ssispack].</span></span>

## <span data-ttu-id="3ed1b-248"><a id="nextsteps"></a>Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="3ed1b-248"><a id="nextsteps"></a>Next steps</span></span>

<span data-ttu-id="3ed1b-249">Maintenant que vous connaissez Hive et que vous avez vu comment l’utiliser avec Hadoop dans HDInsight, utilisez les liens suivants pour découvrir d'autres façons d'utiliser Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="3ed1b-249">Now that you've learned what Hive is and how to use it with Hadoop in HDInsight, use the following links to explore other ways to work with Azure HDInsight.</span></span>

* <span data-ttu-id="3ed1b-250">[Téléchargement de données vers HDInsight][hdinsight-upload-data]</span><span class="sxs-lookup"><span data-stu-id="3ed1b-250">[Upload data to HDInsight][hdinsight-upload-data]</span></span>
* <span data-ttu-id="3ed1b-251">[Utilisation de Pig avec HDInsight][hdinsight-use-pig]</span><span class="sxs-lookup"><span data-stu-id="3ed1b-251">[Use Pig with HDInsight][hdinsight-use-pig]</span></span>
* <span data-ttu-id="3ed1b-252">[Utilisation des tâches MapReduce avec HDInsight][hdinsight-use-mapreduce]</span><span class="sxs-lookup"><span data-stu-id="3ed1b-252">[Use MapReduce jobs with HDInsight][hdinsight-use-mapreduce]</span></span>

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
