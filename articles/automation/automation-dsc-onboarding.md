---
title: Gestion de machines avec Azure Automation DSC | Microsoft Docs
description: "Comment configurer des machines pour les gérer avec Azure Automation DSC"
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
ms.openlocfilehash: cc9b1ea19b4e17374d47e12f970cb333a8051559
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="onboarding-machines-for-management-by-azure-automation-dsc"></a><span data-ttu-id="ce3af-103">Gestion de machines avec Azure Automation DSC</span><span class="sxs-lookup"><span data-stu-id="ce3af-103">Onboarding machines for management by Azure Automation DSC</span></span>

## <a name="why-manage-machines-with-azure-automation-dsc"></a><span data-ttu-id="ce3af-104">Pourquoi gérer des machines avec Azure Automation DSC ?</span><span class="sxs-lookup"><span data-stu-id="ce3af-104">Why manage machines with Azure Automation DSC?</span></span>

<span data-ttu-id="ce3af-105">Tout comme le service [Desired State Configuration de PowerShell](https://technet.microsoft.com/library/dn249912.aspx), le Desired State Configuration d’Azure Automation est un service de gestion de configuration simple et puissant pour les nœuds DSC (machines physiques et virtuelles) dans n’importe quel centre de données sur le cloud ou sur site.</span><span class="sxs-lookup"><span data-stu-id="ce3af-105">Like [PowerShell Desired State Configuration](https://technet.microsoft.com/library/dn249912.aspx), Azure Automation Desired State Configuration is a simple, yet powerful, configuration management service for DSC nodes (physical and virtual machines) in any cloud or on-premises datacenter.</span></span> <span data-ttu-id="ce3af-106">Il permet de faire évoluer des milliers d’ordinateurs rapidement et facilement à partir d’un emplacement central et sécurisé.</span><span class="sxs-lookup"><span data-stu-id="ce3af-106">It enables scalability across thousands of machines quickly and easily from a central, secure location.</span></span> <span data-ttu-id="ce3af-107">Vous pouvez facilement intégrer des machines, leur affecter des configurations déclaratives et afficher des rapports montrant la conformité de chaque machine à l’état souhaité que vous avez spécifié.</span><span class="sxs-lookup"><span data-stu-id="ce3af-107">You can easily onboard machines, assign them declarative configurations, and view reports showing each machine's compliance to the desired state you specified.</span></span> <span data-ttu-id="ce3af-108">La couche de gestion Azure Automation DSC est au DSC ce que la couche de gestion Azure Automation est aux scripts PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ce3af-108">The Azure Automation DSC management layer is to DSC what the Azure Automation management layer is to PowerShell scripting.</span></span> <span data-ttu-id="ce3af-109">En d'autres termes, de la même manière que Azure Automation vous permet de gérer des scripts PowerShell, il vous aide également à gérer des configurations DSC.</span><span class="sxs-lookup"><span data-stu-id="ce3af-109">In other words, in the same way that Azure Automation helps you manage PowerShell scripts, it also helps you manage DSC configurations.</span></span> <span data-ttu-id="ce3af-110">Pour en savoir plus sur les avantages de l’utilisation d’Azure Automation DSC, consultez [Vue d’ensemble d’Azure Automation DSC](automation-dsc-overview.md).</span><span class="sxs-lookup"><span data-stu-id="ce3af-110">To learn more about the benefits of using Azure Automation DSC, see [Azure Automation DSC overview](automation-dsc-overview.md).</span></span>

<span data-ttu-id="ce3af-111">Azure Automation DSC peut servir à gérer une grande diversité de machines :</span><span class="sxs-lookup"><span data-stu-id="ce3af-111">Azure Automation DSC can be used to manage a variety of machines:</span></span>

* <span data-ttu-id="ce3af-112">Machines virtuelles Azure (classiques)</span><span class="sxs-lookup"><span data-stu-id="ce3af-112">Azure virtual machines (classic)</span></span>
* <span data-ttu-id="ce3af-113">Machines virtuelles Azure</span><span class="sxs-lookup"><span data-stu-id="ce3af-113">Azure virtual machines</span></span>
* <span data-ttu-id="ce3af-114">Machines virtuelles Amazon Web Services (AWS)</span><span class="sxs-lookup"><span data-stu-id="ce3af-114">Amazon Web Services (AWS) virtual machines</span></span>
* <span data-ttu-id="ce3af-115">Machines physiques/virtuelles Windows locales ou dans un cloud autre qu’Azure/AWS</span><span class="sxs-lookup"><span data-stu-id="ce3af-115">Physical/virtual Windows machines on-premises, or in a cloud other than Azure/AWS</span></span>
* <span data-ttu-id="ce3af-116">Machines physiques/virtuelles Linux sur site, dans Azure, ou dans un cloud autre qu’Azure</span><span class="sxs-lookup"><span data-stu-id="ce3af-116">Physical/virtual Linux machines on-premises, in Azure, or in a cloud other than Azure</span></span>

<span data-ttu-id="ce3af-117">En outre, si vous n’êtes pas prêt à gérer la configuration de l’ordinateur dans le cloud, Azure Automation DSC peut également servir de point de terminaison dédié uniquement à la génération de rapports.</span><span class="sxs-lookup"><span data-stu-id="ce3af-117">In addition, if you are not ready to manage machine configuration from the cloud, Azure Automation DSC can also be used as a report-only endpoint.</span></span> <span data-ttu-id="ce3af-118">Vous pouvez ainsi définir la configuration (push) de votre choix via une instance DSC en local et afficher des détails de rapports sur la conformité du nœud à l’état souhaité dans Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="ce3af-118">This allows you to set (push) desired configuration through DSC on-premises and view rich reporting details on node compliance with the desired state in Azure Automation.</span></span>

<span data-ttu-id="ce3af-119">Les sections suivantes décrivent la manière dont vous pouvez intégrer chaque type de machine à Azure Automation DSC.</span><span class="sxs-lookup"><span data-stu-id="ce3af-119">The following sections outline how you can onboard each type of machine to Azure Automation DSC.</span></span>

## <a name="azure-virtual-machines-classic"></a><span data-ttu-id="ce3af-120">Machines virtuelles Azure (classiques)</span><span class="sxs-lookup"><span data-stu-id="ce3af-120">Azure virtual machines (classic)</span></span>

<span data-ttu-id="ce3af-121">Avec Azure Automation DSC, vous pouvez facilement intégrer des machines virtuelles Azure (classiques) pour une gestion de configuration via le portail Azure ou via PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ce3af-121">With Azure Automation DSC, you can easily onboard Azure virtual machines (classic) for configuration management using either the Azure portal, or PowerShell.</span></span> <span data-ttu-id="ce3af-122">En arrière-plan, et sans qu’aucun administrateur n’ait à contrôler la machine virtuelle à distance, l’extension Azure VM Desired State Configuration enregistre la machine virtuelle avec Azure Automation DSC.</span><span class="sxs-lookup"><span data-stu-id="ce3af-122">Under the hood, and without an administrator having to remote into the VM, the Azure VM Desired State Configuration extension registers the VM with Azure Automation DSC.</span></span> <span data-ttu-id="ce3af-123">Étant donné que cette extension s’exécute de façon asynchrone, la section [**Résolution des problèmes liés à l’intégration de machines virtuelles Azure**](#troubleshooting-azure-virtual-machine-onboarding) ci-dessous décrit la procédure à suivre pour contrôler sa progression ou résoudre les problèmes.</span><span class="sxs-lookup"><span data-stu-id="ce3af-123">Since the Azure VM Desired State Configuration extension runs asynchronously, steps to track its progress or troubleshoot it are provided in the [**Troubleshooting Azure virtual machine onboarding**](#troubleshooting-azure-virtual-machine-onboarding) section below.</span></span>

### <a name="azure-portal"></a><span data-ttu-id="ce3af-124">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="ce3af-124">Azure portal</span></span>

<span data-ttu-id="ce3af-125">Dans le [portail Azure](http://portal.azure.com/), cliquez sur **Parcourir** -> **Machines virtuelles (classiques)**.</span><span class="sxs-lookup"><span data-stu-id="ce3af-125">In the [Azure portal](http://portal.azure.com/), click **Browse** -> **Virtual machines (classic)**.</span></span> <span data-ttu-id="ce3af-126">Sélectionnez la machine virtuelle Windows que vous souhaitez intégrer.</span><span class="sxs-lookup"><span data-stu-id="ce3af-126">Select the Windows VM you want to onboard.</span></span> <span data-ttu-id="ce3af-127">Dans le panneau du tableau de bord de la machine virtuelle, cliquez sur **Tous les paramètres** -> **Extensions** -> **Ajouter** -> **Azure Automation DSC** -> **Créer**.</span><span class="sxs-lookup"><span data-stu-id="ce3af-127">On the virtual machine's dashboard blade, click **All settings** -> **Extensions** -> **Add** -> **Azure Automation DSC** -> **Create**.</span></span> <span data-ttu-id="ce3af-128">Entrez les [valeurs du gestionnaire de configuration locale de PowerShell DSC](https://msdn.microsoft.com/powershell/dsc/metaconfig4) requises, la clé et l’URL d’inscription de votre compte Automation, et, éventuellement, une configuration de nœud à attribuer à la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="ce3af-128">Enter the [PowerShell DSC Local Configuration Manager values](https://msdn.microsoft.com/powershell/dsc/metaconfig4) required for your use case, your Automation account's registration key and registration URL, and optionally a node configuration to assign to the VM.</span></span>

![](./media/automation-dsc-onboarding/DSC_Onboarding_1.png)

<span data-ttu-id="ce3af-129">Pour trouver l’URL et la clé d’enregistrement pour le compte Automation, consultez la section [**Enregistrement sécurisé**](#secure-registration) ci-dessous décrit la procédure à suivre pour contrôler sa progression ou résoudre les problèmes.</span><span class="sxs-lookup"><span data-stu-id="ce3af-129">To find the registration URL and key for the Automation account to onboard the machine to, see the [**Secure registration**](#secure-registration) section below.</span></span>

### <a name="powershell"></a><span data-ttu-id="ce3af-130">PowerShell</span><span class="sxs-lookup"><span data-stu-id="ce3af-130">PowerShell</span></span>

```powershell
# log in to both Azure Service Management and Azure Resource Manager
Add-AzureAccount
Add-AzureRmAccount

# fill in correct values for your VM/Automation account here
$VMName = ""
$ServiceName = ""
$AutomationAccountName = ""
$AutomationAccountResourceGroup = ""

# fill in the name of a Node Configuration in Azure Automation DSC, for this VM to conform to
$NodeConfigName = ""

# get Azure Automation DSC registration info
$Account = Get-AzureRmAutomationAccount -ResourceGroupName $AutomationAccountResourceGroup -Name $AutomationAccountName
$RegistrationInfo = $Account | Get-AzureRmAutomationRegistrationInfo

# use the DSC extension to onboard the VM for management with Azure Automation DSC
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

## <a name="azure-virtual-machines"></a><span data-ttu-id="ce3af-131">Machines virtuelles Azure</span><span class="sxs-lookup"><span data-stu-id="ce3af-131">Azure virtual machines</span></span>

<span data-ttu-id="ce3af-132">Azure Automation DSC vous permet d’intégrer facilement des machines virtuelles Azure pour une gestion de configuration via le portail Azure, les modèles Azure Resource Manager ou PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ce3af-132">Azure Automation DSC lets you easily onboard Azure virtual machines for configuration management, using either the Azure portal, Azure Resource Manager templates, or PowerShell.</span></span> <span data-ttu-id="ce3af-133">En arrière-plan, et sans qu’aucun administrateur n’ait à contrôler la machine virtuelle à distance, l’extension Azure VM Desired State Configuration enregistre la machine virtuelle avec Azure Automation DSC.</span><span class="sxs-lookup"><span data-stu-id="ce3af-133">Under the hood, and without an administrator having to remote into the VM, the Azure VM Desired State Configuration extension registers the VM with Azure Automation DSC.</span></span> <span data-ttu-id="ce3af-134">Étant donné que cette extension s’exécute de façon asynchrone, la section [**Résolution des problèmes liés à l’intégration de machines virtuelles Azure**](#troubleshooting-azure-virtual-machine-onboarding) ci-dessous décrit la procédure à suivre pour contrôler sa progression ou résoudre les problèmes.</span><span class="sxs-lookup"><span data-stu-id="ce3af-134">Since the Azure VM Desired State Configuration extension runs asynchronously, steps to track its progress or troubleshoot it are provided in the [**Troubleshooting Azure virtual machine onboarding**](#troubleshooting-azure-virtual-machine-onboarding) section below.</span></span>

### <a name="azure-portal"></a><span data-ttu-id="ce3af-135">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="ce3af-135">Azure portal</span></span>

<span data-ttu-id="ce3af-136">Dans le [portail Azure](https://portal.azure.com/), accédez au compte Azure Automation où vous souhaitez intégrer des machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="ce3af-136">In the [Azure portal](https://portal.azure.com/), navigate to the Azure Automation account where you want to onboard virtual machines.</span></span> <span data-ttu-id="ce3af-137">Dans le tableau de bord du compte Automation, cliquez sur **Nœuds DSC** -> **Ajouter une machine virtuelle Azure**.</span><span class="sxs-lookup"><span data-stu-id="ce3af-137">On the Automation account dashboard, click **DSC Nodes** -> **Add Azure VM**.</span></span>

<span data-ttu-id="ce3af-138">Sous **Sélectionner les machines virtuelles à intégrer**, sélectionnez une ou plusieurs machines virtuelles Azure que vous souhaitez intégrer.</span><span class="sxs-lookup"><span data-stu-id="ce3af-138">Under **Select virtual machines to onboard**, select one or more Azure virtual machines to onboard.</span></span>

![](./media/automation-dsc-onboarding/DSC_Onboarding_2.png)

<span data-ttu-id="ce3af-139">Sous **Configure registration data**(Configurer les données de l’enregistrement), entrez les [valeurs du gestionnaire de configuration locale de PowerShell DSC](https://msdn.microsoft.com/powershell/dsc/metaconfig4) requises et, éventuellement, une configuration de nœud à attribuer à la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="ce3af-139">Under **Configure registration data**, enter the [PowerShell DSC Local Configuration Manager values](https://msdn.microsoft.com/powershell/dsc/metaconfig4) required for your use case, and optionally a node configuration to assign to the VM.</span></span>

![](./media/automation-dsc-onboarding/DSC_Onboarding_3.png)

### <a name="azure-resource-manager-templates"></a><span data-ttu-id="ce3af-140">Modèles Microsoft Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="ce3af-140">Azure Resource Manager templates</span></span>

<span data-ttu-id="ce3af-141">Les machines virtuelles Azure peuvent être déployées et intégrées sur Azure Automation DSC via des modèles Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="ce3af-141">Azure virtual machines can be deployed and onboarded to Azure Automation DSC via Azure Resource Manager templates.</span></span> <span data-ttu-id="ce3af-142">Pour un exemple de modèle intégrant une machine virtuelle existante à Azure Automation DSC, consultez [Configurer une machine virtuelle par le biais de l’extension DSC et d’Azure Automation DSC](https://azure.microsoft.com/documentation/templates/dsc-extension-azure-automation-pullserver/) .</span><span class="sxs-lookup"><span data-stu-id="ce3af-142">See [Configure a VM via DSC extension and Azure Automation DSC](https://azure.microsoft.com/documentation/templates/dsc-extension-azure-automation-pullserver/) for an example template that onboards an existing VM to Azure Automation DSC.</span></span> <span data-ttu-id="ce3af-143">Pour trouver la clé et l’URL d’enregistrement utilisées comme entrées dans ce modèle, consultez la section [**Enregistrement sécurisé**](#secure-registration) ci-dessous décrit la procédure à suivre pour contrôler sa progression ou résoudre les problèmes.</span><span class="sxs-lookup"><span data-stu-id="ce3af-143">To find the registration key and registration URL taken as input in this template, see the [**Secure registration**](#secure-registration) section below.</span></span>

### <a name="powershell"></a><span data-ttu-id="ce3af-144">PowerShell</span><span class="sxs-lookup"><span data-stu-id="ce3af-144">PowerShell</span></span>

<span data-ttu-id="ce3af-145">Vous pouvez utiliser l’applet de commande [Register-AzureRmAutomationDscNode](/powershell/module/azurerm.automation/register-azurermautomationdscnode) pour intégrer des machines virtuelles au portail Azure par le biais de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ce3af-145">The [Register-AzureRmAutomationDscNode](/powershell/module/azurerm.automation/register-azurermautomationdscnode) cmdlet can be used to onboard virtual machines in the Azure portal via PowerShell.</span></span>

## <a name="amazon-web-services-aws-virtual-machines"></a><span data-ttu-id="ce3af-146">Machines virtuelles Amazon Web Services (AWS)</span><span class="sxs-lookup"><span data-stu-id="ce3af-146">Amazon Web Services (AWS) virtual machines</span></span>

<span data-ttu-id="ce3af-147">Vous pouvez facilement intégrer Amazon Web Services pour la gestion de configuration par Azure Automation DSC avec la boîte à outils AWS DSC.</span><span class="sxs-lookup"><span data-stu-id="ce3af-147">You can easily onboard Amazon Web Services virtual machines for configuration management by Azure Automation DSC using the AWS DSC Toolkit.</span></span> <span data-ttu-id="ce3af-148">Pour obtenir plus d’informations sur cette boîte à outils, cliquez [ici](https://blogs.msdn.microsoft.com/powershell/2016/04/20/aws-dsc-toolkit/).</span><span class="sxs-lookup"><span data-stu-id="ce3af-148">You can learn more about the toolkit [here](https://blogs.msdn.microsoft.com/powershell/2016/04/20/aws-dsc-toolkit/).</span></span>

## <a name="physicalvirtual-windows-machines-on-premises-or-in-a-cloud-other-than-azureaws"></a><span data-ttu-id="ce3af-149">Machines physiques/virtuelles Windows locales ou dans un cloud autre qu’Azure/AWS</span><span class="sxs-lookup"><span data-stu-id="ce3af-149">Physical/virtual Windows machines on-premises, or in a cloud other than Azure/AWS</span></span>

<span data-ttu-id="ce3af-150">Les ordinateurs Windows en local et les ordinateurs Windows dans des clouds autres qu’Azure (comme Amazon Web Services) peuvent également être intégrés sur Azure Automation DSC à condition qu’ils disposent d’accès sortant à Internet. Leur intégration s’effectue très simplement, en quelques étapes :</span><span class="sxs-lookup"><span data-stu-id="ce3af-150">On-premises Windows machines and Windows machines in non-Azure clouds (such as Amazon Web Services) can also be onboarded to Azure Automation DSC, as long as they have outbound access to the internet, via a few simple steps:</span></span>

1. <span data-ttu-id="ce3af-151">Assurez-vous que la dernière version de [WMF 5](http://aka.ms/wmf5latest) est installée sur les ordinateurs que vous souhaitez intégrer à Azure Automation DSC.</span><span class="sxs-lookup"><span data-stu-id="ce3af-151">Make sure the latest version of [WMF 5](http://aka.ms/wmf5latest) is installed on the machines you want to onboard to Azure Automation DSC.</span></span>
2. <span data-ttu-id="ce3af-152">Suivez les instructions de la section [**Génération de métaconfigurations DSC**](#generating-dsc-metaconfigurations) ci-après pour générer un dossier contenant les métaconfigurations DSC nécessaires.</span><span class="sxs-lookup"><span data-stu-id="ce3af-152">Follow the directions in section [**Generating DSC metaconfigurations**](#generating-dsc-metaconfigurations) below to generate a folder containing the needed DSC metaconfigurations.</span></span>
3. <span data-ttu-id="ce3af-153">Appliquez à distance la métaconfiguration DSC PowerShell aux machines que vous voulez intégrer.</span><span class="sxs-lookup"><span data-stu-id="ce3af-153">Remotely apply the PowerShell DSC metaconfiguration to the machines you want to onboard.</span></span> <span data-ttu-id="ce3af-154">**La machine à partir de laquelle cette commande est exécutée doit disposer de la dernière version de [WMF 5](http://aka.ms/wmf5latest)**:</span><span class="sxs-lookup"><span data-stu-id="ce3af-154">**The machine this command is run from must have the latest version of [WMF 5](http://aka.ms/wmf5latest) installed**:</span></span>

    ```powershell
    Set-DscLocalConfigurationManager -Path C:\Users\joe\Desktop\DscMetaConfigs -ComputerName MyServer1, MyServer2
    ```

4. <span data-ttu-id="ce3af-155">Si vous ne pouvez pas appliquer les métaconfigurations DSC PowerShell à distance, copiez le dossier des métaconfigurations de l’étape 2 sur chaque machine à intégrer.</span><span class="sxs-lookup"><span data-stu-id="ce3af-155">If you cannot apply the PowerShell DSC metaconfigurations remotely, copy the metaconfigurations folder from step 2 onto each machine to onboard.</span></span> <span data-ttu-id="ce3af-156">Appelez ensuite **Set-DscLocalConfigurationManager** localement sur chaque machine à intégrer.</span><span class="sxs-lookup"><span data-stu-id="ce3af-156">Then call **Set-DscLocalConfigurationManager** locally on each machine to onboard.</span></span>
5. <span data-ttu-id="ce3af-157">À l’aide du portail Azure ou des applets de commande, vérifiez que les machines à intégrer s’affichent bien en tant que nœuds DSC enregistrés dans votre compte Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="ce3af-157">Using the Azure portal or cmdlets, check that the machines to onboard now show up as DSC nodes registered in your Azure Automation account.</span></span>

## <a name="physicalvirtual-linux-machines-on-premises-in-azure-or-in-a-cloud-other-than-azure"></a><span data-ttu-id="ce3af-158">Machines physiques/virtuelles Linux sur site, dans Azure, ou dans un cloud autre qu’Azure</span><span class="sxs-lookup"><span data-stu-id="ce3af-158">Physical/virtual Linux machines on-premises, in Azure, or in a cloud other than Azure</span></span>

<span data-ttu-id="ce3af-159">Les ordinateurs Linux en local, les ordinateurs dans Azure et les ordinateurs Linux dans des clouds autres qu’Azure peuvent également être intégrés à Azure Automation DSC à condition qu’ils disposent d’un accès sortant à Internet. Leur intégration s’effectue très simplement, en quelques étapes :</span><span class="sxs-lookup"><span data-stu-id="ce3af-159">On-premises Linux machines, Linux machines in Azure, and Linux machines in non-Azure clouds can also be onboarded to Azure Automation DSC, as long as they have outbound access to the internet, via a few simple steps:</span></span>

1. <span data-ttu-id="ce3af-160">Assurez-vous que la dernière version du service [Desired State Configuration de PowerShel pour Linux](https://github.com/Microsoft/PowerShell-DSC-for-Linux) est installée sur les ordinateurs que vous souhaitez intégrer à Azure Automation DSC.</span><span class="sxs-lookup"><span data-stu-id="ce3af-160">Make sure the latest version of [PowerShell Desired State Configuration for Linux](https://github.com/Microsoft/PowerShell-DSC-for-Linux) is installed on the machines you want to onboard to Azure Automation DSC.</span></span>
2. <span data-ttu-id="ce3af-161">Si les [valeurs par défaut du gestionnaire de configuration locale DSC PowerShell](https://msdn.microsoft.com/powershell/dsc/metaconfig4) correspondent à votre cas d’utilisation et que vous voulez intégrer des machines de sorte qu’elles procèdent **à la fois** à une extraction auprès d’Azure Automation DSC et qu’elles lui adressent des rapports :</span><span class="sxs-lookup"><span data-stu-id="ce3af-161">If the [PowerShell DSC Local Configuration Manager defaults](https://msdn.microsoft.com/powershell/dsc/metaconfig4) match your use case, and you want to onboard machines such that they **both** pull from and report to Azure Automation DSC:</span></span>

   + <span data-ttu-id="ce3af-162">Sur chaque ordinateur Linux que vous souhaitez intégrer sur Azure Automation DSC, utilisez Register.py pour effectuer l’intégration en utilisant les valeurs par défaut du gestionnaire de configuration locale DSC PowerShell :</span><span class="sxs-lookup"><span data-stu-id="ce3af-162">On each Linux machine to onboard to Azure Automation DSC, use Register.py to onboard using the PowerShell DSC Local Configuration Manager defaults:</span></span>

     `/opt/microsoft/dsc/Scripts/Register.py <Automation account registration key> <Automation account registration URL>`

   + <span data-ttu-id="ce3af-163">Pour trouver la clé et l’URL d’enregistrement pour votre compte Automation, consultez la section [**Enregistrement sécurisé**](#secure-registration) ci-dessous décrit la procédure à suivre pour contrôler sa progression ou résoudre les problèmes.</span><span class="sxs-lookup"><span data-stu-id="ce3af-163">To find the registration key and registration URL for your Automation account, see the [**Secure registration**](#secure-registration) section below.</span></span>

     <span data-ttu-id="ce3af-164">Si les valeurs par défaut du gestionnaire de configuration locale DSC PowerShell **ne** correspondent **pas** à votre cas d’utilisation ou si vous voulez intégrer des machines de sorte qu’elles adressent seulement des rapports à Azure Automation DSC, sans en extraire la configuration ou des modules PowerShell, suivez les étapes 3 à 6.</span><span class="sxs-lookup"><span data-stu-id="ce3af-164">If the PowerShell DSC Local Configuration Manager defaults **do** **not** match your use case, or you want to onboard machines such that they only report to Azure Automation DSC, but do not pull configuration or PowerShell modules from it,  follow steps 3 - 6.</span></span> <span data-ttu-id="ce3af-165">Sinon, passez directement à l’étape 6.</span><span class="sxs-lookup"><span data-stu-id="ce3af-165">Otherwise, proceed directly to step 6.</span></span>

3. <span data-ttu-id="ce3af-166">Suivez les instructions de la section [**Génération de métaconfigurations DSC**](#generating-dsc-metaconfigurations) ci-dessous pour générer un dossier contenant les métaconfigurations DSC nécessaires.</span><span class="sxs-lookup"><span data-stu-id="ce3af-166">Follow the directions in the [**Generating DSC metaconfigurations**](#generating-dsc-metaconfigurations) section below to generate a folder containing the needed DSC metaconfigurations.</span></span>
4. <span data-ttu-id="ce3af-167">Appliquez à distance la métaconfiguration PowerShell DSC pour les machines que vous souhaitez intégrer :</span><span class="sxs-lookup"><span data-stu-id="ce3af-167">Remotely apply the PowerShell DSC metaconfiguration to the machines you want to onboard:</span></span>

    ```powershell
    $SecurePass = ConvertTo-SecureString -String "<root password>" -AsPlainText -Force
    $Cred = New-Object System.Management.Automation.PSCredential "root", $SecurePass
    $Opt = New-CimSessionOption -UseSsl -SkipCACheck -SkipCNCheck -SkipRevocationCheck

    # need a CimSession for each Linux machine to onboard

    $Session = New-CimSession -Credential $Cred -ComputerName <your Linux machine> -Port 5986 -Authentication basic -SessionOption $Opt

    Set-DscLocalConfigurationManager -CimSession $Session -Path C:\Users\joe\Desktop\DscMetaConfigs
    ```

<span data-ttu-id="ce3af-168">La machine à partir de laquelle cette commande est exécutée doit disposer de la dernière version de [WMF 5](http://aka.ms/wmf5latest) .</span><span class="sxs-lookup"><span data-stu-id="ce3af-168">The machine this command is run from must have the latest version of [WMF 5](http://aka.ms/wmf5latest) installed.</span></span>

1. <span data-ttu-id="ce3af-169">Si vous ne pouvez pas appliquer à distance les métaconfigurations PowerShell DSC, pour chaque ordinateur Linux à intégrer, copiez la métaconfiguration correspondant à cet ordinateur à partir du dossier de l’étape 5 sur l’ordinateur Linux.</span><span class="sxs-lookup"><span data-stu-id="ce3af-169">If you cannot apply the PowerShell DSC metaconfigurations remotely, for each Linux machine to onboard, copy the metaconfiguration corresponding to that machine from the folder in step 5 onto the Linux machine.</span></span> <span data-ttu-id="ce3af-170">Appelez ensuite `SetDscLocalConfigurationManager.py` localement sur chaque ordinateur Linux que vous souhaitez intégrer à Azure Automation DSC :</span><span class="sxs-lookup"><span data-stu-id="ce3af-170">Then call `SetDscLocalConfigurationManager.py` locally on each Linux machine you want to onboard to Azure Automation DSC:</span></span>

   `/opt/microsoft/dsc/Scripts/SetDscLocalConfigurationManager.py -configurationmof <path to metaconfiguration file>`

2. <span data-ttu-id="ce3af-171">À l’aide du portail Azure ou des applets de commande, vérifiez que les machines à intégrer s’affichent bien en tant que nœuds DSC enregistrés dans votre compte Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="ce3af-171">Using the Azure portal or cmdlets, check that the machines to onboard now show up as DSC nodes registered in your Azure Automation account.</span></span>

## <a name="generating-dsc-metaconfigurations"></a><span data-ttu-id="ce3af-172">Génération de métaconfigurations DSC</span><span class="sxs-lookup"><span data-stu-id="ce3af-172">Generating DSC metaconfigurations</span></span>

<span data-ttu-id="ce3af-173">Pour intégrer de manière générique n’importe quelle machine à Azure Automation DSC, une [métaconfiguration DSC](https://msdn.microsoft.com/en-us/powershell/dsc/metaconfig) peut être générée qui, une fois appliquée, demande à l’agent DSC de la machine d’effectuer une extraction auprès d’Azure Automation DSC et/ou de lui adresser un rapport.</span><span class="sxs-lookup"><span data-stu-id="ce3af-173">To generically onboard any machine to Azure Automation DSC, a [DSC metaconfiguration](https://msdn.microsoft.com/en-us/powershell/dsc/metaconfig) can be generated that, when applied, tells the DSC agent on the machine to pull from and/or report to Azure Automation DSC.</span></span> <span data-ttu-id="ce3af-174">Les métaconfigurations DSC pour Azure Automation DSC peuvent être générées à l’aide d’une configuration PowerShell DSC ou des applets de commande PowerShell Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="ce3af-174">DSC metaconfigurations for Azure Automation DSC can be generated using either a PowerShell DSC configuration, or the Azure Automation PowerShell cmdlets.</span></span>

> [!NOTE]
> <span data-ttu-id="ce3af-175">Les métaconfigurations DSC contiennent les clés secrètes nécessaires à l’intégration d’une machine à un compte Automation à des fins de gestion.</span><span class="sxs-lookup"><span data-stu-id="ce3af-175">DSC metaconfigurations contain the secrets needed to onboard a machine to an Automation account for management.</span></span> <span data-ttu-id="ce3af-176">Veillez à protéger convenablement les métaconfigurations DSC que vous créez ou supprimez-les après utilisation.</span><span class="sxs-lookup"><span data-stu-id="ce3af-176">Make sure to properly protect any DSC metaconfigurations you create, or delete them after use.</span></span>

### <a name="using-a-dsc-configuration"></a><span data-ttu-id="ce3af-177">Utilisation d’une configuration DSC</span><span class="sxs-lookup"><span data-stu-id="ce3af-177">Using a DSC Configuration</span></span>

1. <span data-ttu-id="ce3af-178">Ouvrez PowerShell ISE en tant qu’administrateur sur une machine de votre environnement local.</span><span class="sxs-lookup"><span data-stu-id="ce3af-178">Open the PowerShell ISE as an administrator in a machine in your local environment.</span></span> <span data-ttu-id="ce3af-179">Cette machine doit disposer de la dernière version de [WMF 5](http://aka.ms/wmf5latest) .</span><span class="sxs-lookup"><span data-stu-id="ce3af-179">The machine must have the latest version of [WMF 5](http://aka.ms/wmf5latest) installed.</span></span>
2. <span data-ttu-id="ce3af-180">Copiez le script suivant localement.</span><span class="sxs-lookup"><span data-stu-id="ce3af-180">Copy the following script locally.</span></span> <span data-ttu-id="ce3af-181">Ce script contient une configuration DSC PowerShell pour créer des métaconfigurations, ainsi qu’une commande pour lancer la création de métaconfigurations.</span><span class="sxs-lookup"><span data-stu-id="ce3af-181">This script contains a PowerShell DSC configuration for creating metaconfigurations, and a command to kick off the metaconfiguration creation.</span></span>

    ```powershell
    # The DSC configuration that will generate metaconfigurations
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

    # Create the metaconfigurations
    # TODO: edit the below as needed for your use case
    $Params = @{
        RegistrationUrl = '<fill me in>';
        RegistrationKey = '<fill me in>';
        ComputerName = @('<some VM to onboard>', '<some other VM to onboard>');
        NodeConfigurationName = 'SimpleConfig.webserver';
        RefreshFrequencyMins = 30;
        ConfigurationModeFrequencyMins = 15;
        RebootNodeIfNeeded = $False;
        AllowModuleOverwrite = $False;
        ConfigurationMode = 'ApplyAndMonitor';
        ActionAfterReboot = 'ContinueConfiguration';
        ReportOnly = $False;  # Set to $True to have machines only report to AA DSC but not pull from it
    }

    # Use PowerShell splatting to pass parameters to the DSC configuration being invoked
    # For more info about splatting, run: Get-Help -Name about_Splatting
    DscMetaConfigs @Params
    ```

3. <span data-ttu-id="ce3af-182">Renseignez la clé d’inscription et l’URL de votre compte Automation, ainsi que les noms des machines à intégrer.</span><span class="sxs-lookup"><span data-stu-id="ce3af-182">Fill in the registration key and URL for your Automation account, as well as the names of the machines to onboard.</span></span> <span data-ttu-id="ce3af-183">Tous les autres paramètres sont facultatifs.</span><span class="sxs-lookup"><span data-stu-id="ce3af-183">All other parameters are optional.</span></span> <span data-ttu-id="ce3af-184">Pour trouver la clé et l’URL d’enregistrement pour votre compte Automation, consultez la section [**Enregistrement sécurisé**](#secure-registration) ci-dessous décrit la procédure à suivre pour contrôler sa progression ou résoudre les problèmes.</span><span class="sxs-lookup"><span data-stu-id="ce3af-184">To find the registration key and registration URL for your Automation account, see the [**Secure registration**](#secure-registration) section below.</span></span>
4. <span data-ttu-id="ce3af-185">Si vous voulez que les machines adressent les informations d’état DSC à Azure Automation DSC sans toutefois extraire la configuration ou des modules PowerShell, affectez au paramètre **ReportOnly** la valeur true.</span><span class="sxs-lookup"><span data-stu-id="ce3af-185">If you want the machines to report DSC status information to Azure Automation DSC, but not pull configuration or PowerShell modules, set the **ReportOnly** parameter to true.</span></span>
5. <span data-ttu-id="ce3af-186">Exécutez le script.</span><span class="sxs-lookup"><span data-stu-id="ce3af-186">Run the script.</span></span> <span data-ttu-id="ce3af-187">Vous devez à présent avoir un dossier appelé **DscMetaConfigs** dans votre répertoire de travail contenant les métaconfigurations DSC PowerShell pour les machines à intégrer (en tant qu’administrateur) :</span><span class="sxs-lookup"><span data-stu-id="ce3af-187">You should now have a folder called **DscMetaConfigs** in your working directory, containing the PowerShell DSC metaconfigurations for the machines to onboard (as an administrator):</span></span>

    ```powershell
    Set-DscLocalConfigurationManager -Path ./DscMetaConfigs
    ```

### <a name="using-the-azure-automation-cmdlets"></a><span data-ttu-id="ce3af-188">Utilisation des applets de commande Azure Automation</span><span class="sxs-lookup"><span data-stu-id="ce3af-188">Using the Azure Automation cmdlets</span></span>

<span data-ttu-id="ce3af-189">Si les valeurs par défaut du gestionnaire de configuration locale DSC PowerShell correspondent à votre cas d’utilisation et que vous voulez intégrer des machines de sorte qu’elles procèdent à la fois à une extraction auprès d’Azure Automation DSC et qu’elles lui adressent des rapports, les applets de commande Azure Automation constituent une méthode qui simplifie la génération des métaconfigurations nécessaires :</span><span class="sxs-lookup"><span data-stu-id="ce3af-189">If the PowerShell DSC Local Configuration Manager defaults match your use case, and you want to onboard machines such that they both pull from and report to Azure Automation DSC, the Azure Automation cmdlets provide a simplified method of generating the DSC metaconfigurations needed:</span></span>

1. <span data-ttu-id="ce3af-190">Ouvrez la console PowerShell ou PowerShell ISE en tant qu’administrateur sur un ordinateur de votre environnement local.</span><span class="sxs-lookup"><span data-stu-id="ce3af-190">Open the PowerShell console or PowerShell ISE as an administrator in a machine in your local environment.</span></span>
2. <span data-ttu-id="ce3af-191">Connectez-vous à Azure Resource Manager en utilisant **Add-AzureRmAccount**</span><span class="sxs-lookup"><span data-stu-id="ce3af-191">Connect to Azure Resource Manager using **Add-AzureRmAccount**</span></span>
3. <span data-ttu-id="ce3af-192">Téléchargez les métaconfigurations DSC PowerShell pour les machines à intégrer du compte Automation vers l’emplacement où vous voulez intégrer des nœuds :</span><span class="sxs-lookup"><span data-stu-id="ce3af-192">Download the PowerShell DSC metaconfigurations for the machines you want to onboard from the Automation account to which you want to onboard nodes:</span></span>

    ```powershell
    # Define the parameters for Get-AzureRmAutomationDscOnboardingMetaconfig using PowerShell Splatting
    $Params = @{

        ResourceGroupName = 'ContosoResources'; # The name of the ARM Resource Group that contains your Azure Automation Account
        AutomationAccountName = 'ContosoAutomation'; # The name of the Azure Automation Account where you want a node on-boarded to
        ComputerName = @('web01', 'web02', 'sql01'); # The names of the computers that the meta configuration will be generated for
        OutputFolder = "$env:UserProfile\Desktop\";
    }
    # Use PowerShell splatting to pass parameters to the Azure Automation cmdlet being invoked
    # For more info about splatting, run: Get-Help -Name about_Splatting
    Get-AzureRmAutomationDscOnboardingMetaconfig @Params
    ```
    
4. <span data-ttu-id="ce3af-193">Vous devez à présent avoir un dossier appelé ***DscMetaConfigs***contenant les métaconfigurations DSC PowerShell pour les machines à intégrer (en tant qu’administrateur) :</span><span class="sxs-lookup"><span data-stu-id="ce3af-193">You should now have a folder called ***DscMetaConfigs***, containing the PowerShell DSC metaconfigurations for the machines to onboard (as an administrator):</span></span>
    
    ```powershell
    Set-DscLocalConfigurationManager -Path $env:UserProfile\Desktop\DscMetaConfigs
    ```

## <a name="secure-registration"></a><span data-ttu-id="ce3af-194">Enregistrement sécurisé</span><span class="sxs-lookup"><span data-stu-id="ce3af-194">Secure registration</span></span>

<span data-ttu-id="ce3af-195">Les ordinateurs peuvent en toute sécurité s’intégrer à un compte Azure Automation via le protocole d’enregistrement WMF 5 DSC, qui permet à un nœud DSC de s’authentifier sur un serveur Pull ou Reporting PowerShell DSC V2 (y compris Azure Automation DSC).</span><span class="sxs-lookup"><span data-stu-id="ce3af-195">Machines can securely onboard to an Azure Automation account through the WMF 5 DSC registration protocol, which allows a DSC node to authenticate to a PowerShell DSC V2 Pull or Reporting server (including Azure Automation DSC).</span></span> <span data-ttu-id="ce3af-196">Le nœud s’enregistre sur le serveur au niveau d’une **URL d’inscription** et s’authentifie à l’aide d’une **clé d’inscription**.</span><span class="sxs-lookup"><span data-stu-id="ce3af-196">The node registers to the server at a **Registration URL**, authenticating using a **Registration key**.</span></span> <span data-ttu-id="ce3af-197">Pendant l’enregistrement, le nœud DSC et le serveur Pull / Reporting DSC négocient un certificat unique pour ce nœud qui devra être utilisé pour l’authentification au serveur après l’enregistrement.</span><span class="sxs-lookup"><span data-stu-id="ce3af-197">During registration, the DSC node and DSC Pull/Reporting server negotiate a unique certificate for this node to use for authentication to the server post-registration.</span></span> <span data-ttu-id="ce3af-198">Ce processus empêche les nœuds intégrés d’emprunter l’identité d’un autre nœud, par exemple si un nœud est compromis et agit à des fins malveillantes.</span><span class="sxs-lookup"><span data-stu-id="ce3af-198">This process prevents onboarded nodes from impersonating one another, such as if a node is compromised and behaving maliciously.</span></span> <span data-ttu-id="ce3af-199">Après l’enregistrement, la clé d’enregistrement n’est plus utilisée pour l’authentification et est supprimée du nœud.</span><span class="sxs-lookup"><span data-stu-id="ce3af-199">After registration, the Registration key is not used for authentication again, and is deleted from the node.</span></span>

<span data-ttu-id="ce3af-200">Pour obtenir les informations requises pour le protocole d’enregistrement DSC, accédez au panneau **Gérer les clés** du portail Azure en version préliminaire.</span><span class="sxs-lookup"><span data-stu-id="ce3af-200">You can get the information required for the DSC registration protocol from the **Manage Keys** blade in the Azure preview portal.</span></span> <span data-ttu-id="ce3af-201">Ouvrez ce panneau en cliquant sur l’icône de clé dans le panneau **Bases** du compte Automation.</span><span class="sxs-lookup"><span data-stu-id="ce3af-201">Open this blade by clicking the key icon on the **Essentials** panel for the Automation account.</span></span>

![](./media/automation-dsc-onboarding/DSC_Onboarding_4.png)

* <span data-ttu-id="ce3af-202">L’URL d’enregistrement correspond à la valeur du champ URL dans le panneau Gérer les clés.</span><span class="sxs-lookup"><span data-stu-id="ce3af-202">Registration URL is the URL field in the Manage Keys blade.</span></span>
* <span data-ttu-id="ce3af-203">La clé d’enregistrement correspond à la clé d’accès primaire ou à la clé d’accès secondaire dans le panneau Gérer les clés.</span><span class="sxs-lookup"><span data-stu-id="ce3af-203">Registration key is the Primary Access Key or Secondary Access Key in the Manage Keys blade.</span></span> <span data-ttu-id="ce3af-204">Vous pouvez utiliser l’une de ces deux clés.</span><span class="sxs-lookup"><span data-stu-id="ce3af-204">Either key can be used.</span></span>

<span data-ttu-id="ce3af-205">Pour renforcer la sécurité, les clés d’accès primaire et secondaire d’un compte Automation peuvent être régénérées à tout moment (à partir du panneau **Gérer les clés** ) pour éviter que des nœuds s’enregistrent ultérieurement à l’aide de clés déjà utilisées.</span><span class="sxs-lookup"><span data-stu-id="ce3af-205">For added security, the primary and secondary access keys of an Automation account can be regenerated at any time (on the **Manage Keys** blade) to prevent future node registrations using previous keys.</span></span>

## <a name="troubleshooting-azure-virtual-machine-onboarding"></a><span data-ttu-id="ce3af-206">Résolution des problèmes liés à l’intégration de machines virtuelles Azure</span><span class="sxs-lookup"><span data-stu-id="ce3af-206">Troubleshooting Azure virtual machine onboarding</span></span>

<span data-ttu-id="ce3af-207">Azure Automation DSC vous permet d’intégrer facilement des machines virtuelles Microsoft Azure à des fins de gestion de la configuration.</span><span class="sxs-lookup"><span data-stu-id="ce3af-207">Azure Automation DSC lets you easily onboard Azure Windows VMs for configuration management.</span></span> <span data-ttu-id="ce3af-208">En arrière-plan, l’extension Azure VM Desired State Configuration est utilisée pour enregistrer la machine virtuelle auprès d’Azure Automation DSC.</span><span class="sxs-lookup"><span data-stu-id="ce3af-208">Under the hood, the Azure VM Desired State Configuration extension is used to register the VM with Azure Automation DSC.</span></span> <span data-ttu-id="ce3af-209">Étant donné que cette extension s’exécute de façon asynchrone, il peut être très important d’en suivre la progression et de résoudre ses éventuels problèmes d’exécution.</span><span class="sxs-lookup"><span data-stu-id="ce3af-209">Since the Azure VM Desired State Configuration extension runs asynchronously, tracking its progress and troubleshooting its execution may be important.</span></span>

> [!NOTE]
> <span data-ttu-id="ce3af-210">Quelle que soit la méthode choisie pour intégrer une machine virtuelle Microsoft Azure sur Azure Automation DSC, l’enregistrement du nœud dans Azure Automation peut prendre jusqu’à une heure si l’extension Azure VM Desired State Configuration est utilisée.</span><span class="sxs-lookup"><span data-stu-id="ce3af-210">Any method of onboarding an Azure Windows VM to Azure Automation DSC that uses the Azure VM Desired State Configuration extension could take up to an hour for the node to show up as registered in Azure Automation.</span></span> <span data-ttu-id="ce3af-211">Cela est dû à l'installation de Windows Management Framework 5.0 sur la machine virtuelle par l'extension Azure VM DSC, nécessaire à l’intégration de la machine virtuelle dans Azure Automation DSC.</span><span class="sxs-lookup"><span data-stu-id="ce3af-211">This is due to the installation of Windows Management Framework 5.0 on the VM by the Azure VM DSC extension, which is required to onboard the VM to Azure Automation DSC.</span></span>

<span data-ttu-id="ce3af-212">Pour résoudre les problèmes ou afficher l’état de l’extension Azure VM Desired State Configuration, rendez-vous dans le portail Azure, accédez à la machine virtuelle en cours d’intégration, puis cliquez sur **Tous les paramètres** -> **Extensions** -> **DSC**.</span><span class="sxs-lookup"><span data-stu-id="ce3af-212">To troubleshoot or view the status of the Azure VM Desired State Configuration extension, in the Azure portal navigate to the VM being onboarded, then click -> **All settings** -> **Extensions** -> **DSC**.</span></span> <span data-ttu-id="ce3af-213">Pour plus de détails, vous pouvez cliquer sur **Afficher l’état détaillé**.</span><span class="sxs-lookup"><span data-stu-id="ce3af-213">For more details, you can click **View detailed status**.</span></span>

[![](./media/automation-dsc-onboarding/DSC_Onboarding_5.png)](https://technet.microsoft.com/library/dn249912.aspx)

## <a name="certificate-expiration-and-reregistration"></a><span data-ttu-id="ce3af-214">Expiration du certificat et nouvel enregistrement</span><span class="sxs-lookup"><span data-stu-id="ce3af-214">Certificate expiration and reregistration</span></span>

<span data-ttu-id="ce3af-215">Après avoir inscrit un ordinateur en tant que nœud DSC dans Azure Automation DSC, il se peut que vous ayez besoin de revenir en arrière pour de multiples raisons :</span><span class="sxs-lookup"><span data-stu-id="ce3af-215">After registering a machine as a DSC node in Azure Automation DSC, there are a number of reasons why you may need to reregister that node in the future:</span></span>

* <span data-ttu-id="ce3af-216">Une fois inscrit, chaque nœud négocie automatiquement un certificat unique pour l'authentification qui expire après un an.</span><span class="sxs-lookup"><span data-stu-id="ce3af-216">After registering, each node automatically negotiates a unique certificate for authentication that expires after one year.</span></span> <span data-ttu-id="ce3af-217">À ce stade, le protocole d’inscription PowerShell DSC ne peut pas renouveler automatiquement les certificats lorsqu’ils sont sur le point d’expirer. Vous devez donc renouveler l’inscription des nœuds après un an.</span><span class="sxs-lookup"><span data-stu-id="ce3af-217">Currently, the PowerShell DSC registration protocol cannot automatically renew certificates when they are nearing expiration, so you need to reregister the nodes after a year's time.</span></span> <span data-ttu-id="ce3af-218">Avant la réinscription, assurez-vous que chaque nœud exécute Windows Management Framework 5.0 RTM.</span><span class="sxs-lookup"><span data-stu-id="ce3af-218">Before reregistering, ensure that each node is running Windows Management Framework 5.0 RTM.</span></span> <span data-ttu-id="ce3af-219">Si le certificat d’authentification d’un nœud expire et si le nœud n’est pas réinscrit, le nœud ne pourra pas communiquer avec Azure Automation et sera marqué « Ne répond pas ».</span><span class="sxs-lookup"><span data-stu-id="ce3af-219">If a node's authentication certificate expires, and the node is not reregistered, the node will be unable to communicate with Azure Automation and will be marked 'Unresponsive.'</span></span> <span data-ttu-id="ce3af-220">La réinscription effectuée dans un délai de 90 jours ou moins à partir de l'heure d'expiration du certificat, ou à tout moment après le délai d'expiration du certificat, entraîne la génération et l'utilisation d'un nouveau certificat.</span><span class="sxs-lookup"><span data-stu-id="ce3af-220">Reregistration performed 90 days or less from the certificate expiration time, or at any point after the certificate expiration time, will result in a new certificate being generated and used.</span></span>
* <span data-ttu-id="ce3af-221">Pour modifier des [valeurs du gestionnaire de configuration local PowerShell DSC](https://msdn.microsoft.com/powershell/dsc/metaconfig4) qui ont été définies lors de l’inscription initiale du nœud, telles que ConfigurationMode.</span><span class="sxs-lookup"><span data-stu-id="ce3af-221">To change any [PowerShell DSC Local Configuration Manager values](https://msdn.microsoft.com/powershell/dsc/metaconfig4) that were set during initial registration of the node, such as ConfigurationMode.</span></span> <span data-ttu-id="ce3af-222">Actuellement, ces valeurs de l’agent DSC peuvent être modifiées uniquement via une désinscription.</span><span class="sxs-lookup"><span data-stu-id="ce3af-222">Currently, these DSC agent values can only be changed through reregistration.</span></span> <span data-ttu-id="ce3af-223">La seule exception concerne la configuration du nœud assignée au nœud, qui peut être modifiée directement dans Azure Automation DSC.</span><span class="sxs-lookup"><span data-stu-id="ce3af-223">The one exception is the Node Configuration assigned to the node -- this can be changed in Azure Automation DSC directly.</span></span>

<span data-ttu-id="ce3af-224">L’inscription peut être renouvelée selon la procédure initiale, en utilisant l’une des méthodes d’intégration décrites dans ce document.</span><span class="sxs-lookup"><span data-stu-id="ce3af-224">Reregistration can be performed in the same way you registered the node initially, using any of the onboarding methods described in this document.</span></span> <span data-ttu-id="ce3af-225">Il est inutile d’annuler l’inscription d’un nœud dans Azure Automation DSC avant de le réinscrire.</span><span class="sxs-lookup"><span data-stu-id="ce3af-225">You do not need to unregister a node from Azure Automation DSC before reregistering it.</span></span>

## <a name="related-articles"></a><span data-ttu-id="ce3af-226">Articles connexes</span><span class="sxs-lookup"><span data-stu-id="ce3af-226">Related Articles</span></span>

* [<span data-ttu-id="ce3af-227">Vue d’ensemble d’Azure Automation DSC</span><span class="sxs-lookup"><span data-stu-id="ce3af-227">Azure Automation DSC overview</span></span>](automation-dsc-overview.md)
* [<span data-ttu-id="ce3af-228">Applets de commande Azure Automation DSC</span><span class="sxs-lookup"><span data-stu-id="ce3af-228">Azure Automation DSC cmdlets</span></span>](/powershell/module/azurerm.automation/#automation)
* [<span data-ttu-id="ce3af-229">Tarification d’Azure Automation DSC</span><span class="sxs-lookup"><span data-stu-id="ce3af-229">Azure Automation DSC pricing</span></span>](https://azure.microsoft.com/pricing/details/automation/)
