---
title: configuration du compte Azure Automation aaaValidate | Documents Microsoft
description: "Cet article décrit la configuration de hello tooconfirm de votre compte Automation est configurée correctement."
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
ms.openlocfilehash: 3a990dcc6661cf67c4b62592ce03d55a3791053a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="test-azure-automation-run-as-account-authentication"></a><span data-ttu-id="a2119-103">Test d’authentification du compte d’identification Azure Automation</span><span class="sxs-lookup"><span data-stu-id="a2119-103">Test Azure Automation Run As account authentication</span></span>
<span data-ttu-id="a2119-104">Une fois un compte Automation est créé avec succès, vous pouvez effectuer un tooconfirm de test simple que vous ne pouvez toosuccessfully s’authentifier dans Azure Resource Manager ou un déploiement classique Azure à l’aide de votre compte Automation exécuter en tant que nouvellement créé ou mis à jour.</span><span class="sxs-lookup"><span data-stu-id="a2119-104">After an Automation account is successfully created, you can perform a simple test tooconfirm you are able toosuccessfully authenticate in Azure Resource Manager or Azure classic deployment using your newly created or updated Automation Run As account.</span></span>    

## <a name="automation-run-as-authentication"></a><span data-ttu-id="a2119-105">Authentification d’identification Automation</span><span class="sxs-lookup"><span data-stu-id="a2119-105">Automation Run As authentication</span></span>
<span data-ttu-id="a2119-106">Utilisez hello exemple de code ci-dessous trop[créer un runbook PowerShell](automation-creating-importing-runbook.md) tooverify l’authentification à l’aide de hello exécuter en tant que compte et également dans votre tooauthenticate runbooks personnalisés et de gérer les ressources du Gestionnaire de ressources avec votre compte Automation.</span><span class="sxs-lookup"><span data-stu-id="a2119-106">Use hello sample code below too[create a PowerShell runbook](automation-creating-importing-runbook.md) tooverify authentication using hello Run As account and also in your custom runbooks tooauthenticate and manage Resource Manager resources with your Automation account.</span></span>   

    $connectionName = "AzureRunAsConnection"
    try
    {
        # Get hello connection "AzureRunAsConnection "
        $servicePrincipalConnection=Get-AutomationConnection -Name $connectionName         

        "Logging in tooAzure..."
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

<span data-ttu-id="a2119-107">Notez hello applet de commande utilisée pour l’authentification dans hello runbook - **Add-AzureRmAccount**, utilise hello *ServicePrincipalCertificate* jeu de paramètres.</span><span class="sxs-lookup"><span data-stu-id="a2119-107">Notice hello cmdlet used for authenticating in hello runbook - **Add-AzureRmAccount**, uses hello *ServicePrincipalCertificate* parameter set.</span></span>  <span data-ttu-id="a2119-108">Elle effectue l’authentification à l’aide du certificat du principal du service et non des informations d’identification.</span><span class="sxs-lookup"><span data-stu-id="a2119-108">It authenticates by using service principal certificate, not credentials.</span></span>  

<span data-ttu-id="a2119-109">Lorsque vous [exécuter hello runbook](automation-starting-a-runbook.md#starting-a-runbook-with-the-azure-portal) toovalidate votre compte d’identification, un [tâche du runbook](automation-runbook-execution.md) est créé, panneau de tâche hello s’affiche, et état de la tâche hello affichée Bonjour **récapitulatif**vignette.</span><span class="sxs-lookup"><span data-stu-id="a2119-109">When you [run hello runbook](automation-starting-a-runbook.md#starting-a-runbook-with-the-azure-portal) toovalidate your Run As account, a [runbook job](automation-runbook-execution.md) is created, hello Job blade is displayed, and hello job status displayed in hello **Job Summary** tile.</span></span> <span data-ttu-id="a2119-110">état de la tâche Hello démarrera en tant que *en file d’attente* indiquant qu’il est en attente d’un runbook worker dans hello toobecome de cloud disponible.</span><span class="sxs-lookup"><span data-stu-id="a2119-110">hello job status will start as *Queued* indicating that it is waiting for a runbook worker in hello cloud toobecome available.</span></span> <span data-ttu-id="a2119-111">Il passe alors trop*départ* lorsqu’un processus de travail tâche de hello, les revendications, puis *en cours d’exécution* démarrage hello runbook réellement en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="a2119-111">It will then move too*Starting* when a worker claims hello job, and then *Running* when hello runbook actually starts running.</span></span>  <span data-ttu-id="a2119-112">Lors de la tâche de runbook hello est terminée, nous devons voyez l’état **terminé**.</span><span class="sxs-lookup"><span data-stu-id="a2119-112">When hello runbook job completes, we should see a status of **Completed**.</span></span>

<span data-ttu-id="a2119-113">toosee hello les résultats détaillés de hello runbook, cliquez sur hello **sortie** vignette.</span><span class="sxs-lookup"><span data-stu-id="a2119-113">toosee hello detailed results of hello runbook, click on hello **Output** tile.</span></span>  <span data-ttu-id="a2119-114">Sur hello **sortie** panneau, vous devez voir qu’il a été authentifié et retourne une liste de toutes les ressources de tous les groupes de ressources dans votre abonnement.</span><span class="sxs-lookup"><span data-stu-id="a2119-114">On hello **Output** blade, you should see it has successfully authenticated and returns a list of all resources in all resource groups in your subscription.</span></span>  

<span data-ttu-id="a2119-115">Rappelez-vous simplement le bloc de hello tooremove de code commençant par le commentaire hello `#Get all ARM resources from all resource groups` lorsque vous réutilisez le code de hello pour les procédures opérationnelles.</span><span class="sxs-lookup"><span data-stu-id="a2119-115">Just remember tooremove hello block of code starting with hello comment `#Get all ARM resources from all resource groups` when you reuse hello code for your runbooks.</span></span>

## <a name="classic-run-as-authentication"></a><span data-ttu-id="a2119-116">Authentification d’identification Classic</span><span class="sxs-lookup"><span data-stu-id="a2119-116">Classic Run As authentication</span></span>
<span data-ttu-id="a2119-117">Utilisez hello exemple de code ci-dessous trop[créer un runbook PowerShell](automation-creating-importing-runbook.md) à l’aide de l’authentification tooverify hello classique exécute en tant que compte et également dans votre tooauthenticate runbooks personnalisés et de gérer les ressources dans le modèle de déploiement classique hello.</span><span class="sxs-lookup"><span data-stu-id="a2119-117">Use hello sample code below too[create a PowerShell runbook](automation-creating-importing-runbook.md) tooverify authentication using hello Classic Run As account and also in your custom runbooks tooauthenticate and manage resources in hello classic deployment model.</span></span>  

    $ConnectionAssetName = "AzureClassicRunAsConnection"
    # Get hello connection
    $connection = Get-AutomationConnection -Name $connectionAssetName        

    # Authenticate tooAzure with certificate
    Write-Verbose "Get connection asset: $ConnectionAssetName" -Verbose
    $Conn = Get-AutomationConnection -Name $ConnectionAssetName
    if ($Conn -eq $null)
    {
       throw "Could not retrieve connection asset: $ConnectionAssetName. Assure that this asset exists in hello Automation account."
    }

    $CertificateAssetName = $Conn.CertificateAssetName
    Write-Verbose "Getting hello certificate: $CertificateAssetName" -Verbose
    $AzureCert = Get-AutomationCertificate -Name $CertificateAssetName
    if ($AzureCert -eq $null)
    {
       throw "Could not retrieve certificate asset: $CertificateAssetName. Assure that this asset exists in hello Automation account."
    }

    Write-Verbose "Authenticating tooAzure with certificate." -Verbose
    Set-AzureSubscription -SubscriptionName $Conn.SubscriptionName -SubscriptionId $Conn.SubscriptionID -Certificate $AzureCert
    Select-AzureSubscription -SubscriptionId $Conn.SubscriptionID
    
    #Get all VMs in hello subscription and return list with name of each
    Get-AzureVM | ft Name

<span data-ttu-id="a2119-118">Lorsque vous [exécuter hello runbook](automation-starting-a-runbook.md#starting-a-runbook-with-the-azure-portal) toovalidate votre compte d’identification, un [tâche du runbook](automation-runbook-execution.md) est créé, panneau de tâche hello s’affiche, et état de la tâche hello affichée Bonjour **récapitulatif**vignette.</span><span class="sxs-lookup"><span data-stu-id="a2119-118">When you [run hello runbook](automation-starting-a-runbook.md#starting-a-runbook-with-the-azure-portal) toovalidate your Run As account, a [runbook job](automation-runbook-execution.md) is created, hello Job blade is displayed, and hello job status displayed in hello **Job Summary** tile.</span></span> <span data-ttu-id="a2119-119">état de la tâche Hello démarrera en tant que *en file d’attente* indiquant qu’il est en attente d’un runbook worker dans hello toobecome de cloud disponible.</span><span class="sxs-lookup"><span data-stu-id="a2119-119">hello job status will start as *Queued* indicating that it is waiting for a runbook worker in hello cloud toobecome available.</span></span> <span data-ttu-id="a2119-120">Il passe alors trop*départ* lorsqu’un processus de travail tâche de hello, les revendications, puis *en cours d’exécution* démarrage hello runbook réellement en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="a2119-120">It will then move too*Starting* when a worker claims hello job, and then *Running* when hello runbook actually starts running.</span></span>  <span data-ttu-id="a2119-121">Lors de la tâche de runbook hello est terminée, nous devons voyez l’état **terminé**.</span><span class="sxs-lookup"><span data-stu-id="a2119-121">When hello runbook job completes, we should see a status of **Completed**.</span></span>

<span data-ttu-id="a2119-122">toosee hello les résultats détaillés de hello runbook, cliquez sur hello **sortie** vignette.</span><span class="sxs-lookup"><span data-stu-id="a2119-122">toosee hello detailed results of hello runbook, click on hello **Output** tile.</span></span>  <span data-ttu-id="a2119-123">Sur hello **sortie** panneau, vous devez voir qu’il a été authentifié et retourne une liste de tous les ordinateurs virtuels de Azure à VMName qui sont déployés dans votre abonnement.</span><span class="sxs-lookup"><span data-stu-id="a2119-123">On hello **Output** blade, you should see it has successfully authenticated and returns a list of all Azure VMs by VMName that are deployed in your subscription.</span></span>  

<span data-ttu-id="a2119-124">N’oubliez pas applet de commande hello tooremove **Get-AzureVM** lorsque vous réutilisez le code de hello pour les procédures opérationnelles.</span><span class="sxs-lookup"><span data-stu-id="a2119-124">Just remember tooremove hello cmdlet **Get-AzureVM** when you reuse hello code for your runbooks.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a2119-125">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="a2119-125">Next steps</span></span>
* <span data-ttu-id="a2119-126">tooget main runbook PowerShell, consultez [mon runbook PowerShell premier](automation-first-runbook-textual-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="a2119-126">tooget started with PowerShell runbooks, see [My first PowerShell runbook](automation-first-runbook-textual-powershell.md).</span></span>
* <span data-ttu-id="a2119-127">toolearn plus sur la création de graphiques, consultez [de création graphique dans Azure Automation](automation-graphical-authoring-intro.md).</span><span class="sxs-lookup"><span data-stu-id="a2119-127">toolearn more about Graphical Authoring, see [Graphical authoring in Azure Automation](automation-graphical-authoring-intro.md).</span></span>
