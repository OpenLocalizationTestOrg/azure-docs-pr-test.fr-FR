---
title: "aaaUsing passerelle d’Application Azure avec l’équilibrage de charge interne - PowerShell | Documents Microsoft"
description: "Cette page fournit des instructions toocreate, configurer, démarrer et supprimer une passerelle d’application Windows Azure avec équilibrage de charge interne (ILB) pour le Gestionnaire de ressources Azure"
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: 75cfd5a2-e378-4365-99ee-a2b2abda2e0d
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: gwallace
ms.openlocfilehash: dd0d7e954b1fa219ae6ebe42cb4b479dbcf08653
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-application-gateway-with-an-internal-load-balancer-ilb-by-using-azure-resource-manager"></a>Créer une passerelle Application Gateway avec un équilibrage de charge interne (ILB) à l’aide d’Azure Resource Manager

> [!div class="op_single_selector"]
> * [Azure Classic PowerShell](application-gateway-ilb.md)
> * [Commandes PowerShell pour Azure Resource Manager](application-gateway-ilb-arm.md)

Passerelle d’Application Azure peut être configuré avec une adresse IP virtuelle sur Internet ou avec un point de terminaison interne qui n’est pas exposé toohello Internet, également appelée charge interne (ILB) d’équilibrage point de terminaison. Configuration de passerelle hello avec un équilibrage de charge interne est utile pour les applications de métier internes qui ne sont pas exposé toohello Internet. Il est également utile pour les services et niveaux au sein d’une application multicouche qui se trouvent dans une limite de sécurité qui n’est pas exposé toohello Internet mais nécessitent toujours alternée chargement distribution, caractère collant de session ou l’arrêt de Secure Sockets Layer (SSL).

Cet article vous guide tout au long des étapes de hello tooconfigure une passerelle d’application avec un équilibrage de charge interne.

## <a name="before-you-begin"></a>Avant de commencer

1. Installer version la plus récente des applets de commande PowerShell Azure hello hello à l’aide de hello Web Platform Installer. Vous pouvez télécharger et installer la version la plus récente hello de hello **Windows PowerShell** section Hello [page Téléchargements](https://azure.microsoft.com/downloads/).
2. Vous créez un réseau virtuel et un sous-réseau pour la passerelle Application Gateway. Assurez-vous qu’aucun ordinateur virtuel ou les déploiements de cloud ne sont à l’aide de sous-réseau de hello. La passerelle Application Gateway doit être seule sur un sous-réseau virtuel.
3. serveurs Hello configurer la passerelle d’application hello toouse doivent exister ou aient leurs points de terminaison créés dans le réseau virtuel de hello ou avec une adresse IP publique/VIP affectés.

## <a name="what-is-required-toocreate-an-application-gateway"></a>Qu’est requis toocreate une passerelle d’application ?

* **Pool de serveur principal :** liste hello des adresses IP des serveurs principaux de hello. Hello adresses IP répertoriées doivent soit appartenir toohello des réseaux virtuels, mais dans un autre sous-réseau pour la passerelle d’application hello ou doit être une adresse IP/VIP publique.
* **Paramètres du pool de serveurs principaux :** chaque pool comporte des paramètres tels que le port, le protocole et une affinité basée sur des cookies. Ces paramètres sont lié tooa pool et sont des serveurs tooall appliqué dans le pool de hello.
* **Port frontal :** ce port est le port public hello qui est ouvert sur la passerelle d’application hello. Le trafic atteint ce port et obtient redirigés tooone de hello sur les serveurs principaux.
* **Écouteur :** hello port d’écoute utilise un port frontal, un protocole (Http ou Https, ils respectent la casse) et le nom du certificat SSL hello (si le déchargement de la configuration de SSL).
* **La règle :** règle de hello lie le port d’écoute hello et pool de serveur principal hello et définit le trafic de hello de pool de serveur principal doit être dirigée toowhen il atteint un écouteur particulier. Actuellement, seuls hello *base* règle est pris en charge. Hello *base* règle est la distribution de la charge de tourniquet.

## <a name="create-an-application-gateway"></a>Créer une passerelle Application Gateway

Hello diffère entre l’utilisation classique Azure et Azure Resource Manager commande hello dans lequel vous créez passerelle d’application hello et articles hello toobe configuré.
Avec le Gestionnaire de ressources, tous les éléments qui rendent une passerelle d’application est configuré individuellement et rassembler puis toocreate ressource de passerelle d’application hello.

Voici les étapes hello qui sont nécessaire toocreate une passerelle d’application :

1. Créer un groupe de ressources pour Resource Manager
2. Créer un réseau virtuel et un sous-réseau pour la passerelle d’application hello
3. Créer un objet de configuration de passerelle Application Gateway
4. Créer une ressource de passerelle d’application

## <a name="create-a-resource-group-for-resource-manager"></a>Créer un groupe de ressources pour Resource Manager

Assurez-vous que vous basculez des applets de commande PowerShell en mode toouse hello Azure Resource Manager. Pour plus d’informations, voir [Utilisation de Windows PowerShell avec Azure Resource Manager](../powershell-azure-resource-manager.md).

### <a name="step-1"></a>Étape 1

```powershell
Login-AzureRmAccount
```

### <a name="step-2"></a>Étape 2

Vérifiez les abonnements hello pour le compte de hello.

```powershell
Get-AzureRmSubscription
```

Vous êtes invité à tooauthenticate avec vos informations d’identification.

### <a name="step-3"></a>Étape 3 :

Choisissez parmi vos toouse abonnements Azure.

```powershell
Select-AzureRmSubscription -Subscriptionid "GUID of subscription"
```

### <a name="step-4"></a>Étape 4

Créez un groupe de ressources (ignorez cette étape si vous utilisez un groupe de ressources existant)

```powershell
New-AzureRmResourceGroup -Name appgw-rg -location "West US"
```

Azure Resource Manager requiert que tous les groupes de ressources spécifient un emplacement. Cela est utilisé comme emplacement par défaut de hello pour les ressources dans ce groupe de ressources. Assurez-vous que toutes les commandes toocreate une passerelle d’application utilise hello même groupe de ressources.

Bonjour précédent exemple, nous avons créé un groupe de ressources appelé « Appgw-rg » et l’emplacement « ouest des États-Unis ».

## <a name="create-a-virtual-network-and-a-subnet-for-hello-application-gateway"></a>Créer un réseau virtuel et un sous-réseau pour la passerelle d’application hello

Hello suivant montre l’exemple de comment toocreate un réseau virtuel à l’aide du Gestionnaire de ressources :

### <a name="step-1"></a>Étape 1

```powershell
$subnetconfig = New-AzureRmVirtualNetworkSubnetConfig -Name subnet01 -AddressPrefix 10.0.0.0/24
```

Cette étape affecte hello adresse plage 10.0.0.0/24 tooa sous-réseau toobe variable utilisée toocreate un réseau virtuel.

### <a name="step-2"></a>Étape 2

```powershell
$vnet = New-AzureRmVirtualNetwork -Name appgwvnet -ResourceGroupName appgw-rg -Location "West US" -AddressPrefix 10.0.0.0/16 -Subnet $subnetconfig
```

Cette étape crée un réseau virtuel nommé « appgwvnet » dans la ressource groupe « appgw-rg » pour la région ouest des États-Unis hello à l’aide de hello préfixe 10.0.0.0/16 avec le sous-réseau 10.0.0.0/24.

### <a name="step-3"></a>Étape 3 :

```powershell
$subnet = $vnet.subnets[0]
```

Cette étape affecte hello sous-réseau objet toovariable $subnet pour les étapes suivantes de hello.

## <a name="create-an-application-gateway-configuration-object"></a>Créer un objet de configuration de passerelle Application Gateway

### <a name="step-1"></a>Étape 1

```powershell
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name gatewayIP01 -Subnet $subnet
```

Crée une configuration IP de passerelle Application Gateway nommée « gatewayIP01 ». Au démarrage de la passerelle d’Application, il récupère une adresse IP du sous-réseau hello configuré et acheminer les adresses IP de réseau du trafic toohello dans le pool d’adresses IP hello back-end. Gardez à l’esprit que chaque instance utilise une adresse IP unique.

### <a name="step-2"></a>Étape 2

```powershell
$pool = New-AzureRmApplicationGatewayBackendAddressPool -Name pool01 -BackendIPAddresses 10.1.1.8,10.1.1.9,10.1.1.10
```

Cette étape configure le pool d’adresses IP principal hello nommé « pool01 » avec adresse IP adresses « 10.1.1.8, 10.1.1.9, 10.1.1.10 ». Ce sont les adresses IP hello qui reçoivent le trafic réseau hello qui provient d’un point de terminaison IP frontale hello. Vous remplacez hello précédant tooadd d’adresses IP de vos propres points de terminaison application IP adresse.

### <a name="step-3"></a>Étape 3 :

```powershell
$poolSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name poolsetting01 -Port 80 -Protocol Http -CookieBasedAffinity Disabled
```

Cette étape configure le trafic réseau de passerelle paramètre « poolsetting01 » pour la charge hello équilibrés application dans le pool principal d’hello.

### <a name="step-4"></a>Étape 4

```powershell
$fp = New-AzureRmApplicationGatewayFrontendPort -Name frontendport01  -Port 80
```

Cette étape configure le port IP frontal hello nommé « frontendport01 » pour hello équilibrage de charge interne.

### <a name="step-5"></a>Étape 5

```powershell
$fipconfig = New-AzureRmApplicationGatewayFrontendIPConfig -Name fipconfig01 -Subnet $subnet
```

Cette étape crée la configuration IP frontale hello appelée « fipconfig01 » et l’associe à une adresse IP privée à partir du sous-réseau de réseau virtuel en cours hello.

### <a name="step-6"></a>Étape 6

```powershell
$listener = New-AzureRmApplicationGatewayHttpListener -Name listener01  -Protocol Http -FrontendIPConfiguration $fipconfig -FrontendPort $fp
```

Cette étape crée écouteur hello appelé « listener01 » et associe la configuration IP frontale de hello port frontal toohello.

### <a name="step-7"></a>Étape 7

```powershell
$rule = New-AzureRmApplicationGatewayRequestRoutingRule -Name rule01 -RuleType Basic -BackendHttpSettings $poolSetting -HttpListener $listener -BackendAddressPool $pool
```

Cette étape crée hello règle équilibreur de charge routage appelé « rule01 » qui configure le comportement de programme d’équilibrage de charge hello.

### <a name="step-8"></a>Étape 8

```powershell
$sku = New-AzureRmApplicationGatewaySku -Name Standard_Small -Tier Standard -Capacity 2
```

Cette étape configure la taille de l’instance de la passerelle d’application hello hello.

> [!NOTE]
> Hello la valeur par défaut de *InstanceCount* est 2, avec une valeur maximale de 10. Hello la valeur par défaut de *GatewaySize* est moyenne. Vous pouvez choisir entre Standard_Small, Standard_Medium et Standard_Large.

## <a name="create-an-application-gateway-by-using-new-azureapplicationgateway"></a>Créer une passerelle Application Gateway avec New-AzureApplicationGateway

Crée une passerelle d’application avec tous les éléments de configuration à partir de hello étapes précédentes. Dans cet exemple, passerelle d’application hello est appelé « appgwtest ».

```powershell
$appgw = New-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg -Location "West US" -BackendAddressPools $pool -BackendHttpSettingsCollection $poolSetting -FrontendIpConfigurations $fipconfig  -GatewayIpConfigurations $gipconfig -FrontendPorts $fp -HttpListeners $listener -RequestRoutingRules $rule -Sku $sku
```

Cette étape crée une passerelle d’application avec tous les éléments de configuration à partir de hello étapes précédentes. Dans l’exemple de hello, passerelle d’application hello est appelé « appgwtest ».

## <a name="delete-an-application-gateway"></a>Supprimer une passerelle Application Gateway

toodelete une passerelle d’application, vous devez hello toodo comme suit dans l’ordre :

1. Hello d’utilisation `Stop-AzureRmApplicationGateway` passerelle de hello toostop applet de commande.
2. Hello d’utilisation `Remove-AzureRmApplicationGateway` passerelle de hello tooremove applet de commande.
3. Vérifiez cette passerelle hello a été supprimée à l’aide de hello `Get-AzureApplicationGateway` applet de commande.

### <a name="step-1"></a>Étape 1

Obtenir l’objet de passerelle d’application hello et associez-le tooa variable « $getgw ».

```powershell
$getgw =  Get-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg
```

### <a name="step-2"></a>Étape 2

Utilisez `Stop-AzureRmApplicationGateway` passerelle d’application toostop hello. Cet exemple montre hello `Stop-AzureRmApplicationGateway` applet de commande sur la première ligne de hello, suivie des hello.

```powershell
Stop-AzureRmApplicationGateway -ApplicationGateway $getgw  
```

```
VERBOSE: 9:49:34 PM - Begin Operation: Stop-AzureApplicationGateway
VERBOSE: 10:10:06 PM - Completed Operation: Stop-AzureApplicationGateway
Name       HTTP Status Code     Operation ID                             Error
----       ----------------     ------------                             ----
Successful OK                   ce6c6c95-77b4-2118-9d65-e29defadffb8
```

Une fois que la passerelle d’application hello est dans un état arrêté, utilisez hello `Remove-AzureRmApplicationGateway` service de hello tooremove applet de commande.

```powershell
Remove-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg -Force
```

```
VERBOSE: 10:49:34 PM - Begin Operation: Remove-AzureApplicationGateway
VERBOSE: 10:50:36 PM - Completed Operation: Remove-AzureApplicationGateway
Name       HTTP Status Code     Operation ID                             Error
----       ----------------     ------------                             ----
Successful OK                   055f3a96-8681-2094-a304-8d9a11ad8301
```

> [!NOTE]
> Hello **-force** commutateur peut être le message de confirmation de suppression de hello toosuppress utilisé.

tooverify qui hello service a été supprimé, vous pouvez utiliser hello `Get-AzureRmApplicationGateway` applet de commande. Cette étape n'est pas requise.

```powershell
Get-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg
```

```
VERBOSE: 10:52:46 PM - Begin Operation: Get-AzureApplicationGateway

Get-AzureApplicationGateway : ResourceNotFound: hello gateway does not exist.
```

## <a name="next-steps"></a>Étapes suivantes

Si vous souhaitez tooconfigure le déchargement SSL, consultez [configurer une passerelle d’application pour le déchargement SSL](application-gateway-ssl.md).

Si vous souhaitez tooconfigure un toouse de passerelle d’application avec un équilibrage de charge interne, consultez [créer une passerelle d’application avec un équilibreur de charge interne (ILB)](application-gateway-ilb.md).

Si vous souhaitez plus d'informations sur les options d'équilibrage de charge en général, consultez :

* [Équilibrage de charge Azure](https://azure.microsoft.com/documentation/services/load-balancer/)
* [Azure Traffic Manager](https://azure.microsoft.com/documentation/services/traffic-manager/)

