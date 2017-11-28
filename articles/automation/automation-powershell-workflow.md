---
title: aaaLearning du flux de travail PowerShell pour Azure Automation | Documents Microsoft
description: "Cet article est destiné à une rapide leçon auteurs familiarisés avec PowerShell toounderstand hello des différences spécifiques entre PowerShell et PowerShell Workflow et les procédures opérationnelles de concepts tooAutomation applicable."
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
ms.openlocfilehash: 362c504eb96d31b99a826b128e6a591beecaa084
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="learning-key-windows-powershell-workflow-concepts-for-automation-runbooks"></a><span data-ttu-id="306f6-103">Découvrir les principaux concepts de workflow Windows PowerShell pour les runbooks Automation</span><span class="sxs-lookup"><span data-stu-id="306f6-103">Learning key Windows PowerShell Workflow concepts for Automation runbooks</span></span> 
<span data-ttu-id="306f6-104">Les Runbooks d'Azure Automation sont implémentés en tant que workflows Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="306f6-104">Runbooks in Azure Automation are implemented as Windows PowerShell Workflows.</span></span>  <span data-ttu-id="306f6-105">Un Workflow Windows PowerShell est semblable tooa de script Windows PowerShell, mais présente des différences importantes qui peuvent être déroutant tooa nouvel utilisateur.</span><span class="sxs-lookup"><span data-stu-id="306f6-105">A Windows PowerShell Workflow is similar tooa Windows PowerShell script but has some significant differences that can be confusing tooa new user.</span></span>  <span data-ttu-id="306f6-106">Alors que cet article est prévue toohelp écrire des runbooks à l’aide de flux de travail PowerShell, nous vous recommandons de que écrire des runbooks à l’aide de PowerShell, sauf si vous avez besoin de points de contrôle.</span><span class="sxs-lookup"><span data-stu-id="306f6-106">While this article is intended toohelp you write runbooks using PowerShell workflow, we recommend you write runbooks using PowerShell unless you need checkpoints.</span></span>  <span data-ttu-id="306f6-107">Il existe plusieurs différences de syntaxe pour créer des flux de travail PowerShell runbook et ces différences nécessitent un peu plus travail toowrite efficace des flux de travail.</span><span class="sxs-lookup"><span data-stu-id="306f6-107">There are several syntax differences when authoring PowerShell Workflow runbooks and these differences require a bit more work toowrite effective workflows.</span></span>  

<span data-ttu-id="306f6-108">Un flux de travail est une séquence d’étapes programmées et connectées qui effectuent des tâches longues ou requièrent une coordination hello de plusieurs étapes sur plusieurs appareils ou nœuds gérés.</span><span class="sxs-lookup"><span data-stu-id="306f6-108">A workflow is a sequence of programmed, connected steps that perform long-running tasks or require hello coordination of multiple steps across multiple devices or managed nodes.</span></span> <span data-ttu-id="306f6-109">Hello d’un flux de travail sur un script normal avantages hello permettre toosimultaneously effectuer une action sur plusieurs appareils et hello capacité tooautomatically récupérer après des défaillances.</span><span class="sxs-lookup"><span data-stu-id="306f6-109">hello benefits of a workflow over a normal script include hello ability toosimultaneously perform an action against multiple devices and hello ability tooautomatically recover from failures.</span></span> <span data-ttu-id="306f6-110">Un workflow Windows PowerShell est un script Windows PowerShell qui utilise Windows Workflow Foundation.</span><span class="sxs-lookup"><span data-stu-id="306f6-110">A Windows PowerShell Workflow is a Windows PowerShell script that uses Windows Workflow Foundation.</span></span> <span data-ttu-id="306f6-111">Bien que les flux de travail hello sont écrit avec la syntaxe Windows PowerShell et lancé par Windows PowerShell, il est traité par Windows Workflow Foundation.</span><span class="sxs-lookup"><span data-stu-id="306f6-111">While hello workflow is written with Windows PowerShell syntax and launched by Windows PowerShell, it is processed by Windows Workflow Foundation.</span></span>

<span data-ttu-id="306f6-112">Pour plus d’informations sur les rubriques hello dans cet article, consultez [prise en main de Windows PowerShell Workflow](http://technet.microsoft.com/library/jj134242.aspx).</span><span class="sxs-lookup"><span data-stu-id="306f6-112">For complete details on hello topics in this article, see [Getting Started with Windows PowerShell Workflow](http://technet.microsoft.com/library/jj134242.aspx).</span></span>

## <a name="basic-structure-of-a-workflow"></a><span data-ttu-id="306f6-113">Structure de base d'un workflow</span><span class="sxs-lookup"><span data-stu-id="306f6-113">Basic structure of a workflow</span></span>
<span data-ttu-id="306f6-114">Hello première étape tooconverting un flux de travail PowerShell script tooa PowerShell est plaçant avec hello **Workflow** (mot clé).</span><span class="sxs-lookup"><span data-stu-id="306f6-114">hello first step tooconverting a PowerShell script tooa PowerShell workflow is enclosing it with hello **Workflow** keyword.</span></span>  <span data-ttu-id="306f6-115">Un flux de travail démarre avec hello **Workflow** mot clé suivi des corps hello du script hello entouré accolades.</span><span class="sxs-lookup"><span data-stu-id="306f6-115">A workflow starts with hello **Workflow** keyword followed by hello body of hello script enclosed in braces.</span></span> <span data-ttu-id="306f6-116">nom de Hello du flux de travail hello suit hello **Workflow** mot clé, comme indiqué dans la syntaxe de hello :</span><span class="sxs-lookup"><span data-stu-id="306f6-116">hello name of hello workflow follows hello **Workflow** keyword as shown in hello following syntax:</span></span>

    Workflow Test-Workflow
    {
       <Commands>
    }

<span data-ttu-id="306f6-117">nom Hello du flux de travail hello doit correspondre au nom hello de runbook Automation de hello.</span><span class="sxs-lookup"><span data-stu-id="306f6-117">hello name of hello workflow must match hello name of hello Automation runbook.</span></span> <span data-ttu-id="306f6-118">Si hello runbook est en cours d’importation, nom de fichier hello doit correspondre au nom de flux de travail hello et doit se terminer par *.ps1*.</span><span class="sxs-lookup"><span data-stu-id="306f6-118">If hello runbook is being imported, then hello filename must match hello workflow name and must end in *.ps1*.</span></span>

<span data-ttu-id="306f6-119">tooadd paramètres toohello flux de travail, utilisez hello **Param** mot clé comme vous le feriez tooa script.</span><span class="sxs-lookup"><span data-stu-id="306f6-119">tooadd parameters toohello workflow, use hello **Param** keyword just as you would tooa script.</span></span>

## <a name="code-changes"></a><span data-ttu-id="306f6-120">Modifications du code</span><span class="sxs-lookup"><span data-stu-id="306f6-120">Code changes</span></span>
<span data-ttu-id="306f6-121">Code de flux de travail PowerShell recherche le code de script tooPowerShell presque identique à l’exception de quelques modifications importantes.</span><span class="sxs-lookup"><span data-stu-id="306f6-121">PowerShell workflow code looks almost identical tooPowerShell script code except for a few significant changes.</span></span>  <span data-ttu-id="306f6-122">Hello les sections suivantes décrire les modifications que vous avez besoin toomake tooa PowerShell script pour qu’il toorun dans un flux de travail.</span><span class="sxs-lookup"><span data-stu-id="306f6-122">hello following sections describe changes that you need toomake tooa PowerShell script for it toorun in a workflow.</span></span>

### <a name="activities"></a><span data-ttu-id="306f6-123">Activités</span><span class="sxs-lookup"><span data-stu-id="306f6-123">Activities</span></span>
<span data-ttu-id="306f6-124">Une activité est une tâche spécifique dans un workflow.</span><span class="sxs-lookup"><span data-stu-id="306f6-124">An activity is a specific task in a workflow.</span></span> <span data-ttu-id="306f6-125">Tout comme un script se compose d'une ou de plusieurs commandes, un workflow se compose d'une ou de plusieurs activités exécutées en séquence.</span><span class="sxs-lookup"><span data-stu-id="306f6-125">Just as a script is composed of one or more commands, a workflow is composed of one or more activities that are carried out in a sequence.</span></span> <span data-ttu-id="306f6-126">Flux de travail Windows PowerShell convertit automatiquement la plupart de hello tooactivities d’applets de commande Windows PowerShell lors de l’exécution d’un flux de travail.</span><span class="sxs-lookup"><span data-stu-id="306f6-126">Windows PowerShell Workflow automatically converts many of hello Windows PowerShell cmdlets tooactivities when it runs a workflow.</span></span> <span data-ttu-id="306f6-127">Lorsque vous spécifiez une de ces applets de commande dans votre runbook, activité correspondante hello est exécutée par Windows Workflow Foundation.</span><span class="sxs-lookup"><span data-stu-id="306f6-127">When you specify one of these cmdlets in your runbook, hello corresponding activity is run by Windows Workflow Foundation.</span></span> <span data-ttu-id="306f6-128">Pour ces applets de commande sans activité correspondante, Windows PowerShell Workflow exécute automatiquement l’applet de commande hello dans un [InlineScript](#inlinescript) activité.</span><span class="sxs-lookup"><span data-stu-id="306f6-128">For those cmdlets without a corresponding activity, Windows PowerShell Workflow automatically runs hello cmdlet within an [InlineScript](#inlinescript) activity.</span></span> <span data-ttu-id="306f6-129">Il existe un ensemble d'applets de commande qui sont exclues et ne peuvent pas être utilisées dans un workflow, à moins que vous ne les incluiez explicitement dans un bloc InlineScript.</span><span class="sxs-lookup"><span data-stu-id="306f6-129">There is a set of cmdlets that are excluded and cannot be used in a workflow unless you explicitly include them in an InlineScript block.</span></span> <span data-ttu-id="306f6-130">Pour plus d'informations sur ces concepts, consultez [Utilisation des activités dans les workflows de script](http://technet.microsoft.com/library/jj574194.aspx).</span><span class="sxs-lookup"><span data-stu-id="306f6-130">For further details on these concepts, see [Using Activities in Script Workflows](http://technet.microsoft.com/library/jj574194.aspx).</span></span>

<span data-ttu-id="306f6-131">Activités de flux de travail partagent un ensemble de tooconfigure de paramètres courants de leur fonctionnement.</span><span class="sxs-lookup"><span data-stu-id="306f6-131">Workflow activities share a set of common parameters tooconfigure their operation.</span></span> <span data-ttu-id="306f6-132">Pour plus d’informations sur les paramètres communs de workflow hello, consultez [about_WorkflowCommonParameters](http://technet.microsoft.com/library/jj129719.aspx).</span><span class="sxs-lookup"><span data-stu-id="306f6-132">For details about hello workflow common parameters, see [about_WorkflowCommonParameters](http://technet.microsoft.com/library/jj129719.aspx).</span></span>

### <a name="positional-parameters"></a><span data-ttu-id="306f6-133">Paramètres positionnels</span><span class="sxs-lookup"><span data-stu-id="306f6-133">Positional parameters</span></span>
<span data-ttu-id="306f6-134">Vous ne pouvez pas utiliser les paramètres positionnels avec les activités et les applets de commande dans un workflow.</span><span class="sxs-lookup"><span data-stu-id="306f6-134">You can't use positional parameters with activities and cmdlets in a workflow.</span></span>  <span data-ttu-id="306f6-135">Cela signifie que vous devez utiliser des noms de paramètres.</span><span class="sxs-lookup"><span data-stu-id="306f6-135">All this means is that you must use parameter names.</span></span>

<span data-ttu-id="306f6-136">Par exemple, considérez hello suivant de code qui obtient tous les services en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="306f6-136">For example, consider hello following code that gets all running services.</span></span>

     Get-Service | Where-Object {$_.Status -eq "Running"}

<span data-ttu-id="306f6-137">Si vous essayez toorun ce même code dans un flux de travail, vous recevez un message comme « Paramètre ensemble ne peut pas être résolu à l’aide de hello spécifié des paramètres nommés. »</span><span class="sxs-lookup"><span data-stu-id="306f6-137">If you try toorun this same code in a workflow, you receive a message like "Parameter set cannot be resolved using hello specified named parameters."</span></span>  <span data-ttu-id="306f6-138">toocorrect, nom de paramètre hello comme dans les éléments suivants de hello.</span><span class="sxs-lookup"><span data-stu-id="306f6-138">toocorrect this, provide hello parameter name as in hello following.</span></span>

    Workflow Get-RunningServices
    {
        Get-Service | Where-Object -FilterScript {$_.Status -eq "Running"}
    }

### <a name="deserialized-objects"></a><span data-ttu-id="306f6-139">Objets désérialisés</span><span class="sxs-lookup"><span data-stu-id="306f6-139">Deserialized objects</span></span>
<span data-ttu-id="306f6-140">Dans les workflows, les objets sont désérialisés.</span><span class="sxs-lookup"><span data-stu-id="306f6-140">Objects in workflows are deserialized.</span></span>  <span data-ttu-id="306f6-141">Cela signifie que leurs propriétés restent disponibles, mais pas leurs méthodes.</span><span class="sxs-lookup"><span data-stu-id="306f6-141">This means that their properties are still available, but not their methods.</span></span>  <span data-ttu-id="306f6-142">Par exemple, considérez hello suivant de code PowerShell qui arrête un service à l’aide de la méthode Stop de hello hello d’objet de Service.</span><span class="sxs-lookup"><span data-stu-id="306f6-142">For example, consider hello following PowerShell code that stops a service using hello Stop method of hello Service object.</span></span>

    $Service = Get-Service -Name MyService
    $Service.Stop()

<span data-ttu-id="306f6-143">Si vous essayez toorun dans un flux de travail, vous recevez une erreur indiquant que « l’appel de méthode n'est pas prise en charge dans un Workflow Windows PowerShell. »</span><span class="sxs-lookup"><span data-stu-id="306f6-143">If you try toorun this in a workflow, you receive an error saying "Method invocation is not supported in a Windows PowerShell Workflow."</span></span>  

<span data-ttu-id="306f6-144">Une option consiste à toowrap ces deux lignes de code dans un [InlineScript](#inlinescript) bloquer dans quels cas $Service serait un objet de service au sein du bloc de hello.</span><span class="sxs-lookup"><span data-stu-id="306f6-144">One option is toowrap these two lines of code in an [InlineScript](#inlinescript) block in which case $Service would be a service object within hello block.</span></span>

    Workflow Stop-Service
    {
        InlineScript {
            $Service = Get-Service -Name MyService
            $Service.Stop()
        }
    }

<span data-ttu-id="306f6-145">Une autre option consiste à toouse une autre applet de commande qui exécute hello les mêmes fonctionnalités que la méthode hello, si celle-ci est disponible.</span><span class="sxs-lookup"><span data-stu-id="306f6-145">Another option is toouse another cmdlet that performs hello same functionality as hello method, if one is available.</span></span>  <span data-ttu-id="306f6-146">Dans notre exemple, hello Stop-Service fournit hello même fonctionnalité que la méthode Stop de hello et que vous pouvez utiliser suivant de hello pour un flux de travail.</span><span class="sxs-lookup"><span data-stu-id="306f6-146">In our sample, hello Stop-Service cmdlet provides hello same functionality as hello Stop method, and you could use hello following for a workflow.</span></span>

    Workflow Stop-MyService
    {
        $Service = Get-Service -Name MyService
        Stop-Service -Name $Service.Name
    }


## <a name="inlinescript"></a><span data-ttu-id="306f6-147">InlineScript</span><span class="sxs-lookup"><span data-stu-id="306f6-147">InlineScript</span></span>
<span data-ttu-id="306f6-148">Hello **InlineScript** activité est utile lorsque vous devez toorun une ou plusieurs commandes en tant que script PowerShell traditionnel au lieu de flux de travail PowerShell.</span><span class="sxs-lookup"><span data-stu-id="306f6-148">hello **InlineScript** activity is useful when you need toorun one or more commands as traditional PowerShell script instead of PowerShell workflow.</span></span>  <span data-ttu-id="306f6-149">Alors que les commandes dans un flux de travail sont envoyées tooWindows Workflow Foundation pour le traitement, les commandes dans un bloc InlineScript sont traitées par Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="306f6-149">While commands in a workflow are sent tooWindows Workflow Foundation for processing, commands in an InlineScript block are processed by Windows PowerShell.</span></span>

<span data-ttu-id="306f6-150">InlineScript utilise hello selon la syntaxe ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="306f6-150">InlineScript uses hello following syntax shown below.</span></span>

    InlineScript
    {
      <Script Block>
    } <Common Parameters>

<span data-ttu-id="306f6-151">Vous pouvez retourner la sortie à partir d’un InlineScript en affectant hello sortie tooa variable.</span><span class="sxs-lookup"><span data-stu-id="306f6-151">You can return output from an InlineScript by assigning hello output tooa variable.</span></span> <span data-ttu-id="306f6-152">Bonjour exemple suivant arrête un service et génère ensuite le nom du service hello.</span><span class="sxs-lookup"><span data-stu-id="306f6-152">hello following example stops a service and then outputs hello service name.</span></span>

    Workflow Stop-MyService
    {
        $Output = InlineScript {
            $Service = Get-Service -Name MyService
            $Service.Stop()
            $Service
        }

        $Output.Name
    }


<span data-ttu-id="306f6-153">Vous pouvez passer des valeurs dans un bloc InlineScript, mais vous devez utiliser le modificateur de portée **$Using** .</span><span class="sxs-lookup"><span data-stu-id="306f6-153">You can pass values into an InlineScript block, but you must use **$Using** scope modifier.</span></span>  <span data-ttu-id="306f6-154">Hello suivant est identique toohello précédent exemple, sauf que le nom de service hello est fourni par une variable.</span><span class="sxs-lookup"><span data-stu-id="306f6-154">hello following example is identical toohello previous example except that hello service name is provided by a variable.</span></span>

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


<span data-ttu-id="306f6-155">InlineScript activités peuvent être essentielles pour certains flux de travail, ils ne prennent pas en charge les constructions de flux de travail et doivent être utilisés uniquement lorsque cela est nécessaire pour hello suivant raisons :</span><span class="sxs-lookup"><span data-stu-id="306f6-155">While InlineScript activities may be critical in certain workflows, they do not support workflow constructs and should only be used when necessary for hello following reasons:</span></span>

* <span data-ttu-id="306f6-156">Vous ne pouvez pas utiliser de [points de contrôle](#checkpoints) à l’intérieur d’un bloc InlineScript.</span><span class="sxs-lookup"><span data-stu-id="306f6-156">You cannot use [checkpoints](#checkpoints) inside an InlineScript block.</span></span> <span data-ttu-id="306f6-157">Si une défaillance se produit dans le bloc de hello, il doit être reprise à partir du début de hello du bloc de hello.</span><span class="sxs-lookup"><span data-stu-id="306f6-157">If a failure occurs within hello block, it must be resumed from hello beginning of hello block.</span></span>
* <span data-ttu-id="306f6-158">Vous ne pouvez pas effectuer [d’exécution en parallèle](#parallel-processing) à l’intérieur d’un bloc InlineScriptBlock.</span><span class="sxs-lookup"><span data-stu-id="306f6-158">You cannot use [parallel execution](#parallel-processing) inside an InlineScriptBlock.</span></span>
* <span data-ttu-id="306f6-159">InlineScript affecte l’évolutivité des flux de travail hello puisqu’elle maintient la session Windows PowerShell de hello pour hello toute longueur du bloc InlineScript de hello.</span><span class="sxs-lookup"><span data-stu-id="306f6-159">InlineScript affects scalability of hello workflow since it holds hello Windows PowerShell session for hello entire length of hello InlineScript block.</span></span>

<span data-ttu-id="306f6-160">Pour plus d’informations sur l’utilisation d’InlineScript, consultez [Exécution des commandes Windows PowerShell dans un workflow](http://technet.microsoft.com/library/jj574197.aspx) et [about_InlineScript](http://technet.microsoft.com/library/jj649082.aspx).</span><span class="sxs-lookup"><span data-stu-id="306f6-160">For more information on using InlineScript, see [Running Windows PowerShell Commands in a Workflow](http://technet.microsoft.com/library/jj574197.aspx) and [about_InlineScript](http://technet.microsoft.com/library/jj649082.aspx).</span></span>

## <a name="parallel-processing"></a><span data-ttu-id="306f6-161">Traitement en parallèle</span><span class="sxs-lookup"><span data-stu-id="306f6-161">Parallel processing</span></span>
<span data-ttu-id="306f6-162">Un avantage de flux de travail Windows PowerShell est hello capacité tooperform un ensemble de commandes en parallèle à la place de séquentielle comme avec un script typique.</span><span class="sxs-lookup"><span data-stu-id="306f6-162">One advantage of Windows PowerShell Workflows is hello ability tooperform a set of commands in parallel instead of sequentially as with a typical script.</span></span>

<span data-ttu-id="306f6-163">Vous pouvez utiliser hello **parallèles** mot clé toocreate un bloc de script avec plusieurs commandes qui s’exécutent simultanément.</span><span class="sxs-lookup"><span data-stu-id="306f6-163">You can use hello **Parallel** keyword toocreate a script block with multiple commands that run concurrently.</span></span> <span data-ttu-id="306f6-164">Cette méthode utilise hello selon la syntaxe ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="306f6-164">This uses hello following syntax shown below.</span></span> <span data-ttu-id="306f6-165">Dans ce cas, Activity1 et Activity2 démarre à hello même temps.</span><span class="sxs-lookup"><span data-stu-id="306f6-165">In this case, Activity1 and Activity2 starts at hello same time.</span></span> <span data-ttu-id="306f6-166">Activity3 démarre uniquement quand Activity1 et Activity2 sont toutes deux terminées.</span><span class="sxs-lookup"><span data-stu-id="306f6-166">Activity3 starts only after both Activity1 and Activity2 have completed.</span></span>

    Parallel
    {
      <Activity1>
      <Activity2>
    }
    <Activity3>


<span data-ttu-id="306f6-167">Par exemple, considérez hello suivant les commandes PowerShell qui copie plusieurs fichiers destination réseau tooa.</span><span class="sxs-lookup"><span data-stu-id="306f6-167">For example, consider hello following PowerShell commands that copy multiple files tooa network destination.</span></span>  <span data-ttu-id="306f6-168">Ces commandes sont exécutées de manière séquentielle afin qu’un fichier doit se terminer copie avant hello est redémarrée.</span><span class="sxs-lookup"><span data-stu-id="306f6-168">These commands are run sequentially so that one file must finish copying before hello next is started.</span></span>     

    Copy-Item -Path C:\LocalPath\File1.txt -Destination \\NetworkPath\File1.txt
    Copy-Item -Path C:\LocalPath\File2.txt -Destination \\NetworkPath\File2.txt
    Copy-Item -Path C:\LocalPath\File3.txt -Destination \\NetworkPath\File3.txt

<span data-ttu-id="306f6-169">Hello suivant du flux de travail exécute ces mêmes commandes en parallèle afin que tous les démarrer la copie à hello même temps.</span><span class="sxs-lookup"><span data-stu-id="306f6-169">hello following workflow runs these same commands in parallel so that they all start copying at hello same time.</span></span>  <span data-ttu-id="306f6-170">Uniquement une fois qu’ils sont tous copiés message d’achèvement hello apparaît.</span><span class="sxs-lookup"><span data-stu-id="306f6-170">Only after they are all copied is hello completion message displayed.</span></span>

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


<span data-ttu-id="306f6-171">Vous pouvez utiliser hello **ForEach-Parallel** construire des commandes tooprocess pour chaque élément dans une collection simultanément.</span><span class="sxs-lookup"><span data-stu-id="306f6-171">You can use hello **ForEach -Parallel** construct tooprocess commands for each item in a collection concurrently.</span></span> <span data-ttu-id="306f6-172">éléments Hello dans la collection de hello sont traités en parallèle pendant l’exécutent des commandes hello dans le bloc de script hello séquentiellement.</span><span class="sxs-lookup"><span data-stu-id="306f6-172">hello items in hello collection are processed in parallel while hello commands in hello script block run sequentially.</span></span> <span data-ttu-id="306f6-173">Cette méthode utilise hello selon la syntaxe ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="306f6-173">This uses hello following syntax shown below.</span></span> <span data-ttu-id="306f6-174">Dans ce cas, Activity1 commence hello la même heure pour tous les éléments de collection de hello.</span><span class="sxs-lookup"><span data-stu-id="306f6-174">In this case, Activity1 starts at hello same time for all items in hello collection.</span></span> <span data-ttu-id="306f6-175">Pour chaque élément, Activity2 démarre une fois Activity1 terminée.</span><span class="sxs-lookup"><span data-stu-id="306f6-175">For each item, Activity2 starts after Activity1 is complete.</span></span> <span data-ttu-id="306f6-176">Activity3 démarre uniquement quand Activity1 et Activity2 sont toutes deux terminées pour tous les éléments.</span><span class="sxs-lookup"><span data-stu-id="306f6-176">Activity3 starts only after both Activity1 and Activity2 have completed for all items.</span></span>

    ForEach -Parallel ($<item> in $<collection>)
    {
      <Activity1>
      <Activity2>
    }
    <Activity3>

<span data-ttu-id="306f6-177">Bonjour à l’exemple suivant est similaire exemple précédent toohello copie des fichiers en parallèle.</span><span class="sxs-lookup"><span data-stu-id="306f6-177">hello following example is similar toohello previous example copying files in parallel.</span></span>  <span data-ttu-id="306f6-178">Dans ce cas, un message s'affiche pour chaque fichier après la copie.</span><span class="sxs-lookup"><span data-stu-id="306f6-178">In this case, a message is displayed for each file after it copies.</span></span>  <span data-ttu-id="306f6-179">Uniquement une fois qu’ils sont tous complètement copié message d’achèvement finale hello apparaît.</span><span class="sxs-lookup"><span data-stu-id="306f6-179">Only after they are all completely copied is hello final completion message displayed.</span></span>

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
> <span data-ttu-id="306f6-180">Nous vous déconseillons d’exécution des runbooks enfants en parallèle, car il a été prouvé toogive produisent des résultats incertains.</span><span class="sxs-lookup"><span data-stu-id="306f6-180">We do not recommend running child runbooks in parallel since this has been shown toogive unreliable results.</span></span>  <span data-ttu-id="306f6-181">Hello sortie du runbook parfois de hello enfant ne s’affiche pas, et peuvent affecter les paramètres dans un seul enfant runbook hello autres procédures opérationnelles enfant parallèle</span><span class="sxs-lookup"><span data-stu-id="306f6-181">hello output from hello child runbook sometimes does not show up, and settings in one child runbook can affect hello other parallel child runbooks</span></span>
>

## <a name="checkpoints"></a><span data-ttu-id="306f6-182">Points de contrôle</span><span class="sxs-lookup"><span data-stu-id="306f6-182">Checkpoints</span></span>
<span data-ttu-id="306f6-183">A *point de contrôle* est un instantané de l’état actuel de hello du flux de travail hello qui inclut la valeur actuelle de hello pour les variables et toute sortie est généré toothat point.</span><span class="sxs-lookup"><span data-stu-id="306f6-183">A *checkpoint* is a snapshot of hello current state of hello workflow that includes hello current value for variables and any output generated toothat point.</span></span> <span data-ttu-id="306f6-184">Si un flux de travail se termine par erreur ou est interrompu, puis hello prochaine exécution qu’il démarre à partir de son dernier point de contrôle au lieu de démarrer hello de travail de sous-découpage hello.</span><span class="sxs-lookup"><span data-stu-id="306f6-184">If a workflow ends in error or is suspended, then hello next time it is run it will start from its last checkpoint instead of hello start of hello worfklow.</span></span>  <span data-ttu-id="306f6-185">Vous pouvez définir un point de contrôle dans un flux de travail avec hello **Checkpoint-Workflow** activité.</span><span class="sxs-lookup"><span data-stu-id="306f6-185">You can set a checkpoint in a workflow with hello **Checkpoint-Workflow** activity.</span></span>

<span data-ttu-id="306f6-186">Bonjour suivant l’exemple de code, une exception se produit après Activity2 à l’origine hello tooend de flux de travail.</span><span class="sxs-lookup"><span data-stu-id="306f6-186">In hello following sample code, an exception occurs after Activity2 causing hello workflow tooend.</span></span> <span data-ttu-id="306f6-187">Flux de travail hello est exécuté à nouveau, il commence par exécuter Activity2 puisqu’il s’agissait juste après que le dernier point de contrôle hello définie.</span><span class="sxs-lookup"><span data-stu-id="306f6-187">When hello workflow is run again, it starts by running Activity2 since this was just after hello last checkpoint set.</span></span>

    <Activity1>
    Checkpoint-Workflow
    <Activity2>
    <Exception>
    <Activity3>

<span data-ttu-id="306f6-188">Vous devez définir des points de contrôle dans un flux de travail une fois que les activités qui peuvent être sujette tooexception et ne doivent pas être répété si le flux de travail hello reprend.</span><span class="sxs-lookup"><span data-stu-id="306f6-188">You should set checkpoints in a workflow after activities that may be prone tooexception and should not be repeated if hello workflow is resumed.</span></span> <span data-ttu-id="306f6-189">Par exemple, votre workflow peut créer une machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="306f6-189">For example, your workflow may create a virtual machine.</span></span> <span data-ttu-id="306f6-190">Vous pouvez définir un point de contrôle avant et après l’ordinateur virtuel de hello commandes toocreate hello.</span><span class="sxs-lookup"><span data-stu-id="306f6-190">You could set a checkpoint both before and after hello commands toocreate hello virtual machine.</span></span> <span data-ttu-id="306f6-191">En cas de création de hello, commandes hello sont répétés si le flux de travail hello est démarrée à nouveau.</span><span class="sxs-lookup"><span data-stu-id="306f6-191">If hello creation fails, then hello commands would be repeated if hello workflow is started again.</span></span> <span data-ttu-id="306f6-192">Si le travail de sous-découpage hello échoue après que la création d’hello réussit, puis hello ordinateur virtuel ne sera pas créé à nouveau lors de la reprise du workflow hello.</span><span class="sxs-lookup"><span data-stu-id="306f6-192">If hello worfklow fails after hello creation succeeds, then hello virtual machine will not be created again when hello workflow is resumed.</span></span>

<span data-ttu-id="306f6-193">Bonjour à l’exemple suivant copie plusieurs fichiers tooa du réseau et définit un point de contrôle après chaque fichier.</span><span class="sxs-lookup"><span data-stu-id="306f6-193">hello following example copies multiple files tooa network location and sets a checkpoint after each file.</span></span>  <span data-ttu-id="306f6-194">Si l’emplacement de réseau hello est perdu, les flux de travail hello se termine par erreur.</span><span class="sxs-lookup"><span data-stu-id="306f6-194">If hello network location is lost, then hello workflow ends in error.</span></span>  <span data-ttu-id="306f6-195">Lorsqu’il est démarré à nouveau, il reprend au dernier point de contrôle hello ce qui signifie que que seuls les fichiers hello qui ont déjà été copiés sont ignorés.</span><span class="sxs-lookup"><span data-stu-id="306f6-195">When it is started again, it will resume at hello last checkpoint meaning that only hello files that have already been copied are skipped.</span></span>

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

<span data-ttu-id="306f6-196">Étant donné que les informations d’identification de nom d’utilisateur ne sont pas conservées après avoir appelé hello [Suspend-Workflow](https://technet.microsoft.com/library/jj733586.aspx) activité ou après hello dernier point de contrôle, vous devez toonull d’informations d’identification tooset hello, puis les extraire à nouveau hello asset magasin après  **Suspend-Workflow** ou point de contrôle est appelée.</span><span class="sxs-lookup"><span data-stu-id="306f6-196">Because username credentials are not persisted after you call hello [Suspend-Workflow](https://technet.microsoft.com/library/jj733586.aspx) activity or after hello last checkpoint, you need tooset hello credentials toonull and then retrieve them again from hello asset store after **Suspend-Workflow** or checkpoint is called.</span></span>  <span data-ttu-id="306f6-197">Dans le cas contraire, hello message d’erreur suivant peut s’afficher : *ne peut pas reprendre la tâche de flux de travail de hello, soit parce que les données de persistance est complètement enregistrées, ou enregistrées les données de persistance a été endommagées. Vous devez redémarrer le flux de travail hello.*</span><span class="sxs-lookup"><span data-stu-id="306f6-197">Otherwise, you may receive hello following error message: *hello workflow job cannot be resumed, either because persistence data could not be saved completely, or saved persistence data has been corrupted. You must restart hello workflow.*</span></span>

<span data-ttu-id="306f6-198">Hello suivant le même code montre comment toohandle cela dans vos runbook PowerShell Workflow.</span><span class="sxs-lookup"><span data-stu-id="306f6-198">hello following same code demonstrates how toohandle this in your PowerShell Workflow runbooks.</span></span>

    workflow CreateTestVms
    {
       $Cred = Get-AzureAutomationCredential -Name "MyCredential"
       $null = Add-AzureRmAccount -Credential $Cred

       $VmsToCreate = Get-AzureAutomationVariable -Name "VmsToCreate"

       foreach ($VmName in $VmsToCreate)
         {
          # Do work first toocreate hello VM (code not shown)

          # Now add hello VM
          New-AzureRmVm -VM $Vm -Location "WestUs" -ResourceGroupName "ResourceGroup01"

          # Checkpoint so that VM creation is not repeated if workflow suspends
          $Cred = $null
          Checkpoint-Workflow
          $Cred = Get-AzureAutomationCredential -Name "MyCredential"
          $null = Add-AzureRmAccount -Credential $Cred
         }
     }


<span data-ttu-id="306f6-199">Cette procédure n’est pas nécessaire si vous vous authentifiez à l’aide d’un compte d’identification configuré avec un service principal.</span><span class="sxs-lookup"><span data-stu-id="306f6-199">This is not required if you are authenticating using a Run As account configured with a service principal.</span></span>  

<span data-ttu-id="306f6-200">Pour plus d’informations sur les points de contrôle, consultez [tooa d’ajouter des points de contrôle du Workflow de Script](http://technet.microsoft.com/library/jj574114.aspx).</span><span class="sxs-lookup"><span data-stu-id="306f6-200">For more information about checkpoints, see [Adding Checkpoints tooa Script Workflow](http://technet.microsoft.com/library/jj574114.aspx).</span></span>

## <a name="next-steps"></a><span data-ttu-id="306f6-201">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="306f6-201">Next steps</span></span>
* <span data-ttu-id="306f6-202">tooget a démarré avec des runbooks de flux de travail PowerShell, consultez [mon premier runbook de flux de travail PowerShell](automation-first-runbook-textual.md)</span><span class="sxs-lookup"><span data-stu-id="306f6-202">tooget started with PowerShell workflow runbooks, see [My first PowerShell workflow runbook](automation-first-runbook-textual.md)</span></span>
