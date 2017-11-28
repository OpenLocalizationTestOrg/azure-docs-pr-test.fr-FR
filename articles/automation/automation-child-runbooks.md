---
title: Runbooks enfants dans Azure Automation | Microsoft Docs
description: "Décrit les différentes méthodes permettant le démarrage d’un Runbook à partir d’un autre Runbook dans Azure Automation et le partage d’informations entre eux."
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: 919887b9-43e2-4c16-883c-f81807fe37db
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/02/2017
ms.author: magoedte;bwren
ms.openlocfilehash: a605d278dbbda9613b91007ea6a7042403a7a6ff
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="child-runbooks-in-azure-automation"></a><span data-ttu-id="7647d-103">Runbooks enfants dans Azure Automation</span><span class="sxs-lookup"><span data-stu-id="7647d-103">Child runbooks in Azure Automation</span></span>
<span data-ttu-id="7647d-104">Dans Azure Automation, il est recommandé d’écrire des Runbooks réutilisables et modulaires avec une fonction discrète qui peut être utilisée par d’autres Runbooks.</span><span class="sxs-lookup"><span data-stu-id="7647d-104">It is a best practice in Azure Automation to write reusable, modular runbooks with a discrete function that can be used by other runbooks.</span></span> <span data-ttu-id="7647d-105">Un Runbook parent appelle souvent un ou plusieurs Runbooks enfants pour exécuter la fonctionnalité requise.</span><span class="sxs-lookup"><span data-stu-id="7647d-105">A parent runbook will often call one or more child runbooks to perform required functionality.</span></span> <span data-ttu-id="7647d-106">Il existe deux méthodes pour appeler un Runbook enfant. Vous devez comprendre leurs spécificités afin de déterminer celle répondant le mieux aux exigences de chacun de vos scénarios.</span><span class="sxs-lookup"><span data-stu-id="7647d-106">There are two ways to call a child runbook, and each has distinct differences that you should understand so that you can determine which will be best for your different scenarios.</span></span>

## <a name="invoking-a-child-runbook-using-inline-execution"></a><span data-ttu-id="7647d-107">Appeler un Runbook enfant à l’aide de l’exécution en ligne</span><span class="sxs-lookup"><span data-stu-id="7647d-107">Invoking a child runbook using inline execution</span></span>
<span data-ttu-id="7647d-108">Pour appeler un Runbook en ligne à partir d’un autre Runbook, vous utilisez le nom du Runbook et définissez des valeurs pour ses paramètres de la même façon qu’avec une activité ou une applet de commande.</span><span class="sxs-lookup"><span data-stu-id="7647d-108">To invoke a runbook inline from another runbook, you use the name of the runbook and provide values for its parameters exactly like you would use an activity or cmdlet.</span></span>  <span data-ttu-id="7647d-109">Tous les Runbooks d’un même compte Automation peuvent être utilisés ainsi par les autres Runbooks.</span><span class="sxs-lookup"><span data-stu-id="7647d-109">All runbooks in the same Automation account are available to all others to be used in this manner.</span></span> <span data-ttu-id="7647d-110">Le Runbook parent attend la fin de l’exécution du Runbook enfant avant de passer à la ligne suivante, et toute sortie est retournée directement au parent.</span><span class="sxs-lookup"><span data-stu-id="7647d-110">The parent runbook will wait for the child runbook to complete before moving to the next line, and any output is returned directly to the parent.</span></span>

<span data-ttu-id="7647d-111">Lorsque vous appelez un Runbook en ligne, il est exécuté dans la même tâche que le Runbook parent.</span><span class="sxs-lookup"><span data-stu-id="7647d-111">When you invoke a runbook inline, it runs in the same job as the parent runbook.</span></span> <span data-ttu-id="7647d-112">L’historique des tâches du Runbook enfant n’indique pas qu’il a été exécuté.</span><span class="sxs-lookup"><span data-stu-id="7647d-112">There will be no indication in the job history of the child runbook that it ran.</span></span> <span data-ttu-id="7647d-113">Toutes les exceptions et sorties de flux issues du Runbook enfant seront associées au parent.</span><span class="sxs-lookup"><span data-stu-id="7647d-113">Any exceptions and any stream output from the child runbook will be associated with the parent.</span></span> <span data-ttu-id="7647d-114">Cela réduit le nombre de tâches et simplifie leur suivi, ainsi que la résolution des problèmes. En effet, toutes les exceptions lancées par le Runbook enfant et toute sortie de flux correspondante sont associées à la tâche du parent.</span><span class="sxs-lookup"><span data-stu-id="7647d-114">This results in fewer jobs and makes them easier to track and to troubleshoot since any exceptions thrown by the child runbook and any of its stream output are associated with the parent job.</span></span>

<span data-ttu-id="7647d-115">Lorsqu’un Runbook est publié, les Runbooks enfants qu’il appelle doivent déjà être publiés.</span><span class="sxs-lookup"><span data-stu-id="7647d-115">When a runbook is published, any child runbooks that it calls must already be published.</span></span> <span data-ttu-id="7647d-116">En effet, Azure Automation crée une association avec tous les Runbooks enfants lorsqu’un Runbook est compilé.</span><span class="sxs-lookup"><span data-stu-id="7647d-116">This is because Azure Automation builds an association with any child runbooks when a runbook is compiled.</span></span> <span data-ttu-id="7647d-117">Si ce n’est pas le cas, la publication du Runbook parent semblera correcte, mais le Runbook générera une exception au démarrage.</span><span class="sxs-lookup"><span data-stu-id="7647d-117">If they aren’t, the parent runbook will appear to publish properly, but will generate an exception when it’s started.</span></span> <span data-ttu-id="7647d-118">Dans ce cas, vous pouvez republier le Runbook parent pour référencer correctement les Runbooks enfants.</span><span class="sxs-lookup"><span data-stu-id="7647d-118">If this happens, you can republish the parent runbook in order to properly reference the child runbooks.</span></span> <span data-ttu-id="7647d-119">Il est inutile de republier le Runbook parent si des Runbooks enfants sont modifiés, car l’association aura déjà été créée.</span><span class="sxs-lookup"><span data-stu-id="7647d-119">You do not need to republish the parent runbook if any of the child runbooks are changed because the association will have already been created.</span></span>

<span data-ttu-id="7647d-120">Les paramètres d’un Runbook enfant appelé en ligne peuvent correspondre à n’importe quel type de données, y compris des objets complexes. Aucune [sérialisation JSON](automation-starting-a-runbook.md#runbook-parameters) n’intervient, comme c’est le cas quand vous démarrez le Runbook à l’aide du Portail de gestion Azure ou de l’applet de commande Start-AzureRmAutomationRunbook.</span><span class="sxs-lookup"><span data-stu-id="7647d-120">The parameters of a child runbook called inline can be any data type including complex objects, and there is no [JSON serialization](automation-starting-a-runbook.md#runbook-parameters) as there is when you start the runbook using the Azure Management Portal or with the Start-AzureRmAutomationRunbook cmdlet.</span></span>

### <a name="runbook-types"></a><span data-ttu-id="7647d-121">Types de runbook</span><span class="sxs-lookup"><span data-stu-id="7647d-121">Runbook types</span></span>
<span data-ttu-id="7647d-122">Types pouvant s’appeler mutuellement :</span><span class="sxs-lookup"><span data-stu-id="7647d-122">Which types can call each other:</span></span>

* <span data-ttu-id="7647d-123">Un [runbook PowerShell](automation-runbook-types.md#powershell-runbooks) et des [runbooks graphiques](automation-runbook-types.md#graphical-runbooks) peuvent s’appeler mutuellement en ligne (les deux sont basés sur PowerShell).</span><span class="sxs-lookup"><span data-stu-id="7647d-123">A [PowerShell runbook](automation-runbook-types.md#powershell-runbooks) and [Graphical runbooks](automation-runbook-types.md#graphical-runbooks) can call each other inline (both are PowerShell based).</span></span>
* <span data-ttu-id="7647d-124">Un [runbook PowerShell Workflow](automation-runbook-types.md#powershell-workflow-runbooks) et des runbooks PowerShell Workflow graphiques peuvent s’appeler mutuellement en ligne (les deux sont basé sur PowerShell)</span><span class="sxs-lookup"><span data-stu-id="7647d-124">A [PowerShell Workflow runbook](automation-runbook-types.md#powershell-workflow-runbooks) and Graphical PowerShell Workflow runbooks can call each other inline (both are PowerShell Workflow based)</span></span>
* <span data-ttu-id="7647d-125">Les types PowerShell et PowerShell Workflow ne peuvent pas s’appeler mutuellement en ligne doivent utiliser Start-AzureRmAutomationRunbook.</span><span class="sxs-lookup"><span data-stu-id="7647d-125">The PowerShell types and the PowerShell Workflow types can’t call each other inline, and must use Start-AzureRmAutomationRunbook.</span></span>

<span data-ttu-id="7647d-126">Pertinence de l’ordre de publication :</span><span class="sxs-lookup"><span data-stu-id="7647d-126">When does publish order matter:</span></span>

* <span data-ttu-id="7647d-127">L’ordre de publication de runbooks n’est important que pour les runbooks PowerShell Workflow et les runbooks graphiques PowerShell.</span><span class="sxs-lookup"><span data-stu-id="7647d-127">The publish order of runbooks only matters for PowerShell Workflow and Graphical PowerShell Workflow runbooks.</span></span>

<span data-ttu-id="7647d-128">Lorsque vous appelez un runbook graphique ou PowerShell Workflow enfant à l’aide d’une exécution incorporée, vous utilisez simplement le nom du runbook.</span><span class="sxs-lookup"><span data-stu-id="7647d-128">When you call a Graphical or PowerShell Workflow child runbook using inline execution, you just use the name of the runbook.</span></span>  <span data-ttu-id="7647d-129">Lorsque vous appelez un runbook enfant de PowerShell, vous devez précédé son nom avec *.\\*  pour spécifier que le script se trouve dans le répertoire local.</span><span class="sxs-lookup"><span data-stu-id="7647d-129">When you call a PowerShell child runbook, you must preceded its name with *.\\* to specify that the script is located in the local directory.</span></span> 

### <a name="example"></a><span data-ttu-id="7647d-130">Exemple</span><span class="sxs-lookup"><span data-stu-id="7647d-130">Example</span></span>
<span data-ttu-id="7647d-131">Dans l’exemple suivant, on appelle un Runbook enfant de test qui accepte trois paramètres : un objet complexe, un entier et une valeur booléenne.</span><span class="sxs-lookup"><span data-stu-id="7647d-131">The following example invokes a test child runbook that accepts three parameters, a complex object, an integer, and a boolean.</span></span> <span data-ttu-id="7647d-132">La sortie du Runbook enfant est affectée à une variable.</span><span class="sxs-lookup"><span data-stu-id="7647d-132">The output of the child runbook is assigned to a variable.</span></span>  <span data-ttu-id="7647d-133">Dans ce cas, le runbook enfant est un runbook PowerShell Workflow</span><span class="sxs-lookup"><span data-stu-id="7647d-133">In this case, the child runbook is a PowerShell Workflow runbook</span></span>

    $vm = Get-AzureRmVM –ResourceGroupName "LabRG" –Name "MyVM"
    $output = PSWF-ChildRunbook –VM $vm –RepeatCount 2 –Restart $true

<span data-ttu-id="7647d-134">Voici le même exemple utilisant un runbook PowerShell en tant qu’enfant.</span><span class="sxs-lookup"><span data-stu-id="7647d-134">Following is the same example using a PowerShell runbook as the child.</span></span>

    $vm = Get-AzureRmVM –ResourceGroupName "LabRG" –Name "MyVM"
    $output = .\PS-ChildRunbook.ps1 –VM $vm –RepeatCount 2 –Restart $true


## <a name="starting-a-child-runbook-using-cmdlet"></a><span data-ttu-id="7647d-135">Démarrage d’un Runbook enfant à l’aide d’une applet de commande</span><span class="sxs-lookup"><span data-stu-id="7647d-135">Starting a child runbook using cmdlet</span></span>
<span data-ttu-id="7647d-136">Vous pouvez utiliser l’applet de commande [Start-AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603661.aspx) pour démarrer un runbook, comme décrit dans [Démarrage d’un Runbook avec Windows PowerShell](automation-starting-a-runbook.md#starting-a-runbook-with-windows-powershell).</span><span class="sxs-lookup"><span data-stu-id="7647d-136">You can use the [Start-AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603661.aspx) cmdlet to start a runbook as described in [To start a runbook with Windows PowerShell](automation-starting-a-runbook.md#starting-a-runbook-with-windows-powershell).</span></span> <span data-ttu-id="7647d-137">Il existe deux modes d’utilisation pour cette applet de commande.</span><span class="sxs-lookup"><span data-stu-id="7647d-137">There are two modes of use for this cmdlet.</span></span>  <span data-ttu-id="7647d-138">Dans un mode, l’applet de commande renvoie l’ID de tâche dès que la tâche enfant est créée pour le runbook enfant.</span><span class="sxs-lookup"><span data-stu-id="7647d-138">In one mode, the cmdlet returns the job id as soon as the child job is created for the child runbook.</span></span>  <span data-ttu-id="7647d-139">Dans l’autre mode, que vous activez en spécifiant le paramètre **-wait** , l’applet de commande attend que la tâche enfant se termine et renvoie la sortie du runbook enfant.</span><span class="sxs-lookup"><span data-stu-id="7647d-139">In the other mode, which you enable by specifying the **-wait** parameter, the cmdlet will wait until the child job finishes and will return the output from the child runbook.</span></span>

<span data-ttu-id="7647d-140">La tâche issue d’un Runbook enfant démarré avec une applet de commande est exécutée dans une tâche distincte du Runbook parent.</span><span class="sxs-lookup"><span data-stu-id="7647d-140">The job from a child runbook started with a cmdlet will run in a separate job from the parent runbook.</span></span> <span data-ttu-id="7647d-141">Cela entraîne davantage de tâches que l’appel de runbook en ligne et rend leur suivi plus complexe.</span><span class="sxs-lookup"><span data-stu-id="7647d-141">This results in more jobs than invoking the runbook inline and makes them more difficult to track.</span></span> <span data-ttu-id="7647d-142">Le parent peut démarrer plusieurs Runbooks enfants de façon asynchrone, sans attendre la fin de leur exécution.</span><span class="sxs-lookup"><span data-stu-id="7647d-142">The parent can start multiple child runbooks asynchronously without waiting for each to complete.</span></span> <span data-ttu-id="7647d-143">Pour ce même type d’exécution en parallèle avec appel des runbooks enfants en ligne, le runbook parent doit utiliser le [mot clé parallèle](automation-powershell-workflow.md#parallel-processing).</span><span class="sxs-lookup"><span data-stu-id="7647d-143">For that same kind of parallel execution calling the child runbooks inline, the parent runbook would need to use the [parallel keyword](automation-powershell-workflow.md#parallel-processing).</span></span>

<span data-ttu-id="7647d-144">Les paramètres d’un runbook enfant démarré avec une applet de commande sont fournis sous forme de table de hachage, comme décrit dans [Paramètres du runbook](automation-starting-a-runbook.md#runbook-parameters).</span><span class="sxs-lookup"><span data-stu-id="7647d-144">Parameters for a child runbook started with a cmdlet are provided as a hashtable as described in [Runbook Parameters](automation-starting-a-runbook.md#runbook-parameters).</span></span> <span data-ttu-id="7647d-145">Seuls les types de données simples peuvent être utilisés.</span><span class="sxs-lookup"><span data-stu-id="7647d-145">Only simple data types can be used.</span></span> <span data-ttu-id="7647d-146">Si le Runbook possède un paramètre avec un type de données complexe, il doit être appelé en ligne.</span><span class="sxs-lookup"><span data-stu-id="7647d-146">If the runbook has a parameter with a complex data type, then it must be called inline.</span></span>

### <a name="example"></a><span data-ttu-id="7647d-147">Exemple</span><span class="sxs-lookup"><span data-stu-id="7647d-147">Example</span></span>
<span data-ttu-id="7647d-148">Dans l’exemple suivant, un Runbook enfant avec paramètres est démarré et exécuté avec le paramètre Start-AzureRmAutomationRunbook -wait.</span><span class="sxs-lookup"><span data-stu-id="7647d-148">The following example starts a child runbook with parameters and then waits for it to complete using the Start-AzureRmAutomationRunbook -wait parameter.</span></span> <span data-ttu-id="7647d-149">À l’issue de l’exécution du Runbook, sa sortie est collectée à partir du runbook enfant.</span><span class="sxs-lookup"><span data-stu-id="7647d-149">Once completed, its output is collected from the child runbook.</span></span>

    $params = @{"VMName"="MyVM";"RepeatCount"=2;"Restart"=$true} 
    $joboutput = Start-AzureRmAutomationRunbook –AutomationAccountName "MyAutomationAccount" –Name "Test-ChildRunbook" -ResourceGroupName "LabRG" –Parameters $params –wait


## <a name="comparison-of-methods-for-calling-a-child-runbook"></a><span data-ttu-id="7647d-150">Comparaison des méthodes pour l’appel d’un Runbook enfant</span><span class="sxs-lookup"><span data-stu-id="7647d-150">Comparison of methods for calling a child runbook</span></span>
<span data-ttu-id="7647d-151">Le tableau suivant résume les différences entre les deux méthodes applicables pour appeler un Runbook à partir d’un autre Runbook.</span><span class="sxs-lookup"><span data-stu-id="7647d-151">The following table summarizes the differences between the two methods for calling a runbook from another runbook.</span></span>

|  | <span data-ttu-id="7647d-152">En ligne</span><span class="sxs-lookup"><span data-stu-id="7647d-152">Inline</span></span> | <span data-ttu-id="7647d-153">Applet de commande</span><span class="sxs-lookup"><span data-stu-id="7647d-153">Cmdlet</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="7647d-154">Travail</span><span class="sxs-lookup"><span data-stu-id="7647d-154">Job</span></span> |<span data-ttu-id="7647d-155">Les Runbooks enfants s’exécutent dans la même tâche que le parent.</span><span class="sxs-lookup"><span data-stu-id="7647d-155">Child runbooks run in the same job as the parent.</span></span> |<span data-ttu-id="7647d-156">Une tâche distincte est créée pour le Runbook enfant.</span><span class="sxs-lookup"><span data-stu-id="7647d-156">A separate job is created for the child runbook.</span></span> |
| <span data-ttu-id="7647d-157">Exécution</span><span class="sxs-lookup"><span data-stu-id="7647d-157">Execution</span></span> |<span data-ttu-id="7647d-158">Le Runbook parent attend la fin de l’exécution du Runbook enfant avant de se poursuivre.</span><span class="sxs-lookup"><span data-stu-id="7647d-158">Parent runbook waits for the child runbook to complete before continuing.</span></span> |<span data-ttu-id="7647d-159">Le runbook parent continue immédiatement après le démarrage du runbook enfant *ou* le runbook parent attend que la tâche enfant se termine.</span><span class="sxs-lookup"><span data-stu-id="7647d-159">Parent runbook continues immediately after child runbook is started *or* parent runbook waits for the child job to finish.</span></span> |
| <span data-ttu-id="7647d-160">Sortie</span><span class="sxs-lookup"><span data-stu-id="7647d-160">Output</span></span> |<span data-ttu-id="7647d-161">Le Runbook parent peut obtenir directement la sortie du Runbook enfant.</span><span class="sxs-lookup"><span data-stu-id="7647d-161">Parent runbook can directly get output from child runbook.</span></span> |<span data-ttu-id="7647d-162">Le runbook parent doit récupérer la sortie à partir de la tâche du runbook enfant *ou* le runbook parent peut obtenir directement la sortie du runbook enfant.</span><span class="sxs-lookup"><span data-stu-id="7647d-162">Parent runbook must retrieve output from child runbook job *or* parent runbook can directly get output from child runbook.</span></span> |
| <span data-ttu-id="7647d-163">Paramètres</span><span class="sxs-lookup"><span data-stu-id="7647d-163">Parameters</span></span> |<span data-ttu-id="7647d-164">Les valeurs des paramètres du Runbook enfant sont spécifiées séparément et peuvent utiliser n’importe quel type de données.</span><span class="sxs-lookup"><span data-stu-id="7647d-164">Values for the child runbook parameters are specified separately and can use any data type.</span></span> |<span data-ttu-id="7647d-165">Les valeurs des paramètres du Runbook enfant doivent être combinées dans une table de hachage unique et peuvent inclure uniquement des types de données simples, de tableau et d’objet exploitant la sérialisation JSON.</span><span class="sxs-lookup"><span data-stu-id="7647d-165">Values for the child runbook parameters must be combined into a single hashtable and can only include simple, array, and object data types that leverage JSON serialization.</span></span> |
| <span data-ttu-id="7647d-166">Compte Automation</span><span class="sxs-lookup"><span data-stu-id="7647d-166">Automation Account</span></span> |<span data-ttu-id="7647d-167">Le Runbook parent peut utiliser uniquement un Runbook enfant du même compte Automation.</span><span class="sxs-lookup"><span data-stu-id="7647d-167">Parent runbook can only use child runbook in the same automation account.</span></span> |<span data-ttu-id="7647d-168">Le Runbook parent peut utiliser un Runbook enfant de n’importe quel compte Automation du même abonnement Azure ou d’un autre abonnement si vous disposez de la connexion correspondante.</span><span class="sxs-lookup"><span data-stu-id="7647d-168">Parent runbook can use child runbook from any automation account from the same Azure subscription and even a different subscription if you have a connection to it.</span></span> |
| <span data-ttu-id="7647d-169">Publication</span><span class="sxs-lookup"><span data-stu-id="7647d-169">Publishing</span></span> |<span data-ttu-id="7647d-170">Le Runbook enfant doit être publié avant la publication du Runbook parent.</span><span class="sxs-lookup"><span data-stu-id="7647d-170">Child runbook must be published before parent runbook is published.</span></span> |<span data-ttu-id="7647d-171">Le Runbook enfant doit être publié avant le démarrage du Runbook parent.</span><span class="sxs-lookup"><span data-stu-id="7647d-171">Child runbook must be published any time before parent runbook is started.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="7647d-172">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="7647d-172">Next steps</span></span>
* [<span data-ttu-id="7647d-173">Démarrage d'un Runbook dans Azure Automation</span><span class="sxs-lookup"><span data-stu-id="7647d-173">Starting a runbook in Azure Automation</span></span>](automation-starting-a-runbook.md)
* [<span data-ttu-id="7647d-174">Sortie et messages de Runbook dans Azure Automation</span><span class="sxs-lookup"><span data-stu-id="7647d-174">Runbook output and messages in Azure Automation</span></span>](automation-runbook-output-and-messages.md)
