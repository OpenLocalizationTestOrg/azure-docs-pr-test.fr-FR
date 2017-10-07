---
title: "aaaCreate et gérer une passerelle d’Application Azure - PowerShell | Documents Microsoft"
description: "Cette page fournit des instructions toocreate, configurer, démarrer et supprimer une passerelle d’application Windows Azure à l’aide du Gestionnaire de ressources Azure"
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.service: application-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/31/2017
ms.author: gwallace
ms.openlocfilehash: ab98d5f9aa0dc309f8353b7f72591359e1121849
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-start-or-delete-an-application-gateway-by-using-azure-resource-manager"></a>Créer, démarrer ou supprimer une passerelle Application Gateway à l’aide d’Azure Resource Manager

> [!div class="op_single_selector"]
> * [portail Azure](application-gateway-create-gateway-portal.md)
> * [Commandes PowerShell pour Azure Resource Manager](application-gateway-create-gateway-arm.md)
> * [Azure Classic PowerShell](application-gateway-create-gateway.md)
> * [Modèle Azure Resource Manager](application-gateway-create-gateway-arm-template.md)
> * [Interface de ligne de commande Azure](application-gateway-create-gateway-cli.md)

La passerelle Azure Application Gateway est un équilibreur de charge de couche 7. Il fournit de basculement et le routage des performances des requêtes HTTP entre différents serveurs, qu’ils soient sur le cloud de hello ou localement. Application Gateway offre de nombreuses fonctionnalités de contrôleur de livraison d’applications (ADC) : équilibrage de charge HTTP, affinité de session basée sur les cookies, déchargement SSL (Secure Sockets Layer), sondes d’intégrité personnalisées, prise en charge de plusieurs sites, etc. toofind une liste complète des fonctionnalités prises en charge, visitez [vue d’ensemble de la passerelle d’Application](application-gateway-introduction.md).

Cet article vous guide tout au long des hello étapes toocreate, configurer, démarrer et supprimer une passerelle d’application.

> [!IMPORTANT]
> Avant d’utiliser des ressources Azure, il est important toounderstand que Azure dispose actuellement de deux modèles de déploiement : le Gestionnaire de ressources et classique. Attention à bien comprendre les [modèles et outils de déploiement](../azure-classic-rm.md) avant d’utiliser une ressource Azure. Vous pouvez afficher la documentation hello pour différents outils en cliquant sur les onglets hello haut hello de cet article. Ce document traite de la création d’une passerelle Application Gateway à l’aide d’Azure Resource Manager. version classique de toouse hello, accédez trop[créer un déploiement classique passerelle d’application à l’aide de PowerShell](application-gateway-create-gateway.md).

## <a name="before-you-begin"></a>Avant de commencer

1. Installer version la plus récente des applets de commande PowerShell Azure hello hello à l’aide de hello Web Platform Installer. Vous pouvez télécharger et installer la version la plus récente hello de hello **Windows PowerShell** section Hello [page Téléchargements](https://azure.microsoft.com/downloads/).
1. Si vous avez un réseau virtuel existant, sélectionnez un sous-réseau vide existant ou créer un sous-réseau dans votre réseau virtuel existant uniquement pour une utilisation par la passerelle d’application hello. Vous ne pouvez pas déployer hello application passerelle tooa autre réseau virtuel que les ressources hello vous avez l’intention toodeploy derrière la passerelle d’application hello.
1. serveurs Hello configurer la passerelle d’application hello toouse doivent exister ou aient leurs points de terminaison créés dans le réseau virtuel de hello ou avec une adresse IP publique/VIP affectés.

## <a name="what-is-required-toocreate-an-application-gateway"></a>Qu’est requis toocreate une passerelle d’application ?

* **Pool de serveurs principaux :** liste hello d’adresses IP, des noms de domaine complets ou des cartes réseau des serveurs principaux de hello. Si les adresses IP sont utilisées, elles doivent appartenir soit de sous-réseau de réseau virtuel toohello ou doivent être une adresse IP/VIP publique.
* **Paramètres du pool de serveurs principaux** : chaque pool comporte des paramètres comme le port, le protocole et une affinité basée sur les cookies. Ces paramètres sont lié tooa pool et sont des serveurs tooall appliqué dans le pool de hello.
* **port frontal :** ce port est le port public hello qui est ouvert sur la passerelle d’application hello. Le trafic atteint ce port et obtient ensuite redirigé tooone des serveurs principaux de hello.
* **Écouteur :** écouteur de hello possède un port de serveur frontal, un protocole (Http ou Https, ces valeurs respectent la casse) et le nom du certificat SSL hello (si le déchargement de la configuration de SSL).
* **La règle :** règle de hello lie écouteur hello, pool de serveurs principaux hello et définit le principal serveur pool hello le trafic doit être dirigée toowhen il atteint un écouteur particulier.

## <a name="create-a-resource-group-for-resource-manager"></a>Créer un groupe de ressources pour Resource Manager

Assurez-vous que vous utilisez la version la plus récente d’Azure PowerShell hello. Pour plus d’informations, voir [Utilisation de Windows PowerShell avec Azure Resource Manager](../powershell-azure-resource-manager.md).

1. Connectez-vous à tooAzure et entrez vos informations d’identification.

  ```powershell
  Login-AzureRmAccount
  ```

2. Vérifiez les abonnements hello pour le compte de hello.

  ```powershell
  Get-AzureRmSubscription
  ```

3. Choisissez parmi vos toouse abonnements Azure.

  ```powershell
  Select-AzureRmSubscription -Subscriptionid "GUID of subscription"
  ```

4. Créez un groupe de ressources (ignorez cette étape si vous utilisez un groupe de ressources existant).

  ```powershell
  New-AzureRmResourceGroup -Name ContosoRG -Location "West US"
  ```

Azure Resource Manager requiert que tous les groupes de ressources spécifient un emplacement. Cet emplacement est utilisé comme emplacement par défaut de hello pour les ressources dans ce groupe de ressources. Assurez-vous que toutes les commandes toocreate une passerelle d’application utilise hello même groupe de ressources.

Dans l’exemple hello ci-dessus, nous avons créé un groupe de ressources appelé **ContosoRG** et l’emplacement **États-Unis**.

> [!NOTE]
> Si vous avez besoin de tooconfigure une sonde personnalisée pour votre passerelle d’application, visitez : [créer une passerelle d’application en testant personnalisé à l’aide de PowerShell](application-gateway-create-probe-ps.md). Pour plus d’informations, découvrez les [sondes personnalisées et l’analyse du fonctionnement](application-gateway-probe-overview.md) .


## <a name="create-hello-application-gateway-configuration-objects"></a>Créer des objets de configuration de passerelle d’application hello

Tous les éléments de configuration doivent être configurés avant de créer la passerelle d’application hello. Hello étapes suivantes créent hello des éléments de configuration qui sont nécessaires pour une ressource de passerelle d’application.

```powershell
# Create a subnet and assign hello address space of 10.0.0.0/24
$subnet = New-AzureRmVirtualNetworkSubnetConfig -Name subnet01 -AddressPrefix 10.0.0.0/24

# Create a virtual network with hello address space of 10.0.0.0/16 and add hello subnet
$vnet = New-AzureRmVirtualNetwork -Name ContosoVNET -ResourceGroupName ContosoRG -Location "East US" -AddressPrefix 10.0.0.0/16 -Subnet $subnet

# Retrieve hello newly created subnet
$subnet=$vnet.Subnets[0]

# Create a public IP address that is used tooconnect toohello application gateway. Application Gateway does not support custom DNS names on public IP addresses.  If a custom name is required for hello public endpoint, a CNAME record should be created toopoint toohello automatically generated DNS name for hello public IP address.
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName ContosoRG -name publicIP01 -location "East US" -AllocationMethod Dynamic

# Create a gateway IP configuration. hello gateway picks up an IP addressfrom hello configured subnet and routes network traffic toohello IP addresses in hello backend IP pool. Keep in mind that each instance takes one IP address.
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name gatewayIP01 -Subnet $subnet

# Configure a backend pool with hello addresses of your web servers. These backend pool members are all validated toobe healthy by probes, whether they are basic probes or custom probes.  Traffic is then routed toothem when requests come into hello application gateway. Backend pools can be used by multiple rules within hello application gateway, which means one backend pool could be used for multiple web applications that reside on hello same host.
$pool = New-AzureRmApplicationGatewayBackendAddressPool -Name pool01 -BackendIPAddresses 134.170.185.46, 134.170.188.221, 134.170.185.50

# Configure backend http settings toodetermine hello protocol and port that is used when sending traffic toohello backend servers. Cookie-based sessions are also determined by hello backend HTTP settings.  If enabled, cookie-based session affinity sends traffic toohello same backend as previous requests for each packet.
$poolSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name "besetting01" -Port 80 -Protocol Http -CookieBasedAffinity Disabled -RequestTimeout 120

# Configure a frontend port that is used tooconnect toohello application gateway through hello public IP address
$fp = New-AzureRmApplicationGatewayFrontendPort -Name frontendport01  -Port 80

# Configure hello frontend IP configuration with hello public IP address created earlier.
$fipconfig = New-AzureRmApplicationGatewayFrontendIPConfig -Name fipconfig01 -PublicIPAddress $publicip

# Configure hello listener.  hello listener is a combination of hello front end IP configuration, protocol, and port and is used tooreceive incoming network traffic. 
$listener = New-AzureRmApplicationGatewayHttpListener -Name listener01 -Protocol Http -FrontendIPConfiguration $fipconfig -FrontendPort $fp

# Configure a basic rule that is used tooroute traffic toohello backend servers. hello backend pool settings, listener, and backend pool created in hello previous steps make up hello rule. Based on hello criteria defined traffic is routed toohello appropriate backend.
$rule = New-AzureRmApplicationGatewayRequestRoutingRule -Name rule01 -RuleType Basic -BackendHttpSettings $poolSetting -HttpListener $listener -BackendAddressPool $pool

# Configure hello SKU for hello application gateway, this determines hello size and whether or not WAF is used.
$sku = New-AzureRmApplicationGatewaySku -Name Standard_Small -Tier Standard -Capacity 2

# Create hello application gateway
$appgw = New-AzureRmApplicationGateway -Name ContosoAppGateway -ResourceGroupName ContosoRG -Location "East US" -BackendAddressPools $pool -BackendHttpSettingsCollection $poolSetting -FrontendIpConfigurations $fipconfig  -GatewayIpConfigurations $gipconfig -FrontendPorts $fp -HttpListeners $listener -RequestRoutingRules $rule -Sku $sku
```

Lorsque vous avez terminé, récupérer les détails DNS et adresse IP virtuelle de passerelle d’application hello à partir de la passerelle d’application hello publique IP ressource toohello attaché.

```powershell
Get-AzureRmPublicIpAddress -Name publicIP01 -ResourceGroupName ContosoRG
```

## <a name="delete-hello-application-gateway"></a>Suppression de la passerelle d’application hello

Hello exemple suivant supprime passerelle d’application hello.

```powershell
# Retrieve hello application gateway
$gw = Get-AzureRmApplicationGateway -Name ContosoAppGateway -ResourceGroupName ContosoRG

# Stops hello application gateway
Stop-AzureRmApplicationGateway -ApplicationGateway $gw

# Once hello application gateway is in a stopped state, use hello `Remove-AzureRmApplicationGateway` cmdlet tooremove hello service.
Remove-AzureRmApplicationGateway -Name ContosoAppGateway -ResourceGroupName ContosoRG -Force
```

> [!NOTE]
> Hello **-force** commutateur peut être le message de confirmation de suppression de hello toosuppress utilisé.

tooverify qui hello service a été supprimé, vous pouvez utiliser hello `Get-AzureRmApplicationGateway` applet de commande. Cette étape n'est pas requise.

```powershell
Get-AzureRmApplicationGateway -Name ContosoAppGateway -ResourceGroupName ContosoRG
```

## <a name="get-application-gateway-dns-name"></a>Obtenir le nom DNS d’une passerelle Application Gateway

Après la création de la passerelle de hello, hello prochaine étape consiste tooconfigure hello frontal pour la communication. Lorsque vous utilisez une adresse IP publique, la passerelle Application Gateway requiert un nom DNS attribué dynamiquement, ce qui n’est pas convivial. les utilisateurs finaux de tooensure pouvez atteindre la passerelle d’application hello, un enregistrement CNAME peut être le point de terminaison utilisé toopoint toohello public de la passerelle d’application hello. toodo, détails de récupération de la passerelle d’application hello et son nom IP/DNS associé à l’aide de la passerelle d’application hello PublicIPAddress élément attaché toohello. Cela est possible avec Azure DNS ou d’autres fournisseurs DNS, en créant un enregistrement CNAME qui pointe toohello [adresse IP publique](../dns/dns-custom-domain.md#public-ip-address). les utilisation de Hello d’enregistrements d’un n’est pas recommandée étant donné que l’adresse IP virtuelle hello peut changer lors du redémarrage de la passerelle d’application.

> [!NOTE]
> Une adresse IP est attribuée toohello passerelle d’application au démarrage du service de hello.

```powershell
Get-AzureRmPublicIpAddress -ResourceGroupName ContosoRG -Name publicIP01
```

```
Name                     : publicIP01
ResourceGroupName        : ContosoRG
Location                 : westus
Id                       : /subscriptions/<subscription_id>/resourceGroups/ContosoRG/providers/Microsoft.Network/publicIPAddresses/publicIP01
Etag                     : W/"00000d5b-54ed-4907-bae8-99bd5766d0e5"
ResourceGuid             : 00000000-0000-0000-0000-000000000000
ProvisioningState        : Succeeded
Tags                     : 
PublicIpAllocationMethod : Dynamic
IpAddress                : xx.xx.xxx.xx
PublicIpAddressVersion   : IPv4
IdleTimeoutInMinutes     : 4
IpConfiguration          : {
                                "Id": "/subscriptions/<subscription_id>/resourceGroups/ContosoRG/providers/Microsoft.Network/applicationGateways/ContosoAppGateway/frontendIP
                            Configurations/frontend1"
                            }
DnsSettings              : {
                                "Fqdn": "00000000-0000-xxxx-xxxx-xxxxxxxxxxxx.cloudapp.net"
                            }
```

## <a name="delete-all-resources"></a>Supprimer toutes les ressources

toodelete toutes les ressources créées dans cet article, hello complet suivant l’étape :

```powershell
Remove-AzureRmResourceGroup -Name ContosoRG
```

## <a name="next-steps"></a>Étapes suivantes

Si vous souhaitez tooconfigure le déchargement SSL, visitez : [configurer une passerelle d’application pour le déchargement SSL](application-gateway-ssl.md).

Si vous voulez tooconfigure un toouse de passerelle d’application avec un équilibrage de charge interne, visitez : [créer une passerelle d’application avec un équilibreur de charge interne (ILB)](application-gateway-ilb.md).

Si vous souhaitez plus d’informations sur les options d’équilibrage de charge en général, visitez :

* [Équilibrage de charge Azure](https://azure.microsoft.com/documentation/services/load-balancer/)
* [Azure Traffic Manager](https://azure.microsoft.com/documentation/services/traffic-manager/)
