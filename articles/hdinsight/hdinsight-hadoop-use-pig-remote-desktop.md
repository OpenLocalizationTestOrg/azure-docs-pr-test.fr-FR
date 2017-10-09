---
title: "aaaUse Hadoop Pig avec le Bureau à distance dans HDInsight - Azure | Documents Microsoft"
description: "Découvrez comment toouse hello instructions de Pig Latin Pig commande toorun à partir d’un bureau à distance connexion tooa basé sur Windows de cluster Hadoop dans HDInsight."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: e034a286-de0f-465f-8bf1-3d085ca6abed
ms.service: hdinsight
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 01/17/2017
ms.author: larryfr
ROBOTS: NOINDEX
ms.openlocfilehash: 2a4565fa827cd45fdbe6194b0486df93a6561084
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="run-pig-jobs-from-a-remote-desktop-connection"></a><span data-ttu-id="3b63c-103">Exécution de tâches Pig depuis une connexion Bureau à distance</span><span class="sxs-lookup"><span data-stu-id="3b63c-103">Run Pig jobs from a Remote Desktop connection</span></span>
[!INCLUDE [pig-selector](../../includes/hdinsight-selector-use-pig.md)]

<span data-ttu-id="3b63c-104">Ce document fournit une procédure pas à pas pour l’utilisation d’instructions hello Pig commandes toorun Pig Latin d’un cluster de basés sur Windows de HDInsight de tooa connexion Bureau à distance.</span><span class="sxs-lookup"><span data-stu-id="3b63c-104">This document provides a walkthrough for using hello Pig command toorun Pig Latin statements from a Remote Desktop connection tooa Windows-based HDInsight cluster.</span></span> <span data-ttu-id="3b63c-105">Pig Latin vous permet de toocreate MapReduce applications en décrivant les transformations de données, plutôt que mapper et réduire des fonctions.</span><span class="sxs-lookup"><span data-stu-id="3b63c-105">Pig Latin allows you toocreate MapReduce applications by describing data transformations, rather than map and reduce functions.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3b63c-106">Bureau à distance n’est disponible sur les clusters HDInsight utilisent Windows comme système d’exploitation de hello.</span><span class="sxs-lookup"><span data-stu-id="3b63c-106">Remote Desktop is only available on HDInsight clusters that use Windows as hello operating system.</span></span> <span data-ttu-id="3b63c-107">Linux est hello seul système d’exploitation utilisé sur HDInsight version 3.4 ou supérieure.</span><span class="sxs-lookup"><span data-stu-id="3b63c-107">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="3b63c-108">Pour plus d’informations, consultez [Suppression de HDInsight sous Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="3b63c-108">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>
>
> <span data-ttu-id="3b63c-109">Pour HDInsight 3.4 ou supérieure, consultez [utilisez Pig avec HDInsight et SSH](hdinsight-hadoop-use-pig-ssh.md) pour plus d’informations sur l’exécution de manière interactive Pig travaux directement sur hello de cluster à partir d’une ligne de commande.</span><span class="sxs-lookup"><span data-stu-id="3b63c-109">For HDInsight 3.4 or greater, see [Use Pig with HDInsight and SSH](hdinsight-hadoop-use-pig-ssh.md) for information on interactively running Pig jobs directly on hello cluster from a command-line.</span></span>

## <span data-ttu-id="3b63c-110"><a id="prereq"></a>Configuration requise</span><span class="sxs-lookup"><span data-stu-id="3b63c-110"><a id="prereq"></a>Prerequisites</span></span>
<span data-ttu-id="3b63c-111">toocomplete hello étapes décrites dans cet article, vous devez suivant de hello.</span><span class="sxs-lookup"><span data-stu-id="3b63c-111">toocomplete hello steps in this article, you will need hello following.</span></span>

* <span data-ttu-id="3b63c-112">un cluster HDInsight basé sur Windows (Hadoop sur HDInsight)</span><span class="sxs-lookup"><span data-stu-id="3b63c-112">A Windows-based HDInsight (Hadoop on HDInsight) cluster</span></span>
* <span data-ttu-id="3b63c-113">Un ordinateur client avec Windows 10, Windows 8 ou Windows 7</span><span class="sxs-lookup"><span data-stu-id="3b63c-113">A client computer running Windows 10, Windows 8, or Windows 7</span></span>

## <span data-ttu-id="3b63c-114"><a id="connect"></a>Connexion avec le Bureau à distance</span><span class="sxs-lookup"><span data-stu-id="3b63c-114"><a id="connect"></a>Connect with Remote Desktop</span></span>
<span data-ttu-id="3b63c-115">Activer le Bureau à distance pour le cluster HDInsight de hello, puis connecter tooit en suivant les instructions de hello sur [connecter clusters tooHDInsight à l’aide du protocole RDP](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp).</span><span class="sxs-lookup"><span data-stu-id="3b63c-115">Enable Remote Desktop for hello HDInsight cluster, then connect tooit by following hello instructions at [Connect tooHDInsight clusters using RDP](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp).</span></span>

## <span data-ttu-id="3b63c-116"><a id="pig"></a>Utilisez la commande de Pig hello</span><span class="sxs-lookup"><span data-stu-id="3b63c-116"><a id="pig"></a>Use hello Pig command</span></span>
1. <span data-ttu-id="3b63c-117">Une fois que vous avez une connexion Bureau à distance, démarrer hello **ligne de commande Hadoop** en utilisant l’icône de hello sur le bureau de hello.</span><span class="sxs-lookup"><span data-stu-id="3b63c-117">After you have a Remote Desktop connection, start hello **Hadoop Command Line** by using hello icon on hello desktop.</span></span>
2. <span data-ttu-id="3b63c-118">Utilisez hello toostart hello Pig commande suivante :</span><span class="sxs-lookup"><span data-stu-id="3b63c-118">Use hello following toostart hello Pig command:</span></span>

        %pig_home%\bin\pig

    <span data-ttu-id="3b63c-119">Une invite `grunt>` s’affiche.</span><span class="sxs-lookup"><span data-stu-id="3b63c-119">You will be presented with a `grunt>` prompt.</span></span>
3. <span data-ttu-id="3b63c-120">Entrez hello après l’instruction :</span><span class="sxs-lookup"><span data-stu-id="3b63c-120">Enter hello following statement:</span></span>

        LOGS = LOAD 'wasb:///example/data/sample.log';

    <span data-ttu-id="3b63c-121">Cette commande charge contenu hello du fichier d’exemple.log hello dans les fichiers de journaux hello.</span><span class="sxs-lookup"><span data-stu-id="3b63c-121">This command loads hello contents of hello sample.log file into hello LOGS file.</span></span> <span data-ttu-id="3b63c-122">Vous pouvez afficher le contenu hello du fichier de hello à l’aide de hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="3b63c-122">You can view hello contents of hello file by using hello following command:</span></span>

        DUMP LOGS;
4. <span data-ttu-id="3b63c-123">Transformer les données de hello en appliquant un niveau de journalisation de hello uniquement tooextract expression régulière à partir de chaque enregistrement :</span><span class="sxs-lookup"><span data-stu-id="3b63c-123">Transform hello data by applying a regular expression tooextract only hello logging level from each record:</span></span>

        LEVELS = foreach LOGS generate REGEX_EXTRACT($0, '(TRACE|DEBUG|INFO|WARN|ERROR|FATAL)', 1)  as LOGLEVEL;

    <span data-ttu-id="3b63c-124">Vous pouvez utiliser **DUMP** tooview les données de salutation après la transformation de hello.</span><span class="sxs-lookup"><span data-stu-id="3b63c-124">You can use **DUMP** tooview hello data after hello transformation.</span></span> <span data-ttu-id="3b63c-125">Dans ce cas, `DUMP LEVELS;`.</span><span class="sxs-lookup"><span data-stu-id="3b63c-125">In this case, `DUMP LEVELS;`.</span></span>
5. <span data-ttu-id="3b63c-126">Continuer l’application de transformations à l’aide de hello suivant les instructions.</span><span class="sxs-lookup"><span data-stu-id="3b63c-126">Continue applying transformations by using hello following statements.</span></span> <span data-ttu-id="3b63c-127">Utilisez `DUMP` résultat de hello tooview de transformation hello après chaque étape.</span><span class="sxs-lookup"><span data-stu-id="3b63c-127">Use `DUMP` tooview hello result of hello transformation after each step.</span></span>

    <table>
    <tr>
    <th><span data-ttu-id="3b63c-128">Instruction</span><span class="sxs-lookup"><span data-stu-id="3b63c-128">Statement</span></span></th><th><span data-ttu-id="3b63c-129">Résultat</span><span class="sxs-lookup"><span data-stu-id="3b63c-129">What it does</span></span></th>
    </tr>
    <tr>
    <td><span data-ttu-id="3b63c-130">FILTEREDLEVELS = FILTER LEVELS by LOGLEVEL is not null;</span><span class="sxs-lookup"><span data-stu-id="3b63c-130">FILTEREDLEVELS = FILTER LEVELS by LOGLEVEL is not null;</span></span></td><td><span data-ttu-id="3b63c-131">Supprime les lignes qui contiennent une valeur null pour le niveau de journal hello et stocke les résultats de hello dans FILTEREDLEVELS.</span><span class="sxs-lookup"><span data-stu-id="3b63c-131">Removes rows that contain a null value for hello log level and stores hello results into FILTEREDLEVELS.</span></span></td>
    </tr>
    <tr>
    <td><span data-ttu-id="3b63c-132">GROUPEDLEVELS = GROUP FILTEREDLEVELS by LOGLEVEL;</span><span class="sxs-lookup"><span data-stu-id="3b63c-132">GROUPEDLEVELS = GROUP FILTEREDLEVELS by LOGLEVEL;</span></span></td><td><span data-ttu-id="3b63c-133">Hello de groupes de lignes par niveau de journal et stocke des résultats de hello dans GROUPEDLEVELS.</span><span class="sxs-lookup"><span data-stu-id="3b63c-133">Groups hello rows by log level and stores hello results into GROUPEDLEVELS.</span></span></td>
    </tr>
    <tr>
    <td><span data-ttu-id="3b63c-134">FREQUENCIES = foreach GROUPEDLEVELS generate group as LOGLEVEL, COUNT(FILTEREDLEVELS.LOGLEVEL) as COUNT;</span><span class="sxs-lookup"><span data-stu-id="3b63c-134">FREQUENCIES = foreach GROUPEDLEVELS generate group as LOGLEVEL, COUNT(FILTEREDLEVELS.LOGLEVEL) as COUNT;</span></span></td><td><span data-ttu-id="3b63c-135">Crée un jeu de données qui contient chaque valeur unique au niveau journal et le nombre de fois où elle se produit.</span><span class="sxs-lookup"><span data-stu-id="3b63c-135">Creates a new set of data that contains each unique log level value and how many times it occurs.</span></span> <span data-ttu-id="3b63c-136">Ces informations sont stockées dans FREQUENCIES</span><span class="sxs-lookup"><span data-stu-id="3b63c-136">This is stored into FREQUENCIES</span></span></td>
    </tr>
    <tr>
    <td><span data-ttu-id="3b63c-137">RESULT = order FREQUENCIES by COUNT desc;</span><span class="sxs-lookup"><span data-stu-id="3b63c-137">RESULT = order FREQUENCIES by COUNT desc;</span></span></td><td><span data-ttu-id="3b63c-138">Les niveaux de journalisation hello par nombre (ordre décroissant) et stocke des commandes dans les résultats</span><span class="sxs-lookup"><span data-stu-id="3b63c-138">Orders hello log levels by count (descending,) and stores into RESULT</span></span></td>
    </tr>
    </table><span data-ttu-id="3b63c-139">
6.Vous pouvez également enregistrer les résultats de hello d’une transformation à l’aide de hello `STORE` instruction.</span><span class="sxs-lookup"><span data-stu-id="3b63c-139">
6. You can also save hello results of a transformation by using hello `STORE` statement.</span></span> <span data-ttu-id="3b63c-140">Par exemple, hello commande suivante enregistre hello `RESULT` toohello **/example/data/pigout** répertoire dans le conteneur de stockage par défaut hello pour votre cluster :</span><span class="sxs-lookup"><span data-stu-id="3b63c-140">For example, hello following command saves hello `RESULT` toohello **/example/data/pigout** directory in hello default storage container for your cluster:</span></span>

        STORE RESULT into 'wasb:///example/data/pigout'

   > [!NOTE]
   > <span data-ttu-id="3b63c-141">les données de salutation sont stockées dans le répertoire spécifié de hello dans les fichiers nommés **partie-nnnnn**.</span><span class="sxs-lookup"><span data-stu-id="3b63c-141">hello data is stored in hello specified directory in files named **part-nnnnn**.</span></span> <span data-ttu-id="3b63c-142">Si le répertoire de hello existe déjà, vous recevrez un message d’erreur.</span><span class="sxs-lookup"><span data-stu-id="3b63c-142">If hello directory already exists, you will receive an error message.</span></span>
   >
   >
7. <span data-ttu-id="3b63c-143">tooexit hello des grunt à l’invite, entrez hello après l’instruction.</span><span class="sxs-lookup"><span data-stu-id="3b63c-143">tooexit hello grunt prompt, enter hello following statement.</span></span>

        QUIT;

### <a name="pig-latin-batch-files"></a><span data-ttu-id="3b63c-144">Fichiers de commandes Pig Latin</span><span class="sxs-lookup"><span data-stu-id="3b63c-144">Pig Latin batch files</span></span>
<span data-ttu-id="3b63c-145">Vous pouvez également utiliser hello Pig commande toorun Latin Pig qui est contenue dans un fichier.</span><span class="sxs-lookup"><span data-stu-id="3b63c-145">You can also use hello Pig command toorun Pig Latin that is contained in a file.</span></span>

1. <span data-ttu-id="3b63c-146">Après avoir quitté l’invite de grunt hello, ouvrez **bloc-notes** et créer un nouveau fichier nommé **pigbatch.pig** Bonjour **PIG_HOME %** active.</span><span class="sxs-lookup"><span data-stu-id="3b63c-146">After exiting hello grunt prompt, open **Notepad** and create a new file named **pigbatch.pig** in hello **%PIG_HOME%** directory.</span></span>
2. <span data-ttu-id="3b63c-147">Type ou à la suite de hello coller des lignes en hello **pigbatch.pig** de fichier, puis enregistrez-le :</span><span class="sxs-lookup"><span data-stu-id="3b63c-147">Type or paste hello following lines into hello **pigbatch.pig** file, and then save it:</span></span>

        LOGS = LOAD 'wasb:///example/data/sample.log';
        LEVELS = foreach LOGS generate REGEX_EXTRACT($0, '(TRACE|DEBUG|INFO|WARN|ERROR|FATAL)', 1)  as LOGLEVEL;
        FILTEREDLEVELS = FILTER LEVELS by LOGLEVEL is not null;
        GROUPEDLEVELS = GROUP FILTEREDLEVELS by LOGLEVEL;
        FREQUENCIES = foreach GROUPEDLEVELS generate group as LOGLEVEL, COUNT(FILTEREDLEVELS.LOGLEVEL) as COUNT;
        RESULT = order FREQUENCIES by COUNT desc;
        DUMP RESULT;
3. <span data-ttu-id="3b63c-148">Hello utilisation suivant toorun hello **pigbatch.pig** fichier à l’aide de la commande de pig hello.</span><span class="sxs-lookup"><span data-stu-id="3b63c-148">Use hello following toorun hello **pigbatch.pig** file using hello pig command.</span></span>

        pig %PIG_HOME%\pigbatch.pig

    <span data-ttu-id="3b63c-149">Lors de la tâche hello est terminée, vous devez voir hello suivant de sortie, qui doit être hello de même que lorsque vous avez utilisé `DUMP RESULT;` dans les étapes précédentes hello :</span><span class="sxs-lookup"><span data-stu-id="3b63c-149">When hello batch job completes, you should see hello following output, which should be hello same as when you used `DUMP RESULT;` in hello previous steps:</span></span>

        (TRACE,816)
        (DEBUG,434)
        (INFO,96)
        (WARN,11)
        (ERROR,6)
        (FATAL,2)

## <span data-ttu-id="3b63c-150"><a id="summary"></a>Résumé</span><span class="sxs-lookup"><span data-stu-id="3b63c-150"><a id="summary"></a>Summary</span></span>
<span data-ttu-id="3b63c-151">Comme vous pouvez le voir, hello commande de Pig vous permet de toointeractively exécuter des opérations de MapReduce ou exécuter des travaux Pig Latin qui est stockés dans un fichier de commandes.</span><span class="sxs-lookup"><span data-stu-id="3b63c-151">As you can see, hello Pig command allows you toointeractively run MapReduce operations, or run Pig Latin jobs that are stored in a batch file.</span></span>

## <span data-ttu-id="3b63c-152"><a id="nextsteps"></a>Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="3b63c-152"><a id="nextsteps"></a>Next steps</span></span>
<span data-ttu-id="3b63c-153">Pour obtenir des informations générales sur Pig dans HDInsight :</span><span class="sxs-lookup"><span data-stu-id="3b63c-153">For general information about Pig in HDInsight:</span></span>

* [<span data-ttu-id="3b63c-154">Utilisation de Pig avec Hadoop sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="3b63c-154">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)

<span data-ttu-id="3b63c-155">Pour plus d’informations sur d’autres méthodes de travail avec Hadoop sur HDInsight :</span><span class="sxs-lookup"><span data-stu-id="3b63c-155">For information about other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="3b63c-156">Utilisation de Hive avec Hadoop sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="3b63c-156">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="3b63c-157">Utilisation de MapReduce avec Hadoop sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="3b63c-157">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)
