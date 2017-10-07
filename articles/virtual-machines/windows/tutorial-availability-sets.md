---
title: "aaaAvailability définit le didacticiel pour les machines virtuelles Windows dans Azure | Documents Microsoft"
description: "Découvrez hello disponibilité définit pour les machines virtuelles Windows dans Azure."
documentationcenter: 
services: virtual-machines-windows
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/08/2017
ms.author: cynthn
ms.custom: mvc
ms.openlocfilehash: 853775c5f126dd815c1933f9d71d2274a75ea661
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-availability-sets"></a><span data-ttu-id="702a9-103">Comment à haute disponibilité de toouse</span><span class="sxs-lookup"><span data-stu-id="702a9-103">How toouse availability sets</span></span>

<span data-ttu-id="702a9-104">Dans ce didacticiel, vous allez apprendre comment la disponibilité de hello tooincrease et la fiabilité de vos solutions d’ordinateur virtuel sur Azure à l’aide d’une fonctionnalité appelée haute disponibilité.</span><span class="sxs-lookup"><span data-stu-id="702a9-104">In this tutorial, you will learn how tooincrease hello availability and reliability of your Virtual Machine solutions on Azure using a capability called Availability Sets.</span></span> <span data-ttu-id="702a9-105">Haute disponibilité vous assurer que hello machines virtuelles que vous déployez sur Azure sont réparties entre plusieurs clusters matérielles isolées.</span><span class="sxs-lookup"><span data-stu-id="702a9-105">Availability sets ensure that hello VMs you deploy on Azure are distributed across multiple isolated hardware clusters.</span></span> <span data-ttu-id="702a9-106">Cela garantit que si une défaillance matérielle ou logicielle dans Azure se produit, qu’un ensemble sous-chemin de vos machines virtuelles est concerné et que votre solution globale resteront disponibles et opérationnels du point de vue hello de vos clients à l’utiliser.</span><span class="sxs-lookup"><span data-stu-id="702a9-106">Doing this ensures that if a hardware or software failure within Azure happens, only a sub-set of your VMs will be impacted and that your overall solution will remain available and operational from hello perspective of your customers using it.</span></span> 

<span data-ttu-id="702a9-107">Ce didacticiel vous montre comment effectuer les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="702a9-107">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="702a9-108">Créer un groupe à haute disponibilité</span><span class="sxs-lookup"><span data-stu-id="702a9-108">Create an availability set</span></span>
> * <span data-ttu-id="702a9-109">Créer une machine virtuelle dans un groupe à haute disponibilité</span><span class="sxs-lookup"><span data-stu-id="702a9-109">Create a VM in an availability set</span></span>
> * <span data-ttu-id="702a9-110">Vérifier les tailles de machines virtuelles disponibles</span><span class="sxs-lookup"><span data-stu-id="702a9-110">Check available VM sizes</span></span>

<span data-ttu-id="702a9-111">Ce didacticiel nécessite hello Azure PowerShell version 3.6 ou version ultérieure du module.</span><span class="sxs-lookup"><span data-stu-id="702a9-111">This tutorial requires hello Azure PowerShell module version 3.6 or later.</span></span> <span data-ttu-id="702a9-112">Exécutez ` Get-Module -ListAvailable AzureRM` version de hello toofind.</span><span class="sxs-lookup"><span data-stu-id="702a9-112">Run ` Get-Module -ListAvailable AzureRM` toofind hello version.</span></span> <span data-ttu-id="702a9-113">Si vous avez besoin de tooupgrade, consultez [installez Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="702a9-113">If you need tooupgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>

## <a name="availability-set-overview"></a><span data-ttu-id="702a9-114">Vue d’ensemble des groupes à haute disponibilité</span><span class="sxs-lookup"><span data-stu-id="702a9-114">Availability set overview</span></span>

<span data-ttu-id="702a9-115">Un ensemble de disponibilité d’est une fonctionnalité de regroupement logique que vous pouvez utiliser dans Azure tooensure que les ressources de machine virtuelle de hello que vous placez qu’il contient sont isolées des autres lorsqu’ils sont déployés dans un centre de données Azure.</span><span class="sxs-lookup"><span data-stu-id="702a9-115">An Availability Set is a logical grouping capability that you can use in Azure tooensure that hello VM resources you place within it are isolated from each other when they are deployed within an Azure datacenter.</span></span> <span data-ttu-id="702a9-116">Azure garantit que machines virtuelles que vous placez dans un ensemble de disponibilité s’exécuter sur plusieurs serveurs physiques hello, le calcul des racks, les unités de stockage et les commutateurs de réseau.</span><span class="sxs-lookup"><span data-stu-id="702a9-116">Azure ensures that hello VMs you place within an Availability Set run across multiple physical servers, compute racks, storage units, and network switches.</span></span> <span data-ttu-id="702a9-117">Cela garantit que dans le cas de hello d’un problème matériel ou logiciel d’Azure, uniquement un sous-ensemble de vos machines virtuelles est affecté, et continuer à et continuer toobe disponible tooyour clients de votre application globale.</span><span class="sxs-lookup"><span data-stu-id="702a9-117">This ensures that in hello event of a hardware or Azure software failure, only a subset of your VMs will be impacted, and your overall application will stay up and continue toobe available tooyour customers.</span></span> <span data-ttu-id="702a9-118">À l’aide de la haute disponibilité est une fonctionnalité essentielle de tooleverage toobuild les solutions de cloud fiable.</span><span class="sxs-lookup"><span data-stu-id="702a9-118">Using Availability Sets is an essential capability tooleverage when you want toobuild reliable cloud solutions.</span></span>

<span data-ttu-id="702a9-119">Prenons l’exemple d’une solution basée sur une machine virtuelle classique dans laquelle vous disposez de 4 serveurs web frontaux et utilisez 2 machines virtuelles principales hébergeant une base de données.</span><span class="sxs-lookup"><span data-stu-id="702a9-119">Let’s consider a typical VM-based solution where you might have 4 front-end web servers and use 2 back-end VMs that host a database.</span></span> <span data-ttu-id="702a9-120">Avec Azure, vous souhaiteriez toodefine deux groupes à haute disponibilité avant de déployer vos machines virtuelles : une disponibilité définie pour le niveau de « web » hello et une haute disponibilité pour le niveau de « base de données » hello.</span><span class="sxs-lookup"><span data-stu-id="702a9-120">With Azure, you’d want toodefine two availability sets before you deploy your VMs: one availability set for hello “web” tier and one availability set for hello “database” tier.</span></span> <span data-ttu-id="702a9-121">Lorsque vous créez une nouvelle machine virtuelle que vous pouvez ensuite spécifier hello groupe à haute disponibilité comme une machine virtuelle de paramètre toohello az Créer commande et Azure automatiquement garantit que machines virtuelles que vous créez au sein de hello disponible hello ensemble sont isolés sur plusieurs ressources de matériel physique.</span><span class="sxs-lookup"><span data-stu-id="702a9-121">When you create a new VM you can then specify hello availability set as a parameter toohello az vm create command, and Azure will automatically ensure that hello VMs you create within hello available set are isolated across multiple physical hardware resources.</span></span> <span data-ttu-id="702a9-122">Cela signifie que si le matériel physique hello que votre serveur Web ou les machines virtuelles de serveur de base de données est en cours d’exécution sur a un problème, vous savez que hello autres instances de votre serveur Web et les machines virtuelles de base de données reste en cours d’exécution correctement, car ils sont sur un matériel différent.</span><span class="sxs-lookup"><span data-stu-id="702a9-122">This means that if hello physical hardware that one of your Web Server or Database Server VMs is running on has a problem, you know that hello other instances of your Web Server and Database VMs will remain running fine because they are on different hardware.</span></span>

<span data-ttu-id="702a9-123">Vous devez toujours utiliser des ensembles de disponibilité lorsque vous souhaitez que des solutions toodeploy fiables en fonction de machine virtuelle dans Azure.</span><span class="sxs-lookup"><span data-stu-id="702a9-123">You should always use Availability Sets when you want toodeploy reliable VM based solutions within Azure.</span></span>

## <a name="create-an-availability-set"></a><span data-ttu-id="702a9-124">Créer un groupe à haute disponibilité</span><span class="sxs-lookup"><span data-stu-id="702a9-124">Create an availability set</span></span>

<span data-ttu-id="702a9-125">Vous pouvez créez un groupe à haute disponibilité avec la commande [New-AzureRmAvailabilitySet](/powershell/module/azurerm.compute/new-azurermavailabilityset).</span><span class="sxs-lookup"><span data-stu-id="702a9-125">You can create an availability set using [New-AzureRmAvailabilitySet](/powershell/module/azurerm.compute/new-azurermavailabilityset).</span></span> <span data-ttu-id="702a9-126">Dans cet exemple, nous avons défini à la fois nombre hello domaines de mise à jour et d’erreur à *2* pour hello groupe à haute disponibilité nommée *myAvailabilitySet* Bonjour *myResourceGroupAvailability*groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="702a9-126">In this example, we set both hello number of update and fault domains at *2* for hello availability set named *myAvailabilitySet* in hello *myResourceGroupAvailability* resource group.</span></span>

<span data-ttu-id="702a9-127">Créez un groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="702a9-127">Create a resource group.</span></span>

```powershell
New-AzureRmResourceGroup -Name myResourceGroupAvailability -Location EastUS
```


```powershell
New-AzureRmAvailabilitySet `
   -Location EastUS `
   -Name myAvailabilitySet `
   -ResourceGroupName myResourceGroupAvailability `
   -Managed `
   -PlatformFaultDomainCount 2 `
   -PlatformUpdateDomainCount 2
```

## <a name="create-vms-inside-an-availability-set"></a><span data-ttu-id="702a9-128">Créer des machines virtuelles dans un groupe à haute disponibilité</span><span class="sxs-lookup"><span data-stu-id="702a9-128">Create VMs inside an availability set</span></span>

<span data-ttu-id="702a9-129">Machines virtuelles doivent toobe créé dans hello disponibilité ensemble toomake qu’ils sont correctement distribués sur les matériels hello.</span><span class="sxs-lookup"><span data-stu-id="702a9-129">VMs need toobe created within hello availability set toomake sure they are correctly distributed across hello hardware.</span></span> <span data-ttu-id="702a9-130">Vous ne pouvez pas ajouter un groupe de machines virtuelles tooan disponibilité définie après sa création.</span><span class="sxs-lookup"><span data-stu-id="702a9-130">You can't add an existing VM tooan availability set after it is created.</span></span> 

<span data-ttu-id="702a9-131">matériel Hello dans un emplacement est divisée dans les domaines de mise à jour toomultiple et les domaines d’erreur.</span><span class="sxs-lookup"><span data-stu-id="702a9-131">hello hardware in a location is divided in toomultiple update domains and fault domains.</span></span> <span data-ttu-id="702a9-132">Un **domaine de mise à jour** est un groupe de machines virtuelles et le matériel physique sous-jacent qui peut être redémarré à hello même temps.</span><span class="sxs-lookup"><span data-stu-id="702a9-132">An **update domain** is a group of VMs and underlying physical hardware that can be rebooted at hello same time.</span></span> <span data-ttu-id="702a9-133">Machines virtuelles dans hello même **domaine d’erreur** partager commun, ainsi qu’un commutateur de réseau et de la source power courantes.</span><span class="sxs-lookup"><span data-stu-id="702a9-133">VMs in hello same **fault domain** share common storage as well as a common power source and network switch.</span></span> 

<span data-ttu-id="702a9-134">Lorsque vous créez une machine virtuelle à l’aide de la configuration à l’aide [New-AzureRMVMConfig](/powershell/module/azurerm.compute/new-azurermvmconfig) vous spécifiez hello haute disponibilité via hello `-AvailabilitySetId` hello toospecify du paramètre d’ID de groupe à haute disponibilité hello.</span><span class="sxs-lookup"><span data-stu-id="702a9-134">When you create a VM using configuration using [New-AzureRMVMConfig](/powershell/module/azurerm.compute/new-azurermvmconfig) you specify hello availability set using hello `-AvailabilitySetId` parameter toospecify hello ID of hello availability set.</span></span>

<span data-ttu-id="702a9-135">Créer 2 machines virtuelles avec [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm) groupe à haute disponibilité hello définie.</span><span class="sxs-lookup"><span data-stu-id="702a9-135">Create 2 VMs with [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm) in hello availability set.</span></span>

```powershell
$availabilitySet = Get-AzureRmAvailabilitySet `
    -ResourceGroupName myResourceGroupAvailability `
    -Name myAvailabilitySet

$cred = Get-Credential -Message "Enter a username and password for hello virtual machine."

$subnetConfig = New-AzureRmVirtualNetworkSubnetConfig `
    -Name mySubnet `
    -AddressPrefix 192.168.1.0/24
$vnet = New-AzureRmVirtualNetwork `
    -ResourceGroupName myResourceGroupAvailability `
    -Location EastUS `
    -Name MYvNET `
    -AddressPrefix 192.168.0.0/16 `
    -Subnet $subnetConfig

for ($i=1; $i -le 2; $i++)
{
   $pip = New-AzureRmPublicIpAddress `
        -ResourceGroupName myResourceGroupAvailability `
        -Location EastUS `
        -Name "mypublicdns$(Get-Random)" `
        -AllocationMethod Static `
        -IdleTimeoutInMinutes 4

   $nsgRuleRDP = New-AzureRmNetworkSecurityRuleConfig `
        -Name myNetworkSecurityGroupRuleRDP$i `
        -Protocol Tcp `
        -Direction Inbound `
        -Priority 1000 `
        -SourceAddressPrefix * `
        -SourcePortRange * `
        -DestinationAddressPrefix * `
        -DestinationPortRange 3389 `
        -Access Allow

   $nsg = New-AzureRmNetworkSecurityGroup `
        -ResourceGroupName myResourceGroupAvailability `
        -Location EastUS `
        -Name myNetworkSecurityGroup$i `
        -SecurityRules $nsgRuleRDP

   $nic = New-AzureRmNetworkInterface `
        -Name myNic$i `
        -ResourceGroupName myResourceGroupAvailability `
        -Location EastUS `
        -SubnetId $vnet.Subnets[0].Id `
        -PublicIpAddressId $pip.Id `
        -NetworkSecurityGroupId $nsg.Id

   # Here is where we specify hello availability set
   $vm = New-AzureRmVMConfig `
        -VMName myVM$i `
        -VMSize Standard_D1 `
        -AvailabilitySetId $availabilitySet.Id

   $vm = Set-AzureRmVMOperatingSystem `
        -VM $vm `
        -Windows -ComputerName myVM$i `   
        -Credential $cred `
        -ProvisionVMAgent `
        -EnableAutoUpdate
   $vm = Set-AzureRmVMSourceImage `
        -VM $vm `
        -PublisherName MicrosoftWindowsServer `
        -Offer WindowsServer `
        -Skus 2016-Datacenter `
        -Version latest
   $vm = Set-AzureRmVMOSDisk `
        -VM $vm `
        -Name myOsDisk$i `
        -DiskSizeInGB 128 `
        -CreateOption FromImage `
        -Caching ReadWrite
   $vm = Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id
   New-AzureRmVM `
        -ResourceGroupName myResourceGroupAvailability `
        -Location EastUS `
        -VM $vm
}

```

<span data-ttu-id="702a9-136">Il prend quelques minutes toocreate et configurer les deux ordinateurs virtuels.</span><span class="sxs-lookup"><span data-stu-id="702a9-136">It takes a few minutes toocreate and configure both VMs.</span></span> <span data-ttu-id="702a9-137">Lorsque vous avez terminé, vous aurez 2 machines virtuelles sont réparties entre hello matériel sous-jacent.</span><span class="sxs-lookup"><span data-stu-id="702a9-137">When finished, you will have 2 virtual machines distributed across hello underlying hardware.</span></span> 

## <a name="check-for-available-vm-sizes"></a><span data-ttu-id="702a9-138">Vérifier les tailles de machines virtuelles disponibles</span><span class="sxs-lookup"><span data-stu-id="702a9-138">Check for available VM sizes</span></span> 

<span data-ttu-id="702a9-139">Vous pouvez ajouter plusieurs machines virtuelles toohello haute disponibilité plus tard, mais vous devez tooknow les tailles de machine virtuelle sont disponibles sur le matériel de hello.</span><span class="sxs-lookup"><span data-stu-id="702a9-139">You can add more VMs toohello availability set later, but you need tooknow what VM sizes are available on hello hardware.</span></span> <span data-ttu-id="702a9-140">Utilisez [Get-AzureRMVMSize](/powershell/module/azurerm.compute/get-azurermvmsize) toolist toutes les tailles disponibles hello sur du matériel de hello du cluster pour hello à haute disponibilité.</span><span class="sxs-lookup"><span data-stu-id="702a9-140">Use [Get-AzureRMVMSize](/powershell/module/azurerm.compute/get-azurermvmsize) toolist all hello available sizes on hello hardware cluster for hello availability set.</span></span>

```powershell
Get-AzureRmVMSize `
   -AvailabilitySetName myAvailabilitySet `
   -ResourceGroupName myResourceGroupAvailability  
```

## <a name="next-steps"></a><span data-ttu-id="702a9-141">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="702a9-141">Next steps</span></span>

<span data-ttu-id="702a9-142">Dans ce didacticiel, vous avez appris à :</span><span class="sxs-lookup"><span data-stu-id="702a9-142">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="702a9-143">Créer un groupe à haute disponibilité</span><span class="sxs-lookup"><span data-stu-id="702a9-143">Create an availability set</span></span>
> * <span data-ttu-id="702a9-144">Créer une machine virtuelle dans un groupe à haute disponibilité</span><span class="sxs-lookup"><span data-stu-id="702a9-144">Create a VM in an availability set</span></span>
> * <span data-ttu-id="702a9-145">Vérifier les tailles de machines virtuelles disponibles</span><span class="sxs-lookup"><span data-stu-id="702a9-145">Check available VM sizes</span></span>

<span data-ttu-id="702a9-146">Avance toohello toolearn de didacticiel suivant sur les machines virtuelles identiques.</span><span class="sxs-lookup"><span data-stu-id="702a9-146">Advance toohello next tutorial toolearn about virtual machine scale sets.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="702a9-147">Créer un groupe de machines virtuelles identiques</span><span class="sxs-lookup"><span data-stu-id="702a9-147">Create a VM scale set</span></span>](tutorial-create-vmss.md)


