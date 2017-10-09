---
title: "aaaResize un ordinateur virtuel Windows Azure - modèle de déploiement classique hello | Documents Microsoft"
description: "Redimensionner une machine virtuelle de Windows créée dans le modèle de déploiement classique de hello, à l’aide d’Azure Powershell."
services: virtual-machines-windows
documentationcenter: 
author: Drewm3
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: e3038215-001c-406e-904d-e0f4e326a4c7
ms.service: virtual-machines-windows
ms.workload: na
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 10/19/2016
ms.author: drewm
ms.openlocfilehash: 39fab14431e2351c9515b0611e850eccfec7a798
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="resize-a-windows-vm-created-in-hello-classic-deployment-model"></a><span data-ttu-id="2e32e-103">Redimensionner une machine virtuelle de Windows créé dans le modèle de déploiement classique de hello</span><span class="sxs-lookup"><span data-stu-id="2e32e-103">Resize a Windows VM created in hello classic deployment model</span></span>
<span data-ttu-id="2e32e-104">Cet article explique comment tooresize une machine virtuelle Windows, créé dans le modèle de déploiement classique de hello à l’aide d’Azure Powershell.</span><span class="sxs-lookup"><span data-stu-id="2e32e-104">This article shows you how tooresize a Windows VM, created in hello classic deployment model using Azure Powershell.</span></span>

<span data-ttu-id="2e32e-105">Lorsque vous envisagez hello capacité tooresize une machine virtuelle, il existe deux concepts qui contrôlent la plage hello de machine virtuelle de tailles disponibles tooresize hello.</span><span class="sxs-lookup"><span data-stu-id="2e32e-105">When considering hello ability tooresize a VM, there are two concepts which control hello range of sizes available tooresize hello virtual machine.</span></span> <span data-ttu-id="2e32e-106">Hello premier concept est la région de hello dans lequel votre machine virtuelle est déployée.</span><span class="sxs-lookup"><span data-stu-id="2e32e-106">hello first concept is hello region in which your VM is deployed.</span></span> <span data-ttu-id="2e32e-107">liste de Hello des tailles de machine virtuelle disponibles dans la région est sous l’onglet Services de hello de page web de régions Azure hello.</span><span class="sxs-lookup"><span data-stu-id="2e32e-107">hello list of VM sizes available in region is under hello Services tab of hello Azure Regions web page.</span></span> <span data-ttu-id="2e32e-108">concept de deuxième Hello est votre machine virtuelle qui héberge actuellement un matériel physique hello.</span><span class="sxs-lookup"><span data-stu-id="2e32e-108">hello second concept is hello physical hardware currently hosting your VM.</span></span> <span data-ttu-id="2e32e-109">les serveurs physiques Hello héberge des ordinateurs virtuels sont regroupés dans des clusters de matériel physique commun.</span><span class="sxs-lookup"><span data-stu-id="2e32e-109">hello physical servers hosting VMs are grouped together in clusters of common physical hardware.</span></span> <span data-ttu-id="2e32e-110">méthode Hello de la modification d’une taille de machine virtuelle diffère en fonction de hello souhaitée nouvelle taille de machine virtuelle est prise en charge par cluster de matériel hello hello machine virtuelle qui héberge actuellement.</span><span class="sxs-lookup"><span data-stu-id="2e32e-110">hello method of changing a VM size differs depending on if hello desired new VM size is supported by hello hardware cluster currently hosting hello VM.</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="2e32e-111">Azure dispose de deux modèles de déploiement différents pour créer et utiliser des ressources : [le déploiement Resource Manager et le déploiement classique](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="2e32e-111">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="2e32e-112">Cet article décrit à l’aide du modèle de déploiement classique hello.</span><span class="sxs-lookup"><span data-stu-id="2e32e-112">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="2e32e-113">Microsoft recommande que la plupart des nouveaux déploiements de modèle du Gestionnaire de ressources hello.</span><span class="sxs-lookup"><span data-stu-id="2e32e-113">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="2e32e-114">Vous pouvez également [redimensionner une machine virtuelle créée dans le modèle de déploiement du Gestionnaire de ressources hello](../resize-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="2e32e-114">You can also [resize a VM created in hello Resource Manager deployment model](../resize-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

## <a name="add-your-account"></a><span data-ttu-id="2e32e-115">Ajouter votre compte</span><span class="sxs-lookup"><span data-stu-id="2e32e-115">Add your account</span></span>
<span data-ttu-id="2e32e-116">Vous devez configurer Azure PowerShell toowork avec des ressources Azure classiques.</span><span class="sxs-lookup"><span data-stu-id="2e32e-116">You must configure Azure PowerShell toowork with classic Azure resources.</span></span> <span data-ttu-id="2e32e-117">Suivez les étapes de hello ci-dessous Azure PowerShell tooconfigure toomanage les ressources classiques.</span><span class="sxs-lookup"><span data-stu-id="2e32e-117">Follow hello steps below tooconfigure Azure PowerShell toomanage classic resources.</span></span>

1. <span data-ttu-id="2e32e-118">À l’invite de commandes PowerShell hello, tapez `Add-AzureAccount` et cliquez sur **entrée**.</span><span class="sxs-lookup"><span data-stu-id="2e32e-118">At hello PowerShell prompt, type `Add-AzureAccount` and click **Enter**.</span></span> 
2. <span data-ttu-id="2e32e-119">Tapez hello adresse de messagerie associée à votre abonnement Azure et cliquez sur **continuer**.</span><span class="sxs-lookup"><span data-stu-id="2e32e-119">Type in hello email address associated with your Azure subscription and click **Continue**.</span></span> 
3. <span data-ttu-id="2e32e-120">Tapez hello de mot de passe pour votre compte.</span><span class="sxs-lookup"><span data-stu-id="2e32e-120">Type in hello password for your account.</span></span> 
4. <span data-ttu-id="2e32e-121">Cliquez sur **Se connecter**.</span><span class="sxs-lookup"><span data-stu-id="2e32e-121">Click **Sign in**.</span></span> 

## <a name="resize-in-hello-same-hardware-cluster"></a><span data-ttu-id="2e32e-122">Redimensionner dans hello même cluster de matériel</span><span class="sxs-lookup"><span data-stu-id="2e32e-122">Resize in hello same hardware cluster</span></span>
<span data-ttu-id="2e32e-123">tooresize une taille de tooa de machine virtuelle disponible dans le cluster de matériel hello hébergement hello machine virtuelle, effectuez hello comme suit.</span><span class="sxs-lookup"><span data-stu-id="2e32e-123">tooresize a VM tooa size available in hello hardware cluster hosting hello VM, perform hello following steps.</span></span>

1. <span data-ttu-id="2e32e-124">Exécutez hello suivant de commande PowerShell tailles de machine virtuelle toolist hello disponibles dans le cluster de matériel hello hébergeant un service cloud hello qui contienne hello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="2e32e-124">Run hello following PowerShell command toolist hello VM sizes available in hello hardware cluster hosting hello cloud service which contains hello VM.</span></span>
   
    ```powershell
    Get-AzureService | where {$_.ServiceName -eq "<cloudServiceName>"}
    ```
2. <span data-ttu-id="2e32e-125">Exécutez hello suivant de commandes tooresize hello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="2e32e-125">Run hello following commands tooresize hello VM.</span></span>
   
    ```powershell
    Get-AzureVM -ServiceName <cloudServiceName> -Name <vmName> | Set-AzureVMSize -InstanceSize <newVMSize> | Update-AzureVM
    ```

## <a name="resize-on-a-new-hardware-cluster"></a><span data-ttu-id="2e32e-126">Redimensionner sur un nouveau cluster matériel</span><span class="sxs-lookup"><span data-stu-id="2e32e-126">Resize on a new hardware cluster</span></span>
<span data-ttu-id="2e32e-127">tooresize une taille de tooa de machine virtuelle non disponible dans hello matériel cluster héberge hello VM, hello service cloud et tous les ordinateurs virtuels dans le service cloud hello doivent être recréés.</span><span class="sxs-lookup"><span data-stu-id="2e32e-127">tooresize a VM tooa size not available in hello hardware cluster hosting hello VM, hello cloud service and all VMs in hello cloud service must be recreated.</span></span> <span data-ttu-id="2e32e-128">Chaque service cloud est hébergé sur un cluster de matériel unique pour tous les ordinateurs virtuels dans le service cloud hello doivent avoir une taille qui est pris en charge sur un cluster de matériel.</span><span class="sxs-lookup"><span data-stu-id="2e32e-128">Each cloud service is hosted on a single hardware cluster so all VMs in hello cloud service must be a size that is supported on a hardware cluster.</span></span> <span data-ttu-id="2e32e-129">Hello étapes suivantes décrivent comment tooresize une machine virtuelle en supprimant et en recréant puis hello cloud service.</span><span class="sxs-lookup"><span data-stu-id="2e32e-129">hello following steps will describe how tooresize a VM by deleting and then recreating hello cloud service.</span></span>

1. <span data-ttu-id="2e32e-130">Exécutez hello suivant PowerShell commande toolist hello tailles de machine virtuelle disponibles dans la région de hello.</span><span class="sxs-lookup"><span data-stu-id="2e32e-130">Run hello following PowerShell command toolist hello VM sizes available in hello region.</span></span> 
   
    ```powershell
    Get-AzureLocation | where {$_.Name -eq "<locationName>"}
    ```
2. <span data-ttu-id="2e32e-131">Prenez note de tous les paramètres de configuration pour chaque ordinateur virtuel dans le service cloud hello contenant toobe de machine virtuelle hello redimensionné.</span><span class="sxs-lookup"><span data-stu-id="2e32e-131">Make note of all configuration settings for each VM in hello cloud service which contains hello VM toobe resized.</span></span> 
3. <span data-ttu-id="2e32e-132">Supprimez tous les ordinateurs virtuels dans le service cloud hello en sélectionnant hello option tooretain hello des disques pour chaque machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="2e32e-132">Delete all VMs in hello cloud service selecting hello option tooretain hello disks for each VM.</span></span>
4. <span data-ttu-id="2e32e-133">Recréez toobe de machine virtuelle hello redimensionné à l’aide de la taille de machine virtuelle hello souhaité.</span><span class="sxs-lookup"><span data-stu-id="2e32e-133">Recreate hello VM toobe resized using hello desired VM size.</span></span>
5. <span data-ttu-id="2e32e-134">Recréez toutes les autres machines virtuelles qui étaient dans le service de cloud à l’aide d’une taille de machine virtuelle disponible dans cluster de matériel hello héberge désormais le service de cloud computing hello hello.</span><span class="sxs-lookup"><span data-stu-id="2e32e-134">Recreate all other VMs which were in hello cloud service using a VM size available in hello hardware cluster now hosting hello cloud service.</span></span>

<span data-ttu-id="2e32e-135">Vous trouverez [ici](https://github.com/Azure/azure-vm-scripts) un exemple de script de suppression et de recréation d’un service cloud avec une nouvelle taille de machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="2e32e-135">A sample script for deleting and recreating a cloud service using a new VM size can be found [here](https://github.com/Azure/azure-vm-scripts).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="2e32e-136">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="2e32e-136">Next steps</span></span>
* <span data-ttu-id="2e32e-137">[Redimensionner une machine virtuelle créée dans le modèle de déploiement du Gestionnaire de ressources hello](../resize-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="2e32e-137">[Resize a VM created in hello Resource Manager deployment model](../resize-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

