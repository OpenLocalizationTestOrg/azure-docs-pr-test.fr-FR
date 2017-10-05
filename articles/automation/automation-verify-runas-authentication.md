---
title: Validation de la configuration de compte Azure Automation | Microsoft Docs
description: "Cet article décrit comment vérifier que votre compte Automation est correctement configuré."
services: automation
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: 
ms.assetid: 
ms.service: automation
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/07/2017
ms.author: magoedte
ms.openlocfilehash: 804e05f596e1d6d5f650e4c94a18eff6b7c3ba4e
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="test-azure-automation-run-as-account-authentication"></a><span data-ttu-id="169f5-103">Test d’authentification du compte d’identification Azure Automation</span><span class="sxs-lookup"><span data-stu-id="169f5-103">Test Azure Automation Run As account authentication</span></span>
<span data-ttu-id="169f5-104">Une fois qu’un compte Automation est correctement créé, vous pouvez effectuer un test simple pour confirmer que vous êtes en mesure de vous authentifier dans Azure Resource Manager ou un déploiement classique Azure à l’aide de votre compte d’identification Automation nouvellement créé ou mis à jour.</span><span class="sxs-lookup"><span data-stu-id="169f5-104">After an Automation account is successfully created, you can perform a simple test to confirm you are able to successfully authenticate in Azure Resource Manager or Azure classic deployment using your newly created or updated Automation Run As account.</span></span>    

## <a name="automation-run-as-authentication"></a><span data-ttu-id="169f5-105">Authentification d’identification Automation</span><span class="sxs-lookup"><span data-stu-id="169f5-105">Automation Run As authentication</span></span>
<span data-ttu-id="169f5-106">Utilisez l’exemple de code ci-dessous pour [créer un runbook PowerShell](automation-creating-importing-runbook.md) afin de vérifier l’authentification à l’aide d’un compte d’identification. Utilisez-le aussi sur votre runbook personnalisé pour vous authentifier et gérer les ressources du Gestionnaire des ressources avec un compte Automation.</span><span class="sxs-lookup"><span data-stu-id="169f5-106">Use the sample code below to [create a PowerShell runbook](automation-creating-importing-runbook.md) to verify authentication using the Run As account and also in your custom runbooks to authenticate and manage Resource Manager resources with your Automation account.</span></span>   

    $connectionName = "AzureRunAsConnection"
    try
    {
        # Get the connection "AzureRunAsConnection "
        $servicePrincipalConnection=Get-AutomationConnection -Name $connectionName         

        "Logging in to Azure..."
        Add-AzureRmAccount `
           -ServicePrincipal `
           -TenantId $servicePrincipalConnection.TenantId `
           -ApplicationId $servicePrincipalConnection.ApplicationId `
           -CertificateThumbprint $servicePrincipalConnection.CertificateThumbprint 
    }
    catch {
       if (!$servicePrincipalConnection)
       {
          $ErrorMessage = "Connection $connectionName not found."
          throw $ErrorMessage
      } else{
          Write-Error -Message $_.Exception
          throw $_.Exception
      }
    }

    #Get all ARM resources from all resource groups
    $ResourceGroups = Get-AzureRmResourceGroup 

    foreach ($ResourceGroup in $ResourceGroups)
    {    
       Write-Output ("Showing resources in resource group " + $ResourceGroup.ResourceGroupName)
       $Resources = Find-AzureRmResource -ResourceGroupNameContains $ResourceGroup.ResourceGroupName | Select ResourceName, ResourceType
       ForEach ($Resource in $Resources)
       {
          Write-Output ($Resource.ResourceName + " of type " +  $Resource.ResourceType)
       }
       Write-Output ("")
    } 

<span data-ttu-id="169f5-107">Notez que l’applet de commande utilisée pour l’authentification ( **Add-AzureRmAccount**) dans le Runbook, utilise le jeu de paramètres *ServicePrincipalCertificate* .</span><span class="sxs-lookup"><span data-stu-id="169f5-107">Notice the cmdlet used for authenticating in the runbook - **Add-AzureRmAccount**, uses the *ServicePrincipalCertificate* parameter set.</span></span>  <span data-ttu-id="169f5-108">Elle effectue l’authentification à l’aide du certificat du principal du service et non des informations d’identification.</span><span class="sxs-lookup"><span data-stu-id="169f5-108">It authenticates by using service principal certificate, not credentials.</span></span>  

<span data-ttu-id="169f5-109">Lorsque vous [exécutez un runbook](automation-starting-a-runbook.md#starting-a-runbook-with-the-azure-portal) pour valider un compte d’identification, un [travail du runbook](automation-runbook-execution.md) est créé. Le panneau Travail s’affiche alors et l’état du travail est affiché dans la mosaïque **Résumé du travail**.</span><span class="sxs-lookup"><span data-stu-id="169f5-109">When you [run the runbook](automation-starting-a-runbook.md#starting-a-runbook-with-the-azure-portal) to validate your Run As account, a [runbook job](automation-runbook-execution.md) is created, the Job blade is displayed, and the job status displayed in the **Job Summary** tile.</span></span> <span data-ttu-id="169f5-110">L’état initial du travail est *Mis en file d’attente* pour indiquer qu’il attend la disponibilité d’un Runbook Worker dans le cloud.</span><span class="sxs-lookup"><span data-stu-id="169f5-110">The job status will start as *Queued* indicating that it is waiting for a runbook worker in the cloud to become available.</span></span> <span data-ttu-id="169f5-111">La tâche prend ensuite l’état *Démarrage en cours* lorsqu’un Worker sélectionne la tâche, puis l’état *En cours d’exécution* lorsque le Runbook commence à s’exécuter.</span><span class="sxs-lookup"><span data-stu-id="169f5-111">It will then move to *Starting* when a worker claims the job, and then *Running* when the runbook actually starts running.</span></span>  <span data-ttu-id="169f5-112">À l’issue du travail du Runbook, l’état **Terminé** doit s’afficher.</span><span class="sxs-lookup"><span data-stu-id="169f5-112">When the runbook job completes, we should see a status of **Completed**.</span></span>

<span data-ttu-id="169f5-113">Pour afficher les résultats détaillés du Runbook, cliquez sur la mosaïque **Sortie** .</span><span class="sxs-lookup"><span data-stu-id="169f5-113">To see the detailed results of the runbook, click on the **Output** tile.</span></span>  <span data-ttu-id="169f5-114">Le panneau **Sortie** doit indiquer qu’il a authentifié et retourné la liste de toutes les ressources dans les groupes de ressources de votre abonnement.</span><span class="sxs-lookup"><span data-stu-id="169f5-114">On the **Output** blade, you should see it has successfully authenticated and returns a list of all resources in all resource groups in your subscription.</span></span>  

<span data-ttu-id="169f5-115">Pensez à supprimer le bloc de code en commençant par le commentaire `#Get all ARM resources from all resource groups` lorsque vous réutiliser le code de vos runbooks.</span><span class="sxs-lookup"><span data-stu-id="169f5-115">Just remember to remove the block of code starting with the comment `#Get all ARM resources from all resource groups` when you reuse the code for your runbooks.</span></span>

## <a name="classic-run-as-authentication"></a><span data-ttu-id="169f5-116">Authentification d’identification Classic</span><span class="sxs-lookup"><span data-stu-id="169f5-116">Classic Run As authentication</span></span>
<span data-ttu-id="169f5-117">Utilisez l’exemple de code ci-dessous pour [créer un runbook PowerShell](automation-creating-importing-runbook.md) afin de vérifier l’authentification à l’aide d’un compte d’identification Classic. Utilisez-le aussi sur votre runbook personnalisé pour vous authentifier et gérer les ressources dans le modèle de déploiement Classic.</span><span class="sxs-lookup"><span data-stu-id="169f5-117">Use the sample code below to [create a PowerShell runbook](automation-creating-importing-runbook.md) to verify authentication using the Classic Run As account and also in your custom runbooks to authenticate and manage resources in the classic deployment model.</span></span>  

    $ConnectionAssetName = "AzureClassicRunAsConnection"
    # Get the connection
    $connection = Get-AutomationConnection -Name $connectionAssetName        

    # Authenticate to Azure with certificate
    Write-Verbose "Get connection asset: $ConnectionAssetName" -Verbose
    $Conn = Get-AutomationConnection -Name $ConnectionAssetName
    if ($Conn -eq $null)
    {
       throw "Could not retrieve connection asset: $ConnectionAssetName. Assure that this asset exists in the Automation account."
    }

    $CertificateAssetName = $Conn.CertificateAssetName
    Write-Verbose "Getting the certificate: $CertificateAssetName" -Verbose
    $AzureCert = Get-AutomationCertificate -Name $CertificateAssetName
    if ($AzureCert -eq $null)
    {
       throw "Could not retrieve certificate asset: $CertificateAssetName. Assure that this asset exists in the Automation account."
    }

    Write-Verbose "Authenticating to Azure with certificate." -Verbose
    Set-AzureSubscription -SubscriptionName $Conn.SubscriptionName -SubscriptionId $Conn.SubscriptionID -Certificate $AzureCert
    Select-AzureSubscription -SubscriptionId $Conn.SubscriptionID
    
    #Get all VMs in the subscription and return list with name of each
    Get-AzureVM | ft Name

<span data-ttu-id="169f5-118">Lorsque vous [exécutez un runbook](automation-starting-a-runbook.md#starting-a-runbook-with-the-azure-portal) pour valider un compte d’identification, un [travail du runbook](automation-runbook-execution.md) est créé. Le panneau Travail s’affiche alors et l’état du travail est affiché dans la mosaïque **Résumé du travail**.</span><span class="sxs-lookup"><span data-stu-id="169f5-118">When you [run the runbook](automation-starting-a-runbook.md#starting-a-runbook-with-the-azure-portal) to validate your Run As account, a [runbook job](automation-runbook-execution.md) is created, the Job blade is displayed, and the job status displayed in the **Job Summary** tile.</span></span> <span data-ttu-id="169f5-119">L’état initial du travail est *Mis en file d’attente* pour indiquer qu’il attend la disponibilité d’un Runbook Worker dans le cloud.</span><span class="sxs-lookup"><span data-stu-id="169f5-119">The job status will start as *Queued* indicating that it is waiting for a runbook worker in the cloud to become available.</span></span> <span data-ttu-id="169f5-120">La tâche prend ensuite l’état *Démarrage en cours* lorsqu’un Worker sélectionne la tâche, puis l’état *En cours d’exécution* lorsque le Runbook commence à s’exécuter.</span><span class="sxs-lookup"><span data-stu-id="169f5-120">It will then move to *Starting* when a worker claims the job, and then *Running* when the runbook actually starts running.</span></span>  <span data-ttu-id="169f5-121">À l’issue du travail du Runbook, l’état **Terminé** doit s’afficher.</span><span class="sxs-lookup"><span data-stu-id="169f5-121">When the runbook job completes, we should see a status of **Completed**.</span></span>

<span data-ttu-id="169f5-122">Pour afficher les résultats détaillés du Runbook, cliquez sur la mosaïque **Sortie** .</span><span class="sxs-lookup"><span data-stu-id="169f5-122">To see the detailed results of the runbook, click on the **Output** tile.</span></span>  <span data-ttu-id="169f5-123">Le panneau **Sortie** doit indiquer qu’il a authentifié et retourné la liste de toutes les machines virtuelles Azure de VMName qui sont déployées dans votre abonnement.</span><span class="sxs-lookup"><span data-stu-id="169f5-123">On the **Output** blade, you should see it has successfully authenticated and returns a list of all Azure VMs by VMName that are deployed in your subscription.</span></span>  

<span data-ttu-id="169f5-124">N’oubliez pas de supprimer le cmdlet **Get-AzureVM** lorsque vous réutilisez le code de vos runbooks.</span><span class="sxs-lookup"><span data-stu-id="169f5-124">Just remember to remove the cmdlet **Get-AzureVM** when you reuse the code for your runbooks.</span></span>

## <a name="next-steps"></a><span data-ttu-id="169f5-125">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="169f5-125">Next steps</span></span>
* <span data-ttu-id="169f5-126">Pour une prise en main des Runbooks PowerShell, consultez [Mon premier Runbook PowerShell](automation-first-runbook-textual-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="169f5-126">To get started with PowerShell runbooks, see [My first PowerShell runbook](automation-first-runbook-textual-powershell.md).</span></span>
* <span data-ttu-id="169f5-127">Pour en savoir plus sur la création graphique, consultez [Création de graphiques dans Azure Automation](automation-graphical-authoring-intro.md).</span><span class="sxs-lookup"><span data-stu-id="169f5-127">To learn more about Graphical Authoring, see [Graphical authoring in Azure Automation](automation-graphical-authoring-intro.md).</span></span>
