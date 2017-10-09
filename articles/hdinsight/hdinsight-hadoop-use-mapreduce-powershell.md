---
title: aaaUse MapReduce et PowerShell avec Hadoop - Azure HDInsight | Documents Microsoft
description: "Découvrez comment toouse PowerShell tooremotely exécuter les tâches MapReduce avec Hadoop dans HDInsight."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 21b56d32-1785-4d44-8ae8-94467c12cfba
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/16/2017
ms.author: larryfr
ms.openlocfilehash: 59524f0e8813d4c017f92bccb2e50d4c018acf71
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="run-mapreduce-jobs-with-hadoop-on-hdinsight-using-powershell"></a><span data-ttu-id="29d66-103">Exécution à distance des travaux MapReduce avec Hadoop sur HDInsight à l’aide de PowerShell</span><span class="sxs-lookup"><span data-stu-id="29d66-103">Run MapReduce jobs with Hadoop on HDInsight using PowerShell</span></span>

[!INCLUDE [mapreduce-selector](../../includes/hdinsight-selector-use-mapreduce.md)]

<span data-ttu-id="29d66-104">Ce document fournit un exemple d’utilisation d’Azure PowerShell toorun une tâche MapReduce dans un Hadoop sur le cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="29d66-104">This document provides an example of using Azure PowerShell toorun a MapReduce job in a Hadoop on HDInsight cluster.</span></span>

## <span data-ttu-id="29d66-105"><a id="prereq"></a>Configuration requise</span><span class="sxs-lookup"><span data-stu-id="29d66-105"><a id="prereq"></a>Prerequisites</span></span>

* <span data-ttu-id="29d66-106">**Un cluster Azure HDInsight (Hadoop sur HDInsight)**</span><span class="sxs-lookup"><span data-stu-id="29d66-106">**An Azure HDInsight (Hadoop on HDInsight) cluster**</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="29d66-107">Linux est hello seul système d’exploitation utilisé sur HDInsight version 3.4 ou supérieure.</span><span class="sxs-lookup"><span data-stu-id="29d66-107">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="29d66-108">Pour plus d’informations, consultez [Suppression de HDInsight sous Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="29d66-108">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="29d66-109">**Un poste de travail sur lequel est installé Azure PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="29d66-109">**A workstation with Azure PowerShell**.</span></span>

## <span data-ttu-id="29d66-110"><a id="powershell"></a>Exécution d’une tâche MapReduce avec Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="29d66-110"><a id="powershell"></a>Run a MapReduce job using Azure PowerShell</span></span>

<span data-ttu-id="29d66-111">Azure PowerShell fournit *applets de commande* qui permettent de tooremotely exécuter les tâches MapReduce dans HDInsight.</span><span class="sxs-lookup"><span data-stu-id="29d66-111">Azure PowerShell provides *cmdlets* that allow you tooremotely run MapReduce jobs on HDInsight.</span></span> <span data-ttu-id="29d66-112">En interne, cela est accompli en utilisant des appels REST trop[WebHCat](https://cwiki.apache.org/confluence/display/Hive/WebHCat) (anciennement Templeton) en cours d’exécution hello cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="29d66-112">Internally, this is accomplished by using REST calls too[WebHCat](https://cwiki.apache.org/confluence/display/Hive/WebHCat) (formerly called Templeton) running on hello HDInsight cluster.</span></span>

<span data-ttu-id="29d66-113">applets de commande suivantes Hello sont utilisées lors de l’exécution des tâches MapReduce dans un cluster HDInsight à distance.</span><span class="sxs-lookup"><span data-stu-id="29d66-113">hello following cmdlets are used when running MapReduce jobs in a remote HDInsight cluster.</span></span>

* <span data-ttu-id="29d66-114">**Connexion-AzureRmAccount**: authentifie Azure PowerShell tooyour abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="29d66-114">**Login-AzureRmAccount**: Authenticates Azure PowerShell tooyour Azure subscription.</span></span>

* <span data-ttu-id="29d66-115">**Nouveau-AzureRmHDInsightMapReduceJobDefinition**: crée un nouveau *définition de travail* à l’aide de hello spécifié les informations MapReduce.</span><span class="sxs-lookup"><span data-stu-id="29d66-115">**New-AzureRmHDInsightMapReduceJobDefinition**: Creates a new *job definition* by using hello specified MapReduce information.</span></span>

* <span data-ttu-id="29d66-116">**Start-AzureRmHDInsightJob**: envoie tooHDInsight de définition de tâche hello, démarre le travail de hello et retourne un *travail* objet qui peut être l’état de hello toocheck utilisés du travail de hello.</span><span class="sxs-lookup"><span data-stu-id="29d66-116">**Start-AzureRmHDInsightJob**: Sends hello job definition tooHDInsight, starts hello job, and returns a *job* object that can be used toocheck hello status of hello job.</span></span>

* <span data-ttu-id="29d66-117">**Wait-AzureRmHDInsightJob**: utilise hello objet toocheck hello statut de tâche de travail de hello.</span><span class="sxs-lookup"><span data-stu-id="29d66-117">**Wait-AzureRmHDInsightJob**: Uses hello job object toocheck hello status of hello job.</span></span> <span data-ttu-id="29d66-118">Il attend hello tâche se termine ou dépasse du délai d’attente hello.</span><span class="sxs-lookup"><span data-stu-id="29d66-118">It waits until hello job completes or hello wait time is exceeded.</span></span>

* <span data-ttu-id="29d66-119">**Get-AzureRmHDInsightJobOutput**: utilisé la sortie de hello tooretrieve du travail de hello.</span><span class="sxs-lookup"><span data-stu-id="29d66-119">**Get-AzureRmHDInsightJobOutput**: Used tooretrieve hello output of hello job.</span></span>

<span data-ttu-id="29d66-120">Hello étapes suivantes montrent comment toouse ces applets de commande de toorun un travail dans votre cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="29d66-120">hello following steps demonstrate how toouse these cmdlets toorun a job in your HDInsight cluster.</span></span>

1. <span data-ttu-id="29d66-121">À l’aide d’un éditeur, enregistrer hello suivant le code en tant que **mapreducejob.ps1**.</span><span class="sxs-lookup"><span data-stu-id="29d66-121">Using an editor, save hello following code as **mapreducejob.ps1**.</span></span>

    [!code-powershell[main](../../powershell_scripts/hdinsight/use-mapreduce/use-mapreduce.ps1?range=5-69)]

2. <span data-ttu-id="29d66-122">Ouvrez une invite de commandes **Azure PowerShell** .</span><span class="sxs-lookup"><span data-stu-id="29d66-122">Open a new **Azure PowerShell** command prompt.</span></span> <span data-ttu-id="29d66-123">Modifier l’emplacement de toohello répertoires de hello **mapreducejob.ps1** de fichier, puis utilisez hello commande toorun hello script suivant :</span><span class="sxs-lookup"><span data-stu-id="29d66-123">Change directories toohello location of hello **mapreducejob.ps1** file, then use hello following command toorun hello script:</span></span>

        .\mapreducejob.ps1

    <span data-ttu-id="29d66-124">Lorsque vous exécutez le script de hello, vous êtes invité pour nom hello du cluster HDInsight de hello et nom du compte hello HTTPS/Admin et mot de passe pour le cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="29d66-124">When you run hello script, you are prompted for hello name of hello HDInsight cluster and hello HTTPS/Admin account name and password for hello cluster.</span></span> <span data-ttu-id="29d66-125">Vous pouvez également être invité à tooauthenticate tooyour abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="29d66-125">You may also be prompted tooauthenticate tooyour Azure subscription.</span></span>

3. <span data-ttu-id="29d66-126">Lors de la tâche de hello est terminée, vous recevez toohello similaire de sortie suivant du texte :</span><span class="sxs-lookup"><span data-stu-id="29d66-126">When hello job completes, you receive output similar toohello following text:</span></span>

        Cluster         : CLUSTERNAME
        ExitCode        : 0
        Name            : wordcount
        PercentComplete : map 100% reduce 100%
        Query           :
        State           : Completed
        StatusDirectory : f1ed2028-afe8-402f-a24b-13cc17858097
        SubmissionTime  : 12/5/2014 8:34:09 PM
        JobId           : job_1415949758166_0071

    <span data-ttu-id="29d66-127">Cette sortie indique que le travail hello s’est terminée avec succès.</span><span class="sxs-lookup"><span data-stu-id="29d66-127">This output indicates that hello job completed successfully.</span></span>

    > [!NOTE]
    > <span data-ttu-id="29d66-128">Si hello **ExitCode** est une valeur différente de 0, consultez [dépannage](#troubleshooting).</span><span class="sxs-lookup"><span data-stu-id="29d66-128">If hello **ExitCode** is a value other than 0, see [Troubleshooting](#troubleshooting).</span></span>

    <span data-ttu-id="29d66-129">Cet exemple stocke également hello téléchargé les fichiers tooan **output.txt** fichier hello dans répertoire dans lequel vous exécutez le script hello.</span><span class="sxs-lookup"><span data-stu-id="29d66-129">This example also stores hello downloaded files tooan **output.txt** file in hello directory that you run hello script from.</span></span>

### <a name="view-output"></a><span data-ttu-id="29d66-130">Affichage de la sortie</span><span class="sxs-lookup"><span data-stu-id="29d66-130">View output</span></span>

<span data-ttu-id="29d66-131">Ouvrez hello **output.txt** fichier dans un Bonjour de toosee de l’éditeur de texte les mots et le nombre obtenu par la tâche de hello.</span><span class="sxs-lookup"><span data-stu-id="29d66-131">Open hello **output.txt** file in a text editor toosee hello words and counts produced by hello job.</span></span>

> [!NOTE]
> <span data-ttu-id="29d66-132">Hello des fichiers de sortie d’une tâche MapReduce sont immuables.</span><span class="sxs-lookup"><span data-stu-id="29d66-132">hello output files of a MapReduce job are immutable.</span></span> <span data-ttu-id="29d66-133">Si vous exécutez à nouveau cet exemple, vous devez donc nom de hello toochange hello du fichier de sortie.</span><span class="sxs-lookup"><span data-stu-id="29d66-133">So if you rerun this sample, you need toochange hello name of hello output file.</span></span>

## <span data-ttu-id="29d66-134"><a id="troubleshooting"></a>Résolution des problèmes</span><span class="sxs-lookup"><span data-stu-id="29d66-134"><a id="troubleshooting"></a>Troubleshooting</span></span>

<span data-ttu-id="29d66-135">Si aucune information n’est retournée lorsque hello travail se termine, une erreur peut être survenu lors du traitement.</span><span class="sxs-lookup"><span data-stu-id="29d66-135">If no information is returned when hello job completes, an error may have occurred during processing.</span></span> <span data-ttu-id="29d66-136">informations sur l’erreur tooview à cette tâche, ajouter hello suivant la fin de la commande toohello Hello **mapreducejob.ps1** de fichiers, enregistrez-le et exécutez-le à nouveau.</span><span class="sxs-lookup"><span data-stu-id="29d66-136">tooview error information for this job, add hello following command toohello end of hello **mapreducejob.ps1** file, save it, and then run it again.</span></span>

```powershell
# Print hello output of hello WordCount job.
Write-Host "Display hello standard output ..." -ForegroundColor Green
Get-AzureRmHDInsightJobOutput `
        -Clustername $clusterName `
        -JobId $wordCountJob.JobId `
        -HttpCredential $creds `
        -DisplayOutputType StandardError
```

<span data-ttu-id="29d66-137">Cette applet de commande retourne des informations de hello écrite tooSTDERR sur le serveur de hello lors de l’exécution du travail de hello et il peut aider à déterminer la raison pour laquelle le travail de hello échoue.</span><span class="sxs-lookup"><span data-stu-id="29d66-137">This cmdlet returns hello information that was written tooSTDERR on hello server when you ran hello job, and it may help determine why hello job is failing.</span></span>

## <span data-ttu-id="29d66-138"><a id="summary"></a>Résumé</span><span class="sxs-lookup"><span data-stu-id="29d66-138"><a id="summary"></a>Summary</span></span>

<span data-ttu-id="29d66-139">Comme vous pouvez le voir, Azure PowerShell fournit un moyen simple de toorun tâches MapReduce sur un cluster HDInsight, surveiller le statut de tâche hello et récupérer hello sortie.</span><span class="sxs-lookup"><span data-stu-id="29d66-139">As you can see, Azure PowerShell provides an easy way toorun MapReduce jobs on an HDInsight cluster, monitor hello job status, and retrieve hello output.</span></span>

## <span data-ttu-id="29d66-140"><a id="nextsteps"></a>Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="29d66-140"><a id="nextsteps"></a>Next steps</span></span>

<span data-ttu-id="29d66-141">Pour obtenir des informations générales sur les tâches MapReduce dans HDInsight :</span><span class="sxs-lookup"><span data-stu-id="29d66-141">For general information about MapReduce jobs in HDInsight:</span></span>

* [<span data-ttu-id="29d66-142">Utilisation de MapReduce dans Hadoop HDInsight</span><span class="sxs-lookup"><span data-stu-id="29d66-142">Use MapReduce on HDInsight Hadoop</span></span>](hdinsight-use-mapreduce.md)

<span data-ttu-id="29d66-143">Pour plus d’informations sur d’autres méthodes de travail avec Hadoop sur HDInsight :</span><span class="sxs-lookup"><span data-stu-id="29d66-143">For information about other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="29d66-144">Utilisation de Hive avec Hadoop sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="29d66-144">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="29d66-145">Utilisation de Pig avec Hadoop sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="29d66-145">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)
