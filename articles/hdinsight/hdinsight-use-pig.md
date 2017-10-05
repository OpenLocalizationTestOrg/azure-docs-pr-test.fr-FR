---
title: Utilisation de Hadoop Pig dans HDInsight | Microsoft Docs
description: Utilisation de Pig avec Hadoop sur HDInsight.
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: acfeb52b-4b81-4a7d-af77-3e9908407404
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/15/2017
ms.author: larryfr
ms.openlocfilehash: 474f901ffdaf1ed372ace19076ef723b8b10cb9a
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="use-pig-with-hadoop-on-hdinsight"></a><span data-ttu-id="6c4ba-103">Utilisation de Pig avec Hadoop sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="6c4ba-103">Use Pig with Hadoop on HDInsight</span></span>

<span data-ttu-id="6c4ba-104">Découvrez comment utiliser [Apache Pig](http://pig.apache.org/) avec HDInsight...</span><span class="sxs-lookup"><span data-stu-id="6c4ba-104">Learn how to use [Apache Pig](http://pig.apache.org/) with HDInsight...</span></span>

<span data-ttu-id="6c4ba-105">Pig est une plateforme qui permet de créer des programmes pour Hadoop dans un langage procédural appelé *Pig Latin*.</span><span class="sxs-lookup"><span data-stu-id="6c4ba-105">Pig is a platform for creating programs for Hadoop by using a procedural language known as *Pig Latin*.</span></span> <span data-ttu-id="6c4ba-106">Pig est une alternative à Java, dédiée à la création de solutions *MapReduce* , qui est incluse avec Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="6c4ba-106">Pig is an alternative to Java for creating *MapReduce* solutions, and it is included with Azure HDInsight.</span></span> <span data-ttu-id="6c4ba-107">Utilisez le tableau suivant pour découvrir les différentes façons dont Pig peut être utilisé avec HDInsight :</span><span class="sxs-lookup"><span data-stu-id="6c4ba-107">Use the following table to discover the various ways that Pig can be used with HDInsight:</span></span>

| <span data-ttu-id="6c4ba-108">**Utilisez-le** si vous souhaitez...</span><span class="sxs-lookup"><span data-stu-id="6c4ba-108">**Use this** if you want...</span></span> | <span data-ttu-id="6c4ba-109">... un interpréteur de commandes **interactif**</span><span class="sxs-lookup"><span data-stu-id="6c4ba-109">...an **interactive** shell</span></span> | <span data-ttu-id="6c4ba-110">... un traitement par **lots**</span><span class="sxs-lookup"><span data-stu-id="6c4ba-110">...**batch** processing</span></span> | <span data-ttu-id="6c4ba-111">...avec ce **système d’exploitation cluster**</span><span class="sxs-lookup"><span data-stu-id="6c4ba-111">...with this **cluster operating system**</span></span> | <span data-ttu-id="6c4ba-112">...depuis ce **système d’exploitation cluster**</span><span class="sxs-lookup"><span data-stu-id="6c4ba-112">...from this **client operating system**</span></span> |
|:--- |:---:|:---:|:--- |:--- |
| [<span data-ttu-id="6c4ba-113">SSH</span><span class="sxs-lookup"><span data-stu-id="6c4ba-113">SSH</span></span>](hdinsight-hadoop-use-pig-ssh.md) |<span data-ttu-id="6c4ba-114">✔</span><span class="sxs-lookup"><span data-stu-id="6c4ba-114">✔</span></span> |<span data-ttu-id="6c4ba-115">✔</span><span class="sxs-lookup"><span data-stu-id="6c4ba-115">✔</span></span> |<span data-ttu-id="6c4ba-116">Linux</span><span class="sxs-lookup"><span data-stu-id="6c4ba-116">Linux</span></span> |<span data-ttu-id="6c4ba-117">Linux, Unix, Mac OS X ou Windows</span><span class="sxs-lookup"><span data-stu-id="6c4ba-117">Linux, Unix, Mac OS X, or Windows</span></span> |
| [<span data-ttu-id="6c4ba-118">API REST</span><span class="sxs-lookup"><span data-stu-id="6c4ba-118">REST API</span></span>](hdinsight-hadoop-use-pig-curl.md) |&nbsp; |<span data-ttu-id="6c4ba-119">✔</span><span class="sxs-lookup"><span data-stu-id="6c4ba-119">✔</span></span> |<span data-ttu-id="6c4ba-120">Linux ou Windows</span><span class="sxs-lookup"><span data-stu-id="6c4ba-120">Linux or Windows</span></span> |<span data-ttu-id="6c4ba-121">Linux, Unix, Mac OS X ou Windows</span><span class="sxs-lookup"><span data-stu-id="6c4ba-121">Linux, Unix, Mac OS X, or Windows</span></span> |
| [<span data-ttu-id="6c4ba-122">Kit de développement logiciel (SDK) .NET pour Hadoop</span><span class="sxs-lookup"><span data-stu-id="6c4ba-122">.NET SDK for Hadoop</span></span>](hdinsight-hadoop-use-pig-dotnet-sdk.md) |&nbsp; |<span data-ttu-id="6c4ba-123">✔</span><span class="sxs-lookup"><span data-stu-id="6c4ba-123">✔</span></span> |<span data-ttu-id="6c4ba-124">Linux ou Windows</span><span class="sxs-lookup"><span data-stu-id="6c4ba-124">Linux or Windows</span></span> |<span data-ttu-id="6c4ba-125">Windows (pour l’instant)</span><span class="sxs-lookup"><span data-stu-id="6c4ba-125">Windows (for now)</span></span> |
| [<span data-ttu-id="6c4ba-126">Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="6c4ba-126">Windows PowerShell</span></span>](hdinsight-hadoop-use-pig-powershell.md) |&nbsp; |<span data-ttu-id="6c4ba-127">✔</span><span class="sxs-lookup"><span data-stu-id="6c4ba-127">✔</span></span> |<span data-ttu-id="6c4ba-128">Linux ou Windows</span><span class="sxs-lookup"><span data-stu-id="6c4ba-128">Linux or Windows</span></span> |<span data-ttu-id="6c4ba-129">Windows</span><span class="sxs-lookup"><span data-stu-id="6c4ba-129">Windows</span></span> |
| <span data-ttu-id="6c4ba-130">[Bureau à distance](hdinsight-hadoop-use-pig-remote-desktop.md) (HDInsight 3.2 et 3.3)</span><span class="sxs-lookup"><span data-stu-id="6c4ba-130">[Remote Desktop](hdinsight-hadoop-use-pig-remote-desktop.md) (HDInsight 3.2 and 3.3)</span></span> |<span data-ttu-id="6c4ba-131">✔</span><span class="sxs-lookup"><span data-stu-id="6c4ba-131">✔</span></span> |<span data-ttu-id="6c4ba-132">✔</span><span class="sxs-lookup"><span data-stu-id="6c4ba-132">✔</span></span> |<span data-ttu-id="6c4ba-133">Windows</span><span class="sxs-lookup"><span data-stu-id="6c4ba-133">Windows</span></span> |<span data-ttu-id="6c4ba-134">Windows</span><span class="sxs-lookup"><span data-stu-id="6c4ba-134">Windows</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="6c4ba-135">Linux est le seul système d’exploitation utilisé sur HDInsight version 3.4 ou supérieure.</span><span class="sxs-lookup"><span data-stu-id="6c4ba-135">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="6c4ba-136">Pour plus d’informations, consultez [Suppression de HDInsight sous Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="6c4ba-136">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <span data-ttu-id="6c4ba-137"><a id="why"></a>Pourquoi utiliser Pig ?</span><span class="sxs-lookup"><span data-stu-id="6c4ba-137"><a id="why"></a>Why use Pig</span></span>

<span data-ttu-id="6c4ba-138">Lun des défis de traitement de données à l'aide de MapReduce dans Hadoop consiste à implémenter votre logique de traitement en utilisant uniquement un mappage et une fonction de réduction.</span><span class="sxs-lookup"><span data-stu-id="6c4ba-138">One of the challenges of processing data by using MapReduce in Hadoop is implementing your processing logic by using only a map and a reduce function.</span></span> <span data-ttu-id="6c4ba-139">Pour un traitement complexe, vous devez souvent interrompre le traitement lors de plusieurs opérations MapReduce qui sont chaînées ensemble pour produire le résultat souhaité.</span><span class="sxs-lookup"><span data-stu-id="6c4ba-139">For complex processing, you often have to break processing into multiple MapReduce operations that are chained together to achieve the desired result.</span></span>

<span data-ttu-id="6c4ba-140">Pig permet de définir un traitement comme une série de transformations via lesquelles les données circulent pour produire le résultat souhaité.</span><span class="sxs-lookup"><span data-stu-id="6c4ba-140">Pig allows you to define processing as a series of transformations that the data flows through to produce the desired output.</span></span>

<span data-ttu-id="6c4ba-141">Le langage Pig Latin vous permet de décrire le flux de données provenant d’une entrée brute, via une ou plusieurs transformations, pour produire le résultat souhaité.</span><span class="sxs-lookup"><span data-stu-id="6c4ba-141">The Pig Latin language allows you to describe the data flow from raw input, through one or more transformations, to produce the desired output.</span></span> <span data-ttu-id="6c4ba-142">Les programmes Pig Latin suivent le modèle général suivant :</span><span class="sxs-lookup"><span data-stu-id="6c4ba-142">Pig Latin programs follow this general pattern:</span></span>

* <span data-ttu-id="6c4ba-143">**Chargement**: lecture des données à manipuler dans le système de fichiers</span><span class="sxs-lookup"><span data-stu-id="6c4ba-143">**Load**: Read data to be manipulated from the file system</span></span>

* <span data-ttu-id="6c4ba-144">**Transformation**: manipulation des données</span><span class="sxs-lookup"><span data-stu-id="6c4ba-144">**Transform**: Manipulate the data</span></span>

* <span data-ttu-id="6c4ba-145">**Sortie ou stockage**: affichage du résultat à l'écran ou stockage pour traitement</span><span class="sxs-lookup"><span data-stu-id="6c4ba-145">**Dump or store**: Output data to the screen or store it for processing</span></span>

### <a name="user-defined-functions"></a><span data-ttu-id="6c4ba-146">Fonctions définies par l’utilisateur</span><span class="sxs-lookup"><span data-stu-id="6c4ba-146">User-defined functions</span></span>

<span data-ttu-id="6c4ba-147">Pig Latin prend également en charge les fonctions définies par l'utilisateur (UDF), ce qui vous permet d'appeler des composants externes qui implémentent la logique qui est difficile à modéliser dans Pig Latin.</span><span class="sxs-lookup"><span data-stu-id="6c4ba-147">Pig Latin also supports user-defined functions (UDF), which allows you to invoke external components that implement logic that is difficult to model in Pig Latin.</span></span>

<span data-ttu-id="6c4ba-148">Pour plus d’informations sur Pig Latin, consultez les pages [Manuel de référence Pig Latin 1](http://pig.apache.org/docs/r0.7.0/piglatin_ref1.html) et [Manuel de référence Pig Latin 2](http://pig.apache.org/docs/r0.7.0/piglatin_ref2.html).</span><span class="sxs-lookup"><span data-stu-id="6c4ba-148">For more information about Pig Latin, see [Pig Latin Reference Manual 1](http://pig.apache.org/docs/r0.7.0/piglatin_ref1.html) and [Pig Latin Reference Manual 2](http://pig.apache.org/docs/r0.7.0/piglatin_ref2.html).</span></span>

<span data-ttu-id="6c4ba-149">Pour obtenir un exemple d'utilisation des fonctions définies par l’utilisateur (UDF) avec Pig, consultez les documents suivants :</span><span class="sxs-lookup"><span data-stu-id="6c4ba-149">For an example of using UDFs with Pig, see the following documents:</span></span>

* <span data-ttu-id="6c4ba-150">[Utilisation de DataFu avec Pig dans HDInsight](hdinsight-hadoop-use-pig-datafu-udf.md) : DataFu est une collection de fonctions définies par l’utilisateur utiles gérées par Apache</span><span class="sxs-lookup"><span data-stu-id="6c4ba-150">[Use DataFu with Pig in HDInsight](hdinsight-hadoop-use-pig-datafu-udf.md) - DataFu is a collection of useful UDFs maintained by Apache</span></span>
* [<span data-ttu-id="6c4ba-151">Utilisation de Python avec Hive et Pig dans HDInsight</span><span class="sxs-lookup"><span data-stu-id="6c4ba-151">Use Python with Pig and Hive in HDInsight</span></span>](hdinsight-python.md)
* [<span data-ttu-id="6c4ba-152">Utilisation de C# avec Hive et Pig dans HDInsight</span><span class="sxs-lookup"><span data-stu-id="6c4ba-152">Use C# with Hive and Pig in HDInsight</span></span>](hdinsight-hadoop-hive-pig-udf-dotnet-csharp.md)

## <span data-ttu-id="6c4ba-153"><a id="data"></a>Exemple de données</span><span class="sxs-lookup"><span data-stu-id="6c4ba-153"><a id="data"></a>Example data</span></span>

<span data-ttu-id="6c4ba-154">HDInsight propose différents exemples de jeux de données, qui sont stockés dans les répertoires `/example/data` et `/HdiSamples`.</span><span class="sxs-lookup"><span data-stu-id="6c4ba-154">HDInsight provides various example data sets, which are stored in the `/example/data` and `/HdiSamples` directories.</span></span> <span data-ttu-id="6c4ba-155">Ces répertoires sont disponibles dans le stockage par défaut de votre cluster.</span><span class="sxs-lookup"><span data-stu-id="6c4ba-155">These directories are in the default storage for your cluster.</span></span> <span data-ttu-id="6c4ba-156">L’exemple Pig présenté dans ce document utilise le fichier *log4j* à partir de `/example/data/sample.log`.</span><span class="sxs-lookup"><span data-stu-id="6c4ba-156">The Pig example in this document uses the *log4j* file from `/example/data/sample.log`.</span></span>

<span data-ttu-id="6c4ba-157">Chaque journal à l'intérieur du fichier est constitué d'une ligne de champs qui contient un champ `[LOG LEVEL]` pour indiquer le type et la gravité, par exemple :</span><span class="sxs-lookup"><span data-stu-id="6c4ba-157">Each log inside the file consists of a line of fields that contains a `[LOG LEVEL]` field to show the type and the severity, for example:</span></span>

    2012-02-03 20:26:41 SampleClass3 [ERROR] verbose detail for id 1527353937

<span data-ttu-id="6c4ba-158">Dans l'exemple précédent, le niveau de journal est ERROR.</span><span class="sxs-lookup"><span data-stu-id="6c4ba-158">In the previous example, the log level is ERROR.</span></span>

> [!NOTE]
> <span data-ttu-id="6c4ba-159">Vous pouvez également générer un fichier log4j à l'aide de l’outil de journalisation [Apache Log4j](http://en.wikipedia.org/wiki/Log4j) , puis télécharger ce fichier vers votre objet blob.</span><span class="sxs-lookup"><span data-stu-id="6c4ba-159">You can also generate a log4j file by using the [Apache Log4j](http://en.wikipedia.org/wiki/Log4j) logging tool and then upload that file to your blob.</span></span> <span data-ttu-id="6c4ba-160">Pour des instructions, consultez la page [Téléchargement de données vers HDInsight](hdinsight-upload-data.md) .</span><span class="sxs-lookup"><span data-stu-id="6c4ba-160">See [Upload Data to HDInsight](hdinsight-upload-data.md) for instructions.</span></span> <span data-ttu-id="6c4ba-161">Pour plus d'informations sur l'utilisation du stockage d'objets blob Azure avec HDInsight, consultez la page [Utilisation du stockage d'objets blob Azure avec HDInsight](hdinsight-hadoop-use-blob-storage.md).</span><span class="sxs-lookup"><span data-stu-id="6c4ba-161">For more information about how blobs in Azure storage are used with HDInsight, see [Use Azure Blob Storage with HDInsight](hdinsight-hadoop-use-blob-storage.md).</span></span>

## <span data-ttu-id="6c4ba-162"><a id="job"></a>Exemple de travail</span><span class="sxs-lookup"><span data-stu-id="6c4ba-162"><a id="job"></a>Example job</span></span>

<span data-ttu-id="6c4ba-163">Le travail Pig Latin suivant charge le fichier `sample.log` depuis le stockage par défaut de votre cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="6c4ba-163">The following Pig Latin job loads the `sample.log` file from the default storage for your HDInsight cluster.</span></span> <span data-ttu-id="6c4ba-164">Elle effectue ensuite une série de transformations qui créent un décompte du nombre de fois où chaque niveau du journal s'est produit dans les données d'entrée.</span><span class="sxs-lookup"><span data-stu-id="6c4ba-164">Then it performs a series of transformations that result in a count of how many times each log level occurred in the input data.</span></span> <span data-ttu-id="6c4ba-165">Les résultats sont écrits en STDOUT.</span><span class="sxs-lookup"><span data-stu-id="6c4ba-165">The results are written to STDOUT.</span></span>

    LOGS = LOAD 'wasb:///example/data/sample.log';
    LEVELS = foreach LOGS generate REGEX_EXTRACT($0, '(TRACE|DEBUG|INFO|WARN|ERROR|FATAL)', 1)  as LOGLEVEL;
    FILTEREDLEVELS = FILTER LEVELS by LOGLEVEL is not null;
    GROUPEDLEVELS = GROUP FILTEREDLEVELS by LOGLEVEL;
    FREQUENCIES = foreach GROUPEDLEVELS generate group as LOGLEVEL, COUNT(FILTEREDLEVELS.LOGLEVEL) as COUNT;
    RESULT = order FREQUENCIES by COUNT desc;
    DUMP RESULT;

<span data-ttu-id="6c4ba-166">L’image suivante montre un résumé de ce qu’effectue chaque transformation sur les données.</span><span class="sxs-lookup"><span data-stu-id="6c4ba-166">The following image shows a summary of what each transformation does to the data.</span></span>

![Représentation graphique des transformations][image-hdi-pig-data-transformation]

## <span data-ttu-id="6c4ba-168"><a id="run"></a>Exécution de la tâche Pig Latin</span><span class="sxs-lookup"><span data-stu-id="6c4ba-168"><a id="run"></a>Run the Pig Latin job</span></span>

<span data-ttu-id="6c4ba-169">HDInsight peut exécuter des tâches Pig Latin de différentes façons.</span><span class="sxs-lookup"><span data-stu-id="6c4ba-169">HDInsight can run Pig Latin jobs by using a variety of methods.</span></span> <span data-ttu-id="6c4ba-170">Utilisez le tableau suivant pour découvrir la méthode qui vous convient, puis cliquez sur le lien pour obtenir une présentation détaillée.</span><span class="sxs-lookup"><span data-stu-id="6c4ba-170">Use the following table to decide which method is right for you, then follow the link for a walkthrough.</span></span>

| <span data-ttu-id="6c4ba-171">**Utilisez-le** si vous souhaitez...</span><span class="sxs-lookup"><span data-stu-id="6c4ba-171">**Use this** if you want...</span></span> | <span data-ttu-id="6c4ba-172">... un interpréteur de commandes **interactif**</span><span class="sxs-lookup"><span data-stu-id="6c4ba-172">...an **interactive** shell</span></span> | <span data-ttu-id="6c4ba-173">... un traitement par **lots**</span><span class="sxs-lookup"><span data-stu-id="6c4ba-173">...**batch** processing</span></span> | <span data-ttu-id="6c4ba-174">...avec ce **système d’exploitation cluster**</span><span class="sxs-lookup"><span data-stu-id="6c4ba-174">...with this **cluster operating system**</span></span> | <span data-ttu-id="6c4ba-175">... depuis ce **client**</span><span class="sxs-lookup"><span data-stu-id="6c4ba-175">...from this **client**</span></span> |
|:--- |:---:|:---:|:--- |:--- |
| [<span data-ttu-id="6c4ba-176">SSH</span><span class="sxs-lookup"><span data-stu-id="6c4ba-176">SSH</span></span>](hdinsight-hadoop-use-pig-ssh.md) |<span data-ttu-id="6c4ba-177">✔</span><span class="sxs-lookup"><span data-stu-id="6c4ba-177">✔</span></span> |<span data-ttu-id="6c4ba-178">✔</span><span class="sxs-lookup"><span data-stu-id="6c4ba-178">✔</span></span> |<span data-ttu-id="6c4ba-179">Linux</span><span class="sxs-lookup"><span data-stu-id="6c4ba-179">Linux</span></span> |<span data-ttu-id="6c4ba-180">Linux, Unix, Mac OS X ou Windows</span><span class="sxs-lookup"><span data-stu-id="6c4ba-180">Linux, Unix, Mac OS X, or Windows</span></span> |
| [<span data-ttu-id="6c4ba-181">Curl</span><span class="sxs-lookup"><span data-stu-id="6c4ba-181">Curl</span></span>](hdinsight-hadoop-use-pig-curl.md) |&nbsp; |<span data-ttu-id="6c4ba-182">✔</span><span class="sxs-lookup"><span data-stu-id="6c4ba-182">✔</span></span> |<span data-ttu-id="6c4ba-183">Linux ou Windows</span><span class="sxs-lookup"><span data-stu-id="6c4ba-183">Linux or Windows</span></span> |<span data-ttu-id="6c4ba-184">Linux, Unix, Mac OS X ou Windows</span><span class="sxs-lookup"><span data-stu-id="6c4ba-184">Linux, Unix, Mac OS X, or Windows</span></span> |
| [<span data-ttu-id="6c4ba-185">Kit de développement logiciel (SDK) .NET pour Hadoop</span><span class="sxs-lookup"><span data-stu-id="6c4ba-185">.NET SDK for Hadoop</span></span>](hdinsight-hadoop-use-pig-dotnet-sdk.md) |&nbsp; |<span data-ttu-id="6c4ba-186">✔</span><span class="sxs-lookup"><span data-stu-id="6c4ba-186">✔</span></span> |<span data-ttu-id="6c4ba-187">Linux ou Windows</span><span class="sxs-lookup"><span data-stu-id="6c4ba-187">Linux or Windows</span></span> |<span data-ttu-id="6c4ba-188">Windows (pour l’instant)</span><span class="sxs-lookup"><span data-stu-id="6c4ba-188">Windows (for now)</span></span> |
| [<span data-ttu-id="6c4ba-189">Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="6c4ba-189">Windows PowerShell</span></span>](hdinsight-hadoop-use-pig-powershell.md) |&nbsp; |<span data-ttu-id="6c4ba-190">✔</span><span class="sxs-lookup"><span data-stu-id="6c4ba-190">✔</span></span> |<span data-ttu-id="6c4ba-191">Linux ou Windows</span><span class="sxs-lookup"><span data-stu-id="6c4ba-191">Linux or Windows</span></span> |<span data-ttu-id="6c4ba-192">Windows</span><span class="sxs-lookup"><span data-stu-id="6c4ba-192">Windows</span></span> |
| <span data-ttu-id="6c4ba-193">[Bureau à distance](hdinsight-hadoop-use-pig-remote-desktop.md) (HDInsight 3.2 et 3.3)</span><span class="sxs-lookup"><span data-stu-id="6c4ba-193">[Remote Desktop](hdinsight-hadoop-use-pig-remote-desktop.md) (HDInsight 3.2 and 3.3)</span></span> |<span data-ttu-id="6c4ba-194">✔</span><span class="sxs-lookup"><span data-stu-id="6c4ba-194">✔</span></span> |<span data-ttu-id="6c4ba-195">✔</span><span class="sxs-lookup"><span data-stu-id="6c4ba-195">✔</span></span> |<span data-ttu-id="6c4ba-196">Windows</span><span class="sxs-lookup"><span data-stu-id="6c4ba-196">Windows</span></span> |<span data-ttu-id="6c4ba-197">Windows</span><span class="sxs-lookup"><span data-stu-id="6c4ba-197">Windows</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="6c4ba-198">Linux est le seul système d’exploitation utilisé sur HDInsight version 3.4 ou supérieure.</span><span class="sxs-lookup"><span data-stu-id="6c4ba-198">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="6c4ba-199">Pour plus d’informations, consultez [Suppression de HDInsight sous Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="6c4ba-199">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <a name="pig-and-sql-server-integration-services"></a><span data-ttu-id="6c4ba-200">Pig et SQL Server Integration Services</span><span class="sxs-lookup"><span data-stu-id="6c4ba-200">Pig and SQL Server Integration Services</span></span>

<span data-ttu-id="6c4ba-201">Vous pouvez utiliser les services SQL Server Integration Services (SSIS) pour exécuter une travail Pig.</span><span class="sxs-lookup"><span data-stu-id="6c4ba-201">You can use SQL Server Integration Services (SSIS) to run a Pig job.</span></span> <span data-ttu-id="6c4ba-202">Le pack de fonctionnalités Azure pour SSIS fournit les composants suivants, compatibles avec les tâches Pig sur HDInsight.</span><span class="sxs-lookup"><span data-stu-id="6c4ba-202">The Azure Feature Pack for SSIS provides the following components that work with Pig jobs on HDInsight.</span></span>

* <span data-ttu-id="6c4ba-203">[Tâche d’Azure HDInsight Pig][pigtask]</span><span class="sxs-lookup"><span data-stu-id="6c4ba-203">[Azure HDInsight Pig Task][pigtask]</span></span>

* <span data-ttu-id="6c4ba-204">[Gestionnaire de connexions d’abonnement Azure][connectionmanager]</span><span class="sxs-lookup"><span data-stu-id="6c4ba-204">[Azure Subscription Connection Manager][connectionmanager]</span></span>

<span data-ttu-id="6c4ba-205">Pour en savoir plus sur le pack de fonctionnalités Azure pour SSIS, cliquez [ici][ssispack].</span><span class="sxs-lookup"><span data-stu-id="6c4ba-205">Learn more about the Azure Feature Pack for SSIS [here][ssispack].</span></span>

## <span data-ttu-id="6c4ba-206"><a id="nextsteps"></a>Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="6c4ba-206"><a id="nextsteps"></a>Next steps</span></span>
<span data-ttu-id="6c4ba-207">Maintenant que vous avez vu comment utiliser Pig avec HDInsight, utilisez les liens suivants pour découvrir d'autres façons d'utiliser Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="6c4ba-207">Now that you have learned how to use Pig with HDInsight, use the following links to explore other ways to work with Azure HDInsight.</span></span>

* <span data-ttu-id="6c4ba-208">[Téléchargement de données vers HDInsight][hdinsight-upload-data]</span><span class="sxs-lookup"><span data-stu-id="6c4ba-208">[Upload data to HDInsight][hdinsight-upload-data]</span></span>
* <span data-ttu-id="6c4ba-209">[Utilisation de Hive avec HDInsight][hdinsight-use-hive]</span><span class="sxs-lookup"><span data-stu-id="6c4ba-209">[Use Hive with HDInsight][hdinsight-use-hive]</span></span>
* [<span data-ttu-id="6c4ba-210">Utilisation de Sqoop avec HDInsight</span><span class="sxs-lookup"><span data-stu-id="6c4ba-210">Use Sqoop with HDInsight</span></span>](hdinsight-use-sqoop.md)
* [<span data-ttu-id="6c4ba-211">Utilisation d’Oozie avec HDInsight</span><span class="sxs-lookup"><span data-stu-id="6c4ba-211">Use Oozie with HDInsight</span></span>](hdinsight-use-oozie.md)
* <span data-ttu-id="6c4ba-212">[Utilisation des tâches MapReduce avec HDInsight][hdinsight-use-mapreduce]</span><span class="sxs-lookup"><span data-stu-id="6c4ba-212">[Use MapReduce jobs with HDInsight][hdinsight-use-mapreduce]</span></span>

[apachepig-home]: http://pig.apache.org/
[putty]: http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html
[curl]: http://curl.haxx.se/
[pigtask]: http://msdn.microsoft.com/library/mt146781(v=sql.120).aspx
[connectionmanager]: http://msdn.microsoft.com/library/mt146773(v=sql.120).aspx
[ssispack]: http://msdn.microsoft.com/library/mt146770(v=sql.120).aspx


[hdinsight-upload-data]: hdinsight-upload-data.md

[hdinsight-admin-powershell]: hdinsight-administer-use-powershell.md

[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-mapreduce]: hdinsight-use-mapreduce.md

[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md#mapreduce-sdk

[Powershell-install-configure]: /powershell/azureps-cmdlets-docs

[powershell-start]: http://technet.microsoft.com/library/hh847889.aspx


[image-hdi-pig-data-transformation]: ./media/hdinsight-use-pig/HDI.DataTransformation.gif
