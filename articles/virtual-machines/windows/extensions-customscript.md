---
title: "aaaAzure Extension de Script personnalisé pour Windows | Documents Microsoft"
description: "Automatiser les tâches de configuration de machine virtuelle Windows à l’aide d’extension de Script personnalisé hello"
services: virtual-machines-windows
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: f4181fee-7a9d-4a1c-b517-52956f5b7fa1
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 07/16/2017
ms.author: nepeters
ms.openlocfilehash: 97e065242e9fed116ee20b074f4e302a0cd10585
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="custom-script-extension-for-windows"></a><span data-ttu-id="0bdca-103">Extension de script personnalisé pour Windows</span><span class="sxs-lookup"><span data-stu-id="0bdca-103">Custom Script Extension for Windows</span></span>

<span data-ttu-id="0bdca-104">Extension de Script personnalisé de Hello télécharge et exécute des scripts sur les machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="0bdca-104">hello Custom Script Extension downloads and executes scripts on Azure virtual machines.</span></span> <span data-ttu-id="0bdca-105">Cette extension est utile pour la configuration post-déploiement, l’installation de logiciels ou toute autre tâche de configuration ou de gestion.</span><span class="sxs-lookup"><span data-stu-id="0bdca-105">This extension is useful for post deployment configuration, software installation, or any other configuration / management task.</span></span> <span data-ttu-id="0bdca-106">Scripts pouvant être téléchargés à partir de GitHub ou de stockage Azure, ou toohello portail Azure à l’extension de durée d’exécution.</span><span class="sxs-lookup"><span data-stu-id="0bdca-106">Scripts can be downloaded from Azure storage or GitHub, or provided toohello Azure portal at extension run time.</span></span> <span data-ttu-id="0bdca-107">Hello, extension de Script personnalisé s’intègre aux modèles Azure Resource Manager et peut également être exécuté à l’aide de hello CLI d’Azure, PowerShell, portail Azure ou hello API REST de Machine virtuelle Azure.</span><span class="sxs-lookup"><span data-stu-id="0bdca-107">hello Custom Script extension integrates with Azure Resource Manager templates, and can also be run using hello Azure CLI, PowerShell, Azure portal, or hello Azure Virtual Machine REST API.</span></span>

<span data-ttu-id="0bdca-108">Ce document décrit en détail comment toouse hello Extension de Script personnalisé utilisant hello module Azure PowerShell, modèles Azure Resource Manager et informations de dépannage sur les systèmes Windows.</span><span class="sxs-lookup"><span data-stu-id="0bdca-108">This document details how toouse hello Custom Script Extension using hello Azure PowerShell module, Azure Resource Manager templates, and details troubleshooting steps on Windows systems.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0bdca-109">Composants requis</span><span class="sxs-lookup"><span data-stu-id="0bdca-109">Prerequisites</span></span>

### <a name="operating-system"></a><span data-ttu-id="0bdca-110">Système d’exploitation</span><span class="sxs-lookup"><span data-stu-id="0bdca-110">Operating System</span></span>

<span data-ttu-id="0bdca-111">Hello, Extension de Script personnalisé pour Windows puisse être exécuté sur Windows Server 2008 R2, 2012, 2012 R2 et 2016 libère.</span><span class="sxs-lookup"><span data-stu-id="0bdca-111">hello Custom Script Extension for Windows can be run against Windows Server 2008 R2, 2012, 2012 R2, and 2016 releases.</span></span>

### <a name="script-location"></a><span data-ttu-id="0bdca-112">Emplacement du script</span><span class="sxs-lookup"><span data-stu-id="0bdca-112">Script Location</span></span>

<span data-ttu-id="0bdca-113">script de Hello doit toobe stockée dans le stockage Blob Azure, ou tout autre emplacement accessible via une URL valide.</span><span class="sxs-lookup"><span data-stu-id="0bdca-113">hello script needs toobe stored in Azure Blob storage, or any other location accessible through a valid URL.</span></span>

### <a name="internet-connectivity"></a><span data-ttu-id="0bdca-114">Connectivité Internet</span><span class="sxs-lookup"><span data-stu-id="0bdca-114">Internet Connectivity</span></span>

<span data-ttu-id="0bdca-115">Hello Extension de Script personnalisé pour Windows requiert que l’ordinateur virtuel cible hello est connecté toohello internet.</span><span class="sxs-lookup"><span data-stu-id="0bdca-115">hello Custom Script Extension for Windows requires that hello target virtual machine is connected toohello internet.</span></span> 

## <a name="extension-schema"></a><span data-ttu-id="0bdca-116">Schéma d’extensions</span><span class="sxs-lookup"><span data-stu-id="0bdca-116">Extension schema</span></span>

<span data-ttu-id="0bdca-117">Hello JSON suivant montre schéma hello pour hello Extension de Script personnalisé.</span><span class="sxs-lookup"><span data-stu-id="0bdca-117">hello following JSON shows hello schema for hello Custom Script Extension.</span></span> <span data-ttu-id="0bdca-118">extension de Hello nécessite un emplacement de script (le stockage Azure ou un autre emplacement avec une URL valide) et un tooexecute de commande.</span><span class="sxs-lookup"><span data-stu-id="0bdca-118">hello extension requires a script location (Azure Storage or other location with valid URL), and a command tooexecute.</span></span> <span data-ttu-id="0bdca-119">Si vous utilisez le stockage Azure en tant que source du script hello, une clé de compte et le nom de compte stockage Azure est requise.</span><span class="sxs-lookup"><span data-stu-id="0bdca-119">If using Azure Storage as hello script source, an Azure storage account name and account key is required.</span></span> <span data-ttu-id="0bdca-120">Ces éléments doivent être considérés comme des données sensibles et spécifiés dans la configuration de paramètre protégé hello extensions.</span><span class="sxs-lookup"><span data-stu-id="0bdca-120">These items should be treated as sensitive data and specified in hello extensions protected setting configuration.</span></span> <span data-ttu-id="0bdca-121">Les données de paramètre d’extension protégée de machine virtuelle Azure sont chiffrées et déchiffrées uniquement sur la machine virtuelle cible hello.</span><span class="sxs-lookup"><span data-stu-id="0bdca-121">Azure VM extension protected setting data is encrypted, and only decrypted on hello target virtual machine.</span></span>

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
        "typeHandlerVersion": "1.9",
        "autoUpgradeMinorVersion": true,
        "settings": {
            "fileUris": [
                "script location"
            ]
        },
        "protectedSettings": {
            "commandToExecute": "myExecutionCommand",
            "storageAccountName": "myStorageAccountName",
            "storageAccountKey": "myStorageAccountKey"
        }
    }
}
```

### <a name="property-values"></a><span data-ttu-id="0bdca-122">Valeurs de propriétés</span><span class="sxs-lookup"><span data-stu-id="0bdca-122">Property values</span></span>

| <span data-ttu-id="0bdca-123">Nom</span><span class="sxs-lookup"><span data-stu-id="0bdca-123">Name</span></span> | <span data-ttu-id="0bdca-124">Valeur/Exemple</span><span class="sxs-lookup"><span data-stu-id="0bdca-124">Value / Example</span></span> |
| ---- | ---- |
| <span data-ttu-id="0bdca-125">apiVersion</span><span class="sxs-lookup"><span data-stu-id="0bdca-125">apiVersion</span></span> | <span data-ttu-id="0bdca-126">2015-06-15</span><span class="sxs-lookup"><span data-stu-id="0bdca-126">2015-06-15</span></span> |
| <span data-ttu-id="0bdca-127">publisher</span><span class="sxs-lookup"><span data-stu-id="0bdca-127">publisher</span></span> | <span data-ttu-id="0bdca-128">Microsoft.Compute</span><span class="sxs-lookup"><span data-stu-id="0bdca-128">Microsoft.Compute</span></span> |
| <span data-ttu-id="0bdca-129">type</span><span class="sxs-lookup"><span data-stu-id="0bdca-129">type</span></span> | <span data-ttu-id="0bdca-130">extensions</span><span class="sxs-lookup"><span data-stu-id="0bdca-130">extensions</span></span> |
| <span data-ttu-id="0bdca-131">typeHandlerVersion</span><span class="sxs-lookup"><span data-stu-id="0bdca-131">typeHandlerVersion</span></span> | <span data-ttu-id="0bdca-132">1.9</span><span class="sxs-lookup"><span data-stu-id="0bdca-132">1.9</span></span> |
| <span data-ttu-id="0bdca-133">fileUris (p. ex.)</span><span class="sxs-lookup"><span data-stu-id="0bdca-133">fileUris (e.g)</span></span> | <span data-ttu-id="0bdca-134">https://raw.githubusercontent.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-windows/scripts/configure-music-app.ps1</span><span class="sxs-lookup"><span data-stu-id="0bdca-134">https://raw.githubusercontent.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-windows/scripts/configure-music-app.ps1</span></span> |
| <span data-ttu-id="0bdca-135">commandToExecute (p. ex.)</span><span class="sxs-lookup"><span data-stu-id="0bdca-135">commandToExecute (e.g)</span></span> | <span data-ttu-id="0bdca-136">powershell -ExecutionPolicy Unrestricted -File configure-music-app.ps1</span><span class="sxs-lookup"><span data-stu-id="0bdca-136">powershell -ExecutionPolicy Unrestricted -File configure-music-app.ps1</span></span> |
| <span data-ttu-id="0bdca-137">storageAccountName (p. ex.)</span><span class="sxs-lookup"><span data-stu-id="0bdca-137">storageAccountName (e.g)</span></span> | <span data-ttu-id="0bdca-138">examplestorageacct</span><span class="sxs-lookup"><span data-stu-id="0bdca-138">examplestorageacct</span></span> |
| <span data-ttu-id="0bdca-139">storageAccountKey (p. ex.)</span><span class="sxs-lookup"><span data-stu-id="0bdca-139">storageAccountKey (e.g)</span></span> | <span data-ttu-id="0bdca-140">TmJK/1N3AbAZ3q/+hOXoi/l73zOqsaxXDhqa9Y83/v5UpXQp2DQIBuv2Tifp60cE/OaHsJZmQZ7teQfczQj8hg==</span><span class="sxs-lookup"><span data-stu-id="0bdca-140">TmJK/1N3AbAZ3q/+hOXoi/l73zOqsaxXDhqa9Y83/v5UpXQp2DQIBuv2Tifp60cE/OaHsJZmQZ7teQfczQj8hg==</span></span> |

<span data-ttu-id="0bdca-141">**Remarque** : ces noms de propriété respectent la casse.</span><span class="sxs-lookup"><span data-stu-id="0bdca-141">**Note** - these property names are case sensitive.</span></span> <span data-ttu-id="0bdca-142">Utiliser des noms de hello comme indiqué ci-dessus tooavoid les problèmes de déploiement.</span><span class="sxs-lookup"><span data-stu-id="0bdca-142">Use hello names as seen above tooavoid deployment issues.</span></span>

## <a name="template-deployment"></a><span data-ttu-id="0bdca-143">Déploiement de modèle</span><span class="sxs-lookup"><span data-stu-id="0bdca-143">Template deployment</span></span>

<span data-ttu-id="0bdca-144">Les extensions de machines virtuelles Azure peuvent être déployées avec des modèles Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="0bdca-144">Azure VM extensions can be deployed with Azure Resource Manager templates.</span></span> <span data-ttu-id="0bdca-145">schéma JSON de Hello détaillé dans la section précédente de hello peut être utilisé dans un hello toorun du modèle Azure Resource Manager Extension de Script personnalisé pendant un déploiement de modèle Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="0bdca-145">hello JSON schema detailed in hello previous section can be used in an Azure Resource Manager template toorun hello Custom Script Extension during an Azure Resource Manager template deployment.</span></span> <span data-ttu-id="0bdca-146">Un exemple de modèle qui inclut hello Extension de Script personnalisé se trouve ici, [GitHub](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows).</span><span class="sxs-lookup"><span data-stu-id="0bdca-146">A sample template that includes hello Custom Script Extension can be found here, [GitHub](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows).</span></span>

## <a name="powershell-deployment"></a><span data-ttu-id="0bdca-147">Déploiement PowerShell</span><span class="sxs-lookup"><span data-stu-id="0bdca-147">PowerShell deployment</span></span>

<span data-ttu-id="0bdca-148">Hello `Set-AzureRmVMCustomScriptExtension` commande peut être utilisé tooadd hello Script personnalisé extension tooan ordinateur virtuel.</span><span class="sxs-lookup"><span data-stu-id="0bdca-148">hello `Set-AzureRmVMCustomScriptExtension` command can be used tooadd hello Custom Script extension tooan existing virtual machine.</span></span> <span data-ttu-id="0bdca-149">Pour plus d’informations, consultez [Set-AzureRmVMCustomScriptExtension](https://docs.microsoft.com/en-us/powershell/resourcemanager/azurerm.compute/v2.1.0/set-azurermvmcustomscriptextension).</span><span class="sxs-lookup"><span data-stu-id="0bdca-149">For more information, see [Set-AzureRmVMCustomScriptExtension ](https://docs.microsoft.com/en-us/powershell/resourcemanager/azurerm.compute/v2.1.0/set-azurermvmcustomscriptextension).</span></span>
```powershell
Set-AzureRmVMCustomScriptExtension -ResourceGroupName myResourceGroup `
    -VMName myVM `
    -Location myLocation `
    -FileUri myURL `
    -Run 'myScript.ps1' `
    -Name DemoScriptExtension
```

## <a name="troubleshoot-and-support"></a><span data-ttu-id="0bdca-150">Dépannage et support technique</span><span class="sxs-lookup"><span data-stu-id="0bdca-150">Troubleshoot and support</span></span>

### <a name="troubleshoot"></a><span data-ttu-id="0bdca-151">Résolution des problèmes</span><span class="sxs-lookup"><span data-stu-id="0bdca-151">Troubleshoot</span></span>

<span data-ttu-id="0bdca-152">Données sur l’état de hello de déploiements d’extension peuvent être récupérées à partir de hello portail Azure et à l’aide du module Azure PowerShell de hello.</span><span class="sxs-lookup"><span data-stu-id="0bdca-152">Data about hello state of extension deployments can be retrieved from hello Azure portal, and by using hello Azure PowerShell module.</span></span> <span data-ttu-id="0bdca-153">état du déploiement toosee hello des extensions pour une machine virtuelle donnée, exécutez hello commande suivante.</span><span class="sxs-lookup"><span data-stu-id="0bdca-153">toosee hello deployment state of extensions for a given VM, run hello following command.</span></span>

```powershell
Get-AzureRmVMExtension -ResourceGroupName myResourceGroup -VMName myVM -Name myExtensionName
```

<span data-ttu-id="0bdca-154">Exécution de l’extension de sortie est toofiles connecté sous hello suivant active sur la machine virtuelle cible hello.</span><span class="sxs-lookup"><span data-stu-id="0bdca-154">Extension execution output is logged toofiles found under hello following directory on hello target virtual machine.</span></span>
```cmd
C:\WindowsAzure\Logs\Plugins\Microsoft.Compute.CustomScriptExtension
```

<span data-ttu-id="0bdca-155">Hello spécifié les fichiers sont téléchargés dans hello suivant de répertoire de la machine virtuelle cible hello.</span><span class="sxs-lookup"><span data-stu-id="0bdca-155">hello specified files are downloaded into hello following directory on hello target virtual machine.</span></span>
```cmd
C:\Packages\Plugins\Microsoft.Compute.CustomScriptExtension\1.*\Downloads\<n>
```
<span data-ttu-id="0bdca-156">où `<n>` est un entier décimal qui peut-être changer entre les exécutions de l’extension de hello.</span><span class="sxs-lookup"><span data-stu-id="0bdca-156">where `<n>` is a decimal integer which may change between executions of hello extension.</span></span>  <span data-ttu-id="0bdca-157">Hello `1.*` valeur correspond à celle en cours réel, de hello `typeHandlerVersion` valeur de l’extension hello.</span><span class="sxs-lookup"><span data-stu-id="0bdca-157">hello `1.*` value matches hello actual, current `typeHandlerVersion` value of hello extension.</span></span>  <span data-ttu-id="0bdca-158">Par exemple, le répertoire réels de hello peut être `C:\Packages\Plugins\Microsoft.Compute.CustomScriptExtension\1.8\Downloads\2`.</span><span class="sxs-lookup"><span data-stu-id="0bdca-158">For example, hello actual directory could be `C:\Packages\Plugins\Microsoft.Compute.CustomScriptExtension\1.8\Downloads\2`.</span></span>  

<span data-ttu-id="0bdca-159">Lors de l’exécution hello `commandToExecute` commande, extension de hello ont définira ce répertoire (par exemple, `...\Downloads\2`) en tant que répertoire de travail actuel hello.</span><span class="sxs-lookup"><span data-stu-id="0bdca-159">When executing hello `commandToExecute` command, hello extension will have set this directory (e.g., `...\Downloads\2`) as hello current working directory.</span></span> <span data-ttu-id="0bdca-160">Cette utilisation de hello permet des fichiers de chemins d’accès relatifs toolocate hello téléchargés via hello `fileURIs` propriété.</span><span class="sxs-lookup"><span data-stu-id="0bdca-160">This enables hello use of relative paths toolocate hello files downloaded via hello `fileURIs` property.</span></span> <span data-ttu-id="0bdca-161">Consultez le tableau hello ci-dessous pour obtenir des exemples.</span><span class="sxs-lookup"><span data-stu-id="0bdca-161">See hello table below for examples.</span></span>

<span data-ttu-id="0bdca-162">Étant donné que le chemin d’accès absolu de téléchargement de hello peut varier au fil du temps, il s’agit d’une meilleure tooopt des chemins d’accès/fichier de script relatif Bonjour `commandToExecute` de chaîne, chaque fois que possible.</span><span class="sxs-lookup"><span data-stu-id="0bdca-162">Since hello absolute download path may vary over time, it is better tooopt for relative script/file paths in hello `commandToExecute` string, whenever possible.</span></span> <span data-ttu-id="0bdca-163">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="0bdca-163">For example:</span></span>
```json
    "commandToExecute": "powershell.exe . . . -File './scripts/myscript.ps1'"
```

<span data-ttu-id="0bdca-164">Les informations de chemin d’accès après le premier segment URI hello est conservé pour les fichiers téléchargés via hello `fileUris` liste de propriétés.</span><span class="sxs-lookup"><span data-stu-id="0bdca-164">Path information after hello first URI segment is retained for files downloaded via hello `fileUris` property list.</span></span>  <span data-ttu-id="0bdca-165">Comme indiqué dans le tableau hello ci-dessous, les fichiers téléchargés sont mappés à structure de téléchargement dans les sous-répertoires tooreflect hello Hello `fileUris` valeurs.</span><span class="sxs-lookup"><span data-stu-id="0bdca-165">As shown in hello table below, downloaded files are mapped into download subdirectories tooreflect hello structure of hello `fileUris` values.</span></span>  

#### <a name="examples-of-downloaded-files"></a><span data-ttu-id="0bdca-166">Exemples de fichiers téléchargés</span><span class="sxs-lookup"><span data-stu-id="0bdca-166">Examples of Downloaded Files</span></span>

| <span data-ttu-id="0bdca-167">URI dans fileUris</span><span class="sxs-lookup"><span data-stu-id="0bdca-167">URI in fileUris</span></span> | <span data-ttu-id="0bdca-168">Emplacement téléchargé relatif</span><span class="sxs-lookup"><span data-stu-id="0bdca-168">Relative downloaded location</span></span> | <span data-ttu-id="0bdca-169">Emplacement téléchargé absolu*</span><span class="sxs-lookup"><span data-stu-id="0bdca-169">Absolute downloaded location *</span></span> |
| ---- | ------- |:--- |
| `https://someAcct.blob.core.windows.net/aContainer/scripts/myscript.ps1` | `./scripts/myscript.ps1` |`C:\Packages\Plugins\Microsoft.Compute.CustomScriptExtension\1.8\Downloads\2\scripts\myscript.ps1`  |
| `https://someAcct.blob.core.windows.net/aContainer/topLevel.ps1` | `./topLevel.ps1` | `C:\Packages\Plugins\Microsoft.Compute.CustomScriptExtension\1.8\Downloads\2\topLevel.ps1` |

<span data-ttu-id="0bdca-170">\*Comme ci-dessus, chemins d’accès du répertoire absolu hello change sur la durée de vie hello Hello machine virtuelle, mais pas dans une seule exécution de l’extension CustomScript de hello.</span><span class="sxs-lookup"><span data-stu-id="0bdca-170">\* As above, hello absolute directory paths will change over hello lifetime of hello VM, but not within a single execution of hello CustomScript extension.</span></span>

### <a name="support"></a><span data-ttu-id="0bdca-171">Support</span><span class="sxs-lookup"><span data-stu-id="0bdca-171">Support</span></span>

<span data-ttu-id="0bdca-172">Si vous avez besoin d’aide à tout moment dans cet article, vous pouvez contacter hello experts Azure hello [forums MSDN Azure et Stack Overflow] (https://azure.microsoft.com/en-us/support/forums/).</span><span class="sxs-lookup"><span data-stu-id="0bdca-172">If you need more help at any point in this article, you can contact hello Azure experts on hello [MSDN Azure and Stack Overflow forums] (https://azure.microsoft.com/en-us/support/forums/).</span></span> <span data-ttu-id="0bdca-173">Vous pouvez également signaler un incident au support Azure.</span><span class="sxs-lookup"><span data-stu-id="0bdca-173">Alternatively, you can file an Azure support incident.</span></span> <span data-ttu-id="0bdca-174">Accédez toohello [site de support technique Azure](https://azure.microsoft.com/en-us/support/options/) et sélectionnez la prise en charge de Get.</span><span class="sxs-lookup"><span data-stu-id="0bdca-174">Go toohello [Azure support site](https://azure.microsoft.com/en-us/support/options/) and select Get support.</span></span> <span data-ttu-id="0bdca-175">Pour plus d’informations sur l’utilisation de Azure prend en charge, lire hello [prise en charge de Microsoft Azure FAQ](https://azure.microsoft.com/en-us/support/faq/).</span><span class="sxs-lookup"><span data-stu-id="0bdca-175">For information about using Azure Support, read hello [Microsoft Azure support FAQ](https://azure.microsoft.com/en-us/support/faq/).</span></span>
