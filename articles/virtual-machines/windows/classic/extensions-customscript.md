---
title: aaaCustom extension de Script sur une machine virtuelle Windows | Documents Microsoft
description: "Automatiser les tâches de configuration de machine virtuelle Azure à l’aide de scripts PowerShell toorun hello Script personnalisé extension sur un ordinateur virtuel de Windows à distance"
services: virtual-machines-windows
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: ebb7340a-8f61-4d3c-a290-d7bf8de2d0bd
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 01/17/2017
ms.author: nepeters
ms.openlocfilehash: cf7bb895dd211f07fd010dc03b68cd77df1127b2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="custom-script-extension-for-windows-using-hello-classic-deployment-model"></a><span data-ttu-id="a1f9e-103">Personnalisé Extension pour les fenêtres de Script à l’aide du modèle de déploiement classique de hello</span><span class="sxs-lookup"><span data-stu-id="a1f9e-103">Custom Script Extension for Windows using hello classic deployment model</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="a1f9e-104">Azure dispose de deux modèles de déploiement différents pour créer et utiliser des ressources : [le déploiement Resource Manager et le déploiement classique](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="a1f9e-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="a1f9e-105">Cet article décrit à l’aide du modèle de déploiement classique hello.</span><span class="sxs-lookup"><span data-stu-id="a1f9e-105">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="a1f9e-106">Microsoft recommande que la plupart des nouveaux déploiements de modèle du Gestionnaire de ressources hello.</span><span class="sxs-lookup"><span data-stu-id="a1f9e-106">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="a1f9e-107">Découvrez comment trop[effectuer ces étapes à l’aide du modèle de gestionnaire de ressources hello](../extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="a1f9e-107">Learn how too[perform these steps using hello Resource Manager model](../extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="a1f9e-108">Extension de Script personnalisé de Hello télécharge et exécute des scripts sur les machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="a1f9e-108">hello Custom Script Extension downloads and executes scripts on Azure virtual machines.</span></span> <span data-ttu-id="a1f9e-109">Cette extension est utile pour la configuration post-déploiement, l’installation de logiciels ou toute autre tâche de configuration ou de gestion.</span><span class="sxs-lookup"><span data-stu-id="a1f9e-109">This extension is useful for post deployment configuration, software installation, or any other configuration / management task.</span></span> <span data-ttu-id="a1f9e-110">Scripts pouvant être téléchargés à partir de GitHub ou de stockage Azure, ou toohello portail Azure à l’extension de durée d’exécution.</span><span class="sxs-lookup"><span data-stu-id="a1f9e-110">Scripts can be downloaded from Azure storage or GitHub, or provided toohello Azure portal at extension run time.</span></span> <span data-ttu-id="a1f9e-111">Hello, extension de Script personnalisé s’intègre aux modèles Azure Resource Manager et peut également être exécuté à l’aide de hello CLI d’Azure, PowerShell, portail Azure ou hello API REST de Machine virtuelle Azure.</span><span class="sxs-lookup"><span data-stu-id="a1f9e-111">hello Custom Script extension integrates with Azure Resource Manager templates, and can also be run using hello Azure CLI, PowerShell, Azure portal, or hello Azure Virtual Machine REST API.</span></span>

<span data-ttu-id="a1f9e-112">Ce document décrit en détail comment toouse hello Extension de Script personnalisé utilisant hello module Azure PowerShell, modèles Azure Resource Manager et informations de dépannage sur les systèmes Windows.</span><span class="sxs-lookup"><span data-stu-id="a1f9e-112">This document details how toouse hello Custom Script Extension using hello Azure PowerShell module, Azure Resource Manager templates, and details troubleshooting steps on Windows systems.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a1f9e-113">Composants requis</span><span class="sxs-lookup"><span data-stu-id="a1f9e-113">Prerequisites</span></span>

### <a name="operating-system"></a><span data-ttu-id="a1f9e-114">Système d’exploitation</span><span class="sxs-lookup"><span data-stu-id="a1f9e-114">Operating System</span></span>

<span data-ttu-id="a1f9e-115">Hello, Extension de Script personnalisé pour Windows puisse être exécuté sur Windows Server 2008 R2, 2012, 2012 R2 et 2016 libère.</span><span class="sxs-lookup"><span data-stu-id="a1f9e-115">hello Custom Script Extension for Windows can be run against Windows Server 2008 R2, 2012, 2012 R2, and 2016 releases.</span></span>

### <a name="script-location"></a><span data-ttu-id="a1f9e-116">Emplacement du script</span><span class="sxs-lookup"><span data-stu-id="a1f9e-116">Script Location</span></span>

<span data-ttu-id="a1f9e-117">script de Hello doit toobe stockée dans le stockage Azure, ou tout autre emplacement accessible via une URL valide.</span><span class="sxs-lookup"><span data-stu-id="a1f9e-117">hello script needs toobe stored in Azure storage, or any other location accessible through a valid URL.</span></span>

### <a name="internet-connectivity"></a><span data-ttu-id="a1f9e-118">Connectivité Internet</span><span class="sxs-lookup"><span data-stu-id="a1f9e-118">Internet Connectivity</span></span>

<span data-ttu-id="a1f9e-119">Hello Extension de Script personnalisé pour Windows requiert que l’ordinateur virtuel cible hello est connecté toohello internet.</span><span class="sxs-lookup"><span data-stu-id="a1f9e-119">hello Custom Script Extension for Windows requires that hello target virtual machine is connected toohello internet.</span></span> 

## <a name="extension-schema"></a><span data-ttu-id="a1f9e-120">Schéma d’extensions</span><span class="sxs-lookup"><span data-stu-id="a1f9e-120">Extension schema</span></span>

<span data-ttu-id="a1f9e-121">Hello JSON suivant montre schéma hello pour hello Extension de Script personnalisé.</span><span class="sxs-lookup"><span data-stu-id="a1f9e-121">hello following JSON shows hello schema for hello Custom Script Extension.</span></span> <span data-ttu-id="a1f9e-122">extension de Hello nécessite un emplacement de script (le stockage Azure ou un autre emplacement avec une URL valide) et un tooexecute de commande.</span><span class="sxs-lookup"><span data-stu-id="a1f9e-122">hello extension requires a script location (Azure Storage or other location with valid URL), and a command tooexecute.</span></span> <span data-ttu-id="a1f9e-123">Si vous utilisez le stockage Azure en tant que source du script hello, une clé de compte et le nom de compte stockage Azure est requise.</span><span class="sxs-lookup"><span data-stu-id="a1f9e-123">If using Azure Storage as hello script source, an Azure storage account name and account key is required.</span></span> <span data-ttu-id="a1f9e-124">Ces éléments doivent être considérés comme des données sensibles et spécifiés dans la configuration de paramètre protégé hello extensions.</span><span class="sxs-lookup"><span data-stu-id="a1f9e-124">These items should be treated as sensitive data and specified in hello extensions protected setting configuration.</span></span> <span data-ttu-id="a1f9e-125">Les données de paramètre d’extension protégée de machine virtuelle Azure sont chiffrées et déchiffrées uniquement sur la machine virtuelle cible hello.</span><span class="sxs-lookup"><span data-stu-id="a1f9e-125">Azure VM extension protected setting data is encrypted, and only decrypted on hello target virtual machine.</span></span>

```json
{
    "name": "config-app",
    "type": "Microsoft.ClassicCompute/virtualMachines/extensions",
    "location": "[resourceGroup().location]",
    "apiVersion": "2015-06-01",
    "properties": {
        "publisher": "Microsoft.Compute",
        "extension": "CustomScriptExtension",
        "version": "1.8",
        "parameters": {
            "public": {
                "fileUris": "[myScriptLocation]"
            },
            "private": {
                "commandToExecute": "[myExecutionString]"
            }
        }
    }
}
```

### <a name="property-values"></a><span data-ttu-id="a1f9e-126">Valeurs de propriétés</span><span class="sxs-lookup"><span data-stu-id="a1f9e-126">Property values</span></span>

| <span data-ttu-id="a1f9e-127">Nom</span><span class="sxs-lookup"><span data-stu-id="a1f9e-127">Name</span></span> | <span data-ttu-id="a1f9e-128">Valeur/Exemple</span><span class="sxs-lookup"><span data-stu-id="a1f9e-128">Value / Example</span></span> |
| ---- | ---- |
| <span data-ttu-id="a1f9e-129">apiVersion</span><span class="sxs-lookup"><span data-stu-id="a1f9e-129">apiVersion</span></span> | <span data-ttu-id="a1f9e-130">2015-06-15</span><span class="sxs-lookup"><span data-stu-id="a1f9e-130">2015-06-15</span></span> |
| <span data-ttu-id="a1f9e-131">publisher</span><span class="sxs-lookup"><span data-stu-id="a1f9e-131">publisher</span></span> | <span data-ttu-id="a1f9e-132">Microsoft.Compute</span><span class="sxs-lookup"><span data-stu-id="a1f9e-132">Microsoft.Compute</span></span> |
| <span data-ttu-id="a1f9e-133">extension</span><span class="sxs-lookup"><span data-stu-id="a1f9e-133">extension</span></span> | <span data-ttu-id="a1f9e-134">CustomScriptExtension</span><span class="sxs-lookup"><span data-stu-id="a1f9e-134">CustomScriptExtension</span></span> |
| <span data-ttu-id="a1f9e-135">typeHandlerVersion</span><span class="sxs-lookup"><span data-stu-id="a1f9e-135">typeHandlerVersion</span></span> | <span data-ttu-id="a1f9e-136">1.8</span><span class="sxs-lookup"><span data-stu-id="a1f9e-136">1.8</span></span> |
| <span data-ttu-id="a1f9e-137">fileUris (p. ex.)</span><span class="sxs-lookup"><span data-stu-id="a1f9e-137">fileUris (e.g)</span></span> | <span data-ttu-id="a1f9e-138">https://raw.githubusercontent.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-windows/scripts/configure-music-app.ps1</span><span class="sxs-lookup"><span data-stu-id="a1f9e-138">https://raw.githubusercontent.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-windows/scripts/configure-music-app.ps1</span></span> |
| <span data-ttu-id="a1f9e-139">commandToExecute (p. ex.)</span><span class="sxs-lookup"><span data-stu-id="a1f9e-139">commandToExecute (e.g)</span></span> | <span data-ttu-id="a1f9e-140">powershell -ExecutionPolicy Unrestricted -File configure-music-app.ps1</span><span class="sxs-lookup"><span data-stu-id="a1f9e-140">powershell -ExecutionPolicy Unrestricted -File configure-music-app.ps1</span></span> |

## <a name="template-deployment"></a><span data-ttu-id="a1f9e-141">Déploiement de modèle</span><span class="sxs-lookup"><span data-stu-id="a1f9e-141">Template deployment</span></span>

<span data-ttu-id="a1f9e-142">Les extensions de machines virtuelles Azure peuvent être déployées avec des modèles Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="a1f9e-142">Azure VM extensions can be deployed with Azure Resource Manager templates.</span></span> <span data-ttu-id="a1f9e-143">schéma JSON de Hello détaillé dans la section précédente de hello peut être utilisé dans un hello toorun du modèle Azure Resource Manager Extension de Script personnalisé pendant un déploiement de modèle Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="a1f9e-143">hello JSON schema detailed in hello previous section can be used in an Azure Resource Manager template toorun hello Custom Script Extension during an Azure Resource Manager template deployment.</span></span> <span data-ttu-id="a1f9e-144">Un exemple de modèle qui inclut hello Extension de Script personnalisé se trouve ici, [GitHub](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows).</span><span class="sxs-lookup"><span data-stu-id="a1f9e-144">A sample template that includes hello Custom Script Extension can be found here, [GitHub](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows).</span></span>

## <a name="powershell-deployment"></a><span data-ttu-id="a1f9e-145">Déploiement PowerShell</span><span class="sxs-lookup"><span data-stu-id="a1f9e-145">PowerShell deployment</span></span>

<span data-ttu-id="a1f9e-146">Hello `Set-AzureVMCustomScriptExtension` commande peut être utilisé tooadd hello Script personnalisé extension tooan ordinateur virtuel.</span><span class="sxs-lookup"><span data-stu-id="a1f9e-146">hello `Set-AzureVMCustomScriptExtension` command can be used tooadd hello Custom Script extension tooan existing virtual machine.</span></span> <span data-ttu-id="a1f9e-147">Pour plus d’informations, consultez [Set-AzureRmVMCustomScriptExtension](https://docs.microsoft.com/en-us/powershell/resourcemanager/azurerm.compute/v2.1.0/set-azurermvmcustomscriptextension).</span><span class="sxs-lookup"><span data-stu-id="a1f9e-147">For more information, see [Set-AzureRmVMCustomScriptExtension ](https://docs.microsoft.com/en-us/powershell/resourcemanager/azurerm.compute/v2.1.0/set-azurermvmcustomscriptextension).</span></span>

```powershell
# create vm object
$vm = Get-AzureVM -Name 2016clas -ServiceName 2016clas1313

# set extension
Set-AzureVMCustomScriptExtension -VM $vm -FileUri myFileUri -Run 'create-file.ps1'

# update vm
$vm | Update-AzureVM
```

## <a name="troubleshoot-and-support"></a><span data-ttu-id="a1f9e-148">Dépannage et support technique</span><span class="sxs-lookup"><span data-stu-id="a1f9e-148">Troubleshoot and support</span></span>

### <a name="troubleshoot"></a><span data-ttu-id="a1f9e-149">Résolution des problèmes</span><span class="sxs-lookup"><span data-stu-id="a1f9e-149">Troubleshoot</span></span>

<span data-ttu-id="a1f9e-150">Données sur l’état de hello de déploiements d’extension peuvent être récupérées à partir de hello portail Azure et à l’aide du module Azure PowerShell de hello.</span><span class="sxs-lookup"><span data-stu-id="a1f9e-150">Data about hello state of extension deployments can be retrieved from hello Azure portal, and by using hello Azure PowerShell module.</span></span> <span data-ttu-id="a1f9e-151">état du déploiement toosee hello des extensions pour une machine virtuelle donnée, exécutez hello commande suivante.</span><span class="sxs-lookup"><span data-stu-id="a1f9e-151">toosee hello deployment state of extensions for a given VM, run hello following command.</span></span>

```powershell
Get-AzureVMExtension -ResourceGroupName myResourceGroup -VMName myVM -Name myExtensionName
```

<span data-ttu-id="a1f9e-152">Exécution de l’extension de sortie nous toofiles connecté trouvé dans hello suivant de répertoire de la machine virtuelle cible hello.</span><span class="sxs-lookup"><span data-stu-id="a1f9e-152">Extension execution output us logged toofiles found in hello following directory on hello target virtual machine.</span></span>

```cmd
C:\WindowsAzure\Logs\Plugins\Microsoft.Compute.CustomScriptExtension
```

<span data-ttu-id="a1f9e-153">script Hello proprement dit est téléchargé dans hello suivant de répertoire de la machine virtuelle cible hello.</span><span class="sxs-lookup"><span data-stu-id="a1f9e-153">hello script itself is downloaded into hello following directory on hello target virtual machine.</span></span>

```cmd
C:\Packages\Plugins\Microsoft.Compute.CustomScriptExtension\1.*\Downloads
```

### <a name="support"></a><span data-ttu-id="a1f9e-154">Support</span><span class="sxs-lookup"><span data-stu-id="a1f9e-154">Support</span></span>

<span data-ttu-id="a1f9e-155">Si vous avez besoin d’aide à tout moment dans cet article, vous pouvez contacter hello experts Azure hello [forums MSDN Azure et le débordement de pile](https://azure.microsoft.com/en-us/support/forums/).</span><span class="sxs-lookup"><span data-stu-id="a1f9e-155">If you need more help at any point in this article, you can contact hello Azure experts on hello [MSDN Azure and Stack Overflow forums](https://azure.microsoft.com/en-us/support/forums/).</span></span> <span data-ttu-id="a1f9e-156">Vous pouvez également signaler un incident au support Azure.</span><span class="sxs-lookup"><span data-stu-id="a1f9e-156">Alternatively, you can file an Azure support incident.</span></span> <span data-ttu-id="a1f9e-157">Accédez toohello [site de support technique Azure](https://azure.microsoft.com/en-us/support/options/) et sélectionnez la prise en charge de Get.</span><span class="sxs-lookup"><span data-stu-id="a1f9e-157">Go toohello [Azure support site](https://azure.microsoft.com/en-us/support/options/) and select Get support.</span></span> <span data-ttu-id="a1f9e-158">Pour plus d’informations sur l’utilisation de Azure prend en charge, lire hello [prise en charge de Microsoft Azure FAQ](https://azure.microsoft.com/en-us/support/faq/).</span><span class="sxs-lookup"><span data-stu-id="a1f9e-158">For information about using Azure Support, read hello [Microsoft Azure support FAQ](https://azure.microsoft.com/en-us/support/faq/).</span></span>
