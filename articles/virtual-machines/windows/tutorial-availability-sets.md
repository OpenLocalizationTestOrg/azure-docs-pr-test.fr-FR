---
title: "Tutoriel sur les groupes à haute disponibilité pour les machines virtuelles Windows dans Azure | Microsoft Docs"
description: "Découvrez les groupes à haute disponibilité pour les machines virtuelles Windows dans Azure."
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
ms.openlocfilehash: d918362106ef93cf47620e0018d363cd510884b0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-availability-sets"></a><span data-ttu-id="32284-103">Utilisation des groupes à haute disponibilité</span><span class="sxs-lookup"><span data-stu-id="32284-103">How to use availability sets</span></span>

<span data-ttu-id="32284-104">Ce didacticiel explique comment améliorer la disponibilité et la fiabilité de vos solutions de machine virtuelle sur Azure en utilisant une fonctionnalité appelée Groupes à haute disponibilité.</span><span class="sxs-lookup"><span data-stu-id="32284-104">In this tutorial, you will learn how to increase the availability and reliability of your Virtual Machine solutions on Azure using a capability called Availability Sets.</span></span> <span data-ttu-id="32284-105">Les groupes à haute disponibilité veillent à ce que les machines virtuelles que vous déployez sur Azure soient distribuées sur plusieurs clusters matériels isolés.</span><span class="sxs-lookup"><span data-stu-id="32284-105">Availability sets ensure that the VMs you deploy on Azure are distributed across multiple isolated hardware clusters.</span></span> <span data-ttu-id="32284-106">Cela garantit que, si une défaillance matérielle ou logicielle se produit dans Azure, seul un sous-ensemble de vos machines virtuelles soit concerné et que votre solution globale reste disponible et opérationnelle dans la perspective des clients qui l’utilisent.</span><span class="sxs-lookup"><span data-stu-id="32284-106">Doing this ensures that if a hardware or software failure within Azure happens, only a sub-set of your VMs will be impacted and that your overall solution will remain available and operational from the perspective of your customers using it.</span></span> 

<span data-ttu-id="32284-107">Ce tutoriel vous montre comment effectuer les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="32284-107">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="32284-108">Créer un groupe à haute disponibilité</span><span class="sxs-lookup"><span data-stu-id="32284-108">Create an availability set</span></span>
> * <span data-ttu-id="32284-109">Créer une machine virtuelle dans un groupe à haute disponibilité</span><span class="sxs-lookup"><span data-stu-id="32284-109">Create a VM in an availability set</span></span>
> * <span data-ttu-id="32284-110">Vérifier les tailles de machines virtuelles disponibles</span><span class="sxs-lookup"><span data-stu-id="32284-110">Check available VM sizes</span></span>

<span data-ttu-id="32284-111">Ce didacticiel requiert le module Azure PowerShell version 3.6 ou ultérieure.</span><span class="sxs-lookup"><span data-stu-id="32284-111">This tutorial requires the Azure PowerShell module version 3.6 or later.</span></span> <span data-ttu-id="32284-112">Exécutez ` Get-Module -ListAvailable AzureRM` pour trouver la version.</span><span class="sxs-lookup"><span data-stu-id="32284-112">Run ` Get-Module -ListAvailable AzureRM` to find the version.</span></span> <span data-ttu-id="32284-113">Si vous devez effectuer une mise à niveau, consultez [Installer le module Azure PowerShell](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="32284-113">If you need to upgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>

## <a name="availability-set-overview"></a><span data-ttu-id="32284-114">Vue d’ensemble des groupes à haute disponibilité</span><span class="sxs-lookup"><span data-stu-id="32284-114">Availability set overview</span></span>

<span data-ttu-id="32284-115">Un groupe à haute disponibilité est une fonctionnalité de regroupement logique que vous pouvez utiliser dans Azure pour vous assurer que les ressources de machine virtuelle que vous y incluez sont isolées les unes des autres lors de leur déploiement dans un centre de données Azure.</span><span class="sxs-lookup"><span data-stu-id="32284-115">An Availability Set is a logical grouping capability that you can use in Azure to ensure that the VM resources you place within it are isolated from each other when they are deployed within an Azure datacenter.</span></span> <span data-ttu-id="32284-116">Azure veille à ce que les machines virtuelles que vous placez dans un groupe à haute disponibilité s’exécutent sur plusieurs serveurs physiques, racks de calcul, unités de stockage et commutateurs réseau.</span><span class="sxs-lookup"><span data-stu-id="32284-116">Azure ensures that the VMs you place within an Availability Set run across multiple physical servers, compute racks, storage units, and network switches.</span></span> <span data-ttu-id="32284-117">Cela garantit qu’en cas de panne matérielle ou logicielle d’Azure, seul un sous-ensemble de vos machines virtuelles est affecté, et que votre application globale reste opérationnelle et disponible pour vos clients.</span><span class="sxs-lookup"><span data-stu-id="32284-117">This ensures that in the event of a hardware or Azure software failure, only a subset of your VMs will be impacted, and your overall application will stay up and continue to be available to your customers.</span></span> <span data-ttu-id="32284-118">L’utilisation de groupes à haute disponibilité est essentielle pour créer des solutions cloud fiables.</span><span class="sxs-lookup"><span data-stu-id="32284-118">Using Availability Sets is an essential capability to leverage when you want to build reliable cloud solutions.</span></span>

<span data-ttu-id="32284-119">Prenons l’exemple d’une solution basée sur une machine virtuelle classique dans laquelle vous disposez de 4 serveurs web frontaux et utilisez 2 machines virtuelles principales hébergeant une base de données.</span><span class="sxs-lookup"><span data-stu-id="32284-119">Let’s consider a typical VM-based solution where you might have 4 front-end web servers and use 2 back-end VMs that host a database.</span></span> <span data-ttu-id="32284-120">Avec Azure, vous pouvez définir deux groupes à haute disponibilité avant de déployer vos machines virtuelles : l’un pour le niveau « web » et l’autre pour le niveau « base de données ».</span><span class="sxs-lookup"><span data-stu-id="32284-120">With Azure, you’d want to define two availability sets before you deploy your VMs: one availability set for the “web” tier and one availability set for the “database” tier.</span></span> <span data-ttu-id="32284-121">Lorsque vous créez une machine virtuelle, vous pouvez spécifier le groupe à haute disponibilité en tant que paramètre pour la commande az vm create, de sorte qu’Azure veille automatiquement à ce que les machines virtuelles que vous créez dans le groupe disponible soient isolées sur plusieurs ressources matérielles.</span><span class="sxs-lookup"><span data-stu-id="32284-121">When you create a new VM you can then specify the availability set as a parameter to the az vm create command, and Azure will automatically ensure that the VMs you create within the available set are isolated across multiple physical hardware resources.</span></span> <span data-ttu-id="32284-122">Cela signifie que, si le matériel sur lequel s’exécute l’une de vos machines virtuelles serveur web ou serveur de base de données rencontre un problème, vous savez que les autres instances de votre serveur web et de vos machines virtuelles de base de données continueront à s’exécuter correctement parce qu’elles se trouvent sur d’autres éléments matériels.</span><span class="sxs-lookup"><span data-stu-id="32284-122">This means that if the physical hardware that one of your Web Server or Database Server VMs is running on has a problem, you know that the other instances of your Web Server and Database VMs will remain running fine because they are on different hardware.</span></span>

<span data-ttu-id="32284-123">Vous devriez toujours utiliser des groupes à haute disponibilité lorsque vous souhaitez déployer des solutions fiables basées sur des machines virtuelles dans Azure.</span><span class="sxs-lookup"><span data-stu-id="32284-123">You should always use Availability Sets when you want to deploy reliable VM based solutions within Azure.</span></span>

## <a name="create-an-availability-set"></a><span data-ttu-id="32284-124">Créer un groupe à haute disponibilité</span><span class="sxs-lookup"><span data-stu-id="32284-124">Create an availability set</span></span>

<span data-ttu-id="32284-125">Vous pouvez créez un groupe à haute disponibilité avec la commande [New-AzureRmAvailabilitySet](/powershell/module/azurerm.compute/new-azurermavailabilityset).</span><span class="sxs-lookup"><span data-stu-id="32284-125">You can create an availability set using [New-AzureRmAvailabilitySet](/powershell/module/azurerm.compute/new-azurermavailabilityset).</span></span> <span data-ttu-id="32284-126">Dans cet exemple, nous définissons le nombre de domaines de mise à jour et d’erreur sur *2* pour le groupe à haute disponibilité nommé *myAvailabilitySet* dans le groupe de ressources *myResourceGroupAvailability*.</span><span class="sxs-lookup"><span data-stu-id="32284-126">In this example, we set both the number of update and fault domains at *2* for the availability set named *myAvailabilitySet* in the *myResourceGroupAvailability* resource group.</span></span>

<span data-ttu-id="32284-127">Créez un groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="32284-127">Create a resource group.</span></span>

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

## <a name="create-vms-inside-an-availability-set"></a><span data-ttu-id="32284-128">Créer des machines virtuelles dans un groupe à haute disponibilité</span><span class="sxs-lookup"><span data-stu-id="32284-128">Create VMs inside an availability set</span></span>

<span data-ttu-id="32284-129">Vous devez créer des machines virtuelles au sein du groupe à haute disponibilité pour vous assurer qu’elles sont correctement réparties dans le matériel.</span><span class="sxs-lookup"><span data-stu-id="32284-129">VMs need to be created within the availability set to make sure they are correctly distributed across the hardware.</span></span> <span data-ttu-id="32284-130">Vous ne pouvez pas ajouter une machine virtuelle existante à un groupe à haute disponibilité après sa création.</span><span class="sxs-lookup"><span data-stu-id="32284-130">You can't add an existing VM to an availability set after it is created.</span></span> 

<span data-ttu-id="32284-131">Le matériel situé à un emplacement est divisé en plusieurs domaines de mise à jour et d’erreur.</span><span class="sxs-lookup"><span data-stu-id="32284-131">The hardware in a location is divided in to multiple update domains and fault domains.</span></span> <span data-ttu-id="32284-132">Un **domaine de mise à jour** est un groupe de machines virtuelles et d’équipements physiques sous-jacents pouvant être redémarrés en même temps.</span><span class="sxs-lookup"><span data-stu-id="32284-132">An **update domain** is a group of VMs and underlying physical hardware that can be rebooted at the same time.</span></span> <span data-ttu-id="32284-133">Les machines virtuelles d’un même **domaine d’erreur** partagent un espace de stockage commun ainsi qu’une source d’alimentation et un commutateur réseau.</span><span class="sxs-lookup"><span data-stu-id="32284-133">VMs in the same **fault domain** share common storage as well as a common power source and network switch.</span></span> 

<span data-ttu-id="32284-134">Lorsque vous créez une machine virtuelle à l’aide de la configuration utilisant [New-AzureRMVMConfig](/powershell/module/azurerm.compute/new-azurermvmconfig), vous spécifiez le groupe à haute disponibilité à l’aide du paramètre `-AvailabilitySetId` pour en spécifier l’ID.</span><span class="sxs-lookup"><span data-stu-id="32284-134">When you create a VM using configuration using [New-AzureRMVMConfig](/powershell/module/azurerm.compute/new-azurermvmconfig) you specify the availability set using the `-AvailabilitySetId` parameter to specify the ID of the availability set.</span></span>

<span data-ttu-id="32284-135">Créez 2 machines virtuelles avec [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm) dans le groupe à haute disponibilité.</span><span class="sxs-lookup"><span data-stu-id="32284-135">Create 2 VMs with [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm) in the availability set.</span></span>

```powershell
$availabilitySet = Get-AzureRmAvailabilitySet `
    -ResourceGroupName myResourceGroupAvailability `
    -Name myAvailabilitySet

$cred = Get-Credential -Message "Enter a username and password for the virtual machine."

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

   # Here is where we specify the availability set
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

<span data-ttu-id="32284-136">La création et la configuration des deux machines virtuelles prennent quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="32284-136">It takes a few minutes to create and configure both VMs.</span></span> <span data-ttu-id="32284-137">Vous disposez ensuite de 2 machines virtuelles réparties sur le matériel sous-jacent.</span><span class="sxs-lookup"><span data-stu-id="32284-137">When finished, you will have 2 virtual machines distributed across the underlying hardware.</span></span> 

## <a name="check-for-available-vm-sizes"></a><span data-ttu-id="32284-138">Vérifier les tailles de machines virtuelles disponibles</span><span class="sxs-lookup"><span data-stu-id="32284-138">Check for available VM sizes</span></span> 

<span data-ttu-id="32284-139">Vous pouvez ajouter ultérieurement d’autres machines virtuelles au groupe à haute disponibilité, mais vous devez connaître les tailles des machines virtuelles qui sont disponibles sur le matériel.</span><span class="sxs-lookup"><span data-stu-id="32284-139">You can add more VMs to the availability set later, but you need to know what VM sizes are available on the hardware.</span></span> <span data-ttu-id="32284-140">Utilisez [Get-AzureRMVMSize](/powershell/module/azurerm.compute/get-azurermvmsize) pour répertorier toutes les tailles disponibles sur le cluster matériel pour le groupe à haute disponibilité.</span><span class="sxs-lookup"><span data-stu-id="32284-140">Use [Get-AzureRMVMSize](/powershell/module/azurerm.compute/get-azurermvmsize) to list all the available sizes on the hardware cluster for the availability set.</span></span>

```powershell
Get-AzureRmVMSize `
   -AvailabilitySetName myAvailabilitySet `
   -ResourceGroupName myResourceGroupAvailability  
```

## <a name="next-steps"></a><span data-ttu-id="32284-141">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="32284-141">Next steps</span></span>

<span data-ttu-id="32284-142">Dans ce didacticiel, vous avez appris à :</span><span class="sxs-lookup"><span data-stu-id="32284-142">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="32284-143">Créer un groupe à haute disponibilité</span><span class="sxs-lookup"><span data-stu-id="32284-143">Create an availability set</span></span>
> * <span data-ttu-id="32284-144">Créer une machine virtuelle dans un groupe à haute disponibilité</span><span class="sxs-lookup"><span data-stu-id="32284-144">Create a VM in an availability set</span></span>
> * <span data-ttu-id="32284-145">Vérifier les tailles de machines virtuelles disponibles</span><span class="sxs-lookup"><span data-stu-id="32284-145">Check available VM sizes</span></span>

<span data-ttu-id="32284-146">Passez au didacticiel suivant pour en savoir plus sur les groupes de machines virtuelles identiques.</span><span class="sxs-lookup"><span data-stu-id="32284-146">Advance to the next tutorial to learn about virtual machine scale sets.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="32284-147">Créer un groupe de machines virtuelles identiques</span><span class="sxs-lookup"><span data-stu-id="32284-147">Create a VM scale set</span></span>](tutorial-create-vmss.md)


