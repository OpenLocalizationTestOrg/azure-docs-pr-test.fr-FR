---
title: "aaaConfigure SSL décharger - passerelle d’Application Azure - PowerShell | Documents Microsoft"
description: "Cette page fournit toocreate instructions déchargement d’une passerelle d’application avec SSL à l’aide du Gestionnaire de ressources Azure"
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: 3c3681e0-f928-4682-9d97-567f8e278e13
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/19/2017
ms.author: gwallace
ms.openlocfilehash: c2855d8d3caaa97ec05475c67ff0f8dce72ef2a7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-an-application-gateway-for-ssl-offload-by-using-azure-resource-manager"></a>Configuration d’une passerelle Application Gateway pour le déchargement SSL à l’aide d’Azure Resource Manager

> [!div class="op_single_selector"]
> * [Portail Azure](application-gateway-ssl-portal.md)
> * [Commandes PowerShell pour Azure Resource Manager](application-gateway-ssl-arm.md)
> * [Azure Classic PowerShell](application-gateway-ssl.md)
> * [Azure CLI 2.0](application-gateway-ssl-cli.md)

Passerelle d’Application Azure peut être configuré tooterminate hello Secure Sockets Layer (SSL) session à hello passerelle tooavoid coûteux SSL déchiffrement tâches toohappen au niveau de la batterie de serveurs web hello. Déchargement SSL simplifie également la configuration de serveur frontal de hello et la gestion d’application web de hello.

## <a name="before-you-begin"></a>Avant de commencer

1. Installer version la plus récente des applets de commande PowerShell Azure hello hello à l’aide de hello Web Platform Installer. Vous pouvez télécharger et installer la version la plus récente hello de hello **Windows PowerShell** section Hello [page Téléchargements](https://azure.microsoft.com/downloads/).
2. Vous créez un réseau virtuel et un sous-réseau pour la passerelle d’application hello. Assurez-vous qu’aucun ordinateur virtuel ou les déploiements de cloud ne sont à l’aide de sous-réseau de hello. La passerelle Application Gateway doit être seule sur un sous-réseau virtuel.
3. serveurs Hello vous configurez la passerelle d’application toouse hello doivent exister ou ont créé leurs points de terminaison dans le réseau virtuel de hello ou avec une adresse IP publique/VIP attribué.

## <a name="what-is-required-toocreate-an-application-gateway"></a>Qu’est requis toocreate une passerelle d’application ?

* **Pool de serveur principal :** liste hello des adresses IP des serveurs principaux de hello. adresses IP de Hello répertoriés doivent appartenir soit de sous-réseau de réseau virtuel toohello ou doivent être une adresse IP/VIP publique.
* **Paramètres du pool de serveurs principaux :** chaque pool comporte des paramètres tels que le port, le protocole et une affinité basée sur des cookies. Ces paramètres sont lié tooa pool et sont des serveurs tooall appliqué dans le pool de hello.
* **Port frontal :** ce port est le port public hello qui est ouvert sur la passerelle d’application hello. Le trafic atteint ce port et obtient redirigés tooone de hello sur les serveurs principaux.
* **Écouteur :** hello port d’écoute utilise un port frontal, un protocole (Http ou Https, ces paramètres respectent la casse) et le nom du certificat SSL hello (si le déchargement de la configuration de SSL).
* **La règle :** règle de hello lie le port d’écoute hello et pool de serveur principal hello et définit le trafic de hello de pool de serveur principal doit être dirigée toowhen il atteint un écouteur particulier. Actuellement, seuls hello *base* règle est pris en charge. Hello *base* règle est la distribution de la charge de tourniquet.

**Notes de configuration supplémentaires :**

Pour configurer des certificats SSL, hello protocole dans **HttpListener** doit également modifier*Https* (sensible à la casse). Hello **certificat SSL** l’élément est ajouté trop**HttpListener** avec la valeur de la variable hello configuré pour le certificat SSL de hello. le port frontal Hello doit être too443 mis à jour.

**affinité basé sur cookie de tooenable**: une passerelle d’application peut être configurée tooensure qu’une demande à partir d’une session cliente est toujours dirigée toohello même machine virtuelle dans la batterie de serveurs web hello. Ce scénario est effectué par injection d’un cookie de session qui autorise le trafic toodirect de passerelle de hello de manière appropriée. l’affinité basé sur cookie tooenable, définie **CookieBasedAffinity** trop*activé* Bonjour **paramètres** élément.

## <a name="create-an-application-gateway"></a>Créer une passerelle Application Gateway

Hello différence du modèle de déploiement Azure Classic hello et Gestionnaire de ressources Azure est commande hello que vous créez une application passerelle et hello éléments nécessitant toobe configuré.

Avec le Gestionnaire de ressources, tous les composants d’une passerelle d’application sont configurées individuellement et ensuite placer toocreate ensemble une ressource de passerelle d’application.

Voici une passerelle d’application hello étapes nécessaires toocreate :

1. Créer un groupe de ressources pour Resource Manager
2. Créer le réseau virtuel, sous-réseau et adresse IP publique pour la passerelle d’application hello
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

Créez un groupe de ressources (ignorez cette étape si vous utilisez un groupe de ressources existant).

```powershell
New-AzureRmResourceGroup -Name appgw-rg -Location "West US"
```

Azure Resource Manager requiert que tous les groupes de ressources spécifient un emplacement. Ce paramètre est utilisé comme emplacement par défaut de hello pour les ressources dans ce groupe de ressources. Assurez-vous que toutes les commandes toocreate une passerelle d’application utilise hello même groupe de ressources.

Dans l’exemple hello ci-dessus, nous avons créé un groupe de ressources appelé **appgw-RG** et l’emplacement **ouest des États-Unis**.

## <a name="create-a-virtual-network-and-a-subnet-for-hello-application-gateway"></a>Créer un réseau virtuel et un sous-réseau pour la passerelle d’application hello

Hello suivant montre l’exemple de comment toocreate un réseau virtuel à l’aide du Gestionnaire de ressources :

### <a name="step-1"></a>Étape 1

```powershell
$subnet = New-AzureRmVirtualNetworkSubnetConfig -Name subnet01 -AddressPrefix 10.0.0.0/24
```

Cet exemple assigne hello adresse plage 10.0.0.0/24 tooa sous-réseau toobe variable utilisée toocreate un réseau virtuel.

### <a name="step-2"></a>Étape 2

```powershell
$vnet = New-AzureRmVirtualNetwork -Name appgwvnet -ResourceGroupName appgw-rg -Location "West US" -AddressPrefix 10.0.0.0/16 -Subnet $subnet
```

Cet exemple crée un réseau virtuel nommé **appgwvnet** dans le groupe de ressources **appgw-rg** pour la région ouest des États-Unis hello à l’aide de hello préfixe 10.0.0.0/16 avec le sous-réseau 10.0.0.0/24.

### <a name="step-3"></a>Étape 3 :

```powershell
$subnet = $vnet.Subnets[0]
```

Cet exemple assigne hello sous-réseau objet toovariable $subnet pour les étapes suivantes de hello.

## <a name="create-a-public-ip-address-for-hello-front-end-configuration"></a>Créer une adresse IP publique pour la configuration frontale de hello

```powershell
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName appgw-rg -name publicIP01 -location "West US" -AllocationMethod Dynamic
```

Cet exemple crée une ressource IP publique **publicIP01** dans le groupe de ressources **appgw-rg** pour la région ouest des États-Unis hello.

## <a name="create-an-application-gateway-configuration-object"></a>Créer un objet de configuration de passerelle Application Gateway

### <a name="step-1"></a>Étape 1

```powershell
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name gatewayIP01 -Subnet $subnet
```

Cet exemple crée une configuration IP de passerelle Application Gateway nommée **gatewayIP01**. Au démarrage de la passerelle d’Application, il récupère une adresse IP du sous-réseau hello configuré et acheminer les adresses IP de réseau du trafic toohello dans le pool d’adresses IP hello back-end. Gardez à l’esprit que chaque instance utilise une adresse IP unique.

### <a name="step-2"></a>Étape 2

```powershell
$pool = New-AzureRmApplicationGatewayBackendAddressPool -Name pool01 -BackendIPAddresses 134.170.185.46, 134.170.188.221,134.170.185.50
```

Cet exemple configure le pool d’adresses IP principal hello nommé **pool01** avec des adresses IP **134.170.185.46**, **134.170.188.221**, **134.170.185.50** . Ces valeurs sont des adresses IP hello qui reçoivent le trafic réseau hello qui provient d’un point de terminaison IP frontale hello. Remplacer les adresses IP hello hello précédent exemple avec des adresses IP hello de points de terminaison de votre application web.

### <a name="step-3"></a>Étape 3 :

```powershell
$poolSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name poolsetting01 -Port 80 -Protocol Http -CookieBasedAffinity Enabled
```

Cet exemple configure le paramètre de passerelle d’application **poolsetting01** tooload équilibrée de trafic réseau dans le pool principal d’hello.

### <a name="step-4"></a>Étape 4

```powershell
$fp = New-AzureRmApplicationGatewayFrontendPort -Name frontendport01  -Port 443
```

Cet exemple configure le port IP frontal hello nommé **frontendport01** pour le point de terminaison IP public hello.

### <a name="step-5"></a>Étape 5

```powershell
$cert = New-AzureRmApplicationGatewaySslCertificate -Name cert01 -CertificateFile <full path for certificate file> -Password "<password>"
```

Cet exemple configure un certificat hello utilisée pour la connexion SSL. certificat de Hello doit toobe au format .pfx et hello le mot de passe doit être comprise entre 4 too12 caractères.

### <a name="step-6"></a>Étape 6

```powershell
$fipconfig = New-AzureRmApplicationGatewayFrontendIPConfig -Name fipconfig01 -PublicIPAddress $publicip
```

Cet exemple crée la configuration IP frontale hello nommée **fipconfig01** et associe hello adresse IP publique avec une configuration IP frontale hello.

### <a name="step-7"></a>Étape 7

```powershell
$listener = New-AzureRmApplicationGatewayHttpListener -Name listener01  -Protocol Https -FrontendIPConfiguration $fipconfig -FrontendPort $fp -SslCertificate $cert
```

Cet exemple crée le nom de l’écouteur hello **listener01** et associe hello configuration IP frontale de port frontal toohello et le certificat.

### <a name="step-8"></a>Étape 8

```powershell
$rule = New-AzureRmApplicationGatewayRequestRoutingRule -Name rule01 -RuleType Basic -BackendHttpSettings $poolSetting -HttpListener $listener -BackendAddressPool $pool
```

Cet exemple crée hello règle équilibreur de charge routage nommé **rule01** qui configure le comportement de programme d’équilibrage de charge hello.

### <a name="step-9"></a>Étape 9

```powershell
$sku = New-AzureRmApplicationGatewaySku -Name Standard_Small -Tier Standard -Capacity 2
```

Cet exemple configure la taille de l’instance de la passerelle d’application hello hello.

> [!NOTE]
> Hello la valeur par défaut de *InstanceCount* est 2, avec une valeur maximale de 10. Hello la valeur par défaut de *GatewaySize* est moyenne. Vous pouvez choisir entre Standard_Small, Standard_Medium et Standard_Large.

### <a name="step-10"></a>Étape 10

```powershell
$policy = New-AzureRmApplicationGatewaySslPolicy -PolicyType Predefined -PolicyName AppGwSslPolicy20170401S
```

Cette étape définit toouse de stratégie SSL hello sur la passerelle d’application hello. Visitez [versions de stratégie de configuration de SSL et les suites de chiffrement sur la passerelle d’Application](application-gateway-configure-ssl-policy-powershell.md) toolearn plus.

## <a name="create-an-application-gateway-by-using-new-azureapplicationgateway"></a>Créer une passerelle Application Gateway avec New-AzureApplicationGateway

```powershell
$appgw = New-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg -Location "West US" -BackendAddressPools $pool -BackendHttpSettingsCollection $poolSetting -FrontendIpConfigurations $fipconfig  -GatewayIpConfigurations $gipconfig -FrontendPorts $fp -HttpListeners $listener -RequestRoutingRules $rule -Sku $sku -SslCertificates $cert -SslPolicy $policy
```

Cet exemple crée une passerelle d’application avec tous les éléments de configuration à partir de hello étapes précédentes. Dans l’exemple de hello, la passerelle d’application hello est appelé **appgwtest**.

## <a name="get-application-gateway-dns-name"></a>Obtenir le nom DNS d’une passerelle Application Gateway

Après la création de la passerelle de hello, hello prochaine étape consiste tooconfigure hello frontal pour la communication. Lorsque vous utilisez une adresse IP publique, la passerelle Application Gateway requiert un nom DNS attribué dynamiquement, ce qui n’est pas convivial. les utilisateurs finaux de tooensure pouvez atteindre la passerelle d’application hello, un enregistrement CNAME peut être le point de terminaison utilisé toopoint toohello public de la passerelle d’application hello. [Configuration d’un nom de domaine personnalisé pour Azure](../cloud-services/cloud-services-custom-domain-name-portal.md). toodo, détails de récupération de la passerelle d’application hello et son nom IP/DNS associé à l’aide de la passerelle d’application hello PublicIPAddress élément attaché toohello. nom DNS de la passerelle d’application Hello doit être utilisé toocreate un enregistrement CNAME, le nom DNS de points hello deux web applications toothis. les utilisation de Hello d’enregistrements d’un n’est pas recommandée étant donné que l’adresse IP virtuelle hello peut changer lors du redémarrage de la passerelle d’application.


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

Si vous souhaitez tooconfigure un toouse de passerelle d’application avec un équilibreur de charge interne (ILB), consultez [créer une passerelle d’application avec un équilibreur de charge interne (ILB)](application-gateway-ilb.md).

Si vous souhaitez plus d'informations sur les options d'équilibrage de charge en général, consultez :

* [Équilibrage de charge Azure](https://azure.microsoft.com/documentation/services/load-balancer/)
* [Azure Traffic Manager](https://azure.microsoft.com/documentation/services/traffic-manager/)

