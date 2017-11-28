---
title: "Extensions et fonctionnalités de machine virtuelle pour Windows dans Azure | Microsoft Docs"
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
ms.openlocfilehash: 1ce0eebd2585c9457d7f922898d7f2fa3e7ffad7
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="virtual-machine-extensions-and-features-for-windows"></a><span data-ttu-id="d657b-103">Extensions et fonctionnalités de machine virtuelle pour Windows</span><span class="sxs-lookup"><span data-stu-id="d657b-103">Virtual machine extensions and features for Windows</span></span>

<span data-ttu-id="d657b-104">Les extensions de machine virtuelle Azure sont de petites applications permettant d’exécuter des tâches de configuration et d’automatisation post-déploiement sur des machines virtuelles Azure.</span><span class="sxs-lookup"><span data-stu-id="d657b-104">Azure virtual machine extensions are small applications that provide post-deployment configuration and automation tasks on Azure virtual machines.</span></span> <span data-ttu-id="d657b-105">Par exemple, si une machine virtuelle requiert l’installation d’un logiciel, une protection antivirus ou une configuration de Docker, il est possible d’effectuer ces tâches à l’aide d’une extension de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="d657b-105">For example, if a virtual machine requires software installation, anti-virus protection, or Docker configuration, a VM extension can be used to complete these tasks.</span></span> <span data-ttu-id="d657b-106">Les extensions de machine virtuelle Azure peuvent être exécutées à l’aide de l’interface de ligne de commande Azure, de PowerShell, de modèles Azure Resource Manager et du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="d657b-106">Azure VM extensions can be run by using the Azure CLI, PowerShell, Azure Resource Manager templates, and the Azure portal.</span></span> <span data-ttu-id="d657b-107">Les extensions peuvent être associées à un nouveau déploiement de machine virtuelle ou s’exécuter sur tout système existant.</span><span class="sxs-lookup"><span data-stu-id="d657b-107">Extensions can be bundled with a new virtual machine deployment or run against any existing system.</span></span>

<span data-ttu-id="d657b-108">Ce document offre une vue d’ensemble des extensions de machine virtuelle et des composants requis pour utiliser les extensions de machine virtuelle. Il explique également comment détecter, gérer et supprimer les extensions de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="d657b-108">This document provides an overview of virtual machine extensions, prerequisites for using virtual machine extensions, and guidance on how to detect, manage, and remove virtual machine extensions.</span></span> <span data-ttu-id="d657b-109">Ce document fournit des informations générales, car de nombreuses extensions de machine virtuelle sont disponibles, chacune présentant une configuration potentiellement unique.</span><span class="sxs-lookup"><span data-stu-id="d657b-109">This document provides generalized information because many VM extensions are available, each with a potentially unique configuration.</span></span> <span data-ttu-id="d657b-110">Vous trouverez des informations détaillées sur une extension spécifique dans la documentation consacrée à celle-ci.</span><span class="sxs-lookup"><span data-stu-id="d657b-110">Extension-specific details can be found in each document specific to the individual extension.</span></span>

## <a name="use-cases-and-samples"></a><span data-ttu-id="d657b-111">Cas d’utilisation et exemples</span><span class="sxs-lookup"><span data-stu-id="d657b-111">Use cases and samples</span></span>

<span data-ttu-id="d657b-112">Plusieurs extensions de machine virtuelle Azure sont disponibles, chacune impliquant un cas d’utilisation spécifique.</span><span class="sxs-lookup"><span data-stu-id="d657b-112">There are many different Azure VM extensions available, each with a specific use case.</span></span> <span data-ttu-id="d657b-113">Exemples de cas d’utilisation :</span><span class="sxs-lookup"><span data-stu-id="d657b-113">Some example use cases are:</span></span>

- <span data-ttu-id="d657b-114">Appliquer des configurations d’état souhaité PowerShell à une machine virtuelle à l’aide de l’extension DSC pour Windows.</span><span class="sxs-lookup"><span data-stu-id="d657b-114">Apply PowerShell Desired State configurations to a virtual machine by using the DSC extension for Windows.</span></span> <span data-ttu-id="d657b-115">Pour plus d’informations sur l’extension DSC Azure, consultez [cette page](extensions-dsc-overview.md).</span><span class="sxs-lookup"><span data-stu-id="d657b-115">For more information, see [Azure Desired State configuration extension](extensions-dsc-overview.md).</span></span>
- <span data-ttu-id="d657b-116">Configurer l’analyse des machines virtuelles avec l’extension de machine virtuelle Microsoft Monitoring Agent.</span><span class="sxs-lookup"><span data-stu-id="d657b-116">Configure virtual machine monitoring by using the Microsoft Monitoring Agent VM extension.</span></span> <span data-ttu-id="d657b-117">Pour plus d’informations, consultez [Connecter des machines virtuelles Azure à Log Analytics](../../log-analytics/log-analytics-azure-vm-extension.md).</span><span class="sxs-lookup"><span data-stu-id="d657b-117">For more information, see [Connect Azure virtual machines to Log Analytics](../../log-analytics/log-analytics-azure-vm-extension.md).</span></span>
- <span data-ttu-id="d657b-118">Configurer l’analyse de votre infrastructure Azure à l’aide de l’extension Datadog.</span><span class="sxs-lookup"><span data-stu-id="d657b-118">Configure monitoring of your Azure infrastructure with the Datadog extension.</span></span> <span data-ttu-id="d657b-119">Pour plus d’informations, consultez le [blog Datadog](https://www.datadoghq.com/blog/introducing-azure-monitoring-with-one-click-datadog-deployment/).</span><span class="sxs-lookup"><span data-stu-id="d657b-119">For more information, see the [Datadog blog](https://www.datadoghq.com/blog/introducing-azure-monitoring-with-one-click-datadog-deployment/).</span></span>
- <span data-ttu-id="d657b-120">Configurer une machine virtuelle Azure à l’aide de Chef.</span><span class="sxs-lookup"><span data-stu-id="d657b-120">Configure an Azure virtual machine by using Chef.</span></span> <span data-ttu-id="d657b-121">Pour plus d’informations, consultez [Automatisation du déploiement de machine virtuelle Azure avec Chef](chef-automation.md).</span><span class="sxs-lookup"><span data-stu-id="d657b-121">For more information, see [Automating Azure virtual machine deployment with Chef](chef-automation.md).</span></span>

<span data-ttu-id="d657b-122">En plus des extensions propres à des processus, une extension de script personnalisé est disponible pour les machines virtuelles Windows et Linux.</span><span class="sxs-lookup"><span data-stu-id="d657b-122">In addition to process-specific extensions, a Custom Script extension is available for both Windows and Linux virtual machines.</span></span> <span data-ttu-id="d657b-123">L’extension de script personnalisé pour Windows permet d’exécuter n’importe quel script PowerShell sur une machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="d657b-123">The Custom Script extension for Windows allows any PowerShell script to be run on a virtual machine.</span></span> <span data-ttu-id="d657b-124">Cela s’avère utile pour concevoir des déploiements Azure qui nécessitent une configuration plus avancée que celle permise par les outils Azure.</span><span class="sxs-lookup"><span data-stu-id="d657b-124">This is useful when you're designing Azure deployments that require configuration beyond what native Azure tooling can provide.</span></span> <span data-ttu-id="d657b-125">Pour plus d’informations sur l’extension de script personnalisé pour les machines virtuelles Windows, consultez [cet article](extensions-customscript.md).</span><span class="sxs-lookup"><span data-stu-id="d657b-125">For more information, see [Windows VM Custom Script extension](extensions-customscript.md).</span></span>


## <a name="prerequisites"></a><span data-ttu-id="d657b-126">Composants requis</span><span class="sxs-lookup"><span data-stu-id="d657b-126">Prerequisites</span></span>

<span data-ttu-id="d657b-127">Chaque extension de machine virtuelle peut présenter son propre ensemble de composants requis.</span><span class="sxs-lookup"><span data-stu-id="d657b-127">Each virtual machine extension may have its own set of prerequisites.</span></span> <span data-ttu-id="d657b-128">Par exemple, l’extension de machine virtuelle Docker nécessite une distribution Linux compatible.</span><span class="sxs-lookup"><span data-stu-id="d657b-128">For instance, the Docker VM extension has a prerequisite of a supported Linux distribution.</span></span> <span data-ttu-id="d657b-129">Les composants requis pour une extension spécifique sont présentés en détail dans la documentation consacrée à celle-ci.</span><span class="sxs-lookup"><span data-stu-id="d657b-129">Requirements of individual extensions are detailed in the extension-specific documentation.</span></span>

### <a name="azure-vm-agent"></a><span data-ttu-id="d657b-130">Agent de machine virtuelle Azure</span><span class="sxs-lookup"><span data-stu-id="d657b-130">Azure VM agent</span></span>
<span data-ttu-id="d657b-131">L’agent de machine virtuelle Azure gère l’interaction entre une machine virtuelle Azure et le contrôleur de structure Azure.</span><span class="sxs-lookup"><span data-stu-id="d657b-131">The Azure VM agent manages interaction between an Azure virtual machine and the Azure fabric controller.</span></span> <span data-ttu-id="d657b-132">L’agent de machine virtuelle est responsable de nombreux aspects fonctionnels liés au déploiement et à la gestion des machines virtuelles Azure, dont les extensions de machine virtuelle en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="d657b-132">The VM agent is responsible for many functional aspects of deploying and managing Azure virtual machines, including running VM extensions.</span></span> <span data-ttu-id="d657b-133">L’agent de machine virtuelle Azure est préinstallé sur les images d’Azure Marketplace et peut être installé sur les systèmes d’exploitation pris en charge.</span><span class="sxs-lookup"><span data-stu-id="d657b-133">The Azure VM agent is preinstalled on Azure Marketplace images and can be installed on supported operating systems.</span></span>

<span data-ttu-id="d657b-134">Pour plus d’informations sur les systèmes d’exploitation pris en charge et sur la procédure d’installation, consultez l’article [Agent de machine virtuelle et extensions Azure](agent-user-guide.md).</span><span class="sxs-lookup"><span data-stu-id="d657b-134">For information on supported operating systems and installation instructions, see [Azure virtual machine agent](agent-user-guide.md).</span></span>

## <a name="discover-vm-extensions"></a><span data-ttu-id="d657b-135">Détecter les extensions de machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="d657b-135">Discover VM extensions</span></span>
<span data-ttu-id="d657b-136">De nombreuses extensions de machine virtuelle différentes peuvent être utilisées avec les machines virtuelles Azure.</span><span class="sxs-lookup"><span data-stu-id="d657b-136">Many different VM extensions are available for use with Azure virtual machines.</span></span> <span data-ttu-id="d657b-137">Pour en obtenir la liste complète, exécutez la commande suivante avec le module Azure Resource Manager PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d657b-137">To see a complete list, run the following command with the Azure Resource Manager PowerShell module.</span></span> <span data-ttu-id="d657b-138">Veillez à spécifier l’emplacement de votre choix lorsque vous exécutez cette commande.</span><span class="sxs-lookup"><span data-stu-id="d657b-138">Make sure to specify the desired location when you're running this command.</span></span>

```powershell
Get-AzureRmVmImagePublisher -Location WestUS | `
Get-AzureRmVMExtensionImageType | `
Get-AzureRmVMExtensionImage | Select Type, Version
```

## <a name="run-vm-extensions"></a><span data-ttu-id="d657b-139">Exécuter les extensions de machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="d657b-139">Run VM extensions</span></span>

<span data-ttu-id="d657b-140">Les extensions de machine virtuelle peuvent être exécutées sur des machines virtuelles existantes, ce qui s’avère utile lorsque vous devez apporter des modifications de configuration ou restaurer la connectivité sur une machine virtuelle déjà déployée.</span><span class="sxs-lookup"><span data-stu-id="d657b-140">Azure virtual machine extensions can be run on existing virtual machines, which is useful when you need to make configuration changes or recover connectivity on an already deployed VM.</span></span> <span data-ttu-id="d657b-141">Les extensions de machines virtuelles peuvent également être intégrées dans des déploiements de modèles Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="d657b-141">VM extensions can also be bundled with Azure Resource Manager template deployments.</span></span> <span data-ttu-id="d657b-142">L’utilisation d’extensions avec des modèles Resource Manager permet de déployer et de configurer des machines virtuelles Azure sans avoir à intervenir après le déploiement.</span><span class="sxs-lookup"><span data-stu-id="d657b-142">By using extensions with Resource Manager templates, you can enable Azure virtual machines to be deployed and configured without the need for post-deployment intervention.</span></span>

<span data-ttu-id="d657b-143">Les méthodes suivantes peuvent être utilisées pour exécuter une extension sur une machine virtuelle existante.</span><span class="sxs-lookup"><span data-stu-id="d657b-143">The following methods can be used to run an extension against an existing virtual machine.</span></span>

### <a name="powershell"></a><span data-ttu-id="d657b-144">PowerShell</span><span class="sxs-lookup"><span data-stu-id="d657b-144">PowerShell</span></span>

<span data-ttu-id="d657b-145">Il existe plusieurs commandes PowerShell pour l’exécution des extensions.</span><span class="sxs-lookup"><span data-stu-id="d657b-145">Several PowerShell commands exist for running individual extensions.</span></span> <span data-ttu-id="d657b-146">Pour afficher la liste, exécutez les commandes PowerShell suivantes.</span><span class="sxs-lookup"><span data-stu-id="d657b-146">To see a list, run the following PowerShell commands.</span></span>

```powershell
get-command Set-AzureRM*Extension* -Module AzureRM.Compute
```

<span data-ttu-id="d657b-147">Vous générez ainsi des informations qui ressemblent à ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="d657b-147">This provides output similar to the following:</span></span>

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

<span data-ttu-id="d657b-148">L’exemple suivant utilise l’extension de script personnalisé pour télécharger un script sur la machine virtuelle cible depuis un dépôt GitHub, puis pour exécuter le script.</span><span class="sxs-lookup"><span data-stu-id="d657b-148">The following example uses the Custom Script extension to download a script from a GitHub repository onto the target virtual machine and then run the script.</span></span> <span data-ttu-id="d657b-149">Pour plus d’informations sur l’extension de script personnalisé, consultez [Vue d’ensemble de l’extension de script personnalisé](extensions-customscript.md).</span><span class="sxs-lookup"><span data-stu-id="d657b-149">For more information on the Custom Script extension, see [Custom Script extension overview](extensions-customscript.md).</span></span>

```powershell
Set-AzureRmVMCustomScriptExtension -ResourceGroupName "myResourceGroup" `
    -VMName "myVM" -Name "myCustomScript" `
    -FileUri "https://raw.githubusercontent.com/neilpeterson/nepeters-azure-templates/master/windows-custom-script-simple/support-scripts/Create-File.ps1" `
    -Run "Create-File.ps1" -Location "West US"
```

<span data-ttu-id="d657b-150">Dans cet exemple, l’extension d’accès aux machines virtuelles est utilisée pour réinitialiser le mot de passe d’administration d’une machine virtuelle Windows.</span><span class="sxs-lookup"><span data-stu-id="d657b-150">In this example, the VM Access extension is used to reset the administrative password of a Windows virtual machine.</span></span> <span data-ttu-id="d657b-151">Pour plus d’informations sur l’extension d’accès aux machines virtuelles, consultez [Réinitialiser le service Bureau à distance pour une machine virtuelle Windows](reset-rdp.md).</span><span class="sxs-lookup"><span data-stu-id="d657b-151">For more information on the VM Access extension, see [Reset Remote Desktop service in a Windows VM](reset-rdp.md).</span></span>

```powershell
$cred=Get-Credential

Set-AzureRmVMAccessExtension -ResourceGroupName "myResourceGroup" -VMName "myVM" -Name "myVMAccess" `
    -Location WestUS -UserName $cred.GetNetworkCredential().Username `
    -Password $cred.GetNetworkCredential().Password -typeHandlerVersion "2.0"
```

<span data-ttu-id="d657b-152">Vous pouvez utiliser la commande `Set-AzureRmVMExtension` pour démarrer n’importe quelle extension de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="d657b-152">The `Set-AzureRmVMExtension` command can be used to start any VM extension.</span></span> <span data-ttu-id="d657b-153">Pour plus d’informations, consultez [Référence Set-AzureRmVMExtension](https://msdn.microsoft.com/en-us/library/mt603745.aspx).</span><span class="sxs-lookup"><span data-stu-id="d657b-153">For more information, see the [Set-AzureRmVMExtension reference](https://msdn.microsoft.com/en-us/library/mt603745.aspx).</span></span>


### <a name="azure-portal"></a><span data-ttu-id="d657b-154">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="d657b-154">Azure portal</span></span>

<span data-ttu-id="d657b-155">Une extension de machine virtuelle peut être appliquée à une machine virtuelle existante via le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="d657b-155">A VM extension can be applied to an existing virtual machine through the Azure portal.</span></span> <span data-ttu-id="d657b-156">Pour ce faire, sélectionnez la machine virtuelle à utiliser, choisissez **Extensions**, puis cliquez sur **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="d657b-156">To do so, select the virtual machine you want to use, choose **Extensions**, and click **Add**.</span></span> <span data-ttu-id="d657b-157">La liste des extensions disponibles s’affiche.</span><span class="sxs-lookup"><span data-stu-id="d657b-157">This provides a list of available extensions.</span></span> <span data-ttu-id="d657b-158">Sélectionnez l’extension souhaitée et suivez les étapes de l’Assistant.</span><span class="sxs-lookup"><span data-stu-id="d657b-158">Select the one you want and follow the steps in the wizard.</span></span>

<span data-ttu-id="d657b-159">L’image suivante illustre l’installation de l’extension Microsoft Antimalware à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="d657b-159">The following image shows the installation of the Microsoft Antimalware extension from the Azure portal.</span></span>

![Installer l’extension Antimalware](./media/extensions-features/installantimalwareextension.png)

### <a name="azure-resource-manager-templates"></a><span data-ttu-id="d657b-161">Modèles Microsoft Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="d657b-161">Azure Resource Manager templates</span></span>

<span data-ttu-id="d657b-162">Les extensions de machine virtuelle peuvent être ajoutées à un modèle Azure Resource Manager et exécutées avec le déploiement du modèle.</span><span class="sxs-lookup"><span data-stu-id="d657b-162">VM extensions can be added to an Azure Resource Manager template and executed with the deployment of the template.</span></span> <span data-ttu-id="d657b-163">Le déploiement d’extensions avec un modèle permet de créer des déploiements Azure entièrement configurés.</span><span class="sxs-lookup"><span data-stu-id="d657b-163">Deploying extensions with a template is useful for creating fully configured Azure deployments.</span></span> <span data-ttu-id="d657b-164">Par exemple, le code JSON suivant est tiré d’un modèle Resource Manager qui déploie un ensemble de machines virtuelles à charge équilibrée et une base de données SQL Azure, puis installe une application .NET Core sur chaque machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="d657b-164">For example, the following JSON is taken from a Resource Manager template that deploys a set of load-balanced virtual machines and an Azure SQL database, and then installs a .NET Core application on each VM.</span></span> <span data-ttu-id="d657b-165">L’extension de machine virtuelle se charge de l’installation du logiciel.</span><span class="sxs-lookup"><span data-stu-id="d657b-165">The VM extension takes care of the software installation.</span></span>

<span data-ttu-id="d657b-166">Pour plus d’informations, consultez le [modèle Resource Manager complet](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows).</span><span class="sxs-lookup"><span data-stu-id="d657b-166">For more information, see the [full Resource Manager template](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows).</span></span>

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

<span data-ttu-id="d657b-167">Pour plus d’informations, consultez l’article [Création de modèles Azure Resource Manager avec des extensions de machine virtuelle Windows](template-description.md#extensions).</span><span class="sxs-lookup"><span data-stu-id="d657b-167">For more information, see [Authoring Azure Resource Manager templates with Windows VM extensions](template-description.md#extensions).</span></span>

## <a name="secure-vm-extension-data"></a><span data-ttu-id="d657b-168">Sécuriser les données des extensions de machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="d657b-168">Secure VM extension data</span></span>

<span data-ttu-id="d657b-169">Lorsque vous exécutez une extension de machine virtuelle, vous pouvez avoir besoin d’inclure des informations sensibles telles que des informations d’identification, des noms de compte de stockage et des clés d’accès à des comptes de stockage.</span><span class="sxs-lookup"><span data-stu-id="d657b-169">When you're running a VM extension, it may be necessary to include sensitive information such as credentials, storage account names, and storage account access keys.</span></span> <span data-ttu-id="d657b-170">De nombreuses extensions de machine virtuelle comprennent une configuration protégée qui chiffre les données et les déchiffre uniquement à l’intérieur de la machine virtuelle cible.</span><span class="sxs-lookup"><span data-stu-id="d657b-170">Many VM extensions include a protected configuration that encrypts data and only decrypts it inside the target virtual machine.</span></span> <span data-ttu-id="d657b-171">Chaque extension possède un schéma spécifique de configuration protégée qui sera présenté en détail dans la documentation consacrée à l’extension.</span><span class="sxs-lookup"><span data-stu-id="d657b-171">Each extension has a specific protected configuration schema that will be detailed in extension-specific documentation.</span></span>

<span data-ttu-id="d657b-172">L’exemple suivant illustre une instance de l’extension de script personnalisé pour Windows.</span><span class="sxs-lookup"><span data-stu-id="d657b-172">The following example shows an instance of the Custom Script extension for Windows.</span></span> <span data-ttu-id="d657b-173">Notez que la commande à exécuter inclut un ensemble d’informations d’identification.</span><span class="sxs-lookup"><span data-stu-id="d657b-173">Notice that the command to execute includes a set of credentials.</span></span> <span data-ttu-id="d657b-174">Dans cet exemple, la commande à exécuter ne sera pas chiffrée.</span><span class="sxs-lookup"><span data-stu-id="d657b-174">In this example, the command to execute will not be encrypted.</span></span>


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

<span data-ttu-id="d657b-175">Sécurisez la chaîne d’exécution en déplaçant la propriété **command to execute** dans la configuration **protected**.</span><span class="sxs-lookup"><span data-stu-id="d657b-175">Secure the execution string by moving the **command to execute** property to the **protected** configuration.</span></span>

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

## <a name="troubleshoot-vm-extensions"></a><span data-ttu-id="d657b-176">Résoudre les problèmes liés aux extensions de machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="d657b-176">Troubleshoot VM extensions</span></span>

<span data-ttu-id="d657b-177">Chaque extension de machine virtuelle peut présenter une procédure de résolution des problèmes spécifique.</span><span class="sxs-lookup"><span data-stu-id="d657b-177">Each VM extension may have specific troubleshooting steps.</span></span> <span data-ttu-id="d657b-178">Par exemple, lorsque vous utilisez l’extension de script personnalisé, les détails de l’exécution du script sont accessibles localement sur la machine virtuelle utilisée pour l’exécution de l’extension.</span><span class="sxs-lookup"><span data-stu-id="d657b-178">For instance, when you're using the Custom Script extension, script execution details can be found locally on the virtual machine on which the extension was run.</span></span> <span data-ttu-id="d657b-179">La procédure de résolution des problèmes spécifique d’une extension est présentée en détail dans la documentation de cette dernière.</span><span class="sxs-lookup"><span data-stu-id="d657b-179">Any extension-specific troubleshooting steps are detailed in extension-specific documentation.</span></span>

<span data-ttu-id="d657b-180">La procédure de résolution des problèmes ci-dessous s’applique à toutes les extensions de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="d657b-180">The following troubleshooting steps apply to all virtual machine extensions.</span></span>

### <a name="view-extension-status"></a><span data-ttu-id="d657b-181">Afficher l’état de l’extension</span><span class="sxs-lookup"><span data-stu-id="d657b-181">View extension status</span></span>

<span data-ttu-id="d657b-182">Après avoir exécuté une extension de machine virtuelle, utilisez la commande PowerShell suivante pour obtenir l’état de l’extension.</span><span class="sxs-lookup"><span data-stu-id="d657b-182">After a virtual machine extension has been run against a virtual machine, use the following PowerShell command to return extension status.</span></span> <span data-ttu-id="d657b-183">Remplacez les exemples de noms de paramètre par vos propres valeurs.</span><span class="sxs-lookup"><span data-stu-id="d657b-183">Replace example parameter names with your own values.</span></span> <span data-ttu-id="d657b-184">Le paramètre `Name` accepte le nom donné à l’extension au moment de l’exécution.</span><span class="sxs-lookup"><span data-stu-id="d657b-184">The `Name` parameter takes the name given to the extension at execution time.</span></span>

```PowerShell
Get-AzureRmVMExtension -ResourceGroupName myResourceGroup -VMName myVM -Name myExtensionName
```

<span data-ttu-id="d657b-185">La sortie a l'aspect suivant :</span><span class="sxs-lookup"><span data-stu-id="d657b-185">The output looks like the following:</span></span>

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

<span data-ttu-id="d657b-186">L’état d’exécution de l’extension est également visible dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="d657b-186">Extension execution status can also be found in the Azure portal.</span></span> <span data-ttu-id="d657b-187">Pour afficher l’état d’une extension, sélectionnez la machine virtuelle, choisissez **Extensions**, puis sélectionnez l’extension souhaitée.</span><span class="sxs-lookup"><span data-stu-id="d657b-187">To view the status of an extension, select the virtual machine, choose **Extensions**, and select the desired extension.</span></span>

### <a name="rerun-vm-extensions"></a><span data-ttu-id="d657b-188">Réexécuter les extensions de machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="d657b-188">Rerun VM extensions</span></span>

<span data-ttu-id="d657b-189">Dans certains cas, il se peut que vous deviez réexécuter une extension de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="d657b-189">There may be cases in which a virtual machine extension needs to be rerun.</span></span> <span data-ttu-id="d657b-190">Pour ce faire, vous pouvez supprimer l’extension, puis la réexécuter avec la méthode d’exécution de votre choix.</span><span class="sxs-lookup"><span data-stu-id="d657b-190">You can do this by removing the extension and then rerunning the extension with an execution method of your choice.</span></span> <span data-ttu-id="d657b-191">Pour supprimer une extension, exécutez la commande suivante avec le module Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d657b-191">To remove an extension, run the following command with the Azure PowerShell module.</span></span> <span data-ttu-id="d657b-192">Remplacez les exemples de noms de paramètre par vos propres valeurs.</span><span class="sxs-lookup"><span data-stu-id="d657b-192">Replace example parameter names with your own values.</span></span>

```powershell
Remove-AzureRmVMExtension -ResourceGroupName myResourceGroup -VMName myVM -Name myExtensionName
```

<span data-ttu-id="d657b-193">Une extension peut également être supprimée à l’aide du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="d657b-193">An extension can also be removed using the Azure portal.</span></span> <span data-ttu-id="d657b-194">Pour ce faire :</span><span class="sxs-lookup"><span data-stu-id="d657b-194">To do so:</span></span>

1. <span data-ttu-id="d657b-195">Sélectionnez une machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="d657b-195">Select a virtual machine.</span></span>
2. <span data-ttu-id="d657b-196">Sélectionnez **Extensions**.</span><span class="sxs-lookup"><span data-stu-id="d657b-196">Select **Extensions**.</span></span>
3. <span data-ttu-id="d657b-197">Choisissez l’extension souhaitée.</span><span class="sxs-lookup"><span data-stu-id="d657b-197">Choose the desired extension.</span></span>
4. <span data-ttu-id="d657b-198">Sélectionnez **Désinstaller**.</span><span class="sxs-lookup"><span data-stu-id="d657b-198">Select **Uninstall**.</span></span>

## <a name="common-vm-extensions-reference"></a><span data-ttu-id="d657b-199">Informations de référence sur les extensions de machine virtuelle courantes</span><span class="sxs-lookup"><span data-stu-id="d657b-199">Common VM extensions reference</span></span>
| <span data-ttu-id="d657b-200">Nom de l’extension</span><span class="sxs-lookup"><span data-stu-id="d657b-200">Extension name</span></span> | <span data-ttu-id="d657b-201">Description</span><span class="sxs-lookup"><span data-stu-id="d657b-201">Description</span></span> | <span data-ttu-id="d657b-202">Plus d’informations</span><span class="sxs-lookup"><span data-stu-id="d657b-202">More information</span></span> |
| --- | --- | --- |
| <span data-ttu-id="d657b-203">Extension de script personnalisé pour Windows</span><span class="sxs-lookup"><span data-stu-id="d657b-203">Custom Script Extension for Windows</span></span> |<span data-ttu-id="d657b-204">Exécuter des scripts sur une machine virtuelle Azure</span><span class="sxs-lookup"><span data-stu-id="d657b-204">Run scripts against an Azure virtual machine</span></span> |[<span data-ttu-id="d657b-205">Extension de script personnalisé pour Windows</span><span class="sxs-lookup"><span data-stu-id="d657b-205">Custom Script Extension for Windows</span></span>](extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) |
| <span data-ttu-id="d657b-206">Extension DSC pour Windows</span><span class="sxs-lookup"><span data-stu-id="d657b-206">DSC Extension for Windows</span></span> |<span data-ttu-id="d657b-207">Extension PowerShell DSC (Desired State Configuration, configuration d’état souhaité)</span><span class="sxs-lookup"><span data-stu-id="d657b-207">PowerShell DSC (Desired State Configuration) Extension</span></span> |[<span data-ttu-id="d657b-208">Extension DSC pour Windows</span><span class="sxs-lookup"><span data-stu-id="d657b-208">DSC Extension for Windows</span></span>](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) |
| <span data-ttu-id="d657b-209">Extension Diagnostics Azure</span><span class="sxs-lookup"><span data-stu-id="d657b-209">Azure Diagnostics Extension</span></span> |<span data-ttu-id="d657b-210">Gérer les diagnostics Azure</span><span class="sxs-lookup"><span data-stu-id="d657b-210">Manage Azure Diagnostics</span></span> |[<span data-ttu-id="d657b-211">Extension Diagnostics Azure</span><span class="sxs-lookup"><span data-stu-id="d657b-211">Azure Diagnostics Extension</span></span>](https://azure.microsoft.com/blog/windows-azure-virtual-machine-monitoring-with-wad-extension/) |
| <span data-ttu-id="d657b-212">Extension d’accès aux machines virtuelles Azure</span><span class="sxs-lookup"><span data-stu-id="d657b-212">Azure VM Access Extension</span></span> |<span data-ttu-id="d657b-213">Gérer les utilisateurs et les informations d’identification</span><span class="sxs-lookup"><span data-stu-id="d657b-213">Manage users and credentials</span></span> |[<span data-ttu-id="d657b-214">Extension d’accès aux machines virtuelles pour Linux</span><span class="sxs-lookup"><span data-stu-id="d657b-214">VM Access Extension for Linux</span></span>](https://azure.microsoft.com/en-us/blog/using-vmaccess-extension-to-reset-login-credentials-for-linux-vm/) |
