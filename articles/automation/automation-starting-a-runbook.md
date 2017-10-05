---
title: "Démarrage d’un Runbook dans Azure Automation | Microsoft Docs"
description: "Résume les différentes méthodes qui peuvent être utilisées pour démarrer un Runbook dans Azure Automation et fournit des détails sur l'utilisation du portail Azure et de Windows PowerShell."
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: 6ee756b4-9200-4eb2-9bda-ec156853803b
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/07/2017
ms.author: magoedte;bwren
ms.openlocfilehash: 844831b63d5263987ed05370125fbe9f01913ab9
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="starting-a-runbook-in-azure-automation"></a><span data-ttu-id="8ee88-103">Démarrage d'un Runbook dans Azure Automation</span><span class="sxs-lookup"><span data-stu-id="8ee88-103">Starting a runbook in Azure Automation</span></span>
<span data-ttu-id="8ee88-104">Le tableau suivant vous aide à déterminer la méthode de démarrage d'un Runbook dans Azure Automation la plus appropriée à votre scénario.</span><span class="sxs-lookup"><span data-stu-id="8ee88-104">The following table will help you determine the method to start a runbook in Azure Automation that is most suitable to your particular scenario.</span></span> <span data-ttu-id="8ee88-105">Cet article inclut des informations détaillées sur le démarrage d'un Runbook avec le portail Azure et avec Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="8ee88-105">This article includes details on starting a runbook with the Azure portal and with Windows PowerShell.</span></span> <span data-ttu-id="8ee88-106">Des informations supplémentaires sur les autres méthodes sont fournies dans différentes documentations accessibles depuis les liens ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="8ee88-106">Details on the other methods are provided in other documentation that you can access from the links below.</span></span>

| <span data-ttu-id="8ee88-107">**MÉTHODE**</span><span class="sxs-lookup"><span data-stu-id="8ee88-107">**METHOD**</span></span> | <span data-ttu-id="8ee88-108">**CARACTÉRISTIQUES**</span><span class="sxs-lookup"><span data-stu-id="8ee88-108">**CHARACTERISTICS**</span></span> |
| --- | --- |
| [<span data-ttu-id="8ee88-109">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="8ee88-109">Azure Portal</span></span>](#starting-a-runbook-with-the-azure-portal) |<li><span data-ttu-id="8ee88-110">Méthode la plus simple avec une interface utilisateur interactive.</span><span class="sxs-lookup"><span data-stu-id="8ee88-110">Simplest method with interactive user interface.</span></span><br> <li><span data-ttu-id="8ee88-111">Formulaire pour fournir les valeurs de paramètres simples.</span><span class="sxs-lookup"><span data-stu-id="8ee88-111">Form to provide simple parameter values.</span></span><br> <li><span data-ttu-id="8ee88-112">Suivi aisé de l'état des tâches.</span><span class="sxs-lookup"><span data-stu-id="8ee88-112">Easily track job state.</span></span><br> <li><span data-ttu-id="8ee88-113">Accès authentifié avec ouverture de session Azure.</span><span class="sxs-lookup"><span data-stu-id="8ee88-113">Access authenticated with Azure logon.</span></span> |
| [<span data-ttu-id="8ee88-114">Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="8ee88-114">Windows PowerShell</span></span>](https://msdn.microsoft.com/library/dn690259.aspx) |<li><span data-ttu-id="8ee88-115">Appel à partir de la ligne de commande avec les applets de commande Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="8ee88-115">Call from command line with Windows PowerShell cmdlets.</span></span><br> <li><span data-ttu-id="8ee88-116">Possibilité d'inclusion dans une solution automatisée à plusieurs étapes.</span><span class="sxs-lookup"><span data-stu-id="8ee88-116">Can be included in automated solution with multiple steps.</span></span><br> <li><span data-ttu-id="8ee88-117">Demande authentifiée avec un certificat ou un principal du service / principal d'utilisateur OAuth.</span><span class="sxs-lookup"><span data-stu-id="8ee88-117">Request is authenticated with certificate or OAuth user principal / service principal.</span></span><br> <li><span data-ttu-id="8ee88-118">Fourniture de valeurs de paramètres simples et complexes.</span><span class="sxs-lookup"><span data-stu-id="8ee88-118">Provide simple and complex parameter values.</span></span><br> <li><span data-ttu-id="8ee88-119">Suivi de l’état des tâches.</span><span class="sxs-lookup"><span data-stu-id="8ee88-119">Track job state.</span></span><br> <li><span data-ttu-id="8ee88-120">Client requis pour prendre en charge les applets de commande PowerShell.</span><span class="sxs-lookup"><span data-stu-id="8ee88-120">Client required to support PowerShell cmdlets.</span></span> |
| [<span data-ttu-id="8ee88-121">API Azure Automation</span><span class="sxs-lookup"><span data-stu-id="8ee88-121">Azure Automation API</span></span>](https://msdn.microsoft.com/library/azure/mt662285.aspx) |<li><span data-ttu-id="8ee88-122">Méthode la plus souple, mais également la plus complexe.</span><span class="sxs-lookup"><span data-stu-id="8ee88-122">Most flexible method but also most complex.</span></span><br> <li><span data-ttu-id="8ee88-123">Appel à partir de n'importe quel code personnalisé qui peut envoyer des requêtes HTTP.</span><span class="sxs-lookup"><span data-stu-id="8ee88-123">Call from any custom code that can make HTTP requests.</span></span><br> <li><span data-ttu-id="8ee88-124">Requête authentifiée avec un certificat ou un principal du service / principal d'utilisateur Oauth.</span><span class="sxs-lookup"><span data-stu-id="8ee88-124">Request authenticated with certificate, or Oauth user principal / service principal.</span></span><br> <li><span data-ttu-id="8ee88-125">Fourniture de valeurs de paramètres simples et complexes.</span><span class="sxs-lookup"><span data-stu-id="8ee88-125">Provide simple and complex parameter values.</span></span><br> <li><span data-ttu-id="8ee88-126">Suivi de l’état des tâches.</span><span class="sxs-lookup"><span data-stu-id="8ee88-126">Track job state.</span></span> |
| [<span data-ttu-id="8ee88-127">Webhooks</span><span class="sxs-lookup"><span data-stu-id="8ee88-127">Webhooks</span></span>](automation-webhooks.md) |<li><span data-ttu-id="8ee88-128">Démarrage d'un Runbook à partir d'une simple requête HTTP.</span><span class="sxs-lookup"><span data-stu-id="8ee88-128">Start runbook from single HTTP request.</span></span><br> <li><span data-ttu-id="8ee88-129">Authentification avec un jeton de sécurité dans l'URL.</span><span class="sxs-lookup"><span data-stu-id="8ee88-129">Authenticated with security token in URL.</span></span><br> <li><span data-ttu-id="8ee88-130">Le client ne peut pas remplacer les valeurs de paramètre spécifiées lors de la création du Webhook.</span><span class="sxs-lookup"><span data-stu-id="8ee88-130">Client cannot override parameter values specified when webhook created.</span></span> <span data-ttu-id="8ee88-131">Le Runbook peut définir un paramètre unique qui est rempli avec les détails de la requête HTTP.</span><span class="sxs-lookup"><span data-stu-id="8ee88-131">Runbook can define single parameter that is populated with the HTTP request details.</span></span><br> <li><span data-ttu-id="8ee88-132">Aucune possibilité de suivre l’état des tâches via l’URL du Webhook.</span><span class="sxs-lookup"><span data-stu-id="8ee88-132">No ability to track job state through webhook URL.</span></span> |
| [<span data-ttu-id="8ee88-133">Répondre à une alerte Azure</span><span class="sxs-lookup"><span data-stu-id="8ee88-133">Respond to Azure Alert</span></span>](../log-analytics/log-analytics-alerts.md) |<li><span data-ttu-id="8ee88-134">Démarrer un Runbook en réponse à une alerte Azure.</span><span class="sxs-lookup"><span data-stu-id="8ee88-134">Start a runbook in response to Azure alert.</span></span><br> <li><span data-ttu-id="8ee88-135">Configurer webhook pour Runbook et lien vers l'alerte.</span><span class="sxs-lookup"><span data-stu-id="8ee88-135">Configure webhook for runbook and link to alert.</span></span><br> <li><span data-ttu-id="8ee88-136">Authentification avec un jeton de sécurité dans l'URL.</span><span class="sxs-lookup"><span data-stu-id="8ee88-136">Authenticated with security token in URL.</span></span> |
| [<span data-ttu-id="8ee88-137">Planification</span><span class="sxs-lookup"><span data-stu-id="8ee88-137">Schedule</span></span>](automation-schedules.md) |<li><span data-ttu-id="8ee88-138">Démarrage automatique du runbook selon une planification horaire, quotidienne, hebdomadaire ou mensuelle.</span><span class="sxs-lookup"><span data-stu-id="8ee88-138">Automatically start runbook on hourly, daily, weekly, or monthly schedule.</span></span><br> <li><span data-ttu-id="8ee88-139">Manipulation de la planification via le portail Azure, les applets de commande PowerShell ou les API Azure.</span><span class="sxs-lookup"><span data-stu-id="8ee88-139">Manipulate schedule through Azure portal, PowerShell cmdlets, or Azure API.</span></span><br> <li><span data-ttu-id="8ee88-140">Fourniture des valeurs de paramètres à utiliser avec la planification.</span><span class="sxs-lookup"><span data-stu-id="8ee88-140">Provide parameter values to be used with schedule.</span></span> |
| [<span data-ttu-id="8ee88-141">À partir d'un autre Runbook</span><span class="sxs-lookup"><span data-stu-id="8ee88-141">From Another Runbook</span></span>](automation-child-runbooks.md) |<li><span data-ttu-id="8ee88-142">Utilisation d’un Runbook en tant qu’activité d’un autre Runbook.</span><span class="sxs-lookup"><span data-stu-id="8ee88-142">Use a runbook as an activity in another runbook.</span></span><br> <li><span data-ttu-id="8ee88-143">Utile pour les fonctionnalités utilisées par plusieurs Runbooks.</span><span class="sxs-lookup"><span data-stu-id="8ee88-143">Useful for functionality used by multiple runbooks.</span></span><br> <li><span data-ttu-id="8ee88-144">Fourniture des valeurs de paramètres au Runbook enfant et utilisation de la sortie dans le Runbook parent.</span><span class="sxs-lookup"><span data-stu-id="8ee88-144">Provide parameter values to child runbook and use output in parent runbook.</span></span> |

<span data-ttu-id="8ee88-145">L’image suivante illustre le processus détaillé du cycle de vie d’un Runbook.</span><span class="sxs-lookup"><span data-stu-id="8ee88-145">The following image illustrates detailed step-by-step process in the life cycle of a runbook.</span></span> <span data-ttu-id="8ee88-146">Elle illustre différentes formes de démarrage d’un Runbook dans Azure Automation, les composants requis pour que Runbook Worker hybride exécute des Runbooks Azure Automation, ainsi que les interactions entre les différents composants.</span><span class="sxs-lookup"><span data-stu-id="8ee88-146">It includes different ways a runbook is started in Azure Automation, components required for Hybrid Runbook Worker to execute Azure Automation runbooks and interactions between different components.</span></span> <span data-ttu-id="8ee88-147">Pour en savoir plus sur l’exécution des Runbooks Automation dans votre centre de données, consultez l’article [Runbooks Workers hybrides](automation-hybrid-runbook-worker.md)</span><span class="sxs-lookup"><span data-stu-id="8ee88-147">To learn about executing Automation runbooks in your datacenter, refer to [hybrid runbook workers](automation-hybrid-runbook-worker.md)</span></span>

![Architecture de runbook](media/automation-starting-runbook/runbooks-architecture.png)

## <a name="starting-a-runbook-with-the-azure-portal"></a><span data-ttu-id="8ee88-149">Démarrage d'un Runbook avec le portail Azure</span><span class="sxs-lookup"><span data-stu-id="8ee88-149">Starting a runbook with the Azure portal</span></span>
1. <span data-ttu-id="8ee88-150">Dans le portail Azure, sélectionnez **Automation** , puis cliquez sur le nom d'un compte Automation.</span><span class="sxs-lookup"><span data-stu-id="8ee88-150">In the Azure portal, select **Automation** and then then click the name of an automation account.</span></span>
2. <span data-ttu-id="8ee88-151">Dans le menu Hub, sélectionnez **Runbooks**.</span><span class="sxs-lookup"><span data-stu-id="8ee88-151">On the Hub menu, select **Runbooks**.</span></span>
3. <span data-ttu-id="8ee88-152">Dans le panneau **Runbooks**, sélectionnez un runbook, puis cliquez sur **Démarrer**.</span><span class="sxs-lookup"><span data-stu-id="8ee88-152">On the **Runbooks** blade, select a runbook, and then click **Start**.</span></span>
4. <span data-ttu-id="8ee88-153">Si le Runbook possède des paramètres, vous devez fournir des valeurs avec une zone de texte pour chaque paramètre.</span><span class="sxs-lookup"><span data-stu-id="8ee88-153">If the runbook has parameters, you will be prompted to provide values with a text box for each parameter.</span></span> <span data-ttu-id="8ee88-154">Pour plus d'informations sur les paramètres, consultez [Paramètres du Runbook](#Runbook-parameters) ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="8ee88-154">See [Runbook Parameters](#Runbook-parameters) below for further details on parameters.</span></span>
5. <span data-ttu-id="8ee88-155">Dans le panneau **Tâche**, vous pouvez afficher l’état du travail du runbook.</span><span class="sxs-lookup"><span data-stu-id="8ee88-155">On the **Job** blade, you can view the status of the runbook job.</span></span>

## <a name="starting-a-runbook-with-windows-powershell"></a><span data-ttu-id="8ee88-156">Démarrage d'un Runbook avec Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="8ee88-156">Starting a runbook with Windows PowerShell</span></span>
<span data-ttu-id="8ee88-157">Vous pouvez utiliser l’applet de commande [Start-AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603661.aspx) pour démarrer un Runbook avec Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="8ee88-157">You can use the [Start-AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603661.aspx) to start a runbook with Windows PowerShell.</span></span> <span data-ttu-id="8ee88-158">L'exemple de code suivant démarre un Runbook appelé Test-Runbook.</span><span class="sxs-lookup"><span data-stu-id="8ee88-158">The following sample code starts a runbook called Test-Runbook.</span></span>

```
Start-AzureRmAutomationRunbook -AutomationAccountName "MyAutomationAccount" -Name "Test-Runbook" -ResourceGroupName "ResourceGroup01"
```

<span data-ttu-id="8ee88-159">Start-AzureRmAutomationRunbook retourne un objet de traitement que vous pouvez utiliser pour suivre son état une fois que le Runbook a démarré.</span><span class="sxs-lookup"><span data-stu-id="8ee88-159">Start-AzureRmAutomationRunbook returns a job object that you can use to track its status once the runbook is started.</span></span> <span data-ttu-id="8ee88-160">Vous pouvez ensuite utiliser cet objet de travail avec [Get-AzureRmAutomationJob](https://msdn.microsoft.com/library/mt619440.aspx) pour déterminer l’état du travail et avec [Get-AzureRmAutomationJobOutput](https://msdn.microsoft.com/library/mt603476.aspx) pour obtenir sa sortie.</span><span class="sxs-lookup"><span data-stu-id="8ee88-160">You can then use this job object with [Get-AzureRmAutomationJob](https://msdn.microsoft.com/library/mt619440.aspx) to determine the status of the job and [Get-AzureRmAutomationJobOutput](https://msdn.microsoft.com/library/mt603476.aspx) to get its output.</span></span> <span data-ttu-id="8ee88-161">L'exemple de code suivant démarre un Runbook appelé Test-Runbook, attend qu'il ait terminé, puis affiche sa sortie.</span><span class="sxs-lookup"><span data-stu-id="8ee88-161">The following sample code starts a runbook called Test-Runbook, waits until it has completed, and then displays its output.</span></span>

```
$runbookName = "Test-Runbook"
$ResourceGroup = "ResourceGroup01"
$AutomationAcct = "MyAutomationAccount"

$job = Start-AzureRmAutomationRunbook –AutomationAccountName $AutomationAcct -Name $runbookName -ResourceGroupName $ResourceGroup

$doLoop = $true
While ($doLoop) {
   $job = Get-AzureRmAutomationJob –AutomationAccountName $AutomationAcct -Id $job.JobId -ResourceGroupName $ResourceGroup
   $status = $job.Status
   $doLoop = (($status -ne "Completed") -and ($status -ne "Failed") -and ($status -ne "Suspended") -and ($status -ne "Stopped"))
}

Get-AzureRmAutomationJobOutput –AutomationAccountName $AutomationAcct -Id $job.JobId -ResourceGroupName $ResourceGroup –Stream Output
```

<span data-ttu-id="8ee88-162">Si le Runbook requiert des paramètres, vous devez les fournir comme [table de hachage](http://technet.microsoft.com/library/hh847780.aspx) où la clé de la table de hachage correspond au nom de paramètre et la valeur à la valeur du paramètre.</span><span class="sxs-lookup"><span data-stu-id="8ee88-162">If the runbook requires parameters, then you must provide them as a [hashtable](http://technet.microsoft.com/library/hh847780.aspx) where the key of the hashtable matches the parameter name and the value is the parameter value.</span></span> <span data-ttu-id="8ee88-163">L'exemple suivant montre comment démarrer un Runbook avec deux paramètres de chaîne nommés FirstName et LastName, un entier nommé RepeatCount et un paramètre booléen nommé Show.</span><span class="sxs-lookup"><span data-stu-id="8ee88-163">The following example shows how to start a runbook with two string parameters named FirstName and LastName, an integer named RepeatCount, and a boolean parameter named Show.</span></span> <span data-ttu-id="8ee88-164">Pour plus d'informations sur les paramètres, consultez [Paramètres du Runbook](#Runbook-parameters) .</span><span class="sxs-lookup"><span data-stu-id="8ee88-164">For additional information on parameters, see [Runbook Parameters](#Runbook-parameters) below.</span></span>

```
$params = @{"FirstName"="Joe";"LastName"="Smith";"RepeatCount"=2;"Show"=$true}
Start-AzureRmAutomationRunbook –AutomationAccountName "MyAutomationAccount" –Name "Test-Runbook" -ResourceGroupName "ResourceGroup01" –Parameters $params
```

## <a name="runbook-parameters"></a><span data-ttu-id="8ee88-165">Paramètres du Runbook</span><span class="sxs-lookup"><span data-stu-id="8ee88-165">Runbook parameters</span></span>
<span data-ttu-id="8ee88-166">Quand vous démarrez un Runbook à partir du portail Azure ou de Windows PowerShell, l’instruction est envoyée par le biais du service web Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="8ee88-166">When you start a runbook from the Azure Portal or Windows PowerShell, the instruction is sent through the Azure Automation web service.</span></span> <span data-ttu-id="8ee88-167">Ce service ne prend pas en charge les paramètres avec des types de données complexes.</span><span class="sxs-lookup"><span data-stu-id="8ee88-167">This service does not support parameters with complex data types.</span></span> <span data-ttu-id="8ee88-168">Si vous devez fournir une valeur pour un paramètre complexe, vous devez l’appeler en ligne à partir d’un autre Runbook, comme décrit dans [Runbooks enfants dans Azure Automation](automation-child-runbooks.md).</span><span class="sxs-lookup"><span data-stu-id="8ee88-168">If you need to provide a value for a complex parameter, then you must call it inline from another runbook as described in [Child runbooks in Azure Automation](automation-child-runbooks.md).</span></span>

<span data-ttu-id="8ee88-169">Le service web Azure Automation fournit des fonctionnalités spécifiques pour les paramètres en utilisant certains types de données comme décrit dans les sections suivantes.</span><span class="sxs-lookup"><span data-stu-id="8ee88-169">The Azure Automation web service will provide special functionality for parameters using certain data types as described in the following sections.</span></span>

### <a name="named-values"></a><span data-ttu-id="8ee88-170">Valeurs nommées</span><span class="sxs-lookup"><span data-stu-id="8ee88-170">Named values</span></span>
<span data-ttu-id="8ee88-171">Si le paramètre est un type de données [object], vous pouvez utiliser le format JSON suivant pour lui envoyer une liste de valeurs nommées : *{Nom1:'Valeur1', Nom2:'Valeur2', Nom3:'Valeur3'}*.</span><span class="sxs-lookup"><span data-stu-id="8ee88-171">If the parameter is data type [object], then you can use the following JSON format to send it a list of named values: *{Name1:'Value1', Name2:'Value2', Name3:'Value3'}*.</span></span> <span data-ttu-id="8ee88-172">Ces valeurs doivent avoir des types simples.</span><span class="sxs-lookup"><span data-stu-id="8ee88-172">These values must be simple types.</span></span> <span data-ttu-id="8ee88-173">Le Runbook reçoit le paramètre comme [PSCustomObject](https://msdn.microsoft.com/library/system.management.automation.pscustomobject%28v=vs.85%29.aspx) avec des propriétés correspondant à chaque valeur nommée.</span><span class="sxs-lookup"><span data-stu-id="8ee88-173">The runbook will receive the parameter as a [PSCustomObject](https://msdn.microsoft.com/library/system.management.automation.pscustomobject%28v=vs.85%29.aspx) with properties that correspond to each named value.</span></span>

<span data-ttu-id="8ee88-174">Considérez le Runbook de test suivant qui accepte un paramètre nommé user.</span><span class="sxs-lookup"><span data-stu-id="8ee88-174">Consider the following test runbook that accepts a parameter called user.</span></span>

```
Workflow Test-Parameters
{
   param (
      [Parameter(Mandatory=$true)][object]$user
   )
    $userObject = $user | ConvertFrom-JSON
    if ($userObject.Show) {
        foreach ($i in 1..$userObject.RepeatCount) {
            $userObject.FirstName
            $userObject.LastName
        }
    }
}
```

<span data-ttu-id="8ee88-175">Le texte suivant peut être utilisé pour le paramètre user.</span><span class="sxs-lookup"><span data-stu-id="8ee88-175">The following text could be used for the user parameter.</span></span>

```
{FirstName:'Joe',LastName:'Smith',RepeatCount:'2',Show:'True'}
```

<span data-ttu-id="8ee88-176">Il s'ensuit la sortie suivante.</span><span class="sxs-lookup"><span data-stu-id="8ee88-176">This results in the following output.</span></span>

```
Joe
Smith
Joe
Smith
```

### <a name="arrays"></a><span data-ttu-id="8ee88-177">Tableaux</span><span class="sxs-lookup"><span data-stu-id="8ee88-177">Arrays</span></span>
<span data-ttu-id="8ee88-178">Si le paramètre est un tableau comme [array] ou [string[]], vous pouvez utiliser le format JSON suivant pour lui envoyer une liste de valeurs : *[Valeur1,Valeur2,Valeur3]*.</span><span class="sxs-lookup"><span data-stu-id="8ee88-178">If the parameter is an array such as [array] or [string[]], then you can use the following JSON format to send it a list of values: *[Value1,Value2,Value3]*.</span></span> <span data-ttu-id="8ee88-179">Ces valeurs doivent avoir des types simples.</span><span class="sxs-lookup"><span data-stu-id="8ee88-179">These values must be simple types.</span></span>

<span data-ttu-id="8ee88-180">Considérez le Runbook de test suivant qui accepte un paramètre nommé *user*.</span><span class="sxs-lookup"><span data-stu-id="8ee88-180">Consider the following test runbook that accepts a parameter called *user*.</span></span>

```
Workflow Test-Parameters
{
   param (
      [Parameter(Mandatory=$true)][array]$user
   )
    if ($user[3]) {
        foreach ($i in 1..$user[2]) {
            $ user[0]
            $ user[1]
        }
    }
}
```

<span data-ttu-id="8ee88-181">Le texte suivant peut être utilisé pour le paramètre user.</span><span class="sxs-lookup"><span data-stu-id="8ee88-181">The following text could be used for the user parameter.</span></span>

```
["Joe","Smith",2,true]
```

<span data-ttu-id="8ee88-182">Il s'ensuit la sortie suivante.</span><span class="sxs-lookup"><span data-stu-id="8ee88-182">This results in the following output.</span></span>

```
Joe
Smith
Joe
Smith
```

### <a name="credentials"></a><span data-ttu-id="8ee88-183">Informations d'identification</span><span class="sxs-lookup"><span data-stu-id="8ee88-183">Credentials</span></span>
<span data-ttu-id="8ee88-184">Si le paramètre est un type de données **PSCredential**, vous pouvez fournir le nom d'une [ressource d'informations d'identification](automation-credentials.md)Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="8ee88-184">If the parameter is data type **PSCredential**, then you can provide the name of an Azure Automation [credential asset](automation-credentials.md).</span></span> <span data-ttu-id="8ee88-185">Le Runbook récupère la ressource d'informations d'identification portant le nom que vous spécifiez.</span><span class="sxs-lookup"><span data-stu-id="8ee88-185">The runbook will retrieve the credential with the name that you specify.</span></span>

<span data-ttu-id="8ee88-186">Considérez le Runbook de test suivant qui accepte un paramètre nommé credential.</span><span class="sxs-lookup"><span data-stu-id="8ee88-186">Consider the following test runbook that accepts a parameter called credential.</span></span>

```
Workflow Test-Parameters
{
   param (
      [Parameter(Mandatory=$true)][PSCredential]$credential
   )
   $credential.UserName
}
```

<span data-ttu-id="8ee88-187">Le texte suivant peut être utilisé pour le paramètre user en supposant qu'il existe une ressource d'informations d'identification nommée *My Credential*.</span><span class="sxs-lookup"><span data-stu-id="8ee88-187">The following text could be used for the user parameter assuming that there was a credential asset called *My Credential*.</span></span>

```
My Credential
```

<span data-ttu-id="8ee88-188">En supposant que le nom d'utilisateur des informations d'identification soit *jsmith*, il s'ensuit le résultat suivant.</span><span class="sxs-lookup"><span data-stu-id="8ee88-188">Assuming the username in the credential was *jsmith*, this results in the following output.</span></span>

```
jsmith
```

## <a name="next-steps"></a><span data-ttu-id="8ee88-189">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="8ee88-189">Next steps</span></span>
* <span data-ttu-id="8ee88-190">L’architecture des Runbooks dans cet article fournit une vue d’ensemble globale des ressources de gestion des Runbooks dans Azure et localement avec Runbook Worker hybride.</span><span class="sxs-lookup"><span data-stu-id="8ee88-190">The runbook architecture in current article provides a high-level overview of runbooks managing resources in Azure and on-premises with the Hybrid Runbook Worker.</span></span>  <span data-ttu-id="8ee88-191">Pour en savoir plus sur l’exécution des Runbooks Automation dans votre centre de données, consultez l’article [Runbooks Workers hybrides](automation-hybrid-runbook-worker.md).</span><span class="sxs-lookup"><span data-stu-id="8ee88-191">To learn about executing Automation runbooks in your datacenter, refer to [Hybrid Runbook Workers](automation-hybrid-runbook-worker.md).</span></span>
* <span data-ttu-id="8ee88-192">Pour en savoir plus sur la création de Runbooks modulaires à utiliser par d’autres Runbooks pour des fonctions spécifiques ou communes, consultez [Runbooks enfants](automation-child-runbooks.md).</span><span class="sxs-lookup"><span data-stu-id="8ee88-192">To learn more about the creating modular runbooks to be used by other runbooks for specific or common functions, refer to [Child Runbooks](automation-child-runbooks.md).</span></span>

