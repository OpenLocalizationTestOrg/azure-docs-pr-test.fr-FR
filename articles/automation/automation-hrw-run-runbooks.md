---
title: runbooks aaaRun sur le travail de Runbook hybride Azure Automation | Documents Microsoft
description: "Cet article fournit des informations sur l’exécution des procédures opérationnelles sur des ordinateurs dans votre centre de données local ou d’un fournisseur de cloud avec le rôle de travail de Runbook hybride hello."
services: automation
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: tysonn
ms.assetid: 06227cda-f3d1-47fe-b3f8-436d2b9d81ee
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/22/2017
ms.author: magoedte
ms.openlocfilehash: 51961e02603e5690edd11e577594ad2ddea489a7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="running-runbooks-on-a-hybrid-runbook-worker"></a><span data-ttu-id="5182f-103">Exécution de Runbooks sur un Runbook Worker hybride</span><span class="sxs-lookup"><span data-stu-id="5182f-103">Running runbooks on a Hybrid Runbook Worker</span></span> 
<span data-ttu-id="5182f-104">Il n’existe aucune différence dans la structure de hello des procédures opérationnelles qui s’exécutent dans Azure Automation et celles qui s’exécutent sur un Runbook Worker hybride.</span><span class="sxs-lookup"><span data-stu-id="5182f-104">There is no difference in hello structure of runbooks that run in Azure Automation and those that run on a Hybrid Runbook Worker.</span></span> <span data-ttu-id="5182f-105">Les runbooks que vous utilisez avec chaque très probablement diffèrent considérablement cependant étant donné que les procédures opérationnelles ciblant un Runbook Worker hybride généralement gérer les ressources sur les ordinateur local hello lui-même ou sur des ressources dans l’environnement local de hello où il est déployé, tout en procédures opérationnelles dans Azure Automation généralement gérer les ressources Bonjour cloud Azure.</span><span class="sxs-lookup"><span data-stu-id="5182f-105">Runbooks that you use with each most likely differ significantly though since runbooks targeting a Hybrid Runbook Worker typically manage resources on hello local computer itself or against resources in hello local environment where it is deployed, while runbooks in Azure Automation typically manage resources in hello Azure cloud.</span></span>

<span data-ttu-id="5182f-106">Vous pouvez modifier un runbook pour un Runbook Worker hybride dans Azure Automation, mais peut avoir des difficultés si vous essayez de runbook de hello tootest dans l’éditeur de hello.</span><span class="sxs-lookup"><span data-stu-id="5182f-106">You can edit a runbook for Hybrid Runbook Worker in Azure Automation, but you may have difficulties if you try tootest hello runbook in hello editor.</span></span>  <span data-ttu-id="5182f-107">modules PowerShell Hello qui accèdent aux ressources locales de hello ne peuvent pas être installés dans votre environnement Azure Automation dans ce cas, les tests hello échouerait.</span><span class="sxs-lookup"><span data-stu-id="5182f-107">hello PowerShell modules that access hello local resources may not be installed in your Azure Automation environment in which case, hello test would fail.</span></span>  <span data-ttu-id="5182f-108">Si vous installez hello requis des modules, hello runbook s’exécute, mais il ne sera pas en mesure de tooaccess des ressources locales pour un test complet.</span><span class="sxs-lookup"><span data-stu-id="5182f-108">If you do install hello required modules, then hello runbook will run, but it will not be able tooaccess local resources for a complete test.</span></span>

## <a name="starting-a-runbook-on-hybrid-runbook-worker"></a><span data-ttu-id="5182f-109">Démarrage d’un Runbook sur Runbook Worker hybride</span><span class="sxs-lookup"><span data-stu-id="5182f-109">Starting a runbook on Hybrid Runbook Worker</span></span>
<span data-ttu-id="5182f-110">[Démarrage d'un Runbook dans Azure Automation](automation-starting-a-runbook.md) décrit différentes méthodes de démarrage d'un Runbook.</span><span class="sxs-lookup"><span data-stu-id="5182f-110">[Starting a Runbook in Azure Automation](automation-starting-a-runbook.md) describes different methods for starting a runbook.</span></span>  <span data-ttu-id="5182f-111">Runbook Worker hybride ajoute un **RunOn** option où vous pouvez spécifier le nom de hello d’un groupe de travail de Runbook hybride.</span><span class="sxs-lookup"><span data-stu-id="5182f-111">Hybrid Runbook Worker adds a **RunOn** option where you can specify hello name of a Hybrid Runbook Worker Group.</span></span>  <span data-ttu-id="5182f-112">Si un groupe est spécifié, puis hello runbook est récupéré et exécuté par des travailleurs hello dans ce groupe.</span><span class="sxs-lookup"><span data-stu-id="5182f-112">If a group is specified, then hello runbook is retrieved and run by of hello workers in that group.</span></span>  <span data-ttu-id="5182f-113">Si cette option n'est pas spécifiée, il est exécuté dans Azure Automation comme habituellement.</span><span class="sxs-lookup"><span data-stu-id="5182f-113">If this option is not specified, then it is run in Azure Automation as normal.</span></span>

<span data-ttu-id="5182f-114">Lorsque vous démarrez un runbook dans hello portail Azure, vous sont présentées avec un **s’exécutent sur** option dans laquelle vous pouvez sélectionner **Azure** ou **Worker hybride**.</span><span class="sxs-lookup"><span data-stu-id="5182f-114">When you start a runbook in hello Azure portal, you are presented with a **Run on** option where you can select **Azure** or **Hybrid Worker**.</span></span>  <span data-ttu-id="5182f-115">Si vous sélectionnez **Worker hybride**, vous pouvez sélectionner le groupe de hello dans une liste déroulante.</span><span class="sxs-lookup"><span data-stu-id="5182f-115">If you select **Hybrid Worker**, then you can select hello group from a dropdown.</span></span>

<span data-ttu-id="5182f-116">Hello d’utilisation **RunOn** paramètre.</span><span class="sxs-lookup"><span data-stu-id="5182f-116">Use hello **RunOn** parameter.</span></span>  <span data-ttu-id="5182f-117">Vous pouvez utiliser hello suivant commande toostart un runbook nommé Test-Runbook sur un groupe de travail de Runbook hybride nommé MyHybridGroup à l’aide de Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="5182f-117">You can use hello following command toostart a runbook named Test-Runbook on a Hybrid Runbook Worker Group named MyHybridGroup using Windows PowerShell.</span></span>

    Start-AzureRmAutomationRunbook –AutomationAccountName "MyAutomationAccount" –Name "Test-Runbook" -RunOn "MyHybridGroup"

> [!NOTE]
> <span data-ttu-id="5182f-118">Hello **RunOn** paramètre a été ajouté toohello **Start-AzureAutomationRunbook** applet de commande dans la version 0.9.1 de Microsoft Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="5182f-118">hello **RunOn** parameter was added toohello **Start-AzureAutomationRunbook** cmdlet in version 0.9.1 of Microsoft Azure PowerShell.</span></span>  <span data-ttu-id="5182f-119">Vous devez [télécharger la version la plus récente hello](https://azure.microsoft.com/downloads/) si vous avez une ancienne installée.</span><span class="sxs-lookup"><span data-stu-id="5182f-119">You should [download hello latest version](https://azure.microsoft.com/downloads/) if you have an earlier one installed.</span></span>  <span data-ttu-id="5182f-120">Vous ne devez tooinstall cette version sur une station de travail où vous démarrez hello runbook à partir de Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="5182f-120">You only need tooinstall this version on a workstation where you are starting hello runbook from Windows PowerShell.</span></span>  <span data-ttu-id="5182f-121">Vous n’avez pas besoin de tooinstall sur l’ordinateur de traitement hello, sauf si vous avez l’intention de runbooks toostart à partir de cet ordinateur.</span><span class="sxs-lookup"><span data-stu-id="5182f-121">You do not need tooinstall it on hello worker computer unless you intend toostart runbooks from that computer.</span></span>  <span data-ttu-id="5182f-122">Vous ne pouvez pas actuellement démarrer un runbook sur un Runbook Worker hybride à partir d’un autre runbook, car cela nécessiterait plus récent hello toobe Azure Powershell installé dans votre compte Automation.</span><span class="sxs-lookup"><span data-stu-id="5182f-122">You cannot currently start a runbook on a Hybrid Runbook Worker from another runbook since this would require hello latest version of Azure Powershell toobe installed in your Automation account.</span></span>  <span data-ttu-id="5182f-123">version la plus récente Hello est automatiquement mis à jour dans Azure Automation et automatiquement poussée vers le bas les travailleurs toohello bientôt.</span><span class="sxs-lookup"><span data-stu-id="5182f-123">hello latest version is automatically updated in Azure Automation and automatically pushed down toohello workers soon.</span></span>
>
>

## <a name="runbook-permissions"></a><span data-ttu-id="5182f-124">Autorisations de Runbook</span><span class="sxs-lookup"><span data-stu-id="5182f-124">Runbook permissions</span></span>
<span data-ttu-id="5182f-125">Procédures opérationnelles en cours d’exécution sur un Runbook Worker hybride ne peut pas utiliser hello même méthode qui est généralement utilisé pour les procédures opérationnelles de l’authentification des ressources tooAzure, dans la mesure où ils accèdent à des ressources en dehors d’Azure.</span><span class="sxs-lookup"><span data-stu-id="5182f-125">Runbooks running on a Hybrid Runbook Worker cannot use hello same method that is typically used for runbooks authenticating tooAzure resources, since they are accessing resources outside of Azure.</span></span>  <span data-ttu-id="5182f-126">Hello runbook peut fournir sa propre authentification toolocal ressources, ou vous pouvez spécifier un tooprovide de compte d’identification un contexte utilisateur pour tous les runbooks.</span><span class="sxs-lookup"><span data-stu-id="5182f-126">hello runbook can either provide its own authentication toolocal resources, or you can specify a RunAs account tooprovide a user context for all runbooks.</span></span>

### <a name="runbook-authentication"></a><span data-ttu-id="5182f-127">Authentification des Runbooks</span><span class="sxs-lookup"><span data-stu-id="5182f-127">Runbook authentication</span></span>
<span data-ttu-id="5182f-128">Par défaut, les procédures opérationnelles s’exécute dans le contexte de hello du compte système local de hello sur l’ordinateur local de hello, pour qu’ils doivent fournir leur propre tooresources de l’authentification d’accès.</span><span class="sxs-lookup"><span data-stu-id="5182f-128">By default, runbooks will run in hello context of hello local System account on hello on-premises computer, so they must provide their own authentication tooresources that they will access.</span></span>  

<span data-ttu-id="5182f-129">Vous pouvez utiliser [informations d’identification](http://msdn.microsoft.com/library/dn940015.aspx) et [certificat](http://msdn.microsoft.com/library/dn940013.aspx) actifs dans votre runbook avec les applets de commande qui permettent d’informations d’identification toospecify afin de vous authentifier toodifferent ressources.</span><span class="sxs-lookup"><span data-stu-id="5182f-129">You can use [Credential](http://msdn.microsoft.com/library/dn940015.aspx) and [Certificate](http://msdn.microsoft.com/library/dn940013.aspx) assets in your runbook with cmdlets that allow you toospecify credentials so you can authenticate toodifferent resources.</span></span>  <span data-ttu-id="5182f-130">Hello suivant montre une partie d’un runbook qui redémarre un ordinateur.</span><span class="sxs-lookup"><span data-stu-id="5182f-130">hello following example shows a portion of a runbook that restarts a computer.</span></span>  <span data-ttu-id="5182f-131">Il extrait les informations d’identification à partir d’un nom d’identification de l’élément multimédia et hello d’ordinateur hello à partir d’une ressource de variable et utilise ensuite ces valeurs avec l’applet de commande hello Restart-Computer.</span><span class="sxs-lookup"><span data-stu-id="5182f-131">It retrieves credentials from a credential asset and hello name of hello computer from a variable asset and then uses these values with hello Restart-Computer cmdlet.</span></span>

    $Cred = Get-AzureRmAutomationCredential -ResourceGroupName "ResourceGroup01" -Name "MyCredential"
    $Computer = Get-AzureRmAutomationVariable -ResourceGroupName "ResourceGroup01" -Name  "ComputerName"

    Restart-Computer -ComputerName $Computer -Credential $Cred

<span data-ttu-id="5182f-132">Vous pouvez également exploiter [InlineScript](automation-powershell-workflow.md#inlinescript), qui vous permet de toorun des blocs de code sur un autre ordinateur avec les informations d’identification spécifiées par hello [paramètre commun de PSCredential](http://technet.microsoft.com/library/jj129719.aspx).</span><span class="sxs-lookup"><span data-stu-id="5182f-132">You can also leverage [InlineScript](automation-powershell-workflow.md#inlinescript), which  allows you toorun blocks of code on another computer with credentials specified by hello [PSCredential common parameter](http://technet.microsoft.com/library/jj129719.aspx).</span></span>

### <a name="runas-account"></a><span data-ttu-id="5182f-133">Compte RunAs</span><span class="sxs-lookup"><span data-stu-id="5182f-133">RunAs account</span></span>
<span data-ttu-id="5182f-134">Au lieu de procédures opérationnelles fournir leur propre authentification toolocal ressources, vous pouvez spécifier un **RunAs** compte pour un groupe de travail hybride.</span><span class="sxs-lookup"><span data-stu-id="5182f-134">Instead of having runbooks provide their own authentication toolocal resources, you can specify a **RunAs** account for a Hybrid worker group.</span></span>  <span data-ttu-id="5182f-135">Vous spécifiez un [actif d’informations d’identification](automation-credentials.md) incluant toolocal d’accéder aux ressources, et tous les runbooks s’exécutent sous ces informations d’identification lors de l’exécution sur un Runbook Worker hybride dans le groupe de hello.</span><span class="sxs-lookup"><span data-stu-id="5182f-135">You specify a [credential asset](automation-credentials.md) that has access toolocal resources, and all runbooks run under these credentials when running on a Hybrid Runbook Worker in hello group.</span></span>  

<span data-ttu-id="5182f-136">nom d’utilisateur Hello pour les informations d’identification hello doit être dans un des hello suivant formats :</span><span class="sxs-lookup"><span data-stu-id="5182f-136">hello user name for hello credential must be in one of hello following formats:</span></span>

* <span data-ttu-id="5182f-137">domaine\nom d’utilisateur</span><span class="sxs-lookup"><span data-stu-id="5182f-137">domain\username</span></span>
* username@domain
* <span data-ttu-id="5182f-138">nom d’utilisateur (pour l’ordinateur de comptes locaux toohello local)</span><span class="sxs-lookup"><span data-stu-id="5182f-138">username (for accounts local toohello on-premises computer)</span></span>

<span data-ttu-id="5182f-139">Utilisez hello suivant la procédure toospecify un compte d’identification pour un groupe de travail hybride :</span><span class="sxs-lookup"><span data-stu-id="5182f-139">Use hello following procedure toospecify a RunAs account for a Hybrid worker group:</span></span>

1. <span data-ttu-id="5182f-140">Créer un [actif d’informations d’identification](automation-credentials.md) avec toolocal d’accéder aux ressources.</span><span class="sxs-lookup"><span data-stu-id="5182f-140">Create a [credential asset](automation-credentials.md) with access toolocal resources.</span></span>
2. <span data-ttu-id="5182f-141">Ouvrez le compte Automation de hello Bonjour portail Azure.</span><span class="sxs-lookup"><span data-stu-id="5182f-141">Open hello Automation account in hello Azure portal.</span></span>
3. <span data-ttu-id="5182f-142">Sélectionnez hello **groupes de travail hybride** vignette, puis sélectionnez le groupe de hello.</span><span class="sxs-lookup"><span data-stu-id="5182f-142">Select hello **Hybrid Worker Groups** tile, and then select hello group.</span></span>
4. <span data-ttu-id="5182f-143">Sélectionnez **Tous les paramètres**, puis **Paramètres du groupe Worker hybride**.</span><span class="sxs-lookup"><span data-stu-id="5182f-143">Select **All settings** and then **Hybrid worker group settings**.</span></span>
5. <span data-ttu-id="5182f-144">Modification **exécuter en tant que** de **par défaut** trop**personnalisé**.</span><span class="sxs-lookup"><span data-stu-id="5182f-144">Change **Run As** from **Default** too**Custom**.</span></span>
6. <span data-ttu-id="5182f-145">Sélectionnez les informations d’identification hello et cliquez sur **enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="5182f-145">Select hello credential and click **Save**.</span></span>

### <a name="automation-run-as-account"></a><span data-ttu-id="5182f-146">Compte d’identification Automation</span><span class="sxs-lookup"><span data-stu-id="5182f-146">Automation Run As account</span></span>
<span data-ttu-id="5182f-147">Dans le cadre de votre processus de génération automatisé pour le déploiement de ressources dans Azure, vous pouvez avoir besoin toosupport de systèmes de site tooon accès une tâche ou un ensemble d’étapes dans votre séquence de déploiement.</span><span class="sxs-lookup"><span data-stu-id="5182f-147">As part of your automated build process for deploying resources in Azure, you may require access tooon-premise systems toosupport a task or set of steps in your deployment sequence.</span></span>  <span data-ttu-id="5182f-148">toosupport l’authentification sur Azure à l’aide du compte d’identification hello, vous devez tooinstall hello exécuter en tant que certificat de compte de.</span><span class="sxs-lookup"><span data-stu-id="5182f-148">toosupport authentication against Azure using hello Run As account, you need tooinstall hello Run As account certificate.</span></span>  

<span data-ttu-id="5182f-149">Hello suivant PowerShell runbook, *Export-RunAsCertificateToHybridWorker*, exporte hello exécuter en tant que certificat de votre compte Azure Automation et télécharge et il importe dans le magasin de certificats ordinateur local hello sur un Worker hybride connecté toohello même compte.</span><span class="sxs-lookup"><span data-stu-id="5182f-149">hello following PowerShell runbook, *Export-RunAsCertificateToHybridWorker*, exports hello Run As certificate from your Azure Automation account and downloads and imports it into hello local machine certificate store on a Hybrid worker connected toohello same account.</span></span>  <span data-ttu-id="5182f-150">Une fois cette étape terminée, il vérifie les processus de travail hello peuvent s’authentifier correctement tooAzure à l’aide du compte d’identification hello.</span><span class="sxs-lookup"><span data-stu-id="5182f-150">Once that step is completed, it verifies hello worker can successfully authenticate tooAzure using hello Run As account.</span></span>

    <#PSScriptInfo
    .VERSION 1.0
    .GUID 3a796b9a-623d-499d-86c8-c249f10a6986
    .AUTHOR Azure Automation Team
    .COMPANYNAME Microsoft
    .COPYRIGHT 
    .TAGS Azure Automation 
    .LICENSEURI 
    .PROJECTURI 
    .ICONURI 
    .EXTERNALMODULEDEPENDENCIES 
    .REQUIREDSCRIPTS 
    .EXTERNALSCRIPTDEPENDENCIES 
    .RELEASENOTES
    #>

    <#  
    .SYNOPSIS  
    Exports hello Run As certificate from an Azure Automation account tooa hybrid worker in that account. 
  
    .DESCRIPTION  
    This runbook exports hello Run As certificate from an Azure Automation account tooa hybrid worker in that account.
    Run this runbook in hello hybrid worker where you want hello certificate installed.
    This allows hello use of hello AzureRunAsConnection tooauthenticate tooAzure and manage Azure resources from runbooks running in hello hybrid worker.

    .EXAMPLE
    .\Export-RunAsCertificateToHybridWorker

    .NOTES
    AUTHOR: Azure Automation Team 
    LASTEDIT: 2016.10.13
    #>

    [OutputType([string])] 

    # Set hello password used for this certificate
    $Password = "YourStrongPasswordForTheCert"

    # Stop on errors
    $ErrorActionPreference = 'stop'

    # Get hello management certificate that will be used toomake calls into Azure Service Management resources
    $RunAsCert = Get-AutomationCertificate -Name "AzureRunAsCertificate"
       
    # location toostore temporary certificate in hello Automation service host
    $CertPath = Join-Path $env:temp  "AzureRunAsCertificate.pfx"
   
    # Save hello certificate
    $Cert = $RunAsCert.Export("pfx",$Password)
    Set-Content -Value $Cert -Path $CertPath -Force -Encoding Byte | Write-Verbose 

    Write-Output ("Importing certificate into $env:computername local machine root store from " + $CertPath)
    $SecurePassword = ConvertTo-SecureString $Password -AsPlainText -Force
    Import-PfxCertificate -FilePath $CertPath -CertStoreLocation Cert:\LocalMachine\My -Password $SecurePassword -Exportable | Write-Verbose

    # Test that authentication tooAzure Resource Manager is working
    $RunAsConnection = Get-AutomationConnection -Name "AzureRunAsConnection" 
    
    Add-AzureRmAccount `
      -ServicePrincipal `
      -TenantId $RunAsConnection.TenantId `
      -ApplicationId $RunAsConnection.ApplicationId `
      -CertificateThumbprint $RunAsConnection.CertificateThumbprint | Write-Verbose

    Set-AzureRmContext -SubscriptionId $RunAsConnection.SubscriptionID | Write-Verbose

    # List automation accounts tooconfirm Azure Resource Manager calls are working
    Get-AzureRmAutomationAccount | Select AutomationAccountName

<span data-ttu-id="5182f-151">Enregistrer hello *Export-RunAsCertificateToHybridWorker* runbook tooyour équipé d’un `.ps1` extension.</span><span class="sxs-lookup"><span data-stu-id="5182f-151">Save hello *Export-RunAsCertificateToHybridWorker* runbook tooyour computer with a `.ps1` extension.</span></span>  <span data-ttu-id="5182f-152">Importer dans votre compte Automation et modifier les runbook hello, la modification de valeur hello de variable de hello `$Password` avec votre mot de passe.</span><span class="sxs-lookup"><span data-stu-id="5182f-152">Import it into your Automation account and edit hello runbook, changing hello value of hello variable `$Password` with your own password.</span></span>  <span data-ttu-id="5182f-153">Publier, puis exécutez runbook hello ciblant un groupe Worker hybride hello qui s’exécutent et authentifier des runbooks à l’aide du compte d’identification hello.</span><span class="sxs-lookup"><span data-stu-id="5182f-153">Publish and then run hello runbook targeting hello Hybrid Worker group that run and authenticate runbooks using hello Run As account.</span></span>  <span data-ttu-id="5182f-154">Hello travail flux rapports hello tentative tooimport hello certificat dans le magasin de l’ordinateur local hello et suit avec plusieurs lignes, selon le nombre de comptes Automation est défini dans votre abonnement et si l’authentification réussit.</span><span class="sxs-lookup"><span data-stu-id="5182f-154">hello job stream reports hello attempt tooimport hello certificate into hello local machine store, and follows with multiple lines depending on how many Automation accounts are defined in your subscription and if authentication is successful.</span></span>  

## <a name="troubleshooting-runbooks-on-hybrid-runbook-worker"></a><span data-ttu-id="5182f-155">Résolution de problèmes de runbooks sur un Runbook Worker hybride</span><span class="sxs-lookup"><span data-stu-id="5182f-155">Troubleshooting runbooks on Hybrid Runbook Worker</span></span>
<span data-ttu-id="5182f-156">Les journaux sont stockés localement sur chaque Worker hybride à l’emplacement C:\ProgramData\Microsoft\System Center\Orchestrator\7.2\SMA\Sandboxes.</span><span class="sxs-lookup"><span data-stu-id="5182f-156">Logs are stored locally on each hybrid worker at C:\ProgramData\Microsoft\System Center\Orchestrator\7.2\SMA\Sandboxes.</span></span>  <span data-ttu-id="5182f-157">Worker hybride enregistre également les erreurs et les événements dans le journal des événements Windows hello sous **d’Application et de Services Logs\Microsoft-SMA\Operational**.</span><span class="sxs-lookup"><span data-stu-id="5182f-157">Hybrid worker also records errors and events in hello Windows event log under **Application and Services Logs\Microsoft-SMA\Operational**.</span></span>  <span data-ttu-id="5182f-158">Événements liés toorunbooks exécutées sur le travail de hello sont écrits en trop**d’Application et de Services Logs\Microsoft-Automation\Operational**.</span><span class="sxs-lookup"><span data-stu-id="5182f-158">Events related toorunbooks executed on hello worker are written too**Application and Services Logs\Microsoft-Automation\Operational**.</span></span>  <span data-ttu-id="5182f-159">Hello **Microsoft-SMA** journal inclut des nombreux plus événements connexes toohello runbook toohello envoyées hello et travail de traitement de hello runbook.</span><span class="sxs-lookup"><span data-stu-id="5182f-159">hello **Microsoft-SMA** log includes many more events related toohello runbook job pushed toohello worker and hello processing of hello runbook.</span></span>  <span data-ttu-id="5182f-160">Lors de hello **Microsoft-Automation** journal des événements n’a pas de nombreux événements avec les détails en aidant hello résolution des problèmes d’exécution de runbook, vous trouverez au moins des résultats de la tâche du runbook hello hello.</span><span class="sxs-lookup"><span data-stu-id="5182f-160">While hello **Microsoft-Automation** event log does not have many events with details assisting with hello troubleshooting of runbook execution, you will at least find hello results of hello runbook job.</span></span>  

<span data-ttu-id="5182f-161">[Runbook de sortie et messages](automation-runbook-output-and-messages.md) sont envoyés tooAzure Automation à partir de workers hybrides simplement que les travaux de runbook s’exécutent dans le cloud de hello.</span><span class="sxs-lookup"><span data-stu-id="5182f-161">[Runbook output and messages](automation-runbook-output-and-messages.md) are sent tooAzure Automation from hybrid workers just like runbook jobs run in hello cloud.</span></span>  <span data-ttu-id="5182f-162">Vous pouvez également activer hello Verbose et flux de progression hello même façon que vous le feriez pour d’autres runbooks.</span><span class="sxs-lookup"><span data-stu-id="5182f-162">You can also enable hello Verbose and Progress streams hello same way you would for other runbooks.</span></span>  

<span data-ttu-id="5182f-163">Si vos runbooks ne sont pas correctement terminées et le résumé des tâches hello présente l’état de **Suspended**, passez en revue hello article de résolution des problèmes [Runbook Worker hybride : une tâche de runbook se termine avec l’état Suspendu](automation-troubleshooting-hybrid-runbook-worker.md#a-runbook-job-terminates-with-a-status-of-suspended).</span><span class="sxs-lookup"><span data-stu-id="5182f-163">If your runbooks are not completing successfully and hello job summary shows a status of **Suspended**, please review hello troubleshooting article [Hybrid Runbook Worker: A runbook job terminates with a status of Suspended](automation-troubleshooting-hybrid-runbook-worker.md#a-runbook-job-terminates-with-a-status-of-suspended).</span></span>   

## <a name="next-steps"></a><span data-ttu-id="5182f-164">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="5182f-164">Next steps</span></span>
* <span data-ttu-id="5182f-165">toolearn savoir plus sur hello différentes méthodes qui peuvent être utilisé toostart un runbook, consultez [démarrage d’un Runbook dans Azure Automation](automation-starting-a-runbook.md).</span><span class="sxs-lookup"><span data-stu-id="5182f-165">toolearn more about hello different methods that can be used toostart a runbook, see [Starting a Runbook in Azure Automation](automation-starting-a-runbook.md).</span></span>  
* <span data-ttu-id="5182f-166">toounderstand hello différentes procédures pour travailler avec PowerShell et les flux de travail PowerShell runbooks dans Azure Automation à l’aide de l’éditeur de texte hello, consultez [modification d’un Runbook dans Azure Automation](automation-edit-textual-runbook.md)</span><span class="sxs-lookup"><span data-stu-id="5182f-166">toounderstand hello different procedures for working with PowerShell and PowerShell Workflow runbooks in Azure Automation using hello textual editor, see [Editing a Runbook in Azure Automation](automation-edit-textual-runbook.md)</span></span>
