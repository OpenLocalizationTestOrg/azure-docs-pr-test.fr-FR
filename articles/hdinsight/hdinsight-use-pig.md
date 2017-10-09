---
title: aaaUse Hadoop Pig dans HDInsight | Documents Microsoft
description: "Découvrez comment toouse porc avec Hadoop dans HDInsight."
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
ms.openlocfilehash: 90850f2c742b8954c66ce277127e01b14fc3906f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-pig-with-hadoop-on-hdinsight"></a><span data-ttu-id="93a14-103">Utilisation de Pig avec Hadoop sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="93a14-103">Use Pig with Hadoop on HDInsight</span></span>

<span data-ttu-id="93a14-104">Découvrez comment toouse [Apache Pig](http://pig.apache.org/) avec HDInsight...</span><span class="sxs-lookup"><span data-stu-id="93a14-104">Learn how toouse [Apache Pig](http://pig.apache.org/) with HDInsight...</span></span>

<span data-ttu-id="93a14-105">Pig est une plateforme qui permet de créer des programmes pour Hadoop dans un langage procédural appelé *Pig Latin*.</span><span class="sxs-lookup"><span data-stu-id="93a14-105">Pig is a platform for creating programs for Hadoop by using a procedural language known as *Pig Latin*.</span></span> <span data-ttu-id="93a14-106">Pig est un autre tooJava pour la création de *MapReduce* solutions et il est inclus dans Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="93a14-106">Pig is an alternative tooJava for creating *MapReduce* solutions, and it is included with Azure HDInsight.</span></span> <span data-ttu-id="93a14-107">Utilisez hello suivant hello toodiscover de table que Pig peut être utilisé avec HDInsight de différentes manières :</span><span class="sxs-lookup"><span data-stu-id="93a14-107">Use hello following table toodiscover hello various ways that Pig can be used with HDInsight:</span></span>

| <span data-ttu-id="93a14-108">**Utilisez-le** si vous souhaitez...</span><span class="sxs-lookup"><span data-stu-id="93a14-108">**Use this** if you want...</span></span> | <span data-ttu-id="93a14-109">... un interpréteur de commandes **interactif**</span><span class="sxs-lookup"><span data-stu-id="93a14-109">...an **interactive** shell</span></span> | <span data-ttu-id="93a14-110">... un traitement par **lots**</span><span class="sxs-lookup"><span data-stu-id="93a14-110">...**batch** processing</span></span> | <span data-ttu-id="93a14-111">...avec ce **système d’exploitation cluster**</span><span class="sxs-lookup"><span data-stu-id="93a14-111">...with this **cluster operating system**</span></span> | <span data-ttu-id="93a14-112">...depuis ce **système d’exploitation cluster**</span><span class="sxs-lookup"><span data-stu-id="93a14-112">...from this **client operating system**</span></span> |
|:--- |:---:|:---:|:--- |:--- |
| [<span data-ttu-id="93a14-113">SSH</span><span class="sxs-lookup"><span data-stu-id="93a14-113">SSH</span></span>](hdinsight-hadoop-use-pig-ssh.md) |<span data-ttu-id="93a14-114">✔</span><span class="sxs-lookup"><span data-stu-id="93a14-114">✔</span></span> |<span data-ttu-id="93a14-115">✔</span><span class="sxs-lookup"><span data-stu-id="93a14-115">✔</span></span> |<span data-ttu-id="93a14-116">Linux</span><span class="sxs-lookup"><span data-stu-id="93a14-116">Linux</span></span> |<span data-ttu-id="93a14-117">Linux, Unix, Mac OS X ou Windows</span><span class="sxs-lookup"><span data-stu-id="93a14-117">Linux, Unix, Mac OS X, or Windows</span></span> |
| [<span data-ttu-id="93a14-118">API REST</span><span class="sxs-lookup"><span data-stu-id="93a14-118">REST API</span></span>](hdinsight-hadoop-use-pig-curl.md) |&nbsp; |<span data-ttu-id="93a14-119">✔</span><span class="sxs-lookup"><span data-stu-id="93a14-119">✔</span></span> |<span data-ttu-id="93a14-120">Linux ou Windows</span><span class="sxs-lookup"><span data-stu-id="93a14-120">Linux or Windows</span></span> |<span data-ttu-id="93a14-121">Linux, Unix, Mac OS X ou Windows</span><span class="sxs-lookup"><span data-stu-id="93a14-121">Linux, Unix, Mac OS X, or Windows</span></span> |
| [<span data-ttu-id="93a14-122">Kit de développement logiciel (SDK) .NET pour Hadoop</span><span class="sxs-lookup"><span data-stu-id="93a14-122">.NET SDK for Hadoop</span></span>](hdinsight-hadoop-use-pig-dotnet-sdk.md) |&nbsp; |<span data-ttu-id="93a14-123">✔</span><span class="sxs-lookup"><span data-stu-id="93a14-123">✔</span></span> |<span data-ttu-id="93a14-124">Linux ou Windows</span><span class="sxs-lookup"><span data-stu-id="93a14-124">Linux or Windows</span></span> |<span data-ttu-id="93a14-125">Windows (pour l’instant)</span><span class="sxs-lookup"><span data-stu-id="93a14-125">Windows (for now)</span></span> |
| [<span data-ttu-id="93a14-126">Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="93a14-126">Windows PowerShell</span></span>](hdinsight-hadoop-use-pig-powershell.md) |&nbsp; |<span data-ttu-id="93a14-127">✔</span><span class="sxs-lookup"><span data-stu-id="93a14-127">✔</span></span> |<span data-ttu-id="93a14-128">Linux ou Windows</span><span class="sxs-lookup"><span data-stu-id="93a14-128">Linux or Windows</span></span> |<span data-ttu-id="93a14-129">Windows</span><span class="sxs-lookup"><span data-stu-id="93a14-129">Windows</span></span> |
| <span data-ttu-id="93a14-130">[Bureau à distance](hdinsight-hadoop-use-pig-remote-desktop.md) (HDInsight 3.2 et 3.3)</span><span class="sxs-lookup"><span data-stu-id="93a14-130">[Remote Desktop](hdinsight-hadoop-use-pig-remote-desktop.md) (HDInsight 3.2 and 3.3)</span></span> |<span data-ttu-id="93a14-131">✔</span><span class="sxs-lookup"><span data-stu-id="93a14-131">✔</span></span> |<span data-ttu-id="93a14-132">✔</span><span class="sxs-lookup"><span data-stu-id="93a14-132">✔</span></span> |<span data-ttu-id="93a14-133">Windows</span><span class="sxs-lookup"><span data-stu-id="93a14-133">Windows</span></span> |<span data-ttu-id="93a14-134">Windows</span><span class="sxs-lookup"><span data-stu-id="93a14-134">Windows</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="93a14-135">Linux est hello seul système d’exploitation utilisé sur HDInsight version 3.4 ou supérieure.</span><span class="sxs-lookup"><span data-stu-id="93a14-135">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="93a14-136">Pour plus d’informations, consultez [Suppression de HDInsight sous Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="93a14-136">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <span data-ttu-id="93a14-137"><a id="why"></a>Pourquoi utiliser Pig ?</span><span class="sxs-lookup"><span data-stu-id="93a14-137"><a id="why"></a>Why use Pig</span></span>

<span data-ttu-id="93a14-138">Un des défis hello de traitement de données à l’aide de MapReduce dans Hadoop implémente votre logique de traitement à l’aide uniquement sur une carte et une fonction de la réduire.</span><span class="sxs-lookup"><span data-stu-id="93a14-138">One of hello challenges of processing data by using MapReduce in Hadoop is implementing your processing logic by using only a map and a reduce function.</span></span> <span data-ttu-id="93a14-139">Pour un traitement complexe, fréquence à laquelle vous avez toobreak le traitement en plusieurs opérations MapReduce qui sont chaînées tooachieve de résultats hello souhaité.</span><span class="sxs-lookup"><span data-stu-id="93a14-139">For complex processing, you often have toobreak processing into multiple MapReduce operations that are chained together tooachieve hello desired result.</span></span>

<span data-ttu-id="93a14-140">Pig vous permet de toodefine traitant comme une série de transformations qui hello du flux de données via la sortie de tooproduce hello souhaité.</span><span class="sxs-lookup"><span data-stu-id="93a14-140">Pig allows you toodefine processing as a series of transformations that hello data flows through tooproduce hello desired output.</span></span>

<span data-ttu-id="93a14-141">langage Hello Pig permet de vous toodescribe hello flux de données d’entrée brute, via une ou plusieurs transformations, la sortie de hello souhaité tooproduce.</span><span class="sxs-lookup"><span data-stu-id="93a14-141">hello Pig Latin language allows you toodescribe hello data flow from raw input, through one or more transformations, tooproduce hello desired output.</span></span> <span data-ttu-id="93a14-142">Les programmes Pig Latin suivent le modèle général suivant :</span><span class="sxs-lookup"><span data-stu-id="93a14-142">Pig Latin programs follow this general pattern:</span></span>

* <span data-ttu-id="93a14-143">**Charge**: lire toobe données manipulée hello système de fichiers</span><span class="sxs-lookup"><span data-stu-id="93a14-143">**Load**: Read data toobe manipulated from hello file system</span></span>

* <span data-ttu-id="93a14-144">**Transformer**: manipuler les données de salutation</span><span class="sxs-lookup"><span data-stu-id="93a14-144">**Transform**: Manipulate hello data</span></span>

* <span data-ttu-id="93a14-145">**Dump ou stocker**: toohello l’écran de données de sortie ou de le stocker pour le traitement</span><span class="sxs-lookup"><span data-stu-id="93a14-145">**Dump or store**: Output data toohello screen or store it for processing</span></span>

### <a name="user-defined-functions"></a><span data-ttu-id="93a14-146">Fonctions définies par l’utilisateur</span><span class="sxs-lookup"><span data-stu-id="93a14-146">User-defined functions</span></span>

<span data-ttu-id="93a14-147">Pig Latin prend également en charge les fonctions définies par l’utilisateur (UDF), qui vous permet de tooinvoke des composants externes qui implémentent la logique qui est difficile toomodel dans Pig Latin.</span><span class="sxs-lookup"><span data-stu-id="93a14-147">Pig Latin also supports user-defined functions (UDF), which allows you tooinvoke external components that implement logic that is difficult toomodel in Pig Latin.</span></span>

<span data-ttu-id="93a14-148">Pour plus d’informations sur Pig Latin, consultez les pages [Manuel de référence Pig Latin 1](http://pig.apache.org/docs/r0.7.0/piglatin_ref1.html) et [Manuel de référence Pig Latin 2](http://pig.apache.org/docs/r0.7.0/piglatin_ref2.html).</span><span class="sxs-lookup"><span data-stu-id="93a14-148">For more information about Pig Latin, see [Pig Latin Reference Manual 1](http://pig.apache.org/docs/r0.7.0/piglatin_ref1.html) and [Pig Latin Reference Manual 2](http://pig.apache.org/docs/r0.7.0/piglatin_ref2.html).</span></span>

<span data-ttu-id="93a14-149">Pour obtenir un exemple d’utilisation des UDF avec Pig, consultez hello suivant des documents :</span><span class="sxs-lookup"><span data-stu-id="93a14-149">For an example of using UDFs with Pig, see hello following documents:</span></span>

* <span data-ttu-id="93a14-150">[Utilisation de DataFu avec Pig dans HDInsight](hdinsight-hadoop-use-pig-datafu-udf.md) : DataFu est une collection de fonctions définies par l’utilisateur utiles gérées par Apache</span><span class="sxs-lookup"><span data-stu-id="93a14-150">[Use DataFu with Pig in HDInsight](hdinsight-hadoop-use-pig-datafu-udf.md) - DataFu is a collection of useful UDFs maintained by Apache</span></span>
* [<span data-ttu-id="93a14-151">Utilisation de Python avec Hive et Pig dans HDInsight</span><span class="sxs-lookup"><span data-stu-id="93a14-151">Use Python with Pig and Hive in HDInsight</span></span>](hdinsight-python.md)
* [<span data-ttu-id="93a14-152">Utilisation de C# avec Hive et Pig dans HDInsight</span><span class="sxs-lookup"><span data-stu-id="93a14-152">Use C# with Hive and Pig in HDInsight</span></span>](hdinsight-hadoop-hive-pig-udf-dotnet-csharp.md)

## <span data-ttu-id="93a14-153"><a id="data"></a>Exemple de données</span><span class="sxs-lookup"><span data-stu-id="93a14-153"><a id="data"></a>Example data</span></span>

<span data-ttu-id="93a14-154">HDInsight fournit différents jeux de données d’exemple, qui sont stockées dans hello `/example/data` et `/HdiSamples` répertoires.</span><span class="sxs-lookup"><span data-stu-id="93a14-154">HDInsight provides various example data sets, which are stored in hello `/example/data` and `/HdiSamples` directories.</span></span> <span data-ttu-id="93a14-155">Ces répertoires sont dans le stockage par défaut hello pour votre cluster.</span><span class="sxs-lookup"><span data-stu-id="93a14-155">These directories are in hello default storage for your cluster.</span></span> <span data-ttu-id="93a14-156">exemple de Pig Hello dans ce document utilise hello *log4j* à partir du fichier `/example/data/sample.log`.</span><span class="sxs-lookup"><span data-stu-id="93a14-156">hello Pig example in this document uses hello *log4j* file from `/example/data/sample.log`.</span></span>

<span data-ttu-id="93a14-157">Chaque journal à l’intérieur du fichier de hello se compose d’une ligne de champs qui contient un `[LOG LEVEL]` champ tooshow hello hello et type de niveau de gravité, par exemple :</span><span class="sxs-lookup"><span data-stu-id="93a14-157">Each log inside hello file consists of a line of fields that contains a `[LOG LEVEL]` field tooshow hello type and hello severity, for example:</span></span>

    2012-02-03 20:26:41 SampleClass3 [ERROR] verbose detail for id 1527353937

<span data-ttu-id="93a14-158">Dans l’exemple précédent de hello, niveau de journal hello est erreur.</span><span class="sxs-lookup"><span data-stu-id="93a14-158">In hello previous example, hello log level is ERROR.</span></span>

> [!NOTE]
> <span data-ttu-id="93a14-159">Vous pouvez également générer un fichier log4j à l’aide de hello [Apache Log4j](http://en.wikipedia.org/wiki/Log4j) journalisation de l’outil, puis le télécharger cet objet blob tooyour de fichier.</span><span class="sxs-lookup"><span data-stu-id="93a14-159">You can also generate a log4j file by using hello [Apache Log4j](http://en.wikipedia.org/wiki/Log4j) logging tool and then upload that file tooyour blob.</span></span> <span data-ttu-id="93a14-160">Consultez [tooHDInsight de télécharger des données](hdinsight-upload-data.md) pour obtenir des instructions.</span><span class="sxs-lookup"><span data-stu-id="93a14-160">See [Upload Data tooHDInsight](hdinsight-upload-data.md) for instructions.</span></span> <span data-ttu-id="93a14-161">Pour plus d'informations sur l'utilisation du stockage d'objets blob Azure avec HDInsight, consultez la page [Utilisation du stockage d'objets blob Azure avec HDInsight](hdinsight-hadoop-use-blob-storage.md).</span><span class="sxs-lookup"><span data-stu-id="93a14-161">For more information about how blobs in Azure storage are used with HDInsight, see [Use Azure Blob Storage with HDInsight](hdinsight-hadoop-use-blob-storage.md).</span></span>

## <span data-ttu-id="93a14-162"><a id="job"></a>Exemple de travail</span><span class="sxs-lookup"><span data-stu-id="93a14-162"><a id="job"></a>Example job</span></span>

<span data-ttu-id="93a14-163">tâche Pig Latin suivante Hello charge hello `sample.log` fichier de stockage par défaut de hello pour votre cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="93a14-163">hello following Pig Latin job loads hello `sample.log` file from hello default storage for your HDInsight cluster.</span></span> <span data-ttu-id="93a14-164">Il effectue ensuite une série de transformations qui entraîne le nombre d’illustrant le nombre de fois où chaque données d’entrée de journal au niveau hello s’est produite dans.</span><span class="sxs-lookup"><span data-stu-id="93a14-164">Then it performs a series of transformations that result in a count of how many times each log level occurred in hello input data.</span></span> <span data-ttu-id="93a14-165">les résultats de Hello sont écrits tooSTDOUT.</span><span class="sxs-lookup"><span data-stu-id="93a14-165">hello results are written tooSTDOUT.</span></span>

    LOGS = LOAD 'wasb:///example/data/sample.log';
    LEVELS = foreach LOGS generate REGEX_EXTRACT($0, '(TRACE|DEBUG|INFO|WARN|ERROR|FATAL)', 1)  as LOGLEVEL;
    FILTEREDLEVELS = FILTER LEVELS by LOGLEVEL is not null;
    GROUPEDLEVELS = GROUP FILTEREDLEVELS by LOGLEVEL;
    FREQUENCIES = foreach GROUPEDLEVELS generate group as LOGLEVEL, COUNT(FILTEREDLEVELS.LOGLEVEL) as COUNT;
    RESULT = order FREQUENCIES by COUNT desc;
    DUMP RESULT;

<span data-ttu-id="93a14-166">Hello image suivante affiche un résumé de chaque transformation ne toohello. les données.</span><span class="sxs-lookup"><span data-stu-id="93a14-166">hello following image shows a summary of what each transformation does toohello data.</span></span>

![Représentation graphique des transformations de hello][image-hdi-pig-data-transformation]

## <span data-ttu-id="93a14-168"><a id="run"></a>Exécuter la tâche Pig Latin de hello</span><span class="sxs-lookup"><span data-stu-id="93a14-168"><a id="run"></a>Run hello Pig Latin job</span></span>

<span data-ttu-id="93a14-169">HDInsight peut exécuter des tâches Pig Latin de différentes façons.</span><span class="sxs-lookup"><span data-stu-id="93a14-169">HDInsight can run Pig Latin jobs by using a variety of methods.</span></span> <span data-ttu-id="93a14-170">Utilisez hello suivant toodecide table quelle méthode vous consiste, puis suivez le lien hello pour une procédure pas à pas.</span><span class="sxs-lookup"><span data-stu-id="93a14-170">Use hello following table toodecide which method is right for you, then follow hello link for a walkthrough.</span></span>

| <span data-ttu-id="93a14-171">**Utilisez-le** si vous souhaitez...</span><span class="sxs-lookup"><span data-stu-id="93a14-171">**Use this** if you want...</span></span> | <span data-ttu-id="93a14-172">... un interpréteur de commandes **interactif**</span><span class="sxs-lookup"><span data-stu-id="93a14-172">...an **interactive** shell</span></span> | <span data-ttu-id="93a14-173">... un traitement par **lots**</span><span class="sxs-lookup"><span data-stu-id="93a14-173">...**batch** processing</span></span> | <span data-ttu-id="93a14-174">...avec ce **système d’exploitation cluster**</span><span class="sxs-lookup"><span data-stu-id="93a14-174">...with this **cluster operating system**</span></span> | <span data-ttu-id="93a14-175">... depuis ce **client**</span><span class="sxs-lookup"><span data-stu-id="93a14-175">...from this **client**</span></span> |
|:--- |:---:|:---:|:--- |:--- |
| [<span data-ttu-id="93a14-176">SSH</span><span class="sxs-lookup"><span data-stu-id="93a14-176">SSH</span></span>](hdinsight-hadoop-use-pig-ssh.md) |<span data-ttu-id="93a14-177">✔</span><span class="sxs-lookup"><span data-stu-id="93a14-177">✔</span></span> |<span data-ttu-id="93a14-178">✔</span><span class="sxs-lookup"><span data-stu-id="93a14-178">✔</span></span> |<span data-ttu-id="93a14-179">Linux</span><span class="sxs-lookup"><span data-stu-id="93a14-179">Linux</span></span> |<span data-ttu-id="93a14-180">Linux, Unix, Mac OS X ou Windows</span><span class="sxs-lookup"><span data-stu-id="93a14-180">Linux, Unix, Mac OS X, or Windows</span></span> |
| [<span data-ttu-id="93a14-181">Curl</span><span class="sxs-lookup"><span data-stu-id="93a14-181">Curl</span></span>](hdinsight-hadoop-use-pig-curl.md) |&nbsp; |<span data-ttu-id="93a14-182">✔</span><span class="sxs-lookup"><span data-stu-id="93a14-182">✔</span></span> |<span data-ttu-id="93a14-183">Linux ou Windows</span><span class="sxs-lookup"><span data-stu-id="93a14-183">Linux or Windows</span></span> |<span data-ttu-id="93a14-184">Linux, Unix, Mac OS X ou Windows</span><span class="sxs-lookup"><span data-stu-id="93a14-184">Linux, Unix, Mac OS X, or Windows</span></span> |
| [<span data-ttu-id="93a14-185">Kit de développement logiciel (SDK) .NET pour Hadoop</span><span class="sxs-lookup"><span data-stu-id="93a14-185">.NET SDK for Hadoop</span></span>](hdinsight-hadoop-use-pig-dotnet-sdk.md) |&nbsp; |<span data-ttu-id="93a14-186">✔</span><span class="sxs-lookup"><span data-stu-id="93a14-186">✔</span></span> |<span data-ttu-id="93a14-187">Linux ou Windows</span><span class="sxs-lookup"><span data-stu-id="93a14-187">Linux or Windows</span></span> |<span data-ttu-id="93a14-188">Windows (pour l’instant)</span><span class="sxs-lookup"><span data-stu-id="93a14-188">Windows (for now)</span></span> |
| [<span data-ttu-id="93a14-189">Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="93a14-189">Windows PowerShell</span></span>](hdinsight-hadoop-use-pig-powershell.md) |&nbsp; |<span data-ttu-id="93a14-190">✔</span><span class="sxs-lookup"><span data-stu-id="93a14-190">✔</span></span> |<span data-ttu-id="93a14-191">Linux ou Windows</span><span class="sxs-lookup"><span data-stu-id="93a14-191">Linux or Windows</span></span> |<span data-ttu-id="93a14-192">Windows</span><span class="sxs-lookup"><span data-stu-id="93a14-192">Windows</span></span> |
| <span data-ttu-id="93a14-193">[Bureau à distance](hdinsight-hadoop-use-pig-remote-desktop.md) (HDInsight 3.2 et 3.3)</span><span class="sxs-lookup"><span data-stu-id="93a14-193">[Remote Desktop](hdinsight-hadoop-use-pig-remote-desktop.md) (HDInsight 3.2 and 3.3)</span></span> |<span data-ttu-id="93a14-194">✔</span><span class="sxs-lookup"><span data-stu-id="93a14-194">✔</span></span> |<span data-ttu-id="93a14-195">✔</span><span class="sxs-lookup"><span data-stu-id="93a14-195">✔</span></span> |<span data-ttu-id="93a14-196">Windows</span><span class="sxs-lookup"><span data-stu-id="93a14-196">Windows</span></span> |<span data-ttu-id="93a14-197">Windows</span><span class="sxs-lookup"><span data-stu-id="93a14-197">Windows</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="93a14-198">Linux est hello seul système d’exploitation utilisé sur HDInsight version 3.4 ou supérieure.</span><span class="sxs-lookup"><span data-stu-id="93a14-198">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="93a14-199">Pour plus d’informations, consultez [Suppression de HDInsight sous Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="93a14-199">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <a name="pig-and-sql-server-integration-services"></a><span data-ttu-id="93a14-200">Pig et SQL Server Integration Services</span><span class="sxs-lookup"><span data-stu-id="93a14-200">Pig and SQL Server Integration Services</span></span>

<span data-ttu-id="93a14-201">Vous pouvez utiliser SQL Server Integration Services (SSIS) toorun un travail Pig.</span><span class="sxs-lookup"><span data-stu-id="93a14-201">You can use SQL Server Integration Services (SSIS) toorun a Pig job.</span></span> <span data-ttu-id="93a14-202">Bonjour Azure Feature Pack pour SSIS fournit hello suivant des composants qui fonctionnent avec des travaux Pig dans HDInsight.</span><span class="sxs-lookup"><span data-stu-id="93a14-202">hello Azure Feature Pack for SSIS provides hello following components that work with Pig jobs on HDInsight.</span></span>

* <span data-ttu-id="93a14-203">[Tâche d’Azure HDInsight Pig][pigtask]</span><span class="sxs-lookup"><span data-stu-id="93a14-203">[Azure HDInsight Pig Task][pigtask]</span></span>

* <span data-ttu-id="93a14-204">[Gestionnaire de connexions d’abonnement Azure][connectionmanager]</span><span class="sxs-lookup"><span data-stu-id="93a14-204">[Azure Subscription Connection Manager][connectionmanager]</span></span>

<span data-ttu-id="93a14-205">En savoir plus sur hello Azure Feature Pack pour SSIS [ici][ssispack].</span><span class="sxs-lookup"><span data-stu-id="93a14-205">Learn more about hello Azure Feature Pack for SSIS [here][ssispack].</span></span>

## <span data-ttu-id="93a14-206"><a id="nextsteps"></a>Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="93a14-206"><a id="nextsteps"></a>Next steps</span></span>
<span data-ttu-id="93a14-207">Maintenant que vous avez appris comment toouse Pig hdinsight, hello utilisation suivant lie tooexplore autres toowork manières avec Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="93a14-207">Now that you have learned how toouse Pig with HDInsight, use hello following links tooexplore other ways toowork with Azure HDInsight.</span></span>

* <span data-ttu-id="93a14-208">[Télécharger des données tooHDInsight][hdinsight-upload-data]</span><span class="sxs-lookup"><span data-stu-id="93a14-208">[Upload data tooHDInsight][hdinsight-upload-data]</span></span>
* <span data-ttu-id="93a14-209">[Utilisation de Hive avec HDInsight][hdinsight-use-hive]</span><span class="sxs-lookup"><span data-stu-id="93a14-209">[Use Hive with HDInsight][hdinsight-use-hive]</span></span>
* [<span data-ttu-id="93a14-210">Utilisation de Sqoop avec HDInsight</span><span class="sxs-lookup"><span data-stu-id="93a14-210">Use Sqoop with HDInsight</span></span>](hdinsight-use-sqoop.md)
* [<span data-ttu-id="93a14-211">Utilisation d’Oozie avec HDInsight</span><span class="sxs-lookup"><span data-stu-id="93a14-211">Use Oozie with HDInsight</span></span>](hdinsight-use-oozie.md)
* <span data-ttu-id="93a14-212">[Utilisation des tâches MapReduce avec HDInsight][hdinsight-use-mapreduce]</span><span class="sxs-lookup"><span data-stu-id="93a14-212">[Use MapReduce jobs with HDInsight][hdinsight-use-mapreduce]</span></span>

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
