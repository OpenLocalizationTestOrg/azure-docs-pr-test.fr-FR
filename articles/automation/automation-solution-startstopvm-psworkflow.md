---
title: "Démarrage et arrêt des machines virtuelles avec Azure Automation - Workflow PowerShell | Microsoft Docs"
description: "Version graphique du scénario Azure Automation incluant des runbooks pour démarrer et arrêter des machines virtuelles classiques."
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: d380bd43-d45d-45af-a5b2-78e7f66263c3
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/06/2016
ms.author: magoedte;bwren
redirect_url: https://docs.microsoft.com/azure/automation/automation-solution-vm-management
redirect_document_id: FALSE
ms.openlocfilehash: 95a7b02b0d11bf18c398daea48d16e0ead30b543
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-automation-scenario---starting-and-stopping-virtual-machines"></a><span data-ttu-id="2f832-103">Scénario Azure Automation : démarrage et arrêt de machines virtuelles</span><span class="sxs-lookup"><span data-stu-id="2f832-103">Azure Automation scenario - starting and stopping virtual machines</span></span>
<span data-ttu-id="2f832-104">Ce scénario Azure Automation inclut des runbooks pour démarrer et arrêter des machines virtuelles classiques.</span><span class="sxs-lookup"><span data-stu-id="2f832-104">This Azure Automation scenario includes runbooks to start and stop classic virtual machines.</span></span>  <span data-ttu-id="2f832-105">Vous pouvez utiliser ce scénario dans les cas suivants :</span><span class="sxs-lookup"><span data-stu-id="2f832-105">You can use this scenario for any of the following:</span></span>  

* <span data-ttu-id="2f832-106">Utiliser les runbooks sans modification dans votre propre environnement.</span><span class="sxs-lookup"><span data-stu-id="2f832-106">Use the runbooks without modification in your own environment.</span></span>
* <span data-ttu-id="2f832-107">Modifier les runbooks pour exécuter une fonctionnalité personnalisée.</span><span class="sxs-lookup"><span data-stu-id="2f832-107">Modify the runbooks to perform customized functionality.</span></span>  
* <span data-ttu-id="2f832-108">Appeler les runbooks à partir d’un autre runbook dans le cadre d’une solution globale.</span><span class="sxs-lookup"><span data-stu-id="2f832-108">Call the runbooks from another runbook as part of an overall solution.</span></span>
* <span data-ttu-id="2f832-109">Utiliser les runbooks comme didacticiels pour apprendre les concepts de création de runbook.</span><span class="sxs-lookup"><span data-stu-id="2f832-109">Use the runbooks as tutorials to learn runbook authoring concepts.</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="2f832-110">Graphique</span><span class="sxs-lookup"><span data-stu-id="2f832-110">Graphical</span></span>](automation-solution-startstopvm-graphical.md)
> * [<span data-ttu-id="2f832-111">Workflow PowerShell</span><span class="sxs-lookup"><span data-stu-id="2f832-111">PowerShell Workflow</span></span>](automation-solution-startstopvm-psworkflow.md)
> 
> 

<span data-ttu-id="2f832-112">Il s’agit de la version de runbook du Workflow PowerShell de ce scénario.</span><span class="sxs-lookup"><span data-stu-id="2f832-112">This is the PowerShell Workflow runbook version of this scenario.</span></span> <span data-ttu-id="2f832-113">Elle est également disponible à l’aide des [runbooks graphiques](automation-solution-startstopvm-graphical.md).</span><span class="sxs-lookup"><span data-stu-id="2f832-113">It is also available using [graphical runbooks](automation-solution-startstopvm-graphical.md).</span></span>

## <a name="getting-the-scenario"></a><span data-ttu-id="2f832-114">Obtention du scénario</span><span class="sxs-lookup"><span data-stu-id="2f832-114">Getting the scenario</span></span>
<span data-ttu-id="2f832-115">Ce scénario se compose de deux runbooks Workflow PowerShell que vous pouvez télécharger à partir des liens suivants.</span><span class="sxs-lookup"><span data-stu-id="2f832-115">This scenario consists of two PowerShell Workflow runbooks that you can download from the following links.</span></span>  <span data-ttu-id="2f832-116">Consultez la [version graphique](automation-solution-startstopvm-graphical.md) de ce scénario pour des liens vers les runbooks graphiques.</span><span class="sxs-lookup"><span data-stu-id="2f832-116">See the [graphical version](automation-solution-startstopvm-graphical.md) of this scenario for links to the graphical runbooks.</span></span>

| <span data-ttu-id="2f832-117">Runbook</span><span class="sxs-lookup"><span data-stu-id="2f832-117">Runbook</span></span> | <span data-ttu-id="2f832-118">Lien</span><span class="sxs-lookup"><span data-stu-id="2f832-118">Link</span></span> | <span data-ttu-id="2f832-119">Type</span><span class="sxs-lookup"><span data-stu-id="2f832-119">Type</span></span> | <span data-ttu-id="2f832-120">Description</span><span class="sxs-lookup"><span data-stu-id="2f832-120">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="2f832-121">Start-AzureVMs</span><span class="sxs-lookup"><span data-stu-id="2f832-121">Start-AzureVMs</span></span> |[<span data-ttu-id="2f832-122">Démarrer les machines virtuelles Azure classiques</span><span class="sxs-lookup"><span data-stu-id="2f832-122">Start Azure Classic VMs</span></span>](https://gallery.technet.microsoft.com/Start-Azure-Classic-VMs-86ef746b) |<span data-ttu-id="2f832-123">Workflow PowerShell</span><span class="sxs-lookup"><span data-stu-id="2f832-123">PowerShell Workflow</span></span> |<span data-ttu-id="2f832-124">Démarre toutes les machines virtuelles classiques d’un abonnement Azure ou toutes les machines virtuelles portant un nom de service particulier.</span><span class="sxs-lookup"><span data-stu-id="2f832-124">Starts all classic virtual machines in an Azure subscriptionor all virtual machines with a particular service name.</span></span> |
| <span data-ttu-id="2f832-125">Stop-AzureVMs</span><span class="sxs-lookup"><span data-stu-id="2f832-125">Stop-AzureVMs</span></span> |[<span data-ttu-id="2f832-126">Arrêter les machines virtuelles Azure classiques</span><span class="sxs-lookup"><span data-stu-id="2f832-126">Stop Azure Classic VMs</span></span>](https://gallery.technet.microsoft.com/Stop-Azure-Classic-VMs-7a4ae43e) |<span data-ttu-id="2f832-127">Workflow PowerShell</span><span class="sxs-lookup"><span data-stu-id="2f832-127">PowerShell Workflow</span></span> |<span data-ttu-id="2f832-128">Arrête toutes les machines virtuelles d’un compte Automation ou toutes les machines virtuelles portant un nom de service particulier.</span><span class="sxs-lookup"><span data-stu-id="2f832-128">Stops all virtual machines in an automation account or all virtual machines with a particular service name.</span></span> |

## <a name="installing-and-configuring-the-scenario"></a><span data-ttu-id="2f832-129">Installation et configuration du scénario</span><span class="sxs-lookup"><span data-stu-id="2f832-129">Installing and configuring the scenario</span></span>
### <a name="1-install-the-runbooks"></a><span data-ttu-id="2f832-130">1. Installation des runbooks</span><span class="sxs-lookup"><span data-stu-id="2f832-130">1. Install the runbooks</span></span>
<span data-ttu-id="2f832-131">Après avoir téléchargé les runbooks, vous pouvez les importer à l’aide de la procédure décrite dans [Importation d’un runbook](http://msdn.microsoft.com/library/dn643637.aspx#ImportRunbook).</span><span class="sxs-lookup"><span data-stu-id="2f832-131">After downloading the runbooks, you can import them using the procedure in [Importing a Runbook](http://msdn.microsoft.com/library/dn643637.aspx#ImportRunbook).</span></span>

### <a name="2-review-the-description-and-requirements"></a><span data-ttu-id="2f832-132">2. Examen de la description et des conditions requises</span><span class="sxs-lookup"><span data-stu-id="2f832-132">2. Review the description and requirements</span></span>
<span data-ttu-id="2f832-133">Les runbooks incluent du texte d’aide commenté qui comprend une description et les ressources requises.</span><span class="sxs-lookup"><span data-stu-id="2f832-133">The runbooks include commented help text that includes a description and required assets.</span></span>  <span data-ttu-id="2f832-134">Vous pouvez également obtenir les mêmes informations à partir de cet article.</span><span class="sxs-lookup"><span data-stu-id="2f832-134">You can also get the same information from this article.</span></span>

### <a name="3-configure-assets"></a><span data-ttu-id="2f832-135">3. Configuration des ressources</span><span class="sxs-lookup"><span data-stu-id="2f832-135">3. Configure assets</span></span>
<span data-ttu-id="2f832-136">Les runbooks requièrent les ressources suivantes que vous devez créer et remplir avec les valeurs appropriées.</span><span class="sxs-lookup"><span data-stu-id="2f832-136">The runbooks require the following assets that you must create and populate with appropriate values.</span></span>

| <span data-ttu-id="2f832-137">Type de ressource</span><span class="sxs-lookup"><span data-stu-id="2f832-137">Asset Type</span></span> | <span data-ttu-id="2f832-138">Nom de la ressource</span><span class="sxs-lookup"><span data-stu-id="2f832-138">Asset Name</span></span> | <span data-ttu-id="2f832-139">Description</span><span class="sxs-lookup"><span data-stu-id="2f832-139">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="2f832-140">Informations d'identification</span><span class="sxs-lookup"><span data-stu-id="2f832-140">Credential</span></span> |<span data-ttu-id="2f832-141">AzureCredential</span><span class="sxs-lookup"><span data-stu-id="2f832-141">AzureCredential</span></span> |<span data-ttu-id="2f832-142">Contient des informations d’identification d’un compte ayant les autorisations pour démarrer et arrêter des machines virtuelles dans l’abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="2f832-142">Contains credentials for an account that has authority to start and stop virtual machines in the Azure subscription.</span></span>  <span data-ttu-id="2f832-143">Vous pouvez également spécifier une autre ressource d’informations d’identification dans le paramètre **Credential** de l’activité **Add-AzureAccount**.</span><span class="sxs-lookup"><span data-stu-id="2f832-143">Alternatively, you can specify another credential asset in the **Credential** parameter of the **Add-AzureAccount** activity.</span></span> |
| <span data-ttu-id="2f832-144">Variable</span><span class="sxs-lookup"><span data-stu-id="2f832-144">Variable</span></span> |<span data-ttu-id="2f832-145">AzureSubscriptionId</span><span class="sxs-lookup"><span data-stu-id="2f832-145">AzureSubscriptionId</span></span> |<span data-ttu-id="2f832-146">Contient l’ID d’abonnement de votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="2f832-146">Contains the subscription ID of your Azure subscription.</span></span> |

## <a name="using-the-scenario"></a><span data-ttu-id="2f832-147">Utilisation du scénario</span><span class="sxs-lookup"><span data-stu-id="2f832-147">Using the scenario</span></span>
### <a name="parameters"></a><span data-ttu-id="2f832-148">Paramètres</span><span class="sxs-lookup"><span data-stu-id="2f832-148">Parameters</span></span>
<span data-ttu-id="2f832-149">Les runbooks ont tous les paramètres suivants.</span><span class="sxs-lookup"><span data-stu-id="2f832-149">The runbooks each have the following parameters.</span></span>  <span data-ttu-id="2f832-150">Vous devez fournir des valeurs pour tous les paramètres obligatoires et pouvez éventuellement fournir des valeurs pour les autres paramètres, selon vos besoins.</span><span class="sxs-lookup"><span data-stu-id="2f832-150">You must provide values for any mandatory parameters and can optionally provide values for other parameters depending on your requirements.</span></span>

| <span data-ttu-id="2f832-151">Paramètre</span><span class="sxs-lookup"><span data-stu-id="2f832-151">Parameter</span></span> | <span data-ttu-id="2f832-152">Type</span><span class="sxs-lookup"><span data-stu-id="2f832-152">Type</span></span> | <span data-ttu-id="2f832-153">Obligatoire</span><span class="sxs-lookup"><span data-stu-id="2f832-153">Mandatory</span></span> | <span data-ttu-id="2f832-154">Description</span><span class="sxs-lookup"><span data-stu-id="2f832-154">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="2f832-155">ServiceName</span><span class="sxs-lookup"><span data-stu-id="2f832-155">ServiceName</span></span> |<span data-ttu-id="2f832-156">string</span><span class="sxs-lookup"><span data-stu-id="2f832-156">string</span></span> |<span data-ttu-id="2f832-157">Non</span><span class="sxs-lookup"><span data-stu-id="2f832-157">No</span></span> |<span data-ttu-id="2f832-158">Si une valeur est fournie, toutes les machines virtuelles portant ce nom de service sont démarrées ou arrêtées.</span><span class="sxs-lookup"><span data-stu-id="2f832-158">If a value is provided, then all virtual machines with that service name are started or stopped.</span></span>  <span data-ttu-id="2f832-159">Si aucune valeur n’est fournie, toutes les machines virtuelles classiques dans l’abonnement Azure sont démarrées ou arrêtées.</span><span class="sxs-lookup"><span data-stu-id="2f832-159">If no value is provided, then all classic virtual machines in the Azure subscription are started or stopped.</span></span> |
| <span data-ttu-id="2f832-160">AzureSubscriptionIdAssetName</span><span class="sxs-lookup"><span data-stu-id="2f832-160">AzureSubscriptionIdAssetName</span></span> |<span data-ttu-id="2f832-161">string</span><span class="sxs-lookup"><span data-stu-id="2f832-161">string</span></span> |<span data-ttu-id="2f832-162">Non</span><span class="sxs-lookup"><span data-stu-id="2f832-162">No</span></span> |<span data-ttu-id="2f832-163">Contient le nom de la [ressource variable](#installing-and-configuring-the-scenario) qui contient l’ID de votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="2f832-163">Contains the name of the [variable asset](#installing-and-configuring-the-scenario) that contains the subscription ID of your Azure subscription.</span></span>  <span data-ttu-id="2f832-164">Si vous ne spécifiez aucune valeur, la valeur *AzureSubscriptionId* est utilisée.</span><span class="sxs-lookup"><span data-stu-id="2f832-164">If you don't specify a value, *AzureSubscriptionId* is used.</span></span> |
| <span data-ttu-id="2f832-165">AzureCredentialAssetName</span><span class="sxs-lookup"><span data-stu-id="2f832-165">AzureCredentialAssetName</span></span> |<span data-ttu-id="2f832-166">string</span><span class="sxs-lookup"><span data-stu-id="2f832-166">string</span></span> |<span data-ttu-id="2f832-167">Non</span><span class="sxs-lookup"><span data-stu-id="2f832-167">No</span></span> |<span data-ttu-id="2f832-168">Contient le nom de la [ressource d’informations d’identification](#installing-and-configuring-the-scenario) qui contient les informations d’identification pour le runbook à utiliser.</span><span class="sxs-lookup"><span data-stu-id="2f832-168">Contains the name of the [credential asset](#installing-and-configuring-the-scenario) that contains the credentials for the runbook to use.</span></span>  <span data-ttu-id="2f832-169">Si vous ne spécifiez aucune valeur, la valeur *AzureCredential* est utilisée.</span><span class="sxs-lookup"><span data-stu-id="2f832-169">If you don't specify a value, *AzureCredential* is used.</span></span> |

### <a name="starting-the-runbooks"></a><span data-ttu-id="2f832-170">Démarrage des runbooks</span><span class="sxs-lookup"><span data-stu-id="2f832-170">Starting the runbooks</span></span>
<span data-ttu-id="2f832-171">Vous pouvez utiliser n’importe quelle méthode proposée dans [Démarrage d’un runbook dans Azure Automation](automation-starting-a-runbook.md) pour démarrer le runbook de votre choix dans ce scénario.</span><span class="sxs-lookup"><span data-stu-id="2f832-171">You can use any of the methods in [Starting a runbook in Azure Automation](automation-starting-a-runbook.md) to start either of the runbooks in this scenario.</span></span>

<span data-ttu-id="2f832-172">Les exemples de commandes suivants utilisent Windows PowerShell pour exécuter **StartAzureVMs** afin de démarrer toutes les machines virtuelles portant le nom de service *MyVMService*.</span><span class="sxs-lookup"><span data-stu-id="2f832-172">The following sample commands uses Windows PowerShell to run **StartAzureVMs** to start all virtual machines with the service name *MyVMService*.</span></span>

    $params = @{"ServiceName"="MyVMService"}
    Start-AzureAutomationRunbook –AutomationAccountName "MyAutomationAccount" –Name "Start-AzureVMs" –Parameters $params

### <a name="output"></a><span data-ttu-id="2f832-173">Sortie</span><span class="sxs-lookup"><span data-stu-id="2f832-173">Output</span></span>
<span data-ttu-id="2f832-174">Les Runbooks [généreront un message](automation-runbook-output-and-messages.md) pour chaque machine virtuelle, indiquant si l'instruction de démarrage ou d'arrêt a été correctement envoyée.</span><span class="sxs-lookup"><span data-stu-id="2f832-174">The runbooks will [output a message](automation-runbook-output-and-messages.md) for each virtual machine indicating whether or not the start or stop instruction was successfully submitted.</span></span>  <span data-ttu-id="2f832-175">Vous pouvez rechercher une chaîne spécifique dans la sortie afin de déterminer le résultat pour chaque runbook.</span><span class="sxs-lookup"><span data-stu-id="2f832-175">You can look for a specific string in the output to determine the result for each runbook.</span></span>  <span data-ttu-id="2f832-176">Les chaînes de sortie possibles sont répertoriées dans le tableau suivant.</span><span class="sxs-lookup"><span data-stu-id="2f832-176">The possible output strings are listed in the following table.</span></span>

| <span data-ttu-id="2f832-177">Runbook</span><span class="sxs-lookup"><span data-stu-id="2f832-177">Runbook</span></span> | <span data-ttu-id="2f832-178">Condition</span><span class="sxs-lookup"><span data-stu-id="2f832-178">Condition</span></span> | <span data-ttu-id="2f832-179">Message</span><span class="sxs-lookup"><span data-stu-id="2f832-179">Message</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="2f832-180">Start-AzureVMs</span><span class="sxs-lookup"><span data-stu-id="2f832-180">Start-AzureVMs</span></span> |<span data-ttu-id="2f832-181">Machine virtuelle déjà en cours d’exécution</span><span class="sxs-lookup"><span data-stu-id="2f832-181">Virtual machine is already running</span></span> |<span data-ttu-id="2f832-182">MyVM déjà en cours d’exécution</span><span class="sxs-lookup"><span data-stu-id="2f832-182">MyVM is already running</span></span> |
| <span data-ttu-id="2f832-183">Start-AzureVMs</span><span class="sxs-lookup"><span data-stu-id="2f832-183">Start-AzureVMs</span></span> |<span data-ttu-id="2f832-184">Demande de démarrage de la machine virtuelle envoyée avec succès</span><span class="sxs-lookup"><span data-stu-id="2f832-184">Start request for virtual machine successfully submitted</span></span> |<span data-ttu-id="2f832-185">MyVM démarrée</span><span class="sxs-lookup"><span data-stu-id="2f832-185">MyVM has been started</span></span> |
| <span data-ttu-id="2f832-186">Start-AzureVMs</span><span class="sxs-lookup"><span data-stu-id="2f832-186">Start-AzureVMs</span></span> |<span data-ttu-id="2f832-187">Échec de la demande de démarrage de la machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="2f832-187">Start request for virtual machine failed</span></span> |<span data-ttu-id="2f832-188">MyVM n’a pas pu démarrer</span><span class="sxs-lookup"><span data-stu-id="2f832-188">MyVM failed to start</span></span> |
| <span data-ttu-id="2f832-189">Stop-AzureVMs</span><span class="sxs-lookup"><span data-stu-id="2f832-189">Stop-AzureVMs</span></span> |<span data-ttu-id="2f832-190">Machine virtuelle déjà arrêtée</span><span class="sxs-lookup"><span data-stu-id="2f832-190">Virtual machine is already stopped</span></span> |<span data-ttu-id="2f832-191">MyVM déjà arrêtée</span><span class="sxs-lookup"><span data-stu-id="2f832-191">MyVM is already stopped</span></span> |
| <span data-ttu-id="2f832-192">Stop-AzureVMs</span><span class="sxs-lookup"><span data-stu-id="2f832-192">Stop-AzureVMs</span></span> |<span data-ttu-id="2f832-193">Demande d’arrêt de la machine virtuelle envoyée avec succès</span><span class="sxs-lookup"><span data-stu-id="2f832-193">Stop request for virtual machine successfully submitted</span></span> |<span data-ttu-id="2f832-194">MyVM arrêtée</span><span class="sxs-lookup"><span data-stu-id="2f832-194">MyVM has been stopped</span></span> |
| <span data-ttu-id="2f832-195">Stop-AzureVMs</span><span class="sxs-lookup"><span data-stu-id="2f832-195">Stop-AzureVMs</span></span> |<span data-ttu-id="2f832-196">Échec de la demande d’arrêt de la machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="2f832-196">Stop request for virtual machine failed</span></span> |<span data-ttu-id="2f832-197">Échec de l’arrêt de MyVM</span><span class="sxs-lookup"><span data-stu-id="2f832-197">MyVM failed to stop</span></span> |

<span data-ttu-id="2f832-198">Par exemple, l’extrait de code suivant d’un runbook tente de démarrer toutes les machines virtuelles portant le nom de service *MyServiceName*.</span><span class="sxs-lookup"><span data-stu-id="2f832-198">For example, the following code snippet from a runbook attempts to start all virtual machines with the service name *MyServiceName*.</span></span>  <span data-ttu-id="2f832-199">Si l’une des demandes de démarrage échoue, des mesures peuvent être prises.</span><span class="sxs-lookup"><span data-stu-id="2f832-199">If any of the start requests fail, then error actions can be taken.</span></span>

    $results = Start-AzureVMs -ServiceName "MyServiceName"
    foreach ($result in $results) {
        if ($result -like "* has been started" ) {
            # Action to take in case of success.
        }
        else {
            # Action to take in case of error.
        }
    }


## <a name="detailed-breakdown"></a><span data-ttu-id="2f832-200">Analyse détaillée</span><span class="sxs-lookup"><span data-stu-id="2f832-200">Detailed breakdown</span></span>
<span data-ttu-id="2f832-201">Voici une analyse détaillée des runbooks de ce scénario.</span><span class="sxs-lookup"><span data-stu-id="2f832-201">Following is a detailed breakdown of the runbooks in this scenario.</span></span>  <span data-ttu-id="2f832-202">Vous pouvez utiliser ces informations pour personnaliser les Runbooks ou simplement pour obtenir des informations à partir de ceux-ci afin de créer vos propres scénarios d’automatisation.</span><span class="sxs-lookup"><span data-stu-id="2f832-202">You can use this information to either customize the runbooks or just to learn from them for authoring your own automation scenarios.</span></span>

### <a name="parameters"></a><span data-ttu-id="2f832-203">Paramètres</span><span class="sxs-lookup"><span data-stu-id="2f832-203">Parameters</span></span>
    param (
        [Parameter(Mandatory=$false)]
        [String]  $AzureCredentialAssetName = 'AzureCredential',

        [Parameter(Mandatory=$false)]
        [String] $AzureSubscriptionIdAssetName = 'AzureSubscriptionId',

        [Parameter(Mandatory=$false)]
        [String] $ServiceName
    )

<span data-ttu-id="2f832-204">Le flux de travail démarre en obtenant les valeurs des [paramètres d’entrée](#using-the-scenario).</span><span class="sxs-lookup"><span data-stu-id="2f832-204">The workflow starts by getting the values for the [input parameters](#using-the-scenario).</span></span>  <span data-ttu-id="2f832-205">Si les noms de ressources ne sont pas fournis, les noms par défaut sont utilisés.</span><span class="sxs-lookup"><span data-stu-id="2f832-205">If the asset names are not provided then default names are used.</span></span>

### <a name="output"></a><span data-ttu-id="2f832-206">Sortie</span><span class="sxs-lookup"><span data-stu-id="2f832-206">Output</span></span>
    # Returns strings with status messages
    [OutputType([String])]

<span data-ttu-id="2f832-207">Cette ligne déclare que la sortie du runbook est une chaîne.</span><span class="sxs-lookup"><span data-stu-id="2f832-207">This line declares that the output of the runbook will be a string.</span></span>  <span data-ttu-id="2f832-208">Cette pratique n’est pas obligatoire mais elle est conseillée dans les situations où le runbook est utilisé comme un [runbook enfant](automation-child-runbooks.md) afin qu’un runbook parent connaisse le type de sortie attendu.</span><span class="sxs-lookup"><span data-stu-id="2f832-208">This is not required but is a best practice for when the runbook is used as a [child runbook](automation-child-runbooks.md) so that a parent runbook will know the output type to expect.</span></span>

### <a name="authentication"></a><span data-ttu-id="2f832-209">Authentification</span><span class="sxs-lookup"><span data-stu-id="2f832-209">Authentication</span></span>
    # Connect to Azure and select the subscription to work against
    $Cred = Get-AutomationPSCredential -Name $AzureCredentialAssetName
    $null = Add-AzureAccount -Credential $Cred -ErrorAction Stop
    $SubId = Get-AutomationVariable -Name $AzureSubscriptionIdAssetName
    $null = Select-AzureSubscription -SubscriptionId $SubId -ErrorAction Stop

<span data-ttu-id="2f832-210">Les lignes suivantes définissent les [informations d’identification](automation-credentials.md) et l’abonnement Azure qui seront utilisés pour le reste du runbook.</span><span class="sxs-lookup"><span data-stu-id="2f832-210">The next lines set the [credentials](automation-credentials.md) and Azure subscription that will be used for the rest of the runbook.</span></span>
<span data-ttu-id="2f832-211">Tout d’abord, nous utilisons **Get-AutomationPSCredential** pour obtenir la ressource qui détient les informations d’identification avec accès pour démarrer et arrêter des machines virtuelles dans l’abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="2f832-211">First we use **Get-AutomationPSCredential** to get the asset that holds the credentials with access to start and stop virtual machines in the Azure subscription.</span></span> <span data-ttu-id="2f832-212">**Add-AzureAccount** utilise ensuite cette ressource pour définir les informations d’identification.</span><span class="sxs-lookup"><span data-stu-id="2f832-212">**Add-AzureAccount** then uses this asset to set the credentials.</span></span>  <span data-ttu-id="2f832-213">La sortie est affectée à une variable factice de sorte qu’elle n’est pas incluse dans la sortie de runbook.</span><span class="sxs-lookup"><span data-stu-id="2f832-213">The output is assigned to a dummy variable so that it isn't included in the runbook output.</span></span>  

<span data-ttu-id="2f832-214">La ressource variable avec l’ID d’abonnement est ensuite récupérée avec **Get-AutomationVariable** et l’abonnement est défini avec **Select-AzureSubscription**.</span><span class="sxs-lookup"><span data-stu-id="2f832-214">The variable asset with the subscription ID is then retrieved with **Get-AutomationVariable** and the subscription set with **Select-AzureSubscription**.</span></span>

### <a name="get-vms"></a><span data-ttu-id="2f832-215">Obtention de machines virtuelles</span><span class="sxs-lookup"><span data-stu-id="2f832-215">Get VMs</span></span>
    # If there is a specific cloud service, then get all VMs in the service,
    # otherwise get all VMs in the subscription.
    if ($ServiceName)
    {
        $VMs = Get-AzureVM -ServiceName $ServiceName
    }
    else
    {
        $VMs = Get-AzureVM
    }

<span data-ttu-id="2f832-216">**Get-AzureVM** est utilisée pour récupérer les machines virtuelles avec lesquelles le runbook va fonctionner.</span><span class="sxs-lookup"><span data-stu-id="2f832-216">**Get-AzureVM** is used to retrieve the virtual machines the runbook will work with.</span></span>  <span data-ttu-id="2f832-217">Si une valeur est fournie dans la variable d’entrée **ServiceName** , alors seules les machines virtuelles portant ce nom de service sont récupérées.</span><span class="sxs-lookup"><span data-stu-id="2f832-217">If a value is provided in the **ServiceName** input variable, then only the virtual machines with that service name are retrieved.</span></span>  <span data-ttu-id="2f832-218">Si **ServiceName** est vide, toutes les machines virtuelles sont récupérées.</span><span class="sxs-lookup"><span data-stu-id="2f832-218">If **ServiceName** is empty, then all virtual machines are retrieved.</span></span>

### <a name="startstop-virtual-machines-and-send-output"></a><span data-ttu-id="2f832-219">Démarrage/arrêt des machines virtuelles et envoi de sorties</span><span class="sxs-lookup"><span data-stu-id="2f832-219">Start/Stop virtual machines and send output</span></span>
    # Start each of the stopped VMs
    foreach ($VM in $VMs)
    {
        if ($VM.PowerState -eq "Started")
        {
            # The VM is already started, so send notice
            Write-Output ($VM.InstanceName + " is already running")
        }
        else
        {
            # The VM needs to be started
            $StartRtn = Start-AzureVM -Name $VM.Name -ServiceName $VM.ServiceName -ErrorAction Continue

            if ($StartRtn.OperationStatus -ne 'Succeeded')
            {
                # The VM failed to start, so send notice
                Write-Output ($VM.InstanceName + " failed to start")
            }
            else
            {
                # The VM started, so send notice
                Write-Output ($VM.InstanceName + " has been started")
            }
        }
    }

<span data-ttu-id="2f832-220">Les lignes suivantes passent en revue chaque machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="2f832-220">The next lines step through each virtual machine.</span></span>  <span data-ttu-id="2f832-221">Premièrement, l’état d’alimentation **PowerState** de chaque machine virtuelle est vérifié pour voir si elle est déjà en cours d’exécution ou arrêtée, selon le runbook.</span><span class="sxs-lookup"><span data-stu-id="2f832-221">First the **PowerState** of the virtual machine is checked to see if it is already running or stopped, depending on the runbook.</span></span>  <span data-ttu-id="2f832-222">Si elle est déjà dans l’état cible, un message est envoyé à la sortie et le runbook s’arrête.</span><span class="sxs-lookup"><span data-stu-id="2f832-222">If it is already in the target state, then a message is sent to output, and the runbook ends.</span></span>  <span data-ttu-id="2f832-223">Si ce n’est pas le cas, les commandes **Start-AzureVM** ou **Stop-AzureVM** sont utilisées pour tenter de démarrer ou d’arrêter la machine virtuelle avec le résultat de la demande stocké dans une variable.</span><span class="sxs-lookup"><span data-stu-id="2f832-223">If not, then **Start-AzureVM** or **Stop-AzureVM** is used to attempt to start or stop the virtual machine with the result of the request stored to a variable.</span></span>  <span data-ttu-id="2f832-224">Ensuite, un message est envoyé à la sortie indiquant si la demande de démarrage ou d’arrêter a été envoyée avec succès.</span><span class="sxs-lookup"><span data-stu-id="2f832-224">A message is then sent to output specifying whether the request to start or stop was submitted successfully.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2f832-225">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="2f832-225">Next steps</span></span>
* <span data-ttu-id="2f832-226">Pour en savoir plus sur l’utilisation de runbooks enfants, consultez la rubrique [Runbooks enfants dans Azure Automation](automation-child-runbooks.md)</span><span class="sxs-lookup"><span data-stu-id="2f832-226">To learn more about working with child runbooks, see [Child runbooks in Azure Automation](automation-child-runbooks.md)</span></span>
* <span data-ttu-id="2f832-227">Pour en savoir plus sur les messages de sortie pendant l’exécution d’un runbook et la journalisation pour le dépannage, consultez la rubrique [Sortie et messages de Runbook dans Azure Automation](automation-runbook-output-and-messages.md)</span><span class="sxs-lookup"><span data-stu-id="2f832-227">To learn more about output messages during runbook execution and logging to help troubleshoot, see [Runbook output and messages in Azure Automation](automation-runbook-output-and-messages.md)</span></span>

