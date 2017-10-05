---
title: "Découvrir le workflow PowerShell pour Azure Automation | Microsoft Docs"
description: "Cet article est une rapide leçon expliquant aux auteurs familiarisés avec PowerShell les différences spécifiques entre PowerShell et un workflow PowerShell et les concepts applicables aux runbooks Automation."
services: automation
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: tysonn
ms.assetid: 84bf133e-5343-4e0e-8d6c-bb14304a70db
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/21/2017
ms.author: magoedte;bwren
ms.openlocfilehash: 4de812c7f863e42a6ed10c2312d61b8377e06431
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="learning-key-windows-powershell-workflow-concepts-for-automation-runbooks"></a><span data-ttu-id="1e133-103">Découvrir les principaux concepts de workflow Windows PowerShell pour les runbooks Automation</span><span class="sxs-lookup"><span data-stu-id="1e133-103">Learning key Windows PowerShell Workflow concepts for Automation runbooks</span></span> 
<span data-ttu-id="1e133-104">Les Runbooks d'Azure Automation sont implémentés en tant que workflows Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1e133-104">Runbooks in Azure Automation are implemented as Windows PowerShell Workflows.</span></span>  <span data-ttu-id="1e133-105">Un workflow Windows PowerShell est similaire à un script Windows PowerShell, mais il présente des différences significatives qui peuvent être déconcertantes pour un nouvel utilisateur.</span><span class="sxs-lookup"><span data-stu-id="1e133-105">A Windows PowerShell Workflow is similar to a Windows PowerShell script but has some significant differences that can be confusing to a new user.</span></span>  <span data-ttu-id="1e133-106">Bien que cet article soit destiné à vous aider à écrire des runbooks à l’aide de workflow PowerShell, nous vous recommandons d’écrire des runbooks à l’aide de PowerShell, sauf si vous avez besoin de points de contrôle.</span><span class="sxs-lookup"><span data-stu-id="1e133-106">While this article is intended to help you write runbooks using PowerShell workflow, we recommend you write runbooks using PowerShell unless you need checkpoints.</span></span>  <span data-ttu-id="1e133-107">Il existe plusieurs différences de syntaxe lors de la création de runbooks de workflow PowerShell et ces différences nécessitent un peu plus de travail pour l’écriture de workflows efficaces.</span><span class="sxs-lookup"><span data-stu-id="1e133-107">There are several syntax differences when authoring PowerShell Workflow runbooks and these differences require a bit more work to write effective workflows.</span></span>  

<span data-ttu-id="1e133-108">Un workflow est une séquence d'étapes liées et programmées qui permet d'effectuer des tâches longues ou nécessitant la coordination de plusieurs phases entre plusieurs appareils ou nœuds gérés.</span><span class="sxs-lookup"><span data-stu-id="1e133-108">A workflow is a sequence of programmed, connected steps that perform long-running tasks or require the coordination of multiple steps across multiple devices or managed nodes.</span></span> <span data-ttu-id="1e133-109">Les avantages d'un workflow par rapport à un script normal incluent la possibilité d'exécuter simultanément une action sur plusieurs appareils et de récupérer automatiquement après une défaillance.</span><span class="sxs-lookup"><span data-stu-id="1e133-109">The benefits of a workflow over a normal script include the ability to simultaneously perform an action against multiple devices and the ability to automatically recover from failures.</span></span> <span data-ttu-id="1e133-110">Un workflow Windows PowerShell est un script Windows PowerShell qui utilise Windows Workflow Foundation.</span><span class="sxs-lookup"><span data-stu-id="1e133-110">A Windows PowerShell Workflow is a Windows PowerShell script that uses Windows Workflow Foundation.</span></span> <span data-ttu-id="1e133-111">Le workflow est écrit avec la syntaxe Windows PowerShell et lancé par Windows PowerShell, mais il est traité par Windows Workflow Foundation.</span><span class="sxs-lookup"><span data-stu-id="1e133-111">While the workflow is written with Windows PowerShell syntax and launched by Windows PowerShell, it is processed by Windows Workflow Foundation.</span></span>

<span data-ttu-id="1e133-112">Plus d'informations sur les rubriques de cet article, consultez [Présentation du workflow Windows PowerShell](http://technet.microsoft.com/library/jj134242.aspx).</span><span class="sxs-lookup"><span data-stu-id="1e133-112">For complete details on the topics in this article, see [Getting Started with Windows PowerShell Workflow](http://technet.microsoft.com/library/jj134242.aspx).</span></span>

## <a name="basic-structure-of-a-workflow"></a><span data-ttu-id="1e133-113">Structure de base d'un workflow</span><span class="sxs-lookup"><span data-stu-id="1e133-113">Basic structure of a workflow</span></span>
<span data-ttu-id="1e133-114">La première étape de la conversion d'un script PowerShell en un workflow PowerShell consiste à y intégrer le mot clé **Workflow** .</span><span class="sxs-lookup"><span data-stu-id="1e133-114">The first step to converting a PowerShell script to a PowerShell workflow is enclosing it with the **Workflow** keyword.</span></span>  <span data-ttu-id="1e133-115">Un workflow commence par le mot clé **Workflow** suivi du corps du script entre accolades.</span><span class="sxs-lookup"><span data-stu-id="1e133-115">A workflow starts with the **Workflow** keyword followed by the body of the script enclosed in braces.</span></span> <span data-ttu-id="1e133-116">Le nom du workflow suit le mot clé **Workflow**, comme illustré dans la syntaxe suivante.</span><span class="sxs-lookup"><span data-stu-id="1e133-116">The name of the workflow follows the **Workflow** keyword as shown in the following syntax:</span></span>

    Workflow Test-Workflow
    {
       <Commands>
    }

<span data-ttu-id="1e133-117">Le nom du workflow doit correspondre au nom du Runbook Automation.</span><span class="sxs-lookup"><span data-stu-id="1e133-117">The name of the workflow must match the name of the Automation runbook.</span></span> <span data-ttu-id="1e133-118">Si le Runbook est importé, le nom de fichier doit correspondre au nom du workflow et se terminer par *.ps1*.</span><span class="sxs-lookup"><span data-stu-id="1e133-118">If the runbook is being imported, then the filename must match the workflow name and must end in *.ps1*.</span></span>

<span data-ttu-id="1e133-119">Pour ajouter des paramètres au workflow, utilisez le mot clé **Param** , comme pour un script.</span><span class="sxs-lookup"><span data-stu-id="1e133-119">To add parameters to the workflow, use the **Param** keyword just as you would to a script.</span></span>

## <a name="code-changes"></a><span data-ttu-id="1e133-120">Modifications du code</span><span class="sxs-lookup"><span data-stu-id="1e133-120">Code changes</span></span>
<span data-ttu-id="1e133-121">Le code d'un workflow PowerShell est quasiment identique au code d'un script PowerShell, à l'exception de quelques modifications importantes.</span><span class="sxs-lookup"><span data-stu-id="1e133-121">PowerShell workflow code looks almost identical to PowerShell script code except for a few significant changes.</span></span>  <span data-ttu-id="1e133-122">Les sections suivantes décrivent les modifications que vous devez apporter à un script PowerShell pour l’exécuter dans un workflow.</span><span class="sxs-lookup"><span data-stu-id="1e133-122">The following sections describe changes that you need to make to a PowerShell script for it to run in a workflow.</span></span>

### <a name="activities"></a><span data-ttu-id="1e133-123">Activités</span><span class="sxs-lookup"><span data-stu-id="1e133-123">Activities</span></span>
<span data-ttu-id="1e133-124">Une activité est une tâche spécifique dans un workflow.</span><span class="sxs-lookup"><span data-stu-id="1e133-124">An activity is a specific task in a workflow.</span></span> <span data-ttu-id="1e133-125">Tout comme un script se compose d'une ou de plusieurs commandes, un workflow se compose d'une ou de plusieurs activités exécutées en séquence.</span><span class="sxs-lookup"><span data-stu-id="1e133-125">Just as a script is composed of one or more commands, a workflow is composed of one or more activities that are carried out in a sequence.</span></span> <span data-ttu-id="1e133-126">Le workflow Windows PowerShell convertit automatiquement la plupart des applets de commande Windows PowerShell en activités lors de son exécution.</span><span class="sxs-lookup"><span data-stu-id="1e133-126">Windows PowerShell Workflow automatically converts many of the Windows PowerShell cmdlets to activities when it runs a workflow.</span></span> <span data-ttu-id="1e133-127">Lorsque vous spécifiez une de ces applets de commande dans votre Runbook, l’activité correspondante est exécutée par Windows Workflow Foundation.</span><span class="sxs-lookup"><span data-stu-id="1e133-127">When you specify one of these cmdlets in your runbook, the corresponding activity is run by Windows Workflow Foundation.</span></span> <span data-ttu-id="1e133-128">Pour ces applets de commande sans activité correspondante, le workflow Windows PowerShell exécute automatiquement l'applet de commande au sein d'une activité [InlineScript](#inlinescript) .</span><span class="sxs-lookup"><span data-stu-id="1e133-128">For those cmdlets without a corresponding activity, Windows PowerShell Workflow automatically runs the cmdlet within an [InlineScript](#inlinescript) activity.</span></span> <span data-ttu-id="1e133-129">Il existe un ensemble d'applets de commande qui sont exclues et ne peuvent pas être utilisées dans un workflow, à moins que vous ne les incluiez explicitement dans un bloc InlineScript.</span><span class="sxs-lookup"><span data-stu-id="1e133-129">There is a set of cmdlets that are excluded and cannot be used in a workflow unless you explicitly include them in an InlineScript block.</span></span> <span data-ttu-id="1e133-130">Pour plus d'informations sur ces concepts, consultez [Utilisation des activités dans les workflows de script](http://technet.microsoft.com/library/jj574194.aspx).</span><span class="sxs-lookup"><span data-stu-id="1e133-130">For further details on these concepts, see [Using Activities in Script Workflows](http://technet.microsoft.com/library/jj574194.aspx).</span></span>

<span data-ttu-id="1e133-131">Les activités de workflow partagent un ensemble de paramètres communs pour configurer leur opération.</span><span class="sxs-lookup"><span data-stu-id="1e133-131">Workflow activities share a set of common parameters to configure their operation.</span></span> <span data-ttu-id="1e133-132">Pour plus d’informations sur les paramètres communs de flux de travail, consultez [about_WorkflowCommonParameters](http://technet.microsoft.com/library/jj129719.aspx).</span><span class="sxs-lookup"><span data-stu-id="1e133-132">For details about the workflow common parameters, see [about_WorkflowCommonParameters](http://technet.microsoft.com/library/jj129719.aspx).</span></span>

### <a name="positional-parameters"></a><span data-ttu-id="1e133-133">Paramètres positionnels</span><span class="sxs-lookup"><span data-stu-id="1e133-133">Positional parameters</span></span>
<span data-ttu-id="1e133-134">Vous ne pouvez pas utiliser les paramètres positionnels avec les activités et les applets de commande dans un workflow.</span><span class="sxs-lookup"><span data-stu-id="1e133-134">You can't use positional parameters with activities and cmdlets in a workflow.</span></span>  <span data-ttu-id="1e133-135">Cela signifie que vous devez utiliser des noms de paramètres.</span><span class="sxs-lookup"><span data-stu-id="1e133-135">All this means is that you must use parameter names.</span></span>

<span data-ttu-id="1e133-136">Par exemple, utilisez le code suivant pour afficher tous les services en cours d'exécution.</span><span class="sxs-lookup"><span data-stu-id="1e133-136">For example, consider the following code that gets all running services.</span></span>

     Get-Service | Where-Object {$_.Status -eq "Running"}

<span data-ttu-id="1e133-137">Si vous essayez d’exécuter ce même code dans un workflow, vous recevez un message de type « le jeu de paramètres est introuvable avec les paramètres nommés spécifiés ».</span><span class="sxs-lookup"><span data-stu-id="1e133-137">If you try to run this same code in a workflow, you receive a message like "Parameter set cannot be resolved using the specified named parameters."</span></span>  <span data-ttu-id="1e133-138">Pour corriger ce problème, entrez le nom du paramètre comme dans l’exemple suivant.</span><span class="sxs-lookup"><span data-stu-id="1e133-138">To correct this, provide the parameter name as in the following.</span></span>

    Workflow Get-RunningServices
    {
        Get-Service | Where-Object -FilterScript {$_.Status -eq "Running"}
    }

### <a name="deserialized-objects"></a><span data-ttu-id="1e133-139">Objets désérialisés</span><span class="sxs-lookup"><span data-stu-id="1e133-139">Deserialized objects</span></span>
<span data-ttu-id="1e133-140">Dans les workflows, les objets sont désérialisés.</span><span class="sxs-lookup"><span data-stu-id="1e133-140">Objects in workflows are deserialized.</span></span>  <span data-ttu-id="1e133-141">Cela signifie que leurs propriétés restent disponibles, mais pas leurs méthodes.</span><span class="sxs-lookup"><span data-stu-id="1e133-141">This means that their properties are still available, but not their methods.</span></span>  <span data-ttu-id="1e133-142">Par exemple, utilisez le code PowerShell suivant qui arrête un service à l'aide de la méthode Stop de l'objet Service.</span><span class="sxs-lookup"><span data-stu-id="1e133-142">For example, consider the following PowerShell code that stops a service using the Stop method of the Service object.</span></span>

    $Service = Get-Service -Name MyService
    $Service.Stop()

<span data-ttu-id="1e133-143">Si vous essayez d’exécuter ce code dans un workflow, vous obtenez une erreur indiquant que « l’appel de méthode n’est pas pris en charge dans un workflow Windows PowerShell ».</span><span class="sxs-lookup"><span data-stu-id="1e133-143">If you try to run this in a workflow, you receive an error saying "Method invocation is not supported in a Windows PowerShell Workflow."</span></span>  

<span data-ttu-id="1e133-144">Une option consiste à intégrer ces deux lignes de code dans un bloc [InlineScript](#inlinescript), où $Service représente un objet de service au sein du bloc.</span><span class="sxs-lookup"><span data-stu-id="1e133-144">One option is to wrap these two lines of code in an [InlineScript](#inlinescript) block in which case $Service would be a service object within the block.</span></span>

    Workflow Stop-Service
    {
        InlineScript {
            $Service = Get-Service -Name MyService
            $Service.Stop()
        }
    }

<span data-ttu-id="1e133-145">Une autre option consiste à utiliser une autre applet de commande qui exécute les mêmes fonctionnalités que la méthode, si celle-ci est disponible.</span><span class="sxs-lookup"><span data-stu-id="1e133-145">Another option is to use another cmdlet that performs the same functionality as the method, if one is available.</span></span>  <span data-ttu-id="1e133-146">Dans notre exemple, l’applet de commande Stop-Service fournit les mêmes fonctionnalités que la méthode Stop, et vous pouvez utiliser les éléments suivants pour un workflow.</span><span class="sxs-lookup"><span data-stu-id="1e133-146">In our sample, the Stop-Service cmdlet provides the same functionality as the Stop method, and you could use the following for a workflow.</span></span>

    Workflow Stop-MyService
    {
        $Service = Get-Service -Name MyService
        Stop-Service -Name $Service.Name
    }


## <a name="inlinescript"></a><span data-ttu-id="1e133-147">InlineScript</span><span class="sxs-lookup"><span data-stu-id="1e133-147">InlineScript</span></span>
<span data-ttu-id="1e133-148">L'activité **InlineScript** est utile lorsque vous devez exécuter une ou plusieurs commandes comme un script PowerShell standard au lieu d'un workflow PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1e133-148">The **InlineScript** activity is useful when you need to run one or more commands as traditional PowerShell script instead of PowerShell workflow.</span></span>  <span data-ttu-id="1e133-149">Alors que les commandes d'un workflow sont envoyées à Windows Workflow Foundation pour être traitées, les commandes d'un bloc InlineScript sont traitées par Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1e133-149">While commands in a workflow are sent to Windows Workflow Foundation for processing, commands in an InlineScript block are processed by Windows PowerShell.</span></span>

<span data-ttu-id="1e133-150">InlineScript utilise la syntaxe illustrée ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="1e133-150">InlineScript uses the following syntax shown below.</span></span>

    InlineScript
    {
      <Script Block>
    } <Common Parameters>

<span data-ttu-id="1e133-151">Vous pouvez renvoyer la sortie d'un bloc InlineScript en l'affectant à une variable.</span><span class="sxs-lookup"><span data-stu-id="1e133-151">You can return output from an InlineScript by assigning the output to a variable.</span></span> <span data-ttu-id="1e133-152">L'exemple suivant arrête un service puis renvoie le nom du service.</span><span class="sxs-lookup"><span data-stu-id="1e133-152">The following example stops a service and then outputs the service name.</span></span>

    Workflow Stop-MyService
    {
        $Output = InlineScript {
            $Service = Get-Service -Name MyService
            $Service.Stop()
            $Service
        }

        $Output.Name
    }


<span data-ttu-id="1e133-153">Vous pouvez passer des valeurs dans un bloc InlineScript, mais vous devez utiliser le modificateur de portée **$Using** .</span><span class="sxs-lookup"><span data-stu-id="1e133-153">You can pass values into an InlineScript block, but you must use **$Using** scope modifier.</span></span>  <span data-ttu-id="1e133-154">L'exemple suivant est identique à l'exemple précédent, sauf que le nom du service est fourni par une variable.</span><span class="sxs-lookup"><span data-stu-id="1e133-154">The following example is identical to the previous example except that the service name is provided by a variable.</span></span>

    Workflow Stop-MyService
    {
        $ServiceName = "MyService"

        $Output = InlineScript {
            $Service = Get-Service -Name $Using:ServiceName
            $Service.Stop()
            $Service
        }

        $Output.Name
    }


<span data-ttu-id="1e133-155">Même si les activités InlineScript peuvent être critiques dans certains workflows, elles ne prennent pas en charge les constructions de workflow et doivent être utilisées uniquement lorsque cela est nécessaire pour les raisons suivantes :</span><span class="sxs-lookup"><span data-stu-id="1e133-155">While InlineScript activities may be critical in certain workflows, they do not support workflow constructs and should only be used when necessary for the following reasons:</span></span>

* <span data-ttu-id="1e133-156">Vous ne pouvez pas utiliser de [points de contrôle](#checkpoints) à l’intérieur d’un bloc InlineScript.</span><span class="sxs-lookup"><span data-stu-id="1e133-156">You cannot use [checkpoints](#checkpoints) inside an InlineScript block.</span></span> <span data-ttu-id="1e133-157">Si une défaillance se produit dans le bloc, l'exécution doit reprendre depuis le début du bloc.</span><span class="sxs-lookup"><span data-stu-id="1e133-157">If a failure occurs within the block, it must be resumed from the beginning of the block.</span></span>
* <span data-ttu-id="1e133-158">Vous ne pouvez pas effectuer [d’exécution en parallèle](#parallel-processing) à l’intérieur d’un bloc InlineScriptBlock.</span><span class="sxs-lookup"><span data-stu-id="1e133-158">You cannot use [parallel execution](#parallel-processing) inside an InlineScriptBlock.</span></span>
* <span data-ttu-id="1e133-159">InlineScript affecte l'extensibilité du workflow puisque l'activité maintient la session Windows PowerShell pendant toute la durée du bloc InlineScript.</span><span class="sxs-lookup"><span data-stu-id="1e133-159">InlineScript affects scalability of the workflow since it holds the Windows PowerShell session for the entire length of the InlineScript block.</span></span>

<span data-ttu-id="1e133-160">Pour plus d’informations sur l’utilisation d’InlineScript, consultez [Exécution des commandes Windows PowerShell dans un workflow](http://technet.microsoft.com/library/jj574197.aspx) et [about_InlineScript](http://technet.microsoft.com/library/jj649082.aspx).</span><span class="sxs-lookup"><span data-stu-id="1e133-160">For more information on using InlineScript, see [Running Windows PowerShell Commands in a Workflow](http://technet.microsoft.com/library/jj574197.aspx) and [about_InlineScript](http://technet.microsoft.com/library/jj649082.aspx).</span></span>

## <a name="parallel-processing"></a><span data-ttu-id="1e133-161">Traitement en parallèle</span><span class="sxs-lookup"><span data-stu-id="1e133-161">Parallel processing</span></span>
<span data-ttu-id="1e133-162">L'un des avantages des workflows Windows PowerShell est la possibilité d'exécuter un ensemble de commandes en parallèle, et non séquentiellement comme avec un script classique.</span><span class="sxs-lookup"><span data-stu-id="1e133-162">One advantage of Windows PowerShell Workflows is the ability to perform a set of commands in parallel instead of sequentially as with a typical script.</span></span>

<span data-ttu-id="1e133-163">Vous pouvez utiliser le mot clé **Parallel** pour créer un bloc de script avec plusieurs commandes qui s’exécutent simultanément.</span><span class="sxs-lookup"><span data-stu-id="1e133-163">You can use the **Parallel** keyword to create a script block with multiple commands that run concurrently.</span></span> <span data-ttu-id="1e133-164">Pour ce faire, utilisez la syntaxe illustrée ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="1e133-164">This uses the following syntax shown below.</span></span> <span data-ttu-id="1e133-165">Dans ce cas, Activity1 et Activity2 démarrent en même temps.</span><span class="sxs-lookup"><span data-stu-id="1e133-165">In this case, Activity1 and Activity2 starts at the same time.</span></span> <span data-ttu-id="1e133-166">Activity3 démarre uniquement quand Activity1 et Activity2 sont toutes deux terminées.</span><span class="sxs-lookup"><span data-stu-id="1e133-166">Activity3 starts only after both Activity1 and Activity2 have completed.</span></span>

    Parallel
    {
      <Activity1>
      <Activity2>
    }
    <Activity3>


<span data-ttu-id="1e133-167">Par exemple, considérez les commandes PowerShell suivantes qui copier plusieurs fichiers vers une destination sur le réseau.</span><span class="sxs-lookup"><span data-stu-id="1e133-167">For example, consider the following PowerShell commands that copy multiple files to a network destination.</span></span>  <span data-ttu-id="1e133-168">Ces commandes sont exécutées séquentiellement afin que le fichier termine la copie avant de démarrer la suivante.</span><span class="sxs-lookup"><span data-stu-id="1e133-168">These commands are run sequentially so that one file must finish copying before the next is started.</span></span>     

    Copy-Item -Path C:\LocalPath\File1.txt -Destination \\NetworkPath\File1.txt
    Copy-Item -Path C:\LocalPath\File2.txt -Destination \\NetworkPath\File2.txt
    Copy-Item -Path C:\LocalPath\File3.txt -Destination \\NetworkPath\File3.txt

<span data-ttu-id="1e133-169">Le workflow suivant exécute ces commandes en parallèle afin qu'elles commencent toutes la copie en même temps.</span><span class="sxs-lookup"><span data-stu-id="1e133-169">The following workflow runs these same commands in parallel so that they all start copying at the same time.</span></span>  <span data-ttu-id="1e133-170">Le message confirmant la fin de l’opération apparaît uniquement une fois toutes les copies effectuées.</span><span class="sxs-lookup"><span data-stu-id="1e133-170">Only after they are all copied is the completion message displayed.</span></span>

    Workflow Copy-Files
    {
        Parallel
        {
            Copy-Item -Path "C:\LocalPath\File1.txt" -Destination "\\NetworkPath"
            Copy-Item -Path "C:\LocalPath\File2.txt" -Destination "\\NetworkPath"
            Copy-Item -Path "C:\LocalPath\File3.txt" -Destination "\\NetworkPath"
        }

        Write-Output "Files copied."
    }


<span data-ttu-id="1e133-171">Vous pouvez utiliser la construction **ForEach-Parallel** pour traiter simultanément les commandes de chaque élément d'une collection.</span><span class="sxs-lookup"><span data-stu-id="1e133-171">You can use the **ForEach -Parallel** construct to process commands for each item in a collection concurrently.</span></span> <span data-ttu-id="1e133-172">Les éléments de la collection sont traités en parallèle, tandis que les commandes du bloc de script sont exécutées séquentiellement.</span><span class="sxs-lookup"><span data-stu-id="1e133-172">The items in the collection are processed in parallel while the commands in the script block run sequentially.</span></span> <span data-ttu-id="1e133-173">Pour ce faire, utilisez la syntaxe illustrée ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="1e133-173">This uses the following syntax shown below.</span></span> <span data-ttu-id="1e133-174">Dans ce cas, Activity1 démarre en même temps pour tous les éléments de la collection.</span><span class="sxs-lookup"><span data-stu-id="1e133-174">In this case, Activity1 starts at the same time for all items in the collection.</span></span> <span data-ttu-id="1e133-175">Pour chaque élément, Activity2 démarre une fois Activity1 terminée.</span><span class="sxs-lookup"><span data-stu-id="1e133-175">For each item, Activity2 starts after Activity1 is complete.</span></span> <span data-ttu-id="1e133-176">Activity3 démarre uniquement quand Activity1 et Activity2 sont toutes deux terminées pour tous les éléments.</span><span class="sxs-lookup"><span data-stu-id="1e133-176">Activity3 starts only after both Activity1 and Activity2 have completed for all items.</span></span>

    ForEach -Parallel ($<item> in $<collection>)
    {
      <Activity1>
      <Activity2>
    }
    <Activity3>

<span data-ttu-id="1e133-177">L'exemple suivant est similaire à l'exemple précédent concernant la copie de fichiers en parallèle.</span><span class="sxs-lookup"><span data-stu-id="1e133-177">The following example is similar to the previous example copying files in parallel.</span></span>  <span data-ttu-id="1e133-178">Dans ce cas, un message s'affiche pour chaque fichier après la copie.</span><span class="sxs-lookup"><span data-stu-id="1e133-178">In this case, a message is displayed for each file after it copies.</span></span>  <span data-ttu-id="1e133-179">Le message confirmant la fin de l'opération apparaît uniquement une fois toutes les copies effectuées.</span><span class="sxs-lookup"><span data-stu-id="1e133-179">Only after they are all completely copied is the final completion message displayed.</span></span>

    Workflow Copy-Files
    {
        $files = @("C:\LocalPath\File1.txt","C:\LocalPath\File2.txt","C:\LocalPath\File3.txt")

        ForEach -Parallel ($File in $Files)
        {
            Copy-Item -Path $File -Destination \\NetworkPath
            Write-Output "$File copied."
        }

        Write-Output "All files copied."
    }

> [!NOTE]
> <span data-ttu-id="1e133-180">Nous vous déconseillons d'exécuter des Runbooks enfants en parallèle car les résultats obtenus ne sont pas fiables.</span><span class="sxs-lookup"><span data-stu-id="1e133-180">We do not recommend running child runbooks in parallel since this has been shown to give unreliable results.</span></span>  <span data-ttu-id="1e133-181">Parfois, la sortie du Runbook enfant n’apparaît pas, et les paramètres d’un Runbook enfant peuvent affecter les autres Runbooks enfants parallèles.</span><span class="sxs-lookup"><span data-stu-id="1e133-181">The output from the child runbook sometimes does not show up, and settings in one child runbook can affect the other parallel child runbooks</span></span>
>

## <a name="checkpoints"></a><span data-ttu-id="1e133-182">points de contrôle</span><span class="sxs-lookup"><span data-stu-id="1e133-182">Checkpoints</span></span>
<span data-ttu-id="1e133-183">Un *point de contrôle* est un instantané de l'état actuel du workflow qui inclut la valeur actuelle des variables et toute sortie générée à ce stade.</span><span class="sxs-lookup"><span data-stu-id="1e133-183">A *checkpoint* is a snapshot of the current state of the workflow that includes the current value for variables and any output generated to that point.</span></span> <span data-ttu-id="1e133-184">Si un flux de travail se termine par erreur ou est suspendu, il démarrera à la prochaine exécution à partir de son dernier point de contrôle et non depuis le début du worfklow.</span><span class="sxs-lookup"><span data-stu-id="1e133-184">If a workflow ends in error or is suspended, then the next time it is run it will start from its last checkpoint instead of the start of the worfklow.</span></span>  <span data-ttu-id="1e133-185">Vous pouvez définir un point de contrôle dans un workflow avec l'activité **Checkpoint-Workflow** .</span><span class="sxs-lookup"><span data-stu-id="1e133-185">You can set a checkpoint in a workflow with the **Checkpoint-Workflow** activity.</span></span>

<span data-ttu-id="1e133-186">Dans l'exemple de code suivant, une exception se produit après qu'Activity2 a provoqué l'arrêt du workflow.</span><span class="sxs-lookup"><span data-stu-id="1e133-186">In the following sample code, an exception occurs after Activity2 causing the workflow to end.</span></span> <span data-ttu-id="1e133-187">Lorsque le workflow est réexécuté, il commence par exécuter Activity2, juste après le dernier point de contrôle défini.</span><span class="sxs-lookup"><span data-stu-id="1e133-187">When the workflow is run again, it starts by running Activity2 since this was just after the last checkpoint set.</span></span>

    <Activity1>
    Checkpoint-Workflow
    <Activity2>
    <Exception>
    <Activity3>

<span data-ttu-id="1e133-188">Vous devez définir les points de contrôle d'un workflow après les activités qui peuvent être sujettes à une exception et qui ne doivent pas être réexécutées à la reprise du workflow.</span><span class="sxs-lookup"><span data-stu-id="1e133-188">You should set checkpoints in a workflow after activities that may be prone to exception and should not be repeated if the workflow is resumed.</span></span> <span data-ttu-id="1e133-189">Par exemple, votre workflow peut créer une machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="1e133-189">For example, your workflow may create a virtual machine.</span></span> <span data-ttu-id="1e133-190">Vous pouvez définir un point de contrôle avant et après les commandes de création de la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="1e133-190">You could set a checkpoint both before and after the commands to create the virtual machine.</span></span> <span data-ttu-id="1e133-191">En cas d'échec de la création, les commandes doivent être répétées si le workflow est redémarré.</span><span class="sxs-lookup"><span data-stu-id="1e133-191">If the creation fails, then the commands would be repeated if the workflow is started again.</span></span> <span data-ttu-id="1e133-192">Si le workflow échoue après que la création a réussi, la machine virtuelle n’est pas recréée à la reprise du workflow.</span><span class="sxs-lookup"><span data-stu-id="1e133-192">If the worfklow fails after the creation succeeds, then the virtual machine will not be created again when the workflow is resumed.</span></span>

<span data-ttu-id="1e133-193">L'exemple suivant copie plusieurs fichiers vers un emplacement réseau et définit un point de contrôle après chaque fichier.</span><span class="sxs-lookup"><span data-stu-id="1e133-193">The following example copies multiple files to a network location and sets a checkpoint after each file.</span></span>  <span data-ttu-id="1e133-194">Si l’emplacement réseau est perdu, le workflow s’arrête en générant une erreur.</span><span class="sxs-lookup"><span data-stu-id="1e133-194">If the network location is lost, then the workflow ends in error.</span></span>  <span data-ttu-id="1e133-195">Lorsqu’il est relancé, il reprend au dernier point de contrôle, ce qui signifie que seuls les fichiers qui ont déjà été copiés sont ignorés.</span><span class="sxs-lookup"><span data-stu-id="1e133-195">When it is started again, it will resume at the last checkpoint meaning that only the files that have already been copied are skipped.</span></span>

    Workflow Copy-Files
    {
        $files = @("C:\LocalPath\File1.txt","C:\LocalPath\File2.txt","C:\LocalPath\File3.txt")

        ForEach ($File in $Files)
        {
            Copy-Item -Path $File -Destination \\NetworkPath
            Write-Output "$File copied."
            Checkpoint-Workflow
        }

        Write-Output "All files copied."
    }

<span data-ttu-id="1e133-196">Étant donné que les informations d’identification de nom d’utilisateur ne sont pas conservées après l’appel de l’activité [Suspend-Workflow](https://technet.microsoft.com/library/jj733586.aspx) ou après le dernier point de contrôle, vous devez définir les informations d’identification sur « null », puis les récupérer à nouveau à partir du magasin de ressources après l’activité **Suspend-Workflow** ou après l’appel du point de contrôle.</span><span class="sxs-lookup"><span data-stu-id="1e133-196">Because username credentials are not persisted after you call the [Suspend-Workflow](https://technet.microsoft.com/library/jj733586.aspx) activity or after the last checkpoint, you need to set the credentials to null and then retrieve them again from the asset store after **Suspend-Workflow** or checkpoint is called.</span></span>  <span data-ttu-id="1e133-197">À défaut, vous risquez de rencontrer le message d’erreur suivant : *Impossible de reprendre la tâche de workflow, soit parce que les données de persistance n’ont pas pu être enregistrées en totalité, soit parce que les données de persistance enregistrées ont été endommagées. Vous devez redémarrer le workflow.*</span><span class="sxs-lookup"><span data-stu-id="1e133-197">Otherwise, you may receive the following error message: *The workflow job cannot be resumed, either because persistence data could not be saved completely, or saved persistence data has been corrupted. You must restart the workflow.*</span></span>

<span data-ttu-id="1e133-198">Le même code ci-dessous montre comment traiter ce problème dans vos Runbooks de workflow PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1e133-198">The following same code demonstrates how to handle this in your PowerShell Workflow runbooks.</span></span>

    workflow CreateTestVms
    {
       $Cred = Get-AzureAutomationCredential -Name "MyCredential"
       $null = Add-AzureRmAccount -Credential $Cred

       $VmsToCreate = Get-AzureAutomationVariable -Name "VmsToCreate"

       foreach ($VmName in $VmsToCreate)
         {
          # Do work first to create the VM (code not shown)

          # Now add the VM
          New-AzureRmVm -VM $Vm -Location "WestUs" -ResourceGroupName "ResourceGroup01"

          # Checkpoint so that VM creation is not repeated if workflow suspends
          $Cred = $null
          Checkpoint-Workflow
          $Cred = Get-AzureAutomationCredential -Name "MyCredential"
          $null = Add-AzureRmAccount -Credential $Cred
         }
     }


<span data-ttu-id="1e133-199">Cette procédure n’est pas nécessaire si vous vous authentifiez à l’aide d’un compte d’identification configuré avec un service principal.</span><span class="sxs-lookup"><span data-stu-id="1e133-199">This is not required if you are authenticating using a Run As account configured with a service principal.</span></span>  

<span data-ttu-id="1e133-200">Pour plus d'informations sur les points de contrôle, consultez [Ajout de points de contrôle à un workflow de script](http://technet.microsoft.com/library/jj574114.aspx).</span><span class="sxs-lookup"><span data-stu-id="1e133-200">For more information about checkpoints, see [Adding Checkpoints to a Script Workflow](http://technet.microsoft.com/library/jj574114.aspx).</span></span>

## <a name="next-steps"></a><span data-ttu-id="1e133-201">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="1e133-201">Next steps</span></span>
* <span data-ttu-id="1e133-202">Pour une prise en main des Runbooks de workflow PowerShell, consultez [Mon premier Runbook PowerShell Workflow](automation-first-runbook-textual.md)</span><span class="sxs-lookup"><span data-stu-id="1e133-202">To get started with PowerShell workflow runbooks, see [My first PowerShell workflow runbook](automation-first-runbook-textual.md)</span></span>
