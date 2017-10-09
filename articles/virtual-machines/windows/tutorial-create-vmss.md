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
# <a name="create-a-virtual-machine-scale-set-and-deploy-a-highly-available-app-on-windows"></a>Créer un groupe de machines virtuelles identiques et déployer une application hautement disponible sur Windows
Un ensemble d’échelle de machine virtuelle vous permet de toodeploy et gérer un ensemble de machines virtuelles identiques et la mise à l’échelle automatique. Vous pouvez mettre à l’échelle nombre hello d’ordinateurs virtuels dans un ensemble d’échelle hello manuellement ou définir tooautoscale règles en fonction de l’utilisation du processeur, la demande de mémoire ou le trafic réseau. Ce didacticiel explique comment déployer un groupe de machines virtuelles identiques dans Azure. Vous allez apprendre à effectuer les actions suivantes :

> [!div class="checklist"]
> * Utiliser l’Extension de Script personnalisé de hello toodefine un tooscale de site IIS
> * Créer un équilibrage de charge pour votre groupe identique
> * Créer un groupe de machines virtuelles identiques
> * Augmentez ou diminuez le nombre de hello d’instances dans un ensemble d’échelle
> * Créer des règles de mise à l’échelle automatique

Ce didacticiel nécessite hello Azure PowerShell version 3.6 ou version ultérieure du module. Exécutez ` Get-Module -ListAvailable AzureRM` version de hello toofind. Si vous avez besoin de tooupgrade, consultez [installez Azure PowerShell module](/powershell/azure/install-azurerm-ps).


## <a name="scale-set-overview"></a>Vue d’ensemble des groupes identiques
Jeux de montée en puissance utilisent les concepts similaires que vous avez appris dans le cadre du didacticiel précédent hello trop[créer des ordinateurs virtuels à haute disponibilités](tutorial-availability-sets.md). Les machines virtuelles d’un groupe identique sont réparties entre les domaines d’erreur et de mise à jour, tout comme les machines virtuelles d’un groupe à haute disponibilité.

Les machines virtuelles sont créées en fonction des besoins dans un groupe identique. Vous définissez toocontrol de règles de mise à l’échelle quand et comment les machines virtuelles sont ajoutés ou supprimés à partir d’un ensemble d’échelle hello. Ces règles peuvent se déclencher en fonction de mesures telles que la charge du processeur, l’utilisation de la mémoire ou le trafic réseau.

Échelle définit la prise en charge des too1, 000 des machines virtuelles lorsque vous utilisez une image de plateforme Azure. Pour les charges de travail avec installation significatifs ou des exigences de personnalisation de l’ordinateur virtuel, vous souhaiterez peut-être trop[créer une image de machine virtuelle personnalisée](tutorial-custom-images.md). Vous pouvez créer des machines virtuelles de too100 dans une échelle définie lors de l’utilisation d’une image personnalisée.


## <a name="create-an-app-tooscale"></a>Créer une application tooscale
Avant de créer un groupe identique, créez un groupe de ressources avec [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup). Hello exemple suivant crée un groupe de ressources nommé *myResourceGroupAutomate* Bonjour *EastUS* emplacement :

```powershell
New-AzureRmResourceGroup -ResourceGroupName myResourceGroupScaleSet -Location EastUS
```

Dans un didacticiel antérieur, vous avez appris comment trop[configuration d’ordinateur virtuel d’automatiser](tutorial-automate-vm-deployment.md) à l’aide de hello Extension de Script personnalisé. Créer une configuration de jeu de mise à l’échelle, puis appliquer un tooinstall d’Extension de Script personnalisé et configurer IIS :

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

## <a name="create-scale-load-balancer"></a>Créer un équilibreur de charge d’échelle
Un équilibreur de charge Azure est un équilibreur de charge de type Couche 4 (TCP, UDP) qui offre une haute disponibilité en répartissant le trafic entrant entre les machines virtuelles saines. Une sonde d’intégrité d’équilibrage de charge surveille un port donné sur chaque machine virtuelle et ne distribue le trafic tooan machine virtuelle opérationnelle. Pour plus d’informations, consultez l’étape suivante du didacticiel hello sur [comment tooload équilibrer les machines virtuelles Windows](tutorial-load-balancer.md).

Créez un équilibreur de charge doté d’une adresse IP publique qui distribue le trafic web sur le port 80 :

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

## <a name="create-a-scale-set"></a>Créer un groupe identique
À présent, créez un groupe de machines virtuelles identiques avec [New-AzureRmVmss](/powershell/module/azurerm.compute/new-azurermvm). Hello exemple suivant crée une échelle définie nommée *myScaleSet*:

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

Il prend quelques minutes toocreate et que vous configurez toutes les ressources de jeu de mise à l’échelle hello et machines virtuelles.


## <a name="test-your-app"></a>Test de l'application
toosee votre site Web d’IIS en action, obtenir hello adresse IP publique de votre équilibreur de charge avec [Get-AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress). exemple Hello obtient adresse IP hello *myPublicIP* créé comme faisant partie d’un ensemble d’échelle hello :

```powershell
Get-AzureRmPublicIPAddress -ResourceGroupName myResourceGroupScaleSet -Name myPublicIP | select IpAddress
```

Entrez l’adresse IP publique de hello dans le navigateur web de tooa. application Hello s’affiche, y compris le nom d’hôte hello Hello VM que hello la charge du trafic d’équilibrage distribué à :

![Site IIS en cours d’exécution](./media/tutorial-create-vmss/running-iis-site.png)

toosee hello en puissance en action, vous pouvez forcer l’actualisation de le de votre charge web browser toosee hello équilibrage répartir le trafic entre tous les ordinateurs virtuels de hello votre application en cours d’exécution.


## <a name="management-tasks"></a>Tâches de gestion
Tout au long du cycle de vie hello de hello ensemble d’échelle, vous devrez peut-être toorun une ou plusieurs tâches de gestion. En outre, vous souhaiterez toocreate les scripts qui automatisent différentes pour les tâches de cycle de vie. Azure PowerShell fournit un moyen rapide de toodo ces tâches. Voici quelques tâches courantes.

### <a name="view-vms-in-a-scale-set"></a>Afficher les machines virtuelles d’un groupe identique
une liste d’ordinateurs virtuels en cours d’exécution dans l’échelle de votre jeu de tooview, utilisez [Get-AzureRmVmssVM](/powershell/module/azurerm.compute/get-azurermvmssvm) comme suit :

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


### <a name="increase-or-decrease-vm-instances"></a>Augmenter ou diminuer les instances de machines virtuelles
nombre de hello toosee d’instances actuellement dans une échelle paramétrées, utilisez [Get-AzureRmVmss](/powershell/module/azurerm.compute/get-azurermvmss) et des requêtes sur *sku.capacity*:

```powershell
Get-AzureRmVmss -ResourceGroupName myResourceGroupScaleSet `
    -VMScaleSetName myScaleSet | `
    Select -ExpandProperty Sku
```

Vous pouvez puis manuellement augmenter ou réduire le nombre hello d’ordinateurs virtuels dans l’échelle de hello avec [AzureRmVmss de mise à jour](/powershell/module/azurerm.compute/update-azurermvmss). Hello exemple suivant définit hello nombre de machines virtuelles dans votre échelle définie trop*5*:

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

Si prend quelques hello tooupdate de minutes spécifié nombre d’instances dans votre jeu de mise à l’échelle.


### <a name="configure-autoscale-rules"></a>Configurer des règles de mise à l’échelle automatique
Plutôt que manuellement à l’échelle nombre hello d’instances dans l’échelle de votre jeu, vous définissez les règles de mise à l’échelle. Ces règles surveillent hello instances dans votre échelle définie et répondent en conséquence basé sur des métriques et des seuils que vous définissez. Hello exemple suivant dotée d’une nombre hello d’instances d’une unité lorsque la charge de l’UC moyenne hello est supérieure à 60 % pendant une période de 5 minutes. Si la charge d’UC moyen hello, puis est inférieur à 30 % sur une période de 5 minutes, les instances de hello sont distribuées dans par une instance :

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


## <a name="next-steps"></a>Étapes suivantes
Ce didacticiel vous a montré comment créer un groupe de machines virtuelles identiques. Vous avez appris à effectuer les actions suivantes :

> [!div class="checklist"]
> * Utiliser l’Extension de Script personnalisé de hello toodefine un tooscale de site IIS
> * Créer un équilibrage de charge pour votre groupe identique
> * Créer un groupe de machines virtuelles identiques
> * Augmentez ou diminuez le nombre de hello d’instances dans un ensemble d’échelle
> * Créer des règles de mise à l’échelle automatique

Avance toolearn de didacticiel suivant toohello plus d’informations sur les concepts de machines virtuelles d’équilibrage de charge.

> [!div class="nextstepaction"]
> [Équilibrage de charge des machines virtuelles](tutorial-load-balancer.md)
