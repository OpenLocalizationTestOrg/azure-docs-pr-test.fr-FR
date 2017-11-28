---
title: "Utiliser Hadoop Pig avec le Bureau à distance dans HDInsight - Azure | Documents Microsoft"
description: "Apprenez à utiliser la commande Pig pour exécuter les instructions Pig Latin à partir d'une connexion Bureau à distance vers un cluster Windows Hadoop sur HDInsight."
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
ms.openlocfilehash: 5e8d4fbd8afc54c8bbc1a9a71c66d7022a7d5986
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="run-pig-jobs-from-a-remote-desktop-connection"></a><span data-ttu-id="5eab0-103">Exécution de tâches Pig depuis une connexion Bureau à distance</span><span class="sxs-lookup"><span data-stu-id="5eab0-103">Run Pig jobs from a Remote Desktop connection</span></span>
[!INCLUDE [pig-selector](../../includes/hdinsight-selector-use-pig.md)]

<span data-ttu-id="5eab0-104">Ce document fournit une procédure pas à pas de l'utilisation de la commande Pig pour exécuter les instructions Pig Latin à partir d'une connexion Bureau à distance vers un cluster HDInsight Windows.</span><span class="sxs-lookup"><span data-stu-id="5eab0-104">This document provides a walkthrough for using the Pig command to run Pig Latin statements from a Remote Desktop connection to a Windows-based HDInsight cluster.</span></span> <span data-ttu-id="5eab0-105">Pig Latin permet de créer des applications MapReduce en décrivant les transformations de données, plutôt que de mapper et de réduire les fonctions.</span><span class="sxs-lookup"><span data-stu-id="5eab0-105">Pig Latin allows you to create MapReduce applications by describing data transformations, rather than map and reduce functions.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5eab0-106">Le Bureau à distance n’est disponible que sur les clusters HDInsight qui utilisent Windows comme système d’exploitation.</span><span class="sxs-lookup"><span data-stu-id="5eab0-106">Remote Desktop is only available on HDInsight clusters that use Windows as the operating system.</span></span> <span data-ttu-id="5eab0-107">Linux est le seul système d’exploitation utilisé sur HDInsight version 3.4 ou supérieure.</span><span class="sxs-lookup"><span data-stu-id="5eab0-107">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="5eab0-108">Pour plus d’informations, consultez [Suppression de HDInsight sous Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="5eab0-108">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>
>
> <span data-ttu-id="5eab0-109">Pour HDInsight 3.4 ou les versions ultérieures, consultez l’article [Utiliser Pig avec HDInsight et SSH](hdinsight-hadoop-use-pig-ssh.md) pour plus d’informations sur l’exécution interactive de travaux Pig directement sur le cluster à partir d’une ligne de commande.</span><span class="sxs-lookup"><span data-stu-id="5eab0-109">For HDInsight 3.4 or greater, see [Use Pig with HDInsight and SSH](hdinsight-hadoop-use-pig-ssh.md) for information on interactively running Pig jobs directly on the cluster from a command-line.</span></span>

## <span data-ttu-id="5eab0-110"><a id="prereq"></a>Configuration requise</span><span class="sxs-lookup"><span data-stu-id="5eab0-110"><a id="prereq"></a>Prerequisites</span></span>
<span data-ttu-id="5eab0-111">Pour effectuer les étapes présentées dans cet article, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="5eab0-111">To complete the steps in this article, you will need the following.</span></span>

* <span data-ttu-id="5eab0-112">un cluster HDInsight basé sur Windows (Hadoop sur HDInsight)</span><span class="sxs-lookup"><span data-stu-id="5eab0-112">A Windows-based HDInsight (Hadoop on HDInsight) cluster</span></span>
* <span data-ttu-id="5eab0-113">Un ordinateur client avec Windows 10, Windows 8 ou Windows 7</span><span class="sxs-lookup"><span data-stu-id="5eab0-113">A client computer running Windows 10, Windows 8, or Windows 7</span></span>

## <span data-ttu-id="5eab0-114"><a id="connect"></a>Connexion avec le Bureau à distance</span><span class="sxs-lookup"><span data-stu-id="5eab0-114"><a id="connect"></a>Connect with Remote Desktop</span></span>
<span data-ttu-id="5eab0-115">Activez le Bureau à distance pour le cluster HDInsight, puis connectez-vous à lui en suivant les instructions fournies dans [Connexion à des clusters HDInsight à l’aide de RDP](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp).</span><span class="sxs-lookup"><span data-stu-id="5eab0-115">Enable Remote Desktop for the HDInsight cluster, then connect to it by following the instructions at [Connect to HDInsight clusters using RDP](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp).</span></span>

## <span data-ttu-id="5eab0-116"><a id="pig"></a>Utilisation de la commande Pig</span><span class="sxs-lookup"><span data-stu-id="5eab0-116"><a id="pig"></a>Use the Pig command</span></span>
1. <span data-ttu-id="5eab0-117">Lorsque vous disposez d’une connexion Bureau à distance, démarrez la **ligne de commande Hadoop** en cliquant sur l’icône sur le bureau.</span><span class="sxs-lookup"><span data-stu-id="5eab0-117">After you have a Remote Desktop connection, start the **Hadoop Command Line** by using the icon on the desktop.</span></span>
2. <span data-ttu-id="5eab0-118">Utilisez ce qui suit pour lancer la commande Pig :</span><span class="sxs-lookup"><span data-stu-id="5eab0-118">Use the following to start the Pig command:</span></span>

        %pig_home%\bin\pig

    <span data-ttu-id="5eab0-119">Une invite `grunt>` s’affiche.</span><span class="sxs-lookup"><span data-stu-id="5eab0-119">You will be presented with a `grunt>` prompt.</span></span>
3. <span data-ttu-id="5eab0-120">Entrez l’instruction suivante :</span><span class="sxs-lookup"><span data-stu-id="5eab0-120">Enter the following statement:</span></span>

        LOGS = LOAD 'wasb:///example/data/sample.log';

    <span data-ttu-id="5eab0-121">Cette commande charge le contenu du fichier sample.log dans les JOURNAUX.</span><span class="sxs-lookup"><span data-stu-id="5eab0-121">This command loads the contents of the sample.log file into the LOGS file.</span></span> <span data-ttu-id="5eab0-122">Vous pouvez afficher le contenu du fichier à l’aide de la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="5eab0-122">You can view the contents of the file by using the following command:</span></span>

        DUMP LOGS;
4. <span data-ttu-id="5eab0-123">Transformez ensuite les données en appliquant une expression régulière pour extraire uniquement le niveau de journalisation de chaque enregistrement :</span><span class="sxs-lookup"><span data-stu-id="5eab0-123">Transform the data by applying a regular expression to extract only the logging level from each record:</span></span>

        LEVELS = foreach LOGS generate REGEX_EXTRACT($0, '(TRACE|DEBUG|INFO|WARN|ERROR|FATAL)', 1)  as LOGLEVEL;

    <span data-ttu-id="5eab0-124">Vous pouvez utiliser **DUMP** pour afficher les données après la transformation.</span><span class="sxs-lookup"><span data-stu-id="5eab0-124">You can use **DUMP** to view the data after the transformation.</span></span> <span data-ttu-id="5eab0-125">Dans ce cas, `DUMP LEVELS;`.</span><span class="sxs-lookup"><span data-stu-id="5eab0-125">In this case, `DUMP LEVELS;`.</span></span>
5. <span data-ttu-id="5eab0-126">Continuez à appliquer des transformations à l’aide des instructions suivantes.</span><span class="sxs-lookup"><span data-stu-id="5eab0-126">Continue applying transformations by using the following statements.</span></span> <span data-ttu-id="5eab0-127">Utilisez `DUMP` pour afficher le résultat de la transformation après chaque étape.</span><span class="sxs-lookup"><span data-stu-id="5eab0-127">Use `DUMP` to view the result of the transformation after each step.</span></span>

    <table>
    <tr>
    <th><span data-ttu-id="5eab0-128">Instruction</span><span class="sxs-lookup"><span data-stu-id="5eab0-128">Statement</span></span></th><th><span data-ttu-id="5eab0-129">Résultat</span><span class="sxs-lookup"><span data-stu-id="5eab0-129">What it does</span></span></th>
    </tr>
    <tr>
    <td><span data-ttu-id="5eab0-130">FILTEREDLEVELS = FILTER LEVELS by LOGLEVEL is not null;</span><span class="sxs-lookup"><span data-stu-id="5eab0-130">FILTEREDLEVELS = FILTER LEVELS by LOGLEVEL is not null;</span></span></td><td><span data-ttu-id="5eab0-131">Supprime les lignes contenant une valeur null pour le niveau de journal et stocke les résultats dans FILTEREDLEVELS.</span><span class="sxs-lookup"><span data-stu-id="5eab0-131">Removes rows that contain a null value for the log level and stores the results into FILTEREDLEVELS.</span></span></td>
    </tr>
    <tr>
    <td><span data-ttu-id="5eab0-132">GROUPEDLEVELS = GROUP FILTEREDLEVELS by LOGLEVEL;</span><span class="sxs-lookup"><span data-stu-id="5eab0-132">GROUPEDLEVELS = GROUP FILTEREDLEVELS by LOGLEVEL;</span></span></td><td><span data-ttu-id="5eab0-133">Regroupe les lignes par niveau de journal et stocke les résultats dans GROUPEDLEVELS.</span><span class="sxs-lookup"><span data-stu-id="5eab0-133">Groups the rows by log level and stores the results into GROUPEDLEVELS.</span></span></td>
    </tr>
    <tr>
    <td><span data-ttu-id="5eab0-134">FREQUENCIES = foreach GROUPEDLEVELS generate group as LOGLEVEL, COUNT(FILTEREDLEVELS.LOGLEVEL) as COUNT;</span><span class="sxs-lookup"><span data-stu-id="5eab0-134">FREQUENCIES = foreach GROUPEDLEVELS generate group as LOGLEVEL, COUNT(FILTEREDLEVELS.LOGLEVEL) as COUNT;</span></span></td><td><span data-ttu-id="5eab0-135">Crée un jeu de données qui contient chaque valeur unique au niveau journal et le nombre de fois où elle se produit.</span><span class="sxs-lookup"><span data-stu-id="5eab0-135">Creates a new set of data that contains each unique log level value and how many times it occurs.</span></span> <span data-ttu-id="5eab0-136">Ces informations sont stockées dans FREQUENCIES</span><span class="sxs-lookup"><span data-stu-id="5eab0-136">This is stored into FREQUENCIES</span></span></td>
    </tr>
    <tr>
    <td><span data-ttu-id="5eab0-137">RESULT = order FREQUENCIES by COUNT desc;</span><span class="sxs-lookup"><span data-stu-id="5eab0-137">RESULT = order FREQUENCIES by COUNT desc;</span></span></td><td><span data-ttu-id="5eab0-138">Trie les niveaux du journal par décompte (décroissant) et stocke ces informations dans RESULT</span><span class="sxs-lookup"><span data-stu-id="5eab0-138">Orders the log levels by count (descending,) and stores into RESULT</span></span></td>
    </tr>
    </table><span data-ttu-id="5eab0-139">
6. Vous pouvez également enregistrer les résultats d’une transformation à l’aide de l’instruction `STORE`.</span><span class="sxs-lookup"><span data-stu-id="5eab0-139">
6. You can also save the results of a transformation by using the `STORE` statement.</span></span> <span data-ttu-id="5eab0-140">Par exemple, la commande suivante enregistre `RESULT` dans le répertoire **/example/data/pigout** sur le conteneur de stockage par défaut de votre cluster :</span><span class="sxs-lookup"><span data-stu-id="5eab0-140">For example, the following command saves the `RESULT` to the **/example/data/pigout** directory in the default storage container for your cluster:</span></span>

        STORE RESULT into 'wasb:///example/data/pigout'

   > [!NOTE]
   > <span data-ttu-id="5eab0-141">Les données sont stockées dans le répertoire spécifié dans des fichiers nommés **part-nnnnn**.</span><span class="sxs-lookup"><span data-stu-id="5eab0-141">The data is stored in the specified directory in files named **part-nnnnn**.</span></span> <span data-ttu-id="5eab0-142">Si le répertoire existe déjà, vous recevrez un message d’erreur.</span><span class="sxs-lookup"><span data-stu-id="5eab0-142">If the directory already exists, you will receive an error message.</span></span>
   >
   >
7. <span data-ttu-id="5eab0-143">Pour quitter l’invite Grunt, entrez l’instruction suivante.</span><span class="sxs-lookup"><span data-stu-id="5eab0-143">To exit the grunt prompt, enter the following statement.</span></span>

        QUIT;

### <a name="pig-latin-batch-files"></a><span data-ttu-id="5eab0-144">Fichiers de commandes Pig Latin</span><span class="sxs-lookup"><span data-stu-id="5eab0-144">Pig Latin batch files</span></span>
<span data-ttu-id="5eab0-145">Vous pouvez également utiliser la commande Pig pour exécuter le Pig Latin contenu dans un fichier.</span><span class="sxs-lookup"><span data-stu-id="5eab0-145">You can also use the Pig command to run Pig Latin that is contained in a file.</span></span>

1. <span data-ttu-id="5eab0-146">Après avoir quitté l’invite Grunt, ouvrez le **bloc-notes** et créez un nouveau fichier nommé **pigbatch.pig** dans le répertoire **%PIG_HOME%**.</span><span class="sxs-lookup"><span data-stu-id="5eab0-146">After exiting the grunt prompt, open **Notepad** and create a new file named **pigbatch.pig** in the **%PIG_HOME%** directory.</span></span>
2. <span data-ttu-id="5eab0-147">Tapez ou collez les lignes suivantes dans le fichier **pigbatch.pig** , puis enregistrez-le.</span><span class="sxs-lookup"><span data-stu-id="5eab0-147">Type or paste the following lines into the **pigbatch.pig** file, and then save it:</span></span>

        LOGS = LOAD 'wasb:///example/data/sample.log';
        LEVELS = foreach LOGS generate REGEX_EXTRACT($0, '(TRACE|DEBUG|INFO|WARN|ERROR|FATAL)', 1)  as LOGLEVEL;
        FILTEREDLEVELS = FILTER LEVELS by LOGLEVEL is not null;
        GROUPEDLEVELS = GROUP FILTEREDLEVELS by LOGLEVEL;
        FREQUENCIES = foreach GROUPEDLEVELS generate group as LOGLEVEL, COUNT(FILTEREDLEVELS.LOGLEVEL) as COUNT;
        RESULT = order FREQUENCIES by COUNT desc;
        DUMP RESULT;
3. <span data-ttu-id="5eab0-148">Utilisez les éléments suivants pour exécuter le fichier **pigbatch.pig** à l’aide de la commande pig.</span><span class="sxs-lookup"><span data-stu-id="5eab0-148">Use the following to run the **pigbatch.pig** file using the pig command.</span></span>

        pig %PIG_HOME%\pigbatch.pig

    <span data-ttu-id="5eab0-149">Une fois le traitement par lots terminé, vous devez voir la sortie suivante, qui doit être la même que lorsque vous avez utilisé `DUMP RESULT;` lors des étapes précédentes :</span><span class="sxs-lookup"><span data-stu-id="5eab0-149">When the batch job completes, you should see the following output, which should be the same as when you used `DUMP RESULT;` in the previous steps:</span></span>

        (TRACE,816)
        (DEBUG,434)
        (INFO,96)
        (WARN,11)
        (ERROR,6)
        (FATAL,2)

## <span data-ttu-id="5eab0-150"><a id="summary"></a>Résumé</span><span class="sxs-lookup"><span data-stu-id="5eab0-150"><a id="summary"></a>Summary</span></span>
<span data-ttu-id="5eab0-151">Comme vous pouvez le voir, la commande Pig vous permet d’exécuter interactivement des opérations MapReduce ou d’exécuter des tâches Pig Latin stockées dans un fichier de commandes.</span><span class="sxs-lookup"><span data-stu-id="5eab0-151">As you can see, the Pig command allows you to interactively run MapReduce operations, or run Pig Latin jobs that are stored in a batch file.</span></span>

## <span data-ttu-id="5eab0-152"><a id="nextsteps"></a>Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="5eab0-152"><a id="nextsteps"></a>Next steps</span></span>
<span data-ttu-id="5eab0-153">Pour obtenir des informations générales sur Pig dans HDInsight :</span><span class="sxs-lookup"><span data-stu-id="5eab0-153">For general information about Pig in HDInsight:</span></span>

* [<span data-ttu-id="5eab0-154">Utilisation de Pig avec Hadoop sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="5eab0-154">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)

<span data-ttu-id="5eab0-155">Pour plus d’informations sur d’autres méthodes de travail avec Hadoop sur HDInsight :</span><span class="sxs-lookup"><span data-stu-id="5eab0-155">For information about other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="5eab0-156">Utilisation de Hive avec Hadoop sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="5eab0-156">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="5eab0-157">Utilisation de MapReduce avec Hadoop sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="5eab0-157">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)
