---
title: "aaaCreate Azure interne l’équilibrage de charge - PowerShell | Documents Microsoft"
description: "Découvrez comment toocreate un interne l’équilibrage de charge à l’aide de PowerShell dans le Gestionnaire de ressources"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
tags: azure-resource-manager
ms.assetid: c6c98981-df9d-4dd7-a94b-cc7d1dc99369
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: 4b9657c77aa32a142de49ff7871ed6a396b22223
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-internal-load-balancer-using-powershell"></a>Créer un équilibreur de charge interne à l’aide de PowerShell

> [!div class="op_single_selector"]
> * [Portail Azure](../load-balancer/load-balancer-get-started-ilb-arm-portal.md)
> * [PowerShell](../load-balancer/load-balancer-get-started-ilb-arm-ps.md)
> * [Interface de ligne de commande Azure](../load-balancer/load-balancer-get-started-ilb-arm-cli.md)
> * [Modèle](../load-balancer/load-balancer-get-started-ilb-arm-template.md)

[!INCLUDE [load-balancer-get-started-ilb-intro-include.md](../../includes/load-balancer-get-started-ilb-intro-include.md)]

> [!NOTE]
> Azure dispose de deux modèles de déploiement différents pour créer et utiliser des ressources : [Resource Manager et classique](../azure-resource-manager/resource-manager-deployment-model.md).  Cet article couvre l’utilisation de modèle de déploiement Resource Manager hello, qui recommandées par Microsoft pour la plupart des déploiements de nouveau au lieu de hello [modèle de déploiement classique](load-balancer-get-started-ilb-classic-ps.md).

[!INCLUDE [load-balancer-get-started-ilb-scenario-include.md](../../includes/load-balancer-get-started-ilb-scenario-include.md)]

[!INCLUDE [azure-ps-prerequisites-include.md](../../includes/azure-ps-prerequisites-include.md)]

Hello suit explique comment toocreate un interne l’équilibrage de charge à l’aide du Gestionnaire de ressources Azure avec PowerShell. Avec Azure Resource Manager, hello éléments toocreate un équilibreur de charge interne sont configurées individuellement, puis combinés toocreate un équilibreur de charge.

Vous devez toocreate et que vous configurez hello suivant objets toodeploy un équilibreur de charge :

* Avant la configuration IP de fin - configurera hello adresse IP privée pour le trafic réseau entrant
* Pool d’adresses principales - configure les interfaces réseau hello afin de recevront le trafic à charge équilibrée de hello provenant d’un pool d’adresses IP de serveur frontal
* Règles d’équilibrage de charge - source et la configuration du port local pour hello l’équilibrage de charge.
* Sondes - configure la sonde d’état d’intégrité hello pour les instances de Machine virtuelle hello.
* Les règles NAT de trafic entrant - configure l’accès hello port règles toodirectly une des instances de Machine virtuelle hello.

Pour obtenir plus d’informations sur les composants de l’équilibrage de charge avec Azure Resource Manager, consultez la page [Support Azure Resource Manager pour l’équilibrage de charge](load-balancer-arm.md).

Hello étapes suivantes expliquent comment tooconfigure un équilibrage de charge entre les deux machines virtuelles.

## <a name="setup-powershell-toouse-resource-manager"></a>Le programme d’installation PowerShell toouse Gestionnaire de ressources

Assurez-vous que vous avez hello dernière version de production hello module Azure pour PowerShell et disposez de PowerShell le programme d’installation correctement tooaccess votre abonnement Azure.

### <a name="step-1"></a>Étape 1

```powershell
Login-AzureRmAccount
```

### <a name="step-2"></a>Étape 2

Vérifiez les abonnements hello pour le compte de hello

```powershell
Get-AzureRmSubscription
```

Vous serez invité à tooAuthenticate avec vos informations d’identification.

### <a name="step-3"></a>Étape 3 :

Choisissez parmi vos toouse abonnements Azure.

```powershell
Select-AzureRmSubscription -Subscriptionid "GUID of subscription"
```

### <a name="create-resource-group-for-load-balancer"></a>Création d’un groupe de ressources pour l’équilibrage de charge

Créez un groupe de ressources (ignorez cette étape si vous utilisez un groupe de ressources existant)

```powershell
New-AzureRmResourceGroup -Name NRP-RG -location "West US"
```

Azure Resource Manager requiert que tous les groupes de ressources spécifient un emplacement. Cela est utilisé comme emplacement par défaut de hello pour les ressources dans ce groupe de ressources. Assurez-vous que toutes les commandes toocreate un équilibrage de charge utilisera hello même groupe de ressources.

Bonjour exemple ci-dessus nous avons créé un groupe de ressources appelé « NRP-RG » et l’emplacement « Ouest des États-Unis ».

## <a name="create-virtual-network-and-a-private-ip-address-for-front-end-ip-pool"></a>Créer un réseau virtuel et une adresse IP privée pour le pool d’adresses IP frontal

Crée un sous-réseau de réseau virtuel de hello et assigne toovariable $backendSubnet

```powershell
$backendSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name LB-Subnet-BE -AddressPrefix 10.0.2.0/24
```

Créez un réseau virtuel :

```powershell
$vnet= New-AzureRmVirtualNetwork -Name NRPVNet -ResourceGroupName NRP-RG -Location "West US" -AddressPrefix 10.0.0.0/16 -Subnet $backendSubnet
```

Crée le réseau virtuel de hello et ajoute le réseau virtuel hello sous-réseau toohello d’équilibrage de charge sous-réseau être NRPVNet et assigne toovariable $vnet

## <a name="create-front-end-ip-pool-and-backend-address-pool"></a>Création du pool d’adresses IP frontales et du pool d’adresses principales

Configuration d’un pool d’IP de serveur frontal pour hello entrant charger équilibrage réseau le trafic et principal adresse pool tooreceive hello à charge équilibrée.

### <a name="step-1"></a>Étape 1

Créer un pool d’IP front-end à l’aide d’adresse IP privée de hello 10.0.2.5 pour les 10.0.2.0/24 sous-réseau hello qui sera endpoint de trafic réseau entrant hello.

```powershell
$frontendIP = New-AzureRmLoadBalancerFrontendIpConfig -Name LB-Frontend -PrivateIpAddress 10.0.2.5 -SubnetId $vnet.subnets[0].Id
```

### <a name="step-2"></a>Étape 2

Configurer un pool d’adresses principale utilisée tooreceive le trafic entrant à partir du pool d’adresses IP de serveur frontal :

```powershell
$beaddresspool= New-AzureRmLoadBalancerBackendAddressPoolConfig -Name "LB-backend"
```

## <a name="create-lb-rules-nat-rules-probe-and-load-balancer"></a>Création des règles d’équilibrage de charge, des règles NAT, de la sonde et de l’équilibrage de charge

Après avoir créé le pool d’adresses IP hello frontal et le pool d’adresses principales hello, vous avez besoin des règles de hello toocreate qui appartiendront la ressource de programme d’équilibrage de charge toohello :

### <a name="step-1"></a>Étape 1

```powershell
$inboundNATRule1= New-AzureRmLoadBalancerInboundNatRuleConfig -Name "RDP1" -FrontendIpConfiguration $frontendIP -Protocol TCP -FrontendPort 3441 -BackendPort 3389

$inboundNATRule2= New-AzureRmLoadBalancerInboundNatRuleConfig -Name "RDP2" -FrontendIpConfiguration $frontendIP -Protocol TCP -FrontendPort 3442 -BackendPort 3389

$healthProbe = New-AzureRmLoadBalancerProbeConfig -Name "HealthProbe" -RequestPath "HealthProbe.aspx" -Protocol http -Port 80 -IntervalInSeconds 15 -ProbeCount 2

$lbrule = New-AzureRmLoadBalancerRuleConfig -Name "HTTP" -FrontendIpConfiguration $frontendIP -BackendAddressPool $beAddressPool -Probe $healthProbe -Protocol Tcp -FrontendPort 80 -BackendPort 80
```

exemple Hello ci-dessus crée hello éléments suivants :

* Règle NAT qui tout trafic entrant du trafic tooport 3441 passera tooport 3389.
* une autre règle NAT qui tout trafic entrant du trafic tooport 3442 passera tooport 3389.
* une règle d’équilibreur de charge qui chargera équilibrer tout le trafic entrant sur le port port public 80 toolocal 80 dans le pool d’adresses hello back-end.
* une règle d’analyse qui vérifie l’état d’intégrité de hello pour le chemin d’accès « HealthProbe.aspx »

### <a name="step-2"></a>Étape 2

Créer un équilibreur de charge hello additionnant tous les objets (les règles NAT, règles d’équilibrage de charge, les configurations de sonde) :

```powershell
$NRPLB = New-AzureRmLoadBalancer -ResourceGroupName "NRP-RG" -Name "NRP-LB" -Location "West US" -FrontendIpConfiguration $frontendIP -InboundNatRule $inboundNATRule1,$inboundNatRule2 -LoadBalancingRule $lbrule -BackendAddressPool $beAddressPool -Probe $healthProbe
```

## <a name="create-network-interfaces"></a>Création d’interfaces réseau

Après avoir créé un équilibreur de charge interne hello, vous devez définir les interfaces réseau recevra hello équilibré de charge réseau du trafic entrant, les règles NAT et la sonde. Dans ce cas, interface de réseau Hello est configuré individuellement et peut être affectée tooa virtuels plus tard.

### <a name="step-1"></a>Étape 1

Obtenir les ressources hello virtuels interfaces réseau toocreate réseau et le sous-réseau :

```powershell
$vnet = Get-AzureRmVirtualNetwork -Name NRPVNet -ResourceGroupName NRP-RG

$backendSubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name LB-Subnet-BE -VirtualNetwork $vnet
```

Cette étape crée une interface réseau qui appartiennent toohello pool principal d’équilibrage de charge et associer la première règle NAT de hello pour RDP pour cette interface réseau :

```powershell
$backendnic1= New-AzureRmNetworkInterface -ResourceGroupName "NRP-RG" -Name lb-nic1-be -Location "West US" -PrivateIpAddress 10.0.2.6 -Subnet $backendSubnet -LoadBalancerBackendAddressPool $nrplb.BackendAddressPools[0] -LoadBalancerInboundNatRule $nrplb.InboundNatRules[0]
```

### <a name="step-2"></a>Étape 2

Créez une deuxième interface réseau appelée LB-Nic2-BE :

Cette étape crée une deuxième interface réseau, affectation toohello même équilibreur de charge précédent fin pool associant la deuxième règle NAT hello créé pour RDP :

```powershell
$backendnic2= New-AzureRmNetworkInterface -ResourceGroupName "NRP-RG" -Name lb-nic2-be -Location "West US" -PrivateIpAddress 10.0.2.7 -Subnet $backendSubnet -LoadBalancerBackendAddressPool $nrplb.BackendAddressPools[0] -LoadBalancerInboundNatRule $nrplb.InboundNatRules[1]
```

résultat final de Hello affiche suivant de hello :

    $backendnic1

Sortie attendue :

    Name                 : lb-nic1-be
    ResourceGroupName    : NRP-RG
    Location             : westus
    Id                   : /subscriptions/f50504a2-1865-4541-823a-b32842e3e0ee/resourceGroups/NRP-RG/providers/Microsoft.Network/networkInterfaces/lb-nic1-be
    Etag                 : W/"d448256a-e1df-413a-9103-a137e07276d1"
    ProvisioningState    : Succeeded
    Tags                 :
    VirtualMachine       : null
    IpConfigurations     : [
                         {
                           "PrivateIpAddress": "10.0.2.6",
                           "PrivateIpAllocationMethod": "Static",
                           "Subnet": {
                             "Id": "/subscriptions/f50504a2-1865-4541-823a-b32842e3e0ee/resourceGroups/NRP-RG/providers/Microsoft.Network/virtualNetworks/NRPVNet/subnets/LB-Subnet-BE"
                           },
                           "PublicIpAddress": {
                             "Id": null
                           },
                           "LoadBalancerBackendAddressPools": [
                             {
                               "Id": "/subscriptions/f50504a2-1865-4541-823a-b32842e3e0ee/resourceGroups/NRP-RG/providers/Microsoft.Network/loadBalancers/NRPlb/backendAddressPools/LB-backend"
                             }
                           ],
                           "LoadBalancerInboundNatRules": [
                             {
                               "Id": "/subscriptions/f50504a2-1865-4541-823a-b32842e3e0ee/resourceGroups/NRP-RG/providers/Microsoft.Network/loadBalancers/NRPlb/inboundNatRules/RDP1"
                             }
                           ],
                           "ProvisioningState": "Succeeded",
                           "Name": "ipconfig1",
                           "Etag": "W/\"d448256a-e1df-413a-9103-a137e07276d1\"",
                           "Id": "/subscriptions/f50504a2-1865-4541-823a-b32842e3e0ee/resourceGroups/NRP-RG/providers/Microsoft.Network/networkInterfaces/lb-nic1-be/ipConfigurations/ipconfig1"
                         }
                       ]
    DnsSettings          : {
                         "DnsServers": [],
                         "AppliedDnsServers": []
                       }
    AppliedDnsSettings   :
    NetworkSecurityGroup : null
    Primary              : False



### <a name="step-3"></a>Étape 3 :

Utilisez hello commande Add-AzureRmVMNetworkInterface tooassign hello NIC tooa virtuels.

Vous pouvez trouver hello des instructions étape par étape toocreate une machine virtuelle et affecter tooa NIC suivant la documentation de hello : [créer une machine virtuelle de Azure à l’aide de PowerShell](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json).

## <a name="add-hello-network-interface"></a>Ajouter une interface de réseau hello

Si vous disposez déjà d’un ordinateur virtuel créé, vous pouvez ajouter l’interface de réseau de hello avec hello comme suit :

### <a name="step-1"></a>Étape 1

Charger la ressource de programme d’équilibrage de charge hello dans une variable (si vous n’avez pas encore fait). variable Hello utilisée est appelée $lb et hello utilisez mêmes noms de ressource de programme d’équilibrage de charge hello créés ci-dessus.

```powershell
$lb = Get-AzureRmLoadBalancer –name NRP-LB -resourcegroupname NRP-RG
```

### <a name="step-2"></a>Étape 2

Charge la variable de tooa configuration hello back-end.

```powershell
$backend = Get-AzureRmLoadBalancerBackendAddressPoolConfig -name backendpool1 -LoadBalancer $lb
```

### <a name="step-3"></a>Étape 3 :

Charger l’interface de réseau hello déjà créé dans une variable. nom de variable de Hello utilisée est la carte réseau de $. nom de l’interface réseau Hello utilisé est hello même à partir de l’exemple hello ci-dessus.

```powershell
$nic = Get-AzureRmNetworkInterface –name lb-nic1-be -resourcegroupname NRP-RG
```

### <a name="step-4"></a>Étape 4

Modifier la configuration de serveur principal hello sur l’interface de réseau hello.

```powershell
$nic.IpConfigurations[0].LoadBalancerBackendAddressPools=$backend
```

### <a name="step-5"></a>Étape 5

Enregistrer l’objet d’interface réseau hello.

```powershell
Set-AzureRmNetworkInterface -NetworkInterface $nic
```

Après l’ajout d’une interface réseau toohello pool principal d’équilibrage de charge, il commence à recevoir le trafic de réseau basé sur des règles pour cette ressource d’équilibrage de charge d’équilibrage de charge hello.

## <a name="update-an-existing-load-balancer"></a>Mettre à jour un équilibreur de charge existant

### <a name="step-1"></a>Étape 1
À l’aide d’équilibrage de charge hello à partir de l’exemple hello ci-dessus, affecter charge équilibrage objet toovariable $slb à l’aide de Get-AzureRmLoadBalancer

```powershell
$slb = Get-AzureRmLoadBalancer -Name NRPLB -ResourceGroupName NRP-RG
```

### <a name="step-2"></a>Étape 2

Bonjour l’exemple suivant, vous allez ajouter une règle NAT de trafic entrant via le port 81 dans frontal hello et port 8181 pour la sauvegarde de hello se terminer à équilibrage de charge existante de pool tooan

```powershell
$slb | Add-AzureRmLoadBalancerInboundNatRuleConfig -Name NewRule -FrontendIpConfiguration $slb.FrontendIpConfigurations[0] -FrontendPort 81  -BackendPort 8181 -Protocol Tcp
```

### <a name="step-3"></a>Étape 3 :

Enregistrez hello nouvelle configuration à l’aide de Set-AzureLoadBalancer

```powershell
$slb | Set-AzureRmLoadBalancer
```

## <a name="remove-a-load-balancer"></a>Supprimer un équilibreur de charge

Utilisez hello commande Remove-AzureRmLoadBalancer toodelete un équilibreur de charge créé précédemment nommé « NRP kg » dans un groupe de ressources appelé « NRP-RG »

```powershell
Remove-AzureRmLoadBalancer -Name NRPLB -ResourceGroupName NRP-RG
```

> [!NOTE]
> Vous pouvez utiliser hello facultatif commutateur - invite de commandes de Force tooavoid hello pour suppression.

## <a name="next-steps"></a>Étapes suivantes

[Configuration d’un mode de distribution d’équilibrage de charge](load-balancer-distribution-mode.md)

[Configuration des paramètres du délai d’expiration TCP inactif pour votre équilibrage de charge](load-balancer-tcp-idle-timeout.md)
