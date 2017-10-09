---
title: ordinateurs aaaOnboarding pour la gestion par Azure Automation DSC | Documents Microsoft
description: Comment toosetup machines pour la gestion avec Azure Automation DSC
services: automation
documentationcenter: dev-center-name
author: eslesar
manager: carmonm
ms.assetid: da13e1f5-2a1c-443b-8e3b-9f0d6f9e4810
ms.service: automation
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: powershell
ms.workload: TBD
ms.date: 12/13/2016
ms.author: eslesar
ms.openlocfilehash: ef15801fec2ffea4ba62dcba2fbe9af09268e424
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="onboarding-machines-for-management-by-azure-automation-dsc"></a><span data-ttu-id="dc09c-103">Gestion de machines avec Azure Automation DSC</span><span class="sxs-lookup"><span data-stu-id="dc09c-103">Onboarding machines for management by Azure Automation DSC</span></span>

## <a name="why-manage-machines-with-azure-automation-dsc"></a><span data-ttu-id="dc09c-104">Pourquoi gérer des machines avec Azure Automation DSC ?</span><span class="sxs-lookup"><span data-stu-id="dc09c-104">Why manage machines with Azure Automation DSC?</span></span>

<span data-ttu-id="dc09c-105">Tout comme le service [Desired State Configuration de PowerShell](https://technet.microsoft.com/library/dn249912.aspx), le Desired State Configuration d’Azure Automation est un service de gestion de configuration simple et puissant pour les nœuds DSC (machines physiques et virtuelles) dans n’importe quel centre de données sur le cloud ou sur site.</span><span class="sxs-lookup"><span data-stu-id="dc09c-105">Like [PowerShell Desired State Configuration](https://technet.microsoft.com/library/dn249912.aspx), Azure Automation Desired State Configuration is a simple, yet powerful, configuration management service for DSC nodes (physical and virtual machines) in any cloud or on-premises datacenter.</span></span> <span data-ttu-id="dc09c-106">Il permet de faire évoluer des milliers d’ordinateurs rapidement et facilement à partir d’un emplacement central et sécurisé.</span><span class="sxs-lookup"><span data-stu-id="dc09c-106">It enables scalability across thousands of machines quickly and easily from a central, secure location.</span></span> <span data-ttu-id="dc09c-107">Vous pouvez facilement intégrer machines, affecter les configurations déclaratives et afficher des rapports affichant chaque ordinateur de l’état toohello souhaité de compatibilité spécifié.</span><span class="sxs-lookup"><span data-stu-id="dc09c-107">You can easily onboard machines, assign them declarative configurations, and view reports showing each machine's compliance toohello desired state you specified.</span></span> <span data-ttu-id="dc09c-108">couche de gestion Azure Automation DSC Hello est tooDSC quel couche de gestion Azure Automation hello est tooPowerShell écriture de scripts.</span><span class="sxs-lookup"><span data-stu-id="dc09c-108">hello Azure Automation DSC management layer is tooDSC what hello Azure Automation management layer is tooPowerShell scripting.</span></span> <span data-ttu-id="dc09c-109">En d’autres termes, Bonjour comme Azure Automation vous permet de gérer des scripts PowerShell, il vous permet également de gérer les configurations DSC.</span><span class="sxs-lookup"><span data-stu-id="dc09c-109">In other words, in hello same way that Azure Automation helps you manage PowerShell scripts, it also helps you manage DSC configurations.</span></span> <span data-ttu-id="dc09c-110">toolearn en savoir plus sur les avantages de hello de l’utilisation d’Azure Automation DSC, consultez [vue d’ensemble d’Azure Automation DSC](automation-dsc-overview.md).</span><span class="sxs-lookup"><span data-stu-id="dc09c-110">toolearn more about hello benefits of using Azure Automation DSC, see [Azure Automation DSC overview](automation-dsc-overview.md).</span></span>

<span data-ttu-id="dc09c-111">Azure Automation DSC peut être utilisé toomanage différents ordinateurs :</span><span class="sxs-lookup"><span data-stu-id="dc09c-111">Azure Automation DSC can be used toomanage a variety of machines:</span></span>

* <span data-ttu-id="dc09c-112">Machines virtuelles Azure (classiques)</span><span class="sxs-lookup"><span data-stu-id="dc09c-112">Azure virtual machines (classic)</span></span>
* <span data-ttu-id="dc09c-113">Machines virtuelles Azure</span><span class="sxs-lookup"><span data-stu-id="dc09c-113">Azure virtual machines</span></span>
* <span data-ttu-id="dc09c-114">Machines virtuelles Amazon Web Services (AWS)</span><span class="sxs-lookup"><span data-stu-id="dc09c-114">Amazon Web Services (AWS) virtual machines</span></span>
* <span data-ttu-id="dc09c-115">Machines physiques/virtuelles Windows locales ou dans un cloud autre qu’Azure/AWS</span><span class="sxs-lookup"><span data-stu-id="dc09c-115">Physical/virtual Windows machines on-premises, or in a cloud other than Azure/AWS</span></span>
* <span data-ttu-id="dc09c-116">Machines physiques/virtuelles Linux sur site, dans Azure, ou dans un cloud autre qu’Azure</span><span class="sxs-lookup"><span data-stu-id="dc09c-116">Physical/virtual Linux machines on-premises, in Azure, or in a cloud other than Azure</span></span>

<span data-ttu-id="dc09c-117">En outre, si vous n’êtes pas prêt toomanage configuration de l’ordinateur à partir du cloud de hello, Azure Automation DSC peut également servir comme un point de terminaison de rapport uniquement.</span><span class="sxs-lookup"><span data-stu-id="dc09c-117">In addition, if you are not ready toomanage machine configuration from hello cloud, Azure Automation DSC can also be used as a report-only endpoint.</span></span> <span data-ttu-id="dc09c-118">Cela vous permet de configuration souhaitée de tooset (push) via DSC sur site et afficher les détails rapports riches sur la conformité du nœud avec hello souhaité état dans Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="dc09c-118">This allows you tooset (push) desired configuration through DSC on-premises and view rich reporting details on node compliance with hello desired state in Azure Automation.</span></span>

<span data-ttu-id="dc09c-119">Hello les sections suivantes décrire comment vous pouvez l’intégrer chaque type d’ordinateur tooAzure Automation DSC.</span><span class="sxs-lookup"><span data-stu-id="dc09c-119">hello following sections outline how you can onboard each type of machine tooAzure Automation DSC.</span></span>

## <a name="azure-virtual-machines-classic"></a><span data-ttu-id="dc09c-120">Machines virtuelles Azure (classiques)</span><span class="sxs-lookup"><span data-stu-id="dc09c-120">Azure virtual machines (classic)</span></span>

<span data-ttu-id="dc09c-121">Dans Azure Automation DSC, vous pouvez facilement intégrer des machines virtuelles Azure (classique) pour la gestion de la configuration à l’aide de hello portail Azure ou PowerShell.</span><span class="sxs-lookup"><span data-stu-id="dc09c-121">With Azure Automation DSC, you can easily onboard Azure virtual machines (classic) for configuration management using either hello Azure portal, or PowerShell.</span></span> <span data-ttu-id="dc09c-122">Dans les coulisses de hello et sans un administrateur ayant tooremote dans hello VM, hello extension de Configuration d’état souhaité Azure VM inscrit hello machine virtuelle dans Azure Automation DSC.</span><span class="sxs-lookup"><span data-stu-id="dc09c-122">Under hello hood, and without an administrator having tooremote into hello VM, hello Azure VM Desired State Configuration extension registers hello VM with Azure Automation DSC.</span></span> <span data-ttu-id="dc09c-123">Étant donné que hello extension de Configuration d’état souhaité Azure VM s’exécute de façon asynchrone, étapes tootrack sa progression ou de dépanner il sont fournies dans hello [ **l’intégration de machine virtuelle Azure de dépannage** ](#troubleshooting-azure-virtual-machine-onboarding)section ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="dc09c-123">Since hello Azure VM Desired State Configuration extension runs asynchronously, steps tootrack its progress or troubleshoot it are provided in hello [**Troubleshooting Azure virtual machine onboarding**](#troubleshooting-azure-virtual-machine-onboarding) section below.</span></span>

### <a name="azure-portal"></a><span data-ttu-id="dc09c-124">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="dc09c-124">Azure portal</span></span>

<span data-ttu-id="dc09c-125">Bonjour [portail Azure](http://portal.azure.com/), cliquez sur **Parcourir** -> **machines virtuelles (classiques)**.</span><span class="sxs-lookup"><span data-stu-id="dc09c-125">In hello [Azure portal](http://portal.azure.com/), click **Browse** -> **Virtual machines (classic)**.</span></span> <span data-ttu-id="dc09c-126">Sélectionnez hello Windows machine virtuelle tooonboard.</span><span class="sxs-lookup"><span data-stu-id="dc09c-126">Select hello Windows VM you want tooonboard.</span></span> <span data-ttu-id="dc09c-127">Dans le panneau de tableau de bord de l’ordinateur virtuel de hello, cliquez sur **tous les paramètres** -> **Extensions** -> **ajouter**  ->   **Azure Automation DSC** -> **créer**.</span><span class="sxs-lookup"><span data-stu-id="dc09c-127">On hello virtual machine's dashboard blade, click **All settings** -> **Extensions** -> **Add** -> **Azure Automation DSC** -> **Create**.</span></span> <span data-ttu-id="dc09c-128">Entrez hello [les valeurs de gestionnaire de Configuration Local DSC PowerShell](https://msdn.microsoft.com/powershell/dsc/metaconfig4) requis pour votre cas d’usage, clé d’inscription de votre compte Automation et URL d’inscription et éventuellement un toohello de tooassign de configuration de nœud machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="dc09c-128">Enter hello [PowerShell DSC Local Configuration Manager values](https://msdn.microsoft.com/powershell/dsc/metaconfig4) required for your use case, your Automation account's registration key and registration URL, and optionally a node configuration tooassign toohello VM.</span></span>

![](./media/automation-dsc-onboarding/DSC_Onboarding_1.png)

<span data-ttu-id="dc09c-129">URL d’inscription toofind hello et de clé pour la machine de hello hello Automation compte tooonboard, consultez hello [ **sécuriser l’inscription** ](#secure-registration) section ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="dc09c-129">toofind hello registration URL and key for hello Automation account tooonboard hello machine to, see hello [**Secure registration**](#secure-registration) section below.</span></span>

### <a name="powershell"></a><span data-ttu-id="dc09c-130">PowerShell</span><span class="sxs-lookup"><span data-stu-id="dc09c-130">PowerShell</span></span>

```powershell
# log in tooboth Azure Service Management and Azure Resource Manager
Add-AzureAccount
Add-AzureRmAccount

# fill in correct values for your VM/Automation account here
$VMName = ""
$ServiceName = ""
$AutomationAccountName = ""
$AutomationAccountResourceGroup = ""

# fill in hello name of a Node Configuration in Azure Automation DSC, for this VM tooconform to
$NodeConfigName = ""

# get Azure Automation DSC registration info
$Account = Get-AzureRmAutomationAccount -ResourceGroupName $AutomationAccountResourceGroup -Name $AutomationAccountName
$RegistrationInfo = $Account | Get-AzureRmAutomationRegistrationInfo

# use hello DSC extension tooonboard hello VM for management with Azure Automation DSC
$VM = Get-AzureVM -Name $VMName -ServiceName $ServiceName

$PublicConfiguration = ConvertTo-Json -Depth 8 @{
    SasToken = ""
    ModulesUrl = "https://eus2oaasibizamarketprod1.blob.core.windows.net/automationdscpreview/RegistrationMetaConfigV2.zip"
    ConfigurationFunction = "RegistrationMetaConfigV2.ps1\RegistrationMetaConfigV2"

# update these PowerShell DSC Local Configuration Manager defaults if they do not match your use case.
# See https://technet.microsoft.com/library/dn249922.aspx?f=255&MSPPError=-2147217396 for more details
    Properties = @{
    RegistrationKey = @{
        UserName = 'notused'
        Password = 'PrivateSettingsRef:RegistrationKey'
    }
    RegistrationUrl = $RegistrationInfo.Endpoint
    NodeConfigurationName = $NodeConfigName
    ConfigurationMode = "ApplyAndMonitor"
    ConfigurationModeFrequencyMins = 15
    RefreshFrequencyMins = 30
    RebootNodeIfNeeded = $False
    ActionAfterReboot = "ContinueConfiguration"
    AllowModuleOverwrite = $False
    }
}

$PrivateConfiguration = ConvertTo-Json -Depth 8 @{
    Items = @{
        RegistrationKey = $RegistrationInfo.PrimaryKey
    }
}

$VM = Set-AzureVMExtension `
    -VM $vm `
    -Publisher Microsoft.Powershell `
    -ExtensionName DSC `
    -Version 2.19 `
    -PublicConfiguration $PublicConfiguration `
    -PrivateConfiguration $PrivateConfiguration `
    -ForceUpdate

$VM | Update-AzureVM
```

## <a name="azure-virtual-machines"></a><span data-ttu-id="dc09c-131">Machines virtuelles Azure</span><span class="sxs-lookup"><span data-stu-id="dc09c-131">Azure virtual machines</span></span>

<span data-ttu-id="dc09c-132">Azure Automation DSC vous permet de s’intégrer facilement des machines virtuelles Azure pour la gestion de la configuration à l’aide de hello portail Azure, de modèles Azure Resource Manager ou de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="dc09c-132">Azure Automation DSC lets you easily onboard Azure virtual machines for configuration management, using either hello Azure portal, Azure Resource Manager templates, or PowerShell.</span></span> <span data-ttu-id="dc09c-133">Dans les coulisses de hello et sans un administrateur ayant tooremote dans hello VM, hello extension de Configuration d’état souhaité Azure VM inscrit hello machine virtuelle dans Azure Automation DSC.</span><span class="sxs-lookup"><span data-stu-id="dc09c-133">Under hello hood, and without an administrator having tooremote into hello VM, hello Azure VM Desired State Configuration extension registers hello VM with Azure Automation DSC.</span></span> <span data-ttu-id="dc09c-134">Étant donné que hello extension de Configuration d’état souhaité Azure VM s’exécute de façon asynchrone, étapes tootrack sa progression ou de dépanner il sont fournies dans hello [ **l’intégration de machine virtuelle Azure de dépannage** ](#troubleshooting-azure-virtual-machine-onboarding)section ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="dc09c-134">Since hello Azure VM Desired State Configuration extension runs asynchronously, steps tootrack its progress or troubleshoot it are provided in hello [**Troubleshooting Azure virtual machine onboarding**](#troubleshooting-azure-virtual-machine-onboarding) section below.</span></span>

### <a name="azure-portal"></a><span data-ttu-id="dc09c-135">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="dc09c-135">Azure portal</span></span>

<span data-ttu-id="dc09c-136">Bonjour [portail Azure](https://portal.azure.com/), accédez compte Azure Automation de toohello où vous souhaitez tooonboard virtual machines.</span><span class="sxs-lookup"><span data-stu-id="dc09c-136">In hello [Azure portal](https://portal.azure.com/), navigate toohello Azure Automation account where you want tooonboard virtual machines.</span></span> <span data-ttu-id="dc09c-137">Tableau de bord de compte Automation hello, cliquez sur **nœuds DSC** -> **ajouter Azure VM**.</span><span class="sxs-lookup"><span data-stu-id="dc09c-137">On hello Automation account dashboard, click **DSC Nodes** -> **Add Azure VM**.</span></span>

<span data-ttu-id="dc09c-138">Sous **sélectionner des machines virtuelles tooonboard**, sélectionnez un ou plusieurs Azure virtual machines tooonboard.</span><span class="sxs-lookup"><span data-stu-id="dc09c-138">Under **Select virtual machines tooonboard**, select one or more Azure virtual machines tooonboard.</span></span>

![](./media/automation-dsc-onboarding/DSC_Onboarding_2.png)

<span data-ttu-id="dc09c-139">Sous **configurer les données d’inscription**, entrez hello [les valeurs de gestionnaire de Configuration Local DSC PowerShell](https://msdn.microsoft.com/powershell/dsc/metaconfig4) requis pour votre cas d’usage et éventuellement un toohello de tooassign de configuration de nœud machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="dc09c-139">Under **Configure registration data**, enter hello [PowerShell DSC Local Configuration Manager values](https://msdn.microsoft.com/powershell/dsc/metaconfig4) required for your use case, and optionally a node configuration tooassign toohello VM.</span></span>

![](./media/automation-dsc-onboarding/DSC_Onboarding_3.png)

### <a name="azure-resource-manager-templates"></a><span data-ttu-id="dc09c-140">Modèles Microsoft Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="dc09c-140">Azure Resource Manager templates</span></span>

<span data-ttu-id="dc09c-141">Machines virtuelles peuvent être déployés et embarquées tooAzure Automation DSC via des modèles Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="dc09c-141">Azure virtual machines can be deployed and onboarded tooAzure Automation DSC via Azure Resource Manager templates.</span></span> <span data-ttu-id="dc09c-142">Consultez [configurer une machine virtuelle via l’extension DSC et Azure Automation DSC](https://azure.microsoft.com/documentation/templates/dsc-extension-azure-automation-pullserver/) pour un exemple de modèle qui onboards un tooAzure existant de la machine virtuelle Automation DSC.</span><span class="sxs-lookup"><span data-stu-id="dc09c-142">See [Configure a VM via DSC extension and Azure Automation DSC](https://azure.microsoft.com/documentation/templates/dsc-extension-azure-automation-pullserver/) for an example template that onboards an existing VM tooAzure Automation DSC.</span></span> <span data-ttu-id="dc09c-143">toofind hello URL d’enregistrement clé et l’inscription effectuée en tant qu’entrée dans ce modèle, consultez hello [ **sécuriser l’inscription** ](#secure-registration) section ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="dc09c-143">toofind hello registration key and registration URL taken as input in this template, see hello [**Secure registration**](#secure-registration) section below.</span></span>

### <a name="powershell"></a><span data-ttu-id="dc09c-144">PowerShell</span><span class="sxs-lookup"><span data-stu-id="dc09c-144">PowerShell</span></span>

<span data-ttu-id="dc09c-145">Hello [Register-AzureRmAutomationDscNode](/powershell/module/azurerm.automation/register-azurermautomationdscnode) applet de commande peut être des ordinateurs virtuels utilisés tooonboard hello portail Azure via PowerShell.</span><span class="sxs-lookup"><span data-stu-id="dc09c-145">hello [Register-AzureRmAutomationDscNode](/powershell/module/azurerm.automation/register-azurermautomationdscnode) cmdlet can be used tooonboard virtual machines in hello Azure portal via PowerShell.</span></span>

## <a name="amazon-web-services-aws-virtual-machines"></a><span data-ttu-id="dc09c-146">Machines virtuelles Amazon Web Services (AWS)</span><span class="sxs-lookup"><span data-stu-id="dc09c-146">Amazon Web Services (AWS) virtual machines</span></span>

<span data-ttu-id="dc09c-147">Vous pouvez facilement intégrer Amazon Web Services virtuels pour la gestion de la configuration par Azure Automation DSC à l’aide de hello AWS DSC Toolkit.</span><span class="sxs-lookup"><span data-stu-id="dc09c-147">You can easily onboard Amazon Web Services virtual machines for configuration management by Azure Automation DSC using hello AWS DSC Toolkit.</span></span> <span data-ttu-id="dc09c-148">Plus d’informations sur les outils d’analyse hello [ici](https://blogs.msdn.microsoft.com/powershell/2016/04/20/aws-dsc-toolkit/).</span><span class="sxs-lookup"><span data-stu-id="dc09c-148">You can learn more about hello toolkit [here](https://blogs.msdn.microsoft.com/powershell/2016/04/20/aws-dsc-toolkit/).</span></span>

## <a name="physicalvirtual-windows-machines-on-premises-or-in-a-cloud-other-than-azureaws"></a><span data-ttu-id="dc09c-149">Machines physiques/virtuelles Windows locales ou dans un cloud autre qu’Azure/AWS</span><span class="sxs-lookup"><span data-stu-id="dc09c-149">Physical/virtual Windows machines on-premises, or in a cloud other than Azure/AWS</span></span>

<span data-ttu-id="dc09c-150">Les ordinateurs Windows local et des ordinateurs Windows dans les clouds non-Azure (par exemple, Amazon Web Services) peuvent également être embarquées tooAzure Automation DSC, tant qu’ils ont un accès sortant toohello internet, via les quelques étapes simples :</span><span class="sxs-lookup"><span data-stu-id="dc09c-150">On-premises Windows machines and Windows machines in non-Azure clouds (such as Amazon Web Services) can also be onboarded tooAzure Automation DSC, as long as they have outbound access toohello internet, via a few simple steps:</span></span>

1. <span data-ttu-id="dc09c-151">Vérifiez que hello dernière version de [WMF 5](http://aka.ms/wmf5latest) est installé sur les ordinateurs hello souhaité tooonboard tooAzure Automation DSC.</span><span class="sxs-lookup"><span data-stu-id="dc09c-151">Make sure hello latest version of [WMF 5](http://aka.ms/wmf5latest) is installed on hello machines you want tooonboard tooAzure Automation DSC.</span></span>
2. <span data-ttu-id="dc09c-152">Suivez les instructions de hello de section [ **DSC de génération de métaconfigurations** ](#generating-dsc-metaconfigurations) ci-dessous toogenerate un dossier contenant hello nécessaire métaconfigurations de DSC.</span><span class="sxs-lookup"><span data-stu-id="dc09c-152">Follow hello directions in section [**Generating DSC metaconfigurations**](#generating-dsc-metaconfigurations) below toogenerate a folder containing hello needed DSC metaconfigurations.</span></span>
3. <span data-ttu-id="dc09c-153">À distance s’appliquent hello DSC PowerShell métaconfiguration toohello ordinateurs tooonboard.</span><span class="sxs-lookup"><span data-stu-id="dc09c-153">Remotely apply hello PowerShell DSC metaconfiguration toohello machines you want tooonboard.</span></span> <span data-ttu-id="dc09c-154">**ordinateur Hello cette commande est exécutée à partir de doit avoir la version la plus récente de hello [WMF 5](http://aka.ms/wmf5latest) installé**:</span><span class="sxs-lookup"><span data-stu-id="dc09c-154">**hello machine this command is run from must have hello latest version of [WMF 5](http://aka.ms/wmf5latest) installed**:</span></span>

    ```powershell
    Set-DscLocalConfigurationManager -Path C:\Users\joe\Desktop\DscMetaConfigs -ComputerName MyServer1, MyServer2
    ```

4. <span data-ttu-id="dc09c-155">Si vous ne pouvez pas appliquer hello DSC PowerShell métaconfigurations à distance, copiez le dossier de métaconfigurations de hello de l’étape 2 sur tooonboard de chaque ordinateur.</span><span class="sxs-lookup"><span data-stu-id="dc09c-155">If you cannot apply hello PowerShell DSC metaconfigurations remotely, copy hello metaconfigurations folder from step 2 onto each machine tooonboard.</span></span> <span data-ttu-id="dc09c-156">Appelez ensuite **Set-DscLocalConfigurationManager** localement sur chaque ordinateur tooonboard.</span><span class="sxs-lookup"><span data-stu-id="dc09c-156">Then call **Set-DscLocalConfigurationManager** locally on each machine tooonboard.</span></span>
5. <span data-ttu-id="dc09c-157">À l’aide de hello portail Azure ou des applets de commande, vérifiez que hello machines tooonboard maintenant s’affichent en tant que nœuds DSC inscrit dans votre compte Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="dc09c-157">Using hello Azure portal or cmdlets, check that hello machines tooonboard now show up as DSC nodes registered in your Azure Automation account.</span></span>

## <a name="physicalvirtual-linux-machines-on-premises-in-azure-or-in-a-cloud-other-than-azure"></a><span data-ttu-id="dc09c-158">Machines physiques/virtuelles Linux sur site, dans Azure, ou dans un cloud autre qu’Azure</span><span class="sxs-lookup"><span data-stu-id="dc09c-158">Physical/virtual Linux machines on-premises, in Azure, or in a cloud other than Azure</span></span>

<span data-ttu-id="dc09c-159">Les ordinateurs locaux Linux, les ordinateurs Linux dans Azure, et les ordinateurs Linux dans des clouds non-Azure peuvent également être embarquées tooAzure Automation DSC, tant qu’ils ont un accès sortant toohello internet, via les quelques étapes simples :</span><span class="sxs-lookup"><span data-stu-id="dc09c-159">On-premises Linux machines, Linux machines in Azure, and Linux machines in non-Azure clouds can also be onboarded tooAzure Automation DSC, as long as they have outbound access toohello internet, via a few simple steps:</span></span>

1. <span data-ttu-id="dc09c-160">Vérifiez que hello dernière version de [PowerShell DSC pour Linux](https://github.com/Microsoft/PowerShell-DSC-for-Linux) est installé sur les ordinateurs hello souhaité tooonboard tooAzure Automation DSC.</span><span class="sxs-lookup"><span data-stu-id="dc09c-160">Make sure hello latest version of [PowerShell Desired State Configuration for Linux](https://github.com/Microsoft/PowerShell-DSC-for-Linux) is installed on hello machines you want tooonboard tooAzure Automation DSC.</span></span>
2. <span data-ttu-id="dc09c-161">Si hello [valeurs par défaut du Gestionnaire de Configuration Local DSC PowerShell](https://msdn.microsoft.com/powershell/dsc/metaconfig4) correspond à votre cas d’usage, et que vous souhaitez tooonboard machines telles qu’elles **les deux** extraient et tooAzure Automation DSC de rapports :</span><span class="sxs-lookup"><span data-stu-id="dc09c-161">If hello [PowerShell DSC Local Configuration Manager defaults](https://msdn.microsoft.com/powershell/dsc/metaconfig4) match your use case, and you want tooonboard machines such that they **both** pull from and report tooAzure Automation DSC:</span></span>

   + <span data-ttu-id="dc09c-162">Sur chaque Linux ordinateur tooonboard tooAzure Automation DSC, utilisez tooonboard Register.py à l’aide de hello est par défaut du Gestionnaire de Configuration Local DSC PowerShell :</span><span class="sxs-lookup"><span data-stu-id="dc09c-162">On each Linux machine tooonboard tooAzure Automation DSC, use Register.py tooonboard using hello PowerShell DSC Local Configuration Manager defaults:</span></span>

     `/opt/microsoft/dsc/Scripts/Register.py <Automation account registration key> <Automation account registration URL>`

   + <span data-ttu-id="dc09c-163">toofind hello URL d’enregistrement clé et l’inscription de votre compte Automation, consultez hello [ **sécuriser l’inscription** ](#secure-registration) section ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="dc09c-163">toofind hello registration key and registration URL for your Automation account, see hello [**Secure registration**](#secure-registration) section below.</span></span>

     <span data-ttu-id="dc09c-164">Si hello Gestionnaire de Configuration Local DSC PowerShell par défaut **faire** **pas** correspond à votre cas d’usage ou si vous souhaitez tooonboard machines telles qu’elles uniquement de rapport tooAzure Automation DSC, mais ne tirez pas configuration ou des modules PowerShell à partir de celui-ci, suivez les étapes 3 à 6.</span><span class="sxs-lookup"><span data-stu-id="dc09c-164">If hello PowerShell DSC Local Configuration Manager defaults **do** **not** match your use case, or you want tooonboard machines such that they only report tooAzure Automation DSC, but do not pull configuration or PowerShell modules from it,  follow steps 3 - 6.</span></span> <span data-ttu-id="dc09c-165">Sinon, passez directement toostep 6.</span><span class="sxs-lookup"><span data-stu-id="dc09c-165">Otherwise, proceed directly toostep 6.</span></span>

3. <span data-ttu-id="dc09c-166">Suivez les instructions de hello Bonjour [ **DSC de génération de métaconfigurations** ](#generating-dsc-metaconfigurations) section ci-dessous toogenerate un dossier contenant des métaconfigurations de DSC hello si nécessaire.</span><span class="sxs-lookup"><span data-stu-id="dc09c-166">Follow hello directions in hello [**Generating DSC metaconfigurations**](#generating-dsc-metaconfigurations) section below toogenerate a folder containing hello needed DSC metaconfigurations.</span></span>
4. <span data-ttu-id="dc09c-167">À distance s’appliquent hello DSC PowerShell métaconfiguration toohello ordinateurs tooonboard :</span><span class="sxs-lookup"><span data-stu-id="dc09c-167">Remotely apply hello PowerShell DSC metaconfiguration toohello machines you want tooonboard:</span></span>

    ```powershell
    $SecurePass = ConvertTo-SecureString -String "<root password>" -AsPlainText -Force
    $Cred = New-Object System.Management.Automation.PSCredential "root", $SecurePass
    $Opt = New-CimSessionOption -UseSsl -SkipCACheck -SkipCNCheck -SkipRevocationCheck

    # need a CimSession for each Linux machine tooonboard

    $Session = New-CimSession -Credential $Cred -ComputerName <your Linux machine> -Port 5986 -Authentication basic -SessionOption $Opt

    Set-DscLocalConfigurationManager -CimSession $Session -Path C:\Users\joe\Desktop\DscMetaConfigs
    ```

<span data-ttu-id="dc09c-168">ordinateur Hello cette commande est exécutée à partir de doit avoir la version la plus récente de hello [WMF 5](http://aka.ms/wmf5latest) installé.</span><span class="sxs-lookup"><span data-stu-id="dc09c-168">hello machine this command is run from must have hello latest version of [WMF 5](http://aka.ms/wmf5latest) installed.</span></span>

1. <span data-ttu-id="dc09c-169">Si vous ne pouvez pas appliquer hello DSC PowerShell métaconfigurations à distance, pour chaque tooonboard ordinateur Linux, copiez machine toothat correspondante de hello métaconfiguration à partir du dossier à l’étape 5 sur l’ordinateur Linux de hello hello.</span><span class="sxs-lookup"><span data-stu-id="dc09c-169">If you cannot apply hello PowerShell DSC metaconfigurations remotely, for each Linux machine tooonboard, copy hello metaconfiguration corresponding toothat machine from hello folder in step 5 onto hello Linux machine.</span></span> <span data-ttu-id="dc09c-170">Appelez ensuite `SetDscLocalConfigurationManager.py` localement sur chaque ordinateur Linux, vous souhaitez tooonboard tooAzure Automation DSC :</span><span class="sxs-lookup"><span data-stu-id="dc09c-170">Then call `SetDscLocalConfigurationManager.py` locally on each Linux machine you want tooonboard tooAzure Automation DSC:</span></span>

   `/opt/microsoft/dsc/Scripts/SetDscLocalConfigurationManager.py -configurationmof <path toometaconfiguration file>`

2. <span data-ttu-id="dc09c-171">À l’aide de hello portail Azure ou des applets de commande, vérifiez que hello machines tooonboard maintenant s’affichent en tant que nœuds DSC inscrit dans votre compte Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="dc09c-171">Using hello Azure portal or cmdlets, check that hello machines tooonboard now show up as DSC nodes registered in your Azure Automation account.</span></span>

## <a name="generating-dsc-metaconfigurations"></a><span data-ttu-id="dc09c-172">Génération de métaconfigurations DSC</span><span class="sxs-lookup"><span data-stu-id="dc09c-172">Generating DSC metaconfigurations</span></span>

<span data-ttu-id="dc09c-173">toogenerically intégrer un ordinateur tooAzure Automation DSC, un [métaconfiguration DSC](https://msdn.microsoft.com/en-us/powershell/dsc/metaconfig) peut être générée qui, lorsque appliqué, indique à l’agent de hello DSC sur toopull d’ordinateur hello d’et/ou rapport tooAzure Automation DSC.</span><span class="sxs-lookup"><span data-stu-id="dc09c-173">toogenerically onboard any machine tooAzure Automation DSC, a [DSC metaconfiguration](https://msdn.microsoft.com/en-us/powershell/dsc/metaconfig) can be generated that, when applied, tells hello DSC agent on hello machine toopull from and/or report tooAzure Automation DSC.</span></span> <span data-ttu-id="dc09c-174">Métaconfigurations DSC Azure Automation DSC peuvent être générées à l’aide d’une configuration DSC de PowerShell, ou applets de commande PowerShell d’automatisation Azure hello.</span><span class="sxs-lookup"><span data-stu-id="dc09c-174">DSC metaconfigurations for Azure Automation DSC can be generated using either a PowerShell DSC configuration, or hello Azure Automation PowerShell cmdlets.</span></span>

> [!NOTE]
> <span data-ttu-id="dc09c-175">DSC métaconfigurations contient hello secrets nécessités tooonboard un tooan machine compte Automation pour la gestion.</span><span class="sxs-lookup"><span data-stu-id="dc09c-175">DSC metaconfigurations contain hello secrets needed tooonboard a machine tooan Automation account for management.</span></span> <span data-ttu-id="dc09c-176">Assurez-vous que tooproperly protéger n’importe quel métaconfigurations DSC que vous créez, ou les supprimer après utilisation.</span><span class="sxs-lookup"><span data-stu-id="dc09c-176">Make sure tooproperly protect any DSC metaconfigurations you create, or delete them after use.</span></span>

### <a name="using-a-dsc-configuration"></a><span data-ttu-id="dc09c-177">Utilisation d’une configuration DSC</span><span class="sxs-lookup"><span data-stu-id="dc09c-177">Using a DSC Configuration</span></span>

1. <span data-ttu-id="dc09c-178">Ouvrez hello PowerShell ISE en tant qu’administrateur sur un ordinateur dans votre environnement local.</span><span class="sxs-lookup"><span data-stu-id="dc09c-178">Open hello PowerShell ISE as an administrator in a machine in your local environment.</span></span> <span data-ttu-id="dc09c-179">machine de Hello doit avoir la version la plus récente de hello [WMF 5](http://aka.ms/wmf5latest) installé.</span><span class="sxs-lookup"><span data-stu-id="dc09c-179">hello machine must have hello latest version of [WMF 5](http://aka.ms/wmf5latest) installed.</span></span>
2. <span data-ttu-id="dc09c-180">Copiez hello localement le script suivant.</span><span class="sxs-lookup"><span data-stu-id="dc09c-180">Copy hello following script locally.</span></span> <span data-ttu-id="dc09c-181">Ce script contient une configuration DSC PowerShell pour la création de métaconfigurations et un tookick commande désactiver la création de métaconfiguration hello.</span><span class="sxs-lookup"><span data-stu-id="dc09c-181">This script contains a PowerShell DSC configuration for creating metaconfigurations, and a command tookick off hello metaconfiguration creation.</span></span>

    ```powershell
    # hello DSC configuration that will generate metaconfigurations
    [DscLocalConfigurationManager()]
    Configuration DscMetaConfigs
    {

        param
        (
            [Parameter(Mandatory=$True)]
            [String]$RegistrationUrl,

            [Parameter(Mandatory=$True)]
            [String]$RegistrationKey,

            [Parameter(Mandatory=$True)]
            [String[]]$ComputerName,

            [Int]$RefreshFrequencyMins = 30,

            [Int]$ConfigurationModeFrequencyMins = 15,

            [String]$ConfigurationMode = "ApplyAndMonitor",

            [String]$NodeConfigurationName,

            [Boolean]$RebootNodeIfNeeded= $False,

            [String]$ActionAfterReboot = "ContinueConfiguration",

            [Boolean]$AllowModuleOverwrite = $False,

            [Boolean]$ReportOnly
        )

        if(!$NodeConfigurationName -or $NodeConfigurationName -eq "")
        {
            $ConfigurationNames = $null
        }
        else
        {
            $ConfigurationNames = @($NodeConfigurationName)
        }

        if($ReportOnly)
        {
        $RefreshMode = "PUSH"
        }
        else
        {
        $RefreshMode = "PULL"
        }

        Node $ComputerName
        {

            Settings
            {
                RefreshFrequencyMins = $RefreshFrequencyMins
                RefreshMode = $RefreshMode
                ConfigurationMode = $ConfigurationMode
                AllowModuleOverwrite = $AllowModuleOverwrite
                RebootNodeIfNeeded = $RebootNodeIfNeeded
                ActionAfterReboot = $ActionAfterReboot
                ConfigurationModeFrequencyMins = $ConfigurationModeFrequencyMins
            }

            if(!$ReportOnly)
            {
            ConfigurationRepositoryWeb AzureAutomationDSC
                {
                    ServerUrl = $RegistrationUrl
                    RegistrationKey = $RegistrationKey
                    ConfigurationNames = $ConfigurationNames
                }

                ResourceRepositoryWeb AzureAutomationDSC
                {
                ServerUrl = $RegistrationUrl
                RegistrationKey = $RegistrationKey
                }
            }

            ReportServerWeb AzureAutomationDSC
            {
                ServerUrl = $RegistrationUrl
                RegistrationKey = $RegistrationKey
            }
        }
    }

    # Create hello metaconfigurations
    # TODO: edit hello below as needed for your use case
    $Params = @{
        RegistrationUrl = '<fill me in>';
        RegistrationKey = '<fill me in>';
        ComputerName = @('<some VM tooonboard>', '<some other VM tooonboard>');
        NodeConfigurationName = 'SimpleConfig.webserver';
        RefreshFrequencyMins = 30;
        ConfigurationModeFrequencyMins = 15;
        RebootNodeIfNeeded = $False;
        AllowModuleOverwrite = $False;
        ConfigurationMode = 'ApplyAndMonitor';
        ActionAfterReboot = 'ContinueConfiguration';
        ReportOnly = $False;  # Set too$True toohave machines only report tooAA DSC but not pull from it
    }

    # Use PowerShell splatting toopass parameters toohello DSC configuration being invoked
    # For more info about splatting, run: Get-Help -Name about_Splatting
    DscMetaConfigs @Params
    ```

3. <span data-ttu-id="dc09c-182">Renseignez la clé d’enregistrement hello et l’URL pour votre compte Automation, ainsi que les noms de hello de hello machines tooonboard.</span><span class="sxs-lookup"><span data-stu-id="dc09c-182">Fill in hello registration key and URL for your Automation account, as well as hello names of hello machines tooonboard.</span></span> <span data-ttu-id="dc09c-183">Tous les autres paramètres sont facultatifs.</span><span class="sxs-lookup"><span data-stu-id="dc09c-183">All other parameters are optional.</span></span> <span data-ttu-id="dc09c-184">toofind hello URL d’enregistrement clé et l’inscription de votre compte Automation, consultez hello [ **sécuriser l’inscription** ](#secure-registration) section ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="dc09c-184">toofind hello registration key and registration URL for your Automation account, see hello [**Secure registration**](#secure-registration) section below.</span></span>
4. <span data-ttu-id="dc09c-185">Si vous souhaitez hello machines tooreport DSC état informations tooAzure Automation DSC, mais il extrayez pas de configuration ou des modules PowerShell, définissez hello **ReportOnly** tootrue de paramètre.</span><span class="sxs-lookup"><span data-stu-id="dc09c-185">If you want hello machines tooreport DSC status information tooAzure Automation DSC, but not pull configuration or PowerShell modules, set hello **ReportOnly** parameter tootrue.</span></span>
5. <span data-ttu-id="dc09c-186">Exécutez le script de hello.</span><span class="sxs-lookup"><span data-stu-id="dc09c-186">Run hello script.</span></span> <span data-ttu-id="dc09c-187">Vous devez maintenant avoir un dossier appelé **DscMetaConfigs** dans votre répertoire de travail contenant métaconfigurations de DSC PowerShell hello pour tooonboard de machines hello (en tant qu’administrateur) :</span><span class="sxs-lookup"><span data-stu-id="dc09c-187">You should now have a folder called **DscMetaConfigs** in your working directory, containing hello PowerShell DSC metaconfigurations for hello machines tooonboard (as an administrator):</span></span>

    ```powershell
    Set-DscLocalConfigurationManager -Path ./DscMetaConfigs
    ```

### <a name="using-hello-azure-automation-cmdlets"></a><span data-ttu-id="dc09c-188">À l’aide des applets de commande hello Azure Automation</span><span class="sxs-lookup"><span data-stu-id="dc09c-188">Using hello Azure Automation cmdlets</span></span>

<span data-ttu-id="dc09c-189">Si les valeurs par défaut du Gestionnaire de Configuration Local DSC PowerShell hello correspond à votre cas d’usage, et que vous souhaitez tooonboard machines tels qu’ils extraient et rapport tooAzure Automation DSC, applets de commande hello Azure Automation fournissent une méthode simplifiée de la génération hello DSC métaconfigurations nécessitées :</span><span class="sxs-lookup"><span data-stu-id="dc09c-189">If hello PowerShell DSC Local Configuration Manager defaults match your use case, and you want tooonboard machines such that they both pull from and report tooAzure Automation DSC, hello Azure Automation cmdlets provide a simplified method of generating hello DSC metaconfigurations needed:</span></span>

1. <span data-ttu-id="dc09c-190">Ouvrez la console PowerShell de hello ou PowerShell ISE en tant qu’administrateur sur un ordinateur dans votre environnement local.</span><span class="sxs-lookup"><span data-stu-id="dc09c-190">Open hello PowerShell console or PowerShell ISE as an administrator in a machine in your local environment.</span></span>
2. <span data-ttu-id="dc09c-191">Connectez-vous à l’aide du Gestionnaire de ressources tooAzure **AzureRmAccount-ajouter**</span><span class="sxs-lookup"><span data-stu-id="dc09c-191">Connect tooAzure Resource Manager using **Add-AzureRmAccount**</span></span>
3. <span data-ttu-id="dc09c-192">Télécharger hello DSC PowerShell métaconfigurations pour les ordinateurs hello tooonboard de hello Automation compte toowhich vous voulez que les nœuds de tooonboard :</span><span class="sxs-lookup"><span data-stu-id="dc09c-192">Download hello PowerShell DSC metaconfigurations for hello machines you want tooonboard from hello Automation account toowhich you want tooonboard nodes:</span></span>

    ```powershell
    # Define hello parameters for Get-AzureRmAutomationDscOnboardingMetaconfig using PowerShell Splatting
    $Params = @{

        ResourceGroupName = 'ContosoResources'; # hello name of hello ARM Resource Group that contains your Azure Automation Account
        AutomationAccountName = 'ContosoAutomation'; # hello name of hello Azure Automation Account where you want a node on-boarded to
        ComputerName = @('web01', 'web02', 'sql01'); # hello names of hello computers that hello meta configuration will be generated for
        OutputFolder = "$env:UserProfile\Desktop\";
    }
    # Use PowerShell splatting toopass parameters toohello Azure Automation cmdlet being invoked
    # For more info about splatting, run: Get-Help -Name about_Splatting
    Get-AzureRmAutomationDscOnboardingMetaconfig @Params
    ```
    
4. <span data-ttu-id="dc09c-193">Vous devez maintenant avoir un dossier appelé ***DscMetaConfigs***, contenant métaconfigurations de DSC PowerShell hello pour tooonboard de machines hello (en tant qu’administrateur) :</span><span class="sxs-lookup"><span data-stu-id="dc09c-193">You should now have a folder called ***DscMetaConfigs***, containing hello PowerShell DSC metaconfigurations for hello machines tooonboard (as an administrator):</span></span>
    
    ```powershell
    Set-DscLocalConfigurationManager -Path $env:UserProfile\Desktop\DscMetaConfigs
    ```

## <a name="secure-registration"></a><span data-ttu-id="dc09c-194">Enregistrement sécurisé</span><span class="sxs-lookup"><span data-stu-id="dc09c-194">Secure registration</span></span>

<span data-ttu-id="dc09c-195">Ordinateurs peuvent s’intégrer en toute sécurité tooan compte Azure Automation via le protocole d’inscription hello WMF 5 DSC, ce qui permet un nœud tooauthenticate tooa PowerShell DSC V2 extraire ou création d’un rapport serveur DSC (y compris Azure Automation DSC).</span><span class="sxs-lookup"><span data-stu-id="dc09c-195">Machines can securely onboard tooan Azure Automation account through hello WMF 5 DSC registration protocol, which allows a DSC node tooauthenticate tooa PowerShell DSC V2 Pull or Reporting server (including Azure Automation DSC).</span></span> <span data-ttu-id="dc09c-196">nœud de Hello enregistre toohello sur le serveur à un **URL d’inscription**, l’authentification à l’aide un **clé d’inscription**.</span><span class="sxs-lookup"><span data-stu-id="dc09c-196">hello node registers toohello server at a **Registration URL**, authenticating using a **Registration key**.</span></span> <span data-ttu-id="dc09c-197">Pendant l’inscription, le nœud de hello DSC et DSC par extraction de données/Reporting server négocient un certificat unique pour cette toouse de nœud pour l’authentification toohello server postérieurs à le.</span><span class="sxs-lookup"><span data-stu-id="dc09c-197">During registration, hello DSC node and DSC Pull/Reporting server negotiate a unique certificate for this node toouse for authentication toohello server post-registration.</span></span> <span data-ttu-id="dc09c-198">Ce processus empêche les nœuds intégrés d’emprunter l’identité d’un autre nœud, par exemple si un nœud est compromis et agit à des fins malveillantes.</span><span class="sxs-lookup"><span data-stu-id="dc09c-198">This process prevents onboarded nodes from impersonating one another, such as if a node is compromised and behaving maliciously.</span></span> <span data-ttu-id="dc09c-199">Après l’inscription, clé d’inscription de hello n’est pas utilisée pour l’authentification à nouveau et est supprimée à partir du nœud de hello.</span><span class="sxs-lookup"><span data-stu-id="dc09c-199">After registration, hello Registration key is not used for authentication again, and is deleted from hello node.</span></span>

<span data-ttu-id="dc09c-200">Vous pouvez obtenir des informations de hello requises pour le protocole d’inscription hello DSC de hello **gérer les clés** panneau dans le portail Azure en version préliminaire de hello.</span><span class="sxs-lookup"><span data-stu-id="dc09c-200">You can get hello information required for hello DSC registration protocol from hello **Manage Keys** blade in hello Azure preview portal.</span></span> <span data-ttu-id="dc09c-201">Pour ouvrir ce panneau en cliquant sur icône de clé hello sur hello **Essentials** Panneau de configuration pour hello compte Automation.</span><span class="sxs-lookup"><span data-stu-id="dc09c-201">Open this blade by clicking hello key icon on hello **Essentials** panel for hello Automation account.</span></span>

![](./media/automation-dsc-onboarding/DSC_Onboarding_4.png)

* <span data-ttu-id="dc09c-202">URL d’inscription est le champ URL de hello dans le panneau de gérer les clés hello.</span><span class="sxs-lookup"><span data-stu-id="dc09c-202">Registration URL is hello URL field in hello Manage Keys blade.</span></span>
* <span data-ttu-id="dc09c-203">Clé d’inscription est hello clé d’accès primaire ou clé d’accès secondaire dans le panneau de gérer les clés hello.</span><span class="sxs-lookup"><span data-stu-id="dc09c-203">Registration key is hello Primary Access Key or Secondary Access Key in hello Manage Keys blade.</span></span> <span data-ttu-id="dc09c-204">Vous pouvez utiliser l’une de ces deux clés.</span><span class="sxs-lookup"><span data-stu-id="dc09c-204">Either key can be used.</span></span>

<span data-ttu-id="dc09c-205">Pour renforcer la sécurité des clés d’accès primaire et secondaire hello d’un compte Automation peuvent être régénérées à tout moment (sur hello **gérer les clés** panneau) des enregistrements du nœud futures tooprevent à l’aide des clés précédents.</span><span class="sxs-lookup"><span data-stu-id="dc09c-205">For added security, hello primary and secondary access keys of an Automation account can be regenerated at any time (on hello **Manage Keys** blade) tooprevent future node registrations using previous keys.</span></span>

## <a name="troubleshooting-azure-virtual-machine-onboarding"></a><span data-ttu-id="dc09c-206">Résolution des problèmes liés à l’intégration de machines virtuelles Azure</span><span class="sxs-lookup"><span data-stu-id="dc09c-206">Troubleshooting Azure virtual machine onboarding</span></span>

<span data-ttu-id="dc09c-207">Azure Automation DSC vous permet d’intégrer facilement des machines virtuelles Microsoft Azure à des fins de gestion de la configuration.</span><span class="sxs-lookup"><span data-stu-id="dc09c-207">Azure Automation DSC lets you easily onboard Azure Windows VMs for configuration management.</span></span> <span data-ttu-id="dc09c-208">Dans les coulisses hello, hello extension de Configuration d’état souhaité Azure VM est utilisé tooregister hello machine virtuelle dans Azure Automation DSC.</span><span class="sxs-lookup"><span data-stu-id="dc09c-208">Under hello hood, hello Azure VM Desired State Configuration extension is used tooregister hello VM with Azure Automation DSC.</span></span> <span data-ttu-id="dc09c-209">Étant donné que hello extension de Configuration d’état souhaité Azure VM s’exécute de façon asynchrone, le suivi de sa progression et la résolution des problèmes de son exécution peuvent être importants.</span><span class="sxs-lookup"><span data-stu-id="dc09c-209">Since hello Azure VM Desired State Configuration extension runs asynchronously, tracking its progress and troubleshooting its execution may be important.</span></span>

> [!NOTE]
> <span data-ttu-id="dc09c-210">N’importe quelle méthode de l’intégration une tooAzure de machine virtuelle de Windows Azure Automation DSC qui utilise l’extension de Configuration d’état souhaité Azure VM hello peut prendre les horaires de tooan pour tooshow de nœud hello des tel qu’enregistré dans Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="dc09c-210">Any method of onboarding an Azure Windows VM tooAzure Automation DSC that uses hello Azure VM Desired State Configuration extension could take up tooan hour for hello node tooshow up as registered in Azure Automation.</span></span> <span data-ttu-id="dc09c-211">Il s’agit en raison de l’installation de toohello de Windows Management Framework 5.0 sur hello VM par extension hello DSC des machines virtuelles Azure, qui est requis tooonboard hello VM tooAzure Automation DSC.</span><span class="sxs-lookup"><span data-stu-id="dc09c-211">This is due toohello installation of Windows Management Framework 5.0 on hello VM by hello Azure VM DSC extension, which is required tooonboard hello VM tooAzure Automation DSC.</span></span>

<span data-ttu-id="dc09c-212">tootroubleshoot ou la vue État hello Hello extension de Configuration d’état souhaité Azure VM, Bonjour Azure portal accédez toohello VM à intégrer, puis cliquez sur -> **tous les paramètres** -> **Extensions**   ->  **DSC**.</span><span class="sxs-lookup"><span data-stu-id="dc09c-212">tootroubleshoot or view hello status of hello Azure VM Desired State Configuration extension, in hello Azure portal navigate toohello VM being onboarded, then click -> **All settings** -> **Extensions** -> **DSC**.</span></span> <span data-ttu-id="dc09c-213">Pour plus de détails, vous pouvez cliquer sur **Afficher l’état détaillé**.</span><span class="sxs-lookup"><span data-stu-id="dc09c-213">For more details, you can click **View detailed status**.</span></span>

[![](./media/automation-dsc-onboarding/DSC_Onboarding_5.png)](https://technet.microsoft.com/library/dn249912.aspx)

## <a name="certificate-expiration-and-reregistration"></a><span data-ttu-id="dc09c-214">Expiration du certificat et nouvel enregistrement</span><span class="sxs-lookup"><span data-stu-id="dc09c-214">Certificate expiration and reregistration</span></span>

<span data-ttu-id="dc09c-215">Après avoir inscrit un ordinateur comme un nœud de DSC dans Azure Automation DSC, il existe de nombreuses raisons pour lesquelles vous devrez peut-être tooreregister ce nœud Bonjour ultérieure :</span><span class="sxs-lookup"><span data-stu-id="dc09c-215">After registering a machine as a DSC node in Azure Automation DSC, there are a number of reasons why you may need tooreregister that node in hello future:</span></span>

* <span data-ttu-id="dc09c-216">Une fois inscrit, chaque nœud négocie automatiquement un certificat unique pour l'authentification qui expire après un an.</span><span class="sxs-lookup"><span data-stu-id="dc09c-216">After registering, each node automatically negotiates a unique certificate for authentication that expires after one year.</span></span> <span data-ttu-id="dc09c-217">Actuellement, hello protocole d’inscription DSC PowerShell ne peut pas renouveler automatiquement les certificats quand ils arrivent à expiration, vous avez besoin de nœuds de hello tooreregister après l’heure d’une année.</span><span class="sxs-lookup"><span data-stu-id="dc09c-217">Currently, hello PowerShell DSC registration protocol cannot automatically renew certificates when they are nearing expiration, so you need tooreregister hello nodes after a year's time.</span></span> <span data-ttu-id="dc09c-218">Avant la réinscription, assurez-vous que chaque nœud exécute Windows Management Framework 5.0 RTM.</span><span class="sxs-lookup"><span data-stu-id="dc09c-218">Before reregistering, ensure that each node is running Windows Management Framework 5.0 RTM.</span></span> <span data-ttu-id="dc09c-219">Si l’expiration du certificat d’authentification d’un nœud et le nœud de hello n’est pas inscrit, nœud de hello sera toocommunicate impossible avec Azure Automation et est marqué « Ne répondant pas. »</span><span class="sxs-lookup"><span data-stu-id="dc09c-219">If a node's authentication certificate expires, and hello node is not reregistered, hello node will be unable toocommunicate with Azure Automation and will be marked 'Unresponsive.'</span></span> <span data-ttu-id="dc09c-220">Réinscription effectué 90 jours ou inférieur à partir de l’heure d’expiration du certificat hello ou à tout moment après le délai d’expiration de certificat hello, génère un nouveau certificat généré et utilisé.</span><span class="sxs-lookup"><span data-stu-id="dc09c-220">Reregistration performed 90 days or less from hello certificate expiration time, or at any point after hello certificate expiration time, will result in a new certificate being generated and used.</span></span>
* <span data-ttu-id="dc09c-221">toochange les [les valeurs de gestionnaire de Configuration Local DSC PowerShell](https://msdn.microsoft.com/powershell/dsc/metaconfig4) qui ont été définies lors de l’inscription initiale du nœud hello, telles que ConfigurationMode.</span><span class="sxs-lookup"><span data-stu-id="dc09c-221">toochange any [PowerShell DSC Local Configuration Manager values](https://msdn.microsoft.com/powershell/dsc/metaconfig4) that were set during initial registration of hello node, such as ConfigurationMode.</span></span> <span data-ttu-id="dc09c-222">Actuellement, ces valeurs de l’agent DSC peuvent être modifiées uniquement via une désinscription.</span><span class="sxs-lookup"><span data-stu-id="dc09c-222">Currently, these DSC agent values can only be changed through reregistration.</span></span> <span data-ttu-id="dc09c-223">une exception de Hello est hello Configuration de nœuds affectée toohello nœud : cela peut être modifié directement dans Azure Automation DSC.</span><span class="sxs-lookup"><span data-stu-id="dc09c-223">hello one exception is hello Node Configuration assigned toohello node -- this can be changed in Azure Automation DSC directly.</span></span>

<span data-ttu-id="dc09c-224">L’enregistrement n’est possible dans la même façon que vous avez enregistré les nœud hello au départ, l’une des méthodes d’intégration de hello décrites dans ce document de hello.</span><span class="sxs-lookup"><span data-stu-id="dc09c-224">Reregistration can be performed in hello same way you registered hello node initially, using any of hello onboarding methods described in this document.</span></span> <span data-ttu-id="dc09c-225">Vous n’avez pas besoin de toounregister un nœud à partir d’Azure Automation DSC avant la réinscription qu’il.</span><span class="sxs-lookup"><span data-stu-id="dc09c-225">You do not need toounregister a node from Azure Automation DSC before reregistering it.</span></span>

## <a name="related-articles"></a><span data-ttu-id="dc09c-226">Articles connexes</span><span class="sxs-lookup"><span data-stu-id="dc09c-226">Related Articles</span></span>

* [<span data-ttu-id="dc09c-227">Vue d’ensemble d’Azure Automation DSC</span><span class="sxs-lookup"><span data-stu-id="dc09c-227">Azure Automation DSC overview</span></span>](automation-dsc-overview.md)
* [<span data-ttu-id="dc09c-228">Applets de commande Azure Automation DSC</span><span class="sxs-lookup"><span data-stu-id="dc09c-228">Azure Automation DSC cmdlets</span></span>](/powershell/module/azurerm.automation/#automation)
* [<span data-ttu-id="dc09c-229">Tarification d’Azure Automation DSC</span><span class="sxs-lookup"><span data-stu-id="dc09c-229">Azure Automation DSC pricing</span></span>](https://azure.microsoft.com/pricing/details/automation/)
