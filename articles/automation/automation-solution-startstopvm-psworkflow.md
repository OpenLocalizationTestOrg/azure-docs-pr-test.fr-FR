---
title: "aaaStarting et l’arrêt des machines virtuelles avec Azure Automation - flux de travail PowerShell | Documents Microsoft"
description: "Version graphique du scénario Azure Automation, y compris des procédures opérationnelles toostart et arrêter les machines virtuelles classiques."
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
redirect_document_id: False
ms.openlocfilehash: 273631c7fc5ddb989b3bbdc82b470ac3af6ee482
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-automation-scenario---starting-and-stopping-virtual-machines"></a><span data-ttu-id="f128b-103">Scénario Azure Automation : démarrage et arrêt de machines virtuelles</span><span class="sxs-lookup"><span data-stu-id="f128b-103">Azure Automation scenario - starting and stopping virtual machines</span></span>
<span data-ttu-id="f128b-104">Ce scénario Azure Automation inclut des procédures opérationnelles toostart et arrêter les machines virtuelles classiques.</span><span class="sxs-lookup"><span data-stu-id="f128b-104">This Azure Automation scenario includes runbooks toostart and stop classic virtual machines.</span></span>  <span data-ttu-id="f128b-105">Vous pouvez utiliser ce scénario pour hello suivants :</span><span class="sxs-lookup"><span data-stu-id="f128b-105">You can use this scenario for any of hello following:</span></span>  

* <span data-ttu-id="f128b-106">Utiliser des runbooks de hello sans modification dans votre propre environnement.</span><span class="sxs-lookup"><span data-stu-id="f128b-106">Use hello runbooks without modification in your own environment.</span></span>
* <span data-ttu-id="f128b-107">Modifier les fonctionnalités de tooperform personnalisé de procédures opérationnelles de hello.</span><span class="sxs-lookup"><span data-stu-id="f128b-107">Modify hello runbooks tooperform customized functionality.</span></span>  
* <span data-ttu-id="f128b-108">Appeler des procédures opérationnelles de hello à partir d’un autre runbook dans le cadre d’une solution globale.</span><span class="sxs-lookup"><span data-stu-id="f128b-108">Call hello runbooks from another runbook as part of an overall solution.</span></span>
* <span data-ttu-id="f128b-109">Permet d’utiliser des runbooks de hello en tant que runbook toolearn de didacticiels concepts de création.</span><span class="sxs-lookup"><span data-stu-id="f128b-109">Use hello runbooks as tutorials toolearn runbook authoring concepts.</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="f128b-110">Graphique</span><span class="sxs-lookup"><span data-stu-id="f128b-110">Graphical</span></span>](automation-solution-startstopvm-graphical.md)
> * [<span data-ttu-id="f128b-111">Workflow PowerShell</span><span class="sxs-lookup"><span data-stu-id="f128b-111">PowerShell Workflow</span></span>](automation-solution-startstopvm-psworkflow.md)
> 
> 

<span data-ttu-id="f128b-112">Il s’agit de hello version du runbook PowerShell Workflow de ce scénario.</span><span class="sxs-lookup"><span data-stu-id="f128b-112">This is hello PowerShell Workflow runbook version of this scenario.</span></span> <span data-ttu-id="f128b-113">Elle est également disponible à l’aide des [runbooks graphiques](automation-solution-startstopvm-graphical.md).</span><span class="sxs-lookup"><span data-stu-id="f128b-113">It is also available using [graphical runbooks](automation-solution-startstopvm-graphical.md).</span></span>

## <a name="getting-hello-scenario"></a><span data-ttu-id="f128b-114">Scénario de hello mise en route</span><span class="sxs-lookup"><span data-stu-id="f128b-114">Getting hello scenario</span></span>
<span data-ttu-id="f128b-115">Ce scénario se compose de deux runbook PowerShell Workflow que vous pouvez télécharger à partir de hello suivant liens.</span><span class="sxs-lookup"><span data-stu-id="f128b-115">This scenario consists of two PowerShell Workflow runbooks that you can download from hello following links.</span></span>  <span data-ttu-id="f128b-116">Consultez hello [version graphique](automation-solution-startstopvm-graphical.md) de ce scénario pour les runbooks graphiques toohello de liens.</span><span class="sxs-lookup"><span data-stu-id="f128b-116">See hello [graphical version](automation-solution-startstopvm-graphical.md) of this scenario for links toohello graphical runbooks.</span></span>

| <span data-ttu-id="f128b-117">Runbook</span><span class="sxs-lookup"><span data-stu-id="f128b-117">Runbook</span></span> | <span data-ttu-id="f128b-118">Lien</span><span class="sxs-lookup"><span data-stu-id="f128b-118">Link</span></span> | <span data-ttu-id="f128b-119">Type</span><span class="sxs-lookup"><span data-stu-id="f128b-119">Type</span></span> | <span data-ttu-id="f128b-120">Description</span><span class="sxs-lookup"><span data-stu-id="f128b-120">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="f128b-121">Start-AzureVMs</span><span class="sxs-lookup"><span data-stu-id="f128b-121">Start-AzureVMs</span></span> |[<span data-ttu-id="f128b-122">Démarrer les machines virtuelles Azure classiques</span><span class="sxs-lookup"><span data-stu-id="f128b-122">Start Azure Classic VMs</span></span>](https://gallery.technet.microsoft.com/Start-Azure-Classic-VMs-86ef746b) |<span data-ttu-id="f128b-123">Workflow PowerShell</span><span class="sxs-lookup"><span data-stu-id="f128b-123">PowerShell Workflow</span></span> |<span data-ttu-id="f128b-124">Démarre toutes les machines virtuelles classiques d’un abonnement Azure ou toutes les machines virtuelles portant un nom de service particulier.</span><span class="sxs-lookup"><span data-stu-id="f128b-124">Starts all classic virtual machines in an Azure subscriptionor all virtual machines with a particular service name.</span></span> |
| <span data-ttu-id="f128b-125">Stop-AzureVMs</span><span class="sxs-lookup"><span data-stu-id="f128b-125">Stop-AzureVMs</span></span> |[<span data-ttu-id="f128b-126">Arrêter les machines virtuelles Azure classiques</span><span class="sxs-lookup"><span data-stu-id="f128b-126">Stop Azure Classic VMs</span></span>](https://gallery.technet.microsoft.com/Stop-Azure-Classic-VMs-7a4ae43e) |<span data-ttu-id="f128b-127">Workflow PowerShell</span><span class="sxs-lookup"><span data-stu-id="f128b-127">PowerShell Workflow</span></span> |<span data-ttu-id="f128b-128">Arrête toutes les machines virtuelles d’un compte Automation ou toutes les machines virtuelles portant un nom de service particulier.</span><span class="sxs-lookup"><span data-stu-id="f128b-128">Stops all virtual machines in an automation account or all virtual machines with a particular service name.</span></span> |

## <a name="installing-and-configuring-hello-scenario"></a><span data-ttu-id="f128b-129">Installation et configuration de scénario de hello</span><span class="sxs-lookup"><span data-stu-id="f128b-129">Installing and configuring hello scenario</span></span>
### <a name="1-install-hello-runbooks"></a><span data-ttu-id="f128b-130">1. Installer les procédures opérationnelles de hello</span><span class="sxs-lookup"><span data-stu-id="f128b-130">1. Install hello runbooks</span></span>
<span data-ttu-id="f128b-131">Après avoir téléchargé hello runbooks, vous pouvez les importer à l’aide de la procédure hello dans [importation d’un Runbook](http://msdn.microsoft.com/library/dn643637.aspx#ImportRunbook).</span><span class="sxs-lookup"><span data-stu-id="f128b-131">After downloading hello runbooks, you can import them using hello procedure in [Importing a Runbook](http://msdn.microsoft.com/library/dn643637.aspx#ImportRunbook).</span></span>

### <a name="2-review-hello-description-and-requirements"></a><span data-ttu-id="f128b-132">2. Révision hello description et configuration requise</span><span class="sxs-lookup"><span data-stu-id="f128b-132">2. Review hello description and requirements</span></span>
<span data-ttu-id="f128b-133">Hello runbooks inclure le texte d’aide commentées qui inclut une description et les ressources requises.</span><span class="sxs-lookup"><span data-stu-id="f128b-133">hello runbooks include commented help text that includes a description and required assets.</span></span>  <span data-ttu-id="f128b-134">Vous pouvez également obtenir hello les mêmes informations à partir de cet article.</span><span class="sxs-lookup"><span data-stu-id="f128b-134">You can also get hello same information from this article.</span></span>

### <a name="3-configure-assets"></a><span data-ttu-id="f128b-135">3. Configuration des ressources</span><span class="sxs-lookup"><span data-stu-id="f128b-135">3. Configure assets</span></span>
<span data-ttu-id="f128b-136">les runbooks de Hello nécessitent hello suivant les ressources que vous devez créer et remplir avec les valeurs appropriées.</span><span class="sxs-lookup"><span data-stu-id="f128b-136">hello runbooks require hello following assets that you must create and populate with appropriate values.</span></span>

| <span data-ttu-id="f128b-137">Type de ressource</span><span class="sxs-lookup"><span data-stu-id="f128b-137">Asset Type</span></span> | <span data-ttu-id="f128b-138">Nom de la ressource</span><span class="sxs-lookup"><span data-stu-id="f128b-138">Asset Name</span></span> | <span data-ttu-id="f128b-139">Description</span><span class="sxs-lookup"><span data-stu-id="f128b-139">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="f128b-140">Informations d'identification</span><span class="sxs-lookup"><span data-stu-id="f128b-140">Credential</span></span> |<span data-ttu-id="f128b-141">AzureCredential</span><span class="sxs-lookup"><span data-stu-id="f128b-141">AzureCredential</span></span> |<span data-ttu-id="f128b-142">Contient des informations d’identification d’un compte qui a l’autorité toostart arrêter les machines virtuelles dans hello abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="f128b-142">Contains credentials for an account that has authority toostart and stop virtual machines in hello Azure subscription.</span></span>  <span data-ttu-id="f128b-143">Vous pouvez également spécifier une autre ressource d’informations d’identification Bonjour **informations d’identification** paramètre Hello **Add-AzureAccount** activité.</span><span class="sxs-lookup"><span data-stu-id="f128b-143">Alternatively, you can specify another credential asset in hello **Credential** parameter of hello **Add-AzureAccount** activity.</span></span> |
| <span data-ttu-id="f128b-144">Variable</span><span class="sxs-lookup"><span data-stu-id="f128b-144">Variable</span></span> |<span data-ttu-id="f128b-145">AzureSubscriptionId</span><span class="sxs-lookup"><span data-stu-id="f128b-145">AzureSubscriptionId</span></span> |<span data-ttu-id="f128b-146">Contient l’ID d’abonnement hello de votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="f128b-146">Contains hello subscription ID of your Azure subscription.</span></span> |

## <a name="using-hello-scenario"></a><span data-ttu-id="f128b-147">À l’aide du scénario de hello</span><span class="sxs-lookup"><span data-stu-id="f128b-147">Using hello scenario</span></span>
### <a name="parameters"></a><span data-ttu-id="f128b-148">Paramètres</span><span class="sxs-lookup"><span data-stu-id="f128b-148">Parameters</span></span>
<span data-ttu-id="f128b-149">Hello procédures opérationnelles chaque ont hello paramètres suivants.</span><span class="sxs-lookup"><span data-stu-id="f128b-149">hello runbooks each have hello following parameters.</span></span>  <span data-ttu-id="f128b-150">Vous devez fournir des valeurs pour tous les paramètres obligatoires et pouvez éventuellement fournir des valeurs pour les autres paramètres, selon vos besoins.</span><span class="sxs-lookup"><span data-stu-id="f128b-150">You must provide values for any mandatory parameters and can optionally provide values for other parameters depending on your requirements.</span></span>

| <span data-ttu-id="f128b-151">Paramètre</span><span class="sxs-lookup"><span data-stu-id="f128b-151">Parameter</span></span> | <span data-ttu-id="f128b-152">Type</span><span class="sxs-lookup"><span data-stu-id="f128b-152">Type</span></span> | <span data-ttu-id="f128b-153">Obligatoire</span><span class="sxs-lookup"><span data-stu-id="f128b-153">Mandatory</span></span> | <span data-ttu-id="f128b-154">Description</span><span class="sxs-lookup"><span data-stu-id="f128b-154">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="f128b-155">ServiceName</span><span class="sxs-lookup"><span data-stu-id="f128b-155">ServiceName</span></span> |<span data-ttu-id="f128b-156">string</span><span class="sxs-lookup"><span data-stu-id="f128b-156">string</span></span> |<span data-ttu-id="f128b-157">Non</span><span class="sxs-lookup"><span data-stu-id="f128b-157">No</span></span> |<span data-ttu-id="f128b-158">Si une valeur est fournie, toutes les machines virtuelles portant ce nom de service sont démarrées ou arrêtées.</span><span class="sxs-lookup"><span data-stu-id="f128b-158">If a value is provided, then all virtual machines with that service name are started or stopped.</span></span>  <span data-ttu-id="f128b-159">Si aucune valeur n’est fournie, toutes les machines virtuelles classiques Bonjour abonnement Azure sont démarrés ou arrêtés.</span><span class="sxs-lookup"><span data-stu-id="f128b-159">If no value is provided, then all classic virtual machines in hello Azure subscription are started or stopped.</span></span> |
| <span data-ttu-id="f128b-160">AzureSubscriptionIdAssetName</span><span class="sxs-lookup"><span data-stu-id="f128b-160">AzureSubscriptionIdAssetName</span></span> |<span data-ttu-id="f128b-161">string</span><span class="sxs-lookup"><span data-stu-id="f128b-161">string</span></span> |<span data-ttu-id="f128b-162">Non</span><span class="sxs-lookup"><span data-stu-id="f128b-162">No</span></span> |<span data-ttu-id="f128b-163">Contient le nom hello Hello [ressource de variable](#installing-and-configuring-the-scenario) qui contient l’ID d’abonnement hello de votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="f128b-163">Contains hello name of hello [variable asset](#installing-and-configuring-the-scenario) that contains hello subscription ID of your Azure subscription.</span></span>  <span data-ttu-id="f128b-164">Si vous ne spécifiez aucune valeur, la valeur *AzureSubscriptionId* est utilisée.</span><span class="sxs-lookup"><span data-stu-id="f128b-164">If you don't specify a value, *AzureSubscriptionId* is used.</span></span> |
| <span data-ttu-id="f128b-165">AzureCredentialAssetName</span><span class="sxs-lookup"><span data-stu-id="f128b-165">AzureCredentialAssetName</span></span> |<span data-ttu-id="f128b-166">string</span><span class="sxs-lookup"><span data-stu-id="f128b-166">string</span></span> |<span data-ttu-id="f128b-167">Non</span><span class="sxs-lookup"><span data-stu-id="f128b-167">No</span></span> |<span data-ttu-id="f128b-168">Contient le nom hello Hello [actif d’informations d’identification](#installing-and-configuring-the-scenario) qui contient les informations d’identification de hello pour hello runbook toouse.</span><span class="sxs-lookup"><span data-stu-id="f128b-168">Contains hello name of hello [credential asset](#installing-and-configuring-the-scenario) that contains hello credentials for hello runbook toouse.</span></span>  <span data-ttu-id="f128b-169">Si vous ne spécifiez aucune valeur, la valeur *AzureCredential* est utilisée.</span><span class="sxs-lookup"><span data-stu-id="f128b-169">If you don't specify a value, *AzureCredential* is used.</span></span> |

### <a name="starting-hello-runbooks"></a><span data-ttu-id="f128b-170">Démarrage des runbook de hello</span><span class="sxs-lookup"><span data-stu-id="f128b-170">Starting hello runbooks</span></span>
<span data-ttu-id="f128b-171">Vous pouvez utiliser une des méthodes hello dans [démarrage d’un runbook dans Azure Automation](automation-starting-a-runbook.md) toostart une des procédures opérationnelles de hello dans ce scénario.</span><span class="sxs-lookup"><span data-stu-id="f128b-171">You can use any of hello methods in [Starting a runbook in Azure Automation](automation-starting-a-runbook.md) toostart either of hello runbooks in this scenario.</span></span>

<span data-ttu-id="f128b-172">Hello suivant des exemples de commandes utilise Windows PowerShell toorun **StartAzureVMs** toostart tous les ordinateurs virtuels avec le nom du service hello *MyVMService*.</span><span class="sxs-lookup"><span data-stu-id="f128b-172">hello following sample commands uses Windows PowerShell toorun **StartAzureVMs** toostart all virtual machines with hello service name *MyVMService*.</span></span>

    $params = @{"ServiceName"="MyVMService"}
    Start-AzureAutomationRunbook –AutomationAccountName "MyAutomationAccount" –Name "Start-AzureVMs" –Parameters $params

### <a name="output"></a><span data-ttu-id="f128b-173">Sortie</span><span class="sxs-lookup"><span data-stu-id="f128b-173">Output</span></span>
<span data-ttu-id="f128b-174">Hello runbooks sera [un message de sortie](automation-runbook-output-and-messages.md) pour chaque ordinateur virtuel indiquant hello ou non de démarrer ou d’instruction stop a été correctement envoyée.</span><span class="sxs-lookup"><span data-stu-id="f128b-174">hello runbooks will [output a message](automation-runbook-output-and-messages.md) for each virtual machine indicating whether or not hello start or stop instruction was successfully submitted.</span></span>  <span data-ttu-id="f128b-175">Vous pouvez rechercher une chaîne spécifique dans le résultat de hello toodetermine hello sortie pour chaque runbook.</span><span class="sxs-lookup"><span data-stu-id="f128b-175">You can look for a specific string in hello output toodetermine hello result for each runbook.</span></span>  <span data-ttu-id="f128b-176">chaînes de sortie Hello sont répertoriées dans hello tableau suivant.</span><span class="sxs-lookup"><span data-stu-id="f128b-176">hello possible output strings are listed in hello following table.</span></span>

| <span data-ttu-id="f128b-177">Runbook</span><span class="sxs-lookup"><span data-stu-id="f128b-177">Runbook</span></span> | <span data-ttu-id="f128b-178">Condition</span><span class="sxs-lookup"><span data-stu-id="f128b-178">Condition</span></span> | <span data-ttu-id="f128b-179">Message</span><span class="sxs-lookup"><span data-stu-id="f128b-179">Message</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="f128b-180">Start-AzureVMs</span><span class="sxs-lookup"><span data-stu-id="f128b-180">Start-AzureVMs</span></span> |<span data-ttu-id="f128b-181">Machine virtuelle déjà en cours d’exécution</span><span class="sxs-lookup"><span data-stu-id="f128b-181">Virtual machine is already running</span></span> |<span data-ttu-id="f128b-182">MyVM déjà en cours d’exécution</span><span class="sxs-lookup"><span data-stu-id="f128b-182">MyVM is already running</span></span> |
| <span data-ttu-id="f128b-183">Start-AzureVMs</span><span class="sxs-lookup"><span data-stu-id="f128b-183">Start-AzureVMs</span></span> |<span data-ttu-id="f128b-184">Demande de démarrage de la machine virtuelle envoyée avec succès</span><span class="sxs-lookup"><span data-stu-id="f128b-184">Start request for virtual machine successfully submitted</span></span> |<span data-ttu-id="f128b-185">MyVM démarrée</span><span class="sxs-lookup"><span data-stu-id="f128b-185">MyVM has been started</span></span> |
| <span data-ttu-id="f128b-186">Start-AzureVMs</span><span class="sxs-lookup"><span data-stu-id="f128b-186">Start-AzureVMs</span></span> |<span data-ttu-id="f128b-187">Échec de la demande de démarrage de la machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="f128b-187">Start request for virtual machine failed</span></span> |<span data-ttu-id="f128b-188">Échec de MyVM toostart</span><span class="sxs-lookup"><span data-stu-id="f128b-188">MyVM failed toostart</span></span> |
| <span data-ttu-id="f128b-189">Stop-AzureVMs</span><span class="sxs-lookup"><span data-stu-id="f128b-189">Stop-AzureVMs</span></span> |<span data-ttu-id="f128b-190">Machine virtuelle déjà arrêtée</span><span class="sxs-lookup"><span data-stu-id="f128b-190">Virtual machine is already stopped</span></span> |<span data-ttu-id="f128b-191">MyVM déjà arrêtée</span><span class="sxs-lookup"><span data-stu-id="f128b-191">MyVM is already stopped</span></span> |
| <span data-ttu-id="f128b-192">Stop-AzureVMs</span><span class="sxs-lookup"><span data-stu-id="f128b-192">Stop-AzureVMs</span></span> |<span data-ttu-id="f128b-193">Demande d’arrêt de la machine virtuelle envoyée avec succès</span><span class="sxs-lookup"><span data-stu-id="f128b-193">Stop request for virtual machine successfully submitted</span></span> |<span data-ttu-id="f128b-194">MyVM arrêtée</span><span class="sxs-lookup"><span data-stu-id="f128b-194">MyVM has been stopped</span></span> |
| <span data-ttu-id="f128b-195">Stop-AzureVMs</span><span class="sxs-lookup"><span data-stu-id="f128b-195">Stop-AzureVMs</span></span> |<span data-ttu-id="f128b-196">Échec de la demande d’arrêt de la machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="f128b-196">Stop request for virtual machine failed</span></span> |<span data-ttu-id="f128b-197">Échec de MyVM toostop</span><span class="sxs-lookup"><span data-stu-id="f128b-197">MyVM failed toostop</span></span> |

<span data-ttu-id="f128b-198">Par exemple, hello suivant extrait de code à partir d’un runbook tente toostart tous les ordinateurs virtuels avec le nom du service hello *MyServiceName*.</span><span class="sxs-lookup"><span data-stu-id="f128b-198">For example, hello following code snippet from a runbook attempts toostart all virtual machines with hello service name *MyServiceName*.</span></span>  <span data-ttu-id="f128b-199">Si un des hello démarre demandes échouent, les actions d’erreur peuvent entreprendre.</span><span class="sxs-lookup"><span data-stu-id="f128b-199">If any of hello start requests fail, then error actions can be taken.</span></span>

    $results = Start-AzureVMs -ServiceName "MyServiceName"
    foreach ($result in $results) {
        if ($result -like "* has been started" ) {
            # Action tootake in case of success.
        }
        else {
            # Action tootake in case of error.
        }
    }


## <a name="detailed-breakdown"></a><span data-ttu-id="f128b-200">Analyse détaillée</span><span class="sxs-lookup"><span data-stu-id="f128b-200">Detailed breakdown</span></span>
<span data-ttu-id="f128b-201">Voici une description détaillée des procédures opérationnelles de hello dans ce scénario.</span><span class="sxs-lookup"><span data-stu-id="f128b-201">Following is a detailed breakdown of hello runbooks in this scenario.</span></span>  <span data-ttu-id="f128b-202">Vous pouvez utiliser ces informations tooeither personnaliser hello runbooks ou toolearn uniquement à partir de celles-ci pour la création de vos propres scénarios d’automatisation.</span><span class="sxs-lookup"><span data-stu-id="f128b-202">You can use this information tooeither customize hello runbooks or just toolearn from them for authoring your own automation scenarios.</span></span>

### <a name="parameters"></a><span data-ttu-id="f128b-203">Paramètres</span><span class="sxs-lookup"><span data-stu-id="f128b-203">Parameters</span></span>
    param (
        [Parameter(Mandatory=$false)]
        [String]  $AzureCredentialAssetName = 'AzureCredential',

        [Parameter(Mandatory=$false)]
        [String] $AzureSubscriptionIdAssetName = 'AzureSubscriptionId',

        [Parameter(Mandatory=$false)]
        [String] $ServiceName
    )

<span data-ttu-id="f128b-204">Hello workflow démarre en obtenant les valeurs hello pour hello [paramètres d’entrée](#using-the-scenario).</span><span class="sxs-lookup"><span data-stu-id="f128b-204">hello workflow starts by getting hello values for hello [input parameters](#using-the-scenario).</span></span>  <span data-ttu-id="f128b-205">Si les noms des éléments hello ne sont pas fournies noms par défaut sont utilisés.</span><span class="sxs-lookup"><span data-stu-id="f128b-205">If hello asset names are not provided then default names are used.</span></span>

### <a name="output"></a><span data-ttu-id="f128b-206">Sortie</span><span class="sxs-lookup"><span data-stu-id="f128b-206">Output</span></span>
    # Returns strings with status messages
    [OutputType([String])]

<span data-ttu-id="f128b-207">Cette ligne déclare que la sortie hello de hello runbook sera une chaîne.</span><span class="sxs-lookup"><span data-stu-id="f128b-207">This line declares that hello output of hello runbook will be a string.</span></span>  <span data-ttu-id="f128b-208">Cela n’est pas obligatoire mais est recommandé pour lorsque hello runbook est utilisé comme un [runbook enfant](automation-child-runbooks.md) afin qu’un runbook parent connaissent la sortie de hello tooexpect de type.</span><span class="sxs-lookup"><span data-stu-id="f128b-208">This is not required but is a best practice for when hello runbook is used as a [child runbook](automation-child-runbooks.md) so that a parent runbook will know hello output type tooexpect.</span></span>

### <a name="authentication"></a><span data-ttu-id="f128b-209">Authentification</span><span class="sxs-lookup"><span data-stu-id="f128b-209">Authentication</span></span>
    # Connect tooAzure and select hello subscription toowork against
    $Cred = Get-AutomationPSCredential -Name $AzureCredentialAssetName
    $null = Add-AzureAccount -Credential $Cred -ErrorAction Stop
    $SubId = Get-AutomationVariable -Name $AzureSubscriptionIdAssetName
    $null = Select-AzureSubscription -SubscriptionId $SubId -ErrorAction Stop

<span data-ttu-id="f128b-210">les lignes suivantes Hello définissent hello [informations d’identification](automation-credentials.md) et un abonnement Azure qui sera utilisé pour le reste de hello de hello runbook.</span><span class="sxs-lookup"><span data-stu-id="f128b-210">hello next lines set hello [credentials](automation-credentials.md) and Azure subscription that will be used for hello rest of hello runbook.</span></span>
<span data-ttu-id="f128b-211">Tout d’abord, nous utilisons **Get-AutomationPSCredential** asset hello tooget qui contient les informations d’identification de hello avec accès des machines virtuelles toostart et d’arrêter Bonjour abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="f128b-211">First we use **Get-AutomationPSCredential** tooget hello asset that holds hello credentials with access toostart and stop virtual machines in hello Azure subscription.</span></span> <span data-ttu-id="f128b-212">**Ajouter-AzureAccount** utilise ensuite cette informations d’identification de ressource tooset hello.</span><span class="sxs-lookup"><span data-stu-id="f128b-212">**Add-AzureAccount** then uses this asset tooset hello credentials.</span></span>  <span data-ttu-id="f128b-213">sortie de Hello est attribué variable factice de tooa afin qu’il n’est pas inclus dans la sortie du runbook hello.</span><span class="sxs-lookup"><span data-stu-id="f128b-213">hello output is assigned tooa dummy variable so that it isn't included in hello runbook output.</span></span>  

<span data-ttu-id="f128b-214">ressource de variable Hello avec abonnement hello ID est ensuite extraite avec **Get-AutomationVariable** et abonnement hello avec **Select-AzureSubscription**.</span><span class="sxs-lookup"><span data-stu-id="f128b-214">hello variable asset with hello subscription ID is then retrieved with **Get-AutomationVariable** and hello subscription set with **Select-AzureSubscription**.</span></span>

### <a name="get-vms"></a><span data-ttu-id="f128b-215">Obtention de machines virtuelles</span><span class="sxs-lookup"><span data-stu-id="f128b-215">Get VMs</span></span>
    # If there is a specific cloud service, then get all VMs in hello service,
    # otherwise get all VMs in hello subscription.
    if ($ServiceName)
    {
        $VMs = Get-AzureVM -ServiceName $ServiceName
    }
    else
    {
        $VMs = Get-AzureVM
    }

<span data-ttu-id="f128b-216">**Get-AzureVM** est utilisé tooretrieve virtuels hello hello runbook fonctionnera avec.</span><span class="sxs-lookup"><span data-stu-id="f128b-216">**Get-AzureVM** is used tooretrieve hello virtual machines hello runbook will work with.</span></span>  <span data-ttu-id="f128b-217">Si une valeur est fournie dans hello **ServiceName** d’entrée variable, puis uniquement des machines virtuelles hello portant ce nom de service sont récupérés.</span><span class="sxs-lookup"><span data-stu-id="f128b-217">If a value is provided in hello **ServiceName** input variable, then only hello virtual machines with that service name are retrieved.</span></span>  <span data-ttu-id="f128b-218">Si **ServiceName** est vide, toutes les machines virtuelles sont récupérées.</span><span class="sxs-lookup"><span data-stu-id="f128b-218">If **ServiceName** is empty, then all virtual machines are retrieved.</span></span>

### <a name="startstop-virtual-machines-and-send-output"></a><span data-ttu-id="f128b-219">Démarrage/arrêt des machines virtuelles et envoi de sorties</span><span class="sxs-lookup"><span data-stu-id="f128b-219">Start/Stop virtual machines and send output</span></span>
    # Start each of hello stopped VMs
    foreach ($VM in $VMs)
    {
        if ($VM.PowerState -eq "Started")
        {
            # hello VM is already started, so send notice
            Write-Output ($VM.InstanceName + " is already running")
        }
        else
        {
            # hello VM needs toobe started
            $StartRtn = Start-AzureVM -Name $VM.Name -ServiceName $VM.ServiceName -ErrorAction Continue

            if ($StartRtn.OperationStatus -ne 'Succeeded')
            {
                # hello VM failed toostart, so send notice
                Write-Output ($VM.InstanceName + " failed toostart")
            }
            else
            {
                # hello VM started, so send notice
                Write-Output ($VM.InstanceName + " has been started")
            }
        }
    }

<span data-ttu-id="f128b-220">les lignes suivantes Hello Parcourez chaque ordinateur virtuel.</span><span class="sxs-lookup"><span data-stu-id="f128b-220">hello next lines step through each virtual machine.</span></span>  <span data-ttu-id="f128b-221">Tout d’abord hello **PowerState** hello machine virtuelle est activé toosee si elle est déjà en cours d’exécution ou arrêté, selon les runbook hello.</span><span class="sxs-lookup"><span data-stu-id="f128b-221">First hello **PowerState** of hello virtual machine is checked toosee if it is already running or stopped, depending on hello runbook.</span></span>  <span data-ttu-id="f128b-222">Si elle est déjà dans l’état cible de hello, un message est envoyé toooutput et se termine le runbook hello.</span><span class="sxs-lookup"><span data-stu-id="f128b-222">If it is already in hello target state, then a message is sent toooutput, and hello runbook ends.</span></span>  <span data-ttu-id="f128b-223">Si ce n’est pas le cas, puis **Start-AzureVM** ou **Stop-AzureVM** est utilisé tooattempt toostart ou arrêt hello virtuels avec un résultat de variable de hello demande tooa stockée hello.</span><span class="sxs-lookup"><span data-stu-id="f128b-223">If not, then **Start-AzureVM** or **Stop-AzureVM** is used tooattempt toostart or stop hello virtual machine with hello result of hello request stored tooa variable.</span></span>  <span data-ttu-id="f128b-224">Un message est ensuite envoyé toooutput spécifiant si hello demande toostart ou arrêt a été soumise.</span><span class="sxs-lookup"><span data-stu-id="f128b-224">A message is then sent toooutput specifying whether hello request toostart or stop was submitted successfully.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f128b-225">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="f128b-225">Next steps</span></span>
* <span data-ttu-id="f128b-226">toolearn en savoir plus sur l’utilisation des procédures opérationnelles enfant, consultez [runbooks enfants dans Azure Automation](automation-child-runbooks.md)</span><span class="sxs-lookup"><span data-stu-id="f128b-226">toolearn more about working with child runbooks, see [Child runbooks in Azure Automation](automation-child-runbooks.md)</span></span>
* <span data-ttu-id="f128b-227">toolearn en savoir plus sur les messages pendant l’exécution du runbook et de journalisation toohelp résoudre les problèmes de sortie, consultez [Runbook sortie et les messages dans Azure Automation](automation-runbook-output-and-messages.md)</span><span class="sxs-lookup"><span data-stu-id="f128b-227">toolearn more about output messages during runbook execution and logging toohelp troubleshoot, see [Runbook output and messages in Azure Automation](automation-runbook-output-and-messages.md)</span></span>

