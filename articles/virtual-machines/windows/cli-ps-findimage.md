---
title: les images aaaSelect machine virtuelle Windows dans Azure | Documents Microsoft
description: "Découvrez comment toouse Azure PowerSHell toodetermine hello publisher, offre, référence (SKU) et la version pour les images de machine virtuelle du Marketplace."
services: virtual-machines-windows
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 188b8974-fabd-4cd3-b7dc-559cbb86b98a
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 07/12/2017
ms.author: danlep
ms.openlocfilehash: 752edcd0935f5141832e49503ae800ea0145e219
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toofind-windows-vm-images-in-hello-azure-marketplace-with-azure-powershell"></a><span data-ttu-id="4d052-103">Comment toofind machine virtuelle Windows images Bonjour Azure Marketplace avec Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="4d052-103">How toofind Windows VM images in hello Azure Marketplace with Azure PowerShell</span></span>

<span data-ttu-id="4d052-104">Cette rubrique décrit comment toouse Azure PowerShell toofind VM images Bonjour Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="4d052-104">This topic describes how toouse Azure PowerShell toofind VM images in hello Azure Marketplace.</span></span> <span data-ttu-id="4d052-105">Utilisez cette toospecify informations une image de Marketplace lorsque vous créez une machine virtuelle Windows.</span><span class="sxs-lookup"><span data-stu-id="4d052-105">Use this information toospecify a Marketplace image when you create a Windows VM.</span></span>

<span data-ttu-id="4d052-106">Assurez-vous que vous installé et configuré hello dernières [module Azure PowerShell](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="4d052-106">Make sure that you installed and configured hello latest [Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>



## <a name="table-of-commonly-used-windows-images"></a><span data-ttu-id="4d052-107">Tableau des images système Windows couramment utilisées</span><span class="sxs-lookup"><span data-stu-id="4d052-107">Table of commonly used Windows images</span></span>
| <span data-ttu-id="4d052-108">PublisherName</span><span class="sxs-lookup"><span data-stu-id="4d052-108">PublisherName</span></span> | <span data-ttu-id="4d052-109">Offer</span><span class="sxs-lookup"><span data-stu-id="4d052-109">Offer</span></span> | <span data-ttu-id="4d052-110">Sku</span><span class="sxs-lookup"><span data-stu-id="4d052-110">Sku</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="4d052-111">MicrosoftWindowsServer</span><span class="sxs-lookup"><span data-stu-id="4d052-111">MicrosoftWindowsServer</span></span> |<span data-ttu-id="4d052-112">WindowsServer</span><span class="sxs-lookup"><span data-stu-id="4d052-112">WindowsServer</span></span> |<span data-ttu-id="4d052-113">2016-centre-de-données</span><span class="sxs-lookup"><span data-stu-id="4d052-113">2016-Datacenter</span></span> |
| <span data-ttu-id="4d052-114">MicrosoftWindowsServer</span><span class="sxs-lookup"><span data-stu-id="4d052-114">MicrosoftWindowsServer</span></span> |<span data-ttu-id="4d052-115">WindowsServer</span><span class="sxs-lookup"><span data-stu-id="4d052-115">WindowsServer</span></span> |<span data-ttu-id="4d052-116">2016-Datacenter-Server-Core</span><span class="sxs-lookup"><span data-stu-id="4d052-116">2016-Datacenter-Server-Core</span></span> |
| <span data-ttu-id="4d052-117">MicrosoftWindowsServer</span><span class="sxs-lookup"><span data-stu-id="4d052-117">MicrosoftWindowsServer</span></span> |<span data-ttu-id="4d052-118">WindowsServer</span><span class="sxs-lookup"><span data-stu-id="4d052-118">WindowsServer</span></span> |<span data-ttu-id="4d052-119">2016-centre-de-données-avec-conteneurs</span><span class="sxs-lookup"><span data-stu-id="4d052-119">2016-Datacenter-with-Containers</span></span> |
| <span data-ttu-id="4d052-120">MicrosoftWindowsServer</span><span class="sxs-lookup"><span data-stu-id="4d052-120">MicrosoftWindowsServer</span></span> |<span data-ttu-id="4d052-121">WindowsServer</span><span class="sxs-lookup"><span data-stu-id="4d052-121">WindowsServer</span></span> |<span data-ttu-id="4d052-122">2016-Nano-Server</span><span class="sxs-lookup"><span data-stu-id="4d052-122">2016-Nano-Server</span></span> |
| <span data-ttu-id="4d052-123">MicrosoftWindowsServer</span><span class="sxs-lookup"><span data-stu-id="4d052-123">MicrosoftWindowsServer</span></span> |<span data-ttu-id="4d052-124">WindowsServer</span><span class="sxs-lookup"><span data-stu-id="4d052-124">WindowsServer</span></span> |<span data-ttu-id="4d052-125">2012-R2-Datacenter</span><span class="sxs-lookup"><span data-stu-id="4d052-125">2012-R2-Datacenter</span></span> |
| <span data-ttu-id="4d052-126">MicrosoftWindowsServer</span><span class="sxs-lookup"><span data-stu-id="4d052-126">MicrosoftWindowsServer</span></span> |<span data-ttu-id="4d052-127">WindowsServer</span><span class="sxs-lookup"><span data-stu-id="4d052-127">WindowsServer</span></span> |<span data-ttu-id="4d052-128">2008-R2-SP1</span><span class="sxs-lookup"><span data-stu-id="4d052-128">2008-R2-SP1</span></span> |
| <span data-ttu-id="4d052-129">MicrosoftDynamicsNAV</span><span class="sxs-lookup"><span data-stu-id="4d052-129">MicrosoftDynamicsNAV</span></span> |<span data-ttu-id="4d052-130">DynamicsNAV</span><span class="sxs-lookup"><span data-stu-id="4d052-130">DynamicsNAV</span></span> |<span data-ttu-id="4d052-131">2017</span><span class="sxs-lookup"><span data-stu-id="4d052-131">2017</span></span> |
| <span data-ttu-id="4d052-132">MicrosoftSharePoint</span><span class="sxs-lookup"><span data-stu-id="4d052-132">MicrosoftSharePoint</span></span> |<span data-ttu-id="4d052-133">MicrosoftSharePointServer</span><span class="sxs-lookup"><span data-stu-id="4d052-133">MicrosoftSharePointServer</span></span> |<span data-ttu-id="4d052-134">2016</span><span class="sxs-lookup"><span data-stu-id="4d052-134">2016</span></span> |
| <span data-ttu-id="4d052-135">MicrosoftSQLServer</span><span class="sxs-lookup"><span data-stu-id="4d052-135">MicrosoftSQLServer</span></span> |<span data-ttu-id="4d052-136">SQL2016-WS2016</span><span class="sxs-lookup"><span data-stu-id="4d052-136">SQL2016-WS2016</span></span> |<span data-ttu-id="4d052-137">Entreprise</span><span class="sxs-lookup"><span data-stu-id="4d052-137">Enterprise</span></span> |
| <span data-ttu-id="4d052-138">MicrosoftSQLServer</span><span class="sxs-lookup"><span data-stu-id="4d052-138">MicrosoftSQLServer</span></span> |<span data-ttu-id="4d052-139">SQL2014SP2-WS2012R2</span><span class="sxs-lookup"><span data-stu-id="4d052-139">SQL2014SP2-WS2012R2</span></span> |<span data-ttu-id="4d052-140">Entreprise</span><span class="sxs-lookup"><span data-stu-id="4d052-140">Enterprise</span></span> |
| <span data-ttu-id="4d052-141">MicrosoftWindowsServerHPCPack</span><span class="sxs-lookup"><span data-stu-id="4d052-141">MicrosoftWindowsServerHPCPack</span></span> |<span data-ttu-id="4d052-142">WindowsServerHPCPack</span><span class="sxs-lookup"><span data-stu-id="4d052-142">WindowsServerHPCPack</span></span> |<span data-ttu-id="4d052-143">2012R2</span><span class="sxs-lookup"><span data-stu-id="4d052-143">2012R2</span></span> |
| <span data-ttu-id="4d052-144">MicrosoftWindowsServerEssentials</span><span class="sxs-lookup"><span data-stu-id="4d052-144">MicrosoftWindowsServerEssentials</span></span> |<span data-ttu-id="4d052-145">WindowsServerEssentials</span><span class="sxs-lookup"><span data-stu-id="4d052-145">WindowsServerEssentials</span></span> |<span data-ttu-id="4d052-146">WindowsServerEssentials</span><span class="sxs-lookup"><span data-stu-id="4d052-146">WindowsServerEssentials</span></span> |

## <a name="find-specific-images"></a><span data-ttu-id="4d052-147">Recherche d’images spécifiques</span><span class="sxs-lookup"><span data-stu-id="4d052-147">Find specific images</span></span>


<span data-ttu-id="4d052-148">Lorsque vous créez une machine virtuelle avec Azure Resource Manager, dans certains cas vous devez toospecify une image avec une combinaison de hello de hello image propriétés suivantes :</span><span class="sxs-lookup"><span data-stu-id="4d052-148">When creating a new virtual machine with Azure Resource Manager, in some cases you need toospecify an image with hello combination of hello following image properties:</span></span>

* <span data-ttu-id="4d052-149">Éditeur</span><span class="sxs-lookup"><span data-stu-id="4d052-149">Publisher</span></span>
* <span data-ttu-id="4d052-150">Offer</span><span class="sxs-lookup"><span data-stu-id="4d052-150">Offer</span></span>
* <span data-ttu-id="4d052-151">SKU</span><span class="sxs-lookup"><span data-stu-id="4d052-151">SKU</span></span>

<span data-ttu-id="4d052-152">Par exemple, utilisez ces valeurs avec hello [Set-AzureRMVMSourceImage](/powershell/module/azurerm.compute/set-azurermvmsourceimage) applet de commande PowerShell ou avec un modèle de groupe de ressources dans lequel vous devez spécifier le type hello de toobe de machine virtuelle créée.</span><span class="sxs-lookup"><span data-stu-id="4d052-152">For example, use these values with hello [Set-AzureRMVMSourceImage](/powershell/module/azurerm.compute/set-azurermvmsourceimage) PowerShell cmdlet, or with a resource group template in which you must specify hello type of VM toobe created.</span></span>

<span data-ttu-id="4d052-153">Si vous devez toodetermine ces valeurs, vous pouvez exécuter hello [Get-AzureRMVMImagePublisher](/powershell/module/azurerm.compute/get-azurermvmimagepublisher), [Get-AzureRMVMImageOffer](/powershell/module/azurerm.compute/get-azurermvmimageoffer), et [Get-AzureRMVMImageSku](/powershell/module/azurerm.compute/get-azurermvmimagesku) applets de commande images hello toonavigate.</span><span class="sxs-lookup"><span data-stu-id="4d052-153">If you need toodetermine these values, you can run hello [Get-AzureRMVMImagePublisher](/powershell/module/azurerm.compute/get-azurermvmimagepublisher), [Get-AzureRMVMImageOffer](/powershell/module/azurerm.compute/get-azurermvmimageoffer), and [Get-AzureRMVMImageSku](/powershell/module/azurerm.compute/get-azurermvmimagesku) cmdlets toonavigate hello images.</span></span> <span data-ttu-id="4d052-154">Vous déterminez ces valeurs :</span><span class="sxs-lookup"><span data-stu-id="4d052-154">You determine these values:</span></span>

1. <span data-ttu-id="4d052-155">Serveurs de publication liste hello image.</span><span class="sxs-lookup"><span data-stu-id="4d052-155">List hello image publishers.</span></span>
2. <span data-ttu-id="4d052-156">pour un éditeur donné, en répertoriant ses offres ;</span><span class="sxs-lookup"><span data-stu-id="4d052-156">For a given publisher, list their offers.</span></span>
3. <span data-ttu-id="4d052-157">pour une offre donnée, en répertoriant ses références SKU.</span><span class="sxs-lookup"><span data-stu-id="4d052-157">For a given offer, list their SKUs.</span></span>

<span data-ttu-id="4d052-158">Tout d’abord, la liste des éditeurs de hello avec hello suivant les commandes :</span><span class="sxs-lookup"><span data-stu-id="4d052-158">First, list hello publishers with hello following commands:</span></span>

```powershell
$locName="<Azure location, such as West US>"
Get-AzureRMVMImagePublisher -Location $locName | Select PublisherName
```

<span data-ttu-id="4d052-159">Renseignez le nom de votre serveur de publication choisie et exécutez hello suivant les commandes :</span><span class="sxs-lookup"><span data-stu-id="4d052-159">Fill in your chosen publisher name and run hello following commands:</span></span>

```powershell
$pubName="<publisher>"
Get-AzureRMVMImageOffer -Location $locName -Publisher $pubName | Select Offer
```

<span data-ttu-id="4d052-160">Renseignez le nom de votre offre choisie et exécutez hello suivant les commandes :</span><span class="sxs-lookup"><span data-stu-id="4d052-160">Fill in your chosen offer name and run hello following commands:</span></span>

```powershell
$offerName="<offer>"
Get-AzureRMVMImageSku -Location $locName -Publisher $pubName -Offer $offerName | Select Skus
```

<span data-ttu-id="4d052-161">À partir de la sortie de hello Hello `Get-AzureRMVMImageSku` de commande, vous disposez de toutes les informations de hello vous avez besoin d’une image de hello toospecify pour une machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="4d052-161">From hello output of hello `Get-AzureRMVMImageSku` command, you have all hello information you need toospecify hello image for a new virtual machine.</span></span>

<span data-ttu-id="4d052-162">Hello Voici un exemple complet :</span><span class="sxs-lookup"><span data-stu-id="4d052-162">hello following shows a full example:</span></span>

```powershell
$locName="West US"
Get-AzureRMVMImagePublisher -Location $locName | Select PublisherName

```

<span data-ttu-id="4d052-163">Output:</span><span class="sxs-lookup"><span data-stu-id="4d052-163">Output:</span></span>

```
PublisherName
-------------
a10networks
aiscaler-cache-control-ddos-and-url-rewriting-
alertlogic
AlertLogic.Extension
Barracuda.Azure.ConnectivityAgent
barracudanetworks
basho
boxless
bssw
Canonical
...
```

<span data-ttu-id="4d052-164">Pour le serveur de publication « MicrosoftWindowsServer » hello :</span><span class="sxs-lookup"><span data-stu-id="4d052-164">For hello "MicrosoftWindowsServer" publisher:</span></span>

```powershell
$pubName="MicrosoftWindowsServer"
Get-AzureRMVMImageOffer -Location $locName -Publisher $pubName | Select Offer
```

<span data-ttu-id="4d052-165">Output:</span><span class="sxs-lookup"><span data-stu-id="4d052-165">Output:</span></span>

```
Offer
-----
Windows-HUB
WindowsServer
WindowsServer-HUB
```

<span data-ttu-id="4d052-166">Pour l’offre de « Windows Server » hello :</span><span class="sxs-lookup"><span data-stu-id="4d052-166">For hello "WindowsServer" offer:</span></span>

```powershell
$offerName="WindowsServer"
Get-AzureRMVMImageSku -Location $locName -Publisher $pubName -Offer $offerName | Select Skus
```

<span data-ttu-id="4d052-167">Output:</span><span class="sxs-lookup"><span data-stu-id="4d052-167">Output:</span></span>

```
Skus
----
2008-R2-SP1
2008-R2-SP1-smalldisk
2012-Datacenter
2012-Datacenter-smalldisk
2012-R2-Datacenter
2012-R2-Datacenter-smalldisk
2016-Datacenter
2016-Datacenter-Server-Core
2016-Datacenter-Server-Core-smalldisk
2016-Datacenter-smalldisk
2016-Datacenter-with-Containers
2016-Nano-Server
```

<span data-ttu-id="4d052-168">À partir de cette liste, copiez hello choisi le nom de référence (SKU), et que toutes les informations de hello pour hello `Set-AzureRMVMSourceImage` applet de commande PowerShell ou d’un modèle de groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="4d052-168">From this list, copy hello chosen SKU name, and you have all hello information for hello `Set-AzureRMVMSourceImage` PowerShell cmdlet or for a resource group template.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4d052-169">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="4d052-169">Next steps</span></span>
<span data-ttu-id="4d052-170">À présent, vous pouvez choisir précisément hello image lequel toouse.</span><span class="sxs-lookup"><span data-stu-id="4d052-170">Now you can choose precisely hello image you want toouse.</span></span> <span data-ttu-id="4d052-171">voir d’un ordinateur virtuel rapidement en utilisant les informations d’image de hello, qui vous venez de trouver, toocreate [créer une machine virtuelle Windows avec PowerShell](quick-create-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="4d052-171">toocreate a virtual machine quickly by using hello image information, which you just found, see [Create a Windows virtual machine with PowerShell](quick-create-powershell.md).</span></span>
