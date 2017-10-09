---
title: aaaUse Hadoop Pig avec PowerShell dans HDInsight - Azure | Documents Microsoft
description: "Découvrez comment tooa de travaux toosubmit Pig Hadoop cluster sur HDInsight à l’aide d’Azure PowerShell."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 737089c1-b494-4387-9def-7b4dac3be532
ms.service: hdinsight
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/16/2017
ms.author: larryfr
ms.custom: H1Hack27Feb2017,hdinsightactive
ms.openlocfilehash: 771617df203011eaec715a0dba6f5014a42877f3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-powershell-toorun-pig-jobs-with-hdinsight"></a><span data-ttu-id="97415-103">Utiliser des travaux de Azure PowerShell toorun Pig hdinsight</span><span class="sxs-lookup"><span data-stu-id="97415-103">Use Azure PowerShell toorun Pig jobs with HDInsight</span></span>

[!INCLUDE [pig-selector](../../includes/hdinsight-selector-use-pig.md)]

<span data-ttu-id="97415-104">Ce document fournit un exemple d’utilisation d’Azure PowerShell toosubmit Pig travaux tooa Hadoop sur le cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="97415-104">This document provides an example of using Azure PowerShell toosubmit Pig jobs tooa Hadoop on HDInsight cluster.</span></span> <span data-ttu-id="97415-105">Pig vous permet des tâches MapReduce toowrite à l’aide d’un langage (Pig Latin) qui modélise les transformations de données, plutôt que mapper et réduire des fonctions.</span><span class="sxs-lookup"><span data-stu-id="97415-105">Pig allows you toowrite MapReduce jobs by using a language (Pig Latin) that models data transformations, rather than map and reduce functions.</span></span>

> [!NOTE]
> <span data-ttu-id="97415-106">Ce document ne fournit pas une description détaillée de ce que font les instructions de Pig Latin hello utilisées dans les exemples hello.</span><span class="sxs-lookup"><span data-stu-id="97415-106">This document does not provide a detailed description of what hello Pig Latin statements used in hello examples do.</span></span> <span data-ttu-id="97415-107">Pour plus d’informations sur hello Latin Pig utilisé dans cet exemple, consultez [utilisez Pig avec Hadoop dans HDInsight](hdinsight-use-pig.md).</span><span class="sxs-lookup"><span data-stu-id="97415-107">For information about hello Pig Latin used in this example, see [Use Pig with Hadoop on HDInsight](hdinsight-use-pig.md).</span></span>

## <span data-ttu-id="97415-108"><a id="prereq"></a>Configuration requise</span><span class="sxs-lookup"><span data-stu-id="97415-108"><a id="prereq"></a>Prerequisites</span></span>

* <span data-ttu-id="97415-109">**Un cluster Azure HDInsight**</span><span class="sxs-lookup"><span data-stu-id="97415-109">**An Azure HDInsight cluster**</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="97415-110">Linux est hello seul système d’exploitation utilisé sur HDInsight version 3.4 ou supérieure.</span><span class="sxs-lookup"><span data-stu-id="97415-110">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="97415-111">Pour plus d’informations, consultez [Suppression de HDInsight sous Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="97415-111">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="97415-112">**Un poste de travail sur lequel est installé Azure PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="97415-112">**A workstation with Azure PowerShell**.</span></span>

[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell.md)]

## <span data-ttu-id="97415-113"><a id="powershell"></a>Exécution de tâches Pig avec PowerShell</span><span class="sxs-lookup"><span data-stu-id="97415-113"><a id="powershell"></a>Run Pig jobs using PowerShell</span></span>

<span data-ttu-id="97415-114">Azure PowerShell fournit *applets de commande* qui permettent de travaux de tooremotely exécution Pig dans HDInsight.</span><span class="sxs-lookup"><span data-stu-id="97415-114">Azure PowerShell provides *cmdlets* that allow you tooremotely run Pig jobs on HDInsight.</span></span> <span data-ttu-id="97415-115">En interne, PowerShell utilise des appels REST trop[WebHCat](https://cwiki.apache.org/confluence/display/Hive/WebHCat) en cours d’exécution sur le cluster HDInsight de hello.</span><span class="sxs-lookup"><span data-stu-id="97415-115">Internally, PowerShell uses REST calls too[WebHCat](https://cwiki.apache.org/confluence/display/Hive/WebHCat) running on hello HDInsight cluster.</span></span>

<span data-ttu-id="97415-116">applets de commande suivantes Hello sont utilisées lors de l’exécution des travaux de Pig sur un cluster HDInsight à distance :</span><span class="sxs-lookup"><span data-stu-id="97415-116">hello following cmdlets are used when running Pig jobs on a remote HDInsight cluster:</span></span>

* <span data-ttu-id="97415-117">**Connexion-AzureRmAccount**: authentifie Azure PowerShell tooyour abonnement Azure</span><span class="sxs-lookup"><span data-stu-id="97415-117">**Login-AzureRmAccount**: Authenticates Azure PowerShell tooyour Azure Subscription</span></span>
* <span data-ttu-id="97415-118">**Nouveau-AzureRmHDInsightPigJobDefinition**: crée un *définition de travail* à l’aide de hello spécifié Pig Latin instructions</span><span class="sxs-lookup"><span data-stu-id="97415-118">**New-AzureRmHDInsightPigJobDefinition**: Creates a *job definition* by using hello specified Pig Latin statements</span></span>
* <span data-ttu-id="97415-119">**Start-AzureRmHDInsightJob**: envoie tooHDInsight de définition de tâche hello, démarre le travail de hello et retourne un *travail* objet qui peut être l’état de hello toocheck utilisés du travail de hello</span><span class="sxs-lookup"><span data-stu-id="97415-119">**Start-AzureRmHDInsightJob**: Sends hello job definition tooHDInsight, starts hello job, and returns a *job* object that can be used toocheck hello status of hello job</span></span>
* <span data-ttu-id="97415-120">**Wait-AzureRmHDInsightJob**: utilise hello objet toocheck hello statut de tâche de travail de hello.</span><span class="sxs-lookup"><span data-stu-id="97415-120">**Wait-AzureRmHDInsightJob**: Uses hello job object toocheck hello status of hello job.</span></span> <span data-ttu-id="97415-121">Il attend hello est terminée, ou délai d’attente hello a été dépassé.</span><span class="sxs-lookup"><span data-stu-id="97415-121">It waits until hello job has completed, or hello wait time has been exceeded.</span></span>
* <span data-ttu-id="97415-122">**Get-AzureRmHDInsightJobOutput**: utilisé la sortie de hello tooretrieve du travail de hello</span><span class="sxs-lookup"><span data-stu-id="97415-122">**Get-AzureRmHDInsightJobOutput**: Used tooretrieve hello output of hello job</span></span>

<span data-ttu-id="97415-123">Hello étapes suivantes montrent comment toouse ces applets de commande de toorun une tâche sur votre cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="97415-123">hello following steps demonstrate how toouse these cmdlets toorun a job on your HDInsight cluster.</span></span>

1. <span data-ttu-id="97415-124">À l’aide d’un éditeur, enregistrer hello suivant le code en tant que **pigjob.ps1**.</span><span class="sxs-lookup"><span data-stu-id="97415-124">Using an editor, save hello following code as **pigjob.ps1**.</span></span>

    [!code-powershell[main](../../powershell_scripts/hdinsight/use-pig/use-pig.ps1?range=5-51)]

1. <span data-ttu-id="97415-125">Ouvrez une invite de commandes Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="97415-125">Open a new Windows PowerShell command prompt.</span></span> <span data-ttu-id="97415-126">Modifier l’emplacement de toohello répertoires de hello **pigjob.ps1** de fichier, puis utilisez hello commande toorun hello script suivant :</span><span class="sxs-lookup"><span data-stu-id="97415-126">Change directories toohello location of hello **pigjob.ps1** file, then use hello following command toorun hello script:</span></span>

        .\pigjob.ps1

    <span data-ttu-id="97415-127">Vous êtes invité à toolog dans tooyour abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="97415-127">You are prompted toolog in tooyour Azure subscription.</span></span> <span data-ttu-id="97415-128">Ensuite, vous êtes invité à entrer nom du compte hello HTTPs/Admin et le mot de passe pour le cluster HDInsight de hello.</span><span class="sxs-lookup"><span data-stu-id="97415-128">Then, you are asked for hello HTTPs/Admin account name and password for hello HDInsight cluster.</span></span>

2. <span data-ttu-id="97415-129">Lors de la tâche de hello est terminée, elle doit retourner toohello similaire à informations suivant le texte :</span><span class="sxs-lookup"><span data-stu-id="97415-129">When hello job completes, it should return information similar toohello following text:</span></span>

        Start hello Pig job ...
        Wait for hello Pig job toocomplete ...
        Display hello standard output ...
        (TRACE,816)
        (DEBUG,434)
        (INFO,96)
        (WARN,11)
        (ERROR,6)
        (FATAL,2)

## <span data-ttu-id="97415-130"><a id="troubleshooting"></a>Résolution des problèmes</span><span class="sxs-lookup"><span data-stu-id="97415-130"><a id="troubleshooting"></a>Troubleshooting</span></span>

<span data-ttu-id="97415-131">Si aucune information n’est retournée lorsque hello travail se termine, une erreur peut être survenu lors du traitement.</span><span class="sxs-lookup"><span data-stu-id="97415-131">If no information is returned when hello job completes, an error may have occurred during processing.</span></span> <span data-ttu-id="97415-132">informations sur l’erreur tooview à cette tâche, ajouter hello suivant la fin de la commande toohello Hello **pigjob.ps1** de fichiers, enregistrez-le et exécutez-le à nouveau.</span><span class="sxs-lookup"><span data-stu-id="97415-132">tooview error information for this job, add hello following command toohello end of hello **pigjob.ps1** file, save it, and then run it again.</span></span>

    # Print hello output of hello Pig job.
    Write-Host "Display hello standard error output ..." -ForegroundColor Green
    Get-AzureRmHDInsightJobOutput `
            -Clustername $clusterName `
            -JobId $pigJob.JobId `
            -HttpCredential $creds `
            -DisplayOutputType StandardError

<span data-ttu-id="97415-133">Cela retourne les informations de hello écrite tooSTDERR sur le serveur de hello lors de l’exécution du travail de hello et il peut aider à déterminer la raison pour laquelle le travail de hello échoue.</span><span class="sxs-lookup"><span data-stu-id="97415-133">This returns hello information that was written tooSTDERR on hello server when you ran hello job, and it may help determine why hello job is failing.</span></span>

## <span data-ttu-id="97415-134"><a id="summary"></a>Résumé</span><span class="sxs-lookup"><span data-stu-id="97415-134"><a id="summary"></a>Summary</span></span>
<span data-ttu-id="97415-135">Comme vous pouvez le voir, Azure PowerShell fournit un moyen simple de toorun les travaux Pig sur un cluster HDInsight, surveiller le statut de tâche hello et récupérer hello sortie.</span><span class="sxs-lookup"><span data-stu-id="97415-135">As you can see, Azure PowerShell provides an easy way toorun Pig jobs on an HDInsight cluster, monitor hello job status, and retrieve hello output.</span></span>

## <span data-ttu-id="97415-136"><a id="nextsteps"></a>Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="97415-136"><a id="nextsteps"></a>Next steps</span></span>
<span data-ttu-id="97415-137">Pour obtenir des informations générales sur Pig dans HDInsight :</span><span class="sxs-lookup"><span data-stu-id="97415-137">For general information about Pig in HDInsight:</span></span>

* [<span data-ttu-id="97415-138">Utilisation de Pig avec Hadoop sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="97415-138">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)

<span data-ttu-id="97415-139">Pour plus d’informations sur d’autres méthodes de travail avec Hadoop sur HDInsight :</span><span class="sxs-lookup"><span data-stu-id="97415-139">For information about other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="97415-140">Utilisation de Hive avec Hadoop sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="97415-140">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="97415-141">Utilisation de MapReduce avec Hadoop sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="97415-141">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)
