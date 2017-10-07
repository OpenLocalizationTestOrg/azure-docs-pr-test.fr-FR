---
title: "aaaAzure extension de machine virtuelle de l’Agent de l’Observateur réseau pour Windows | Documents Microsoft"
description: "Déployer hello Agent de l’Observateur réseau sur l’ordinateur virtuel de Windows à l’aide d’une extension de machine virtuelle."
services: virtual-machines-windows
documentationcenter: 
author: dennisg
manager: amku
editor: 
tags: azure-resource-manager
ms.assetid: 27e46af7-2150-45e8-b084-ba33de8c5e3f
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 02/14/2017
ms.author: dennisg
ms.openlocfilehash: 21298706e462ff32c4d314f9a1ad127074ddf481
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="network-watcher-agent-virtual-machine-extension-for-windows"></a><span data-ttu-id="14d08-103">Extension de machine virtuelle Agent Network Watcher pour Windows</span><span class="sxs-lookup"><span data-stu-id="14d08-103">Network Watcher Agent virtual machine extension for Windows</span></span>

## <a name="overview"></a><span data-ttu-id="14d08-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="14d08-104">Overview</span></span>

<span data-ttu-id="14d08-105">[Azure Network Watcher](https://review.docs.microsoft.com/en-us/azure/network-watcher/) est un service d’analyse, de diagnostic et d’analytique des performances réseau permettant de surveiller les réseaux Azure.</span><span class="sxs-lookup"><span data-stu-id="14d08-105">[Azure Network Watcher](https://review.docs.microsoft.com/en-us/azure/network-watcher/) is a network performance monitoring, diagnostic, and analytics service that allows monitoring for Azure networks.</span></span> <span data-ttu-id="14d08-106">Hello, extension de machine virtuelle de l’Agent de l’Observateur réseau est obligatoire pour certaines des fonctionnalités de l’Observateur réseau hello sur des machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="14d08-106">hello Network Watcher Agent virtual machine extension is a requirement for some of hello Network Watcher features on Azure virtual machines.</span></span> <span data-ttu-id="14d08-107">notamment la capture du trafic réseau à la demande et d’autres fonctionnalités avancées.</span><span class="sxs-lookup"><span data-stu-id="14d08-107">This includes capturing network traffic on demand and other advanced functionality.</span></span>

<span data-ttu-id="14d08-108">Cette hello de détails de document pris en charge les options de déploiement et les plateformes pour hello extension de machine virtuelle de l’Agent de l’Observateur réseau pour Windows.</span><span class="sxs-lookup"><span data-stu-id="14d08-108">This document details hello supported platforms and deployment options for hello Network Watcher Agent virtual machine extension for Windows.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="14d08-109">Composants requis</span><span class="sxs-lookup"><span data-stu-id="14d08-109">Prerequisites</span></span>

### <a name="operating-system"></a><span data-ttu-id="14d08-110">Système d’exploitation</span><span class="sxs-lookup"><span data-stu-id="14d08-110">Operating system</span></span>

<span data-ttu-id="14d08-111">Hello, extension de l’Agent de l’Observateur réseau pour Windows puisse être exécuté sur Windows Server 2008 R2, 2012, 2012 R2 et 2016 libère.</span><span class="sxs-lookup"><span data-stu-id="14d08-111">hello Network Watcher Agent extension for Windows can be run against Windows Server 2008 R2, 2012, 2012 R2, and 2016 releases.</span></span> <span data-ttu-id="14d08-112">Notez que hello Nano Server n’est pas prise en charge pour l’instant.</span><span class="sxs-lookup"><span data-stu-id="14d08-112">Note that hello Nano Server is not supported at this time.</span></span>

### <a name="internet-connectivity"></a><span data-ttu-id="14d08-113">Connectivité Internet</span><span class="sxs-lookup"><span data-stu-id="14d08-113">Internet connectivity</span></span>

<span data-ttu-id="14d08-114">Certaines des hello fonctionnalités de l’Agent de l’Observateur réseau exige que l’ordinateur virtuel cible hello toohello connecté Internet.</span><span class="sxs-lookup"><span data-stu-id="14d08-114">Some of hello Network Watcher Agent functionality requires that hello target virtual machine be connected toohello Internet.</span></span> <span data-ttu-id="14d08-115">Sans les connexions sortantes hello capacité tooestablish certaines des fonctionnalités de l’Agent de l’Observateur réseau hello peuvent fonctionner correctement ou deviennent indisponibles.</span><span class="sxs-lookup"><span data-stu-id="14d08-115">Without hello ability tooestablish outgoing connections some of hello Network Watcher Agent features may malfunction or become unavailable.</span></span> <span data-ttu-id="14d08-116">Pour plus d’informations, consultez hello [documentation de l’Observateur réseau](../../network-watcher/network-watcher-monitoring-overview.md).</span><span class="sxs-lookup"><span data-stu-id="14d08-116">For more details, please see hello [Network Watcher documentation](../../network-watcher/network-watcher-monitoring-overview.md).</span></span>

## <a name="extension-schema"></a><span data-ttu-id="14d08-117">Schéma d’extensions</span><span class="sxs-lookup"><span data-stu-id="14d08-117">Extension schema</span></span>

<span data-ttu-id="14d08-118">Hello JSON suivant montre schéma hello pour hello extension de l’Agent de l’Observateur réseau.</span><span class="sxs-lookup"><span data-stu-id="14d08-118">hello following JSON shows hello schema for hello Network Watcher Agent extension.</span></span> <span data-ttu-id="14d08-119">extension de Hello ni requiert ni prend en charge tous les paramètres fournis par l’utilisateur pour l’instant et s’appuie sur sa configuration par défaut.</span><span class="sxs-lookup"><span data-stu-id="14d08-119">hello extension neither requires nor supports any user-supplied settings at this time and relies on its default configuration.</span></span>

```json
{
    "type": "extensions",
    "name": "Microsoft.Azure.NetworkWatcher",
    "apiVersion": "[variables('apiVersion')]",
    "location": "[resourceGroup().location]",
    "dependsOn": [
        "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'))]"
    ],
    "properties": {
        "publisher": "Microsoft.Azure.NetworkWatcher",
        "type": "NetworkWatcherAgentWindows",
        "typeHandlerVersion": "1.4",
        "autoUpgradeMinorVersion": true
    }
}
```

### <a name="property-values"></a><span data-ttu-id="14d08-120">Valeurs de propriétés</span><span class="sxs-lookup"><span data-stu-id="14d08-120">Property values</span></span>

| <span data-ttu-id="14d08-121">Nom</span><span class="sxs-lookup"><span data-stu-id="14d08-121">Name</span></span> | <span data-ttu-id="14d08-122">Valeur/Exemple</span><span class="sxs-lookup"><span data-stu-id="14d08-122">Value / Example</span></span> |
| ---- | ---- |
| <span data-ttu-id="14d08-123">apiVersion</span><span class="sxs-lookup"><span data-stu-id="14d08-123">apiVersion</span></span> | <span data-ttu-id="14d08-124">2015-06-15</span><span class="sxs-lookup"><span data-stu-id="14d08-124">2015-06-15</span></span> |
| <span data-ttu-id="14d08-125">publisher</span><span class="sxs-lookup"><span data-stu-id="14d08-125">publisher</span></span> | <span data-ttu-id="14d08-126">Microsoft.Azure.NetworkWatcher</span><span class="sxs-lookup"><span data-stu-id="14d08-126">Microsoft.Azure.NetworkWatcher</span></span> |
| <span data-ttu-id="14d08-127">type</span><span class="sxs-lookup"><span data-stu-id="14d08-127">type</span></span> | <span data-ttu-id="14d08-128">NetworkWatcherAgentWindows</span><span class="sxs-lookup"><span data-stu-id="14d08-128">NetworkWatcherAgentWindows</span></span> |
| <span data-ttu-id="14d08-129">typeHandlerVersion</span><span class="sxs-lookup"><span data-stu-id="14d08-129">typeHandlerVersion</span></span> | <span data-ttu-id="14d08-130">1.4</span><span class="sxs-lookup"><span data-stu-id="14d08-130">1.4</span></span> |


## <a name="template-deployment"></a><span data-ttu-id="14d08-131">Déploiement de modèle</span><span class="sxs-lookup"><span data-stu-id="14d08-131">Template deployment</span></span>

<span data-ttu-id="14d08-132">Les extensions de machines virtuelles Azure peuvent être déployées avec des modèles Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="14d08-132">Azure VM extensions can be deployed with Azure Resource Manager templates.</span></span> <span data-ttu-id="14d08-133">schéma JSON de Hello détaillé dans la section précédente de hello peut être utilisé dans un hello toorun du modèle Azure Resource Manager extension de l’Agent de l’Observateur réseau pendant un déploiement de modèle Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="14d08-133">hello JSON schema detailed in hello previous section can be used in an Azure Resource Manager template toorun hello Network Watcher Agent extension during an Azure Resource Manager template deployment.</span></span>

## <a name="powershell-deployment"></a><span data-ttu-id="14d08-134">Déploiement PowerShell</span><span class="sxs-lookup"><span data-stu-id="14d08-134">PowerShell deployment</span></span>

<span data-ttu-id="14d08-135">Hello `Set-AzureRmVMExtension` commande peut être utilisé toodeploy hello Agent de l’Observateur réseau machine virtuelle extension tooan machine virtuelle existante.</span><span class="sxs-lookup"><span data-stu-id="14d08-135">hello `Set-AzureRmVMExtension` command can be used toodeploy hello Network Watcher Agent virtual machine extension tooan existing virtual machine.</span></span>

```powershell
Set-AzureRmVMExtension -ResourceGroupName "myResourceGroup1" `
                       -Location "WestUS" `
                       -VMName "myVM1" `
                       -Name "networkWatcherAgent" `
                       -Publisher "Microsoft.Azure.NetworkWatcher" `
                       -Type "NetworkWatcherAgentWindows" `
                       -TypeHandlerVersion "1.4"
```

## <a name="troubleshooting-and-support"></a><span data-ttu-id="14d08-136">Résolution des problèmes et support</span><span class="sxs-lookup"><span data-stu-id="14d08-136">Troubleshooting and support</span></span>

### <a name="troubleshooting"></a><span data-ttu-id="14d08-137">Résolution des problèmes</span><span class="sxs-lookup"><span data-stu-id="14d08-137">Troubleshooting</span></span>

<span data-ttu-id="14d08-138">Données sur l’état de hello de déploiements d’extension peuvent être récupérées à partir de hello portail Azure et à l’aide du module Azure PowerShell de hello.</span><span class="sxs-lookup"><span data-stu-id="14d08-138">Data about hello state of extension deployments can be retrieved from hello Azure portal, and by using hello Azure PowerShell module.</span></span> <span data-ttu-id="14d08-139">état du déploiement hello toosee des extensions pour un ordinateur virtuel donné, hello exécution suite à l’aide de la commande hello module PowerShell Azure.</span><span class="sxs-lookup"><span data-stu-id="14d08-139">toosee hello deployment state of extensions for a given VM, run hello following command using hello Azure PowerShell module.</span></span>

```powershell
Get-AzureRmVMExtension -ResourceGroupName myResourceGroup1 -VMName myVM1 -Name networkWatcherAgent
```

<span data-ttu-id="14d08-140">Exécution de l’extension de sortie est journalisée toofiles trouvé dans hello suivant active :</span><span class="sxs-lookup"><span data-stu-id="14d08-140">Extension execution output is logged toofiles found in hello following directory:</span></span>

```cmd
C:\WindowsAzure\Logs\Plugins\Microsoft.Azure.NetworkWatcher.NetworkWatcherAgentWindows\
```

### <a name="support"></a><span data-ttu-id="14d08-141">Support</span><span class="sxs-lookup"><span data-stu-id="14d08-141">Support</span></span>

<span data-ttu-id="14d08-142">Si vous avez besoin d’aide à tout moment dans cet article, vous pouvez consultez la documentation du Guide de l’utilisateur l’Observateur réseau toohello ou contactez hello Azure experts de hello [forums MSDN Azure et le débordement de pile](https://azure.microsoft.com/en-us/support/forums/).</span><span class="sxs-lookup"><span data-stu-id="14d08-142">If you need more help at any point in this article, you can refer toohello Network Watcher User Guide documentation or contact hello Azure experts on hello [MSDN Azure and Stack Overflow forums](https://azure.microsoft.com/en-us/support/forums/).</span></span> <span data-ttu-id="14d08-143">Vous pouvez également signaler un incident au support Azure.</span><span class="sxs-lookup"><span data-stu-id="14d08-143">Alternatively, you can file an Azure support incident.</span></span> <span data-ttu-id="14d08-144">Accédez toohello [site de support technique Azure](https://azure.microsoft.com/en-us/support/options/) et sélectionnez la prise en charge de Get.</span><span class="sxs-lookup"><span data-stu-id="14d08-144">Go toohello [Azure support site](https://azure.microsoft.com/en-us/support/options/) and select Get support.</span></span> <span data-ttu-id="14d08-145">Pour plus d’informations sur l’utilisation de Azure prend en charge, lire hello [prise en charge de Microsoft Azure FAQ](https://azure.microsoft.com/en-us/support/faq/).</span><span class="sxs-lookup"><span data-stu-id="14d08-145">For information about using Azure Support, read hello [Microsoft Azure support FAQ](https://azure.microsoft.com/en-us/support/faq/).</span></span>
