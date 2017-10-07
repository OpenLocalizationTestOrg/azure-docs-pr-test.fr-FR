---
title: aaaStarting un runbook dans Azure Automation | Documents Microsoft
description: "Résume hello différentes méthodes qui peuvent être utilisé toostart un runbook dans Azure Automation et fournit des détails sur l’utilisation des deux hello portail Azure et Windows PowerShell."
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
ms.openlocfilehash: e44bce5b56b8e803f9247fbb4f3d4db7ab35c913
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="starting-a-runbook-in-azure-automation"></a><span data-ttu-id="48e1e-103">Démarrage d'un Runbook dans Azure Automation</span><span class="sxs-lookup"><span data-stu-id="48e1e-103">Starting a runbook in Azure Automation</span></span>
<span data-ttu-id="48e1e-104">Hello tableau suivant vous aidera à déterminer hello méthode toostart un runbook dans Azure Automation qui est le scénario tooyour plus approprié.</span><span class="sxs-lookup"><span data-stu-id="48e1e-104">hello following table will help you determine hello method toostart a runbook in Azure Automation that is most suitable tooyour particular scenario.</span></span> <span data-ttu-id="48e1e-105">Cet article contient des informations sur le démarrage d’un runbook avec hello portail Azure et Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="48e1e-105">This article includes details on starting a runbook with hello Azure portal and with Windows PowerShell.</span></span> <span data-ttu-id="48e1e-106">Détails sur hello autres méthodes sont fournies dans les autres documentations auquel vous pouvez accéder à partir de liens hello ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="48e1e-106">Details on hello other methods are provided in other documentation that you can access from hello links below.</span></span>

| <span data-ttu-id="48e1e-107">**MÉTHODE**</span><span class="sxs-lookup"><span data-stu-id="48e1e-107">**METHOD**</span></span> | <span data-ttu-id="48e1e-108">**CARACTÉRISTIQUES**</span><span class="sxs-lookup"><span data-stu-id="48e1e-108">**CHARACTERISTICS**</span></span> |
| --- | --- |
| [<span data-ttu-id="48e1e-109">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="48e1e-109">Azure Portal</span></span>](#starting-a-runbook-with-the-azure-portal) |<li><span data-ttu-id="48e1e-110">Méthode la plus simple avec une interface utilisateur interactive.</span><span class="sxs-lookup"><span data-stu-id="48e1e-110">Simplest method with interactive user interface.</span></span><br> <li><span data-ttu-id="48e1e-111">Valeurs de paramètre simple formulaire tooprovide.</span><span class="sxs-lookup"><span data-stu-id="48e1e-111">Form tooprovide simple parameter values.</span></span><br> <li><span data-ttu-id="48e1e-112">Suivi aisé de l'état des tâches.</span><span class="sxs-lookup"><span data-stu-id="48e1e-112">Easily track job state.</span></span><br> <li><span data-ttu-id="48e1e-113">Accès authentifié avec ouverture de session Azure.</span><span class="sxs-lookup"><span data-stu-id="48e1e-113">Access authenticated with Azure logon.</span></span> |
| [<span data-ttu-id="48e1e-114">Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="48e1e-114">Windows PowerShell</span></span>](https://msdn.microsoft.com/library/dn690259.aspx) |<li><span data-ttu-id="48e1e-115">Appel à partir de la ligne de commande avec les applets de commande Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="48e1e-115">Call from command line with Windows PowerShell cmdlets.</span></span><br> <li><span data-ttu-id="48e1e-116">Possibilité d'inclusion dans une solution automatisée à plusieurs étapes.</span><span class="sxs-lookup"><span data-stu-id="48e1e-116">Can be included in automated solution with multiple steps.</span></span><br> <li><span data-ttu-id="48e1e-117">Demande authentifiée avec un certificat ou un principal du service / principal d'utilisateur OAuth.</span><span class="sxs-lookup"><span data-stu-id="48e1e-117">Request is authenticated with certificate or OAuth user principal / service principal.</span></span><br> <li><span data-ttu-id="48e1e-118">Fourniture de valeurs de paramètres simples et complexes.</span><span class="sxs-lookup"><span data-stu-id="48e1e-118">Provide simple and complex parameter values.</span></span><br> <li><span data-ttu-id="48e1e-119">Suivi de l’état des tâches.</span><span class="sxs-lookup"><span data-stu-id="48e1e-119">Track job state.</span></span><br> <li><span data-ttu-id="48e1e-120">Client requis toosupport applets de commande PowerShell.</span><span class="sxs-lookup"><span data-stu-id="48e1e-120">Client required toosupport PowerShell cmdlets.</span></span> |
| [<span data-ttu-id="48e1e-121">API Azure Automation</span><span class="sxs-lookup"><span data-stu-id="48e1e-121">Azure Automation API</span></span>](https://msdn.microsoft.com/library/azure/mt662285.aspx) |<li><span data-ttu-id="48e1e-122">Méthode la plus souple, mais également la plus complexe.</span><span class="sxs-lookup"><span data-stu-id="48e1e-122">Most flexible method but also most complex.</span></span><br> <li><span data-ttu-id="48e1e-123">Appel à partir de n'importe quel code personnalisé qui peut envoyer des requêtes HTTP.</span><span class="sxs-lookup"><span data-stu-id="48e1e-123">Call from any custom code that can make HTTP requests.</span></span><br> <li><span data-ttu-id="48e1e-124">Requête authentifiée avec un certificat ou un principal du service / principal d'utilisateur Oauth.</span><span class="sxs-lookup"><span data-stu-id="48e1e-124">Request authenticated with certificate, or Oauth user principal / service principal.</span></span><br> <li><span data-ttu-id="48e1e-125">Fourniture de valeurs de paramètres simples et complexes.</span><span class="sxs-lookup"><span data-stu-id="48e1e-125">Provide simple and complex parameter values.</span></span><br> <li><span data-ttu-id="48e1e-126">Suivi de l’état des tâches.</span><span class="sxs-lookup"><span data-stu-id="48e1e-126">Track job state.</span></span> |
| [<span data-ttu-id="48e1e-127">Webhooks</span><span class="sxs-lookup"><span data-stu-id="48e1e-127">Webhooks</span></span>](automation-webhooks.md) |<li><span data-ttu-id="48e1e-128">Démarrage d'un Runbook à partir d'une simple requête HTTP.</span><span class="sxs-lookup"><span data-stu-id="48e1e-128">Start runbook from single HTTP request.</span></span><br> <li><span data-ttu-id="48e1e-129">Authentification avec un jeton de sécurité dans l'URL.</span><span class="sxs-lookup"><span data-stu-id="48e1e-129">Authenticated with security token in URL.</span></span><br> <li><span data-ttu-id="48e1e-130">Le client ne peut pas remplacer les valeurs de paramètre spécifiées lors de la création du Webhook.</span><span class="sxs-lookup"><span data-stu-id="48e1e-130">Client cannot override parameter values specified when webhook created.</span></span> <span data-ttu-id="48e1e-131">Runbook peut définir un paramètre unique qui est rempli avec les détails de la demande HTTP hello.</span><span class="sxs-lookup"><span data-stu-id="48e1e-131">Runbook can define single parameter that is populated with hello HTTP request details.</span></span><br> <li><span data-ttu-id="48e1e-132">Aucun état de tâche tootrack possibilité via l’URL du webhook.</span><span class="sxs-lookup"><span data-stu-id="48e1e-132">No ability tootrack job state through webhook URL.</span></span> |
| [<span data-ttu-id="48e1e-133">Répondre tooAzure alerte</span><span class="sxs-lookup"><span data-stu-id="48e1e-133">Respond tooAzure Alert</span></span>](../log-analytics/log-analytics-alerts.md) |<li><span data-ttu-id="48e1e-134">Démarrer un runbook dans l’alerte tooAzure de réponse.</span><span class="sxs-lookup"><span data-stu-id="48e1e-134">Start a runbook in response tooAzure alert.</span></span><br> <li><span data-ttu-id="48e1e-135">Configurer le webhook pour le runbook et lier les tooalert.</span><span class="sxs-lookup"><span data-stu-id="48e1e-135">Configure webhook for runbook and link tooalert.</span></span><br> <li><span data-ttu-id="48e1e-136">Authentification avec un jeton de sécurité dans l'URL.</span><span class="sxs-lookup"><span data-stu-id="48e1e-136">Authenticated with security token in URL.</span></span> |
| [<span data-ttu-id="48e1e-137">Planification</span><span class="sxs-lookup"><span data-stu-id="48e1e-137">Schedule</span></span>](automation-schedules.md) |<li><span data-ttu-id="48e1e-138">Démarrage automatique du runbook selon une planification horaire, quotidienne, hebdomadaire ou mensuelle.</span><span class="sxs-lookup"><span data-stu-id="48e1e-138">Automatically start runbook on hourly, daily, weekly, or monthly schedule.</span></span><br> <li><span data-ttu-id="48e1e-139">Manipulation de la planification via le portail Azure, les applets de commande PowerShell ou les API Azure.</span><span class="sxs-lookup"><span data-stu-id="48e1e-139">Manipulate schedule through Azure portal, PowerShell cmdlets, or Azure API.</span></span><br> <li><span data-ttu-id="48e1e-140">Fournir toobe de valeurs de paramètre utilisée avec une planification.</span><span class="sxs-lookup"><span data-stu-id="48e1e-140">Provide parameter values toobe used with schedule.</span></span> |
| [<span data-ttu-id="48e1e-141">À partir d'un autre Runbook</span><span class="sxs-lookup"><span data-stu-id="48e1e-141">From Another Runbook</span></span>](automation-child-runbooks.md) |<li><span data-ttu-id="48e1e-142">Utilisation d’un Runbook en tant qu’activité d’un autre Runbook.</span><span class="sxs-lookup"><span data-stu-id="48e1e-142">Use a runbook as an activity in another runbook.</span></span><br> <li><span data-ttu-id="48e1e-143">Utile pour les fonctionnalités utilisées par plusieurs Runbooks.</span><span class="sxs-lookup"><span data-stu-id="48e1e-143">Useful for functionality used by multiple runbooks.</span></span><br> <li><span data-ttu-id="48e1e-144">Fournir des runbook de toochild de valeurs de paramètre et utiliser la sortie dans le runbook parent.</span><span class="sxs-lookup"><span data-stu-id="48e1e-144">Provide parameter values toochild runbook and use output in parent runbook.</span></span> |

<span data-ttu-id="48e1e-145">Hello image suivante illustre les processus pas à pas détaillé hello cycle de vie d’un runbook.</span><span class="sxs-lookup"><span data-stu-id="48e1e-145">hello following image illustrates detailed step-by-step process in hello life cycle of a runbook.</span></span> <span data-ttu-id="48e1e-146">Il inclut les différentes façons qu'un runbook est démarré dans Azure Automation, les composants requis pour les runbooks d’Azure Automation Runbook Worker hybride tooexecute et les interactions entre les différents composants.</span><span class="sxs-lookup"><span data-stu-id="48e1e-146">It includes different ways a runbook is started in Azure Automation, components required for Hybrid Runbook Worker tooexecute Azure Automation runbooks and interactions between different components.</span></span> <span data-ttu-id="48e1e-147">toolearn sur l’exécution des runbooks Automation dans votre centre de données, consultez trop[workers hybrides](automation-hybrid-runbook-worker.md)</span><span class="sxs-lookup"><span data-stu-id="48e1e-147">toolearn about executing Automation runbooks in your datacenter, refer too[hybrid runbook workers](automation-hybrid-runbook-worker.md)</span></span>

![Architecture de runbook](media/automation-starting-runbook/runbooks-architecture.png)

## <a name="starting-a-runbook-with-hello-azure-portal"></a><span data-ttu-id="48e1e-149">Démarrage d’un runbook avec hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="48e1e-149">Starting a runbook with hello Azure portal</span></span>
1. <span data-ttu-id="48e1e-150">Bonjour portail Azure, sélectionnez **Automation** , puis cliquez sur nom hello d’un compte automation.</span><span class="sxs-lookup"><span data-stu-id="48e1e-150">In hello Azure portal, select **Automation** and then then click hello name of an automation account.</span></span>
2. <span data-ttu-id="48e1e-151">Dans le menu du Hub hello, sélectionnez **Runbooks**.</span><span class="sxs-lookup"><span data-stu-id="48e1e-151">On hello Hub menu, select **Runbooks**.</span></span>
3. <span data-ttu-id="48e1e-152">Sur hello **Runbooks** panneau, sélectionnez un runbook, puis cliquez sur **Démarrer**.</span><span class="sxs-lookup"><span data-stu-id="48e1e-152">On hello **Runbooks** blade, select a runbook, and then click **Start**.</span></span>
4. <span data-ttu-id="48e1e-153">Si hello runbook possède des paramètres, vous serez valeurs tooprovide demandée avec une zone de texte pour chaque paramètre.</span><span class="sxs-lookup"><span data-stu-id="48e1e-153">If hello runbook has parameters, you will be prompted tooprovide values with a text box for each parameter.</span></span> <span data-ttu-id="48e1e-154">Pour plus d'informations sur les paramètres, consultez [Paramètres du Runbook](#Runbook-parameters) ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="48e1e-154">See [Runbook Parameters](#Runbook-parameters) below for further details on parameters.</span></span>
5. <span data-ttu-id="48e1e-155">Sur hello **travail** panneau, vous pouvez afficher le statut de hello de tâche du runbook hello.</span><span class="sxs-lookup"><span data-stu-id="48e1e-155">On hello **Job** blade, you can view hello status of hello runbook job.</span></span>

## <a name="starting-a-runbook-with-windows-powershell"></a><span data-ttu-id="48e1e-156">Démarrage d'un Runbook avec Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="48e1e-156">Starting a runbook with Windows PowerShell</span></span>
<span data-ttu-id="48e1e-157">Vous pouvez utiliser hello [Start-AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603661.aspx) toostart un runbook avec Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="48e1e-157">You can use hello [Start-AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603661.aspx) toostart a runbook with Windows PowerShell.</span></span> <span data-ttu-id="48e1e-158">Hello exemple de code suivant démarre un runbook appelé Test-Runbook.</span><span class="sxs-lookup"><span data-stu-id="48e1e-158">hello following sample code starts a runbook called Test-Runbook.</span></span>

```
Start-AzureRmAutomationRunbook -AutomationAccountName "MyAutomationAccount" -Name "Test-Runbook" -ResourceGroupName "ResourceGroup01"
```

<span data-ttu-id="48e1e-159">Retourne AzureRmAutomationRunbook de démarrer un travail de l’objet que vous pouvez utiliser tootrack son état une fois hello runbook est démarré.</span><span class="sxs-lookup"><span data-stu-id="48e1e-159">Start-AzureRmAutomationRunbook returns a job object that you can use tootrack its status once hello runbook is started.</span></span> <span data-ttu-id="48e1e-160">Vous pouvez ensuite utiliser cet objet de tâche avec [Get-AzureRmAutomationJob](https://msdn.microsoft.com/library/mt619440.aspx) état de hello toodetermine du travail de hello et [Get-AzureRmAutomationJobOutput](https://msdn.microsoft.com/library/mt603476.aspx) tooget sa sortie.</span><span class="sxs-lookup"><span data-stu-id="48e1e-160">You can then use this job object with [Get-AzureRmAutomationJob](https://msdn.microsoft.com/library/mt619440.aspx) toodetermine hello status of hello job and [Get-AzureRmAutomationJobOutput](https://msdn.microsoft.com/library/mt603476.aspx) tooget its output.</span></span> <span data-ttu-id="48e1e-161">Hello suivant l’exemple de code démarre un runbook appelé Test-Runbook, attend qu’il ait terminé, puis affiche sa sortie.</span><span class="sxs-lookup"><span data-stu-id="48e1e-161">hello following sample code starts a runbook called Test-Runbook, waits until it has completed, and then displays its output.</span></span>

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

<span data-ttu-id="48e1e-162">Si hello runbook nécessite des paramètres, vous devez lui fournir en tant qu’un [hashtable](http://technet.microsoft.com/library/hh847780.aspx) où la clé hello de table de hachage hello correspond au nom du paramètre hello et la valeur de hello est la valeur du paramètre hello.</span><span class="sxs-lookup"><span data-stu-id="48e1e-162">If hello runbook requires parameters, then you must provide them as a [hashtable](http://technet.microsoft.com/library/hh847780.aspx) where hello key of hello hashtable matches hello parameter name and hello value is hello parameter value.</span></span> <span data-ttu-id="48e1e-163">Hello suivant montre comment toostart un runbook avec deux paramètres de chaîne nommés FirstName et LastName, un entier nommé RepeatCount et un paramètre booléen nommé Show.</span><span class="sxs-lookup"><span data-stu-id="48e1e-163">hello following example shows how toostart a runbook with two string parameters named FirstName and LastName, an integer named RepeatCount, and a boolean parameter named Show.</span></span> <span data-ttu-id="48e1e-164">Pour plus d'informations sur les paramètres, consultez [Paramètres du Runbook](#Runbook-parameters) .</span><span class="sxs-lookup"><span data-stu-id="48e1e-164">For additional information on parameters, see [Runbook Parameters](#Runbook-parameters) below.</span></span>

```
$params = @{"FirstName"="Joe";"LastName"="Smith";"RepeatCount"=2;"Show"=$true}
Start-AzureRmAutomationRunbook –AutomationAccountName "MyAutomationAccount" –Name "Test-Runbook" -ResourceGroupName "ResourceGroup01" –Parameters $params
```

## <a name="runbook-parameters"></a><span data-ttu-id="48e1e-165">Paramètres du Runbook</span><span class="sxs-lookup"><span data-stu-id="48e1e-165">Runbook parameters</span></span>
<span data-ttu-id="48e1e-166">Lorsque vous démarrez un runbook à partir de hello portail Azure ou Windows PowerShell, instruction de hello est envoyée via hello service web Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="48e1e-166">When you start a runbook from hello Azure Portal or Windows PowerShell, hello instruction is sent through hello Azure Automation web service.</span></span> <span data-ttu-id="48e1e-167">Ce service ne prend pas en charge les paramètres avec des types de données complexes.</span><span class="sxs-lookup"><span data-stu-id="48e1e-167">This service does not support parameters with complex data types.</span></span> <span data-ttu-id="48e1e-168">Si vous avez besoin de tooprovide une valeur pour un paramètre complexe, vous devez l’appeler en ligne à partir d’un autre runbook comme décrit dans [runbooks enfants dans Azure Automation](automation-child-runbooks.md).</span><span class="sxs-lookup"><span data-stu-id="48e1e-168">If you need tooprovide a value for a complex parameter, then you must call it inline from another runbook as described in [Child runbooks in Azure Automation](automation-child-runbooks.md).</span></span>

<span data-ttu-id="48e1e-169">Hello service web Azure Automation fournit des fonctionnalités spéciales pour les paramètres utilisant certains types de données, comme décrit dans les sections suivantes de hello.</span><span class="sxs-lookup"><span data-stu-id="48e1e-169">hello Azure Automation web service will provide special functionality for parameters using certain data types as described in hello following sections.</span></span>

### <a name="named-values"></a><span data-ttu-id="48e1e-170">Valeurs nommées</span><span class="sxs-lookup"><span data-stu-id="48e1e-170">Named values</span></span>
<span data-ttu-id="48e1e-171">Si le paramètre hello est un type de données [object], puis vous pouvez utiliser hello suivant toosend du format JSON il une liste de valeurs nommées : *{nom1 : 'Valeur1', nom2 : 'Value2', Nom3 : 'Valeur3'}*.</span><span class="sxs-lookup"><span data-stu-id="48e1e-171">If hello parameter is data type [object], then you can use hello following JSON format toosend it a list of named values: *{Name1:'Value1', Name2:'Value2', Name3:'Value3'}*.</span></span> <span data-ttu-id="48e1e-172">Ces valeurs doivent avoir des types simples.</span><span class="sxs-lookup"><span data-stu-id="48e1e-172">These values must be simple types.</span></span> <span data-ttu-id="48e1e-173">Hello runbook reçoit paramètre hello comme un [PSCustomObject](https://msdn.microsoft.com/library/system.management.automation.pscustomobject%28v=vs.85%29.aspx) avec des propriétés qui correspondent tooeach valeur nommée.</span><span class="sxs-lookup"><span data-stu-id="48e1e-173">hello runbook will receive hello parameter as a [PSCustomObject](https://msdn.microsoft.com/library/system.management.automation.pscustomobject%28v=vs.85%29.aspx) with properties that correspond tooeach named value.</span></span>

<span data-ttu-id="48e1e-174">Envisagez de hello suivant runbook de test qui accepte un paramètre utilisateur.</span><span class="sxs-lookup"><span data-stu-id="48e1e-174">Consider hello following test runbook that accepts a parameter called user.</span></span>

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

<span data-ttu-id="48e1e-175">Hello texte suivant peut être utilisé pour le paramètre de l’utilisateur hello.</span><span class="sxs-lookup"><span data-stu-id="48e1e-175">hello following text could be used for hello user parameter.</span></span>

```
{FirstName:'Joe',LastName:'Smith',RepeatCount:'2',Show:'True'}
```

<span data-ttu-id="48e1e-176">Cela entraîne hello suivant de sortie.</span><span class="sxs-lookup"><span data-stu-id="48e1e-176">This results in hello following output.</span></span>

```
Joe
Smith
Joe
Smith
```

### <a name="arrays"></a><span data-ttu-id="48e1e-177">Tableaux</span><span class="sxs-lookup"><span data-stu-id="48e1e-177">Arrays</span></span>
<span data-ttu-id="48e1e-178">Si le paramètre hello est un tableau tel que [array] ou [string []], vous pouvez ensuite utiliser hello suivant toosend du format JSON une liste de valeurs : *[valeur1, valeur2, valeur3]*.</span><span class="sxs-lookup"><span data-stu-id="48e1e-178">If hello parameter is an array such as [array] or [string[]], then you can use hello following JSON format toosend it a list of values: *[Value1,Value2,Value3]*.</span></span> <span data-ttu-id="48e1e-179">Ces valeurs doivent avoir des types simples.</span><span class="sxs-lookup"><span data-stu-id="48e1e-179">These values must be simple types.</span></span>

<span data-ttu-id="48e1e-180">Envisagez de hello suivant runbook de test qui accepte un paramètre appelé *utilisateur*.</span><span class="sxs-lookup"><span data-stu-id="48e1e-180">Consider hello following test runbook that accepts a parameter called *user*.</span></span>

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

<span data-ttu-id="48e1e-181">Hello texte suivant peut être utilisé pour le paramètre de l’utilisateur hello.</span><span class="sxs-lookup"><span data-stu-id="48e1e-181">hello following text could be used for hello user parameter.</span></span>

```
["Joe","Smith",2,true]
```

<span data-ttu-id="48e1e-182">Cela entraîne hello suivant de sortie.</span><span class="sxs-lookup"><span data-stu-id="48e1e-182">This results in hello following output.</span></span>

```
Joe
Smith
Joe
Smith
```

### <a name="credentials"></a><span data-ttu-id="48e1e-183">Informations d'identification</span><span class="sxs-lookup"><span data-stu-id="48e1e-183">Credentials</span></span>
<span data-ttu-id="48e1e-184">Si le paramètre hello est le type de données **PSCredential**, vous pouvez fournir le nom hello d’une automatisation Azure [actif d’informations d’identification](automation-credentials.md).</span><span class="sxs-lookup"><span data-stu-id="48e1e-184">If hello parameter is data type **PSCredential**, then you can provide hello name of an Azure Automation [credential asset](automation-credentials.md).</span></span> <span data-ttu-id="48e1e-185">Hello runbook récupère des informations d’identification hello nom hello que vous spécifiez.</span><span class="sxs-lookup"><span data-stu-id="48e1e-185">hello runbook will retrieve hello credential with hello name that you specify.</span></span>

<span data-ttu-id="48e1e-186">Envisagez de hello suivant runbook de test qui accepte un paramètre appelé des informations d’identification.</span><span class="sxs-lookup"><span data-stu-id="48e1e-186">Consider hello following test runbook that accepts a parameter called credential.</span></span>

```
Workflow Test-Parameters
{
   param (
      [Parameter(Mandatory=$true)][PSCredential]$credential
   )
   $credential.UserName
}
```

<span data-ttu-id="48e1e-187">Hello texte suivant peut être utilisé pour le paramètre de l’utilisateur hello en supposant qu’il existe une ressource d’informations d’identification appelée *My Credential*.</span><span class="sxs-lookup"><span data-stu-id="48e1e-187">hello following text could be used for hello user parameter assuming that there was a credential asset called *My Credential*.</span></span>

```
My Credential
```

<span data-ttu-id="48e1e-188">En supposant que le nom d’utilisateur hello dans informations d’identification hello a été *jsmith*, cela entraîne hello suivant de sortie.</span><span class="sxs-lookup"><span data-stu-id="48e1e-188">Assuming hello username in hello credential was *jsmith*, this results in hello following output.</span></span>

```
jsmith
```

## <a name="next-steps"></a><span data-ttu-id="48e1e-189">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="48e1e-189">Next steps</span></span>
* <span data-ttu-id="48e1e-190">architecture de runbook Hello dans l’article en cours fournit une vue d’ensemble de la gestion des ressources de runbook dans Azure et locales avec hello Runbook Worker hybride.</span><span class="sxs-lookup"><span data-stu-id="48e1e-190">hello runbook architecture in current article provides a high-level overview of runbooks managing resources in Azure and on-premises with hello Hybrid Runbook Worker.</span></span>  <span data-ttu-id="48e1e-191">toolearn sur l’exécution des runbooks Automation dans votre centre de données, consultez trop[Workers hybrides](automation-hybrid-runbook-worker.md).</span><span class="sxs-lookup"><span data-stu-id="48e1e-191">toolearn about executing Automation runbooks in your datacenter, refer too[Hybrid Runbook Workers](automation-hybrid-runbook-worker.md).</span></span>
* <span data-ttu-id="48e1e-192">toolearn en savoir plus sur hello création toobe runbooks modulaire utilisé par d’autres runbooks pour les fonctions spécifiques ou courants, consultez trop[Runbooks enfants](automation-child-runbooks.md).</span><span class="sxs-lookup"><span data-stu-id="48e1e-192">toolearn more about hello creating modular runbooks toobe used by other runbooks for specific or common functions, refer too[Child Runbooks](automation-child-runbooks.md).</span></span>

