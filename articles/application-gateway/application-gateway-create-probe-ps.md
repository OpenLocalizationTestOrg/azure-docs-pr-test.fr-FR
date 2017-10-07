---
title: "aaaCreate personnalisé sonde - passerelle d’Application Azure - PowerShell | Documents Microsoft"
description: "Découvrez comment toocreate personnalisé sondage pour la passerelle d’Application à l’aide de PowerShell dans le Gestionnaire de ressources"
services: application-gateway
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 68feb660-7fa4-4f69-a7e4-bdd7bdc474db
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/26/2017
ms.author: gwallace
ms.openlocfilehash: 44c9ffa75401d6d0db023e66fa82c701fb0cf8bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-custom-probe-for-azure-application-gateway-by-using-powershell-for-azure-resource-manager"></a>Création d'une sonde personnalisée pour Azure Application Gateway avec PowerShell pour Azure Resource Manager

> [!div class="op_single_selector"]
> * [Portail Azure](application-gateway-create-probe-portal.md)
> * [Commandes PowerShell pour Azure Resource Manager](application-gateway-create-probe-ps.md)
> * [Azure Classic PowerShell](application-gateway-create-probe-classic-ps.md)

Dans cet article, vous ajoutez une passerelle existante d’application sonde personnalisée tooan avec PowerShell. Les sondes personnalisés sont utiles pour les applications qui ont une page de vérification d’intégrité spécifique ou pour les applications qui ne fournissent pas une réponse correcte sur l’application web de hello par défaut.

> [!NOTE]
> Azure dispose de deux modèles de déploiement différents pour créer et utiliser des ressources : [Resource Manager et classique](../azure-resource-manager/resource-manager-deployment-model.md).  Cet article couvre l’utilisation de modèle de déploiement Resource Manager hello, qui recommandées par Microsoft pour la plupart des déploiements de nouveau au lieu de hello [modèle de déploiement classique](application-gateway-create-probe-classic-ps.md).

[!INCLUDE [azure-ps-prerequisites-include.md](../../includes/azure-ps-prerequisites-include.md)]

## <a name="create-an-application-gateway-with-a-custom-probe"></a>Créer une passerelle d’application avec une sonde personnalisée

### <a name="sign-in-and-create-resource-group"></a>Se connecter et créer un groupe de ressources

1. Utilisez `Login-AzureRmAccount` tooauthenticate.

  ```powershell
  Login-AzureRmAccount
  ```

1. Obtient les abonnements hello pour le compte de hello.

  ```powershell
  Get-AzureRmSubscription
  ```

1. Choisissez parmi vos toouse abonnements Azure.

  ```powershell
  Select-AzureRmSubscription -Subscriptionid '{subscriptionGuid}'
  ```

1. Créez un groupe de ressources. Vous pouvez ignorer cette étape si vous disposez d’un groupe de ressources existant.

  ```powershell
  New-AzureRmResourceGroup -Name appgw-rg -Location 'West US'
  ```

Azure Resource Manager requiert que tous les groupes de ressources spécifient un emplacement. Cet emplacement est utilisé comme emplacement par défaut de hello pour les ressources dans ce groupe de ressources. Assurez-vous que toutes les commandes toocreate un hello d’utilisation de passerelle application même groupe de ressources.

Bonjour précédent exemple, nous avons créé un groupe de ressources appelé **appgw-RG** dans emplacement **ouest des États-Unis**.

### <a name="create-a-virtual-network-and-a-subnet"></a>Créer un réseau virtuel et un sous-réseau

Hello exemple suivant crée un réseau virtuel et un sous-réseau pour la passerelle d’application hello. La passerelle d’application a besoin d’utiliser son propre sous-réseau. Pour cette raison, sous-réseau hello créé pour la passerelle d’application hello doit être inférieure à l’espace d’adressage hello de tooallow de réseau virtuel hello pour les autres toobe sous-réseaux créés et utilisés.

```powershell
# Assign hello address range 10.0.0.0/24 tooa subnet variable toobe used toocreate a virtual network.
$subnet = New-AzureRmVirtualNetworkSubnetConfig -Name subnet01 -AddressPrefix 10.0.0.0/24

# Create a virtual network named appgwvnet in resource group appgw-rg for hello West US region using hello prefix 10.0.0.0/16 with subnet 10.0.0.0/24.
$vnet = New-AzureRmVirtualNetwork -Name appgwvnet -ResourceGroupName appgw-rg -Location 'West US' -AddressPrefix 10.0.0.0/16 -Subnet $subnet

# Assign a subnet variable for hello next steps, which create an application gateway.
$subnet = $vnet.Subnets[0]
```

### <a name="create-a-public-ip-address-for-hello-front-end-configuration"></a>Créer une adresse IP publique pour la configuration frontale de hello

Créer une ressource IP publique **publicIP01** dans le groupe de ressources **appgw-rg** pour la région ouest des États-Unis hello. Cet exemple utilise une adresse IP publique pour les adresses IP frontales hello de passerelle d’application hello.  Passerelle d’application nécessite hello publique IP adresse toohave un nom DNS créé dynamiquement par conséquent hello `-DomainNameLabel` ne peut pas être spécifié lors de la création de hello d’adresse IP publique de hello.

```powershell
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName appgw-rg -Name publicIP01 -Location 'West US' -AllocationMethod Dynamic
```

### <a name="create-an-application-gateway"></a>Créer une passerelle Application Gateway

Pour configurer tous les éléments de configuration avant de créer la passerelle d’application hello. Hello exemple suivant crée hello des éléments de configuration qui sont nécessaires pour une ressource de passerelle d’application.

| **Composant** | **Description** |
|---|---|
| **Configuration IP de la passerelle** | Configuration IP d’une passerelle d’application.|
| **Pool back-end** | Un pool d’adresses IP, du nom de domaine complet ou aux cartes réseau qui sont des serveurs d’applications toohello hello web application hôte|
| **Sonde d’intégrité** | Une sonde personnalisée utilisée intégrité hello toomonitor membres du pool principal hello|
| **Paramètres HTTP** | Collection de paramètres comprenant le port, le protocole, l’affinité basée sur les cookies, la sonde et le délai d’expiration.  Ces paramètres déterminent la façon dont le trafic est routé toohello les membres du pool principal|
| **Port frontal** | port Hello hello passerelle d’application écoute le trafic sur|
| **Écouteur** | Combinaison d’un protocole, d’une configuration d’adresses IP frontales et d’un port frontal. C’est ce qui écoute les demandes entrantes.
|**Règle**| Itinéraires hello trafic toohello approprié back-end basé sur les paramètres HTTP.|

```powershell
# Creates a application gateway Frontend IP configuration named gatewayIP01
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name gatewayIP01 -Subnet $subnet

#Creates a back-end IP address pool named pool01 with IP addresses 134.170.185.46, 134.170.188.221, 134.170.185.50.
$pool = New-AzureRmApplicationGatewayBackendAddressPool -Name pool01 -BackendIPAddresses 134.170.185.46, 134.170.188.221, 134.170.185.50

# Creates a probe that will check health at http://contoso.com/path/path.htm
$probe = New-AzureRmApplicationGatewayProbeConfig -Name probe01 -Protocol Http -HostName 'contoso.com' -Path '/path/path.htm' -Interval 30 -Timeout 120 -UnhealthyThreshold 8

# Creates hello backend http settings toobe used. This component references hello $probe created in hello previous command.
$poolSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name poolsetting01 -Port 80 -Protocol Http -CookieBasedAffinity Disabled -Probe $probe -RequestTimeout 80

# Creates a frontend port for hello application gateway toolisten on port 80 that will be used by hello listener.
$fp = New-AzureRmApplicationGatewayFrontendPort -Name frontendport01 -Port 80

# Creates a frontend IP configuration. This associates hello $publicip variable defined previously with hello front-end IP that will be used by hello listener.
$fipconfig = New-AzureRmApplicationGatewayFrontendIPConfig -Name fipconfig01 -PublicIPAddress $publicip

# Creates hello listener. hello listener is a combination of protocol and hello frontend IP configuration $fipconfig and frontend port $fp created in previous steps.
$listener = New-AzureRmApplicationGatewayHttpListener -Name listener01  -Protocol Http -FrontendIPConfiguration $fipconfig -FrontendPort $fp

# Creates hello rule that routes traffic toohello backend pools.  In this example we create a basic rule that uses hello previous defined http settings and backend address pool.  It also associates hello listener toohello rule
$rule = New-AzureRmApplicationGatewayRequestRoutingRule -Name rule01 -RuleType Basic -BackendHttpSettings $poolSetting -HttpListener $listener -BackendAddressPool $pool

# Sets hello SKU of hello application gateway, in this example we create a small standard application gateway with 2 instances.
$sku = New-AzureRmApplicationGatewaySku -Name Standard_Small -Tier Standard -Capacity 2

# hello final step creates hello application gateway with all hello previously defined components.
$appgw = New-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg -Location 'West US' -BackendAddressPools $pool -Probes $probe -BackendHttpSettingsCollection $poolSetting -FrontendIpConfigurations $fipconfig  -GatewayIpConfigurations $gipconfig -FrontendPorts $fp -HttpListeners $listener -RequestRoutingRules $rule -Sku $sku
```

## <a name="add-a-probe-tooan-existing-application-gateway"></a>Ajouter une passerelle d’application existant sonde tooan

Hello extrait de code suivant ajoute une passerelle d’application sonde tooan existant.

```powershell
# Load hello application gateway resource into a PowerShell variable by using Get-AzureRmApplicationGateway.
$getgw =  Get-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg

# Create hello probe object that will check health at http://contoso.com/path/path.htm
$getgw = Add-AzureRmApplicationGatewayProbeConfig -ApplicationGateway $getgw -Name probe01 -Protocol Http -HostName 'contoso.com' -Path '/path/custompath.htm' -Interval 30 -Timeout 120 -UnhealthyThreshold 8

# Set hello backend HTTP settings toouse hello new probe
$getgw = Set-AzureRmApplicationGatewayBackendHttpSettings -ApplicationGateway $getgw -Name $getgw.BackendHttpSettingsCollection.name -Port 80 -Protocol Http -CookieBasedAffinity Disabled -Probe $probe -RequestTimeout 120

# Save hello application gateway with hello configuration changes
Set-AzureRmApplicationGateway -ApplicationGateway $getgw
```

## <a name="remove-a-probe-from-an-existing-application-gateway"></a>Supprimer une sonde d’une passerelle d’application existante

Hello suivant extrait de code supprime une sonde d’une passerelle d’application existant.

```powershell
# Load hello application gateway resource into a PowerShell variable by using Get-AzureRmApplicationGateway.
$getgw =  Get-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg

# Remove hello probe from hello application gateway configuration object
$getgw = Remove-AzureRmApplicationGatewayProbeConfig -ApplicationGateway $getgw -Name $getgw.Probes.name

# Set hello backend HTTP settings tooremove hello reference toohello probe. hello backend http settings now use hello default probe
$getgw = Set-AzureRmApplicationGatewayBackendHttpSettings -ApplicationGateway $getgw -Name $getgw.BackendHttpSettingsCollection.name -Port 80 -Protocol http -CookieBasedAffinity Disabled

# Save hello application gateway with hello configuration changes
Set-AzureRmApplicationGateway -ApplicationGateway $getgw
```

## <a name="get-application-gateway-dns-name"></a>Obtenir le nom DNS d’une passerelle Application Gateway

Après la création de la passerelle de hello, hello prochaine étape consiste tooconfigure hello frontal pour la communication. Lorsque vous utilisez une adresse IP publique, la passerelle Application Gateway requiert un nom DNS attribué dynamiquement, ce qui n’est pas convivial. les utilisateurs finaux de tooensure pouvez atteindre la passerelle d’application hello un enregistrement CNAME peut être utilisé toopoint toohello public point de terminaison de la passerelle d’application hello. [Configuration d’un nom de domaine personnalisé pour Azure](../cloud-services/cloud-services-custom-domain-name-portal.md). toodo, détails de récupération de la passerelle d’application hello et son nom IP/DNS associé à l’aide de la passerelle d’application hello PublicIPAddress élément attaché toohello. nom DNS de la passerelle d’application Hello doit être utilisé toocreate un enregistrement CNAME, le nom DNS de points hello deux web applications toothis. les utilisation de Hello d’enregistrements d’un n’est pas recommandée étant donné que l’adresse IP virtuelle hello peut changer lors du redémarrage de la passerelle d’application.

```powershell
Get-AzureRmPublicIpAddress -ResourceGroupName appgw-RG -Name publicIP01
```

```
Name                     : publicIP01
ResourceGroupName        : appgw-RG
Location                 : westus
Id                       : /subscriptions/<subscription_id>/resourceGroups/appgw-RG/providers/Microsoft.Network/publicIPAddresses/publicIP01
Etag                     : W/"00000d5b-54ed-4907-bae8-99bd5766d0e5"
ResourceGuid             : 00000000-0000-0000-0000-000000000000
ProvisioningState        : Succeeded
Tags                     : 
PublicIpAllocationMethod : Dynamic
IpAddress                : xx.xx.xxx.xx
PublicIpAddressVersion   : IPv4
IdleTimeoutInMinutes     : 4
IpConfiguration          : {
                                "Id": "/subscriptions/<subscription_id>/resourceGroups/appgw-RG/providers/Microsoft.Network/applicationGateways/appgwtest/frontendIP
                            Configurations/frontend1"
                            }
DnsSettings              : {
                                "Fqdn": "00000000-0000-xxxx-xxxx-xxxxxxxxxxxx.cloudapp.net"
                            }
```

## <a name="next-steps"></a>Étapes suivantes

En savoir tooconfigure le déchargement SSL en vous rendant sur : [configurer le déchargement SSL](application-gateway-ssl-arm.md)

