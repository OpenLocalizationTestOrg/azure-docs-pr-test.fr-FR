---
title: "ensemble d’une échelle de machine virtuelle Azure aaaCreate | Documents Microsoft"
description: "Créez et déployez un groupe de machines virtuelles identiques Linux ou Windows Azure avec Azure CLI, PowerShell, un modèle ou Visual Studio."
services: virtual-machine-scale-sets
documentationcenter: 
author: Thraka
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machine-scale-sets
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: azurecli
ms.topic: article
ms.date: 07/21/2017
ms.author: adegeo
ms.openlocfilehash: 73de25c1dd2424e64655b3accfea848926e72f69
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-deploy-a-virtual-machine-scale-set"></a>Créer et déployer un groupe de machines virtuelles identiques
Machines virtuelles identiques facilitent vous toodeploy et gérer des machines virtuelles identiques en tant qu’ensemble. Les groupes à échelle identique fournissent une couche de calcul hautement évolutive et personnalisable pour les applications « hyperscale », et prennent en charge les images de plateforme Windows, les images de plateforme Linux, des images personnalisées et les extensions. Pour plus d’informations sur les groupes identiques, consultez [Groupes de machines virtuelles identiques](virtual-machine-scale-sets-overview.md).

Ce didacticiel vous montre comment toocreate définie une échelle de machines virtuelles **sans** à l’aide de hello portail Azure. Pour plus d’informations sur la façon dont toouse hello portail Azure, consultez [toocreate une échelle de machines virtuelles définition avec hello Azure portal](virtual-machine-scale-sets-portal-create.md).

>[!NOTE]
>Pour plus d’informations sur les ressources Azure Resource Manager, consultez [Déploiement Azure Resource Manager et déploiement classique](../azure-resource-manager/resource-manager-deployment-model.md).

## <a name="sign-in-tooazure"></a>Connectez-vous à tooAzure

Si vous utilisez Azure CLI 2.0 ou Azure PowerShell toocreate une échelle définie, vous devez tout d’abord toosign dans tooyour abonnement.

Pour plus d’informations sur la façon dont tooinstall, configurer et vous connecter tooAzure avec CLI d’Azure ou de PowerShell, consultez [prise en main d’Azure CLI 2.0](/cli/azure/get-started-with-azure-cli.md) ou [prise en main des applets de commande Azure PowerShell](/powershell/azure/overview).

```azurecli
az login
```

```powershell
Login-AzureRmAccount
```

## <a name="create-a-resource-group"></a>Créer un groupe de ressources

Vous devez tout d’abord toocreate un groupe de ressources ensemble d’échelle de machine virtuelle hello est associé.

```azurecli
az group create --location westus2 --name MyResourceGroup1
```

```powershell
New-AzureRmResourceGroup -Location westus2 -Name MyResourceGroup1
```

## <a name="create-from-azure-cli"></a>Créer à partir de l’interface de ligne de commande Azure

Avec Azure CLI, vous pouvez créer un groupe de machines virtuelles identiques avec un minimum d’effort. Si vous omettez les valeurs par défaut, elles vous sont fournies. Par exemple, si vous ne spécifiez pas les informations du réseau virtuel, un réseau virtuel est créé pour vous. Si vous omettez les composants suivants de hello, ils sont créés pour vous : 
- Un équilibrage de charge
- Un réseau virtuel
- Une adresse IP publique

Lorsque les choix hello image de machine virtuelle que vous souhaitez toouse sur l’ensemble d’échelle de machine virtuelle hello, vous avez le choix :

- URN  
Identificateur Hello d’une ressource :  
**Win2012R2Datacenter**

- Alias d’URN  
nom convivial de Hello d’un URN :  
**MicrosoftWindowsServer:WindowsServer:2012-R2-Datacenter:latest**

- ID de ressource personnalisé  
tooan de chemin d’accès Hello ressource Azure :  
**/subscriptions/subscription-guid/resourceGroups/MyResourceGroup/providers/Microsoft.Compute/images/MyImage**

- Ressource web  
tooan de chemin d’accès Hello URI HTTP :  
**http://contoso.blob.core.windows.net/vhds/osdiskimage.vhd**

>[!TIP]
>Vous pouvez obtenir la liste des images disponibles avec `az vm image list`.

définie d’une échelle de machines virtuelles toocreate, vous devez spécifier hello suivantes :

- Groupe de ressources 
- Nom
- Image du système d’exploitation
- Informations d’authentification 
 
Hello, l’exemple suivant crée un ensemble d’échelle base ordinateur virtuel (cette étape peut prendre quelques minutes).

```azurecli
az vmss create --resource-group MyResourceGroup1 --name MyScaleSet --image UbuntuLTS --authentication-type password --admin-username azureuser --admin-password P@ssw0rd!
```

Une fois que la fin de la commande hello maintenant avoir votre échelle de l’ordinateur virtuel créé. Vous devrez peut-être adresse tooget hello de machine virtuelle de hello afin que vous pouvez vous connecter à tooit. Vous pouvez obtenir de nombreuses informations différents sur l’ordinateur virtuel de hello (y compris l’adresse IP de hello) avec hello commande suivante. 

```azurecli
az vmss list-instance-connection-info --resource-group MyResourceGroup1 --name MyScaleSet
```

## <a name="create-from-powershell"></a>Créer à partir de PowerShell

PowerShell est toouse plus compliqué que CLI d’Azure. Alors que l’interface CLI Azure fournit les valeurs par défaut pour les ressources relatives à la mise en réseau (équilibrage de charge, adresse IP, réseau virtuel), ce n’est pas le cas de PowerShell. La référence à une image avec PowerShell est également un peu plus complexe. Vous pouvez obtenir des images avec hello suivant d’applets de commande :

1. Get-AzureRMVMImagePublisher
2. Get-AzureRMVMImageOffer
3. Get-AzureRmVMImageSku

travail d’applets de commande Hello peut être transmis dans la séquence. Voici un exemple de comment tooget toutes les images pour hello **ouest des États-Unis 2** région avec un serveur de publication qui a le nom de hello **microsoft** qu’il contient.

```powershell
Get-AzureRMVMImagePublisher -Location WestUS2 | Where-Object PublisherName -Like *microsoft* | Get-AzureRMVMImageOffer | Get-AzureRmVMImageSku | Select-Object PublisherName, Offer, Skus
```

```
PublisherName              Offer                    Skus
-------------              -----                    ----
microsoft-ads              linux-data-science-vm    linuxdsvm
microsoft-ads              standard-data-science-vm standard-data-science-vm
MicrosoftAzureSiteRecovery Process-Server           Windows-2012-R2-Datacenter
MicrosoftBizTalkServer     BizTalk-Server           2013-R2-Enterprise
MicrosoftBizTalkServer     BizTalk-Server           2013-R2-Standard
MicrosoftBizTalkServer     BizTalk-Server           2016-Developer
MicrosoftBizTalkServer     BizTalk-Server           2016-Enterprise
...
```

flux de travail Hello pour la création d’un ensemble d’échelle de machine virtuelle est la suivante :

1. Créer un objet de configuration qui conserve des informations sur l’ensemble d’échelle hello.
2. Référence hello du système d’exploitation image de base.
3. Configurer les paramètres de système d’exploitation hello : authentification, préfixe du nom de machine virtuelle et/passe de l’utilisateur.
4. Configurez la mise en réseau.
5. Créer un ensemble d’échelle hello.

Cet exemple crée un groupe identique de base à deux instances pour un ordinateur où Windows Server 2016 est installé.

```powershell
# Resource group name from above
$rg = "MyResourceGroup1"
$location = "WestUS2"

# Create a config object
$vmssConfig = New-AzureRmVmssConfig -Location $location -SkuCapacity 2 -SkuName Standard_A0  -UpgradePolicyMode Automatic

# Reference a virtual machine image from hello gallery
Set-AzureRmVmssStorageProfile $vmssConfig -ImageReferencePublisher MicrosoftWindowsServer -ImageReferenceOffer WindowsServer -ImageReferenceSku 2016-Datacenter -ImageReferenceVersion latest

# Set up information for authenticating with hello virtual machine
Set-AzureRmVmssOsProfile $vmssConfig -AdminUsername azureuser -AdminPassword P@ssw0rd! -ComputerNamePrefix myvmssvm

# Create hello virtual network resources

## Basics
$subnet = New-AzureRmVirtualNetworkSubnetConfig -Name "my-subnet" -AddressPrefix 10.0.0.0/24
$vnet = New-AzureRmVirtualNetwork -Name "my-network" -ResourceGroupName $rg -Location $location -AddressPrefix 10.0.0.0/16 -Subnet $subnet

## Load balancer
$publicIP = New-AzureRmPublicIpAddress -Name "PublicIP" -ResourceGroupName $rg -Location $location -AllocationMethod Static -DomainNameLabel "myuniquedomain"
$frontendIP = New-AzureRmLoadBalancerFrontendIpConfig -Name "LB-Frontend" -PublicIpAddress $publicIP
$backendPool = New-AzureRmLoadBalancerBackendAddressPoolConfig -Name "LB-backend"
$probe = New-AzureRmLoadBalancerProbeConfig -Name "HealthProbe" -Protocol Tcp -Port 80 -IntervalInSeconds 15 -ProbeCount 2
$inboundNATRule1= New-AzureRmLoadBalancerRuleConfig -Name "webserver" -FrontendIpConfiguration $frontendIP -Protocol Tcp -FrontendPort 80 -BackendPort 80 -IdleTimeoutInMinutes 15 -Probe $probe -BackendAddressPool $backendPool
$inboundNATPool1 = New-AzureRmLoadBalancerInboundNatPoolConfig -Name "RDP" -FrontendIpConfigurationId $frontendIP.Id -Protocol TCP -FrontendPortRangeStart 53380 -FrontendPortRangeEnd 53390 -BackendPort 3389

New-AzureRmLoadBalancer -ResourceGroupName $rg -Name "LB1" -Location $location -FrontendIpConfiguration $frontendIP -LoadBalancingRule $inboundNATRule1 -InboundNatPool $inboundNATPool1 -BackendAddressPool $backendPool -Probe $probe

## IP address config
$ipConfig = New-AzureRmVmssIpConfig -Name "my-ipaddress" -LoadBalancerBackendAddressPoolsId $backendPool.Id -SubnetId $vnet.Subnets[0].Id -LoadBalancerInboundNatPoolsId $inboundNATPool1.Id

# Attach hello virtual network toohello IP object
Add-AzureRmVmssNetworkInterfaceConfiguration -VirtualMachineScaleSet $vmssConfig -Name "network-config" -Primary $true -IPConfiguration $ipConfig

# Create hello scale set with hello config object (this step might take a few minutes)
New-AzureRmVmss -ResourceGroupName $rg -Name "MyScaleSet1" -VirtualMachineScaleSet $vmssConfig
```

### <a name="using-a-custom-virtual-machine-image"></a>Utilisation d’une image de machine virtuelle personnalisée
Si vous créez une échelle définie à partir de votre propre image personnalisée, au lieu de référencement d’une image de machine virtuelle à partir de la galerie de hello, hello _Set-AzureRmVmssStorageProfile_ commande ressemble à ceci :
```PowerShell
Set-AzureRmVmssStorageProfile -OsDiskCreateOption FromImage -ManagedDisk PremiumLRS -OsDiskCaching "None" -OsDiskOsType Linux -ImageReferenceId (Get-AzureRmImage -ImageName $VMImage -ResourceGroupName $rg).id
```

## <a name="create-from-a-template"></a>Créer à partir d’un modèle

Vous pouvez déployer un groupe de machines virtuelles identiques à l’aide d’un modèle Azure Resource Manager. Vous pouvez créer votre propre modèle, ou utilisez une de hello [référentiel de modèles](https://azure.microsoft.com/resources/templates/?term=vmss). Ces modèles peuvent être déployés directement tooyour abonnement Azure.

>[!NOTE]
>toocreate votre propre modèle, vous créez un fichier de texte JSON. Pour plus d’informations sur la façon toocreate et personnaliser un modèle, consultez [modèles Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md).

Un exemple de modèle est disponible [sur GitHub](https://github.com/gatneil/mvss/tree/minimum-viable-scale-set). Pour plus d’informations sur la façon dont toocreate et utiliser ces exemples, consultez [un ensemble d’échelle viable Minimum](.\virtual-machine-scale-sets-mvss-start.md).

## <a name="create-from-visual-studio"></a>Créer à partir de Visual Studio

Avec Visual Studio, vous pouvez créer un projet de groupe de ressources Azure et ajouter qu'une échelle de machines virtuelles des ensembles de tooit de modèle. Vous pouvez choisir si vous souhaitez que tooimport à partir de GitHub ou hello Galerie d’applications Web Azure. Un script de déploiement PowerShell est également généré pour vous. Pour plus d’informations, consultez [toocreate une échelle de machines virtuelles définition avec Visual Studio](virtual-machine-scale-sets-vs-create.md).

## <a name="create-from-hello-azure-portal"></a>Créer à partir de hello portail Azure

Hello portail Azure fournit un moyen pratique tooquickly créer un ensemble d’échelle. Pour plus d’informations, consultez [toocreate une échelle de machines virtuelles définition avec hello Azure portal](virtual-machine-scale-sets-portal-create.md).

## <a name="next-steps"></a>Étapes suivantes

En savoir plus sur les [disques de données](virtual-machine-scale-sets-attached-disks.md).

Découvrez comment trop[gérer vos applications](virtual-machine-scale-sets-deploy-app.md).
