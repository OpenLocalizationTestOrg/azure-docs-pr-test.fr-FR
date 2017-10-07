---
title: "aaaCreate une côté Azure Internet l’équilibrage de charge - PowerShell | Documents Microsoft"
description: "Découvrez comment toocreate une côté Internet l’équilibrage de charge dans le Gestionnaire de ressources à l’aide de PowerShell"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
tags: azure-resource-manager
ms.assetid: 8257f548-7019-417f-b15f-d004a1eec826
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: e4e0e5271bc83c23fc62c0910e784c57d2b30065
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started"></a>Création d’un équilibrage de charge accessible sur Internet dans Resource Manager à l’aide de PowerShell

> [!div class="op_single_selector"]
> * [Portail](../load-balancer/load-balancer-get-started-internet-portal.md)
> * [PowerShell](../load-balancer/load-balancer-get-started-internet-arm-ps.md)
> * [Interface de ligne de commande Azure](../load-balancer/load-balancer-get-started-internet-arm-cli.md)
> * [Modèle](../load-balancer/load-balancer-get-started-internet-arm-template.md)

[!INCLUDE [load-balancer-get-started-internet-intro-include.md](../../includes/load-balancer-get-started-internet-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

Cet article décrit le modèle de déploiement du Gestionnaire de ressources hello. Vous pouvez également [apprendre comment toocreate une côté Internet l’équilibrage de charge à l’aide du modèle de déploiement classique hello](load-balancer-get-started-internet-classic-cli.md).

[!INCLUDE [load-balancer-get-started-internet-scenario-include.md](../../includes/load-balancer-get-started-internet-scenario-include.md)]

## <a name="deploying-hello-solution-by-using-azure-powershell"></a>Déploiement des solutions de hello à l’aide d’Azure PowerShell

Hello procédures suivantes explique comment toocreate une côté Internet l’équilibrage de charge à l’aide du Gestionnaire de ressources Azure avec PowerShell. Avec Azure Resource Manager, chaque ressource est créé et configuré individuellement et puis rassembler toocreate un équilibreur de charge.

Vous devez créer et configurer hello suivant objets toodeploy un équilibreur de charge :

* Configuration d’adresses IP frontales : contient les adresses IP publiques (PIP) pour le trafic réseau entrant.
* Pool d’adresses de serveur principal : contient des interfaces réseau (NIC) pour le trafic réseau tooreceive de hello machines virtuelles à partir de l’équilibrage de charge hello.
* Règles d’équilibrage de charge : contient des règles pour mappent un port public sur le port de tooa d’équilibrage de charge de hello dans un pool d’adresses de serveur principal hello.
* Les règles NAT de trafic entrant : contient des règles pour mappent un port public sur le port de tooa d’équilibrage de charge de hello pour un ordinateur virtuel spécifique dans le pool d’adresses principal hello.
* Sondes : contient la disponibilité de toocheck les sondes utilisées de contrôle d’intégrité des instances de machine virtuelle dans le pool d’adresses principal hello.

Pour plus d’informations, consultez [Prise en charge d’un équilibreur de charge par Azure Resource Manager](load-balancer-arm.md).

## <a name="set-up-powershell-toouse-resource-manager"></a>Configuration PowerShell toouse Gestionnaire de ressources

Vérifiez que vous avez la dernière version de production hello du module du Gestionnaire de ressources Azure hello pour PowerShell :

1. Connectez-vous tooAzure.

    ```powershell
    Login-AzureRmAccount
    ```

    À l’invite, entrez vos informations d’identification.

2. Vérifiez les abonnements hello pour le compte de hello.

    ```powershell
    Get-AzureRmSubscription
    ```

3. Choisissez parmi vos toouse abonnements Azure.

    ```powershell
    Select-AzureRmSubscription -SubscriptionId 'GUID of subscription'
    ```

4. Créez un groupe de ressources. (Ignorez cette étape si vous utilisez un groupe de ressources existant.)

    ```powershell
    New-AzureRmResourceGroup -Name NRP-RG -location "West US"
    ```

## <a name="create-a-virtual-network-and-a-public-ip-address-for-hello-front-end-ip-pool"></a>Créer un réseau virtuel et une adresse IP publique hello frontal pool d’adresses IP

1. Créez un sous-réseau et un réseau virtuel.

    ```powershell
    $backendSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name LB-Subnet-BE -AddressPrefix 10.0.2.0/24
    New-AzureRmvirtualNetwork -Name NRPVNet -ResourceGroupName NRP-RG -Location 'West US' -AddressPrefix 10.0.0.0/16 -Subnet $backendSubnet
    ```

2. Créer une Azure publique ressource d’adresse IP, nommée **adresse IP publique**, toobe utilisé par un pool IP frontal portant le nom DNS de hello **loadbalancernrp.westus.cloudapp.azure.com**. hello commande suivante utilise hello type d’allocation statique.

    ```powershell
    $publicIP = New-AzureRmPublicIpAddress -Name PublicIp -ResourceGroupName NRP-RG -Location 'West US' -AllocationMethod Static -DomainNameLabel loadbalancernrp
    ```

   > [!IMPORTANT]
   > équilibrage de charge Hello utilise le nom de domaine hello de l’adresse IP publique hello en tant que préfixe pour son nom de domaine complet. Cela est différent du modèle de déploiement classique de hello, qui utilise le service de cloud computing hello comme hello d’équilibrage de charge nom de domaine complet.
   > Dans cet exemple, hello nom de domaine complet est **loadbalancernrp.westus.cloudapp.azure.com**.

## <a name="create-a-front-end-ip-pool-and-a-back-end-address-pool"></a>Créer un pool d’adresses IP frontales et un pool d’adresses principales

1. Créer un pool IP frontal nommé **LB-Frontend** qui utilise hello **adresse IP publique** ressource.

    ```powershell
    $frontendIP = New-AzureRmLoadBalancerFrontendIpConfig -Name LB-Frontend -PublicIpAddress $publicIP
    ```

2. Créez un pool d’adresses principales nommé **LB-backend**.

    ```powershell
    $beaddresspool = New-AzureRmLoadBalancerBackendAddressPoolConfig -Name LB-backend
    ```

## <a name="create-nat-rules-a-load-balancer-rule-a-probe-and-a-load-balancer"></a>Créer des règles NAT, une règle d’équilibreur de charge, une sonde et un équilibreur de charge

Cet exemple crée hello éléments suivants :

* Un tootranslate de règle NAT tout le trafic entrant sur le port 3441 tooport 3389
* Un tootranslate de règle NAT tout le trafic entrant sur le port 3442 tooport 3389
* Un état d’intégrité sonde règle toocheck hello, dans une page nommée **HealthProbe.aspx**
* Un toobalance de règle d’équilibrage de charge tout le trafic entrant sur le port 80 tooport 80 sur hello adresses dans le pool principal de hello
* Un équilibreur de charge qui utilise tous les objets ci-dessus

Suivez ces étapes :

1. Créer des règles NAT hello.

    ```powershell
    $inboundNATRule1= New-AzureRmLoadBalancerInboundNatRuleConfig -Name RDP1 -FrontendIpConfiguration $frontendIP -Protocol TCP -FrontendPort 3441 -BackendPort 3389

    $inboundNATRule2= New-AzureRmLoadBalancerInboundNatRuleConfig -Name RDP2 -FrontendIpConfiguration $frontendIP -Protocol TCP -FrontendPort 3442 -BackendPort 3389
    ```

2. Créer une sonde d’intégrité. Il existe deux façons tooconfigure une sonde :

    Sonde HTTP

    ```powershell
    $healthProbe = New-AzureRmLoadBalancerProbeConfig -Name HealthProbe -RequestPath 'HealthProbe.aspx' -Protocol http -Port 80 -IntervalInSeconds 15 -ProbeCount 2
    ```

    Sonde TCP

    ```powershell
    $healthProbe = New-AzureRmLoadBalancerProbeConfig -Name HealthProbe -Protocol Tcp -Port 80 -IntervalInSeconds 15 -ProbeCount 2
    ```

3. Créez une règle d’équilibreur de charge.

    ```powershell
    $lbrule = New-AzureRmLoadBalancerRuleConfig -Name HTTP -FrontendIpConfiguration $frontendIP -BackendAddressPool  $beAddressPool -Probe $healthProbe -Protocol Tcp -FrontendPort 80 -BackendPort 80
    ```

4. Créer l’équilibreur de charge hello en utilisant des objets de hello créé précédemment.

    ```powershell
    $NRPLB = New-AzureRmLoadBalancer -ResourceGroupName NRP-RG -Name NRP-LB -Location 'West US' -FrontendIpConfiguration $frontendIP -InboundNatRule $inboundNATRule1,$inboundNatRule2 -LoadBalancingRule $lbrule -BackendAddressPool $beAddressPool -Probe $healthProbe
    ```

## <a name="create-nics"></a>Créer des cartes réseau

Créer des interfaces réseau (ou modifier des modèles existants) et les associer tooNAT règles, des règles d’équilibrage de charge et des sondes :

1. Obtenir les réseaux virtuels hello et un sous-réseau de réseau virtuel, où les cartes réseau de hello doivent toobe créé.

    ```powershell
    $vnet = Get-AzureRmVirtualNetwork -Name NRPVNet -ResourceGroupName NRP-RG
    $backendSubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name LB-Subnet-BE -VirtualNetwork $vnet
    ```

2. Créez une carte réseau nommée **être lb-nic1**et l’associer à la première règle NAT de hello et un pool d’adresses de serveur principal premier (et unique) hello.

    ```powershell
    $backendnic1= New-AzureRmNetworkInterface -ResourceGroupName NRP-RG -Name lb-nic1-be -Location 'West US' -PrivateIpAddress 10.0.2.6 -Subnet $backendSubnet -LoadBalancerBackendAddressPool $nrplb.BackendAddressPools[0] -LoadBalancerInboundNatRule $nrplb.InboundNatRules[0]
    ```

3. Créez une carte réseau nommée **être lb-nic2**et l’associer à la deuxième règle NAT hello et un pool d’adresses de serveur principal premier (et unique) hello.

    ```powershell
    $backendnic2= New-AzureRmNetworkInterface -ResourceGroupName NRP-RG -Name lb-nic2-be -Location 'West US' -PrivateIpAddress 10.0.2.7 -Subnet $backendSubnet -LoadBalancerBackendAddressPool $nrplb.BackendAddressPools[0] -LoadBalancerInboundNatRule $nrplb.InboundNatRules[1]
    ```

4. Vérifiez les cartes réseau de hello.

        $backendnic1

    Sortie attendue :

        Name                 : lb-nic1-be
        ResourceGroupName    : NRP-RG
        Location             : westus
        Id                   : /subscriptions/f50504a2-1865-4541-823a-b32842e3e0ee/resourceGroups/NRP-RG/providers/Microsoft.Network/networkInterfaces/lb-nic1-be
        Etag                 : W/"d448256a-e1df-413a-9103-a137e07276d1"
        ResourceGuid         : 896cac4f-152a-40b9-b079-3e2201a5906e
        ProvisioningState    : Succeeded
        Tags                 :
        VirtualMachine       : null
        IpConfigurations     : [
                            {
                            "Name": "ipconfig1",
                            "Etag": "W/\"d448256a-e1df-413a-9103-a137e07276d1\"",
                            "Id": "/subscriptions/f50504a2-1865-4541-823a-b32842e3e0ee/resourceGroups/NRP-RG/providers/Microsoft.Network/networkInterfaces/lb-nic1-be/ipConfigurations/ipconfig1",
                            "PrivateIpAddress": "10.0.2.6",
                            "PrivateIpAllocationMethod": "Static",
                            "Subnet": {
                                "Id": "/subscriptions/f50504a2-1865-4541-823a-b32842e3e0ee/resourceGroups/NRP-RG/providers/Microsoft.Network/virtualNetworks/NRPVNet/subnets/LB-Subnet-BE"
                            },
                            "ProvisioningState": "Succeeded",
                            "PrivateIpAddressVersion": "IPv4",
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
                            "Primary": true,
                            "ApplicationGatewayBackendAddressPools": []
                            }
                        ]
        DnsSettings          : {
                            "DnsServers": [],
                            "AppliedDnsServers": [],
                            "InternalDomainNameSuffix": "prcwibzcuvie5hnxav0yjks2cd.dx.internal.cloudapp.net"
                        }
        EnableIPForwarding   : False
        NetworkSecurityGroup : null
        Primary              :

5. Hello d’utilisation `Add-AzureRmVMNetworkInterface` applet de commande tooassign hello NIC toodifferent machines virtuelles.

## <a name="create-a-virtual-machine"></a>Création d'une machine virtuelle

Pour des instructions sur la création d’une machine virtuelle et l’attribution d’une carte résau, voir [Création d’une machine virtuelle Azure à l’aide de PowerShell](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json).

## <a name="add-hello-network-interface-toohello-load-balancer"></a>Ajouter l’équilibrage de charge hello toohello de l’interface réseau

1. Équilibrage de charge hello de récupérer à partir d’Azure.

    Charger la ressource de programme d’équilibrage de charge hello dans une variable (si vous n’avez pas encore fait). variable de Hello est appelée **$lb**. Utilisez hello même les noms de ressource d’équilibrage de charge hello que vous avez créé précédemment.

    ```powershell
    $lb= get-azurermloadbalancer -name NRP-LB -resourcegroupname NRP-RG
    ```

2. Charge la variable de tooa hello configuration principale.

    ```powershell
    $backend=Get-AzureRmLoadBalancerBackendAddressPoolConfig -name LB-backend -LoadBalancer $lb
    ```

3. Charger l’interface de réseau hello déjà créé dans une variable. nom de variable Hello est **$nic**. Hello nom de l’interface réseau est hello identique à celui de hello exemple précédent.

    ```powershell
    $nic =get-azurermnetworkinterface -name lb-nic1-be -resourcegroupname NRP-RG
    ```

4. Modifier la configuration de serveur principal hello sur l’interface de réseau hello.

    ```powershell
    $nic.IpConfigurations[0].LoadBalancerBackendAddressPools=$backend
    ```

5. Enregistrer l’objet d’interface réseau hello.

    ```powershell
    Set-AzureRmNetworkInterface -NetworkInterface $nic
    ```

    Après l’ajout d’une interface réseau toohello pool principal d’équilibrage de charge, il commence à recevoir le trafic de réseau en fonction des règles d’équilibrage de charge hello pour cette ressource d’équilibrage de charge.

## <a name="update-an-existing-load-balancer"></a>Mettre à jour un équilibreur de charge existant

1. À l’aide de hello charger équilibrage de hello l’exemple précédent, assignez une variable de charge équilibrage objet toohello **$slb** à l’aide de `Get-AzureLoadBalancer`.

    ```powershell
    $slb = get-AzureRmLoadBalancer -Name NRP-LB -ResourceGroupName NRP-RG
    ```

2. Dans l’exemple suivant de hello, vous ajouter une règle NAT entrante--à l’aide du port 81 de pool frontal de hello et port 8181 pour le pool principal de hello--tooan équilibreur de charge existant.

    ```powershell
    $slb | Add-AzureRmLoadBalancerInboundNatRuleConfig -Name NewRule -FrontendIpConfiguration $slb.FrontendIpConfigurations[0] -FrontendPort 81  -BackendPort 8181 -Protocol TCP
    ```

3. Enregistrer la nouvelle configuration de hello à l’aide de `Set-AzureLoadBalancer`.

    ```powershell
    $slb | Set-AzureRmLoadBalancer
    ```

## <a name="remove-a-load-balancer"></a>Supprimer un équilibreur de charge

Utilisez la commande hello `Remove-AzureLoadBalancer` toodelete un équilibreur de charge créé précédemment nommé **kg NRP** dans un groupe de ressources appelé **NRP-RG**.

```powershell
Remove-AzureRmLoadBalancer -Name NRP-LB -ResourceGroupName NRP-RG
```

> [!NOTE]
> Vous pouvez utiliser le commutateur facultatif de hello **-Force** invite de commandes tooavoid hello pour suppression.

## <a name="next-steps"></a>Étapes suivantes

[Prise en main de la configuration d’un équilibrage de charge interne](load-balancer-get-started-ilb-arm-ps.md)

[Configuration d'un mode de distribution d'équilibrage de charge](load-balancer-distribution-mode.md)

[Configuration des paramètres du délai d’expiration TCP inactif pour votre équilibrage de charge](load-balancer-tcp-idle-timeout.md)
