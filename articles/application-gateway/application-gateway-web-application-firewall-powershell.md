---
title: "pare-feu d’applications web aaaConfigure - passerelle d’Application Azure | Documents Microsoft"
description: "Cet article fournit des conseils sur comment toostart à l’aide de web des pare-feu d’applications sur une passerelle d’Application existant ou nouveau."
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: 670b9732-874b-43e6-843b-d2585c160982
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/03/2017
ms.author: gwallace
ms.openlocfilehash: bd2a69901f0ec0d6551d633e2588b74c3ab59a71
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-web-application-firewall-on-a-new-or-existing-application-gateway"></a>Configurer un pare-feu d’application web sur une passerelle Application Gateway nouvelle ou existante

> [!div class="op_single_selector"]
> * [Portail Azure](application-gateway-web-application-firewall-portal.md)
> * [PowerShell](application-gateway-web-application-firewall-powershell.md)
> * [Interface de ligne de commande Azure](application-gateway-web-application-firewall-cli.md)

Découvrez comment toocreate un pare-feu d’applications web activé la passerelle d’Application, ou ajoutez des tooan de pare-feu d’application web existante de passerelle d’Application.

pare-feu d’applications Hello web (WAF) dans la passerelle d’Application Azure protège les applications web à partir des attaques courantes basée sur le web telles que l’injection SQL, les attaques de script entre sites et des détournements de session.

La passerelle Azure Application Gateway est un équilibreur de charge de couche 7. Il fournit un basculement, routage des performances des requêtes HTTP entre différents serveurs, qu’ils soient sur le cloud de hello ou localement. Application Gateway offre de nombreuses fonctionnalités de contrôleur de livraison d’applications (ADC) : équilibrage de charge HTTP, affinité de session basée sur les cookies, déchargement de protocole SSL, sondes d’intégrité personnalisées, prise en charge multisite, etc. toofind une liste complète des fonctionnalités prises en charge, visitez : [vue d’ensemble de la passerelle d’Application](application-gateway-introduction.md).

Hello ci-dessous montre comment trop[ajouter tooan de pare-feu d’application web existante Application Gateway](#add-web-application-firewall-to-an-existing-application-gateway) et [créer une passerelle d’Application qui utilise le pare-feu d’applications web](#create-an-application-gateway-with-web-application-firewall).

![image du scénario][scenario]

## <a name="waf-configuration-differences"></a>Différences de configuration WAF

Si vous avez lu [créer une passerelle d’Application avec PowerShell](application-gateway-create-gateway-arm.md), vous comprenez tooconfigure de paramètres de référence (SKU) hello lors de la création d’une passerelle d’Application. WAF fournit des paramètres supplémentaires toodefine lors de la configuration de référence (SKU) de hello sur une passerelle d’Application. Il n’y a aucune modification supplémentaire que vous apportez sur hello passerelle d’Application lui-même.

| **Paramètre** | **Détails**
|---|---|
|**Référence (SKU)** |Une passerelle Application Gateway normale sans WAF prend en charge les tailles **Standard\_Small**, **Standard\_Medium** et **Standard\_Large**. Avec l’introduction de hello de WAF, il existe deux références supplémentaires, **WAF\_support** et **WAF\_grande**. WAF n’est pas pris en charge sur les petites passerelles Application Gateway.|
|**Niveau** | les valeurs disponibles Hello sont **Standard** ou **WAF**. Lorsque vous utilisez un pare-feu d’applications web, vous devez choisir **WAF**.|
|**Mode** | Ce paramètre est le mode de WAF hello. Les valeurs autorisées sont **Détection** et **Prévention**. Lorsque WAF est configuré en mode de détection, toutes les menaces sont stockées dans un fichier journal. En mode de prévention, les événements sont toujours enregistrés, mais les intrus hello reçoive une réponse non autorisé 403 hello passerelle d’Application.|

## <a name="add-web-application-firewall-tooan-existing-application-gateway"></a>Ajouter tooan de pare-feu d’application web existante Application Gateway

Assurez-vous que vous utilisez la version la plus récente d’Azure PowerShell hello. Pour plus d’informations, voir [Utilisation de Windows PowerShell avec Azure Resource Manager](../powershell-azure-resource-manager.md).

1. Ouvrez une session dans tooyour compte Azure.

    ```powershell
    Login-AzureRmAccount
    ```

2. Sélectionnez toouse d’abonnement hello pour ce scénario.

    ```powershell
    Select-AzureRmSubscription -SubscriptionName "<Subscription name>"
    ```

3. Récupérer la passerelle hello que vous ajoutez au pare-feu d’applications web.

    ```powershell
    $gw = Get-AzureRmApplicationGateway -Name "AdatumGateway" -ResourceGroupName "MyResourceGroup"
    ```

1. Configurer la référence (SKU) de hello web application pare-feu. les tailles disponibles Hello sont **WAF\_grande** et **WAF\_support**. Pare-feu d’applications web est utilisé lors de la couche de hello doit être **WAF**, capacité de hello doit être confirmée lors de la configuration de référence (SKU) hello.

    ```powershell
    $gw | Set-AzureRmApplicationGatewaySku -Name WAF_Large -Tier WAF -Capacity 2
    ```

1. Configurer les paramètres de hello WAF tel que défini dans hello l’exemple suivant :

   Pour **FirewallMode**, les valeurs disponibles hello sont la détection et la prévention.

    ```powershell
    $gw | Set-AzureRmApplicationGatewayWebApplicationFirewallConfiguration -Enabled $true -FirewallMode Prevention
    ```

1. Mettre à jour hello passerelle d’Application avec les paramètres de hello définis dans hello précédant l’étape.

    ```powershell
    Set-AzureRmApplicationGateway -ApplicationGateway $gw
    ```

Cette commande met à jour hello passerelle d’Application avec le pare-feu d’applications web. Visitez [diagnostics de la passerelle d’Application](application-gateway-diagnostics.md) toounderstand comment tooview se connecte pour la passerelle de votre Application. En raison de la nature de sécurité toohello de WAF, journaux besoin toobe révisé régulièrement posture de sécurité hello toounderstand de vos applications web.

## <a name="create-an-application-gateway-with-web-application-firewall"></a>Créer une passerelle Application Gateway avec le pare-feu d’applications web

Hello étapes suivantes vous guident tout processus de hello de tooend de début pour la création d’une passerelle d’Application avec le pare-feu d’applications web.

Assurez-vous que vous utilisez la version la plus récente d’Azure PowerShell hello. Pour plus d’informations, voir [Utilisation de Windows PowerShell avec Azure Resource Manager](../powershell-azure-resource-manager.md).

1. Connectez-vous à tooAzure en exécutant `Login-AzureRmAccount`, vous êtes invité à tooauthenticate avec vos informations d’identification.

1. Vérifier les abonnements hello pour le compte de hello en exécutant`Get-AzureRmSubscription`

1. Choisissez parmi vos toouse abonnements Azure.

    ```powershell
    Select-AzureRmsubscription -SubscriptionName "<Subscription name>"
    ```

### <a name="create-a-resource-group"></a>Créer un groupe de ressources

Créer un groupe de ressources pour hello passerelle d’Application.

```powershell
New-AzureRmResourceGroup -Name appgw-rg -Location "West US"
```

Azure Resource Manager requiert que tous les groupes de ressources spécifient un emplacement. Cet emplacement est utilisé comme emplacement par défaut de hello pour les ressources dans ce groupe de ressources. Assurez-vous que toutes les commandes toocreate une passerelle d’Application utilise hello même groupe de ressources.

Bonjour précédent exemple, nous avons créé un groupe de ressources appelé « Appgw-RG » et l’emplacement « ouest des États-Unis. »

> [!NOTE]
> Si vous devez tooconfigure une sonde personnalisée pour votre passerelle d’Application, consultez [créer une passerelle d’Application en testant personnalisé à l’aide de PowerShell](application-gateway-create-probe-ps.md). Pour plus d’informations, découvrez les [sondes personnalisées et l’analyse du fonctionnement](application-gateway-probe-overview.md) .

### <a name="configure-virtual-network"></a>Configurer un réseau virtuel

Application Gateway nécessite son propre sous-réseau. Dans cette étape, vous créez un réseau virtuel avec un espace d’adressage de 10.0.0.0/16 et deux sous-réseaux, un pour hello passerelle d’Application et l’autre pour les membres du pool principal.

```powershell
# Create a subnet configuration object for hello Application Gateway subnet. A subnet for an application should have a minimum of 28 mask bits. This value leaves 10 available addresses in hello subnet for Application Gateway instances. With a smaller subnet, you may not be able tooadd more instance of your Application Gateway in hello future.
$gwSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name 'appgwsubnet' -AddressPrefix 10.0.0.0/24

# Create a subnet configuration object for hello backend pool members subnet
$nicSubnet = New-AzureRmVirtualNetworkSubnetConfig  -Name 'appsubnet' -AddressPrefix 10.0.2.0/24

# Create hello virtual network with hello previous created subnets
$vnet = New-AzureRmvirtualNetwork -Name 'appgwvnet' -ResourceGroupName appgw-rg -Location "West US" -AddressPrefix 10.0.0.0/16 -Subnet $gwSubnet, $nicSubnet
```

### <a name="configure-public-ip-address"></a>Configurer une adresse IP publique

Dans l’ordre toohandle les demandes externes, passerelle d’Application requiert une adresse IP publique. Cette adresse IP publique ne doit pas avoir un `DomainNameLabel` défini toobe utilisé par hello passerelle d’Application.

```powershell
# Create a public IP address for use with hello Application Gateway. Defining hello domainnamelabel during creation is not supported for use with Application Gateway
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName appgw-rg -name 'appgwpip' -Location "West US" -AllocationMethod Dynamic
```

### <a name="configure-hello-application-gateway"></a>Configurer hello Application Gateway

```powershell
# Create a IP configuration. This configures what subnet hello Application Gateway uses. When Application Gateway starts, it picks up an IP address from hello subnet configured and routes network traffic toohello IP addresses in hello back-end IP pool.
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name 'gwconfig' -Subnet $gwSubnet

# Create a backend pool toohold hello addresses or NICs for hello application that Application Gateway is protecting.
$pool = New-AzureRmApplicationGatewayBackendAddressPool -Name 'pool01' -BackendIPAddresses 1.1.1.1, 2.2.2.2, 3.3.3.3

# Upload hello authenication certificate that will be used toocommunicate with hello backend servers
$authcert = New-AzureRmApplicationGatewayAuthenticationCertificate -Name 'whitelistcert1' -CertificateFile <full path too.cer file>

# Conifugre hello backend HTTP settings toobe used toodefine how traffic is routed toohello backend pool. hello authenication certificate used in hello previous step is added toohello backend http settings.
$poolSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name 'setting01' -Port 443 -Protocol Https -CookieBasedAffinity Enabled -AuthenticationCertificates $authcert

# Create a frontend port toobe used by hello listener.
$fp = New-AzureRmApplicationGatewayFrontendPort -Name 'port01'  -Port 443

# Create a frontend IP configuration tooassociate hello public IP address with hello Application Gateway
$fipconfig = New-AzureRmApplicationGatewayFrontendIPConfig -Name 'fip01' -PublicIPAddress $publicip

# Configure hello certificate for hello Application Gateway. This certificate is used toodecrypt and re-encrypt hello traffic on hello Application Gateway.
$cert = New-AzureRmApplicationGatewaySslCertificate -Name cert01 -CertificateFile <full path too.pfx file> -Password <password for certificate file>

# Create hello HTTP listener for hello Application Gateway. Assign hello front-end ip configuration, port, and ssl certificate toouse.
$listener = New-AzureRmApplicationGatewayHttpListener -Name listener01 -Protocol Https -FrontendIPConfiguration $fipconfig -FrontendPort $fp -SslCertificate $cert

#Create a load balancer routing rule that configures hello load balancer behavior. In this example, a basic round robin rule is created.
$rule = New-AzureRmApplicationGatewayRequestRoutingRule -Name 'rule01' -RuleType basic -BackendHttpSettings $poolSetting -HttpListener $listener -BackendAddressPool $pool

# Configure hello SKU of hello Application Gateway
$sku = New-AzureRmApplicationGatewaySku -Name WAF_Medium -Tier WAF -Capacity 2

# Define hello SSL policy toouse
$policy = New-AzureRmApplicationGatewaySslPolicy -PolicyType Predefined -PolicyName AppGwSslPolicy20170401S

#Configure hello waf configuration settings.
$config = New-AzureRmApplicationGatewayWebApplicationFirewallConfiguration -Enabled $true -FirewallMode "Prevention"

# Create hello Application Gateway utilizing all hello previously created configuration objects
$appgw = New-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg -Location "West US" -BackendAddressPools $pool -BackendHttpSettingsCollection $poolSetting -FrontendIpConfigurations $fipconfig  -GatewayIpConfigurations $gipconfig -FrontendPorts $fp -HttpListeners $listener -RequestRoutingRules $rule -Sku $sku -WebApplicationFirewallConfig $config -SslCertificates $cert -AuthenticationCertificates $authcert
```

> [!NOTE]
> Passerelles d’application créés avec la configuration du pare-feu application hello web de base sont configurés avec CRS 3.0 pour les protections.

## <a name="get-application-gateway-dns-name"></a>Obtenir le nom DNS d’une passerelle Application Gateway

Après la création de la passerelle de hello, hello prochaine étape consiste tooconfigure hello frontal pour la communication. Lorsque vous utilisez une adresse IP publique, la passerelle Application Gateway requiert un nom DNS attribué dynamiquement, ce qui n’est pas convivial. les utilisateurs finaux de tooensure pouvez atteindre hello passerelle d’Application, un enregistrement CNAME peut être le point de terminaison utilisé toopoint toohello public de hello passerelle d’Application. [Configuration d’un nom de domaine personnalisé pour Azure](../cloud-services/cloud-services-custom-domain-name-portal.md). tooconfigure un alias, de récupérer les détails de hello passerelle d’Application et son nom IP/DNS associé à l’aide de hello PublicIPAddress élément attaché toohello passerelle d’Application. nom DNS de la passerelle d’Application Hello doit être utilisé toocreate un enregistrement CNAME, le nom DNS de points hello deux web applications toothis. les utilisation de Hello d’enregistrements d’un n’est pas recommandée étant donné que l’adresse IP virtuelle hello peut changer lors du redémarrage de la passerelle d’Application.

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

Découvrez comment tooconfigure journalisation des diagnostics, événements de hello toolog détectés ou prévenir pare-feu d’applications web en vous rendant sur [Diagnostics de passerelle d’Application](application-gateway-diagnostics.md)

[scenario]: ./media/application-gateway-web-application-firewall-powershell/scenario.png
