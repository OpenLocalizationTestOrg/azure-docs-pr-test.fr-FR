---
title: "fonctionnalités et extensions de l’ordinateur aaaVirtual pour Windows dans Azure | Documents Microsoft"
description: "Découvrez les extensions disponibles pour les machines virtuelles, regroupées par ce qu’ils fournissent ou améliorent."
services: virtual-machines-windows
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: 999d63ee-890e-432e-9391-25b3fc6cde28
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 03/06/2017
ms.author: nepeters
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 61ccfd696b38e9be1026d836d5796c2346fd650f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="virtual-machine-extensions-and-features-for-windows"></a><span data-ttu-id="e05e2-103">Extensions et fonctionnalités de machine virtuelle pour Windows</span><span class="sxs-lookup"><span data-stu-id="e05e2-103">Virtual machine extensions and features for Windows</span></span>

<span data-ttu-id="e05e2-104">Les extensions de machine virtuelle Azure sont de petites applications permettant d’exécuter des tâches de configuration et d’automatisation post-déploiement sur des machines virtuelles Azure.</span><span class="sxs-lookup"><span data-stu-id="e05e2-104">Azure virtual machine extensions are small applications that provide post-deployment configuration and automation tasks on Azure virtual machines.</span></span> <span data-ttu-id="e05e2-105">Par exemple, si un ordinateur virtuel requiert l’installation du logiciel, de protection antivirus ou de configuration de Docker, une extension de machine virtuelle peut être utilisé toocomplete ces tâches.</span><span class="sxs-lookup"><span data-stu-id="e05e2-105">For example, if a virtual machine requires software installation, anti-virus protection, or Docker configuration, a VM extension can be used toocomplete these tasks.</span></span> <span data-ttu-id="e05e2-106">Les extensions de machine virtuelle Azure peuvent être exécutées à l’aide de hello CLI d’Azure PowerShell, les modèles Azure Resource Manager et hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="e05e2-106">Azure VM extensions can be run by using hello Azure CLI, PowerShell, Azure Resource Manager templates, and hello Azure portal.</span></span> <span data-ttu-id="e05e2-107">Les extensions peuvent être associées à un nouveau déploiement de machine virtuelle ou s’exécuter sur tout système existant.</span><span class="sxs-lookup"><span data-stu-id="e05e2-107">Extensions can be bundled with a new virtual machine deployment or run against any existing system.</span></span>

<span data-ttu-id="e05e2-108">Ce document fournit une vue d’ensemble des extensions de machine virtuelle, les conditions préalables pour l’utilisation des extensions de machine virtuelle et de conseils toodetect, gérer et supprimer des extensions de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="e05e2-108">This document provides an overview of virtual machine extensions, prerequisites for using virtual machine extensions, and guidance on how toodetect, manage, and remove virtual machine extensions.</span></span> <span data-ttu-id="e05e2-109">Ce document fournit des informations générales, car de nombreuses extensions de machine virtuelle sont disponibles, chacune présentant une configuration potentiellement unique.</span><span class="sxs-lookup"><span data-stu-id="e05e2-109">This document provides generalized information because many VM extensions are available, each with a potentially unique configuration.</span></span> <span data-ttu-id="e05e2-110">Vous trouverez plus d’informations spécifiques à l’extension dans chaque document spécifique toohello individuels d’extension.</span><span class="sxs-lookup"><span data-stu-id="e05e2-110">Extension-specific details can be found in each document specific toohello individual extension.</span></span>

## <a name="use-cases-and-samples"></a><span data-ttu-id="e05e2-111">Cas d’utilisation et exemples</span><span class="sxs-lookup"><span data-stu-id="e05e2-111">Use cases and samples</span></span>

<span data-ttu-id="e05e2-112">Plusieurs extensions de machine virtuelle Azure sont disponibles, chacune impliquant un cas d’utilisation spécifique.</span><span class="sxs-lookup"><span data-stu-id="e05e2-112">There are many different Azure VM extensions available, each with a specific use case.</span></span> <span data-ttu-id="e05e2-113">Exemples de cas d’utilisation :</span><span class="sxs-lookup"><span data-stu-id="e05e2-113">Some example use cases are:</span></span>

- <span data-ttu-id="e05e2-114">Appliquer l’état souhaité de PowerShell configurations tooa virtual machine pour Windows à l’aide d’extension de hello DSC.</span><span class="sxs-lookup"><span data-stu-id="e05e2-114">Apply PowerShell Desired State configurations tooa virtual machine by using hello DSC extension for Windows.</span></span> <span data-ttu-id="e05e2-115">Pour plus d’informations sur l’extension DSC Azure, consultez [cette page](extensions-dsc-overview.md).</span><span class="sxs-lookup"><span data-stu-id="e05e2-115">For more information, see [Azure Desired State configuration extension](extensions-dsc-overview.md).</span></span>
- <span data-ttu-id="e05e2-116">Configurer la surveillance de machine virtuelle à l’aide d’extension de VM de l’Agent de surveillance Microsoft hello.</span><span class="sxs-lookup"><span data-stu-id="e05e2-116">Configure virtual machine monitoring by using hello Microsoft Monitoring Agent VM extension.</span></span> <span data-ttu-id="e05e2-117">Pour plus d’informations, consultez [tooLog de machines virtuelles Azure de se connecter Analytique](../../log-analytics/log-analytics-azure-vm-extension.md).</span><span class="sxs-lookup"><span data-stu-id="e05e2-117">For more information, see [Connect Azure virtual machines tooLog Analytics](../../log-analytics/log-analytics-azure-vm-extension.md).</span></span>
- <span data-ttu-id="e05e2-118">Configurer la surveillance de votre infrastructure d’Azure avec hello Datadog extension.</span><span class="sxs-lookup"><span data-stu-id="e05e2-118">Configure monitoring of your Azure infrastructure with hello Datadog extension.</span></span> <span data-ttu-id="e05e2-119">Pour plus d’informations, consultez hello [Datadog blog](https://www.datadoghq.com/blog/introducing-azure-monitoring-with-one-click-datadog-deployment/).</span><span class="sxs-lookup"><span data-stu-id="e05e2-119">For more information, see hello [Datadog blog](https://www.datadoghq.com/blog/introducing-azure-monitoring-with-one-click-datadog-deployment/).</span></span>
- <span data-ttu-id="e05e2-120">Configurer une machine virtuelle Azure à l’aide de Chef.</span><span class="sxs-lookup"><span data-stu-id="e05e2-120">Configure an Azure virtual machine by using Chef.</span></span> <span data-ttu-id="e05e2-121">Pour plus d’informations, consultez [Automatisation du déploiement de machine virtuelle Azure avec Chef](chef-automation.md).</span><span class="sxs-lookup"><span data-stu-id="e05e2-121">For more information, see [Automating Azure virtual machine deployment with Chef](chef-automation.md).</span></span>

<span data-ttu-id="e05e2-122">En outre extensions tooprocess spécifiques, une extension de Script personnalisé est disponible pour les machines virtuelles Windows et Linux.</span><span class="sxs-lookup"><span data-stu-id="e05e2-122">In addition tooprocess-specific extensions, a Custom Script extension is available for both Windows and Linux virtual machines.</span></span> <span data-ttu-id="e05e2-123">Hello extension de Script personnalisé pour Windows permet à n’importe quel toobe de script PowerShell s’exécutent sur un ordinateur virtuel.</span><span class="sxs-lookup"><span data-stu-id="e05e2-123">hello Custom Script extension for Windows allows any PowerShell script toobe run on a virtual machine.</span></span> <span data-ttu-id="e05e2-124">Cela s’avère utile pour concevoir des déploiements Azure qui nécessitent une configuration plus avancée que celle permise par les outils Azure.</span><span class="sxs-lookup"><span data-stu-id="e05e2-124">This is useful when you're designing Azure deployments that require configuration beyond what native Azure tooling can provide.</span></span> <span data-ttu-id="e05e2-125">Pour plus d’informations sur l’extension de script personnalisé pour les machines virtuelles Windows, consultez [cet article](extensions-customscript.md).</span><span class="sxs-lookup"><span data-stu-id="e05e2-125">For more information, see [Windows VM Custom Script extension](extensions-customscript.md).</span></span>


## <a name="prerequisites"></a><span data-ttu-id="e05e2-126">Composants requis</span><span class="sxs-lookup"><span data-stu-id="e05e2-126">Prerequisites</span></span>

<span data-ttu-id="e05e2-127">Chaque extension de machine virtuelle peut présenter son propre ensemble de composants requis.</span><span class="sxs-lookup"><span data-stu-id="e05e2-127">Each virtual machine extension may have its own set of prerequisites.</span></span> <span data-ttu-id="e05e2-128">Par exemple, hello extension de machine virtuelle de Docker a une condition préalable d’une distribution Linux pris en charge.</span><span class="sxs-lookup"><span data-stu-id="e05e2-128">For instance, hello Docker VM extension has a prerequisite of a supported Linux distribution.</span></span> <span data-ttu-id="e05e2-129">Configuration requise des extensions individuelles est détaillées dans la documentation spécifique à l’extension de hello.</span><span class="sxs-lookup"><span data-stu-id="e05e2-129">Requirements of individual extensions are detailed in hello extension-specific documentation.</span></span>

### <a name="azure-vm-agent"></a><span data-ttu-id="e05e2-130">Agent de machine virtuelle Azure</span><span class="sxs-lookup"><span data-stu-id="e05e2-130">Azure VM agent</span></span>
<span data-ttu-id="e05e2-131">l’agent de machine virtuelle Azure Hello gère l’interaction entre une machine virtuelle Azure et le contrôleur de structure Azure hello.</span><span class="sxs-lookup"><span data-stu-id="e05e2-131">hello Azure VM agent manages interaction between an Azure virtual machine and hello Azure fabric controller.</span></span> <span data-ttu-id="e05e2-132">agent de machine virtuelle Hello est chargé de nombreux aspects fonctionnels de déploiement et la gestion des machines virtuelles Azure, y compris les extensions de machine virtuelle en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="e05e2-132">hello VM agent is responsible for many functional aspects of deploying and managing Azure virtual machines, including running VM extensions.</span></span> <span data-ttu-id="e05e2-133">l’agent de machine virtuelle Azure Hello est préinstallé sur les images Azure Marketplace et peut être installé sur les systèmes d’exploitation pris en charge.</span><span class="sxs-lookup"><span data-stu-id="e05e2-133">hello Azure VM agent is preinstalled on Azure Marketplace images and can be installed on supported operating systems.</span></span>

<span data-ttu-id="e05e2-134">Pour plus d’informations sur les systèmes d’exploitation pris en charge et sur la procédure d’installation, consultez l’article [Agent de machine virtuelle et extensions Azure](agent-user-guide.md).</span><span class="sxs-lookup"><span data-stu-id="e05e2-134">For information on supported operating systems and installation instructions, see [Azure virtual machine agent](agent-user-guide.md).</span></span>

## <a name="discover-vm-extensions"></a><span data-ttu-id="e05e2-135">Détecter les extensions de machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="e05e2-135">Discover VM extensions</span></span>
<span data-ttu-id="e05e2-136">De nombreuses extensions de machine virtuelle différentes peuvent être utilisées avec les machines virtuelles Azure.</span><span class="sxs-lookup"><span data-stu-id="e05e2-136">Many different VM extensions are available for use with Azure virtual machines.</span></span> <span data-ttu-id="e05e2-137">toosee une liste complète, exécutez hello commande avec le module de hello Azure Resource Manager PowerShell suivante.</span><span class="sxs-lookup"><span data-stu-id="e05e2-137">toosee a complete list, run hello following command with hello Azure Resource Manager PowerShell module.</span></span> <span data-ttu-id="e05e2-138">Transformer en emplacement de hello souhaité toospecify que lorsque vous exécutez cette commande.</span><span class="sxs-lookup"><span data-stu-id="e05e2-138">Make sure toospecify hello desired location when you're running this command.</span></span>

```powershell
Get-AzureRmVmImagePublisher -Location WestUS | `
Get-AzureRmVMExtensionImageType | `
Get-AzureRmVMExtensionImage | Select Type, Version
```

## <a name="run-vm-extensions"></a><span data-ttu-id="e05e2-139">Exécuter les extensions de machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="e05e2-139">Run VM extensions</span></span>

<span data-ttu-id="e05e2-140">Extensions de machine virtuelle Azure peuvent être exécutées sur des ordinateurs virtuels existants, ce qui est utile lorsque vous avez besoin de modifications de configuration toomake ou restaurer la connectivité sur une machine virtuelle déjà déployée.</span><span class="sxs-lookup"><span data-stu-id="e05e2-140">Azure virtual machine extensions can be run on existing virtual machines, which is useful when you need toomake configuration changes or recover connectivity on an already deployed VM.</span></span> <span data-ttu-id="e05e2-141">Les extensions de machines virtuelles peuvent également être intégrées dans des déploiements de modèles Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="e05e2-141">VM extensions can also be bundled with Azure Resource Manager template deployments.</span></span> <span data-ttu-id="e05e2-142">À l’aide des extensions avec des modèles de gestionnaire de ressources, vous pouvez activer toobe de machines virtuelles déployés et configurés sans hello intervention de post-déploiement.</span><span class="sxs-lookup"><span data-stu-id="e05e2-142">By using extensions with Resource Manager templates, you can enable Azure virtual machines toobe deployed and configured without hello need for post-deployment intervention.</span></span>

<span data-ttu-id="e05e2-143">Hello méthodes suivantes peut être utilisée toorun une extension sur un ordinateur virtuel existant.</span><span class="sxs-lookup"><span data-stu-id="e05e2-143">hello following methods can be used toorun an extension against an existing virtual machine.</span></span>

### <a name="powershell"></a><span data-ttu-id="e05e2-144">PowerShell</span><span class="sxs-lookup"><span data-stu-id="e05e2-144">PowerShell</span></span>

<span data-ttu-id="e05e2-145">Il existe plusieurs commandes PowerShell pour l’exécution des extensions.</span><span class="sxs-lookup"><span data-stu-id="e05e2-145">Several PowerShell commands exist for running individual extensions.</span></span> <span data-ttu-id="e05e2-146">toosee obtenir la liste, exécutez hello suivant de commandes PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e05e2-146">toosee a list, run hello following PowerShell commands.</span></span>

```powershell
get-command Set-AzureRM*Extension* -Module AzureRM.Compute
```

<span data-ttu-id="e05e2-147">Cela fournit suivant toohello similaire de sortie :</span><span class="sxs-lookup"><span data-stu-id="e05e2-147">This provides output similar toohello following:</span></span>

```powershell
CommandType     Name                                               Version    Source
-----------     ----                                               -------    ------
Cmdlet          Set-AzureRmVMAccessExtension                       2.2.0      AzureRM.Compute
Cmdlet          Set-AzureRmVMADDomainExtension                     2.2.0      AzureRM.Compute
Cmdlet          Set-AzureRmVMAEMExtension                          2.2.0      AzureRM.Compute
Cmdlet          Set-AzureRmVMBackupExtension                       2.2.0      AzureRM.Compute
Cmdlet          Set-AzureRmVMBginfoExtension                       2.2.0      AzureRM.Compute
Cmdlet          Set-AzureRmVMChefExtension                         2.2.0      AzureRM.Compute
Cmdlet          Set-AzureRmVMCustomScriptExtension                 2.2.0      AzureRM.Compute
Cmdlet          Set-AzureRmVMDiagnosticsExtension                  2.2.0      AzureRM.Compute
Cmdlet          Set-AzureRmVMDiskEncryptionExtension               2.2.0      AzureRM.Compute
Cmdlet          Set-AzureRmVMDscExtension                          2.2.0      AzureRM.Compute
Cmdlet          Set-AzureRmVMExtension                             2.2.0      AzureRM.Compute
Cmdlet          Set-AzureRmVMSqlServerExtension                    2.2.0      AzureRM.Compute
```

<span data-ttu-id="e05e2-148">Hello exemple suivant utilise toodownload extension de Script personnalisé hello un script à partir d’un référentiel GitHub sur la machine virtuelle cible hello et puis exécutez le script de hello.</span><span class="sxs-lookup"><span data-stu-id="e05e2-148">hello following example uses hello Custom Script extension toodownload a script from a GitHub repository onto hello target virtual machine and then run hello script.</span></span> <span data-ttu-id="e05e2-149">Pour plus d’informations sur l’extension de Script personnalisé de hello, consultez [vue d’ensemble des extensions de Script personnalisé](extensions-customscript.md).</span><span class="sxs-lookup"><span data-stu-id="e05e2-149">For more information on hello Custom Script extension, see [Custom Script extension overview](extensions-customscript.md).</span></span>

```powershell
Set-AzureRmVMCustomScriptExtension -ResourceGroupName "myResourceGroup" `
    -VMName "myVM" -Name "myCustomScript" `
    -FileUri "https://raw.githubusercontent.com/neilpeterson/nepeters-azure-templates/master/windows-custom-script-simple/support-scripts/Create-File.ps1" `
    -Run "Create-File.ps1" -Location "West US"
```

<span data-ttu-id="e05e2-150">Dans cet exemple, hello extension d’accès de la machine virtuelle est le mot de passe utilisé tooreset hello d’administration d’une machine virtuelle Windows.</span><span class="sxs-lookup"><span data-stu-id="e05e2-150">In this example, hello VM Access extension is used tooreset hello administrative password of a Windows virtual machine.</span></span> <span data-ttu-id="e05e2-151">Pour plus d’informations sur hello extension d’accès de la machine virtuelle, consultez [service réinitialiser le Bureau à distance dans une machine virtuelle Windows](reset-rdp.md).</span><span class="sxs-lookup"><span data-stu-id="e05e2-151">For more information on hello VM Access extension, see [Reset Remote Desktop service in a Windows VM](reset-rdp.md).</span></span>

```powershell
$cred=Get-Credential

Set-AzureRmVMAccessExtension -ResourceGroupName "myResourceGroup" -VMName "myVM" -Name "myVMAccess" `
    -Location WestUS -UserName $cred.GetNetworkCredential().Username `
    -Password $cred.GetNetworkCredential().Password -typeHandlerVersion "2.0"
```

<span data-ttu-id="e05e2-152">Hello `Set-AzureRmVMExtension` commande peut être utilisé toostart n’importe quelle extension de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="e05e2-152">hello `Set-AzureRmVMExtension` command can be used toostart any VM extension.</span></span> <span data-ttu-id="e05e2-153">Pour plus d’informations, consultez hello [Set-AzureRmVMExtension référence](https://msdn.microsoft.com/en-us/library/mt603745.aspx).</span><span class="sxs-lookup"><span data-stu-id="e05e2-153">For more information, see hello [Set-AzureRmVMExtension reference](https://msdn.microsoft.com/en-us/library/mt603745.aspx).</span></span>


### <a name="azure-portal"></a><span data-ttu-id="e05e2-154">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="e05e2-154">Azure portal</span></span>

<span data-ttu-id="e05e2-155">Une extension de machine virtuelle peut être appliqué tooan une machine virtuelle existante via hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="e05e2-155">A VM extension can be applied tooan existing virtual machine through hello Azure portal.</span></span> <span data-ttu-id="e05e2-156">toodo par conséquent, activez la machine virtuelle de hello vous souhaitez toouse, choisissez **Extensions**, puis cliquez sur **ajouter**.</span><span class="sxs-lookup"><span data-stu-id="e05e2-156">toodo so, select hello virtual machine you want toouse, choose **Extensions**, and click **Add**.</span></span> <span data-ttu-id="e05e2-157">La liste des extensions disponibles s’affiche.</span><span class="sxs-lookup"><span data-stu-id="e05e2-157">This provides a list of available extensions.</span></span> <span data-ttu-id="e05e2-158">Sélectionnez hello une souhaité et suivez les étapes de hello dans l’Assistant de hello.</span><span class="sxs-lookup"><span data-stu-id="e05e2-158">Select hello one you want and follow hello steps in hello wizard.</span></span>

<span data-ttu-id="e05e2-159">Hello image suivante montre installation hello Hello extension Microsoft Antimalware de hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="e05e2-159">hello following image shows hello installation of hello Microsoft Antimalware extension from hello Azure portal.</span></span>

![Installer l’extension Antimalware](./media/extensions-features/installantimalwareextension.png)

### <a name="azure-resource-manager-templates"></a><span data-ttu-id="e05e2-161">Modèles Microsoft Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="e05e2-161">Azure Resource Manager templates</span></span>

<span data-ttu-id="e05e2-162">Extensions de machine virtuelle peuvent être ajoutée tooan Azure Resource Manager modèle et exécutée avec un déploiement hello du modèle de hello.</span><span class="sxs-lookup"><span data-stu-id="e05e2-162">VM extensions can be added tooan Azure Resource Manager template and executed with hello deployment of hello template.</span></span> <span data-ttu-id="e05e2-163">Le déploiement d’extensions avec un modèle permet de créer des déploiements Azure entièrement configurés.</span><span class="sxs-lookup"><span data-stu-id="e05e2-163">Deploying extensions with a template is useful for creating fully configured Azure deployments.</span></span> <span data-ttu-id="e05e2-164">Par exemple, hello que JSON suivant est tiré d’un modèle de gestionnaire de ressources qui déploie un ensemble de l’équilibrage de la charge des machines virtuelles et d’une base de données SQL Azure, puis installe une application .NET Core sur chaque machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="e05e2-164">For example, hello following JSON is taken from a Resource Manager template that deploys a set of load-balanced virtual machines and an Azure SQL database, and then installs a .NET Core application on each VM.</span></span> <span data-ttu-id="e05e2-165">prend en charge de l’installation du logiciel hello Hello extension de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="e05e2-165">hello VM extension takes care of hello software installation.</span></span>

<span data-ttu-id="e05e2-166">Pour plus d’informations, consultez hello [modèle de gestionnaire de ressources complet](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows).</span><span class="sxs-lookup"><span data-stu-id="e05e2-166">For more information, see hello [full Resource Manager template](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows).</span></span>

```json
{
    "apiVersion": "2015-06-15",
    "type": "extensions",
    "name": "config-app",
    "location": "[resourceGroup().location]",
    "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'),copyindex())]",
    "[variables('musicstoresqlName')]"
    ],
    "tags": {
    "displayName": "config-app"
    },
    "properties": {
    "publisher": "Microsoft.Compute",
    "type": "CustomScriptExtension",
    "typeHandlerVersion": "1.4",
    "autoUpgradeMinorVersion": true,
    "settings": {
        "fileUris": [
        "https://raw.githubusercontent.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-windows/scripts/configure-music-app.ps1"
        ]
    },
    "protectedSettings": {
        "commandToExecute": "[concat('powershell -ExecutionPolicy Unrestricted -File configure-music-app.ps1 -user ',parameters('adminUsername'),' -password ',parameters('adminPassword'),' -sqlserver ',variables('musicstoresqlName'),'.database.windows.net')]"
    }
    }
}
```

<span data-ttu-id="e05e2-167">Pour plus d’informations, consultez l’article [Création de modèles Azure Resource Manager avec des extensions de machine virtuelle Windows](template-description.md#extensions).</span><span class="sxs-lookup"><span data-stu-id="e05e2-167">For more information, see [Authoring Azure Resource Manager templates with Windows VM extensions](template-description.md#extensions).</span></span>

## <a name="secure-vm-extension-data"></a><span data-ttu-id="e05e2-168">Sécuriser les données des extensions de machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="e05e2-168">Secure VM extension data</span></span>

<span data-ttu-id="e05e2-169">Lorsque vous exécutez une extension de machine virtuelle, il peut être nécessaire de tooinclude des informations sensibles telles que les informations d’identification, les noms de compte de stockage et les clés d’accès de compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="e05e2-169">When you're running a VM extension, it may be necessary tooinclude sensitive information such as credentials, storage account names, and storage account access keys.</span></span> <span data-ttu-id="e05e2-170">Plusieurs extensions de machine virtuelle incluent une configuration protégée qui chiffre les données et la déchiffre uniquement à l’intérieur de la machine virtuelle cible hello.</span><span class="sxs-lookup"><span data-stu-id="e05e2-170">Many VM extensions include a protected configuration that encrypts data and only decrypts it inside hello target virtual machine.</span></span> <span data-ttu-id="e05e2-171">Chaque extension possède un schéma spécifique de configuration protégée qui sera présenté en détail dans la documentation consacrée à l’extension.</span><span class="sxs-lookup"><span data-stu-id="e05e2-171">Each extension has a specific protected configuration schema that will be detailed in extension-specific documentation.</span></span>

<span data-ttu-id="e05e2-172">Bonjour à l’exemple suivant montre une instance de hello extension de Script personnalisé pour Windows.</span><span class="sxs-lookup"><span data-stu-id="e05e2-172">hello following example shows an instance of hello Custom Script extension for Windows.</span></span> <span data-ttu-id="e05e2-173">Notez que tooexecute de commande hello comprend un ensemble d’informations d’identification.</span><span class="sxs-lookup"><span data-stu-id="e05e2-173">Notice that hello command tooexecute includes a set of credentials.</span></span> <span data-ttu-id="e05e2-174">Dans cet exemple, hello commande tooexecute n’est pas chiffrée.</span><span class="sxs-lookup"><span data-stu-id="e05e2-174">In this example, hello command tooexecute will not be encrypted.</span></span>


```json
{
    "apiVersion": "2015-06-15",
    "type": "extensions",
    "name": "config-app",
    "location": "[resourceGroup().location]",
    "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'),copyindex())]",
    "[variables('musicstoresqlName')]"
    ],
    "tags": {
    "displayName": "config-app"
    },
    "properties": {
    "publisher": "Microsoft.Compute",
    "type": "CustomScriptExtension",
    "typeHandlerVersion": "1.4",
    "autoUpgradeMinorVersion": true,
    "settings": {
        "fileUris": [
        "https://raw.githubusercontent.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-windows/scripts/configure-music-app.ps1"
        ],
        "commandToExecute": "[concat('powershell -ExecutionPolicy Unrestricted -File configure-music-app.ps1 -user ',parameters('adminUsername'),' -password ',parameters('adminPassword'),' -sqlserver ',variables('musicstoresqlName'),'.database.windows.net')]"
    }
    }
}
```

<span data-ttu-id="e05e2-175">Protéger la chaîne de l’exécution de hello en déplaçant hello **commande tooexecute** propriété toohello **protégé** configuration.</span><span class="sxs-lookup"><span data-stu-id="e05e2-175">Secure hello execution string by moving hello **command tooexecute** property toohello **protected** configuration.</span></span>

```json
{
    "apiVersion": "2015-06-15",
    "type": "extensions",
    "name": "config-app",
    "location": "[resourceGroup().location]",
    "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'),copyindex())]",
    "[variables('musicstoresqlName')]"
    ],
    "tags": {
    "displayName": "config-app"
    },
    "properties": {
    "publisher": "Microsoft.Compute",
    "type": "CustomScriptExtension",
    "typeHandlerVersion": "1.4",
    "autoUpgradeMinorVersion": true,
    "settings": {
        "fileUris": [
        "https://raw.githubusercontent.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-windows/scripts/configure-music-app.ps1"
        ]
    },
    "protectedSettings": {
        "commandToExecute": "[concat('powershell -ExecutionPolicy Unrestricted -File configure-music-app.ps1 -user ',parameters('adminUsername'),' -password ',parameters('adminPassword'),' -sqlserver ',variables('musicstoresqlName'),'.database.windows.net')]"
    }
    }
}
```

## <a name="troubleshoot-vm-extensions"></a><span data-ttu-id="e05e2-176">Résoudre les problèmes liés aux extensions de machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="e05e2-176">Troubleshoot VM extensions</span></span>

<span data-ttu-id="e05e2-177">Chaque extension de machine virtuelle peut présenter une procédure de résolution des problèmes spécifique.</span><span class="sxs-lookup"><span data-stu-id="e05e2-177">Each VM extension may have specific troubleshooting steps.</span></span> <span data-ttu-id="e05e2-178">Par exemple, lorsque vous utilisez l’extension de Script personnalisé hello, détails de l’exécution de script sont accessibles localement sur l’ordinateur virtuel de hello sur lequel l’extension de hello a été exécutée.</span><span class="sxs-lookup"><span data-stu-id="e05e2-178">For instance, when you're using hello Custom Script extension, script execution details can be found locally on hello virtual machine on which hello extension was run.</span></span> <span data-ttu-id="e05e2-179">La procédure de résolution des problèmes spécifique d’une extension est présentée en détail dans la documentation de cette dernière.</span><span class="sxs-lookup"><span data-stu-id="e05e2-179">Any extension-specific troubleshooting steps are detailed in extension-specific documentation.</span></span>

<span data-ttu-id="e05e2-180">Hello suivant les étapes de dépannage s’appliquent à des extensions de machine virtuelle tooall.</span><span class="sxs-lookup"><span data-stu-id="e05e2-180">hello following troubleshooting steps apply tooall virtual machine extensions.</span></span>

### <a name="view-extension-status"></a><span data-ttu-id="e05e2-181">Afficher l’état de l’extension</span><span class="sxs-lookup"><span data-stu-id="e05e2-181">View extension status</span></span>

<span data-ttu-id="e05e2-182">Une fois une extension de machine virtuelle a été exécutée sur un ordinateur virtuel, utilisez hello suivant l’état de l’extension tooreturn commande PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e05e2-182">After a virtual machine extension has been run against a virtual machine, use hello following PowerShell command tooreturn extension status.</span></span> <span data-ttu-id="e05e2-183">Remplacez les exemples de noms de paramètre par vos propres valeurs.</span><span class="sxs-lookup"><span data-stu-id="e05e2-183">Replace example parameter names with your own values.</span></span> <span data-ttu-id="e05e2-184">Hello `Name` paramètre prend le nom hello toohello extension au moment de l’exécution.</span><span class="sxs-lookup"><span data-stu-id="e05e2-184">hello `Name` parameter takes hello name given toohello extension at execution time.</span></span>

```PowerShell
Get-AzureRmVMExtension -ResourceGroupName myResourceGroup -VMName myVM -Name myExtensionName
```

<span data-ttu-id="e05e2-185">sortie de Hello ressemble à hello suivantes :</span><span class="sxs-lookup"><span data-stu-id="e05e2-185">hello output looks like hello following:</span></span>

```json
ResourceGroupName       : myResourceGroup
VMName                  : myVM
Name                    : myExtensionName
Location                : westus
Etag                    : null
Publisher               : Microsoft.Azure.Extensions
ExtensionType           : DockerExtension
TypeHandlerVersion      : 1.0
Id                      : /subscriptions/mySubscriptionIS/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachines/myVM/extensions/myExtensionName
PublicSettings          :
ProtectedSettings       :
ProvisioningState       : Succeeded
Statuses                :
SubStatuses             :
AutoUpgradeMinorVersion : False
ForceUpdateTag          :
```

<span data-ttu-id="e05e2-186">État d’exécution de l’extension peut également trouver dans hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="e05e2-186">Extension execution status can also be found in hello Azure portal.</span></span> <span data-ttu-id="e05e2-187">état de hello tooview d’extension, sélectionnez hello virtual machine, choisissez **Extensions**, et sélectionnez hello extension souhaitée.</span><span class="sxs-lookup"><span data-stu-id="e05e2-187">tooview hello status of an extension, select hello virtual machine, choose **Extensions**, and select hello desired extension.</span></span>

### <a name="rerun-vm-extensions"></a><span data-ttu-id="e05e2-188">Réexécuter les extensions de machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="e05e2-188">Rerun VM extensions</span></span>

<span data-ttu-id="e05e2-189">Il peut y avoir des cas dans lesquels une extension de machine virtuelle doit toobe exécuter à nouveau.</span><span class="sxs-lookup"><span data-stu-id="e05e2-189">There may be cases in which a virtual machine extension needs toobe rerun.</span></span> <span data-ttu-id="e05e2-190">Pour cela, en supprimant hello extension, puis en réexécutant les extension hello avec une méthode d’exécution de votre choix.</span><span class="sxs-lookup"><span data-stu-id="e05e2-190">You can do this by removing hello extension and then rerunning hello extension with an execution method of your choice.</span></span> <span data-ttu-id="e05e2-191">tooremove une extension, exécutez hello commande avec le module de hello Azure PowerShell suivante.</span><span class="sxs-lookup"><span data-stu-id="e05e2-191">tooremove an extension, run hello following command with hello Azure PowerShell module.</span></span> <span data-ttu-id="e05e2-192">Remplacez les exemples de noms de paramètre par vos propres valeurs.</span><span class="sxs-lookup"><span data-stu-id="e05e2-192">Replace example parameter names with your own values.</span></span>

```powershell
Remove-AzureRmVMExtension -ResourceGroupName myResourceGroup -VMName myVM -Name myExtensionName
```

<span data-ttu-id="e05e2-193">Une extension peut également être supprimée à l’aide de hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="e05e2-193">An extension can also be removed using hello Azure portal.</span></span> <span data-ttu-id="e05e2-194">toodo pour :</span><span class="sxs-lookup"><span data-stu-id="e05e2-194">toodo so:</span></span>

1. <span data-ttu-id="e05e2-195">Sélectionnez une machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="e05e2-195">Select a virtual machine.</span></span>
2. <span data-ttu-id="e05e2-196">Sélectionnez **Extensions**.</span><span class="sxs-lookup"><span data-stu-id="e05e2-196">Select **Extensions**.</span></span>
3. <span data-ttu-id="e05e2-197">Choisissez les extension hello souhaité.</span><span class="sxs-lookup"><span data-stu-id="e05e2-197">Choose hello desired extension.</span></span>
4. <span data-ttu-id="e05e2-198">Sélectionnez **Désinstaller**.</span><span class="sxs-lookup"><span data-stu-id="e05e2-198">Select **Uninstall**.</span></span>

## <a name="common-vm-extensions-reference"></a><span data-ttu-id="e05e2-199">Informations de référence sur les extensions de machine virtuelle courantes</span><span class="sxs-lookup"><span data-stu-id="e05e2-199">Common VM extensions reference</span></span>
| <span data-ttu-id="e05e2-200">Nom de l’extension</span><span class="sxs-lookup"><span data-stu-id="e05e2-200">Extension name</span></span> | <span data-ttu-id="e05e2-201">Description</span><span class="sxs-lookup"><span data-stu-id="e05e2-201">Description</span></span> | <span data-ttu-id="e05e2-202">Plus d’informations</span><span class="sxs-lookup"><span data-stu-id="e05e2-202">More information</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e05e2-203">Extension de script personnalisé pour Windows</span><span class="sxs-lookup"><span data-stu-id="e05e2-203">Custom Script Extension for Windows</span></span> |<span data-ttu-id="e05e2-204">Exécuter des scripts sur une machine virtuelle Azure</span><span class="sxs-lookup"><span data-stu-id="e05e2-204">Run scripts against an Azure virtual machine</span></span> |[<span data-ttu-id="e05e2-205">Extension de script personnalisé pour Windows</span><span class="sxs-lookup"><span data-stu-id="e05e2-205">Custom Script Extension for Windows</span></span>](extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) |
| <span data-ttu-id="e05e2-206">Extension DSC pour Windows</span><span class="sxs-lookup"><span data-stu-id="e05e2-206">DSC Extension for Windows</span></span> |<span data-ttu-id="e05e2-207">Extension PowerShell DSC (Desired State Configuration, configuration d’état souhaité)</span><span class="sxs-lookup"><span data-stu-id="e05e2-207">PowerShell DSC (Desired State Configuration) Extension</span></span> |[<span data-ttu-id="e05e2-208">Extension DSC pour Windows</span><span class="sxs-lookup"><span data-stu-id="e05e2-208">DSC Extension for Windows</span></span>](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) |
| <span data-ttu-id="e05e2-209">Extension Diagnostics Azure</span><span class="sxs-lookup"><span data-stu-id="e05e2-209">Azure Diagnostics Extension</span></span> |<span data-ttu-id="e05e2-210">Gérer les diagnostics Azure</span><span class="sxs-lookup"><span data-stu-id="e05e2-210">Manage Azure Diagnostics</span></span> |[<span data-ttu-id="e05e2-211">Extension Diagnostics Azure</span><span class="sxs-lookup"><span data-stu-id="e05e2-211">Azure Diagnostics Extension</span></span>](https://azure.microsoft.com/blog/windows-azure-virtual-machine-monitoring-with-wad-extension/) |
| <span data-ttu-id="e05e2-212">Extension d’accès aux machines virtuelles Azure</span><span class="sxs-lookup"><span data-stu-id="e05e2-212">Azure VM Access Extension</span></span> |<span data-ttu-id="e05e2-213">Gérer les utilisateurs et les informations d’identification</span><span class="sxs-lookup"><span data-stu-id="e05e2-213">Manage users and credentials</span></span> |[<span data-ttu-id="e05e2-214">Extension d’accès aux machines virtuelles pour Linux</span><span class="sxs-lookup"><span data-stu-id="e05e2-214">VM Access Extension for Linux</span></span>](https://azure.microsoft.com/en-us/blog/using-vmaccess-extension-to-reset-login-credentials-for-linux-vm/) |
