---
title: "aaaCollecting données Analytique de journal avec un runbook dans Azure Automation | Documents Microsoft"
description: "Didacticiel étape par étape qui guide à travers la création d’un runbook dans le référentiel d’OMS hello pour l’analyse par Analytique de journal dans les données de toocollect Azure Automation."
services: log-analytics
documentationcenter: 
author: bwren
manager: carmonm
editor: 
ms.assetid: a831fd90-3f55-423b-8b20-ccbaaac2ca75
ms.service: operations-management-suite
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/27/2017
ms.author: bwren
ms.openlocfilehash: e644dc3ef20fb1e930cae02e0fd44ccca31dc13d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="collect-data-in-log-analytics-with-an-azure-automation-runbook"></a><span data-ttu-id="8d871-103">Collecter des données dans Log Analytics avec un runbook Azure Automation</span><span class="sxs-lookup"><span data-stu-id="8d871-103">Collect data in Log Analytics with an Azure Automation runbook</span></span>
<span data-ttu-id="8d871-104">Vous pouvez collecter une quantité importante de données dans Log Analytics à partir de diverses sources, y compris des [sources de données](../log-analytics/log-analytics-data-sources.md) sur les agents et les [données recueillies à partir d’Azure](../log-analytics/log-analytics-azure-storage.md).</span><span class="sxs-lookup"><span data-stu-id="8d871-104">You can collect a significant amount of data in Log Analytics from a variety of sources including [data sources](../log-analytics/log-analytics-data-sources.md) on agents and also [data collected from Azure](../log-analytics/log-analytics-azure-storage.md).</span></span>  <span data-ttu-id="8d871-105">Il existe un scénario où vous avez besoin des données de toocollect qui n’est pas accessible via ces sources standards.</span><span class="sxs-lookup"><span data-stu-id="8d871-105">There are a scenarios though where you need toocollect data that isn't accessible through these standard sources.</span></span>  <span data-ttu-id="8d871-106">Dans ce cas, vous pouvez utiliser hello [API du collecteur de données HTTP](../log-analytics/log-analytics-data-collector-api.md) toowrite données tooLog Analytique à partir de n’importe quel client de l’API REST.</span><span class="sxs-lookup"><span data-stu-id="8d871-106">In these cases, you can use hello [HTTP Data Collector API](../log-analytics/log-analytics-data-collector-api.md) toowrite data tooLog Analytics from any REST API client.</span></span>  <span data-ttu-id="8d871-107">Un tooperform méthode commune cette collecte de données à l’aide un runbook dans Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="8d871-107">A common method tooperform this data collection is using a runbook in Azure Automation.</span></span>   

<span data-ttu-id="8d871-108">Ce didacticiel vous guide tout au long processus hello pour la création et la planification d’un runbook dans Azure Automation toowrite données tooLog Analytique.</span><span class="sxs-lookup"><span data-stu-id="8d871-108">This tutorial walks through hello process for creating and scheduling a runbook in Azure Automation toowrite data tooLog Analytics.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="8d871-109">Composants requis</span><span class="sxs-lookup"><span data-stu-id="8d871-109">Prerequisites</span></span>
<span data-ttu-id="8d871-110">Ce scénario nécessite hello suivant les ressources configurées dans votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="8d871-110">This scenario requires hello following resources configured in your Azure subscription.</span></span>  <span data-ttu-id="8d871-111">Les deux peuvent être des comptes gratuits.</span><span class="sxs-lookup"><span data-stu-id="8d871-111">Both can be a free account.</span></span>

- <span data-ttu-id="8d871-112">[Espace de travail Log Analytics](../log-analytics/log-analytics-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="8d871-112">[Log Analytics workspace](../log-analytics/log-analytics-get-started.md).</span></span>
- <span data-ttu-id="8d871-113">[Compte Azure Automation](../automation/automation-offering-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="8d871-113">[Azure automation account](../automation/automation-offering-get-started.md).</span></span>

## <a name="overview-of-scenario"></a><span data-ttu-id="8d871-114">Présentation du scénario</span><span class="sxs-lookup"><span data-stu-id="8d871-114">Overview of scenario</span></span>
<span data-ttu-id="8d871-115">Pour ce didacticiel, vous allez écrire un runbook qui collecte les informations sur les tâches Automation.</span><span class="sxs-lookup"><span data-stu-id="8d871-115">For this tutorial, you'll write a runbook that collects information about Automation jobs.</span></span>  <span data-ttu-id="8d871-116">Runbooks d’Azure Automation sont implémentés avec PowerShell, afin que vous allez commencer à écrire et tester un script dans l’éditeur d’Azure Automation hello.</span><span class="sxs-lookup"><span data-stu-id="8d871-116">Runbooks in Azure Automation are implemented with PowerShell, so you'll start by writing and testing a script in hello Azure Automation editor.</span></span>  <span data-ttu-id="8d871-117">Une fois que vous avez vérifié que vous collectez des informations de hello requis, vous écrire ce tooLog données Analytique et vérifier le type de données personnalisé hello.</span><span class="sxs-lookup"><span data-stu-id="8d871-117">Once you verify that you're collecting hello required information, you'll write that data tooLog Analytics and verify hello custom data type.</span></span>  <span data-ttu-id="8d871-118">Enfin, vous allez créer un runbook de hello planification toostart à intervalles réguliers.</span><span class="sxs-lookup"><span data-stu-id="8d871-118">Finally, you'll create a schedule toostart hello runbook at regular intervals.</span></span>

> [!NOTE]
> <span data-ttu-id="8d871-119">Vous pouvez configurer Azure Automation toosend travail informations tooLog Analytique sans ce runbook.</span><span class="sxs-lookup"><span data-stu-id="8d871-119">You can configure Azure Automation toosend job information tooLog Analytics without this runbook.</span></span>  <span data-ttu-id="8d871-120">Ce scénario est principalement le didacticiel de hello toosupport utilisés, et il est recommandé que vous envoyez un espace de travail de test à tooa hello données.</span><span class="sxs-lookup"><span data-stu-id="8d871-120">This scenario is primarily used toosupport hello tutorial, and it's recommended that you send hello data tooa test workspace.</span></span>  


## <a name="1-install-data-collector-api-module"></a><span data-ttu-id="8d871-121">1. Installer le module de l’API du collecteur de données</span><span class="sxs-lookup"><span data-stu-id="8d871-121">1. Install Data Collector API module</span></span>
<span data-ttu-id="8d871-122">Chaque [demande à partir de l’API du collecteur de données HTTP de hello](../log-analytics/log-analytics-data-collector-api.md#create-a-request) doit être correctement mises en forme et d’inclure un en-tête d’autorisation.</span><span class="sxs-lookup"><span data-stu-id="8d871-122">Every [request from hello HTTP Data Collector API](../log-analytics/log-analytics-data-collector-api.md#create-a-request) must be formatted appropriately and include an authorization header.</span></span>  <span data-ttu-id="8d871-123">Vous pouvez l’effectuer dans votre runbook, mais vous pouvez réduire hello code nécessaire à l’aide d’un module qui simplifie ce processus.</span><span class="sxs-lookup"><span data-stu-id="8d871-123">You can do this in your runbook, but you can reduce hello amount of code required by using a module that simplifies this process.</span></span>  <span data-ttu-id="8d871-124">Un module que vous pouvez utiliser est [OMSIngestionAPI module](https://www.powershellgallery.com/packages/OMSIngestionAPI) Bonjour PowerShell Gallery.</span><span class="sxs-lookup"><span data-stu-id="8d871-124">One module that you can use is [OMSIngestionAPI module](https://www.powershellgallery.com/packages/OMSIngestionAPI) in hello PowerShell Gallery.</span></span>

<span data-ttu-id="8d871-125">toouse un [module](../automation/automation-integration-modules.md) dans un runbook, il doit être installé dans votre compte Automation.</span><span class="sxs-lookup"><span data-stu-id="8d871-125">toouse a [module](../automation/automation-integration-modules.md) in a runbook, it must be installed in your Automation account.</span></span>  <span data-ttu-id="8d871-126">N’importe quel runbook dans le même compte peut ensuite utiliser de hello hello fonctions hello module.</span><span class="sxs-lookup"><span data-stu-id="8d871-126">Any runbook in hello same account can then use hello functions in hello module.</span></span>  <span data-ttu-id="8d871-127">Vous pouvez installer un module en sélectionnant **Ressources** > **Modules** > **Ajouter un module** dans votre compte Automation.</span><span class="sxs-lookup"><span data-stu-id="8d871-127">You can install a new module by selecting **Assets** > **Modules** > **Add a module** in your Automation account.</span></span>  

<span data-ttu-id="8d871-128">Hello PowerShell Gallery cependant vous donne un toodeploy option rapide un module directement tooyour automation compte afin de pouvoir utiliser cette option pour ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="8d871-128">hello PowerShell Gallery though gives you a quick option toodeploy a module directly tooyour automation account so you can use that option for this tutorial.</span></span>  

![Module OMSIngestionAPI](media/operations-management-suite-runbook-datacollect/OMSIngestionAPI.png)

1. <span data-ttu-id="8d871-130">Accédez trop[PowerShell Gallery](https://www.powershellgallery.com/).</span><span class="sxs-lookup"><span data-stu-id="8d871-130">Go too[PowerShell Gallery](https://www.powershellgallery.com/).</span></span>
2. <span data-ttu-id="8d871-131">Recherchez **OMSIngestionAPI**.</span><span class="sxs-lookup"><span data-stu-id="8d871-131">Search for **OMSIngestionAPI**.</span></span>
3. <span data-ttu-id="8d871-132">Cliquez sur hello **déployer tooAzure Automation** bouton.</span><span class="sxs-lookup"><span data-stu-id="8d871-132">Click on hello **Deploy tooAzure Automation** button.</span></span>
4. <span data-ttu-id="8d871-133">Sélectionnez votre compte automation, cliquez sur **OK** module de hello tooinstall.</span><span class="sxs-lookup"><span data-stu-id="8d871-133">Select your automation account and click **OK** tooinstall hello module.</span></span>


## <a name="2-create-automation-variables"></a><span data-ttu-id="8d871-134">2. Créer des variables Automation</span><span class="sxs-lookup"><span data-stu-id="8d871-134">2. Create Automation variables</span></span>
<span data-ttu-id="8d871-135">Les [variables Automation](..\automation\automation-variables.md) contiennent des valeurs qui peuvent être utilisées par tous les runbooks de votre compte Automation.</span><span class="sxs-lookup"><span data-stu-id="8d871-135">[Automation variables](..\automation\automation-variables.md) hold values that can be used by all runbooks in your Automation account.</span></span>  <span data-ttu-id="8d871-136">Celles-ci permettent de procédures opérationnelles plus flexible en vous toochange ces valeurs sans avoir à modifier hello runbook réel.</span><span class="sxs-lookup"><span data-stu-id="8d871-136">They make runbooks more flexible by allowing you toochange these values without editing hello actual runbook.</span></span> <span data-ttu-id="8d871-137">Chaque demande hello API du collecteur de données HTTP nécessite une ID de hello et la clé de l’espace de travail OMS hello et les ressources de variables toostore idéale ces informations.</span><span class="sxs-lookup"><span data-stu-id="8d871-137">Every request from hello HTTP Data Collector API requires hello ID and key of hello OMS workspace, and variable assets are ideal toostore this information.</span></span>  

![variables](media/operations-management-suite-runbook-datacollect/variables.png)

1. <span data-ttu-id="8d871-139">Bonjour portail Azure, accédez à compte Automation de tooyour.</span><span class="sxs-lookup"><span data-stu-id="8d871-139">In hello Azure portal, navigate tooyour Automation account.</span></span>
2. <span data-ttu-id="8d871-140">Sélectionnez **Variables** sous **Ressources partagées**.</span><span class="sxs-lookup"><span data-stu-id="8d871-140">Select **Variables** under **Shared Resources**.</span></span>
2. <span data-ttu-id="8d871-141">Cliquez sur **ajouter une variable** et créer des deux variables hello Bonjour tableau suivant.</span><span class="sxs-lookup"><span data-stu-id="8d871-141">Click **Add a variable** and create hello two variables in hello following table.</span></span>

| <span data-ttu-id="8d871-142">Propriété</span><span class="sxs-lookup"><span data-stu-id="8d871-142">Property</span></span> | <span data-ttu-id="8d871-143">Valeur d’ID d’espace de travail</span><span class="sxs-lookup"><span data-stu-id="8d871-143">Workspace ID Value</span></span> | <span data-ttu-id="8d871-144">Valeur de clé d’espace de travail</span><span class="sxs-lookup"><span data-stu-id="8d871-144">Workspace Key Value</span></span> |
|:--|:--|:--|
| <span data-ttu-id="8d871-145">Nom</span><span class="sxs-lookup"><span data-stu-id="8d871-145">Name</span></span> | <span data-ttu-id="8d871-146">WorkspaceID</span><span class="sxs-lookup"><span data-stu-id="8d871-146">WorkspaceId</span></span> | <span data-ttu-id="8d871-147">WorkspaceKey</span><span class="sxs-lookup"><span data-stu-id="8d871-147">WorkspaceKey</span></span> |
| <span data-ttu-id="8d871-148">Type</span><span class="sxs-lookup"><span data-stu-id="8d871-148">Type</span></span> | <span data-ttu-id="8d871-149">String</span><span class="sxs-lookup"><span data-stu-id="8d871-149">String</span></span> | <span data-ttu-id="8d871-150">String</span><span class="sxs-lookup"><span data-stu-id="8d871-150">String</span></span> |
| <span data-ttu-id="8d871-151">Valeur</span><span class="sxs-lookup"><span data-stu-id="8d871-151">Value</span></span> | <span data-ttu-id="8d871-152">Collez hello ID de l’espace de travail de votre espace de travail Analytique de journal.</span><span class="sxs-lookup"><span data-stu-id="8d871-152">Paste in hello Workspace ID of your Log Analytics workspace.</span></span> | <span data-ttu-id="8d871-153">Coller avec hello clé primaire ou secondaire de votre espace de travail Analytique de journal.</span><span class="sxs-lookup"><span data-stu-id="8d871-153">Paste in with hello Primary or Secondary Key of your Log Analytics workspace.</span></span> |
| <span data-ttu-id="8d871-154">Chiffré</span><span class="sxs-lookup"><span data-stu-id="8d871-154">Encrypted</span></span> | <span data-ttu-id="8d871-155">Non</span><span class="sxs-lookup"><span data-stu-id="8d871-155">No</span></span> | <span data-ttu-id="8d871-156">Oui</span><span class="sxs-lookup"><span data-stu-id="8d871-156">Yes</span></span> |



## <a name="3-create-runbook"></a><span data-ttu-id="8d871-157">3. Créer un runbook</span><span class="sxs-lookup"><span data-stu-id="8d871-157">3. Create runbook</span></span>

<span data-ttu-id="8d871-158">Azure Automation dispose d’un éditeur dans le portail hello où vous pouvez modifier et tester votre runbook.</span><span class="sxs-lookup"><span data-stu-id="8d871-158">Azure Automation has an editor in hello portal where you can edit and test your runbook.</span></span>  <span data-ttu-id="8d871-159">Vous avez hello option toouse hello script éditeur toowork avec [PowerShell directement](../automation/automation-edit-textual-runbook.md) ou [créer un runbook graphique](../automation/automation-graphical-authoring-intro.md).</span><span class="sxs-lookup"><span data-stu-id="8d871-159">You have hello option toouse hello script editor toowork with [PowerShell directly](../automation/automation-edit-textual-runbook.md) or [create a graphical runbook](../automation/automation-graphical-authoring-intro.md).</span></span>  <span data-ttu-id="8d871-160">Pour ce didacticiel, vous allez travailler avec un script PowerShell.</span><span class="sxs-lookup"><span data-stu-id="8d871-160">For this tutorial, you will work with a PowerShell script.</span></span> 

![Modifier un runbook](media/operations-management-suite-runbook-datacollect/edit-runbook.png)

1. <span data-ttu-id="8d871-162">Accédez à compte Automation de tooyour.</span><span class="sxs-lookup"><span data-stu-id="8d871-162">Navigate tooyour Automation account.</span></span>  
2. <span data-ttu-id="8d871-163">Cliquez sur **Runbooks** > **Ajouter un runbook** > **Create a new runbook** (Créer un runbook).</span><span class="sxs-lookup"><span data-stu-id="8d871-163">Click **Runbooks** > **Add a runbook** > **Create a new runbook**.</span></span>
3. <span data-ttu-id="8d871-164">Pour le nom du runbook hello, tapez **tâches d’automatisation collecter**.</span><span class="sxs-lookup"><span data-stu-id="8d871-164">For hello runbook name, type **Collect-Automation-jobs**.</span></span>  <span data-ttu-id="8d871-165">Pour le type de runbook hello, sélectionnez **PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="8d871-165">For hello runbook type, select **PowerShell**.</span></span>
4. <span data-ttu-id="8d871-166">Cliquez sur **créer** toocreate hello runbook et démarrer hello l’éditeur.</span><span class="sxs-lookup"><span data-stu-id="8d871-166">Click **Create** toocreate hello runbook and start hello editor.</span></span>
5. <span data-ttu-id="8d871-167">Copiez et collez hello après le code dans les runbook hello.</span><span class="sxs-lookup"><span data-stu-id="8d871-167">Copy and paste hello following code into hello runbook.</span></span>  <span data-ttu-id="8d871-168">Consultez toohello des commentaires dans le script de hello pour une explication du code de hello.</span><span class="sxs-lookup"><span data-stu-id="8d871-168">Refer toohello comments in hello script for explanation of hello code.</span></span>
    
        # Get information required for hello automation account from parameter values when hello runbook is started.
        Param
        (
            [Parameter(Mandatory = $True)]
            [string]$resourceGroupName,
            [Parameter(Mandatory = $True)]
            [string]$automationAccountName
        )
        
        # Authenticate toohello Automation account using hello Azure connection created when hello Automation account was created.
        # Code copied from hello runbook AzureAutomationTutorial.
        $connectionName = "AzureRunAsConnection"
        $servicePrincipalConnection=Get-AutomationConnection -Name $connectionName         
        Add-AzureRmAccount `
            -ServicePrincipal `
            -TenantId $servicePrincipalConnection.TenantId `
            -ApplicationId $servicePrincipalConnection.ApplicationId `
            -CertificateThumbprint $servicePrincipalConnection.CertificateThumbprint 
        
        # Set hello $VerbosePreference variable so that we get verbose output in test environment.
        $VerbosePreference = "Continue"
        
        # Get information required for Log Analytics workspace from Automation variables.
        $customerId = Get-AutomationVariable -Name 'WorkspaceID'
        $sharedKey = Get-AutomationVariable -Name 'WorkspaceKey'
        
        # Set hello name of hello record type.
        $logType = "AutomationJob"
        
        # Get hello jobs from hello past hour.
        $jobs = Get-AzureRmAutomationJob -ResourceGroupName $resourceGroupName -AutomationAccountName $automationAccountName -StartTime (Get-Date).AddHours(-1)
        
        if ($jobs -ne $null) {
            # Convert hello job data toojson
            $body = $jobs | ConvertTo-Json
        
            # Write hello body tooverbose output so we can inspect it if verbose logging is on for hello runbook.
            Write-Verbose $body
        
            # Send hello data tooLog Analytics.
            Send-OMSAPIIngestionFile -customerId $customerId -sharedKey $sharedKey -body $body -logType $logType -TimeStampField CreationTime
        }


## <a name="4-test-runbook"></a><span data-ttu-id="8d871-169">4. Tester le runbook</span><span class="sxs-lookup"><span data-stu-id="8d871-169">4. Test runbook</span></span>
<span data-ttu-id="8d871-170">Azure Automation inclut un environnement trop[tester votre runbook](../automation/automation-testing-runbook.md) avant de le publier.</span><span class="sxs-lookup"><span data-stu-id="8d871-170">Azure Automation includes an environment too[test your runbook](../automation/automation-testing-runbook.md) before you publish it.</span></span>  <span data-ttu-id="8d871-171">Vous pouvez inspecter les données hello collectées par les runbook hello et vérifiez qu’il écrit tooLog Analytique comme prévu avant sa publication tooproduction.</span><span class="sxs-lookup"><span data-stu-id="8d871-171">You can inspect hello data collected by hello runbook and verify that it writes tooLog Analytics as expected before publishing it tooproduction.</span></span> 
 
![Tester le runbook](media/operations-management-suite-runbook-datacollect/test-runbook.png)

6. <span data-ttu-id="8d871-173">Cliquez sur **enregistrer** toosave hello runbook.</span><span class="sxs-lookup"><span data-stu-id="8d871-173">Click **Save** toosave hello runbook.</span></span>
1. <span data-ttu-id="8d871-174">Cliquez sur **Test volet** runbook de hello tooopen dans l’environnement de test hello.</span><span class="sxs-lookup"><span data-stu-id="8d871-174">Click **Test pane** tooopen hello runbook in hello test environment.</span></span>
3. <span data-ttu-id="8d871-175">Depuis votre runbook possède des paramètres, vous êtes valeurs demandées par invite tooenter pour eux.</span><span class="sxs-lookup"><span data-stu-id="8d871-175">Since your runbook has parameters, you're prompted tooenter values for them.</span></span>  <span data-ttu-id="8d871-176">Entrez le nom hello hello du groupe de ressources et automatisation de hello qui compte vos informations de tâche toocollect continu à partir de.</span><span class="sxs-lookup"><span data-stu-id="8d871-176">Enter hello name of hello resource group and hello automation account that your going toocollect job information from.</span></span>
4. <span data-ttu-id="8d871-177">Cliquez sur **Démarrer** toohello démarrer hello runbook.</span><span class="sxs-lookup"><span data-stu-id="8d871-177">Click **Start** toohello start hello runbook.</span></span>
3. <span data-ttu-id="8d871-178">Hello runbook démarre avec l’état **en file d’attente** avant d’entrer trop**en cours d’exécution**.</span><span class="sxs-lookup"><span data-stu-id="8d871-178">hello runbook will start with a status of **Queued** before it goes too**Running**.</span></span>  
3. <span data-ttu-id="8d871-179">Hello runbook doit afficher la sortie des commentaires avec les travaux hello collectées au format json.</span><span class="sxs-lookup"><span data-stu-id="8d871-179">hello runbook should display verbose output with hello jobs collected in json format.</span></span>  <span data-ttu-id="8d871-180">Si aucune tâche n’est répertorié, puis qu’il n’y ait aucune tâche créée dans le compte d’automatisation hello Bonjour dernière heure.</span><span class="sxs-lookup"><span data-stu-id="8d871-180">If no jobs are listed, then there may have been no jobs created in hello automation account in hello last hour.</span></span>  <span data-ttu-id="8d871-181">Essayez de démarrer n’importe quel runbook dans le compte d’automatisation hello et puis effectuez à nouveau le test de hello.</span><span class="sxs-lookup"><span data-stu-id="8d871-181">Try starting any runbook in hello automation account and then perform hello test again.</span></span>
4. <span data-ttu-id="8d871-182">Vérifiez que la sortie de hello n’affiche pas que les erreurs de hello valider commande tooLog Analytique.</span><span class="sxs-lookup"><span data-stu-id="8d871-182">Ensure that hello output doesn't show any errors in hello post command tooLog Analytics.</span></span>  <span data-ttu-id="8d871-183">Vous devez disposer d’un message similaire toohello.</span><span class="sxs-lookup"><span data-stu-id="8d871-183">You should have a message similar toohello following.</span></span>

    ![Sortie post](media/operations-management-suite-runbook-datacollect/post-output.png)

## <a name="5-verify-records-in-log-analytics"></a><span data-ttu-id="8d871-185">5. Vérifier les enregistrements dans Log Analytics</span><span class="sxs-lookup"><span data-stu-id="8d871-185">5. Verify records in Log Analytics</span></span>
<span data-ttu-id="8d871-186">Une fois hello runbook s’est terminée dans le test, et vous avez vérifié que le résultat de hello a été reçue, vous pouvez vérifier que les enregistrements de hello ont été créés à l’aide un [recherche de journal dans le journal Analytique](../log-analytics/log-analytics-log-searches.md).</span><span class="sxs-lookup"><span data-stu-id="8d871-186">Once hello runbook has completed in test, and you verified that hello output was successfully received, you can verify that hello records were created using a [log search in Log Analytics](../log-analytics/log-analytics-log-searches.md).</span></span>

![Sortie du journal](media/operations-management-suite-runbook-datacollect/log-output.png)

1. <span data-ttu-id="8d871-188">Bonjour portail Azure, sélectionnez votre espace de travail Analytique de journal.</span><span class="sxs-lookup"><span data-stu-id="8d871-188">In hello Azure portal, select your Log Analytics workspace.</span></span>
2. <span data-ttu-id="8d871-189">Cliquez sur **Recherche dans les journaux**.</span><span class="sxs-lookup"><span data-stu-id="8d871-189">Click on **Log Search**.</span></span>
3. <span data-ttu-id="8d871-190">Hello type commande suivante `Type=AutomationJob_CL` et cliquez sur le bouton de recherche hello.</span><span class="sxs-lookup"><span data-stu-id="8d871-190">Type hello following command `Type=AutomationJob_CL` and click hello search button.</span></span> <span data-ttu-id="8d871-191">Notez que le type d’enregistrement hello inclut _CL n’est pas spécifié dans le script de hello.</span><span class="sxs-lookup"><span data-stu-id="8d871-191">Note that hello record type includes _CL that isn't specified in hello script.</span></span>  <span data-ttu-id="8d871-192">Ce suffixe est ajouté automatiquement toohello journal type tooindicate qu’il s’agit d’un type de journal personnalisé.</span><span class="sxs-lookup"><span data-stu-id="8d871-192">That suffix is automatically appended toohello log type tooindicate that it's a custom log type.</span></span>
4. <span data-ttu-id="8d871-193">Vous devez voir un ou plusieurs enregistrements retournées indiquant que ce runbook hello fonctionne comme prévu.</span><span class="sxs-lookup"><span data-stu-id="8d871-193">You should see one or more records returned indicating that hello runbook is working as expected.</span></span>


## <a name="6-publish-hello-runbook"></a><span data-ttu-id="8d871-194">6. Publier hello runbook</span><span class="sxs-lookup"><span data-stu-id="8d871-194">6. Publish hello runbook</span></span>
<span data-ttu-id="8d871-195">Une fois que vous avez vérifié que runbook hello fonctionne correctement, vous devez toopublish il est donc vous pouvez l’exécuter en production.</span><span class="sxs-lookup"><span data-stu-id="8d871-195">Once you've verified that hello runbook is working correctly, you need toopublish it so you can run it in production.</span></span>  <span data-ttu-id="8d871-196">Vous pouvez continuer tooedit et hello runbook de test sans modifier la version publiée de hello.</span><span class="sxs-lookup"><span data-stu-id="8d871-196">You can continue tooedit and test hello runbook without modifying hello published version.</span></span>  

![Publier le runbook](media/operations-management-suite-runbook-datacollect/publish-runbook.png)

1. <span data-ttu-id="8d871-198">Compte d’automatisation tooyour de retour.</span><span class="sxs-lookup"><span data-stu-id="8d871-198">Return tooyour automation account.</span></span>
2. <span data-ttu-id="8d871-199">Cliquez sur **Runbooks** et sélectionnez **Collect-Automation-jobs**.</span><span class="sxs-lookup"><span data-stu-id="8d871-199">Click on **Runbooks** and select **Collect-Automation-jobs**.</span></span>
3. <span data-ttu-id="8d871-200">Cliquez sur **Modifier**, puis sur **Publier**.</span><span class="sxs-lookup"><span data-stu-id="8d871-200">Click **Edit** and then **Publish**.</span></span>
4. <span data-ttu-id="8d871-201">Cliquez sur **Oui** lorsque tooverify fréquentes que vous souhaitez toooverwrite hello précédemment version publiée.</span><span class="sxs-lookup"><span data-stu-id="8d871-201">Click **Yes** when asked tooverify that you want toooverwrite hello previously published version.</span></span>

## <a name="7-set-logging-options"></a><span data-ttu-id="8d871-202">7. Définir les options de journalisation</span><span class="sxs-lookup"><span data-stu-id="8d871-202">7. Set logging options</span></span> 
<span data-ttu-id="8d871-203">Pour le test, vous ont été en mesure de tooview [documenté](../automation/automation-runbook-output-and-messages.md#message-streams) car vous définir la variable de hello $VerbosePreference dans le script de hello.</span><span class="sxs-lookup"><span data-stu-id="8d871-203">For test, you were able tooview [verbose output](../automation/automation-runbook-output-and-messages.md#message-streams) because you set hello $VerbosePreference variable in hello script.</span></span>  <span data-ttu-id="8d871-204">Pour la production, vous devez les propriétés de journalisation de hello de tooset pour hello runbook si vous souhaitez que la sortie des commentaires tooview.</span><span class="sxs-lookup"><span data-stu-id="8d871-204">For production, you need tooset hello logging properties for hello runbook if you want tooview verbose output.</span></span>  <span data-ttu-id="8d871-205">Runbook hello utilisé dans ce didacticiel, les données de json hello envoyées tooLog Analytique s’affiche.</span><span class="sxs-lookup"><span data-stu-id="8d871-205">For hello runbook used in this tutorial, this will display hello json data being sent tooLog Analytics.</span></span>

![Journalisation et suivi](media/operations-management-suite-runbook-datacollect/logging.png)

1. <span data-ttu-id="8d871-207">Dans Propriétés hello votre runbook sélectionnez **journalisation et le suivi** sous **Runbook paramètres**.</span><span class="sxs-lookup"><span data-stu-id="8d871-207">In hello properties for your runbook select **Logging and tracing** under **Runbook Settings**.</span></span>
2. <span data-ttu-id="8d871-208">Modification du paramètre hello pour **journaliser les enregistrements détaillés** trop**sur**.</span><span class="sxs-lookup"><span data-stu-id="8d871-208">Change hello setting for **Log verbose records** too**On**.</span></span>
3. <span data-ttu-id="8d871-209">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="8d871-209">Click **Save**.</span></span>

## <a name="8-schedule-runbook"></a><span data-ttu-id="8d871-210">8. Planifier un runbook</span><span class="sxs-lookup"><span data-stu-id="8d871-210">8. Schedule runbook</span></span>
<span data-ttu-id="8d871-211">Bonjour courants toostart façon un runbook qui collecte les données d’analyse est tooschedule il toorun automatiquement.</span><span class="sxs-lookup"><span data-stu-id="8d871-211">hello most common way toostart a runbook that collects monitoring data is tooschedule it toorun automatically.</span></span>  <span data-ttu-id="8d871-212">Pour cela, vous devez créer un [planification dans Azure Automation](../automation/automation-schedules.md) et en l’attachant tooyour runbook.</span><span class="sxs-lookup"><span data-stu-id="8d871-212">You do this by creating a [schedule in Azure Automation](../automation/automation-schedules.md) and attaching it tooyour runbook.</span></span>

![Planifier un runbook](media/operations-management-suite-runbook-datacollect/schedule-runbook.png)

1. <span data-ttu-id="8d871-214">Dans Propriétés hello votre runbook, sélectionnez **planifications** sous **ressources**.</span><span class="sxs-lookup"><span data-stu-id="8d871-214">In hello properties for your runbook, select **Schedules** under **Resources**.</span></span>
2. <span data-ttu-id="8d871-215">Cliquez sur **ajouter une planification** > **liez un runbook de tooyour planification** > **créer une planification**.</span><span class="sxs-lookup"><span data-stu-id="8d871-215">Click **Add a schedule** > **Link a schedule tooyour runbook** > **Create a new schedule**.</span></span>
5. <span data-ttu-id="8d871-216">Type Bonjour suivant de valeurs pour la planification de hello et cliquez sur **créer**.</span><span class="sxs-lookup"><span data-stu-id="8d871-216">Type in hello following values for hello schedule and click **Create**.</span></span>

| <span data-ttu-id="8d871-217">Propriété</span><span class="sxs-lookup"><span data-stu-id="8d871-217">Property</span></span> | <span data-ttu-id="8d871-218">Valeur</span><span class="sxs-lookup"><span data-stu-id="8d871-218">Value</span></span> |
|:--|:--|
| <span data-ttu-id="8d871-219">Nom</span><span class="sxs-lookup"><span data-stu-id="8d871-219">Name</span></span> | <span data-ttu-id="8d871-220">AutomationJobs-Hourly</span><span class="sxs-lookup"><span data-stu-id="8d871-220">AutomationJobs-Hourly</span></span> |
| <span data-ttu-id="8d871-221">Démarrages</span><span class="sxs-lookup"><span data-stu-id="8d871-221">Starts</span></span> | <span data-ttu-id="8d871-222">Sélectionnez n’importe quel moment passées au moins 5 minutes hello heure actuelle.</span><span class="sxs-lookup"><span data-stu-id="8d871-222">Select any time at least 5 minutes past hello current time.</span></span> |
| <span data-ttu-id="8d871-223">Périodicité</span><span class="sxs-lookup"><span data-stu-id="8d871-223">Recurrence</span></span> | <span data-ttu-id="8d871-224">Récurrent</span><span class="sxs-lookup"><span data-stu-id="8d871-224">Recurring</span></span> |
| <span data-ttu-id="8d871-225">Répéter toutes les</span><span class="sxs-lookup"><span data-stu-id="8d871-225">Recur every</span></span> | <span data-ttu-id="8d871-226">1 heure</span><span class="sxs-lookup"><span data-stu-id="8d871-226">1 hour</span></span> |
| <span data-ttu-id="8d871-227">Définir une expiration</span><span class="sxs-lookup"><span data-stu-id="8d871-227">Set expiration</span></span> | <span data-ttu-id="8d871-228">Non</span><span class="sxs-lookup"><span data-stu-id="8d871-228">No</span></span> |

<span data-ttu-id="8d871-229">Une fois que la planification de hello est créée, vous devez tooset les valeurs de paramètre hello qui seront utilisés chaque fois que cette planification démarre hello runbook.</span><span class="sxs-lookup"><span data-stu-id="8d871-229">Once hello schedule is created, you need tooset hello parameter values that will be used each time this schedule starts hello runbook.</span></span>

6. <span data-ttu-id="8d871-230">Cliquez sur **Configure parameters and run settings (Configurer les paramètres et les paramètres d’exécution)**.</span><span class="sxs-lookup"><span data-stu-id="8d871-230">Click **Configure parameters and run settings**.</span></span>
7. <span data-ttu-id="8d871-231">Renseignez les valeurs pour **ResourceGroupName** et **AutomationAccountName**.</span><span class="sxs-lookup"><span data-stu-id="8d871-231">Fill in values for your **ResourceGroupName** and **AutomationAccountName**.</span></span>
8. <span data-ttu-id="8d871-232">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="8d871-232">Click **OK**.</span></span> 

## <a name="9-verify-runbook-starts-on-schedule"></a><span data-ttu-id="8d871-233">9. Vérifier la conformité du démarrage du runbook avec la planification</span><span class="sxs-lookup"><span data-stu-id="8d871-233">9. Verify runbook starts on schedule</span></span>
<span data-ttu-id="8d871-234">À chaque démarrage d’un runbook, [un travail est créé](../automation/automation-runbook-execution.md) et toute sortie est enregistrée.</span><span class="sxs-lookup"><span data-stu-id="8d871-234">Everytime a runbook is started, [a job is created](../automation/automation-runbook-execution.md) and any output logged.</span></span>  <span data-ttu-id="8d871-235">En fait, il s’agit de hello collecte les mêmes tâches que hello runbook.</span><span class="sxs-lookup"><span data-stu-id="8d871-235">In fact, these are hello same jobs that hello runbook is collecting.</span></span>  <span data-ttu-id="8d871-236">Vous pouvez vérifier que ce runbook hello démarre comme prévu en vérifiant les travaux hello pour hello runbook après hello pour la planification de hello a commencé.</span><span class="sxs-lookup"><span data-stu-id="8d871-236">You can verify that hello runbook starts as expected by checking hello jobs for hello runbook after hello start time for hello schedule has passed.</span></span>

![Tâches](media/operations-management-suite-runbook-datacollect/jobs.png)

1. <span data-ttu-id="8d871-238">Dans Propriétés hello votre runbook, sélectionnez **travaux** sous **ressources**.</span><span class="sxs-lookup"><span data-stu-id="8d871-238">In hello properties for your runbook, select **Jobs** under **Resources**.</span></span>
2. <span data-ttu-id="8d871-239">Vous devez voir qu'une liste de tâches pour chaque runbook hello de temps a été démarrée.</span><span class="sxs-lookup"><span data-stu-id="8d871-239">You should see a listing of jobs for each time hello runbook was started.</span></span>
3. <span data-ttu-id="8d871-240">Cliquez sur l’un des hello travaux tooview ses détails.</span><span class="sxs-lookup"><span data-stu-id="8d871-240">Click on one of hello jobs tooview its details.</span></span>
4. <span data-ttu-id="8d871-241">Cliquez sur **tous les journaux** tooview hello journaux et sortie à partir de runbook de hello.</span><span class="sxs-lookup"><span data-stu-id="8d871-241">Click on **All logs** tooview hello logs and output from hello runbook.</span></span>
5. <span data-ttu-id="8d871-242">Faites défiler toohello bas toofind une entrée toohello une image similaire ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="8d871-242">Scroll toohello bottom toofind an entry similar toohello image below.</span></span><br>![Détaillé](media/operations-management-suite-runbook-datacollect/verbose.png)
6. <span data-ttu-id="8d871-244">Cliquez sur cette entrée tooview hello détaillées des données json qui a été envoyées tooLog Analytique.</span><span class="sxs-lookup"><span data-stu-id="8d871-244">Click on this entry tooview hello detailed json data  that was sent tooLog Analytics.</span></span>



## <a name="next-steps"></a><span data-ttu-id="8d871-245">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="8d871-245">Next steps</span></span>
- <span data-ttu-id="8d871-246">Utilisez [Concepteur de vue](../log-analytics/log-analytics-view-designer.md) toocreate un affichage hello des données que vous avez collectées référentiel d’Analytique de journal toohello.</span><span class="sxs-lookup"><span data-stu-id="8d871-246">Use [View Designer](../log-analytics/log-analytics-view-designer.md) toocreate a view displaying hello data that you've collected toohello Log Analytics repository.</span></span>
- <span data-ttu-id="8d871-247">Package de votre runbook dans un [solution de gestion](operations-management-suite-solutions-creating.md) toodistribute toocustomers.</span><span class="sxs-lookup"><span data-stu-id="8d871-247">Package your runbook in a [management solution](operations-management-suite-solutions-creating.md) toodistribute toocustomers.</span></span>
- <span data-ttu-id="8d871-248">En savoir plus sur [Log Analytics](https://docs.microsoft.com/azure/log-analytics/).</span><span class="sxs-lookup"><span data-stu-id="8d871-248">Learn more about [Log Analytics](https://docs.microsoft.com/azure/log-analytics/).</span></span>
- <span data-ttu-id="8d871-249">En savoir plus sur [Azure Automation](https://docs.microsoft.com/azure/automation/).</span><span class="sxs-lookup"><span data-stu-id="8d871-249">Learn more about [Azure Automation](https://docs.microsoft.com/azure/automation/).</span></span>
- <span data-ttu-id="8d871-250">En savoir plus sur hello [API du collecteur de données HTTP](../log-analytics/log-analytics-data-collector-api.md).</span><span class="sxs-lookup"><span data-stu-id="8d871-250">Learn more about hello [HTTP Data Collector API](../log-analytics/log-analytics-data-collector-api.md).</span></span>
