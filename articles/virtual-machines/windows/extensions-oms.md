---
title: aaaOMS extension de machine virtuelle Azure pour Windows | Documents Microsoft
description: "Déployer l’agent OMS de hello sur la machine virtuelle de Windows à l’aide d’une extension de machine virtuelle."
services: virtual-machines-windows
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: feae6176-2373-4034-b5d9-a32c6b4e1f10
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 03/14/2017
ms.author: nepeters
ms.openlocfilehash: 3000f66c0acdec1d1fad2125b8c6b72a92b1ec92
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="oms-virtual-machine-extension-for-windows"></a><span data-ttu-id="ba399-103">Extension de machine virtuelle OMS pour Windows</span><span class="sxs-lookup"><span data-stu-id="ba399-103">OMS virtual machine extension for Windows</span></span>

<span data-ttu-id="ba399-104">Operations Management Suite (OMS) fournit des fonctionnalités de surveillance, d’alerte et de correction des alertes sur le ressources cloud et locales.</span><span class="sxs-lookup"><span data-stu-id="ba399-104">Operations Management Suite (OMS) provides monitoring, alerting, and alert remediation capabilities across cloud and on-premises assets.</span></span> <span data-ttu-id="ba399-105">Hello, extension de machine virtuelle de l’Agent OMS pour Windows est publié et pris en charge par Microsoft.</span><span class="sxs-lookup"><span data-stu-id="ba399-105">hello OMS Agent virtual machine extension for Windows is published and supported by Microsoft.</span></span> <span data-ttu-id="ba399-106">extension de Hello installe l’agent OMS de hello sur des machines virtuelles et inscrit les machines virtuelles dans un espace de travail OMS existant.</span><span class="sxs-lookup"><span data-stu-id="ba399-106">hello extension installs hello OMS agent on Azure virtual machines, and enrolls virtual machines into an existing OMS workspace.</span></span> <span data-ttu-id="ba399-107">Cette hello de détails de document pris en charge plates-formes, les configurations et les options de déploiement pour hello extension de machine virtuelle OMS pour Windows.</span><span class="sxs-lookup"><span data-stu-id="ba399-107">This document details hello supported platforms, configurations, and deployment options for hello OMS virtual machine extension for Windows.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ba399-108">Composants requis</span><span class="sxs-lookup"><span data-stu-id="ba399-108">Prerequisites</span></span>

### <a name="operating-system"></a><span data-ttu-id="ba399-109">Système d’exploitation</span><span class="sxs-lookup"><span data-stu-id="ba399-109">Operating system</span></span>
<span data-ttu-id="ba399-110">Hello extension OMS Agent pour Windows puisse être exécuté sur Windows Server 2008 R2, 2012, 2012 R2 et 2016 libère.</span><span class="sxs-lookup"><span data-stu-id="ba399-110">hello OMS Agent extension for Windows can be run against Windows Server 2008 R2, 2012, 2012 R2, and 2016 releases.</span></span>

### <a name="internet-connectivity"></a><span data-ttu-id="ba399-111">Connectivité Internet</span><span class="sxs-lookup"><span data-stu-id="ba399-111">Internet connectivity</span></span>
<span data-ttu-id="ba399-112">Hello extension OMS Agent pour Windows requiert que l’ordinateur virtuel cible hello est connecté toohello internet.</span><span class="sxs-lookup"><span data-stu-id="ba399-112">hello OMS Agent extension for Windows requires that hello target virtual machine is connected toohello internet.</span></span> 

## <a name="extension-schema"></a><span data-ttu-id="ba399-113">Schéma d’extensions</span><span class="sxs-lookup"><span data-stu-id="ba399-113">Extension schema</span></span>

<span data-ttu-id="ba399-114">Hello JSON suivant montre schéma hello pour hello extension OMS Agent.</span><span class="sxs-lookup"><span data-stu-id="ba399-114">hello following JSON shows hello schema for hello OMS Agent extension.</span></span> <span data-ttu-id="ba399-115">extension de Hello requiert hello espace de travail et Id de clé à partir de l’espace de travail OMS hello cible, elles sont accessibles dans portail OMS : hello.</span><span class="sxs-lookup"><span data-stu-id="ba399-115">hello extension requires hello workspace Id and workspace key from hello target OMS workspace, these can be found in hello OMS portal.</span></span> <span data-ttu-id="ba399-116">Étant donné que la clé d’espace de travail hello doit être traité comme des données sensibles, il doit être stocké dans une configuration protégée.</span><span class="sxs-lookup"><span data-stu-id="ba399-116">Because hello workspace key should be treated as sensitive data, it should be stored in a protected setting configuration.</span></span> <span data-ttu-id="ba399-117">Les données de paramètre d’extension protégée de machine virtuelle Azure sont chiffrées et déchiffrées uniquement sur la machine virtuelle cible hello.</span><span class="sxs-lookup"><span data-stu-id="ba399-117">Azure VM extension protected setting data is encrypted, and only decrypted on hello target virtual machine.</span></span> <span data-ttu-id="ba399-118">Notez que **workspaceId** et **workspaceKey** respectent la casse.</span><span class="sxs-lookup"><span data-stu-id="ba399-118">Note that **workspaceId** and **workspaceKey** are case-sensitive.</span></span>

```json
{
    "type": "extensions",
    "name": "OMSExtension",
    "apiVersion": "[variables('apiVersion')]",
    "location": "[resourceGroup().location]",
    "dependsOn": [
        "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'))]"
    ],
    "properties": {
        "publisher": "Microsoft.EnterpriseCloud.Monitoring",
        "type": "MicrosoftMonitoringAgent",
        "typeHandlerVersion": "1.0",
        "autoUpgradeMinorVersion": true,
        "settings": {
            "workspaceId": "myWorkSpaceId"
        },
        "protectedSettings": {
            "workspaceKey": "myWorkspaceKey"
        }
    }
}
```
### <a name="property-values"></a><span data-ttu-id="ba399-119">Valeurs de propriétés</span><span class="sxs-lookup"><span data-stu-id="ba399-119">Property values</span></span>

| <span data-ttu-id="ba399-120">Nom</span><span class="sxs-lookup"><span data-stu-id="ba399-120">Name</span></span> | <span data-ttu-id="ba399-121">Valeur/Exemple</span><span class="sxs-lookup"><span data-stu-id="ba399-121">Value / Example</span></span> |
| ---- | ---- |
| <span data-ttu-id="ba399-122">apiVersion</span><span class="sxs-lookup"><span data-stu-id="ba399-122">apiVersion</span></span> | <span data-ttu-id="ba399-123">2015-06-15</span><span class="sxs-lookup"><span data-stu-id="ba399-123">2015-06-15</span></span> |
| <span data-ttu-id="ba399-124">publisher</span><span class="sxs-lookup"><span data-stu-id="ba399-124">publisher</span></span> | <span data-ttu-id="ba399-125">Microsoft.EnterpriseCloud.Monitoring</span><span class="sxs-lookup"><span data-stu-id="ba399-125">Microsoft.EnterpriseCloud.Monitoring</span></span> |
| <span data-ttu-id="ba399-126">type</span><span class="sxs-lookup"><span data-stu-id="ba399-126">type</span></span> | <span data-ttu-id="ba399-127">MicrosoftMonitoringAgent</span><span class="sxs-lookup"><span data-stu-id="ba399-127">MicrosoftMonitoringAgent</span></span> |
| <span data-ttu-id="ba399-128">typeHandlerVersion</span><span class="sxs-lookup"><span data-stu-id="ba399-128">typeHandlerVersion</span></span> | <span data-ttu-id="ba399-129">1.0</span><span class="sxs-lookup"><span data-stu-id="ba399-129">1.0</span></span> |
| <span data-ttu-id="ba399-130">workspaceId (par exemple)</span><span class="sxs-lookup"><span data-stu-id="ba399-130">workspaceId (e.g)</span></span> | <span data-ttu-id="ba399-131">6f680a37-00c6-41c7-a93f-1437e3462574</span><span class="sxs-lookup"><span data-stu-id="ba399-131">6f680a37-00c6-41c7-a93f-1437e3462574</span></span> |
| <span data-ttu-id="ba399-132">workspaceKey (par exemple)</span><span class="sxs-lookup"><span data-stu-id="ba399-132">workspaceKey (e.g)</span></span> | <span data-ttu-id="ba399-133">z4bU3p1/GrnWpQkky4gdabWXAhbWSTz70hm4m2Xt92XI+rSRgE8qVvRhsGo9TXffbrTahyrwv35W0pOqQAU7uQ==</span><span class="sxs-lookup"><span data-stu-id="ba399-133">z4bU3p1/GrnWpQkky4gdabWXAhbWSTz70hm4m2Xt92XI+rSRgE8qVvRhsGo9TXffbrTahyrwv35W0pOqQAU7uQ==</span></span> |

## <a name="template-deployment"></a><span data-ttu-id="ba399-134">Déploiement de modèle</span><span class="sxs-lookup"><span data-stu-id="ba399-134">Template deployment</span></span>

<span data-ttu-id="ba399-135">Les extensions de machines virtuelles Azure peuvent être déployées avec des modèles Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="ba399-135">Azure VM extensions can be deployed with Azure Resource Manager templates.</span></span> <span data-ttu-id="ba399-136">schéma JSON de Hello détaillé dans la section précédente de hello peut être utilisé dans un hello toorun du modèle Azure Resource Manager extension OMS Agent pendant un déploiement de modèle Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="ba399-136">hello JSON schema detailed in hello previous section can be used in an Azure Resource Manager template toorun hello OMS Agent extension during an Azure Resource Manager template deployment.</span></span> <span data-ttu-id="ba399-137">Vous trouverez un exemple de modèle qui inclut l’extension de machine virtuelle de l’Agent OMS hello sur hello [galerie de démarrage rapide Azure](https://github.com/Azure/azure-quickstart-templates/tree/master/201-oms-extension-windows-vm).</span><span class="sxs-lookup"><span data-stu-id="ba399-137">A sample template that includes hello OMS Agent VM extension can be found on hello [Azure Quick Start Gallery](https://github.com/Azure/azure-quickstart-templates/tree/master/201-oms-extension-windows-vm).</span></span> 

<span data-ttu-id="ba399-138">Hello JSON pour une extension de machine virtuelle peut être imbriquée dans une ressource d’ordinateur virtuel hello ou placé au niveau racine de hello ou un niveau supérieur d’un modèle de gestionnaire de ressources JSON.</span><span class="sxs-lookup"><span data-stu-id="ba399-138">hello JSON for a virtual machine extension can be nested inside hello virtual machine resource, or placed at hello root or top level of a Resource Manager JSON template.</span></span> <span data-ttu-id="ba399-139">la sélection élective Hello Hello JSON affecte la valeur hello du nom de la ressource hello et type.</span><span class="sxs-lookup"><span data-stu-id="ba399-139">hello placement of hello JSON affects hello value of hello resource name and type.</span></span> <span data-ttu-id="ba399-140">Pour plus d’informations, consultez [Définition du nom et du type des ressources enfants](../../azure-resource-manager/resource-manager-template-child-resource.md).</span><span class="sxs-lookup"><span data-stu-id="ba399-140">For more information, see [Set name and type for child resources](../../azure-resource-manager/resource-manager-template-child-resource.md).</span></span> 

<span data-ttu-id="ba399-141">Hello suppose extension d’OMS hello est imbriquée dans la ressource d’ordinateur virtuel hello.</span><span class="sxs-lookup"><span data-stu-id="ba399-141">hello following example assumes hello OMS extension is nested inside hello virtual machine resource.</span></span> <span data-ttu-id="ba399-142">Lors de l’imbrication des ressources d’extension de hello, hello JSON est placée dans hello `"resources": []` objet de machine virtuelle de hello.</span><span class="sxs-lookup"><span data-stu-id="ba399-142">When nesting hello extension resource, hello JSON is placed in hello `"resources": []` object of hello virtual machine.</span></span>


```json
{
    "type": "extensions",
    "name": "OMSExtension",
    "apiVersion": "[variables('apiVersion')]",
    "location": "[resourceGroup().location]",
    "dependsOn": [
        "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'))]"
    ],
    "properties": {
        "publisher": "Microsoft.EnterpriseCloud.Monitoring",
        "type": "MicrosoftMonitoringAgent",
        "typeHandlerVersion": "1.0",
        "autoUpgradeMinorVersion": true,
        "settings": {
            "workspaceId": "myWorkSpaceId"
        },
        "protectedSettings": {
            "workspaceKey": "myWorkspaceKey"
        }
    }
}
```

<span data-ttu-id="ba399-143">Lorsque vous placez l’extension hello JSON au niveau racine hello du modèle de hello, nom de la ressource hello inclut un ordinateur virtuel de référence toohello parent, et type de hello reflète configuration imbriqués de hello.</span><span class="sxs-lookup"><span data-stu-id="ba399-143">When placing hello extension JSON at hello root of hello template, hello resource name includes a reference toohello parent virtual machine, and hello type reflects hello nested configuration.</span></span> 

```json
{
    "type": "Microsoft.Compute/virtualMachines/extensions",
    "name": "<parentVmResource>/OMSExtension",
    "apiVersion": "[variables('apiVersion')]",
    "location": "[resourceGroup().location]",
    "dependsOn": [
        "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'))]"
    ],
    "properties": {
        "publisher": "Microsoft.EnterpriseCloud.Monitoring",
        "type": "MicrosoftMonitoringAgent",
        "typeHandlerVersion": "1.0",
        "autoUpgradeMinorVersion": true,
        "settings": {
            "workspaceId": "myWorkSpaceId"
        },
        "protectedSettings": {
            "workspaceKey": "myWorkspaceKey"
        }
    }
}
```

## <a name="powershell-deployment"></a><span data-ttu-id="ba399-144">Déploiement PowerShell</span><span class="sxs-lookup"><span data-stu-id="ba399-144">PowerShell deployment</span></span>

<span data-ttu-id="ba399-145">Hello `Set-AzureRmVMExtension` commande peut être utilisé toodeploy hello Agent OMS machine virtuelle extension tooan machine virtuelle existante.</span><span class="sxs-lookup"><span data-stu-id="ba399-145">hello `Set-AzureRmVMExtension` command can be used toodeploy hello OMS Agent virtual machine extension tooan existing virtual machine.</span></span> <span data-ttu-id="ba399-146">Avant d’exécuter la commande hello, les configurations publiques et privées hello doivent toobe stockée dans une table de hachage de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ba399-146">Before running hello command, hello public and private configurations need toobe stored in a PowerShell hash table.</span></span> 

```powershell
$PublicSettings = @{"workspaceId" = "myWorkspaceId"}
$ProtectedSettings = @{"workspaceKey" = "myWorkspaceKey"}

Set-AzureRmVMExtension -ExtensionName "Microsoft.EnterpriseCloud.Monitoring" `
    -ResourceGroupName "myResourceGroup" `
    -VMName "myVM" `
    -Publisher "Microsoft.EnterpriseCloud.Monitoring" `
    -ExtensionType "MicrosoftMonitoringAgent" `
    -TypeHandlerVersion 1.0 `
    -Settings $PublicSettings `
    -ProtectedSettings $ProtectedSettings `
    -Location WestUS ` 
```

## <a name="troubleshoot-and-support"></a><span data-ttu-id="ba399-147">Dépannage et support technique</span><span class="sxs-lookup"><span data-stu-id="ba399-147">Troubleshoot and support</span></span>

### <a name="troubleshoot"></a><span data-ttu-id="ba399-148">Résolution des problèmes</span><span class="sxs-lookup"><span data-stu-id="ba399-148">Troubleshoot</span></span>

<span data-ttu-id="ba399-149">Données sur l’état de hello de déploiements d’extension peuvent être récupérées à partir de hello portail Azure et à l’aide du module Azure PowerShell de hello.</span><span class="sxs-lookup"><span data-stu-id="ba399-149">Data about hello state of extension deployments can be retrieved from hello Azure portal, and by using hello Azure PowerShell module.</span></span> <span data-ttu-id="ba399-150">état du déploiement hello toosee des extensions pour un ordinateur virtuel donné, hello exécution suite à l’aide de la commande hello module PowerShell Azure.</span><span class="sxs-lookup"><span data-stu-id="ba399-150">toosee hello deployment state of extensions for a given VM, run hello following command using hello Azure PowerShell module.</span></span>

```powershell
Get-AzureRmVMExtension -ResourceGroupName myResourceGroup -VMName myVM -Name myExtensionName
```

<span data-ttu-id="ba399-151">Exécution de l’extension de sortie est journalisée toofiles trouvé dans hello suivant active :</span><span class="sxs-lookup"><span data-stu-id="ba399-151">Extension execution output is logged toofiles found in hello following directory:</span></span>

```cmd
C:\WindowsAzure\Logs\Plugins\Microsoft.EnterpriseCloud.Monitoring.MicrosoftMonitoringAgent\
```

### <a name="support"></a><span data-ttu-id="ba399-152">Support</span><span class="sxs-lookup"><span data-stu-id="ba399-152">Support</span></span>

<span data-ttu-id="ba399-153">Si vous avez besoin d’aide à tout moment dans cet article, vous pouvez contacter hello experts Azure hello [forums MSDN Azure et le débordement de pile](https://azure.microsoft.com/en-us/support/forums/).</span><span class="sxs-lookup"><span data-stu-id="ba399-153">If you need more help at any point in this article, you can contact hello Azure experts on hello [MSDN Azure and Stack Overflow forums](https://azure.microsoft.com/en-us/support/forums/).</span></span> <span data-ttu-id="ba399-154">Vous pouvez également signaler un incident au support Azure.</span><span class="sxs-lookup"><span data-stu-id="ba399-154">Alternatively, you can file an Azure support incident.</span></span> <span data-ttu-id="ba399-155">Accédez toohello [site de support technique Azure](https://azure.microsoft.com/en-us/support/options/) et sélectionnez la prise en charge de Get.</span><span class="sxs-lookup"><span data-stu-id="ba399-155">Go toohello [Azure support site](https://azure.microsoft.com/en-us/support/options/) and select Get support.</span></span> <span data-ttu-id="ba399-156">Pour plus d’informations sur l’utilisation de Azure prend en charge, lire hello [prise en charge de Microsoft Azure FAQ](https://azure.microsoft.com/en-us/support/faq/).</span><span class="sxs-lookup"><span data-stu-id="ba399-156">For information about using Azure Support, read hello [Microsoft Azure support FAQ](https://azure.microsoft.com/en-us/support/faq/).</span></span>
