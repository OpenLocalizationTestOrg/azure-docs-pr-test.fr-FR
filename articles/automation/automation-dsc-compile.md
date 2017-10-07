---
title: configurations aaaCompiling dans Azure Automation DSC | Documents Microsoft
description: "Cet article décrit comment toocompile les configurations de Configuration d’état souhaité (DSC) pour Azure Automation."
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
ms.openlocfilehash: b195311318a2d7431c4d6b29f4b9a5f3a0a0a9a5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="compiling-configurations-in-azure-automation-dsc"></a><span data-ttu-id="8cd84-103">Compilation de configurations dans Azure Automation DSC</span><span class="sxs-lookup"><span data-stu-id="8cd84-103">Compiling configurations in Azure Automation DSC</span></span>

<span data-ttu-id="8cd84-104">Vous pouvez compiler des configurations de Configuration d’état souhaité (DSC) de deux manières avec Azure Automation : Bonjour portail Azure et avec Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="8cd84-104">You can compile Desired State Configuration (DSC) configurations in two ways with Azure Automation: in hello Azure portal, and with Windows PowerShell.</span></span> <span data-ttu-id="8cd84-105">Hello tableau suivant vous aide à déterminer quand toouse sur lequel la méthode en fonction des caractéristiques de hello de chacun :</span><span class="sxs-lookup"><span data-stu-id="8cd84-105">hello following table will help you determine when toouse which method based on hello characteristics of each:</span></span>

### <a name="azure-portal"></a><span data-ttu-id="8cd84-106">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="8cd84-106">Azure portal</span></span>

* <span data-ttu-id="8cd84-107">Méthode la plus simple avec une interface utilisateur interactive</span><span class="sxs-lookup"><span data-stu-id="8cd84-107">Simplest method with interactive user interface</span></span>
* <span data-ttu-id="8cd84-108">Valeurs de formulaire tooprovide paramètres simples.</span><span class="sxs-lookup"><span data-stu-id="8cd84-108">Form tooprovide simple parameter values</span></span>
* <span data-ttu-id="8cd84-109">Suivi aisé de l’état des tâches</span><span class="sxs-lookup"><span data-stu-id="8cd84-109">Easily track job state</span></span>
* <span data-ttu-id="8cd84-110">Accès authentifié avec ouverture de session Azure</span><span class="sxs-lookup"><span data-stu-id="8cd84-110">Access authenticated with Azure logon</span></span>

### <a name="windows-powershell"></a><span data-ttu-id="8cd84-111">Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="8cd84-111">Windows PowerShell</span></span>

* <span data-ttu-id="8cd84-112">Appel à partir de la ligne de commande avec les applets de commande Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="8cd84-112">Call from command line with Windows PowerShell cmdlets</span></span>
* <span data-ttu-id="8cd84-113">Possibilité d’inclusion dans une solution automatisée à plusieurs étapes</span><span class="sxs-lookup"><span data-stu-id="8cd84-113">Can be included in automated solution with multiple steps</span></span>
* <span data-ttu-id="8cd84-114">Fourniture de valeurs de paramètres simples et complexes</span><span class="sxs-lookup"><span data-stu-id="8cd84-114">Provide simple and complex parameter values</span></span>
* <span data-ttu-id="8cd84-115">Suivi de l’état des tâches</span><span class="sxs-lookup"><span data-stu-id="8cd84-115">Track job state</span></span>
* <span data-ttu-id="8cd84-116">Client requis toosupport applets de commande PowerShell</span><span class="sxs-lookup"><span data-stu-id="8cd84-116">Client required toosupport PowerShell cmdlets</span></span>
* <span data-ttu-id="8cd84-117">Transmission ConfigurationData</span><span class="sxs-lookup"><span data-stu-id="8cd84-117">Pass ConfigurationData</span></span>
* <span data-ttu-id="8cd84-118">Compilation de configurations utilisant des informations d’identification</span><span class="sxs-lookup"><span data-stu-id="8cd84-118">Compile configurations that use credentials</span></span>

<span data-ttu-id="8cd84-119">Une fois que vous avez choisi une méthode de compilation, vous pouvez suivre les procédures de respectifs de hello ci-dessous toostart la compilation.</span><span class="sxs-lookup"><span data-stu-id="8cd84-119">Once you have decided on a compilation method, you can follow hello respective procedures below toostart compiling.</span></span>

## <a name="compiling-a-dsc-configuration-with-hello-azure-portal"></a><span data-ttu-id="8cd84-120">La compilation d’une Configuration DSC avec hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="8cd84-120">Compiling a DSC Configuration with hello Azure portal</span></span>

1. <span data-ttu-id="8cd84-121">Dans votre compte Automation, cliquez sur **Configurations DSC**.</span><span class="sxs-lookup"><span data-stu-id="8cd84-121">From your Automation account, click **DSC Configurations**.</span></span>
2. <span data-ttu-id="8cd84-122">Cliquez sur une configuration tooopen son panneau.</span><span class="sxs-lookup"><span data-stu-id="8cd84-122">Click a configuration tooopen its blade.</span></span>
3. <span data-ttu-id="8cd84-123">Cliquez sur **Compiler**.</span><span class="sxs-lookup"><span data-stu-id="8cd84-123">Click **Compile**.</span></span>
4. <span data-ttu-id="8cd84-124">Si la configuration de hello n’a aucun paramètre, vous serez invité à tooconfirm si vous souhaitez toocompile il.</span><span class="sxs-lookup"><span data-stu-id="8cd84-124">If hello configuration has no parameters, you will be prompted tooconfirm whether you want toocompile it.</span></span> <span data-ttu-id="8cd84-125">Si la configuration de hello possède des paramètres, hello **compiler la Configuration** panneau afin de pouvoir fournir des valeurs de paramètre.</span><span class="sxs-lookup"><span data-stu-id="8cd84-125">If hello configuration has parameters, hello **Compile Configuration** blade will open so you can provide parameter values.</span></span> <span data-ttu-id="8cd84-126">Consultez hello [ **paramètres de base** ](#basic-parameters) section ci-dessous pour plus d’informations sur les paramètres.</span><span class="sxs-lookup"><span data-stu-id="8cd84-126">See hello [**Basic Parameters**](#basic-parameters) section below for further details on parameters.</span></span>
5. <span data-ttu-id="8cd84-127">Hello **tâche de Compilation** panneau est ouvert afin que vous pouvez suivre le statut de la tâche de compilation hello et hello configurations de nœuds (documents MOF de configuration) a provoqué toobe placé sur hello serveur d’extraction Azure Automation DSC.</span><span class="sxs-lookup"><span data-stu-id="8cd84-127">hello **Compilation Job** blade is opened so that you can track hello compilation job's status, and hello node configurations (MOF configuration documents) it caused toobe placed on hello Azure Automation DSC Pull Server.</span></span>

## <a name="compiling-a-dsc-configuration-with-windows-powershell"></a><span data-ttu-id="8cd84-128">Compilation d’une configuration DSC avec Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="8cd84-128">Compiling a DSC Configuration with Windows PowerShell</span></span>

<span data-ttu-id="8cd84-129">Vous pouvez utiliser [ `Start-AzureRmAutomationDscCompilationJob` ](/powershell/module/azurerm.automation/start-azurermautomationdsccompilationjob) toostart la compilation avec Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="8cd84-129">You can use [`Start-AzureRmAutomationDscCompilationJob`](/powershell/module/azurerm.automation/start-azurermautomationdsccompilationjob) toostart compiling with Windows PowerShell.</span></span> <span data-ttu-id="8cd84-130">Hello suivant l’exemple de code démarre la compilation d’une configuration DSC nommée **SampleConfig**.</span><span class="sxs-lookup"><span data-stu-id="8cd84-130">hello following sample code starts compilation of a DSC configuration called **SampleConfig**.</span></span>

```powershell
Start-AzureRmAutomationDscCompilationJob -ResourceGroupName "MyResourceGroup" -AutomationAccountName "MyAutomationAccount" -ConfigurationName "SampleConfig"
```

<span data-ttu-id="8cd84-131">`Start-AzureRmAutomationDscCompilationJob`objet que vous pouvez utiliser tootrack son état de la tâche retourne une compilation.</span><span class="sxs-lookup"><span data-stu-id="8cd84-131">`Start-AzureRmAutomationDscCompilationJob` returns a compilation job object that you can use tootrack its status.</span></span> <span data-ttu-id="8cd84-132">Vous pouvez ensuite utiliser cet objet de tâche de compilation avec [ `Get-AzureRmAutomationDscCompilationJob` ](/powershell/module/azurerm.automation/get-azurermautomationdsccompilationjob) état de hello toodetermine de la tâche de compilation hello, et [ `Get-AzureRmAutomationDscCompilationJobOutput` ](/powershell/module/azurerm.automation/get-azurermautomationdsccompilationjoboutput) tooview ses flux (sortie).</span><span class="sxs-lookup"><span data-stu-id="8cd84-132">You can then use this compilation job object with [`Get-AzureRmAutomationDscCompilationJob`](/powershell/module/azurerm.automation/get-azurermautomationdsccompilationjob) toodetermine hello status of hello compilation job, and [`Get-AzureRmAutomationDscCompilationJobOutput`](/powershell/module/azurerm.automation/get-azurermautomationdsccompilationjoboutput) tooview its streams (output).</span></span> <span data-ttu-id="8cd84-133">Hello suivant l’exemple de code démarre la compilation de hello **SampleConfig** configuration, attend qu’il a terminé, puis affiche son flux de données.</span><span class="sxs-lookup"><span data-stu-id="8cd84-133">hello following sample code starts compilation of hello **SampleConfig** configuration, waits until it has completed, and then displays its streams.</span></span>

```powershell
$CompilationJob = Start-AzureRmAutomationDscCompilationJob -ResourceGroupName "MyResourceGroup" -AutomationAccountName "MyAutomationAccount" -ConfigurationName "SampleConfig"

while($CompilationJob.EndTime –eq $null -and $CompilationJob.Exception –eq $null)
{
    $CompilationJob = $CompilationJob | Get-AzureRmAutomationDscCompilationJob
    Start-Sleep -Seconds 3
}

$CompilationJob | Get-AzureRmAutomationDscCompilationJobOutput –Stream Any
```

## <a name="basic-parameters"></a><span data-ttu-id="8cd84-134">Paramètres de base</span><span class="sxs-lookup"><span data-stu-id="8cd84-134">Basic Parameters</span></span>
<span data-ttu-id="8cd84-135">Déclaration de paramètre dans les configurations DSC, y compris les types de paramètres et les propriétés, fonctionne même hello comme dans les runbooks Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="8cd84-135">Parameter declaration in DSC configurations, including parameter types and properties, works hello same as in Azure Automation runbooks.</span></span> <span data-ttu-id="8cd84-136">Consultez [démarrage d’un runbook dans Azure Automation](automation-starting-a-runbook.md) toolearn plus d’informations sur les paramètres du runbook.</span><span class="sxs-lookup"><span data-stu-id="8cd84-136">See [Starting a runbook in Azure Automation](automation-starting-a-runbook.md) toolearn more about runbook parameters.</span></span>

<span data-ttu-id="8cd84-137">Hello exemple suivant utilise deux paramètres appelés **FeatureName** et **IsPresent**, toodetermine les valeurs de hello des propriétés dans hello **ParametersExample.sample** nœud configuration, générée pendant la compilation.</span><span class="sxs-lookup"><span data-stu-id="8cd84-137">hello following example uses two parameters called **FeatureName** and **IsPresent**, toodetermine hello values of properties in hello **ParametersExample.sample** node configuration, generated during compilation.</span></span>

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

<span data-ttu-id="8cd84-138">Vous pouvez compiler les Configurations DSC qui utilisent les paramètres de base dans le portail d’Azure Automation DSC hello, ou Azure PowerShell :</span><span class="sxs-lookup"><span data-stu-id="8cd84-138">You can compile DSC Configurations that use basic parameters in hello Azure Automation DSC portal, or with Azure PowerShell:</span></span>

### <a name="portal"></a><span data-ttu-id="8cd84-139">Portail</span><span class="sxs-lookup"><span data-stu-id="8cd84-139">Portal</span></span>

<span data-ttu-id="8cd84-140">Dans le portail hello, vous pouvez entrer des valeurs de paramètre après avoir cliqué sur **compiler**.</span><span class="sxs-lookup"><span data-stu-id="8cd84-140">In hello portal, you can enter parameter values after clicking **Compile**.</span></span>

![alt text](./media/automation-dsc-compile/DSC_compiling_1.png)

### <a name="powershell"></a><span data-ttu-id="8cd84-142">PowerShell</span><span class="sxs-lookup"><span data-stu-id="8cd84-142">PowerShell</span></span>

<span data-ttu-id="8cd84-143">PowerShell requiert des paramètres dans un [hashtable](http://technet.microsoft.com/library/hh847780.aspx) clé de hello correspond au nom du paramètre hello, alors que la valeur du paramètre hello a la valeur hello.</span><span class="sxs-lookup"><span data-stu-id="8cd84-143">PowerShell requires parameters in a [hashtable](http://technet.microsoft.com/library/hh847780.aspx) where hello key matches hello parameter name, and hello value equals hello parameter value.</span></span>

```powershell
$Parameters = @{
    "FeatureName" = "Web-Server"
    "IsPresent" = $False
}

Start-AzureRmAutomationDscCompilationJob -ResourceGroupName "MyResourceGroup" -AutomationAccountName "MyAutomationAccount" -ConfigurationName "ParametersExample" -Parameters $Parameters
```

<span data-ttu-id="8cd84-144">Pour plus d’informations sur la transmission d’informations d’identification PowerShell en tant que paramètres, voir la section <a href="#credential-assets">**Ressources d’informations d’identification**</a> ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="8cd84-144">For information about passing PSCredentials as parameters, see <a href="#credential-assets">**Credential Assets**</a> below.</span></span>

## <a name="configurationdata"></a><span data-ttu-id="8cd84-145">ConfigurationData</span><span class="sxs-lookup"><span data-stu-id="8cd84-145">ConfigurationData</span></span>
<span data-ttu-id="8cd84-146">**ConfigurationData** vous permet de tooseparate la configuration structurelle à partir de n’importe quel configuration spécifique de l’environnement lors de l’utilisation de DSC PowerShell.</span><span class="sxs-lookup"><span data-stu-id="8cd84-146">**ConfigurationData** allows you tooseparate structural configuration from any environment specific configuration while using PowerShell DSC.</span></span> <span data-ttu-id="8cd84-147">Consultez [séparant « ce » qu’à partir de « Where » dans DSC PowerShell](http://blogs.msdn.com/b/powershell/archive/2014/01/09/continuous-deployment-using-dsc-with-minimal-change.aspx) toolearn plus **ConfigurationData**.</span><span class="sxs-lookup"><span data-stu-id="8cd84-147">See [Separating "What" from "Where" in PowerShell DSC](http://blogs.msdn.com/b/powershell/archive/2014/01/09/continuous-deployment-using-dsc-with-minimal-change.aspx) toolearn more about **ConfigurationData**.</span></span>

> [!NOTE]
> <span data-ttu-id="8cd84-148">Vous pouvez utiliser **ConfigurationData** lors de la compilation dans Azure Automation DSC à l’aide d’Azure PowerShell, mais pas dans hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="8cd84-148">You can use **ConfigurationData** when compiling in Azure Automation DSC using Azure PowerShell, but not in hello Azure portal.</span></span>

<span data-ttu-id="8cd84-149">Hello DSC configuration suivante utilise **ConfigurationData** via hello **$ConfigurationData** et **$AllNodes** mots clés.</span><span class="sxs-lookup"><span data-stu-id="8cd84-149">hello following example DSC configuration uses **ConfigurationData** via hello **$ConfigurationData** and **$AllNodes** keywords.</span></span> <span data-ttu-id="8cd84-150">Vous devez également hello [ **xWebAdministration** module](https://www.powershellgallery.com/packages/xWebAdministration/) pour cet exemple :</span><span class="sxs-lookup"><span data-stu-id="8cd84-150">You'll also need hello [**xWebAdministration** module](https://www.powershellgallery.com/packages/xWebAdministration/) for this example:</span></span>

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

<span data-ttu-id="8cd84-151">Vous pouvez compiler hello DSC la configuration ci-dessus avec PowerShell.</span><span class="sxs-lookup"><span data-stu-id="8cd84-151">You can compile hello DSC configuration above with PowerShell.</span></span> <span data-ttu-id="8cd84-152">Hello sous PowerShell ajoute deux toohello de configurations de nœud serveur de collecteur Azure Automation DSC : **ConfigurationDataSample.MyVM1** et **ConfigurationDataSample.MyVM3**:</span><span class="sxs-lookup"><span data-stu-id="8cd84-152">hello below PowerShell adds two node configurations toohello Azure Automation DSC Pull Server: **ConfigurationDataSample.MyVM1** and **ConfigurationDataSample.MyVM3**:</span></span>

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

## <a name="assets"></a><span data-ttu-id="8cd84-153">Éléments multimédias</span><span class="sxs-lookup"><span data-stu-id="8cd84-153">Assets</span></span>

<span data-ttu-id="8cd84-154">Références de l’élément multimédia sont hello même dans les runbooks et les configurations Azure Automation DSC.</span><span class="sxs-lookup"><span data-stu-id="8cd84-154">Asset references are hello same in Azure Automation DSC configurations and runbooks.</span></span> <span data-ttu-id="8cd84-155">Consultez les rubriques suivantes de hello pour plus d’informations :</span><span class="sxs-lookup"><span data-stu-id="8cd84-155">See hello following for more information:</span></span>

* [<span data-ttu-id="8cd84-156">Certificats</span><span class="sxs-lookup"><span data-stu-id="8cd84-156">Certificates</span></span>](automation-certificates.md)
* [<span data-ttu-id="8cd84-157">Connexions</span><span class="sxs-lookup"><span data-stu-id="8cd84-157">Connections</span></span>](automation-connections.md)
* [<span data-ttu-id="8cd84-158">Informations d'identification</span><span class="sxs-lookup"><span data-stu-id="8cd84-158">Credentials</span></span>](automation-credentials.md)
* [<span data-ttu-id="8cd84-159">Variables</span><span class="sxs-lookup"><span data-stu-id="8cd84-159">Variables</span></span>](automation-variables.md)

### <a name="credential-assets"></a><span data-ttu-id="8cd84-160">Ressources d’informations d’identification</span><span class="sxs-lookup"><span data-stu-id="8cd84-160">Credential Assets</span></span>

<span data-ttu-id="8cd84-161">Bien que les configurations DSC dans Azure Automation puissent référencer des ressources d’informations d’identification en utilisant **Get-AzureRmAutomationCredential**, vous pouvez également transmettre les ressources d’informations d’identification par le biais de paramètres si vous le souhaitez.</span><span class="sxs-lookup"><span data-stu-id="8cd84-161">While DSC configurations in Azure Automation can reference credential assets using **Get-AzureRmAutomationCredential**, credential assets can also be passed in via parameters, if desired.</span></span> <span data-ttu-id="8cd84-162">Si une configuration prend un paramètre de **PSCredential** de type, vous devez le nom de chaîne hello toopass d’une ressource d’informations d’identification Azure Automation en tant que valeur de ce paramètre, plutôt que sur un objet PSCredential.</span><span class="sxs-lookup"><span data-stu-id="8cd84-162">If a configuration takes a parameter of **PSCredential** type, then you need toopass hello string name of an Azure Automation credential asset as that parameter’s value, rather than a PSCredential object.</span></span> <span data-ttu-id="8cd84-163">Coulisses de hello, ressource d’informations d’identification Azure Automation hello portant ce nom sera récupéré et passé toohello configuration.</span><span class="sxs-lookup"><span data-stu-id="8cd84-163">Behind hello scenes, hello Azure Automation credential asset with that name will be retrieved and passed toohello configuration.</span></span>

<span data-ttu-id="8cd84-164">Conservation des informations d’identification sécurisé dans les configurations de nœuds (documents MOF de configuration) nécessite le chiffrement des informations d’identification hello dans le fichier MOF de configuration de nœud hello.</span><span class="sxs-lookup"><span data-stu-id="8cd84-164">Keeping credentials secure in node configurations (MOF configuration documents) requires encrypting hello credentials in hello node configuration MOF file.</span></span> <span data-ttu-id="8cd84-165">Azure Automation est une étape supplémentaire et chiffre la totalité du fichier MOF hello.</span><span class="sxs-lookup"><span data-stu-id="8cd84-165">Azure Automation takes this one step further and encrypts hello entire MOF file.</span></span> <span data-ttu-id="8cd84-166">Toutefois, actuellement vous devez indiquer à DSC PowerShell c’est OK pour toobe des informations d’identification envoyée en texte brut pendant la génération de fichier MOF de configuration de nœud, parce que PowerShell DSC ne sait pas que les Azure Automation sera chiffrer le fichier MOF entière hello après son génération par une tâche de compilation.</span><span class="sxs-lookup"><span data-stu-id="8cd84-166">However, currently you must tell PowerShell DSC it is okay for credentials toobe outputted in plain text during node configuration MOF generation, because PowerShell DSC doesn’t know that Azure Automation will be encrypting hello entire MOF file after its generation via a compilation job.</span></span>

<span data-ttu-id="8cd84-167">Vous pouvez indiquer à DSC PowerShell qu’il est OK pour toobe des informations d’identification envoyée en texte brut dans la configuration du nœud hello généré MOF à l’aide de [ **ConfigurationData**](#configurationdata).</span><span class="sxs-lookup"><span data-stu-id="8cd84-167">You can tell PowerShell DSC that it is okay for credentials toobe outputted in plain text in hello generated node configuration MOFs using [**ConfigurationData**](#configurationdata).</span></span> <span data-ttu-id="8cd84-168">Vous devez passer `PSDscAllowPlainTextPassword = $true` via **ConfigurationData** pour le nom du chaque bloc nœud qui s’affiche dans la configuration de hello DSC et utilise les informations d’identification.</span><span class="sxs-lookup"><span data-stu-id="8cd84-168">You should pass `PSDscAllowPlainTextPassword = $true` via **ConfigurationData** for each node block’s name that appears in hello DSC configuration and uses credentials.</span></span>

<span data-ttu-id="8cd84-169">Hello suivant montre une configuration DSC qui utilise une ressource d’informations d’identification Automation.</span><span class="sxs-lookup"><span data-stu-id="8cd84-169">hello following example shows a DSC configuration that uses an Automation credential asset.</span></span>

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

<span data-ttu-id="8cd84-170">Vous pouvez compiler hello DSC la configuration ci-dessus avec PowerShell.</span><span class="sxs-lookup"><span data-stu-id="8cd84-170">You can compile hello DSC configuration above with PowerShell.</span></span> <span data-ttu-id="8cd84-171">Hello sous PowerShell ajoute deux toohello de configurations de nœud serveur de collecteur Azure Automation DSC : **CredentialSample.MyVM1** et **CredentialSample.MyVM2**.</span><span class="sxs-lookup"><span data-stu-id="8cd84-171">hello below PowerShell adds two node configurations toohello Azure Automation DSC Pull Server:  **CredentialSample.MyVM1** and **CredentialSample.MyVM2**.</span></span>

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

## <a name="importing-node-configurations"></a><span data-ttu-id="8cd84-172">Importation de configurations de nœuds</span><span class="sxs-lookup"><span data-stu-id="8cd84-172">Importing node configurations</span></span>

<span data-ttu-id="8cd84-173">Vous pouvez également importer des configurations de nœuds (MOF) que vous avez compilées en dehors d’Azure.</span><span class="sxs-lookup"><span data-stu-id="8cd84-173">You can also import node configuratons (MOFs) that you have compiled outside of Azure.</span></span> <span data-ttu-id="8cd84-174">Cette configuration de nœuds offre l’avantage de pouvoir être signée.</span><span class="sxs-lookup"><span data-stu-id="8cd84-174">One advantage of this is that node confiturations can be signed.</span></span>
<span data-ttu-id="8cd84-175">Une configuration de nœud signé est vérifiée localement sur un nœud géré par agent hello DSC, de s’assurer que la configuration hello étant appliqués toohello nœud proviennent d’une source autorisée.</span><span class="sxs-lookup"><span data-stu-id="8cd84-175">A signed node configuration is verified locally on a managed node by hello DSC agent, ensuring that hello configuration being applied toohello node comes from an authorized source.</span></span>

> [!NOTE]
> <span data-ttu-id="8cd84-176">Vous pouvez importer des configurations signées dans votre compte Azure Automation, mais Azure Automation ne prend pas en charge la compilation de configurations signées.</span><span class="sxs-lookup"><span data-stu-id="8cd84-176">You can use import signed configurations into your Azure Automation account, but Azure Automation does not currently support compiling signed configurations.</span></span>

> [!NOTE]
> <span data-ttu-id="8cd84-177">Un fichier de configuration de nœud doit pas être supérieur à 1 Mo tooallow il toobe importé dans Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="8cd84-177">A node configuration file must be no larger than 1 MB tooallow it toobe imported into Azure Automation.</span></span>

<span data-ttu-id="8cd84-178">Vous pouvez apprendre comment toosign des configurations de nœuds à https://msdn.microsoft.com/en-us/powershell/wmf/5.1/dsc-improvements#how-to-sign-configuration-and-module.</span><span class="sxs-lookup"><span data-stu-id="8cd84-178">You can learn how toosign node configurations at https://msdn.microsoft.com/en-us/powershell/wmf/5.1/dsc-improvements#how-to-sign-configuration-and-module.</span></span>

### <a name="importing-a-node-configuration-in-hello-azure-portal"></a><span data-ttu-id="8cd84-179">Importation d’une configuration de nœud Bonjour portail Azure</span><span class="sxs-lookup"><span data-stu-id="8cd84-179">Importing a node configuration in hello Azure portal</span></span>

1. <span data-ttu-id="8cd84-180">Dans votre compte Automation, cliquez sur **Configurations de nœuds DSC**.</span><span class="sxs-lookup"><span data-stu-id="8cd84-180">From your Automation account, click **DSC node configurations**.</span></span>

    ![Configurations de nœuds DSC](./media/automation-dsc-compile/node-config.png)
2. <span data-ttu-id="8cd84-182">Bonjour **configurations de nœuds DSC** panneau, cliquez sur **ajouter une NodeConfiguration**.</span><span class="sxs-lookup"><span data-stu-id="8cd84-182">In hello **DSC node configurations** blade, click **Add a NodeConfiguration**.</span></span>
3. <span data-ttu-id="8cd84-183">Bonjour **importation** panneau, cliquez sur hello dossier icône suivant toohello **fichier de Configuration de nœud** toobrowse de zone de texte d’un fichier de configuration de nœud (MOF) sur votre ordinateur local.</span><span class="sxs-lookup"><span data-stu-id="8cd84-183">In hello **Import** blade, click hello folder icon next toohello **Node Configuration File** textbox toobrowse for a node configuration file (MOF) on your local computer.</span></span>

    ![Rechercher un fichier local](./media/automation-dsc-compile/import-browse.png)
4. <span data-ttu-id="8cd84-185">Entrez un nom dans hello **nom de la Configuration** zone de texte.</span><span class="sxs-lookup"><span data-stu-id="8cd84-185">Enter a name in hello **Configuration Name** textbox.</span></span> <span data-ttu-id="8cd84-186">Ce nom doit correspondre au nom hello de configuration hello à partir de laquelle la configuration du nœud hello a été compilée.</span><span class="sxs-lookup"><span data-stu-id="8cd84-186">This name must match hello name of hello configuration from which hello node configuration was compiled.</span></span>
5. <span data-ttu-id="8cd84-187">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="8cd84-187">Click **OK**.</span></span>

### <a name="importing-a-node-configuration-with-powershell"></a><span data-ttu-id="8cd84-188">Importation d’une configuration de nœuds avec PowerShell</span><span class="sxs-lookup"><span data-stu-id="8cd84-188">Importing a node configuration with PowerShell</span></span>

<span data-ttu-id="8cd84-189">Vous pouvez utiliser hello [Import-AzureRmAutomationDscNodeConfiguration](/powershell/module/azurerm.automation/import-azurermautomationdscnodeconfiguration) tooimport de l’applet de commande une configuration de nœud dans votre compte automation.</span><span class="sxs-lookup"><span data-stu-id="8cd84-189">You can use hello [Import-AzureRmAutomationDscNodeConfiguration](/powershell/module/azurerm.automation/import-azurermautomationdscnodeconfiguration) cmdlet tooimport a node configuration into your automation account.</span></span>

```powershell
Import-AzureRmAutomationDscNodeConfiguration -AutomationAccountName "MyAutomationAccount" -ResourceGroupName "MyResourceGroup" -ConfigurationName "MyNodeConfiguration" -Path "C:\MyConfigurations\TestVM1.mof"
```



