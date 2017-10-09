---
title: "aaaCreate une Machine virtuelle échelle jeux pour Windows dans Azure | Documents Microsoft"
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
ms.openlocfilehash: a3914571005c28a492c069d880992630851afae7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-machine-scale-set-and-deploy-a-highly-available-app-on-windows"></a><span data-ttu-id="91da6-103">Créer un groupe de machines virtuelles identiques et déployer une application hautement disponible sur Windows</span><span class="sxs-lookup"><span data-stu-id="91da6-103">Create a Virtual Machine Scale Set and deploy a highly available app on Windows</span></span>
<span data-ttu-id="91da6-104">Un ensemble d’échelle de machine virtuelle vous permet de toodeploy et gérer un ensemble de machines virtuelles identiques et la mise à l’échelle automatique.</span><span class="sxs-lookup"><span data-stu-id="91da6-104">A virtual machine scale set allows you toodeploy and manage a set of identical, auto-scaling virtual machines.</span></span> <span data-ttu-id="91da6-105">Vous pouvez mettre à l’échelle nombre hello d’ordinateurs virtuels dans un ensemble d’échelle hello manuellement ou définir tooautoscale règles en fonction de l’utilisation du processeur, la demande de mémoire ou le trafic réseau.</span><span class="sxs-lookup"><span data-stu-id="91da6-105">You can scale hello number of VMs in hello scale set manually, or define rules tooautoscale based on CPU usage, memory demand, or network traffic.</span></span> <span data-ttu-id="91da6-106">Ce didacticiel explique comment déployer un groupe de machines virtuelles identiques dans Azure.</span><span class="sxs-lookup"><span data-stu-id="91da6-106">In this tutorial, you deploy a virtual machine scale set in Azure.</span></span> <span data-ttu-id="91da6-107">Vous allez apprendre à effectuer les actions suivantes :</span><span class="sxs-lookup"><span data-stu-id="91da6-107">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="91da6-108">Utiliser l’Extension de Script personnalisé de hello toodefine un tooscale de site IIS</span><span class="sxs-lookup"><span data-stu-id="91da6-108">Use hello Custom Script Extension toodefine an IIS site tooscale</span></span>
> * <span data-ttu-id="91da6-109">Créer un équilibrage de charge pour votre groupe identique</span><span class="sxs-lookup"><span data-stu-id="91da6-109">Create a load balancer for your scale set</span></span>
> * <span data-ttu-id="91da6-110">Créer un groupe de machines virtuelles identiques</span><span class="sxs-lookup"><span data-stu-id="91da6-110">Create a virtual machine scale set</span></span>
> * <span data-ttu-id="91da6-111">Augmentez ou diminuez le nombre de hello d’instances dans un ensemble d’échelle</span><span class="sxs-lookup"><span data-stu-id="91da6-111">Increase or decrease hello number of instances in a scale set</span></span>
> * <span data-ttu-id="91da6-112">Créer des règles de mise à l’échelle automatique</span><span class="sxs-lookup"><span data-stu-id="91da6-112">Create autoscale rules</span></span>

<span data-ttu-id="91da6-113">Ce didacticiel nécessite hello Azure PowerShell version 3.6 ou version ultérieure du module.</span><span class="sxs-lookup"><span data-stu-id="91da6-113">This tutorial requires hello Azure PowerShell module version 3.6 or later.</span></span> <span data-ttu-id="91da6-114">Exécutez ` Get-Module -ListAvailable AzureRM` version de hello toofind.</span><span class="sxs-lookup"><span data-stu-id="91da6-114">Run ` Get-Module -ListAvailable AzureRM` toofind hello version.</span></span> <span data-ttu-id="91da6-115">Si vous avez besoin de tooupgrade, consultez [installez Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="91da6-115">If you need tooupgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>


## <a name="scale-set-overview"></a><span data-ttu-id="91da6-116">Vue d’ensemble des groupes identiques</span><span class="sxs-lookup"><span data-stu-id="91da6-116">Scale Set overview</span></span>
<span data-ttu-id="91da6-117">Jeux de montée en puissance utilisent les concepts similaires que vous avez appris dans le cadre du didacticiel précédent hello trop[créer des ordinateurs virtuels à haute disponibilités](tutorial-availability-sets.md).</span><span class="sxs-lookup"><span data-stu-id="91da6-117">Scale sets use similar concepts as you learned about in hello previous tutorial too[Create highly available VMs](tutorial-availability-sets.md).</span></span> <span data-ttu-id="91da6-118">Les machines virtuelles d’un groupe identique sont réparties entre les domaines d’erreur et de mise à jour, tout comme les machines virtuelles d’un groupe à haute disponibilité.</span><span class="sxs-lookup"><span data-stu-id="91da6-118">VMs in a scale set are distributed across fault and update domains just like VMs in an availability set.</span></span>

<span data-ttu-id="91da6-119">Les machines virtuelles sont créées en fonction des besoins dans un groupe identique.</span><span class="sxs-lookup"><span data-stu-id="91da6-119">VMs are created as needed in a scale set.</span></span> <span data-ttu-id="91da6-120">Vous définissez toocontrol de règles de mise à l’échelle quand et comment les machines virtuelles sont ajoutés ou supprimés à partir d’un ensemble d’échelle hello.</span><span class="sxs-lookup"><span data-stu-id="91da6-120">You define autoscale rules toocontrol how and when VMs are added or removed from hello scale set.</span></span> <span data-ttu-id="91da6-121">Ces règles peuvent se déclencher en fonction de mesures telles que la charge du processeur, l’utilisation de la mémoire ou le trafic réseau.</span><span class="sxs-lookup"><span data-stu-id="91da6-121">These rules can trigger based on metrics such as CPU load, memory usage, or network traffic.</span></span>

<span data-ttu-id="91da6-122">Échelle définit la prise en charge des too1, 000 des machines virtuelles lorsque vous utilisez une image de plateforme Azure.</span><span class="sxs-lookup"><span data-stu-id="91da6-122">Scale sets support up too1,000 VMs when you use an Azure platform image.</span></span> <span data-ttu-id="91da6-123">Pour les charges de travail avec installation significatifs ou des exigences de personnalisation de l’ordinateur virtuel, vous souhaiterez peut-être trop[créer une image de machine virtuelle personnalisée](tutorial-custom-images.md).</span><span class="sxs-lookup"><span data-stu-id="91da6-123">For workloads with significant installation or VM customization requirements, you may wish too[Create a custom VM image](tutorial-custom-images.md).</span></span> <span data-ttu-id="91da6-124">Vous pouvez créer des machines virtuelles de too100 dans une échelle définie lors de l’utilisation d’une image personnalisée.</span><span class="sxs-lookup"><span data-stu-id="91da6-124">You can create up too100 VMs in a scale set when using a custom image.</span></span>


## <a name="create-an-app-tooscale"></a><span data-ttu-id="91da6-125">Créer une application tooscale</span><span class="sxs-lookup"><span data-stu-id="91da6-125">Create an app tooscale</span></span>
<span data-ttu-id="91da6-126">Avant de créer un groupe identique, créez un groupe de ressources avec [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span><span class="sxs-lookup"><span data-stu-id="91da6-126">Before you can create a scale set, create a resource group with [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span></span> <span data-ttu-id="91da6-127">Hello exemple suivant crée un groupe de ressources nommé *myResourceGroupAutomate* Bonjour *EastUS* emplacement :</span><span class="sxs-lookup"><span data-stu-id="91da6-127">hello following example creates a resource group named *myResourceGroupAutomate* in hello *EastUS* location:</span></span>

```powershell
New-AzureRmResourceGroup -ResourceGroupName myResourceGroupScaleSet -Location EastUS
```

<span data-ttu-id="91da6-128">Dans un didacticiel antérieur, vous avez appris comment trop[configuration d’ordinateur virtuel d’automatiser](tutorial-automate-vm-deployment.md) à l’aide de hello Extension de Script personnalisé.</span><span class="sxs-lookup"><span data-stu-id="91da6-128">In an earlier tutorial, you learned how too[Automate VM configuration](tutorial-automate-vm-deployment.md) using hello Custom Script Extension.</span></span> <span data-ttu-id="91da6-129">Créer une configuration de jeu de mise à l’échelle, puis appliquer un tooinstall d’Extension de Script personnalisé et configurer IIS :</span><span class="sxs-lookup"><span data-stu-id="91da6-129">Create a scale set configuration then apply a Custom Script Extension tooinstall and configure IIS:</span></span>

```powershell
# Create a config object
$vmssConfig = New-AzureRmVmssConfig `
    -Location EastUS `
    -SkuCapacity 2 `
    -SkuName Standard_DS2 `
    -UpgradePolicyMode Automatic

# Define hello script for your Custom Script Extension toorun
$publicSettings = @{
    "fileUris" = (,"https://raw.githubusercontent.com/iainfoulds/azure-samples/master/automate-iis.ps1");
    "commandToExecute" = "powershell -ExecutionPolicy Unrestricted -File automate-iis.ps1"
}

# Use Custom Script Extension tooinstall IIS and configure basic website
Add-AzureRmVmssExtension -VirtualMachineScaleSet $vmssConfig `
    -Name "customScript" `
    -Publisher "Microsoft.Compute" `
    -Type "CustomScriptExtension" `
    -TypeHandlerVersion 1.8 `
    -Setting $publicSettings
```

## <a name="create-scale-load-balancer"></a><span data-ttu-id="91da6-130">Créer un équilibreur de charge d’échelle</span><span class="sxs-lookup"><span data-stu-id="91da6-130">Create scale load balancer</span></span>
<span data-ttu-id="91da6-131">Un équilibreur de charge Azure est un équilibreur de charge de type Couche 4 (TCP, UDP) qui offre une haute disponibilité en répartissant le trafic entrant entre les machines virtuelles saines.</span><span class="sxs-lookup"><span data-stu-id="91da6-131">An Azure load balancer is a Layer-4 (TCP, UDP) load balancer that provides high availability by distributing incoming traffic among healthy VMs.</span></span> <span data-ttu-id="91da6-132">Une sonde d’intégrité d’équilibrage de charge surveille un port donné sur chaque machine virtuelle et ne distribue le trafic tooan machine virtuelle opérationnelle.</span><span class="sxs-lookup"><span data-stu-id="91da6-132">A load balancer health probe monitors a given port on each VM and only distributes traffic tooan operational VM.</span></span> <span data-ttu-id="91da6-133">Pour plus d’informations, consultez l’étape suivante du didacticiel hello sur [comment tooload équilibrer les machines virtuelles Windows](tutorial-load-balancer.md).</span><span class="sxs-lookup"><span data-stu-id="91da6-133">For more information, see hello next tutorial on [How tooload balance Windows virtual machines](tutorial-load-balancer.md).</span></span>

<span data-ttu-id="91da6-134">Créez un équilibreur de charge doté d’une adresse IP publique qui distribue le trafic web sur le port 80 :</span><span class="sxs-lookup"><span data-stu-id="91da6-134">Create a load balancer that has a public IP address and distributes web traffic on port 80:</span></span>

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

# Create hello load balancer
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

# Create a load balancer rule toodistribute traffic on port 80
Add-AzureRmLoadBalancerRuleConfig `
  -Name myLoadBalancerRule `
  -LoadBalancer $lb `
  -FrontendIpConfiguration $lb.FrontendIpConfigurations[0] `
  -BackendAddressPool $lb.BackendAddressPools[0] `
  -Protocol Tcp `
  -FrontendPort 80 `
  -BackendPort 80

# Update hello load balancer configuration
Set-AzureRmLoadBalancer -LoadBalancer $lb
```

## <a name="create-a-scale-set"></a><span data-ttu-id="91da6-135">Créer un groupe identique</span><span class="sxs-lookup"><span data-stu-id="91da6-135">Create a scale set</span></span>
<span data-ttu-id="91da6-136">À présent, créez un groupe de machines virtuelles identiques avec [New-AzureRmVmss](/powershell/module/azurerm.compute/new-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="91da6-136">Now create a virtual machine scale set with [New-AzureRmVmss](/powershell/module/azurerm.compute/new-azurermvm).</span></span> <span data-ttu-id="91da6-137">Hello exemple suivant crée une échelle définie nommée *myScaleSet*:</span><span class="sxs-lookup"><span data-stu-id="91da6-137">hello following example creates a scale set named *myScaleSet*:</span></span>

```powershell
# Reference a virtual machine image from hello gallery
Set-AzureRmVmssStorageProfile $vmssConfig `
  -ImageReferencePublisher MicrosoftWindowsServer `
  -ImageReferenceOffer WindowsServer `
  -ImageReferenceSku 2016-Datacenter `
  -ImageReferenceVersion latest

# Set up information for authenticating with hello virtual machine
Set-AzureRmVmssOsProfile $vmssConfig `
  -AdminUsername azureuser `
  -AdminPassword P@ssword! `
  -ComputerNamePrefix myVM

# Create hello virtual network resources
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

# Attach hello virtual network toohello config object
Add-AzureRmVmssNetworkInterfaceConfiguration `
  -VirtualMachineScaleSet $vmssConfig `
  -Name "network-config" `
  -Primary $true `
  -IPConfiguration $ipConfig

# Create hello scale set with hello config object (this step might take a few minutes)
New-AzureRmVmss `
  -ResourceGroupName myResourceGroupScaleSet `
  -Name myScaleSet `
  -VirtualMachineScaleSet $vmssConfig
```

<span data-ttu-id="91da6-138">Il prend quelques minutes toocreate et que vous configurez toutes les ressources de jeu de mise à l’échelle hello et machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="91da6-138">It takes a few minutes toocreate and configure all hello scale set resources and VMs.</span></span>


## <a name="test-your-app"></a><span data-ttu-id="91da6-139">Test de l'application</span><span class="sxs-lookup"><span data-stu-id="91da6-139">Test your app</span></span>
<span data-ttu-id="91da6-140">toosee votre site Web d’IIS en action, obtenir hello adresse IP publique de votre équilibreur de charge avec [Get-AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress).</span><span class="sxs-lookup"><span data-stu-id="91da6-140">toosee your IIS website in action, obtain hello public IP address of your load balancer with [Get-AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress).</span></span> <span data-ttu-id="91da6-141">exemple Hello obtient adresse IP hello *myPublicIP* créé comme faisant partie d’un ensemble d’échelle hello :</span><span class="sxs-lookup"><span data-stu-id="91da6-141">hello following example obtains hello IP address for *myPublicIP* created as part of hello scale set:</span></span>

```powershell
Get-AzureRmPublicIPAddress -ResourceGroupName myResourceGroupScaleSet -Name myPublicIP | select IpAddress
```

<span data-ttu-id="91da6-142">Entrez l’adresse IP publique de hello dans le navigateur web de tooa.</span><span class="sxs-lookup"><span data-stu-id="91da6-142">Enter hello public IP address in tooa web browser.</span></span> <span data-ttu-id="91da6-143">application Hello s’affiche, y compris le nom d’hôte hello Hello VM que hello la charge du trafic d’équilibrage distribué à :</span><span class="sxs-lookup"><span data-stu-id="91da6-143">hello app is displayed, including hello hostname of hello VM that hello load balancer distributed traffic to:</span></span>

![Site IIS en cours d’exécution](./media/tutorial-create-vmss/running-iis-site.png)

<span data-ttu-id="91da6-145">toosee hello en puissance en action, vous pouvez forcer l’actualisation de le de votre charge web browser toosee hello équilibrage répartir le trafic entre tous les ordinateurs virtuels de hello votre application en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="91da6-145">toosee hello scale set in action, you can force-refresh your web browser toosee hello load balancer distribute traffic across all hello VMs running your app.</span></span>


## <a name="management-tasks"></a><span data-ttu-id="91da6-146">Tâches de gestion</span><span class="sxs-lookup"><span data-stu-id="91da6-146">Management tasks</span></span>
<span data-ttu-id="91da6-147">Tout au long du cycle de vie hello de hello ensemble d’échelle, vous devrez peut-être toorun une ou plusieurs tâches de gestion.</span><span class="sxs-lookup"><span data-stu-id="91da6-147">Throughout hello lifecycle of hello scale set, you may need toorun one or more management tasks.</span></span> <span data-ttu-id="91da6-148">En outre, vous souhaiterez toocreate les scripts qui automatisent différentes pour les tâches de cycle de vie.</span><span class="sxs-lookup"><span data-stu-id="91da6-148">Additionally, you may want toocreate scripts that automate various lifecycle-tasks.</span></span> <span data-ttu-id="91da6-149">Azure PowerShell fournit un moyen rapide de toodo ces tâches.</span><span class="sxs-lookup"><span data-stu-id="91da6-149">Azure PowerShell provides a quick way toodo those tasks.</span></span> <span data-ttu-id="91da6-150">Voici quelques tâches courantes.</span><span class="sxs-lookup"><span data-stu-id="91da6-150">Here are a few common tasks.</span></span>

### <a name="view-vms-in-a-scale-set"></a><span data-ttu-id="91da6-151">Afficher les machines virtuelles d’un groupe identique</span><span class="sxs-lookup"><span data-stu-id="91da6-151">View VMs in a scale set</span></span>
<span data-ttu-id="91da6-152">une liste d’ordinateurs virtuels en cours d’exécution dans l’échelle de votre jeu de tooview, utilisez [Get-AzureRmVmssVM](/powershell/module/azurerm.compute/get-azurermvmssvm) comme suit :</span><span class="sxs-lookup"><span data-stu-id="91da6-152">tooview a list of VMs running in your scale set, use [Get-AzureRmVmssVM](/powershell/module/azurerm.compute/get-azurermvmssvm) as follows:</span></span>

```powershell
# Get current scale set
$scaleset = Get-AzureRmVmss `
  -ResourceGroupName myResourceGroupScaleSet `
  -VMScaleSetName myScaleSet

# Loop through hello instanaces in your scale set
for ($i=1; $i -le ($scaleset.Sku.Capacity - 1); $i++) {
    Get-AzureRmVmssVM -ResourceGroupName myResourceGroupScaleSet `
      -VMScaleSetName myScaleSet `
      -InstanceId $i
}
```


### <a name="increase-or-decrease-vm-instances"></a><span data-ttu-id="91da6-153">Augmenter ou diminuer les instances de machines virtuelles</span><span class="sxs-lookup"><span data-stu-id="91da6-153">Increase or decrease VM instances</span></span>
<span data-ttu-id="91da6-154">nombre de hello toosee d’instances actuellement dans une échelle paramétrées, utilisez [Get-AzureRmVmss](/powershell/module/azurerm.compute/get-azurermvmss) et des requêtes sur *sku.capacity*:</span><span class="sxs-lookup"><span data-stu-id="91da6-154">toosee hello number of instances you currently have in a scale set, use [Get-AzureRmVmss](/powershell/module/azurerm.compute/get-azurermvmss) and query on *sku.capacity*:</span></span>

```powershell
Get-AzureRmVmss -ResourceGroupName myResourceGroupScaleSet `
    -VMScaleSetName myScaleSet | `
    Select -ExpandProperty Sku
```

<span data-ttu-id="91da6-155">Vous pouvez puis manuellement augmenter ou réduire le nombre hello d’ordinateurs virtuels dans l’échelle de hello avec [AzureRmVmss de mise à jour](/powershell/module/azurerm.compute/update-azurermvmss).</span><span class="sxs-lookup"><span data-stu-id="91da6-155">You can then manually increase or decrease hello number of virtual machines in hello scale set with [Update-AzureRmVmss](/powershell/module/azurerm.compute/update-azurermvmss).</span></span> <span data-ttu-id="91da6-156">Hello exemple suivant définit hello nombre de machines virtuelles dans votre échelle définie trop*5*:</span><span class="sxs-lookup"><span data-stu-id="91da6-156">hello following example sets hello number of VMs in your scale set too*5*:</span></span>

```powershell
# Get current scale set
$scaleset = Get-AzureRmVmss `
  -ResourceGroupName myResourceGroupScaleSet `
  -VMScaleSetName myScaleSet

# Set and update hello capacity of your scale set
$scaleset.sku.capacity = 5
Update-AzureRmVmss -ResourceGroupName myResourceGroupScaleSet `
    -Name myScaleSet `
    -VirtualMachineScaleSet $scaleset
```

<span data-ttu-id="91da6-157">Si prend quelques hello tooupdate de minutes spécifié nombre d’instances dans votre jeu de mise à l’échelle.</span><span class="sxs-lookup"><span data-stu-id="91da6-157">If takes a few minutes tooupdate hello specified number of instances in your scale set.</span></span>


### <a name="configure-autoscale-rules"></a><span data-ttu-id="91da6-158">Configurer des règles de mise à l’échelle automatique</span><span class="sxs-lookup"><span data-stu-id="91da6-158">Configure autoscale rules</span></span>
<span data-ttu-id="91da6-159">Plutôt que manuellement à l’échelle nombre hello d’instances dans l’échelle de votre jeu, vous définissez les règles de mise à l’échelle.</span><span class="sxs-lookup"><span data-stu-id="91da6-159">Rather than manually scaling hello number of instances in your scale set, you define autoscale rules.</span></span> <span data-ttu-id="91da6-160">Ces règles surveillent hello instances dans votre échelle définie et répondent en conséquence basé sur des métriques et des seuils que vous définissez.</span><span class="sxs-lookup"><span data-stu-id="91da6-160">These rules monitor hello instances in your scale set and respond accordingly based on metrics and thresholds you define.</span></span> <span data-ttu-id="91da6-161">Hello exemple suivant dotée d’une nombre hello d’instances d’une unité lorsque la charge de l’UC moyenne hello est supérieure à 60 % pendant une période de 5 minutes.</span><span class="sxs-lookup"><span data-stu-id="91da6-161">hello following example scales out hello number of instances by one when hello average CPU load is greater than 60% over a 5 minute period.</span></span> <span data-ttu-id="91da6-162">Si la charge d’UC moyen hello, puis est inférieur à 30 % sur une période de 5 minutes, les instances de hello sont distribuées dans par une instance :</span><span class="sxs-lookup"><span data-stu-id="91da6-162">If hello average CPU load then drops below 30% over a 5 minute period, hello instances are scaled in by one instance:</span></span>

```powershell
# Define your scale set information
$mySubscriptionId = (Get-AzureRmSubscription).Id
$myResourceGroup = "myResourceGroupScaleSet"
$myScaleSet = "myScaleSet"
$myLocation = "East US"

# Create a scale up rule tooincrease hello number instances after 60% average CPU usage exceeded for a 5 minute period
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

# Create a scale down rule toodecrease hello number of instances after 30% average CPU usage over a 5 minute period
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

# Apply hello autoscale rules
Add-AzureRmAutoscaleSetting `
  -Location $myLocation `
  -Name "autosetting" `
  -ResourceGroup $myResourceGroup `
  -TargetResourceId /subscriptions/$mySubscriptionId/resourceGroups/$myResourceGroup/providers/Microsoft.Compute/virtualMachineScaleSets/$myScaleSet `
  -AutoscaleProfiles $myScaleProfile
```


## <a name="next-steps"></a><span data-ttu-id="91da6-163">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="91da6-163">Next steps</span></span>
<span data-ttu-id="91da6-164">Ce didacticiel vous a montré comment créer un groupe de machines virtuelles identiques.</span><span class="sxs-lookup"><span data-stu-id="91da6-164">In this tutorial, you created a virtual machine scale set.</span></span> <span data-ttu-id="91da6-165">Vous avez appris à effectuer les actions suivantes :</span><span class="sxs-lookup"><span data-stu-id="91da6-165">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="91da6-166">Utiliser l’Extension de Script personnalisé de hello toodefine un tooscale de site IIS</span><span class="sxs-lookup"><span data-stu-id="91da6-166">Use hello Custom Script Extension toodefine an IIS site tooscale</span></span>
> * <span data-ttu-id="91da6-167">Créer un équilibrage de charge pour votre groupe identique</span><span class="sxs-lookup"><span data-stu-id="91da6-167">Create a load balancer for your scale set</span></span>
> * <span data-ttu-id="91da6-168">Créer un groupe de machines virtuelles identiques</span><span class="sxs-lookup"><span data-stu-id="91da6-168">Create a virtual machine scale set</span></span>
> * <span data-ttu-id="91da6-169">Augmentez ou diminuez le nombre de hello d’instances dans un ensemble d’échelle</span><span class="sxs-lookup"><span data-stu-id="91da6-169">Increase or decrease hello number of instances in a scale set</span></span>
> * <span data-ttu-id="91da6-170">Créer des règles de mise à l’échelle automatique</span><span class="sxs-lookup"><span data-stu-id="91da6-170">Create autoscale rules</span></span>

<span data-ttu-id="91da6-171">Avance toolearn de didacticiel suivant toohello plus d’informations sur les concepts de machines virtuelles d’équilibrage de charge.</span><span class="sxs-lookup"><span data-stu-id="91da6-171">Advance toohello next tutorial toolearn more about load balancing concepts for virtual machines.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="91da6-172">Équilibrage de charge des machines virtuelles</span><span class="sxs-lookup"><span data-stu-id="91da6-172">Load balance virtual machines</span></span>](tutorial-load-balancer.md)
