---
title: aaaUse Hadoop Pig avec SSH sur un cluster HDInsight - Azure | Documents Microsoft
description: "Découvrez comment connecter tooa Hadoop basé sur Linux cluster avec SSH, puis utilisez hello Pig commande toorun Pig Latin instructions en mode interactif ou comme un traitement de la tâche."
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
ms.openlocfilehash: 1da303e239b537e6b331b1d33010058582718c90
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="run-pig-jobs-on-a-linux-based-cluster-with-hello-pig-command-ssh"></a><span data-ttu-id="6ebfe-103">Exécuter des travaux de Pig sur un cluster basé sur Linux avec hello commande de Pig (SSH)</span><span class="sxs-lookup"><span data-stu-id="6ebfe-103">Run Pig jobs on a Linux-based cluster with hello Pig command (SSH)</span></span>

[!INCLUDE [pig-selector](../../includes/hdinsight-selector-use-pig.md)]

<span data-ttu-id="6ebfe-104">Découvrez comment toointeractively exécuter des travaux de Pig à partir d’un cluster de HDInsight de tooyour de connexion SSH.</span><span class="sxs-lookup"><span data-stu-id="6ebfe-104">Learn how toointeractively run Pig jobs from an SSH connection tooyour HDInsight cluster.</span></span> <span data-ttu-id="6ebfe-105">Hello langage de programmation Pig Latin permet des transformations toodescribe toohello appliqué d’entrée données tooproduce hello souhaité sortie.</span><span class="sxs-lookup"><span data-stu-id="6ebfe-105">hello Pig Latin programming language allows you toodescribe transformations that are applied toohello input data tooproduce hello desired output.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6ebfe-106">Hello étapes décrites dans ce document nécessitent un cluster HDInsight de basés sur Linux.</span><span class="sxs-lookup"><span data-stu-id="6ebfe-106">hello steps in this document require a Linux-based HDInsight cluster.</span></span> <span data-ttu-id="6ebfe-107">Linux est hello seul système d’exploitation utilisé sur HDInsight version 3.4 ou supérieure.</span><span class="sxs-lookup"><span data-stu-id="6ebfe-107">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="6ebfe-108">Pour plus d’informations, consultez [Suppression de HDInsight sous Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="6ebfe-108">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <span data-ttu-id="6ebfe-109"><a id="ssh"></a>Connexion avec SSH</span><span class="sxs-lookup"><span data-stu-id="6ebfe-109"><a id="ssh"></a>Connect with SSH</span></span>

<span data-ttu-id="6ebfe-110">Utiliser SSH tooconnect tooyour HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="6ebfe-110">Use SSH tooconnect tooyour HDInsight cluster.</span></span> <span data-ttu-id="6ebfe-111">exemple Hello connecte cluster tooa nommé **myhdinsight** en tant que compte hello nommé **sshuser**:</span><span class="sxs-lookup"><span data-stu-id="6ebfe-111">hello following example connects tooa cluster named **myhdinsight** as hello account named **sshuser**:</span></span>

    ssh sshuser@myhdinsight-ssh.azurehdinsight.net

<span data-ttu-id="6ebfe-112">**Si vous avez fourni une clé de certificat pour l’authentification SSH** lorsque vous avez créé le cluster HDInsight de hello, vous devrez peut-être l’emplacement de hello toospecify de clé privée de hello sur votre système client.</span><span class="sxs-lookup"><span data-stu-id="6ebfe-112">**If you provided a certificate key for SSH authentication** when you created hello HDInsight cluster, you may need toospecify hello location of hello private key on your client system.</span></span>

    ssh sshuser@myhdinsight-ssh.azurehdinsight.net -i ~/mykey.key

<span data-ttu-id="6ebfe-113">**Si vous avez fourni un mot de passe pour l’authentification SSH** lorsque vous avez créé le cluster HDInsight de hello, fournir un mot de passe hello lorsque vous y êtes invité.</span><span class="sxs-lookup"><span data-stu-id="6ebfe-113">**If you provided a password for SSH authentication** when you created hello HDInsight cluster, provide hello password when prompted.</span></span>

<span data-ttu-id="6ebfe-114">Pour en savoir plus sur l’utilisation de SSH avec HDInsight, voir [Utilisation de SSH avec HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="6ebfe-114">For more information on using SSH with HDInsight, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

## <span data-ttu-id="6ebfe-115"><a id="pig"></a>Utilisez la commande de Pig hello</span><span class="sxs-lookup"><span data-stu-id="6ebfe-115"><a id="pig"></a>Use hello Pig command</span></span>

1. <span data-ttu-id="6ebfe-116">Une fois connecté, démarrez hello Pig interface de ligne de commande (CLI) à l’aide de hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="6ebfe-116">Once connected, start hello Pig command-line interface (CLI) by using hello following command:</span></span>

        pig

    <span data-ttu-id="6ebfe-117">Après quelques instants, vous devriez voir une invite `grunt>` .</span><span class="sxs-lookup"><span data-stu-id="6ebfe-117">After a moment, you should see a `grunt>` prompt.</span></span>

2. <span data-ttu-id="6ebfe-118">Entrez hello après l’instruction :</span><span class="sxs-lookup"><span data-stu-id="6ebfe-118">Enter hello following statement:</span></span>

        LOGS = LOAD '/example/data/sample.log';

    <span data-ttu-id="6ebfe-119">Cette commande charge contenu hello du fichier d’exemple.log hello dans les journaux.</span><span class="sxs-lookup"><span data-stu-id="6ebfe-119">This command loads hello contents of hello sample.log file into LOGS.</span></span> <span data-ttu-id="6ebfe-120">Vous pouvez afficher le contenu hello du fichier de hello à l’aide de hello après l’instruction :</span><span class="sxs-lookup"><span data-stu-id="6ebfe-120">You can view hello contents of hello file by using hello following statement:</span></span>

        DUMP LOGS;

3. <span data-ttu-id="6ebfe-121">Transformez ensuite les données de salutation en appliquant un niveau de journalisation de hello uniquement tooextract expression régulière à partir de chaque enregistrement à l’aide de hello après l’instruction :</span><span class="sxs-lookup"><span data-stu-id="6ebfe-121">Next, transform hello data by applying a regular expression tooextract only hello logging level from each record by using hello following statement:</span></span>

        LEVELS = foreach LOGS generate REGEX_EXTRACT($0, '(TRACE|DEBUG|INFO|WARN|ERROR|FATAL)', 1)  as LOGLEVEL;

    <span data-ttu-id="6ebfe-122">Vous pouvez utiliser **DUMP** tooview les données de salutation après la transformation de hello.</span><span class="sxs-lookup"><span data-stu-id="6ebfe-122">You can use **DUMP** tooview hello data after hello transformation.</span></span> <span data-ttu-id="6ebfe-123">Dans ce cas, utilisez `DUMP LEVELS;`.</span><span class="sxs-lookup"><span data-stu-id="6ebfe-123">In this case, use `DUMP LEVELS;`.</span></span>

4. <span data-ttu-id="6ebfe-124">Poursuivre l’application de transformations à l’aide des instructions de hello Bonjour tableau suivant :</span><span class="sxs-lookup"><span data-stu-id="6ebfe-124">Continue applying transformations by using hello statements in hello following table:</span></span>

    | <span data-ttu-id="6ebfe-125">Instruction Pig Latin</span><span class="sxs-lookup"><span data-stu-id="6ebfe-125">Pig Latin statement</span></span> | <span data-ttu-id="6ebfe-126">Les instruction hello</span><span class="sxs-lookup"><span data-stu-id="6ebfe-126">What hello statement does</span></span> |
    | ---- | ---- |
    | `FILTEREDLEVELS = FILTER LEVELS by LOGLEVEL is not null;` | <span data-ttu-id="6ebfe-127">Supprime les lignes qui contiennent une valeur null pour le niveau de journal hello et stocke les résultats hello dans `FILTEREDLEVELS`.</span><span class="sxs-lookup"><span data-stu-id="6ebfe-127">Removes rows that contain a null value for hello log level and stores hello results into `FILTEREDLEVELS`.</span></span> |
    | `GROUPEDLEVELS = GROUP FILTEREDLEVELS by LOGLEVEL;` | <span data-ttu-id="6ebfe-128">Hello de groupes de lignes par niveau de journal et stocke les résultats de hello dans `GROUPEDLEVELS`.</span><span class="sxs-lookup"><span data-stu-id="6ebfe-128">Groups hello rows by log level and stores hello results into `GROUPEDLEVELS`.</span></span> |
    | `FREQUENCIES = foreach GROUPEDLEVELS generate group as LOGLEVEL, COUNT(FILTEREDLEVELS.LOGLEVEL) as COUNT;` | <span data-ttu-id="6ebfe-129">Crée un jeu de données qui contient chaque valeur unique au niveau journal et le nombre de fois où elle se produit.</span><span class="sxs-lookup"><span data-stu-id="6ebfe-129">Creates a set of data that contains each unique log level value and how many times it occurs.</span></span> <span data-ttu-id="6ebfe-130">jeu de données Hello est stocké dans `FREQUENCIES`.</span><span class="sxs-lookup"><span data-stu-id="6ebfe-130">hello data set is stored into `FREQUENCIES`.</span></span> |
    | `RESULT = order FREQUENCIES by COUNT desc;` | <span data-ttu-id="6ebfe-131">Trie les niveaux de journalisation hello par nombre (ordre décroissant) et le stocke dans `RESULT`.</span><span class="sxs-lookup"><span data-stu-id="6ebfe-131">Orders hello log levels by count (descending) and stores into `RESULT`.</span></span> |

    > [!TIP]
    > <span data-ttu-id="6ebfe-132">Utilisez `DUMP` résultat de hello tooview de transformation hello après chaque étape.</span><span class="sxs-lookup"><span data-stu-id="6ebfe-132">Use `DUMP` tooview hello result of hello transformation after each step.</span></span>

5. <span data-ttu-id="6ebfe-133">Vous pouvez également enregistrer les résultats de hello d’une transformation à l’aide de hello `STORE` instruction.</span><span class="sxs-lookup"><span data-stu-id="6ebfe-133">You can also save hello results of a transformation by using hello `STORE` statement.</span></span> <span data-ttu-id="6ebfe-134">Par exemple, après l’instruction de hello enregistre hello `RESULT` toohello `/example/data/pigout` répertoire sur le stockage par défaut hello pour votre cluster :</span><span class="sxs-lookup"><span data-stu-id="6ebfe-134">For example, hello following statement saves hello `RESULT` toohello `/example/data/pigout` directory on hello default storage for your cluster:</span></span>

        STORE RESULT into '/example/data/pigout';

   > [!NOTE]
   > <span data-ttu-id="6ebfe-135">les données de salutation sont stockées dans le répertoire spécifié de hello dans les fichiers nommés `part-nnnnn`.</span><span class="sxs-lookup"><span data-stu-id="6ebfe-135">hello data is stored in hello specified directory in files named `part-nnnnn`.</span></span> <span data-ttu-id="6ebfe-136">Si le répertoire de hello existe déjà, vous recevez une erreur.</span><span class="sxs-lookup"><span data-stu-id="6ebfe-136">If hello directory already exists, you receive an error.</span></span>

6. <span data-ttu-id="6ebfe-137">tooexit hello des grunt à l’invite, entrez hello après l’instruction :</span><span class="sxs-lookup"><span data-stu-id="6ebfe-137">tooexit hello grunt prompt, enter hello following statement:</span></span>

        QUIT;

### <a name="pig-latin-batch-files"></a><span data-ttu-id="6ebfe-138">Fichiers de commandes Pig Latin</span><span class="sxs-lookup"><span data-stu-id="6ebfe-138">Pig Latin batch files</span></span>

<span data-ttu-id="6ebfe-139">Vous pouvez également utiliser hello Pig commande toorun Latin Pig contenus dans un fichier.</span><span class="sxs-lookup"><span data-stu-id="6ebfe-139">You can also use hello Pig command toorun Pig Latin contained in a file.</span></span>

1. <span data-ttu-id="6ebfe-140">Après avoir quitté l’invite de grunt hello, suivant de hello utilisez commande toopipe STDIN dans un fichier nommé `pigbatch.pig`.</span><span class="sxs-lookup"><span data-stu-id="6ebfe-140">After exiting hello grunt prompt, use hello following command toopipe STDIN into a file named `pigbatch.pig`.</span></span> <span data-ttu-id="6ebfe-141">Ce fichier est créé dans le répertoire de base hello pour hello compte d’utilisateur SSH.</span><span class="sxs-lookup"><span data-stu-id="6ebfe-141">This file is created in hello home directory for hello SSH user account.</span></span>

        cat > ~/pigbatch.pig

2. <span data-ttu-id="6ebfe-142">Tapez ou collez hello lignes suivantes, puis utilisez Ctrl + D, une fois.</span><span class="sxs-lookup"><span data-stu-id="6ebfe-142">Type or paste hello following lines, and then use Ctrl+D when finished.</span></span>

        LOGS = LOAD '/example/data/sample.log';
        LEVELS = foreach LOGS generate REGEX_EXTRACT($0, '(TRACE|DEBUG|INFO|WARN|ERROR|FATAL)', 1)  as LOGLEVEL;
        FILTEREDLEVELS = FILTER LEVELS by LOGLEVEL is not null;
        GROUPEDLEVELS = GROUP FILTEREDLEVELS by LOGLEVEL;
        FREQUENCIES = foreach GROUPEDLEVELS generate group as LOGLEVEL, COUNT(FILTEREDLEVELS.LOGLEVEL) as COUNT;
        RESULT = order FREQUENCIES by COUNT desc;
        DUMP RESULT;

3. <span data-ttu-id="6ebfe-143">Suivant de hello utilisez commande toorun hello `pigbatch.pig` fichier à l’aide des commandes de Pig hello.</span><span class="sxs-lookup"><span data-stu-id="6ebfe-143">Use hello following command toorun hello `pigbatch.pig` file by using hello Pig command.</span></span>

        pig ~/pigbatch.pig

    <span data-ttu-id="6ebfe-144">Une fois le traitement par lots hello se termine, vous voyez hello suivant de sortie :</span><span class="sxs-lookup"><span data-stu-id="6ebfe-144">Once hello batch job finishes, you see hello following output:</span></span>

        (TRACE,816)
        (DEBUG,434)
        (INFO,96)
        (WARN,11)
        (ERROR,6)
        (FATAL,2)


## <span data-ttu-id="6ebfe-145"><a id="nextsteps"></a>Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="6ebfe-145"><a id="nextsteps"></a>Next steps</span></span>

<span data-ttu-id="6ebfe-146">Pour obtenir des informations générales sur Pig dans HDInsight, consultez hello suivant du document :</span><span class="sxs-lookup"><span data-stu-id="6ebfe-146">For general information on Pig in HDInsight, see hello following document:</span></span>

* [<span data-ttu-id="6ebfe-147">Utilisation de Pig avec Hadoop sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="6ebfe-147">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)

<span data-ttu-id="6ebfe-148">Pour plus d’informations sur les autres façons de toowork avec Hadoop dans HDInsight, consultez hello suivant des documents :</span><span class="sxs-lookup"><span data-stu-id="6ebfe-148">For more information on other ways toowork with Hadoop on HDInsight, see hello following documents:</span></span>

* [<span data-ttu-id="6ebfe-149">Utilisation de Hive avec Hadoop sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="6ebfe-149">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="6ebfe-150">Utilisation de MapReduce avec Hadoop sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="6ebfe-150">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)
