---
title: Utiliser Hadoop Pig avec SSH sur un cluster HDInsight - Azure | Documents Microsoft
description: "Découvrez comment se connecter à un cluster Hadoop Linux avec SSH, avant d’utiliser la commande Pig pour exécuter interactivement des instructions Pig Latin ou avec le traitement par lots."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: b646a93b-4c51-4ba4-84da-3275d9124ebe
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/12/2017
ms.author: larryfr
ms.openlocfilehash: e4c893ef4bfa573dd9fbc9c9b0ae296720769842
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="run-pig-jobs-on-a-linux-based-cluster-with-the-pig-command-ssh"></a><span data-ttu-id="ad314-103">Exécution de tâches Pig sur un cluster Linux avec la commande Pig (SSH)</span><span class="sxs-lookup"><span data-stu-id="ad314-103">Run Pig jobs on a Linux-based cluster with the Pig command (SSH)</span></span>

[!INCLUDE [pig-selector](../../includes/hdinsight-selector-use-pig.md)]

<span data-ttu-id="ad314-104">Découvrez comment exécuter interactivement des tâches Pig à partir d’une connexion SSH sur votre cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="ad314-104">Learn how to interactively run Pig jobs from an SSH connection to your HDInsight cluster.</span></span> <span data-ttu-id="ad314-105">Le langage de programmation Pig Latin permet de décrire les transformations appliquées aux données d’entrée pour produire le résultat souhaité.</span><span class="sxs-lookup"><span data-stu-id="ad314-105">The Pig Latin programming language allows you to describe transformations that are applied to the input data to produce the desired output.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ad314-106">Les étapes décrites dans ce document nécessitent un cluster HDInsight Linux.</span><span class="sxs-lookup"><span data-stu-id="ad314-106">The steps in this document require a Linux-based HDInsight cluster.</span></span> <span data-ttu-id="ad314-107">Linux est le seul système d’exploitation utilisé sur HDInsight version 3.4 ou supérieure.</span><span class="sxs-lookup"><span data-stu-id="ad314-107">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="ad314-108">Pour plus d’informations, consultez [Suppression de HDInsight sous Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="ad314-108">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <span data-ttu-id="ad314-109"><a id="ssh"></a>Connexion avec SSH</span><span class="sxs-lookup"><span data-stu-id="ad314-109"><a id="ssh"></a>Connect with SSH</span></span>

<span data-ttu-id="ad314-110">Utilisez SSH pour vous connecter à votre cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="ad314-110">Use SSH to connect to your HDInsight cluster.</span></span> <span data-ttu-id="ad314-111">L’exemple suivant se connecte à un cluster nommé **myhdinsight** à l’aide du nom de compte **sshuser** :</span><span class="sxs-lookup"><span data-stu-id="ad314-111">The following example connects to a cluster named **myhdinsight** as the account named **sshuser**:</span></span>

    ssh sshuser@myhdinsight-ssh.azurehdinsight.net

<span data-ttu-id="ad314-112">**Si vous avez fourni une clé de certificat pour l’authentification SSH** lorsque vous avez créé le cluster HDInsight, vous devez spécifier l’emplacement de la clé privée sur votre système client.</span><span class="sxs-lookup"><span data-stu-id="ad314-112">**If you provided a certificate key for SSH authentication** when you created the HDInsight cluster, you may need to specify the location of the private key on your client system.</span></span>

    ssh sshuser@myhdinsight-ssh.azurehdinsight.net -i ~/mykey.key

<span data-ttu-id="ad314-113">**Si vous avez fourni un mot de passe pour l’authentification SSH** lorsque vous avez créé le cluster HDInsight, fournissez le mot de passe lorsque vous y êtes invité.</span><span class="sxs-lookup"><span data-stu-id="ad314-113">**If you provided a password for SSH authentication** when you created the HDInsight cluster, provide the password when prompted.</span></span>

<span data-ttu-id="ad314-114">Pour en savoir plus sur l’utilisation de SSH avec HDInsight, voir [Utilisation de SSH avec HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="ad314-114">For more information on using SSH with HDInsight, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

## <span data-ttu-id="ad314-115"><a id="pig"></a>Utilisation de la commande Pig</span><span class="sxs-lookup"><span data-stu-id="ad314-115"><a id="pig"></a>Use the Pig command</span></span>

1. <span data-ttu-id="ad314-116">Une fois connecté, lancez l’interface de ligne de commande Pig à l’aide de la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="ad314-116">Once connected, start the Pig command-line interface (CLI) by using the following command:</span></span>

        pig

    <span data-ttu-id="ad314-117">Après quelques instants, vous devriez voir une invite `grunt>` .</span><span class="sxs-lookup"><span data-stu-id="ad314-117">After a moment, you should see a `grunt>` prompt.</span></span>

2. <span data-ttu-id="ad314-118">Entrez l’instruction suivante :</span><span class="sxs-lookup"><span data-stu-id="ad314-118">Enter the following statement:</span></span>

        LOGS = LOAD '/example/data/sample.log';

    <span data-ttu-id="ad314-119">Cette commande charge le contenu du fichier sample.log dans les JOURNAUX.</span><span class="sxs-lookup"><span data-stu-id="ad314-119">This command loads the contents of the sample.log file into LOGS.</span></span> <span data-ttu-id="ad314-120">Vous pouvez afficher le contenu du fichier à l’aide de l’instruction suivante :</span><span class="sxs-lookup"><span data-stu-id="ad314-120">You can view the contents of the file by using the following statement:</span></span>

        DUMP LOGS;

3. <span data-ttu-id="ad314-121">Transformez ensuite les données en appliquant une expression régulière pour extraire uniquement le niveau de journalisation de chaque enregistrement à l’aide de l’instruction suivante :</span><span class="sxs-lookup"><span data-stu-id="ad314-121">Next, transform the data by applying a regular expression to extract only the logging level from each record by using the following statement:</span></span>

        LEVELS = foreach LOGS generate REGEX_EXTRACT($0, '(TRACE|DEBUG|INFO|WARN|ERROR|FATAL)', 1)  as LOGLEVEL;

    <span data-ttu-id="ad314-122">Vous pouvez utiliser **DUMP** pour afficher les données après la transformation.</span><span class="sxs-lookup"><span data-stu-id="ad314-122">You can use **DUMP** to view the data after the transformation.</span></span> <span data-ttu-id="ad314-123">Dans ce cas, utilisez `DUMP LEVELS;`.</span><span class="sxs-lookup"><span data-stu-id="ad314-123">In this case, use `DUMP LEVELS;`.</span></span>

4. <span data-ttu-id="ad314-124">Continuez à appliquer des transformations à l’aide des instructions dans le tableau suivant :</span><span class="sxs-lookup"><span data-stu-id="ad314-124">Continue applying transformations by using the statements in the following table:</span></span>

    | <span data-ttu-id="ad314-125">Instruction Pig Latin</span><span class="sxs-lookup"><span data-stu-id="ad314-125">Pig Latin statement</span></span> | <span data-ttu-id="ad314-126">Descriptif de l’instruction</span><span class="sxs-lookup"><span data-stu-id="ad314-126">What the statement does</span></span> |
    | ---- | ---- |
    | `FILTEREDLEVELS = FILTER LEVELS by LOGLEVEL is not null;` | <span data-ttu-id="ad314-127">Supprime les lignes contenant une valeur null pour le niveau de journal et stocke les résultats dans `FILTEREDLEVELS`.</span><span class="sxs-lookup"><span data-stu-id="ad314-127">Removes rows that contain a null value for the log level and stores the results into `FILTEREDLEVELS`.</span></span> |
    | `GROUPEDLEVELS = GROUP FILTEREDLEVELS by LOGLEVEL;` | <span data-ttu-id="ad314-128">Regroupe les lignes par niveau de journal et stocke les résultats dans `GROUPEDLEVELS`.</span><span class="sxs-lookup"><span data-stu-id="ad314-128">Groups the rows by log level and stores the results into `GROUPEDLEVELS`.</span></span> |
    | `FREQUENCIES = foreach GROUPEDLEVELS generate group as LOGLEVEL, COUNT(FILTEREDLEVELS.LOGLEVEL) as COUNT;` | <span data-ttu-id="ad314-129">Crée un jeu de données qui contient chaque valeur unique au niveau journal et le nombre de fois où elle se produit.</span><span class="sxs-lookup"><span data-stu-id="ad314-129">Creates a set of data that contains each unique log level value and how many times it occurs.</span></span> <span data-ttu-id="ad314-130">Le jeu de données est stocké dans `FREQUENCIES`.</span><span class="sxs-lookup"><span data-stu-id="ad314-130">The data set is stored into `FREQUENCIES`.</span></span> |
    | `RESULT = order FREQUENCIES by COUNT desc;` | <span data-ttu-id="ad314-131">Trie les niveaux du journal par décompte (décroissant) et stocke ces informations dans `RESULT`.</span><span class="sxs-lookup"><span data-stu-id="ad314-131">Orders the log levels by count (descending) and stores into `RESULT`.</span></span> |

    > [!TIP]
    > <span data-ttu-id="ad314-132">Utilisez `DUMP` pour afficher le résultat de la transformation après chaque étape.</span><span class="sxs-lookup"><span data-stu-id="ad314-132">Use `DUMP` to view the result of the transformation after each step.</span></span>

5. <span data-ttu-id="ad314-133">Vous pouvez également enregistrer les résultats d’une transformation à l’aide de l’instruction `STORE` .</span><span class="sxs-lookup"><span data-stu-id="ad314-133">You can also save the results of a transformation by using the `STORE` statement.</span></span> <span data-ttu-id="ad314-134">Par exemple, l’instruction qui suit enregistre `RESULT` dans le répertoire `/example/data/pigout` sur le stockage par défaut de votre cluster :</span><span class="sxs-lookup"><span data-stu-id="ad314-134">For example, the following statement saves the `RESULT` to the `/example/data/pigout` directory on the default storage for your cluster:</span></span>

        STORE RESULT into '/example/data/pigout';

   > [!NOTE]
   > <span data-ttu-id="ad314-135">Les données sont stockées dans le répertoire spécifié dans des fichiers nommés `part-nnnnn`.</span><span class="sxs-lookup"><span data-stu-id="ad314-135">The data is stored in the specified directory in files named `part-nnnnn`.</span></span> <span data-ttu-id="ad314-136">Si le répertoire existe déjà, vous recevez un message d’erreur.</span><span class="sxs-lookup"><span data-stu-id="ad314-136">If the directory already exists, you receive an error.</span></span>

6. <span data-ttu-id="ad314-137">Pour quitter l’invite Grunt, entrez l’instruction suivante :</span><span class="sxs-lookup"><span data-stu-id="ad314-137">To exit the grunt prompt, enter the following statement:</span></span>

        QUIT;

### <a name="pig-latin-batch-files"></a><span data-ttu-id="ad314-138">Fichiers de commandes Pig Latin</span><span class="sxs-lookup"><span data-stu-id="ad314-138">Pig Latin batch files</span></span>

<span data-ttu-id="ad314-139">Vous pouvez également utiliser la commande Pig pour exécuter le Pig Latin contenu dans un fichier.</span><span class="sxs-lookup"><span data-stu-id="ad314-139">You can also use the Pig command to run Pig Latin contained in a file.</span></span>

1. <span data-ttu-id="ad314-140">Après avoir quitté l’invite Grunt, utilisez la commande suivante pour canaliser STDIN dans un fichier nommé `pigbatch.pig`.</span><span class="sxs-lookup"><span data-stu-id="ad314-140">After exiting the grunt prompt, use the following command to pipe STDIN into a file named `pigbatch.pig`.</span></span> <span data-ttu-id="ad314-141">Ce fichier est créé dans le répertoire de base du compte d’utilisateur SSH.</span><span class="sxs-lookup"><span data-stu-id="ad314-141">This file is created in the home directory for the SSH user account.</span></span>

        cat > ~/pigbatch.pig

2. <span data-ttu-id="ad314-142">Tapez ou collez les lignes suivantes, puis utilisez Ctrl + D lorsque vous avez terminé.</span><span class="sxs-lookup"><span data-stu-id="ad314-142">Type or paste the following lines, and then use Ctrl+D when finished.</span></span>

        LOGS = LOAD '/example/data/sample.log';
        LEVELS = foreach LOGS generate REGEX_EXTRACT($0, '(TRACE|DEBUG|INFO|WARN|ERROR|FATAL)', 1)  as LOGLEVEL;
        FILTEREDLEVELS = FILTER LEVELS by LOGLEVEL is not null;
        GROUPEDLEVELS = GROUP FILTEREDLEVELS by LOGLEVEL;
        FREQUENCIES = foreach GROUPEDLEVELS generate group as LOGLEVEL, COUNT(FILTEREDLEVELS.LOGLEVEL) as COUNT;
        RESULT = order FREQUENCIES by COUNT desc;
        DUMP RESULT;

3. <span data-ttu-id="ad314-143">Utilisez la commande suivante pour exécuter le fichier `pigbatch.pig` à l’aide de la commande Pig.</span><span class="sxs-lookup"><span data-stu-id="ad314-143">Use the following command to run the `pigbatch.pig` file by using the Pig command.</span></span>

        pig ~/pigbatch.pig

    <span data-ttu-id="ad314-144">Une fois le traitement par lots terminé, vous observez la sortie suivante :</span><span class="sxs-lookup"><span data-stu-id="ad314-144">Once the batch job finishes, you see the following output:</span></span>

        (TRACE,816)
        (DEBUG,434)
        (INFO,96)
        (WARN,11)
        (ERROR,6)
        (FATAL,2)


## <span data-ttu-id="ad314-145"><a id="nextsteps"></a>Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="ad314-145"><a id="nextsteps"></a>Next steps</span></span>

<span data-ttu-id="ad314-146">Pour obtenir des informations générales sur Pig sur HDInsight, consultez le document suivant :</span><span class="sxs-lookup"><span data-stu-id="ad314-146">For general information on Pig in HDInsight, see the following document:</span></span>

* [<span data-ttu-id="ad314-147">Utilisation de Pig avec Hadoop sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="ad314-147">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)

<span data-ttu-id="ad314-148">Pour plus d’informations sur les autres façons de travailler avec Hadoop sur HDInsight, consultez les documents suivants :</span><span class="sxs-lookup"><span data-stu-id="ad314-148">For more information on other ways to work with Hadoop on HDInsight, see the following documents:</span></span>

* [<span data-ttu-id="ad314-149">Utilisation de Hive avec Hadoop sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="ad314-149">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="ad314-150">Utilisation de MapReduce avec Hadoop sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="ad314-150">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)
