---
title: "Compilation de configurations dans Azure Automation DSC | Microsoft Docs"
description: "Cet article explique comment compiler des configurations d’état souhaité (DSC) pour Azure Automation."
services: automation
documentationcenter: na
author: eslesar
manager: carmonm
ms.assetid: 49f20b31-4fa5-4712-b1c7-8f4409f1aecc
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: powershell
ms.workload: na
ms.date: 02/07/2017
ms.author: magoedte; eslesar
ms.openlocfilehash: 1aadd604e676659475f00760af3b0bdfb13a4792
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="compiling-configurations-in-azure-automation-dsc"></a><span data-ttu-id="22a6b-103">Compilation de configurations dans Azure Automation DSC</span><span class="sxs-lookup"><span data-stu-id="22a6b-103">Compiling configurations in Azure Automation DSC</span></span>

<span data-ttu-id="22a6b-104">Dans Azure Automation, vous pouvez compiler des configurations d’état souhaité (DSC) de deux manières : dans le portail Azure et avec Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="22a6b-104">You can compile Desired State Configuration (DSC) configurations in two ways with Azure Automation: in the Azure portal, and with Windows PowerShell.</span></span> <span data-ttu-id="22a6b-105">Le tableau suivant vous aide à déterminer quand utiliser chaque méthode en fonction des caractéristiques de chacune :</span><span class="sxs-lookup"><span data-stu-id="22a6b-105">The following table will help you determine when to use which method based on the characteristics of each:</span></span>

### <a name="azure-portal"></a><span data-ttu-id="22a6b-106">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="22a6b-106">Azure portal</span></span>

* <span data-ttu-id="22a6b-107">Méthode la plus simple avec une interface utilisateur interactive</span><span class="sxs-lookup"><span data-stu-id="22a6b-107">Simplest method with interactive user interface</span></span>
* <span data-ttu-id="22a6b-108">Formulaire pour fournir les valeurs de paramètres simples</span><span class="sxs-lookup"><span data-stu-id="22a6b-108">Form to provide simple parameter values</span></span>
* <span data-ttu-id="22a6b-109">Suivi aisé de l’état des tâches</span><span class="sxs-lookup"><span data-stu-id="22a6b-109">Easily track job state</span></span>
* <span data-ttu-id="22a6b-110">Accès authentifié avec ouverture de session Azure</span><span class="sxs-lookup"><span data-stu-id="22a6b-110">Access authenticated with Azure logon</span></span>

### <a name="windows-powershell"></a><span data-ttu-id="22a6b-111">Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="22a6b-111">Windows PowerShell</span></span>

* <span data-ttu-id="22a6b-112">Appel à partir de la ligne de commande avec les applets de commande Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="22a6b-112">Call from command line with Windows PowerShell cmdlets</span></span>
* <span data-ttu-id="22a6b-113">Possibilité d’inclusion dans une solution automatisée à plusieurs étapes</span><span class="sxs-lookup"><span data-stu-id="22a6b-113">Can be included in automated solution with multiple steps</span></span>
* <span data-ttu-id="22a6b-114">Fourniture de valeurs de paramètres simples et complexes</span><span class="sxs-lookup"><span data-stu-id="22a6b-114">Provide simple and complex parameter values</span></span>
* <span data-ttu-id="22a6b-115">Suivi de l’état des tâches</span><span class="sxs-lookup"><span data-stu-id="22a6b-115">Track job state</span></span>
* <span data-ttu-id="22a6b-116">Client requis pour prendre en charge les applets de commande PowerShell</span><span class="sxs-lookup"><span data-stu-id="22a6b-116">Client required to support PowerShell cmdlets</span></span>
* <span data-ttu-id="22a6b-117">Transmission ConfigurationData</span><span class="sxs-lookup"><span data-stu-id="22a6b-117">Pass ConfigurationData</span></span>
* <span data-ttu-id="22a6b-118">Compilation de configurations utilisant des informations d’identification</span><span class="sxs-lookup"><span data-stu-id="22a6b-118">Compile configurations that use credentials</span></span>

<span data-ttu-id="22a6b-119">Une fois que vous avez choisi une méthode de compilation, vous pouvez suivre les procédures correspondantes ci-dessous pour lancer la compilation.</span><span class="sxs-lookup"><span data-stu-id="22a6b-119">Once you have decided on a compilation method, you can follow the respective procedures below to start compiling.</span></span>

## <a name="compiling-a-dsc-configuration-with-the-azure-portal"></a><span data-ttu-id="22a6b-120">Compilation d’une configuration DSC avec le portail Azure</span><span class="sxs-lookup"><span data-stu-id="22a6b-120">Compiling a DSC Configuration with the Azure portal</span></span>

1. <span data-ttu-id="22a6b-121">Dans votre compte Automation, cliquez sur **Configurations DSC**.</span><span class="sxs-lookup"><span data-stu-id="22a6b-121">From your Automation account, click **DSC Configurations**.</span></span>
2. <span data-ttu-id="22a6b-122">Cliquez sur une configuration pour ouvrir son panneau.</span><span class="sxs-lookup"><span data-stu-id="22a6b-122">Click a configuration to open its blade.</span></span>
3. <span data-ttu-id="22a6b-123">Cliquez sur **Compiler**.</span><span class="sxs-lookup"><span data-stu-id="22a6b-123">Click **Compile**.</span></span>
4. <span data-ttu-id="22a6b-124">Si la configuration ne possède aucun paramètre, vous devez confirmer si vous souhaitez la compiler.</span><span class="sxs-lookup"><span data-stu-id="22a6b-124">If the configuration has no parameters, you will be prompted to confirm whether you want to compile it.</span></span> <span data-ttu-id="22a6b-125">Si la configuration possède des paramètres, le panneau **Compiler la configuration** s’ouvre afin que vous puissiez fournir les valeurs de paramètre.</span><span class="sxs-lookup"><span data-stu-id="22a6b-125">If the configuration has parameters, the **Compile Configuration** blade will open so you can provide parameter values.</span></span> <span data-ttu-id="22a6b-126">Pour plus d’informations sur les paramètres, voir la section [**Paramètres de base**](#basic-parameters) ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="22a6b-126">See the [**Basic Parameters**](#basic-parameters) section below for further details on parameters.</span></span>
5. <span data-ttu-id="22a6b-127">Le panneau **Tâche de compilation** est ouvert de sorte que vous pouvez suivre l’état de la tâche de compilation, ainsi que les configurations de nœud (documents de configuration MOF) qui ont dû être placés sur le serveur collecteur Azure Automation DSC.</span><span class="sxs-lookup"><span data-stu-id="22a6b-127">The **Compilation Job** blade is opened so that you can track the compilation job's status, and the node configurations (MOF configuration documents) it caused to be placed on the Azure Automation DSC Pull Server.</span></span>

## <a name="compiling-a-dsc-configuration-with-windows-powershell"></a><span data-ttu-id="22a6b-128">Compilation d’une configuration DSC avec Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="22a6b-128">Compiling a DSC Configuration with Windows PowerShell</span></span>

<span data-ttu-id="22a6b-129">Vous pouvez utiliser [`Start-AzureRmAutomationDscCompilationJob`](/powershell/module/azurerm.automation/start-azurermautomationdsccompilationjob) pour démarrer la compilation avec Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="22a6b-129">You can use [`Start-AzureRmAutomationDscCompilationJob`](/powershell/module/azurerm.automation/start-azurermautomationdsccompilationjob) to start compiling with Windows PowerShell.</span></span> <span data-ttu-id="22a6b-130">L’exemple de code suivant commence la compilation d’une configuration DSC appelée **SampleConfig**.</span><span class="sxs-lookup"><span data-stu-id="22a6b-130">The following sample code starts compilation of a DSC configuration called **SampleConfig**.</span></span>

```powershell
Start-AzureRmAutomationDscCompilationJob -ResourceGroupName "MyResourceGroup" -AutomationAccountName "MyAutomationAccount" -ConfigurationName "SampleConfig"
```

<span data-ttu-id="22a6b-131">`Start-AzureRmAutomationDscCompilationJob` renvoie un objet de tâche de compilation que vous pouvez utiliser pour suivre son état.</span><span class="sxs-lookup"><span data-stu-id="22a6b-131">`Start-AzureRmAutomationDscCompilationJob` returns a compilation job object that you can use to track its status.</span></span> <span data-ttu-id="22a6b-132">Vous pouvez ensuite utiliser cet objet de tâche de compilation avec [`Get-AzureRmAutomationDscCompilationJob`](/powershell/module/azurerm.automation/get-azurermautomationdsccompilationjob) pour déterminer l’état de la tâche de compilation, et [`Get-AzureRmAutomationDscCompilationJobOutput`](/powershell/module/azurerm.automation/get-azurermautomationdsccompilationjoboutput) pour afficher ses flux (sortie).</span><span class="sxs-lookup"><span data-stu-id="22a6b-132">You can then use this compilation job object with [`Get-AzureRmAutomationDscCompilationJob`](/powershell/module/azurerm.automation/get-azurermautomationdsccompilationjob) to determine the status of the compilation job, and [`Get-AzureRmAutomationDscCompilationJobOutput`](/powershell/module/azurerm.automation/get-azurermautomationdsccompilationjoboutput) to view its streams (output).</span></span> <span data-ttu-id="22a6b-133">L’exemple de code suivant démarre la compilation de la configuration **SampleConfig** , attend qu’elle soit terminée, puis affiche ses flux.</span><span class="sxs-lookup"><span data-stu-id="22a6b-133">The following sample code starts compilation of the **SampleConfig** configuration, waits until it has completed, and then displays its streams.</span></span>

```powershell
$CompilationJob = Start-AzureRmAutomationDscCompilationJob -ResourceGroupName "MyResourceGroup" -AutomationAccountName "MyAutomationAccount" -ConfigurationName "SampleConfig"

while($CompilationJob.EndTime –eq $null -and $CompilationJob.Exception –eq $null)
{
    $CompilationJob = $CompilationJob | Get-AzureRmAutomationDscCompilationJob
    Start-Sleep -Seconds 3
}

$CompilationJob | Get-AzureRmAutomationDscCompilationJobOutput –Stream Any
```

## <a name="basic-parameters"></a><span data-ttu-id="22a6b-134">Paramètres de base</span><span class="sxs-lookup"><span data-stu-id="22a6b-134">Basic Parameters</span></span>
<span data-ttu-id="22a6b-135">La déclaration de paramètres dans les configurations DSC, y compris les types de paramètres et les propriétés, fonctionne de la même manière que pour les runbooks Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="22a6b-135">Parameter declaration in DSC configurations, including parameter types and properties, works the same as in Azure Automation runbooks.</span></span> <span data-ttu-id="22a6b-136">Consultez [Démarrage d’un runbook dans Azure Automation](automation-starting-a-runbook.md) pour en savoir plus sur les paramètres de runbooks.</span><span class="sxs-lookup"><span data-stu-id="22a6b-136">See [Starting a runbook in Azure Automation](automation-starting-a-runbook.md) to learn more about runbook parameters.</span></span>

<span data-ttu-id="22a6b-137">L’exemple suivant utilise deux paramètres appelés **FeatureName** et **IsPresent** pour déterminer les valeurs des propriétés dans la configuration du nœud **ParametersExample.sample**, générée pendant la compilation.</span><span class="sxs-lookup"><span data-stu-id="22a6b-137">The following example uses two parameters called **FeatureName** and **IsPresent**, to determine the values of properties in the **ParametersExample.sample** node configuration, generated during compilation.</span></span>

```powershell
Configuration ParametersExample
{
    param(
        [Parameter(Mandatory=$true)]

        [string] $FeatureName,

        [Parameter(Mandatory=$true)]
        [boolean] $IsPresent
    )

    $EnsureString = "Present"
    if($IsPresent -eq $false)
    {
        $EnsureString = "Absent"
    }

    Node "sample"
    {
        WindowsFeature ($FeatureName + "Feature")
        {
            Ensure = $EnsureString
            Name = $FeatureName
        }
    }
}
```

<span data-ttu-id="22a6b-138">Vous pouvez compiler les configurations DSC qui utilisent des paramètres de base dans le portail Azure Automation DSC ou avec Azure PowerShell :</span><span class="sxs-lookup"><span data-stu-id="22a6b-138">You can compile DSC Configurations that use basic parameters in the Azure Automation DSC portal, or with Azure PowerShell:</span></span>

### <a name="portal"></a><span data-ttu-id="22a6b-139">Portail</span><span class="sxs-lookup"><span data-stu-id="22a6b-139">Portal</span></span>

<span data-ttu-id="22a6b-140">Dans le portail, vous pouvez entrer des valeurs de paramètre après avoir cliqué sur **Compiler**.</span><span class="sxs-lookup"><span data-stu-id="22a6b-140">In the portal, you can enter parameter values after clicking **Compile**.</span></span>

![texte de remplacement](./media/automation-dsc-compile/DSC_compiling_1.png)

### <a name="powershell"></a><span data-ttu-id="22a6b-142">PowerShell</span><span class="sxs-lookup"><span data-stu-id="22a6b-142">PowerShell</span></span>

<span data-ttu-id="22a6b-143">PowerShell requiert des paramètres dans une [table de hachage](http://technet.microsoft.com/library/hh847780.aspx) où la clé correspond au nom de paramètre et la valeur est égale à la valeur du paramètre.</span><span class="sxs-lookup"><span data-stu-id="22a6b-143">PowerShell requires parameters in a [hashtable](http://technet.microsoft.com/library/hh847780.aspx) where the key matches the parameter name, and the value equals the parameter value.</span></span>

```powershell
$Parameters = @{
    "FeatureName" = "Web-Server"
    "IsPresent" = $False
}

Start-AzureRmAutomationDscCompilationJob -ResourceGroupName "MyResourceGroup" -AutomationAccountName "MyAutomationAccount" -ConfigurationName "ParametersExample" -Parameters $Parameters
```

<span data-ttu-id="22a6b-144">Pour plus d’informations sur la transmission d’informations d’identification PowerShell en tant que paramètres, voir la section <a href="#credential-assets">**Ressources d’informations d’identification**</a> ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="22a6b-144">For information about passing PSCredentials as parameters, see <a href="#credential-assets">**Credential Assets**</a> below.</span></span>

## <a name="configurationdata"></a><span data-ttu-id="22a6b-145">ConfigurationData</span><span class="sxs-lookup"><span data-stu-id="22a6b-145">ConfigurationData</span></span>
<span data-ttu-id="22a6b-146">**ConfigurationData** vous permet de séparer la configuration structurelle de toute configuration spécifique de l’environnement lors de l’utilisation de la configuration de l’état souhaité PowerShell.</span><span class="sxs-lookup"><span data-stu-id="22a6b-146">**ConfigurationData** allows you to separate structural configuration from any environment specific configuration while using PowerShell DSC.</span></span> <span data-ttu-id="22a6b-147">Consultez [Distinguer « objet » et « emplacement » dans la configuration de l’état souhaité PowerShell](http://blogs.msdn.com/b/powershell/archive/2014/01/09/continuous-deployment-using-dsc-with-minimal-change.aspx) pour en savoir plus sur **ConfigurationData**.</span><span class="sxs-lookup"><span data-stu-id="22a6b-147">See [Separating "What" from "Where" in PowerShell DSC](http://blogs.msdn.com/b/powershell/archive/2014/01/09/continuous-deployment-using-dsc-with-minimal-change.aspx) to learn more about **ConfigurationData**.</span></span>

> [!NOTE]
> <span data-ttu-id="22a6b-148">Vous pouvez utiliser **ConfigurationData** lors de la compilation dans Azure Automation DSC à l’aide d’Azure PowerShell, mais pas dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="22a6b-148">You can use **ConfigurationData** when compiling in Azure Automation DSC using Azure PowerShell, but not in the Azure portal.</span></span>

<span data-ttu-id="22a6b-149">L’exemple de configuration DSC suivant utilise **ConfigurationData** via les mots-clés **$ConfigurationData** et **$AllNodes**.</span><span class="sxs-lookup"><span data-stu-id="22a6b-149">The following example DSC configuration uses **ConfigurationData** via the **$ConfigurationData** and **$AllNodes** keywords.</span></span> <span data-ttu-id="22a6b-150">Vous aurez également besoin du module [**xWebAdministration**](https://www.powershellgallery.com/packages/xWebAdministration/) pour cet exemple :</span><span class="sxs-lookup"><span data-stu-id="22a6b-150">You'll also need the [**xWebAdministration** module](https://www.powershellgallery.com/packages/xWebAdministration/) for this example:</span></span>

```powershell
Configuration ConfigurationDataSample
{
    Import-DscResource -ModuleName xWebAdministration -Name MSFT_xWebsite

    Write-Verbose $ConfigurationData.NonNodeData.SomeMessage

    Node $AllNodes.Where{$_.Role -eq "WebServer"}.NodeName
    {
        xWebsite Site
        {
            Name = $Node.SiteName
            PhysicalPath = $Node.SiteContents
            Ensure   = "Present"
        }
    }
}
```

<span data-ttu-id="22a6b-151">Vous pouvez compiler la configuration DSC ci-dessus avec PowerShell.</span><span class="sxs-lookup"><span data-stu-id="22a6b-151">You can compile the DSC configuration above with PowerShell.</span></span> <span data-ttu-id="22a6b-152">La commande PowerShell ci-dessous ajoute deux configurations de nœud au serveur collecteur Azure Automation DSC : **ConfigurationDataSample.MyVM1** et **ConfigurationDataSample.MyVM3** :</span><span class="sxs-lookup"><span data-stu-id="22a6b-152">The below PowerShell adds two node configurations to the Azure Automation DSC Pull Server: **ConfigurationDataSample.MyVM1** and **ConfigurationDataSample.MyVM3**:</span></span>

```powershell
$ConfigData = @{
    AllNodes = @(
        @{
            NodeName = "MyVM1"
            Role = "WebServer"
        },
        @{
            NodeName = "MyVM2"
            Role = "SQLServer"
        },
        @{
            NodeName = "MyVM3"
            Role = "WebServer"
        }
    )

    NonNodeData = @{
        SomeMessage = "I love Azure Automation DSC!"
    }
}

Start-AzureRmAutomationDscCompilationJob -ResourceGroupName "MyResourceGroup" -AutomationAccountName "MyAutomationAccount" -ConfigurationName "ConfigurationDataSample" -ConfigurationData $ConfigData
```

## <a name="assets"></a><span data-ttu-id="22a6b-153">Éléments multimédias</span><span class="sxs-lookup"><span data-stu-id="22a6b-153">Assets</span></span>

<span data-ttu-id="22a6b-154">Les références de ressources sont les mêmes dans les configurations Azure Automation DSC et les runbooks.</span><span class="sxs-lookup"><span data-stu-id="22a6b-154">Asset references are the same in Azure Automation DSC configurations and runbooks.</span></span> <span data-ttu-id="22a6b-155">Consultez les liens suivants pour plus d’informations :</span><span class="sxs-lookup"><span data-stu-id="22a6b-155">See the following for more information:</span></span>

* [<span data-ttu-id="22a6b-156">Certificats</span><span class="sxs-lookup"><span data-stu-id="22a6b-156">Certificates</span></span>](automation-certificates.md)
* [<span data-ttu-id="22a6b-157">Connexions</span><span class="sxs-lookup"><span data-stu-id="22a6b-157">Connections</span></span>](automation-connections.md)
* [<span data-ttu-id="22a6b-158">Informations d'identification</span><span class="sxs-lookup"><span data-stu-id="22a6b-158">Credentials</span></span>](automation-credentials.md)
* [<span data-ttu-id="22a6b-159">Variables</span><span class="sxs-lookup"><span data-stu-id="22a6b-159">Variables</span></span>](automation-variables.md)

### <a name="credential-assets"></a><span data-ttu-id="22a6b-160">Ressources d’informations d’identification</span><span class="sxs-lookup"><span data-stu-id="22a6b-160">Credential Assets</span></span>

<span data-ttu-id="22a6b-161">Bien que les configurations DSC dans Azure Automation puissent référencer des ressources d’informations d’identification en utilisant **Get-AzureRmAutomationCredential**, vous pouvez également transmettre les ressources d’informations d’identification par le biais de paramètres si vous le souhaitez.</span><span class="sxs-lookup"><span data-stu-id="22a6b-161">While DSC configurations in Azure Automation can reference credential assets using **Get-AzureRmAutomationCredential**, credential assets can also be passed in via parameters, if desired.</span></span> <span data-ttu-id="22a6b-162">Si une configuration accepte un paramètre de type **PSCredential** , vous devez transmettre le nom de chaîne d’une ressource d’informations d’identification Azure Automation comme valeur de ce paramètre, plutôt qu’un objet PSCredential.</span><span class="sxs-lookup"><span data-stu-id="22a6b-162">If a configuration takes a parameter of **PSCredential** type, then you need to pass the string name of an Azure Automation credential asset as that parameter’s value, rather than a PSCredential object.</span></span> <span data-ttu-id="22a6b-163">En arrière-plan, la ressource d’informations d’identification Azure Automation portant le même nom est récupérée et transmise à la configuration.</span><span class="sxs-lookup"><span data-stu-id="22a6b-163">Behind the scenes, the Azure Automation credential asset with that name will be retrieved and passed to the configuration.</span></span>

<span data-ttu-id="22a6b-164">Conserver les informations d’identification en sûreté dans les configurations de nœud (documents de configuration MOF) nécessite le chiffrement des informations d’identification dans le fichier MOF de configuration de nœud.</span><span class="sxs-lookup"><span data-stu-id="22a6b-164">Keeping credentials secure in node configurations (MOF configuration documents) requires encrypting the credentials in the node configuration MOF file.</span></span> <span data-ttu-id="22a6b-165">Azure Automation va encore plus loin et chiffre la totalité du fichier MOF.</span><span class="sxs-lookup"><span data-stu-id="22a6b-165">Azure Automation takes this one step further and encrypts the entire MOF file.</span></span> <span data-ttu-id="22a6b-166">Cependant, actuellement, vous devez indiquer à la configuration de l’état souhaité PowerShell que vous êtes d’accord pour que les informations d’identification soient extraites en texte brut lors de la génération du fichier MOF de configuration de nœud, parce que la configuration de l’état souhaité PowerShell ne sait pas qu’Azure Automation va chiffrer l’intégralité du fichier MOF après sa génération via une tâche de compilation.</span><span class="sxs-lookup"><span data-stu-id="22a6b-166">However, currently you must tell PowerShell DSC it is okay for credentials to be outputted in plain text during node configuration MOF generation, because PowerShell DSC doesn’t know that Azure Automation will be encrypting the entire MOF file after its generation via a compilation job.</span></span>

<span data-ttu-id="22a6b-167">Vous pouvez indiquer à la configuration DSC PowerShell que vous êtes d’accord pour que les informations d’identification soient extraites en texte brut dans les fichiers MOF de configuration de nœud générés en utilisant [**ConfigurationData**](#configurationdata).</span><span class="sxs-lookup"><span data-stu-id="22a6b-167">You can tell PowerShell DSC that it is okay for credentials to be outputted in plain text in the generated node configuration MOFs using [**ConfigurationData**](#configurationdata).</span></span> <span data-ttu-id="22a6b-168">Vous devez transmettre `PSDscAllowPlainTextPassword = $true` par le biais de **ConfigurationData** pour chaque nom de bloc de nœuds qui apparaît dans la configuration DSC et utilise les informations d’identification.</span><span class="sxs-lookup"><span data-stu-id="22a6b-168">You should pass `PSDscAllowPlainTextPassword = $true` via **ConfigurationData** for each node block’s name that appears in the DSC configuration and uses credentials.</span></span>

<span data-ttu-id="22a6b-169">L’exemple suivant montre une configuration de l’état souhaité qui utilise une ressource d’informations d’identification Automation.</span><span class="sxs-lookup"><span data-stu-id="22a6b-169">The following example shows a DSC configuration that uses an Automation credential asset.</span></span>

```powershell
Configuration CredentialSample
{
    $Cred = Get-AzureRmAutomationCredential -ResourceGroupName "ResourceGroup01" -AutomationAccountName "AutomationAcct" -Name "SomeCredentialAsset"

    Node $AllNodes.NodeName
    {
        File ExampleFile
        {
            SourcePath = "\\Server\share\path\file.ext"
            DestinationPath = "C:\destinationPath"
            Credential = $Cred
        }
    }
}
```

<span data-ttu-id="22a6b-170">Vous pouvez compiler la configuration DSC ci-dessus avec PowerShell.</span><span class="sxs-lookup"><span data-stu-id="22a6b-170">You can compile the DSC configuration above with PowerShell.</span></span> <span data-ttu-id="22a6b-171">La commande PowerShell ci-dessous ajoute deux configurations de nœud au serveur collecteur Azure Automation DSC : **CredentialSample.MyVM1** et **CredentialSample.MyVM2**.</span><span class="sxs-lookup"><span data-stu-id="22a6b-171">The below PowerShell adds two node configurations to the Azure Automation DSC Pull Server:  **CredentialSample.MyVM1** and **CredentialSample.MyVM2**.</span></span>

```powershell
$ConfigData = @{
    AllNodes = @(
        @{
            NodeName = "*"
            PSDscAllowPlainTextPassword = $True
        },
        @{
            NodeName = "MyVM1"
        },
        @{
            NodeName = "MyVM2"
        }
    )
}

Start-AzureRmAutomationDscCompilationJob -ResourceGroupName "MyResourceGroup" -AutomationAccountName "MyAutomationAccount" -ConfigurationName "CredentialSample" -ConfigurationData $ConfigData
```

## <a name="importing-node-configurations"></a><span data-ttu-id="22a6b-172">Importation de configurations de nœuds</span><span class="sxs-lookup"><span data-stu-id="22a6b-172">Importing node configurations</span></span>

<span data-ttu-id="22a6b-173">Vous pouvez également importer des configurations de nœuds (MOF) que vous avez compilées en dehors d’Azure.</span><span class="sxs-lookup"><span data-stu-id="22a6b-173">You can also import node configuratons (MOFs) that you have compiled outside of Azure.</span></span> <span data-ttu-id="22a6b-174">Cette configuration de nœuds offre l’avantage de pouvoir être signée.</span><span class="sxs-lookup"><span data-stu-id="22a6b-174">One advantage of this is that node confiturations can be signed.</span></span>
<span data-ttu-id="22a6b-175">Une configuration de nœuds signée est vérifiée localement sur un nœud géré par l’agent DSC, garantissant ainsi que la configuration appliquée au nœud provient d’une source autorisée.</span><span class="sxs-lookup"><span data-stu-id="22a6b-175">A signed node configuration is verified locally on a managed node by the DSC agent, ensuring that the configuration being applied to the node comes from an authorized source.</span></span>

> [!NOTE]
> <span data-ttu-id="22a6b-176">Vous pouvez importer des configurations signées dans votre compte Azure Automation, mais Azure Automation ne prend pas en charge la compilation de configurations signées.</span><span class="sxs-lookup"><span data-stu-id="22a6b-176">You can use import signed configurations into your Azure Automation account, but Azure Automation does not currently support compiling signed configurations.</span></span>

> [!NOTE]
> <span data-ttu-id="22a6b-177">Un fichier de configuration de nœuds ne doit pas être supérieur à 1 Mo pour pouvoir être importé dans Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="22a6b-177">A node configuration file must be no larger than 1 MB to allow it to be imported into Azure Automation.</span></span>

<span data-ttu-id="22a6b-178">Pour apprendre à signer des configurations de nœuds, consultez le site https://msdn.microsoft.com/en-us/powershell/wmf/5.1/dsc-improvements#how-to-sign-configuration-and-module.</span><span class="sxs-lookup"><span data-stu-id="22a6b-178">You can learn how to sign node configurations at https://msdn.microsoft.com/en-us/powershell/wmf/5.1/dsc-improvements#how-to-sign-configuration-and-module.</span></span>

### <a name="importing-a-node-configuration-in-the-azure-portal"></a><span data-ttu-id="22a6b-179">Importation d’une configuration de nœuds dans le portail Azure</span><span class="sxs-lookup"><span data-stu-id="22a6b-179">Importing a node configuration in the Azure portal</span></span>

1. <span data-ttu-id="22a6b-180">Dans votre compte Automation, cliquez sur **Configurations de nœuds DSC**.</span><span class="sxs-lookup"><span data-stu-id="22a6b-180">From your Automation account, click **DSC node configurations**.</span></span>

    ![Configurations de nœuds DSC](./media/automation-dsc-compile/node-config.png)
2. <span data-ttu-id="22a6b-182">Dans le panneau **Configurations de nœuds DSC**, cliquez sur **Ajouter une configuration de nœuds**.</span><span class="sxs-lookup"><span data-stu-id="22a6b-182">In the **DSC node configurations** blade, click **Add a NodeConfiguration**.</span></span>
3. <span data-ttu-id="22a6b-183">Dans le panneau **Importer**, cliquez sur l’icône de dossier en regard de la zone de texte **Fichier de configuration de nœuds** pour rechercher un fichier de configuration de nœuds (MOF) sur votre ordinateur local.</span><span class="sxs-lookup"><span data-stu-id="22a6b-183">In the **Import** blade, click the folder icon next to the **Node Configuration File** textbox to browse for a node configuration file (MOF) on your local computer.</span></span>

    ![Rechercher un fichier local](./media/automation-dsc-compile/import-browse.png)
4. <span data-ttu-id="22a6b-185">Entrez un nom dans la zone de texte **Nom de la configuration**.</span><span class="sxs-lookup"><span data-stu-id="22a6b-185">Enter a name in the **Configuration Name** textbox.</span></span> <span data-ttu-id="22a6b-186">Ce nom doit correspondre au nom de la configuration à partir de laquelle la configuration de nœuds a été compilée.</span><span class="sxs-lookup"><span data-stu-id="22a6b-186">This name must match the name of the configuration from which the node configuration was compiled.</span></span>
5. <span data-ttu-id="22a6b-187">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="22a6b-187">Click **OK**.</span></span>

### <a name="importing-a-node-configuration-with-powershell"></a><span data-ttu-id="22a6b-188">Importation d’une configuration de nœuds avec PowerShell</span><span class="sxs-lookup"><span data-stu-id="22a6b-188">Importing a node configuration with PowerShell</span></span>

<span data-ttu-id="22a6b-189">Vous pouvez utiliser l’applet de commande [Import-AzureRmAutomationDscNodeConfiguration](/powershell/module/azurerm.automation/import-azurermautomationdscnodeconfiguration) pour importer une configuration de nœuds dans votre compte Automation.</span><span class="sxs-lookup"><span data-stu-id="22a6b-189">You can use the [Import-AzureRmAutomationDscNodeConfiguration](/powershell/module/azurerm.automation/import-azurermautomationdscnodeconfiguration) cmdlet to import a node configuration into your automation account.</span></span>

```powershell
Import-AzureRmAutomationDscNodeConfiguration -AutomationAccountName "MyAutomationAccount" -ResourceGroupName "MyResourceGroup" -ConfigurationName "MyNodeConfiguration" -Path "C:\MyConfigurations\TestVM1.mof"
```



