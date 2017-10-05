---
title: "Créer un groupe de machines virtuelles identiques pour Windows dans Azure | Microsoft Docs"
description: "Créez et déployez une application hautement disponible sur des machines virtuelles Windows en utilisant un groupe de machines virtuelles identiques"
services: virtual-machine-scale-sets
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: 
ms.assetid: 
ms.service: virtual-machine-scale-sets
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: 
ms.topic: article
ms.date: 08/11/2017
ms.author: iainfou
ms.custom: mvc
ms.openlocfilehash: 6600d3b401495f6c291249935b16bcc36c9b8f4b
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-virtual-machine-scale-set-and-deploy-a-highly-available-app-on-windows"></a><span data-ttu-id="56a4f-103">Créer un groupe de machines virtuelles identiques et déployer une application hautement disponible sur Windows</span><span class="sxs-lookup"><span data-stu-id="56a4f-103">Create a Virtual Machine Scale Set and deploy a highly available app on Windows</span></span>
<span data-ttu-id="56a4f-104">Un groupe de machines virtuelles identiques vous permet de déployer et de gérer un ensemble de machines virtuelles identiques prenant en charge la mise à l’échelle automatique.</span><span class="sxs-lookup"><span data-stu-id="56a4f-104">A virtual machine scale set allows you to deploy and manage a set of identical, auto-scaling virtual machines.</span></span> <span data-ttu-id="56a4f-105">Vous pouvez mettre à l’échelle manuellement le nombre de machines virtuelles du groupe identique ou définir des règles pour mettre à l’échelle automatiquement en fonction de l’utilisation du processeur, de la demande de mémoire ou du trafic réseau.</span><span class="sxs-lookup"><span data-stu-id="56a4f-105">You can scale the number of VMs in the scale set manually, or define rules to autoscale based on CPU usage, memory demand, or network traffic.</span></span> <span data-ttu-id="56a4f-106">Ce didacticiel explique comment déployer un groupe de machines virtuelles identiques dans Azure.</span><span class="sxs-lookup"><span data-stu-id="56a4f-106">In this tutorial, you deploy a virtual machine scale set in Azure.</span></span> <span data-ttu-id="56a4f-107">Vous allez apprendre à effectuer les actions suivantes :</span><span class="sxs-lookup"><span data-stu-id="56a4f-107">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="56a4f-108">Utiliser l’extension de script personnalisé pour définir un site IIS à mettre à l’échelle</span><span class="sxs-lookup"><span data-stu-id="56a4f-108">Use the Custom Script Extension to define an IIS site to scale</span></span>
> * <span data-ttu-id="56a4f-109">Créer un équilibrage de charge pour votre groupe identique</span><span class="sxs-lookup"><span data-stu-id="56a4f-109">Create a load balancer for your scale set</span></span>
> * <span data-ttu-id="56a4f-110">Créer un groupe de machines virtuelles identiques</span><span class="sxs-lookup"><span data-stu-id="56a4f-110">Create a virtual machine scale set</span></span>
> * <span data-ttu-id="56a4f-111">Augmenter ou réduire le nombre d’instances dans un groupe identique</span><span class="sxs-lookup"><span data-stu-id="56a4f-111">Increase or decrease the number of instances in a scale set</span></span>
> * <span data-ttu-id="56a4f-112">Créer des règles de mise à l’échelle automatique</span><span class="sxs-lookup"><span data-stu-id="56a4f-112">Create autoscale rules</span></span>

<span data-ttu-id="56a4f-113">Ce didacticiel requiert le module Azure PowerShell version 3.6 ou ultérieure.</span><span class="sxs-lookup"><span data-stu-id="56a4f-113">This tutorial requires the Azure PowerShell module version 3.6 or later.</span></span> <span data-ttu-id="56a4f-114">Exécutez ` Get-Module -ListAvailable AzureRM` pour trouver la version.</span><span class="sxs-lookup"><span data-stu-id="56a4f-114">Run ` Get-Module -ListAvailable AzureRM` to find the version.</span></span> <span data-ttu-id="56a4f-115">Si vous devez effectuer une mise à niveau, consultez [Installer le module Azure PowerShell](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="56a4f-115">If you need to upgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>


## <a name="scale-set-overview"></a><span data-ttu-id="56a4f-116">Vue d’ensemble des groupes identiques</span><span class="sxs-lookup"><span data-stu-id="56a4f-116">Scale Set overview</span></span>
<span data-ttu-id="56a4f-117">Les groupes identiques reposent sur les mêmes concepts que ceux que vous avez découverts dans le tutoriel précédent, qui traitait de la [création de machines virtuelles hautement disponibles](tutorial-availability-sets.md).</span><span class="sxs-lookup"><span data-stu-id="56a4f-117">Scale sets use similar concepts as you learned about in the previous tutorial to [Create highly available VMs](tutorial-availability-sets.md).</span></span> <span data-ttu-id="56a4f-118">Les machines virtuelles d’un groupe identique sont réparties entre les domaines d’erreur et de mise à jour, tout comme les machines virtuelles d’un groupe à haute disponibilité.</span><span class="sxs-lookup"><span data-stu-id="56a4f-118">VMs in a scale set are distributed across fault and update domains just like VMs in an availability set.</span></span>

<span data-ttu-id="56a4f-119">Les machines virtuelles sont créées en fonction des besoins dans un groupe identique.</span><span class="sxs-lookup"><span data-stu-id="56a4f-119">VMs are created as needed in a scale set.</span></span> <span data-ttu-id="56a4f-120">En définissant des règles de mise à l’échelle automatique, vous pouvez contrôler quand et comment les machines virtuelles sont ajoutées ou supprimées au niveau du groupe identique.</span><span class="sxs-lookup"><span data-stu-id="56a4f-120">You define autoscale rules to control how and when VMs are added or removed from the scale set.</span></span> <span data-ttu-id="56a4f-121">Ces règles peuvent se déclencher en fonction de mesures telles que la charge du processeur, l’utilisation de la mémoire ou le trafic réseau.</span><span class="sxs-lookup"><span data-stu-id="56a4f-121">These rules can trigger based on metrics such as CPU load, memory usage, or network traffic.</span></span>

<span data-ttu-id="56a4f-122">Les groupes identiques peuvent prendre en charge jusqu’à 1 000 machines virtuelles quand vous utilisez une image de plateforme Azure.</span><span class="sxs-lookup"><span data-stu-id="56a4f-122">Scale sets support up to 1,000 VMs when you use an Azure platform image.</span></span> <span data-ttu-id="56a4f-123">Pour les charges de travail qui s’accompagnent de contraintes importantes en matière d’installation ou de personnalisation de machines virtuelles, vous pouvez [créer une image de machine virtuelle personnalisée](tutorial-custom-images.md).</span><span class="sxs-lookup"><span data-stu-id="56a4f-123">For workloads with significant installation or VM customization requirements, you may wish to [Create a custom VM image](tutorial-custom-images.md).</span></span> <span data-ttu-id="56a4f-124">Vous pouvez créer jusqu’à 100 machines virtuelles dans un groupe identique quand vous utilisez une image personnalisée.</span><span class="sxs-lookup"><span data-stu-id="56a4f-124">You can create up to 100 VMs in a scale set when using a custom image.</span></span>


## <a name="create-an-app-to-scale"></a><span data-ttu-id="56a4f-125">Créer une application à mettre à l’échelle</span><span class="sxs-lookup"><span data-stu-id="56a4f-125">Create an app to scale</span></span>
<span data-ttu-id="56a4f-126">Avant de créer un groupe identique, créez un groupe de ressources avec [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span><span class="sxs-lookup"><span data-stu-id="56a4f-126">Before you can create a scale set, create a resource group with [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span></span> <span data-ttu-id="56a4f-127">L’exemple suivant crée un groupe de ressources nommé *myResourceGroupAutomate* dans l’emplacement *EastUS* :</span><span class="sxs-lookup"><span data-stu-id="56a4f-127">The following example creates a resource group named *myResourceGroupAutomate* in the *EastUS* location:</span></span>

```powershell
New-AzureRmResourceGroup -ResourceGroupName myResourceGroupScaleSet -Location EastUS
```

<span data-ttu-id="56a4f-128">Dans un tutoriel précédent, vous avez appris à [automatiser la configuration des machines virtuelles](tutorial-automate-vm-deployment.md) à l’aide de l’extension de script personnalisé.</span><span class="sxs-lookup"><span data-stu-id="56a4f-128">In an earlier tutorial, you learned how to [Automate VM configuration](tutorial-automate-vm-deployment.md) using the Custom Script Extension.</span></span> <span data-ttu-id="56a4f-129">Créez une configuration de groupe identique, puis appliquez une extension de script personnalisé pour installer et configurer IIS :</span><span class="sxs-lookup"><span data-stu-id="56a4f-129">Create a scale set configuration then apply a Custom Script Extension to install and configure IIS:</span></span>

```powershell
# Create a config object
$vmssConfig = New-AzureRmVmssConfig `
    -Location EastUS `
    -SkuCapacity 2 `
    -SkuName Standard_DS2 `
    -UpgradePolicyMode Automatic

# Define the script for your Custom Script Extension to run
$publicSettings = @{
    "fileUris" = (,"https://raw.githubusercontent.com/iainfoulds/azure-samples/master/automate-iis.ps1");
    "commandToExecute" = "powershell -ExecutionPolicy Unrestricted -File automate-iis.ps1"
}

# Use Custom Script Extension to install IIS and configure basic website
Add-AzureRmVmssExtension -VirtualMachineScaleSet $vmssConfig `
    -Name "customScript" `
    -Publisher "Microsoft.Compute" `
    -Type "CustomScriptExtension" `
    -TypeHandlerVersion 1.8 `
    -Setting $publicSettings
```

## <a name="create-scale-load-balancer"></a><span data-ttu-id="56a4f-130">Créer un équilibreur de charge d’échelle</span><span class="sxs-lookup"><span data-stu-id="56a4f-130">Create scale load balancer</span></span>
<span data-ttu-id="56a4f-131">Un équilibreur de charge Azure est un équilibreur de charge de type Couche 4 (TCP, UDP) qui offre une haute disponibilité en répartissant le trafic entrant entre les machines virtuelles saines.</span><span class="sxs-lookup"><span data-stu-id="56a4f-131">An Azure load balancer is a Layer-4 (TCP, UDP) load balancer that provides high availability by distributing incoming traffic among healthy VMs.</span></span> <span data-ttu-id="56a4f-132">Une sonde d’intégrité d’équilibreur de charge surveille un port donné sur chaque machine virtuelle et ne distribue le trafic qu’à une machine virtuelle opérationnelle.</span><span class="sxs-lookup"><span data-stu-id="56a4f-132">A load balancer health probe monitors a given port on each VM and only distributes traffic to an operational VM.</span></span> <span data-ttu-id="56a4f-133">Pour plus d’informations, consultez le prochain tutoriel qui traite de [l’équilibrage de la charge des machines virtuelles Windows](tutorial-load-balancer.md).</span><span class="sxs-lookup"><span data-stu-id="56a4f-133">For more information, see the next tutorial on [How to load balance Windows virtual machines](tutorial-load-balancer.md).</span></span>

<span data-ttu-id="56a4f-134">Créez un équilibreur de charge doté d’une adresse IP publique qui distribue le trafic web sur le port 80 :</span><span class="sxs-lookup"><span data-stu-id="56a4f-134">Create a load balancer that has a public IP address and distributes web traffic on port 80:</span></span>

```powershell
# Create a public IP address
$publicIP = New-AzureRmPublicIpAddress `
  -ResourceGroupName myResourceGroupScaleSet `
  -Location EastUS `
  -AllocationMethod Static `
  -Name myPublicIP

# Create a frontend and backend IP pool
$frontendIP = New-AzureRmLoadBalancerFrontendIpConfig `
  -Name myFrontEndPool `
  -PublicIpAddress $publicIP
$backendPool = New-AzureRmLoadBalancerBackendAddressPoolConfig -Name myBackEndPool

# Create the load balancer
$lb = New-AzureRmLoadBalancer `
  -ResourceGroupName myResourceGroupScaleSet `
  -Name myLoadBalancer `
  -Location EastUS `
  -FrontendIpConfiguration $frontendIP `
  -BackendAddressPool $backendPool

# Create a load balancer health probe on port 80
Add-AzureRmLoadBalancerProbeConfig -Name myHealthProbe `
  -LoadBalancer $lb `
  -Protocol tcp `
  -Port 80 `
  -IntervalInSeconds 15 `
  -ProbeCount 2

# Create a load balancer rule to distribute traffic on port 80
Add-AzureRmLoadBalancerRuleConfig `
  -Name myLoadBalancerRule `
  -LoadBalancer $lb `
  -FrontendIpConfiguration $lb.FrontendIpConfigurations[0] `
  -BackendAddressPool $lb.BackendAddressPools[0] `
  -Protocol Tcp `
  -FrontendPort 80 `
  -BackendPort 80

# Update the load balancer configuration
Set-AzureRmLoadBalancer -LoadBalancer $lb
```

## <a name="create-a-scale-set"></a><span data-ttu-id="56a4f-135">Créer un groupe identique</span><span class="sxs-lookup"><span data-stu-id="56a4f-135">Create a scale set</span></span>
<span data-ttu-id="56a4f-136">À présent, créez un groupe de machines virtuelles identiques avec [New-AzureRmVmss](/powershell/module/azurerm.compute/new-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="56a4f-136">Now create a virtual machine scale set with [New-AzureRmVmss](/powershell/module/azurerm.compute/new-azurermvm).</span></span> <span data-ttu-id="56a4f-137">L’exemple suivant crée un groupe identique nommé *myScaleSet* :</span><span class="sxs-lookup"><span data-stu-id="56a4f-137">The following example creates a scale set named *myScaleSet*:</span></span>

```powershell
# Reference a virtual machine image from the gallery
Set-AzureRmVmssStorageProfile $vmssConfig `
  -ImageReferencePublisher MicrosoftWindowsServer `
  -ImageReferenceOffer WindowsServer `
  -ImageReferenceSku 2016-Datacenter `
  -ImageReferenceVersion latest

# Set up information for authenticating with the virtual machine
Set-AzureRmVmssOsProfile $vmssConfig `
  -AdminUsername azureuser `
  -AdminPassword P@ssword! `
  -ComputerNamePrefix myVM

# Create the virtual network resources
$subnet = New-AzureRmVirtualNetworkSubnetConfig `
  -Name "mySubnet" `
  -AddressPrefix 10.0.0.0/24
$vnet = New-AzureRmVirtualNetwork `
  -ResourceGroupName "myResourceGroupScaleSet" `
  -Name "myVnet" `
  -Location "EastUS" `
  -AddressPrefix 10.0.0.0/16 `
  -Subnet $subnet
$ipConfig = New-AzureRmVmssIpConfig `
  -Name "myIPConfig" `
  -LoadBalancerBackendAddressPoolsId $lb.BackendAddressPools[0].Id `
  -SubnetId $vnet.Subnets[0].Id

# Attach the virtual network to the config object
Add-AzureRmVmssNetworkInterfaceConfiguration `
  -VirtualMachineScaleSet $vmssConfig `
  -Name "network-config" `
  -Primary $true `
  -IPConfiguration $ipConfig

# Create the scale set with the config object (this step might take a few minutes)
New-AzureRmVmss `
  -ResourceGroupName myResourceGroupScaleSet `
  -Name myScaleSet `
  -VirtualMachineScaleSet $vmssConfig
```

<span data-ttu-id="56a4f-138">La création et la configuration des l’ensemble des ressources et des machines virtuelles du groupe identique prennent quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="56a4f-138">It takes a few minutes to create and configure all the scale set resources and VMs.</span></span>


## <a name="test-your-app"></a><span data-ttu-id="56a4f-139">Test de l'application</span><span class="sxs-lookup"><span data-stu-id="56a4f-139">Test your app</span></span>
<span data-ttu-id="56a4f-140">Pour voir fonctionner votre site web IIS, obtenez l’adresse IP publique de votre équilibreur de charge avec [Get-AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress).</span><span class="sxs-lookup"><span data-stu-id="56a4f-140">To see your IIS website in action, obtain the public IP address of your load balancer with [Get-AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress).</span></span> <span data-ttu-id="56a4f-141">L’exemple suivant obtient l’adresse IP pour *myPublicIP* qui a été créée pour le groupe identique :</span><span class="sxs-lookup"><span data-stu-id="56a4f-141">The following example obtains the IP address for *myPublicIP* created as part of the scale set:</span></span>

```powershell
Get-AzureRmPublicIPAddress -ResourceGroupName myResourceGroupScaleSet -Name myPublicIP | select IpAddress
```

<span data-ttu-id="56a4f-142">Entrez l’adresse IP publique dans un navigateur web.</span><span class="sxs-lookup"><span data-stu-id="56a4f-142">Enter the public IP address in to a web browser.</span></span> <span data-ttu-id="56a4f-143">L’application s’affiche, avec notamment le nom d’hôte de la machine virtuelle sur laquelle l’équilibrage de charge a distribué le trafic :</span><span class="sxs-lookup"><span data-stu-id="56a4f-143">The app is displayed, including the hostname of the VM that the load balancer distributed traffic to:</span></span>

![Site IIS en cours d’exécution](./media/tutorial-create-vmss/running-iis-site.png)

<span data-ttu-id="56a4f-145">Pour voir fonctionner le groupe identique, vous pouvez forcer l’actualisation de votre navigateur web. L’équilibreur de charge répartit alors le trafic entre toutes les machines virtuelles exécutant votre application.</span><span class="sxs-lookup"><span data-stu-id="56a4f-145">To see the scale set in action, you can force-refresh your web browser to see the load balancer distribute traffic across all the VMs running your app.</span></span>


## <a name="management-tasks"></a><span data-ttu-id="56a4f-146">Tâches de gestion</span><span class="sxs-lookup"><span data-stu-id="56a4f-146">Management tasks</span></span>
<span data-ttu-id="56a4f-147">Tout au long du cycle de vie du groupe identique, vous devrez peut-être exécuter une ou plusieurs tâches de gestion.</span><span class="sxs-lookup"><span data-stu-id="56a4f-147">Throughout the lifecycle of the scale set, you may need to run one or more management tasks.</span></span> <span data-ttu-id="56a4f-148">En outre, vous souhaiterez peut-être créer des scripts pour automatiser les diverses tâches liées au cycle de vie.</span><span class="sxs-lookup"><span data-stu-id="56a4f-148">Additionally, you may want to create scripts that automate various lifecycle-tasks.</span></span> <span data-ttu-id="56a4f-149">Azure PowerShell offre un moyen rapide d’effectuer ces tâches.</span><span class="sxs-lookup"><span data-stu-id="56a4f-149">Azure PowerShell provides a quick way to do those tasks.</span></span> <span data-ttu-id="56a4f-150">Voici quelques tâches courantes.</span><span class="sxs-lookup"><span data-stu-id="56a4f-150">Here are a few common tasks.</span></span>

### <a name="view-vms-in-a-scale-set"></a><span data-ttu-id="56a4f-151">Voir les machines virtuelles d’un groupe identique</span><span class="sxs-lookup"><span data-stu-id="56a4f-151">View VMs in a scale set</span></span>
<span data-ttu-id="56a4f-152">Pour afficher la liste des machines virtuelles s’exécutant dans votre groupe identique, utilisez [Get-AzureRmVmssVM](/powershell/module/azurerm.compute/get-azurermvmssvm) comme suit :</span><span class="sxs-lookup"><span data-stu-id="56a4f-152">To view a list of VMs running in your scale set, use [Get-AzureRmVmssVM](/powershell/module/azurerm.compute/get-azurermvmssvm) as follows:</span></span>

```powershell
# Get current scale set
$scaleset = Get-AzureRmVmss `
  -ResourceGroupName myResourceGroupScaleSet `
  -VMScaleSetName myScaleSet

# Loop through the instanaces in your scale set
for ($i=1; $i -le ($scaleset.Sku.Capacity - 1); $i++) {
    Get-AzureRmVmssVM -ResourceGroupName myResourceGroupScaleSet `
      -VMScaleSetName myScaleSet `
      -InstanceId $i
}
```


### <a name="increase-or-decrease-vm-instances"></a><span data-ttu-id="56a4f-153">Augmenter ou diminuer les instances de machines virtuelles</span><span class="sxs-lookup"><span data-stu-id="56a4f-153">Increase or decrease VM instances</span></span>
<span data-ttu-id="56a4f-154">Pour afficher le nombre d’instances actuellement présentes dans un groupe identique, utilisez [Get-AzureRmVmss](/powershell/module/azurerm.compute/get-azurermvmss) et formulez une requête *sku.capacity* :</span><span class="sxs-lookup"><span data-stu-id="56a4f-154">To see the number of instances you currently have in a scale set, use [Get-AzureRmVmss](/powershell/module/azurerm.compute/get-azurermvmss) and query on *sku.capacity*:</span></span>

```powershell
Get-AzureRmVmss -ResourceGroupName myResourceGroupScaleSet `
    -VMScaleSetName myScaleSet | `
    Select -ExpandProperty Sku
```

<span data-ttu-id="56a4f-155">Vous pouvez ensuite augmenter ou diminuer manuellement le nombre de machines virtuelles présentes dans le groupe identique avec [Update-AzureRmVmss](/powershell/module/azurerm.compute/update-azurermvmss).</span><span class="sxs-lookup"><span data-stu-id="56a4f-155">You can then manually increase or decrease the number of virtual machines in the scale set with [Update-AzureRmVmss](/powershell/module/azurerm.compute/update-azurermvmss).</span></span> <span data-ttu-id="56a4f-156">L’exemple suivant fixe le nombre de machines virtuelles présentes dans votre groupe identique à *5* :</span><span class="sxs-lookup"><span data-stu-id="56a4f-156">The following example sets the number of VMs in your scale set to *5*:</span></span>

```powershell
# Get current scale set
$scaleset = Get-AzureRmVmss `
  -ResourceGroupName myResourceGroupScaleSet `
  -VMScaleSetName myScaleSet

# Set and update the capacity of your scale set
$scaleset.sku.capacity = 5
Update-AzureRmVmss -ResourceGroupName myResourceGroupScaleSet `
    -Name myScaleSet `
    -VirtualMachineScaleSet $scaleset
```

<span data-ttu-id="56a4f-157">Plusieurs minutes sont nécessaires avant que le nombre d’instances spécifié soit mis à jour pour votre groupe identique.</span><span class="sxs-lookup"><span data-stu-id="56a4f-157">If takes a few minutes to update the specified number of instances in your scale set.</span></span>


### <a name="configure-autoscale-rules"></a><span data-ttu-id="56a4f-158">Configurer des règles de mise à l’échelle automatique</span><span class="sxs-lookup"><span data-stu-id="56a4f-158">Configure autoscale rules</span></span>
<span data-ttu-id="56a4f-159">Au lieu d’adapter manuellement le nombre d’instances présentes dans votre groupe identique, vous pouvez définir des règles de mise à l’échelle automatique.</span><span class="sxs-lookup"><span data-stu-id="56a4f-159">Rather than manually scaling the number of instances in your scale set, you define autoscale rules.</span></span> <span data-ttu-id="56a4f-160">Ces règles surveillent les instances présentes dans votre groupe identique et répondent en conséquence en fonction des métriques et des seuils que vous définissez.</span><span class="sxs-lookup"><span data-stu-id="56a4f-160">These rules monitor the instances in your scale set and respond accordingly based on metrics and thresholds you define.</span></span> <span data-ttu-id="56a4f-161">L’exemple suivant augmente le nombre d’instances d’une unité dès que la charge moyenne du processeur dépasse 60 % sur une période de 5 minutes.</span><span class="sxs-lookup"><span data-stu-id="56a4f-161">The following example scales out the number of instances by one when the average CPU load is greater than 60% over a 5 minute period.</span></span> <span data-ttu-id="56a4f-162">Si la charge moyenne du processeur descend ensuite en dessous de 30 % sur une période de 5 minutes, le nombre d’instances diminue d’une unité :</span><span class="sxs-lookup"><span data-stu-id="56a4f-162">If the average CPU load then drops below 30% over a 5 minute period, the instances are scaled in by one instance:</span></span>

```powershell
# Define your scale set information
$mySubscriptionId = (Get-AzureRmSubscription).Id
$myResourceGroup = "myResourceGroupScaleSet"
$myScaleSet = "myScaleSet"
$myLocation = "East US"

# Create a scale up rule to increase the number instances after 60% average CPU usage exceeded for a 5 minute period
$myRuleScaleUp = New-AzureRmAutoscaleRule `
  -MetricName "Percentage CPU" `
  -MetricResourceId /subscriptions/$mySubscriptionId/resourceGroups/$myResourceGroup/providers/Microsoft.Compute/virtualMachineScaleSets/$myScaleSet `
  -Operator GreaterThan `
  -MetricStatistic Average `
  -Threshold 60 `
  -TimeGrain 00:01:00 `
  -TimeWindow 00:05:00 `
  -ScaleActionCooldown 00:05:00 `
  -ScaleActionDirection Increase `
  -ScaleActionValue 1

# Create a scale down rule to decrease the number of instances after 30% average CPU usage over a 5 minute period
$myRuleScaleDown = New-AzureRmAutoscaleRule `
  -MetricName "Percentage CPU" `
  -MetricResourceId /subscriptions/$mySubscriptionId/resourceGroups/$myResourceGroup/providers/Microsoft.Compute/virtualMachineScaleSets/$myScaleSet `
  -Operator LessThan `
  -MetricStatistic Average `
  -Threshold 30 `
  -TimeGrain 00:01:00 `
  -TimeWindow 00:05:00 `
  -ScaleActionCooldown 00:05:00 `
  -ScaleActionDirection Decrease `
  -ScaleActionValue 1

# Create a scale profile with your scale up and scale down rules
$myScaleProfile = New-AzureRmAutoscaleProfile `
  -DefaultCapacity 2  `
  -MaximumCapacity 10 `
  -MinimumCapacity 2 `
  -Rules $myRuleScaleUp,$myRuleScaleDown `
  -Name "autoprofile"

# Apply the autoscale rules
Add-AzureRmAutoscaleSetting `
  -Location $myLocation `
  -Name "autosetting" `
  -ResourceGroup $myResourceGroup `
  -TargetResourceId /subscriptions/$mySubscriptionId/resourceGroups/$myResourceGroup/providers/Microsoft.Compute/virtualMachineScaleSets/$myScaleSet `
  -AutoscaleProfiles $myScaleProfile
```


## <a name="next-steps"></a><span data-ttu-id="56a4f-163">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="56a4f-163">Next steps</span></span>
<span data-ttu-id="56a4f-164">Ce didacticiel vous a montré comment créer un groupe de machines virtuelles identiques.</span><span class="sxs-lookup"><span data-stu-id="56a4f-164">In this tutorial, you created a virtual machine scale set.</span></span> <span data-ttu-id="56a4f-165">Vous avez appris à effectuer les actions suivantes :</span><span class="sxs-lookup"><span data-stu-id="56a4f-165">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="56a4f-166">Utiliser l’extension de script personnalisé pour définir un site IIS à mettre à l’échelle</span><span class="sxs-lookup"><span data-stu-id="56a4f-166">Use the Custom Script Extension to define an IIS site to scale</span></span>
> * <span data-ttu-id="56a4f-167">Créer un équilibrage de charge pour votre groupe identique</span><span class="sxs-lookup"><span data-stu-id="56a4f-167">Create a load balancer for your scale set</span></span>
> * <span data-ttu-id="56a4f-168">Créer un groupe de machines virtuelles identiques</span><span class="sxs-lookup"><span data-stu-id="56a4f-168">Create a virtual machine scale set</span></span>
> * <span data-ttu-id="56a4f-169">Augmenter ou réduire le nombre d’instances dans un groupe identique</span><span class="sxs-lookup"><span data-stu-id="56a4f-169">Increase or decrease the number of instances in a scale set</span></span>
> * <span data-ttu-id="56a4f-170">Créer des règles de mise à l’échelle automatique</span><span class="sxs-lookup"><span data-stu-id="56a4f-170">Create autoscale rules</span></span>

<span data-ttu-id="56a4f-171">Passez au didacticiel suivant pour en savoir plus sur les concepts de l’équilibrage de charge des machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="56a4f-171">Advance to the next tutorial to learn more about load balancing concepts for virtual machines.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="56a4f-172">Équilibrage de charge des machines virtuelles</span><span class="sxs-lookup"><span data-stu-id="56a4f-172">Load balance virtual machines</span></span>](tutorial-load-balancer.md)
