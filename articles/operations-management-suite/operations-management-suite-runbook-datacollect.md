---
title: "Collecte des données Log Analytics avec un runbook dans Azure Automation | Microsoft Docs"
description: "Didacticiel étape par étape expliquant comment créer un runbook dans Azure Automation pour collecter des données dans le référentiel OMS en vue de l’analyse par Log Analytics."
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
ms.openlocfilehash: 59f674c9c6404da7f5384539189f41a4ba1a939a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="collect-data-in-log-analytics-with-an-azure-automation-runbook"></a><span data-ttu-id="8bc2b-103">Collecter des données dans Log Analytics avec un runbook Azure Automation</span><span class="sxs-lookup"><span data-stu-id="8bc2b-103">Collect data in Log Analytics with an Azure Automation runbook</span></span>
<span data-ttu-id="8bc2b-104">Vous pouvez collecter une quantité importante de données dans Log Analytics à partir de diverses sources, y compris des [sources de données](../log-analytics/log-analytics-data-sources.md) sur les agents et les [données recueillies à partir d’Azure](../log-analytics/log-analytics-azure-storage.md).</span><span class="sxs-lookup"><span data-stu-id="8bc2b-104">You can collect a significant amount of data in Log Analytics from a variety of sources including [data sources](../log-analytics/log-analytics-data-sources.md) on agents and also [data collected from Azure](../log-analytics/log-analytics-azure-storage.md).</span></span>  <span data-ttu-id="8bc2b-105">Il existe cependant des cas où vous devez recueillir des données qui ne sont pas accessibles via ces sources standard.</span><span class="sxs-lookup"><span data-stu-id="8bc2b-105">There are a scenarios though where you need to collect data that isn't accessible through these standard sources.</span></span>  <span data-ttu-id="8bc2b-106">Dans ce cas, vous pouvez utiliser l’[API Collecte de données HTTP](../log-analytics/log-analytics-data-collector-api.md) pour écrire des données dans Log Analytics à partir de n’importe quel client API REST.</span><span class="sxs-lookup"><span data-stu-id="8bc2b-106">In these cases, you can use the [HTTP Data Collector API](../log-analytics/log-analytics-data-collector-api.md) to write data to Log Analytics from any REST API client.</span></span>  <span data-ttu-id="8bc2b-107">Une méthode courante pour effectuer cette collecte de données consiste à utiliser un runbook dans Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="8bc2b-107">A common method to perform this data collection is using a runbook in Azure Automation.</span></span>   

<span data-ttu-id="8bc2b-108">Ce didacticiel vous guide dans le processus de création et de planification d’un runbook dans Azure Automation pour écrire des données dans Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="8bc2b-108">This tutorial walks through the process for creating and scheduling a runbook in Azure Automation to write data to Log Analytics.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="8bc2b-109">Composants requis</span><span class="sxs-lookup"><span data-stu-id="8bc2b-109">Prerequisites</span></span>
<span data-ttu-id="8bc2b-110">Ce scénario nécessite que les ressources suivantes soient configurées dans votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="8bc2b-110">This scenario requires the following resources configured in your Azure subscription.</span></span>  <span data-ttu-id="8bc2b-111">Les deux peuvent être des comptes gratuits.</span><span class="sxs-lookup"><span data-stu-id="8bc2b-111">Both can be a free account.</span></span>

- <span data-ttu-id="8bc2b-112">[Espace de travail Log Analytics](../log-analytics/log-analytics-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="8bc2b-112">[Log Analytics workspace](../log-analytics/log-analytics-get-started.md).</span></span>
- <span data-ttu-id="8bc2b-113">[Compte Azure Automation](../automation/automation-offering-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="8bc2b-113">[Azure automation account](../automation/automation-offering-get-started.md).</span></span>

## <a name="overview-of-scenario"></a><span data-ttu-id="8bc2b-114">Présentation du scénario</span><span class="sxs-lookup"><span data-stu-id="8bc2b-114">Overview of scenario</span></span>
<span data-ttu-id="8bc2b-115">Pour ce didacticiel, vous allez écrire un runbook qui collecte les informations sur les tâches Automation.</span><span class="sxs-lookup"><span data-stu-id="8bc2b-115">For this tutorial, you'll write a runbook that collects information about Automation jobs.</span></span>  <span data-ttu-id="8bc2b-116">Dans Azure Automation, les runbooks sont implémentés avec PowerShell. Vous devrez donc commencer par écrire et tester un script dans l’éditeur d’Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="8bc2b-116">Runbooks in Azure Automation are implemented with PowerShell, so you'll start by writing and testing a script in the Azure Automation editor.</span></span>  <span data-ttu-id="8bc2b-117">Une fois que vous avez vérifié que vous collectez les informations requises, vous écrirez ces données dans Log Analytics et vérifierez le type de données personnalisé.</span><span class="sxs-lookup"><span data-stu-id="8bc2b-117">Once you verify that you're collecting the required information, you'll write that data to Log Analytics and verify the custom data type.</span></span>  <span data-ttu-id="8bc2b-118">Enfin, vous créerez une planification pour démarrer le runbook à intervalles réguliers.</span><span class="sxs-lookup"><span data-stu-id="8bc2b-118">Finally, you'll create a schedule to start the runbook at regular intervals.</span></span>

> [!NOTE]
> <span data-ttu-id="8bc2b-119">Vous pouvez configurer Azure Automation de manière à envoyer les informations sur les tâches à Log Analytics sans ce runbook.</span><span class="sxs-lookup"><span data-stu-id="8bc2b-119">You can configure Azure Automation to send job information to Log Analytics without this runbook.</span></span>  <span data-ttu-id="8bc2b-120">Ce scénario est principalement utilisé pour prendre en charge le didacticiel. Il est recommandé d’envoyer les données à un espace de travail de test.</span><span class="sxs-lookup"><span data-stu-id="8bc2b-120">This scenario is primarily used to support the tutorial, and it's recommended that you send the data to a test workspace.</span></span>  


## <a name="1-install-data-collector-api-module"></a><span data-ttu-id="8bc2b-121">1. Installer le module de l’API du collecteur de données</span><span class="sxs-lookup"><span data-stu-id="8bc2b-121">1. Install Data Collector API module</span></span>
<span data-ttu-id="8bc2b-122">Chaque [requête émanant de l’API du collecteur de données HTTP](../log-analytics/log-analytics-data-collector-api.md#create-a-request) doit être correctement mise en forme et inclure un en-tête d’autorisation.</span><span class="sxs-lookup"><span data-stu-id="8bc2b-122">Every [request from the HTTP Data Collector API](../log-analytics/log-analytics-data-collector-api.md#create-a-request) must be formatted appropriately and include an authorization header.</span></span>  <span data-ttu-id="8bc2b-123">Vous pouvez effectuer ces actions dans votre runbook, mais vous pouvez réduire la quantité de code nécessaire en utilisant un module qui simplifie ce processus.</span><span class="sxs-lookup"><span data-stu-id="8bc2b-123">You can do this in your runbook, but you can reduce the amount of code required by using a module that simplifies this process.</span></span>  <span data-ttu-id="8bc2b-124">Vous pouvez par exemple utiliser le [module OMSIngestionAPI](https://www.powershellgallery.com/packages/OMSIngestionAPI) disponible dans PowerShell Gallery.</span><span class="sxs-lookup"><span data-stu-id="8bc2b-124">One module that you can use is [OMSIngestionAPI module](https://www.powershellgallery.com/packages/OMSIngestionAPI) in the PowerShell Gallery.</span></span>

<span data-ttu-id="8bc2b-125">Pour utiliser un [module](../automation/automation-integration-modules.md) dans un runbook, il doit être installé dans votre compte Automation.</span><span class="sxs-lookup"><span data-stu-id="8bc2b-125">To use a [module](../automation/automation-integration-modules.md) in a runbook, it must be installed in your Automation account.</span></span>  <span data-ttu-id="8bc2b-126">Tout runbook du même compte peut ensuite utiliser les fonctionnalités du module.</span><span class="sxs-lookup"><span data-stu-id="8bc2b-126">Any runbook in the same account can then use the functions in the module.</span></span>  <span data-ttu-id="8bc2b-127">Vous pouvez installer un module en sélectionnant **Ressources** > **Modules** > **Ajouter un module** dans votre compte Automation.</span><span class="sxs-lookup"><span data-stu-id="8bc2b-127">You can install a new module by selecting **Assets** > **Modules** > **Add a module** in your Automation account.</span></span>  

<span data-ttu-id="8bc2b-128">PowerShell Gallery offre cependant une option rapide pour déployer un module directement sur votre compte Automation afin de pouvoir utiliser cette option pour ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="8bc2b-128">The PowerShell Gallery though gives you a quick option to deploy a module directly to your automation account so you can use that option for this tutorial.</span></span>  

![Module OMSIngestionAPI](media/operations-management-suite-runbook-datacollect/OMSIngestionAPI.png)

1. <span data-ttu-id="8bc2b-130">Accédez à [PowerShell Gallery](https://www.powershellgallery.com/).</span><span class="sxs-lookup"><span data-stu-id="8bc2b-130">Go to [PowerShell Gallery](https://www.powershellgallery.com/).</span></span>
2. <span data-ttu-id="8bc2b-131">Recherchez **OMSIngestionAPI**.</span><span class="sxs-lookup"><span data-stu-id="8bc2b-131">Search for **OMSIngestionAPI**.</span></span>
3. <span data-ttu-id="8bc2b-132">Cliquez sur le bouton **Deploy to Azure Automation** (Déployer sur Azure Automation).</span><span class="sxs-lookup"><span data-stu-id="8bc2b-132">Click on the **Deploy to Azure Automation** button.</span></span>
4. <span data-ttu-id="8bc2b-133">Sélectionnez votre compte Automation, puis cliquez sur **OK** pour installer le module.</span><span class="sxs-lookup"><span data-stu-id="8bc2b-133">Select your automation account and click **OK** to install the module.</span></span>


## <a name="2-create-automation-variables"></a><span data-ttu-id="8bc2b-134">2. Créer des variables Automation</span><span class="sxs-lookup"><span data-stu-id="8bc2b-134">2. Create Automation variables</span></span>
<span data-ttu-id="8bc2b-135">Les [variables Automation](..\automation\automation-variables.md) contiennent des valeurs qui peuvent être utilisées par tous les runbooks de votre compte Automation.</span><span class="sxs-lookup"><span data-stu-id="8bc2b-135">[Automation variables](..\automation\automation-variables.md) hold values that can be used by all runbooks in your Automation account.</span></span>  <span data-ttu-id="8bc2b-136">Elles rendent les runbooks plus souples en vous permettant de modifier ces valeurs sans modifier le runbook en lui-même.</span><span class="sxs-lookup"><span data-stu-id="8bc2b-136">They make runbooks more flexible by allowing you to change these values without editing the actual runbook.</span></span> <span data-ttu-id="8bc2b-137">Chaque requête émanant de l’API du collecteur de données HTTP nécessite l’ID et la clé de l’espace de travail OMS. Les ressources de variables sont idéales pour stocker ces informations.</span><span class="sxs-lookup"><span data-stu-id="8bc2b-137">Every request from the HTTP Data Collector API requires the ID and key of the OMS workspace, and variable assets are ideal to store this information.</span></span>  

![Variables](media/operations-management-suite-runbook-datacollect/variables.png)

1. <span data-ttu-id="8bc2b-139">Sur le Portail Azure, accédez à votre compte Automation.</span><span class="sxs-lookup"><span data-stu-id="8bc2b-139">In the Azure portal, navigate to your Automation account.</span></span>
2. <span data-ttu-id="8bc2b-140">Sélectionnez **Variables** sous **Ressources partagées**.</span><span class="sxs-lookup"><span data-stu-id="8bc2b-140">Select **Variables** under **Shared Resources**.</span></span>
2. <span data-ttu-id="8bc2b-141">Cliquez sur **Ajouter une variable** et créez les deux variables dans le tableau suivant.</span><span class="sxs-lookup"><span data-stu-id="8bc2b-141">Click **Add a variable** and create the two variables in the following table.</span></span>

| <span data-ttu-id="8bc2b-142">Propriété</span><span class="sxs-lookup"><span data-stu-id="8bc2b-142">Property</span></span> | <span data-ttu-id="8bc2b-143">Valeur d’ID d’espace de travail</span><span class="sxs-lookup"><span data-stu-id="8bc2b-143">Workspace ID Value</span></span> | <span data-ttu-id="8bc2b-144">Valeur de clé d’espace de travail</span><span class="sxs-lookup"><span data-stu-id="8bc2b-144">Workspace Key Value</span></span> |
|:--|:--|:--|
| <span data-ttu-id="8bc2b-145">Nom</span><span class="sxs-lookup"><span data-stu-id="8bc2b-145">Name</span></span> | <span data-ttu-id="8bc2b-146">WorkspaceID</span><span class="sxs-lookup"><span data-stu-id="8bc2b-146">WorkspaceId</span></span> | <span data-ttu-id="8bc2b-147">WorkspaceKey</span><span class="sxs-lookup"><span data-stu-id="8bc2b-147">WorkspaceKey</span></span> |
| <span data-ttu-id="8bc2b-148">Type</span><span class="sxs-lookup"><span data-stu-id="8bc2b-148">Type</span></span> | <span data-ttu-id="8bc2b-149">String</span><span class="sxs-lookup"><span data-stu-id="8bc2b-149">String</span></span> | <span data-ttu-id="8bc2b-150">String</span><span class="sxs-lookup"><span data-stu-id="8bc2b-150">String</span></span> |
| <span data-ttu-id="8bc2b-151">Valeur</span><span class="sxs-lookup"><span data-stu-id="8bc2b-151">Value</span></span> | <span data-ttu-id="8bc2b-152">Collez l’ID de votre espace de travail Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="8bc2b-152">Paste in the Workspace ID of your Log Analytics workspace.</span></span> | <span data-ttu-id="8bc2b-153">Collez la clé principale ou secondaire de votre espace de travail Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="8bc2b-153">Paste in with the Primary or Secondary Key of your Log Analytics workspace.</span></span> |
| <span data-ttu-id="8bc2b-154">Chiffré</span><span class="sxs-lookup"><span data-stu-id="8bc2b-154">Encrypted</span></span> | <span data-ttu-id="8bc2b-155">Non</span><span class="sxs-lookup"><span data-stu-id="8bc2b-155">No</span></span> | <span data-ttu-id="8bc2b-156">Oui</span><span class="sxs-lookup"><span data-stu-id="8bc2b-156">Yes</span></span> |



## <a name="3-create-runbook"></a><span data-ttu-id="8bc2b-157">3. Créer un runbook</span><span class="sxs-lookup"><span data-stu-id="8bc2b-157">3. Create runbook</span></span>

<span data-ttu-id="8bc2b-158">Azure Automation fournit un éditeur dans le portail, où vous pouvez modifier et tester votre runbook.</span><span class="sxs-lookup"><span data-stu-id="8bc2b-158">Azure Automation has an editor in the portal where you can edit and test your runbook.</span></span>  <span data-ttu-id="8bc2b-159">Vous pouvez utiliser l’éditeur de script pour travailler avec [PowerShell directement](../automation/automation-edit-textual-runbook.md) ou [créer un runbook graphique](../automation/automation-graphical-authoring-intro.md).</span><span class="sxs-lookup"><span data-stu-id="8bc2b-159">You have the option to use the script editor to work with [PowerShell directly](../automation/automation-edit-textual-runbook.md) or [create a graphical runbook](../automation/automation-graphical-authoring-intro.md).</span></span>  <span data-ttu-id="8bc2b-160">Pour ce didacticiel, vous allez travailler avec un script PowerShell.</span><span class="sxs-lookup"><span data-stu-id="8bc2b-160">For this tutorial, you will work with a PowerShell script.</span></span> 

![Modifier un runbook](media/operations-management-suite-runbook-datacollect/edit-runbook.png)

1. <span data-ttu-id="8bc2b-162">Accédez à votre compte Automation.</span><span class="sxs-lookup"><span data-stu-id="8bc2b-162">Navigate to your Automation account.</span></span>  
2. <span data-ttu-id="8bc2b-163">Cliquez sur **Runbooks** > **Ajouter un runbook** > **Create a new runbook** (Créer un runbook).</span><span class="sxs-lookup"><span data-stu-id="8bc2b-163">Click **Runbooks** > **Add a runbook** > **Create a new runbook**.</span></span>
3. <span data-ttu-id="8bc2b-164">Pour le nom du runbook, saisissez **Collect-Automation-jobs**.</span><span class="sxs-lookup"><span data-stu-id="8bc2b-164">For the runbook name, type **Collect-Automation-jobs**.</span></span>  <span data-ttu-id="8bc2b-165">Pour le type de runbook, sélectionnez **PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="8bc2b-165">For the runbook type, select **PowerShell**.</span></span>
4. <span data-ttu-id="8bc2b-166">Cliquez sur **Créer** pour créer le runbook et démarrer l’éditeur.</span><span class="sxs-lookup"><span data-stu-id="8bc2b-166">Click **Create** to create the runbook and start the editor.</span></span>
5. <span data-ttu-id="8bc2b-167">Copiez et collez le code suivant dans le runbook.</span><span class="sxs-lookup"><span data-stu-id="8bc2b-167">Copy and paste the following code into the runbook.</span></span>  <span data-ttu-id="8bc2b-168">Consultez les commentaires dans le script pour obtenir une explication du code.</span><span class="sxs-lookup"><span data-stu-id="8bc2b-168">Refer to the comments in the script for explanation of the code.</span></span>
    
        # Get information required for the automation account from parameter values when the runbook is started.
        Param
        (
            [Parameter(Mandatory = $True)]
            [string]$resourceGroupName,
            [Parameter(Mandatory = $True)]
            [string]$automationAccountName
        )
        
        # Authenticate to the Automation account using the Azure connection created when the Automation account was created.
        # Code copied from the runbook AzureAutomationTutorial.
        $connectionName = "AzureRunAsConnection"
        $servicePrincipalConnection=Get-AutomationConnection -Name $connectionName         
        Add-AzureRmAccount `
            -ServicePrincipal `
            -TenantId $servicePrincipalConnection.TenantId `
            -ApplicationId $servicePrincipalConnection.ApplicationId `
            -CertificateThumbprint $servicePrincipalConnection.CertificateThumbprint 
        
        # Set the $VerbosePreference variable so that we get verbose output in test environment.
        $VerbosePreference = "Continue"
        
        # Get information required for Log Analytics workspace from Automation variables.
        $customerId = Get-AutomationVariable -Name 'WorkspaceID'
        $sharedKey = Get-AutomationVariable -Name 'WorkspaceKey'
        
        # Set the name of the record type.
        $logType = "AutomationJob"
        
        # Get the jobs from the past hour.
        $jobs = Get-AzureRmAutomationJob -ResourceGroupName $resourceGroupName -AutomationAccountName $automationAccountName -StartTime (Get-Date).AddHours(-1)
        
        if ($jobs -ne $null) {
            # Convert the job data to json
            $body = $jobs | ConvertTo-Json
        
            # Write the body to verbose output so we can inspect it if verbose logging is on for the runbook.
            Write-Verbose $body
        
            # Send the data to Log Analytics.
            Send-OMSAPIIngestionFile -customerId $customerId -sharedKey $sharedKey -body $body -logType $logType -TimeStampField CreationTime
        }


## <a name="4-test-runbook"></a><span data-ttu-id="8bc2b-169">4. Tester le runbook</span><span class="sxs-lookup"><span data-stu-id="8bc2b-169">4. Test runbook</span></span>
<span data-ttu-id="8bc2b-170">Azure Automation inclut un environnement permettant de [tester votre runbook](../automation/automation-testing-runbook.md) avant de le publier.</span><span class="sxs-lookup"><span data-stu-id="8bc2b-170">Azure Automation includes an environment to [test your runbook](../automation/automation-testing-runbook.md) before you publish it.</span></span>  <span data-ttu-id="8bc2b-171">Vous pouvez inspecter les données collectées par le runbook et vérifiez que l’écriture dans Log Analytics est correcte avant de publier le runbook pour production.</span><span class="sxs-lookup"><span data-stu-id="8bc2b-171">You can inspect the data collected by the runbook and verify that it writes to Log Analytics as expected before publishing it to production.</span></span> 
 
![Tester le runbook](media/operations-management-suite-runbook-datacollect/test-runbook.png)

6. <span data-ttu-id="8bc2b-173">Cliquez sur **Enregistrer** pour enregistrer le runbook.</span><span class="sxs-lookup"><span data-stu-id="8bc2b-173">Click **Save** to save the runbook.</span></span>
1. <span data-ttu-id="8bc2b-174">Cliquez sur **Volet de test** pour ouvrir le runbook dans l’environnement de test.</span><span class="sxs-lookup"><span data-stu-id="8bc2b-174">Click **Test pane** to open the runbook in the test environment.</span></span>
3. <span data-ttu-id="8bc2b-175">Étant donné que votre runbook possède des paramètres, vous êtes invité à entrer les valeurs de ces derniers.</span><span class="sxs-lookup"><span data-stu-id="8bc2b-175">Since your runbook has parameters, you're prompted to enter values for them.</span></span>  <span data-ttu-id="8bc2b-176">Entrez le nom du groupe de ressources et du compte Automation à partir desquels vous allez collecter des informations sur les tâches.</span><span class="sxs-lookup"><span data-stu-id="8bc2b-176">Enter the name of the resource group and the automation account that your going to collect job information from.</span></span>
4. <span data-ttu-id="8bc2b-177">Cliquez sur **Démarrer** pour démarrer le runbook.</span><span class="sxs-lookup"><span data-stu-id="8bc2b-177">Click **Start** to the start the runbook.</span></span>
3. <span data-ttu-id="8bc2b-178">Le runbook démarre avec l’état **Mis en file d’attente** avant de passer à l’état **Exécution**.</span><span class="sxs-lookup"><span data-stu-id="8bc2b-178">The runbook will start with a status of **Queued** before it goes to **Running**.</span></span>  
3. <span data-ttu-id="8bc2b-179">Le runbook doit afficher une sortie détaillée avec les tâches collectées au format json.</span><span class="sxs-lookup"><span data-stu-id="8bc2b-179">The runbook should display verbose output with the jobs collected in json format.</span></span>  <span data-ttu-id="8bc2b-180">Si aucune tâche n’est répertoriée, il se peut qu’aucune tâche n’ait été créée dans le compte Automation dans la dernière heure.</span><span class="sxs-lookup"><span data-stu-id="8bc2b-180">If no jobs are listed, then there may have been no jobs created in the automation account in the last hour.</span></span>  <span data-ttu-id="8bc2b-181">Essayez de démarrer un autre runbook dans le compte Automation, puis effectuez de nouveau le test.</span><span class="sxs-lookup"><span data-stu-id="8bc2b-181">Try starting any runbook in the automation account and then perform the test again.</span></span>
4. <span data-ttu-id="8bc2b-182">Vérifiez que la sortie n’affiche pas d’erreur dans la commande post pour Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="8bc2b-182">Ensure that the output doesn't show any errors in the post command to Log Analytics.</span></span>  <span data-ttu-id="8bc2b-183">Un message similaire à celui ci-dessous doit s’afficher.</span><span class="sxs-lookup"><span data-stu-id="8bc2b-183">You should have a message similar to the following.</span></span>

    ![Sortie post](media/operations-management-suite-runbook-datacollect/post-output.png)

## <a name="5-verify-records-in-log-analytics"></a><span data-ttu-id="8bc2b-185">5. Vérifier les enregistrements dans Log Analytics</span><span class="sxs-lookup"><span data-stu-id="8bc2b-185">5. Verify records in Log Analytics</span></span>
<span data-ttu-id="8bc2b-186">Une fois le test du runbook terminé, et après avoir vérifié que la sortie a bien été reçue, vous pouvez vérifier que les enregistrements ont été créés à l’aide d’une [recherche dans les journaux de Log Analytics](../log-analytics/log-analytics-log-searches.md).</span><span class="sxs-lookup"><span data-stu-id="8bc2b-186">Once the runbook has completed in test, and you verified that the output was successfully received, you can verify that the records were created using a [log search in Log Analytics](../log-analytics/log-analytics-log-searches.md).</span></span>

![Sortie du journal](media/operations-management-suite-runbook-datacollect/log-output.png)

1. <span data-ttu-id="8bc2b-188">Dans le portail Azure, sélectionnez votre espace de travail Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="8bc2b-188">In the Azure portal, select your Log Analytics workspace.</span></span>
2. <span data-ttu-id="8bc2b-189">Cliquez sur **Recherche dans les journaux**.</span><span class="sxs-lookup"><span data-stu-id="8bc2b-189">Click on **Log Search**.</span></span>
3. <span data-ttu-id="8bc2b-190">Tapez la commande suivante `Type=AutomationJob_CL` et cliquez sur le bouton de recherche.</span><span class="sxs-lookup"><span data-stu-id="8bc2b-190">Type the following command `Type=AutomationJob_CL` and click the search button.</span></span> <span data-ttu-id="8bc2b-191">Notez que le type d’enregistrement inclut _CL, qui n’est pas spécifié dans le script.</span><span class="sxs-lookup"><span data-stu-id="8bc2b-191">Note that the record type includes _CL that isn't specified in the script.</span></span>  <span data-ttu-id="8bc2b-192">Ce suffixe est ajouté automatiquement au type de journal pour indiquer qu’il s’agit d’un type de journal personnalisé.</span><span class="sxs-lookup"><span data-stu-id="8bc2b-192">That suffix is automatically appended to the log type to indicate that it's a custom log type.</span></span>
4. <span data-ttu-id="8bc2b-193">Un ou plusieurs enregistrements devraient être renvoyés pour signaler que le runbook fonctionne comme prévu.</span><span class="sxs-lookup"><span data-stu-id="8bc2b-193">You should see one or more records returned indicating that the runbook is working as expected.</span></span>


## <a name="6-publish-the-runbook"></a><span data-ttu-id="8bc2b-194">6. Publier le runbook</span><span class="sxs-lookup"><span data-stu-id="8bc2b-194">6. Publish the runbook</span></span>
<span data-ttu-id="8bc2b-195">Une fois que vous avez vérifié que le runbook fonctionne correctement, vous devez le publier afin de pouvoir l’exécuter en production.</span><span class="sxs-lookup"><span data-stu-id="8bc2b-195">Once you've verified that the runbook is working correctly, you need to publish it so you can run it in production.</span></span>  <span data-ttu-id="8bc2b-196">Vous pouvez continuer à modifier et tester le runbook sans modifier la version publiée.</span><span class="sxs-lookup"><span data-stu-id="8bc2b-196">You can continue to edit and test the runbook without modifying the published version.</span></span>  

![Publier le runbook](media/operations-management-suite-runbook-datacollect/publish-runbook.png)

1. <span data-ttu-id="8bc2b-198">Revenez à votre compte Automation.</span><span class="sxs-lookup"><span data-stu-id="8bc2b-198">Return to your automation account.</span></span>
2. <span data-ttu-id="8bc2b-199">Cliquez sur **Runbooks** et sélectionnez **Collect-Automation-jobs**.</span><span class="sxs-lookup"><span data-stu-id="8bc2b-199">Click on **Runbooks** and select **Collect-Automation-jobs**.</span></span>
3. <span data-ttu-id="8bc2b-200">Cliquez sur **Modifier**, puis sur **Publier**.</span><span class="sxs-lookup"><span data-stu-id="8bc2b-200">Click **Edit** and then **Publish**.</span></span>
4. <span data-ttu-id="8bc2b-201">Cliquez sur **Oui** lorsque vous êtes invité à vérifier que vous souhaitez remplacer la version précédemment publiée.</span><span class="sxs-lookup"><span data-stu-id="8bc2b-201">Click **Yes** when asked to verify that you want to overwrite the previously published version.</span></span>

## <a name="7-set-logging-options"></a><span data-ttu-id="8bc2b-202">7. Définir les options de journalisation</span><span class="sxs-lookup"><span data-stu-id="8bc2b-202">7. Set logging options</span></span> 
<span data-ttu-id="8bc2b-203">Pour le test, vous pouviez afficher une [sortie détaillée](../automation/automation-runbook-output-and-messages.md#message-streams) parce que vous aviez défini la variable $VerbosePreference dans le script.</span><span class="sxs-lookup"><span data-stu-id="8bc2b-203">For test, you were able to view [verbose output](../automation/automation-runbook-output-and-messages.md#message-streams) because you set the $VerbosePreference variable in the script.</span></span>  <span data-ttu-id="8bc2b-204">Pour la production, vous devez définir les propriétés de journalisation du runbook si vous souhaitez afficher une sortie détaillée.</span><span class="sxs-lookup"><span data-stu-id="8bc2b-204">For production, you need to set the logging properties for the runbook if you want to view verbose output.</span></span>  <span data-ttu-id="8bc2b-205">Pour le runbook utilisé dans ce didacticiel, cette opération affiche les données json envoyées à Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="8bc2b-205">For the runbook used in this tutorial, this will display the json data being sent to Log Analytics.</span></span>

![Journalisation et suivi](media/operations-management-suite-runbook-datacollect/logging.png)

1. <span data-ttu-id="8bc2b-207">Dans les propriétés de votre runbook, sélectionnez **Journalisation et suivi** sous **Paramètres des runbooks**.</span><span class="sxs-lookup"><span data-stu-id="8bc2b-207">In the properties for your runbook select **Logging and tracing** under **Runbook Settings**.</span></span>
2. <span data-ttu-id="8bc2b-208">Modifiez le paramètre **Log verbose records** (Journaliser les enregistrements détaillés) sur **Activé**.</span><span class="sxs-lookup"><span data-stu-id="8bc2b-208">Change the setting for **Log verbose records** to **On**.</span></span>
3. <span data-ttu-id="8bc2b-209">Cliquez sur **Save**.</span><span class="sxs-lookup"><span data-stu-id="8bc2b-209">Click **Save**.</span></span>

## <a name="8-schedule-runbook"></a><span data-ttu-id="8bc2b-210">8. Planifier un runbook</span><span class="sxs-lookup"><span data-stu-id="8bc2b-210">8. Schedule runbook</span></span>
<span data-ttu-id="8bc2b-211">La méthode la plus courante pour démarrer un runbook qui collecte les données de surveillance consiste à planifier son exécution automatique.</span><span class="sxs-lookup"><span data-stu-id="8bc2b-211">The most common way to start a runbook that collects monitoring data is to schedule it to run automatically.</span></span>  <span data-ttu-id="8bc2b-212">Pour cela, vous devez créer une [planification dans Azure Automation](../automation/automation-schedules.md) et la lier à votre runbook.</span><span class="sxs-lookup"><span data-stu-id="8bc2b-212">You do this by creating a [schedule in Azure Automation](../automation/automation-schedules.md) and attaching it to your runbook.</span></span>

![Planifier un runbook](media/operations-management-suite-runbook-datacollect/schedule-runbook.png)

1. <span data-ttu-id="8bc2b-214">Dans les propriétés de votre runbook, sélectionnez **Planifications** sous **Ressources**.</span><span class="sxs-lookup"><span data-stu-id="8bc2b-214">In the properties for your runbook, select **Schedules** under **Resources**.</span></span>
2. <span data-ttu-id="8bc2b-215">Cliquez sur **Add a schedule (Ajouter une planification)** > **Link a schedule to your runbook (Lier une planification à votre runbook)** > **Create a new schedule (Créer une planification)**.</span><span class="sxs-lookup"><span data-stu-id="8bc2b-215">Click **Add a schedule** > **Link a schedule to your runbook** > **Create a new schedule**.</span></span>
5. <span data-ttu-id="8bc2b-216">Saisissez les valeurs suivantes pour la planification, puis cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="8bc2b-216">Type in the following values for the schedule and click **Create**.</span></span>

| <span data-ttu-id="8bc2b-217">Propriété</span><span class="sxs-lookup"><span data-stu-id="8bc2b-217">Property</span></span> | <span data-ttu-id="8bc2b-218">Valeur</span><span class="sxs-lookup"><span data-stu-id="8bc2b-218">Value</span></span> |
|:--|:--|
| <span data-ttu-id="8bc2b-219">Nom</span><span class="sxs-lookup"><span data-stu-id="8bc2b-219">Name</span></span> | <span data-ttu-id="8bc2b-220">AutomationJobs-Hourly</span><span class="sxs-lookup"><span data-stu-id="8bc2b-220">AutomationJobs-Hourly</span></span> |
| <span data-ttu-id="8bc2b-221">Démarrages</span><span class="sxs-lookup"><span data-stu-id="8bc2b-221">Starts</span></span> | <span data-ttu-id="8bc2b-222">Sélectionnez une heure au moins 5 minutes après l’heure actuelle.</span><span class="sxs-lookup"><span data-stu-id="8bc2b-222">Select any time at least 5 minutes past the current time.</span></span> |
| <span data-ttu-id="8bc2b-223">Périodicité</span><span class="sxs-lookup"><span data-stu-id="8bc2b-223">Recurrence</span></span> | <span data-ttu-id="8bc2b-224">Récurrent</span><span class="sxs-lookup"><span data-stu-id="8bc2b-224">Recurring</span></span> |
| <span data-ttu-id="8bc2b-225">Répéter toutes les</span><span class="sxs-lookup"><span data-stu-id="8bc2b-225">Recur every</span></span> | <span data-ttu-id="8bc2b-226">1 heure</span><span class="sxs-lookup"><span data-stu-id="8bc2b-226">1 hour</span></span> |
| <span data-ttu-id="8bc2b-227">Définir une expiration</span><span class="sxs-lookup"><span data-stu-id="8bc2b-227">Set expiration</span></span> | <span data-ttu-id="8bc2b-228">Non</span><span class="sxs-lookup"><span data-stu-id="8bc2b-228">No</span></span> |

<span data-ttu-id="8bc2b-229">Une fois que la planification est créée, vous devez définir les valeurs de paramètre qui seront utilisées chaque fois que cette planification démarre le runbook.</span><span class="sxs-lookup"><span data-stu-id="8bc2b-229">Once the schedule is created, you need to set the parameter values that will be used each time this schedule starts the runbook.</span></span>

6. <span data-ttu-id="8bc2b-230">Cliquez sur **Configure parameters and run settings (Configurer les paramètres et les paramètres d’exécution)**.</span><span class="sxs-lookup"><span data-stu-id="8bc2b-230">Click **Configure parameters and run settings**.</span></span>
7. <span data-ttu-id="8bc2b-231">Renseignez les valeurs pour **ResourceGroupName** et **AutomationAccountName**.</span><span class="sxs-lookup"><span data-stu-id="8bc2b-231">Fill in values for your **ResourceGroupName** and **AutomationAccountName**.</span></span>
8. <span data-ttu-id="8bc2b-232">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="8bc2b-232">Click **OK**.</span></span> 

## <a name="9-verify-runbook-starts-on-schedule"></a><span data-ttu-id="8bc2b-233">9. Vérifier la conformité du démarrage du runbook avec la planification</span><span class="sxs-lookup"><span data-stu-id="8bc2b-233">9. Verify runbook starts on schedule</span></span>
<span data-ttu-id="8bc2b-234">À chaque démarrage d’un runbook, [un travail est créé](../automation/automation-runbook-execution.md) et toute sortie est enregistrée.</span><span class="sxs-lookup"><span data-stu-id="8bc2b-234">Everytime a runbook is started, [a job is created](../automation/automation-runbook-execution.md) and any output logged.</span></span>  <span data-ttu-id="8bc2b-235">En fait, il s’agit des mêmes travaux que ceux que le runbook collecte.</span><span class="sxs-lookup"><span data-stu-id="8bc2b-235">In fact, these are the same jobs that the runbook is collecting.</span></span>  <span data-ttu-id="8bc2b-236">Vous pouvez vérifier que le runbook démarre comme prévu en vérifiant les travaux du runbook après l’heure de démarrage indiquée dans la planification.</span><span class="sxs-lookup"><span data-stu-id="8bc2b-236">You can verify that the runbook starts as expected by checking the jobs for the runbook after the start time for the schedule has passed.</span></span>

![Travaux](media/operations-management-suite-runbook-datacollect/jobs.png)

1. <span data-ttu-id="8bc2b-238">Dans les propriétés de votre runbook, sélectionnez **Travaux** sous **Ressources**.</span><span class="sxs-lookup"><span data-stu-id="8bc2b-238">In the properties for your runbook, select **Jobs** under **Resources**.</span></span>
2. <span data-ttu-id="8bc2b-239">Vous devez voir une liste des travaux pour chaque démarrage du runbook.</span><span class="sxs-lookup"><span data-stu-id="8bc2b-239">You should see a listing of jobs for each time the runbook was started.</span></span>
3. <span data-ttu-id="8bc2b-240">Cliquez sur l’un des travaux pour en afficher les détails.</span><span class="sxs-lookup"><span data-stu-id="8bc2b-240">Click on one of the jobs to view its details.</span></span>
4. <span data-ttu-id="8bc2b-241">Cliquez sur **Tous les journaux** pour afficher les journaux et les sorties du runbook.</span><span class="sxs-lookup"><span data-stu-id="8bc2b-241">Click on **All logs** to view the logs and output from the runbook.</span></span>
5. <span data-ttu-id="8bc2b-242">Faites défiler vers le bas pour rechercher une entrée similaire à l’image ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="8bc2b-242">Scroll to the bottom to find an entry similar to the image below.</span></span><br>![Détaillé](media/operations-management-suite-runbook-datacollect/verbose.png)
6. <span data-ttu-id="8bc2b-244">Cliquez sur cette entrée pour afficher les données json détaillées qui ont été envoyées à Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="8bc2b-244">Click on this entry to view the detailed json data  that was sent to Log Analytics.</span></span>



## <a name="next-steps"></a><span data-ttu-id="8bc2b-245">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="8bc2b-245">Next steps</span></span>
- <span data-ttu-id="8bc2b-246">Utilisez le [concepteur de vue](../log-analytics/log-analytics-view-designer.md) pour créer une vue affichant les données que vous avez collectées dans le référentiel Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="8bc2b-246">Use [View Designer](../log-analytics/log-analytics-view-designer.md) to create a view displaying the data that you've collected to the Log Analytics repository.</span></span>
- <span data-ttu-id="8bc2b-247">Intégrez votre runbook dans une [solution de gestion](operations-management-suite-solutions-creating.md) à distribuer aux clients.</span><span class="sxs-lookup"><span data-stu-id="8bc2b-247">Package your runbook in a [management solution](operations-management-suite-solutions-creating.md) to distribute to customers.</span></span>
- <span data-ttu-id="8bc2b-248">En savoir plus sur [Log Analytics](https://docs.microsoft.com/azure/log-analytics/).</span><span class="sxs-lookup"><span data-stu-id="8bc2b-248">Learn more about [Log Analytics](https://docs.microsoft.com/azure/log-analytics/).</span></span>
- <span data-ttu-id="8bc2b-249">En savoir plus sur [Azure Automation](https://docs.microsoft.com/azure/automation/).</span><span class="sxs-lookup"><span data-stu-id="8bc2b-249">Learn more about [Azure Automation](https://docs.microsoft.com/azure/automation/).</span></span>
- <span data-ttu-id="8bc2b-250">En savoir plus sur l’[API du collecteur de données HTTP](../log-analytics/log-analytics-data-collector-api.md).</span><span class="sxs-lookup"><span data-stu-id="8bc2b-250">Learn more about the [HTTP Data Collector API](../log-analytics/log-analytics-data-collector-api.md).</span></span>